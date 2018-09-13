---
title: Project Answer Search overview - Microsoft Cognitive Services | Microsoft Docs
description: Introduction to the Project Answer Search.
services: cognitive-services
author: mikedodaro
manager: rosh
ms.service: cognitive-services
ms.technology: project-answer-search
ms.topic: article
ms.date: 04/13/2018
ms.author: rosh, v-gedod
ms.openlocfilehash: d87cf1390970d2c815b94bcaee7e07c19bc03cce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857174"
---
# <a name="what-is-project-answer-search"></a><span data-ttu-id="8bdf3-103">What is Project Answer Search?</span><span class="sxs-lookup"><span data-stu-id="8bdf3-103">What is Project Answer Search?</span></span>
<span data-ttu-id="8bdf3-104">Project Answer Search API uses the Bing v7 endpoint to get answers to interrogative queries.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-104">Project Answer Search API uses the Bing v7 endpoint to get answers to interrogative queries.</span></span> <span data-ttu-id="8bdf3-105">A question such as "What is the circumference of the earth?"</span><span class="sxs-lookup"><span data-stu-id="8bdf3-105">A question such as "What is the circumference of the earth?"</span></span> <span data-ttu-id="8bdf3-106">returns an answer with factual information.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-106">returns an answer with factual information.</span></span>  <span data-ttu-id="8bdf3-107">A query for a person, place, or thing returns information about the entity identified by the query.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-107">A query for a person, place, or thing returns information about the entity identified by the query.</span></span> <span data-ttu-id="8bdf3-108">These scenarios can be useful in applications such as conversational bots, messaging apps, readers, etc.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-108">These scenarios can be useful in applications such as conversational bots, messaging apps, readers, etc.</span></span>  

<span data-ttu-id="8bdf3-109">Queries return responses that depend on the query scenario: webpages are always returned, while [facts](fact-queries.md) and/or [entities](entity-queries.md) are returned if relevant.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-109">Queries return responses that depend on the query scenario: webpages are always returned, while [facts](fact-queries.md) and/or [entities](entity-queries.md) are returned if relevant.</span></span>

## <a name="endpoint"></a><span data-ttu-id="8bdf3-110">Endpoint</span><span class="sxs-lookup"><span data-stu-id="8bdf3-110">Endpoint</span></span>
<span data-ttu-id="8bdf3-111">To get answers to a question or information about a person, place, or thing, send a request to the Answer Search API endpoint.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-111">To get answers to a question or information about a person, place, or thing, send a request to the Answer Search API endpoint.</span></span> <span data-ttu-id="8bdf3-112">Use the headers and URL parameters for various specifications.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-112">Use the headers and URL parameters for various specifications.</span></span>  <span data-ttu-id="8bdf3-113">Include *Ocp-Apim-Subscription-Key* header with a valid token.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-113">Include *Ocp-Apim-Subscription-Key* header with a valid token.</span></span>  <span data-ttu-id="8bdf3-114">The market parameter is required.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-114">The market parameter is required.</span></span> <span data-ttu-id="8bdf3-115">Only `en-us` market is currently supported.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-115">Only `en-us` market is currently supported.</span></span>

<span data-ttu-id="8bdf3-116">The following query gets answers to the question: "What is the circumference of the earth?"</span><span class="sxs-lookup"><span data-stu-id="8bdf3-116">The following query gets answers to the question: "What is the circumference of the earth?"</span></span>

<span data-ttu-id="8bdf3-117">GET:</span><span class="sxs-lookup"><span data-stu-id="8bdf3-117">GET:</span></span>
````
https://api.labs.cognitive.microsoft.com/answerSearch/v7.0/search?q=what+is+circumference+of+the=earth?&mkt=en-us

````

<span data-ttu-id="8bdf3-118">The URL parameter `q=` is required to specify the object of search.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-118">The URL parameter `q=` is required to specify the object of search.</span></span>

## <a name="response-object"></a><span data-ttu-id="8bdf3-119">Response object</span><span class="sxs-lookup"><span data-stu-id="8bdf3-119">Response object</span></span>

<span data-ttu-id="8bdf3-120">The response includes HTTP headers, webpages, facts, and/or entities.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-120">The response includes HTTP headers, webpages, facts, and/or entities.</span></span>

````
BingAPIs-TraceId: AB2E75C998614ADB8EBF5110DF648298
X-MSEdge-ClientID: 1E48FC4F7B8768C80B14F7997A106906
BingAPIs-SessionId: 0504DDD6DAE84861A4842306F8DA7A58
BingAPIs-Market: en-US
X-MSEdge-Ref: Ref A: AB2E75C998614ADB8EBF5110DF648298 Ref B: CO1EDGE0322 Ref C: 2018-04-19T19:57:13Z

