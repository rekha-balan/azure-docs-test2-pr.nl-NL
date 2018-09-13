---
title: Project Answer Search fact query - Microsoft Cognitive Services | Microsoft Docs
description: Queries for facts using Project Answer Search
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/16/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 0a9d1925d5ae26f40824676fbebdcb0ffc450c53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871281"
---
# <a name="query-for-facts"></a><span data-ttu-id="d3b22-103">Query for facts</span><span class="sxs-lookup"><span data-stu-id="d3b22-103">Query for facts</span></span>

<span data-ttu-id="d3b22-104">If the query is for a fact such as a date or identifiable knowledge, the response can contain `facts` answers.</span><span class="sxs-lookup"><span data-stu-id="d3b22-104">If the query is for a fact such as a date or identifiable knowledge, the response can contain `facts` answers.</span></span> <span data-ttu-id="d3b22-105">Fact answers contain relevant results extracted from paragraphs in web documents.</span><span class="sxs-lookup"><span data-stu-id="d3b22-105">Fact answers contain relevant results extracted from paragraphs in web documents.</span></span>  <span data-ttu-id="d3b22-106">These queries always return webpages, and [facts](fact-queries.md) and/or [entities](entity-queries.md) are query-dependent.</span><span class="sxs-lookup"><span data-stu-id="d3b22-106">These queries always return webpages, and [facts](fact-queries.md) and/or [entities](entity-queries.md) are query-dependent.</span></span>

<span data-ttu-id="d3b22-107">Queries such as valentines+2016, when+is+ramadan are considered date-related queries.</span><span class="sxs-lookup"><span data-stu-id="d3b22-107">Queries such as valentines+2016, when+is+ramadan are considered date-related queries.</span></span> <span data-ttu-id="d3b22-108">If Bing determines that the query is date-related, the response contains a `facts` answer.</span><span class="sxs-lookup"><span data-stu-id="d3b22-108">If Bing determines that the query is date-related, the response contains a `facts` answer.</span></span> 

<span data-ttu-id="d3b22-109">The following example is a date-related `facts` answer.</span><span class="sxs-lookup"><span data-stu-id="d3b22-109">The following example is a date-related `facts` answer.</span></span> 

<span data-ttu-id="d3b22-110">**Query:**</span><span class="sxs-lookup"><span data-stu-id="d3b22-110">**Query:**</span></span>
````
https://labsportalppe.azure-api.net/answerSearch/v7.0/search?q=valentines+2016

````

<span data-ttu-id="d3b22-111">**Response:** The `subjectName` field contains a display version of the user's query that you can use as a label when displaying the fact.</span><span class="sxs-lookup"><span data-stu-id="d3b22-111">**Response:** The `subjectName` field contains a display version of the user's query that you can use as a label when displaying the fact.</span></span> <span data-ttu-id="d3b22-112">If the query string is valentines+2016, Bing may change it Valentine's Day 2016.</span><span class="sxs-lookup"><span data-stu-id="d3b22-112">If the query string is valentines+2016, Bing may change it Valentine's Day 2016.</span></span> <span data-ttu-id="d3b22-113">The description field contains the fact.</span><span class="sxs-lookup"><span data-stu-id="d3b22-113">The description field contains the fact.</span></span>

````
{   
    "_type" : "SearchResponse",   
    "queryContext" : {   
        "originalQuery" : "valentines 2016" 
    },   
    "facts" : {   
        "id" : "https:\/\/www.bingapis.com\/api\/v7\/#Facts",   
        "value" : [{   
            "description" : "Valentine's Day was on Sunday, February 14, 2016.",   
            "subjectName" : "Valentine's Day 2016"   
        }]   
    },   
    "rankingResponse" : {   
        "mainline" : {   
            "items" : [{   
                "answerType" : "Facts",   
                "value" : {   
                    "id" : "https:\/\/www.bingapis.com\/api\/v7\/knowledge\/#Facts"                   }   
            }]   
        }   
    }   
}   

````

<span data-ttu-id="d3b22-114">The query "Why is the sky blue?"</span><span class="sxs-lookup"><span data-stu-id="d3b22-114">The query "Why is the sky blue?"</span></span> <span data-ttu-id="d3b22-115">returns an example of a knowledge-related answer.</span><span class="sxs-lookup"><span data-stu-id="d3b22-115">returns an example of a knowledge-related answer.</span></span>

<span data-ttu-id="d3b22-116">**Query:**</span><span class="sxs-lookup"><span data-stu-id="d3b22-116">**Query:**</span></span>

````
https://api.labs.cognitive.microsoft.com/answerSearch/v7.0/search?q=why+is+the+sky+blue

````

<span data-ttu-id="d3b22-117">**Response:** The `value/description` field contains the knowledge or information requested by the query.</span><span class="sxs-lookup"><span data-stu-id="d3b22-117">**Response:** The `value/description` field contains the knowledge or information requested by the query.</span></span>

