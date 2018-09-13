---
title: Bing Search SDK | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Bing Search SDK for applications that search the web.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.assetid: ''
ms.service: cognitive-services
ms.component: bing-news-search
ms.topic: article
ms.date: 1/24/2018
ms.author: v-gedod
ms.openlocfilehash: 4a40ea665e153536d2322706b455598902ce41eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857105"
---
# <a name="bing-search-sdk"></a><span data-ttu-id="2002b-103">Bing Search SDK</span><span class="sxs-lookup"><span data-stu-id="2002b-103">Bing Search SDK</span></span>
<span data-ttu-id="2002b-104">The Bing News Search API samples include scenarios that:</span><span class="sxs-lookup"><span data-stu-id="2002b-104">The Bing News Search API samples include scenarios that:</span></span>
1. <span data-ttu-id="2002b-105">Query news for search terms with `market` and `count` parameters, verify number of results, and print out `totalEstimatedMatches`, name, URL, description, published time, and name of provider of the first news result.</span><span class="sxs-lookup"><span data-stu-id="2002b-105">Query news for search terms with `market` and `count` parameters, verify number of results, and print out `totalEstimatedMatches`, name, URL, description, published time, and name of provider of the first news result.</span></span>
2. <span data-ttu-id="2002b-106">Query most recent news for search terms with `freshness` and `sortBy` parameters, verify number of results, and print out `totalEstimatedMatches`, URL, description, published time and name of provider of the first news result.</span><span class="sxs-lookup"><span data-stu-id="2002b-106">Query most recent news for search terms with `freshness` and `sortBy` parameters, verify number of results, and print out `totalEstimatedMatches`, URL, description, published time and name of provider of the first news result.</span></span>
3. <span data-ttu-id="2002b-107">Query category news for `movie` and `TV entertainment` with safe search, verify number of results, and print out category, name, URL, description, published time and name of provider of the first news result.</span><span class="sxs-lookup"><span data-stu-id="2002b-107">Query category news for `movie` and `TV entertainment` with safe search, verify number of results, and print out category, name, URL, description, published time and name of provider of the first news result.</span></span>
4. <span data-ttu-id="2002b-108">Query news trending topics in Bing, verify number of results and print out name, text of query, `webSearchUrl`, `newsSearchUrl` and image URL of the first news result.</span><span class="sxs-lookup"><span data-stu-id="2002b-108">Query news trending topics in Bing, verify number of results and print out name, text of query, `webSearchUrl`, `newsSearchUrl` and image URL of the first news result.</span></span>

<span data-ttu-id="2002b-109">The Bing Search SDKs make web search functionality readily accessible in the following programming languages:</span><span class="sxs-lookup"><span data-stu-id="2002b-109">The Bing Search SDKs make web search functionality readily accessible in the following programming languages:</span></span>
* <span data-ttu-id="2002b-110">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span><span class="sxs-lookup"><span data-stu-id="2002b-110">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span></span>
    * [<span data-ttu-id="2002b-111">NuGet package</span><span class="sxs-lookup"><span data-stu-id="2002b-111">NuGet package</span></span>](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.NewsSearch/1.2.0)
    * <span data-ttu-id="2002b-112">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingNewsSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="2002b-112">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingNewsSearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="2002b-113">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="2002b-113">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span></span> 
    * <span data-ttu-id="2002b-114">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/newsSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="2002b-114">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/newsSearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="2002b-115">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="2002b-115">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span></span> 
    * <span data-ttu-id="2002b-116">See also [Java libraries](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingNewsSearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="2002b-116">See also [Java libraries](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples/tree/master/Search/BingNewsSearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="2002b-117">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="2002b-117">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span></span> 
    * <span data-ttu-id="2002b-118">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-newssearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="2002b-118">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-newssearch) for definitions and dependencies.</span></span>

<span data-ttu-id="2002b-119">SDK samples for each language include a ReadMe file with details about prerequisites and installing/running the samples.</span><span class="sxs-lookup"><span data-stu-id="2002b-119">SDK samples for each language include a ReadMe file with details about prerequisites and installing/running the samples.</span></span>