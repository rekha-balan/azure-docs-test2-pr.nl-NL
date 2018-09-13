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
# <a name="phonenumber-entity"></a>Phonenumber entity
The `phonenumber` entity extracts a variety of phone numbers including country code. Because this entity is already trained, you do not need to add example utterances to the application. The `phonenumber` entity is supported in `en-us` culture only. 

## <a name="types-of-phonenumber"></a>Types of phonenumber
Phonenumber is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-PhoneNumbers.yaml) Github repository

## <a name="resolution-for-prebuilt-phonenumber-entity"></a>Resolution for prebuilt phonenumber entity
The following example shows the resolution of the **builtin.phonenumber** entity.

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


## <a name="next-steps"></a>Next steps

Learn about the [percentage](luis-reference-prebuilt-percentage.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities. 