JSON Response:

{
  "_type": "SearchResponse",
  "queryContext": {
    "originalQuery": "what is the circumference of earth"
  },
  "webPages": {
    "webSearchUrl": "https://www.bing.com/search?q\u003dwhat+is+the+circumference+of+earth",
    "totalEstimatedMatches": 217000,
    "value": [
      {
        "id": "https://www.bingapis.com/api/v7/#WebPages.0",
        "name": "Circumference of the Earth - Universe Today",
        "url": "https://www.universetoday.com/26461/circumference-of-the-earth/",
        "isFamilyFriendly": true,
        "displayUrl": "https://www.universetoday.com/26461/circumference-of-the-earth",
        "snippet": "The circumference of the Earth in kilometers is 40,075 km, and the circumference of the Earth in miles is 24,901. In other words, if you could drive your car around the equator of the Earth (yes, even over the oceans), youâ€™d put on an extra 40,075 km on the odometer.",
        "deepLinks": [
          {
            "name": "About Earth",
            "url": "https://www.universetoday.com/14382/10-interesting-facts-about-planet-earth/"
          }
        ],
        "dateLastCrawled": "2018-04-12T14:13:00.0000000Z",
        "language": "en"
      },
      {
        "id": "https://www.bingapis.com/api/v7/#WebPages.1",
        "name": "Earth - Wikipedia",
        "url": "https://en.wikipedia.org/wiki/Earth",
        "about": [
          {
            "name": "Earth"
          },
          {
            "name": "Earth"
          }
        ],
        "isFamilyFriendly": true,
        "displayUrl": "https://en.wikipedia.org/wiki/Earth",
        "snippet": "Circumference: 40 075.017 km equatorial (24 901.461 mi) ... Earth is the third planet from the Sun and the only object in the Universe known to harbor life.",
        "deepLinks": [
          {
            "name": "Moon",
            "url": "https://en.wikipedia.org/wiki/Moon"
          },
          {
            "name": "Planet",
            "url": "https://en.wikipedia.org/wiki/Planet"
          },
          {
            "name": "Quasi-Satellites",
            "url": "https://en.wikipedia.org/wiki/Quasi-satellite"
          },
          {
            "name": "World Population",
            "url": "https://en.wikipedia.org/wiki/World_population"
          },
   . . .

    ]
  },
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
            "url": "http://en.wikipedia.org/wiki/Earth"
          },
          {
            "_type": "ContractualRules/MediaAttribution",
            "targetPropertyName": "image",
            "mustBeCloseToContent": true,
            "url": "http://en.wikipedia.org/wiki/Earth"
          }
        ],
        "webSearchUrl": "https://www.bing.com/entityexplore?q\u003dEarth\u0026filters\u003dsid:%226ddb3372-4801-5567-321e-e8a53bd774a4%22\u0026elv\u003dAXXfrEiqqD9r3GuelwApulpmymQx!ODfuQu*veOQHkvP0!Zbvi5F5tVcMSDJvDEWiQWwrdueYTtIszgj03oFQHykYYLYgq3q5!Sf00QxXGIS",
        "name": "Earth",
        "image": {
          "name": "Earth",
          "thumbnailUrl": "https://www.bing.com/th?id\u003dA3ab623665ab412f386c162bd29f0683a\u0026w\u003d110\u0026h\u003d110\u0026c\u003d7\u0026rs\u003d1\u0026qlt\u003d80\u0026cdv\u003d1\u0026pid\u003d16.1",
          "provider": [
            {
              "_type": "Organization",
              "url": "http://en.wikipedia.org/wiki/Earth"
            }
          ],
          "hostPageUrl": "http://upload.wikimedia.org/wikipedia/commons/9/97/The_Earth_seen_from_Apollo_17.jpg",
          "width": 110,
          "height": 110,
          "sourceWidth": 799,
          "sourceHeight": 800
        },
        "description": "Earth is the third planet from the Sun and the only object in the Universe known to harbor life. According to radiometric dating and other sources of evidence, Earth formed over 4.5 billion years ago. Earth\u0027s gravity interacts with other objects in space, especially the Sun and the Moon, Earth\u0027s only natural satellite. Earth revolves around the Sun in 365.26 days, a period known as an Earth year. During this time, Earth rotates about its axis about 366.26 times.",
        "entityPresentationInfo": {
          "entityScenario": "DominantEntity",
          "entityTypeHints": [
            "Generic"
          ]
        },
        "bingId": "6ddb3372-4801-5567-321e-e8a53bd774a4"
      }
    ]
  },
  "facts": {
    "id": "https://www.bingapis.com/api/v7/#Facts",
    "contractualRules": [
      {
        "_type": "ContractualRules/LinkAttribution",
        "text": "www.universetoday.com/26461/circumference-of-the-earth/",
        "url": "http://www.universetoday.com/26461/circumference-of-the-earth/"
      }
    ],
    "attributions": [
      {
        "providerDisplayName": "www.universetoday.com/26461/circumference-of-the-earth/",
        "seeMoreUrl": "http://www.universetoday.com/26461/circumference-of-the-earth/"
      }
    ],
    "value": [
      {
        "description": "The circumference of the Earth in kilometers is 40,075 km, and the circumference of the Earth in miles is 24,901. In other words, if you could drive your car around the equator of the Earth (yes, even over the oceans), youâ€™d put on an extra 40,075 km on the odometer.",
        "subjectName": ""
      }
    ]
  },
  "rankingResponse": {
    "mainline": {
      "items": [
        {
          "answerType": "Facts",
          "value": {
            "id": "https://www.bingapis.com/api/v7/#Facts"
          }
        },
        {
          "answerType": "WebPages",
          "resultIndex": 0,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#WebPages.0"
          }
        },
        {
          "answerType": "WebPages",
          "resultIndex": 1,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#WebPages.1"
          }
        },
        {
          "answerType": "WebPages",
          "resultIndex": 2,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#WebPages.2"
          }
        },
        
        . . . 
      ]
    },
    "sidebar": {
      "items": [
        {
          "answerType": "Entities",
          "resultIndex": 0,
          "value": {
            "id": "https://www.bingapis.com/api/v7/#Entities.0"
          }
        }
      ]
    }
  }
}

