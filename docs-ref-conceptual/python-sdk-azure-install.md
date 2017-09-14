---
title: "Instalación"
description: "Cómo instalar Azure SDK para Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: d65f07a30b3aa8b0a1a502baa86986ad50848873
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="installation"></a>Instalación

## <a name="installation-with-pip"></a>Instalación con pip

Puede instalar individualmente la biblioteca de cada servicio de Azure:

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

Los paquetes de versión preliminar pueden instalarse con el indicador `--pre` :

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

También puede instalar un conjunto de bibliotecas de Azure en una sola línea con el metapaquete `azure` .

```bash
pip install azure
```

Hemos publicado una versión preliminar de este paquete, al que puede acceder con la marca --pre:

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Instalación de GitHub

Si desea instalar `azure` desde el origen:

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install

## <a name="stable-packages"></a>Paquetes estables
| Nombre del paquete |
|--------------|
|[azure-batch](https://pypi.org/project/azure-batch/)  |   
|[azure-mgmt-batch](https://pypi.org/project/azure-mgmt-batch/)|
|[azure-mgmt-cognitiveservices](https://pypi.org/project/azure-mgmt-cognitiveservices/)|    
|[azure-mgmt-devtestlabs](https://pypi.org/project/azure-mgmt-devtestlabs/)|    
|[azure-mgmt-dns](https://pypi.org/project/azure-mgmt-dns/) |
|[azure-mgmt-logic](https://pypi.org/project/azure-mgmt-logic/)|
|[azure-mgmt-redis](https://pypi.org/project/azure-mgmt-redis/)|
|[azure-mgmt-scheduler](https://pypi.org/project/azure-mgmt-scheduler/)|    
|[azure-mgmt-servermanager](https://pypi.org/project/azure-mgmt-servermanager/)|    
|[azure-servicebus](https://pypi.org/project/azure-mgmt-servicebus/)|   
|[azure-servicefabric](https://pypi.org/project/azure-servicefabric/)|  
|[azure-servicemanagement-legacy](https://pypi.org/project/azure-servicemanagement-legacy/)|    
|[azure-storage](https://pypi.org/project/azure-storage/)|  

## <a name="preview-packages"></a>Paquetes en versión preliminar
| Nombre del paquete | 
|--------------|
|[azure-keyvault](https://pypi.org/project/azure-keyvault/)|    
|[azure-monitor](https://pypi.org/project/azure-monitor)|   
|[azure-mgmt-resource](https://pypi.org/project/azure-mgmt-resource)|   
|[azure-mgmt-compute](https://pypi.org/project/azure-mgmt-compute)| 
|[azure-mgmt-network](https://pypi.org/project/azure-mgmt-network)| 
|[azure-mgmt-storage](https://pypi.org/project/azure-mgmt-storage)| 
|[azure-mgmt-keyvault](https://pypi.org/project/azure-mgmt-keyvault)|   
|[azure-graphrbac](https://pypi.org/project/azure-graphrbac)|   
|[azure-mgmt-authorization](https://pypi.org/project/azure-mgmt-authorization)| 
|[azure-mgmt-billing](https://pypi.org/project/azure-mgmt-billing)| 
|[azure-mgmt-cdn](https://pypi.org/project/azure-mgmt-cdn)| 
|[azure-mgmt-containerregistry](https://pypi.org/project/azure-mgmt-containerregistry)| 
|[azure-mgmt-commerce](https://pypi.org/project/azure-mgmt-commerce)|   
|[azure-mgmt-consumption](https://pypi.org/project/azure-mgmt-consumption)| 
|[azure-mgmt-datalake-analytics](https://pypi.org/project/azure-mgmt-datalake-analytics)|   
|[azure-mgmt-datalake-store](https://pypi.org/project/azure-mgmt-datalake-store)|   
|[azure-mgmt-documentdb](https://pypi.org/project/azure-mgmt-documentdb)|   
|[azure-mgmt-eventhub](https://pypi.org/project/azure-mgmt-eventhub)|   
|[azure-mgmt-iothub](https://pypi.org/project/azure-mgmt-iothub)|
|[azure-mgmt-media](https://pypi.org/project/azure-mgmt-media)| 
|[azure-mgmt-monitor](https://pypi.org/project/azure-mgmt-monitor)| 
|[azure-mgmt-notificationhubs](https://pypi.org/project/azure-mgmt-notificationhubs)|   
|[azure-mgmt-powerbiembedded](https://pypi.org/project/azure-mgmt-powerbiembedded)| 
|[azure-mgmt-search](https://pypi.org/project/azure-mgmt-search)|
|[azure-mgmt-servicebus](https://pypi.org/project/azure-mgmt-servicebus)|   
|[azure-mgmt-sql](https://pypi.org/project/azure-mgmt-sql)| 
|[azure-mgmt-trafficmanager](https://pypi.org/project/azure-mgmt-trafficmanager)|   
|[azure-mgmt-web](https://pypi.org/project/azure-mgmt-web)|