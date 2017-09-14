---
title: Bibliotecas de Azure Event Grid para Python
description: 
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: 81c4e74b00ac59c789c5a0b83eaa10652ec6d8ac
ms.sourcegitcommit: db4608e494cb4340649bce98ba9fb4504d3686bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2017
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="79fb4-103">Bibliotecas de Service Bus para Python</span><span class="sxs-lookup"><span data-stu-id="79fb4-103">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="79fb4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="79fb4-104">Overview</span></span>
<span data-ttu-id="79fb4-105">Azure Event Grid es un servicio de enrutamiento de eventos inteligente completamente administrado que permite el consumo de eventos uniforme mediante un modelo de publicación-suscripción.</span><span class="sxs-lookup"><span data-stu-id="79fb4-105">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

## <a name="management-api"></a><span data-ttu-id="79fb4-106">API de administración</span><span class="sxs-lookup"><span data-stu-id="79fb4-106">Management API</span></span>
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="79fb4-107">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="79fb4-107">Example</span></span>
<span data-ttu-id="79fb4-108">A continuación, crea un tema personalizado, se suscribe al tema y desencadena el evento para ver el resultado.</span><span class="sxs-lookup"><span data-stu-id="79fb4-108">The following creates a custom topic, subscribes to the topic, and triggers the event to view the result.</span></span> <span data-ttu-id="79fb4-109">RequestBin es una herramienta de código abierto de terceros que le permite crear un punto de conexión y ver las solicitudes que se envían a él.</span><span class="sxs-lookup"><span data-stu-id="79fb4-109">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="79fb4-110">Vaya a [RequestBin](https://requestb.in/) y haga clic en **Create a RequestBin** (Crear RequestBin).</span><span class="sxs-lookup"><span data-stu-id="79fb4-110">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="79fb4-111">Copie la dirección URL de la ubicación, la necesitará para suscribirse al tema.</span><span class="sxs-lookup"><span data-stu-id="79fb4-111">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
<span data-ttu-id="79fb4-112">Vaya a la dirección URL de RequestBin creada anteriormente para ver los eventos que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="79fb4-112">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="79fb4-113">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="79fb4-113">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="79fb4-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="79fb4-114">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/managementlibrary)
