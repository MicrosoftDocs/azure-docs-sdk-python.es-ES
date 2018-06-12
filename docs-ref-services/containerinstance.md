---
title: Bibliotecas de Azure Container Instances para Python
description: Referencia de las bibliotecas de Azure Container Instances para Python
keywords: Azure, python, SDK, API, ACI, contenedor, instancias
author: mmacy
manager: jeconnoc
ms.date: 06/04/2018
ms.author: marsma
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 09f39375e0e92b6d09a965c3972d772a1437d0d4
ms.sourcegitcommit: 8c70bfd95309c3a77a4c0f73373c1785d59cdd10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34761333"
---
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="82c28-104">Bibliotecas de Azure Container Instances para Python</span><span class="sxs-lookup"><span data-stu-id="82c28-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="82c28-105">Use las bibliotecas de Microsoft Azure Container Instances para Python para crear y administrar instancias de contenedor de Azure.</span><span class="sxs-lookup"><span data-stu-id="82c28-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="82c28-106">Para más información, consulte la [Introducción a Azure Container Instances](/azure/container-instances/container-instances-overview).</span><span class="sxs-lookup"><span data-stu-id="82c28-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="82c28-107">API de administración</span><span class="sxs-lookup"><span data-stu-id="82c28-107">Management APIs</span></span>

<span data-ttu-id="82c28-108">Use la biblioteca de administración para crear y administrar instancias de contenedor en Azure.</span><span class="sxs-lookup"><span data-stu-id="82c28-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="82c28-109">Instale el paquete de administración mediante pip:</span><span class="sxs-lookup"><span data-stu-id="82c28-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="82c28-110">Ejemplo de código fuente</span><span class="sxs-lookup"><span data-stu-id="82c28-110">Example source</span></span>

<span data-ttu-id="82c28-111">Si desea ver los ejemplos de código siguientes en contexto, los encontrará en el repositorio de GitHub siguiente:</span><span class="sxs-lookup"><span data-stu-id="82c28-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="82c28-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="82c28-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="82c28-113">Autenticación</span><span class="sxs-lookup"><span data-stu-id="82c28-113">Authentication</span></span>

