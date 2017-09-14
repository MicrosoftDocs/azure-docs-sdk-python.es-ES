---
title: Bibliotecas de Azure DNS para Python
description: Referencia de las bibliotecas de Azure DNS para Python
keywords: Azure, python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="72905-104">Bibliotecas de Azure DNS para Python</span><span class="sxs-lookup"><span data-stu-id="72905-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="72905-105">Información general</span><span class="sxs-lookup"><span data-stu-id="72905-105">Overview</span></span>

<span data-ttu-id="72905-106">[Azure DNS](/azure/dns/dns-overview) es un servicio de hospedaje para dominios DNS que permite resolver nombres mediante la infraestructura de Azure.</span><span class="sxs-lookup"><span data-stu-id="72905-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="72905-107">Para empezar a usar Azure DNS, consulte [Introducción a Azure DNS mediante Azure Portal](/azure/dns/dns-getstarted-portal).</span><span class="sxs-lookup"><span data-stu-id="72905-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="72905-108">API de administración</span><span class="sxs-lookup"><span data-stu-id="72905-108">Management APIs</span></span>

<span data-ttu-id="72905-109">Cree y administre zonas DNS y con la API de administración.</span><span class="sxs-lookup"><span data-stu-id="72905-109">Create and manage DNS zones and records with the management API.</span></span>

<span data-ttu-id="72905-110">Instale el paquete de administración con pip.</span><span class="sxs-lookup"><span data-stu-id="72905-110">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a><span data-ttu-id="72905-111">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="72905-111">Example</span></span>

<span data-ttu-id="72905-112">Cree una nueva zona DNS.</span><span class="sxs-lookup"><span data-stu-id="72905-112">Create a new DNS zone.</span></span>

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="72905-113">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="72905-113">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/managementlibrary)
