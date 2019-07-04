---
title: Instalación
description: Cómo instalar Azure SDK para Python
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 478118642122d7c0c80b1ddf37b13f71d8ca3adc
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534458"
---
# <a name="installation"></a><span data-ttu-id="0b872-104">Instalación</span><span class="sxs-lookup"><span data-stu-id="0b872-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="0b872-105">Qué es Python y qué versión usar</span><span class="sxs-lookup"><span data-stu-id="0b872-105">Which Python and which version to use</span></span>

<span data-ttu-id="0b872-106">Existen varios intérpretes de Python disponibles, entre ellos se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="0b872-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="0b872-107">CPython: El intérprete Python estándar y que se usa con más frecuencia.</span><span class="sxs-lookup"><span data-stu-id="0b872-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="0b872-108">PyPy: implementación alternativa rápida y compatible con CPython</span><span class="sxs-lookup"><span data-stu-id="0b872-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="0b872-109">IronPython: El intérprete Python que se ejecuta en .Net/CLR.</span><span class="sxs-lookup"><span data-stu-id="0b872-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="0b872-110">Jython: el intérprete Python que se ejecuta en Java Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="0b872-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="0b872-111">**CPython** v2.7 o v3.4+ y PyPy 5.4.0 se han probado y son compatibles con el SDK de Azure para Python.</span><span class="sxs-lookup"><span data-stu-id="0b872-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="0b872-112">¿Dónde obtener Python?</span><span class="sxs-lookup"><span data-stu-id="0b872-112">Where to get Python?</span></span>

<span data-ttu-id="0b872-113">Existen diferentes formas de obtener CPython:</span><span class="sxs-lookup"><span data-stu-id="0b872-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="0b872-114">Directamente desde [Python](https://www.python.org/)</span><span class="sxs-lookup"><span data-stu-id="0b872-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="0b872-115">De una distribución de buena reputación como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) o [ActiveState](https://www.activestate.com/)</span><span class="sxs-lookup"><span data-stu-id="0b872-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="0b872-116">Creación a partir del origen.</span><span class="sxs-lookup"><span data-stu-id="0b872-116">Build from source!</span></span>

<span data-ttu-id="0b872-117">A menos que tenga una necesidad específica, recomendamos las dos primeras opciones.</span><span class="sxs-lookup"><span data-stu-id="0b872-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="0b872-118">Instalación con pip</span><span class="sxs-lookup"><span data-stu-id="0b872-118">Installation with pip</span></span>

<span data-ttu-id="0b872-119">Puede instalar individualmente la biblioteca de cada servicio de Azure:</span><span class="sxs-lookup"><span data-stu-id="0b872-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="0b872-120">Los paquetes de versión preliminar pueden instalarse con el indicador `--pre` :</span><span class="sxs-lookup"><span data-stu-id="0b872-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="0b872-121">También puede instalar un conjunto de bibliotecas de Azure en una sola línea con el metapaquete `azure` .</span><span class="sxs-lookup"><span data-stu-id="0b872-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="0b872-122">Hemos publicado una versión preliminar de este paquete, al que puede acceder con la marca --pre:</span><span class="sxs-lookup"><span data-stu-id="0b872-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="0b872-123">Instalación de GitHub</span><span class="sxs-lookup"><span data-stu-id="0b872-123">Install from GitHub</span></span>

<span data-ttu-id="0b872-124">Si desea instalar `azure` desde el origen:</span><span class="sxs-lookup"><span data-stu-id="0b872-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="0b872-125">Instalar una versión anterior con pip</span><span class="sxs-lookup"><span data-stu-id="0b872-125">Install an older version with pip</span></span>
<span data-ttu-id="0b872-126">Puede instalar una versión anterior de `azure` especificando los detalles de la versión "azure==3.0.0".</span><span class="sxs-lookup"><span data-stu-id="0b872-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="0b872-127">Comprobar la información de la instalación del SDK con pip</span><span class="sxs-lookup"><span data-stu-id="0b872-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="0b872-128">Puede consultar la ubicación de la instalación y la versión del SDK `azure`, entre otra información.</span><span class="sxs-lookup"><span data-stu-id="0b872-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="0b872-129">Para desinstalar con pip</span><span class="sxs-lookup"><span data-stu-id="0b872-129">To uninstall with pip</span></span>
<span data-ttu-id="0b872-130">También puede desinstalar todas las bibliotecas de Azure en una sola línea con el metapaquete `azure`.</span><span class="sxs-lookup"><span data-stu-id="0b872-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="0b872-131">`pip uninstall azure`Quita el metapaquete `azure` pero deja los paquetes `azure-*` individuales (y otros, como `adal` y `msrest`).</span><span class="sxs-lookup"><span data-stu-id="0b872-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="0b872-132">Un aspecto de Python y pip es que, para todos los paquetes que tienen dependencias, al desinstalar el paquete inicial no se desinstalan las dependencias.</span><span class="sxs-lookup"><span data-stu-id="0b872-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="0b872-133">Para quitar `azure-` y sus paquetes complementarios, ejecute el comando `pip freeze | grep 'azure-' | xargs pip uninstall -y` (y realice desinstalaciones individuales de adal, msrest y msrestazure).</span><span class="sxs-lookup"><span data-stu-id="0b872-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

