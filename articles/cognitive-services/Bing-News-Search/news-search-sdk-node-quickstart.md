---
title: News Search SDK Node quickstart | Microsoft Docs
description: Set up the News Search SDK console application
titleSuffix: Azure cognitive services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 02/12/2018
ms.author: v-gedod
ms.openlocfilehash: 4ae99aa100b697a0dd75863c6f0c3c556dfa3d21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966125"
---
# <a name="news-search-sdk-node-quickstart"></a><span data-ttu-id="120cd-103">News Search SDK Node quickstart</span><span class="sxs-lookup"><span data-stu-id="120cd-103">News Search SDK Node quickstart</span></span>

<span data-ttu-id="120cd-104">The Bing News Search SDK contains the functionality of the REST API for news queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="120cd-104">The Bing News Search SDK contains the functionality of the REST API for news queries and parsing results.</span></span> 

<span data-ttu-id="120cd-105">The [source code for Node Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/newsSearch.js) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="120cd-105">The [source code for Node Bing News Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/newsSearch.js) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="120cd-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="120cd-106">Application dependencies</span></span>

<span data-ttu-id="120cd-107">To set up a console application using the Bing News Search SDK, run `npm install azure-cognitiveservices-newssearch` in your development environment.</span><span class="sxs-lookup"><span data-stu-id="120cd-107">To set up a console application using the Bing News Search SDK, run `npm install azure-cognitiveservices-newssearch` in your development environment.</span></span>

## <a name="news-search-client"></a><span data-ttu-id="120cd-108">News Search client</span><span class="sxs-lookup"><span data-stu-id="120cd-108">News Search client</span></span>
<span data-ttu-id="120cd-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="120cd-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="120cd-110">Create an instance of the `CognitiveServicesCredentials`:</span><span class="sxs-lookup"><span data-stu-id="120cd-110">Create an instance of the `CognitiveServicesCredentials`:</span></span>
```
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
```
<span data-ttu-id="120cd-111">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="120cd-111">Then, instantiate the client:</span></span>
```
const NewsSearchAPIClient = require('azure-cognitiveservices-newssearch');
let client = new NewsSearchAPIClient(credentials);
```
<span data-ttu-id="120cd-112">Use the client to search with a query text, in this case 'Winter Olympics':</span><span class="sxs-lookup"><span data-stu-id="120cd-112">Use the client to search with a query text, in this case 'Winter Olympics':</span></span>
```
client.newsOperations.search('Winter Olympics').then((result) => {
    console.log(result.value);
}).catch((err) => {
    throw err;
});

```
<span data-ttu-id="120cd-113">The code prints `result.value` items to the console without parsing any text.</span><span class="sxs-lookup"><span data-stu-id="120cd-113">The code prints `result.value` items to the console without parsing any text.</span></span> <span data-ttu-id="120cd-114">The results, if any per category, will include:</span><span class="sxs-lookup"><span data-stu-id="120cd-114">The results, if any per category, will include:</span></span>
- <span data-ttu-id="120cd-115">_type: 'NewsArticle'</span><span class="sxs-lookup"><span data-stu-id="120cd-115">_type: 'NewsArticle'</span></span>
- <span data-ttu-id="120cd-116">_type: 'WebPage'</span><span class="sxs-lookup"><span data-stu-id="120cd-116">_type: 'WebPage'</span></span>
- <span data-ttu-id="120cd-117">_type: 'VideoObject'</span><span class="sxs-lookup"><span data-stu-id="120cd-117">_type: 'VideoObject'</span></span>
- <span data-ttu-id="120cd-118">_type: 'ImageObject'</span><span class="sxs-lookup"><span data-stu-id="120cd-118">_type: 'ImageObject'</span></span>

<!-- Remove until we can replace with santized version
![News results](media/node-sdk-quickstart-results.png)
-->

## <a name="next-steps"></a><span data-ttu-id="120cd-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="120cd-119">Next steps</span></span>

[<span data-ttu-id="120cd-120">Cognitive services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="120cd-120">Cognitive services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)
