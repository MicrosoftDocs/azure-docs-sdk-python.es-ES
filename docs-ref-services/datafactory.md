---
title: Bibliotecas de Azure Data Factory para Python
description: Referencia de las bibliotecas de Azure Data Factory para Python
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 05/10/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 05d93f7d1838c110c3ba77f7abd3967f7870774b
ms.sourcegitcommit: d65549030a0edb50d75482f79aac0962d1dacb57
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34759056"
---
# <a name="azure-data-factory-libraries-for-python"></a>Bibliotecas de Azure Data Factory para Python

Cree servicios de almacenamiento, traslado y procesamiento de datos con canalizaciones de datos automatizadas con [Azure Data Factory](/azure/data-factory/)

[Obtenga más información](/azure/data-factory/introduction) acerca de Data Factory y empiece a trabajar con la guía de inicio rápido [Create a data factory and pipeline using Python](/azure/data-factory/quickstart-create-data-factory-python). 

## <a name="management-module"></a>Módulo de administración

Cree y administre instancias de Data Factory en su suscripción con el módulo de administración.

### <a name="installation"></a>Instalación

Instale el paquete con [pip](https://pip.pypa.io/en/stable/quickstart/):

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a>Ejemplo 

Cree una instancia de Data Factory en su suscripción en la región Este de EE. UU.

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
import time

#Create a data factory
subscription_id = '<Specify your Azure Subscription ID>'
credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
adf_client = DataFactoryManagementClient(credentials, subscription_id)

rg_params = {'location':'eastus'}
df_params = {'location':'eastus'}  

df_resource = Factory(location='eastus')
df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
print_item(df)
while df.provisioning_state != 'Succeeded':
    df = adf_client.factories.get(rg_name, df_name)
    time.sleep(1)
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/datafactory/management)