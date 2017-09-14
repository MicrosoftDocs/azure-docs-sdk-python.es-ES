---
title: Bibliotecas de Azure Web Apps para Python
description: 
keywords: Azure, Python, SDK, API, Web Apps, App Service
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 05f6ad173f4ec051654b5eb2a986b2c2a93cc33a
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-web-apps-libraries-for-python"></a>Bibliotecas de Azure Web Apps para Python

## <a name="overview"></a>Información general

Implemente y escale sitios web, aplicaciones web, servicios y API de REST con [Azure App Service](/azure/app-service).

Para empezar a trabajar con Azure App Service, consulte [Creación de una aplicación web de Python en Azure](/azure/app-service-web/app-service-web-get-started-python).

## <a name="management-api"></a>API de administración

Implemente, administre y escale elementos hospedados en Azure App Service con la API de administración.

Instale la biblioteca mediante pip.

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>Ejemplo

Implemente una aplicación web desde un repositorio de GitHub en Azure Web App.

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```
> [!div class="nextstepaction"]
> [Explorar las API de administración](/python/api/overview/azure/webapps/managementlibrary)

## <a name="samples"></a>Muestras 

* [Administración de sitios web de Azure con Node.js][1]
* [Creación de un flujo de trabajo de aplicación lógica][2]
 
Vea la [lista completa](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app) de ejemplos de aplicaciones web.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md