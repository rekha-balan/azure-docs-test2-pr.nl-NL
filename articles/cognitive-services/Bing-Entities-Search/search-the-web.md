---
title: What is Bing Entity Search? | Microsoft Docs
description: Learn how to use the Bing Entity Search API to search the web for entities and places.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: 0B54E747-61BF-42AA-8788-E25D63F625FC
ms.service: cognitive-services
ms.component: bing-entity-search
ms.topic: article
ms.date: 07/06/2016
ms.author: scottwhi
ms.openlocfilehash: 275430bc6ee8f935978243e61f68713974648189
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855570"
---
# <a name="what-is-bing-entity-search"></a><span data-ttu-id="602a4-104">What is Bing Entity Search?</span><span class="sxs-lookup"><span data-stu-id="602a4-104">What is Bing Entity Search?</span></span>

<span data-ttu-id="602a4-105">The Bing Entity Search API sends a search query to Bing and gets results that include entities and places.</span><span class="sxs-lookup"><span data-stu-id="602a4-105">The Bing Entity Search API sends a search query to Bing and gets results that include entities and places.</span></span> <span data-ttu-id="602a4-106">Place results include restaurants, hotel, or other local businesses.</span><span class="sxs-lookup"><span data-stu-id="602a4-106">Place results include restaurants, hotel, or other local businesses.</span></span> <span data-ttu-id="602a4-107">Bing returns places if the query specifies the name of the local business or asks for a type of business (for example, restaurants near me).</span><span class="sxs-lookup"><span data-stu-id="602a4-107">Bing returns places if the query specifies the name of the local business or asks for a type of business (for example, restaurants near me).</span></span> <span data-ttu-id="602a4-108">Bing returns entities if the query specifies well-known people, places (tourist attractions, states, countries, etc.), or things.</span><span class="sxs-lookup"><span data-stu-id="602a4-108">Bing returns entities if the query specifies well-known people, places (tourist attractions, states, countries, etc.), or things.</span></span>

## <a name="suggesting--using-search-terms"></a><span data-ttu-id="602a4-109">Suggesting & using search terms</span><span class="sxs-lookup"><span data-stu-id="602a4-109">Suggesting & using search terms</span></span>

<span data-ttu-id="602a4-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span><span class="sxs-lookup"><span data-stu-id="602a4-110">If you provide a search box where the user enters their search term, use the [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md) to improve the experience.</span></span> <span data-ttu-id="602a4-111">The API returns suggested query strings based on partial search terms as the user types.</span><span class="sxs-lookup"><span data-stu-id="602a4-111">The API returns suggested query strings based on partial search terms as the user types.</span></span>

