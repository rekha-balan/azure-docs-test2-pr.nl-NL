---
title: Using ranking to display answers | Microsoft Docs
description: Shows how to use ranking to display the answers that the Bing Entity Search API returns.
services: cognitive-services
author: v-jerkin
manager: ehansen
ms.assetid: BBF87972-B6C3-4910-BB52-DE90893F6C71
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 12/12/2017
ms.author: v-jerkin
ms.openlocfilehash: 6ec325d99404cc4eca31cf36db8b739a61aec3ca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870944"
---
# <a name="using-ranking-to-display-results"></a><span data-ttu-id="f65c8-103">Using ranking to display results</span><span class="sxs-lookup"><span data-stu-id="f65c8-103">Using ranking to display results</span></span>  

<span data-ttu-id="f65c8-104">Each entity search response includes a [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse) answer, similar to the one in a Bing Web Search response, that specifies how you must display the search results.</span><span class="sxs-lookup"><span data-stu-id="f65c8-104">Each entity search response includes a [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse) answer, similar to the one in a Bing Web Search response, that specifies how you must display the search results.</span></span> <span data-ttu-id="f65c8-105">The ranking response groups results into pole, mainline, and sidebar content.</span><span class="sxs-lookup"><span data-stu-id="f65c8-105">The ranking response groups results into pole, mainline, and sidebar content.</span></span> <span data-ttu-id="f65c8-106">The pole result is the most important or prominent result and should be displayed first.</span><span class="sxs-lookup"><span data-stu-id="f65c8-106">The pole result is the most important or prominent result and should be displayed first.</span></span> <span data-ttu-id="f65c8-107">If you do not display the remaining results in a traditional mainline and sidebar format, you must provide the mainline content higher visibility than the sidebar content.</span><span class="sxs-lookup"><span data-stu-id="f65c8-107">If you do not display the remaining results in a traditional mainline and sidebar format, you must provide the mainline content higher visibility than the sidebar content.</span></span> 
  
<span data-ttu-id="f65c8-108">Within each group, the [Items](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankinggroup-items) array identifies the order that the content must appear in.</span><span class="sxs-lookup"><span data-stu-id="f65c8-108">Within each group, the [Items](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankinggroup-items) array identifies the order that the content must appear in.</span></span> <span data-ttu-id="f65c8-109">Each item provides two ways to identify the result within an answer.</span><span class="sxs-lookup"><span data-stu-id="f65c8-109">Each item provides two ways to identify the result within an answer.</span></span>  
  
-   <span data-ttu-id="f65c8-110">`answerType` and `resultIndex` — The `answerType` field identifies the answer (either Entity or Place) and `resultIndex` identifies a result within the answer (for example, an entity).</span><span class="sxs-lookup"><span data-stu-id="f65c8-110">`answerType` and `resultIndex` — The `answerType` field identifies the answer (either Entity or Place) and `resultIndex` identifies a result within the answer (for example, an entity).</span></span> <span data-ttu-id="f65c8-111">The index is zero based.</span><span class="sxs-lookup"><span data-stu-id="f65c8-111">The index is zero based.</span></span>  
  
-   <span data-ttu-id="f65c8-112">`value` — The `value` field contains an ID that matches the ID of either an answer or a result within the answer.</span><span class="sxs-lookup"><span data-stu-id="f65c8-112">`value` — The `value` field contains an ID that matches the ID of either an answer or a result within the answer.</span></span> <span data-ttu-id="f65c8-113">Either the answer or the results contain the ID but not both.</span><span class="sxs-lookup"><span data-stu-id="f65c8-113">Either the answer or the results contain the ID but not both.</span></span>  
  
<span data-ttu-id="f65c8-114">Using the ID requires you to match the ranking ID with the ID of an answer or one of its results.</span><span class="sxs-lookup"><span data-stu-id="f65c8-114">Using the ID requires you to match the ranking ID with the ID of an answer or one of its results.</span></span> <span data-ttu-id="f65c8-115">If an answer object includes an `id` field, display all the answer's results together.</span><span class="sxs-lookup"><span data-stu-id="f65c8-115">If an answer object includes an `id` field, display all the answer's results together.</span></span> <span data-ttu-id="f65c8-116">For example, if the `Entities` object includes the `id` field, display all the entities articles together.</span><span class="sxs-lookup"><span data-stu-id="f65c8-116">For example, if the `Entities` object includes the `id` field, display all the entities articles together.</span></span> <span data-ttu-id="f65c8-117">If the `Entities` object does not include the `id` field, then each entity contains an `id` field and the ranking response mixes the entities with the Places results.</span><span class="sxs-lookup"><span data-stu-id="f65c8-117">If the `Entities` object does not include the `id` field, then each entity contains an `id` field and the ranking response mixes the entities with the Places results.</span></span>  
  
<span data-ttu-id="f65c8-118">Using the `answerType` and `resultIndex` is a two-step process.</span><span class="sxs-lookup"><span data-stu-id="f65c8-118">Using the `answerType` and `resultIndex` is a two-step process.</span></span> <span data-ttu-id="f65c8-119">First, you use `answerType` to identify the answer that contains the results to display.</span><span class="sxs-lookup"><span data-stu-id="f65c8-119">First, you use `answerType` to identify the answer that contains the results to display.</span></span> <span data-ttu-id="f65c8-120">Then you use `resultIndex` to index into that answer's results to get the result to display.</span><span class="sxs-lookup"><span data-stu-id="f65c8-120">Then you use `resultIndex` to index into that answer's results to get the result to display.</span></span> <span data-ttu-id="f65c8-121">(The `answerType` value is the name of the field in the [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object.) If you're supposed to display all the answer's results together, the ranking response item doesn't include the `resultIndex` field.</span><span class="sxs-lookup"><span data-stu-id="f65c8-121">(The `answerType` value is the name of the field in the [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object.) If you're supposed to display all the answer's results together, the ranking response item doesn't include the `resultIndex` field.</span></span>

## <a name="ranking-response-example"></a><span data-ttu-id="f65c8-122">Ranking response example</span><span class="sxs-lookup"><span data-stu-id="f65c8-122">Ranking response example</span></span>

<span data-ttu-id="f65c8-123">The following shows an example [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse).</span><span class="sxs-lookup"><span data-stu-id="f65c8-123">The following shows an example [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse).</span></span>
  
```json
{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "Jimi Hendrix"
  },
  "entities": { ... },
  "rankingResponse": {
    "sidebar": {
      "items": [
        {
          "answerType": "Entities",
          "resultIndex": 0,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#Entities.0"
          }
        },
        {
          "answerType": "Entities",
          "resultIndex": 1,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#Entities.1"
          }
        }
      ]
    }
  }
}
```

<span data-ttu-id="f65c8-124">Based on this ranking response, the sidebar would display the two entity results related to Jimi Hendrix.</span><span class="sxs-lookup"><span data-stu-id="f65c8-124">Based on this ranking response, the sidebar would display the two entity results related to Jimi Hendrix.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f65c8-125">Next steps</span><span class="sxs-lookup"><span data-stu-id="f65c8-125">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f65c8-126">Bing Entity Search tutorial</span><span class="sxs-lookup"><span data-stu-id="f65c8-126">Bing Entity Search tutorial</span></span>](tutorial-bing-entities-search-single-page-app.md)
