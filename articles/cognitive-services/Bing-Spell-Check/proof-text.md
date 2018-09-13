---
title: Bing Spell Check API overview - Azure Cognitive Services  | Microsoft Docs
description: The Bing Spell Check API uses machine learning and statistical machine translation for contextual spell checking.
services: cognitive-services
author: noellelacharite
manager: nolachar
ms.assetid: 64ABDFD4-0118-4B6C-A592-68E5EDDB8491
ms.service: cognitive-services
ms.component: bing-spell-check
ms.topic: overview
ms.date: 05/03/2018
ms.author: nolachar
ms.openlocfilehash: 15c5f7eeb7d94d7e80533ee1fd12e33fa3bcd134
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870579"
---
# <a name="what-is-bing-spell-check-api"></a><span data-ttu-id="8f68e-103">What is Bing Spell Check API?</span><span class="sxs-lookup"><span data-stu-id="8f68e-103">What is Bing Spell Check API?</span></span>

<span data-ttu-id="8f68e-104">The Bing Spell Check API lets you perform contextual grammar and spell checking.</span><span class="sxs-lookup"><span data-stu-id="8f68e-104">The Bing Spell Check API lets you perform contextual grammar and spell checking.</span></span>

<span data-ttu-id="8f68e-105">What’s the difference between regular spell-checkers and Bing’s third-generation spell-checker?</span><span class="sxs-lookup"><span data-stu-id="8f68e-105">What’s the difference between regular spell-checkers and Bing’s third-generation spell-checker?</span></span> <span data-ttu-id="8f68e-106">Current spell-checkers rely on verifying spelling and grammar against dictionary-based rule sets, which get updated and expanded periodically.</span><span class="sxs-lookup"><span data-stu-id="8f68e-106">Current spell-checkers rely on verifying spelling and grammar against dictionary-based rule sets, which get updated and expanded periodically.</span></span> <span data-ttu-id="8f68e-107">In other words, the spell-checker is only as strong as the dictionary that supports it, and the editorial staff who supports the dictionary.</span><span class="sxs-lookup"><span data-stu-id="8f68e-107">In other words, the spell-checker is only as strong as the dictionary that supports it, and the editorial staff who supports the dictionary.</span></span> <span data-ttu-id="8f68e-108">You know this type of spell-checker from Microsoft Word and other word processors.</span><span class="sxs-lookup"><span data-stu-id="8f68e-108">You know this type of spell-checker from Microsoft Word and other word processors.</span></span>

<span data-ttu-id="8f68e-109">In contrast, Bing has developed a web-based spell-checker that leverages machine learning and statistical machine translation to dynamically train a constantly evolving and highly contextual algorithm.</span><span class="sxs-lookup"><span data-stu-id="8f68e-109">In contrast, Bing has developed a web-based spell-checker that leverages machine learning and statistical machine translation to dynamically train a constantly evolving and highly contextual algorithm.</span></span> <span data-ttu-id="8f68e-110">The spell-checker is based on a massive corpus of web searches and documents.</span><span class="sxs-lookup"><span data-stu-id="8f68e-110">The spell-checker is based on a massive corpus of web searches and documents.</span></span>

<span data-ttu-id="8f68e-111">This spell-checker can handle any word-processing scenario:</span><span class="sxs-lookup"><span data-stu-id="8f68e-111">This spell-checker can handle any word-processing scenario:</span></span>

- <span data-ttu-id="8f68e-112">Recognizes slang and informal language</span><span class="sxs-lookup"><span data-stu-id="8f68e-112">Recognizes slang and informal language</span></span>
- <span data-ttu-id="8f68e-113">Recognizes common name errors in context</span><span class="sxs-lookup"><span data-stu-id="8f68e-113">Recognizes common name errors in context</span></span>
- <span data-ttu-id="8f68e-114">Corrects word breaking issues with a single flag</span><span class="sxs-lookup"><span data-stu-id="8f68e-114">Corrects word breaking issues with a single flag</span></span>
- <span data-ttu-id="8f68e-115">Is able to correct homophones in context, and other difficult to spot errors</span><span class="sxs-lookup"><span data-stu-id="8f68e-115">Is able to correct homophones in context, and other difficult to spot errors</span></span>
- <span data-ttu-id="8f68e-116">Supports new brands, digital entertainment, and popular expressions as they emerge</span><span class="sxs-lookup"><span data-stu-id="8f68e-116">Supports new brands, digital entertainment, and popular expressions as they emerge</span></span>
- <span data-ttu-id="8f68e-117">Words that sound the same but differ in meaning and spelling, for example “see” and “sea.”</span><span class="sxs-lookup"><span data-stu-id="8f68e-117">Words that sound the same but differ in meaning and spelling, for example “see” and “sea.”</span></span>

