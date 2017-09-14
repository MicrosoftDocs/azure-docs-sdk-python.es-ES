---
title: Bibliotecas de Azure Virtual Machines para Python
description: 
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: c25665e19adb44c7112bf1533097ce1e6c739cb8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
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

Cree una nueva máquina virtual Linux en un grupo de recursos de Azure existente.

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
> [Explorar las API de administración](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a>Muestras

* [Administración de máquinas virtuales][1]
* [Administración de un equilibrador de carga][2]
* [Creación y configuración de discos administrados][3]
* [Lista de imágenes][4] 
* [Supervisión de máquinas virtuales][5]

Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de ejemplos de máquina virtual.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[3]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md