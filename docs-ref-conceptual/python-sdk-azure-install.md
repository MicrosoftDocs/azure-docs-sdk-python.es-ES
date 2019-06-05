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
ms.openlocfilehash: 6014937fb41d6074e94578ccc47c30eb7b3f63d2
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376875"
---
# <a name="installation"></a>Instalación

## <a name="which-python-and-which-version-to-use"></a>Qué es Python y qué versión usar

Existen varios intérpretes de Python disponibles, entre ellos se incluyen los siguientes:

* CPython: El intérprete Python estándar y que se usa con más frecuencia.
* PyPy: implementación alternativa rápida y compatible con CPython
* IronPython: El intérprete Python que se ejecuta en .Net/CLR.
* Jython: el intérprete Python que se ejecuta en Java Virtual Machine

**CPython** v2.7 o v3.4+ y PyPy 5.4.0 se han probado y son compatibles con el SDK de Azure para Python.

## <a name="where-to-get-python"></a>¿Dónde obtener Python?

Existen diferentes formas de obtener CPython:

* Directamente desde [Python](https://www.python.org/)
* De una distribución de buena reputación como [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) o [ActiveState](https://www.activestate.com/)
* Creación a partir del origen.

A menos que tenga una necesidad específica, recomendamos las dos primeras opciones.

## <a name="installation-with-pip"></a>Instalación con pip

Puede instalar individualmente la biblioteca de cada servicio de Azure:

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

Los paquetes de versión preliminar pueden instalarse con el indicador `--pre` :

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

También puede instalar un conjunto de bibliotecas de Azure en una sola línea con el metapaquete `azure` .

```bash
pip install azure
```

Hemos publicado una versión preliminar de este paquete, al que puede acceder con la marca --pre:

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>Instalación de GitHub

Si desea instalar `azure` desde el origen:

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```
