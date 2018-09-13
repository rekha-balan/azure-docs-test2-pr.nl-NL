---
title: Bing Web Search SDK samples
titleSuffix: Microsoft Cognitive Services
description: Use the Bing Web Search SDK to add search capabilities to your Python, Node.js, C#, or Java application.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.assetid: ''
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 08/16/2018
ms.author: erhopf
ms.openlocfilehash: 0f82d40611dde69eb8ab63f49d6fd337e34cb8cc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857108"
---
# <a name="bing-web-search-sdk-samples"></a><span data-ttu-id="93df8-103">Bing Web Search SDK samples</span><span class="sxs-lookup"><span data-stu-id="93df8-103">Bing Web Search SDK samples</span></span>

<span data-ttu-id="93df8-104">The Bing Web Search SDK is available in Python, Node.js, C#, and Java.</span><span class="sxs-lookup"><span data-stu-id="93df8-104">The Bing Web Search SDK is available in Python, Node.js, C#, and Java.</span></span> <span data-ttu-id="93df8-105">Code samples, prerequisites, and build instructions are provided on GitHub.</span><span class="sxs-lookup"><span data-stu-id="93df8-105">Code samples, prerequisites, and build instructions are provided on GitHub.</span></span> <span data-ttu-id="93df8-106">The following scenarios are covered:</span><span class="sxs-lookup"><span data-stu-id="93df8-106">The following scenarios are covered:</span></span>

* <span data-ttu-id="93df8-107">Query a single word and print the name and URL of the first result for web pages, images, news articles, and videos.</span><span class="sxs-lookup"><span data-stu-id="93df8-107">Query a single word and print the name and URL of the first result for web pages, images, news articles, and videos.</span></span>
* <span data-ttu-id="93df8-108">Query a phrase, verify the number of results, and print out the name and URL of first result.</span><span class="sxs-lookup"><span data-stu-id="93df8-108">Query a phrase, verify the number of results, and print out the name and URL of first result.</span></span>
* <span data-ttu-id="93df8-109">Query a search term with response filters set to `news` and print the details of news results.</span><span class="sxs-lookup"><span data-stu-id="93df8-109">Query a search term with response filters set to `news` and print the details of news results.</span></span>
* <span data-ttu-id="93df8-110">Query a search term with `answerCount` and `promote` parameters, then print details of results.</span><span class="sxs-lookup"><span data-stu-id="93df8-110">Query a search term with `answerCount` and `promote` parameters, then print details of results.</span></span>

## <a name="sdks-and-libraries"></a><span data-ttu-id="93df8-111">SDKs and libraries</span><span class="sxs-lookup"><span data-stu-id="93df8-111">SDKs and libraries</span></span>

<span data-ttu-id="93df8-112">Use these links to access the SDK for your preferred language.</span><span class="sxs-lookup"><span data-stu-id="93df8-112">Use these links to access the SDK for your preferred language.</span></span>

* <span data-ttu-id="93df8-113">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="93df8-113">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span></span>
  * <span data-ttu-id="93df8-114">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-websearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="93df8-114">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-websearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="93df8-115">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="93df8-115">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span></span>
  * <span data-ttu-id="93df8-116">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/webSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="93df8-116">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/webSearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="93df8-117">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span><span class="sxs-lookup"><span data-stu-id="93df8-117">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span></span>
  * [<span data-ttu-id="93df8-118">NuGet package</span><span class="sxs-lookup"><span data-stu-id="93df8-118">NuGet package</span></span>](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.WebSearch/1.2.0)
  * <span data-ttu-id="93df8-119">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingWebSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="93df8-119">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingWebSearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="93df8-120">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="93df8-120">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span></span>
  * <span data-ttu-id="93df8-121">See also [Java libraries](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingWebSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="93df8-121">See also [Java libraries](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingWebSearch) for definitions and dependencies.</span></span>