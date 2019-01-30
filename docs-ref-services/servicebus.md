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
ms.openlocfilehash: 540a2a248f7a2abcc83517bc4a4ef96ef03e8a9f
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747745"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="1e8cc-104">Bibliotecas de Service Bus para Python</span><span class="sxs-lookup"><span data-stu-id="1e8cc-104">Service Bus libraries for Python</span></span>

<span data-ttu-id="1e8cc-105">Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-105">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span>

* [<span data-ttu-id="1e8cc-106">Código fuente del SDK</span><span class="sxs-lookup"><span data-stu-id="1e8cc-106">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="1e8cc-107">Documentación de referencia del SDK</span><span class="sxs-lookup"><span data-stu-id="1e8cc-107">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a><span data-ttu-id="1e8cc-108">Novedades de la versión 0.50.0</span><span class="sxs-lookup"><span data-stu-id="1e8cc-108">What's new in v0.50.0?</span></span>
<span data-ttu-id="1e8cc-109">A partir de la versión 0.50.0, hay una nueva API basada en AMQP disponible para enviar y recibir mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-109">As of version 0.50.0 a new AMQP-based API is available for sending and receiving messages.</span></span> <span data-ttu-id="1e8cc-110">Esta actualización implica **cambios importantes**.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-110">This update involves **breaking changes**.</span></span>
<span data-ttu-id="1e8cc-111">Lea el documento de [migración de v0.21.1 a v0.50.0](#migration-from-v0211-to-v0500) para determinar si debe actualizar en este momento.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-111">Please read [Migration from v0.21.1 to v0.50.0](#migration-from-v0211-to-v0500) to determine if upgrading is right for you at this time.</span></span>

<span data-ttu-id="1e8cc-112">La nueva API basada en AMQP ofrece confiabilidad, rendimiento, compatibilidad y más características para el envío de mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-112">The new AMQP-based API offers improved message passing reliability, performance and expanded feature support going forward.</span></span>
<span data-ttu-id="1e8cc-113">También ofrece compatibilidad para las operaciones asincrónicas (basadas en asyncio) para enviar, recibir y controlar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-113">The new API also offers support for asynchronous operations (based on asyncio) for sending, receiving and handling messages.</span></span>

<span data-ttu-id="1e8cc-114">Para ver la documentación sobre las operaciones basadas en HTTP heredadas, consulte [Uso de las operaciones basadas en HTTP de la API heredada](#using-http-based-operations-of-the-legacy-api).</span><span class="sxs-lookup"><span data-stu-id="1e8cc-114">For documentation on the legacy HTTP-based operations please see [Using HTTP-based operations of the legacy API](#using-http-based-operations-of-the-legacy-api).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="1e8cc-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1e8cc-115">Prerequisites</span></span>

* <span data-ttu-id="1e8cc-116">Una suscripción de Azure (cree una [cuenta gratuita](https://azure.microsoft.com/free/)).</span><span class="sxs-lookup"><span data-stu-id="1e8cc-116">Azure subscription - [Create a free account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="1e8cc-117">Un [espacio de nombres de Service Bus y credenciales de administración](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal) de Azure.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-117">Azure [Service Bus namespace and management credentials](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span></span>
* [<span data-ttu-id="1e8cc-118">Python 2.7-3.7</span><span class="sxs-lookup"><span data-stu-id="1e8cc-118">Python 2.7-3.7</span></span>](https://www.python.org/downloads/)


## <a name="installation"></a><span data-ttu-id="1e8cc-119">Instalación</span><span class="sxs-lookup"><span data-stu-id="1e8cc-119">Installation</span></span>
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a><span data-ttu-id="1e8cc-120">Conexión a Azure Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-120">Connect to Azure Service Bus</span></span>

### <a name="get-credentials"></a><span data-ttu-id="1e8cc-121">Obtener credenciales</span><span class="sxs-lookup"><span data-stu-id="1e8cc-121">Get credentials</span></span>
<span data-ttu-id="1e8cc-122">Use el siguiente fragmento de la CLI de Azure para rellenar una variable de entorno con la cadena de conexión de Service Bus (también puede encontrar este valor en Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="1e8cc-122">Use the Azure CLI snippet below to populate an environment variable with the Service Bus connection string (you can also find this value in the Azure portal).</span></span> <span data-ttu-id="1e8cc-123">El fragmento de código tiene el formato para el shell de Bash.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-123">The snippet is formatted for the Bash shell.</span></span>

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

### <a name="create-client"></a><span data-ttu-id="1e8cc-124">Crear el cliente</span><span class="sxs-lookup"><span data-stu-id="1e8cc-124">Create client</span></span>
<span data-ttu-id="1e8cc-125">Una vez que ha rellenado la variable de entorno `SB_CONN_STR`, puede crear el cliente de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-125">Once you've populated the `SB_CONN_STR` environment variable, you can create the ServiceBusClient.</span></span>
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
<span data-ttu-id="1e8cc-126">Si desea usar operaciones asincrónicas, use el espacio de nombres `azure.servicebus.aio`.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-126">If you wish to use asynchronous operations, please use the `azure.servicebus.aio` namespace.</span></span>
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a><span data-ttu-id="1e8cc-127">Colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-127">Service Bus queues</span></span>
<span data-ttu-id="1e8cc-128">Las colas de Service Bus son una alternativa a las colas de Storage que podrían ser útiles en escenarios en los que se necesitan características de mensajería más avanzadas (tamaños de mensaje más grandes, orden de los mensajes, lecturas destructivas de una sola operación o entrega programada) con entrega de inserción (mediante sondeo largo).</span><span class="sxs-lookup"><span data-stu-id="1e8cc-128">Service Bus queues are an alternative to Storage queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

### <a name="create-queue"></a><span data-ttu-id="1e8cc-129">Crear cola</span><span class="sxs-lookup"><span data-stu-id="1e8cc-129">Create queue</span></span>
<span data-ttu-id="1e8cc-130">Se crea una nueva cola en el espacio de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-130">This creates a new queue within the Service Bus namespace.</span></span> <span data-ttu-id="1e8cc-131">Si ya existe una cola con el mismo nombre en el espacio de nombres, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-131">If a queue of the same name already exists within the namespace an error will be raised.</span></span> 
```python
sb_client.create_queue("MyQueue")
```
<span data-ttu-id="1e8cc-132">También se pueden especificar parámetros opcionales para configurar el comportamiento de la cola.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-132">Optional parameters to configure the queue behaviour can also be specified.</span></span>
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a><span data-ttu-id="1e8cc-133">Obtener un cliente de cola</span><span class="sxs-lookup"><span data-stu-id="1e8cc-133">Get a queue client</span></span>
<span data-ttu-id="1e8cc-134">Se puede usar QueueClient para enviar y recibir mensajes de la cola, además de otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-134">A QueueClient can be used to send and receive messages from the queue, along with other operations.</span></span>
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a><span data-ttu-id="1e8cc-135">Envío de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e8cc-135">Sending messages</span></span>
<span data-ttu-id="1e8cc-136">El cliente de cola puede enviar uno o varios mensajes a la vez:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-136">The queue client can send one or more messages at a time:</span></span>
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
<span data-ttu-id="1e8cc-137">Cada llamada a QueueClient.send creará una nueva conexión de servicio.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-137">Each call to QueueClient.send will create a new service connection.</span></span> <span data-ttu-id="1e8cc-138">Para reutilizar la misma conexión para varias llamadas de envío, puede abrir un remitente:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-138">To reuse the same connection for multiple send calls, you can open a sender:</span></span>
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
<span data-ttu-id="1e8cc-139">Si usa a un cliente asincrónico, las operaciones anteriores usará la sintaxis de async:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-139">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
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


### <a name="receiving-messages"></a><span data-ttu-id="1e8cc-140">Recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e8cc-140">Receiving messages</span></span>
<span data-ttu-id="1e8cc-141">Los mensajes se pueden recibir de una cola como un iterador continuo.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-141">Messages can be received from a queue as a continuous iterator.</span></span> <span data-ttu-id="1e8cc-142">El modo predeterminado para la recepción del mensaje es [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), que requiere que cada mensaje se complete explícitamente para poder quitarlo de la cola.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-142">The default mode for message receiving is [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), which requires each message to be explicitly completed in order that it be removed from the queue.</span></span>
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
<span data-ttu-id="1e8cc-143">La conexión de servicio permanecerá abierta durante todo el iterador.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-143">The service connection will remain open for the entirety of the iterator.</span></span>
<span data-ttu-id="1e8cc-144">Si detecta que la iteración por la secuencia de mensajes se realiza solo parcialmente, debe ejecutar el receptor una instrucción `with` para asegurarse de que la conexión se cierra:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-144">If you find yourself only partially iterating the message stream, you should run the receiver in a `with` statement to ensure the connection is closed:</span></span>
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
<span data-ttu-id="1e8cc-145">Si usa a un cliente asincrónico, las operaciones anteriores usará la sintaxis de async:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-145">If you are using an asynchronous client, the above operations will use async syntax:</span></span>
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a><span data-ttu-id="1e8cc-146">Temas y suscripciones de Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-146">Service Bus topics and subscriptions</span></span>

<span data-ttu-id="1e8cc-147">Los temas y las suscripciones de Service Bus son una abstracción que se sitúan encima de las colas de Service Bus y que proporcionan una o varias formas de comunicación según un modelo publicación/suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-147">Service Bus topics and subscriptions are an abstraction on top of Service Bus queues that provide a one-to-many form of communication, in a publish/subscribe pattern.</span></span> <span data-ttu-id="1e8cc-148">Los mensajes se envían a un tema y entregan a una o varias suscripciones asociadas, lo que resulta útil para escalar a un gran número de destinatarios.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-148">Messages are sent to a topic and delivered to one or more associated subscriptions, which is useful for scaling to large numbers of recipients.</span></span>

### <a name="create-topic"></a><span data-ttu-id="1e8cc-149">Crear tema</span><span class="sxs-lookup"><span data-stu-id="1e8cc-149">Create topic</span></span>
<span data-ttu-id="1e8cc-150">Se crea un nuevo tema en el espacio de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-150">This creates a new topic within the Service Bus namespace.</span></span> <span data-ttu-id="1e8cc-151">Si ya existe un tema con el mismo nombre, se producirá un error.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-151">If a topic of the same name already exists an error will be raised.</span></span> 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a><span data-ttu-id="1e8cc-152">Obtener un cliente de tema</span><span class="sxs-lookup"><span data-stu-id="1e8cc-152">Get a topic client</span></span>
<span data-ttu-id="1e8cc-153">Se puede usar TopicClient para enviar mensajes al tema, además de otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-153">A TopicClient can be used to send messages to the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a><span data-ttu-id="1e8cc-154">Creación de una suscripción</span><span class="sxs-lookup"><span data-stu-id="1e8cc-154">Create subscription</span></span>
<span data-ttu-id="1e8cc-155">Se crea una nueva suscripción para el tema especificado dentro del espacio de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-155">This creates a new subscription for the specified topic within the Service Bus namespace.</span></span>
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a><span data-ttu-id="1e8cc-156">Obtener un cliente de suscripción</span><span class="sxs-lookup"><span data-stu-id="1e8cc-156">Get a subscription client</span></span>
<span data-ttu-id="1e8cc-157">Se puede usar SubscriptionClient para recibir mensajes del tema, además de otras operaciones.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-157">A SubscriptionClient can be used to receive messages from the topic, along with other operations.</span></span>
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a><span data-ttu-id="1e8cc-158">Migración de v0.21.1 a v0.50.0</span><span class="sxs-lookup"><span data-stu-id="1e8cc-158">Migration from v0.21.1 to v0.50.0</span></span>
<span data-ttu-id="1e8cc-159">Se introdujeron cambios importantes en la versión 0.50.0.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-159">Major breaking changes were introduced in version 0.50.0.</span></span>
<span data-ttu-id="1e8cc-160">La API basada en HTTP original sigue estando disponible en la versión 0.50.0; sin embargo, ahora existe en un espacio de nombres nuevo: `azure.servicebus.control_client`.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-160">The original HTTP-based API is still available in v0.50.0 - however it now exists under a new namesapce: `azure.servicebus.control_client`.</span></span>

### <a name="should-i-upgrade"></a><span data-ttu-id="1e8cc-161">¿Debería actualizar?</span><span class="sxs-lookup"><span data-stu-id="1e8cc-161">Should I upgrade?</span></span>
<span data-ttu-id="1e8cc-162">El nuevo paquete (v0.50.0) no ofrece mejoras en las operaciones basadas en HTTP respecto a v0.21.1.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-162">The new package (v0.50.0) offers no improvements in HTTP-based operations over v0.21.1.</span></span> <span data-ttu-id="1e8cc-163">La API basada en HTTP es idéntica, salvo que ahora existe en un nuevo espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-163">The HTTP-based API is identical except that it now exists under a new namespace.</span></span> <span data-ttu-id="1e8cc-164">Por este motivo, si solo desea usar operaciones basadas en HTTP (`create_queue`, `delete_queue` etc), actualizar en este momento no aportará ninguna ventaja adicional.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-164">For this reason if you only wish to use HTTP-based operations (`create_queue`, `delete_queue` etc) - there will be no additional benefit in upgrading at this time.</span></span>


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a><span data-ttu-id="1e8cc-165">¿Cómo migro mi código a la nueva versión?</span><span class="sxs-lookup"><span data-stu-id="1e8cc-165">How do I migrate my code to the new version?</span></span>
<span data-ttu-id="1e8cc-166">El código escrito en la versión 0.21.0 se puede portar a la versión 0.50.0 simplemente cambiando el espacio de nombres de importación:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-166">Code written against v0.21.0 can be ported to version 0.50.0 by simply changing the import namespace:</span></span>

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a><span data-ttu-id="1e8cc-167">Uso de las operaciones basadas en HTTP de la API heredada</span><span class="sxs-lookup"><span data-stu-id="1e8cc-167">Using HTTP-based operations of the legacy API</span></span>
<span data-ttu-id="1e8cc-168">En la documentación siguiente se describe la API heredada, que deberán usarla aquellos que quieran portal el código existente desde la versión 0.50.0 sin realizar ningún cambio adicional.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-168">The following documentation describes the legacy API and should be used for those wishing to port existing code to v0.50.0 without making any additional changes.</span></span> <span data-ttu-id="1e8cc-169">Esta referencia también sirve como guía para los usuarios de la versión 0.21.1.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-169">This reference can also be used as guidance by those using v0.21.1.</span></span>
<span data-ttu-id="1e8cc-170">Para los que están escribiendo código nuevo, se recomienda usar la nueva API descrita anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-170">For those writing new code, we recommend using the new API described above.</span></span>

### <a name="service-bus-queues"></a><span data-ttu-id="1e8cc-171">Colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-171">Service Bus queues</span></span>

#### <a name="shared-access-signature-sas-authentication"></a><span data-ttu-id="1e8cc-172">Autenticación de Firma de acceso compartido (SAS)</span><span class="sxs-lookup"><span data-stu-id="1e8cc-172">Shared Access Signature (SAS) authentication</span></span>

<span data-ttu-id="1e8cc-173">Para usar la autenticación con firma de acceso compartido, cree el servicio de Service Bus con:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-173">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a><span data-ttu-id="1e8cc-174">Autenticación de Access Control Service (ACS)</span><span class="sxs-lookup"><span data-stu-id="1e8cc-174">Access Control Service (ACS) authentication</span></span>
<span data-ttu-id="1e8cc-175">ACS ya no se admite en los nuevos espacios de nombres de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-175">ACS is no longer supported on new Service Bus namespaces.</span></span> <span data-ttu-id="1e8cc-176">Se recomienda [migrar las aplicaciones a la autenticación de SAS](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span><span class="sxs-lookup"><span data-stu-id="1e8cc-176">We recommend [migrating applications to SAS authentication](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span></span>
<span data-ttu-id="1e8cc-177">Para usar la autenticación de ACS dentro de un espacio de nombres de Service Bus anterior, cree ServiceBusService con:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-177">To use ACS authentication within an older Service Bus namesapce, create the ServiceBusService with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a><span data-ttu-id="1e8cc-178">Envío y recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="1e8cc-178">Sending and receiving messages</span></span>

<span data-ttu-id="1e8cc-179">El método **create\_queue** se puede utilizar para asegurarse de existe que una cola:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-179">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="1e8cc-180">A continuación, se puede llamar al método **send\_queue\_message** para insertar el mensaje en la cola:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-180">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="1e8cc-181">Se puede llamar al método **send\_queue\_message_batch** para enviar varios mensajes a la vez:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-181">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="1e8cc-182">A continuación, es posible llamar al método **receive\_queue\_message** para eliminar el mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-182">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a><span data-ttu-id="1e8cc-183">Temas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-183">Service Bus topics</span></span>

<span data-ttu-id="1e8cc-184">El método **create\_topic** se puede utilizar para crear un tema de servidor:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-184">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="1e8cc-185">El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-185">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="1e8cc-186">El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-186">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="1e8cc-187">Tenga en cuenta que, en Python 3, un mensaje de tipo cadena se codificará en utf-8 y debe administrar la codificación por sí mismo en Python 2.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-187">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="1e8cc-188">Después, un cliente puede crear una suscripción y empezar a consumir mensajes mediante una llamada al método **create\_subscription** seguida de otra al método **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-188">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="1e8cc-189">Tenga en cuenta que no se recibirán los mensajes enviados antes de crear la suscripción.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-189">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a><span data-ttu-id="1e8cc-190">Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="1e8cc-190">Event Hub</span></span>

<span data-ttu-id="1e8cc-191">Event Hubs permite recopilar secuencias de eventos con un alto rendimiento desde una amplia variedad de dispositivos y servicios.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-191">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="1e8cc-192">El método **create\_event\_hub** se puede utilizar para crear un centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-192">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="1e8cc-193">Para enviar un evento:</span><span class="sxs-lookup"><span data-stu-id="1e8cc-193">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="1e8cc-194">El contenido del evento es el mensaje del evento o una cadena codificada en JSON que contiene varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-194">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

### <a name="advanced-features"></a><span data-ttu-id="1e8cc-195">Características avanzadas</span><span class="sxs-lookup"><span data-stu-id="1e8cc-195">Advanced features</span></span>

#### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="1e8cc-196">Propiedades de agente y de usuario</span><span class="sxs-lookup"><span data-stu-id="1e8cc-196">Broker properties and user properties</span></span>

<span data-ttu-id="1e8cc-197">En esta sección se describe cómo utilizar las propiedades de agente y de usuario definidas [aquí](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="1e8cc-197">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
<span data-ttu-id="1e8cc-198">Puede usar datetime, int, float o boolean</span><span class="sxs-lookup"><span data-stu-id="1e8cc-198">You can use datetime, int, float or boolean</span></span>

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
<span data-ttu-id="1e8cc-199">Por motivos de compatibilidad con la versión anterior de esta biblioteca, `broker_properties` también se puede definir como una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-199">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="1e8cc-200">Si esta es la situación, es responsable de escribir una cadena JSON válida, ya que Python no realizará ninguna comprobación antes del envío a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="1e8cc-200">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a><span data-ttu-id="1e8cc-201">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1e8cc-201">Next Steps</span></span>
* [<span data-ttu-id="1e8cc-202">documentación de Service Bus</span><span class="sxs-lookup"><span data-stu-id="1e8cc-202">Service Bus documentation</span></span>](https://docs.microsoft.com/azure/service-bus-messaging)
* [<span data-ttu-id="1e8cc-203">Código fuente del SDK</span><span class="sxs-lookup"><span data-stu-id="1e8cc-203">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="1e8cc-204">Documentación de referencia del SDK</span><span class="sxs-lookup"><span data-stu-id="1e8cc-204">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [<span data-ttu-id="1e8cc-205">Ejemplos adicionales</span><span class="sxs-lookup"><span data-stu-id="1e8cc-205">Additional samples</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
