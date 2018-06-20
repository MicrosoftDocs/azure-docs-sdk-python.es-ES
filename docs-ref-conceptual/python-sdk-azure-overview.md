---
title: Bibliotecas de Azure para Python
description: Introducción a la administración de Azure y las bibliotecas de servicios para Python
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: ''
ms.openlocfilehash: 2b3e6d31edd7b946664853b3478e22205ab8c92e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478808"
---
# <a name="azure-libraries-for-python"></a><span data-ttu-id="9a08d-104">Bibliotecas de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="9a08d-104">Azure libraries for Python</span></span>

<span data-ttu-id="9a08d-105">Las bibliotecas de Azure para Python le permiten usar los servicios de Azure y administrar los recursos de Azure desde el código de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9a08d-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="9a08d-106">Administración de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="9a08d-106">Manage Azure resources</span></span>

<span data-ttu-id="9a08d-107">Cree y administre recursos de Azure desde las aplicaciones Python mediante las bibliotecas de Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="9a08d-107">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="9a08d-108">Por ejemplo, para crear una instancia de SQL Server, puede usar el código siguiente:</span><span class="sxs-lookup"><span data-stu-id="9a08d-108">For example, to create a SQL Server instance, you can use the following code:</span></span>

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

<span data-ttu-id="9a08d-109">Revise las [instrucciones de instalación](python-sdk-azure-install.md) para obtener una lista completa de las bibliotecas y cómo importarlas en los proyectos y, a continuación, consulte el artículo de [Introducción](python-sdk-azure-get-started.yml) para configurar la autenticación y ejecutar código de ejemplo en su propia suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9a08d-109">Review the [install instructions](python-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="9a08d-110">Conexión a los servicios de Azure</span><span class="sxs-lookup"><span data-stu-id="9a08d-110">Connect to Azure services</span></span>

<span data-ttu-id="9a08d-111">Además de utilizar las bibliotecas de Python para crear y administrar recursos en Azure, también puede utilizarlas para conectarse a esos recursos y usarlos en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9a08d-111">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="9a08d-112">Por ejemplo, puede actualizar una tabla de SQL Database o almacenar archivos en Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9a08d-112">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="9a08d-113">En la lista completa de bibliotecas, seleccione la biblioteca que necesita para un servicio determinado y visite el centro para desarrolladores de Python para ver tutoriales y código de ejemplo y obtener ayuda para usarlos en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9a08d-113">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="9a08d-114">Por ejemplo, para cargar una página HTML sencilla en un blob y obtener la dirección URL:</span><span class="sxs-lookup"><span data-stu-id="9a08d-114">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="9a08d-115">Código de ejemplo y referencia</span><span class="sxs-lookup"><span data-stu-id="9a08d-115">Sample code and reference</span></span>
<span data-ttu-id="9a08d-116">Los ejemplos siguientes incluyen las tareas comunes de automatización con las bibliotecas de administración de Azure para Python, y tienen código listo para usar en sus propias aplicaciones:</span><span class="sxs-lookup"><span data-stu-id="9a08d-116">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="9a08d-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="9a08d-117">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="9a08d-118">Aplicaciones web</span><span class="sxs-lookup"><span data-stu-id="9a08d-118">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="9a08d-119">SQL Database</span><span class="sxs-lookup"><span data-stu-id="9a08d-119">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="9a08d-120">Hay disponible una [referencia](/python/api/overview/azure) para todos los paquetes tanto en el servicio como en las bibliotecas de administración.</span><span class="sxs-lookup"><span data-stu-id="9a08d-120">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="9a08d-121">Las nuevas características, cambios importantes e instrucciones de migración desde versiones anteriores están disponibles en las [notas de la versión](python-sdk-azure-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="9a08d-121">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="9a08d-122">Obtención de ayuda y ofrecimiento de comentarios</span><span class="sxs-lookup"><span data-stu-id="9a08d-122">Get help and give feedback</span></span>

<span data-ttu-id="9a08d-123">Envíe preguntas a la Comunidad sobre [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) y abra problemas en el SDK sobre el [GitHub del proyecto](https://github.com/Azure/azure-sdk-for-python).</span><span class="sxs-lookup"><span data-stu-id="9a08d-123">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
