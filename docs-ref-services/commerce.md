---
title: Bibliotecas de Azure Commerce para Python
description: Referencia de las bibliotecas de Azure Commerce para Python
keywords: Azure, python, SDK, API, Commerce
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 77008eb76c3a925d9c7e63fe9360ea5b25da49de
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551608"
---
# <a name="azure-commerce-libraries-for-python"></a><span data-ttu-id="47a67-104">Bibliotecas de Azure Commerce para Python</span><span class="sxs-lookup"><span data-stu-id="47a67-104">Azure Commerce libraries for python</span></span>

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[<span data-ttu-id="47a67-105">API de administración</span><span class="sxs-lookup"><span data-stu-id="47a67-105">Management API</span></span>](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a><span data-ttu-id="47a67-106">Creación del cliente de Commerce</span><span class="sxs-lookup"><span data-stu-id="47a67-106">Create the commerce client</span></span>

<span data-ttu-id="47a67-107">El código siguiente crea una instancia del cliente de administración.</span><span class="sxs-lookup"><span data-stu-id="47a67-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="47a67-108">Debe proporcionar el valor de ``subscription_id``, que se puede obtener en [la lista de suscripciones](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span><span class="sxs-lookup"><span data-stu-id="47a67-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="47a67-109">Consulte [Autenticación de la administración de recursos](/python/azure/python-sdk-azure-authenticate) para más información sobre cómo controlar la autenticación de Azure Active Directory con el SDK de Python, y crear una instancia de ``Credentials``.</span><span class="sxs-lookup"><span data-stu-id="47a67-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.commerce import UsageManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

commerce_client = UsageManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="get-rate-card"></a><span data-ttu-id="47a67-110">Obtener la clasificación de la tarjeta</span><span class="sxs-lookup"><span data-stu-id="47a67-110">Get rate card</span></span>

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a><span data-ttu-id="47a67-111">Obtener el uso</span><span class="sxs-lookup"><span data-stu-id="47a67-111">Get Usage</span></span>

```python
from datetime import date, timedelta

# Takes onky dates in full ISO8601 with 'T00:00:00Z'
# Return an iterator like object: https://docs.python.org/3/library/stdtypes.html#iterator-types
usage_iterator = commerce_client.usage_aggregates.list(
    str(date.today() - timedelta(days=1))+'T00:00:00Z',
    str(date.today())+'T00:00:00Z'
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="47a67-112">Explorar las API de administración</span><span class="sxs-lookup"><span data-stu-id="47a67-112">Explore the Management APIs</span></span>](/python/api/overview/azure/commerce/management)