---
title: Bibliotecas de Azure Resources para Python
description: Referencia de las bibliotecas de Azure Resources para Python
keywords: Azure, python, SDK, API, Resources
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: d924a8aea18d9b59ec8c78d85dce8fe0ce7c8d6c
ms.sourcegitcommit: d521a7350216461eb2fa68152c4975f55152f831
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/06/2017
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="ee3e1-104">Bibliotecas de Azure Resources para Python</span><span class="sxs-lookup"><span data-stu-id="ee3e1-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="ee3e1-105">Información general</span><span class="sxs-lookup"><span data-stu-id="ee3e1-105">Overview</span></span> 
<span data-ttu-id="ee3e1-106">Implemente, supervise y administre grupos de recursos con [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="ee3e1-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="ee3e1-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="ee3e1-107">Management API</span></span>
<span data-ttu-id="ee3e1-108">Use la API de administración para crear grupos de recursos e implementar recursos desde plantillas.</span><span class="sxs-lookup"><span data-stu-id="ee3e1-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="ee3e1-109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="ee3e1-109">Example</span></span> 
<span data-ttu-id="ee3e1-110">Cree un nuevo grupo de recursos en la región de Azure este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="ee3e1-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="ee3e1-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="ee3e1-111">Explore the Management APIs</span></span>](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a><span data-ttu-id="ee3e1-112">Muestras</span><span class="sxs-lookup"><span data-stu-id="ee3e1-112">Samples</span></span>
[<span data-ttu-id="ee3e1-113">Administración de recursos y grupos de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="ee3e1-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="ee3e1-114">Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) de ejemplos de Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee3e1-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
