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
# <a name="operation-config"></a><span data-ttu-id="100fe-104">Configuración de operaciones</span><span class="sxs-lookup"><span data-stu-id="100fe-104">Operation config</span></span> 

<span data-ttu-id="100fe-105">Los métodos en operaciones tienen parámetros adicionales que se pueden proporcionar en elementos `kwargs`.</span><span class="sxs-lookup"><span data-stu-id="100fe-105">Methods on operations have extra parameters which can be provided in the `kwargs`.</span></span> <span data-ttu-id="100fe-106">Esto se denomina operation_config.</span><span class="sxs-lookup"><span data-stu-id="100fe-106">This is called operation_config.</span></span>

<span data-ttu-id="100fe-107">Las opciones de configuración de operaciones son:</span><span class="sxs-lookup"><span data-stu-id="100fe-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="100fe-108">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="100fe-108">Parameter name</span></span>|<span data-ttu-id="100fe-109">Type</span><span class="sxs-lookup"><span data-stu-id="100fe-109">Type</span></span>|<span data-ttu-id="100fe-110">Rol</span><span class="sxs-lookup"><span data-stu-id="100fe-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="100fe-111">Comprobación</span><span class="sxs-lookup"><span data-stu-id="100fe-111">verify</span></span> |`bool`|<span data-ttu-id="100fe-112">Si se debe comprobar el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="100fe-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="100fe-113">El valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="100fe-113">Default is True.</span></span>|
|  <span data-ttu-id="100fe-114">cert</span><span class="sxs-lookup"><span data-stu-id="100fe-114">cert</span></span> |`str`| <span data-ttu-id="100fe-115">Ruta de acceso al certificado local para la comprobación del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="100fe-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="100fe-116">timeout</span><span class="sxs-lookup"><span data-stu-id="100fe-116">timeout</span></span> |`int`| <span data-ttu-id="100fe-117">Tiempo de espera para establecer una conexión de servidor, en segundos.</span><span class="sxs-lookup"><span data-stu-id="100fe-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="100fe-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="100fe-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="100fe-119">Si se permiten redirecciones.</span><span class="sxs-lookup"><span data-stu-id="100fe-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="100fe-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="100fe-120">max_redirects</span></span>  |`int`| <span data-ttu-id="100fe-121">Número máximo de redirecciones permitido.</span><span class="sxs-lookup"><span data-stu-id="100fe-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="100fe-122">proxies</span><span class="sxs-lookup"><span data-stu-id="100fe-122">proxies</span></span>  |`dict` |<span data-ttu-id="100fe-123">Configuración del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="100fe-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="100fe-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="100fe-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="100fe-125">Si se debe leer la configuración del servidor proxy de las variables de entorno locales.</span><span class="sxs-lookup"><span data-stu-id="100fe-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="100fe-126">retries</span><span class="sxs-lookup"><span data-stu-id="100fe-126">retries</span></span>  |`int` | <span data-ttu-id="100fe-127">Número total de reintentos.</span><span class="sxs-lookup"><span data-stu-id="100fe-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="100fe-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="100fe-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="100fe-129">Habilitar los registros de HTTP en modo de depuración (False de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="100fe-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
