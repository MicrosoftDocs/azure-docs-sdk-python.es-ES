---
title: Bibliotecas de Azure Authorization para Python
description: Referencia de las bibliotecas de Azure Authorization para Python
keywords: Azure, python, SDK, API, Authorization
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 8709bbd3cff448c7beb394621b163a4b3e3c3cd8
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276769"
---
# <a name="azure-authorization-libraries-for-python"></a><span data-ttu-id="fe5b1-104">Bibliotecas de Azure Authorization para Python</span><span class="sxs-lookup"><span data-stu-id="fe5b1-104">Azure Authorization libraries for python</span></span>

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[<span data-ttu-id="fe5b1-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="fe5b1-105">Management API</span></span>](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a><span data-ttu-id="fe5b1-106">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="fe5b1-106">Create the management client</span></span>

<span data-ttu-id="fe5b1-107">El siguiente código crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="fe5b1-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="fe5b1-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a><span data-ttu-id="fe5b1-110">Comprobación de los permisos de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="fe5b1-110">Check permissions for a resource group</span></span>

<span data-ttu-id="fe5b1-111">El código siguiente comprueba los permisos de un grupo de recursos determinado.</span><span class="sxs-lookup"><span data-stu-id="fe5b1-111">The following code checks permissions in a given resource group.</span></span>
<span data-ttu-id="fe5b1-112">Para crear o administrar grupos de recursos, consulte [Administración de recursos](/python/api/overview/azure/azure.mgmt.resource).</span><span class="sxs-lookup"><span data-stu-id="fe5b1-112">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="fe5b1-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="fe5b1-113">Explore the Management APIs</span></span>](/python/api/overview/azure/authorization/management)

