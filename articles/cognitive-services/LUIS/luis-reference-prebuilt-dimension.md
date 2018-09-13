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
# <a name="dimension-entity"></a>Dimension entity
The prebuilt dimension entity detects various types of dimensions, regardless of the LUIS app culture. Because this entity is already trained, you do not need to add example utterances containing dimensions to the application intents. Dimension entity is supported in [many cultures](luis-reference-prebuilt-entities.md). 

## <a name="types-of-dimension"></a>Types of dimension

Dimension is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/English/English-NumbersWithUnit.yaml) Github repository


## <a name="resolution-for-dimension-entity"></a>Resolution for dimension entity
The following example shows the resolution of the **builtin.dimension** entity.

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

## <a name="next-steps"></a>Next steps

Learn about the [email](luis-reference-prebuilt-email.md), [number](luis-reference-prebuilt-number.md), and [ordinal](luis-reference-prebuilt-ordinal.md) entities. 