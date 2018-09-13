---
title: 'Quickstart: Request and filter images using the SDK in Node.js'
description: In this quickstart, you request and filter the images returned by Bing Image Search, using Node.js.
titleSuffix: Azure cognitive services
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 02/12/2018
ms.author: v-gedod
ms.openlocfilehash: e88c045b220192a617e6b8caf5d8d53f70a25b5e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967467"
---
# <a name="quickstart-request-and-filter-images-using-the-sdk-and-nodejs"></a><span data-ttu-id="28788-103">Quickstart: Request and filter images using the SDK and Node.js</span><span class="sxs-lookup"><span data-stu-id="28788-103">Quickstart: Request and filter images using the SDK and Node.js</span></span>

<span data-ttu-id="28788-104">The Bing Image Search SDK contains the functionality of the REST API for image queries and parsing results.</span><span class="sxs-lookup"><span data-stu-id="28788-104">The Bing Image Search SDK contains the functionality of the REST API for image queries and parsing results.</span></span> 

<span data-ttu-id="28788-105">The [source code for Node Bing Image Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/imageSearch.js) is available on Git Hub.</span><span class="sxs-lookup"><span data-stu-id="28788-105">The [source code for Node Bing Image Search SDK samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples/blob/master/Samples/imageSearch.js) is available on Git Hub.</span></span>

## <a name="application-dependencies"></a><span data-ttu-id="28788-106">Application dependencies</span><span class="sxs-lookup"><span data-stu-id="28788-106">Application dependencies</span></span>

<span data-ttu-id="28788-107">To set up a console application using the Bing Image Search SDK, run `npm install azure-cognitiveservices-imagesearch` in your development environment.</span><span class="sxs-lookup"><span data-stu-id="28788-107">To set up a console application using the Bing Image Search SDK, run `npm install azure-cognitiveservices-imagesearch` in your development environment.</span></span>

## <a name="image-search-client"></a><span data-ttu-id="28788-108">Image Search client</span><span class="sxs-lookup"><span data-stu-id="28788-108">Image Search client</span></span>
<span data-ttu-id="28788-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span><span class="sxs-lookup"><span data-stu-id="28788-109">Get a [Cognitive Services access key](https://azure.microsoft.com/try/cognitive-services/) under *Search*.</span></span> <span data-ttu-id="28788-110">Create an instance of the `CognitiveServicesCredentials`:</span><span class="sxs-lookup"><span data-stu-id="28788-110">Create an instance of the `CognitiveServicesCredentials`:</span></span>
```
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
```
<span data-ttu-id="28788-111">Then, instantiate the client:</span><span class="sxs-lookup"><span data-stu-id="28788-111">Then, instantiate the client:</span></span>
```
const ImageSearchAPIClient = require('azure-cognitiveservices-imagesearch');
let client = new ImageSearchAPIClient(credentials);
```
<span data-ttu-id="28788-112">Use the client to search with a query text, in this case 'El Capitan':</span><span class="sxs-lookup"><span data-stu-id="28788-112">Use the client to search with a query text, in this case 'El Capitan':</span></span>
```
client.imagesOperations.search('El Capitan', function (err, result, request, response) {
    if (err) throw err;
    console.log(result.value);
});

```
<!-- Need to sanitize result
The code prints `result.value` items to the console without parsing any text. The results will be:
- _type: 'ImageObjectElementType'

![Imageresults](media/node-sdk-quickstart-image-results.png)
-->

## <a name="next-steps"></a><span data-ttu-id="28788-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="28788-113">Next steps</span></span>

[<span data-ttu-id="28788-114">Cognitive services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="28788-114">Cognitive services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)