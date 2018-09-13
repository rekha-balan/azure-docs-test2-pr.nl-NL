---
title: Understanding intents in LUIS apps in Azure | Microsoft Docs
description: Describes what intents are in Language Understanding Intelligent Service (LUIS) apps.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 06/04/2018
ms.author: diberry
ms.openlocfilehash: 456f28191161c9a2fac223bf2a31e62e54ae28ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868089"
---
# <a name="intents-in-luis"></a>Intents in LUIS

An intent represents a task or action the user wants to perform. It is a purpose or goal expressed in a user's [utterance](luis-concept-utterance.md).

Define a set of intents that corresponds to actions users want to take in your application. For example, a travel app defines several intents:

Travel app intents   |   Example utterances   | 
------|------|
 BookFlight     |   "Book me a flight to Rio next week" <br/> "Fly me to Rio on the 24th" <br/> "I need a plane ticket next Sunday to Rio de Janeiro"    |
 Greeting     |   "Hi" <br/>"Hello" <br/>"Good morning"  |
 CheckWeather | "What's the weather like in Boston?" <br/> "Show me the forecast for this weekend" |
 None         | "Get me a cookie recipe"<br>"Did the Lakers win?" |

All applications come with the predefined intent, "[None](#none-intent-is-fallback-for-app)" which is the fallback intent. 

## <a name="prebuilt-domains-provide-intents"></a>Prebuilt domains provide intents
In addition to intents that you define, you can use prebuilt intents from one of the prebuilt domains. For more information, see [Use prebuilt domains in LUIS apps](luis-how-to-use-prebuilt-domains.md) to learn about how to customize intents from a prebuilt domain for use in your app.

## <a name="return-all-intents-scores"></a>Return all intents' scores
You assign an utterance to a single intent. When LUIS receives an utterance on the endpoint, it returns the one top intent for that utterance. If you want scores for all intents for the utterance, you can provide `verbose=true` flag on the query string of the API [endpoint call](https://aka.ms/v1-endpoint-api-docs). 

## <a name="intent-compared-to-entity"></a>Intent compared to entity
The intent represents action the chatbot should take for the user and is based on the entire utterance. The entity represents words or phrases contained inside the utterance. An utterance can have only one top scoring intent but it can have many entities. 

<a name="how-do-intents-relate-to-entities"></a> Create an intent when the user's _intention_ would trigger an action in your client application, like a call to the checkweather() function. Then create an entity to represent parameters required to execute the action. 

|Example intent   | Entity | Entity in example utterances   | 
|------------------|------------------------------|------------------------------|
| CheckWeather | { "type": "location", "entity": "seattle" }<br>{ "type": "builtin.datetimeV2.date","entity": "tomorrow","resolution":"2018-05-23" } | What's the weather like in `Seattle` `tomorrow`? |
| CheckWeather | { "type": "date_range", "entity": "this weekend" } | Show me the forecast for `this weekend` | 

## <a name="custom-intents"></a>Custom intents

Similarly intentioned [utterances](luis-concept-utterance.md) correspond to a single intent. Utterances in your intent can use any [entity](luis-concept-entity-types.md) in the app since entities are not intent-specific. 

## <a name="prebuilt-domain-intents"></a>Prebuilt domain intents

[Prebuilt domains](luis-how-to-use-prebuilt-domains.md) have intents with utterances.  

## <a name="none-intent-is-fallback-for-app"></a>None intent is fallback for app
The **None** intent is a catch-all or fallback intent. It is used to teach LUIS utterances that are not important in the app domain (subject area). The **None** intent should have between 10 and 20 percent of the total utterances in the application. Do not leave it empty. 

### <a name="none-intent-helps-conversation-direction"></a>None intent helps conversation direction
When an utterance is predicted as the None intent and returned to the chatbot with that prediction, the bot can ask more questions or provide a menu to direct the user to valid choices in the chatbot. 

### <a name="no-utterances-in-none-intent-skews-predictions"></a>No utterances in None intent skews predictions
If you do not add any utterances for the **None** intent, LUIS forces an utterance that is outside the domain into one of the domain intents. This will skew the prediction scores by teaching LUIS the wrong intent for the utterance. 

### <a name="add-utterances-to-the-none-intent"></a>Add utterances to the None intent
The **None** intent is created but left empty on purpose. Fill it with utterances that are outside of your domain. A good utterance for **None** is something completely outside the app as well as the industry the app serves. For example, a travel app should not use any utterances for **None** that can relate to travel such as reservations, billing, food, hospitality, cargo, inflight entertainment. 

What type of utterances are left for the None intent? Start with something specific that your bot shouldn't answer such "What kind of dinosaur has blue teeth?" This is a very specific question far outside of a travel app. 

### <a name="none-is-a-required-intent"></a>None is a required intent
The **None** intent is a required intent and can't be deleted or renamed.

## <a name="negative-intentions"></a>Negative intentions 
If you want to determine negative and positive intentions, such as "I **want** a car" and "I **don't** want a car", you can create two intents (one positive, and one negative) and add appropriate utterances for each. Or you can create a single intent and mark the two different positive and negative terms as an entity.  

## <a name="intent-balance"></a>Intent balance
The app domain intents should have a balance of utterances across each intent. Do not have one intent with 10 utterances and another intent with 500 utterances. This is not balanced. If you have this situation, review the intent with 500 utterances to see if many of the intents can be reorganized into a [pattern](luis-concept-patterns.md). 

The **None** intent is not included in the balance. That intent should contain 10% of the total utterances in the app.

## <a name="intent-limits"></a>Intent limits
Review [limits](luis-boundaries.md#model-boundaries) to understand how many intents you can add to a model. 

### <a name="if-you-need-more-than-the-maximum-number-of-intents"></a>If you need more than the maximum number of intents 
First, consider whether your system is using too many intents. 

### <a name="can-multiple-intents-be-combined-into-single-intent-with-entities"></a>Can multiple intents be combined into single intent with entities 
Intents that are too similar can make it more difficult for LUIS to distinguish between them. Intents should be varied enough to capture the main tasks that the user is asking for, but they don't need to capture every path your code takes. For example, BookFlight and FlightCustomerService might be separate intents in a travel app, but BookInternationalFlight and BookDomesticFlight are too similar. If your system needs to distinguish them, use entities or other logic rather than intents. 

### <a name="dispatcher-model"></a>Dispatcher model
Learn more about combining LUIS and QnA maker apps with the [dispatch model](luis-concept-enterprise.md#when-you-need-to-combine-several-luis-and-qna-maker-apps). 

### <a name="request-help-for-apps-with-significant-number-of-intents"></a>Request help for apps with significant number of intents
If reducing the number of intents or dividing your intents into multiple apps doesn't work for you, contact support. If your Azure subscription includes support services, contact [Azure technical support](https://azure.microsoft.com/support/options/). 

## <a name="next-steps"></a>Next steps

* Learn more about [entities](luis-concept-entity-types.md), which are important words relevant to intents
* Learn how to [add and manage intents](luis-how-to-add-intents.md) in your LUIS app.
* Review intent [best practices](luis-concept-best-practices.md)