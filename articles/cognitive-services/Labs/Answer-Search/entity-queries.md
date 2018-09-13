---
title: Project Answer Search Entity query - Microsoft Cognitive Services | Microsoft Docs
description: Queries for Entities using Project Answer Search
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/16/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: 2b8382b791c02514e5110097700e223d98fafd6a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866655"
---
# <a name="query-for-entities"></a><span data-ttu-id="29508-103">Query for Entities</span><span class="sxs-lookup"><span data-stu-id="29508-103">Query for Entities</span></span>

<span data-ttu-id="29508-104">If the query requests information about a person, place or thing, the response can contain an `entities` answer.</span><span class="sxs-lookup"><span data-stu-id="29508-104">If the query requests information about a person, place or thing, the response can contain an `entities` answer.</span></span>  <span data-ttu-id="29508-105">Queries always return webpages, [facts](fact-queries.md) and/or [entities](entity-queries.md) are query dependent.</span><span class="sxs-lookup"><span data-stu-id="29508-105">Queries always return webpages, [facts](fact-queries.md) and/or [entities](entity-queries.md) are query dependent.</span></span>

<span data-ttu-id="29508-106">Entities support three query scenarios:</span><span class="sxs-lookup"><span data-stu-id="29508-106">Entities support three query scenarios:</span></span> 
-   <span data-ttu-id="29508-107">DominantEntity—There is only one entity that matches the user's query and intent.</span><span class="sxs-lookup"><span data-stu-id="29508-107">DominantEntity—There is only one entity that matches the user's query and intent.</span></span> <span data-ttu-id="29508-108">For example, the query, Space Needle, is a DominantEntity scenario.</span><span class="sxs-lookup"><span data-stu-id="29508-108">For example, the query, Space Needle, is a DominantEntity scenario.</span></span> 
-   <span data-ttu-id="29508-109">Disambiguation—There is more than one entity that matches the user's query and intent and it is up to the user to select the correct entity.</span><span class="sxs-lookup"><span data-stu-id="29508-109">Disambiguation—There is more than one entity that matches the user's query and intent and it is up to the user to select the correct entity.</span></span> <span data-ttu-id="29508-110">For example, the query Game of Thrones is a Disambiguation scenario that returns the television show and the book series.</span><span class="sxs-lookup"><span data-stu-id="29508-110">For example, the query Game of Thrones is a Disambiguation scenario that returns the television show and the book series.</span></span> 
-   <span data-ttu-id="29508-111">List—There are multiple entities that match the user's query and intent.</span><span class="sxs-lookup"><span data-stu-id="29508-111">List—There are multiple entities that match the user's query and intent.</span></span> <span data-ttu-id="29508-112">For example, the query "List of endangered species" is a list scenario that returns tabular values formatted for display in rows and cells.</span><span class="sxs-lookup"><span data-stu-id="29508-112">For example, the query "List of endangered species" is a list scenario that returns tabular values formatted for display in rows and cells.</span></span> 
 
<span data-ttu-id="29508-113">To determine the query scenario, use the `queryScenario` field of the `entities` object.</span><span class="sxs-lookup"><span data-stu-id="29508-113">To determine the query scenario, use the `queryScenario` field of the `entities` object.</span></span> <span data-ttu-id="29508-114">The data that the entity includes depends on the entity's type.</span><span class="sxs-lookup"><span data-stu-id="29508-114">The data that the entity includes depends on the entity's type.</span></span> <span data-ttu-id="29508-115">Although entities include the same basic information, some entities such as tourist attractions or books include additional properties.</span><span class="sxs-lookup"><span data-stu-id="29508-115">Although entities include the same basic information, some entities such as tourist attractions or books include additional properties.</span></span> <span data-ttu-id="29508-116">Entities that include additional properties include the `_type` field that contains a hint used by the serializer.</span><span class="sxs-lookup"><span data-stu-id="29508-116">Entities that include additional properties include the `_type` field that contains a hint used by the serializer.</span></span> <span data-ttu-id="29508-117">The following entities include additional properties:</span><span class="sxs-lookup"><span data-stu-id="29508-117">The following entities include additional properties:</span></span> 
-   <span data-ttu-id="29508-118">Book</span><span class="sxs-lookup"><span data-stu-id="29508-118">Book</span></span> 
-   <span data-ttu-id="29508-119">MusicRecording</span><span class="sxs-lookup"><span data-stu-id="29508-119">MusicRecording</span></span> 
-   <span data-ttu-id="29508-120">Person</span><span class="sxs-lookup"><span data-stu-id="29508-120">Person</span></span> 
-   <span data-ttu-id="29508-121">Attraction</span><span class="sxs-lookup"><span data-stu-id="29508-121">Attraction</span></span> 
 
