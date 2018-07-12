---
title: Bibliotecas de Azure Key Vault para Python
description: Documentación de referencia de las bibliotecas de cliente de Python para Azure Key Vault
author: lisawong19
keywords: Azure, Python, SDK, API, claves, Key Vault, autenticación, secreto, clave, seguridad
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 555f55dcf7355a1a82dc3ca5826e0d0bd3fad414
ms.sourcegitcommit: 8476146ae9bcd1533db47adbe2524b27b93aaba0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2018
ms.locfileid: "37925946"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="057e7-104">Bibliotecas de Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="057e7-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="057e7-105">Información general</span><span class="sxs-lookup"><span data-stu-id="057e7-105">Overview</span></span>

<span data-ttu-id="057e7-106">Cree, actualice y elimine claves y secretos en Azure Key Vault con las bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="057e7-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="057e7-107">Uso de las bibliotecas de administración de Azure Key Vault para crear almacenes de claves, autorizar aplicaciones y administrar permisos.</span><span class="sxs-lookup"><span data-stu-id="057e7-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="057e7-108">Obtenga más información sobre [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span><span class="sxs-lookup"><span data-stu-id="057e7-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="057e7-109">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="057e7-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="057e7-110">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="057e7-110">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="057e7-111">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="057e7-111">Examples</span></span>

<span data-ttu-id="057e7-112">Recupere una [clave de web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) desde un almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="057e7-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```

<span data-ttu-id="057e7-113">De forma similar, puede utilizar el siguiente fragmento de código para recuperar un secreto desde el almacén:</span><span class="sxs-lookup"><span data-stu-id="057e7-113">Similarly, you can use the following snippet to retrieve a secret from the vault:</span></span>

```
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret("https://VAULT_ID.vault.azure.net/", "SECRET_ID", "SECRET_VERSION")

print(secret_bundle.value)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="057e7-114">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="057e7-114">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a><span data-ttu-id="057e7-115">API de administración</span><span class="sxs-lookup"><span data-stu-id="057e7-115">Management API</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="057e7-116">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="057e7-116">Example</span></span>
<span data-ttu-id="057e7-117">En el ejemplo siguiente se muestra cómo crear un almacén de claves de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="057e7-117">The following example shows how to create an Azure Key Vault.</span></span> 

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
> [<span data-ttu-id="057e7-118">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="057e7-118">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

> [!div class="nextstepaction"]
> [<span data-ttu-id="057e7-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="057e7-119">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="057e7-120">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="057e7-120">Samples</span></span>
* <span data-ttu-id="057e7-121">[Administración de almacenes de claves][1]</span><span class="sxs-lookup"><span data-stu-id="057e7-121">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="057e7-122">[Recuperación de almacenes de claves][2]</span><span class="sxs-lookup"><span data-stu-id="057e7-122">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="057e7-123">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de ejemplos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="057e7-123">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
