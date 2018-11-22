---
title: Bibliotecas Azure CDN para Python
description: Referencia de las bibliotecas de Azure CDN para Python
keywords: Azure, python, SDK, API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 06e6c8786ebbd88b7d3996b640af96a23cd5689b
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52275539"
---
# <a name="azure-cdn-libraries-for-python"></a>Bibliotecas Azure CDN para Python

## <a name="overview"></a>Información general

[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) permite proporcionar memorias caché de contenido web para garantizar la disponibilidad de suficiente ancho de banda en todo el mundo.

Para empezar a trabajar con Azure CDN, consulte [Introducción a Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).

## <a name="management-apis"></a>API de administración

Cree, consulte y administre redes CDN de Azure con la API de administración.

Instale el paquete de administración mediante pip.

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a>Ejemplo

Cree un perfil de CDN con un único punto de conexión definido:

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/cdn/management)
