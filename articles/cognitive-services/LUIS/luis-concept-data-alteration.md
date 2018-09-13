---
title: Data alteration concepts in LUIS - Lanuage Understanding
titleSuffix: Azure Cognitive Services
description: Learn how data can be changed before predictions in Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 03/26/2018
ms.author: diberry
ms.openlocfilehash: 2949f7afa5d04d9f7ea738ad6f7b9333bfaf958f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967864"
---
# <a name="data-alterations"></a><span data-ttu-id="5f17f-103">Data alterations</span><span class="sxs-lookup"><span data-stu-id="5f17f-103">Data alterations</span></span>
<span data-ttu-id="5f17f-104">LUIS provides ways to manipulate the utterance before or during the prediction.</span><span class="sxs-lookup"><span data-stu-id="5f17f-104">LUIS provides ways to manipulate the utterance before or during the prediction.</span></span> 

## <a name="correct-spelling-errors-in-utterance"></a><span data-ttu-id="5f17f-105">Correct spelling errors in utterance</span><span class="sxs-lookup"><span data-stu-id="5f17f-105">Correct spelling errors in utterance</span></span>
<span data-ttu-id="5f17f-106">LUIS uses [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) to correct spelling errors in the utterance.</span><span class="sxs-lookup"><span data-stu-id="5f17f-106">LUIS uses [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) to correct spelling errors in the utterance.</span></span> <span data-ttu-id="5f17f-107">LUIS needs the key associated with that service.</span><span class="sxs-lookup"><span data-stu-id="5f17f-107">LUIS needs the key associated with that service.</span></span> <span data-ttu-id="5f17f-108">Create the key, then add the key as a querystring parameter at the [endpoint](https://aka.ms/luis-endpoint-apis).</span><span class="sxs-lookup"><span data-stu-id="5f17f-108">Create the key, then add the key as a querystring parameter at the [endpoint](https://aka.ms/luis-endpoint-apis).</span></span> 

<span data-ttu-id="5f17f-109">You can also correct spelling errors in the **Test** panel by [entering the key](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel).</span><span class="sxs-lookup"><span data-stu-id="5f17f-109">You can also correct spelling errors in the **Test** panel by [entering the key](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel).</span></span> <span data-ttu-id="5f17f-110">The key is kept as a session variable in the browser for the Test panel.</span><span class="sxs-lookup"><span data-stu-id="5f17f-110">The key is kept as a session variable in the browser for the Test panel.</span></span> <span data-ttu-id="5f17f-111">Add the key to the Test panel in each browser session you want spelling corrected.</span><span class="sxs-lookup"><span data-stu-id="5f17f-111">Add the key to the Test panel in each browser session you want spelling corrected.</span></span> 

<span data-ttu-id="5f17f-112">Usage of the key in the test panel and at the endpoint count toward the [key usage](https://azure.microsoft.com/pricing/details/cognitive-services/spellcheck-api/) quota.</span><span class="sxs-lookup"><span data-stu-id="5f17f-112">Usage of the key in the test panel and at the endpoint count toward the [key usage](https://azure.microsoft.com/pricing/details/cognitive-services/spellcheck-api/) quota.</span></span> <span data-ttu-id="5f17f-113">LUIS implements Bing Spell Check limits for text length.</span><span class="sxs-lookup"><span data-stu-id="5f17f-113">LUIS implements Bing Spell Check limits for text length.</span></span> 

<span data-ttu-id="5f17f-114">The endpoint requires two params for spelling corrections to work:</span><span class="sxs-lookup"><span data-stu-id="5f17f-114">The endpoint requires two params for spelling corrections to work:</span></span>

|<span data-ttu-id="5f17f-115">Param</span><span class="sxs-lookup"><span data-stu-id="5f17f-115">Param</span></span>|<span data-ttu-id="5f17f-116">Value</span><span class="sxs-lookup"><span data-stu-id="5f17f-116">Value</span></span>|
|--|--|
|`spellCheck`|<span data-ttu-id="5f17f-117">boolean</span><span class="sxs-lookup"><span data-stu-id="5f17f-117">boolean</span></span>|
|`bing-spell-check-subscription-key`|<span data-ttu-id="5f17f-118">[Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) endpoint key</span><span class="sxs-lookup"><span data-stu-id="5f17f-118">[Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) endpoint key</span></span>|

<span data-ttu-id="5f17f-119">When [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) detects an error, the original utterance, and the corrected utterance are returned along with predictions from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="5f17f-119">When [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) detects an error, the original utterance, and the corrected utterance are returned along with predictions from the endpoint.</span></span>

```JSON
{
  "query": "Book a flite to London?",
  "alteredQuery": "Book a flight to London?",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 0.780123
  },
  "entities": []
}
```
 
## <a name="change-time-zone-of-prebuilt-datetimev2-entity"></a><span data-ttu-id="5f17f-120">Change time zone of prebuilt datetimeV2 entity</span><span class="sxs-lookup"><span data-stu-id="5f17f-120">Change time zone of prebuilt datetimeV2 entity</span></span>
<span data-ttu-id="5f17f-121">When a LUIS app uses the prebuilt datetimeV2 entity, a datetime value can be returned in the prediction response.</span><span class="sxs-lookup"><span data-stu-id="5f17f-121">When a LUIS app uses the prebuilt datetimeV2 entity, a datetime value can be returned in the prediction response.</span></span> <span data-ttu-id="5f17f-122">The timezone of the request is used to determine the correct datetime to return.</span><span class="sxs-lookup"><span data-stu-id="5f17f-122">The timezone of the request is used to determine the correct datetime to return.</span></span> <span data-ttu-id="5f17f-123">If the request is coming from a bot or another centralized application before getting to LUIS, correct the timezone LUIS uses.</span><span class="sxs-lookup"><span data-stu-id="5f17f-123">If the request is coming from a bot or another centralized application before getting to LUIS, correct the timezone LUIS uses.</span></span> 

### <a name="endpoint-querystring-parameter"></a><span data-ttu-id="5f17f-124">Endpoint querystring parameter</span><span class="sxs-lookup"><span data-stu-id="5f17f-124">Endpoint querystring parameter</span></span>
<span data-ttu-id="5f17f-125">The timezone is corrected by adding the user's timezone to the [endpoint](https://aka.ms/luis-endpoint-apis) using the `timezoneOffset` param.</span><span class="sxs-lookup"><span data-stu-id="5f17f-125">The timezone is corrected by adding the user's timezone to the [endpoint](https://aka.ms/luis-endpoint-apis) using the `timezoneOffset` param.</span></span> <span data-ttu-id="5f17f-126">The value of `timezoneOffset` should be the positive or negative number, in minutes, to alter the time.</span><span class="sxs-lookup"><span data-stu-id="5f17f-126">The value of `timezoneOffset` should be the positive or negative number, in minutes, to alter the time.</span></span>  

|<span data-ttu-id="5f17f-127">Param</span><span class="sxs-lookup"><span data-stu-id="5f17f-127">Param</span></span>|<span data-ttu-id="5f17f-128">Value</span><span class="sxs-lookup"><span data-stu-id="5f17f-128">Value</span></span>|
|--|--|
|`timezoneOffset`|<span data-ttu-id="5f17f-129">positive or negative number, in minutes</span><span class="sxs-lookup"><span data-stu-id="5f17f-129">positive or negative number, in minutes</span></span>|

### <a name="daylight-savings-example"></a><span data-ttu-id="5f17f-130">Daylight savings example</span><span class="sxs-lookup"><span data-stu-id="5f17f-130">Daylight savings example</span></span>
<span data-ttu-id="5f17f-131">If you need the returned prebuilt datetimeV2 to adjust for daylight savings time, you should use the `timezoneOffset` querystring parameter with a +/- value in minutes for the [endpoint](https://aka.ms/luis-endpoint-apis) query.</span><span class="sxs-lookup"><span data-stu-id="5f17f-131">If you need the returned prebuilt datetimeV2 to adjust for daylight savings time, you should use the `timezoneOffset` querystring parameter with a +/- value in minutes for the [endpoint](https://aka.ms/luis-endpoint-apis) query.</span></span>

<span data-ttu-id="5f17f-132">Add 60 minutes:</span><span class="sxs-lookup"><span data-stu-id="5f17f-132">Add 60 minutes:</span></span> 

<span data-ttu-id="5f17f-133">https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}</span><span class="sxs-lookup"><span data-stu-id="5f17f-133">https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}</span></span>

<span data-ttu-id="5f17f-134">Remove 60 minutes:</span><span class="sxs-lookup"><span data-stu-id="5f17f-134">Remove 60 minutes:</span></span> 

<span data-ttu-id="5f17f-135">https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=-60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}</span><span class="sxs-lookup"><span data-stu-id="5f17f-135">https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=-60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}</span></span>

