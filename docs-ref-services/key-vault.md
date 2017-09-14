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
# <a name="azure-key-vault-libraries-for-python"></a>Bibliotecas de Azure Key Vault para Python

## <a name="overview"></a>Información general

Cree, actualice y elimine claves y secretos en Azure Key Vault con las bibliotecas de cliente.

Uso de las bibliotecas de administración de Azure Key Vault para crear almacenes de claves, autorizar aplicaciones y administrar permisos. 

Obtenga más información sobre [Azure Key Vault](/azure/key-vault/key-vault-whatis).

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

### <a name="client-library"></a>Biblioteca de cliente
```bash
pip install azure-keyvault
```

## <a name="example"></a>Ejemplo
Recupere una [clave de web JSON](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) desde un almacén de claves.

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
[Explorar las API de cliente](/python/api/overview/azure/keyvault/clientlibrary)

### <a name="management-api"></a>API de administración
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>Ejemplo
En el ejemplo siguiente se muestra cómo crear un almacén de claves de Azure Key Vault. 

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
> [Explorar las API de administración](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a>Muestras
* [Administración de almacenes de claves][1] 
* [Recuperación de almacenes de claves][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) de ejemplos de Azure Key Vault. 