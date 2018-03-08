---
title: "Nubes múltiples"
description: uso de Azure en todas las regiones
author: lmazuel
ms.author: lmazuel
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 48c6cc1872ef985641efc957a78e4b489f27ab56
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
---
# <a name="multi-cloud---use-azure-on-all-regions"></a><span data-ttu-id="9e69c-103">Nubes múltiples: uso de Azure en todas las regiones</span><span class="sxs-lookup"><span data-stu-id="9e69c-103">Multi-cloud - use Azure on all regions</span></span>

<span data-ttu-id="9e69c-104">Puede usar el SDK de Azure para Python para conectarse a todas las regiones en las que Azure está [disponible](https://azure.microsoft.com/regions/services).</span><span class="sxs-lookup"><span data-stu-id="9e69c-104">You can use the Azure SDK for Python to connect to all regions where Azure is [available](https://azure.microsoft.com/regions/services).</span></span>

<span data-ttu-id="9e69c-105">De forma predeterminada, el SDK de Azure para Python está configurado para conectarse a la nube pública de Azure.</span><span class="sxs-lookup"><span data-stu-id="9e69c-105">By default, the Azure SDK for Python is configured to connect to public Azure.</span></span>

## <a name="using-predeclared-cloud-definition"></a><span data-ttu-id="9e69c-106">Uso de la definición de nube previamente declarada</span><span class="sxs-lookup"><span data-stu-id="9e69c-106">Using predeclared cloud definition</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e69c-107">La versión del paquete `msrestazure` debe ser superior o igual a la 0.4.11 para esta sección.</span><span class="sxs-lookup"><span data-stu-id="9e69c-107">The `msrestazure` package must be superior or equals to 0.4.11 for this section.</span></span>

<span data-ttu-id="9e69c-108">Puede usar el módulo `azure_cloud` de `msrestazure`</span><span class="sxs-lookup"><span data-stu-id="9e69c-108">You can use the `azure_cloud` module of `msrestazure`</span></span>

```python
from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=AZURE_CHINA_CLOUD
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager
)
``` 
  
<span data-ttu-id="9e69c-109">Las definiciones de nube disponibles son</span><span class="sxs-lookup"><span data-stu-id="9e69c-109">Available cloud definition are</span></span>
  - <span data-ttu-id="9e69c-110">AZURE_PUBLIC_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9e69c-110">AZURE_PUBLIC_CLOUD</span></span>
  - <span data-ttu-id="9e69c-111">AZURE_CHINA_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9e69c-111">AZURE_CHINA_CLOUD</span></span>
  - <span data-ttu-id="9e69c-112">AZURE_US_GOV_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9e69c-112">AZURE_US_GOV_CLOUD</span></span>
  - <span data-ttu-id="9e69c-113">AZURE_GERMAN_CLOUD</span><span class="sxs-lookup"><span data-stu-id="9e69c-113">AZURE_GERMAN_CLOUD</span></span>

## <a name="using-your-own-cloud-definition-eg-azure-stack"></a><span data-ttu-id="9e69c-114">Con su propia definición de nube (por ejemplo, Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="9e69c-114">Using your own cloud definition (e.g. Azure Stack)</span></span>
<span data-ttu-id="9e69c-115">ARM tiene un punto de conexión de metadatos como ayuda:</span><span class="sxs-lookup"><span data-stu-id="9e69c-115">ARM has a metadata endpoint to help you:</span></span>

```python
from msrestazure.azure_cloud import get_cloud_from_metadata_endpoint
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

mystack_cloud = get_cloud_from_metadata_endpoint("https://myazurestack-arm-endpoint.com")
credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=mystack_cloud
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=mystack_cloud.endpoints.resource_manager
)
```
## <a name="using-adal"></a><span data-ttu-id="9e69c-116">Uso de ADAL</span><span class="sxs-lookup"><span data-stu-id="9e69c-116">Using ADAL</span></span>

<span data-ttu-id="9e69c-117">Hay algunas cosas a tener en cuenta para conectarse a otra región:</span><span class="sxs-lookup"><span data-stu-id="9e69c-117">To connect to another region, a few things have to be considered:</span></span>

- <span data-ttu-id="9e69c-118">¿Cuál es el punto de conexión donde se debe solicitar un token (autenticación)?</span><span class="sxs-lookup"><span data-stu-id="9e69c-118">What is the endpoint where to ask for a token (authentication)?</span></span>
- <span data-ttu-id="9e69c-119">¿Cuál es el punto de conexión donde se usará este token (uso)?</span><span class="sxs-lookup"><span data-stu-id="9e69c-119">What is the endpoint where I will use this token (usage)?</span></span>

<span data-ttu-id="9e69c-120">Este es un ejemplo genérico:</span><span class="sxs-lookup"><span data-stu-id="9e69c-120">This is a generic example:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password

# Public Azure - default values
authentication_endpoint = 'https://login.microsoftonline.com/'
azure_endpoint = 'https://management.azure.com/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-government"></a><span data-ttu-id="9e69c-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="9e69c-121">Azure Government</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password

# Government
authentication_endpoint = 'https://login-us.microsoftonline.com/'
azure_endpoint = 'https://management.usgovcloudapi.net/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-germany"></a><span data-ttu-id="9e69c-122">Azure Alemania</span><span class="sxs-lookup"><span data-stu-id="9e69c-122">Azure Germany</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password

# Azure Germany
authentication_endpoint = 'https://login.microsoftonline.de/'
azure_endpoint = 'https://management.microsoftazure.de/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-china"></a><span data-ttu-id="9e69c-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="9e69c-123">Azure China</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password

# Azure China
authentication_endpoint = 'https://login.chinacloudapi.cn/'
azure_endpoint = 'https://management.chinacloudapi.cn/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```