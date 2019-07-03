---
title: Bibliotecas de Azure Batch para Python
description: Documentación de referencia de las bibliotecas de Batch para Python
keywords: Azure, Python, SDK, API, Batch, proceso, programación, ejecución larga
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: bbc691a8db6597c77575900b4e2a06f34ebb179c
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534355"
---
# <a name="azure-batch-libraries-for-python"></a><span data-ttu-id="f1c1c-104">Bibliotecas de Azure Batch para Python</span><span class="sxs-lookup"><span data-stu-id="f1c1c-104">Azure Batch libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="f1c1c-105">Información general</span><span class="sxs-lookup"><span data-stu-id="f1c1c-105">Overview</span></span>

<span data-ttu-id="f1c1c-106">[Azure Batch](/azure/batch/batch-technical-overview) permite ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.</span><span class="sxs-lookup"><span data-stu-id="f1c1c-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>

<span data-ttu-id="f1c1c-107">Para empezar a trabajar con Azure Batch, consulte [Creación de una cuenta de Batch con Azure Portal](/azure/batch/batch-account-create-portal).</span><span class="sxs-lookup"><span data-stu-id="f1c1c-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="f1c1c-108">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="f1c1c-108">Install the libraries</span></span>

## <a name="client-library"></a><span data-ttu-id="f1c1c-109">Biblioteca de cliente</span><span class="sxs-lookup"><span data-stu-id="f1c1c-109">Client library</span></span>
<span data-ttu-id="f1c1c-110">Las bibliotecas de cliente de Azure Batch le permiten configurar nodos de cálculo y grupos, definir tareas y configurarlos para ejecutar trabajos y configurar un administrador de trabajos para controlar y supervisar la ejecución de trabajos.</span><span class="sxs-lookup"><span data-stu-id="f1c1c-110">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="f1c1c-111">[Obtenga más información](/azure/batch/batch-api-basics) sobre el uso de estos objetos para ejecutar soluciones de proceso en paralelo a gran escala.</span><span class="sxs-lookup"><span data-stu-id="f1c1c-111">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

```bash
pip install azure-batch
```
### <a name="example"></a><span data-ttu-id="f1c1c-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f1c1c-112">Example</span></span>

<span data-ttu-id="f1c1c-113">Configure un grupo de nodos de proceso de Linux en una cuenta de Batch:</span><span class="sxs-lookup"><span data-stu-id="f1c1c-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```python
# create the batch client for an account using its URI and keys
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

## <a name="management-api"></a><span data-ttu-id="f1c1c-114">API de administración</span><span class="sxs-lookup"><span data-stu-id="f1c1c-114">Management API</span></span>
<span data-ttu-id="f1c1c-115">Use las bibliotecas de administración de Azure Batch para crear y eliminar cuentas de Batch, leer y volver a generar las claves de cuenta de Batch y administrar la cuenta de almacenamiento de Batch.</span><span class="sxs-lookup"><span data-stu-id="f1c1c-115">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="f1c1c-116">Explorar las API de cliente</span><span class="sxs-lookup"><span data-stu-id="f1c1c-116">Explore the Client APIs</span></span>](/python/api/overview/azure/batch/client)

### <a name="example"></a><span data-ttu-id="f1c1c-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="f1c1c-117">Example</span></span>
<span data-ttu-id="f1c1c-118">Cree una cuenta de Azure Batch y configure una nueva aplicación y una cuenta de Azure Storage para ella.</span><span class="sxs-lookup"><span data-stu-id="f1c1c-118">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```python
from azure.mgmt.batch import BatchManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.storage import StorageManagementClient

LOCATION ='eastus'
GROUP_NAME ='batchresourcegroup'
STORAGE_ACCOUNT_NAME ='batchstorageaccount'

# Create Resource group
print('Create Resource Group')
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})

# Create a storage account
storage_async_operation = storage_client.storage_accounts.create(
    GROUP_NAME,
    STORAGE_ACCOUNT_NAME,
    StorageAccountCreateParameters(
        sku=Sku(SkuName.standard_ragrs),
        kind=Kind.storage,
        location=LOCATION
    )
)
storage_account = storage_async_operation.result()

# Create a Batch Account, specifying the storage account we want to link
storage_resource = storage_account.id
batch_account = azure.mgmt.batch.models.BatchAccountCreateParameters(
    location=LOCATION,
    auto_storage=azure.mgmt.batch.models.AutoStorageBaseProperties(storage_resource)
)
creating = batch_client.account.create('MyBatchAccount', LOCATION, batch_account)
creating.wait()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f1c1c-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="f1c1c-119">Explore the Management APIs</span></span>](/python/api/overview/azure/batch/management)
