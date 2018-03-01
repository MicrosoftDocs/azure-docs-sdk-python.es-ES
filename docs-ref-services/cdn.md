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
ms.openlocfilehash: 92d6dd6ce55964bc48bb9bc654e8dec25f6b8344
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
---
# <a name="azure-cdn-libraries-for-python"></a>Bibliotecas Azure CDN para Python

## <a name="overview"></a>Información general

[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) permite proporcionar memorias caché de contenido web para garantizar la disponibilidad de suficiente ancho de banda en todo el mundo.

Para empezar a trabajar con la red CDN de Azure, consulte [Introducción a la red CDN de Azure](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).

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
