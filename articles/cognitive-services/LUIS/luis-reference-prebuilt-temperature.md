---
title: LUIS Prebuilt entities temperature reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains temperature prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 6436a7ee8d7b796595813fa613c442824aeae8f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869250"
---
# <a name="temperature-entity"></a><span data-ttu-id="81daa-103">Temperature entity</span><span class="sxs-lookup"><span data-stu-id="81daa-103">Temperature entity</span></span>
<span data-ttu-id="81daa-104">Temperature extracts a variety of temperature types.</span><span class="sxs-lookup"><span data-stu-id="81daa-104">Temperature extracts a variety of temperature types.</span></span> <span data-ttu-id="81daa-105">Because this entity is already trained, you do not need to add example utterances containing temperature to the application.</span><span class="sxs-lookup"><span data-stu-id="81daa-105">Because this entity is already trained, you do not need to add example utterances containing temperature to the application.</span></span> <span data-ttu-id="81daa-106">Temperature entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="81daa-106">Temperature entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span></span> 

## <a name="types-of-temperature"></a><span data-ttu-id="81daa-107">Types of temperature</span><span class="sxs-lookup"><span data-stu-id="81daa-107">Types of temperature</span></span>
<span data-ttu-id="81daa-108">Temperature is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L819) Github repository</span><span class="sxs-lookup"><span data-stu-id="81daa-108">Temperature is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L819) Github repository</span></span>

## <a name="resolution-for-prebuilt-temperature-entity"></a><span data-ttu-id="81daa-109">Resolution for prebuilt temperature entity</span><span class="sxs-lookup"><span data-stu-id="81daa-109">Resolution for prebuilt temperature entity</span></span>
<span data-ttu-id="81daa-110">The following example shows the resolution of the **builtin.temperature** entity.</span><span class="sxs-lookup"><span data-stu-id="81daa-110">The following example shows the resolution of the **builtin.temperature** entity.</span></span>

```JSON
{
  "query": "set the temperature to 30 degrees",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.85310787
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.85310787
    }
  ],
  "entities": [
    {
      "entity": "30 degrees",
      "type": "builtin.temperature",
      "startIndex": 23,
      "endIndex": 32,
      "resolution": {
        "unit": "Degree",
        "value": "30"
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="81daa-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="81daa-111">Next steps</span></span>

<span data-ttu-id="81daa-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [age](luis-reference-prebuilt-age.md) entities.</span><span class="sxs-lookup"><span data-stu-id="81daa-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [age](luis-reference-prebuilt-age.md) entities.</span></span> 