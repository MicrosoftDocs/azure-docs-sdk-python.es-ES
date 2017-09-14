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
# <a name="azure-network-libraries-for-python"></a>Bibliotecas de Azure Virtual Network para Python

## <a name="overview"></a>Información general

[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) permite conectarse a los recursos de Azure, así como conectarlos a la red local.

Para empezar a trabajar con Azure Virtual Network, consulte [Creación de su primera red virtual](/azure/virtual-network/virtual-network-get-started-vnet-subnet).

## <a name="management-apis"></a>API de administración

Inspeccione, administre y configure redes virtuales de Azure con las API de administración.

A diferencia de otras API de Azure para Python, las versiones de las API de red están explícitamente divididas en paquetes separados. No es necesario importarlas individualmente porque la información del paquete se especifica en el constructor del cliente.

Instale el paquete de administración con pip.

```bash
pip install azure-mgmt-network
```

### <a name="example"></a>Ejemplo

Cree una red virtual y una subred asociada.

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
> [Explorar las API de administración](/python/api/overview/azure/network/managementlibrary)

### <a name="samples"></a>Muestras

* [Introducción a los equilibradores de carga en Azure Resource Manager para Python][1]

Vea la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) de ejemplos de Azure Virtual Network.

[1]: [https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/]
