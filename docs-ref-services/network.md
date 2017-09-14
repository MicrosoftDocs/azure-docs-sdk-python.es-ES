---
title: Bibliotecas de Azure Virtual Network para Python
description: Referencia de las bibliotecas de Azure Virtual Network para Python
keywords: Azure, python, SDK, API, Virtual Network
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: ed6ddfe4d1f4d860952369a75e10166a1f22c483
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-network-libraries-for-python"></a><span data-ttu-id="4c81e-104">Bibliotecas de Azure Virtual Network para Python</span><span class="sxs-lookup"><span data-stu-id="4c81e-104">Azure Network libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="4c81e-105">Información general</span><span class="sxs-lookup"><span data-stu-id="4c81e-105">Overview</span></span>

<span data-ttu-id="4c81e-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) permite conectarse a los recursos de Azure, así como conectarlos a la red local.</span><span class="sxs-lookup"><span data-stu-id="4c81e-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows you to connect Azure resources, and also connect them to your on-premises network.</span></span>

<span data-ttu-id="4c81e-107">Para empezar a trabajar con Azure Virtual Network, consulte [Creación de su primera red virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span><span class="sxs-lookup"><span data-stu-id="4c81e-107">To get started with Azure Virtual Network, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-apis"></a><span data-ttu-id="4c81e-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="4c81e-108">Management APIs</span></span>

<span data-ttu-id="4c81e-109">Inspeccione, administre y configure redes virtuales de Azure con las API de administración.</span><span class="sxs-lookup"><span data-stu-id="4c81e-109">Inspect, manage, and configure Azure virtual networks with the management APIs.</span></span>

<span data-ttu-id="4c81e-110">A diferencia de otras API de Azure para Python, las versiones de las API de red están explícitamente divididas en paquetes separados.</span><span class="sxs-lookup"><span data-stu-id="4c81e-110">Unlike other Azure python APIs, the networking APIs are explicitly versioned into separage packages.</span></span> <span data-ttu-id="4c81e-111">No es necesario importarlas individualmente porque la información del paquete se especifica en el constructor del cliente.</span><span class="sxs-lookup"><span data-stu-id="4c81e-111">You do not need to import them individually since the package information is specified in the client constructor.</span></span>

<span data-ttu-id="4c81e-112">Instale el paquete de administración con pip.</span><span class="sxs-lookup"><span data-stu-id="4c81e-112">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-network
```

### <a name="example"></a><span data-ttu-id="4c81e-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="4c81e-113">Example</span></span>

<span data-ttu-id="4c81e-114">Cree una red virtual y una subred asociada.</span><span class="sxs-lookup"><span data-stu-id="4c81e-114">Create a virtual network and an associated subnet.</span></span>

```python
from azure.mgmt.network import NetworkManagementClient

GROUP_NAME = 'resource-group'
VNET_NAME = 'your-vnet-identifier'
LOCATION = 'region'
SUBNET_NAME = 'your-subnet-identifier'

network_client = NetworkManagementClient(credentials, 'your-subscription-id')

async_vnet_creation = network_client.virtual_networks.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    {
        'location': LOCATION,
        'address_space': {
            'address_prefixes': ['10.0.0.0/16']
        }
    }
)
async_vnet_creation.wait()

# Create Subnet
async_subnet_creation = network_client.subnets.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    SUBNET_NAME,
    {'address_prefix': '10.0.0.0/24'}
)
subnet_info = async_subnet_creation.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c81e-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="4c81e-115">Explore the Management APIs</span></span>](/python/api/overview/azure/network/managementlibrary)

### <a name="samples"></a><span data-ttu-id="4c81e-116">Muestras</span><span class="sxs-lookup"><span data-stu-id="4c81e-116">Samples</span></span>

* <span data-ttu-id="4c81e-117">[Introducción a los equilibradores de carga en Azure Resource Manager para Python][1]</span><span class="sxs-lookup"><span data-stu-id="4c81e-117">[Getting started with Azure Resource Manager for load balancers in Python][1]</span></span>

<span data-ttu-id="4c81e-118">Vea la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) de ejemplos de Azure Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="4c81e-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) of Azure Virtual Network samples.</span></span>

[1]: [https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/]