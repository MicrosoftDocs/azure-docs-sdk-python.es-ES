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
ms.assetid: 
ms.openlocfilehash: 1dba0bdd9b543c11b31f3001737038e7e99daf08
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="39929-104">Autenticación con las bibliotecas de administración de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="39929-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="39929-105">Hay varias opciones para autenticar la aplicación en Azure cuando se usan las bibliotecas de administración para Python para crear y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="39929-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <span data-ttu-id="39929-106"><a name="mgmt-auth-token"></a>Autenticación con credenciales de token</span><span class="sxs-lookup"><span data-stu-id="39929-106"><a name="mgmt-auth-token"></a>Authenticate with token credentials</span></span>

<span data-ttu-id="39929-107">Almacene las credenciales de forma segura en un archivo de configuración, el Registro o Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="39929-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="39929-108">En el ejemplo siguiente se usa una [entidad de servicio](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="39929-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="39929-109">Puede crear una entidad de servicio con la CLI de Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="39929-109">You can create a Service Principal via the Azure CLI 2.0</span></span>
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

> <span data-ttu-id="39929-110">[Nota] Para conectarse a una de las nubes soberanas de Azure, use el parámetro `cloud_environment`.</span><span class="sxs-lookup"><span data-stu-id="39929-110">[Note!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>

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

<span data-ttu-id="39929-111">Si necesita más control, se recomienda usar [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) y el contenedor ADAL del SDK.</span><span class="sxs-lookup"><span data-stu-id="39929-111">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="39929-112">Consulte el sitio web de ADAL para ver todos los ejemplos y la lista de escenarios disponibles.</span><span class="sxs-lookup"><span data-stu-id="39929-112">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="39929-113">Por ejemplo, para la autenticación de entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="39929-113">For instance for service principal authentication:</span></span>

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

<span data-ttu-id="39929-114">Se pueden usar todas las llamadas válidas a ADAL con la clase `AdalAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="39929-114">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="39929-115">Después, cree un objeto de cliente para empezar a trabajar con la API:</span><span class="sxs-lookup"><span data-stu-id="39929-115">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="39929-116">[Nota] Cuando se usa una nube soberana de Azure, debe especificar también la dirección URL base apropiada (mediante las constantes de `msrestazure.azure_cloud`) al crear el cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="39929-116">[Note!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="39929-117">Por ejemplo, para la nube de China de Azure:</span><span class="sxs-lookup"><span data-stu-id="39929-117">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.active_directory_resource_id)
> ```

## <span data-ttu-id="39929-118"><a name="mgmt-auth-file"></a>Autenticación basada en archivos</span><span class="sxs-lookup"><span data-stu-id="39929-118"><a name="mgmt-auth-file"></a>File based authentication</span></span>

<span data-ttu-id="39929-119">La manera más sencilla de autenticar es crear un archivo JSON que contenga las credenciales de una entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="39929-119">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="39929-120">Puede utilizar el siguiente comando de la CLI para crear una nueva entidad de servicio y este archivo al mismo tiempo:</span><span class="sxs-lookup"><span data-stu-id="39929-120">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="39929-121">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="39929-121">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="39929-122">Establezca una variable de entorno con la ruta de acceso completa al archivo en el shell:</span><span class="sxs-lookup"><span data-stu-id="39929-122">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="39929-123">Si desea crear el archivo por sí mismo, siga este formato:</span><span class="sxs-lookup"><span data-stu-id="39929-123">If you want to create the file yourself, please follow this format:</span></span>

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

<span data-ttu-id="39929-124">A continuación, puede crear cualquier cliente mediante la factoría de clientes:</span><span class="sxs-lookup"><span data-stu-id="39929-124">You can then create any client using the client factory:</span></span>
```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```


## <span data-ttu-id="39929-125"><a name="mgmt-auth-cli"></a>Autenticación basada en la CLI</span><span class="sxs-lookup"><span data-stu-id="39929-125"><a name="mgmt-auth-cli"></a>CLI-based authentication</span></span>

<span data-ttu-id="39929-126">El SDK es capaz de crear un cliente con su suscripción activa de la CLI.</span><span class="sxs-lookup"><span data-stu-id="39929-126">The SDK is able to create a client using your CLI active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39929-127">Esto se debe usar como inicio rápido a la experiencia del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="39929-127">This should be used as quick start developer experience.</span></span> <span data-ttu-id="39929-128">Con fines de producción, use [ADAL](#authenticate-with-token-credentials) o su propio sistema de credenciales.</span><span class="sxs-lookup"><span data-stu-id="39929-128">For production purposes, use [ADAL](#authenticate-with-token-credentials) or your own credentials system.</span></span>
> <span data-ttu-id="39929-129">Cualquier cambio en la configuración de la CLI afectará a la ejecución del SDK.</span><span class="sxs-lookup"><span data-stu-id="39929-129">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="39929-130">Para definir las credenciales activas, utilice [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39929-130">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="39929-131">El identificador predeterminado de la suscripción puede ser el que ya tiene o puede definirlo con [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="39929-131">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <span data-ttu-id="39929-132"><a name="mgmt-auth-legacy"></a>Autenticación con credenciales de token (heredado)</span><span class="sxs-lookup"><span data-stu-id="39929-132"><a name="mgmt-auth-legacy"></a>Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="39929-133">En versiones anteriores del SDK, ADAL aún no estaba disponible y se proporciona una clase `UserPassCredentials`.</span><span class="sxs-lookup"><span data-stu-id="39929-133">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="39929-134">Esto se considera en desuso y no debe usarse más.</span><span class="sxs-lookup"><span data-stu-id="39929-134">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="39929-135">Este ejemplo muestra el escenario de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="39929-135">This sample shows user/password scenario.</span></span> <span data-ttu-id="39929-136">No admite la autenticación de doble factor.</span><span class="sxs-lookup"><span data-stu-id="39929-136">This does not support 2FA.</span></span>

```python
    from azure.common.credentials import UserPassCredentials

    credentials = UserPassCredentials(
        'user@domain.com',
        'my_smart_password',
    )
```