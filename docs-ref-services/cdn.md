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
# <a name="azure-cdn-libraries-for-python"></a><span data-ttu-id="2f8a5-104">Bibliotecas Azure CDN para Python</span><span class="sxs-lookup"><span data-stu-id="2f8a5-104">Azure CDN libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="2f8a5-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2f8a5-105">Overview</span></span>

<span data-ttu-id="2f8a5-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) permite proporcionar memorias caché de contenido web para garantizar la disponibilidad de suficiente ancho de banda en todo el mundo.</span><span class="sxs-lookup"><span data-stu-id="2f8a5-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) allows you to provide web content caches to ensure high-bandwidth availability across the globe.</span></span>

<span data-ttu-id="2f8a5-107">Para empezar a trabajar con Azure CDN, consulte [Introducción a Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span><span class="sxs-lookup"><span data-stu-id="2f8a5-107">To get started with Azure CDN, see [Getting started with Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-apis"></a><span data-ttu-id="2f8a5-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="2f8a5-108">Management APIs</span></span>

<span data-ttu-id="2f8a5-109">Cree, consulte y administre redes CDN de Azure con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="2f8a5-109">Create, query, and manage Azure CDNs with the management API.</span></span>

<span data-ttu-id="2f8a5-110">Instale el paquete de administración mediante pip.</span><span class="sxs-lookup"><span data-stu-id="2f8a5-110">Install the management package via pip.</span></span>

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a><span data-ttu-id="2f8a5-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="2f8a5-111">Example</span></span>

<span data-ttu-id="2f8a5-112">Cree un perfil de CDN con un único punto de conexión definido:</span><span class="sxs-lookup"><span data-stu-id="2f8a5-112">Creating a CDN profile with a single defined endpoint:</span></span>

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
> [<span data-ttu-id="2f8a5-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="2f8a5-113">Explore the Management APIs</span></span>](/python/api/overview/azure/cdn/management)
