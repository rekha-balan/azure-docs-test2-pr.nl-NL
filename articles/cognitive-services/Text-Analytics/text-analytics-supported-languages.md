---
title: Supported languages in Text Analytics API - Azure Cognitive Services | Microsoft Docs
description: List of generally available and preview language support for Text Analytics API operations. Applies to sentiment analysis, key phrase extraction, and language detection.
services: cognitive-services
author: ashmaka
manager: cgronlun
ms.service: cognitive-services
ms.technology: text-analytics
ms.topic: conceptual
ms.date: 05/02/2018
ms.author: ashmaka
ms.openlocfilehash: 2d341cfaf261bea6367bb55dd5d322f419e22d34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870731"
---
# <a name="supported-languages-in-the-text-analytics-api"></a>Supported languages in the Text Analytics API

This article explains which languages are supported for each operation: sentiment analysis, key phrase extraction, and language detection.

## <a name="language-detection"></a>Language Detection

The Text Analytics API can detect up to 120 different languages. Language Detection returns the "script" of a language. For instance, for the phrase "I have a dog" it will return  `en` instead of  `en-US`. The only special case is Chinese, where the language detection capability will return `zh_CHS` or `zh_CHT` if it can determine the script given the text provided. In situations where a specific script cannot be identified for a Chinese document, it will return simply `zh`.

## <a name="sentiment-analysis-key-phrase-extraction-and-entity-linking"></a>Sentiment Analysis, Key Phrase Extraction, and Entity Linking

For sentiment analysis, key phrase extraction, and entity linking, the list of supported languages is more selective as the analyzers are refined to accommodate the linguistic rules of additional languages.

## <a name="language-list-and-status"></a>Language list and status

Language support is initially rolled out in preview, graduating to generally available (GA) status, independently of each other and of the Text Analytics service overall. It's possible for languages to remain in preview, even while Text Analytics API transitions to generally available.

| Language    | Language code | Sentiment | Key phrases | Entity Linking |   Notes  |
|:----------- |:-------------:|:---------:|:-----------:|:-----------:|:-----------:
| Danish      | `da`          | ✔ \*     | ✔           |             |     |
| Dutch       | `nl`          | ✔ \*     | ✔          |             |     |
| English     | `en`          | ✔        | ✔           |  ✔ \*   |      |
| Finnish     | `fi`          | ✔ \*     | ✔           |             |     |
| French      | `fr`          | ✔        | ✔           |             |     |
| German      | `de`          | ✔ \*     | ✔           |            |     |
| Greek       | `el`          | ✔ \*     |             |            |     |
| Italian     | `it`          | ✔ \*     | ✔           |             |     |
| Japanese    | `ja`          |          | ✔           |            |     |
| Korean      | `ko`          |          | ✔           |            |     |
| Norwegian  (Bokmål) | `no`          | ✔ \*     |  ✔          |             |     |
| Polish      | `pl`          | ✔ \*     |  ✔          |             |     |
| Portuguese (Portugal) | `pt-PT`| ✔        |  ✔          |       |`pt` also accepted|
| Portuguese (Brazil)   | `pt-BR`|          |  ✔   |         |     |
| Russian     | `ru`          | ✔ \*     | ✔           |             |     |
| Spanish     | `es`          | ✔        | ✔           |     |     |
| Swedish     | `sv`          | ✔ \*     | ✔           |             |     |
| Turkish     | `tr`          | ✔ \*     |             |             |     |

\* indicates language support in preview

## <a name="see-also"></a>See also

[Cognitive Services Documentation page](https://docs.microsoft.com/azure/cognitive-services/)   
[Cognitive Services Product page](https://azure.microsoft.com/services/cognitive-services/)
