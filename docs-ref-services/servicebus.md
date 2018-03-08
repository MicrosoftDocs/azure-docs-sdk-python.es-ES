---
title: Bibliotecas de Service Bus para Python
description: "Documentación de referencia del cliente de Python y las bibliotecas de administración de Service"
keywords: "Azure, Python, SDK, API, mensajería, pubsub, pub-sub, agente de mensajes"
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 6c0bc66fbe8194b5b8f34ee8e29945b03ba8c242
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
---
# <a name="service-bus-libraries-for-python"></a>Bibliotecas de Service Bus para Python

## <a name="overview"></a>Información general

Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera. 

## <a name="install-the-libraries"></a>Instalación de las bibliotecas
```bash
pip install azure-mgmt-servicebus
```

## <a name="servicebus-queues"></a>Colas de Service Bus
Las colas de Service Bus son una alternativa a las colas de Storage que podrían ser útiles en escenarios en los que se necesitan características de mensajería más avanzadas (tamaños de mensaje más grandes, orden de los mensajes, lecturas destructivas de una sola operación o entrega programada) con entrega de inserción (mediante sondeo largo).

El servicio puede usar autenticación con firma de acceso compartido o autenticación de ACS.

Los espacios de nombres de Service Bus creados mediante Azure Portal después de agosto de 2014 no admiten la autenticación de ACS. Puede crear espacios de nombres compatibles con ACS con el SDK de Azure.

### <a name="shared-access-signature-authentication"></a>Autenticación con firma de acceso compartido

Para usar la autenticación con firma de acceso compartido, cree el servicio de Service Bus con:

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a>Autenticación de ACS

Para usar la autenticación de ACS, cree el servicio de Service Bus con:

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a>Envío y recepción de mensajes

El método **create\_queue** se puede utilizar para asegurarse de existe que una cola:

```python
sbs.create_queue('taskqueue')
```
A continuación, se puede llamar al método **send\_queue\_message** para insertar el mensaje en la cola:

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
Se puede llamar al método **send\_queue\_message_batch** para enviar varios mensajes a la vez:

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
A continuación, es posible llamar al método **receive\_queue\_message** para eliminar el mensaje de la cola.

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a>Temas de Service Bus

Los temas de Service Bus son una abstracción por encima de las colas de Service Bus que facilitan la implementación de escenarios de publicación y suscripción.

El método **create\_topic** se puede utilizar para crear un tema de servidor:

```python
sbs.create_topic('taskdiscussion')
```
El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Tenga en cuenta que, en Python 3, un mensaje de tipo cadena se codificará en utf-8 y debe administrar la codificación por sí mismo en Python 2.

Después, un cliente puede crear una suscripción y empezar a consumir mensajes mediante una llamada al método **create\_subscription** seguida de otra al método **receive\_subscription\_message**. Tenga en cuenta que no se recibirán los mensajes enviados antes de crear la suscripción.

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a>Centro de eventos

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

## <a name="advanced-features"></a>Características avanzadas

### <a name="broker-properties-and-user-properties"></a>Propiedades de agente y de usuario

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

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/servicebus/management)