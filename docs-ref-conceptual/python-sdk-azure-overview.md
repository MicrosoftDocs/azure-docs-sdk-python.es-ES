---
title: Bibliotecas de Azure para Python
description: Introducción a la administración de Azure y las bibliotecas de servicios para Python
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: ''
ms.openlocfilehash: bb17295de2f0272f0525fda5edab87e840764478
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534467"
---
# <a name="azure-libraries-for-python"></a>Bibliotecas de Azure para Python

Las bibliotecas de Azure para Python le permiten usar los servicios de Azure y administrar los recursos de Azure desde el código de la aplicación. 

## <a name="manage-azure-resources"></a>Administración de recursos de Azure

Cree y administre recursos de Azure desde las aplicaciones Python mediante las bibliotecas de Azure para Python.

Por ejemplo, para crear una instancia de SQL Server, puede usar el código siguiente:

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

Revise las [instrucciones de instalación](python-sdk-azure-install.md) para obtener una lista completa de las bibliotecas y cómo importarlas en los proyectos y, a continuación, consulte el artículo de [Introducción](python-sdk-azure-get-started.yml) para configurar la autenticación y ejecutar código de ejemplo en su propia suscripción de Azure.

## <a name="connect-to-azure-services"></a>Conexión a los servicios de Azure

Además de utilizar las bibliotecas de Python para crear y administrar recursos en Azure, también puede utilizarlas para conectarse a esos recursos y usarlos en las aplicaciones. Por ejemplo, puede actualizar una tabla de SQL Database o almacenar archivos en Azure Storage. En la lista completa de bibliotecas, seleccione la biblioteca que necesita para un servicio determinado y visite el centro para desarrolladores de Python para ver tutoriales y código de ejemplo y obtener ayuda para usarlos en sus aplicaciones.

Por ejemplo, para cargar una página HTML sencilla en un blob y obtener la dirección URL:

```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

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

## <a name="sample-code-and-reference"></a>Código de ejemplo y referencia
Los ejemplos siguientes incluyen las tareas comunes de automatización con las bibliotecas de administración de Azure para Python, y tienen código listo para usar en sus propias aplicaciones:
- [Máquinas virtuales](python-sdk-azure-virtual-machine-samples.md)
- [Aplicaciones web](python-sdk-azure-web-apps-samples.md)
- [SQL Database](python-sdk-azure-sql-database-samples.md)

Hay disponible una [referencia](/python/api/overview/azure) para todos los paquetes tanto en el servicio como en las bibliotecas de administración. Las nuevas características, cambios importantes e instrucciones de migración desde versiones anteriores están disponibles en las [notas de la versión](python-sdk-azure-release-notes.md). 

## <a name="get-help-and-give-feedback"></a>Obtención de ayuda y ofrecimiento de comentarios

Envíe preguntas a la Comunidad sobre [Stack Overflow](https://stackoverflow.com/questions/tagged/azure-sdk-python) y abra problemas en el SDK sobre el [GitHub del proyecto](https://github.com/Azure/azure-sdk-for-python).
