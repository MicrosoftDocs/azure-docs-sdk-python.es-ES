---
title: Bibliotecas de Azure Event Grid para Python
description: ''
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: bfaa1908295eb77531e399f1337acdeee512005f
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276839"
---
# <a name="event-grid-libraries-for-python"></a>Bibliotecas de Event Grid para Python


Azure Event Grid es un servicio de enrutamiento de eventos inteligente completamente administrado que permite el consumo de eventos uniforme mediante un modelo de publicación-suscripción.

[Para más información](/azure/event-grid/overview) acerca de Azure Event Grid y empezar a trabajar con el [tutorial de eventos de Azure Blob Storage](/azure/storage/blobs/storage-blob-event-quickstart). 

## <a name="publish-sdk"></a>SDK de publicación

Puede autenticar, crear, controlar y publicar eventos en temas con el SDK de publicación de Azure Event Grid.

### <a name="installation"></a>Instalación 

Instale el paquete con [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-eventgrid
```

### <a name="example"></a>Ejemplo 

El código siguiente publica un evento en un tema. Puede recuperar la clave del tema y el punto de conexión desde Azure Portal o a través de la CLI de Azure:

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
> [Explorar las API de cliente](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>SDK de administración

El SDK de administración permite crear, actualizar y eliminar instancias, temas y suscripciones de Event Grid.

### <a name="installation"></a>Instalación 

Instale el paquete con [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>Ejemplo

A continuación se crea un tema personalizado y se suscribe un punto de conexión al tema. El código, a continuación, envía un evento al tema a través de HTTPS.
RequestBin es una herramienta de código abierto de terceros que le permite crear un punto de conexión y ver las solicitudes que se envían a él. Vaya a [RequestBin](https://requestb.in/) y haga clic en **Create a RequestBin** (Crear RequestBin). Copie la dirección URL de la ubicación, la necesitará para suscribirse al tema.

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
Vaya a la dirección URL de RequestBin creada anteriormente para ver los eventos que acabamos de enviar.

Limpieza de recursos
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>Más información

[Recepción de eventos mediante el SDK de Event Grid](/azure/event-grid/receive-events)
