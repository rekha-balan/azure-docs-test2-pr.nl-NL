---
title: Python Quickstart for Azure Cognitive Services, Bing Video Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing Video Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: ce4356f05e69540bc3bc3241e2ec1751ff7a7276
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869217"
---
# <a name="quickstart-for-bing-video-search-api-with-python"></a><span data-ttu-id="4fc7c-103">Quickstart for Bing Video Search API with Python</span><span class="sxs-lookup"><span data-stu-id="4fc7c-103">Quickstart for Bing Video Search API with Python</span></span>

<span data-ttu-id="4fc7c-104">This walkthrough shows you how to use the Bing Video Search API, part of Microsoft Cognitive Services on Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-104">This walkthrough shows you how to use the Bing Video Search API, part of Microsoft Cognitive Services on Azure.</span></span> <span data-ttu-id="4fc7c-105">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) for technical details about the APIs.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-105">Refer to the [API reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) for technical details about the APIs.</span></span>

<span data-ttu-id="4fc7c-106">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span><span class="sxs-lookup"><span data-stu-id="4fc7c-106">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span></span> 

<span data-ttu-id="4fc7c-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingVideoSearchAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="4fc7c-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingVideoSearchAPI.ipynb)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="4fc7c-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4fc7c-108">Prerequisites</span></span>
<span data-ttu-id="4fc7c-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="4fc7c-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="4fc7c-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="running-the-walkthrough"></a><span data-ttu-id="4fc7c-112">Running the walkthrough</span><span class="sxs-lookup"><span data-stu-id="4fc7c-112">Running the walkthrough</span></span>

<span data-ttu-id="4fc7c-113">First, set `subscription_key` to your API key for the Bing API service.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-113">First, set `subscription_key` to your API key for the Bing API service.</span></span>


```python
subscription_key = None
assert subscription_key
```

<span data-ttu-id="4fc7c-114">Next, verify that the `search_url` endpoint is correct.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-114">Next, verify that the `search_url` endpoint is correct.</span></span> <span data-ttu-id="4fc7c-115">At this writing, only one endpoint is used for Bing search APIs.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-115">At this writing, only one endpoint is used for Bing search APIs.</span></span> <span data-ttu-id="4fc7c-116">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-116">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span></span>


```python
search_url = "https://api.cognitive.microsoft.com/bing/v7.0/videos/search"
```

<span data-ttu-id="4fc7c-117">Set `search_term` to look for videos of kittens</span><span class="sxs-lookup"><span data-stu-id="4fc7c-117">Set `search_term` to look for videos of kittens</span></span>


```python
search_term = "kittens"
```

<span data-ttu-id="4fc7c-118">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-118">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span></span> <span data-ttu-id="4fc7c-119">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-119">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span></span> <span data-ttu-id="4fc7c-120">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) documentation.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-120">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-video-api-v7-reference) documentation.</span></span>


```python
import requests

headers = {"Ocp-Apim-Subscription-Key" : subscription_key}
params  = {"q": search_term, "count":5, "pricing": "free", "videoLength":"short"}
response = requests.get(search_url, headers=headers, params=params)
response.raise_for_status()
search_results = response.json()
```

<span data-ttu-id="4fc7c-121">The `search_results` object contains the relevant videos along with rich metadata.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-121">The `search_results` object contains the relevant videos along with rich metadata.</span></span> <span data-ttu-id="4fc7c-122">To view one of the videos, use its `embedHtml` property and insert it into an `IFrame`.</span><span class="sxs-lookup"><span data-stu-id="4fc7c-122">To view one of the videos, use its `embedHtml` property and insert it into an `IFrame`.</span></span>


```python
from IPython.display import HTML
HTML(search_results["value"][0]["embedHtml"].replace("autoplay=1","autoplay=0"))
```

## <a name="next-steps"></a><span data-ttu-id="4fc7c-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="4fc7c-123">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="4fc7c-124">[Paging videos](paging-videos.md)
> [Resizing and cropping thumbnail images](resize-and-crop-thumbnails.md)</span><span class="sxs-lookup"><span data-stu-id="4fc7c-124">[Paging videos](paging-videos.md)
[Resizing and cropping thumbnail images](resize-and-crop-thumbnails.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="4fc7c-125">See also</span><span class="sxs-lookup"><span data-stu-id="4fc7c-125">See also</span></span> 

 <span data-ttu-id="4fc7c-126">[Searching the web for videos](search-the-web.md) [Try it](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/)</span><span class="sxs-lookup"><span data-stu-id="4fc7c-126">[Searching the web for videos](search-the-web.md) [Try it](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/)</span></span>
