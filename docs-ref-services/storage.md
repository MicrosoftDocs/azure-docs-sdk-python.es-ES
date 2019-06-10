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
ms.openlocfilehash: 5b4d4cc2dfb32dceb66bdb5be3fe0f0075840d8f
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376757"
---
# <a name="azure-storage-libraries-for-python"></a>Bibliotecas de Azure Storage para Python

## <a name="overview"></a>Información general
- Lea y escriba objetos y archivos en [Azure Blob Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage).
- Envíe y reciba mensajes entre aplicaciones conectadas en la nube con [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage).
- Lea y escriba datos estructurados grandes con [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage). 
- Comparta almacenamiento entre aplicaciones con [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage).

Cree, actualice y administre cuentas y consultas de Azure Storage, y regenere las claves de acceso desde su código Python con las bibliotecas de administración.

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

### <a name="client"></a>Cliente

Las bibliotecas de cliente de Azure Storage se componen de cuatro paquetes: Blob, File, Queue y Table. Para instalar el paquete Blob, ejecute:

```bash
pip install azure-storage-blob
```

### <a name="management"></a>Administración

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>Ejemplo
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

## <a name="samples"></a>Ejemplos

| | |
|--|--|
| [Introducción a Azure Blob Storage en Python](https://docs.microsoft.com/azure/storage/blobs/storage-python-how-to-use-blob-storage) | Cree, lea, actualice, restrinja el acceso y elimine archivos y objetos Azure Storage. |
| [Introducción a Azure Queue Storage en Python](https://docs.microsoft.com/azure/storage/queues/storage-python-how-to-use-queue-storage) | Inserte, consulte, recupere y elimine mensajes de las colas de Azure Storage. | 
| [Administración de cuentas de Azure Storage](https://azure.microsoft.com/resources/samples/storage-python-manage) | Cree, actualice y elimine cuentas de almacenamiento. Recupere y regenere las claves de acceso de la cuenta de almacenamiento.

Vea más [código de Python ejemplo](https://azure.microsoft.com/resources/samples/?platform=python) que puede usar en sus aplicaciones.
