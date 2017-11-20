---
title: "Introducción a las bibliotecas de Azure para Python"
description: "Introducción a las bibliotecas de Azure para Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: get-started
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 848ca9dc40000e68e5e3cea3af8b8a0d22747881
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-azure-libraries-for-python"></a><span data-ttu-id="e8cca-104">Introducción a las bibliotecas de Azure para Python</span><span class="sxs-lookup"><span data-stu-id="e8cca-104">Get started with the Azure libraries for Python</span></span>

<span data-ttu-id="e8cca-105">Esta guía muestra cómo utilizar diversas bibliotecas de Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="e8cca-105">This guide demonstrates the usage of several Azure libraries for Python.</span></span>  <span data-ttu-id="e8cca-106">Configurará la autenticación, creará y usará una cuenta de Azure Storage, creará y usará una instancia de Azure SQL Database, implementará algunas máquinas virtuales e implementará una aplicación web de Azure App Service desde GitHub.</span><span class="sxs-lookup"><span data-stu-id="e8cca-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8cca-107">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e8cca-107">Prerequisites</span></span>

- <span data-ttu-id="e8cca-108">Una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="e8cca-108">An Azure account.</span></span> <span data-ttu-id="e8cca-109">Si no tiene una, [obtenga la versión de evaluación gratuita](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e8cca-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
- [<span data-ttu-id="e8cca-110">Python</span><span class="sxs-lookup"><span data-stu-id="e8cca-110">Python</span></span>](https://www.python.org/downloads/)
- <span data-ttu-id="e8cca-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) o [CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="e8cca-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

[!INCLUDE [azure-cloud-shell](../docs-ref-conceptual/includes/cloud-shell-try-it.md)]

## <a name="set-up-authentication"></a><span data-ttu-id="e8cca-112">Configuración de la autenticación</span><span class="sxs-lookup"><span data-stu-id="e8cca-112">Set up authentication</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e8cca-113">Esto se debe usar como inicio rápido a la experiencia del desarrollador.</span><span class="sxs-lookup"><span data-stu-id="e8cca-113">This should be used as quick start developer experience.</span></span> <span data-ttu-id="e8cca-114">Con fines de producción, use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) o su propio sistema de credenciales.</span><span class="sxs-lookup"><span data-stu-id="e8cca-114">For production purposes, use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) or your own credentials system.</span></span>
> <span data-ttu-id="e8cca-115">Cualquier cambio en la configuración de la CLI afectará a la ejecución del SDK.</span><span class="sxs-lookup"><span data-stu-id="e8cca-115">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="e8cca-116">El SDK es capaz de crear a un cliente con su suscripción activa de la CLI.</span><span class="sxs-lookup"><span data-stu-id="e8cca-116">The SDK is able to create a client using your CLI active subscription.</span></span>

<span data-ttu-id="e8cca-117">Para definir las credenciales activas, utilice [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e8cca-117">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="e8cca-118">El identificador predeterminado de la suscripción puede ser el que ya tiene o puede definirlo con [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e8cca-118">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```
## <a name="create-a-virtual-environment"></a><span data-ttu-id="e8cca-119">Creación de un entorno virtual</span><span class="sxs-lookup"><span data-stu-id="e8cca-119">Create a virtual environment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8cca-120">La creación de un entorno virtual es opcional, pero es muy recomendable.</span><span class="sxs-lookup"><span data-stu-id="e8cca-120">Create a virtual environment is optional, but we strongly suggest you to do it.</span></span>

<span data-ttu-id="e8cca-121">Cree un entorno virtual en Bash (Linux o [Bash para Windows](https://msdn.microsoft.com/commandline/wsl/about)):</span><span class="sxs-lookup"><span data-stu-id="e8cca-121">Create a virtual environment in Bash (Linux or [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about)):</span></span>
```bash
pip install virtualenv
virtualenv mytestenv
cd mytestenv
source ./bin/activate
```

<span data-ttu-id="e8cca-122">Cree un entorno virtual en Powershell:</span><span class="sxs-lookup"><span data-stu-id="e8cca-122">Create a virtual environment in Powershell:</span></span>
```powershell
pip install virtualenv
virtualenv mytestenv
cd mytestenv
.\Scripts\activate
```

> [!IMPORTANT]
> <span data-ttu-id="e8cca-123">Tenga en cuenta que si usa [VSCode](https://code.visualstudio.com/) y la [extensión Python](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python), puede iniciarlo mediante `code .` y obtener su entorno configurado.</span><span class="sxs-lookup"><span data-stu-id="e8cca-123">Note that if you use [VSCode](https://code.visualstudio.com/) and the [Python extension](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python),  you can start it using `code .` and get your environment configured.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="e8cca-124">Creación de una máquina virtual con Linux</span><span class="sxs-lookup"><span data-stu-id="e8cca-124">Create a Linux virtual machine</span></span>
<span data-ttu-id="e8cca-125">Este código crea una nueva máquina virtual Linux con el nombre `testLinuxVM` en un grupo de recursos `sampleVmResourceGroup` que se ejecuta en la región de Azure este de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="e8cca-125">This code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleVmResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="e8cca-126">Autenticación:</span><span class="sxs-lookup"><span data-stu-id="e8cca-126">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e8cca-127">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e8cca-127">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus --n sampleVmResourceGroup
```

<span data-ttu-id="e8cca-128">Cree una red virtual y una subred:</span><span class="sxs-lookup"><span data-stu-id="e8cca-128">Create a virtual network and subnet:</span></span>
```azurecli-interactive
az network vnet create -g sampleVmResourceGroup -n azure-sample-vnet --address-prefix 10.0.0.0/16 --subnet-name azure-sample-subnet --subnet-prefix 10.0.0.0/24
```

<span data-ttu-id="e8cca-129">Cree una dirección IP pública:</span><span class="sxs-lookup"><span data-stu-id="e8cca-129">Create a public IP address:</span></span>
```azurecli-interactive
az network public-ip create -g sampleVmResourceGroup -n azure-sample-ip --allocation-method Dynamic --version IPv6
```
<span data-ttu-id="e8cca-130">Cree un cliente de interfaz de red:</span><span class="sxs-lookup"><span data-stu-id="e8cca-130">Create a network interface client:</span></span>
```azurecli-interactive
az network nic create -g sampleVmResourceGroup --vnet-name azure-sample-vnet --subnet azure-sample-subnet -n azure-sample-nic --public-ip-address azure-sample-ip
```

```python
from azure.mgmt.network import NetworkManagementClient
from azure.mgmt.compute import ComputeManagementClient
from azure.common.client_factory import get_client_from_cli_profile

# Azure Datacenter
LOCATION = 'eastus'

# Resource Group
GROUP_NAME = 'sampleVmResourceGroup'

# Network
VNET_NAME = 'azure-sample-vnet'
SUBNET_NAME = 'azure-sample-subnet'

# VM
NIC_NAME = 'azure-sample-nic'
VM_NAME = 'testLinuxVM'

USERNAME = 'userlogin'
PASSWORD = 'Pa$$w0rd91'

IP_ADDRESS_NAME='azure-sample-ip'

VM_REFERENCE = {
    'linux': {
        'publisher': 'Canonical',
        'offer': 'UbuntuServer',
        'sku': '16.04.0-LTS',
        'version': 'latest'
    },
    'windows': {
        'publisher': 'MicrosoftWindowsServerEssentials',
        'offer': 'WindowsServerEssentials',
        'sku': 'WindowsServerEssentials',
        'version': 'latest'
    }
}


def run_example():

    compute_client = get_client_from_cli_profile(ComputeManagementClient)
    network_client = get_client_from_cli_profile(NetworkManagementClient)

    # get nic id
    nic = network_client.network_interfaces.get(GROUP_NAME, NIC_NAME)

    # Create Linux VM
    print('\nCreating Linux Virtual Machine')
    vm_parameters = create_vm_parameters(nic.id, VM_REFERENCE['linux'])
    print(vm_parameters)
    async_vm_creation = compute_client.virtual_machines.create_or_update(
        GROUP_NAME, VM_NAME, vm_parameters)
    async_vm_creation.wait()


def create_vm_parameters(nic_id, vm_reference):
    """Create the VM parameters structure.
    """
    return {
        'location': LOCATION,
        'os_profile': {
            'computer_name': VM_NAME,
            'admin_username': USERNAME,
            'admin_password': PASSWORD
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': vm_reference['publisher'],
                'offer': vm_reference['offer'],
                'sku': vm_reference['sku'],
                'version': vm_reference['version']
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': nic_id,
            }]
        },
    }


if __name__ == "__main__":
    run_example()
```

<span data-ttu-id="e8cca-131">Cuando finalice el programa, compruebe la máquina virtual en la suscripción con la CLI de Azure 2.0:</span><span class="sxs-lookup"><span data-stu-id="e8cca-131">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="e8cca-132">Una vez que haya comprobado que el código ha funcionado, utilice la CLI para eliminar la máquina virtual y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="e8cca-132">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="e8cca-133">Implementación de una aplicación web desde un repositorio de GitHub</span><span class="sxs-lookup"><span data-stu-id="e8cca-133">Deploy a web app from a GitHub repo</span></span>
<span data-ttu-id="e8cca-134">Este código implementa una aplicación web de Flask de la rama `master` de un repositorio de GitHub en una nueva [aplicación web de Azure App Service](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) que se ejecuta en el nivel gratuito.</span><span class="sxs-lookup"><span data-stu-id="e8cca-134">This code deploys a Flask web application from the `master` branch in a GitHub repo in to a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free tier.</span></span> 

<span data-ttu-id="e8cca-135">Antes de empezar you begin: bifurque https://github.com/Azure-Samples/python-docs-hello-world</span><span class="sxs-lookup"><span data-stu-id="e8cca-135">Before you begin: Fork https://github.com/Azure-Samples/python-docs-hello-world</span></span>

<span data-ttu-id="e8cca-136">Autenticación:</span><span class="sxs-lookup"><span data-stu-id="e8cca-136">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e8cca-137">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e8cca-137">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleWebResourceGroup
```

<span data-ttu-id="e8cca-138">Cree un plan gratuito de App Service:</span><span class="sxs-lookup"><span data-stu-id="e8cca-138">Create a free app service plan:</span></span>
```azurecli-interactive
az appservice plan create -g sampleWebResourceGroup -n sampleFreePlan  --sku Free
```

```python
from azure.mgmt.web import WebSiteManagementClient
from azure.mgmt.web.models import Site, SiteSourceControl, SiteConfig
from azure.common.client_factory import get_client_from_cli_profile

RESOURCE_GROUP_NAME = 'sampleWebResourceGroup'
SERVICE_PLAN_NAME = 'sampleFreePlanName'
WEB_APP_NAME = 'sampleflaskapp123'
REPO_URL = 'GitHub_Repository_URL'

#log in
web_client = get_client_from_cli_profile(WebSiteManagementClient)

# get service plan id
service_plan = web_client.app_service_plans.get(RESOURCE_GROUP_NAME, SERVICE_PLAN_NAME)

# create a web app
siteConfiguration = SiteConfig(
    python_version='3.4',
)
site_async_operation = web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=service_plan.id,
        site_config=siteConfiguration
    ),
)

site = site_async_operation.result()
print('created webapp: ' + site.default_host_name)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url= REPO_URL,
        branch='master'
    )
)

