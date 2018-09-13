---
title: Glossary for the Language Understanding (LUIS) API Service | Microsoft Docs
description: The glossary explains terms that you might encounter as you work with the LUIS API Service.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.openlocfilehash: 1c0e9e6d02a3062d5493e39211eabf328da41d4b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864678"
---
# <a name="glossary"></a><span data-ttu-id="68387-103">Glossary</span><span class="sxs-lookup"><span data-stu-id="68387-103">Glossary</span></span>

## <a name="active-version"></a><span data-ttu-id="68387-104">Active version</span><span class="sxs-lookup"><span data-stu-id="68387-104">Active version</span></span>

<span data-ttu-id="68387-105">The active LUIS version is the version that receives any changes to the model.</span><span class="sxs-lookup"><span data-stu-id="68387-105">The active LUIS version is the version that receives any changes to the model.</span></span> <span data-ttu-id="68387-106">In the [LUIS](luis-reference-regions.md) website, if you want to make changes to a version that is not the active version, you need to first set that version as active.</span><span class="sxs-lookup"><span data-stu-id="68387-106">In the [LUIS](luis-reference-regions.md) website, if you want to make changes to a version that is not the active version, you need to first set that version as active.</span></span> 

## <a name="authoring"></a><span data-ttu-id="68387-107">Authoring</span><span class="sxs-lookup"><span data-stu-id="68387-107">Authoring</span></span>

