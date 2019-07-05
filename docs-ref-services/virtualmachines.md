---
title: Bibliotecas de Azure Virtual Machines para Python
description: ''
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: e09ffed98f3f6050e34ca2cb39e645e30f8bdb15
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534188"
---
# <a name="azure-virtual-machine-libraries"></a>Bibliotecas de Azure Virtual Machines

## <a name="overview"></a>Información general

Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.

Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).

## <a name="management-api"></a>API de administración

Cree, configure, administre y escale máquinas virtuales Windows y Linux en Azure desde su propio código con la API de administración.

Instale la biblioteca mediante pip.

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a>Ejemplo

Cree una nueva máquina virtual Linux en un grupo de recursos de Azure existente con la autenticación de Managed Service Identity (MSI).

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a>Ejemplos

* [Administración de máquinas virtuales][1]
* [Autenticación con Managed Service Identity ][2]
* [Creación de una máquina virtual con la extensión de identidad de servicio administrada][3]
* [Administración de un equilibrador de carga][4]
* [Creación y configuración de discos administrados][5]
* [Lista de imágenes][6] 
* [Supervisión de máquinas virtuales][7]

Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de ejemplos de máquina virtual.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