<span data-ttu-id="29508-122">To determine the type of entity that the response contains, use the `entityTypeHints` field as shown in the query for Bill Gates.</span><span class="sxs-lookup"><span data-stu-id="29508-122">To determine the type of entity that the response contains, use the `entityTypeHints` field as shown in the query for Bill Gates.</span></span>
````
        },
        "description": "Bill Gates is an American business man and philanthropist, co-founder of Microsoft",
        "entityPresentationInfo": {
          "entityScenario": "DominantEntity",
          "entityTypeHints": [
            "Person"
          ]
        },
        "bingId": "6d7d66a7-2cb8-0ae9-637c-f81fd749dc9a"
      }
````
<span data-ttu-id="29508-123">The following is a query for Space Needle:</span><span class="sxs-lookup"><span data-stu-id="29508-123">The following is a query for Space Needle:</span></span>
````
https://api.labs.cognitive.microsoft.com/answerSearch/v7.0/search?q=space+needle&mkt=en-us
````
<span data-ttu-id="29508-124">The response includes the `entities` answer.</span><span class="sxs-lookup"><span data-stu-id="29508-124">The response includes the `entities` answer.</span></span> <span data-ttu-id="29508-125">Note the `entityScenario` and `entityTypeHints` fields.</span><span class="sxs-lookup"><span data-stu-id="29508-125">Note the `entityScenario` and `entityTypeHints` fields.</span></span> 
````
  "entities": {
    "value": [
      {
        "id": "https://www.bingapis.com/api/v7/#Entities.0",
        "contractualRules": [
          {
            "_type": "ContractualRules/LicenseAttribution",
            "targetPropertyName": "description",
            "mustBeCloseToContent": true,
            "license": {
              "name": "CC-BY-SA",
              "url": "http://creativecommons.org/licenses/by-sa/3.0/"
            },
            "licenseNotice": "Text under CC-BY-SA license"
          },
          {
            "_type": "ContractualRules/LinkAttribution",
            "targetPropertyName": "description",
            "mustBeCloseToContent": true,
            "text": "Wikipedia",
            "url": "http://en.wikipedia.org/wiki/Space_Needle"
          },
          {
            "_type": "ContractualRules/MediaAttribution",
            "targetPropertyName": "image",
            "mustBeCloseToContent": true,
            "url": "http://en.wikipedia.org/wiki/Space_Needle"
          }
        ],
        "webSearchUrl": "https://www.bing.com/entityexplore?q\u003dSpace+Needle\u0026filters\u003dsid:%22f8dd5b08-206d-2554-6e4a-893f51f4de7e%22\u0026elv\u003dAXXfrEiqqD9r3GuelwApulpmymQx!ODfuQu*veOQHkvP0!Zbvi5F5tVcMSDJvDEWiQWwrdueYTtIszgj03oFQHykYYLYgq3q5!Sf00QxXGIS",
        "name": "Space Needle",
        "image": {
          "name": "Space Needle",
          "thumbnailUrl": "https://www.bing.com/th?id\u003dA15d336cf119b9b5c7e0ab37e271421d3\u0026w\u003d110\u0026h\u003d110\u0026c\u003d7\u0026rs\u003d1\u0026qlt\u003d80\u0026cdv\u003d1\u0026pid\u003d16.1",
          "provider": [
            {
              "_type": "Organization",
              "url": "http://en.wikipedia.org/wiki/Space_Needle"
            }
          ],
          "hostPageUrl": "http://upload.wikimedia.org/wikipedia/commons/2/23/Space_Needle_2011-07-04.jpg",
          "width": 110,
          "height": 110,
          "sourceWidth": 152,
          "sourceHeight": 300
        },
        "description": "The Space Needle is an observation tower in Seattle, Washington, a landmark of the Pacific Northwest, and an icon of Seattle. It was built in the Seattle Center for the 1962 World\u0027s Fair, which drew over 2.3 million visitors, when nearly 20,000 people a day used its elevators.",
        "entityPresentationInfo": {
          "entityScenario": "DominantEntity",
          "entityTypeHints": [
            "Attraction"
          ]
        },
        "bingId": "f8dd5b08-206d-2554-6e4a-893f51f4de7e"
      }
    ]
  },
