---
title: Using ranking to display the web answers | Microsoft Docs
description: Shows how to use ranking to display the answers that the Bing Web Search API returns.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: BBF87972-B6C3-4910-BB52-DE90893F6C71
ms.service: cognitive-services
ms.component: bing-web-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 750146f3bb28b94594a71733b68f092880360c5a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867115"
---
# <a name="using-ranking-to-display-results"></a><span data-ttu-id="6301e-103">Using ranking to display results</span><span class="sxs-lookup"><span data-stu-id="6301e-103">Using ranking to display results</span></span>  

<span data-ttu-id="6301e-104">Each search response includes a [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse) answer, that specifies how you must display the search results.</span><span class="sxs-lookup"><span data-stu-id="6301e-104">Each search response includes a [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse) answer, that specifies how you must display the search results.</span></span> <span data-ttu-id="6301e-105">The ranking response groups results by mainline content and sidebar content for a traditional search results page.</span><span class="sxs-lookup"><span data-stu-id="6301e-105">The ranking response groups results by mainline content and sidebar content for a traditional search results page.</span></span> <span data-ttu-id="6301e-106">If you do not display the results in a traditional mainline and sidebar format, you must provide the mainline content higher visibility than the sidebar content.</span><span class="sxs-lookup"><span data-stu-id="6301e-106">If you do not display the results in a traditional mainline and sidebar format, you must provide the mainline content higher visibility than the sidebar content.</span></span>  
  
<span data-ttu-id="6301e-107">Within each group (mainline or sidebar), the [Items](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankinggroup-items) array identifies the order that the content must appear in.</span><span class="sxs-lookup"><span data-stu-id="6301e-107">Within each group (mainline or sidebar), the [Items](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankinggroup-items) array identifies the order that the content must appear in.</span></span> <span data-ttu-id="6301e-108">Each item provides the following two ways to identify the result within an answer.</span><span class="sxs-lookup"><span data-stu-id="6301e-108">Each item provides the following two ways to identify the result within an answer.</span></span>  
  
-   <span data-ttu-id="6301e-109">`answerType` and `resultIndex` — The `answerType` field identifies the answer (for example, Webpage or News) and `resultIndex` identifies a result within the answer (for example, a news article).</span><span class="sxs-lookup"><span data-stu-id="6301e-109">`answerType` and `resultIndex` — The `answerType` field identifies the answer (for example, Webpage or News) and `resultIndex` identifies a result within the answer (for example, a news article).</span></span> <span data-ttu-id="6301e-110">The index is zero based.</span><span class="sxs-lookup"><span data-stu-id="6301e-110">The index is zero based.</span></span>  
  
-   <span data-ttu-id="6301e-111">`value` — The `value` field contains an ID that matches the ID of either an answer or a result within the answer.</span><span class="sxs-lookup"><span data-stu-id="6301e-111">`value` — The `value` field contains an ID that matches the ID of either an answer or a result within the answer.</span></span> <span data-ttu-id="6301e-112">Either the answer or the results contain the ID but not both.</span><span class="sxs-lookup"><span data-stu-id="6301e-112">Either the answer or the results contain the ID but not both.</span></span>  
  
<span data-ttu-id="6301e-113">Using the ID is simpler to use because you only need to match the ranking ID with the ID of an answer or one of its results.</span><span class="sxs-lookup"><span data-stu-id="6301e-113">Using the ID is simpler to use because you only need to match the ranking ID with the ID of an answer or one of its results.</span></span> <span data-ttu-id="6301e-114">If an answer object includes an `id` field, display all the answer's results together.</span><span class="sxs-lookup"><span data-stu-id="6301e-114">If an answer object includes an `id` field, display all the answer's results together.</span></span> <span data-ttu-id="6301e-115">For example, if the `News` object includes the `id` field, display all the news articles together.</span><span class="sxs-lookup"><span data-stu-id="6301e-115">For example, if the `News` object includes the `id` field, display all the news articles together.</span></span> <span data-ttu-id="6301e-116">If the `News` object does not include the `id` field, then each news article contains an `id` field and the ranking response mixes the news articles with the results from other answers.</span><span class="sxs-lookup"><span data-stu-id="6301e-116">If the `News` object does not include the `id` field, then each news article contains an `id` field and the ranking response mixes the news articles with the results from other answers.</span></span>  
  
