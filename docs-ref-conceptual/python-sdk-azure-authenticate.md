---
title: "Autenticación con las bibliotecas de administración de Azure para Python"
description: "Autentique con una entidad de servicio en las bibliotecas de administración de Azure para Python."
keywords: "Azure, Python, SDK, API, autenticación, active directory, entidad de servicio"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/24/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 271722eee1ef982d1f091b3d3af29069917f3e17
ms.sourcegitcommit: 97e5d660eb4a006f969c3010087e1386cc6eb482
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/14/2018
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a>Autenticación con las bibliotecas de administración de Azure para Python

Hay varias opciones para autenticar la aplicación en Azure cuando se usan las bibliotecas de administración para Python para crear y administrar recursos.

## <a name="mgmt-auth-token"></a>Autenticación con credenciales de token

Almacene las credenciales de forma segura en un archivo de configuración, el Registro o Azure Key Vault.

En el ejemplo siguiente se usa una [entidad de servicio](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) para la autenticación.

> [!NOTE]
> Puede crear una entidad de servicio con la CLI de Azure 2.0
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```

```python
    from azure.common.credentials import ServicePrincipalCredentials

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID
    )
```

> [NOTA] Para conectarse a una de las nubes soberanas de Azure, use el parámetro `cloud_environment`.

```python
    from azure.common.credentials import ServicePrincipalCredentials
    from msrestazure.azure_cloud import AZURE_CHINA_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    credentials = ServicePrincipalCredentials(
        client_id = CLIENT,
        secret = KEY,
        tenant = TENANT_ID,
        cloud_environment = AZURE_CHINA_CLOUD
    )
```

Si necesita más control, se recomienda usar [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) y el contenedor ADAL del SDK. Consulte el sitio web de ADAL para ver todos los ejemplos y la lista de escenarios disponibles. Por ejemplo, para la autenticación de entidad de servicio:

```python
    import adal
    from msrestazure.azure_active_directory import AdalAuthentication
    from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD

    # Tenant ID for your Azure Subscription
    TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

    # Your Service Principal App ID
    CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

    # Your Service Principal Password
    KEY = 'password'

    LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
    RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

    context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
    credentials = AdalAuthentication(
        context.acquire_token_with_client_credentials,
        RESOURCE,
        CLIENT,
        KEY
    )
```

Se pueden usar todas las llamadas válidas a ADAL con la clase `AdalAuthentication`.

Después, cree un objeto de cliente para empezar a trabajar con la API:

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> [NOTA] Cuando se usa una nube soberana de Azure, debe especificar también la dirección URL base apropiada (mediante las constantes de `msrestazure.azure_cloud`) al crear el cliente de administración. Por ejemplo, para la nube de China de Azure:
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a>Autenticación basada en archivos

La manera más sencilla de autenticar es crear un archivo JSON que contenga las credenciales de una entidad de servicio de Azure. Puede utilizar el siguiente comando de la CLI para crear una nueva entidad de servicio y este archivo al mismo tiempo:

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo. Establezca una variable de entorno con la ruta de acceso completa al archivo en el shell:

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

Si desea crear el archivo por sí mismo, siga este formato:

```json
{
    "clientId": "ad735158-65ca-11e7-ba4d-ecb1d756380e",
    "clientSecret": "b70bb224-65ca-11e7-810c-ecb1d756380e",
    "subscriptionId": "bfc42d3a-65ca-11e7-95cf-ecb1d756380e",
    "tenantId": "c81da1d8-65ca-11e7-b1d1-ecb1d756380e",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

A continuación, puede crear cualquier cliente mediante la factoría de clientes:
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a>Autenticación con Managed Service Identity (MSI) 
MSI es una manera sencilla para que un recurso de Azure pueda usar el SDK o la CLI sin necesidad de crear credenciales específicas.

```python
from msrestazure.azure_active_directory import MSIAuthentication
from azure.mgmt.resource import ResourceManagementClient, SubscriptionClient

    # Create MSI Authentication
    credentials = MSIAuthentication()


    # Create a Subscription Client
    subscription_client = SubscriptionClient(credentials)
    subscription = next(subscription_client.subscriptions.list())
    subscription_id = subscription.subscription_id

    # Create a Resource Management client
    resource_client = ResourceManagementClient(credentials, subscription_id)

    
    # List resource groups as an example. The only limit is what role and policy are assigned to this MSI token.
    for resource_group in resource_client.resource_groups.list():
        print(resource_group.name)

```

## <a name="mgmt-auth-cli"></a>Autenticación basada en la CLI

El SDK es capaz de crear un cliente con su suscripción activa de la CLI.

> [!IMPORTANT]
> Esto se debe usar como inicio rápido a la experiencia del desarrollador. Con fines de producción, use [ADAL](#authenticate-with-token-credentials) o su propio sistema de credenciales.
> Cualquier cambio en la configuración de la CLI afectará a la ejecución del SDK.

Para definir las credenciales activas, utilice [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).
El identificador predeterminado de la suscripción puede ser el que ya tiene o puede definirlo con [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a>Autenticación con credenciales de token (heredado)

En versiones anteriores del SDK, ADAL aún no estaba disponible y se proporciona una clase `UserPassCredentials`. Esto se considera en desuso y no debe usarse más.

Este ejemplo muestra el escenario de usuario y contraseña. No admite la autenticación de doble factor.

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password',
    )
```
