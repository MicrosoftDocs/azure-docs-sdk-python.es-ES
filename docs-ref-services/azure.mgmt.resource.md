---
title: Bibliotecas de Azure Resources para Python
description: ''
keywords: Azure, Python, SDK, API, Resources
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: 32e13bee27db091f0bca12c7d9ae4fc62165f4c0
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
ms.locfileid: "20909398"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="19d81-103">Bibliotecas de Azure Resources para Python</span><span class="sxs-lookup"><span data-stu-id="19d81-103">Azure Resources libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="19d81-104">Información general</span><span class="sxs-lookup"><span data-stu-id="19d81-104">Overview</span></span> 
<span data-ttu-id="19d81-105">Administración de recursos de Azure en grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="19d81-105">Manage Azure resources in resource groups.</span></span>

| <span data-ttu-id="19d81-106">Paquete</span><span class="sxs-lookup"><span data-stu-id="19d81-106">Package</span></span>  |  <span data-ttu-id="19d81-107">Descripción</span><span class="sxs-lookup"><span data-stu-id="19d81-107">Description</span></span> |
|---|---|
|<span data-ttu-id="19d81-108">[Azure.Mgmt.Resource.Features][1]</span><span class="sxs-lookup"><span data-stu-id="19d81-108">[azure.mgmt.resource.features][1]</span></span>|<span data-ttu-id="19d81-109">El Control de exposición de características de Azure (AFEC) proporciona a los proveedores de recursos un mecanismo para controlar la exposición de característica a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="19d81-109">Azure Feature Exposure Control (AFEC) provides a mechanism for the resource providers to control feature exposure to users.</span></span>|
|<span data-ttu-id="19d81-110">[azure.mgmt.resource.links][2]</span><span class="sxs-lookup"><span data-stu-id="19d81-110">[azure.mgmt.resource.links][2]</span></span>|<span data-ttu-id="19d81-111">Los recursos de Azure se pueden vincular entre sí para formar relaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="19d81-111">Azure resources can be linked together to form logical relationships.</span></span> <span data-ttu-id="19d81-112">Puede establecer vínculos entre recursos que pertenecen a distintos grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="19d81-112">You can establish links between resources belonging to different resource groups.</span></span>|
|<span data-ttu-id="19d81-113">[azure.mgmt.resource.locks][3]</span><span class="sxs-lookup"><span data-stu-id="19d81-113">[azure.mgmt.resource.locks][3]</span></span>|<span data-ttu-id="19d81-114">Los recursos de Azure se pueden bloquear para impedir que otros usuarios de su organización los eliminen o modifiquen.</span><span class="sxs-lookup"><span data-stu-id="19d81-114">Azure resources can be locked to prevent other users in your organization from deleting or modifying resources.</span></span>|
|<span data-ttu-id="19d81-115">[azure.mgmt.resource.managedapplications][4]</span><span class="sxs-lookup"><span data-stu-id="19d81-115">[azure.mgmt.resource.managedapplications][4]</span></span>|<span data-ttu-id="19d81-116">Aplicaciones administradas de ARM.</span><span class="sxs-lookup"><span data-stu-id="19d81-116">ARM managed applications (appliances).</span></span>|
|<span data-ttu-id="19d81-117">[azure.mgmt.resource.policy][5]</span><span class="sxs-lookup"><span data-stu-id="19d81-117">[azure.mgmt.resource.policy][5]</span></span>|<span data-ttu-id="19d81-118">Para administrar y controlar el acceso a los recursos, puede definir directivas personalizadas y asignarlas en un ámbito.</span><span class="sxs-lookup"><span data-stu-id="19d81-118">To manage and control access to your resources, you can define customized policies and assign them at a scope.</span></span>|
|<span data-ttu-id="19d81-119">[azure.mgmt.resource.resources][6]</span><span class="sxs-lookup"><span data-stu-id="19d81-119">[azure.mgmt.resource.resources][6]</span></span>| <span data-ttu-id="19d81-120">Proporciona operaciones para trabajar con recursos y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="19d81-120">Provides operations for working with resources and resource groups.</span></span>|
|<span data-ttu-id="19d81-121">[azure.mgmt.resource.subscriptions][7]</span><span class="sxs-lookup"><span data-stu-id="19d81-121">[azure.mgmt.resource.subscriptions][7]</span></span>|<span data-ttu-id="19d81-122">Todos los recursos y grupos de recursos existen dentro de las suscripciones.</span><span class="sxs-lookup"><span data-stu-id="19d81-122">All resource groups and resources exist within subscriptions.</span></span> <span data-ttu-id="19d81-123">Estas operaciones permiten obtener información acerca de las suscripciones y los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="19d81-123">These operation enable you get information about your subscriptions and tenants.</span></span>|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a><span data-ttu-id="19d81-124">Instalación de las bibliotecas</span><span class="sxs-lookup"><span data-stu-id="19d81-124">Install the libraries</span></span> 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="19d81-125">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="19d81-125">Example</span></span>
<span data-ttu-id="19d81-126">El siguiente código muestra cómo crear un grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="19d81-126">The following is an example of how to create a resource group.</span></span> 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

<span data-ttu-id="19d81-127">Vea más [código de Python ejemplo](https://azure.microsoft.com/resources/samples/?platform=python) que puede usar en sus aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="19d81-127">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span> 