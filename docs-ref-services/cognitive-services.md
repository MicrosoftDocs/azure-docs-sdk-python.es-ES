---
title: Módulos de Azure Cognitive Services para Python
description: Referencia de los módulos de Azure Cognitive Services para Python
keywords: Azure, python, SDK, API, Cognitive Services
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 736b2dd747842caa50418afc8219dafae655db39
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277462"
---
# <a name="azure-cognitive-services-modules-for-python"></a>Módulos de Azure Cognitive Services para Python

Agregue funciones de reconocimiento de imagen y cara, análisis de lenguaje y búsqueda a sus aplicaciones Python, sitios web y herramientas con los módulos de Azure Cognitive Services para Python.

## <a name="vision-modules"></a>Módulos de visión

### <a name="computer-vision"></a>Computer Vision 

Devuelve información sobre el contenido visual encontrado en una imagen:

- Use etiquetado, descripciones y modelos específicos del dominio para identificar el contenido y etiquetarlo con confianza.
- Aplique la configuración para adultos para habilitar la restricción automatizada de contenido adulto.
- Identifique los tipos y los esquemas de color de las imágenes.

[Pruebe Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) de forma gratuita en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-computervision
```

[Obtenga más información](/azure/cognitive-services/computer-vision/home) acerca de Computer Vision API y empiece a trabajar con la [guía de inicio rápido de Computer Vision API para Python](/azure/cognitive-services/computer-vision/quickstarts/python).

### <a name="content-moderator"></a>Content Moderator

Moderación de texto, vídeo e imágenes asistida por máquina, mejorada con herramientas de revisión humanas.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-computervision
```

[Obtenga más información](/azure/cognitive-services/content-moderator/overview) acerca del servicio Content Moderator.

### <a name="custom-vision-service"></a>Custom Vision Service

Cargue imágenes para entrenar y personalizar un modelo de visión de equipo para sus necesidades específicas. Una vez entrenado el modelo, puede usar la API para etiquetar imágenes utilizando el modelo y evaluar los resultados para mejorar el clasificador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-vision-customvision
```

[Obtenga más información](/azure/cognitive-services/Custom-Vision-Service/home) acerca del servicio Custom Vision y empiece a trabajar con el [tutorial de Custom Vision para Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)

### <a name="face-api"></a>Face API

Detecte, identifique, analice, organice y etiquete las caras en las fotos. 

[Pruebe Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install cognitive-face
```

[Obtenga más información](/azure/cognitive-services/face/overview) acerca de Face API y empiece a trabajar con la [guía de inicio rápido de Face API para Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).

## <a name="search-modules"></a>Módulos de búsqueda

### <a name="web-search"></a>Búsqueda web

Recupere documentos web indexados por Bing Web Search API y limite los resultados según el tipo, la actualidad y muchos otros criterios. 

[Pruebe Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-websearch
```

[Obtenga más información](/azure/cognitive-services/bing-web-search/overview) acerca de Bing Web Search API y empiece a trabajar con la [guía de inicio rápido de Web Search API para Python](/azure/cognitive-services/bing-web-search/quickstarts/python).

### <a name="image-search"></a>Búsqueda de imágenes

Busque imágenes y obtenga vistas en miniatura, direcciones URL completas de imágenes, metadatos de imagen y mucho más en los resultados.

[Pruebe Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-imagesearch
```

[Obtenga más información](/azure/cognitive-services/bing-image-search/overview) acerca de Bing Image Search API y empiece a trabajar con la [guía de inicio rápido de Image Search API para Python](/azure/cognitive-services/bing-image-search/quickstarts/python).


### <a name="entity-search"></a>Búsqueda de entidades

Busque la entidad más pertinente (lugar, persona o cosa) para un término de búsqueda o una ubicación determinados.

[Pruebe Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-entitysearch
```

[Obtenga más información](/azure/cognitive-services/bing-entities-search/search-the-web) acerca de Bing Entity Search API y empiece a trabajar con la [guía de inicio rápido de Entity Search API para Python](/azure/cognitive-services/bing-entities-search/quickstarts/python).

### <a name="custom-search"></a>Búsqueda personalizada

Cree una búsqueda web personalizada que cumpla los requisitos específicos de su dominio de búsqueda.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-customsearch
```

[Obtenga más información](/azure/cognitive-services/bing-custom-search/) acerca del servicio Bing Custom Search y empiece a realizar consultas a su motor de búsqueda personalizado desde Python con la [guía de inicio rápido de Custom Search API para Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python).

### <a name="video-search"></a>Búsqueda de vídeos

Busque vídeos en Internet y obtenga resultados con metadatos del creador, codificación, duración y número de visualizaciones.

[Pruebe Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-videosearch
```

[Obtenga más información](/azure/cognitive-services/bing-video-search/search-the-web) acerca del servicio Bing Video Search y empiece a trabajar con la [guía de inicio rápido de Video Search API para Python](/azure/cognitive-services/bing-video-search/python).


### <a name="news-search"></a>Búsqueda de noticias

Busque en Internet artículos de noticias y trabaje con los metadatos del artículo, noticias relacionadas, imágenes e información del proveedor.

[Pruebe News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-search-newssearch
```

[Obtenga más información](/azure/cognitive-services/bing-news-search/search-the-web) acerca del servicio Bing News Search y empiece a trabajar con la [guía de inicio rápido de News Search API para Python](//azure/cognitive-services/bing-news-search/python).


## <a name="language-modules"></a>Modelo de lenguaje

### <a name="text-analytics"></a>Text Analytics 

Text Analytics API es un servicio en la nube que realiza el procesamiento del lenguaje natural en textos sin formato. La API incluye tres funciones principales:

- análisis de opiniones
- Extracción de la frase clave
- Detección de idiomas

[Pruebe Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-textanalytics
```

[Obtenga más información](/azure/cognitive-services/text-analytics/overview) acerca de Text Analytics API y empiece a trabajar con la [guía de inicio rápido de Text Analytics API para Python](/azure/cognitive-services/text-analytics/quickstarts/python).


### <a name="spell-check"></a>Corrector ortográfico

Compruebe la gramática y la ortografía en contexto con Bing Spell Check API.

[Pruebe Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) en su explorador.

Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):

```
pip install azure-cognitiveservices-language-spellcheck
```

[Obtenga más información](/azure/cognitive-services/bing-spell-check/proof-text) acerca de Spell Check API y empiece a trabajar con la [guía de inicio rápido de Spell Check API para Python](/azure/cognitive-services/bing-spell-check/quickstarts/python).