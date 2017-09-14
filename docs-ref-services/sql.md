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
# <a name="azure-sql-database-libraries-for-python"></a><span data-ttu-id="61593-103">Bibliotecas Azure SQL Database para Python</span><span class="sxs-lookup"><span data-stu-id="61593-103">Azure SQL Database libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="61593-104">Información general</span><span class="sxs-lookup"><span data-stu-id="61593-104">Overview</span></span>

<span data-ttu-id="61593-105">Trabaje con datos almacenados en [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) desde Python con el controlador ODBC de Microsoft y pyodbc.</span><span class="sxs-lookup"><span data-stu-id="61593-105">Work with data stored in [Azure SQL Database](/azure/sql-database/sql-database-technical-overview) from Python with the Microsoft ODBC driver and pyodbc.</span></span> 

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="61593-106">Controlador ODBC de cliente y pyodbc</span><span class="sxs-lookup"><span data-stu-id="61593-106">Client ODBC driver and pyodbc</span></span>

```bash
pip install pyodbc
```
<span data-ttu-id="61593-107">Pueden encontrar más detalles acerca de cómo instalar las bibliotecas de comunicación de python y base de datos [aquí](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span><span class="sxs-lookup"><span data-stu-id="61593-107">More details about installing the python and database communication libraries can be found [here](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries).</span></span>

### <a name="example"></a><span data-ttu-id="61593-108">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="61593-108">Example</span></span>

<span data-ttu-id="61593-109">Conéctese a una base de datos SQL y seleccione todos los registros de una tabla.</span><span class="sxs-lookup"><span data-stu-id="61593-109">Connect to a SQL database and select all records in a table.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="61593-110">API de administración</span><span class="sxs-lookup"><span data-stu-id="61593-110">Management API</span></span>

<span data-ttu-id="61593-111">Cree y administre los recursos de Azure SQL Database de la suscripción con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="61593-111">Create and manage Azure SQL Database resources in your subscription with the management API.</span></span> 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a><span data-ttu-id="61593-112">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="61593-112">Example</span></span>

<span data-ttu-id="61593-113">Cree un recurso de SQL Database y restrinja el acceso a un intervalo de direcciones IP mediante una regla de firewall.</span><span class="sxs-lookup"><span data-stu-id="61593-113">Create a SQL Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="61593-114">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="61593-114">Explore the Management APIs</span></span>](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a><span data-ttu-id="61593-115">Muestras</span><span class="sxs-lookup"><span data-stu-id="61593-115">Samples</span></span>

* <span data-ttu-id="61593-116">[Creación y administración de bases de datos SQL][1]</span><span class="sxs-lookup"><span data-stu-id="61593-116">[Create and manage SQL databases][1]</span></span>    
* <span data-ttu-id="61593-117">[Uso de Python para conectarse a los datos y consultarlos][2]</span><span class="sxs-lookup"><span data-stu-id="61593-117">[Use Python to connect and query data][2]</span></span>   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

<span data-ttu-id="61593-118">Vea la [lista completa](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) de ejemplos de Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="61593-118">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL) of Azure SQL database samples.</span></span> 