## <a name="spell-check-modes"></a><span data-ttu-id="8f68e-118">Spell check modes</span><span class="sxs-lookup"><span data-stu-id="8f68e-118">Spell check modes</span></span>

<span data-ttu-id="8f68e-119">The API supports two proofing modes, `Proof` and `Spell`.</span><span class="sxs-lookup"><span data-stu-id="8f68e-119">The API supports two proofing modes, `Proof` and `Spell`.</span></span>  <span data-ttu-id="8f68e-120">Try examples [here](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/).</span><span class="sxs-lookup"><span data-stu-id="8f68e-120">Try examples [here](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/).</span></span>
### <a name="proof---for-documents-scenario"></a><span data-ttu-id="8f68e-121">Proof - for documents scenario</span><span class="sxs-lookup"><span data-stu-id="8f68e-121">Proof - for documents scenario</span></span>
<span data-ttu-id="8f68e-122">The default mode is `Proof`.</span><span class="sxs-lookup"><span data-stu-id="8f68e-122">The default mode is `Proof`.</span></span> <span data-ttu-id="8f68e-123">The `Proof` spelling mode provides the most comprehensive checks,  adding capitalization, basic punctuation, and other features to aid document creation.</span><span class="sxs-lookup"><span data-stu-id="8f68e-123">The `Proof` spelling mode provides the most comprehensive checks,  adding capitalization, basic punctuation, and other features to aid document creation.</span></span> <span data-ttu-id="8f68e-124">but it is available only in the en-US (English-United States), es-ES(Spanish), pt-BR(Portuguese) markets (Note: only in beta version for Spanish and Portuguese).</span><span class="sxs-lookup"><span data-stu-id="8f68e-124">but it is available only in the en-US (English-United States), es-ES(Spanish), pt-BR(Portuguese) markets (Note: only in beta version for Spanish and Portuguese).</span></span> <span data-ttu-id="8f68e-125">For all other markets, set the mode query parameter to Spell.</span><span class="sxs-lookup"><span data-stu-id="8f68e-125">For all other markets, set the mode query parameter to Spell.</span></span> 
<br /><br/><span data-ttu-id="8f68e-126">**NOTE:**   If the length of query text exceeds 4096, it will be truncated to 4096 characters, then get processed.</span><span class="sxs-lookup"><span data-stu-id="8f68e-126">**NOTE:**   If the length of query text exceeds 4096, it will be truncated to 4096 characters, then get processed.</span></span> 
### <a name="spell----for-web-searchesqueries-scenario"></a><span data-ttu-id="8f68e-127">Spell -  for web searches/queries scenario</span><span class="sxs-lookup"><span data-stu-id="8f68e-127">Spell -  for web searches/queries scenario</span></span>
<span data-ttu-id="8f68e-128">`Spell` is more aggressive in order to return better search results.</span><span class="sxs-lookup"><span data-stu-id="8f68e-128">`Spell` is more aggressive in order to return better search results.</span></span> <span data-ttu-id="8f68e-129">The `Spell` mode finds most spelling mistakes but doesn't find some of the grammar errors that `Proof` catches, for example, capitalization and repeated words.</span><span class="sxs-lookup"><span data-stu-id="8f68e-129">The `Spell` mode finds most spelling mistakes but doesn't find some of the grammar errors that `Proof` catches, for example, capitalization and repeated words.</span></span>
<br /></br><span data-ttu-id="8f68e-130">**NOTE:** The max query length supported is as below.</span><span class="sxs-lookup"><span data-stu-id="8f68e-130">**NOTE:** The max query length supported is as below.</span></span> <span data-ttu-id="8f68e-131">If query exceed the bound, the result appears that the query is not altered.</span><span class="sxs-lookup"><span data-stu-id="8f68e-131">If query exceed the bound, the result appears that the query is not altered.</span></span>
<ul><li><span data-ttu-id="8f68e-132">130 characters for language code of en, de, es, fr, pl, pt, sv, ru, nl, nb, tr-tr, it, zh, ko.</span><span class="sxs-lookup"><span data-stu-id="8f68e-132">130 characters for language code of en, de, es, fr, pl, pt, sv, ru, nl, nb, tr-tr, it, zh, ko.</span></span> </li>
<li><span data-ttu-id="8f68e-133">65 characters for others</span><span class="sxs-lookup"><span data-stu-id="8f68e-133">65 characters for others</span></span></li></ul>

