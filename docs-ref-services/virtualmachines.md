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
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="c3c68-103">Bibliotecas de Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="c3c68-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="c3c68-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c3c68-104">Overview</span></span>

<span data-ttu-id="c3c68-105">Recursos informáticos bajo demanda y escalables que se ejecutan en Linux o Windows.</span><span class="sxs-lookup"><span data-stu-id="c3c68-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="c3c68-106">Para empezar a trabajar con Azure Virtual Machines, consulte [Creación de una máquina virtual Linux con Azure Portal](/azure/virtual-machines/linux/quick-create-portal).</span><span class="sxs-lookup"><span data-stu-id="c3c68-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="c3c68-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="c3c68-107">Management API</span></span>

<span data-ttu-id="c3c68-108">Cree, configure, administre y escale máquinas virtuales Windows y Linux en Azure desde su propio código con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="c3c68-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="c3c68-109">Instale la biblioteca mediante pip.</span><span class="sxs-lookup"><span data-stu-id="c3c68-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a><span data-ttu-id="c3c68-110">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="c3c68-110">Example</span></span>

<span data-ttu-id="c3c68-111">Cree una nueva máquina virtual Linux en un grupo de recursos de Azure existente con la autenticación de Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="c3c68-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

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
> [<span data-ttu-id="c3c68-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="c3c68-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a><span data-ttu-id="c3c68-113">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="c3c68-113">Samples</span></span>

* <span data-ttu-id="c3c68-114">[Administración de máquinas virtuales][1]</span><span class="sxs-lookup"><span data-stu-id="c3c68-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="c3c68-115">[Autenticación con Managed Service Identity ][2]</span><span class="sxs-lookup"><span data-stu-id="c3c68-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="c3c68-116">[Creación de una máquina virtual con la extensión de identidad de servicio administrada][3]</span><span class="sxs-lookup"><span data-stu-id="c3c68-116">[Create a virtual machine with Managed Service Identity Extension][3]</span></span>
* <span data-ttu-id="c3c68-117">[Administración de un equilibrador de carga][4]</span><span class="sxs-lookup"><span data-stu-id="c3c68-117">[Manage a load balancer][4]</span></span>
* <span data-ttu-id="c3c68-118">[Creación y configuración de discos administrados][5]</span><span class="sxs-lookup"><span data-stu-id="c3c68-118">[Create and configure managed disks][5]</span></span>
* <span data-ttu-id="c3c68-119">[Lista de imágenes][6]</span><span class="sxs-lookup"><span data-stu-id="c3c68-119">[List images][6]</span></span> 
* <span data-ttu-id="c3c68-120">[Supervisión de máquinas virtuales][7]</span><span class="sxs-lookup"><span data-stu-id="c3c68-120">[Monitor virtual machines][7]</span></span>

<span data-ttu-id="c3c68-121">Ver el [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) de ejemplos de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="c3c68-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
