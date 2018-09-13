---
title: Support localization - Language Understanding (LUIS) - Azure Cognitive Services | Microsoft Docs
description: LUIS has a variety of features within the service. Not all features are at the same language parity. Make sure the features you are interested in are supported in the language culture you are targeting. A LUIS app is culture-specific and cannot be changed once it is set.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 08/17/2017
ms.author: diberry
ms.openlocfilehash: 4fa58843f7e888a8fc1cfbbf76a8131bba6c488a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871682"
---
# <a name="culture-specific-understanding-in-luis-apps"></a>Culture-specific understanding in LUIS apps

LUIS has a variety of features within the service. Not all features are at the same language parity. Make sure the features you are interested in are supported in the language culture you are targeting. A LUIS app is culture-specific and cannot be changed once it is set. 

## <a name="multi-language-luis-apps"></a>Multi-language LUIS apps
If you need a multi-language LUIS client application such as a chatbot, you have a few options. If LUIS supports all the languages, you develop a LUIS app for each language. Each LUIS app has a unique app ID, and endpoint log. If you need to provide language understanding for a language LUIS does not support, you can use [Microsoft Translator API](../Translator/translator-info-overview.md) to translate the utterance into a supported language, submit the utterance to the LUIS endpoint, and receive the resulting scores.

## <a name="languages-supported"></a>Languages supported
LUIS understands utterances in the following languages:


| Language |Locale  |  Prebuilt domain | Prebuilt entity | Phrase suggestions | **[Text analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/text-analytics-supported-languages)<br>(Sentiment and<br>Keywords)| 
|--|--|:--:|:--:|:--:|:--:|
| American English |`en-US` | ✔ | ✔  |✔|✔|
| Canadian French |`fr-CA` |-|   -   |-|✔|
| *[Chinese](#chinese-support-notes) |`zh-CN` | ✔ | ✔ |✔|-|
| Dutch |`nl-NL` |-|  -   |-|✔|
| French (France) |`fr-FR` |-| ✔ |✔ |✔|
| German |`de-DE` |-| ✔ |✔ |✔|
| Italian |`it-IT` |-| ✔ |✔|✔|
| *[Japanese](#japanese-support-notes) |`ja-JP` |-| ✔ |✔|Key phrase only|
| Korean |`ko-KR` |-|   -   |-|Key phrase only|
| Portuguese (Brazil) |`pt-BR` |-| ✔ |✔ |not all sub-cultures|
| Spanish (Spain) |`es-ES` |-| ✔ |✔|✔|
| Spanish (Mexico)|`es-MX` |-|  -   |✔|✔|


Language support varies for [prebuilt entities](luis-reference-prebuilt-entities.md) and [prebuilt domains](luis-reference-prebuilt-domains.md). 

### <a name="chinese-support-notes"></a>*Chinese support notes

 - In the `zh-cn` culture, LUIS expects the simplified Chinese character set instead of the traditional character set.
 - The names of intents, entities, features, and regular expressions may be in Chinese or Roman characters.
 - See the [prebuilt domains reference ](luis-reference-prebuilt-domains.md) for information on which prebuilt domains are supported in the `zh-cn` culture.
<!--- When writing regular expressions in Chinese, do not insert whitespace between Chinese characters.-->

### <a name="japanese-support-notes"></a>*Japanese support notes

 - Because LUIS does not provide syntactic analysis and will not understand the difference between Keigo and informal Japanese, you need to incorporate the different levels of formality as training examples for your applications. 
     - でございます is not the same as です. 
     - です is not the same as だ. 

### <a name="text-analytics-support-notes"></a>**Text analytics support notes
Text analytics includes keyPhrase prebuilt entity and sentiment analysis. Only Portuguese is supported for subcultures: `pt-PT` and `pt-BR`. All other cultures are supported at the primary culture level. Learn more about Text Analytics [supported languages](https://docs.microsoft.com/azure/cognitive-services/text-analytics/text-analytics-supported-languages). 

### <a name="speech-api-supported-languages"></a>Speech API supported languages
See Speech [Supported languages](https://docs.microsoft.com/azure/cognitive-services/Speech/api-reference-rest/supportedlanguages##interactive-and-dictation-mode) for Speech dictation mode languages.

### <a name="bing-spell-check-supported-languages"></a>Bing Spell Check supported languages
See Bing Spell Check [Supported languages](https://docs.microsoft.com/azure/cognitive-services/bing-spell-check/bing-spell-check-supported-languages) for a list of supported languages and status.

## <a name="rare-or-foreign-words-in-an-application"></a>Rare or foreign words in an application
In the `en-us` culture, LUIS learns to distinguish most English words, including slang. In the `zh-cn` culture, LUIS learns to distinguish most Chinese characters. If you use a rare word in `en-us` or character in `zh-cn`, and you see that LUIS seems unable to distinguish that word or character, you can add that word or character to a [phrase-list feature](luis-how-to-add-features.md). For example, words outside of the culture of the application -- that is, foreign words -- should be added to a phrase-list feature. This phrase list should be marked non-interchangeable, to indicate that the set of rare words forms a class that LUIS should learn to recognize, but they are not synonyms or interchangeable with each other.

### <a name="hybrid-languages"></a>Hybrid languages
Hybrid languages combine words from two cultures such as English and Chinese. These languages are not supported in LUIS because an app is based on a single culture.

## <a name="tokenization"></a>Tokenization
To perform machine learning, LUIS breaks an utterance into [tokens](luis-glossary.md#token) based on culture. 

|Language|  every space or special character | character level|compound words|[tokenized entity returned](luis-concept-data-extraction.md#tokenized-entity-returned)
|--|:--:|:--:|:--:|:--:|
|Chinese||✔||✔|
|Dutch|||✔|✔|
|English (en-us)|✔ ||||
|French (fr-FR)|✔||||
|French (fr-CA)|✔||||
|German|||✔|✔|
|Italian|✔||||
|Japanese||||✔|
|Korean||✔||✔|
|Portuguese (Brazil)|✔||||
|Spanish (es-ES)|✔||||
|Spanish (es-MX)|✔||||

 