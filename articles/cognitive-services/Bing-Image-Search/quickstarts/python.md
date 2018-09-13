---
title: 'Quickstart: Send search queries using the REST API for the Bing Image Search API in Python'
description: In this quickstart, you send search queries to the Bing Search API to get a list of relevant images using Python.
services: cognitive-services
author: v-jerkin
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 9/21/2017
ms.author: v-jerkin
ms.openlocfilehash: bc527ba39b580935f113f56aa63f7bdd283ba304
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869878"
---
# <a name="quickstart-send-search-queries-using-the-rest-api-and-python"></a><span data-ttu-id="6ed21-103">Quickstart: Send search queries using the REST API and Python</span><span class="sxs-lookup"><span data-stu-id="6ed21-103">Quickstart: Send search queries using the REST API and Python</span></span>

<span data-ttu-id="6ed21-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span><span class="sxs-lookup"><span data-stu-id="6ed21-104">The Bing Image Search API provides an experience similar to Bing.com/Images by letting you send a user search query to Bing and get back a list of relevant images.</span></span>

<span data-ttu-id="6ed21-105">This walkthrough demonstrates a simple example of calling into the Bing Image Search API and post-processing the resulting JSON object.</span><span class="sxs-lookup"><span data-stu-id="6ed21-105">This walkthrough demonstrates a simple example of calling into the Bing Image Search API and post-processing the resulting JSON object.</span></span> <span data-ttu-id="6ed21-106">For more information, see [Bing Image Search documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference).</span><span class="sxs-lookup"><span data-stu-id="6ed21-106">For more information, see [Bing Image Search documentation](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference).</span></span>

<span data-ttu-id="6ed21-107">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span><span class="sxs-lookup"><span data-stu-id="6ed21-107">You can run this example as a Jupyter notebook on [MyBinder](https://mybinder.org) by clicking on the launch Binder badge:</span></span> 

<span data-ttu-id="6ed21-108">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingImageSearchAPI.ipynb)</span><span class="sxs-lookup"><span data-stu-id="6ed21-108">[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingImageSearchAPI.ipynb)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ed21-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6ed21-109">Prerequisites</span></span>

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

## <a name="running-the-walkthrough"></a><span data-ttu-id="6ed21-110">Running the walkthrough</span><span class="sxs-lookup"><span data-stu-id="6ed21-110">Running the walkthrough</span></span>
<span data-ttu-id="6ed21-111">To continue with the walkthrough, set `subscription_key` to your API key for the Bing API service.</span><span class="sxs-lookup"><span data-stu-id="6ed21-111">To continue with the walkthrough, set `subscription_key` to your API key for the Bing API service.</span></span>


```python
subscription_key = None
assert subscription_key
```

<span data-ttu-id="6ed21-112">Next, verify that the `search_url` endpoint is correct.</span><span class="sxs-lookup"><span data-stu-id="6ed21-112">Next, verify that the `search_url` endpoint is correct.</span></span> <span data-ttu-id="6ed21-113">At this writing, only one endpoint is used for Bing search APIs.</span><span class="sxs-lookup"><span data-stu-id="6ed21-113">At this writing, only one endpoint is used for Bing search APIs.</span></span> <span data-ttu-id="6ed21-114">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="6ed21-114">If you encounter authorization errors, double-check this value against the Bing search endpoint in your Azure dashboard.</span></span>


```python
search_url = "https://api.cognitive.microsoft.com/bing/v7.0/images/search"
```

<span data-ttu-id="6ed21-115">Set `search_term` to look for images of puppies.</span><span class="sxs-lookup"><span data-stu-id="6ed21-115">Set `search_term` to look for images of puppies.</span></span>


```python
search_term = "puppies"
```

<span data-ttu-id="6ed21-116">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="6ed21-116">The following block uses the `requests` library in Python to call out to the Bing search APIs and return the results as a JSON object.</span></span> <span data-ttu-id="6ed21-117">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span><span class="sxs-lookup"><span data-stu-id="6ed21-117">Observe that we pass in the API key via the `headers` dictionary and the search term via the `params` dictionary.</span></span> <span data-ttu-id="6ed21-118">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) documentation.</span><span class="sxs-lookup"><span data-stu-id="6ed21-118">To see the full list of options that can be used to filter search results, refer to the [REST API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference) documentation.</span></span>


```python
import requests

headers = {"Ocp-Apim-Subscription-Key" : subscription_key}
params  = {"q": search_term, "license": "public", "imageType": "photo"}
response = requests.get(search_url, headers=headers, params=params)
response.raise_for_status()
search_results = response.json()
```

<span data-ttu-id="6ed21-119">The `search_results` object contains the actual images along with rich metadata such as related items.</span><span class="sxs-lookup"><span data-stu-id="6ed21-119">The `search_results` object contains the actual images along with rich metadata such as related items.</span></span> <span data-ttu-id="6ed21-120">For example, the following line of code can extract the thumbnail URLS for the first 16 results.</span><span class="sxs-lookup"><span data-stu-id="6ed21-120">For example, the following line of code can extract the thumbnail URLS for the first 16 results.</span></span>


```python
thumbnail_urls = [img["thumbnailUrl"] for img in search_results["value"][:16]]
```

<span data-ttu-id="6ed21-121">Then, we can use the `PIL` library to download the thumbnail images and the `matplotlib` library to render them on a $4 \times 4$ grid.</span><span class="sxs-lookup"><span data-stu-id="6ed21-121">Then, we can use the `PIL` library to download the thumbnail images and the `matplotlib` library to render them on a $4 \times 4$ grid.</span></span>


```python
%matplotlib inline
import matplotlib.pyplot as plt
from PIL import Image
from io import BytesIO

f, axes = plt.subplots(4, 4)
for i in range(4):
    for j in range(4):
        image_data = requests.get(thumbnail_urls[i+4*j])
        image_data.raise_for_status()
        image = Image.open(BytesIO(image_data.content))        
        axes[i][j].imshow(image)
        axes[i][j].axis("off")
```

## <a name="next-steps"></a><span data-ttu-id="6ed21-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="6ed21-122">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ed21-123">Bing Image Search single-page app tutorial</span><span class="sxs-lookup"><span data-stu-id="6ed21-123">Bing Image Search single-page app tutorial</span></span>](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a><span data-ttu-id="6ed21-124">See also</span><span class="sxs-lookup"><span data-stu-id="6ed21-124">See also</span></span> 

[<span data-ttu-id="6ed21-125">Bing Image Search overview</span><span class="sxs-lookup"><span data-stu-id="6ed21-125">Bing Image Search overview</span></span>](../overview.md)  
[<span data-ttu-id="6ed21-126">Try it</span><span class="sxs-lookup"><span data-stu-id="6ed21-126">Try it</span></span>](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
[<span data-ttu-id="6ed21-127">Get a free trial access key</span><span class="sxs-lookup"><span data-stu-id="6ed21-127">Get a free trial access key</span></span>](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
[<span data-ttu-id="6ed21-128">Bing Image Search API reference</span><span class="sxs-lookup"><span data-stu-id="6ed21-128">Bing Image Search API reference</span></span>](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