<span data-ttu-id="602a4-112">After the user enters their search term, URL encode the term before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query) query parameter.</span><span class="sxs-lookup"><span data-stu-id="602a4-112">After the user enters their search term, URL encode the term before setting the [q](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#query) query parameter.</span></span> <span data-ttu-id="602a4-113">For example, if the user enters *Marcus Appel*, set `q` to *Marcus+Appel* or *Marcus%20Appel*.</span><span class="sxs-lookup"><span data-stu-id="602a4-113">For example, if the user enters *Marcus Appel*, set `q` to *Marcus+Appel* or *Marcus%20Appel*.</span></span>

<span data-ttu-id="602a4-114">If the search term contains a spelling mistake, the search response includes a [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#querycontext) object.</span><span class="sxs-lookup"><span data-stu-id="602a4-114">If the search term contains a spelling mistake, the search response includes a [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#querycontext) object.</span></span> <span data-ttu-id="602a4-115">The object shows the original spelling and the corrected spelling that Bing used for the search.</span><span class="sxs-lookup"><span data-stu-id="602a4-115">The object shows the original spelling and the corrected spelling that Bing used for the search.</span></span>

```json
"queryContext": {
    "originalQuery": "hollo wrld",
    "alteredQuery": "hello world",
    "alterationOverrideQuery": "+hollo wrld",
    "adultIntent": false
}
```

## <a name="requesting-entities"></a><span data-ttu-id="602a4-116">Requesting entities</span><span class="sxs-lookup"><span data-stu-id="602a4-116">Requesting entities</span></span>

<span data-ttu-id="602a4-117">For an example request, see [Making your first request](./quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="602a4-117">For an example request, see [Making your first request](./quick-start.md).</span></span>

## <a name="the-response"></a><span data-ttu-id="602a4-118">The response</span><span class="sxs-lookup"><span data-stu-id="602a4-118">The response</span></span>

<span data-ttu-id="602a4-119">The response contains a [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#searchresponse) object.</span><span class="sxs-lookup"><span data-stu-id="602a4-119">The response contains a [SearchResponse](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#searchresponse) object.</span></span> <span data-ttu-id="602a4-120">If Bing finds an entity or place that's relevant, the object includes the `entities` field, `places` field, or both.</span><span class="sxs-lookup"><span data-stu-id="602a4-120">If Bing finds an entity or place that's relevant, the object includes the `entities` field, `places` field, or both.</span></span> <span data-ttu-id="602a4-121">Otherwise, the response object does not include either field.</span><span class="sxs-lookup"><span data-stu-id="602a4-121">Otherwise, the response object does not include either field.</span></span>
> [!NOTE]
> <span data-ttu-id="602a4-122">Entity responses support multiple markets, but the Places response supports only US Business locations.</span><span class="sxs-lookup"><span data-stu-id="602a4-122">Entity responses support multiple markets, but the Places response supports only US Business locations.</span></span> 

<span data-ttu-id="602a4-123">The `entities` field is an [EntityAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entityanswer) object that contains a list of [Entity](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity) objects (see the `value` field).</span><span class="sxs-lookup"><span data-stu-id="602a4-123">The `entities` field is an [EntityAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entityanswer) object that contains a list of [Entity](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity) objects (see the `value` field).</span></span> <span data-ttu-id="602a4-124">The list may contain a single dominant entity, multiple disambiguation entities, or both.</span><span class="sxs-lookup"><span data-stu-id="602a4-124">The list may contain a single dominant entity, multiple disambiguation entities, or both.</span></span> 

<span data-ttu-id="602a4-125">A dominant entity is an entity that Bing believes is the only entity that satisfies the request (there is no ambiguity as to which entity satisfies the request).</span><span class="sxs-lookup"><span data-stu-id="602a4-125">A dominant entity is an entity that Bing believes is the only entity that satisfies the request (there is no ambiguity as to which entity satisfies the request).</span></span> <span data-ttu-id="602a4-126">If multiple entities could satisfy the request, the list contains more than one disambiguation entity.</span><span class="sxs-lookup"><span data-stu-id="602a4-126">If multiple entities could satisfy the request, the list contains more than one disambiguation entity.</span></span> <span data-ttu-id="602a4-127">For example, if the request uses the generic title of a movie franchise, the list likely contains disambiguation entities.</span><span class="sxs-lookup"><span data-stu-id="602a4-127">For example, if the request uses the generic title of a movie franchise, the list likely contains disambiguation entities.</span></span> <span data-ttu-id="602a4-128">But, if the request specifies a specific title from the franchise, the list likely contains a single dominant entity.</span><span class="sxs-lookup"><span data-stu-id="602a4-128">But, if the request specifies a specific title from the franchise, the list likely contains a single dominant entity.</span></span>

<span data-ttu-id="602a4-129">Entities include well-known personalities such as singers, actors, athletes, models, etc.; places and landmarks such as Mount Rainier or Lincoln Memorial; and things such as a banana, goldendoodle, book, or movie title.</span><span class="sxs-lookup"><span data-stu-id="602a4-129">Entities include well-known personalities such as singers, actors, athletes, models, etc.; places and landmarks such as Mount Rainier or Lincoln Memorial; and things such as a banana, goldendoodle, book, or movie title.</span></span> <span data-ttu-id="602a4-130">The [entityPresentationInfo](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entitypresentationinfo) field contains hints that identify the entity's type.</span><span class="sxs-lookup"><span data-stu-id="602a4-130">The [entityPresentationInfo](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entitypresentationinfo) field contains hints that identify the entity's type.</span></span> <span data-ttu-id="602a4-131">For example, if it's a person, movie, animal, or attraction.</span><span class="sxs-lookup"><span data-stu-id="602a4-131">For example, if it's a person, movie, animal, or attraction.</span></span> <span data-ttu-id="602a4-132">For a list of possible types, see [Entity Types](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity-types)</span><span class="sxs-lookup"><span data-stu-id="602a4-132">For a list of possible types, see [Entity Types](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity-types)</span></span>

```json
"entityPresentationInfo": {
    "entityScenario": "DominantEntity",
    "entityTypeHints": ["Attraction"],
    "entityTypeDisplayHint": "Mountain"
}, ...
```

<span data-ttu-id="602a4-133">The following shows a response that includes a dominant and disambiguation entity.</span><span class="sxs-lookup"><span data-stu-id="602a4-133">The following shows a response that includes a dominant and disambiguation entity.</span></span>

```json
{
    "_type": "SearchResponse",
    "queryContext": {
        "originalQuery": "Mount Rainier"
    },
    "entities": {
        "value": [{
            "contractualRules": [{
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
                "text": "contoso.com",
                "url": "http://contoso.com/mount_rainier"
            },
            {
                "_type": "ContractualRules/MediaAttribution",
                "targetPropertyName": "image",
                "mustBeCloseToContent": true,
                "url": "http://contoso.com/mount-rainier"
            }],
            "webSearchUrl": "https://www.bing.com/search?q=Mount%20Rainier...",
            "name": "Mount Rainier",
            "url": "http://www.northwindtraders.com/",
            "image": {
                "name": "Mount Rainier",
                "thumbnailUrl": "https://www.bing.com/th?id=A4ae343983daa4...",
                "provider": [{
                    "_type": "Organization",
                    "url": "http://contoso.com/mount_rainier"
                }],
                "hostPageUrl": "http://contoso.com/commons/7/72/mount_rain...",
                "width": 110,
                "height": 110
            },
            "description": "Mount Rainier is 14,411 ft tall and the highest mountain...",
            "entityPresentationInfo": {
                "entityScenario": "DominantEntity",
                "entityTypeHints": ["Attraction"]
            },
            "bingId": "38b9431e-cf91-93be-0584-c42a3ecbfdc7"
        },
        {
            "contractualRules": [{
                "_type": "ContractualRules/MediaAttribution",
                "targetPropertyName": "image",
                "mustBeCloseToContent": true,
                "url": "http://contoso.com/mount_rainier_national_park"
            }],
            "webSearchUrl": "https://www.bing.com/search?q=Mount%20Rainier%20National...",
            "name": "Mount Rainier National Park",
            "url": "http://worldwideimporters.com/",
            "image": {
                "name": "Mount Rainier National Park",
                "thumbnailUrl": "https://www.bing.com/th?id=A91bdc5a1b648a695a39...",
                "provider": [{
                    "_type": "Organization",
                    "url": "http://contoso.com/mount_rainier_national_park"
                }],
                "hostPageUrl": "http://contoso.com/en/7/7a...",
                "width": 50,
                "height": 50
            },
            "description": "Mount Rainier National Park is a United States National Park...",
            "entityPresentationInfo": {
                "entityScenario": "DisambiguationItem",
                "entityTypeHints": ["Organization"]
            },
            "bingId": "29d4b681-227a-3924-7bb1-8a54e8666b8c"
        }]
    }
}
```

<span data-ttu-id="602a4-134">The entity includes a `name`, `description`, and `image` field.</span><span class="sxs-lookup"><span data-stu-id="602a4-134">The entity includes a `name`, `description`, and `image` field.</span></span> <span data-ttu-id="602a4-135">When you display these fields in your user experience, you must attribute them.</span><span class="sxs-lookup"><span data-stu-id="602a4-135">When you display these fields in your user experience, you must attribute them.</span></span> <span data-ttu-id="602a4-136">The `contractualRules` field contains a list of attributions that you must apply.</span><span class="sxs-lookup"><span data-stu-id="602a4-136">The `contractualRules` field contains a list of attributions that you must apply.</span></span> <span data-ttu-id="602a4-137">The contractual rule identifies the field that the attribution applies to.</span><span class="sxs-lookup"><span data-stu-id="602a4-137">The contractual rule identifies the field that the attribution applies to.</span></span> <span data-ttu-id="602a4-138">For information about applying attribution, see [Attribution](#data-attribution).</span><span class="sxs-lookup"><span data-stu-id="602a4-138">For information about applying attribution, see [Attribution](#data-attribution).</span></span>

```json
"contractualRules": [{
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
    "text": "contoso.com",
    "url": "http://contoso.com/wiki/Mount_Rainier"
},
{
    "_type": "ContractualRules/MediaAttribution",
    "targetPropertyName": "image",
    "mustBeCloseToContent": true,
    "url": "http://contoso.com/wiki/Mount_Rainier"
}], ...
```

<span data-ttu-id="602a4-139">When you display the entity information (name, description, and image), you must also use the URL in the `webSearchUrl` field to link to the Bing search results page that contains the entity.</span><span class="sxs-lookup"><span data-stu-id="602a4-139">When you display the entity information (name, description, and image), you must also use the URL in the `webSearchUrl` field to link to the Bing search results page that contains the entity.</span></span>


<span data-ttu-id="602a4-140">The `places` field is a [LocalEntityAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#localentityanswer) object that contains a list of [Place](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#place) objects (see the `value` field).</span><span class="sxs-lookup"><span data-stu-id="602a4-140">The `places` field is a [LocalEntityAnswer](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#localentityanswer) object that contains a list of [Place](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#place) objects (see the `value` field).</span></span> <span data-ttu-id="602a4-141">The list contains one or more local entities that satisfy the request.</span><span class="sxs-lookup"><span data-stu-id="602a4-141">The list contains one or more local entities that satisfy the request.</span></span>

<span data-ttu-id="602a4-142">Places include restaurant, hotels, or local businesses.</span><span class="sxs-lookup"><span data-stu-id="602a4-142">Places include restaurant, hotels, or local businesses.</span></span> <span data-ttu-id="602a4-143">The [entityPresentationInfo](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entitypresentationinfo) field contains hints that identify the local entity's type.</span><span class="sxs-lookup"><span data-stu-id="602a4-143">The [entityPresentationInfo](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entitypresentationinfo) field contains hints that identify the local entity's type.</span></span> <span data-ttu-id="602a4-144">The list contains a list of hints such as Place, LocalBusiness, Restaurant.</span><span class="sxs-lookup"><span data-stu-id="602a4-144">The list contains a list of hints such as Place, LocalBusiness, Restaurant.</span></span> <span data-ttu-id="602a4-145">Each successive hint in the array narrows the entity's type.</span><span class="sxs-lookup"><span data-stu-id="602a4-145">Each successive hint in the array narrows the entity's type.</span></span> <span data-ttu-id="602a4-146">For a list of possible types, see [Entity Types](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity-types)</span><span class="sxs-lookup"><span data-stu-id="602a4-146">For a list of possible types, see [Entity Types](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#entity-types)</span></span>

```json
"entityPresentationInfo": {
    "entityScenario": "ListItem",
    "entityTypeHints": ["Place",
    "LocalBusiness",
    "Restaurant"]
}, ...
```
> [!NOTE]
> <span data-ttu-id="602a4-147">Entity responses support multiple markets, but the Places response supports only US Business locations.</span><span class="sxs-lookup"><span data-stu-id="602a4-147">Entity responses support multiple markets, but the Places response supports only US Business locations.</span></span> 

<span data-ttu-id="602a4-148">Local aware entity queries such as *restaurant near me* require the user's location to provide accurate results.</span><span class="sxs-lookup"><span data-stu-id="602a4-148">Local aware entity queries such as *restaurant near me* require the user's location to provide accurate results.</span></span> <span data-ttu-id="602a4-149">Your requests should always use the X-Search-Location and X-MSEdge-ClientIP headers to specify the user's location.</span><span class="sxs-lookup"><span data-stu-id="602a4-149">Your requests should always use the X-Search-Location and X-MSEdge-ClientIP headers to specify the user's location.</span></span> <span data-ttu-id="602a4-150">If Bing thinks the query would benefit from the user's location, it sets the `askUserForLocation` field of [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#querycontext) to **true**.</span><span class="sxs-lookup"><span data-stu-id="602a4-150">If Bing thinks the query would benefit from the user's location, it sets the `askUserForLocation` field of [QueryContext](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#querycontext) to **true**.</span></span> 

```json
{
    "_type": "SearchResponse",
    "queryContext": {
        "originalQuery": "Sinful Bakery and Cafe",
        "askUserForLocation": true
    },
    ...
}
```

<span data-ttu-id="602a4-151">A place result includes the place's name, address, telephone number, and URL to the entity's website.</span><span class="sxs-lookup"><span data-stu-id="602a4-151">A place result includes the place's name, address, telephone number, and URL to the entity's website.</span></span> <span data-ttu-id="602a4-152">When you display the entity information, you must also use the URL in the `webSearchUrl` field to link to the Bing search results page that contains the entity.</span><span class="sxs-lookup"><span data-stu-id="602a4-152">When you display the entity information, you must also use the URL in the `webSearchUrl` field to link to the Bing search results page that contains the entity.</span></span>

```json
"places": {
    "value": [{
        "_type": "Restaurant",
        "webSearchUrl": "https://www.bing.com/search?q=Sinful%20Bakery...",
        "name": "Liberty's Delightful Sinful Bakery & Cafe",
        "url": "http://libertysdelightfulsinfulbakeryandcafe.com/",
        "entityPresentationInfo": {
            "entityScenario": "ListItem",
            "entityTypeHints": ["Place",
            "LocalBusiness",
            "Restaurant"]
        },
        "address": {
            "addressLocality": "Seattle",
            "addressRegion": "WA",
            "postalCode": "98112",
            "addressCountry": "US",
            "neighborhood": "Madison Park"
        },
        "telephone": "(800) 555-1212"
    }]
}
```

> [!NOTE]
> <span data-ttu-id="602a4-153">You, or a third party on your behalf, may not use, retain, store, cache, share, or distribute any data from the Entities API for the purpose of testing, developing, training, distributing or making available any non-Microsoft service or feature.</span><span class="sxs-lookup"><span data-stu-id="602a4-153">You, or a third party on your behalf, may not use, retain, store, cache, share, or distribute any data from the Entities API for the purpose of testing, developing, training, distributing or making available any non-Microsoft service or feature.</span></span>  

## <a name="data-attribution"></a><span data-ttu-id="602a4-154">Data attribution</span><span class="sxs-lookup"><span data-stu-id="602a4-154">Data attribution</span></span>

<span data-ttu-id="602a4-155">Bing Entity API responses contain information owned by third parties.</span><span class="sxs-lookup"><span data-stu-id="602a4-155">Bing Entity API responses contain information owned by third parties.</span></span> <span data-ttu-id="602a4-156">You are responsible to ensure your use is appropriate, for example by complying with any creative commons license your user experience may rely on.</span><span class="sxs-lookup"><span data-stu-id="602a4-156">You are responsible to ensure your use is appropriate, for example by complying with any creative commons license your user experience may rely on.</span></span>

<span data-ttu-id="602a4-157">If an answer or result includes the `contractualRules`, `attributions`, or `provider` fields, you must attribute the data.</span><span class="sxs-lookup"><span data-stu-id="602a4-157">If an answer or result includes the `contractualRules`, `attributions`, or `provider` fields, you must attribute the data.</span></span> <span data-ttu-id="602a4-158">If the answer does not include any of these fields, no attribution is required.</span><span class="sxs-lookup"><span data-stu-id="602a4-158">If the answer does not include any of these fields, no attribution is required.</span></span> <span data-ttu-id="602a4-159">If the answer includes the `contractualRules` field and the `attributions` and/or `provider` fields, you must use the contractual rules to attribute the data.</span><span class="sxs-lookup"><span data-stu-id="602a4-159">If the answer includes the `contractualRules` field and the `attributions` and/or `provider` fields, you must use the contractual rules to attribute the data.</span></span>

<span data-ttu-id="602a4-160">The following example shows an entity that includes a MediaAttribution contractual rule and an Image that includes a `provider` field.</span><span class="sxs-lookup"><span data-stu-id="602a4-160">The following example shows an entity that includes a MediaAttribution contractual rule and an Image that includes a `provider` field.</span></span> <span data-ttu-id="602a4-161">The MediaAttribution rule identifies the image as the target of the rule, so you'd ignore the image's `provider` field and instead use the MediaAttribution rule to provide attribution.</span><span class="sxs-lookup"><span data-stu-id="602a4-161">The MediaAttribution rule identifies the image as the target of the rule, so you'd ignore the image's `provider` field and instead use the MediaAttribution rule to provide attribution.</span></span>  

```json
"value": [{
    "contractualRules": [
        ...
        {
            "_type": "ContractualRules/MediaAttribution",
            "targetPropertyName": "image",
            "mustBeCloseToContent": true,
            "url": "http://contoso.com/mount_rainier"
        }
    ],
    ...
    "image": {
        "name": "Mount Rainier",
        "thumbnailUrl": "https://www.bing.com/th?id=A46378861201...",
        "provider": [{
            "_type": "Organization",
            "url": "http://contoso.com/mount_rainier"
        }],
        "hostPageUrl": "http://www.graphicdesigninstitute.com/Uploaded...",
        "width": 110,
        "height": 110
    },
    ...
}]
```

<span data-ttu-id="602a4-162">If a contractual rule includes the `targetPropertyName` field, the rule applies only to the targeted field.</span><span class="sxs-lookup"><span data-stu-id="602a4-162">If a contractual rule includes the `targetPropertyName` field, the rule applies only to the targeted field.</span></span> <span data-ttu-id="602a4-163">Otherwise, the rule applies to the parent object that contains the `contractualRules` field.</span><span class="sxs-lookup"><span data-stu-id="602a4-163">Otherwise, the rule applies to the parent object that contains the `contractualRules` field.</span></span>

<span data-ttu-id="602a4-164">In the following example, the `LinkAttribution` rule includes the `targetPropertyName` field, so the rule applies to the `description` field.</span><span class="sxs-lookup"><span data-stu-id="602a4-164">In the following example, the `LinkAttribution` rule includes the `targetPropertyName` field, so the rule applies to the `description` field.</span></span> <span data-ttu-id="602a4-165">For rules that apply to specific fields, you must include a line immediately following the targeted data that contains a hyperlink to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="602a4-165">For rules that apply to specific fields, you must include a line immediately following the targeted data that contains a hyperlink to the provider's website.</span></span> <span data-ttu-id="602a4-166">For example, to attribute the description, include a line immediately following the description text that contains a hyperlink to the data on the provider's website, in this case create a link to contoso.com.</span><span class="sxs-lookup"><span data-stu-id="602a4-166">For example, to attribute the description, include a line immediately following the description text that contains a hyperlink to the data on the provider's website, in this case create a link to contoso.com.</span></span>

```json
"entities": {
    "value": [{
            ...
            "description": "Marcus Appel is a former American....",
            ...
            "contractualRules": [{
                    "_type": "ContractualRules/LinkAttribution",
                    "targetPropertyName": "description",
                    "mustBeCloseToContent": true,
                    "text": "contoso.com",
                    "url": "http://contoso.com/cr?IG=B8AD73..."
                 },
            ...
  
```

### <a name="license-attribution"></a><span data-ttu-id="602a4-167">License attribution</span><span class="sxs-lookup"><span data-stu-id="602a4-167">License attribution</span></span>

<span data-ttu-id="602a4-168">If the list of contractual rules includes a [LicenseAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#licenseattribution) rule, you must display the notice on the line immediately following the content that the license applies to.</span><span class="sxs-lookup"><span data-stu-id="602a4-168">If the list of contractual rules includes a [LicenseAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#licenseattribution) rule, you must display the notice on the line immediately following the content that the license applies to.</span></span> <span data-ttu-id="602a4-169">The `LicenseAttribution` rule uses the `targetPropertyName` field to identify the property that the license applies to.</span><span class="sxs-lookup"><span data-stu-id="602a4-169">The `LicenseAttribution` rule uses the `targetPropertyName` field to identify the property that the license applies to.</span></span>

<span data-ttu-id="602a4-170">The following shows an example that includes a `LicenseAttribution` rule.</span><span class="sxs-lookup"><span data-stu-id="602a4-170">The following shows an example that includes a `LicenseAttribution` rule.</span></span>

![License attribution](./media/cognitive-services-bing-entities-api/licenseattribution.png)

<span data-ttu-id="602a4-172">The license notice that you display must include a hyperlink to the website that contains information about the license.</span><span class="sxs-lookup"><span data-stu-id="602a4-172">The license notice that you display must include a hyperlink to the website that contains information about the license.</span></span> <span data-ttu-id="602a4-173">Typically, you make the name of the license a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="602a4-173">Typically, you make the name of the license a hyperlink.</span></span> <span data-ttu-id="602a4-174">For example, if the notice is **Text under CC-BY-SA license** and CC-BY-SA is the name of the license, you would make CC-BY-SA a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="602a4-174">For example, if the notice is **Text under CC-BY-SA license** and CC-BY-SA is the name of the license, you would make CC-BY-SA a hyperlink.</span></span>

### <a name="link-and-text-attribution"></a><span data-ttu-id="602a4-175">Link and text attribution</span><span class="sxs-lookup"><span data-stu-id="602a4-175">Link and text attribution</span></span>

<span data-ttu-id="602a4-176">The [LinkAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#linkattribution) and [TextAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#textattribution) rules are typically used to identify the provider of the data.</span><span class="sxs-lookup"><span data-stu-id="602a4-176">The [LinkAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#linkattribution) and [TextAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#textattribution) rules are typically used to identify the provider of the data.</span></span> <span data-ttu-id="602a4-177">The `targetPropertyName` field identifies the field that the rule applies to.</span><span class="sxs-lookup"><span data-stu-id="602a4-177">The `targetPropertyName` field identifies the field that the rule applies to.</span></span>

<span data-ttu-id="602a4-178">To attribute the providers, include a line immediately following the content that the attributions apply to (for example, the targeted field).</span><span class="sxs-lookup"><span data-stu-id="602a4-178">To attribute the providers, include a line immediately following the content that the attributions apply to (for example, the targeted field).</span></span> <span data-ttu-id="602a4-179">The line should be clearly labeled to indicate that the providers are the source of the data.</span><span class="sxs-lookup"><span data-stu-id="602a4-179">The line should be clearly labeled to indicate that the providers are the source of the data.</span></span> <span data-ttu-id="602a4-180">For example, "Data from: contoso.com".</span><span class="sxs-lookup"><span data-stu-id="602a4-180">For example, "Data from: contoso.com".</span></span> <span data-ttu-id="602a4-181">For `LinkAttribution` rules, you must create a hyperlink to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="602a4-181">For `LinkAttribution` rules, you must create a hyperlink to the provider's website.</span></span>

<span data-ttu-id="602a4-182">The following shows an example that includes `LinkAttribution` and `TextAttribution` rules.</span><span class="sxs-lookup"><span data-stu-id="602a4-182">The following shows an example that includes `LinkAttribution` and `TextAttribution` rules.</span></span>

![Link text attribution](./media/cognitive-services-bing-entities-api/linktextattribution.png)

### <a name="media-attribution"></a><span data-ttu-id="602a4-184">Media attribution</span><span class="sxs-lookup"><span data-stu-id="602a4-184">Media attribution</span></span>

<span data-ttu-id="602a4-185">If the entity includes an image and you display it, you must provide a click-through link to the provider's website.</span><span class="sxs-lookup"><span data-stu-id="602a4-185">If the entity includes an image and you display it, you must provide a click-through link to the provider's website.</span></span> <span data-ttu-id="602a4-186">If the entity includes a [MediaAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#mediaattribution) rule, use the rule's URL to create the click-through link.</span><span class="sxs-lookup"><span data-stu-id="602a4-186">If the entity includes a [MediaAttribution](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference#mediaattribution) rule, use the rule's URL to create the click-through link.</span></span> <span data-ttu-id="602a4-187">Otherwise, use the URL included in the image's `provider` field to create the click-through link.</span><span class="sxs-lookup"><span data-stu-id="602a4-187">Otherwise, use the URL included in the image's `provider` field to create the click-through link.</span></span>

<span data-ttu-id="602a4-188">The following shows an example that includes an image's `provider` field and contractual rules.</span><span class="sxs-lookup"><span data-stu-id="602a4-188">The following shows an example that includes an image's `provider` field and contractual rules.</span></span> <span data-ttu-id="602a4-189">Because the example includes the contractual rule, you ignore the image's `provider` field and apply the `MediaAttribution` rule.</span><span class="sxs-lookup"><span data-stu-id="602a4-189">Because the example includes the contractual rule, you ignore the image's `provider` field and apply the `MediaAttribution` rule.</span></span>

![Media attribution](./media/cognitive-services-bing-entities-api/mediaattribution.png)

### <a name="search-or-search-like-experience"></a><span data-ttu-id="602a4-191">Search or search-like experience</span><span class="sxs-lookup"><span data-stu-id="602a4-191">Search or search-like experience</span></span>

<span data-ttu-id="602a4-192">Just like with Bing Web Search API, the Bing Entity Search API may only be used as a result of a direct user query or search, or as a result of an action within an app or experience that logically can be interpreted as a user’s search request.</span><span class="sxs-lookup"><span data-stu-id="602a4-192">Just like with Bing Web Search API, the Bing Entity Search API may only be used as a result of a direct user query or search, or as a result of an action within an app or experience that logically can be interpreted as a user’s search request.</span></span> <span data-ttu-id="602a4-193">For illustration purposes, the following are some examples of acceptable search or search-like experiences.</span><span class="sxs-lookup"><span data-stu-id="602a4-193">For illustration purposes, the following are some examples of acceptable search or search-like experiences.</span></span>

- <span data-ttu-id="602a4-194">User enters a query directly into a search box in an app</span><span class="sxs-lookup"><span data-stu-id="602a4-194">User enters a query directly into a search box in an app</span></span>
- <span data-ttu-id="602a4-195">User selects specific text or image and requests “more information” or “additional information”</span><span class="sxs-lookup"><span data-stu-id="602a4-195">User selects specific text or image and requests “more information” or “additional information”</span></span>
- <span data-ttu-id="602a4-196">User asks a search bot about a particular topic</span><span class="sxs-lookup"><span data-stu-id="602a4-196">User asks a search bot about a particular topic</span></span>
- <span data-ttu-id="602a4-197">User dwells on a particular object or entity in a visual search type scenario</span><span class="sxs-lookup"><span data-stu-id="602a4-197">User dwells on a particular object or entity in a visual search type scenario</span></span>

<span data-ttu-id="602a4-198">If you are not sure if your experience can be considered a search-like experience, it is recommended that you check with Microsoft.</span><span class="sxs-lookup"><span data-stu-id="602a4-198">If you are not sure if your experience can be considered a search-like experience, it is recommended that you check with Microsoft.</span></span>

## <a name="throttling-requests"></a><span data-ttu-id="602a4-199">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="602a4-199">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="602a4-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="602a4-200">Next steps</span></span>

<span data-ttu-id="602a4-201">To get started quickly with your first request, see [Making Your First Request](./quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="602a4-201">To get started quickly with your first request, see [Making Your First Request](./quick-start.md).</span></span>

<span data-ttu-id="602a4-202">Familiarize yourself with the [Bing Entity Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference) reference.</span><span class="sxs-lookup"><span data-stu-id="602a4-202">Familiarize yourself with the [Bing Entity Search API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-entities-api-v7-reference) reference.</span></span> <span data-ttu-id="602a4-203">The reference contains the headers and query parameters that you use to request search results.</span><span class="sxs-lookup"><span data-stu-id="602a4-203">The reference contains the headers and query parameters that you use to request search results.</span></span> <span data-ttu-id="602a4-204">It also includes definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="602a4-204">It also includes definitions of the response objects.</span></span> 

<span data-ttu-id="602a4-205">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span><span class="sxs-lookup"><span data-stu-id="602a4-205">To improve your search box user experience, see [Bing Autosuggest API](../bing-autosuggest/get-suggested-search-terms.md).</span></span> <span data-ttu-id="602a4-206">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span><span class="sxs-lookup"><span data-stu-id="602a4-206">As the user enters their query term, you can call this API to get relevant query terms that were used by others.</span></span>

<span data-ttu-id="602a4-207">Be sure to read [Bing Use and Display Requirements](./use-display-requirements.md) so you don't break any of the rules about using the search results.</span><span class="sxs-lookup"><span data-stu-id="602a4-207">Be sure to read [Bing Use and Display Requirements](./use-display-requirements.md) so you don't break any of the rules about using the search results.</span></span>