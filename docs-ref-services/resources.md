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
ms.openlocfilehash: d8a27bc2b5480b07728a0b3f892f5c3c70c913d9
ms.sourcegitcommit: 427b44319ae99bf19e167f427e7681b2103dd8e4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/28/2017
---
# <a name="azure-resources-libraries-for-python"></a>Bibliotecas de Azure Resources para Python

## <a name="overview"></a>Información general 
Implemente, supervise y administre grupos de recursos con [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).

## <a name="management-api"></a>API de administración
Use la API de administración para crear grupos de recursos e implementar recursos desde plantillas.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>Ejemplo 
Cree un nuevo grupo de recursos en la región de Azure este de EE. UU.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagmentClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>Muestras
[Administración de recursos y grupos de recursos de Azure](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

Consulte la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) de ejemplos de Azure Resource Manager.