source_control = source_control_async_operation.result()
print("added source control to: " + source_control.name + "azurewebsites.net")
```

<span data-ttu-id="e8cca-139">Abra un explorador que apunta a la aplicación mediante la CLI:</span><span class="sxs-lookup"><span data-stu-id="e8cca-139">Open a browser pointed to the application using the CLI:</span></span>
```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="e8cca-140">Elimine la aplicación web y el plan de su suscripción una vez que haya comprobado la implementación.</span><span class="sxs-lookup"><span data-stu-id="e8cca-140">Remove the web app and plan from your subscription once you've verified the deployment.</span></span> 
```azurecli-interactive
az group delete --name sampleWebResourceGroup
```


## <a name="connect-to-a-sql-database"></a><span data-ttu-id="e8cca-141">Conexión a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="e8cca-141">Connect to a SQL database</span></span>
<span data-ttu-id="e8cca-142">Este código crea una nueva base de datos SQL con una regla de firewall que permita el acceso remoto y, a continuación, se conecta a ella mediante el controlador ODBC de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e8cca-142">This code creates a new SQL database with a firewall rule allowing remote access, and then connected to it using the Microsoft ODBC driver.</span></span> <span data-ttu-id="e8cca-143">Pyodbc usa Microsoft ODBC Driver on Linux para conectarse a bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="e8cca-143">Pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span> 

