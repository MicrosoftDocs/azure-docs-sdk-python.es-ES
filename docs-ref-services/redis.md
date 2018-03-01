---
title: Bibliotecas de Azure Redis para Python
description: "Documentación de referencia de las bibliotecas de cliente de Python para Redis"
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
---
# <a name="azure-redis-cache-libraries-for-python"></a><span data-ttu-id="32c35-104">Bibliotecas de Azure Redis Cache para Python</span><span class="sxs-lookup"><span data-stu-id="32c35-104">Azure Redis Cache libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="32c35-105">Información general</span><span class="sxs-lookup"><span data-stu-id="32c35-105">Overview</span></span>

<span data-ttu-id="32c35-106">Azure Redis Cache se basa en el popular proyecto de código abierto Redis.</span><span class="sxs-lookup"><span data-stu-id="32c35-106">Azure Redis Cache is based on the popular open source Redis project.</span></span> <span data-ttu-id="32c35-107">Ofrece acceso a una instancia de Redis segura y dedicada, administrada por Microsoft y accesible desde sus aplicaciones de Azure.</span><span class="sxs-lookup"><span data-stu-id="32c35-107">It gives you access to a secure, dedicated Redis instance, managed by Microsoft and accessible from your Azure apps.</span></span>

<span data-ttu-id="32c35-108">Redis es un almacén de pares clave-valor avanzado, donde las claves pueden contener estructuras de datos tales como cadenas, algoritmos hash, listas, conjuntos y conjuntos ordenados.</span><span class="sxs-lookup"><span data-stu-id="32c35-108">Redis is an advanced key-value store, where keys can contain data structures such as strings, hashes, lists, sets, and sorted sets.</span></span> <span data-ttu-id="32c35-109">Redis admite un conjunto de operaciones atómicas con estos tipos de datos.</span><span class="sxs-lookup"><span data-stu-id="32c35-109">Redis supports a set of atomic operations on these data types.</span></span>

<span data-ttu-id="32c35-110">Obtenga más información acerca de [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span><span class="sxs-lookup"><span data-stu-id="32c35-110">Learn more about [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span></span>

## <a name="management-api"></a><span data-ttu-id="32c35-111">API de administración</span><span class="sxs-lookup"><span data-stu-id="32c35-111">Management API</span></span>

<span data-ttu-id="32c35-112">Cree y administre los recursos de Redis en su suscripción con la API de administración de Redis.</span><span class="sxs-lookup"><span data-stu-id="32c35-112">Create and manage your Redis resources in your subscription with the Redis management API.</span></span>

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a><span data-ttu-id="32c35-113">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="32c35-113">Example</span></span>

<span data-ttu-id="32c35-114">En el ejemplo siguiente se crea una nueva memoria caché de Redis:</span><span class="sxs-lookup"><span data-stu-id="32c35-114">The following example creates a new Redis cache:</span></span>

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
> [<span data-ttu-id="32c35-115">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="32c35-115">Explore the Management APIs</span></span>](/python/api/overview/azure/redis/management)

