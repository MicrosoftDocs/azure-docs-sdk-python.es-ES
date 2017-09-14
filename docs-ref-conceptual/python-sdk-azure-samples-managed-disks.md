---
title: Managed Disks
description: "Cree, cambie el tamaño y actualice un disco administrado."
author: lisawong19
manager: douge
ms.assetid: 
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: 4154367f0449b174790ee3f3c9480ca0bceeea87
ms.sourcegitcommit: c6d9500492131bf782488fcafc7c5c41c2703e92
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/13/2017
---
# <a name="managed-disks"></a><span data-ttu-id="67d9e-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="67d9e-103">Managed Disks</span></span>

<span data-ttu-id="67d9e-104">Ya están disponibles Azure Managed Disks y un conjunto de escalado de 1000 máquinas virtuales [de forma general](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/). Azure Managed Disks proporcionan una administración de discos simplificada, mayor escalabilidad, mejor seguridad y escalado.</span><span class="sxs-lookup"><span data-stu-id="67d9e-104">Azure Managed Disks and 1000 VMs in a Scale Set are now [generally available](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/) Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="67d9e-105">Elimina la noción de cuenta de almacenamiento para los discos, lo que permite a los clientes escalar sin tener que preocuparse por las limitaciones asociadas con las cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="67d9e-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="67d9e-106">Esta publicación proporciona una introducción rápida y referencia para utilizar el servicio desde Python.</span><span class="sxs-lookup"><span data-stu-id="67d9e-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>



<span data-ttu-id="67d9e-107">Desde la perspectiva del desarrollador, la experiencia con los discos administrados en la CLI de Azure es específica del idioma de la experiencia de la CLI en otras herramientas multiplataforma.</span><span class="sxs-lookup"><span data-stu-id="67d9e-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="67d9e-108">Puede usar [Azure SDK para Python](https://azure.microsoft.com/develop/python/) y el [paquete azure-mgmt-compute 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) para administrar discos administrados.</span><span class="sxs-lookup"><span data-stu-id="67d9e-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="67d9e-109">Puede crear un cliente de proceso mediante este [tutorial](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html).</span><span class="sxs-lookup"><span data-stu-id="67d9e-109">You can create a compute client using this [tutorial](http://azure-sdk-for-python.readthedocs.io/en/latest/resourcemanagementcomputenetwork.html).</span></span>


## <a name="standalone-managed-disks"></a><span data-ttu-id="67d9e-110">Discos administrados independientes</span><span class="sxs-lookup"><span data-stu-id="67d9e-110">Standalone Managed Disks</span></span>

<span data-ttu-id="67d9e-111">Hay varias formas de crear discos administrados independientes fácilmente.</span><span class="sxs-lookup"><span data-stu-id="67d9e-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="67d9e-112">Crear un disco administrado vacío.</span><span class="sxs-lookup"><span data-stu-id="67d9e-112">Create an empty Managed Disk.</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="67d9e-113">Crear un disco administrado a partir de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="67d9e-113">Create a Managed Disk from Blob Storage.</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="67d9e-114">Crear un disco administrado a partir de su propia imagen.</span><span class="sxs-lookup"><span data-stu-id="67d9e-114">Create a Managed Disk from your own Image</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="67d9e-115">Máquina virtual con discos administrados</span><span class="sxs-lookup"><span data-stu-id="67d9e-115">Virtual Machine with Managed Disks</span></span>

<span data-ttu-id="67d9e-116">Puede crear una máquina virtual con un disco administrado implícito para una imagen de disco específica.</span><span class="sxs-lookup"><span data-stu-id="67d9e-116">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="67d9e-117">La creación se simplifica con la creación implícita de discos administrados sin especificar todos los detalles del disco.</span><span class="sxs-lookup"><span data-stu-id="67d9e-117">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="67d9e-118">No tiene que preocuparse por crear y administrar cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="67d9e-118">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="67d9e-119">Un disco administrado se crea implícitamente al crear la máquina virtual a partir de una imagen de sistema operativo en Azure.</span><span class="sxs-lookup"><span data-stu-id="67d9e-119">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="67d9e-120">En el parámetro ``storage_profile``, ``os_disk`` ahora es opcional y no es necesario crear una cuenta de almacenamiento como condición previa necesaria para crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="67d9e-120">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
``` 
<span data-ttu-id="67d9e-121">Este parámetro ``storage_profile`` ahora es válido.</span><span class="sxs-lookup"><span data-stu-id="67d9e-121">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="67d9e-122">Para obtener un ejemplo completo sobre cómo crear una máquina virtual en Python (incluida la red, etc.), consulte el [tutorial completo sobre máquinas virtuales en Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span><span class="sxs-lookup"><span data-stu-id="67d9e-122">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="67d9e-123">Puede asociar fácilmente un disco administrado aprovisionado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="67d9e-123">You can easily attach a previously provisioned Managed Disk.</span></span>
```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="67d9e-124">Conjuntos de escalado de máquinas virtuales con discos administrados</span><span class="sxs-lookup"><span data-stu-id="67d9e-124">Virtual Machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="67d9e-125">Antes de los discos administrados, había que crear manualmente una cuenta de almacenamiento para todas las máquinas virtuales que quería dentro del conjunto de escalado y, a continuación, usar el parámetro de lista ``vhd_containers`` para proporcionar el nombre de todas las cuentas de almacenamiento a la API de REST del conjunto de escalado.</span><span class="sxs-lookup"><span data-stu-id="67d9e-125">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="67d9e-126">La guía de transición oficial está disponible en este `article <https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`__.</span><span class="sxs-lookup"><span data-stu-id="67d9e-126">The official transition guide is available in this `article <https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`__.</span></span>

<span data-ttu-id="67d9e-127">Ahora, con los discos administrados, no es necesario administrar ninguna cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="67d9e-127">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="67d9e-128">Si está acostumbrado al SDK de VMSS para Python, su ``storage_profile`` puede ser exactamente el mismo que el que se usó para crear las máquinas virtuales:</span><span class="sxs-lookup"><span data-stu-id="67d9e-128">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

<span data-ttu-id="67d9e-129">El ejemplo completo es este:</span><span class="sxs-lookup"><span data-stu-id="67d9e-129">The full sample being:</span></span>

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
``` 

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="67d9e-130">Otras operaciones con discos administrados</span><span class="sxs-lookup"><span data-stu-id="67d9e-130">Other Operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="67d9e-131">Cambie el tamaño de un disco administrado.</span><span class="sxs-lookup"><span data-stu-id="67d9e-131">Resizing a managed disk.</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="67d9e-132">Actualice del tipo de cuenta de almacenamiento de los discos administrados.</span><span class="sxs-lookup"><span data-stu-id="67d9e-132">Update the Storage Account type of the Managed Disks.</span></span>
```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-blob-storage"></a><span data-ttu-id="67d9e-133">Cree una imagen a partir de Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="67d9e-133">Create an image from Blob Storage.</span></span>
```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="67d9e-134">Cree una instantánea de un disco administrado que esté asociado a una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="67d9e-134">Create a snapshot of a Managed Disk that is currently attached to a Virtual Machine.</span></span>
```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```