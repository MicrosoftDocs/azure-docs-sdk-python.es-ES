---
title: Bibliotecas de Azure MySQL para Python
description: ''
keywords: Azure, Python, SDK, API, SQL, Database, MySQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: mysql
ms.openlocfilehash: f03134bfddfabc426cbcaf4d98ef86d14038861f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479188"
---
# <a name="azure-mysql-libraries-for-python"></a>Bibliotecas de Azure MySQL para Python 

## <a name="overview"></a>Información general

Trabaje con los recursos y datos almacenados en [Azure Database for MySQL](/azure/mysql/overview) desde Python con el administrador de MySQL y pyodbc.

## <a name="client-odbc-driver-and-pyodbc"></a>Controlador ODBC de cliente y pyodbc

La biblioteca de cliente recomendada para acceder a Azure Database for MySQL es el [controlador ODBC](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries). Use el controlador ODBC para conectarse a la base de datos y ejecutar instrucciones SQL directamente.

### <a name="example"></a>Ejemplo

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

## <a name="management-api"></a>API de administración

Cree y administre los recursos de MySQL de la suscripción con la API de administración.

### <a name="requirements"></a>Requisitos
Debe instalar las bibliotecas de administración de MySQL para Python.
```bash
pip install azure-mgmt-rdbms
```

Para más información acerca de cómo obtener credenciales para autenticarse con el cliente de administración, consulte la página sobre la [autenticación del SDK de Python](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate).

### <a name="example"></a>Ejemplo

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
> [Explorar las API de administración](/python/api/overview/azure/mysql/management)