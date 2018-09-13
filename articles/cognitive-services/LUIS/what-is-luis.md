---
title: What is Language Understanding (LUIS) - Azure Cognitive Services | Microsoft Docs
description: Language Understanding (LUIS) is a cloud-based API service that applies custom machine-learning intelligence to a user's conversational, natural language text to predict overall meaning, and pull out relevant, detailed information. A client application for LUIS is any conversational application that communicates with a user in natural language to complete a task. Examples of client applications include social media apps, chat bots, and speech-enabled desktop applications.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: overview
ms.date: 08/15/2018
ms.author: diberry
ms.openlocfilehash: e74abb30709f186d3c1139793cf34d3e033ff967
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867930"
---
# <a name="what-is-language-understanding-luis"></a><span data-ttu-id="cc575-105">What is Language Understanding (LUIS)?</span><span class="sxs-lookup"><span data-stu-id="cc575-105">What is Language Understanding (LUIS)?</span></span>

<span data-ttu-id="cc575-106">Language Understanding (LUIS) is a cloud-based API service that applies custom machine-learning intelligence to a user's conversational, natural language text to predict overall meaning, and pull out relevant, detailed information.</span><span class="sxs-lookup"><span data-stu-id="cc575-106">Language Understanding (LUIS) is a cloud-based API service that applies custom machine-learning intelligence to a user's conversational, natural language text to predict overall meaning, and pull out relevant, detailed information.</span></span> 

<span data-ttu-id="cc575-107">A client application for LUIS is any conversational application that communicates with a user in natural language to complete a task.</span><span class="sxs-lookup"><span data-stu-id="cc575-107">A client application for LUIS is any conversational application that communicates with a user in natural language to complete a task.</span></span> <span data-ttu-id="cc575-108">Examples of client applications include social media apps, chat bots, and speech-enabled desktop applications.</span><span class="sxs-lookup"><span data-stu-id="cc575-108">Examples of client applications include social media apps, chat bots, and speech-enabled desktop applications.</span></span>  

<span data-ttu-id="cc575-109">![Conceptual image of 3 client applications working with Cognitive Services Language Understanding (LUIS)](./media/luis-overview/luis-entry-point.png "Conceptual image of 3 client applications working with Cognitive Services Language Understanding (LUIS)")</span><span class="sxs-lookup"><span data-stu-id="cc575-109">![Conceptual image of 3 client applications working with Cognitive Services Language Understanding (LUIS)](./media/luis-overview/luis-entry-point.png "Conceptual image of 3 client applications working with Cognitive Services Language Understanding (LUIS)")</span></span>

## <a name="use-luis-in-a-chat-bot"></a><span data-ttu-id="cc575-110">Use LUIS in a chat bot</span><span class="sxs-lookup"><span data-stu-id="cc575-110">Use LUIS in a chat bot</span></span>

<a name="Accessing-LUIS"></a>

<span data-ttu-id="cc575-111">Once the LUIS app is published, a client application sends utterances (text) to the LUIS natural language processing endpoint [API][endpoint-apis] and receives the results as JSON responses.</span><span class="sxs-lookup"><span data-stu-id="cc575-111">Once the LUIS app is published, a client application sends utterances (text) to the LUIS natural language processing endpoint [API][endpoint-apis] and receives the results as JSON responses.</span></span> <span data-ttu-id="cc575-112">A common client application for LUIS is a chat bot.</span><span class="sxs-lookup"><span data-stu-id="cc575-112">A common client application for LUIS is a chat bot.</span></span>


<span data-ttu-id="cc575-113">![Conceptual imagery of LUIS working with Chat bot to predict user text with natural language understanding (NLP)](./media/luis-overview/luis-overview-process-2.png "Conceptual imagery of LUIS working with Chat bot to predict user text with natural language understanding (NLP")</span><span class="sxs-lookup"><span data-stu-id="cc575-113">![Conceptual imagery of LUIS working with Chat bot to predict user text with natural language understanding (NLP)](./media/luis-overview/luis-overview-process-2.png "Conceptual imagery of LUIS working with Chat bot to predict user text with natural language understanding (NLP")</span></span>

