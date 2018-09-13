---
title: LUIS Prebuilt entities percentage reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains percentage prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: d445dbf69e3d2163b5d44b894f8795d41fbd34e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865877"
---
# <a name="percentage-entity"></a><span data-ttu-id="96aa4-103">Percentage entity</span><span class="sxs-lookup"><span data-stu-id="96aa4-103">Percentage entity</span></span>
<span data-ttu-id="96aa4-104">Percentage numbers can appear as fractions, `3 1/2`, or as percentage, `2%`.</span><span class="sxs-lookup"><span data-stu-id="96aa4-104">Percentage numbers can appear as fractions, `3 1/2`, or as percentage, `2%`.</span></span> <span data-ttu-id="96aa4-105">Because this entity is already trained, you do not need to add example utterances containing percentage to the application intents.</span><span class="sxs-lookup"><span data-stu-id="96aa4-105">Because this entity is already trained, you do not need to add example utterances containing percentage to the application intents.</span></span> <span data-ttu-id="96aa4-106">Percentage entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="96aa4-106">Percentage entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span></span> 

## <a name="types-of-percentage"></a><span data-ttu-id="96aa4-107">Types of percentage</span><span class="sxs-lookup"><span data-stu-id="96aa4-107">Types of percentage</span></span>
<span data-ttu-id="96aa4-108">Percentage is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-Numbers.yaml#L114) Github repository</span><span class="sxs-lookup"><span data-stu-id="96aa4-108">Percentage is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-Numbers.yaml#L114) Github repository</span></span>

## <a name="resolution-for-prebuilt-percentage-entity"></a><span data-ttu-id="96aa4-109">Resolution for prebuilt percentage entity</span><span class="sxs-lookup"><span data-stu-id="96aa4-109">Resolution for prebuilt percentage entity</span></span>
<span data-ttu-id="96aa4-110">The following example shows the resolution of the **builtin.percentage** entity.</span><span class="sxs-lookup"><span data-stu-id="96aa4-110">The following example shows the resolution of the **builtin.percentage** entity.</span></span>

```JSON
{
  "query": "set a trigger when my stock goes up 2%",
  "topScoringIntent": {
    "intent": "SetTrigger",
    "score": 0.971157849
  },
  "intents": [
    {
      "intent": "SetTrigger",
      "score": 0.971157849
    }
  ],
  "entities": [
    {
      "entity": "2%",
      "type": "builtin.percentage",
      "startIndex": 36,
      "endIndex": 37,
      "resolution": {
        "value": "2%"
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="96aa4-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="96aa4-111">Next steps</span></span>

<span data-ttu-id="96aa4-112">Learn about the [ordinal](luis-reference-prebuilt-ordinal.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span><span class="sxs-lookup"><span data-stu-id="96aa4-112">Learn about the [ordinal](luis-reference-prebuilt-ordinal.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span></span> 