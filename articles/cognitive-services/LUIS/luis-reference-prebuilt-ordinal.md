---
title: LUIS Prebuilt entities ordinal reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains ordinal prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 216114ec521e2065cb13cd39b4086f50ec81ba56
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867755"
---
# <a name="ordinal-entity"></a><span data-ttu-id="27e87-103">Ordinal entity</span><span class="sxs-lookup"><span data-stu-id="27e87-103">Ordinal entity</span></span>
<span data-ttu-id="27e87-104">Ordinal number is a numeric representation of an object inside a set: `first`, `second`, `third`.</span><span class="sxs-lookup"><span data-stu-id="27e87-104">Ordinal number is a numeric representation of an object inside a set: `first`, `second`, `third`.</span></span> <span data-ttu-id="27e87-105">Because this entity is already trained, you do not need to add example utterances containing ordinal to the application intents.</span><span class="sxs-lookup"><span data-stu-id="27e87-105">Because this entity is already trained, you do not need to add example utterances containing ordinal to the application intents.</span></span> <span data-ttu-id="27e87-106">Ordinal entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="27e87-106">Ordinal entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span></span> 

## <a name="types-of-ordinal"></a><span data-ttu-id="27e87-107">Types of ordinal</span><span class="sxs-lookup"><span data-stu-id="27e87-107">Types of ordinal</span></span>
<span data-ttu-id="27e87-108">Ordinal is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-Numbers.yaml#L45) Github repository</span><span class="sxs-lookup"><span data-stu-id="27e87-108">Ordinal is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-Numbers.yaml#L45) Github repository</span></span>

## <a name="resolution-for-prebuilt-ordinal-entity"></a><span data-ttu-id="27e87-109">Resolution for prebuilt ordinal entity</span><span class="sxs-lookup"><span data-stu-id="27e87-109">Resolution for prebuilt ordinal entity</span></span>
<span data-ttu-id="27e87-110">The following example shows the resolution of the **builtin.ordinal** entity.</span><span class="sxs-lookup"><span data-stu-id="27e87-110">The following example shows the resolution of the **builtin.ordinal** entity.</span></span>

```JSON
{
  "query": "Order the second option",
  "topScoringIntent": {
    "intent": "OrderFood",
    "score": 0.9993253
  },
  "intents": [
    {
      "intent": "OrderFood",
      "score": 0.9993253
    },
    {
      "intent": "None",
      "score": 0.05046708
    }
  ],
  "entities": [
    {
      "entity": "second",
      "type": "builtin.ordinal",
      "startIndex": 10,
      "endIndex": 15,
      "resolution": {
        "value": "2"
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="27e87-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="27e87-111">Next steps</span></span>

<span data-ttu-id="27e87-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [phonenumber](luis-reference-prebuilt-phonenumber.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span><span class="sxs-lookup"><span data-stu-id="27e87-112">Learn about the [percentage](luis-reference-prebuilt-percentage.md), [phonenumber](luis-reference-prebuilt-phonenumber.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span></span> 