|<span data-ttu-id="cc575-114">Step</span><span class="sxs-lookup"><span data-stu-id="cc575-114">Step</span></span>|<span data-ttu-id="cc575-115">Action</span><span class="sxs-lookup"><span data-stu-id="cc575-115">Action</span></span>|
|:--|:--|
|<span data-ttu-id="cc575-116">1</span><span class="sxs-lookup"><span data-stu-id="cc575-116">1</span></span>|<span data-ttu-id="cc575-117">The client application sends the user _utterance_ (text in their own words), "I want to call my HR rep."</span><span class="sxs-lookup"><span data-stu-id="cc575-117">The client application sends the user _utterance_ (text in their own words), "I want to call my HR rep."</span></span> <span data-ttu-id="cc575-118">to the LUIS endpoint as an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="cc575-118">to the LUIS endpoint as an HTTP request.</span></span>|
|<span data-ttu-id="cc575-119">2</span><span class="sxs-lookup"><span data-stu-id="cc575-119">2</span></span>|<span data-ttu-id="cc575-120">LUIS applies the learned model to the natural language text to provide intelligent understanding about the user input.</span><span class="sxs-lookup"><span data-stu-id="cc575-120">LUIS applies the learned model to the natural language text to provide intelligent understanding about the user input.</span></span> <span data-ttu-id="cc575-121">LUIS returns a JSON-formatted response, with a top intent, "HRContact".</span><span class="sxs-lookup"><span data-stu-id="cc575-121">LUIS returns a JSON-formatted response, with a top intent, "HRContact".</span></span> <span data-ttu-id="cc575-122">The minimum JSON endpoint response contains the query utterance, and the top scoring intent.</span><span class="sxs-lookup"><span data-stu-id="cc575-122">The minimum JSON endpoint response contains the query utterance, and the top scoring intent.</span></span> <span data-ttu-id="cc575-123">It can also extract data such as the Contact Type entity.</span><span class="sxs-lookup"><span data-stu-id="cc575-123">It can also extract data such as the Contact Type entity.</span></span>|
|<span data-ttu-id="cc575-124">3</span><span class="sxs-lookup"><span data-stu-id="cc575-124">3</span></span>|<span data-ttu-id="cc575-125">The client application uses the JSON response to make decisions about how to fulfill the user's requests.</span><span class="sxs-lookup"><span data-stu-id="cc575-125">The client application uses the JSON response to make decisions about how to fulfill the user's requests.</span></span> <span data-ttu-id="cc575-126">These decisions can include some decision tree in the bot framework code and calls to other services.</span><span class="sxs-lookup"><span data-stu-id="cc575-126">These decisions can include some decision tree in the bot framework code and calls to other services.</span></span> |

<span data-ttu-id="cc575-127">The LUIS app provides intelligence so the client application can make smart choices.</span><span class="sxs-lookup"><span data-stu-id="cc575-127">The LUIS app provides intelligence so the client application can make smart choices.</span></span> <span data-ttu-id="cc575-128">LUIS doesn't provide those choices.</span><span class="sxs-lookup"><span data-stu-id="cc575-128">LUIS doesn't provide those choices.</span></span> 

<!--

### Example of JSON endpoint response

The minimum JSON endpoint response contains the query utterance, and the top scoring intent. It can also extract data such as the following **Contact Type** entity. 

```JSON
{
  "query": "I want to call my HR rep.",
  "topScoringIntent": {
    "intent": "HRContact",
    "score": 0.921233
  },
  "entities": [
    {
      "entity": "call",
      "type": "Contact Type",
      "startIndex": 10,
      "endIndex": 13,
      "score": 0.7615982
    }
  ]
}
```
-->

<a name="Key-LUIS-concepts"></a>
<a name="what-is-a-luis-model"></a>

## <a name="natural-language-processing"></a><span data-ttu-id="cc575-129">Natural language processing</span><span class="sxs-lookup"><span data-stu-id="cc575-129">Natural language processing</span></span>

<span data-ttu-id="cc575-130">A LUIS app contains a domain-specific natural language model.</span><span class="sxs-lookup"><span data-stu-id="cc575-130">A LUIS app contains a domain-specific natural language model.</span></span> <span data-ttu-id="cc575-131">You can start the LUIS app with a prebuilt domain model, build your own model, or blend pieces of a prebuilt domain with your own custom information.</span><span class="sxs-lookup"><span data-stu-id="cc575-131">You can start the LUIS app with a prebuilt domain model, build your own model, or blend pieces of a prebuilt domain with your own custom information.</span></span>

