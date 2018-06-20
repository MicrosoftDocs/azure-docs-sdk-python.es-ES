---
title: Bibliotecas de Azure DevTest Labs para Python
description: Referencia de las bibliotecas de Azure DevTest Labs para Python
keywords: Azure, python, SDK, API, DNS
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5807b85f02c05c2a767a2df2e89d9e98b7e6e05b
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551578"
---
# <a name="azure-devtest-labs-libraries-for-python"></a><span data-ttu-id="2f619-104">Bibliotecas de Azure DevTest Labs para Python</span><span class="sxs-lookup"><span data-stu-id="2f619-104">Azure DevTest Labs libraries for python</span></span>

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[<span data-ttu-id="2f619-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="2f619-105">Management API</span></span>](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a><span data-ttu-id="2f619-106">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="2f619-106">Create the management client</span></span>

<span data-ttu-id="2f619-107">El código siguiente crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="2f619-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="2f619-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="2f619-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="2f619-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="2f619-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.devtestlabs import DevTestLabsClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

devtestlabs_client = DevTestLabsClient(
    credentials,
    subscription_id
)
```

## <a name="create-lab"></a><span data-ttu-id="2f619-110">Creación del laboratorio</span><span class="sxs-lookup"><span data-stu-id="2f619-110">Create lab</span></span>

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
``` 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2f619-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="2f619-111">Explore the Management APIs</span></span>](/python/api/overview/azure/devtestlabs/management)