<span data-ttu-id="e8cca-144">Autenticación:</span><span class="sxs-lookup"><span data-stu-id="e8cca-144">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e8cca-145">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e8cca-145">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n azure-sample-group
```

<span data-ttu-id="e8cca-146">Cree un servidor SQL:</span><span class="sxs-lookup"><span data-stu-id="e8cca-146">Create a SQL server:</span></span>
```azurecli-interactive
az sql server create --admin-password HusH_Sec4et --admin-user mysecretname -l eastus -n samplesqlserver123 -g azure-sample-group
```

<span data-ttu-id="e8cca-147">Agregue una regla de firewall:</span><span class="sxs-lookup"><span data-stu-id="e8cca-147">Add firewall rule:</span></span>
```azurecli-interactive
az sql server firewall-rule create --end-ip-address 167.220.0.235 --name firewall_rule_name_123.123.123.123 --resource-group azure-sample-group --server samplesqlserver123 --start-ip-address 123.123.123.123
```

<span data-ttu-id="e8cca-148">Cree una base de datos SQL:</span><span class="sxs-lookup"><span data-stu-id="e8cca-148">Create a SQL database:</span></span>
```azurecli-interactive
az sql db create --name sample-db --resource-group azure-sample-group --server samplesqlserver123
```


```python
from azure.mgmt.sql import SqlManagementClient
from azure.common.client_factory import get_client_from_cli_profile
import pyodbc