## <a name="market-setting"></a><span data-ttu-id="8f68e-134">Market setting</span><span class="sxs-lookup"><span data-stu-id="8f68e-134">Market setting</span></span>
<span data-ttu-id="8f68e-135">Market needs to be specified in the query parameter in request URL, otherwise speller will take the default market based on IP address.</span><span class="sxs-lookup"><span data-stu-id="8f68e-135">Market needs to be specified in the query parameter in request URL, otherwise speller will take the default market based on IP address.</span></span>


## <a name="post-vs-get"></a><span data-ttu-id="8f68e-136">POST vs. GET</span><span class="sxs-lookup"><span data-stu-id="8f68e-136">POST vs. GET</span></span>

<span data-ttu-id="8f68e-137">The API supports either HTTP POST or HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="8f68e-137">The API supports either HTTP POST or HTTP GET.</span></span> <span data-ttu-id="8f68e-138">Which you use depends on the length of text you plan to proof.</span><span class="sxs-lookup"><span data-stu-id="8f68e-138">Which you use depends on the length of text you plan to proof.</span></span> <span data-ttu-id="8f68e-139">If the strings are always less than 1,500 characters, you'd use a GET.</span><span class="sxs-lookup"><span data-stu-id="8f68e-139">If the strings are always less than 1,500 characters, you'd use a GET.</span></span> <span data-ttu-id="8f68e-140">But if you want to support strings up to 10,000 characters, you'd use POST.</span><span class="sxs-lookup"><span data-stu-id="8f68e-140">But if you want to support strings up to 10,000 characters, you'd use POST.</span></span> <span data-ttu-id="8f68e-141">The text string may include any valid UTF-8 character.</span><span class="sxs-lookup"><span data-stu-id="8f68e-141">The text string may include any valid UTF-8 character.</span></span>

