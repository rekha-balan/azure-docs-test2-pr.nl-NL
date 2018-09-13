---
title: Data extraction concepts in LUIS - Language Understanding
titleSuffix: Azure Cognitive Services
description: Learn what kind of data can be extracted from Language Understanding (LUIS)
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.openlocfilehash: 40c7e0744825697779e6bd19a78d8d3512b5d63e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864723"
---
# <a name="data-extraction"></a><span data-ttu-id="4469b-103">Data extraction</span><span class="sxs-lookup"><span data-stu-id="4469b-103">Data extraction</span></span>
<span data-ttu-id="4469b-104">LUIS gives you the ability to get information from a user's natural language utterances.</span><span class="sxs-lookup"><span data-stu-id="4469b-104">LUIS gives you the ability to get information from a user's natural language utterances.</span></span> <span data-ttu-id="4469b-105">The information is extracted in a way that it can be used by a program, application, or chatbot to take action.</span><span class="sxs-lookup"><span data-stu-id="4469b-105">The information is extracted in a way that it can be used by a program, application, or chatbot to take action.</span></span>

<span data-ttu-id="4469b-106">In the following sections, learn what data is returned from intents and entities with examples of JSON.</span><span class="sxs-lookup"><span data-stu-id="4469b-106">In the following sections, learn what data is returned from intents and entities with examples of JSON.</span></span> <span data-ttu-id="4469b-107">The hardest data to extract is the machine-learned data because it is not an exact text match.</span><span class="sxs-lookup"><span data-stu-id="4469b-107">The hardest data to extract is the machine-learned data because it is not an exact text match.</span></span> <span data-ttu-id="4469b-108">Data extraction of the machine-learned [entities](luis-concept-entity-types.md) needs to be part of the [authoring cycle](luis-concept-app-iteration.md) until you are confident you receive the data you expect.</span><span class="sxs-lookup"><span data-stu-id="4469b-108">Data extraction of the machine-learned [entities](luis-concept-entity-types.md) needs to be part of the [authoring cycle](luis-concept-app-iteration.md) until you are confident you receive the data you expect.</span></span> 

