---
title: SDK de Azure para la configuración de operaciones de Python
description: C iniciado por el SDK de Azure para Python
keywords: Azure, Python, SDK, API, excepciones
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 03/07/2018
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: adeb6aa8a2c363c3119e97503df9536fb0633b4c
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376864"
---
# <a name="operation-config"></a>Configuración de operaciones 

Los métodos en operaciones tienen parámetros adicionales que se pueden proporcionar en elementos `kwargs`. Esto se denomina operation_config.

Las opciones de configuración de operaciones son:

|Nombre de parámetro|Type|Rol|
|----------------------|------|---------------|
| Comprobación |`bool`|Si se debe comprobar el certificado SSL. El valor predeterminado es True.|
|  cert |`str`| Ruta de acceso al certificado local para la comprobación del lado cliente.|
|  timeout |`int`| Tiempo de espera para establecer una conexión de servidor, en segundos.|
|  allow_redirects |`bool` | Si se permiten redirecciones.|
|  max_redirects  |`int`| Número máximo de redirecciones permitido.|
|  proxies  |`dict` |Configuración del servidor proxy.|
|  use_env_proxies |`bool` |Si se debe leer la configuración del servidor proxy de las variables de entorno locales.|
|  retries  |`int` | Número total de reintentos.|
|  enable_http_logger | `bool`| Habilitar los registros de HTTP en modo de depuración (False de forma predeterminada).|
