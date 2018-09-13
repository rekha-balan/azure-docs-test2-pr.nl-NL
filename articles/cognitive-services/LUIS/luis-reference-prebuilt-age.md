---
title: LUIS Prebuilt entities age reference - Azure | Microsoft Docs
titleSuffix: Azure
description: This article contains age prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: f93acb8bece8c66c3ed7197f1c4530011aec3f29
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866668"
---
# <a name="age-entity"></a>Age entity
The prebuilt age entity captures the age value both numerically and in terms of days, weeks, months, and years. Because this entity is already trained, you do not need to add example utterances containing age to the application intents. Age entity is supported in [many cultures](luis-reference-prebuilt-entities.md). 

## <a name="types-of-age"></a>Types of age
Age is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml#L3) Github repository

## <a name="resolution-for-prebuilt-age-entity"></a>Resolution for prebuilt age entity
The following example shows the resolution of the **builtin.age** entity.

```JSON
{
  "query": "A 90 day old utilities bill is quite late.",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.8236133
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.8236133
    }
  ],
  "entities": [
    {
      "entity": "90 day old",
      "type": "builtin.age",
      "startIndex": 2,
      "endIndex": 11,
      "resolution": {
        "unit": "Day",
        "value": "90"
      }
    }
  ]
}
```

## <a name="next-steps"></a>Next steps

Learn about the [currency](luis-reference-prebuilt-currency.md), [datetimeV2](luis-reference-prebuilt-datetimev2.md), and [dimension](luis-reference-prebuilt-dimension.md) entities. 