<span data-ttu-id="82c28-114">Una de las formas más sencillas para autenticar los clientes de SDK (por ejemplo, los clientes de Azure Container Instances y Resource Manager en el ejemplo siguiente) es con la [autenticación basada en archivo](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span><span class="sxs-lookup"><span data-stu-id="82c28-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="82c28-115">La autenticación basada en archivo consulta la variable de entorno `AZURE_AUTH_LOCATION` para obtener la ruta de acceso a un archivo de credenciales.</span><span class="sxs-lookup"><span data-stu-id="82c28-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="82c28-116">Para usar la autenticación basada en archivo</span><span class="sxs-lookup"><span data-stu-id="82c28-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="82c28-117">Cree un archivo de credenciales con la [CLI de Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="82c28-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="82c28-118">Si usa [Cloud Shell](https://shell.azure.com/) para generar el archivo de credenciales, copie su contenido en un archivo local al que pueda tener acceso la aplicación de Python.</span><span class="sxs-lookup"><span data-stu-id="82c28-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="82c28-119">Establezca la variable de entorno `AZURE_AUTH_LOCATION` en la ruta de acceso completa del archivo de credenciales generado.</span><span class="sxs-lookup"><span data-stu-id="82c28-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="82c28-120">Por ejemplo, en Bash:</span><span class="sxs-lookup"><span data-stu-id="82c28-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="82c28-121">Después de crear el archivo de credenciales y de rellenar la variable de entorno `AZURE_AUTH_LOCATION`, use el método `get_client_from_auth_file` del módulo [client_factory][client_factory] para inicializar los objetos [ResourceManagementClient][ResourceManagementClient] y [ContainerInstanceManagementClient][ContainerInstanceManagementClient].</span><span class="sxs-lookup"><span data-stu-id="82c28-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

<span data-ttu-id="82c28-122">Para más información acerca de los métodos de autenticación disponibles en las bibliotecas de administración de Python para Azure, consulte [Autenticación con las bibliotecas de administración de Azure para Python](/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="82c28-122">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="82c28-123">Creación de un grupo de contenedores: un solo contenedor</span><span class="sxs-lookup"><span data-stu-id="82c28-123">Create container group - single container</span></span>

<span data-ttu-id="82c28-124">En este ejemplo se crea un grupo de contenedores con un solo contenedor</span><span class="sxs-lookup"><span data-stu-id="82c28-124">This example creates a container group with a single container</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="82c28-125">Creación de un grupo de contenedores: varios contenedores</span><span class="sxs-lookup"><span data-stu-id="82c28-125">Create container group - multiple containers</span></span>

<span data-ttu-id="82c28-126">En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.</span><span class="sxs-lookup"><span data-stu-id="82c28-126">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]

## <a name="create-task-based-container-group"></a><span data-ttu-id="82c28-127">Creación de un grupo de contenedores basado en tareas</span><span class="sxs-lookup"><span data-stu-id="82c28-127">Create task-based container group</span></span>

<span data-ttu-id="82c28-128">En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas.</span><span class="sxs-lookup"><span data-stu-id="82c28-128">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="82c28-129">En este ejemplo se muestran varias características:</span><span class="sxs-lookup"><span data-stu-id="82c28-129">This example demonstrates several features:</span></span>

* <span data-ttu-id="82c28-130">[Invalidación de la línea de comandos](/azure/container-instances/container-instances-restart-policy#command-line-override): se especifica una línea de comandos personalizada, diferente de la que se especifica en la línea `CMD` del archivo Docker del contenedor.</span><span class="sxs-lookup"><span data-stu-id="82c28-130">[Command line override](/azure/container-instances/container-instances-restart-policy#command-line-override) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="82c28-131">La invalidación de la línea de comandos permite especificar la línea de comandos personalizada que se ejecutará ejecutar durante el inicio del contenedor y que reemplazará la línea de comandos predeterminada incluida en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="82c28-131">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="82c28-132">En relación con la ejecución de varios comandos durante el inicio del contenedor, se aplica lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="82c28-132">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="82c28-133">Si desea ejecutar un **único comando** con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una lista de cadenas a la propiedad `command` de [Container][Container].</span><span class="sxs-lookup"><span data-stu-id="82c28-133">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="82c28-134">Por ejemplo: </span><span class="sxs-lookup"><span data-stu-id="82c28-134">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="82c28-135">En cambio, si desea ejecutar **varios comandos** con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento.</span><span class="sxs-lookup"><span data-stu-id="82c28-135">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="82c28-136">Por ejemplo, esto ejecuta los comandos `echo` y `tail`:</span><span class="sxs-lookup"><span data-stu-id="82c28-136">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="82c28-137">[Variables de entorno](/azure/container-instances/container-instances-environment-variables): se especifican dos variables de entorno para el contenedor en el grupo de contenedores.</span><span class="sxs-lookup"><span data-stu-id="82c28-137">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="82c28-138">Use variables de entorno para modificar el comportamiento de un script o aplicación en tiempo de ejecución; de lo contrario, pase información dinámica a una aplicación que se ejecuta en el contenedor.</span><span class="sxs-lookup"><span data-stu-id="82c28-138">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="82c28-139">[Directiva de reinicio](/azure/container-instances/container-instances-restart-policy): el contenedor está configurado con una directiva de reinicio de "Nunca", que resulta útil para los contenedores basados en tareas que se ejecutan como parte de un trabajo por lotes.</span><span class="sxs-lookup"><span data-stu-id="82c28-139">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="82c28-140">Sondeo de la operación con [AzureOperationPoller][AzureOperationPoller]: después de invocar el método Create, se sondea la operación para determinar cuándo se ha completado y obtener los registros del grupo de contenedores.</span><span class="sxs-lookup"><span data-stu-id="82c28-140">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]

## <a name="list-container-groups"></a><span data-ttu-id="82c28-141">Enumeración de grupos de contenedores</span><span class="sxs-lookup"><span data-stu-id="82c28-141">List container groups</span></span>

<span data-ttu-id="82c28-142">En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos y se imprimen algunas de sus propiedades.</span><span class="sxs-lookup"><span data-stu-id="82c28-142">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="82c28-143">Cuando se enumeran grupos de contenedores, el valor de [instance_view][instance_view] de cada grupo es `None`.</span><span class="sxs-lookup"><span data-stu-id="82c28-143">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="82c28-144">Para obtener los detalles de los contenedores dentro de un grupo de contenedores, deberá ejecutar [get][containergroupoperations_get] en el grupo de contenedores, que devuelve el grupo con la `instance_view` propiedad rellena.</span><span class="sxs-lookup"><span data-stu-id="82c28-144">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="82c28-145">Consulte la sección siguiente, [Obtención de un grupo de contenedores existente](#get-an-existing-container-group), para ver un ejemplo de cómo recorrer en iteración los contenedores de un grupo de contenedores en su `instance_view`.</span><span class="sxs-lookup"><span data-stu-id="82c28-145">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]

## <a name="get-an-existing-container-group"></a><span data-ttu-id="82c28-146">Obtención de un grupo de contenedores existente</span><span class="sxs-lookup"><span data-stu-id="82c28-146">Get an existing container group</span></span>

<span data-ttu-id="82c28-147">En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades (incluidos sus contenedores) y sus valores.</span><span class="sxs-lookup"><span data-stu-id="82c28-147">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="82c28-148">La [operación get][containergroupoperations_get] devuelve un grupo de contenedor con el valor de [instance_view][instance_view] relleno, lo que permite recorrer en iteración cada contenedor del grupo.</span><span class="sxs-lookup"><span data-stu-id="82c28-148">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="82c28-149">Solo la operación `get` rellena la propiedad `instance_vew` del grupo de contenedores. Enumerar los grupos de contenedores de una suscripción o grupo de recursos no rellena instance_view debido a la naturaleza potencialmente costosa de la operación; por ejemplo, cuando se enumeran cientos de grupos de contenedores, cada uno de ellos puede contener a su vez varios contenedores.</span><span class="sxs-lookup"><span data-stu-id="82c28-149">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="82c28-150">Tal y como se mencionó anteriormente en la sección [Enumeración de grupos de contenedores](#list-container-groups), después un `list`, se debe ejecutar `get` en un grupo de contenedores específico para obtener información detallada de su instancia de contenedor.</span><span class="sxs-lookup"><span data-stu-id="82c28-150">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]

## <a name="delete-a-container-group"></a><span data-ttu-id="82c28-151">Eliminación de un grupo de contenedores</span><span class="sxs-lookup"><span data-stu-id="82c28-151">Delete a container group</span></span>

<span data-ttu-id="82c28-152">En este ejemplo se eliminan varios grupos de contenedores de un grupo de recursos, así como el grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="82c28-152">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a><span data-ttu-id="82c28-153">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="82c28-153">Next steps</span></span>

* <span data-ttu-id="82c28-154">El código fuente de los ejemplos anteriores se encuentra en GitHub:</span><span class="sxs-lookup"><span data-stu-id="82c28-154">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="82c28-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="82c28-155">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="82c28-156">Más ejemplos de código de Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="82c28-156">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="82c28-157">[Ejemplos de código de Azure][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="82c28-157">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="82c28-158">Vea más [ejemplos de código de Python][samples-python] que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="82c28-158">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82c28-159">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="82c28-159">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient