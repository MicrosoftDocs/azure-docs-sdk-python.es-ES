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
# <a name="azure-key-vault-libraries-for-python"></a>Bibliotecas de Azure Key Vault para Python

[Azure Key Vault](/azure/key-vault/) es el sistema de almacenamiento y administración de Azure para las claves de cifrado, los secretos y la administración de certificados. La API del SDK de Python para Key Vault se divide entre las bibliotecas de cliente y las bibliotecas de administración.

Use la biblioteca cliente para:
- Acceder, actualizar o eliminar los elementos almacenados en Azure Key Vault.
- Obtener los metadatos de los certificados almacenados.
- Verificar las firmas con las claves simétricas en Key Vault.

Use la biblioteca de administración para:
- Crear, actualizar o eliminar nuevos almacenes de Key Vault.
- Controlar las directivas de acceso de Key Vault.
- Enumerar los almacenes por suscripción o grupo de recursos.
- Comprobar la disponibilidad del nombre del almacén.

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

### <a name="client-library"></a>Biblioteca de cliente

```bash
pip install azure-keyvault
```

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes usan la autenticación de entidad de servicio, que es el método de inicio de sesión recomendado para las aplicaciones que se conectan a Azure. Para más información acerca de la autenticación de entidad de servicio, consulte [Autenticación con el SDK de Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate).

Recuperar la parte pública de una clave asimétrica de un almacén:

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

Recuperar un secreto de un almacén:

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
> [Explorar las API de cliente](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>Biblioteca de administración

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se muestra cómo crear un almacén de claves de Azure Key Vault. 

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
> [Explorar las API de administración](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>Ejemplos
* [Administrar almacenes de Azure Key Vault][1] 
* [Recuperar almacenes de Azure Key Vault][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de ejemplos de Azure Key Vault. 
