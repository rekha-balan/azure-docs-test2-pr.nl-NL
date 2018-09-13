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
# <a name="data-alterations"></a>Data alterations
LUIS provides ways to manipulate the utterance before or during the prediction. 

## <a name="correct-spelling-errors-in-utterance"></a>Correct spelling errors in utterance
LUIS uses [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) to correct spelling errors in the utterance. LUIS needs the key associated with that service. Create the key, then add the key as a querystring parameter at the [endpoint](https://aka.ms/luis-endpoint-apis). 

You can also correct spelling errors in the **Test** panel by [entering the key](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel). The key is kept as a session variable in the browser for the Test panel. Add the key to the Test panel in each browser session you want spelling corrected. 

Usage of the key in the test panel and at the endpoint count toward the [key usage](https://azure.microsoft.com/pricing/details/cognitive-services/spellcheck-api/) quota. LUIS implements Bing Spell Check limits for text length. 

The endpoint requires two params for spelling corrections to work:

|Param|Value|
|--|--|
|`spellCheck`|boolean|
|`bing-spell-check-subscription-key`|[Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) endpoint key|

When [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) detects an error, the original utterance, and the corrected utterance are returned along with predictions from the endpoint.

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
 
## <a name="change-time-zone-of-prebuilt-datetimev2-entity"></a>Change time zone of prebuilt datetimeV2 entity
When a LUIS app uses the prebuilt datetimeV2 entity, a datetime value can be returned in the prediction response. The timezone of the request is used to determine the correct datetime to return. If the request is coming from a bot or another centralized application before getting to LUIS, correct the timezone LUIS uses. 

### <a name="endpoint-querystring-parameter"></a>Endpoint querystring parameter
The timezone is corrected by adding the user's timezone to the [endpoint](https://aka.ms/luis-endpoint-apis) using the `timezoneOffset` param. The value of `timezoneOffset` should be the positive or negative number, in minutes, to alter the time.  

|Param|Value|
|--|--|
|`timezoneOffset`|positive or negative number, in minutes|

### <a name="daylight-savings-example"></a>Daylight savings example
If you need the returned prebuilt datetimeV2 to adjust for daylight savings time, you should use the `timezoneOffset` querystring parameter with a +/- value in minutes for the [endpoint](https://aka.ms/luis-endpoint-apis) query.

Add 60 minutes: 

https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}

Remove 60 minutes: 

https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appId}?q=Turn the lights on?**timezoneOffset=-60**&verbose={boolean}&spellCheck={boolean}&staging={boolean}&bing-spell-check-subscription-key={string}&log={boolean}

## <a name="c-code-determines-correct-value-of-timezoneoffset"></a>C# code determines correct value of timezoneOffset
The following C# code uses the [TimeZoneInfo](https://docs.microsoft.com/dotnet/api/system.timezoneinfo?view=netframework-4.7.1) class's [FindSystemTimeZoneById](https://docs.microsoft.com/dotnet/api/system.timezoneinfo.findsystemtimezonebyid?view=netframework-4.7.1#examples) method to determine the correct `timezoneOffset` based on system time:

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

## <a name="next-steps"></a>Next steps

> [!div class="nextstepaction"]
> [Correct spelling mistakes with this tutorial](luis-tutorial-bing-spellcheck.md)