* <span data-ttu-id="cc575-132">**Prebuilt model** LUIS has many prebuilt domain models including intents, utterances, and prebuilt entities.</span><span class="sxs-lookup"><span data-stu-id="cc575-132">**Prebuilt model** LUIS has many prebuilt domain models including intents, utterances, and prebuilt entities.</span></span> <span data-ttu-id="cc575-133">You can use the prebuilt entities without having to use the intents and utterances of the prebuilt model.</span><span class="sxs-lookup"><span data-stu-id="cc575-133">You can use the prebuilt entities without having to use the intents and utterances of the prebuilt model.</span></span> <span data-ttu-id="cc575-134">[Prebuilt domain models](luis-how-to-use-prebuilt-domains.md) include the entire design for you and are a great way to start using LUIS quickly.</span><span class="sxs-lookup"><span data-stu-id="cc575-134">[Prebuilt domain models](luis-how-to-use-prebuilt-domains.md) include the entire design for you and are a great way to start using LUIS quickly.</span></span>

* <span data-ttu-id="cc575-135">**Custom Entities** LUIS gives you several ways to identify your own custom intents and entities including machine-learned entities, specific or literal entities, and a combination of machine-learned and literal.</span><span class="sxs-lookup"><span data-stu-id="cc575-135">**Custom Entities** LUIS gives you several ways to identify your own custom intents and entities including machine-learned entities, specific or literal entities, and a combination of machine-learned and literal.</span></span>

