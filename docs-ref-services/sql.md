---
title: Bibliotecas Azure SQL Database para Python
description: 
keywords: Azure, Python, SDK, API, SQL, Database, pyodbc
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: b580c5011412bc77fd8fd55b709a305be07e2316
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-sql-database-libraries-for-python"></a>Bibliotecas Azure SQL Database para Python

## <a name="overview"></a>Información general

Trabaje con datos almacenados en [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) desde Python con el controlador ODBC de Microsoft y pyodbc. 

## <a name="client-odbc-driver-and-pyodbc"></a>Controlador ODBC de cliente y pyodbc

```bash
pip install pyodbc
```
Pueden encontrar más detalles acerca de cómo instalar las bibliotecas de comunicación de python y base de datos [aquí](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

### <a name="example"></a>Ejemplo

Conéctese a una base de datos SQL y seleccione todos los registros de una tabla.

```python
import pyodbc 

SERVER = 'YOUR_SERVER_NAME.database.windows.net'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_DB_USERNAME'
PASSWORD = 'YOUR_DB_PASSWORD'

DRIVER= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER=' + DRIVER + ';PORT=1433;SERVER=' + SERVER +
    ';PORT=1443;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>API de administración

Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración. 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a>Ejemplo

Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a>Muestras

* [Creación y administración de bases de datos SQL][1]    
* [Uso de Python para conectarse a los datos y consultarlos][2]   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) de ejemplos de Azure SQL Database. 