---
title: Bibliotecas de Azure Data Lake Analytics para Python
description: Referencia de las bibliotecas de Azure Data Lake Analytics para Python
keywords: Azure, python, SDK, API, Data Lake Analytics
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 08/04/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e98b2f314080146429c89061ab5e154526a87a48
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534303"
---
# <a name="azure-data-lake-analytics-libraries-for-python"></a>Bibliotecas de Azure Data Lake Analytics para Python

## <a name="overview"></a>Información general
Ejecute trabajos de análisis de macrodatos con capacidad de escalado a conjuntos de datos masivos con [Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview).

## <a name="install-the-libraries"></a>Instalación de las bibliotecas

## <a name="management-api"></a>API de administración
Use la API de administración para administrar cuentas, trabajos, directivas y catálogos de Data Lake Analytics.

```bash
pip install azure-mgmt-datalake-analytics
```

### <a name="example"></a>Ejemplo
Este es un ejemplo de cómo crear una cuenta de Data Lake Analytics y enviar un trabajo. 

```python
## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adls = '<Azure Data Lake Analytics Account Name>'

# Create the clients
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')

# Create resource group
armGroupResult = resourceClient.resource_groups.create_or_update(rg, ResourceGroup(location=location))

# Create a store account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Create an ADLA account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Submit a job
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>Ejemplos
[Administración de Azure Data Lake Analytics](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-python-sdk)