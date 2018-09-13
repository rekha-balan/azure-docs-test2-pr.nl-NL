---
title: Boundaries and limits for Language Understanding (LUIS)
titleSuffix: Azure Cognitive Services
description: This article contains the known limits of Azure Cognitive Services Language Understanding (LUIS). LUIS has several boundary areas. Model boundary controls intents, entities, and features in LUIS. Quota limits based on key type. Keyboard combination controls the LUIS website.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 07/31/2018
ms.author: diberry
ms.openlocfilehash: 551d2c06887b5c6133f281776081fb1b737ba0bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869624"
---
# <a name="luis-boundaries"></a>LUIS boundaries
LUIS has several boundary areas. The first is the [model boundary](#model-boundaries), which controls intents, entities, and features in LUIS. The second area is [quota limits](#key-limits) based on key type. A third area of boundaries is the [keyboard combination](#keyboard-controls) for controlling the LUIS website. A fourth area is the [world region mapping](luis-reference-regions.md) between the LUIS authoring website and the LUIS [endpoint](luis-glossary.md#endpoint) APIs. 


## <a name="model-boundaries"></a>Model boundaries

|Area|Limit|
|--|:--|--|
| [App name][luis-get-started-create-app] | *Default character max |
| [Batch testing][batch-testing]| 10 datasets, 1000 utterances per dataset|
| **[Composite](./luis-concept-entity-types.md)|100 with up to 10 children |
| Explicit list | 50 per application|
| **[Hierarchical](./luis-concept-entity-types.md) |100 with up to 10 children |
| [Intents][intents]|500 per application<br>[Dispatch-based](https://github.com/Microsoft/botbuilder-tools/tree/master/Dispatch) application has corresponding 500 dispatch sources|
| [List entities](./luis-concept-entity-types.md) | Parent: 50, child: 20,000 items. Canonical name is *default character max. Synonym values have no length restriction. |
| [Patterns](luis-concept-patterns.md)|500 patterns per application.<br>Maximum length of pattern is 400 characters.<br>3 Pattern.any entities per pattern<br>Maximum of 2 nested optional texts in pattern|
| [Pattern.any](./luis-concept-entity-types.md)|100 per application, 3 pattern.any entities per pattern |
| [Phrase list][phrase-list]|10 phrase lists, 5,000 items per list|
| [Prebuilt entities](./luis-prebuilt-entities.md) | no limit|
| [Regular expression entities](./luis-concept-entity-types.md)|20 entities<br>500 character max. per regular expression entity pattern|
| [Roles](luis-concept-roles.md)|300 roles per application. 10 roles per entity|
| **[Simple](./luis-concept-entity-types.md)| 100 entities|
| [Utterance][utterances] | 500 characters|
| [Utterances][utterances] | 15,000 per application|
| [Versions](luis-concept-version.md)| no limit |
| [Version name][luis-how-to-manage-versions] | 10 characters restricted to alphanumeric and period (.) |

*Default character max is 50 characters. 

**The total count of simple, hierarchical, and composite entities can't exceed 100. The total count of hierarchical entities, composite entities, simple entities, and hierarchical children entities can't exceed 330. 

## <a name="intent-and-entity-naming"></a>Intent and entity naming
Do not use the following characters in intent and entity names:

|Character|Name|
|--|--|
|`{`|Left curly bracket|
|`}`|Right curly bracket|
|`[`|Left bracket|
|`]`|Right bracket|
|`\`|Backslash|

## <a name="key-limits"></a>Key limits
The authoring key has different limits for authoring and endpoint. The LUIS service endpoint key is only valid for endpoint queries.

|Key|Authoring|Endpoint|Purpose|
|--|--|--|--|
|Authoring/Starter|1 million/month, 5/second|1 thousand/month, 5/second|Authoring your LUIS app|
|[Subscription][pricing] - F0 - Free tier |invalid|10 thousand/month, 5/second|Querying your LUIS endpoint|
|[Subscription][pricing] - S0 - Basic tier|invalid|50/second|Querying your LUIS endpoint|
|[Sentiment analysis integration](luis-how-to-publish-app.md#enable-sentiment-analysis)|invalid|no charge|Adding sentiment information including key phrase data extraction |
|Speech integration|invalid|$5.50 USD/1 thousand endpoint requests|Convert spoken utterance to text utterance and return LUIS results|

## <a name="keyboard-controls"></a>Keyboard controls

|Keyboard input | Description | 
|--|--|
|Control+E|switches between tokens and entities on utterances list|

## <a name="website-sign-in-time-period"></a>Website sign in time period

Your sign-in access is for **60 minutes**. After this time period, you will get this error. You need to log in again.

[luis-get-started-create-app]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-get-started-create-app
[batch-testing]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-test#batch-testing
[intents]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-intent
[phrase-list]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-feature
[utterances]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-utterance
[luis-how-to-manage-versions]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-manage-versions
[pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
<!-- TBD: fix this link -->
[speech-to-intent-pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
