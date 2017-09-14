---
title: Bibliotecas de Service Bus para Python
description: "Documentación de referencia del cliente de Python y las bibliotecas de administración de Service"
keywords: "Azure, Python, SDK, API, mensajería, pubsub, pub-sub, agente de mensajes"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: bf7be945f2c7a3daea93ff4e5b770459c00632c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="b89c7-104">Bibliotecas de Service Bus para Python</span><span class="sxs-lookup"><span data-stu-id="b89c7-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="b89c7-105">Información general</span><span class="sxs-lookup"><span data-stu-id="b89c7-105">Overview</span></span>

<span data-ttu-id="b89c7-106">Microsoft Azure Service Bus admite un conjunto de tecnologías de middleware basadas en la nube y orientadas a mensajes, incluidas una cola de mensajes de confianza y una mensajería de publicación/suscripción duradera.</span><span class="sxs-lookup"><span data-stu-id="b89c7-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="b89c7-107">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="b89c7-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a><span data-ttu-id="b89c7-108">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="b89c7-108">Example</span></span>
<span data-ttu-id="b89c7-109">Envíe mensajes a una cola.</span><span class="sxs-lookup"><span data-stu-id="b89c7-109">Send messages to a queue.</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="b89c7-110">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="b89c7-110">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/managementlibrary)

