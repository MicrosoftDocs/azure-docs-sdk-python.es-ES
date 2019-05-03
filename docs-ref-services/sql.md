---
title: Bibliotecas Azure SQL Database para Python
description: Conecte con Azure SQL Database mediante el controlador ODBC y pyodbc o administre las instancias de Azure SQL con la API de administración.
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 01/09/2018
ms.topic: reference
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: 5b73977fb58ed3cb17d675784da921b0e199d165
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/08/2018
ms.locfileid: "33901358"
---
# <a name="azure-sql-database-libraries-for-python"></a><span data-ttu-id="a4dc0-103">Bibliotecas Azure SQL Database para Python</span><span class="sxs-lookup"><span data-stu-id="a4dc0-103">Azure SQL Database libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="a4dc0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="a4dc0-104">Overview</span></span>

<span data-ttu-id="a4dc0-105">Trabaje con datos almacenados en [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) desde Python con el [controlador de base de datos de ODBC](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers) de pyodbc.</span><span class="sxs-lookup"><span data-stu-id="a4dc0-105">Work with data stored in [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) from Python with the pyodbc [ODBC database driver](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers).</span></span> <span data-ttu-id="a4dc0-106">Consulte nuestra [guía de inicio rápido](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) sobre la conexión a una base de datos de Azure SQL y el uso de instrucciones Transact-SQL para consultar los datos y comenzar el [ejemplo](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) con pyodbc.</span><span class="sxs-lookup"><span data-stu-id="a4dc0-106">View our [quickstart](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) on connecting to an Azure SQL database and using Transact-SQL statements to query data and getting started [sample](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) with pyodbc.</span></span>

## <a name="install-odbc-driver-and-pyodbc"></a><span data-ttu-id="a4dc0-107">Instalación del controlador ODBC y pyodbc</span><span class="sxs-lookup"><span data-stu-id="a4dc0-107">Install ODBC driver and pyodbc</span></span>

```bash
pip install pyodbc
```
<span data-ttu-id="a4dc0-108">Puede encontrar [aquí](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) más información sobre cómo instalar las bibliotecas de comunicación de python y base de datos.</span><span class="sxs-lookup"><span data-stu-id="a4dc0-108">More [details](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) about installing the python and database communication libraries.</span></span>

## <a name="connect-and-execute-a-sql-query"></a><span data-ttu-id="a4dc0-109">Conexión y ejecución de una consulta SQL</span><span class="sxs-lookup"><span data-stu-id="a4dc0-109">Connect and execute a SQL query</span></span>

### <a name="connect-to-a-sql-database"></a><span data-ttu-id="a4dc0-110">Conexión a una base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="a4dc0-110">Connect to a SQL database</span></span>

```python
import pyodbc

server = 'your_server.database.windows.net'
database = 'your_database'
username = 'your_username'
password = 'your_password'
driver= '{ODBC Driver 13 for SQL Server}'

cnxn = pyodbc.connect('DRIVER='+driver+';PORT=1433;SERVER='+server+';PORT=1443;DATABASE='+database+';UID='+username+';PWD='+ password)
cursor = cnxn.cursor()
```

### <a name="execute-a-sql-query"></a><span data-ttu-id="a4dc0-111">Ejecución de una consulta SQL</span><span class="sxs-lookup"><span data-stu-id="a4dc0-111">Execute a SQL query</span></span>

```python
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4dc0-112">ejemplo de pyodbc</span><span class="sxs-lookup"><span data-stu-id="a4dc0-112">pyodbc sample</span></span>](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)

## <a name="connecting-to-orms"></a><span data-ttu-id="a4dc0-113">Conexión a ORM</span><span class="sxs-lookup"><span data-stu-id="a4dc0-113">Connecting to ORMs</span></span>

<span data-ttu-id="a4dc0-114">pyodbc funciona con otros ORM como [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) y [Django](https://github.com/lionheart/django-pyodbc/).</span><span class="sxs-lookup"><span data-stu-id="a4dc0-114">pyodbc works with other ORMs such as [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) and [Django](https://github.com/lionheart/django-pyodbc/).</span></span> 

## <a name="management-apipythonapioverviewazuresqlmanagement"></a>[<span data-ttu-id="a4dc0-115">API de administración</span><span class="sxs-lookup"><span data-stu-id="a4dc0-115">Management API</span></span>](/python/api/overview/azure/sql/management)

<span data-ttu-id="a4dc0-116">Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="a4dc0-116">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span> 

```bash
pip install azure-common
pip install azure-mgmt-sql
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="a4dc0-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="a4dc0-117">Example</span></span>

<span data-ttu-id="a4dc0-118">Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="a4dc0-118">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.sql import SqlManagementClient

RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_SERVER = 'yourvirtualsqlserver'
SQL_DB = 'YOUR_SQLDB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

# create resource client
resource_client = get_client_from_cli_profile(ResourceManagementClient)
# create resource group
resource_client.resource_groups.create_or_update(RESOURCE_GROUP, {'location': LOCATION})

sql_client = get_client_from_cli_profile(SqlManagementClient)

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Create a SQL database in the Basic tier
database = sql_client.databases.create_or_update(
    RESOURCE_GROUP,
    SQL_SERVER,
    SQL_DB,
    {
        'location': LOCATION,
        'collation': 'SQL_Latin1_General_CP1_CI_AS',
        'create_mode': 'default',
        'requested_service_objective_name': 'Basic'
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="a4dc0-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="a4dc0-119">Explore the Management APIs</span></span>](/python/api/overview/azure/sql/management)

