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

## <a name="install-an-older-version-with-pip"></a>Instalar una versión anterior con pip
Puede instalar una versión anterior de `azure` especificando los detalles de la versión "azure==3.0.0".
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a>Comprobar la información de la instalación del SDK con pip
Puede consultar la ubicación de la instalación y la versión del SDK `azure`, entre otra información.
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a>Para desinstalar con pip
También puede desinstalar todas las bibliotecas de Azure en una sola línea con el metapaquete `azure`.
```bash
pip uninstall azure 
```
> [!NOTE]
> `pip uninstall azure`Quita el metapaquete `azure` pero deja los paquetes `azure-*` individuales (y otros, como `adal` y `msrest`). Un aspecto de Python y pip es que, para todos los paquetes que tienen dependencias, al desinstalar el paquete inicial no se desinstalan las dependencias. Para quitar `azure-` y sus paquetes complementarios, ejecute el comando `pip freeze | grep 'azure-' | xargs pip uninstall -y` (y realice desinstalaciones individuales de adal, msrest y msrestazure).

