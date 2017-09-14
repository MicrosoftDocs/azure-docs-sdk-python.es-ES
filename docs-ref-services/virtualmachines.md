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
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="cc64a-103">Bibliotecas de Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="cc64a-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="cc64a-104">Información general</span><span class="sxs-lookup"><span data-stu-id="cc64a-104">Overview</span></span>

<span data-ttu-id="cc64a-105">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="cc64a-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="cc64a-106">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="cc64a-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="cc64a-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="cc64a-107">Management API</span></span>

<span data-ttu-id="cc64a-108">Cree, configure, administre y escale máquinas virtuales Windows y Linux en Azure desde su propio código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="cc64a-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="cc64a-109">Instale la biblioteca mediante pip.</span><span class="sxs-lookup"><span data-stu-id="cc64a-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="cc64a-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="cc64a-110">Example</span></span>

<span data-ttu-id="cc64a-111">Cree una nueva máquina virtual Linux en un grupo de recursos de Azure existente.</span><span class="sxs-lookup"><span data-stu-id="cc64a-111">Create a new Linux virtual machine in an existing Azure resource group.</span></span>

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
> [<span data-ttu-id="cc64a-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="cc64a-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a><span data-ttu-id="cc64a-113">Muestras</span><span class="sxs-lookup"><span data-stu-id="cc64a-113">Samples</span></span>

* <span data-ttu-id="cc64a-114">[Administración de máquinas virtuales][1]</span><span class="sxs-lookup"><span data-stu-id="cc64a-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="cc64a-115">[Administración de un equilibrador de carga][2]</span><span class="sxs-lookup"><span data-stu-id="cc64a-115">[Manage a load balancer][2]</span></span>
* <span data-ttu-id="cc64a-116">[Creación y configuración de discos administrados][3]</span><span class="sxs-lookup"><span data-stu-id="cc64a-116">[Create and configure managed disks][3]</span></span>
* <span data-ttu-id="cc64a-117">[Lista de imágenes][4]</span><span class="sxs-lookup"><span data-stu-id="cc64a-117">[List images][4]</span></span> 
* <span data-ttu-id="cc64a-118">[Supervisión de máquinas virtuales][5]</span><span class="sxs-lookup"><span data-stu-id="cc64a-118">[Monitor virtual machines][5]</span></span>

<span data-ttu-id="cc64a-119">Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de ejemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cc64a-119">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[3]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md