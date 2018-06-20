---
title: Bibliotecas de Azure Event Grid para Python
description: ''
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
ms.openlocfilehash: e68504b3ba5834a145af1231eacc076e424a2256
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
ms.locfileid: "33901430"
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="76c8e-103">Bibliotecas de Event Grid para Python</span><span class="sxs-lookup"><span data-stu-id="76c8e-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="76c8e-104">Azure Event Grid es un servicio de enrutamiento de eventos inteligente completamente administrado que permite el consumo de eventos uniforme mediante un modelo de publicación-suscripción.</span><span class="sxs-lookup"><span data-stu-id="76c8e-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="76c8e-105">[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart).</span><span class="sxs-lookup"><span data-stu-id="76c8e-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="76c8e-106">SDK de publicación</span><span class="sxs-lookup"><span data-stu-id="76c8e-106">Publish SDK</span></span>

<span data-ttu-id="76c8e-107">Puede autenticar, crear, controlar y publicar eventos en temas con el SDK de publicación de Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="76c8e-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="76c8e-108">Instalación</span><span class="sxs-lookup"><span data-stu-id="76c8e-108">Installation</span></span> 

<span data-ttu-id="76c8e-109">Instale el paquete con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="76c8e-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="76c8e-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="76c8e-110">Example</span></span> 

<span data-ttu-id="76c8e-111">El código siguiente publica un evento en un tema.</span><span class="sxs-lookup"><span data-stu-id="76c8e-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="76c8e-112">Puede recuperar la clave del tema y el punto de conexión desde Azure Portal o a través de la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="76c8e-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="76c8e-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="76c8e-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="76c8e-114">SDK de administración</span><span class="sxs-lookup"><span data-stu-id="76c8e-114">Management SDK</span></span>

<span data-ttu-id="76c8e-115">El SDK de administración permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.</span><span class="sxs-lookup"><span data-stu-id="76c8e-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="76c8e-116">Instalación</span><span class="sxs-lookup"><span data-stu-id="76c8e-116">Installation</span></span> 

<span data-ttu-id="76c8e-117">Instale el paquete con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="76c8e-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="76c8e-118">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="76c8e-118">Example</span></span>

<span data-ttu-id="76c8e-119">A continuación se crea un tema personalizado y se suscribe un punto de conexión al tema.</span><span class="sxs-lookup"><span data-stu-id="76c8e-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="76c8e-120">El código, a continuación, envía un evento al tema a través de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="76c8e-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="76c8e-121">RequestBin es una herramienta de código abierto de terceros que le permite crear un punto de conexión y ver las solicitudes que se envían a él.</span><span class="sxs-lookup"><span data-stu-id="76c8e-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="76c8e-122">Vaya a [RequestBin](https://requestb.in/) y haga clic en **Create a RequestBin** (Crear RequestBin).</span><span class="sxs-lookup"><span data-stu-id="76c8e-122">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="76c8e-123">Copie la dirección URL de la ubicación, la necesitará para suscribirse al tema.</span><span class="sxs-lookup"><span data-stu-id="76c8e-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="76c8e-124">Vaya a la dirección URL de RequestBin creada anteriormente para ver los eventos que acabamos de enviar.</span><span class="sxs-lookup"><span data-stu-id="76c8e-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="76c8e-125">Limpieza de recursos</span><span class="sxs-lookup"><span data-stu-id="76c8e-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="76c8e-126">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="76c8e-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="76c8e-127">Más información</span><span class="sxs-lookup"><span data-stu-id="76c8e-127">Learn more</span></span>

[<span data-ttu-id="76c8e-128">Recepción de eventos mediante el SDK de Event Grid</span><span class="sxs-lookup"><span data-stu-id="76c8e-128">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)