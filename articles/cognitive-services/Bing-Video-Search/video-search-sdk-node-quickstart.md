---
title: Video Search SDK Node quickstart | Microsoft Docs
description: Setup for Video Search SDK console application.
titleSuffix: Azure cognitive services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-video-search
ms.topic: article
ms.date: 02/12/2018
ms.author: v-gedod
ms.openlocfilehash: 5718c750288e0a5605db3296d2911cca5e03375c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865974"
---
# <a name="video-search-sdk-node-quickstart"></a><span data-ttu-id="078d5-103">Video Search SDK Node quickstart</span><span class="sxs-lookup"><span data-stu-id="078d5-103">Video Search SDK Node quickstart</span></span>

<span data-ttu-id="078d5-104">The Bing Video Search SDK contains the functionality of the REST API for video queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="078d5-104">The Bing Video Search SDK contains the functionality of the REST API for video queries and parsing results.</span></span> 

<span data-ttu-id="078d5-105">The [source code for Node Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/videoSearch.js) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="078d5-105">The [source code for Node Bing Video Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/videoSearch.js) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="078d5-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="078d5-106">Application dependencies</span></span>

<span data-ttu-id="078d5-107">To set up a console application using the Bing Video Search SDK, run `npm install azure-cognitiveservices-videosearch` in your development environment.</span><span class="sxs-lookup"><span data-stu-id="078d5-107">To set up a console application using the Bing Video Search SDK, run `npm install azure-cognitiveservices-videosearch` in your development environment.</span></span>

## <a name="video-search-client"></a><span data-ttu-id="078d5-108">Video Search client</span><span class="sxs-lookup"><span data-stu-id="078d5-108">Video Search client</span></span>
<span data-ttu-id="078d5-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="078d5-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="078d5-110">Create an instance of the `CognitiveServicesCredentials`:</span><span class="sxs-lookup"><span data-stu-id="078d5-110">Create an instance of the `CognitiveServicesCredentials`:</span></span>
```
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
```
<span data-ttu-id="078d5-111">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="078d5-111">Then, instantiate the client:</span></span>
```
const VideoSearchAPIClient = require('azure-cognitiveservices-videosearch');
let client = new VideoSearchAPIClient(credentials);
```
<span data-ttu-id="078d5-112">Search for results.</span><span class="sxs-lookup"><span data-stu-id="078d5-112">Search for results.</span></span>
```
client.videosOperations.search('Interstellar Trailer').then((result) => {
    console.log(result.value);
}).catch((err) => {
    throw err;
});

```

<!-- Remove until the response can be replace with a sanitized version.
The code prints `result.value` items to the console without parsing any text. The results will be:
- _type: 'VideoObjectElementType'

![Video results](media/video-search-sdk-node-results.png)
-->

## <a name="next-steps"></a><span data-ttu-id="078d5-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="078d5-113">Next steps</span></span>

[<span data-ttu-id="078d5-114">Cognitive services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="078d5-114">Cognitive services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)