<span data-ttu-id="6301e-117">Using the `answerType` and `resultIndex` is a little more complicated.</span><span class="sxs-lookup"><span data-stu-id="6301e-117">Using the `answerType` and `resultIndex` is a little more complicated.</span></span> <span data-ttu-id="6301e-118">You use `answerType` to identify the answer that contains the results to display.</span><span class="sxs-lookup"><span data-stu-id="6301e-118">You use `answerType` to identify the answer that contains the results to display.</span></span> <span data-ttu-id="6301e-119">Then, you use `resultIndex` to index through the answer's results to get the result to display.</span><span class="sxs-lookup"><span data-stu-id="6301e-119">Then, you use `resultIndex` to index through the answer's results to get the result to display.</span></span> <span data-ttu-id="6301e-120">(The `answerType` value is the name of the field in the [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object.) If you're supposed to display all the answer's results together, the ranking response item doesn't include the `resultIndex` field.</span><span class="sxs-lookup"><span data-stu-id="6301e-120">(The `answerType` value is the name of the field in the [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#searchresponse) object.) If you're supposed to display all the answer's results together, the ranking response item doesn't include the `resultIndex` field.</span></span>  

## <a name="ranking-response-example"></a><span data-ttu-id="6301e-121">Ranking response example</span><span class="sxs-lookup"><span data-stu-id="6301e-121">Ranking response example</span></span>

<span data-ttu-id="6301e-122">The following shows an example [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse).</span><span class="sxs-lookup"><span data-stu-id="6301e-122">The following shows an example [RankingResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-web-api-v7-reference#rankingresponse).</span></span> <span data-ttu-id="6301e-123">Because the Web answer does not include an `id` field, you'd display all webpages individually based on the ranking (each webpage includes an `id` field).</span><span class="sxs-lookup"><span data-stu-id="6301e-123">Because the Web answer does not include an `id` field, you'd display all webpages individually based on the ranking (each webpage includes an `id` field).</span></span> <span data-ttu-id="6301e-124">And because the images, videos, and related searches answers do include the `id` field, you'd display the results of each of those answers together based on the ranking.</span><span class="sxs-lookup"><span data-stu-id="6301e-124">And because the images, videos, and related searches answers do include the `id` field, you'd display the results of each of those answers together based on the ranking.</span></span>
  
```json
{  
    "_type" : "SearchResponse",
    "webPages" : {
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF214...",
        "totalEstimatedMatches" : 835000,
        "value" : [
            {
                "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0",
                "name" : "Motor Sports - Live at the race track ...",
                "url" : "http:\/\/www.bing.com\/cr?IG=96C4CF214A0A43...",
                "displayUrl" : "www.contoso.com\/usa\/eventsandracing\/motorsport",
                "snippet" : "Here you will find detailed information about racing...",
                "deepLinks" : [{
                    "name" : "Customer Racing",
                    "url" : "http:\/\/www.bing.com\/cr?IG=96C4CF214A0A43...",
                    "snippet" : "Customer racing news; General news..."
            },
            . . .  
        ]  
    },  
    "images" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Images",
        "readLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/images...",
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF214A...",
        "isFamilyFriendly" : true,
        "value" : [
            {
                "name" : "2016 Supercar Wallpapers",
                "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4...",
                "thumbnailUrl" : "https:\/\/tse1.mm.bing.net\/th?id=OIP...",
                "datePublished" : "2017-03-25T11:14:00",
                "contentUrl" : "http:\/\/www.contoso.com\/wall...",
                "hostPageUrl" : "http:\/\/www.bing.com\/cr?IG=96C4CF214...",
                "contentSize" : "373283 B",
                "encodingFormat" : "jpeg",
                "hostPageDisplayUrl" : "http:\/\/www.contoso.com\/lmp-...",
                "width" : 1920,
                "height" : 1080,
                "thumbnail" : {
                    "width" : 300,
                    "height" : 168
                },
                "insightsSourcesSummary" : {
                    "shoppingSourcesCount" : 0,
                    "recipeSourcesCount" : 0
                }
            },
            . . .  
        ]  
    },  
    "relatedSearches" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#RelatedSearches",
        "value" : [
            {
                "text" : "vintage racing teams",
                "displayText" : "vintage racing teams",
                "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF2..."
            },
            . . .  
        ]  
    },  
    "videos" : {
        "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Videos",
        "readLink" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/videos...",
        "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF214A...",
        "isFamilyFriendly" : true,
        "value" : [
            {
                "name" : "Why We Race",
                "description" : "A new era begins in motorsports this weekend...",
                "webSearchUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF2...",
                "thumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?id=OVP.Vo1...",
                "datePublished" : "2014-01-25T16:31:48",
                "publisher" : [
                    {
                        "name" : "Fabrikam"
                    }
                ],
                "contentUrl" : "https:\/\/www.fabrikam.com\/watch?v=oL...",
                "hostPageUrl" : "https:\/\/www.bing.com\/cr?IG=96C4CF214...",
                "encodingFormat" : "mp4",
                "hostPageDisplayUrl" : "https:\/\/www.fabrikam.com\/watch?v=oLAZgD...",
                "width" : 480,
                "height" : 360,
                "duration" : "PT2M42S",
                "motionThumbnailUrl" : "https:\/\/tse4.mm.bing.net\/th?id=OM...",
                "embedHtml" : "<iframe width=\"1280\" height=\"720\" src=\"http:\/\/www.you...<\/iframe>",
                "allowHttpsEmbed" : true,
                "viewCount" : 47325,
                "thumbnail" : {
                    "width" : 300,
                    "height" : 168
                },
                "allowMobileEmbed" : true,
                "isSuperfresh" : false
            },
            . . .  
        ]  
    },  
    "rankingResponse" : {
        "mainline" : {
            "items" : [{
                "answerType" : "WebPages",
                "resultIndex" : 0,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.0"
                }
            },
            {
                "answerType" : "Images",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Images"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 1,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.1"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 2,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.2"
                }
            },
            {
                "answerType" : "Videos",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#Videos"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 3,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.3"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 4,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.4"
                }
            },
            {
                "answerType" : "WebPages",
                "resultIndex" : 5,
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#WebPages.5"
                }
            }]
        },
        "sidebar" : {
            "items" : [{
                "answerType" : "RelatedSearches",
                "value" : {
                    "id" : "https:\/\/api.cognitive.microsoft.com\/api\/v7\/#RelatedSearches"
                }
            }]
        }
    }
}  
```  
  
<span data-ttu-id="6301e-125">Based on this ranking response, the mainline would display the following search results:</span><span class="sxs-lookup"><span data-stu-id="6301e-125">Based on this ranking response, the mainline would display the following search results:</span></span>  
  
-   <span data-ttu-id="6301e-126">The first webpage result</span><span class="sxs-lookup"><span data-stu-id="6301e-126">The first webpage result</span></span> 
-   <span data-ttu-id="6301e-127">All the images</span><span class="sxs-lookup"><span data-stu-id="6301e-127">All the images</span></span>  
-   <span data-ttu-id="6301e-128">The second and third webpage results</span><span class="sxs-lookup"><span data-stu-id="6301e-128">The second and third webpage results</span></span>  
-   <span data-ttu-id="6301e-129">All the videos</span><span class="sxs-lookup"><span data-stu-id="6301e-129">All the videos</span></span>  
-   <span data-ttu-id="6301e-130">The 4th, 5th, and 6th webpage results</span><span class="sxs-lookup"><span data-stu-id="6301e-130">The 4th, 5th, and 6th webpage results</span></span>  
  
<span data-ttu-id="6301e-131">And the sidebar would display the following search results:</span><span class="sxs-lookup"><span data-stu-id="6301e-131">And the sidebar would display the following search results:</span></span>  
  
-   <span data-ttu-id="6301e-132">All the related searches</span><span class="sxs-lookup"><span data-stu-id="6301e-132">All the related searches</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="6301e-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="6301e-133">Next steps</span></span>

<span data-ttu-id="6301e-134">For information about promoting unranked results, see [Promoting answers that are not ranked](./filter-answers.md#promoting-answers-that-are-not-ranked).</span><span class="sxs-lookup"><span data-stu-id="6301e-134">For information about promoting unranked results, see [Promoting answers that are not ranked](./filter-answers.md#promoting-answers-that-are-not-ranked).</span></span>

<span data-ttu-id="6301e-135">For information about limiting the number of ranked answers in the response, see [Limiting the number of answers in the response](./filter-answers.md#limiting-the-number-of-answers-in-the-response).</span><span class="sxs-lookup"><span data-stu-id="6301e-135">For information about limiting the number of ranked answers in the response, see [Limiting the number of answers in the response](./filter-answers.md#limiting-the-number-of-answers-in-the-response).</span></span>

<span data-ttu-id="6301e-136">For a C# example that uses ranking to display results, see [C# ranking tutorial](./csharp-ranking-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6301e-136">For a C# example that uses ranking to display results, see [C# ranking tutorial](./csharp-ranking-tutorial.md).</span></span>