---
title: LUIS Prebuilt entities dimension reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains dimension prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 3c923e7791c58255690100b04700577eb5c3f5dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869734"
---
# <a name="dimension-entity"></a><span data-ttu-id="5c51e-103">Dimension entity</span><span class="sxs-lookup"><span data-stu-id="5c51e-103">Dimension entity</span></span>
<span data-ttu-id="5c51e-104">The prebuilt dimension entity detects various types of dimensions, regardless of the LUIS app culture.</span><span class="sxs-lookup"><span data-stu-id="5c51e-104">The prebuilt dimension entity detects various types of dimensions, regardless of the LUIS app culture.</span></span> <span data-ttu-id="5c51e-105">Because this entity is already trained, you do not need to add example utterances containing dimensions to the application intents.</span><span class="sxs-lookup"><span data-stu-id="5c51e-105">Because this entity is already trained, you do not need to add example utterances containing dimensions to the application intents.</span></span> <span data-ttu-id="5c51e-106">Dimension entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="5c51e-106">Dimension entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span></span> 

## <a name="types-of-dimension"></a><span data-ttu-id="5c51e-107">Types of dimension</span><span class="sxs-lookup"><span data-stu-id="5c51e-107">Types of dimension</span></span>

<span data-ttu-id="5c51e-108">Dimension is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml) Github repository</span><span class="sxs-lookup"><span data-stu-id="5c51e-108">Dimension is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml) Github repository</span></span>


## <a name="resolution-for-dimension-entity"></a><span data-ttu-id="5c51e-109">Resolution for dimension entity</span><span class="sxs-lookup"><span data-stu-id="5c51e-109">Resolution for dimension entity</span></span>
<span data-ttu-id="5c51e-110">The following example shows the resolution of the **builtin.dimension** entity.</span><span class="sxs-lookup"><span data-stu-id="5c51e-110">The following example shows the resolution of the **builtin.dimension** entity.</span></span>

```JSON
{
  "query": "it takes more than 10 1/2 miles of cable and wire to hook it all up , and 23 computers.",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.762141049
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.762141049
    }
  ],
  "entities": [
    {
      "entity": "10 1/2 miles",
      "type": "builtin.dimension",
      "startIndex": 19,
      "endIndex": 30,
      "resolution": {
        "unit": "Mile",
        "value": "10.5"
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="5c51e-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c51e-111">Next steps</span></span>

<span data-ttu-id="5c51e-112">Learn about the [email](luis-reference-prebuilt-email.md), [number](luis-reference-prebuilt-number.md), and [ordinal](luis-reference-prebuilt-ordinal.md) entities.</span><span class="sxs-lookup"><span data-stu-id="5c51e-112">Learn about the [email](luis-reference-prebuilt-email.md), [number](luis-reference-prebuilt-number.md), and [ordinal](luis-reference-prebuilt-ordinal.md) entities.</span></span> 