LOCATION = 'eastus'
GROUP_NAME = 'azure-sample-group'
SERVER_NAME = 'samplesqlserver123'
DATABASE_NAME = 'sample-db'
USER_NAME ='mysecretname'
PASSWORD='HusH_Sec4et'

# authenticate
sql_client = get_client_from_cli_profile(SqlManagementClient)


def run_example():
    # Get SQL database
    print('Get SQL database')
    database = sql_client.databases.get(
        GROUP_NAME,
        SERVER_NAME,
        DATABASE_NAME
    )
    print(database)
    print("\n\n")


def create_and_insert():
    server = SERVER_NAME+'.database.windows.net'
    database = DATABASE_NAME
    username = USER_NAME
    password = PASSWORD
    driver = '{ODBC Driver 13 for SQL Server}'
    cnxn = pyodbc.connect(
        'DRIVER=' + driver + ';PORT=1433;SERVER=' + server + ';PORT=1443;DATABASE=' + database + ';UID=' + username + ';PWD=' + password)
    cursor = cnxn.cursor()
    tsql = "CREATE TABLE CLOUD (name varchar(255), code int);"
    tsqlInsert = "INSERT INTO CLOUD (name, code) VALUES ('Azure', 1); "
    selectValues = "SELECT * FROM CLOUD"
    with cursor.execute(tsql):
        print('Successfully created table!')
    with cursor.execute(tsqlInsert):
        print('Successfully inserted data into table')
    cursor.execute(selectValues)
    row = cursor.fetchone()
    while row:
        print(str(row[0]) + " " + str(row[1]))
        row = cursor.fetchone()
    cnxn.commit()

if __name__ == "__main__":
    run_example()
    create_and_insert()
