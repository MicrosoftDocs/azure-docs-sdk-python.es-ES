---
title: Bibliotecas del administrador del servidor de Azure para Python
description: Referencia del administrador del servidor de Azure para Python
keywords: Azure, python, SDK, API, Administrador del servidor
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 480513a76683c97fdac8d2a65b38fde0fffb6dcd
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479238"
---
# <a name="azure-server-manager-libraries-for-python"></a><span data-ttu-id="254c6-104">Bibliotecas del administrador del servidor de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="254c6-104">Azure Server Manager libraries for python</span></span>

## <a name="management-apipythonapioverviewazureservermanagermanagement"></a>[<span data-ttu-id="254c6-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="254c6-105">Management API</span></span>](/python/api/overview/azure/servermanager/management)

```bash
pip install azure-mgmt-servermanager
```

## <a name="create-the-management-client"></a><span data-ttu-id="254c6-106">Creación del cliente de administración</span><span class="sxs-lookup"><span data-stu-id="254c6-106">Create the management client</span></span>

<span data-ttu-id="254c6-107">El código siguiente crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="254c6-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="254c6-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en la [lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="254c6-108">You will need to provide your ``subscription_id`` which can be retrieved from your [subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="254c6-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="254c6-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.servermanager import ServerManagement
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

servermanager_client = ServerManagement(
    credentials,
    subscription_id
)
``` 

## <a name="create-gateway"></a><span data-ttu-id="254c6-110">Crear puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="254c6-110">Create gateway</span></span>
```python
gateway_async = servermanager_client.gateway.create(
    'MyResourceGroup',
    'MyGateway',
    'centralus'
)
gateway = gateway_async.result() # Blocking wait
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="254c6-111">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="254c6-111">Explore the Management APIs</span></span>](/python/api/overview/azure/servermanager/management)