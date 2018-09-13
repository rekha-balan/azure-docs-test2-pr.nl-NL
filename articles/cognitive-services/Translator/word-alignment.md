---
title: Word alignment information with the Microsoft Translator Text API | Microsoft Docs
description: Receive word alignment information from the Microsoft Translator Text API.
services: cognitive-services
author: Jann-Skotdal
manager: chriswendt1
ms.service: cognitive-services
ms.component: translator-text
ms.topic: article
ms.date: 12/14/2017
ms.author: v-jansko
ms.openlocfilehash: 61e7c2e03af4d1bcca5829ebf64a9eeb07a4368f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857676"
---
# <a name="how-to-receive-word-alignment-information"></a>How to receive word alignment information

## <a name="receiving-word-alignment-information"></a>Receiving word alignment information
To receive alignment information, use the Translate method and include the optional includeAlignment parameter.

## <a name="alignment-information-format"></a>Alignment information format
Alignment is returned as a string value of the following format for every word of the source. The information for each word is separated by a space, including for non-space-separated languages (scripts) like Chinese:

[[SourceTextStartIndex]:[SourceTextEndIndex]–[TgtTextStartIndex]:[TgtTextEndIndex]] *

Example alignment string: "0:0-7:10 1:2-11:20 3:4-0:3 3:4-4:6 5:5-21:21".

In other words, the colon separates start and end index, the dash separates the languages, and space separates the words. One word may align with zero, one, or multiple words in the other language, and the aligned words may be non-contiguous. When no alignment information is available, the Alignment element will be empty. The method returns no error in that case.

## <a name="restrictions"></a>Restrictions
Alignment is only returned for a subset of the language pairs at this point:
* from English to any other language;
* from any other language to English except for Chinese Simplified, Chinese Traditional, and Latvian to English
* from Japanese to Korean or from Korean to Japanese You will not receive alignment information if the sentence is a canned translation. Example of a canned translation is "This is a test", "I love you", and other high frequency sentences.

## <a name="example"></a>Example

Example JSON

```json
[
  {
    "translations": [
      {
        "text": "Kann ich morgen Ihr Auto fahren?",
        "to": "de",
        "alignment": {
          "proj": "0:2-0:3 4:4-5:7 6:10-25:30 12:15-16:18 17:19-20:23 21:28-9:14 29:29-31:31"
        }
      }
    ]
  }
]
```
