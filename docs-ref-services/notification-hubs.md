---
title: Bibliotecas de Azure Notification Hubs para Python
description: Referencia de las bibliotecas de Azure Notification Hubs para Python
keywords: Azure, python, SDK, API, Notification Hubs
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 66b452a40fd524672f4dad92a9d1bd0ffb77a99d
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551588"
---
# <a name="azure-notification-hubs-libraries-for-python"></a><span data-ttu-id="7883e-104">Bibliotecas de Azure Notification Hubs para Python</span><span class="sxs-lookup"><span data-stu-id="7883e-104">Azure Notification Hubs libraries for python</span></span>

## <a name="management-apipythonapioverviewazurenotificationhubsmanagement"></a>[<span data-ttu-id="7883e-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="7883e-105">Management API</span></span>](/python/api/overview/azure/notificationhubs/management)

```bash
pip install azure-mgmt-notificationhubs
```

## <a name="create-the-management-client"></a><span data-ttu-id="7883e-106">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="7883e-106">Create the management client</span></span>

<span data-ttu-id="7883e-107">El código siguiente crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="7883e-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="7883e-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="7883e-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="7883e-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="7883e-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.notificationhubs import NotificationHubsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

redis_client = NotificationHubsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="check-namespace-availability"></a><span data-ttu-id="7883e-110">Comprobación de la disponibilidad del espacio de nombres</span><span class="sxs-lookup"><span data-stu-id="7883e-110">Check namespace availability</span></span>

<span data-ttu-id="7883e-111">El siguiente código comprueba la disponibilidad del espacio de nombres de un centro de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="7883e-111">The following code check namespace availability of a notification hub.</span></span>
```python
from azure.mgmt.notificationhubs.models import CheckAvailabilityParameters

account_name = 'mynotificationhub'
output = notificationhubs_client.namespaces.check_availability(
    azure.mgmt.notificationhubs.models.CheckAvailabilityParameters(
        name = account_name
    )
)
# output is a CheckAvailibilityResource instance
print(output.is_availiable) # Yes, it's 'availiable', it's a typo in the REST API
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7883e-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="7883e-112">Explore the Management APIs</span></span>](/python/api/overview/azure/notificationhubs/management)
