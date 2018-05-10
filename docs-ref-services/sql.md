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
---
# <a name="azure-sql-database-libraries-for-python"></a>Bibliotecas Azure SQL Database para Python

## <a name="overview"></a>Información general

Trabaje con datos almacenados en [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) desde Python con el [controlador de base de datos de ODBC](https://github.com/mkleehammer/pyodbc/wiki/Drivers-and-Driver-Managers) de pyodbc. Consulte nuestra [guía de inicio rápido](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) sobre la conexión a una base de datos SQL de Azure y el uso de instrucciones Transact-SQL para consultar los datos y comenzar el [ejemplo](https://github.com/mkleehammer/pyodbc/wiki/Getting-started) con pyodbc.

## <a name="install-odbc-driver-and-pyodbc"></a>Instalación del controlador ODBC y pyodbc

```bash
pip install pyodbc
```
Puede encontrar [aquí](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) más información sobre cómo instalar las bibliotecas de comunicación de python y base de datos.

## <a name="connect-and-execute-a-sql-query"></a>Conexión y ejecución de una consulta SQL

### <a name="connect-to-a-sql-database"></a>Conexión a una base de datos SQL

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

### <a name="execute-a-sql-query"></a>Ejecución de una consulta SQL

```python
cursor.execute("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName FROM [SalesLT].[ProductCategory] pc JOIN [SalesLT].[Product] p ON pc.productcategoryid = p.productcategoryid")
row = cursor.fetchone()
while row:
    print (str(row[0]) + " " + str(row[1]))
    row = cursor.fetchone()
```

> [!div class="nextstepaction"]
> [ejemplo de pyodbc](https://github.com/mkleehammer/pyodbc/wiki/Getting-started)

## <a name="connecting-to-orms"></a>Conexión a ORM

pyodbc funciona con otros ORM como [SQLAlchemy](http://docs.sqlalchemy.org/en/latest/dialects/mssql.html?highlight=pyodbc#module-sqlalchemy.dialects.mssql.pyodbc) y [Django](https://github.com/lionheart/django-pyodbc/). 

## <a name="management-apipythonapioverviewazuresqlmanagement"></a>[API de administración](/python/api/overview/azure/sql/management)

Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración. 

```bash
pip install azure-common
pip install azure-mgmt-sql
pip install azure-mgmt-resource
```

## <a name="example"></a>Ejemplo

Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.

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
> [Explorar las API de administración](/python/api/overview/azure/sql/management)

