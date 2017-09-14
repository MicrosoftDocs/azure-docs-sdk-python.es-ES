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
# <a name="azure-dns-libraries-for-python"></a>Bibliotecas de Azure DNS para Python

## <a name="overview"></a>Información general

[Azure DNS](/azure/dns/dns-overview) es un servicio de hospedaje para dominios DNS que permite resolver nombres mediante la infraestructura de Azure.

Para empezar a usar Azure DNS, consulte [Introducción a Azure DNS mediante Azure Portal](/azure/dns/dns-getstarted-portal).

## <a name="management-apis"></a>API de administración

Cree y administre zonas DNS y con la API de administración.

Instale el paquete de administración con pip.

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a>Ejemplo

Cree una nueva zona DNS.

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
> [Explorar las API de administración](/python/api/overview/azure/dns/managementlibrary)