````

## <a name="terms-of-use"></a><span data-ttu-id="8bdf3-121">Terms of use</span><span class="sxs-lookup"><span data-stu-id="8bdf3-121">Terms of use</span></span>
<span data-ttu-id="8bdf3-122">Project Answer Search and Project Video Trends are subject to the [Bing Search Use and Display Requirements](use-display-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8bdf3-122">Project Answer Search and Project Video Trends are subject to the [Bing Search Use and Display Requirements](use-display-requirements.md).</span></span>

<span data-ttu-id="8bdf3-123">You, or a third party on your behalf, may not use, retain, store, cache, share, or distribute any data from the URL Preview API for the purpose of testing, developing, training, distributing or making available any non-Microsoft service or feature.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-123">You, or a third party on your behalf, may not use, retain, store, cache, share, or distribute any data from the URL Preview API for the purpose of testing, developing, training, distributing or making available any non-Microsoft service or feature.</span></span> 

## <a name="throttling-requests"></a><span data-ttu-id="8bdf3-124">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="8bdf3-124">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../../includes/cognitive-services-bing-throttling-requests.md)]


## <a name="data-attribution"></a><span data-ttu-id="8bdf3-125">Data attribution</span><span class="sxs-lookup"><span data-stu-id="8bdf3-125">Data attribution</span></span>  

<span data-ttu-id="8bdf3-126">Project Answer Search responses contain information owned by third parties.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-126">Project Answer Search responses contain information owned by third parties.</span></span> <span data-ttu-id="8bdf3-127">You are responsible to ensure your use is appropriate, for example by complying with any creative commons license your user experience may rely on.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-127">You are responsible to ensure your use is appropriate, for example by complying with any creative commons license your user experience may rely on.</span></span>  
  
<span data-ttu-id="8bdf3-128">If an answer or result includes the `contractualRules`, `attributions`, or `provider` fields, you must attribute the data.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-128">If an answer or result includes the `contractualRules`, `attributions`, or `provider` fields, you must attribute the data.</span></span> <span data-ttu-id="8bdf3-129">If the answer does not include any of these fields, no attribution is required.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-129">If the answer does not include any of these fields, no attribution is required.</span></span> <span data-ttu-id="8bdf3-130">If the answer includes the `contractualRules` field and the `attributions` and/or `provider` fields, you must use the contractual rules to attribute the data.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-130">If the answer includes the `contractualRules` field and the `attributions` and/or `provider` fields, you must use the contractual rules to attribute the data.</span></span>  
  
<span data-ttu-id="8bdf3-131">The following example shows an entity that includes a MediaAttribution contractual rule and an Image that includes a `provider` field.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-131">The following example shows an entity that includes a MediaAttribution contractual rule and an Image that includes a `provider` field.</span></span> <span data-ttu-id="8bdf3-132">The MediaAttribution rule identifies the image as the target of the rule, so you'd ignore the image's `provider` field and instead use the MediaAttribution rule to provide attribution.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-132">The MediaAttribution rule identifies the image as the target of the rule, so you'd ignore the image's `provider` field and instead use the MediaAttribution rule to provide attribution.</span></span>  
  
```  
        "value" : [{
            "contractualRules" : [
                . . .
                {
                    "_type" : "ContractualRules\/MediaAttribution",
                    "targetPropertyName" : "image",
                    "mustBeCloseToContent" : true,
                    "url" : "http:\/\/en.wikipedia.org\/wiki\/Space_Needle"
                }
            ],
            . . .
            "image" : {
                "name" : "Space Needle",
                "thumbnailUrl" : "https:\/\/www.bing.com\/th?id=A46378861201...",
                "provider" : [{
                    "_type" : "Organization",
                    "url" : "http:\/\/en.wikipedia.org\/wiki\/Space_Needle"
                }],
                "hostPageUrl" : "http:\/\/www.citydictionary.com\/Uploaded...",
                "width" : 110,
                "height" : 110
            },
            . . .
        }]
```  
  
<span data-ttu-id="8bdf3-133">If a contractual rule includes the `targetPropertyName` field, the rule applies only to the targeted field.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-133">If a contractual rule includes the `targetPropertyName` field, the rule applies only to the targeted field.</span></span> <span data-ttu-id="8bdf3-134">Otherwise, the rule applies to the parent object that contains the `contractualRules` field.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-134">Otherwise, the rule applies to the parent object that contains the `contractualRules` field.</span></span>  
  
  
<span data-ttu-id="8bdf3-135">In the following example, the `LinkAttribution` rule includes the `targetPropertyName` field, so the rule applies to the `description` field.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-135">In the following example, the `LinkAttribution` rule includes the `targetPropertyName` field, so the rule applies to the `description` field.</span></span> <span data-ttu-id="8bdf3-136">For rules that apply to specific fields, you must include a line immediately following the targeted data that contains a hyperlink to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-136">For rules that apply to specific fields, you must include a line immediately following the targeted data that contains a hyperlink to the provider's website.</span></span> <span data-ttu-id="8bdf3-137">For example, to attribute the description, include a line immediately following the description text that contains a hyperlink to the data on the provider's website, in this case create a link to en.wikipedia.org.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-137">For example, to attribute the description, include a line immediately following the description text that contains a hyperlink to the data on the provider's website, in this case create a link to en.wikipedia.org.</span></span>  
  
```  
"entities" : {  
    "value" : [{  
            . . .  
            "description" : "Peyton Williams Manning is a former American....",  
            . . .  
            "contractualRules" : [{  
                    "_type" : "ContractualRules\/LinkAttribution",  
                    "targetPropertyName" : "description",  
                    "mustBeCloseToContent" : true,  
                    "text" : "en.wikipedia.org",  
                    "url" : "http:\/\/www.bing.com\/cr?IG=B8AD73..."  
                 },  
            . . .  
  
```  

### <a name="license-attribution"></a><span data-ttu-id="8bdf3-138">License Attribution</span><span class="sxs-lookup"><span data-stu-id="8bdf3-138">License Attribution</span></span>  

<span data-ttu-id="8bdf3-139">If the list of contractual rules includes a [LicenseAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#licenseattribution) rule, you must display the notice on the line immediately following the content that the license applies to.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-139">If the list of contractual rules includes a [LicenseAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#licenseattribution) rule, you must display the notice on the line immediately following the content that the license applies to.</span></span> <span data-ttu-id="8bdf3-140">The `LicenseAttribution` rule uses the `targetPropertyName` field to identify the property that the license applies to.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-140">The `LicenseAttribution` rule uses the `targetPropertyName` field to identify the property that the license applies to.</span></span>  
  
<span data-ttu-id="8bdf3-141">The following shows an example that includes a `LicenseAttribution` rule.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-141">The following shows an example that includes a `LicenseAttribution` rule.</span></span>  
  
![License attribution](./media/licenseattribution.png)  
  
<span data-ttu-id="8bdf3-143">The license notice that you display must include a hyperlink to the website that contains information about the license.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-143">The license notice that you display must include a hyperlink to the website that contains information about the license.</span></span> <span data-ttu-id="8bdf3-144">Typically, you make the name of the license a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-144">Typically, you make the name of the license a hyperlink.</span></span> <span data-ttu-id="8bdf3-145">For example, if the notice is **Text under CC-BY-SA license** and CC-BY-SA is the name of the license, you would make CC-BY-SA a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-145">For example, if the notice is **Text under CC-BY-SA license** and CC-BY-SA is the name of the license, you would make CC-BY-SA a hyperlink.</span></span>  
  
### <a name="link-and-text-attribution"></a><span data-ttu-id="8bdf3-146">Link and Text Attribution</span><span class="sxs-lookup"><span data-stu-id="8bdf3-146">Link and Text Attribution</span></span>  

<span data-ttu-id="8bdf3-147">The [LinkAttribution](reference.md#linkattribution) and [TextAttribution](reference.md#textattribution) rules are typically used to identify the provider of the data.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-147">The [LinkAttribution](reference.md#linkattribution) and [TextAttribution](reference.md#textattribution) rules are typically used to identify the provider of the data.</span></span> <span data-ttu-id="8bdf3-148">The `targetPropertyName` field identifies the field that the rule applies to.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-148">The `targetPropertyName` field identifies the field that the rule applies to.</span></span>  
  
<span data-ttu-id="8bdf3-149">To attribute the providers, include a line immediately following the content that the attributions apply to (for example, the targeted field).</span><span class="sxs-lookup"><span data-stu-id="8bdf3-149">To attribute the providers, include a line immediately following the content that the attributions apply to (for example, the targeted field).</span></span> <span data-ttu-id="8bdf3-150">The line should be clearly labeled to indicate that the providers are the source of the data.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-150">The line should be clearly labeled to indicate that the providers are the source of the data.</span></span> <span data-ttu-id="8bdf3-151">For example, "Data from: en.wikipedia.org".</span><span class="sxs-lookup"><span data-stu-id="8bdf3-151">For example, "Data from: en.wikipedia.org".</span></span> <span data-ttu-id="8bdf3-152">For `LinkAttribution` rules, you must create a hyperlink to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-152">For `LinkAttribution` rules, you must create a hyperlink to the provider's website.</span></span>  
  
<span data-ttu-id="8bdf3-153">The following shows an example that includes `LinkAttribution` and `TextAttribution` rules.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-153">The following shows an example that includes `LinkAttribution` and `TextAttribution` rules.</span></span>  
  
![Link text attribution](./media/linktextattribution.png)  

### <a name="media-attribution"></a><span data-ttu-id="8bdf3-155">Media Attribution</span><span class="sxs-lookup"><span data-stu-id="8bdf3-155">Media Attribution</span></span>  

<span data-ttu-id="8bdf3-156">If the entity includes an image and you display it, you must provide a click-through link to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-156">If the entity includes an image and you display it, you must provide a click-through link to the provider's website.</span></span> <span data-ttu-id="8bdf3-157">If the entity includes a [MediaAttribution](reference.md#mediaattribution) rule, use the rule's URL to create the click-through link.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-157">If the entity includes a [MediaAttribution](reference.md#mediaattribution) rule, use the rule's URL to create the click-through link.</span></span> <span data-ttu-id="8bdf3-158">Otherwise, use the URL included in the image's `provider` field to create the click-through link.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-158">Otherwise, use the URL included in the image's `provider` field to create the click-through link.</span></span>  
  
<span data-ttu-id="8bdf3-159">The following shows an example that includes an image's `provider` field and contractual rules.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-159">The following shows an example that includes an image's `provider` field and contractual rules.</span></span> <span data-ttu-id="8bdf3-160">Because the example includes the contractual rule, you will ignore the image's `provider` field and apply the `MediaAttribution` rule.</span><span class="sxs-lookup"><span data-stu-id="8bdf3-160">Because the example includes the contractual rule, you will ignore the image's `provider` field and apply the `MediaAttribution` rule.</span></span>  
  
![Media attribution](./media/mediaattribution.png)  

## <a name="next-steps"></a><span data-ttu-id="8bdf3-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bdf3-162">Next steps</span></span>
- [<span data-ttu-id="8bdf3-163">C# quickstart</span><span class="sxs-lookup"><span data-stu-id="8bdf3-163">C# quickstart</span></span>](c-sharp-quickstart.md)
- [<span data-ttu-id="8bdf3-164">Java quickstart</span><span class="sxs-lookup"><span data-stu-id="8bdf3-164">Java quickstart</span></span>](java-quickstart.md)
- [<span data-ttu-id="8bdf3-165">Node quickstart</span><span class="sxs-lookup"><span data-stu-id="8bdf3-165">Node quickstart</span></span>](node-quickstart.md)
- [<span data-ttu-id="8bdf3-166">Python quickstart</span><span class="sxs-lookup"><span data-stu-id="8bdf3-166">Python quickstart</span></span>](python-quickstart.md)
