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
# <a name="hdinsight-python-management-sdk-preview"></a>Versión preliminar del SDK de administración de HDInsight para Python

## <a name="overview"></a>Información general

El SDK de HDInsight para Python proporciona clases y métodos que permiten administrar los clústeres de HDInsight. Incluye operaciones para crear, eliminar, actualizar, enumerar, escalar, ejecutar acciones de script, supervisar y obtener propiedades de clústeres de HDInsight y mucho más.

## <a name="prerequisites"></a>Requisitos previos

* Una cuenta de Azure. Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>Instalación del SDK

El SDK de HDInsight para Python se puede encontrar en el [Índice de paquetes de Python](https://pypi.org/project/azure-mgmt-hdinsight/) y se puede instalar mediante la ejecución de: 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>Autenticación

En primer lugar, el SDK necesita autenticarse en su suscripción de Azure.  Siga el ejemplo siguiente para crear una entidad de servicio y usarla para la autenticación. Una vez hecho esto, tendrá una instancia de `HDInsightManagementClient`, que contiene muchos métodos que pueden usarse para realizar operaciones de administración (se describen en las secciones siguientes).

> [!NOTE]
> Además del siguiente ejemplo, hay otras maneras de autenticar que podrían ser más adecuadas para sus necesidades. Todos los métodos se describen aquí: [Autenticación con las bibliotecas de administración de Azure para Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>Ejemplo de autenticación con una entidad de servicio

En primer lugar, inicie sesión en [Azure Cloud Shell](https://shell.azure.com/bash). Compruebe que está usando la suscripción en la que desea crear la entidad de servicio. 

```azurecli-interactive
az account show
```

La información de la suscripción se muestra en formato JSON.

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

Si no ha iniciado sesión en la suscripción correcta, ejecute lo siguiente para seleccionar la correcta: 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Si aún no ha registrado el proveedor de recursos de HDInsight con otro método (por ejemplo, creando un clúster de HDInsight mediante Azure Portal), deberá hacerlo una vez antes de poder realizar la autenticación. Se puede hacer desde [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

A continuación, elija un nombre para la entidad de servicio y créela con el siguiente comando:

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

La información de la entidad de servicio se muestra con formato JSON.

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
Copie el siguiente fragmento de código de Python y rellene `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` y `SUBSCRIPTION_ID` con las cadenas del código JSON que se devolvió después de ejecutar el comando para crear la entidad de servicio.

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


## <a name="cluster-management"></a>Administración de clústeres

> [!NOTE]
> En esta sección se da por supuesto que ya ha autenticado y construido una instancia de `HDInsightManagementClient`, y que la ha almacenado en una variable llamada `client`. En la sección Autenticación anterior encontrará las instrucciones para autenticarse y obtener un `HDInsightManagementClient`.

### <a name="create-a-cluster"></a>Creación de un clúster

Para crear un nuevo clúster, se puede llamar a `client.clusters.create()`. 

#### <a name="example"></a>Ejemplo

En este ejemplo se muestra cómo crear un clúster de Spark con dos nodos principales y un nodo de trabajo.

> [!NOTE]
> En primer lugar debe crear un grupo de recursos y la cuenta de almacenamiento, tal y como se explica más adelante. Si ya los ha creado, puede omitir estos pasos.

##### <a name="creating-a-resource-group"></a>Creación de un grupo de recursos

Puede crear un grupo de recursos con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>Creación de una cuenta de almacenamiento

Puede crear una cuenta de almacenamiento con [Azure Cloud Shell](https://shell.azure.com/bash), con el siguiente comando:
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
Ahora, ejecute el siguiente comando para obtener la clave de la cuenta de almacenamiento (que necesitará para crear un clúster):
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
El siguiente fragmento de código de Python crea un clúster de Spark con dos nodos principales y un nodo de trabajo. Rellene las variables en blanco tal y como se explica en los comentarios y no dude en cambiar otros parámetros para que se adapten a sus necesidades específicas.

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

### <a name="get-cluster-details"></a>Obtención de los detalles del clúster

Para obtener las propiedades de un clúster determinado:

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Ejemplo

Puede usar `get` para confirmar que ha creado correctamente el clúster.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

La salida debe ser similar a la siguiente:

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>Lista de clústeres

#### <a name="list-clusters-under-the-subscription"></a>Lista de clústeres de la suscripción

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>Lista de clústeres por grupo de recursos

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> Tanto `list()` como `list_by_resource_group()` devuelven un objeto `ClusterPaged`. Una llamada a `advance_page()` devuelve la lista de clústeres de esa página y hace avanzar el objeto `ClusterPaged` a la página siguiente. Esto se puede repetir hasta que se produzca una excepción `StopIteration`, que indica que no existen más páginas.

#### <a name="example"></a>Ejemplo

El ejemplo siguiente imprime las propiedades de todos los clústeres de la suscripción actual:

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>Eliminación de un clúster

Para eliminar un clúster:

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>Actualización de las etiquetas del clúster

Puede actualizar las etiquetas de un clúster determinado de este modo:

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>Ejemplo

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="scale-cluster"></a>Escalado de clústeres

Para escalar el número de nodos de trabajo de un clúster determinado, puede especificar un nuevo tamaño:

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>Supervisión de clústeres

El SDK de administración de HDInsight también puede utilizarse para administrar la supervisión en los clústeres mediante Operations Management Suite (OMS).

### <a name="enable-oms-monitoring"></a>Habilitación de OMS Monitoring

> [!NOTE]
> Para habilitar OMS Monitoring, debe tener un área de trabajo de Log Analytics. Si aún no ha creado una, consulte cómo hacerlo aquí: [Creación de un área de trabajo de Log Analytics en Azure Portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

Para habilitar OMS Monitoring en el clúster:

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>Ver el estado de OMS Monitoring

Para obtener el estado de OMS en el clúster:

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>Deshabilitación de OMS Monitoring

Para deshabilitar OMS en el clúster:

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>Acciones de script

HDInsight proporciona un método de configuración llamado acciones de script, que invoca scripts personalizados para personalizar el clúster.
> [!NOTE]
> Para más información sobre cómo usar las acciones de script, consulte [Personalización de clústeres de HDInsight basados en Linux mediante la acción de script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>Ejecución de acciones de script
Para ejecutar acciones de script en un clúster determinado:

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>Eliminación de una acción de script

Para eliminar una acción de script persistente específica en un clúster determinado:

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>Lista de acciones de script persistentes

> [!NOTE]
> `list()` y `list_persisted_scripts()` devuelven un objeto `RuntimeScriptActionDetailPaged`. Una llamada a `advance_page()` devuelve la lista de `RuntimeScriptActionDetail` de esa página y hace avanzar el objeto `RuntimeScriptActionDetailPaged` a la página siguiente. Esto se puede repetir hasta que se produzca una excepción `StopIteration`, que indica que no existen más páginas. Observe el ejemplo siguiente.

Para mostrar una lista de todas las acciones de script persistentes para el clúster especificado:
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Ejemplo

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>Lista del historial de ejecución de todos los scripts

Para mostrar una lista del historial de ejecución de todos los scripts para el clúster especificado:

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>Ejemplo

Este ejemplo imprime todos los detalles de todas las ejecuciones de script pasadas.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
