---
title: "Instalación"
description: "Cómo instalar Azure SDK para Python"
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 1ee0c110673f908832c1c9e8fd6dac4c90c16e8e
ms.sourcegitcommit: ce2921d9a6f21d58fdf77cbc843c9b4af0ea796d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/31/2017
---
# <a name="installation"></a><span data-ttu-id="58800-104">Instalación</span><span class="sxs-lookup"><span data-stu-id="58800-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="58800-105">Instalación con pip</span><span class="sxs-lookup"><span data-stu-id="58800-105">Installation with pip</span></span>

<span data-ttu-id="58800-106">Puede instalar individualmente la biblioteca de cada servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="58800-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="58800-107">Los paquetes de versión preliminar pueden instalarse con el indicador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="58800-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="58800-108">También puede instalar un conjunto de bibliotecas de Azure en una sola línea con el metapaquete `azure` .</span><span class="sxs-lookup"><span data-stu-id="58800-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="58800-109">Hemos publicado una versión preliminar de este paquete, al que puede acceder con la marca --pre:</span><span class="sxs-lookup"><span data-stu-id="58800-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="58800-110">Instalación de GitHub</span><span class="sxs-lookup"><span data-stu-id="58800-110">Install from GitHub</span></span>

<span data-ttu-id="58800-111">Si desea instalar `azure` desde el origen:</span><span class="sxs-lookup"><span data-stu-id="58800-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
