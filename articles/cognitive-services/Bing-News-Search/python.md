---
title: Python Quickstart for Azure Cognitive Services, Bing News Search API | Microsoft Docs
description: Get information and code samples to help you quickly get started using the Bing News Search API in Microsoft Cognitive Services on Azure.
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: 0fde478b650513aa1527c1d47f5b453ba094506c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865776"
---
# <a name="quickstart-for-bing-news-search-api-with-python"></a><span data-ttu-id="a8c98-103">Quickstart for Bing News Search API with Python</span><span class="sxs-lookup"><span data-stu-id="a8c98-103">Quickstart for Bing News Search API with Python</span></span>
<span data-ttu-id="a8c98-104">This walkthrough demonstrates a simple example of calling into the Bing News Search API and post-processing the resulting JSON object.</span><span class="sxs-lookup"><span data-stu-id="a8c98-104">This walkthrough demonstrates a simple example of calling into the Bing News Search API and post-processing the resulting JSON object.</span></span> <span data-ttu-id="a8c98-105">For more information, see [Bing New Search documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference).</span><span class="sxs-lookup"><span data-stu-id="a8c98-105">For more information, see [Bing New Search documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference).</span></span>  

<span data-ttu-id="a8c98-106">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span><span class="sxs-lookup"><span data-stu-id="a8c98-106">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span></span> 

<span data-ttu-id="a8c98-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingNewsSearchAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="a8c98-107">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingNewsSearchAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8c98-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8c98-108">Prerequisites</span></span>

<span data-ttu-id="a8c98-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="a8c98-109">You must have a [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="a8c98-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="a8c98-110">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-web-search-api) is sufficient for this quickstart.</span></span> <span data-ttu-id="a8c98-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="a8c98-111">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="running-the-walkthrough"></a><span data-ttu-id="a8c98-112">Running the walkthrough</span><span class="sxs-lookup"><span data-stu-id="a8c98-112">Running the walkthrough</span></span>
<span data-ttu-id="a8c98-113">First, set `subscription_key` to your API key for the Bing API service.</span><span class="sxs-lookup"><span data-stu-id="a8c98-113">First, set `subscription_key` to your API key for the Bing API service.</span></span>


```python
subscription_key = None
assert subscription_key
```

<span data-ttu-id="a8c98-114">Next, verify that the `search_url` endpoint is correct.</span><span class="sxs-lookup"><span data-stu-id="a8c98-114">Next, verify that the `search_url` endpoint is correct.</span></span> <span data-ttu-id="a8c98-115">At this writing, only one endpoint is used for Bing search APIs.</span><span class="sxs-lookup"><span data-stu-id="a8c98-115">At this writing, only one endpoint is used for Bing search APIs.</span></span> <span data-ttu-id="a8c98-116">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="a8c98-116">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span></span>


```python
search_url = "https://api.cognitive.microsoft.com/bing/v7.0/news/search"
```

<span data-ttu-id="a8c98-117">Set `search_term` to look for news articles about Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a8c98-117">Set `search_term` to look for news articles about Microsoft.</span></span>


```python
search_term = "Microsoft"
```

<span data-ttu-id="a8c98-118">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="a8c98-118">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span></span> <span data-ttu-id="a8c98-119">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="a8c98-119">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span></span> <span data-ttu-id="a8c98-120">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) documentation.</span><span class="sxs-lookup"><span data-stu-id="a8c98-120">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-news-api-v7-reference) documentation.</span></span>


```python
import requests

headers = {"Ocp-Apim-Subscription-Key" : subscription_key}
params  = {"q": search_term, "textDecorations": True, "textFormat": "HTML"}
response = requests.get(search_url, headers=headers, params=params)
response.raise_for_status()
search_results = response.json()
```

<span data-ttu-id="a8c98-121">The `search_results` object contains the relevant new articles along with rich metadata.</span><span class="sxs-lookup"><span data-stu-id="a8c98-121">The `search_results` object contains the relevant new articles along with rich metadata.</span></span> <span data-ttu-id="a8c98-122">For example, the following line of code extracts the descriptions of the articles.</span><span class="sxs-lookup"><span data-stu-id="a8c98-122">For example, the following line of code extracts the descriptions of the articles.</span></span>


```python
descriptions = [article["description"] for article in search_results["value"]]
```

<span data-ttu-id="a8c98-123">These descriptions can then be rendered as a table with the search keyword highlighted in **bold**.</span><span class="sxs-lookup"><span data-stu-id="a8c98-123">These descriptions can then be rendered as a table with the search keyword highlighted in **bold**.</span></span>


```python
from IPython.display import HTML
rows = "\n".join(["<tr><td>{0}</td></tr>".format(desc) for desc in descriptions])
HTML("<table>"+rows+"</table>")
```

## <a name="next-steps"></a><span data-ttu-id="a8c98-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8c98-124">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="a8c98-125">[Paging news](paging-news.md)
> [Using decoration markers to highlight text](hit-highlighting.md)</span><span class="sxs-lookup"><span data-stu-id="a8c98-125">[Paging news](paging-news.md)
[Using decoration markers to highlight text](hit-highlighting.md)</span></span>

## <a name="see-also"></a><span data-ttu-id="a8c98-126">See also</span><span class="sxs-lookup"><span data-stu-id="a8c98-126">See also</span></span> 

 [<span data-ttu-id="a8c98-127">Searching the web for news</span><span class="sxs-lookup"><span data-stu-id="a8c98-127">Searching the web for news</span></span>](search-the-web.md)  
 [<span data-ttu-id="a8c98-128">Try it</span><span class="sxs-lookup"><span data-stu-id="a8c98-128">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/)