```

<span data-ttu-id="e8cca-149">Una vez que haya comprobado que el código funciona, use la CLI para eliminar la base de datos SQL y sus recursos.</span><span class="sxs-lookup"><span data-stu-id="e8cca-149">Once you've verified that the code worked, use the CLI to delete the SQL database and its resources.</span></span>

```azurecli-interactive
az group delete --name azure-sample-group
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="e8cca-150">Escritura de un blob en una nueva cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e8cca-150">Write a blob into a new storage account</span></span>

<span data-ttu-id="e8cca-151">Autenticación:</span><span class="sxs-lookup"><span data-stu-id="e8cca-151">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="e8cca-152">Cree un grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="e8cca-152">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleStorageResourceGroup
```

<span data-ttu-id="e8cca-153">Cree una cuenta de almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="e8cca-153">Create a storage account:</span></span>
```azurecli-interactive
az storage account create -n samplestorageaccountname -g sampleStorageResourceGroup -l eastus --sku Standard_RAGRS
```

<span data-ttu-id="e8cca-154">Este código crea una [cuenta de almacenamiento de Azure](https://docs.microsoft.com/azure/storage/storage-introduction) y, a continuación, usa las bibliotecas de Azure Storage para Python para crear un nuevo archivo html en la nube.</span><span class="sxs-lookup"><span data-stu-id="e8cca-154">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Python to create a new html file in the cloud.</span></span> 
```python
from azure.storage import CloudStorageAccount
from azure.storage.blob import PublicAccess
from azure.storage.blob.models import ContentSettings
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.storage import StorageManagementClient

RESOURCE_GROUP = 'sampleStorageResourceGroup'
STORAGE_ACCOUNT_NAME = 'samplestorageaccountname'
CONTAINER_NAME = 'samplecontainername'

# log in
storage_client = get_client_from_cli_profile(StorageManagementClient)

# create a public storage container to hold the file
storage_keys = storage_client.storage_accounts.list_keys(RESOURCE_GROUP, STORAGE_ACCOUNT_NAME)
storage_keys = {v.key_name: v.value for v in storage_keys.keys}

storage_client = CloudStorageAccount(STORAGE_ACCOUNT_NAME, storage_keys['key1'])
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(CONTAINER_NAME, public_access=PublicAccess.Container)

blob_service.create_blob_from_bytes(
    CONTAINER_NAME,
    'helloworld.html',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url(CONTAINER_NAME, 'helloworld.html'))
```
<span data-ttu-id="e8cca-155">Para comprobar que el contenido se ha cargado correctamente, vaya a la dirección URL impresa.</span><span class="sxs-lookup"><span data-stu-id="e8cca-155">To verify content successfully uploaded, navigate to the url printed.</span></span> 

<span data-ttu-id="e8cca-156">Limpie la cuenta de almacenamiento mediante la CLI:</span><span class="sxs-lookup"><span data-stu-id="e8cca-156">Clean up the storage account using the CLI:</span></span>
```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="e8cca-157">Ver más ejemplos</span><span class="sxs-lookup"><span data-stu-id="e8cca-157">Explore more samples</span></span>

<span data-ttu-id="e8cca-158">Para más información sobre cómo usar las bibliotecas de administración de Azure para Python para administrar los recursos y automatizar las tareas, vea el código de ejemplo para [máquinas virtuales](python-sdk-azure-web-apps-samples.md), [aplicaciones web](python-sdk-azure-web-apps-samples.md) y [base de datos SQL](python-sdk-azure-sql-database-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e8cca-158">To learn more about how to use the Azure management libraries for Python to manage resources and automate tasks, see our sample code for [virtual machines](python-sdk-azure-web-apps-samples.md), [web apps](python-sdk-azure-web-apps-samples.md) and [SQL database](python-sdk-azure-sql-database-samples.md).</span></span>


## <a name="reference"></a><span data-ttu-id="e8cca-159">Referencia</span><span class="sxs-lookup"><span data-stu-id="e8cca-159">Reference</span></span>

<span data-ttu-id="e8cca-160">Hay una [referencia](/python/api/overview/azure/?view=azure-python) disponible para todos los paquetes.</span><span class="sxs-lookup"><span data-stu-id="e8cca-160">A [reference](/python/api/overview/azure/?view=azure-python) is available for all packages.</span></span>
