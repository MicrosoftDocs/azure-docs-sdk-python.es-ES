---
title: Instalación
description: Cómo instalar Azure SDK para Python
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
ms.openlocfilehash: 792feac12f8328e2467017530065350e347c59b7
ms.sourcegitcommit: 757bf84535fd9d8299c4b51ec92a5ab1926cb671
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2018
ms.locfileid: "29565824"
---
# <a name="installation"></a><span data-ttu-id="5bb34-104">Instalación</span><span class="sxs-lookup"><span data-stu-id="5bb34-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="5bb34-105">Qué es Python y qué versión usar</span><span class="sxs-lookup"><span data-stu-id="5bb34-105">Which Python and which version to use</span></span>
<span data-ttu-id="5bb34-106">Existen varios intérpretes de Python disponibles, entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="5bb34-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="5bb34-107">CPython: El intérprete Python estándar y que se usa con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="5bb34-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="5bb34-108">PyPy: implementación alternativa rápida y compatible con CPython</span><span class="sxs-lookup"><span data-stu-id="5bb34-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="5bb34-109">IronPython: El intérprete Python que se ejecuta en .Net/CLR.</span><span class="sxs-lookup"><span data-stu-id="5bb34-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="5bb34-110">Jython: el intérprete Python que se ejecuta en Java Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="5bb34-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="5bb34-111">**CPython** v2.7 o v3.4+ y PyPy 5.4.0 se han probado y son compatibles con el SDK de Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="5bb34-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="5bb34-112">¿Dónde obtener Python?</span><span class="sxs-lookup"><span data-stu-id="5bb34-112">Where to get Python?</span></span>
<span data-ttu-id="5bb34-113">Existen diferentes formas de obtener CPython:</span><span class="sxs-lookup"><span data-stu-id="5bb34-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="5bb34-114">Directamente desde [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="5bb34-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="5bb34-115">De una distribución de buena reputación como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) o [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="5bb34-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="5bb34-116">Creación a partir del origen.</span><span class="sxs-lookup"><span data-stu-id="5bb34-116">Build from source!</span></span>

<span data-ttu-id="5bb34-117">A menos que tenga una necesidad específica, recomendamos las dos primeras opciones.</span><span class="sxs-lookup"><span data-stu-id="5bb34-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="5bb34-118">Instalación con pip</span><span class="sxs-lookup"><span data-stu-id="5bb34-118">Installation with pip</span></span>

<span data-ttu-id="5bb34-119">Puede instalar individualmente la biblioteca de cada servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="5bb34-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="5bb34-120">Los paquetes de versión preliminar pueden instalarse con el indicador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="5bb34-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="5bb34-121">También puede instalar un conjunto de bibliotecas de Azure en una sola línea con el metapaquete `azure` .</span><span class="sxs-lookup"><span data-stu-id="5bb34-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="5bb34-122">Hemos publicado una versión preliminar de este paquete, al que puede acceder con la marca --pre:</span><span class="sxs-lookup"><span data-stu-id="5bb34-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="5bb34-123">Instalación de GitHub</span><span class="sxs-lookup"><span data-stu-id="5bb34-123">Install from GitHub</span></span>

<span data-ttu-id="5bb34-124">Si desea instalar `azure` desde el origen:</span><span class="sxs-lookup"><span data-stu-id="5bb34-124">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install