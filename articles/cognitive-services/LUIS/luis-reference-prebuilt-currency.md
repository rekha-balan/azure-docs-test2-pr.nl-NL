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
# <a name="currency-entity"></a>Currency entity
The prebuilt currency entity detects currency in many denominations and countries, regardless of LUIS app culture. Because this entity is already trained, you do not need to add example utterances containing currency to the application intents. Currency entity is supported in [many cultures](luis-reference-prebuilt-entities.md). 

## <a name="types-of-currency"></a>Types of currency
Currency is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L26) Github repository

## <a name="resolution-for-currency-entity"></a>Resolution for currency entity
The following example shows the resolution of the **builtin.currency** entity.

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

## <a name="next-steps"></a>Next steps

Learn about the [datetimeV2](luis-reference-prebuilt-datetimev2.md), [dimension](luis-reference-prebuilt-dimension.md), and [email](luis-reference-prebuilt-email.md) entities. 