## <a name="data-location-and-key-usage"></a><span data-ttu-id="4469b-109">Data location and key usage</span><span class="sxs-lookup"><span data-stu-id="4469b-109">Data location and key usage</span></span>
<span data-ttu-id="4469b-110">LUIS provides the data from the published [endpoint](luis-glossary.md#endpoint).</span><span class="sxs-lookup"><span data-stu-id="4469b-110">LUIS provides the data from the published [endpoint](luis-glossary.md#endpoint).</span></span> <span data-ttu-id="4469b-111">The **HTTPS request** (POST or GET) contains the utterance as well as some optional configurations such as staging or production environments.</span><span class="sxs-lookup"><span data-stu-id="4469b-111">The **HTTPS request** (POST or GET) contains the utterance as well as some optional configurations such as staging or production environments.</span></span> 

`https://westus.api.cognitive.microsoft.com/luis/v2.0/apps/<appID>?subscription-key=<subscription-key>&verbose=true&timezoneOffset=0&q=book 2 tickets to paris`

<span data-ttu-id="4469b-112">The `appID` is available on the **Settings** page of your LUIS app as well as part of the URL (after `/apps/`) when you are editing that LUIS app.</span><span class="sxs-lookup"><span data-stu-id="4469b-112">The `appID` is available on the **Settings** page of your LUIS app as well as part of the URL (after `/apps/`) when you are editing that LUIS app.</span></span> <span data-ttu-id="4469b-113">The `subscription-key` is the endpoint key used for querying your app.</span><span class="sxs-lookup"><span data-stu-id="4469b-113">The `subscription-key` is the endpoint key used for querying your app.</span></span> <span data-ttu-id="4469b-114">While you can use your free authoring/starter key while you are learning LUIS, it is important to change the endpoint key to a key that supports your [expected LUIS usage](luis-boundaries.md#key-limits).</span><span class="sxs-lookup"><span data-stu-id="4469b-114">While you can use your free authoring/starter key while you are learning LUIS, it is important to change the endpoint key to a key that supports your [expected LUIS usage](luis-boundaries.md#key-limits).</span></span> <span data-ttu-id="4469b-115">The `timezoneOffset` unit is minutes.</span><span class="sxs-lookup"><span data-stu-id="4469b-115">The `timezoneOffset` unit is minutes.</span></span>

<span data-ttu-id="4469b-116">The **HTTPS response** contains all the intent and entity information LUIS can determine based on the current published model of either the staging or production endpoint.</span><span class="sxs-lookup"><span data-stu-id="4469b-116">The **HTTPS response** contains all the intent and entity information LUIS can determine based on the current published model of either the staging or production endpoint.</span></span> <span data-ttu-id="4469b-117">The endpoint URL is found on the [LUIS](luis-reference-regions.md) website **Publish** page.</span><span class="sxs-lookup"><span data-stu-id="4469b-117">The endpoint URL is found on the [LUIS](luis-reference-regions.md) website **Publish** page.</span></span> 

## <a name="data-from-intents"></a><span data-ttu-id="4469b-118">Data from intents</span><span class="sxs-lookup"><span data-stu-id="4469b-118">Data from intents</span></span>
<span data-ttu-id="4469b-119">The primary data is the top scoring **intent name**.</span><span class="sxs-lookup"><span data-stu-id="4469b-119">The primary data is the top scoring **intent name**.</span></span> <span data-ttu-id="4469b-120">Using the `MyStore` [quickstart](luis-quickstart-intents-only.md), the endpoint response is:</span><span class="sxs-lookup"><span data-stu-id="4469b-120">Using the `MyStore` [quickstart](luis-quickstart-intents-only.md), the endpoint response is:</span></span>

```JSON
{
  "query": "when do you open next?",
  "topScoringIntent": {
    "intent": "GetStoreInfo",
    "score": 0.984749258
  },
  "entities": []
}
```

|<span data-ttu-id="4469b-121">Data Object</span><span class="sxs-lookup"><span data-stu-id="4469b-121">Data Object</span></span>|<span data-ttu-id="4469b-122">Data Type</span><span class="sxs-lookup"><span data-stu-id="4469b-122">Data Type</span></span>|<span data-ttu-id="4469b-123">Data Location</span><span class="sxs-lookup"><span data-stu-id="4469b-123">Data Location</span></span>|<span data-ttu-id="4469b-124">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-124">Value</span></span>|
|--|--|--|--|
|<span data-ttu-id="4469b-125">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-125">Intent</span></span>|<span data-ttu-id="4469b-126">String</span><span class="sxs-lookup"><span data-stu-id="4469b-126">String</span></span>|<span data-ttu-id="4469b-127">topScoringIntent.intent</span><span class="sxs-lookup"><span data-stu-id="4469b-127">topScoringIntent.intent</span></span>|<span data-ttu-id="4469b-128">"GetStoreInfo"</span><span class="sxs-lookup"><span data-stu-id="4469b-128">"GetStoreInfo"</span></span>|

<span data-ttu-id="4469b-129">If your chatbot or LUIS-calling app makes a decision based on more than one intent score, return all the intents' scores by setting the querystring parameter, `verbose=true`.</span><span class="sxs-lookup"><span data-stu-id="4469b-129">If your chatbot or LUIS-calling app makes a decision based on more than one intent score, return all the intents' scores by setting the querystring parameter, `verbose=true`.</span></span> <span data-ttu-id="4469b-130">The endpoint response is:</span><span class="sxs-lookup"><span data-stu-id="4469b-130">The endpoint response is:</span></span>

```JSON
{
  "query": "when do you open next?",
  "topScoringIntent": {
    "intent": "GetStoreInfo",
    "score": 0.984749258
  },
  "intents": [
    {
      "intent": "GetStoreInfo",
      "score": 0.984749258
    },
    {
      "intent": "None",
      "score": 0.2040639
    }
  ],
  "entities": []
}
```

<span data-ttu-id="4469b-131">The intents are ordered from highest to lowest score.</span><span class="sxs-lookup"><span data-stu-id="4469b-131">The intents are ordered from highest to lowest score.</span></span>

|<span data-ttu-id="4469b-132">Data Object</span><span class="sxs-lookup"><span data-stu-id="4469b-132">Data Object</span></span>|<span data-ttu-id="4469b-133">Data Type</span><span class="sxs-lookup"><span data-stu-id="4469b-133">Data Type</span></span>|<span data-ttu-id="4469b-134">Data Location</span><span class="sxs-lookup"><span data-stu-id="4469b-134">Data Location</span></span>|<span data-ttu-id="4469b-135">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-135">Value</span></span>|<span data-ttu-id="4469b-136">Score</span><span class="sxs-lookup"><span data-stu-id="4469b-136">Score</span></span>|
|--|--|--|--|:--|
|<span data-ttu-id="4469b-137">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-137">Intent</span></span>|<span data-ttu-id="4469b-138">String</span><span class="sxs-lookup"><span data-stu-id="4469b-138">String</span></span>|<span data-ttu-id="4469b-139">intents[0].intent</span><span class="sxs-lookup"><span data-stu-id="4469b-139">intents[0].intent</span></span>|<span data-ttu-id="4469b-140">"GetStoreInfo"</span><span class="sxs-lookup"><span data-stu-id="4469b-140">"GetStoreInfo"</span></span>|<span data-ttu-id="4469b-141">0.984749258</span><span class="sxs-lookup"><span data-stu-id="4469b-141">0.984749258</span></span>|
|<span data-ttu-id="4469b-142">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-142">Intent</span></span>|<span data-ttu-id="4469b-143">String</span><span class="sxs-lookup"><span data-stu-id="4469b-143">String</span></span>|<span data-ttu-id="4469b-144">intents[1].intent</span><span class="sxs-lookup"><span data-stu-id="4469b-144">intents[1].intent</span></span>|<span data-ttu-id="4469b-145">"None"</span><span class="sxs-lookup"><span data-stu-id="4469b-145">"None"</span></span>|<span data-ttu-id="4469b-146">0.0168218873</span><span class="sxs-lookup"><span data-stu-id="4469b-146">0.0168218873</span></span>|

<span data-ttu-id="4469b-147">If you add prebuilt domains, the intent name indicates the domain, such as `Utilties` or `Communication` as well as the intent:</span><span class="sxs-lookup"><span data-stu-id="4469b-147">If you add prebuilt domains, the intent name indicates the domain, such as `Utilties` or `Communication` as well as the intent:</span></span>

```JSON
{
  "query": "Turn on the lights next monday at 9am",
  "topScoringIntent": {
    "intent": "Utilities.ShowNext",
    "score": 0.07842206
  },
  "intents": [
    {
      "intent": "Utilities.ShowNext",
      "score": 0.07842206
    },
    {
      "intent": "Communication.StartOver",
      "score": 0.0239675418
    },
    {
      "intent": "None",
      "score": 0.0168218873
    }],
  "entities": []
}
```
    
|<span data-ttu-id="4469b-148">Domain</span><span class="sxs-lookup"><span data-stu-id="4469b-148">Domain</span></span>|<span data-ttu-id="4469b-149">Data Object</span><span class="sxs-lookup"><span data-stu-id="4469b-149">Data Object</span></span>|<span data-ttu-id="4469b-150">Data Type</span><span class="sxs-lookup"><span data-stu-id="4469b-150">Data Type</span></span>|<span data-ttu-id="4469b-151">Data Location</span><span class="sxs-lookup"><span data-stu-id="4469b-151">Data Location</span></span>|<span data-ttu-id="4469b-152">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-152">Value</span></span>|
|--|--|--|--|--|
|<span data-ttu-id="4469b-153">Utilities</span><span class="sxs-lookup"><span data-stu-id="4469b-153">Utilities</span></span>|<span data-ttu-id="4469b-154">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-154">Intent</span></span>|<span data-ttu-id="4469b-155">String</span><span class="sxs-lookup"><span data-stu-id="4469b-155">String</span></span>|<span data-ttu-id="4469b-156">intents[0].intent</span><span class="sxs-lookup"><span data-stu-id="4469b-156">intents[0].intent</span></span>|<span data-ttu-id="4469b-157">"<b>Utilities</b>.ShowNext"</span><span class="sxs-lookup"><span data-stu-id="4469b-157">"<b>Utilities</b>.ShowNext"</span></span>|
|<span data-ttu-id="4469b-158">Communication</span><span class="sxs-lookup"><span data-stu-id="4469b-158">Communication</span></span>|<span data-ttu-id="4469b-159">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-159">Intent</span></span>|<span data-ttu-id="4469b-160">String</span><span class="sxs-lookup"><span data-stu-id="4469b-160">String</span></span>|<span data-ttu-id="4469b-161">intents[1].intent</span><span class="sxs-lookup"><span data-stu-id="4469b-161">intents[1].intent</span></span>|<span data-ttu-id="4469b-162"><b>Communication</b>.StartOver"</span><span class="sxs-lookup"><span data-stu-id="4469b-162"><b>Communication</b>.StartOver"</span></span>|
||<span data-ttu-id="4469b-163">Intent</span><span class="sxs-lookup"><span data-stu-id="4469b-163">Intent</span></span>|<span data-ttu-id="4469b-164">String</span><span class="sxs-lookup"><span data-stu-id="4469b-164">String</span></span>|<span data-ttu-id="4469b-165">intents[2].intent</span><span class="sxs-lookup"><span data-stu-id="4469b-165">intents[2].intent</span></span>|<span data-ttu-id="4469b-166">"None"</span><span class="sxs-lookup"><span data-stu-id="4469b-166">"None"</span></span>|


## <a name="data-from-entities"></a><span data-ttu-id="4469b-167">Data from entities</span><span class="sxs-lookup"><span data-stu-id="4469b-167">Data from entities</span></span>
<span data-ttu-id="4469b-168">Most chatbots and applications need more than the intent name.</span><span class="sxs-lookup"><span data-stu-id="4469b-168">Most chatbots and applications need more than the intent name.</span></span> <span data-ttu-id="4469b-169">This additional, optional data comes from entities discovered in the utterance.</span><span class="sxs-lookup"><span data-stu-id="4469b-169">This additional, optional data comes from entities discovered in the utterance.</span></span> <span data-ttu-id="4469b-170">Each type of entity returns different information about the match.</span><span class="sxs-lookup"><span data-stu-id="4469b-170">Each type of entity returns different information about the match.</span></span> 

<span data-ttu-id="4469b-171">A single word or phrase in an utterance can match more than one entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-171">A single word or phrase in an utterance can match more than one entity.</span></span> <span data-ttu-id="4469b-172">In that case, each matching entity is returned with its score.</span><span class="sxs-lookup"><span data-stu-id="4469b-172">In that case, each matching entity is returned with its score.</span></span> 

<span data-ttu-id="4469b-173">All entities are returned in the **entities** array of the response from the endpoint:</span><span class="sxs-lookup"><span data-stu-id="4469b-173">All entities are returned in the **entities** array of the response from the endpoint:</span></span>

```JSON
"entities": [
  {
    "entity": "bob jones",
    "type": "Name",
    "startIndex": 0,
    "endIndex": 8,
    "score": 0.473899543
  },
  {
    "entity": "3",
    "type": "builtin.number",
    "startIndex": 16,
    "endIndex": 16,
    "resolution": {
      "value": "3"
    }
  }
]
```

## <a name="tokenized-entity-returned"></a><span data-ttu-id="4469b-174">Tokenized entity returned</span><span class="sxs-lookup"><span data-stu-id="4469b-174">Tokenized entity returned</span></span>
<span data-ttu-id="4469b-175">Several [cultures](luis-supported-languages.md#tokenization) return the entity object with the `entity` value [tokenized](luis-glossary.md#token).</span><span class="sxs-lookup"><span data-stu-id="4469b-175">Several [cultures](luis-supported-languages.md#tokenization) return the entity object with the `entity` value [tokenized](luis-glossary.md#token).</span></span> <span data-ttu-id="4469b-176">The startIndex and endIndex returned by LUIS in the entity object do not map to the new, tokenized value but instead to the original query in order for you to extract the raw entity programmatically.</span><span class="sxs-lookup"><span data-stu-id="4469b-176">The startIndex and endIndex returned by LUIS in the entity object do not map to the new, tokenized value but instead to the original query in order for you to extract the raw entity programmatically.</span></span> 

<span data-ttu-id="4469b-177">For example, in German, the word `das Bauernbrot` is tokenized into `das bauern brot`.</span><span class="sxs-lookup"><span data-stu-id="4469b-177">For example, in German, the word `das Bauernbrot` is tokenized into `das bauern brot`.</span></span> <span data-ttu-id="4469b-178">The tokenized value, `das bauern brot`, is returned and the original value can be programmatically determined from the startIndex and endIndex of the original query, giving you `das Bauernbrot`.</span><span class="sxs-lookup"><span data-stu-id="4469b-178">The tokenized value, `das bauern brot`, is returned and the original value can be programmatically determined from the startIndex and endIndex of the original query, giving you `das Bauernbrot`.</span></span>

## <a name="simple-entity-data"></a><span data-ttu-id="4469b-179">Simple entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-179">Simple entity data</span></span>

<span data-ttu-id="4469b-180">A [simple entity](luis-concept-entity-types.md) is a machine-learned value.</span><span class="sxs-lookup"><span data-stu-id="4469b-180">A [simple entity](luis-concept-entity-types.md) is a machine-learned value.</span></span> <span data-ttu-id="4469b-181">It can be a word or phrase.</span><span class="sxs-lookup"><span data-stu-id="4469b-181">It can be a word or phrase.</span></span> 

`Bob Jones wants 3 meatball pho`

<span data-ttu-id="4469b-182">In the previous utterance, `Bob Jones` is labeled as a simple `Customer` entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-182">In the previous utterance, `Bob Jones` is labeled as a simple `Customer` entity.</span></span>

<span data-ttu-id="4469b-183">The data returned from the endpoint includes the entity name, the discovered text from the utterance, the location of the discovered text, and the score:</span><span class="sxs-lookup"><span data-stu-id="4469b-183">The data returned from the endpoint includes the entity name, the discovered text from the utterance, the location of the discovered text, and the score:</span></span>

```JSON
"entities": [
  {
  "entity": "bob jones",
  "type": "Customer",
  "startIndex": 0,
  "endIndex": 8,
  "score": 0.473899543
  }
]
```

|<span data-ttu-id="4469b-184">Data object</span><span class="sxs-lookup"><span data-stu-id="4469b-184">Data object</span></span>|<span data-ttu-id="4469b-185">Entity name</span><span class="sxs-lookup"><span data-stu-id="4469b-185">Entity name</span></span>|<span data-ttu-id="4469b-186">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-186">Value</span></span>|
|--|--|--|
|<span data-ttu-id="4469b-187">Simple Entity</span><span class="sxs-lookup"><span data-stu-id="4469b-187">Simple Entity</span></span>|<span data-ttu-id="4469b-188">"Customer"</span><span class="sxs-lookup"><span data-stu-id="4469b-188">"Customer"</span></span>|<span data-ttu-id="4469b-189">"bob jones"</span><span class="sxs-lookup"><span data-stu-id="4469b-189">"bob jones"</span></span>|

## <a name="hierarchical-entity-data"></a><span data-ttu-id="4469b-190">Hierarchical entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-190">Hierarchical entity data</span></span>

<span data-ttu-id="4469b-191">[Hierarchical](luis-concept-entity-types.md) entities are machine-learned and can include a word or phrase.</span><span class="sxs-lookup"><span data-stu-id="4469b-191">[Hierarchical](luis-concept-entity-types.md) entities are machine-learned and can include a word or phrase.</span></span> <span data-ttu-id="4469b-192">Children are identified by context.</span><span class="sxs-lookup"><span data-stu-id="4469b-192">Children are identified by context.</span></span> <span data-ttu-id="4469b-193">If you are looking for a parent-child relationship with exact text match, use a [List](#list-entity-data) entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-193">If you are looking for a parent-child relationship with exact text match, use a [List](#list-entity-data) entity.</span></span> 

`book 2 tickets to paris`

<span data-ttu-id="4469b-194">In the previous utterance, `paris` is labeled a `Location::ToLocation` child of the `Location` hierarchical entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-194">In the previous utterance, `paris` is labeled a `Location::ToLocation` child of the `Location` hierarchical entity.</span></span> 

<span data-ttu-id="4469b-195">The data returned from the endpoint includes the entity name and child name, the discovered text from the utterance, the location of the discovered text, and the score:</span><span class="sxs-lookup"><span data-stu-id="4469b-195">The data returned from the endpoint includes the entity name and child name, the discovered text from the utterance, the location of the discovered text, and the score:</span></span> 

```JSON
"entities": [
  {
    "entity": "paris",
    "type": "Location::ToLocation",
    "startIndex": 18,
    "endIndex": 22,
    "score": 0.6866132
  }
]
```

|<span data-ttu-id="4469b-196">Data object</span><span class="sxs-lookup"><span data-stu-id="4469b-196">Data object</span></span>|<span data-ttu-id="4469b-197">Parent</span><span class="sxs-lookup"><span data-stu-id="4469b-197">Parent</span></span>|<span data-ttu-id="4469b-198">Child</span><span class="sxs-lookup"><span data-stu-id="4469b-198">Child</span></span>|<span data-ttu-id="4469b-199">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-199">Value</span></span>|
|--|--|--|--|--|
|<span data-ttu-id="4469b-200">Hierarchical Entity</span><span class="sxs-lookup"><span data-stu-id="4469b-200">Hierarchical Entity</span></span>|<span data-ttu-id="4469b-201">Location</span><span class="sxs-lookup"><span data-stu-id="4469b-201">Location</span></span>|<span data-ttu-id="4469b-202">ToLocation</span><span class="sxs-lookup"><span data-stu-id="4469b-202">ToLocation</span></span>|<span data-ttu-id="4469b-203">"paris"</span><span class="sxs-lookup"><span data-stu-id="4469b-203">"paris"</span></span>|

## <a name="composite-entity-data"></a><span data-ttu-id="4469b-204">Composite entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-204">Composite entity data</span></span>
<span data-ttu-id="4469b-205">[Composite](luis-concept-entity-types.md) entities are machine-learned and can include a word or phrase.</span><span class="sxs-lookup"><span data-stu-id="4469b-205">[Composite](luis-concept-entity-types.md) entities are machine-learned and can include a word or phrase.</span></span> <span data-ttu-id="4469b-206">For example, consider a composite entity of prebuilt `number` and `Location::ToLocation` with the following utterance:</span><span class="sxs-lookup"><span data-stu-id="4469b-206">For example, consider a composite entity of prebuilt `number` and `Location::ToLocation` with the following utterance:</span></span>

`book 2 tickets to paris`

<span data-ttu-id="4469b-207">Notice that `2`, the number, and `paris`, the ToLocation have words between them that are not part of any of the entities.</span><span class="sxs-lookup"><span data-stu-id="4469b-207">Notice that `2`, the number, and `paris`, the ToLocation have words between them that are not part of any of the entities.</span></span> <span data-ttu-id="4469b-208">The green underline, used in a labeled utterance in the [LUIS](luis-reference-regions.md) website, indicates a composite entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-208">The green underline, used in a labeled utterance in the [LUIS](luis-reference-regions.md) website, indicates a composite entity.</span></span>

![Composite Entity](./media/luis-concept-data-extraction/composite-entity.png)

<span data-ttu-id="4469b-210">Composite entities are returned in a `compositeEntities` array and all entities within the composite are also returned in the `entities` array:</span><span class="sxs-lookup"><span data-stu-id="4469b-210">Composite entities are returned in a `compositeEntities` array and all entities within the composite are also returned in the `entities` array:</span></span>

```JSON
  "entities": [
    {
      "entity": "paris",
      "type": "Location::ToLocation",
      "startIndex": 18,
      "endIndex": 22,
      "score": 0.956998169
    },
    {
      "entity": "2",
      "type": "builtin.number",
      "startIndex": 5,
      "endIndex": 5,
      "resolution": {
        "value": "2"
      }
    },
    {
      "entity": "2 tickets to paris",
      "type": "Order",
      "startIndex": 5,
      "endIndex": 22,
      "score": 0.7714499
    }
  ],
  "compositeEntities": [
    {
      "parentType": "Order",
      "value": "2 tickets to paris",
      "children": [
        {
          "type": "builtin.number",
          "value": "2"
        },
        {
          "type": "Location::ToLocation",
          "value": "paris"
        }
      ]
    }
  ]
```    

|<span data-ttu-id="4469b-211">Data object</span><span class="sxs-lookup"><span data-stu-id="4469b-211">Data object</span></span>|<span data-ttu-id="4469b-212">Entity name</span><span class="sxs-lookup"><span data-stu-id="4469b-212">Entity name</span></span>|<span data-ttu-id="4469b-213">Value</span><span class="sxs-lookup"><span data-stu-id="4469b-213">Value</span></span>|
|--|--|--|
|<span data-ttu-id="4469b-214">Prebuilt Entity - number</span><span class="sxs-lookup"><span data-stu-id="4469b-214">Prebuilt Entity - number</span></span>|<span data-ttu-id="4469b-215">"builtin.number"</span><span class="sxs-lookup"><span data-stu-id="4469b-215">"builtin.number"</span></span>|<span data-ttu-id="4469b-216">"2"</span><span class="sxs-lookup"><span data-stu-id="4469b-216">"2"</span></span>|
|<span data-ttu-id="4469b-217">Hierarchical Entity - Location</span><span class="sxs-lookup"><span data-stu-id="4469b-217">Hierarchical Entity - Location</span></span>|<span data-ttu-id="4469b-218">"Location::ToLocation"</span><span class="sxs-lookup"><span data-stu-id="4469b-218">"Location::ToLocation"</span></span>|<span data-ttu-id="4469b-219">"paris"</span><span class="sxs-lookup"><span data-stu-id="4469b-219">"paris"</span></span>|

## <a name="list-entity-data"></a><span data-ttu-id="4469b-220">List entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-220">List entity data</span></span>

<span data-ttu-id="4469b-221">A [list](luis-concept-entity-types.md) entity is not machine-learned.</span><span class="sxs-lookup"><span data-stu-id="4469b-221">A [list](luis-concept-entity-types.md) entity is not machine-learned.</span></span> <span data-ttu-id="4469b-222">It is an exact text match.</span><span class="sxs-lookup"><span data-stu-id="4469b-222">It is an exact text match.</span></span> <span data-ttu-id="4469b-223">A list represents items in the list along with synonyms for those items.</span><span class="sxs-lookup"><span data-stu-id="4469b-223">A list represents items in the list along with synonyms for those items.</span></span> <span data-ttu-id="4469b-224">LUIS marks any match to an item in any list as an entity in the response.</span><span class="sxs-lookup"><span data-stu-id="4469b-224">LUIS marks any match to an item in any list as an entity in the response.</span></span> <span data-ttu-id="4469b-225">A synonym can be in more than one list.</span><span class="sxs-lookup"><span data-stu-id="4469b-225">A synonym can be in more than one list.</span></span> 

<span data-ttu-id="4469b-226">Suppose the app has a list, named `Cities`, allowing for variations of city names including city of airport (Sea-tac), airport code (SEA), postal zip code (98101), and phone area code (206).</span><span class="sxs-lookup"><span data-stu-id="4469b-226">Suppose the app has a list, named `Cities`, allowing for variations of city names including city of airport (Sea-tac), airport code (SEA), postal zip code (98101), and phone area code (206).</span></span> 

|<span data-ttu-id="4469b-227">List item</span><span class="sxs-lookup"><span data-stu-id="4469b-227">List item</span></span>|<span data-ttu-id="4469b-228">Item synonyms</span><span class="sxs-lookup"><span data-stu-id="4469b-228">Item synonyms</span></span>|
|---|---|
|<span data-ttu-id="4469b-229">Seattle</span><span class="sxs-lookup"><span data-stu-id="4469b-229">Seattle</span></span>|<span data-ttu-id="4469b-230">sea-tac, sea, 98101, 206, +1</span><span class="sxs-lookup"><span data-stu-id="4469b-230">sea-tac, sea, 98101, 206, +1</span></span> |
|<span data-ttu-id="4469b-231">Paris</span><span class="sxs-lookup"><span data-stu-id="4469b-231">Paris</span></span>|<span data-ttu-id="4469b-232">cdg, roissy, ory, 75001, 1, +33</span><span class="sxs-lookup"><span data-stu-id="4469b-232">cdg, roissy, ory, 75001, 1, +33</span></span>|

`book 2 tickets to paris`

<span data-ttu-id="4469b-233">In the previous utterance, the word `paris` is mapped to the paris item as part of the `Cities` list entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-233">In the previous utterance, the word `paris` is mapped to the paris item as part of the `Cities` list entity.</span></span> <span data-ttu-id="4469b-234">The list entity matches both the item's normalized name as well as the item synonyms.</span><span class="sxs-lookup"><span data-stu-id="4469b-234">The list entity matches both the item's normalized name as well as the item synonyms.</span></span> 

```JSON
"entities": [
  {
    "entity": "paris",
    "type": "Cities",
    "startIndex": 18,
    "endIndex": 22,
    "resolution": {
      "values": [
        "Paris"
      ]
    }
  }
]
```

<span data-ttu-id="4469b-235">Another example utterance, using a synonym for Paris:</span><span class="sxs-lookup"><span data-stu-id="4469b-235">Another example utterance, using a synonym for Paris:</span></span>

`book 2 tickets to roissy`

```JSON
"entities": [
  {
    "entity": "roissy",
    "type": "Cities",
    "startIndex": 18,
    "endIndex": 23,
    "resolution": {
      "values": [
        "Paris"
      ]
    }
  }
]
```

## <a name="prebuilt-entity-data"></a><span data-ttu-id="4469b-236">Prebuilt entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-236">Prebuilt entity data</span></span>
<span data-ttu-id="4469b-237">[Prebuilt](luis-concept-entity-types.md) entities are discovered based on a regular expression match using the open-source [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text) project.</span><span class="sxs-lookup"><span data-stu-id="4469b-237">[Prebuilt](luis-concept-entity-types.md) entities are discovered based on a regular expression match using the open-source [Recognizers-Text](https://github.com/Microsoft/Recognizers-Text) project.</span></span> <span data-ttu-id="4469b-238">Prebuilt entities are returned in the entities array and use the type name prefixed with `builtin::`.</span><span class="sxs-lookup"><span data-stu-id="4469b-238">Prebuilt entities are returned in the entities array and use the type name prefixed with `builtin::`.</span></span> <span data-ttu-id="4469b-239">The following text is an example utterance with the returned prebuilt entities:</span><span class="sxs-lookup"><span data-stu-id="4469b-239">The following text is an example utterance with the returned prebuilt entities:</span></span>

`Dec 5th send to +1 360-555-1212`

```JSON
"entities": [
    {
      "entity": "dec 5th",
      "type": "builtin.datetimeV2.date",
      "startIndex": 0,
      "endIndex": 6,
      "resolution": {
        "values": [
          {
            "timex": "XXXX-12-05",
            "type": "date",
            "value": "2017-12-05"
          },
          {
            "timex": "XXXX-12-05",
            "type": "date",
            "value": "2018-12-05"
          }
        ]
      }
    },
    {
      "entity": "1",
      "type": "builtin.number",
      "startIndex": 18,
      "endIndex": 18,
      "resolution": {
        "value": "1"
      }
    },
    {
      "entity": "360",
      "type": "builtin.number",
      "startIndex": 20,
      "endIndex": 22,
      "resolution": {
        "value": "360"
      }
    },
    {
      "entity": "555",
      "type": "builtin.number",
      "startIndex": 26,
      "endIndex": 28,
      "resolution": {
        "value": "555"
      }
    },
    {
      "entity": "1212",
      "type": "builtin.number",
      "startIndex": 32,
      "endIndex": 35,
      "resolution": {
        "value": "1212"
      }
    },
    {
      "entity": "5th",
      "type": "builtin.ordinal",
      "startIndex": 4,
      "endIndex": 6,
      "resolution": {
        "value": "5"
      }
    },
    {
      "entity": "1 360 - 555 - 1212",
      "type": "builtin.phonenumber",
      "startIndex": 18,
      "endIndex": 35,
      "resolution": {
        "value": "1 360 - 555 - 1212"
      }
    }
  ]
``` 

## <a name="regular-expression-entity-data"></a><span data-ttu-id="4469b-240">Regular expression entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-240">Regular expression entity data</span></span>
<span data-ttu-id="4469b-241">[Regular expression](luis-concept-entity-types.md) entities are discovered based on a regular expression match using an expression you provide when you create the entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-241">[Regular expression](luis-concept-entity-types.md) entities are discovered based on a regular expression match using an expression you provide when you create the entity.</span></span> <span data-ttu-id="4469b-242">When using `kb[0-9]{6}` as the regular expression entity definition, the following JSON response is an example utterance with the returned regular expression entities for the query `When was kb123456 published?`:</span><span class="sxs-lookup"><span data-stu-id="4469b-242">When using `kb[0-9]{6}` as the regular expression entity definition, the following JSON response is an example utterance with the returned regular expression entities for the query `When was kb123456 published?`:</span></span>

```JSON
{
  "query": "when was kb123456 published?",
  "topScoringIntent": {
    "intent": "FindKBArticle",
    "score": 0.933641255
  },
  "intents": [
    {
      "intent": "FindKBArticle",
      "score": 0.933641255
    },
    {
      "intent": "None",
      "score": 0.04397359
    }
  ],
  "entities": [
    {
      "entity": "kb123456",
      "type": "KB number",
      "startIndex": 9,
      "endIndex": 16
    }
  ]
}
```

## <a name="extracting-names"></a><span data-ttu-id="4469b-243">Extracting names</span><span class="sxs-lookup"><span data-stu-id="4469b-243">Extracting names</span></span>
<span data-ttu-id="4469b-244">Getting names from an utterance is difficult because a name can be almost any combination of letters and words.</span><span class="sxs-lookup"><span data-stu-id="4469b-244">Getting names from an utterance is difficult because a name can be almost any combination of letters and words.</span></span> <span data-ttu-id="4469b-245">Depending on what type of name you are extracting, you have several options.</span><span class="sxs-lookup"><span data-stu-id="4469b-245">Depending on what type of name you are extracting, you have several options.</span></span> <span data-ttu-id="4469b-246">These are not rules but more guidelines.</span><span class="sxs-lookup"><span data-stu-id="4469b-246">These are not rules but more guidelines.</span></span> 

### <a name="names-of-people"></a><span data-ttu-id="4469b-247">Names of people</span><span class="sxs-lookup"><span data-stu-id="4469b-247">Names of people</span></span>
<span data-ttu-id="4469b-248">People's name can have some slight format depending on language and culture.</span><span class="sxs-lookup"><span data-stu-id="4469b-248">People's name can have some slight format depending on language and culture.</span></span> <span data-ttu-id="4469b-249">Use either a hierarchical entity with first and last names as children or use a simple entity with roles of first and last name.</span><span class="sxs-lookup"><span data-stu-id="4469b-249">Use either a hierarchical entity with first and last names as children or use a simple entity with roles of first and last name.</span></span> <span data-ttu-id="4469b-250">Make sure to give examples that use the first and last name in different parts of the utterance, in utterances of different lengths, and utterances across all intents including the None intent.</span><span class="sxs-lookup"><span data-stu-id="4469b-250">Make sure to give examples that use the first and last name in different parts of the utterance, in utterances of different lengths, and utterances across all intents including the None intent.</span></span> <span data-ttu-id="4469b-251">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span><span class="sxs-lookup"><span data-stu-id="4469b-251">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span></span> 

### <a name="names-of-places"></a><span data-ttu-id="4469b-252">Names of places</span><span class="sxs-lookup"><span data-stu-id="4469b-252">Names of places</span></span>
<span data-ttu-id="4469b-253">Location names are set and known such as cities, counties, states, provinces, and countries.</span><span class="sxs-lookup"><span data-stu-id="4469b-253">Location names are set and known such as cities, counties, states, provinces, and countries.</span></span> <span data-ttu-id="4469b-254">If your app uses a know set of locations, consider a list entity.</span><span class="sxs-lookup"><span data-stu-id="4469b-254">If your app uses a know set of locations, consider a list entity.</span></span> <span data-ttu-id="4469b-255">If you need to find all place names, create a simple entity, and provide a variety of examples.</span><span class="sxs-lookup"><span data-stu-id="4469b-255">If you need to find all place names, create a simple entity, and provide a variety of examples.</span></span> <span data-ttu-id="4469b-256">Add a phrase list of place names to reinforce what place names look like in your app.</span><span class="sxs-lookup"><span data-stu-id="4469b-256">Add a phrase list of place names to reinforce what place names look like in your app.</span></span> <span data-ttu-id="4469b-257">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span><span class="sxs-lookup"><span data-stu-id="4469b-257">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span></span> 

### <a name="new-and-emerging-names"></a><span data-ttu-id="4469b-258">New and emerging names</span><span class="sxs-lookup"><span data-stu-id="4469b-258">New and emerging names</span></span>
<span data-ttu-id="4469b-259">Some apps need to be able to find new and emerging names such as products or companies.</span><span class="sxs-lookup"><span data-stu-id="4469b-259">Some apps need to be able to find new and emerging names such as products or companies.</span></span> <span data-ttu-id="4469b-260">This is the most difficult type of data extraction.</span><span class="sxs-lookup"><span data-stu-id="4469b-260">This is the most difficult type of data extraction.</span></span> <span data-ttu-id="4469b-261">Begin with a simple entity and add a phrase list.</span><span class="sxs-lookup"><span data-stu-id="4469b-261">Begin with a simple entity and add a phrase list.</span></span> <span data-ttu-id="4469b-262">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span><span class="sxs-lookup"><span data-stu-id="4469b-262">[Review](luis-how-to-review-endoint-utt.md) endpoint utterances on a regular basis to label any names that were not predicted correctly.</span></span> 

## <a name="pattern-roles-data"></a><span data-ttu-id="4469b-263">Pattern roles data</span><span class="sxs-lookup"><span data-stu-id="4469b-263">Pattern roles data</span></span>
<span data-ttu-id="4469b-264">Roles are contextual differences of entities.</span><span class="sxs-lookup"><span data-stu-id="4469b-264">Roles are contextual differences of entities.</span></span> 

```JSON
{
  "query": "move bob jones from seattle to redmond",
  "topScoringIntent": {
    "intent": "MoveAssetsOrPeople",
    "score": 0.9999998
  },
  "intents": [
    {
      "intent": "MoveAssetsOrPeople",
      "score": 0.9999998
    },
    {
      "intent": "None",
      "score": 1.02040713E-06
    },
    {
      "intent": "GetEmployeeBenefits",
      "score": 6.12244548E-07
    },
    {
      "intent": "GetEmployeeOrgChart",
      "score": 6.12244548E-07
    },
    {
      "intent": "FindForm",
      "score": 1.1E-09
    }
  ],
  "entities": [
    {
      "entity": "bob jones",
      "type": "Employee",
      "startIndex": 5,
      "endIndex": 13,
      "score": 0.922820568,
      "role": ""
    },
    {
      "entity": "seattle",
      "type": "Location",
      "startIndex": 20,
      "endIndex": 26,
      "score": 0.948008537,
      "role": "Origin"
    },
    {
      "entity": "redmond",
      "type": "Location",
      "startIndex": 31,
      "endIndex": 37,
      "score": 0.7047979,
      "role": "Destination"
    }
  ]
}
```

## <a name="patternany-entity-data"></a><span data-ttu-id="4469b-265">Pattern.any entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-265">Pattern.any entity data</span></span>
<span data-ttu-id="4469b-266">Pattern.any entities are variable-length entities used in template utterances of a [pattern](luis-concept-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="4469b-266">Pattern.any entities are variable-length entities used in template utterances of a [pattern](luis-concept-patterns.md).</span></span> 

```JSON
{
  "query": "where is the form Understand your responsibilities as a member of the community and who needs to sign it after I read it?",
  "topScoringIntent": {
    "intent": "FindForm",
    "score": 0.999999464
  },
  "intents": [
    {
      "intent": "FindForm",
      "score": 0.999999464
    },
    {
      "intent": "GetEmployeeBenefits",
      "score": 4.883697E-06
    },
    {
      "intent": "None",
      "score": 1.02040713E-06
    },
    {
      "intent": "GetEmployeeOrgChart",
      "score": 9.278342E-07
    },
    {
      "intent": "MoveAssetsOrPeople",
      "score": 9.278342E-07
    }
  ],
  "entities": [
    {
      "entity": "understand your responsibilities as a member of the community",
      "type": "FormName",
      "startIndex": 18,
      "endIndex": 78,
      "role": ""
    }
  ]
}
```


## <a name="sentiment-analysis"></a><span data-ttu-id="4469b-267">Sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="4469b-267">Sentiment analysis</span></span>
<span data-ttu-id="4469b-268">If Sentiment analysis is configured, the LUIS json response includes sentiment analysis.</span><span class="sxs-lookup"><span data-stu-id="4469b-268">If Sentiment analysis is configured, the LUIS json response includes sentiment analysis.</span></span> <span data-ttu-id="4469b-269">Learn more about sentiment analysis in the [Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/) documentation.</span><span class="sxs-lookup"><span data-stu-id="4469b-269">Learn more about sentiment analysis in the [Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/) documentation.</span></span>

### <a name="sentiment-data"></a><span data-ttu-id="4469b-270">Sentiment data</span><span class="sxs-lookup"><span data-stu-id="4469b-270">Sentiment data</span></span>
<span data-ttu-id="4469b-271">Sentiment data is a score between 1 and 0 indicating the positive (closer to 1) or negative (closer to 0) sentiment of the data.</span><span class="sxs-lookup"><span data-stu-id="4469b-271">Sentiment data is a score between 1 and 0 indicating the positive (closer to 1) or negative (closer to 0) sentiment of the data.</span></span>

<span data-ttu-id="4469b-272">When culture is `en-us`, the response is:</span><span class="sxs-lookup"><span data-stu-id="4469b-272">When culture is `en-us`, the response is:</span></span>

```JSON
"sentimentAnalysis": {
  "label": "positive",
  "score": 0.9163064
}
```

<span data-ttu-id="4469b-273">For all other cultures, the response is:</span><span class="sxs-lookup"><span data-stu-id="4469b-273">For all other cultures, the response is:</span></span>

```JSON
"sentimentAnalysis": {
  "score": 0.9163064
}
```


### <a name="key-phrase-extraction-entity-data"></a><span data-ttu-id="4469b-274">Key phrase extraction entity data</span><span class="sxs-lookup"><span data-stu-id="4469b-274">Key phrase extraction entity data</span></span>
<span data-ttu-id="4469b-275">The key phrase extraction entity returns key phrases in the utterance, provided by [Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/).</span><span class="sxs-lookup"><span data-stu-id="4469b-275">The key phrase extraction entity returns key phrases in the utterance, provided by [Text Analytics](https://docs.microsoft.com/azure/cognitive-services/text-analytics/).</span></span>

<!-- TBD: verify JSON-->
```JSON
"keyPhrases": [
    "places",
    "beautiful views",
    "favorite trail"
]
```

## <a name="data-matching-multiple-entities"></a><span data-ttu-id="4469b-276">Data matching multiple entities</span><span class="sxs-lookup"><span data-stu-id="4469b-276">Data matching multiple entities</span></span>
<span data-ttu-id="4469b-277">LUIS returns all entities discovered in the utterance.</span><span class="sxs-lookup"><span data-stu-id="4469b-277">LUIS returns all entities discovered in the utterance.</span></span> <span data-ttu-id="4469b-278">As a result, your chatbot may need to make decision based on the results.</span><span class="sxs-lookup"><span data-stu-id="4469b-278">As a result, your chatbot may need to make decision based on the results.</span></span> <span data-ttu-id="4469b-279">An utterance can have many entities in an utterance:</span><span class="sxs-lookup"><span data-stu-id="4469b-279">An utterance can have many entities in an utterance:</span></span>

`book me 2 adult business tickets to paris tomorrow on air france`

<span data-ttu-id="4469b-280">The LUIS endpoint can discover the same data in different entities:</span><span class="sxs-lookup"><span data-stu-id="4469b-280">The LUIS endpoint can discover the same data in different entities:</span></span> 

```JSON
{
  "query": "book me 2 adult business tickets to paris tomorrow on air france",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 1.0
  },
  "intents": [
    {
      "intent": "BookFlight",
      "score": 1.0
    },
    {
      "intent": "Concierge",
      "score": 0.04216196
    },
    {
      "intent": "None",
      "score": 0.03610297
    }
  ],
  "entities": [
    {
      "entity": "air france",
      "type": "Airline",
      "startIndex": 54,
      "endIndex": 63,
      "score": 0.8291798
    },
    {
      "entity": "adult",
      "type": "Category",
      "startIndex": 10,
      "endIndex": 14,
      "resolution": {
        "values": [
          "adult"
        ]
      }
    },
    {
      "entity": "paris",
      "type": "Cities",
      "startIndex": 36,
      "endIndex": 40,
      "resolution": {
        "values": [
          "Paris"
        ]
      }
    },
    {
      "entity": "tomorrow",
      "type": "builtin.datetimeV2.date",
      "startIndex": 42,
      "endIndex": 49,
      "resolution": {
        "values": [
          {
            "timex": "2018-02-21",
            "type": "date",
            "value": "2018-02-21"
          }
        ]
      }
    },
    {
      "entity": "paris",
      "type": "Location::ToLocation",
      "startIndex": 36,
      "endIndex": 40,
      "score": 0.9730773
    },
    {
      "entity": "2",
      "type": "builtin.number",
      "startIndex": 8,
      "endIndex": 8,
      "resolution": {
        "value": "2"
      }
    },
    {
      "entity": "business",
      "type": "Seat",
      "startIndex": 16,
      "endIndex": 23,
      "resolution": {
        "values": [
          "business"
        ]
      }
    },
    {
      "entity": "2 adult business",
      "type": "TicketSeatOrder",
      "startIndex": 8,
      "endIndex": 23,
      "score": 0.8784727
    }
  ],
  "compositeEntities": [
    {
      "parentType": "TicketSeatOrder",
      "value": "2 adult business",
      "children": [
        {
          "type": "Category",
          "value": "adult"
        },
        {
          "type": "builtin.number",
          "value": "2"
        },
        {
          "type": "Seat",
          "value": "business"
        }
      ]
    }
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="4469b-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="4469b-281">Next steps</span></span>

<span data-ttu-id="4469b-282">See [Add entities](luis-how-to-add-entities.md) to learn more about how to add entities to your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="4469b-282">See [Add entities](luis-how-to-add-entities.md) to learn more about how to add entities to your LUIS app.</span></span>