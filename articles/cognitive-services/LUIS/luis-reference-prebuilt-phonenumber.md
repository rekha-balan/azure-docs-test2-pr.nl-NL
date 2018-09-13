---
title: LUIS Prebuilt entities phone number reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains phone number prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 1ae14f72f0dc610b9399e675f49ef5fff51a6965
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870619"
---
# <a name="phonenumber-entity"></a><span data-ttu-id="2b478-103">Phonenumber entity</span><span class="sxs-lookup"><span data-stu-id="2b478-103">Phonenumber entity</span></span>
<span data-ttu-id="2b478-104">The `phonenumber` entity extracts a variety of phone numbers including country code.</span><span class="sxs-lookup"><span data-stu-id="2b478-104">The `phonenumber` entity extracts a variety of phone numbers including country code.</span></span> <span data-ttu-id="2b478-105">Because this entity is already trained, you do not need to add example utterances to the application.</span><span class="sxs-lookup"><span data-stu-id="2b478-105">Because this entity is already trained, you do not need to add example utterances to the application.</span></span> <span data-ttu-id="2b478-106">The `phonenumber` entity is supported in `en-us` culture only.</span><span class="sxs-lookup"><span data-stu-id="2b478-106">The `phonenumber` entity is supported in `en-us` culture only.</span></span> 

## <a name="types-of-phonenumber"></a><span data-ttu-id="2b478-107">Types of phonenumber</span><span class="sxs-lookup"><span data-stu-id="2b478-107">Types of phonenumber</span></span>
<span data-ttu-id="2b478-108">Phonenumber is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-PhoneNumbers.yaml) Github repository</span><span class="sxs-lookup"><span data-stu-id="2b478-108">Phonenumber is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-PhoneNumbers.yaml) Github repository</span></span>

## <a name="resolution-for-prebuilt-phonenumber-entity"></a><span data-ttu-id="2b478-109">Resolution for prebuilt phonenumber entity</span><span class="sxs-lookup"><span data-stu-id="2b478-109">Resolution for prebuilt phonenumber entity</span></span>
<span data-ttu-id="2b478-110">The following example shows the resolution of the **builtin.phonenumber** entity.</span><span class="sxs-lookup"><span data-stu-id="2b478-110">The following example shows the resolution of the **builtin.phonenumber** entity.</span></span>

```JSON
{
  "query": "my mobile is 00 44 161 1234567",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.8448457
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.8448457
    }
  ],
  "entities": [
    {
      "entity": "00 44 161 1234567",
      "type": "builtin.phonenumber",
      "startIndex": 13,
      "endIndex": 29,
      "resolution": {
        "value": "00 44 161 1234567"
      }
    }
  ]
}
```


## <a name="next-steps"></a><span data-ttu-id="2b478-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b478-111">Next steps</span></span>

<span data-ttu-id="2b478-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span><span class="sxs-lookup"><span data-stu-id="2b478-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span></span> 