<span data-ttu-id="8f68e-142">The following example shows a POST request to check the spelling and grammar of a text string.</span><span class="sxs-lookup"><span data-stu-id="8f68e-142">The following example shows a POST request to check the spelling and grammar of a text string.</span></span> <span data-ttu-id="8f68e-143">The example includes the [mode](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#mode) query parameter for completeness (it could have been left out since `mode` defaults to Proof).</span><span class="sxs-lookup"><span data-stu-id="8f68e-143">The example includes the [mode](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#mode) query parameter for completeness (it could have been left out since `mode` defaults to Proof).</span></span> <span data-ttu-id="8f68e-144">The [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#text) query parameter contains the string to be proofed.</span><span class="sxs-lookup"><span data-stu-id="8f68e-144">The [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#text) query parameter contains the string to be proofed.</span></span>
  
```  
POST https://api.cognitive.microsoft.com/bing/v7.0/spellcheck?mode=proof&mkt=en-us HTTP/1.1  
Content-Type: application/x-www-form-urlencoded  
Content-Length: 47  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
 
text=when+its+your+turn+turn,+john,+come+runing  
``` 

<span data-ttu-id="8f68e-145">If you use HTTP GET, you'd include the `text` query parameter in the URL's query string</span><span class="sxs-lookup"><span data-stu-id="8f68e-145">If you use HTTP GET, you'd include the `text` query parameter in the URL's query string</span></span>
  
<span data-ttu-id="8f68e-146">The following shows the response to the previous request.</span><span class="sxs-lookup"><span data-stu-id="8f68e-146">The following shows the response to the previous request.</span></span> <span data-ttu-id="8f68e-147">The response contains a [SpellCheck](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#spellcheck) object.</span><span class="sxs-lookup"><span data-stu-id="8f68e-147">The response contains a [SpellCheck](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#spellcheck) object.</span></span> 
  
```  
{  
    "_type" : "SpellCheck",  
    "flaggedTokens" : [{  
        "offset" : 5,  
        "token" : "its",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "it's",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 25,  
        "token" : "john",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "John",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 19,  
        "token" : "turn",  
        "type" : "RepeatedToken",  
        "suggestions" : [{  
            "suggestion" : "",  
            "score" : 1  
        }]  
    },  
    {  
        "offset" : 35,  
        "token" : "runing",  
        "type" : "UnknownToken",  
        "suggestions" : [{  
            "suggestion" : "running",  
            "score" : 1  
        }]  
    }]  
}  
```  
  
<span data-ttu-id="8f68e-148">The [flaggedTokens](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#flaggedtokens) field lists the spelling and grammar errors that the API found in the [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#text) string.</span><span class="sxs-lookup"><span data-stu-id="8f68e-148">The [flaggedTokens](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#flaggedtokens) field lists the spelling and grammar errors that the API found in the [text](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference#text) string.</span></span> <span data-ttu-id="8f68e-149">The `token` field contains the word to be replaced.</span><span class="sxs-lookup"><span data-stu-id="8f68e-149">The `token` field contains the word to be replaced.</span></span> <span data-ttu-id="8f68e-150">You'd use the zero-based offset in the `offset` field to find the token in the `text` string.</span><span class="sxs-lookup"><span data-stu-id="8f68e-150">You'd use the zero-based offset in the `offset` field to find the token in the `text` string.</span></span> <span data-ttu-id="8f68e-151">You'd then replace the word at that location with the word in the `suggestion` field.</span><span class="sxs-lookup"><span data-stu-id="8f68e-151">You'd then replace the word at that location with the word in the `suggestion` field.</span></span> 

<span data-ttu-id="8f68e-152">If the `type` field is RepeatedToken, you'd still replace the token with `suggestion` but you'd also likely need to remove the trailing space.</span><span class="sxs-lookup"><span data-stu-id="8f68e-152">If the `type` field is RepeatedToken, you'd still replace the token with `suggestion` but you'd also likely need to remove the trailing space.</span></span>

## <a name="throttling-requests"></a><span data-ttu-id="8f68e-153">Throttling requests</span><span class="sxs-lookup"><span data-stu-id="8f68e-153">Throttling requests</span></span>

[!INCLUDE [cognitive-services-bing-throttling-requests](../../../includes/cognitive-services-bing-throttling-requests.md)]

## <a name="next-steps"></a><span data-ttu-id="8f68e-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f68e-154">Next steps</span></span>

<span data-ttu-id="8f68e-155">To get started quickly with your first request, see [Making Your First Request](quickstarts/csharp.md).</span><span class="sxs-lookup"><span data-stu-id="8f68e-155">To get started quickly with your first request, see [Making Your First Request](quickstarts/csharp.md).</span></span>

<span data-ttu-id="8f68e-156">Familiarize yourself with the [Bing Spell Check API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference).</span><span class="sxs-lookup"><span data-stu-id="8f68e-156">Familiarize yourself with the [Bing Spell Check API Reference](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference).</span></span> <span data-ttu-id="8f68e-157">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results, and the definitions of the response objects.</span><span class="sxs-lookup"><span data-stu-id="8f68e-157">The reference contains the list of endpoints, headers, and query parameters that you'd use to request search results, and the definitions of the response objects.</span></span> 

<span data-ttu-id="8f68e-158">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the results.</span><span class="sxs-lookup"><span data-stu-id="8f68e-158">Be sure to read [Bing Use and Display Requirements](./useanddisplayrequirements.md) so you don't break any of the rules about using the results.</span></span>
