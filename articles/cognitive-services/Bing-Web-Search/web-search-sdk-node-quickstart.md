---
title: 'Quickstart: Use the Bing Web Search SDK for Node.js'
description: Learn to use the Bing Web Search SDK for Node.js.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: quickstart
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: 7c3003ab4ba40a9d0212e7c94b6dd3bfbc8f0ca2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869013"
---
# <a name="quickstart-use-the-bing-web-search-sdk-for-nodejs"></a><span data-ttu-id="bfff4-103">Quickstart: Use the Bing Web Search SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="bfff4-103">Quickstart: Use the Bing Web Search SDK for Node.js</span></span>

<span data-ttu-id="bfff4-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="bfff4-104">The Bing Web Search SDK makes it easy to integrate Bing Web Search into your Node.js application.</span></span> <span data-ttu-id="bfff4-105">In this quickstart, you'll learn how to instantiate a client, send a request, and print the response.</span><span class="sxs-lookup"><span data-stu-id="bfff4-105">In this quickstart, you'll learn how to instantiate a client, send a request, and print the response.</span></span>

<span data-ttu-id="bfff4-106">Want to see the code right now?</span><span class="sxs-lookup"><span data-stu-id="bfff4-106">Want to see the code right now?</span></span> <span data-ttu-id="bfff4-107">The [Bing Web Search SDK for Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples) are available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="bfff4-107">The [Bing Web Search SDK for Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples) are available on GitHub.</span></span>

[!INCLUDE [bing-web-search-quickstart-signup](../../../includes/bing-web-search-quickstart-signup.md)]

## <a name="prerequisites"></a><span data-ttu-id="bfff4-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bfff4-108">Prerequisites</span></span>

<span data-ttu-id="bfff4-109">Here are a few things that you'll need before running this quickstart:</span><span class="sxs-lookup"><span data-stu-id="bfff4-109">Here are a few things that you'll need before running this quickstart:</span></span>