## <a name="c-code-determines-correct-value-of-timezoneoffset"></a><span data-ttu-id="5f17f-136">C# code determines correct value of timezoneOffset</span><span class="sxs-lookup"><span data-stu-id="5f17f-136">C# code determines correct value of timezoneOffset</span></span>
<span data-ttu-id="5f17f-137">The following C# code uses the [TimeZoneInfo](https://docs.microsoft.com/dotnet/api/system.timezoneinfo?view=netframework-4.7.1) class's [FindSystemTimeZoneById](https://docs.microsoft.com/dotnet/api/system.timezoneinfo.findsystemtimezonebyid?view=netframework-4.7.1#examples) method to determine the correct `timezoneOffset` based on system time:</span><span class="sxs-lookup"><span data-stu-id="5f17f-137">The following C# code uses the [TimeZoneInfo](https://docs.microsoft.com/dotnet/api/system.timezoneinfo?view=netframework-4.7.1) class's [FindSystemTimeZoneById](https://docs.microsoft.com/dotnet/api/system.timezoneinfo.findsystemtimezonebyid?view=netframework-4.7.1#examples) method to determine the correct `timezoneOffset` based on system time:</span></span>

```CSharp
// Get CST zone id
TimeZoneInfo targetZone = TimeZoneInfo.FindSystemTimeZoneById("Central Standard Time");

// Get local machine's value of Now
DateTime utcDatetime = DateTime.UtcNow;

// Get Central Standard Time value of Now
DateTime cstDatetime = TimeZoneInfo.ConvertTimeFromUtc(utcDatetime, targetZone);

// Find timezoneOffset
int timezoneOffset = (int)((cstDatetime - utcDatetime).TotalMinutes);
```

## <a name="next-steps"></a><span data-ttu-id="5f17f-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="5f17f-138">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5f17f-139">Correct spelling mistakes with this tutorial</span><span class="sxs-lookup"><span data-stu-id="5f17f-139">Correct spelling mistakes with this tutorial</span></span>](luis-tutorial-bing-spellcheck.md)