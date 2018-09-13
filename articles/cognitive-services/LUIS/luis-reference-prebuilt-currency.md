---
title: LUIS Prebuilt entities currency reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains currency prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: b383e21f870d15818c540b79a9a56c1dd65fa342
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856681"
---
# <a name="currency-entity"></a><span data-ttu-id="16bc4-103">Currency entity</span><span class="sxs-lookup"><span data-stu-id="16bc4-103">Currency entity</span></span>
<span data-ttu-id="16bc4-104">The prebuilt currency entity detects currency in many denominations and countries, regardless of LUIS app culture.</span><span class="sxs-lookup"><span data-stu-id="16bc4-104">The prebuilt currency entity detects currency in many denominations and countries, regardless of LUIS app culture.</span></span> <span data-ttu-id="16bc4-105">Because this entity is already trained, you do not need to add example utterances containing currency to the application intents.</span><span class="sxs-lookup"><span data-stu-id="16bc4-105">Because this entity is already trained, you do not need to add example utterances containing currency to the application intents.</span></span> <span data-ttu-id="16bc4-106">Currency entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span><span class="sxs-lookup"><span data-stu-id="16bc4-106">Currency entity is supported in [many cultures](luis-reference-prebuilt-entities.md).</span></span> 

## <a name="types-of-currency"></a><span data-ttu-id="16bc4-107">Types of currency</span><span class="sxs-lookup"><span data-stu-id="16bc4-107">Types of currency</span></span>
<span data-ttu-id="16bc4-108">Currency is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L26) Github repository</span><span class="sxs-lookup"><span data-stu-id="16bc4-108">Currency is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L26) Github repository</span></span>

## <a name="resolution-for-currency-entity"></a><span data-ttu-id="16bc4-109">Resolution for currency entity</span><span class="sxs-lookup"><span data-stu-id="16bc4-109">Resolution for currency entity</span></span>
<span data-ttu-id="16bc4-110">The following example shows the resolution of the **builtin.currency** entity.</span><span class="sxs-lookup"><span data-stu-id="16bc4-110">The following example shows the resolution of the **builtin.currency** entity.</span></span>

```JSON
{
  "query": "search for items under $10.99",
  "topScoringIntent": {
    "intent": "SearchForItems",
    "score": 0.926173568
  },
  "intents": [
    {
      "intent": "SearchForItems",
      "score": 0.926173568
    },
    {
      "intent": "None",
      "score": 0.07376878
    }
  ],
  "entities": [
    {
      "entity": "$10.99",
      "type": "builtin.currency",
      "startIndex": 23,
      "endIndex": 28,
      "resolution": {
        "unit": "Dollar",
        "value": "10.99"
      }
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="16bc4-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="16bc4-111">Next steps</span></span>

<span data-ttu-id="16bc4-112">Learn about the [datetimeV2](luis-reference-prebuilt-datetimev2.md), [dimension](luis-reference-prebuilt-dimension.md), and [email](luis-reference-prebuilt-email.md) entities.</span><span class="sxs-lookup"><span data-stu-id="16bc4-112">Learn about the [datetimeV2](luis-reference-prebuilt-datetimev2.md), [dimension](luis-reference-prebuilt-dimension.md), and [email](luis-reference-prebuilt-email.md) entities.</span></span> 