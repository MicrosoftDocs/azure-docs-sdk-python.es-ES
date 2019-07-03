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
ms.openlocfilehash: 5a23a52414e70facd6feae3af3956a5131f6b5c4
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534340"
---
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="0844a-104">Módulos de Azure Cognitive Services para Python</span><span class="sxs-lookup"><span data-stu-id="0844a-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="0844a-105">Agregue funciones de reconocimiento de imagen y cara, análisis de lenguaje y búsqueda a sus aplicaciones Python, sitios web y herramientas con los módulos de Azure Cognitive Services para Python.</span><span class="sxs-lookup"><span data-stu-id="0844a-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="0844a-106">Módulos de visión</span><span class="sxs-lookup"><span data-stu-id="0844a-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="0844a-107">Computer Vision</span><span class="sxs-lookup"><span data-stu-id="0844a-107">Computer Vision</span></span> 

<span data-ttu-id="0844a-108">Devuelve información sobre el contenido visual encontrado en una imagen:</span><span class="sxs-lookup"><span data-stu-id="0844a-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="0844a-109">Use etiquetado, descripciones y modelos específicos del dominio para identificar el contenido y etiquetarlo con confianza.</span><span class="sxs-lookup"><span data-stu-id="0844a-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="0844a-110">Aplique la configuración para adultos para habilitar la restricción automatizada de contenido adulto.</span><span class="sxs-lookup"><span data-stu-id="0844a-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="0844a-111">Identifique los tipos y los esquemas de color de las imágenes.</span><span class="sxs-lookup"><span data-stu-id="0844a-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="0844a-112">[Pruebe Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) de forma gratuita en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="0844a-113">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="0844a-114">[Obtenga más información](/azure/cognitive-services/computer-vision/home) acerca de Computer Vision API y empiece a trabajar con la [guía de inicio rápido de Computer Vision API para Python](/azure/cognitive-services/computer-vision/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="0844a-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="0844a-115">Content Moderator</span></span>

<span data-ttu-id="0844a-116">Moderación de texto, vídeo e imágenes asistida por máquina, mejorada con herramientas de revisión humanas.</span><span class="sxs-lookup"><span data-stu-id="0844a-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="0844a-117">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-contentmoderator
```

<span data-ttu-id="0844a-118">[Obtenga más información](/azure/cognitive-services/content-moderator/overview) acerca del servicio Content Moderator.</span><span class="sxs-lookup"><span data-stu-id="0844a-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="0844a-119">Custom Vision Service</span><span class="sxs-lookup"><span data-stu-id="0844a-119">Custom Vision Service</span></span>

<span data-ttu-id="0844a-120">Cargue imágenes para entrenar y personalizar un modelo de visión de equipo para sus necesidades específicas.</span><span class="sxs-lookup"><span data-stu-id="0844a-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="0844a-121">Una vez entrenado el modelo, puede usar la API para etiquetar imágenes utilizando el modelo y evaluar los resultados para mejorar el clasificador.</span><span class="sxs-lookup"><span data-stu-id="0844a-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="0844a-122">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="0844a-123">[Obtenga más información](/azure/cognitive-services/Custom-Vision-Service/home) acerca del servicio Custom Vision y empiece a trabajar con el [tutorial de Custom Vision para Python](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span><span class="sxs-lookup"><span data-stu-id="0844a-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="0844a-124">Face API</span><span class="sxs-lookup"><span data-stu-id="0844a-124">Face API</span></span>

<span data-ttu-id="0844a-125">Detecte, identifique, analice, organice y etiquete las caras en las fotos.</span><span class="sxs-lookup"><span data-stu-id="0844a-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="0844a-126">[Pruebe Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="0844a-127">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install cognitive-face
```

<span data-ttu-id="0844a-128">[Obtenga más información](/azure/cognitive-services/face/overview) acerca de Face API y empiece a trabajar con la [guía de inicio rápido de Face API para Python](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span><span class="sxs-lookup"><span data-stu-id="0844a-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="0844a-129">Módulos de búsqueda</span><span class="sxs-lookup"><span data-stu-id="0844a-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="0844a-130">Búsqueda web</span><span class="sxs-lookup"><span data-stu-id="0844a-130">Web search</span></span>

<span data-ttu-id="0844a-131">Recupere documentos web indexados por Bing Web Search API y limite los resultados según el tipo, la actualidad y muchos otros criterios.</span><span class="sxs-lookup"><span data-stu-id="0844a-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="0844a-132">[Pruebe Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="0844a-133">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="0844a-134">[Obtenga más información](/azure/cognitive-services/bing-web-search/overview) acerca de Bing Web Search API y empiece a trabajar con la [guía de inicio rápido de Web Search API para Python](/azure/cognitive-services/bing-web-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="0844a-135">Búsqueda de imágenes</span><span class="sxs-lookup"><span data-stu-id="0844a-135">Image search</span></span>

<span data-ttu-id="0844a-136">Busque imágenes y obtenga vistas en miniatura, direcciones URL completas de imágenes, metadatos de imagen y mucho más en los resultados.</span><span class="sxs-lookup"><span data-stu-id="0844a-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="0844a-137">[Pruebe Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="0844a-138">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="0844a-139">[Obtenga más información](/azure/cognitive-services/bing-image-search/overview) acerca de Bing Image Search API y empiece a trabajar con la [guía de inicio rápido de Image Search API para Python](/azure/cognitive-services/bing-image-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="0844a-140">Búsqueda de entidades</span><span class="sxs-lookup"><span data-stu-id="0844a-140">Entity search</span></span>

<span data-ttu-id="0844a-141">Busque la entidad más pertinente (lugar, persona o cosa) para un término de búsqueda o una ubicación determinados.</span><span class="sxs-lookup"><span data-stu-id="0844a-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="0844a-142">[Pruebe Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="0844a-143">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="0844a-144">[Obtenga más información](/azure/cognitive-services/bing-entities-search/search-the-web) acerca de Bing Entity Search API y empiece a trabajar con la [guía de inicio rápido de Entity Search API para Python](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="0844a-145">Búsqueda personalizada</span><span class="sxs-lookup"><span data-stu-id="0844a-145">Custom search</span></span>

<span data-ttu-id="0844a-146">Cree una búsqueda web personalizada que cumpla los requisitos específicos de su dominio de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="0844a-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="0844a-147">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="0844a-148">[Obtenga más información](/azure/cognitive-services/bing-custom-search/) acerca del servicio Bing Custom Search y empiece a realizar consultas a su motor de búsqueda personalizado desde Python con la [guía de inicio rápido de Custom Search API para Python](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span><span class="sxs-lookup"><span data-stu-id="0844a-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="0844a-149">Búsqueda de vídeos</span><span class="sxs-lookup"><span data-stu-id="0844a-149">Video search</span></span>

<span data-ttu-id="0844a-150">Busque vídeos en Internet y obtenga resultados con metadatos del creador, codificación, duración y número de visualizaciones.</span><span class="sxs-lookup"><span data-stu-id="0844a-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="0844a-151">[Pruebe Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="0844a-152">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="0844a-153">[Obtenga más información](/azure/cognitive-services/bing-video-search/search-the-web) acerca del servicio Bing Video Search y empiece a trabajar con la [guía de inicio rápido de Video Search API para Python](/azure/cognitive-services/bing-video-search/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="0844a-154">Búsqueda de noticias</span><span class="sxs-lookup"><span data-stu-id="0844a-154">News search</span></span>

<span data-ttu-id="0844a-155">Busque en Internet artículos de noticias y trabaje con los metadatos del artículo, noticias relacionadas, imágenes e información del proveedor.</span><span class="sxs-lookup"><span data-stu-id="0844a-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="0844a-156">[Pruebe News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="0844a-157">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="0844a-158">[Obtenga más información](/azure/cognitive-services/bing-news-search/search-the-web) acerca del servicio Bing News Search y empiece a trabajar con la [guía de inicio rápido de News Search API para Python](/azure/cognitive-services/bing-news-search/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](/azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="0844a-159">Modelo de lenguaje</span><span class="sxs-lookup"><span data-stu-id="0844a-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="0844a-160">Text Analytics</span><span class="sxs-lookup"><span data-stu-id="0844a-160">Text Analytics</span></span> 

<span data-ttu-id="0844a-161">Text Analytics API es un servicio en la nube que realiza el procesamiento del lenguaje natural en textos sin formato.</span><span class="sxs-lookup"><span data-stu-id="0844a-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="0844a-162">La API incluye tres funciones principales:</span><span class="sxs-lookup"><span data-stu-id="0844a-162">The API includes three main functions:</span></span>

- <span data-ttu-id="0844a-163">análisis de opiniones</span><span class="sxs-lookup"><span data-stu-id="0844a-163">Sentiment analysis</span></span>
- <span data-ttu-id="0844a-164">Extracción de la frase clave</span><span class="sxs-lookup"><span data-stu-id="0844a-164">Key phrase extraction</span></span>
- <span data-ttu-id="0844a-165">Detección de idiomas</span><span class="sxs-lookup"><span data-stu-id="0844a-165">Language detection</span></span>

<span data-ttu-id="0844a-166">[Pruebe Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="0844a-167">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="0844a-168">[Obtenga más información](/azure/cognitive-services/text-analytics/overview) acerca de Text Analytics API y empiece a trabajar con la [guía de inicio rápido de Text Analytics API para Python](/azure/cognitive-services/text-analytics/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="0844a-169">Corrector ortográfico</span><span class="sxs-lookup"><span data-stu-id="0844a-169">Spell Check</span></span>

<span data-ttu-id="0844a-170">Compruebe la gramática y la ortografía en contexto con Bing Spell Check API.</span><span class="sxs-lookup"><span data-stu-id="0844a-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="0844a-171">[Pruebe Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) en su explorador.</span><span class="sxs-lookup"><span data-stu-id="0844a-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="0844a-172">Obtenga el módulo de Python con [pip](https://pip.pypa.io/en/stable/quickstart/):</span><span class="sxs-lookup"><span data-stu-id="0844a-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="0844a-173">[Obtenga más información](/azure/cognitive-services/bing-spell-check/proof-text) acerca de Spell Check API y empiece a trabajar con la [guía de inicio rápido de Spell Check API para Python](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span><span class="sxs-lookup"><span data-stu-id="0844a-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>
