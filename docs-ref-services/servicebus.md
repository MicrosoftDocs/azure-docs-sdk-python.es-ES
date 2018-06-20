---
title: Bibliotecas de Service Bus para Python
description: Documentación de referencia del cliente de Python y las bibliotecas de administración de Service
keywords: Azure, Python, SDK, API, mensajería, pubsub, pub-sub, agente de mensajes
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
ms.locfileid: "29551598"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="3872e-104">Bibliotecas de Service Bus para Python</span><span class="sxs-lookup"><span data-stu-id="3872e-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="3872e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="3872e-105">Overview</span></span>

<span data-ttu-id="3872e-106">Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera.</span><span class="sxs-lookup"><span data-stu-id="3872e-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="3872e-107">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="3872e-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="servicebus-queues"></a><span data-ttu-id="3872e-108">Colas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="3872e-108">ServiceBus Queues</span></span>
<span data-ttu-id="3872e-109">Las colas de Service Bus son una alternativa a las colas de Storage que podrían ser útiles en escenarios en los que se necesitan características de mensajería más avanzadas (tamaños de mensaje más grandes, orden de los mensajes, lecturas destructivas de una sola operación o entrega programada) con entrega de inserción (mediante sondeo largo).</span><span class="sxs-lookup"><span data-stu-id="3872e-109">ServiceBus Queues are an alternative to Storage Queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

<span data-ttu-id="3872e-110">El servicio puede usar autenticación con firma de acceso compartido o autenticación de ACS.</span><span class="sxs-lookup"><span data-stu-id="3872e-110">The service can use Shared Access Signature authentication, or ACS authentication.</span></span>

<span data-ttu-id="3872e-111">Los espacios de nombres de Service Bus creados mediante Azure Portal después de agosto de 2014 no admiten la autenticación de ACS.</span><span class="sxs-lookup"><span data-stu-id="3872e-111">Service bus namespaces created using the Azure portal after August 2014 no longer support ACS authentication.</span></span> <span data-ttu-id="3872e-112">Puede crear espacios de nombres compatibles con ACS con el SDK de Azure.</span><span class="sxs-lookup"><span data-stu-id="3872e-112">You can create ACS compatible namespaces with the Azure SDK.</span></span>

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="3872e-113">Autenticación con firma de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="3872e-113">Shared Access Signature Authentication</span></span>

<span data-ttu-id="3872e-114">Para usar la autenticación con firma de acceso compartido, cree el servicio de Service Bus con:</span><span class="sxs-lookup"><span data-stu-id="3872e-114">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a><span data-ttu-id="3872e-115">Autenticación de ACS</span><span class="sxs-lookup"><span data-stu-id="3872e-115">ACS Authentication</span></span>

<span data-ttu-id="3872e-116">Para usar la autenticación de ACS, cree el servicio de Service Bus con:</span><span class="sxs-lookup"><span data-stu-id="3872e-116">To use ACS authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a><span data-ttu-id="3872e-117">Envío y recepción de mensajes</span><span class="sxs-lookup"><span data-stu-id="3872e-117">Sending and Receiving Messages</span></span>

<span data-ttu-id="3872e-118">El método **create\_queue** se puede utilizar para asegurarse de existe que una cola:</span><span class="sxs-lookup"><span data-stu-id="3872e-118">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="3872e-119">A continuación, se puede llamar al método **send\_queue\_message** para insertar el mensaje en la cola:</span><span class="sxs-lookup"><span data-stu-id="3872e-119">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="3872e-120">Se puede llamar al método **send\_queue\_message_batch** para enviar varios mensajes a la vez:</span><span class="sxs-lookup"><span data-stu-id="3872e-120">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="3872e-121">A continuación, es posible llamar al método **receive\_queue\_message** para eliminar el mensaje de la cola.</span><span class="sxs-lookup"><span data-stu-id="3872e-121">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a><span data-ttu-id="3872e-122">Temas de Service Bus</span><span class="sxs-lookup"><span data-stu-id="3872e-122">ServiceBus Topics</span></span>

<span data-ttu-id="3872e-123">Los temas de Service Bus son una abstracción por encima de las colas de Service Bus que facilitan la implementación de escenarios de publicación y suscripción.</span><span class="sxs-lookup"><span data-stu-id="3872e-123">ServiceBus topics are an abstraction on top of ServiceBus Queues that make pub/sub scenarios easy to implement.</span></span>

<span data-ttu-id="3872e-124">El método **create\_topic** se puede utilizar para crear un tema de servidor:</span><span class="sxs-lookup"><span data-stu-id="3872e-124">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="3872e-125">El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:</span><span class="sxs-lookup"><span data-stu-id="3872e-125">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="3872e-126">El método **send\_topic\_message** se puede utilizar para enviar un mensaje a un tema:</span><span class="sxs-lookup"><span data-stu-id="3872e-126">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="3872e-127">Tenga en cuenta que, en Python 3, un mensaje de tipo cadena se codificará en utf-8 y debe administrar la codificación por sí mismo en Python 2.</span><span class="sxs-lookup"><span data-stu-id="3872e-127">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="3872e-128">Después, un cliente puede crear una suscripción y empezar a consumir mensajes mediante una llamada al método **create\_subscription** seguida de otra al método **receive\_subscription\_message**.</span><span class="sxs-lookup"><span data-stu-id="3872e-128">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="3872e-129">Tenga en cuenta que no se recibirán los mensajes enviados antes de crear la suscripción.</span><span class="sxs-lookup"><span data-stu-id="3872e-129">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a><span data-ttu-id="3872e-130">Centro de eventos</span><span class="sxs-lookup"><span data-stu-id="3872e-130">Event Hub</span></span>

<span data-ttu-id="3872e-131">Event Hubs permite recopilar secuencias de eventos con un alto rendimiento desde una amplia variedad de dispositivos y servicios.</span><span class="sxs-lookup"><span data-stu-id="3872e-131">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="3872e-132">El método **create\_event\_hub** se puede utilizar para crear un centro de eventos:</span><span class="sxs-lookup"><span data-stu-id="3872e-132">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="3872e-133">Para enviar un evento:</span><span class="sxs-lookup"><span data-stu-id="3872e-133">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="3872e-134">El contenido del evento es el mensaje del evento o una cadena codificada en JSON que contiene varios mensajes.</span><span class="sxs-lookup"><span data-stu-id="3872e-134">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="3872e-135">Características avanzadas</span><span class="sxs-lookup"><span data-stu-id="3872e-135">Advanced features</span></span>

### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="3872e-136">Propiedades de agente y de usuario</span><span class="sxs-lookup"><span data-stu-id="3872e-136">Broker Properties and User Properties</span></span>

<span data-ttu-id="3872e-137">En esta sección se describe cómo utilizar las propiedades de agente y de usuario definidas [aquí](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span><span class="sxs-lookup"><span data-stu-id="3872e-137">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
<span data-ttu-id="3872e-138">Puede usar datetime, int, float o boolean</span><span class="sxs-lookup"><span data-stu-id="3872e-138">You can use datetime, int, float or boolean</span></span>

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
<span data-ttu-id="3872e-139">Por motivos de compatibilidad con la versión anterior de esta biblioteca, `broker_properties` también se puede definir como una cadena JSON.</span><span class="sxs-lookup"><span data-stu-id="3872e-139">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="3872e-140">Si esta es la situación, es responsable de escribir una cadena JSON válida, ya que Python no realizará ninguna comprobación antes del envío a la API de REST.</span><span class="sxs-lookup"><span data-stu-id="3872e-140">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="3872e-141">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="3872e-141">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/management)