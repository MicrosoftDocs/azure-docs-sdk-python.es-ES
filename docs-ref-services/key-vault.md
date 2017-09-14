---
title: Bibliotecas de Azure Key Vault para Python
description: "Documentación de referencia de las bibliotecas de cliente de Python para Azure Key Vault"
author: lisawong19
keywords: "Azure, Python, SDK, API, claves, Key Vault, autenticación, secreto, clave, seguridad"
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3eac46eb4d5d19273ead9f19b739f6fb6d72e5cc
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="18abe-104">Bibliotecas de Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="18abe-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="18abe-105">Información general</span><span class="sxs-lookup"><span data-stu-id="18abe-105">Overview</span></span>

<span data-ttu-id="18abe-106">Cree, actualice y elimine claves y secretos en Azure Key Vault con las bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="18abe-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="18abe-107">Uso de las bibliotecas de administración de Azure Key Vault para crear almacenes de claves, autorizar aplicaciones y administrar permisos.</span><span class="sxs-lookup"><span data-stu-id="18abe-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="18abe-108">Obtenga más información sobre [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="18abe-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="18abe-109">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="18abe-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="18abe-110">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="18abe-110">Client library</span></span>
```bash
pip install azure-keyvault
```

## <a name="example"></a><span data-ttu-id="18abe-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="18abe-111">Example</span></span>
<span data-ttu-id="18abe-112">Recupere una [clave de web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) desde un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="18abe-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callack(server, resource, scope):
    credentials = credentials or ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = resource
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callack))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```
[!div class="nextstepaction"]
[<span data-ttu-id="18abe-113">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="18abe-113">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/clientlibrary)

### <a name="management-api"></a><span data-ttu-id="18abe-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="18abe-114">Management API</span></span>
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="18abe-115">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="18abe-115">Example</span></span>
<span data-ttu-id="18abe-116">En el ejemplo siguiente se muestra cómo crear un almacén de claves de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="18abe-116">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'

kv_client = KeyVaultManagementClient(credentials, subscription_id)

vault = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': os.environ['AZURE_TENANT_ID'],
            'access_policies': [{
                'tenant_id': os.environ['AZURE_TENANT_ID'],
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="18abe-117">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="18abe-117">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="18abe-118">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="18abe-118">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a><span data-ttu-id="18abe-119">Muestras</span><span class="sxs-lookup"><span data-stu-id="18abe-119">Samples</span></span>
* <span data-ttu-id="18abe-120">[Administración de almacenes de claves][1]</span><span class="sxs-lookup"><span data-stu-id="18abe-120">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="18abe-121">[Recuperación de almacenes de claves][2]</span><span class="sxs-lookup"><span data-stu-id="18abe-121">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="18abe-122">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de ejemplos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="18abe-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 