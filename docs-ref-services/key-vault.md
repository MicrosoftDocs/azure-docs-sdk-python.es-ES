---
title: Bibliotecas de Azure Key Vault para Python
description: Documentación de referencia de las bibliotecas de cliente de Python para Azure Key Vault
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149335"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="bbbc9-103">Bibliotecas de Azure Key Vault para Python</span><span class="sxs-lookup"><span data-stu-id="bbbc9-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="bbbc9-104">[Azure Key Vault](/azure/key-vault/) es el sistema de almacenamiento y administración de Azure para las claves de cifrado, los secretos y la administración de certificados.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="bbbc9-105">La API del SDK de Python para Key Vault se divide entre las bibliotecas de cliente y las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="bbbc9-106">Use la biblioteca cliente para:</span><span class="sxs-lookup"><span data-stu-id="bbbc9-106">Use the client library to:</span></span>
- <span data-ttu-id="bbbc9-107">Acceder, actualizar o eliminar los elementos almacenados en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="bbbc9-108">Obtener los metadatos de los certificados almacenados.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="bbbc9-109">Verificar las firmas con las claves simétricas en Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="bbbc9-110">Use la biblioteca de administración para:</span><span class="sxs-lookup"><span data-stu-id="bbbc9-110">Use the management library to:</span></span>
- <span data-ttu-id="bbbc9-111">Crear, actualizar o eliminar nuevos almacenes de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="bbbc9-112">Controlar las directivas de acceso de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-112">Control vault access policies</span></span>
- <span data-ttu-id="bbbc9-113">Enumerar los almacenes por suscripción o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="bbbc9-114">Comprobar la disponibilidad del nombre del almacén.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="bbbc9-115">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="bbbc9-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="bbbc9-116">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="bbbc9-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="bbbc9-117">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbbc9-117">Examples</span></span>

<span data-ttu-id="bbbc9-118">Los ejemplos siguientes usan la autenticación de entidad de servicio, que es el método de inicio de sesión recomendado para las aplicaciones que se conectan a Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="bbbc9-119">Para más información acerca de la autenticación de entidad de servicio, consulte [Autenticación con el SDK de Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="bbbc9-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="bbbc9-120">Recuperar la parte pública de una clave asimétrica de un almacén:</span><span class="sxs-lookup"><span data-stu-id="bbbc9-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

<span data-ttu-id="bbbc9-121">Recuperar un secreto de un almacén:</span><span class="sxs-lookup"><span data-stu-id="bbbc9-121">Retrieve a secret from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbbc9-122">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="bbbc9-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="bbbc9-123">Biblioteca de administración</span><span class="sxs-lookup"><span data-stu-id="bbbc9-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="bbbc9-124">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="bbbc9-124">Example</span></span>

<span data-ttu-id="bbbc9-125">En el ejemplo siguiente se muestra cómo crear un almacén de claves de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-125">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="bbbc9-126">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="bbbc9-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="bbbc9-127">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="bbbc9-127">Samples</span></span>
* <span data-ttu-id="bbbc9-128">[Administrar almacenes de Azure Key Vault][1]</span><span class="sxs-lookup"><span data-stu-id="bbbc9-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="bbbc9-129">[Recuperar almacenes de Azure Key Vault][2]</span><span class="sxs-lookup"><span data-stu-id="bbbc9-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="bbbc9-130">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de ejemplos de Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="bbbc9-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
