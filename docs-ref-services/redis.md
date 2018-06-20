---
title: Bibliotecas de Azure Redis para Python
description: Documentación de referencia de las bibliotecas de cliente de Python para Redis
keywords: Azure, Python, Redis, API, SDK, Database, NoSQL
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: c2f8ebcbcbd7b71c1fa96e46a8148a3c0b88877f
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479248"
---
# <a name="azure-redis-cache-libraries-for-python"></a>Bibliotecas de Azure Redis Cache para Python

## <a name="overview"></a>Información general

Azure Redis Cache se basa en el popular proyecto de código abierto Redis. Ofrece acceso a una instancia de Redis segura y dedicada, administrada por Microsoft y accesible desde sus aplicaciones de Azure.

Redis es un almacén de pares clave-valor avanzado, donde las claves pueden contener estructuras de datos tales como cadenas, algoritmos hash, listas, conjuntos y conjuntos ordenados. Redis admite un conjunto de operaciones atómicas con estos tipos de datos.

Obtenga más información acerca de [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).

## <a name="management-api"></a>API de administración

Cree y administre los recursos de Redis en su suscripción con la API de administración de Redis.

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a>Ejemplo

En el ejemplo siguiente se crea una nueva memoria caché de Redis:

```python
from azure.mgmt.redis import RedisManagementClient
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

redis_client = RedisManagementClient(
    credentials,
    subscription_id
)
group_name = 'myresourcegroup'
cache_name = 'mycachename'
redis_cache = redis_client.redis.create_or_update(
    group_name,
    cache_name,
    RedisCreateOrUpdateParameters(
        sku = Sku(name = 'Basic', family = 'C', capacity = '1'),
        location = "East US"
    )
)
# redis_cache is a RedisResourceWithAccessKey instance
```

> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/redis/management)

