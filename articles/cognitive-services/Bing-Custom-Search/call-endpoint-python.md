---
title: Call endpoint by using Python - Bing Custom Search - Microsoft Cognitive Services
description: This quickstart shows how to request search results from your custom search instance by using Python to call the Bing Custom Search endpoint.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 05/07/2018
ms.author: v-brapel
ms.openlocfilehash: 88bf82805ba46abf79b7899e0428a83485062302
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865673"
---
# <a name="call-bing-custom-search-endpoint-python"></a><span data-ttu-id="87a05-103">Call Bing Custom Search endpoint (Python)</span><span class="sxs-lookup"><span data-stu-id="87a05-103">Call Bing Custom Search endpoint (Python)</span></span>

<span data-ttu-id="87a05-104">This quickstart shows how to request search results from your custom search instance by using Python to call the Bing Custom Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="87a05-104">This quickstart shows how to request search results from your custom search instance by using Python to call the Bing Custom Search endpoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="87a05-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="87a05-105">Prerequisites</span></span>
<span data-ttu-id="87a05-106">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="87a05-106">To complete this quickstart, you need:</span></span>

- <span data-ttu-id="87a05-107">A custom search instance.</span><span class="sxs-lookup"><span data-stu-id="87a05-107">A custom search instance.</span></span> <span data-ttu-id="87a05-108">See [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="87a05-108">See [Create your first Bing Custom Search instance](quick-start.md).</span></span>

-  <span data-ttu-id="87a05-109">[Python](https://www.python.org/) installed.</span><span class="sxs-lookup"><span data-stu-id="87a05-109">[Python](https://www.python.org/) installed.</span></span>

- <span data-ttu-id="87a05-110">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="87a05-110">A [Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="87a05-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="87a05-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span></span> <span data-ttu-id="87a05-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="87a05-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span> 

## <a name="run-the-code"></a><span data-ttu-id="87a05-113">Run the code</span><span class="sxs-lookup"><span data-stu-id="87a05-113">Run the code</span></span>

<span data-ttu-id="87a05-114">To call the Bing Custom Search endpoint, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="87a05-114">To call the Bing Custom Search endpoint, follow these steps:</span></span>

1. <span data-ttu-id="87a05-115">Create a folder for your code.</span><span class="sxs-lookup"><span data-stu-id="87a05-115">Create a folder for your code.</span></span>

2. <span data-ttu-id="87a05-116">From an administrator command prompt or terminal, navigate to the folder you just created.</span><span class="sxs-lookup"><span data-stu-id="87a05-116">From an administrator command prompt or terminal, navigate to the folder you just created.</span></span>

3. <span data-ttu-id="87a05-117">Install the **requests** python module:</span><span class="sxs-lookup"><span data-stu-id="87a05-117">Install the **requests** python module:</span></span>

    <pre>
    pip install pipenv
    pipenv install requests
    </pre>
    
7. <span data-ttu-id="87a05-118">Create the file BingCustomSearch.py and copy the following code to it.</span><span class="sxs-lookup"><span data-stu-id="87a05-118">Create the file BingCustomSearch.py and copy the following code to it.</span></span>

8. <span data-ttu-id="87a05-119">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID (see step 1).</span><span class="sxs-lookup"><span data-stu-id="87a05-119">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID (see step 1).</span></span>

    ``` Python
    import json
    import requests
    
    subscriptionKey = "YOUR-SUBSCRIPTION-KEY"
    customConfigId = "YOUR-CUSTOM-CONFIG-ID"
    searchTerm = "microsoft"
    
    url = 'https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?q=' + searchTerm + '&customconfig=' + customConfigId
    r = requests.get(url, headers={'Ocp-Apim-Subscription-Key': subscriptionKey})
    print(r.text)
    ```
9. <span data-ttu-id="87a05-120">Run the code using the following command.</span><span class="sxs-lookup"><span data-stu-id="87a05-120">Run the code using the following command.</span></span>
    ```
    python BingCustomSearch.py
    ```

## <a name="next-steps"></a><span data-ttu-id="87a05-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="87a05-121">Next steps</span></span>
- [<span data-ttu-id="87a05-122">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="87a05-122">Configure your hosted UI experience</span></span>](./hosted-ui.md)
- [<span data-ttu-id="87a05-123">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="87a05-123">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="87a05-124">Page webpages</span><span class="sxs-lookup"><span data-stu-id="87a05-124">Page webpages</span></span>](./page-webpages.md)
