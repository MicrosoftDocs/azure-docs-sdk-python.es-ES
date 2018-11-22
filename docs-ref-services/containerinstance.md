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
ms.openlocfilehash: 95571e0da6ef82ef045d8c9ba0a5beb0abe9b63a
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52273021"
---
# <a name="azure-container-instances-libraries-for-python"></a>Bibliotecas de Azure Container Instances para Python

Use las bibliotecas de Microsoft Azure Container Instances para Python para crear y administrar instancias de contenedor de Azure. Para más información, consulte la [Introducción a Azure Container Instances](/azure/container-instances/container-instances-overview).

## <a name="management-apis"></a>API de administración

Use la biblioteca de administración para crear y administrar instancias de contenedor en Azure.

Instale el paquete de administración mediante pip:

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>Ejemplo de código fuente

Si desea ver los ejemplos de código siguientes en contexto, los encontrará en el repositorio de GitHub siguiente:

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Autenticación

Una de las formas más sencillas para autenticar los clientes de SDK (por ejemplo, los clientes de Azure Container Instances y Resource Manager en el ejemplo siguiente) es con la [autenticación basada en archivo](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file). La autenticación basada en archivo consulta la variable de entorno `AZURE_AUTH_LOCATION` para obtener la ruta de acceso a un archivo de credenciales. Para usar la autenticación basada en archivo

1. Cree un archivo de credenciales con la [CLI de Azure](/cli/azure) o [Cloud Shell](https://shell.azure.com/):

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   Si usa [Cloud Shell](https://shell.azure.com/) para generar el archivo de credenciales, copie su contenido en un archivo local al que pueda tener acceso la aplicación de Python.

2. Establezca la variable de entorno `AZURE_AUTH_LOCATION` en la ruta de acceso completa del archivo de credenciales generado. Por ejemplo, en Bash:

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

Después de crear el archivo de credenciales y de rellenar la variable de entorno `AZURE_AUTH_LOCATION`, use el método `get_client_from_auth_file` del módulo [client_factory][client_factory] para inicializar los objetos [ResourceManagementClient][ResourceManagementClient] y [ContainerInstanceManagementClient][ContainerInstanceManagementClient].

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Para más información acerca de los métodos de autenticación disponibles en las bibliotecas de administración de Python para Azure, consulte [Autenticación con las bibliotecas de administración de Azure para Python](/python/azure/python-sdk-azure-authenticate).

## <a name="create-container-group---single-container"></a>Creación de un grupo de contenedores: un solo contenedor

En este ejemplo se crea un grupo de contenedores con un solo contenedor

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>Creación de un grupo de contenedores: varios contenedores

En este ejemplo se crea un grupo de contenedores con dos contenedores: un contenedor de aplicaciones y un contenedor asociado.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>Creación de un grupo de contenedores basado en tareas

En este ejemplo se crea un grupo de contenedores con un solo contenedor basado en tareas. En este ejemplo se muestran varias características:

* [Invalidación de la línea de comandos](/azure/container-instances/container-instances-restart-policy#command-line-override): se especifica una línea de comandos personalizada, diferente de la que se especifica en la línea `CMD` del archivo Docker del contenedor. La invalidación de la línea de comandos permite especificar la línea de comandos personalizada que se ejecutará ejecutar durante el inicio del contenedor y que reemplazará la línea de comandos predeterminada incluida en el contenedor. En relación con la ejecución de varios comandos durante el inicio del contenedor, se aplica lo siguiente:

   Si desea ejecutar un **único comando** con varios argumentos de línea de comandos, por ejemplo `echo FOO BAR`, debe proporcionarlos como una lista de cadenas a la propiedad `command` de [Container][Container]. Por ejemplo: 

   `command = ['echo', 'FOO', 'BAR']`

   En cambio, si desea ejecutar **varios comandos** con varios argumentos posibles, debe ejecutar un shell y pasar los comandos encadenados como argumento. Por ejemplo, esto ejecuta los comandos `echo` y `tail`:

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [Variables de entorno](/azure/container-instances/container-instances-environment-variables): se especifican dos variables de entorno para el contenedor en el grupo de contenedores. Use variables de entorno para modificar el comportamiento de un script o aplicación en tiempo de ejecución; de lo contrario, pase información dinámica a una aplicación que se ejecuta en el contenedor.
* [Directiva de reinicio](/azure/container-instances/container-instances-restart-policy): el contenedor está configurado con una directiva de reinicio de "Nunca", que resulta útil para los contenedores basados en tareas que se ejecutan como parte de un trabajo por lotes.
* Sondeo de la operación con [AzureOperationPoller][AzureOperationPoller]: después de invocar el método Create, se sondea la operación para determinar cuándo se ha completado y obtener los registros del grupo de contenedores.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]

## <a name="list-container-groups"></a>Enumeración de grupos de contenedores

En este ejemplo se enumeran los grupos de contenedores de un grupo de recursos y se imprimen algunas de sus propiedades.

Cuando se enumeran grupos de contenedores, el valor de [instance_view][instance_view] de cada grupo es `None`. Para obtener los detalles de los contenedores dentro de un grupo de contenedores, deberá ejecutar [get][containergroupoperations_get] en el grupo de contenedores, que devuelve el grupo con la `instance_view` propiedad rellena. Consulte la sección siguiente, [Obtención de un grupo de contenedores existente](#get-an-existing-container-group), para ver un ejemplo de cómo recorrer en iteración los contenedores de un grupo de contenedores en su `instance_view`.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]

## <a name="get-an-existing-container-group"></a>Obtención de un grupo de contenedores existente

En este ejemplo se obtiene un grupo de contenedores específico que reside en un grupo de recursos y, a continuación, se imprimen algunas de sus propiedades (incluidos sus contenedores) y sus valores.

La [operación get][containergroupoperations_get] devuelve un grupo de contenedor con el valor de [instance_view][instance_view] relleno, lo que permite recorrer en iteración cada contenedor del grupo. Solo la operación `get` rellena la propiedad `instance_vew` del grupo de contenedores. Enumerar los grupos de contenedores de una suscripción o grupo de recursos no rellena instance_view debido a la naturaleza potencialmente costosa de la operación; por ejemplo, cuando se enumeran cientos de grupos de contenedores, cada uno de ellos puede contener a su vez varios contenedores. Tal y como se mencionó anteriormente en la sección [Enumeración de grupos de contenedores](#list-container-groups), después un `list`, se debe ejecutar `get` en un grupo de contenedores específico para obtener información detallada de su instancia de contenedor.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]

## <a name="delete-a-container-group"></a>Eliminación de un grupo de contenedores

En este ejemplo se eliminan varios grupos de contenedores de un grupo de recursos, así como el grupo de recursos.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>Pasos siguientes

* El código fuente de los ejemplos anteriores se encuentra en GitHub:

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* Más ejemplos de código de Azure Container Instances:

  [Ejemplos de código de Azure][samples-aci]

* Vea más [ejemplos de código de Python][samples-python] que puede usar en sus aplicaciones.

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/containerinstance/management)

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