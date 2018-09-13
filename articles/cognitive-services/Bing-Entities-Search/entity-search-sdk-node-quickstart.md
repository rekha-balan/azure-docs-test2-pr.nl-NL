---
title: Entity search SDK Node quickstart | Microsoft Docs
description: Setup for Entity search SDK console application.
titleSuffix: Azure cognitive services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 02/12/2018
ms.author: v-gedod
ms.openlocfilehash: 2904ecfed33334458f9b6a9ca2500cd0bfef13bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857438"
---
# <a name="entity-search-sdk-node-quickstart"></a><span data-ttu-id="5ff64-103">Entity Search SDK Node quickstart</span><span class="sxs-lookup"><span data-stu-id="5ff64-103">Entity Search SDK Node quickstart</span></span>

<span data-ttu-id="5ff64-104">The Bing Entity Search SDK contains the functionality of the REST API for entity queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="5ff64-104">The Bing Entity Search SDK contains the functionality of the REST API for entity queries and parsing results.</span></span> 

<span data-ttu-id="5ff64-105">The [source code for C# Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/entitySearch.js) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="5ff64-105">The [source code for C# Bing Entity Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/entitySearch.js) is available on Git Hub.</span></span>
## <a name="application-dependencies"></a><span data-ttu-id="5ff64-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="5ff64-106">Application dependencies</span></span>

<span data-ttu-id="5ff64-107">To set up a console application using the Bing Entity Search SDK, run `npm install azure-cognitiveservices-entitysearch` in your development environment.</span><span class="sxs-lookup"><span data-stu-id="5ff64-107">To set up a console application using the Bing Entity Search SDK, run `npm install azure-cognitiveservices-entitysearch` in your development environment.</span></span>

## <a name="entity-search-client"></a><span data-ttu-id="5ff64-108">Entity Search client</span><span class="sxs-lookup"><span data-stu-id="5ff64-108">Entity Search client</span></span>
<span data-ttu-id="5ff64-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="5ff64-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="5ff64-110">Create an instance of the `CognitiveServicesCredentials`:</span><span class="sxs-lookup"><span data-stu-id="5ff64-110">Create an instance of the `CognitiveServicesCredentials`:</span></span>
```
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
```
<span data-ttu-id="5ff64-111">Then, instantiate the client, and search for results:</span><span class="sxs-lookup"><span data-stu-id="5ff64-111">Then, instantiate the client, and search for results:</span></span>
```
const EntitySearchAPIClient = require('azure-cognitiveservices-entitysearch');

let entitySearchApiClient = new EntitySearchAPIClient(credentials);

entitySearchApiClient.entitiesOperations.search('seahawks').then((result) => {
    console.log(result.queryContext);
    console.log(result.entities.value);
    console.log(result.entities.value[0].description);
}).catch((err) => {
    throw err;
});

```
<span data-ttu-id="5ff64-112">The code prints `result.value` items to the console without parsing any text.</span><span class="sxs-lookup"><span data-stu-id="5ff64-112">The code prints `result.value` items to the console without parsing any text.</span></span>  <span data-ttu-id="5ff64-113">The results, if any per category, will include:</span><span class="sxs-lookup"><span data-stu-id="5ff64-113">The results, if any per category, will include:</span></span>
- <span data-ttu-id="5ff64-114">_type: 'Thing'</span><span class="sxs-lookup"><span data-stu-id="5ff64-114">_type: 'Thing'</span></span>
- <span data-ttu-id="5ff64-115">_type: 'ImageObject'</span><span class="sxs-lookup"><span data-stu-id="5ff64-115">_type: 'ImageObject'</span></span>

<!-- Removing until we can replace with a sanitized version.
![Entity results](media/entity-search-sdk-node-quickstart-results.png)
-->

## <a name="next-steps"></a><span data-ttu-id="5ff64-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ff64-116">Next steps</span></span>

[<span data-ttu-id="5ff64-117">Cognitive services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="5ff64-117">Cognitive services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)