---
title: Bibliotecas de Azure Resources para Python
description: ''
keywords: Azure, Python, SDK, API, Resources
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534377"
---
# <a name="azure-resources-libraries-for-python"></a>Bibliotecas de Azure Resources para Python 

## <a name="overview"></a>Información general 
Administración de recursos de Azure en grupos de recursos

| Paquete  |  DESCRIPCIÓN |
|---|---|
|[azure.mgmt.resource.features][1]|El Control de exposición de características de Azure (AFEC) proporciona a los proveedores de recursos un mecanismo para controlar la exposición de característica a los usuarios.|
|[azure.mgmt.resource.links][2]|Los recursos de Azure se pueden vincular entre sí para formar relaciones lógicas. Puede establecer vínculos entre recursos que pertenecen a distintos grupos de recursos.|
|[azure.mgmt.resource.locks][3]|Los recursos de Azure se pueden bloquear para impedir que otros usuarios de su organización los eliminen o modifiquen.|
|[azure.mgmt.resource.managedapplications][4]|Aplicaciones administradas de ARM.|
|[azure.mgmt.resource.policy][5]|Para administrar y controlar el acceso a los recursos, puede definir directivas personalizadas y asignarlas en un ámbito.|
|[azure.mgmt.resource.resources][6]| Proporciona operaciones para trabajar con recursos y grupos de recursos.|
|[azure.mgmt.resource.subscriptions][7]|Todos los recursos y grupos de recursos existen dentro de las suscripciones. Estas operaciones permiten obtener información acerca de las suscripciones y los inquilinos.|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a>Instalación de las bibliotecas 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a>Ejemplo
El siguiente código muestra cómo crear un grupo de recursos. 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

Vea más [código de Python ejemplo](https://azure.microsoft.com/resources/samples/?platform=python) que puede usar en sus aplicaciones. 