---
title: Bibliotecas de Azure PostgreSQL para Python
description: ''
keywords: Azure, Python, SDK, API, SQL, Database, Postgres, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: postgresql
ms.openlocfilehash: cad5995072d5040764986765d9a900f46f5141ec
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478938"
---
#<a name="azure-postgresql-libraries-for-python"></a><span data-ttu-id="1199b-103">Bibliotecas de Azure PostgreSQL para Python</span><span class="sxs-lookup"><span data-stu-id="1199b-103">Azure PostgreSQL libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="1199b-104">Información general</span><span class="sxs-lookup"><span data-stu-id="1199b-104">Overview</span></span>
<span data-ttu-id="1199b-105">Use el controlador ODBC y pyodbc para conectarse a la base de datos y ejecutar instrucciones SQL directamente.</span><span class="sxs-lookup"><span data-stu-id="1199b-105">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="1199b-106">Obtenga más información acerca de [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span><span class="sxs-lookup"><span data-stu-id="1199b-106">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="1199b-107">Controlador ODBC de cliente y pyodbc</span><span class="sxs-lookup"><span data-stu-id="1199b-107">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="1199b-108">La biblioteca de cliente recomendada para acceder a Azure Database for PostgreSQL es el [controlador ODBC y pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="1199b-108">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

### <a name="example"></a><span data-ttu-id="1199b-109">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1199b-109">Example</span></span> 

<span data-ttu-id="1199b-110">Conecte con Azure Database for PostgreSQL y seleccione todos los registros de la tabla `SALES`.</span><span class="sxs-lookup"><span data-stu-id="1199b-110">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="1199b-111">Puede obtener la cadena de conexión ODBC para la base de datos en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="1199b-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="1199b-112">API de administración</span><span class="sxs-lookup"><span data-stu-id="1199b-112">Management API</span></span>
### <a name="requirements"></a><span data-ttu-id="1199b-113">Requisitos</span><span class="sxs-lookup"><span data-stu-id="1199b-113">Requirements</span></span>
<span data-ttu-id="1199b-114">Debe instalar las bibliotecas de administración de PostgreSQL para Python.</span><span class="sxs-lookup"><span data-stu-id="1199b-114">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="1199b-115">Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).</span><span class="sxs-lookup"><span data-stu-id="1199b-115">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="1199b-116">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="1199b-116">Example</span></span>
<span data-ttu-id="1199b-117">En este ejemplo, se creará una nueva base de datos de Postgres en nuestro servidor Postgres existente.</span><span class="sxs-lookup"><span data-stu-id="1199b-117">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
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
> [<span data-ttu-id="1199b-118">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="1199b-118">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/management)

