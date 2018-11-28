---
title: Versión preliminar del SDK de Azure HDInsight para Python
description: Referencia del SDK de Azure HDInsight para Python. El SDK de HDInsight para Python proporciona clases y métodos que permiten administrar los clústeres de HDInsight.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 42e1e36b5854fda93188564be3ed3064b9ba4435
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277479"
---
# <a name="hdinsight-python-management-sdk-preview"></a><span data-ttu-id="e963a-104">Versión preliminar del SDK de administración de HDInsight para Python</span><span class="sxs-lookup"><span data-stu-id="e963a-104">HDInsight Python Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="e963a-105">Información general</span><span class="sxs-lookup"><span data-stu-id="e963a-105">Overview</span></span>

<span data-ttu-id="e963a-106">El SDK de HDInsight para Python proporciona clases y métodos que permiten administrar los clústeres de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e963a-106">The HDInsight Python SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="e963a-107">Incluye operaciones para crear, eliminar, actualizar, enumerar, escalar, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight y mucho más.</span><span class="sxs-lookup"><span data-stu-id="e963a-107">It includes operations to create, delete, update, list, scale, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e963a-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e963a-108">Prerequisites</span></span>

* <span data-ttu-id="e963a-109">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e963a-109">An Azure account.</span></span> <span data-ttu-id="e963a-110">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e963a-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="e963a-111">Python</span><span class="sxs-lookup"><span data-stu-id="e963a-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="e963a-112">pip</span><span class="sxs-lookup"><span data-stu-id="e963a-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="e963a-113">Instalación del SDK</span><span class="sxs-lookup"><span data-stu-id="e963a-113">SDK Installation</span></span>

