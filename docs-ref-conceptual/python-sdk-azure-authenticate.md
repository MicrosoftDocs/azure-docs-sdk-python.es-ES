---
title: Autenticación con las bibliotecas de administración de Azure para Python
description: Autentique con una entidad de servicio en las bibliotecas de administración de Azure para Python.
keywords: Azure, Python, SDK, API, autenticación, active directory, entidad de servicio
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/11/2019
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51f26b120cefffd2d7f4af9c2b6b2cb532bc6006
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586813"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="63608-104">Autenticación con las bibliotecas de administración de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="63608-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="63608-105">Hay varias opciones para autenticar la aplicación en Azure cuando se usan las bibliotecas de administración para Python para crear y administrar recursos.</span><span class="sxs-lookup"><span data-stu-id="63608-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="63608-106">Autenticación con credenciales de token</span><span class="sxs-lookup"><span data-stu-id="63608-106">Authenticate with token credentials</span></span>

<span data-ttu-id="63608-107">Almacene las credenciales de forma segura en un archivo de configuración, el Registro o Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="63608-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="63608-108">En el ejemplo siguiente se usa una [entidad de servicio](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="63608-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="63608-109">Para crear una entidad de servicio con la CLI de Azure, use el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="63608-109">To create a service principal with the Azure CLI, use the following command:</span></span>
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> <span data-ttu-id="63608-110">Para más información sobre cómo configurar entidades de servicio con la CLI, consulte [Creación de una entidad de servicio de Azure con la CLI de Azure](/cli/azure/create-an-azure-service-principal-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="63608-110">To learn more about setting up service princpals with the CLI, see [Create an Azure service principal with Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials

# Tenant ID for your Azure subscription
TENANT_ID = '<Your tenant ID>'

# Your service principal App ID
CLIENT = '<Your service principal ID>'

# Your service principal password
KEY = '<Your service principal password>'

credentials = ServicePrincipalCredentials(
    client_id = CLIENT,
    secret = KEY,
    tenant = TENANT_ID
)
```

> <span data-ttu-id="63608-111">[NOTA] Para conectarse a una de las nubes soberanas de Azure, use el parámetro `cloud_environment`.</span><span class="sxs-lookup"><span data-stu-id="63608-111">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>
>
> ```python
> from azure.common.credentials import ServicePrincipalCredentials
> from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
> 
> # Tenant ID for your Azure Subscription
> TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
> 
> # Your Service Principal App ID
> CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'
> 
> # Your Service Principal Password
> KEY = 'password'
> 
> credentials = ServicePrincipalCredentials(
>     client_id = CLIENT,
>     secret = KEY,
>     tenant = TENANT_ID,
>     cloud_environment = AZURE_CHINA_CLOUD
> )
> ```

<span data-ttu-id="63608-112">Si necesita más control, se recomienda usar [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) y el contenedor ADAL del SDK.</span><span class="sxs-lookup"><span data-stu-id="63608-112">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="63608-113">Consulte el sitio web de ADAL para ver todos los ejemplos y la lista de escenarios disponibles.</span><span class="sxs-lookup"><span data-stu-id="63608-113">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="63608-114">Por ejemplo, para la autenticación de entidad de servicio:</span><span class="sxs-lookup"><span data-stu-id="63608-114">For instance for service principal authentication:</span></span>

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

<span data-ttu-id="63608-115">Se pueden usar todas las llamadas válidas a ADAL con la clase `AdalAuthentication`.</span><span class="sxs-lookup"><span data-stu-id="63608-115">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="63608-116">Después, cree un objeto de cliente para empezar a trabajar con la API:</span><span class="sxs-lookup"><span data-stu-id="63608-116">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="63608-117">[NOTA] Cuando se usa una nube soberana de Azure, debe especificar también la dirección URL base apropiada (mediante las constantes de `msrestazure.azure_cloud`) al crear el cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="63608-117">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="63608-118">Por ejemplo, para la nube de China de Azure:</span><span class="sxs-lookup"><span data-stu-id="63608-118">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="63608-119">Autenticación basada en archivos</span><span class="sxs-lookup"><span data-stu-id="63608-119">File based authentication</span></span>

<span data-ttu-id="63608-120">La manera más sencilla de autenticar es crear un archivo JSON que contenga las credenciales de una entidad de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="63608-120">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="63608-121">Puede utilizar el siguiente comando de la CLI para crear una nueva entidad de servicio y este archivo al mismo tiempo:</span><span class="sxs-lookup"><span data-stu-id="63608-121">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="63608-122">Guarde este archivo en una ubicación segura en el sistema donde el código pueda leerlo.</span><span class="sxs-lookup"><span data-stu-id="63608-122">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="63608-123">Establezca una variable de entorno con la ruta de acceso completa al archivo en el shell:</span><span class="sxs-lookup"><span data-stu-id="63608-123">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="63608-124">Si desea crear el archivo por sí mismo, siga este formato:</span><span class="sxs-lookup"><span data-stu-id="63608-124">If you want to create the file yourself, please follow this format:</span></span>

```json
{
    "clientId": "<Service principal ID>",
    "clientSecret": "<Service principal secret/password>",
    "subscriptionId": "<Subscription associated with the service principal>",
    "tenantId": "<The service principal's tenant>",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="63608-125">A continuación, puede crear cualquier cliente mediante la factoría de clientes:</span><span class="sxs-lookup"><span data-stu-id="63608-125">You can then create any client using the client factory:</span></span>

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="63608-126">Autenticación con identidades administradas de Azure</span><span class="sxs-lookup"><span data-stu-id="63608-126">Authenticate with Azure Managed Identities</span></span>
<span data-ttu-id="63608-127">Las identidades administradas de Azure son una manera sencilla para que un recurso de Azure pueda usar el SDK o la CLI sin necesidad de crear credenciales específicas.</span><span class="sxs-lookup"><span data-stu-id="63608-127">Azure Managed Identity is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="63608-128">Para usar identidades administradas, debe conectarse a Azure desde un recurso de Azure, como una función de Azure o una máquina virtual que se ejecuta en Azure.</span><span class="sxs-lookup"><span data-stu-id="63608-128">To use managed identities, you must be connecting to Azure from an Azure resource, such as an Azure Function or a VM running in Azure.</span></span> <span data-ttu-id="63608-129">Para más información acerca de cómo configurar una identidad administrada para un recurso, consulte [Configuración de identidades administradas para recursos de Azure](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) y [Uso de identidades administradas para recursos de Azure](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span><span class="sxs-lookup"><span data-stu-id="63608-129">To learn how to configure a managed identity for a resource, see [Configure managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) and [How to use managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span></span>

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

## <a name="mgmt-auth-cli"></a><span data-ttu-id="63608-130">Autenticación basada en la CLI</span><span class="sxs-lookup"><span data-stu-id="63608-130">CLI-based authentication</span></span>

<span data-ttu-id="63608-131">El SDK puede crear un cliente con la suscripción activa de la CLI de Azure.</span><span class="sxs-lookup"><span data-stu-id="63608-131">The SDK is able to create a client using the Azure CLI's active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63608-132">Esto se debe usar como inicio rápido a la experiencia del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="63608-132">This should be used as quick start developer experience.</span></span> <span data-ttu-id="63608-133">Con fines de producción, use [ADAL](#mgmt-auth-legacy) o su propio sistema de credenciales.</span><span class="sxs-lookup"><span data-stu-id="63608-133">For production purposes, use [ADAL](#mgmt-auth-legacy) or your own credentials system.</span></span>
> <span data-ttu-id="63608-134">Cualquier cambio en la configuración de la CLI afectará a la ejecución del SDK.</span><span class="sxs-lookup"><span data-stu-id="63608-134">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="63608-135">Para definir las credenciales activas, utilice [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="63608-135">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="63608-136">El identificador predeterminado de la suscripción puede ser el que ya tiene o puede definirlo con [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="63608-136">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="63608-137">Autenticación con credenciales de token (heredado)</span><span class="sxs-lookup"><span data-stu-id="63608-137">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="63608-138">En versiones anteriores del SDK, ADAL aún no estaba disponible y se proporciona una clase `UserPassCredentials`.</span><span class="sxs-lookup"><span data-stu-id="63608-138">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="63608-139">Esto se considera en desuso y no debe usarse más.</span><span class="sxs-lookup"><span data-stu-id="63608-139">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="63608-140">Este ejemplo muestra el escenario de usuario y contraseña.</span><span class="sxs-lookup"><span data-stu-id="63608-140">This sample shows user/password scenario.</span></span> <span data-ttu-id="63608-141">No admite la autenticación de doble factor.</span><span class="sxs-lookup"><span data-stu-id="63608-141">This does not support 2FA.</span></span>

```python
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
    'user@domain.com',
    'my_smart_password'
)
```
