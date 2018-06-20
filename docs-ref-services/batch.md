---
title: Bibliotecas de Azure Batch para Python
description: Documentación de referencia de las bibliotecas de Batch para Python
keywords: Azure, Python, SDK, API, Batch, proceso, programación, ejecución larga
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: de5f3a98b1712ff9bdcc417daf10719178819364
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478988"
---
# <a name="azure-batch-libraries-for-python"></a>Bibliotecas de Azure Batch para Python

## <a name="overview"></a>Información general

[Azure Batch](/azure/batch/batch-technical-overview) permite ejecutar aplicaciones en paralelo a gran escala y de informática de alto rendimiento de manera eficaz en la nube.   

Para empezar a trabajar con Azure Batch, consulte [Creación de una cuenta de Batch con Azure Portal](/azure/batch/batch-account-create-portal).

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

## <a name="client-library"></a>Biblioteca de cliente
Las bibliotecas de cliente de Azure Batch le permiten configurar nodos de cálculo y grupos, definir tareas y configurarlos para ejecutar trabajos y configurar un administrador de trabajos para controlar y supervisar la ejecución de trabajos. [Obtenga más información](/azure/batch/batch-api-basics) sobre el uso de estos objetos para ejecutar soluciones de proceso en paralelo a gran escala.

```bash
pip install azure-batch
```
### <a name="example"></a>Ejemplo

Configure un grupo de nodos de proceso de Linux en una cuenta de Batch:

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

## <a name="management-api"></a>API de administración
Use las bibliotecas de administración de Azure Batch para crear y eliminar cuentas de Batch, leer y volver a generar las claves de cuenta de Batch y administrar la cuenta de almacenamiento de Batch.

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [Explorar las API de cliente](/python/api/overview/azure/batch/client)

### <a name="example"></a>Ejemplo
Cree una cuenta de Azure Batch y configure una nueva aplicación y una cuenta de Azure Storage para ella.

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
> [Explorar las API de administración](/python/api/overview/azure/batch/management)