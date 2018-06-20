---
title: Bibliotecas de Azure Scheduler para Python
description: Referencia de las bibliotecas de Azure Scheduler para Python
keywords: Azure, python, SDK, API, Scheduler
author: lisawong19
ms.author: liwong
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3d2691ae1ba84c41f25de2b099aacefaa92152ed
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551618"
---
# <a name="azure-scheduler-libraries-for-python"></a>Bibliotecas de Azure Scheduler para Python

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

## <a name="management"></a>Administración

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a>Ejemplo

### <a name="create-the-management-client"></a>Creación del cliente de administración

El código siguiente crea una instancia del cliente de administración.

Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a>Creación de una colección de trabajos

El código siguiente crea una colección de trabajos en un grupo de recursos existente.
Para crear o administrar grupos de recursos, consulte [Administración de recursos](/python/api/overview/azure/azure.mgmt.resource).

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/scheduler/management)