## <a name="build-the-luis-model"></a><span data-ttu-id="cc575-136">Build the LUIS model</span><span class="sxs-lookup"><span data-stu-id="cc575-136">Build the LUIS model</span></span>
<span data-ttu-id="cc575-137">Build the model with the [authoring](https://aka.ms/luis-authoring-apis) APIs or with the LUIS portal.</span><span class="sxs-lookup"><span data-stu-id="cc575-137">Build the model with the [authoring](https://aka.ms/luis-authoring-apis) APIs or with the LUIS portal.</span></span>

<span data-ttu-id="cc575-138">The LUIS model begins with categories of user intentions called **[intents](luis-concept-intent.md)**.</span><span class="sxs-lookup"><span data-stu-id="cc575-138">The LUIS model begins with categories of user intentions called **[intents](luis-concept-intent.md)**.</span></span> <span data-ttu-id="cc575-139">Each intent needs examples of user **[utterances](luis-concept-utterance.md)**.</span><span class="sxs-lookup"><span data-stu-id="cc575-139">Each intent needs examples of user **[utterances](luis-concept-utterance.md)**.</span></span> <span data-ttu-id="cc575-140">Each utterance can provide a variety of data that needs to be extracted with **[entities](luis-concept-entity-types.md)**.</span><span class="sxs-lookup"><span data-stu-id="cc575-140">Each utterance can provide a variety of data that needs to be extracted with **[entities](luis-concept-entity-types.md)**.</span></span> 

|<span data-ttu-id="cc575-141">Example user utterance</span><span class="sxs-lookup"><span data-stu-id="cc575-141">Example user utterance</span></span>|<span data-ttu-id="cc575-142">Intent</span><span class="sxs-lookup"><span data-stu-id="cc575-142">Intent</span></span>|<span data-ttu-id="cc575-143">Entities</span><span class="sxs-lookup"><span data-stu-id="cc575-143">Entities</span></span>|
|-----------|-----------|-----------|
|<span data-ttu-id="cc575-144">"Book a flight to __Seattle__?"</span><span class="sxs-lookup"><span data-stu-id="cc575-144">"Book a flight to __Seattle__?"</span></span>|<span data-ttu-id="cc575-145">BookFlight</span><span class="sxs-lookup"><span data-stu-id="cc575-145">BookFlight</span></span>|<span data-ttu-id="cc575-146">Seattle</span><span class="sxs-lookup"><span data-stu-id="cc575-146">Seattle</span></span>|
|<span data-ttu-id="cc575-147">"When does your store __open__?"</span><span class="sxs-lookup"><span data-stu-id="cc575-147">"When does your store __open__?"</span></span>|<span data-ttu-id="cc575-148">StoreHoursAndLocation</span><span class="sxs-lookup"><span data-stu-id="cc575-148">StoreHoursAndLocation</span></span>|<span data-ttu-id="cc575-149">open</span><span class="sxs-lookup"><span data-stu-id="cc575-149">open</span></span>|
|<span data-ttu-id="cc575-150">"Schedule a meeting at __1pm__ with __Bob__ in Distribution"</span><span class="sxs-lookup"><span data-stu-id="cc575-150">"Schedule a meeting at __1pm__ with __Bob__ in Distribution"</span></span>|<span data-ttu-id="cc575-151">ScheduleMeeting</span><span class="sxs-lookup"><span data-stu-id="cc575-151">ScheduleMeeting</span></span>|<span data-ttu-id="cc575-152">1pm, Bob</span><span class="sxs-lookup"><span data-stu-id="cc575-152">1pm, Bob</span></span>|

<!--
## What is a natural language model?

A model begins with a list of general user intentions, called _intents_, such as "Book Flight" or "Contact Help Desk." You provide user's example text, called _example utterances_ for the intents. Then mark significant words or phrases in the utterance, called _entities_.


A model includes:

* **[intents](#intents)**: categories of user intentions (overall intended action or result)
* **[entities](#entities)**: specific types of data in utterances such as number, email, or name contained in text
* **[example utterances](#example-utterances)**: example text a user might enter in the client application

### Intents 

An [intent](luis-how-to-add-intents.md), short for _intention_, is a purpose or goal expressed in a user's utterance, such as booking a flight, paying a bill, or finding a news article. You create an intent for each action. A LUIS travel app may define an intent named "BookFlight." Each prediction query includes the top scored intent. 

The client application can use the top scoring intent to trigger an action. For example, when "BookFlight" intent is returned from LUIS, a client application could trigger an API call to an external service for booking a plane ticket.

### Entities

An [entity](luis-how-to-add-entities.md) represents detailed information found within the utterance that is relevant to the user's request. For example, in the utterance "Book a ticket to Paris",  a single ticket is requested, and "Paris" is a location. Two entities are found "a ticket" indicating a single ticket and "Paris" indicating the destination. 

After LUIS returns the entities found in the user’s utterance, the client application can use the list of entities as parameters to trigger an action. For example, booking a flight requires entities like the travel destination, date, and airline.
-->
<!--
### Example utterances

An example [utterance](luis-how-to-add-example-utterances.md) is text input from the user that the client application needs to understand. It may be a sentence, like "Book a ticket to Paris", or a fragment of a sentence, like "Booking" or "Paris flight." Utterances aren't always well-formed, and there can be many utterance variations for a particular intent. Add 10 to 20 example utterances to each intent and mark entities in every utterance.

|Example user utterance|Intent|Entities|
|-----------|-----------|-----------|
|"Book a flight to __Seattle__?"|BookFlight|Seattle|
|"When does your store __open__?"|StoreHoursAndLocation|open|
|"Schedule a meeting at __1pm__ with __Bob__ in Distribution"|ScheduleMeeting|1pm, Bob|
-->
## <a name="query-prediction-endpoint"></a><span data-ttu-id="cc575-153">Query prediction endpoint</span><span class="sxs-lookup"><span data-stu-id="cc575-153">Query prediction endpoint</span></span>

<span data-ttu-id="cc575-154">After the model is built and published to the endpoint, the client application sends utterances to the published prediction [endpoint](https://aka.ms/luis-endpoint-apis) API.</span><span class="sxs-lookup"><span data-stu-id="cc575-154">After the model is built and published to the endpoint, the client application sends utterances to the published prediction [endpoint](https://aka.ms/luis-endpoint-apis) API.</span></span> <span data-ttu-id="cc575-155">The API applies the model to the text for analysis.</span><span class="sxs-lookup"><span data-stu-id="cc575-155">The API applies the model to the text for analysis.</span></span> <span data-ttu-id="cc575-156">The API responds with the prediction results in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="cc575-156">The API responds with the prediction results in a JSON format.</span></span>  

<span data-ttu-id="cc575-157">The minimum JSON endpoint response contains the query utterance, and the top scoring intent.</span><span class="sxs-lookup"><span data-stu-id="cc575-157">The minimum JSON endpoint response contains the query utterance, and the top scoring intent.</span></span> <span data-ttu-id="cc575-158">It can also extract data such as the following **Contact Type** entity.</span><span class="sxs-lookup"><span data-stu-id="cc575-158">It can also extract data such as the following **Contact Type** entity.</span></span> 

```JSON
{
  "query": "I want to call my HR rep.",
  "topScoringIntent": {
    "intent": "HRContact",
    "score": 0.921233
  },
  "entities": [
    {
      "entity": "call",
      "type": "Contact Type",
      "startIndex": 10,
      "endIndex": 13,
      "score": 0.7615982
    }
  ]
}
```

## <a name="improve-model-prediction"></a><span data-ttu-id="cc575-159">Improve model prediction</span><span class="sxs-lookup"><span data-stu-id="cc575-159">Improve model prediction</span></span>

<span data-ttu-id="cc575-160">After a LUIS model is published and receives real user utterances, LUIS provides several methods to improve prediction accuracy: [active learning](#active-learning) of endpoint utterances, [phrase lists](#phrase-lists) for domain word inclusion, and [patterns](#patterns) to reduce the number of utterances needed.</span><span class="sxs-lookup"><span data-stu-id="cc575-160">After a LUIS model is published and receives real user utterances, LUIS provides several methods to improve prediction accuracy: [active learning](#active-learning) of endpoint utterances, [phrase lists](#phrase-lists) for domain word inclusion, and [patterns](#patterns) to reduce the number of utterances needed.</span></span>
<!--
### Active learning

In the [active learning](luis-how-to-review-endoint-utt.md) process, LUIS allows you to adapt the LUIS app to real-world utterances by selecting utterances it received at the endpoint for your review. You can accept or correct the endpoint prediction, retrain, and republish. LUIS learns quickly with this iterative process, taking the minimum amount of your time and effort. 

### Phrase lists 

LUIS provides [phrases lists](luis-concept-feature.md) so you can indicate important words or phrases of the model. LUIS uses these lists to add additional significance to those words and phrases that would otherwise not be found in the model.

### Patterns 

Patterns allow you to simplify an intent's utterance collection into common [templates](luis-concept-patterns.md) of word choice and word order. This allows LUIS to learn quicker by needing fewer example utterances for the intents. Patterns are a hybrid system of regular expressions and machine-learned expressions. 
-->
<a name="using-luis"></a>
<!--
## Authoring and accessing models
Author LUIS from the [authoring](https://aka.ms/luis-authoring-apis) APIs or from the LUIS portal. Query the published prediction endpoint of the model from the [endpoint](https://aka.ms/luis-endpoint-apis) APIs.
-->

## <a name="integrating-with-luis"></a><span data-ttu-id="cc575-161">Integrating with LUIS</span><span class="sxs-lookup"><span data-stu-id="cc575-161">Integrating with LUIS</span></span>
<span data-ttu-id="cc575-162">LUIS, as a REST API, can be used with any product, service, or framework that makes an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="cc575-162">LUIS, as a REST API, can be used with any product, service, or framework that makes an HTTP request.</span></span> <span data-ttu-id="cc575-163">The following list contains the top Microsoft products and services used with LUIS.</span><span class="sxs-lookup"><span data-stu-id="cc575-163">The following list contains the top Microsoft products and services used with LUIS.</span></span>

<span data-ttu-id="cc575-164">Microsoft client applications for LUIS include:</span><span class="sxs-lookup"><span data-stu-id="cc575-164">Microsoft client applications for LUIS include:</span></span>
* <span data-ttu-id="cc575-165">[Web app bot](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-3.0) quickly creates a LUIS-enabled chat bot to talk with a user via text input.</span><span class="sxs-lookup"><span data-stu-id="cc575-165">[Web app bot](https://docs.microsoft.com/azure/bot-service/?view=azure-bot-service-3.0) quickly creates a LUIS-enabled chat bot to talk with a user via text input.</span></span> <span data-ttu-id="cc575-166">Uses [Bot Framework][bot-framework] version [3.x](https://github.com/Microsoft/BotBuilder) or [4.x](https://github.com/Microsoft/botbuilder-dotnet) for a complete bot experience.</span><span class="sxs-lookup"><span data-stu-id="cc575-166">Uses [Bot Framework][bot-framework] version [3.x](https://github.com/Microsoft/BotBuilder) or [4.x](https://github.com/Microsoft/botbuilder-dotnet) for a complete bot experience.</span></span>
* <span data-ttu-id="cc575-167">[Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/) - learn more with this [Mixed reality course](https://docs.microsoft.com/windows/mixed-reality/mr-azure-303) with LUIS.</span><span class="sxs-lookup"><span data-stu-id="cc575-167">[Windows Mixed Reality](https://docs.microsoft.com/windows/mixed-reality/) - learn more with this [Mixed reality course](https://docs.microsoft.com/windows/mixed-reality/mr-azure-303) with LUIS.</span></span> 

<span data-ttu-id="cc575-168">Microsoft tools to use LUIS with a bot:</span><span class="sxs-lookup"><span data-stu-id="cc575-168">Microsoft tools to use LUIS with a bot:</span></span>
* <span data-ttu-id="cc575-169">[Dispatch](https://github.com/Microsoft/botbuilder-tools/tree/master/Dispatch) allows several LUIS and QnA Maker apps to be used from a parent app using dispatcher model.</span><span class="sxs-lookup"><span data-stu-id="cc575-169">[Dispatch](https://github.com/Microsoft/botbuilder-tools/tree/master/Dispatch) allows several LUIS and QnA Maker apps to be used from a parent app using dispatcher model.</span></span>
* <span data-ttu-id="cc575-170">[Conversation learner](https://docs.microsoft.com/azure/cognitive-services/labs/conversation-learner/overview) allows you to build bot conversations quicker with LUIS.</span><span class="sxs-lookup"><span data-stu-id="cc575-170">[Conversation learner](https://docs.microsoft.com/azure/cognitive-services/labs/conversation-learner/overview) allows you to build bot conversations quicker with LUIS.</span></span>
* <span data-ttu-id="cc575-171">[Project personality chat](https://docs.microsoft.com/azure/cognitive-services/project-personality-chat/overview) to handle bot small talk.</span><span class="sxs-lookup"><span data-stu-id="cc575-171">[Project personality chat](https://docs.microsoft.com/azure/cognitive-services/project-personality-chat/overview) to handle bot small talk.</span></span>

<span data-ttu-id="cc575-172">Other Cognitive Services used with LUIS:</span><span class="sxs-lookup"><span data-stu-id="cc575-172">Other Cognitive Services used with LUIS:</span></span>
* <span data-ttu-id="cc575-173">[QnA Maker][qnamaker] allows several types of text to combine into a question and answer knowledge base.</span><span class="sxs-lookup"><span data-stu-id="cc575-173">[QnA Maker][qnamaker] allows several types of text to combine into a question and answer knowledge base.</span></span>
* <span data-ttu-id="cc575-174">[Bing Spell Check API](../bing-spell-check/proof-text.md) provides text correction before prediction.</span><span class="sxs-lookup"><span data-stu-id="cc575-174">[Bing Spell Check API](../bing-spell-check/proof-text.md) provides text correction before prediction.</span></span> 
* <span data-ttu-id="cc575-175">[Speech service](../Speech-Service/overview.md) converts spoken language requests into text.</span><span class="sxs-lookup"><span data-stu-id="cc575-175">[Speech service](../Speech-Service/overview.md) converts spoken language requests into text.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="cc575-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc575-176">Next steps</span></span>

<span data-ttu-id="cc575-177">Author a new LUIS app with a [prebuilt](luis-get-started-create-app.md) or [custom](luis-quickstart-intents-only.md) domain.</span><span class="sxs-lookup"><span data-stu-id="cc575-177">Author a new LUIS app with a [prebuilt](luis-get-started-create-app.md) or [custom](luis-quickstart-intents-only.md) domain.</span></span> <span data-ttu-id="cc575-178">[Query the prediction endpoint](luis-get-started-cs-get-intent.md) of a public IoT app.</span><span class="sxs-lookup"><span data-stu-id="cc575-178">[Query the prediction endpoint](luis-get-started-cs-get-intent.md) of a public IoT app.</span></span>

<!-- Reference-style links -->
[bot-framework]: https://docs.microsoft.com/bot-framework/
[flow]: https://docs.microsoft.com/connectors/luis/
[authoring-apis]: https://aka.ms/luis-authoring-api
[endpoint-apis]: https://aka.ms/luis-endpoint-apis
[qnamaker]: https://qnamaker.ai/