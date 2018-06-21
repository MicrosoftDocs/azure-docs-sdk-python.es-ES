---
title: Bibliotecas de Azure Storage para Python
description: ''
keywords: Azure, Python, SDK, API, Storage
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: e45b12af9e026e0f6390556813385d86784feaa4
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720066"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="e4ee9-103">Bibliotecas de Azure Storage para Python</span><span class="sxs-lookup"><span data-stu-id="e4ee9-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="e4ee9-104">Información general</span><span class="sxs-lookup"><span data-stu-id="e4ee9-104">Overview</span></span>
- <span data-ttu-id="e4ee9-105">Lea y escriba objetos y archivos en [Azure Blob Storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="e4ee9-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="e4ee9-106">Envíe y reciba mensajes entre aplicaciones conectadas en la nube con [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage).</span><span class="sxs-lookup"><span data-stu-id="e4ee9-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="e4ee9-107">Lea y escriba datos estructurados grandes con [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage).</span><span class="sxs-lookup"><span data-stu-id="e4ee9-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="e4ee9-108">Comparta almacenamiento entre aplicaciones con [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage).</span><span class="sxs-lookup"><span data-stu-id="e4ee9-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="e4ee9-109">Cree, actualice y administre cuentas y consultas de Azure Storage, y regenere las claves de acceso desde su código Python con las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="e4ee9-110">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="e4ee9-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="e4ee9-111">Cliente</span><span class="sxs-lookup"><span data-stu-id="e4ee9-111">Client</span></span>

<span data-ttu-id="e4ee9-112">Las bibliotecas de cliente de Azure Storage se componen de cuatro paquetes: Blob, File, Queue y Table.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="e4ee9-113">Para instalar el paquete Blob, ejecute:</span><span class="sxs-lookup"><span data-stu-id="e4ee9-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="e4ee9-114">Administración</span><span class="sxs-lookup"><span data-stu-id="e4ee9-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="e4ee9-115">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e4ee9-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

blob_service = BlockBlobService(account_name, account_key)

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="samples"></a><span data-ttu-id="e4ee9-116">Ejemplos</span><span class="sxs-lookup"><span data-stu-id="e4ee9-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="e4ee9-117">Introducción a Azure Blob Storage en Python</span><span class="sxs-lookup"><span data-stu-id="e4ee9-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="e4ee9-118">Cree, lea, actualice, restrinja el acceso y elimine archivos y objetos Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="e4ee9-119">Introducción a Azure Queue Storage en Python</span><span class="sxs-lookup"><span data-stu-id="e4ee9-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="e4ee9-120">Inserte, consulte, recupere y elimine mensajes de las colas de Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="e4ee9-121">Administración de cuentas de Azure Storage</span><span class="sxs-lookup"><span data-stu-id="e4ee9-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="e4ee9-122">Cree, actualice y elimine cuentas de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="e4ee9-123">Recupere y regenere las claves de acceso de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="e4ee9-124">Vea más [código de Python ejemplo](https://azure.microsoft.com/resources/samples/?platform=python) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="e4ee9-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