````

<span data-ttu-id="29508-126">A query can return a list if it is relevant.</span><span class="sxs-lookup"><span data-stu-id="29508-126">A query can return a list if it is relevant.</span></span>

<span data-ttu-id="29508-127">**Query:** The following query finds a list of endangered species:</span><span class="sxs-lookup"><span data-stu-id="29508-127">**Query:** The following query finds a list of endangered species:</span></span>

````
https://api.labs.cognitive.microsoft.com/answerSearch/v7.0/search?q=list+of+endangered+species

````

<span data-ttu-id="29508-128">**Response:** The response includes a list formatted for display as tabular values:</span><span class="sxs-lookup"><span data-stu-id="29508-128">**Response:** The response includes a list formatted for display as tabular values:</span></span>
````
  "facts": {
    "id": "https://www.bingapis.com/api/v7/#Facts",
    "contractualRules": [
      {
        "_type": "ContractualRules/LinkAttribution",
        "text": "www.worldwildlife.org/species/directory?direction=desc&sort=e…",
        "url": "https://www.worldwildlife.org/species/directory?direction=desc&sort=extinction_status"
      }
    ],
    "attributions": [
      {
        "providerDisplayName": "www.worldwildlife.org/species/directory?direction=desc&sort=e…",
        "seeMoreUrl": "https://www.worldwildlife.org/species/directory?direction=desc&sort=extinction_status"
      }
    ],
    "value": [
      {
        "subjectName": "Species Directory",
        "richCaption": {
          "_type": "StructuredValue/TabularData",
          "header": [
            "Common name",
            "Scientific name",
            "Conservation status ↓"
          ],
          "rows": [
            {
              "cells": [
                {
                  "_type": "Properties/Link",
                  "text": "Amur Leopard",
                  "url": "https://www.bing.com/https//www.worldwildlife.org/species/amur-leopard"
                },
                {
                  "text": "Panthera pardus orientalis"
                },
                {
                  "text": "Critically Endangered"
                }
              ]
            },
            {
              "cells": [
                {
                  "_type": "Properties/Link",
                  "text": "Black Rhino",
                  "url": "https://www.bing.com/https//www.worldwildlife.org/species/black-rhino"
                },
                {
                  "text": "Diceros bicornis"
                },
                {
                  "text": "Critically Endangered"
                }
              ]
            },
            {
              "cells": [
                {
                  "_type": "Properties/Link",
                  "text": "Bornean Orangutan",
                  "url": "https://www.bing.com/https//www.worldwildlife.org/species/bornean-orangutan"
                },
                {
                  "text": "Pongo pygmaeus"
                },
                {
                  "text": "Critically Endangered"
                }
              ]
            },
            {
              "cells": [
                {
                  "_type": "Properties/Link",
                  "text": "Cross River Gorilla",
                  "url": "https://www.bing.com/https//www.worldwildlife.org/species/cross-river-gorilla"
                },
                {
                  "text": "Gorilla gorilla diehli"
                },
                {
                  "text": "Critically Endangered"
                }
              ]
            }
          ],
          "seeMoreUrl": {
            "text": "46 more rows",
            "url": "https://www.worldwildlife.org/species/directory?direction=desc&sort=extinction_status"
          }
        }
      }
    ]
  },

````


## <a name="next-steps"></a><span data-ttu-id="29508-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="29508-129">Next steps</span></span>
- [<span data-ttu-id="29508-130">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="29508-130">C# quickstart</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="29508-131">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="29508-131">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="29508-132">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="29508-132">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="29508-133">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="29508-133">Python quickstart</span></span>](python-quickstart.md)