````
  "facts": {
    "id": "https://www.bingapis.com/api/v7/#Facts",
    "contractualRules": [
      {
        "_type": "ContractualRules/LinkAttribution",
        "text": "en.wikipedia.org/wiki/Diffuse_sky_radiation",
        "url": "http://en.wikipedia.org/wiki/Diffuse_sky_radiation"
      },
      {
        "_type": "ContractualRules/LinkAttribution",
        "text": "spaceplace.nasa.gov/blue-sky/en/",
        "url": "http://spaceplace.nasa.gov/blue-sky/en/"
      }
    ],
    "attributions": [
      {
        "providerDisplayName": "en.wikipedia.org/wiki/Diffuse_sky_radiation",
        "seeMoreUrl": "http://en.wikipedia.org/wiki/Diffuse_sky_radiation"
      },
      {
        "providerDisplayName": "spaceplace.nasa.gov/blue-sky/en/",
        "seeMoreUrl": "http://spaceplace.nasa.gov/blue-sky/en/"
      }
    ],
    "value": [
      {
        "image": {
          "webSearchUrl": "https://www.bing.com/images/search?view=detailv2&FORM=OIIRPO&q=&id=B632272C4E934D7F0B18790300B2DE34E7676C7A&simid=608045681196075791&iss=eqna",
          "name": "Why is the sky blue in the sky?",
          "thumbnailUrl": "https://www.bing.com/th?id=ODE.858093005&w=140&h=140&c=8&rs=1&qlt=100&pid=3.1",
          "isFamilyFriendly": true
        },
        "description": "When sunlight reaches Earth's atmosphere, it is scattered in all directions by all the gases and particles in the air. Blue is scattered by air molecules more than other colors because it travels as shorter, smaller waves. This is why we see a blue sky most of the time.\n\nCloser to the horizon, the sky fades to a lighter blue or white. The sunlight reaching us from low in the sky has passed through even more air than the sunlight reaching us from overhead. As the sunlight has passed through all this air, the air molecules have scattered and rescattered the blue light many times in many directions. Also, the surface of Earth has reflected and scattered the light. All this scattering mixes the colors together again so we see more white and less blue.",
        "subjectName": "Why is the sky blue in the sky?",
        "primaryData": [
          "The atmosphere scatters more blue light"
        ]
      }
    ]
  },

````

## <a name="tabular-data"></a><span data-ttu-id="d3b22-118">Tabular data</span><span class="sxs-lookup"><span data-stu-id="d3b22-118">Tabular data</span></span>
<span data-ttu-id="d3b22-119">In some cases, facts can be returned as `_type: StructuredValue/TabularData`.</span><span class="sxs-lookup"><span data-stu-id="d3b22-119">In some cases, facts can be returned as `_type: StructuredValue/TabularData`.</span></span> <span data-ttu-id="d3b22-120">The following query gets tabular data with contrasting information about coffee and tea.</span><span class="sxs-lookup"><span data-stu-id="d3b22-120">The following query gets tabular data with contrasting information about coffee and tea.</span></span>

````
https://labsportalppe.azure-api.net/answerSearch/v7.0/search?q=coffee+vs+tea&mkt=en-us 

````
<span data-ttu-id="d3b22-121">The `facts` results include the following rows and cells:</span><span class="sxs-lookup"><span data-stu-id="d3b22-121">The `facts` results include the following rows and cells:</span></span>
````
    "value": [
      {
        "subjectName": "Coffee vs. Tea",
        "richCaption": {
          "_type": "StructuredValue/TabularData",
          "header": [
            "",
            "Coffee",
            "Tea"
          ],
          "rows": [
            {
              "cells": [
                {
                  "text": "Part of plant used"
                },
                {
                  "text": "Bean"
                },
                {
                  "text": "Leaf"
                }
              ]
            },
            {
              "cells": [
                {
                  "text": "Caffeine Content"
                },
                {
                  "text": "80-185 mg per 8 ounce cup depending upon the brew and the..."
                },
                {
                  "text": "15 - 70 mg per cup"
                }
              ]
            },
            {
              "cells": [
                {
                  "text": "Types of Consumption"
                },
                {
                  "text": "Drip Coffee"
                },
                {
                  "text": "White Tea"
                }
              ]
            },
            {
              "cells": [
                {
                  "text": "Additions"
                },
                {
                  "text": "Sugar"
                },
                {
                  "text": "Milk"
                }
              ]
            }
          ],
          "seeMoreUrl": {
            "text": "8 more rows",
            "url": "http://www.diffen.com/difference/Coffee_vs_Tea"
          }
        }
      }
    ]
  },

````

## <a name="next-steps"></a><span data-ttu-id="d3b22-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="d3b22-122">Next steps</span></span>
- [<span data-ttu-id="d3b22-123">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="d3b22-123">C# quickstart</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="d3b22-124">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="d3b22-124">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="d3b22-125">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="d3b22-125">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="d3b22-126">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="d3b22-126">Python quickstart</span></span>](python-quickstart.md)
