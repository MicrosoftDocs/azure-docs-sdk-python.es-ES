---
title: Bibliotecas de Azure MySQL/PostgreSQL para Python
description: ''
keywords: Azure, Python, SDK, API, SQL, Database, MySQL, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: e3cd84288ad8d49cfcd673506e2db150c02e7918
ms.sourcegitcommit: 16eecfc4ed0e2a8344ce5887327cdf2619ba89e4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2018
ms.locfileid: "39189595"
---
# <a name="azure-mysqlpostgresql-libraries-for-python"></a>Bibliotecas de Azure MySQL/PostgreSQL para Python

## <a name="mysql"></a>MySQL

Trabaje con los recursos y datos almacenados en [Azure Database for MySQL](/azure/mysql/overview) desde Python con el administrador de MySQL y pyodbc.

### <a name="client-odbc-driver-and-pyodbc"></a>Controlador ODBC de cliente y pyodbc

La biblioteca de cliente recomendada para acceder a Azure Database for MySQL es el [controlador ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries). Use el controlador ODBC para conectarse a la base de datos y ejecutar instrucciones SQL directamente.

#### <a name="example"></a>Ejemplo

Conecte con Azure Database for MySQL y seleccione todos los registros de la tabla de ventas. Puede obtener la cadena de conexión ODBC para la base de datos en Azure Portal.

```python
SERVER = 'YOUR_SEVER_NAME' + '.mysql.database.azure.com'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_MYSQL_USERNAME'
PASSWORD = 'YOUR_MYSQL_PASSWORD'

DRIVER = '{MySQL ODBC 5.3 UNICODE Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=3306;SERVER=' + SERVER + ';PORT=3306;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

### <a name="management-api"></a>API de administración

Cree y administre los recursos de MySQL de la suscripción con la API de administración.

#### <a name="requirements"></a>Requisitos
Debe instalar las bibliotecas de administración de MySQL para Python.
```bash
pip install azure-mgmt-rdbms
```

Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

#### <a name="example"></a>Ejemplo

Cree un recurso de base de datos de MySQL 5.7 y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.

```python

from azure.mgmt.rdbms.mysql import MySQLManagementClient
from azure.mgmt.rdbms.mysql.models import ServerForCreate, ServerPropertiesForDefaultCreate, ServerVersion

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE-GROUP_WITH_POSTGRES"
MYSQL_SERVER = "YOUR_DESIRED_MYSQL_SERVER_NAME"
MYSQL_ADMIN_USER = "YOUR_MYSQL_ADMIN_USERNAME"
MYSQL_ADMIN_PASSWORD = "YOUR_MYSQL_ADMIN_PASSOWRD"
LOCATION = "westus"  # example Azure availability zone, should match resource group


client = MySQLManagementClient(credentials=creds,
    subscription_id=SUBSCRIPTION_ID)

server_creation_poller = client.servers.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=MYSQL_SERVER,
    ServerForCreate(
        ServerPropertiesForDefaultCreate(
            administrator_login=MYSQL_ADMIN_USER,
            administrator_login_password=MYSQL_ADMIN_PASSWORD,
            version=ServerVersion.five_full_stop_seven
        ),
        location=LOCATION
    )
)

server = server_creation_poller.result()

# Open access to this server for IPs
rule_creation_poller = client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    MYSQL_SERVER,
    "some_custom_ip_range_whitelist_rule_name",  # Custom firewall rule name
    "123.123.123.123",  # Start ip range
    "167.220.0.235"  # End ip range
)

firewall_rule = rule_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a>PostgreSQL
Use el controlador ODBC y pyodbc para conectarse a la base de datos y ejecutar instrucciones SQL directamente.

Obtenga más información acerca de [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).

### <a name="client-odbc-driver-and-pyodbc"></a>Controlador ODBC de cliente y pyodbc
La biblioteca de cliente recomendada para acceder a Azure Database for PostgreSQL es el [controlador ODBC y pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).

#### <a name="example"></a>Ejemplo 

Conecte con Azure Database for PostgreSQL y seleccione todos los registros de la tabla `SALES`. Puede obtener la cadena de conexión ODBC para la base de datos en Azure Portal.

```python
import pyodbc

SERVER = 'YOUR_SERVER_NAME.postgres.database.azure.com'
DATABASE = 'YOUR_DB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

DRIVER = '{PostgreSQL ODBC Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=5432;SERVER=' + SERVER +
    ';PORT=5432;DATABASE=' + DATABASE + ';UID=' + USERNAME +
    ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES" # SALES is an example table name
cursor.execute(selectsql)
```

### <a name="management-api"></a>API de administración
#### <a name="requirements"></a>Requisitos
Debe instalar las bibliotecas de administración de PostgreSQL para Python.
```bash
pip install azure-mgmt-rdbms
```

Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

#### <a name="example"></a>Ejemplo
En este ejemplo, se creará una nueva base de datos de Postgres en nuestro servidor Postgres existente.
```python
from azure.mgtm.rdbms.postgresql import PostgreSQLManagementClient

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE_GROUP_WITH_POSTGRES"
POSTGRES_SERVER = "YOUR_POSTGRES_SERVER_NAME"
DB_NAME = "YOUR_DESIRED_DATABASE_NAME"

client = PostgreSQLManagementClient(credentials, SUBSCRIPTION_ID)

db_creation_poller = client.databases.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=POSTGRES_SERVER, database_name=DB_NAME)
db = db_creation_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/postgresql/mysql/management)