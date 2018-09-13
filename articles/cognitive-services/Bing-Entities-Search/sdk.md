---
title: Bing Search SDK | Microsoft Docs
titleSuffix: Microsoft Cognitive Services
description: Bing Search SDK for applications that search the web.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.assetid: ''
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 1/24/2018
ms.author: v-gedod
ms.openlocfilehash: 41e4880eec0df16ee012226389d0c054baa7bd4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869115"
---
# <a name="bing-search-sdk"></a><span data-ttu-id="5bcb5-103">Bing Search SDK</span><span class="sxs-lookup"><span data-stu-id="5bcb5-103">Bing Search SDK</span></span>
<span data-ttu-id="5bcb5-104">The Bing Entity Search API samples include scenarios that:</span><span class="sxs-lookup"><span data-stu-id="5bcb5-104">The Bing Entity Search API samples include scenarios that:</span></span>
1.  <span data-ttu-id="5bcb5-105">Search for entity such as Tom Cruise and get rich information.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-105">Search for entity such as Tom Cruise and get rich information.</span></span>
2.  <span data-ttu-id="5bcb5-106">Handle disambiguation of terms for queries with possibly multiple intents.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-106">Handle disambiguation of terms for queries with possibly multiple intents.</span></span>
3.  <span data-ttu-id="5bcb5-107">Search for a local entity such as a restaurant and get rich information around it.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-107">Search for a local entity such as a restaurant and get rich information around it.</span></span>
4.  <span data-ttu-id="5bcb5-108">Search for local businesses such as restaurants and get rich information.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-108">Search for local businesses such as restaurants and get rich information.</span></span>
5.  <span data-ttu-id="5bcb5-109">Trigger a bad request and error handling.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-109">Trigger a bad request and error handling.</span></span>

> [!NOTE] 
> <span data-ttu-id="5bcb5-110">Some SDKs are now in GA and changes to documentation are pending.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-110">Some SDKs are now in GA and changes to documentation are pending.</span></span> 

<span data-ttu-id="5bcb5-111">The Bing Search SDKs make web search functionality readily accessible in the following programming languages:</span><span class="sxs-lookup"><span data-stu-id="5bcb5-111">The Bing Search SDKs make web search functionality readily accessible in the following programming languages:</span></span>
* <span data-ttu-id="5bcb5-112">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span><span class="sxs-lookup"><span data-stu-id="5bcb5-112">Get started with [.NET samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/BingSearchv7)</span></span> 
    * [<span data-ttu-id="5bcb5-113">NuGet package</span><span class="sxs-lookup"><span data-stu-id="5bcb5-113">NuGet package</span></span>](https://www.nuget.org/packages/Microsoft.Azure.CognitiveServices.Search.EntitySearch/1.2.0)
    * <span data-ttu-id="5bcb5-114">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingEntitySearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-114">See also [.NET libraries](https://github.com/Azure/azure-sdk-for-net/tree/psSdkJson6/src/SDKs/CognitiveServices/dataPlane/Search/BingEntitySearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="5bcb5-115">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="5bcb5-115">Get started with [Node.js samples](https://github.com/Azure-Samples/cognitive-services-node-sdk-samples)</span></span> 
    * <span data-ttu-id="5bcb5-116">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/entitySearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-116">See also [Node.js libraries](https://github.com/Azure/azure-sdk-for-node/tree/master/lib/services/entitySearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="5bcb5-117">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="5bcb5-117">Get started with [Java samples](https://github.com/Azure-Samples/cognitive-services-java-sdk-samples)</span></span> 
    * <span data-ttu-id="5bcb5-118">See also [Java libraries](https://github.com/Azure/azure-sdk-for-java/tree/master/azure-cognitiveservices/search/bingentitysearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-118">See also [Java libraries](https://github.com/Azure/azure-sdk-for-java/tree/master/azure-cognitiveservices/search/bingentitysearch) for definitions and dependencies.</span></span>
* <span data-ttu-id="5bcb5-119">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span><span class="sxs-lookup"><span data-stu-id="5bcb5-119">Get started with [Python samples](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)</span></span> 
    * <span data-ttu-id="5bcb5-120">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-entitysearch) for definitions and dependencies.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-120">See also [Python libraries](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-cognitiveservices-search-entitysearch) for definitions and dependencies.</span></span>

<span data-ttu-id="5bcb5-121">SDK samples for each language include a ReadMe file with details about prerequisites and installing/running the samples.</span><span class="sxs-lookup"><span data-stu-id="5bcb5-121">SDK samples for each language include a ReadMe file with details about prerequisites and installing/running the samples.</span></span>