<span data-ttu-id="e963a-114">El SDK de HDInsight para Python se puede encontrar en el [Índice de paquetes de Python](https://pypi.org/project/azure-mgmt-hdinsight/) y se puede instalar mediante la ejecución de:</span><span class="sxs-lookup"><span data-stu-id="e963a-114">The HDInsight Python SDK can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="e963a-115">Autenticación</span><span class="sxs-lookup"><span data-stu-id="e963a-115">Authentication</span></span>

<span data-ttu-id="e963a-116">En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="e963a-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="e963a-117">Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e963a-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="e963a-118">Una vez hecho esto, tendrá una instancia de `HDInsightManagementClient`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).</span><span class="sxs-lookup"><span data-stu-id="e963a-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="e963a-119">Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="e963a-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="e963a-120">Todos los métodos se describen aquí: [Autenticación con las bibliotecas de administración de Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="e963a-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="e963a-121">Ejemplo de autenticación con una entidad de servicio</span><span class="sxs-lookup"><span data-stu-id="e963a-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="e963a-122">En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash).</span><span class="sxs-lookup"><span data-stu-id="e963a-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="e963a-123">Compruebe que está usando la suscripción en la que desea crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e963a-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="e963a-124">La información de la suscripción se muestra en formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e963a-124">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="e963a-125">Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta:</span><span class="sxs-lookup"><span data-stu-id="e963a-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="e963a-126">Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="e963a-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="e963a-127">Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e963a-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="e963a-128">A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e963a-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="e963a-129">La información de la entidad de servicio se muestra con formato JSON.</span><span class="sxs-lookup"><span data-stu-id="e963a-129">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="e963a-130">Copie el siguiente fragmento de código de Python y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="e963a-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a><span data-ttu-id="e963a-131">Administración de clústeres</span><span class="sxs-lookup"><span data-stu-id="e963a-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="e963a-132">En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClient`, y que la ha almacenado en una variable llamada `client`.</span><span class="sxs-lookup"><span data-stu-id="e963a-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="e963a-133">En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClient`.</span><span class="sxs-lookup"><span data-stu-id="e963a-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="e963a-134">Creación de un clúster</span><span class="sxs-lookup"><span data-stu-id="e963a-134">Create a Cluster</span></span>

<span data-ttu-id="e963a-135">Para crear un nuevo clúster, se puede llamar a `client.clusters.create()`.</span><span class="sxs-lookup"><span data-stu-id="e963a-135">A new cluster can be created by calling `client.clusters.create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="e963a-136">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-136">Example</span></span>

<span data-ttu-id="e963a-137">En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e963a-137">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="e963a-138">En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante.</span><span class="sxs-lookup"><span data-stu-id="e963a-138">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="e963a-139">Si ya los ha creado, puede omitir estos pasos.</span><span class="sxs-lookup"><span data-stu-id="e963a-139">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="e963a-140">Creación de un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e963a-140">Creating a Resource Group</span></span>

<span data-ttu-id="e963a-141">Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e963a-141">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="e963a-142">Creación de una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e963a-142">Creating a Storage Account</span></span>

<span data-ttu-id="e963a-143">Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e963a-143">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="e963a-144">Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):</span><span class="sxs-lookup"><span data-stu-id="e963a-144">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="e963a-145">El siguiente fragmento de código de Python crea un clúster de Spark con dos nodos principales y un nodo de trabajo.</span><span class="sxs-lookup"><span data-stu-id="e963a-145">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="e963a-146">Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="e963a-146">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

### <a name="get-cluster-details"></a><span data-ttu-id="e963a-147">Obtención de los detalles del clúster</span><span class="sxs-lookup"><span data-stu-id="e963a-147">Get Cluster Details</span></span>

<span data-ttu-id="e963a-148">Para obtener las propiedades de un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="e963a-148">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e963a-149">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-149">Example</span></span>

<span data-ttu-id="e963a-150">Puede usar `get` para confirmar que ha creado correctamente el clúster.</span><span class="sxs-lookup"><span data-stu-id="e963a-150">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="e963a-151">La salida debe ser similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="e963a-151">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="e963a-152">Lista de clústeres</span><span class="sxs-lookup"><span data-stu-id="e963a-152">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="e963a-153">Lista de clústeres de la suscripción</span><span class="sxs-lookup"><span data-stu-id="e963a-153">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="e963a-154">Lista de clústeres por grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e963a-154">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="e963a-155">Tanto `list()` como `list_by_resource_group()` devuelven un objeto `ClusterPaged`.</span><span class="sxs-lookup"><span data-stu-id="e963a-155">Both `list()` and `list_by_resource_group()` return an `ClusterPaged` object.</span></span> <span data-ttu-id="e963a-156">Una llamada a `advance_page()` devuelve la lista de clústeres de esa página y hace avanzar el objeto `ClusterPaged` a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="e963a-156">Calling `advance_page()` returns the a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="e963a-157">Esto se puede repetir hasta que se produzca una excepción `StopIteration`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="e963a-157">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="e963a-158">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-158">Example</span></span>

<span data-ttu-id="e963a-159">El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:</span><span class="sxs-lookup"><span data-stu-id="e963a-159">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="e963a-160">Eliminación de un clúster</span><span class="sxs-lookup"><span data-stu-id="e963a-160">Delete a Cluster</span></span>

<span data-ttu-id="e963a-161">Para eliminar un clúster:</span><span class="sxs-lookup"><span data-stu-id="e963a-161">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="e963a-162">Actualización de las etiquetas del clúster</span><span class="sxs-lookup"><span data-stu-id="e963a-162">Update Cluster Tags</span></span>

<span data-ttu-id="e963a-163">Puede actualizar las etiquetas de un clúster determinado de este modo:</span><span class="sxs-lookup"><span data-stu-id="e963a-163">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="e963a-164">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-164">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="scale-cluster"></a><span data-ttu-id="e963a-165">Escalado de clústeres</span><span class="sxs-lookup"><span data-stu-id="e963a-165">Scale Cluster</span></span>

<span data-ttu-id="e963a-166">Para escalar el número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño:</span><span class="sxs-lookup"><span data-stu-id="e963a-166">You can scale a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="e963a-167">Supervisión de clústeres</span><span class="sxs-lookup"><span data-stu-id="e963a-167">Cluster Monitoring</span></span>

<span data-ttu-id="e963a-168">El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="e963a-168">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="e963a-169">Habilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="e963a-169">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="e963a-170">Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e963a-170">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="e963a-171">Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="e963a-171">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="e963a-172">Para habilitar OMS Monitoring en el clúster:</span><span class="sxs-lookup"><span data-stu-id="e963a-172">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="e963a-173">Ver el estado de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="e963a-173">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="e963a-174">Para obtener el estado de OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="e963a-174">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="e963a-175">Deshabilitación de OMS Monitoring</span><span class="sxs-lookup"><span data-stu-id="e963a-175">Disable OMS Monitoring</span></span>

<span data-ttu-id="e963a-176">Para deshabilitar OMS en el clúster:</span><span class="sxs-lookup"><span data-stu-id="e963a-176">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="e963a-177">Acciones de script</span><span class="sxs-lookup"><span data-stu-id="e963a-177">Script Actions</span></span>

<span data-ttu-id="e963a-178">HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.</span><span class="sxs-lookup"><span data-stu-id="e963a-178">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="e963a-179">Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="e963a-179">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="e963a-180">Ejecución de acciones de script</span><span class="sxs-lookup"><span data-stu-id="e963a-180">Execute Script Actions</span></span>
<span data-ttu-id="e963a-181">Para ejecutar acciones de script en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="e963a-181">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="e963a-182">Eliminación de una acción de script</span><span class="sxs-lookup"><span data-stu-id="e963a-182">Delete Script Action</span></span>

<span data-ttu-id="e963a-183">Para eliminar una acción de script persistente específica en un clúster determinado:</span><span class="sxs-lookup"><span data-stu-id="e963a-183">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="e963a-184">Lista de acciones de script persistentes</span><span class="sxs-lookup"><span data-stu-id="e963a-184">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="e963a-185">`list()` y `list_persisted_scripts()` devuelven un objeto `RuntimeScriptActionDetailPaged`.</span><span class="sxs-lookup"><span data-stu-id="e963a-185">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="e963a-186">Una llamada a `advance_page()` devuelve la lista de `RuntimeScriptActionDetail` de esa página y hace avanzar el objeto `RuntimeScriptActionDetailPaged` a la página siguiente.</span><span class="sxs-lookup"><span data-stu-id="e963a-186">Calling `advance_page()` returns the a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="e963a-187">Esto se puede repetir hasta que se produzca una excepción `StopIteration`, que indica que no existen más páginas.</span><span class="sxs-lookup"><span data-stu-id="e963a-187">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="e963a-188">Observe el ejemplo siguiente.</span><span class="sxs-lookup"><span data-stu-id="e963a-188">See the example below.</span></span>

<span data-ttu-id="e963a-189">Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="e963a-189">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e963a-190">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-190">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="e963a-191">Lista del historial de ejecución de todos los scripts</span><span class="sxs-lookup"><span data-stu-id="e963a-191">List All Scripts' Execution History</span></span>

<span data-ttu-id="e963a-192">Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:</span><span class="sxs-lookup"><span data-stu-id="e963a-192">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e963a-193">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="e963a-193">Example</span></span>

<span data-ttu-id="e963a-194">Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.</span><span class="sxs-lookup"><span data-stu-id="e963a-194">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
