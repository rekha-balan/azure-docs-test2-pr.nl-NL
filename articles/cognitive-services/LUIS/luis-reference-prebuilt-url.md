---
title: LUIS Prebuilt entities url reference - Azure| Microsoft Docs
titleSuffix: Azure
description: This article contains url prebuilt entity information in Language Understanding (LUIS).
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/20/2018
ms.author: diberry
ms.openlocfilehash: 86989abab1dcf64384b8b26b9484bc508f2ce31f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869779"
---
# <a name="url-entity"></a><span data-ttu-id="fd547-103">URL entity</span><span class="sxs-lookup"><span data-stu-id="fd547-103">URL entity</span></span>
<span data-ttu-id="fd547-104">URL entity extracts URLs with domain names or IP addresses.</span><span class="sxs-lookup"><span data-stu-id="fd547-104">URL entity extracts URLs with domain names or IP addresses.</span></span> <span data-ttu-id="fd547-105">Because this entity is already trained, you do not need to add example utterances containing URLs to the application.</span><span class="sxs-lookup"><span data-stu-id="fd547-105">Because this entity is already trained, you do not need to add example utterances containing URLs to the application.</span></span> <span data-ttu-id="fd547-106">URL entity is supported in `en-us` culture only.</span><span class="sxs-lookup"><span data-stu-id="fd547-106">URL entity is supported in `en-us` culture only.</span></span> 

## <a name="types-of-urls"></a><span data-ttu-id="fd547-107">Types of URLs</span><span class="sxs-lookup"><span data-stu-id="fd547-107">Types of URLs</span></span>
<span data-ttu-id="fd547-108">Url is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-URL.yaml) Github repository</span><span class="sxs-lookup"><span data-stu-id="fd547-108">Url is managed from the [Recognizers-text](https://github.com/Microsoft/Recognizers-Text/blob/master/Patterns/Base-URL.yaml) Github repository</span></span>

## <a name="resolution-for-prebuilt-url-entity"></a><span data-ttu-id="fd547-109">Resolution for prebuilt URL entity</span><span class="sxs-lookup"><span data-stu-id="fd547-109">Resolution for prebuilt URL entity</span></span>
<span data-ttu-id="fd547-110">The following example shows the resolution of the **builtin.url** entity.</span><span class="sxs-lookup"><span data-stu-id="fd547-110">The following example shows the resolution of the **builtin.url** entity.</span></span>

```JSON
{
  "query": "http://www.luis.ai is a great cognitive services example of artificial intelligence",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.781975448
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.781975448
    }
  ],
  "entities": [
    {
      "entity": "http://www.luis.ai",
      "type": "builtin.url",
      "startIndex": 0,
      "endIndex": 17
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="fd547-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd547-111">Next steps</span></span>

<span data-ttu-id="fd547-112">Learn about the [ordinal](luis-reference-prebuilt-ordinal.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span><span class="sxs-lookup"><span data-stu-id="fd547-112">Learn about the [ordinal](luis-reference-prebuilt-ordinal.md), [number](luis-reference-prebuilt-number.md), and [temperature](luis-reference-prebuilt-temperature.md) entities.</span></span>