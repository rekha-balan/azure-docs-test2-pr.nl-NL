---
title: Call endpoint by using Node.js - Bing Custom Search - Microsoft Cognitive Services
description: This quickstart shows how to request search results from your custom search instance by using Node.js to call the Bing Custom Search endpoint.
services: cognitive-services
author: brapel
manager: ehansen
ms.service: cognitive-services
ms.component: bing-custom-search
ms.topic: article
ms.date: 05/07/2018
ms.author: v-brapel
ms.openlocfilehash: 5d9391cc486dc868a1a291ccc7095291cddd3e4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870022"
---
# <a name="call-bing-custom-search-endpoint-nodejs"></a><span data-ttu-id="96a15-103">Call Bing Custom Search endpoint (Node.js)</span><span class="sxs-lookup"><span data-stu-id="96a15-103">Call Bing Custom Search endpoint (Node.js)</span></span>

<span data-ttu-id="96a15-104">This quickstart shows how to request search results from your custom search instance by using Node.js to call the Bing Custom Search endpoint.</span><span class="sxs-lookup"><span data-stu-id="96a15-104">This quickstart shows how to request search results from your custom search instance by using Node.js to call the Bing Custom Search endpoint.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="96a15-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96a15-105">Prerequisites</span></span>
<span data-ttu-id="96a15-106">To complete this quickstart, you need:</span><span class="sxs-lookup"><span data-stu-id="96a15-106">To complete this quickstart, you need:</span></span>

- <span data-ttu-id="96a15-107">A custom search instance.</span><span class="sxs-lookup"><span data-stu-id="96a15-107">A custom search instance.</span></span> <span data-ttu-id="96a15-108">See [Create your first Bing Custom Search instance](quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="96a15-108">See [Create your first Bing Custom Search instance](quick-start.md).</span></span>

- <span data-ttu-id="96a15-109">[Node.js](https://www.nodejs.org/) installed.</span><span class="sxs-lookup"><span data-stu-id="96a15-109">[Node.js](https://www.nodejs.org/) installed.</span></span>

-  <span data-ttu-id="96a15-110">[Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span><span class="sxs-lookup"><span data-stu-id="96a15-110">[Cognitive Services API account](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) with **Bing Search APIs**.</span></span> <span data-ttu-id="96a15-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span><span class="sxs-lookup"><span data-stu-id="96a15-111">The [free trial](https://azure.microsoft.com/try/cognitive-services/?api=bing-custom-search) is sufficient for this quickstart.</span></span> <span data-ttu-id="96a15-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span><span class="sxs-lookup"><span data-stu-id="96a15-112">You need the access key provided when you activate your free trial, or you may use a paid subscription key from your Azure dashboard.</span></span>

## <a name="run-the-code"></a><span data-ttu-id="96a15-113">Run the code</span><span class="sxs-lookup"><span data-stu-id="96a15-113">Run the code</span></span>

<span data-ttu-id="96a15-114">To call the Bing Custom Search endpoint, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="96a15-114">To call the Bing Custom Search endpoint, follow these steps:</span></span>

1. <span data-ttu-id="96a15-115">Create a folder for your code.</span><span class="sxs-lookup"><span data-stu-id="96a15-115">Create a folder for your code.</span></span>

2. <span data-ttu-id="96a15-116">From a command prompt or terminal, navigate to the folder you just created.</span><span class="sxs-lookup"><span data-stu-id="96a15-116">From a command prompt or terminal, navigate to the folder you just created.</span></span>

3. <span data-ttu-id="96a15-117">Install the **request** node module:</span><span class="sxs-lookup"><span data-stu-id="96a15-117">Install the **request** node module:</span></span>
    <pre>
    npm install request
    </pre>
    
4. <span data-ttu-id="96a15-118">Create the file BingCustomSearch.js and copy the following code to it.</span><span class="sxs-lookup"><span data-stu-id="96a15-118">Create the file BingCustomSearch.js and copy the following code to it.</span></span>

5. <span data-ttu-id="96a15-119">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID (see step 1).</span><span class="sxs-lookup"><span data-stu-id="96a15-119">Replace **YOUR-SUBSCRIPTION-KEY** and **YOUR-CUSTOM-CONFIG-ID** with your key and configuration ID (see step 1).</span></span>

    ``` javascript
    var request = require("request");
    
    var subscriptionKey = 'YOUR-SUBSCRIPTION-KEY';
    var customConfigId = 'YOUR-CUSTOM-CONFIG-ID';
    var searchTerm = 'microsoft';
    
    var options = {
        url: 'https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search?' + 
          'q=' + searchTerm + 
          '&customconfig=' + customConfigId,
        headers: {
            'Ocp-Apim-Subscription-Key' : subscriptionKey
        }
    }
    
    request(options, function(error, response, body){
        var searchResponse = JSON.parse(body);
        for(var i = 0; i < searchResponse.webPages.value.length; ++i){
            var webPage = searchResponse.webPages.value[i];
            console.log('name: ' + webPage.name);
            console.log('url: ' + webPage.url);
            console.log('displayUrl: ' + webPage.displayUrl);
            console.log('snippet: ' + webPage.snippet);
            console.log('dateLastCrawled: ' + webPage.dateLastCrawled);
            console.log();
        }
    })
    ```
6. <span data-ttu-id="96a15-120">Run the code using the following command.</span><span class="sxs-lookup"><span data-stu-id="96a15-120">Run the code using the following command.</span></span>
    ```    
    node BingCustomSearch.js
   ``` 

## <a name="next-steps"></a><span data-ttu-id="96a15-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="96a15-121">Next steps</span></span>
- [<span data-ttu-id="96a15-122">Configure your hosted UI experience</span><span class="sxs-lookup"><span data-stu-id="96a15-122">Configure your hosted UI experience</span></span>](./hosted-ui.md)
- [<span data-ttu-id="96a15-123">Use decoration markers to highlight text</span><span class="sxs-lookup"><span data-stu-id="96a15-123">Use decoration markers to highlight text</span></span>](./hit-highlighting.md)
- [<span data-ttu-id="96a15-124">Page webpages</span><span class="sxs-lookup"><span data-stu-id="96a15-124">Page webpages</span></span>](./page-webpages.md)
