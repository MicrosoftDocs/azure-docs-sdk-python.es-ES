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
# <a name="azure-mysqlpostgresql-libraries-for-python"></a><span data-ttu-id="66f27-103">Bibliotecas de Azure MySQL/PostgreSQL para Python</span><span class="sxs-lookup"><span data-stu-id="66f27-103">Azure MySQL/PostgreSQL libraries for Python</span></span>

## <a name="mysql"></a><span data-ttu-id="66f27-104">MySQL</span><span class="sxs-lookup"><span data-stu-id="66f27-104">MySQL</span></span>

<span data-ttu-id="66f27-105">Trabaje con los recursos y datos almacenados en [Azure Database for MySQL](/azure/mysql/overview) desde Python con el administrador de MySQL y pyodbc.</span><span class="sxs-lookup"><span data-stu-id="66f27-105">Work with resources and data stored in [Azure MySQL Database](/azure/mysql/overview) from python with the MySQL manager and pyodbc.</span></span>

### <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="66f27-106">Controlador ODBC de cliente y pyodbc</span><span class="sxs-lookup"><span data-stu-id="66f27-106">Client ODBC driver and pyodbc</span></span>

<span data-ttu-id="66f27-107">La biblioteca de cliente recomendada para acceder a Azure Database for MySQL es el [controlador ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="66f27-107">The recommended client library for accessing Azure Database for MySQL is the Microsoft [ODBC driver](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span> <span data-ttu-id="66f27-108">Use el controlador ODBC para conectarse a la base de datos y ejecutar instrucciones SQL directamente.</span><span class="sxs-lookup"><span data-stu-id="66f27-108">Use the ODBC driver to connect to the database and execute SQL statements directly.</span></span>

#### <a name="example"></a><span data-ttu-id="66f27-109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66f27-109">Example</span></span>

<span data-ttu-id="66f27-110">Conecte con Azure Database for MySQL y seleccione todos los registros de la tabla de ventas.</span><span class="sxs-lookup"><span data-stu-id="66f27-110">Connect to a Azure Database for MySQL and select all records in the sales table.</span></span> <span data-ttu-id="66f27-111">Puede obtener la cadena de conexión ODBC para la base de datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66f27-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

### <a name="management-api"></a><span data-ttu-id="66f27-112">API de administración</span><span class="sxs-lookup"><span data-stu-id="66f27-112">Management API</span></span>

<span data-ttu-id="66f27-113">Cree y administre los recursos de MySQL de la suscripción con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="66f27-113">Create and manage MySQL resources in your subscription with the management API.</span></span>

#### <a name="requirements"></a><span data-ttu-id="66f27-114">Requisitos</span><span class="sxs-lookup"><span data-stu-id="66f27-114">Requirements</span></span>
<span data-ttu-id="66f27-115">Debe instalar las bibliotecas de administración de MySQL para Python.</span><span class="sxs-lookup"><span data-stu-id="66f27-115">You must install the MySQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="66f27-116">Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="66f27-116">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

#### <a name="example"></a><span data-ttu-id="66f27-117">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66f27-117">Example</span></span>

<span data-ttu-id="66f27-118">Cree un recurso de base de datos de MySQL 5.7 y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="66f27-118">Create a MySQL 5.7 Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="66f27-119">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="66f27-119">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a><span data-ttu-id="66f27-120">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="66f27-120">PostgreSQL</span></span>
<span data-ttu-id="66f27-121">Use el controlador ODBC y pyodbc para conectarse a la base de datos y ejecutar instrucciones SQL directamente.</span><span class="sxs-lookup"><span data-stu-id="66f27-121">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="66f27-122">Obtenga más información acerca de [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="66f27-122">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

### <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="66f27-123">Controlador ODBC de cliente y pyodbc</span><span class="sxs-lookup"><span data-stu-id="66f27-123">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="66f27-124">La biblioteca de cliente recomendada para acceder a Azure Database for PostgreSQL es el [controlador ODBC y pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="66f27-124">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

#### <a name="example"></a><span data-ttu-id="66f27-125">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66f27-125">Example</span></span> 

<span data-ttu-id="66f27-126">Conecte con Azure Database for PostgreSQL y seleccione todos los registros de la tabla `SALES`.</span><span class="sxs-lookup"><span data-stu-id="66f27-126">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="66f27-127">Puede obtener la cadena de conexión ODBC para la base de datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="66f27-127">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

### <a name="management-api"></a><span data-ttu-id="66f27-128">API de administración</span><span class="sxs-lookup"><span data-stu-id="66f27-128">Management API</span></span>
#### <a name="requirements"></a><span data-ttu-id="66f27-129">Requisitos</span><span class="sxs-lookup"><span data-stu-id="66f27-129">Requirements</span></span>
<span data-ttu-id="66f27-130">Debe instalar las bibliotecas de administración de PostgreSQL para Python.</span><span class="sxs-lookup"><span data-stu-id="66f27-130">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="66f27-131">Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="66f27-131">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

#### <a name="example"></a><span data-ttu-id="66f27-132">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="66f27-132">Example</span></span>
<span data-ttu-id="66f27-133">En este ejemplo, se creará una nueva base de datos de Postgres en nuestro servidor Postgres existente.</span><span class="sxs-lookup"><span data-stu-id="66f27-133">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
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
> [<span data-ttu-id="66f27-134">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="66f27-134">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/mysql/management)