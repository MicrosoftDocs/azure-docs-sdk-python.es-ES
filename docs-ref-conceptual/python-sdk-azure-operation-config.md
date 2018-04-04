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
# <a name="operation-config"></a><span data-ttu-id="a85ce-104">Configuración de operaciones</span><span class="sxs-lookup"><span data-stu-id="a85ce-104">Operation config</span></span> 

<span data-ttu-id="a85ce-105">Los métodos en operaciones tienen parámetros adicionales que se pueden proporcionar en argumentos kwargs.</span><span class="sxs-lookup"><span data-stu-id="a85ce-105">Methods on operations have extra parameters which can be provided in the kwargs.</span></span> <span data-ttu-id="a85ce-106">Esto se denomina operation_config.</span><span class="sxs-lookup"><span data-stu-id="a85ce-106">This is called operation_config.</span></span>

<span data-ttu-id="a85ce-107">Las opciones de configuración de operaciones son:</span><span class="sxs-lookup"><span data-stu-id="a85ce-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="a85ce-108">Nombre de parámetro</span><span class="sxs-lookup"><span data-stu-id="a85ce-108">Parameter name</span></span>|<span data-ttu-id="a85ce-109">type</span><span class="sxs-lookup"><span data-stu-id="a85ce-109">Type</span></span>|<span data-ttu-id="a85ce-110">Rol</span><span class="sxs-lookup"><span data-stu-id="a85ce-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="a85ce-111">Comprobación</span><span class="sxs-lookup"><span data-stu-id="a85ce-111">verify</span></span> |`bool`|<span data-ttu-id="a85ce-112">Si se debe comprobar el certificado SSL.</span><span class="sxs-lookup"><span data-stu-id="a85ce-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="a85ce-113">El valor predeterminado es True.</span><span class="sxs-lookup"><span data-stu-id="a85ce-113">Default is True.</span></span>|
|  <span data-ttu-id="a85ce-114">cert</span><span class="sxs-lookup"><span data-stu-id="a85ce-114">cert</span></span> |`str`| <span data-ttu-id="a85ce-115">Ruta de acceso al certificado local para la comprobación del lado cliente.</span><span class="sxs-lookup"><span data-stu-id="a85ce-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="a85ce-116">timeout</span><span class="sxs-lookup"><span data-stu-id="a85ce-116">timeout</span></span> |`int`| <span data-ttu-id="a85ce-117">Tiempo de espera para establecer una conexión de servidor, en segundos.</span><span class="sxs-lookup"><span data-stu-id="a85ce-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="a85ce-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="a85ce-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="a85ce-119">Si se permiten redirecciones.</span><span class="sxs-lookup"><span data-stu-id="a85ce-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="a85ce-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="a85ce-120">max_redirects</span></span>  |`int`| <span data-ttu-id="a85ce-121">Número máximo de redirecciones permitido.</span><span class="sxs-lookup"><span data-stu-id="a85ce-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="a85ce-122">proxies</span><span class="sxs-lookup"><span data-stu-id="a85ce-122">proxies</span></span>  |`dict` |<span data-ttu-id="a85ce-123">Configuración del servidor proxy.</span><span class="sxs-lookup"><span data-stu-id="a85ce-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="a85ce-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="a85ce-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="a85ce-125">Si se debe leer la configuración del servidor proxy de las variables de entorno locales.</span><span class="sxs-lookup"><span data-stu-id="a85ce-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="a85ce-126">retries</span><span class="sxs-lookup"><span data-stu-id="a85ce-126">retries</span></span>  |`int` | <span data-ttu-id="a85ce-127">Número total de reintentos.</span><span class="sxs-lookup"><span data-stu-id="a85ce-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="a85ce-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="a85ce-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="a85ce-129">Habilitar los registros de HTTP en modo de depuración (False de forma predeterminada).</span><span class="sxs-lookup"><span data-stu-id="a85ce-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
