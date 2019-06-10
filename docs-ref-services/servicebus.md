---
title: Bibliotecas de Service Bus para Python
description: Documentación de referencia del cliente de Python y las bibliotecas de administración de Service
keywords: Azure, Python, SDK, API, mensajería, pubsub, pub-sub, agente de mensajes
author: annatisch
ms.author: antisch
manager: mayurid
ms.date: 01/15/2019
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 014f34b6ba3d3a2a8ce15afcd826195d6051f98a
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376767"
---
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Service Bus para Python

Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera.

* [Código fuente del SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Documentación de referencia del SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a>Novedades de la versión 0.50.0

A partir de la versión 0.50.0, hay una nueva API basada en AMQP disponible para enviar y recibir mensajes. Esta actualización implica **cambios importantes**.

Lea el documento de [migración de v0.21.1 a v0.50.0](#migration-from-v0211-to-v0500) para determinar si debe actualizar en este momento.

La nueva API basada en AMQP ofrece confiabilidad, rendimiento, compatibilidad y más características para el envío de mensajes.
También ofrece compatibilidad para las operaciones asincrónicas (basadas en asyncio) para enviar, recibir y controlar los mensajes.

Para ver la documentación sobre las operaciones basadas en HTTP heredadas, consulte [Uso de las operaciones basadas en HTTP de la API heredada](#using-http-based-operations-of-the-legacy-api).

## <a name="prerequisites"></a>Requisitos previos

* Una suscripción de Azure (cree una [cuenta gratuita](https://azure.microsoft.com/free/)).
* Un [espacio de nombres de Service Bus y credenciales de administración](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal) de Azure.
* [Python 2.7-3.7](https://www.python.org/downloads/)

## <a name="installation"></a>Instalación

```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a>Conexión a Azure Service Bus

### <a name="get-credentials"></a>Obtener credenciales

Use el siguiente fragmento de la CLI de Azure para rellenar una variable de entorno con la cadena de conexión de Service Bus (también puede encontrar este valor en Azure Portal). El fragmento de código tiene el formato para el shell de Bash.

```Bash
RES_GROUP=<resource-group-name>
NAMESPACE=<servicebus-namespace>

export SB_CONN_STR=$(az servicebus namespace authorization-rule keys list \
 --resource-group $RES_GROUP \
 --namespace-name $NAMESPACE \
 --name RootManageSharedAccessKey \
 --query primaryConnectionString \
 --output tsv)
```

### <a name="create-client"></a>Crear el cliente

Una vez que ha rellenado la variable de entorno `SB_CONN_STR`, puede crear el cliente de Service Bus.

```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

Si desea usar operaciones asincrónicas, use el espacio de nombres `azure.servicebus.aio`.

```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

## <a name="service-bus-queues"></a>Colas de Service Bus

Las colas de Service Bus son una alternativa a las colas de Storage que podrían ser útiles en escenarios en los que se necesitan características de mensajería más avanzadas (tamaños de mensaje más grandes, orden de los mensajes, lecturas destructivas de una sola operación o entrega programada) con entrega de inserción (mediante sondeo largo).

### <a name="create-queue"></a>Crear cola

Se crea una nueva cola en el espacio de nombres de Service Bus. Si ya existe una cola con el mismo nombre en el espacio de nombres, se producirá un error.

```python
sb_client.create_queue("MyQueue")
```

También se pueden especificar parámetros opcionales para configurar el comportamiento de la cola.

```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a>Obtener un cliente de cola

Se puede usar QueueClient para enviar y recibir mensajes de la cola, además de otras operaciones.

```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a>Envío de mensajes

El cliente de cola puede enviar uno o varios mensajes a la vez:

```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```

Cada llamada a QueueClient.send creará una nueva conexión de servicio. Para reutilizar la misma conexión para varias llamadas de envío, puede abrir un remitente:

```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```

Si usa a un cliente asincrónico, las operaciones anteriores usará la sintaxis de async:

```python
from azure.servicebus.aio import Message

message = Message("Hello World")
await queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
async with queue_client.get_sender() as sender:
    await sender.send(message_one)
    await sender.send(message_two)
```

### <a name="receiving-messages"></a>Recepción de mensajes

Los mensajes se pueden recibir de una cola como un iterador continuo. El modo predeterminado para la recepción del mensaje es [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), que requiere que cada mensaje se complete explícitamente para poder quitarlo de la cola.

```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```

La conexión de servicio permanecerá abierta durante todo el iterador. Si detecta que la iteración por la secuencia de mensajes se realiza solo parcialmente, debe ejecutar el receptor una instrucción `with` para asegurarse de que la conexión se cierra:

```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
Si usa a un cliente asincrónico, las operaciones anteriores usará la sintaxis de async:

```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a>Temas y suscripciones de Service Bus

Los temas y las suscripciones de Service Bus son una abstracción que se sitúan encima de las colas de Service Bus y que proporcionan una o varias formas de comunicación según un modelo publicación/suscripción. Los mensajes se envían a un tema y entregan a una o varias suscripciones asociadas, lo que resulta útil para escalar a un gran número de destinatarios.

### <a name="create-topic"></a>Crear tema

Se crea un nuevo tema en el espacio de nombres de Service Bus. Si ya existe un tema con el mismo nombre, se producirá un error.

```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a>Obtener un cliente de tema

Se puede usar TopicClient para enviar mensajes al tema, además de otras operaciones.

```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a>Creación de una suscripción

Se crea una nueva suscripción para el tema especificado dentro del espacio de nombres de Service Bus.

```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a>Obtener un cliente de suscripción

Se puede usar SubscriptionClient para recibir mensajes del tema, además de otras operaciones.

```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a>Migración de v0.21.1 a v0.50.0

Se introdujeron cambios importantes en la versión 0.50.0. La API basada en HTTP original sigue estando disponible en la versión 0.50.0; sin embargo, ahora existe en un espacio de nombres nuevo: `azure.servicebus.control_client`.

### <a name="should-i-upgrade"></a>¿Debería actualizar?

El nuevo paquete (v0.50.0) no ofrece mejoras en las operaciones basadas en HTTP respecto a v0.21.1. La API basada en HTTP es idéntica, salvo que ahora existe en un nuevo espacio de nombres. Por este motivo, si solo desea usar operaciones basadas en HTTP (`create_queue`, `delete_queue` etc), actualizar en este momento no aportará ninguna ventaja adicional.

### <a name="how-do-i-migrate-my-code-to-the-new-version"></a>¿Cómo migro mi código a la nueva versión?

El código escrito en la versión 0.21.0 se puede portar a la versión 0.50.0 simplemente cambiando el espacio de nombres de importación:

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a>Uso de las operaciones basadas en HTTP de la API heredada

En la documentación siguiente se describe la API heredada, que deberán usarla aquellos que quieran portal el código existente desde la versión 0.50.0 sin realizar ningún cambio adicional. Esta referencia también sirve como guía para los usuarios de la versión 0.21.1.
Para los que están escribiendo código nuevo, se recomienda usar la nueva API descrita anteriormente.

### <a name="service-bus-queues"></a>Colas de Service Bus

#### <a name="shared-access-signature-sas-authentication"></a>Autenticación de Firma de acceso compartido (SAS)

Para usar la autenticación con firma de acceso compartido, cree el servicio de Service Bus con:

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a>Autenticación de Access Control Service (ACS)

ACS no se admite en los nuevos espacios de nombres de Service Bus. Se recomienda [migrar las aplicaciones a la autenticación de SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas). Para usar la autenticación de ACS dentro de un espacio de nombres de Service Bus anterior, cree ServiceBusService con:

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```

#### <a name="sending-and-receiving-messages"></a>Envío y recepción de mensajes

El método **create\_queue** se puede utilizar para asegurarse de existe que una cola:

```python
sbs.create_queue('taskqueue')
```

A continuación, se puede llamar al método **send\_queue\_message** para insertar el mensaje en la cola:

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```

Se puede llamar al método **send\_queue\_message_batch** para enviar varios mensajes a la vez:

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```

A continuación, es posible llamar al método **receive\_queue\_message** para eliminar el mensaje de la cola.

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a>Temas de Service Bus

El método **create\_topic** se puede utilizar para crear un tema de servidor:

```python
sbs.create_topic('taskdiscussion')
```

El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

El método **send\_topic\_message_batch** se puede utilizar para enviar varios mensajes a la vez:

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Tenga en cuenta que, en Python 3, un mensaje de tipo cadena se codificará en utf-8 y debe administrar la codificación por sí mismo en Python 2.

Después, un cliente puede crear una suscripción y empezar a consumir mensajes mediante una llamada al método **create\_subscription** seguida de otra al método **receive\_subscription\_message**. Tenga en cuenta que no se recibirán los mensajes enviados antes de crear la suscripción.

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a>Centro de eventos

Event Hubs permite recopilar secuencias de eventos con un alto rendimiento desde una amplia variedad de dispositivos y servicios.

El método **create\_event\_hub** se puede utilizar para crear un centro de eventos:

```python
sbs.create_event_hub('myhub')
```

Para enviar un evento:

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```

El contenido del evento es el mensaje del evento o una cadena codificada en JSON que contiene varios mensajes.

### <a name="advanced-features"></a>Características avanzadas

#### <a name="broker-properties-and-user-properties"></a>Propiedades de agente y de usuario

En esta sección se describe cómo utilizar las propiedades de agente y de usuario definidas [aquí](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```

Puede usar datetime, int, float o boolean

```python
props = {'hello': 'world',
         'number': 42,
         'active': True,
         'deceased': False,
         'large': 8555111000,
         'floating': 3.14,
         'dob': datetime(2011, 12, 14),
         'double_quote_message': 'This "should" work fine',
         'quote_message': "This 'should' work fine"}
sent_msg = Message(b'message with properties', custom_properties=props)
```

Por motivos de compatibilidad con la versión anterior de esta biblioteca, `broker_properties` también se puede definir como una cadena JSON.
Si esta es la situación, es responsable de escribir una cadena JSON válida, ya que Python no realizará ninguna comprobación antes del envío a la API de REST.

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a>Pasos siguientes

* [documentación de Service Bus](https://docs.microsoft.com/azure/service-bus-messaging)
* [Código fuente del SDK](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [Documentación de referencia del SDK](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [Ejemplos adicionales](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
