---
title: Publish your LUIS app | Microsoft Docs
description: After you build and test your app by using Language Understanding (LUIS), publish it as a web service on Azure.
services: cognitive-services
titleSuffix: Azure
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 05/07/2018
ms.author: diberry
ms.openlocfilehash: a653d854901f5dc84b957c316c4174610af4be30
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870104"
---
# <a name="publish-your-trained-app"></a><span data-ttu-id="c2f82-103">Publish your trained app</span><span class="sxs-lookup"><span data-stu-id="c2f82-103">Publish your trained app</span></span>
<span data-ttu-id="c2f82-104">When you finish building and testing your LUIS app, publish it.</span><span class="sxs-lookup"><span data-stu-id="c2f82-104">When you finish building and testing your LUIS app, publish it.</span></span> <span data-ttu-id="c2f82-105">After the app is published, the Publish page shows all associated HTTP [endpoints](luis-glossary.md#endpoint).</span><span class="sxs-lookup"><span data-stu-id="c2f82-105">After the app is published, the Publish page shows all associated HTTP [endpoints](luis-glossary.md#endpoint).</span></span> <span data-ttu-id="c2f82-106">These endpoints, per [region](luis-reference-regions.md) and per [key](luis-how-to-manage-keys.md), are then integrated into any client, chatbot, or backend application.</span><span class="sxs-lookup"><span data-stu-id="c2f82-106">These endpoints, per [region](luis-reference-regions.md) and per [key](luis-how-to-manage-keys.md), are then integrated into any client, chatbot, or backend application.</span></span> 

<span data-ttu-id="c2f82-107">You can always [test](luis-interactive-test.md) your app before publishing it.</span><span class="sxs-lookup"><span data-stu-id="c2f82-107">You can always [test](luis-interactive-test.md) your app before publishing it.</span></span> 

## <a name="production-and-staging-slots"></a><span data-ttu-id="c2f82-108">Production and staging slots</span><span class="sxs-lookup"><span data-stu-id="c2f82-108">Production and staging slots</span></span>
<span data-ttu-id="c2f82-109">You can publish your app to the **Staging slot** or the **Production Slot**.</span><span class="sxs-lookup"><span data-stu-id="c2f82-109">You can publish your app to the **Staging slot** or the **Production Slot**.</span></span> <span data-ttu-id="c2f82-110">By using two publishing slots, this allows you to have two different versions with published endpoints or the same version on two different endpoints.</span><span class="sxs-lookup"><span data-stu-id="c2f82-110">By using two publishing slots, this allows you to have two different versions with published endpoints or the same version on two different endpoints.</span></span> 

<!-- TBD: what is the technical difference? log files, endpoint quota? -->

## <a name="settings-configuration-requires-publishing-model"></a><span data-ttu-id="c2f82-111">Settings configuration requires publishing model</span><span class="sxs-lookup"><span data-stu-id="c2f82-111">Settings configuration requires publishing model</span></span>
<span data-ttu-id="c2f82-112">Publish to the endpoint after changes to the following settings.</span><span class="sxs-lookup"><span data-stu-id="c2f82-112">Publish to the endpoint after changes to the following settings.</span></span> 

## <a name="external-services-settings"></a><span data-ttu-id="c2f82-113">External services settings</span><span class="sxs-lookup"><span data-stu-id="c2f82-113">External services settings</span></span>
<span data-ttu-id="c2f82-114">External service settings include **[Sentiment Analysis](#enable-sentiment-analysis)** and **[Speech Priming](#enable-speech-priming)**.</span><span class="sxs-lookup"><span data-stu-id="c2f82-114">External service settings include **[Sentiment Analysis](#enable-sentiment-analysis)** and **[Speech Priming](#enable-speech-priming)**.</span></span>

### <a name="enable-sentiment-analysis"></a><span data-ttu-id="c2f82-115">Enable sentiment analysis</span><span class="sxs-lookup"><span data-stu-id="c2f82-115">Enable sentiment analysis</span></span>
<span data-ttu-id="c2f82-116">In the **External services settings**, the **Enable Sentiment Analysis** checkbox allows LUIS to integrate with [Text Analytics](https://azure.microsoft.com/services/cognitive-services/text-analytics/) to provide sentiment and key phrase analysis.</span><span class="sxs-lookup"><span data-stu-id="c2f82-116">In the **External services settings**, the **Enable Sentiment Analysis** checkbox allows LUIS to integrate with [Text Analytics](https://azure.microsoft.com/services/cognitive-services/text-analytics/) to provide sentiment and key phrase analysis.</span></span> <span data-ttu-id="c2f82-117">You do not have to provide a Text Analytics key and there is no billing charge for this service to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="c2f82-117">You do not have to provide a Text Analytics key and there is no billing charge for this service to your Azure account.</span></span> <span data-ttu-id="c2f82-118">Once you check this setting, it is persistent.</span><span class="sxs-lookup"><span data-stu-id="c2f82-118">Once you check this setting, it is persistent.</span></span> 

<span data-ttu-id="c2f82-119">Sentiment data is a score between 1 and 0 indicating the positive (closer to 1) or negative (closer to 0) sentiment of the data.</span><span class="sxs-lookup"><span data-stu-id="c2f82-119">Sentiment data is a score between 1 and 0 indicating the positive (closer to 1) or negative (closer to 0) sentiment of the data.</span></span>

<span data-ttu-id="c2f82-120">For more information about the JSON endpoint response with sentiment analysis, see [Sentiment analysis](luis-concept-data-extraction.md#sentiment-analysis)</span><span class="sxs-lookup"><span data-stu-id="c2f82-120">For more information about the JSON endpoint response with sentiment analysis, see [Sentiment analysis](luis-concept-data-extraction.md#sentiment-analysis)</span></span>

### <a name="enable-speech-priming"></a><span data-ttu-id="c2f82-121">Enable speech priming</span><span class="sxs-lookup"><span data-stu-id="c2f82-121">Enable speech priming</span></span> 
<span data-ttu-id="c2f82-122">In the **External services settings**, the **Enable Speech Priming** checkbox allows you to have a single endpoint to get a spoken utterance from a chatbot or LUIS-calling application and receive a LUIS prediction response.</span><span class="sxs-lookup"><span data-stu-id="c2f82-122">In the **External services settings**, the **Enable Speech Priming** checkbox allows you to have a single endpoint to get a spoken utterance from a chatbot or LUIS-calling application and receive a LUIS prediction response.</span></span> <span data-ttu-id="c2f82-123">The Speech priming uses the Cognitive service [Speech API](../Speech-Service/rest-apis.md).</span><span class="sxs-lookup"><span data-stu-id="c2f82-123">The Speech priming uses the Cognitive service [Speech API](../Speech-Service/rest-apis.md).</span></span> 

![Image of Speech priming confirmation dialog](./media/luis-how-to-publish-app/speech-prime-modal.png)

<span data-ttu-id="c2f82-125">Once this feature is enabled, publish your app.</span><span class="sxs-lookup"><span data-stu-id="c2f82-125">Once this feature is enabled, publish your app.</span></span> <span data-ttu-id="c2f82-126">When you publish your LUIS app, your app model is sent to your own Speech service to prime the Speech service.</span><span class="sxs-lookup"><span data-stu-id="c2f82-126">When you publish your LUIS app, your app model is sent to your own Speech service to prime the Speech service.</span></span> <span data-ttu-id="c2f82-127">Your model information is **not** used outside of your own service.</span><span class="sxs-lookup"><span data-stu-id="c2f82-127">Your model information is **not** used outside of your own service.</span></span> 

<span data-ttu-id="c2f82-128">In order to complete the use of Speech priming, you need the following information to use in the [Speech SDK](../speech-service/speech-sdk-reference.md):</span><span class="sxs-lookup"><span data-stu-id="c2f82-128">In order to complete the use of Speech priming, you need the following information to use in the [Speech SDK](../speech-service/speech-sdk-reference.md):</span></span>
* <span data-ttu-id="c2f82-129">A LUIS endpoint key.</span><span class="sxs-lookup"><span data-stu-id="c2f82-129">A LUIS endpoint key.</span></span>
* <span data-ttu-id="c2f82-130">The LUIS app ID.</span><span class="sxs-lookup"><span data-stu-id="c2f82-130">The LUIS app ID.</span></span>
* <span data-ttu-id="c2f82-131">An endpoint domain, referred to as "Hostname" in Speech SDK, such as "westus.api.cognitive.microsoft.com," where the first subdomain is the region where the app is published.</span><span class="sxs-lookup"><span data-stu-id="c2f82-131">An endpoint domain, referred to as "Hostname" in Speech SDK, such as "westus.api.cognitive.microsoft.com," where the first subdomain is the region where the app is published.</span></span>

<span data-ttu-id="c2f82-132">For more information, see the [Speech to Intent](http://aka.ms/speechsdk) sample.</span><span class="sxs-lookup"><span data-stu-id="c2f82-132">For more information, see the [Speech to Intent](http://aka.ms/speechsdk) sample.</span></span>

<span data-ttu-id="c2f82-133">When your LUIS app is deleted or the Speech service is deleted, your model data is removed.</span><span class="sxs-lookup"><span data-stu-id="c2f82-133">When your LUIS app is deleted or the Speech service is deleted, your model data is removed.</span></span> 

## <a name="endpoint-url-settings"></a><span data-ttu-id="c2f82-134">Endpoint URL settings</span><span class="sxs-lookup"><span data-stu-id="c2f82-134">Endpoint URL settings</span></span>
<span data-ttu-id="c2f82-135">Endpoint URL services settings include **[Timezone](#set-timezone-offset)** offset, **[all predicted intent scores](#include-all-predicted-intent-scores)**, and **[Bing spell checker](#enable-bing-spell-checker)**.</span><span class="sxs-lookup"><span data-stu-id="c2f82-135">Endpoint URL services settings include **[Timezone](#set-timezone-offset)** offset, **[all predicted intent scores](#include-all-predicted-intent-scores)**, and **[Bing spell checker](#enable-bing-spell-checker)**.</span></span>

### <a name="set-timezone-offset"></a><span data-ttu-id="c2f82-136">Set Timezone offset</span><span class="sxs-lookup"><span data-stu-id="c2f82-136">Set Timezone offset</span></span> 
<span data-ttu-id="c2f82-137">Part of the slot choice is the time zone selection.</span><span class="sxs-lookup"><span data-stu-id="c2f82-137">Part of the slot choice is the time zone selection.</span></span> <span data-ttu-id="c2f82-138">This timezone setting allows LUIS to [alter](luis-concept-data-alteration.md#change-time-zone-of-prebuilt-datetimev2-entity) any prebuilt datetimeV2 time values during prediction so that the returned entity data is correct according to the selected time zone.</span><span class="sxs-lookup"><span data-stu-id="c2f82-138">This timezone setting allows LUIS to [alter](luis-concept-data-alteration.md#change-time-zone-of-prebuilt-datetimev2-entity) any prebuilt datetimeV2 time values during prediction so that the returned entity data is correct according to the selected time zone.</span></span> 

### <a name="include-all-predicted-intent-scores"></a><span data-ttu-id="c2f82-139">Include all predicted intent scores</span><span class="sxs-lookup"><span data-stu-id="c2f82-139">Include all predicted intent scores</span></span>
<span data-ttu-id="c2f82-140">The **Include all predicted intent scores** checkbox allows the endpoint query response to include the prediction score for each intent.</span><span class="sxs-lookup"><span data-stu-id="c2f82-140">The **Include all predicted intent scores** checkbox allows the endpoint query response to include the prediction score for each intent.</span></span> 

<span data-ttu-id="c2f82-141">This setting allows your chatbot or LUIS-calling application to make a programmatic decision based on the scores of the returned intents.</span><span class="sxs-lookup"><span data-stu-id="c2f82-141">This setting allows your chatbot or LUIS-calling application to make a programmatic decision based on the scores of the returned intents.</span></span> <span data-ttu-id="c2f82-142">Generally the top two intents are the most interesting.</span><span class="sxs-lookup"><span data-stu-id="c2f82-142">Generally the top two intents are the most interesting.</span></span> <span data-ttu-id="c2f82-143">If the top score is the None intent, your chatbot can choose to ask a follow-up question that makes a definitive choice between the None intent and the other high-scoring intent.</span><span class="sxs-lookup"><span data-stu-id="c2f82-143">If the top score is the None intent, your chatbot can choose to ask a follow-up question that makes a definitive choice between the None intent and the other high-scoring intent.</span></span> 

<span data-ttu-id="c2f82-144">The intents and their scores are also included the endpoint logs.</span><span class="sxs-lookup"><span data-stu-id="c2f82-144">The intents and their scores are also included the endpoint logs.</span></span> <span data-ttu-id="c2f82-145">You can [export](luis-how-to-start-new-app.md#export-app) those logs and analyze the scores.</span><span class="sxs-lookup"><span data-stu-id="c2f82-145">You can [export](luis-how-to-start-new-app.md#export-app) those logs and analyze the scores.</span></span> 

```
{
  "query": "book a flight to Cairo",
  "topScoringIntent": {
    "intent": "None",
    "score": 0.5223427
  },
  "intents": [
    {
      "intent": "None",
      "score": 0.5223427
    },
    {
      "intent": "BookFlight",
      "score": 0.372391433
    }
  ],
  "entities": []
}
```

### <a name="enable-bing-spell-checker"></a><span data-ttu-id="c2f82-146">Enable Bing spell checker</span><span class="sxs-lookup"><span data-stu-id="c2f82-146">Enable Bing spell checker</span></span> 
<span data-ttu-id="c2f82-147">In the **Endpoint url settings**, the **Enable Bing spell checker** checkbox allows LUIS to correct misspelled words before prediction.</span><span class="sxs-lookup"><span data-stu-id="c2f82-147">In the **Endpoint url settings**, the **Enable Bing spell checker** checkbox allows LUIS to correct misspelled words before prediction.</span></span> <span data-ttu-id="c2f82-148">Create a **[Bing Spell Check key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api)**.</span><span class="sxs-lookup"><span data-stu-id="c2f82-148">Create a **[Bing Spell Check key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api)**.</span></span> <span data-ttu-id="c2f82-149">Once the key is created, two querystring parameters are added to the endpoint URL on the publish page.</span><span class="sxs-lookup"><span data-stu-id="c2f82-149">Once the key is created, two querystring parameters are added to the endpoint URL on the publish page.</span></span> 

<span data-ttu-id="c2f82-150">Add the **spellCheck=true** querystring parameter and the **bing-spell-check-subscription-key={YOUR_BING_KEY_HERE}** .</span><span class="sxs-lookup"><span data-stu-id="c2f82-150">Add the **spellCheck=true** querystring parameter and the **bing-spell-check-subscription-key={YOUR_BING_KEY_HERE}** .</span></span> <span data-ttu-id="c2f82-151">Replace the `{YOUR_BING_KEY_HERE}` with your Bing spell checker key.</span><span class="sxs-lookup"><span data-stu-id="c2f82-151">Replace the `{YOUR_BING_KEY_HERE}` with your Bing spell checker key.</span></span>

```JSON
{
  "query": "Book a flite to London?",
  "alteredQuery": "Book a flight to London?",
  "topScoringIntent": {
    "intent": "BookFlight",
    "score": 0.780123
  },
  "entities": []
}
```

## <a name="publish-your-trained-app-to-an-http-endpoint"></a><span data-ttu-id="c2f82-152">Publish your trained app to an HTTP endpoint</span><span class="sxs-lookup"><span data-stu-id="c2f82-152">Publish your trained app to an HTTP endpoint</span></span>
<span data-ttu-id="c2f82-153">Open your app by clicking its name on the **My Apps** page, and then click **Publish** in the top panel.</span><span class="sxs-lookup"><span data-stu-id="c2f82-153">Open your app by clicking its name on the **My Apps** page, and then click **Publish** in the top panel.</span></span> 

![Publish page-](./media/luis-how-to-publish-app/publish-to-production.png)
 
<span data-ttu-id="c2f82-155">When your app is successfully published, a green success notification appears at the top of the browser.</span><span class="sxs-lookup"><span data-stu-id="c2f82-155">When your app is successfully published, a green success notification appears at the top of the browser.</span></span> 

* <span data-ttu-id="c2f82-156">Choose whether to publish to **Production** or to **Staging** by selecting from the drop-down menu under **Select slot**.</span><span class="sxs-lookup"><span data-stu-id="c2f82-156">Choose whether to publish to **Production** or to **Staging** by selecting from the drop-down menu under **Select slot**.</span></span> 

## <a name="assign-key"></a><span data-ttu-id="c2f82-157">Assign key</span><span class="sxs-lookup"><span data-stu-id="c2f82-157">Assign key</span></span>

<span data-ttu-id="c2f82-158">If you want to use a key other than the free Starter_Key shown, click the **Add Key** button.</span><span class="sxs-lookup"><span data-stu-id="c2f82-158">If you want to use a key other than the free Starter_Key shown, click the **Add Key** button.</span></span> <span data-ttu-id="c2f82-159">This action opens a dialog that allows you to select an existing endpoint key to assign to the app.</span><span class="sxs-lookup"><span data-stu-id="c2f82-159">This action opens a dialog that allows you to select an existing endpoint key to assign to the app.</span></span> <span data-ttu-id="c2f82-160">For more information on how to create and add endpoint keys to your LUIS app, see [Manage your keys](luis-how-to-manage-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c2f82-160">For more information on how to create and add endpoint keys to your LUIS app, see [Manage your keys](luis-how-to-manage-keys.md).</span></span>

<span data-ttu-id="c2f82-161">To see endpoints and keys associated with other regions, use the radio buttons to switch regions.</span><span class="sxs-lookup"><span data-stu-id="c2f82-161">To see endpoints and keys associated with other regions, use the radio buttons to switch regions.</span></span> <span data-ttu-id="c2f82-162">Each row in the **Resources and Keys** table lists Azure resources associated with your account and the endpoint keys associated with that resource.</span><span class="sxs-lookup"><span data-stu-id="c2f82-162">Each row in the **Resources and Keys** table lists Azure resources associated with your account and the endpoint keys associated with that resource.</span></span>

## <a name="endpoint-url-construction"></a><span data-ttu-id="c2f82-163">Endpoint URL construction</span><span class="sxs-lookup"><span data-stu-id="c2f82-163">Endpoint URL construction</span></span>
<span data-ttu-id="c2f82-164">The endpoint URL corresponds to the Azure region associated with the endpoint key.</span><span class="sxs-lookup"><span data-stu-id="c2f82-164">The endpoint URL corresponds to the Azure region associated with the endpoint key.</span></span>

<span data-ttu-id="c2f82-165">This table conveniently reflects your publishing configuration in the URL endpoint with route choices and query string values.</span><span class="sxs-lookup"><span data-stu-id="c2f82-165">This table conveniently reflects your publishing configuration in the URL endpoint with route choices and query string values.</span></span> <span data-ttu-id="c2f82-166">If you are constructing your endpoint URLs for your LUIS-calling application, make sure these same routes and query string values are set for the endpoint used -- if you want them set.</span><span class="sxs-lookup"><span data-stu-id="c2f82-166">If you are constructing your endpoint URLs for your LUIS-calling application, make sure these same routes and query string values are set for the endpoint used -- if you want them set.</span></span>

<span data-ttu-id="c2f82-167">The URL route is constructed with the region, and the app ID.</span><span class="sxs-lookup"><span data-stu-id="c2f82-167">The URL route is constructed with the region, and the app ID.</span></span> <span data-ttu-id="c2f82-168">If you are publishing in other regions or with other apps, the endpoint URL can be constructed by changing the region and app ID values.</span><span class="sxs-lookup"><span data-stu-id="c2f82-168">If you are publishing in other regions or with other apps, the endpoint URL can be constructed by changing the region and app ID values.</span></span> 

* <span data-ttu-id="c2f82-169">Select the Production slot and the **Publish** button.</span><span class="sxs-lookup"><span data-stu-id="c2f82-169">Select the Production slot and the **Publish** button.</span></span> <span data-ttu-id="c2f82-170">When the publish succeeds, use the displayed endpoint URL to access your LUIS app.</span><span class="sxs-lookup"><span data-stu-id="c2f82-170">When the publish succeeds, use the displayed endpoint URL to access your LUIS app.</span></span> 

### <a name="optional-query-string-parameters"></a><span data-ttu-id="c2f82-171">Optional query string parameters</span><span class="sxs-lookup"><span data-stu-id="c2f82-171">Optional query string parameters</span></span>
<span data-ttu-id="c2f82-172">The following query string parameters can be used with the endpoint URL:</span><span class="sxs-lookup"><span data-stu-id="c2f82-172">The following query string parameters can be used with the endpoint URL:</span></span>

<!-- TBD: what about speech priming? -->

|<span data-ttu-id="c2f82-173">Query string</span><span class="sxs-lookup"><span data-stu-id="c2f82-173">Query string</span></span>|<span data-ttu-id="c2f82-174">Type</span><span class="sxs-lookup"><span data-stu-id="c2f82-174">Type</span></span>|<span data-ttu-id="c2f82-175">Example value</span><span class="sxs-lookup"><span data-stu-id="c2f82-175">Example value</span></span>|<span data-ttu-id="c2f82-176">Purpose</span><span class="sxs-lookup"><span data-stu-id="c2f82-176">Purpose</span></span>|
|--|--|--|--|
|<span data-ttu-id="c2f82-177">verbose</span><span class="sxs-lookup"><span data-stu-id="c2f82-177">verbose</span></span>|<span data-ttu-id="c2f82-178">boolean</span><span class="sxs-lookup"><span data-stu-id="c2f82-178">boolean</span></span>|<span data-ttu-id="c2f82-179">true</span><span class="sxs-lookup"><span data-stu-id="c2f82-179">true</span></span>|<span data-ttu-id="c2f82-180">Include [all intent scores](#include-all-predicted-intent-scores) for utterance</span><span class="sxs-lookup"><span data-stu-id="c2f82-180">Include [all intent scores](#include-all-predicted-intent-scores) for utterance</span></span>|
|<span data-ttu-id="c2f82-181">timezoneOffset</span><span class="sxs-lookup"><span data-stu-id="c2f82-181">timezoneOffset</span></span>|<span data-ttu-id="c2f82-182">number (unit is minutes)</span><span class="sxs-lookup"><span data-stu-id="c2f82-182">number (unit is minutes)</span></span>|<span data-ttu-id="c2f82-183">60</span><span class="sxs-lookup"><span data-stu-id="c2f82-183">60</span></span>|<span data-ttu-id="c2f82-184">Set [timezone offset](luis-concept-data-alteration.md#change-time-zone-of-prebuilt-datetimev2-entity) for [datetimeV2 prebuilt entities](luis-reference-prebuilt-datetimev2.md)</span><span class="sxs-lookup"><span data-stu-id="c2f82-184">Set [timezone offset](luis-concept-data-alteration.md#change-time-zone-of-prebuilt-datetimev2-entity) for [datetimeV2 prebuilt entities](luis-reference-prebuilt-datetimev2.md)</span></span>|
|<span data-ttu-id="c2f82-185">spellCheck</span><span class="sxs-lookup"><span data-stu-id="c2f82-185">spellCheck</span></span>|<span data-ttu-id="c2f82-186">boolean</span><span class="sxs-lookup"><span data-stu-id="c2f82-186">boolean</span></span>|<span data-ttu-id="c2f82-187">true</span><span class="sxs-lookup"><span data-stu-id="c2f82-187">true</span></span>|<span data-ttu-id="c2f82-188">[correct spelling](#enable-bing-spell-checker) of utterance -- used in conjunction with bing-spell-check-subscription-key query string parameter</span><span class="sxs-lookup"><span data-stu-id="c2f82-188">[correct spelling](#enable-bing-spell-checker) of utterance -- used in conjunction with bing-spell-check-subscription-key query string parameter</span></span>|
|<span data-ttu-id="c2f82-189">bing-spell-check-subscription-key</span><span class="sxs-lookup"><span data-stu-id="c2f82-189">bing-spell-check-subscription-key</span></span>|<span data-ttu-id="c2f82-190">subscription ID</span><span class="sxs-lookup"><span data-stu-id="c2f82-190">subscription ID</span></span>||<span data-ttu-id="c2f82-191">used in conjunction with spellCheck query string parameter</span><span class="sxs-lookup"><span data-stu-id="c2f82-191">used in conjunction with spellCheck query string parameter</span></span>|
|<span data-ttu-id="c2f82-192">staging</span><span class="sxs-lookup"><span data-stu-id="c2f82-192">staging</span></span>|<span data-ttu-id="c2f82-193">boolean</span><span class="sxs-lookup"><span data-stu-id="c2f82-193">boolean</span></span>|<span data-ttu-id="c2f82-194">false</span><span class="sxs-lookup"><span data-stu-id="c2f82-194">false</span></span>|<span data-ttu-id="c2f82-195">select staging or production endpoint</span><span class="sxs-lookup"><span data-stu-id="c2f82-195">select staging or production endpoint</span></span>|
|<span data-ttu-id="c2f82-196">log</span><span class="sxs-lookup"><span data-stu-id="c2f82-196">log</span></span>|<span data-ttu-id="c2f82-197">boolean</span><span class="sxs-lookup"><span data-stu-id="c2f82-197">boolean</span></span>|<span data-ttu-id="c2f82-198">true</span><span class="sxs-lookup"><span data-stu-id="c2f82-198">true</span></span>|<span data-ttu-id="c2f82-199">add query and results to log</span><span class="sxs-lookup"><span data-stu-id="c2f82-199">add query and results to log</span></span>|


## <a name="test-your-published-endpoint-in-a-browser"></a><span data-ttu-id="c2f82-200">Test your published endpoint in a browser</span><span class="sxs-lookup"><span data-stu-id="c2f82-200">Test your published endpoint in a browser</span></span>
<span data-ttu-id="c2f82-201">Test your published endpoint by selecting the URL in the **Endpoint** column.</span><span class="sxs-lookup"><span data-stu-id="c2f82-201">Test your published endpoint by selecting the URL in the **Endpoint** column.</span></span> <span data-ttu-id="c2f82-202">The default browser opens with the generated URL.</span><span class="sxs-lookup"><span data-stu-id="c2f82-202">The default browser opens with the generated URL.</span></span> <span data-ttu-id="c2f82-203">Set the URL parameter "&q" to your test query.</span><span class="sxs-lookup"><span data-stu-id="c2f82-203">Set the URL parameter "&q" to your test query.</span></span> <span data-ttu-id="c2f82-204">For example, append `&q=Book me a flight to Boston on May 4` to your URL, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="c2f82-204">For example, append `&q=Book me a flight to Boston on May 4` to your URL, and then press Enter.</span></span> <span data-ttu-id="c2f82-205">The browser displays the JSON response of your HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="c2f82-205">The browser displays the JSON response of your HTTP endpoint.</span></span> 

![JSON response from a published HTTP endpoint](./media/luis-how-to-publish-app/luis-publish-app-json-response.png)

## <a name="next-steps"></a><span data-ttu-id="c2f82-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2f82-207">Next steps</span></span>

* <span data-ttu-id="c2f82-208">See [Manage keys](./luis-how-to-manage-keys.md) to add keys to your LUIS app, and learn about how keys map to regions.</span><span class="sxs-lookup"><span data-stu-id="c2f82-208">See [Manage keys](./luis-how-to-manage-keys.md) to add keys to your LUIS app, and learn about how keys map to regions.</span></span>
* <span data-ttu-id="c2f82-209">See [Train and test your app](luis-interactive-test.md) for instructions on how to test your published app in the test console.</span><span class="sxs-lookup"><span data-stu-id="c2f82-209">See [Train and test your app](luis-interactive-test.md) for instructions on how to test your published app in the test console.</span></span>