<span data-ttu-id="68387-108">Authoring is the ability to create, manage and deploy a [LUIS app](#luis-app), either using the [LUIS](luis-reference-regions.md) website or the [authoring APIs](https://aka.ms/luis-authoring-api).</span><span class="sxs-lookup"><span data-stu-id="68387-108">Authoring is the ability to create, manage and deploy a [LUIS app](#luis-app), either using the [LUIS](luis-reference-regions.md) website or the [authoring APIs](https://aka.ms/luis-authoring-api).</span></span> 

## <a name="authoring-key"></a><span data-ttu-id="68387-109">Authoring Key</span><span class="sxs-lookup"><span data-stu-id="68387-109">Authoring Key</span></span>

<span data-ttu-id="68387-110">Previously named "Programmatic" key.</span><span class="sxs-lookup"><span data-stu-id="68387-110">Previously named "Programmatic" key.</span></span> <span data-ttu-id="68387-111">Used to author the app.</span><span class="sxs-lookup"><span data-stu-id="68387-111">Used to author the app.</span></span> <span data-ttu-id="68387-112">Not used for production-level endpoint queries.</span><span class="sxs-lookup"><span data-stu-id="68387-112">Not used for production-level endpoint queries.</span></span> <span data-ttu-id="68387-113">For more information, see [Key limits](luis-boundaries.md#key-limits).</span><span class="sxs-lookup"><span data-stu-id="68387-113">For more information, see [Key limits](luis-boundaries.md#key-limits).</span></span>   

## <a name="batch-test-json-file"></a><span data-ttu-id="68387-114">Batch text JSON file</span><span class="sxs-lookup"><span data-stu-id="68387-114">Batch text JSON file</span></span>

<span data-ttu-id="68387-115">The batch file is a JSON array.</span><span class="sxs-lookup"><span data-stu-id="68387-115">The batch file is a JSON array.</span></span> <span data-ttu-id="68387-116">Each element in the array has three properties: `text`, `intent`, and `entities`.</span><span class="sxs-lookup"><span data-stu-id="68387-116">Each element in the array has three properties: `text`, `intent`, and `entities`.</span></span> <span data-ttu-id="68387-117">The `entities` property is an array.</span><span class="sxs-lookup"><span data-stu-id="68387-117">The `entities` property is an array.</span></span> <span data-ttu-id="68387-118">The array can be empty.</span><span class="sxs-lookup"><span data-stu-id="68387-118">The array can be empty.</span></span> <span data-ttu-id="68387-119">If the `entities` array is not empty, it needs to accurately identify the entities.</span><span class="sxs-lookup"><span data-stu-id="68387-119">If the `entities` array is not empty, it needs to accurately identify the entities.</span></span>

```JSON
[
    {
        "text": "drive me home",
        "intent": "None",
        "entities": []
    },
    {
        "text": "book a flight to orlando on the 25th",
        "intent": "BookFlight",
        "entities": [
            {
                "entity": "orlando",
                "type": "Location",
                "startIndex": 18,
                "endIndex": 25
            }
        ]
    }
]

```


## <a name="collaborator"></a><span data-ttu-id="68387-120">Collaborator</span><span class="sxs-lookup"><span data-stu-id="68387-120">Collaborator</span></span>

<span data-ttu-id="68387-121">A collaborator is not the [owner](#owner) of the app, but has the same permissions to add, edit, and delete the intents, entities, utterances.</span><span class="sxs-lookup"><span data-stu-id="68387-121">A collaborator is not the [owner](#owner) of the app, but has the same permissions to add, edit, and delete the intents, entities, utterances.</span></span>

## <a name="currently-editing"></a><span data-ttu-id="68387-122">Currently editing</span><span class="sxs-lookup"><span data-stu-id="68387-122">Currently editing</span></span>

<span data-ttu-id="68387-123">Same as [active version](#active-version)</span><span class="sxs-lookup"><span data-stu-id="68387-123">Same as [active version](#active-version)</span></span>

## <a name="domain"></a><span data-ttu-id="68387-124">Domain</span><span class="sxs-lookup"><span data-stu-id="68387-124">Domain</span></span>

<span data-ttu-id="68387-125">In the LUIS context, a **domain** is an area of knowledge.</span><span class="sxs-lookup"><span data-stu-id="68387-125">In the LUIS context, a **domain** is an area of knowledge.</span></span> <span data-ttu-id="68387-126">Your domain is specific to your app area of knowledge.</span><span class="sxs-lookup"><span data-stu-id="68387-126">Your domain is specific to your app area of knowledge.</span></span> <span data-ttu-id="68387-127">This can be a general area such as the travel agent app.</span><span class="sxs-lookup"><span data-stu-id="68387-127">This can be a general area such as the travel agent app.</span></span> <span data-ttu-id="68387-128">A travel agent app can also be specific to just the areas of information for your company such as specific geographical locations, languages, and services.</span><span class="sxs-lookup"><span data-stu-id="68387-128">A travel agent app can also be specific to just the areas of information for your company such as specific geographical locations, languages, and services.</span></span> 

## <a name="endpoint"></a><span data-ttu-id="68387-129">Endpoint</span><span class="sxs-lookup"><span data-stu-id="68387-129">Endpoint</span></span>

<span data-ttu-id="68387-130">The [LUIS endpoint](https://aka.ms/luis-endpoint-apis) URL is where you submit LUIS queries after the [LUIS app](#luis-app) is authored and published.</span><span class="sxs-lookup"><span data-stu-id="68387-130">The [LUIS endpoint](https://aka.ms/luis-endpoint-apis) URL is where you submit LUIS queries after the [LUIS app](#luis-app) is authored and published.</span></span> <span data-ttu-id="68387-131">The endpoint URL contains the region of the published app as well as the app ID.</span><span class="sxs-lookup"><span data-stu-id="68387-131">The endpoint URL contains the region of the published app as well as the app ID.</span></span> <span data-ttu-id="68387-132">You can find the endpoint on the **[Publish](luis-how-to-publish-app.md)** page of your app, in the Resources and Keys table or you can get the endpoint URL from the [Get App Info](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c37) API.</span><span class="sxs-lookup"><span data-stu-id="68387-132">You can find the endpoint on the **[Publish](luis-how-to-publish-app.md)** page of your app, in the Resources and Keys table or you can get the endpoint URL from the [Get App Info](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c37) API.</span></span>

<span data-ttu-id="68387-133">An example endpoint looks like:</span><span class="sxs-lookup"><span data-stu-id="68387-133">An example endpoint looks like:</span></span>

`https://<region>.api.cognitive.microsoft.com/luis/v2.0/apps/<appID>?subscription-key=<subscriptionID>&verbose=true&timezoneOffset=0&q=<utterance>`

|<span data-ttu-id="68387-134">Querystring parameter</span><span class="sxs-lookup"><span data-stu-id="68387-134">Querystring parameter</span></span>|<span data-ttu-id="68387-135">description</span><span class="sxs-lookup"><span data-stu-id="68387-135">description</span></span>|
|--|--|
|<span data-ttu-id="68387-136">region</span><span class="sxs-lookup"><span data-stu-id="68387-136">region</span></span>| [<span data-ttu-id="68387-137">published region</span><span class="sxs-lookup"><span data-stu-id="68387-137">published region</span></span>](luis-reference-regions.md#publishing-regions) |
|<span data-ttu-id="68387-138">appID</span><span class="sxs-lookup"><span data-stu-id="68387-138">appID</span></span> | <span data-ttu-id="68387-139">LUIS app ID</span><span class="sxs-lookup"><span data-stu-id="68387-139">LUIS app ID</span></span> |
|<span data-ttu-id="68387-140">subscriptionID</span><span class="sxs-lookup"><span data-stu-id="68387-140">subscriptionID</span></span> | <span data-ttu-id="68387-141">LUIS endpoint (subscription) key created in Azure portal</span><span class="sxs-lookup"><span data-stu-id="68387-141">LUIS endpoint (subscription) key created in Azure portal</span></span> |
|<span data-ttu-id="68387-142">q</span><span class="sxs-lookup"><span data-stu-id="68387-142">q</span></span> | <span data-ttu-id="68387-143">utterance</span><span class="sxs-lookup"><span data-stu-id="68387-143">utterance</span></span> |
|<span data-ttu-id="68387-144">timezoneOffset</span><span class="sxs-lookup"><span data-stu-id="68387-144">timezoneOffset</span></span>| <span data-ttu-id="68387-145">minutes</span><span class="sxs-lookup"><span data-stu-id="68387-145">minutes</span></span>|

## <a name="entity"></a><span data-ttu-id="68387-146">Entity</span><span class="sxs-lookup"><span data-stu-id="68387-146">Entity</span></span>

<span data-ttu-id="68387-147">[Entities](luis-concept-entity-types.md) are important words in [utterances](luis-concept-utterance.md) that describe information relevant to the [intent](luis-concept-intent.md), and sometimes they are essential to it.</span><span class="sxs-lookup"><span data-stu-id="68387-147">[Entities](luis-concept-entity-types.md) are important words in [utterances](luis-concept-utterance.md) that describe information relevant to the [intent](luis-concept-intent.md), and sometimes they are essential to it.</span></span> <span data-ttu-id="68387-148">An entity is essentially a datatype in LUIS.</span><span class="sxs-lookup"><span data-stu-id="68387-148">An entity is essentially a datatype in LUIS.</span></span> 

## <a name="f-measure"></a><span data-ttu-id="68387-149">F-measure</span><span class="sxs-lookup"><span data-stu-id="68387-149">F-measure</span></span>

<span data-ttu-id="68387-150">In [batch testing](luis-interactive-test.md#batch-testing), a measure of the test's accuracy.</span><span class="sxs-lookup"><span data-stu-id="68387-150">In [batch testing](luis-interactive-test.md#batch-testing), a measure of the test's accuracy.</span></span>

## <a name="false-negative"></a><span data-ttu-id="68387-151">False negative (TN)</span><span class="sxs-lookup"><span data-stu-id="68387-151">False negative (TN)</span></span>

<span data-ttu-id="68387-152">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app incorrectly predicted the absence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="68387-152">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app incorrectly predicted the absence of the target intent/entity.</span></span>

## <a name="false-positive"></a><span data-ttu-id="68387-153">False positive (TP)</span><span class="sxs-lookup"><span data-stu-id="68387-153">False positive (TP)</span></span>

<span data-ttu-id="68387-154">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app incorrectly predicted the existence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="68387-154">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app incorrectly predicted the existence of the target intent/entity.</span></span>

## <a name="features"></a><span data-ttu-id="68387-155">Features</span><span class="sxs-lookup"><span data-stu-id="68387-155">Features</span></span>

<span data-ttu-id="68387-156">In machine learning, a [feature](luis-concept-feature.md) is a distinguishing trait or attribute of data that your system observes.</span><span class="sxs-lookup"><span data-stu-id="68387-156">In machine learning, a [feature](luis-concept-feature.md) is a distinguishing trait or attribute of data that your system observes.</span></span>

## <a name="intent"></a><span data-ttu-id="68387-157">Intent</span><span class="sxs-lookup"><span data-stu-id="68387-157">Intent</span></span>

<span data-ttu-id="68387-158">An [intent](luis-concept-intent.md) represents a task or action the user wants to perform.</span><span class="sxs-lookup"><span data-stu-id="68387-158">An [intent](luis-concept-intent.md) represents a task or action the user wants to perform.</span></span> <span data-ttu-id="68387-159">It is a purpose or goal expressed in a user's input, such as booking a flight, paying a bill, or finding a news article.</span><span class="sxs-lookup"><span data-stu-id="68387-159">It is a purpose or goal expressed in a user's input, such as booking a flight, paying a bill, or finding a news article.</span></span> <span data-ttu-id="68387-160">In LUIS, the intent prediction is based on the entire utterance.</span><span class="sxs-lookup"><span data-stu-id="68387-160">In LUIS, the intent prediction is based on the entire utterance.</span></span> <span data-ttu-id="68387-161">Entities, by comparison, are pieces of an utterance.</span><span class="sxs-lookup"><span data-stu-id="68387-161">Entities, by comparison, are pieces of an utterance.</span></span>

## <a name="labeling"></a><span data-ttu-id="68387-162">Labeling</span><span class="sxs-lookup"><span data-stu-id="68387-162">Labeling</span></span>

<span data-ttu-id="68387-163">Labeling is the process of associating a word or phrase in an intent's [utterance](#utterance) with an [entity](#entity) (datatype).</span><span class="sxs-lookup"><span data-stu-id="68387-163">Labeling is the process of associating a word or phrase in an intent's [utterance](#utterance) with an [entity](#entity) (datatype).</span></span> 

## <a name="luis-app"></a><span data-ttu-id="68387-164">LUIS app</span><span class="sxs-lookup"><span data-stu-id="68387-164">LUIS app</span></span>

<span data-ttu-id="68387-165">A LUIS app is a trained data model for natural language processing including [intents](#intent), [entities](#entity), and labeled [utterances](#utterance).</span><span class="sxs-lookup"><span data-stu-id="68387-165">A LUIS app is a trained data model for natural language processing including [intents](#intent), [entities](#entity), and labeled [utterances](#utterance).</span></span>

## <a name="owner"></a><span data-ttu-id="68387-166">Owner</span><span class="sxs-lookup"><span data-stu-id="68387-166">Owner</span></span>

<span data-ttu-id="68387-167">Each app has one owner who is the person that created the app.</span><span class="sxs-lookup"><span data-stu-id="68387-167">Each app has one owner who is the person that created the app.</span></span> <span data-ttu-id="68387-168">The owner can add [collaborators](#collaborator).</span><span class="sxs-lookup"><span data-stu-id="68387-168">The owner can add [collaborators](#collaborator).</span></span>

## <a name="pattern"></a><span data-ttu-id="68387-169">Patterns</span><span class="sxs-lookup"><span data-stu-id="68387-169">Patterns</span></span>
<span data-ttu-id="68387-170">The previous Pattern feature is replaced with [Patterns](luis-concept-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="68387-170">The previous Pattern feature is replaced with [Patterns](luis-concept-patterns.md).</span></span> <span data-ttu-id="68387-171">Use patterns to improve prediction accuracy by providing fewer training examples.</span><span class="sxs-lookup"><span data-stu-id="68387-171">Use patterns to improve prediction accuracy by providing fewer training examples.</span></span> 

## <a name="phrase-list"></a><span data-ttu-id="68387-172">Phrase list</span><span class="sxs-lookup"><span data-stu-id="68387-172">Phrase list</span></span>

<span data-ttu-id="68387-173">A [phrase list](luis-concept-feature.md#what-is-a-phrase-list-feature) includes a group of values (words or phrases) that belong to the same class and must be treated similarly (for example, names of cities or products).</span><span class="sxs-lookup"><span data-stu-id="68387-173">A [phrase list](luis-concept-feature.md#what-is-a-phrase-list-feature) includes a group of values (words or phrases) that belong to the same class and must be treated similarly (for example, names of cities or products).</span></span> <span data-ttu-id="68387-174">An interchangeable list is treated as synonyms.</span><span class="sxs-lookup"><span data-stu-id="68387-174">An interchangeable list is treated as synonyms.</span></span> 

## <a name="prebuilt-domains"></a><span data-ttu-id="68387-175">Prebuilt domain</span><span class="sxs-lookup"><span data-stu-id="68387-175">Prebuilt domain</span></span>

<span data-ttu-id="68387-176">A [prebuilt domain](luis-how-to-use-prebuilt-domains.md) is a LUIS app configured for a specific domain such as home automation (HomeAutomation) or restaurant reservations (RestaurantReservation).</span><span class="sxs-lookup"><span data-stu-id="68387-176">A [prebuilt domain](luis-how-to-use-prebuilt-domains.md) is a LUIS app configured for a specific domain such as home automation (HomeAutomation) or restaurant reservations (RestaurantReservation).</span></span> <span data-ttu-id="68387-177">The intents, utterances, and entities are configured for this domain.</span><span class="sxs-lookup"><span data-stu-id="68387-177">The intents, utterances, and entities are configured for this domain.</span></span> 

## <a name="prebuilt-entity"></a><span data-ttu-id="68387-178">Prebuilt entity</span><span class="sxs-lookup"><span data-stu-id="68387-178">Prebuilt entity</span></span>

<span data-ttu-id="68387-179">A [prebuilt entity](luis-prebuilt-entities.md) is an entity LUIS provides for common types of information such as number, URL, and email.</span><span class="sxs-lookup"><span data-stu-id="68387-179">A [prebuilt entity](luis-prebuilt-entities.md) is an entity LUIS provides for common types of information such as number, URL, and email.</span></span> <span data-ttu-id="68387-180">You choose to add a prebuilt entity to your application.</span><span class="sxs-lookup"><span data-stu-id="68387-180">You choose to add a prebuilt entity to your application.</span></span> 

## <a name="precision"></a><span data-ttu-id="68387-181">Precision</span><span class="sxs-lookup"><span data-stu-id="68387-181">Precision</span></span>
<span data-ttu-id="68387-182">In [batch testing](luis-interactive-test.md#batch-testing), precision (also called positive predictive value) is the fraction of relevant utterances among the retrieved utterances.</span><span class="sxs-lookup"><span data-stu-id="68387-182">In [batch testing](luis-interactive-test.md#batch-testing), precision (also called positive predictive value) is the fraction of relevant utterances among the retrieved utterances.</span></span>

## <a name="programmatic-key"></a><span data-ttu-id="68387-183">Programmatic key</span><span class="sxs-lookup"><span data-stu-id="68387-183">Programmatic key</span></span>

<span data-ttu-id="68387-184">Renamed to [authoring key](#authoring-key).</span><span class="sxs-lookup"><span data-stu-id="68387-184">Renamed to [authoring key](#authoring-key).</span></span> 

## <a name="publish"></a><span data-ttu-id="68387-185">Publish</span><span class="sxs-lookup"><span data-stu-id="68387-185">Publish</span></span>

<span data-ttu-id="68387-186">Publishing means making a LUIS [active version](#active-version) available on either the staging or production [endpoint](#endpoint).</span><span class="sxs-lookup"><span data-stu-id="68387-186">Publishing means making a LUIS [active version](#active-version) available on either the staging or production [endpoint](#endpoint).</span></span>  

## <a name="quota"></a><span data-ttu-id="68387-187">Quota</span><span class="sxs-lookup"><span data-stu-id="68387-187">Quota</span></span>

<span data-ttu-id="68387-188">LUIS quota is the limitation of the [Azure subscription tier](https://aka.ms/luis-price-tier).</span><span class="sxs-lookup"><span data-stu-id="68387-188">LUIS quota is the limitation of the [Azure subscription tier](https://aka.ms/luis-price-tier).</span></span> <span data-ttu-id="68387-189">The LUIS quota can be limited by both requests per second (HTTP Status 429) and total requests in a month (HTTP Status 403).</span><span class="sxs-lookup"><span data-stu-id="68387-189">The LUIS quota can be limited by both requests per second (HTTP Status 429) and total requests in a month (HTTP Status 403).</span></span> 

## <a name="recall"></a><span data-ttu-id="68387-190">Recall</span><span class="sxs-lookup"><span data-stu-id="68387-190">Recall</span></span>
<span data-ttu-id="68387-191">In [batch testing](luis-interactive-test.md#batch-testing), recall (also known as sensitivity), is the ability for LUIS to generalize.</span><span class="sxs-lookup"><span data-stu-id="68387-191">In [batch testing](luis-interactive-test.md#batch-testing), recall (also known as sensitivity), is the ability for LUIS to generalize.</span></span> 

## <a name="semantic-dictionary"></a><span data-ttu-id="68387-192">Semantic dictionary</span><span class="sxs-lookup"><span data-stu-id="68387-192">Semantic dictionary</span></span>
<span data-ttu-id="68387-193">A semantic dictionary is provided on the List entity page as well as the Phrase list page.</span><span class="sxs-lookup"><span data-stu-id="68387-193">A semantic dictionary is provided on the List entity page as well as the Phrase list page.</span></span> <span data-ttu-id="68387-194">The semantic dictionary provides suggestions of words based on the current scope.</span><span class="sxs-lookup"><span data-stu-id="68387-194">The semantic dictionary provides suggestions of words based on the current scope.</span></span>

## <a name="sentiment-analysis"></a><span data-ttu-id="68387-195">Sentiment Analysis</span><span class="sxs-lookup"><span data-stu-id="68387-195">Sentiment Analysis</span></span>
<span data-ttu-id="68387-196">Sentiment analysis provides positive or negative values of the utterances provided by [Text Analytics](https://azure.microsoft.com/services/cognitive-services/text-analytics/).</span><span class="sxs-lookup"><span data-stu-id="68387-196">Sentiment analysis provides positive or negative values of the utterances provided by [Text Analytics](https://azure.microsoft.com/services/cognitive-services/text-analytics/).</span></span> 

## <a name="speech-priming"></a><span data-ttu-id="68387-197">Speech priming</span><span class="sxs-lookup"><span data-stu-id="68387-197">Speech priming</span></span>

<span data-ttu-id="68387-198">Speech priming allows your speech service to be primed with your LUIS model.</span><span class="sxs-lookup"><span data-stu-id="68387-198">Speech priming allows your speech service to be primed with your LUIS model.</span></span> 

## <a name="spelling-correction"></a><span data-ttu-id="68387-199">Spelling correction</span><span class="sxs-lookup"><span data-stu-id="68387-199">Spelling correction</span></span>

<span data-ttu-id="68387-200">On the Publish page, enable [Bing spell checker](luis-how-to-publish-app.md#enable-bing-spell-checker) to correct misspelled words in the utterances before prediction.</span><span class="sxs-lookup"><span data-stu-id="68387-200">On the Publish page, enable [Bing spell checker](luis-how-to-publish-app.md#enable-bing-spell-checker) to correct misspelled words in the utterances before prediction.</span></span> 

## <a name="starter-key"></a><span data-ttu-id="68387-201">Starter key</span><span class="sxs-lookup"><span data-stu-id="68387-201">Starter key</span></span>

<span data-ttu-id="68387-202">Same as [programmatic key](#programmatic-key), renamed to Authoring key.</span><span class="sxs-lookup"><span data-stu-id="68387-202">Same as [programmatic key](#programmatic-key), renamed to Authoring key.</span></span>

## <a name="subscription-key"></a><span data-ttu-id="68387-203">Subscription key</span><span class="sxs-lookup"><span data-stu-id="68387-203">Subscription key</span></span>

<span data-ttu-id="68387-204">The subscription key is the **endpoint** key associated with the LUIS service [you created in Azure](luis-how-to-azure-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="68387-204">The subscription key is the **endpoint** key associated with the LUIS service [you created in Azure](luis-how-to-azure-subscription.md).</span></span> <span data-ttu-id="68387-205">This key is not the [authoring key](#programmatic-key).</span><span class="sxs-lookup"><span data-stu-id="68387-205">This key is not the [authoring key](#programmatic-key).</span></span> <span data-ttu-id="68387-206">If you have an endpoint key, it should be used for any endpoint requests instead of the authoring key.</span><span class="sxs-lookup"><span data-stu-id="68387-206">If you have an endpoint key, it should be used for any endpoint requests instead of the authoring key.</span></span> <span data-ttu-id="68387-207">You can see your current endpoint key inside the endpoint URL at the bottom of [**Publish App** page](luis-how-to-publish-app.md) in [LUIS](luis-reference-regions.md) website.</span><span class="sxs-lookup"><span data-stu-id="68387-207">You can see your current endpoint key inside the endpoint URL at the bottom of [**Publish App** page](luis-how-to-publish-app.md) in [LUIS](luis-reference-regions.md) website.</span></span> <span data-ttu-id="68387-208">It is the value of **subscription-key** name/value pair.</span><span class="sxs-lookup"><span data-stu-id="68387-208">It is the value of **subscription-key** name/value pair.</span></span> 

## <a name="test"></a><span data-ttu-id="68387-209">Test</span><span class="sxs-lookup"><span data-stu-id="68387-209">Test</span></span>

<span data-ttu-id="68387-210">[Testing](luis-interactive-test.md#test-your-app) a LUIS app means passing an utterance to LUIS and viewing the JSON results.</span><span class="sxs-lookup"><span data-stu-id="68387-210">[Testing](luis-interactive-test.md#test-your-app) a LUIS app means passing an utterance to LUIS and viewing the JSON results.</span></span>

## <a name="timezoneoffset"></a><span data-ttu-id="68387-211">Timezone offset</span><span class="sxs-lookup"><span data-stu-id="68387-211">Timezone offset</span></span>

<span data-ttu-id="68387-212">The endpoint includes timezoneOffset.</span><span class="sxs-lookup"><span data-stu-id="68387-212">The endpoint includes timezoneOffset.</span></span> <span data-ttu-id="68387-213">This is the number in minutes you want to add or remove from the datetimeV2 prebuilt entity.</span><span class="sxs-lookup"><span data-stu-id="68387-213">This is the number in minutes you want to add or remove from the datetimeV2 prebuilt entity.</span></span> <span data-ttu-id="68387-214">For example, if the utterance is "what time is it now?", the datetimeV2 returned is the current time for the client request.</span><span class="sxs-lookup"><span data-stu-id="68387-214">For example, if the utterance is "what time is it now?", the datetimeV2 returned is the current time for the client request.</span></span> <span data-ttu-id="68387-215">If your client request is coming from a bot or other application that is not the same as your bot's user, you should pass in the offset between the bot and the user.</span><span class="sxs-lookup"><span data-stu-id="68387-215">If your client request is coming from a bot or other application that is not the same as your bot's user, you should pass in the offset between the bot and the user.</span></span> 

<span data-ttu-id="68387-216">See [Change time zone of prebuilt datetimeV2 entity](luis-concept-data-alteration.md?#change-time-zone-of-prebuilt-datetimev2-entity).</span><span class="sxs-lookup"><span data-stu-id="68387-216">See [Change time zone of prebuilt datetimeV2 entity](luis-concept-data-alteration.md?#change-time-zone-of-prebuilt-datetimev2-entity).</span></span>

## <a name="token"></a><span data-ttu-id="68387-217">Token</span><span class="sxs-lookup"><span data-stu-id="68387-217">Token</span></span>
<span data-ttu-id="68387-218">A token is the smallest unit that can be labeled in an entity.</span><span class="sxs-lookup"><span data-stu-id="68387-218">A token is the smallest unit that can be labeled in an entity.</span></span> <span data-ttu-id="68387-219">Tokenization is based on the application's [culture](luis-supported-languages.md#tokenization).</span><span class="sxs-lookup"><span data-stu-id="68387-219">Tokenization is based on the application's [culture](luis-supported-languages.md#tokenization).</span></span>

## <a name="train"></a><span data-ttu-id="68387-220">Train</span><span class="sxs-lookup"><span data-stu-id="68387-220">Train</span></span>

<span data-ttu-id="68387-221">Training is the process of teaching LUIS about any changes to the [active version](#active-version) since the last training.</span><span class="sxs-lookup"><span data-stu-id="68387-221">Training is the process of teaching LUIS about any changes to the [active version](#active-version) since the last training.</span></span>

## <a name="true-negative"></a><span data-ttu-id="68387-222">True negative (TN)</span><span class="sxs-lookup"><span data-stu-id="68387-222">True negative (TN)</span></span>

<span data-ttu-id="68387-223">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app correctly predicted the absence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="68387-223">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app correctly predicted the absence of the target intent/entity.</span></span>

## <a name="true-positive"></a><span data-ttu-id="68387-224">True positive (TP)</span><span class="sxs-lookup"><span data-stu-id="68387-224">True positive (TP)</span></span>

<span data-ttu-id="68387-225">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app correctly predicted the existence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="68387-225">In [batch testing](luis-interactive-test.md#batch-testing), the data points represent utterances in which your app correctly predicted the existence of the target intent/entity.</span></span>

## <a name="utterance"></a><span data-ttu-id="68387-226">Utterance</span><span class="sxs-lookup"><span data-stu-id="68387-226">Utterance</span></span>

<span data-ttu-id="68387-227">An utterance is a natural language phrase such as "book 2 tickets to Seattle next Tuesday".</span><span class="sxs-lookup"><span data-stu-id="68387-227">An utterance is a natural language phrase such as "book 2 tickets to Seattle next Tuesday".</span></span> <span data-ttu-id="68387-228">Example utterances are added to the intent.</span><span class="sxs-lookup"><span data-stu-id="68387-228">Example utterances are added to the intent.</span></span> 

## <a name="version"></a><span data-ttu-id="68387-229">Version</span><span class="sxs-lookup"><span data-stu-id="68387-229">Version</span></span>

<span data-ttu-id="68387-230">A LUIS [version](luis-how-to-manage-versions.md) is a specific data model associated with a LUIS app ID and the published endpoint.</span><span class="sxs-lookup"><span data-stu-id="68387-230">A LUIS [version](luis-how-to-manage-versions.md) is a specific data model associated with a LUIS app ID and the published endpoint.</span></span> <span data-ttu-id="68387-231">Every LUIS app has at least one version.</span><span class="sxs-lookup"><span data-stu-id="68387-231">Every LUIS app has at least one version.</span></span>
