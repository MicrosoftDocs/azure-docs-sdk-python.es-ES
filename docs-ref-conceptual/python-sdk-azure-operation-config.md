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
ms.openlocfilehash: d7be7cd76d019c6741d93c04458376a9352e363b
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/28/2018
---
# <a name="operation-config"></a>Configuración de operaciones 

Los métodos en operaciones tienen parámetros adicionales que se pueden proporcionar en argumentos kwargs. Esto se denomina operation_config.

Las opciones de configuración de operaciones son:

|Nombre de parámetro|type|Rol|
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