* <span data-ttu-id="bfff4-110">[Node.js 6](https://nodejs.org/en/download/) or later</span><span class="sxs-lookup"><span data-stu-id="bfff4-110">[Node.js 6](https://nodejs.org/en/download/) or later</span></span>
* <span data-ttu-id="bfff4-111">A subscription key</span><span class="sxs-lookup"><span data-stu-id="bfff4-111">A subscription key</span></span>  

## <a name="set-up-your-development-environment"></a><span data-ttu-id="bfff4-112">Set up your development environment</span><span class="sxs-lookup"><span data-stu-id="bfff4-112">Set up your development environment</span></span>

<span data-ttu-id="bfff4-113">Let's start by setting up the development environment for our Node.js project.</span><span class="sxs-lookup"><span data-stu-id="bfff4-113">Let's start by setting up the development environment for our Node.js project.</span></span>

1. <span data-ttu-id="bfff4-114">Create a new directory for your project:</span><span class="sxs-lookup"><span data-stu-id="bfff4-114">Create a new directory for your project:</span></span>

    ```console
    mkdir YOUR_PROJECT
    ```

2. <span data-ttu-id="bfff4-115">Create a new package file:</span><span class="sxs-lookup"><span data-stu-id="bfff4-115">Create a new package file:</span></span>

    ```console
    cd YOUR_PROJECT
    npm init
    ```

3. <span data-ttu-id="bfff4-116">Now, let's install some azure modules and add them to the `package.json`:</span><span class="sxs-lookup"><span data-stu-id="bfff4-116">Now, let's install some azure modules and add them to the `package.json`:</span></span>

    ```console
    npm install --save azure-cognitiveservices-websearch
    npm install --save ms-rest-azure
    ```

## <a name="create-a-project-and-declare-required-modules"></a><span data-ttu-id="bfff4-117">Create a project and declare required modules</span><span class="sxs-lookup"><span data-stu-id="bfff4-117">Create a project and declare required modules</span></span>

<span data-ttu-id="bfff4-118">In the same directory as your `package.json`, create a new Node.js project using your favorite IDE or editor.</span><span class="sxs-lookup"><span data-stu-id="bfff4-118">In the same directory as your `package.json`, create a new Node.js project using your favorite IDE or editor.</span></span> <span data-ttu-id="bfff4-119">For example: `sample.js`.</span><span class="sxs-lookup"><span data-stu-id="bfff4-119">For example: `sample.js`.</span></span>

<span data-ttu-id="bfff4-120">Next, copy this code into your project.</span><span class="sxs-lookup"><span data-stu-id="bfff4-120">Next, copy this code into your project.</span></span> <span data-ttu-id="bfff4-121">It loads the modules installed in the previous section.</span><span class="sxs-lookup"><span data-stu-id="bfff4-121">It loads the modules installed in the previous section.</span></span>

```javascript
const CognitiveServicesCredentials = require('ms-rest-azure').CognitiveServicesCredentials;
const WebSearchAPIClient = require('azure-cognitiveservices-websearch');
```

## <a name="instantiate-the-client"></a><span data-ttu-id="bfff4-122">Instantiate the client</span><span class="sxs-lookup"><span data-stu-id="bfff4-122">Instantiate the client</span></span>

<span data-ttu-id="bfff4-123">This code instantiates a client and using the `azure-cognitiveservices-websearch` module.</span><span class="sxs-lookup"><span data-stu-id="bfff4-123">This code instantiates a client and using the `azure-cognitiveservices-websearch` module.</span></span> <span data-ttu-id="bfff4-124">Make sure that you enter a valid subscription key for your Azure account before continuing.</span><span class="sxs-lookup"><span data-stu-id="bfff4-124">Make sure that you enter a valid subscription key for your Azure account before continuing.</span></span>

```javascript
let credentials = new CognitiveServicesCredentials('YOUR-ACCESS-KEY');
let webSearchApiClient = new WebSearchAPIClient(credentials);
```

## <a name="make-a-request-and-print-the-results"></a><span data-ttu-id="bfff4-125">Make a request and print the results</span><span class="sxs-lookup"><span data-stu-id="bfff4-125">Make a request and print the results</span></span>

<span data-ttu-id="bfff4-126">Use the client to send a search query to Bing Web Search.</span><span class="sxs-lookup"><span data-stu-id="bfff4-126">Use the client to send a search query to Bing Web Search.</span></span> <span data-ttu-id="bfff4-127">If the response includes results for any of the items in the `properties` array, the `result.value` is printed to console.</span><span class="sxs-lookup"><span data-stu-id="bfff4-127">If the response includes results for any of the items in the `properties` array, the `result.value` is printed to console.</span></span>

```javascript
webSearchApiClient.web.search('seahawks').then((result) => {
    let properties = ["images", "webPages", "news", "videos"];
    for (let i = 0; i < properties.length; i++) {
        if (result[properties[i]]) {
            console.log(result[properties[i]].value);
        } else {
            console.log(`No ${properties[i]} data`);
        }
    }
}).catch((err) => {
    throw err;
})
```

## <a name="run-the-program"></a><span data-ttu-id="bfff4-128">Run the program</span><span class="sxs-lookup"><span data-stu-id="bfff4-128">Run the program</span></span>

<span data-ttu-id="bfff4-129">The final step is to run your program!</span><span class="sxs-lookup"><span data-stu-id="bfff4-129">The final step is to run your program!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="bfff4-130">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bfff4-130">Clean up resources</span></span>

<span data-ttu-id="bfff4-131">When you're done with this project, make sure to remove your subscription key from the program's code.</span><span class="sxs-lookup"><span data-stu-id="bfff4-131">When you're done with this project, make sure to remove your subscription key from the program's code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfff4-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfff4-132">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfff4-133">Cognitive Services Node.js SDK samples</span><span class="sxs-lookup"><span data-stu-id="bfff4-133">Cognitive Services Node.js SDK samples</span></span>](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)

## <a name="see-also"></a><span data-ttu-id="bfff4-134">See also</span><span class="sxs-lookup"><span data-stu-id="bfff4-134">See also</span></span>

* [<span data-ttu-id="bfff4-135">Azure Node SDK reference</span><span class="sxs-lookup"><span data-stu-id="bfff4-135">Azure Node SDK reference</span></span>](https://docs.microsoft.com/javascript/api/azure-cognitiveservices-websearch/)
