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
---
# <a name="azure-devtest-labs-libraries-for-python"></a>Bibliotecas de Azure DevTest Labs para Python

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[API de administración](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a>Creación del cliente de administración

El código siguiente crea una instancia del cliente de administración.

Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).

Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.

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

## <a name="create-lab"></a>Creación del laboratorio

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
``` 

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/devtestlabs/management)