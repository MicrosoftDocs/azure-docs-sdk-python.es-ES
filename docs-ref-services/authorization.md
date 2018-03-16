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
ms.openlocfilehash: ba8814b22ee07a27181b214c6cc49607d4bc5d50
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2018
---
# <a name="azure-authorization-libraries-for-python"></a>Bibliotecas de Azure Authorization para Python

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[API de administración](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a>Creación del cliente de administración

El código siguiente crea una instancia del cliente de administración.

Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a>Comprobación de los permisos de un grupo de recursos

El código siguiente comprueba los permisos de un grupo de recursos determinado.
Para crear o administrar grupos de recursos, consulte [Administración de recursos](/python/api/overview/azure/azure.mgmt.resource).

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/authorization/management)

