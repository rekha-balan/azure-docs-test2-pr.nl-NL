---
title: Add Bing Spell Check API v7 to LUIS queries | Microsoft Docs
titleSuffix: Azure
description: Correct misspelled words in utterances by adding Bing Spell Check API V7 to LUIS endpoint queries.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 02/27/2018
ms.author: diberry
ms.openlocfilehash: 19774d2a87e9c74f291f030aab09cb21fe4a931b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966137"
---
# <a name="correct-misspelled-words-with-bing-spell-check"></a><span data-ttu-id="d34f4-103">Correct misspelled words with Bing Spell Check</span><span class="sxs-lookup"><span data-stu-id="d34f4-103">Correct misspelled words with Bing Spell Check</span></span>

<span data-ttu-id="d34f4-104">You can integrate your LUIS app with [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) to correct misspelled words in utterances before LUIS predicts the score and entities of the utterance.</span><span class="sxs-lookup"><span data-stu-id="d34f4-104">You can integrate your LUIS app with [Bing Spell Check API V7](https://azure.microsoft.com/services/cognitive-services/spell-check/) to correct misspelled words in utterances before LUIS predicts the score and entities of the utterance.</span></span> 

## <a name="create-first-key-for-bing-spell-check-v7"></a><span data-ttu-id="d34f4-105">Create first key for Bing Spell Check V7</span><span class="sxs-lookup"><span data-stu-id="d34f4-105">Create first key for Bing Spell Check V7</span></span>
<span data-ttu-id="d34f4-106">Your [first Bing Spell Check API v7 key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api) is free.</span><span class="sxs-lookup"><span data-stu-id="d34f4-106">Your [first Bing Spell Check API v7 key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api) is free.</span></span> 

![Create free key](./media/luis-tutorial-bing-spellcheck/free-key.png)

<a name"create-subscription-key"></a><span data-ttu-id="d34f4-108"></span><span class="sxs-lookup"><span data-stu-id="d34f4-108"></span></span>
## <a name="create-endpoint-key"></a><span data-ttu-id="d34f4-109">Create Endpoint key</span><span class="sxs-lookup"><span data-stu-id="d34f4-109">Create Endpoint key</span></span>
<span data-ttu-id="d34f4-110">If your free key expired, create an endpoint key.</span><span class="sxs-lookup"><span data-stu-id="d34f4-110">If your free key expired, create an endpoint key.</span></span>

1. <span data-ttu-id="d34f4-111">Log in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d34f4-111">Log in to the [Azure portal](https://portal.azure.com).</span></span> 

2. <span data-ttu-id="d34f4-112">Select **Create a resource** in the top left corner.</span><span class="sxs-lookup"><span data-stu-id="d34f4-112">Select **Create a resource** in the top left corner.</span></span>

3. <span data-ttu-id="d34f4-113">In the search box, enter `Bing Spell Check API V7`.</span><span class="sxs-lookup"><span data-stu-id="d34f4-113">In the search box, enter `Bing Spell Check API V7`.</span></span>

    ![Search for Bing Spell Check API V7](./media/luis-tutorial-bing-spellcheck/portal-search.png)

4. <span data-ttu-id="d34f4-115">Select the service.</span><span class="sxs-lookup"><span data-stu-id="d34f4-115">Select the service.</span></span> 

5. <span data-ttu-id="d34f4-116">An information panel appears to the right containing information including the Legal Notice.</span><span class="sxs-lookup"><span data-stu-id="d34f4-116">An information panel appears to the right containing information including the Legal Notice.</span></span> <span data-ttu-id="d34f4-117">Select **Create** to begin the subscription creation process.</span><span class="sxs-lookup"><span data-stu-id="d34f4-117">Select **Create** to begin the subscription creation process.</span></span> 

6. <span data-ttu-id="d34f4-118">In the next panel, enter your service settings.</span><span class="sxs-lookup"><span data-stu-id="d34f4-118">In the next panel, enter your service settings.</span></span> <span data-ttu-id="d34f4-119">Wait for service creation process to finish.</span><span class="sxs-lookup"><span data-stu-id="d34f4-119">Wait for service creation process to finish.</span></span>

    ![Enter service settings](./media/luis-tutorial-bing-spellcheck/subscription-settings.png)

7. <span data-ttu-id="d34f4-121">Select **All resources** under the **Favorites** title on the left side navigation.</span><span class="sxs-lookup"><span data-stu-id="d34f4-121">Select **All resources** under the **Favorites** title on the left side navigation.</span></span>

8. <span data-ttu-id="d34f4-122">Select the new service.</span><span class="sxs-lookup"><span data-stu-id="d34f4-122">Select the new service.</span></span> <span data-ttu-id="d34f4-123">Its type is **Cognitive Services** and the location is **global**.</span><span class="sxs-lookup"><span data-stu-id="d34f4-123">Its type is **Cognitive Services** and the location is **global**.</span></span> 

9. <span data-ttu-id="d34f4-124">In the main panel, select **Keys** to see your new keys.</span><span class="sxs-lookup"><span data-stu-id="d34f4-124">In the main panel, select **Keys** to see your new keys.</span></span>

    ![Grab keys](./media/luis-tutorial-bing-spellcheck/grab-keys.png)

10. <span data-ttu-id="d34f4-126">Copy the first key.</span><span class="sxs-lookup"><span data-stu-id="d34f4-126">Copy the first key.</span></span> <span data-ttu-id="d34f4-127">You only need one of the two keys.</span><span class="sxs-lookup"><span data-stu-id="d34f4-127">You only need one of the two keys.</span></span> 

## <a name="using-the-key-in-luis-test-panel"></a><span data-ttu-id="d34f4-128">Using the key in LUIS test panel</span><span class="sxs-lookup"><span data-stu-id="d34f4-128">Using the key in LUIS test panel</span></span>
<span data-ttu-id="d34f4-129">There are two places in LUIS to use the key.</span><span class="sxs-lookup"><span data-stu-id="d34f4-129">There are two places in LUIS to use the key.</span></span> <span data-ttu-id="d34f4-130">The first is in the [test panel](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel).</span><span class="sxs-lookup"><span data-stu-id="d34f4-130">The first is in the [test panel](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel).</span></span> <span data-ttu-id="d34f4-131">The key isn't saved into LUIS but instead is a session variable.</span><span class="sxs-lookup"><span data-stu-id="d34f4-131">The key isn't saved into LUIS but instead is a session variable.</span></span> <span data-ttu-id="d34f4-132">You need to set the key every time you want the test panel to apply the Bing Spell Check API v7 service to the utterance.</span><span class="sxs-lookup"><span data-stu-id="d34f4-132">You need to set the key every time you want the test panel to apply the Bing Spell Check API v7 service to the utterance.</span></span> <span data-ttu-id="d34f4-133">See [instructions](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel) in the test panel for setting the key.</span><span class="sxs-lookup"><span data-stu-id="d34f4-133">See [instructions](luis-interactive-test.md#view-bing-spell-check-corrections-in-test-panel) in the test panel for setting the key.</span></span>

## <a name="adding-the-key-to-the-endpoint-url"></a><span data-ttu-id="d34f4-134">Adding the key to the endpoint URL</span><span class="sxs-lookup"><span data-stu-id="d34f4-134">Adding the key to the endpoint URL</span></span>
<span data-ttu-id="d34f4-135">The endpoint query needs the key passed in the query string parameters for each query you want to apply spelling correction.</span><span class="sxs-lookup"><span data-stu-id="d34f4-135">The endpoint query needs the key passed in the query string parameters for each query you want to apply spelling correction.</span></span> <span data-ttu-id="d34f4-136">You may have a chatbot that calls LUIS or you may call the LUIS endpoint API directly.</span><span class="sxs-lookup"><span data-stu-id="d34f4-136">You may have a chatbot that calls LUIS or you may call the LUIS endpoint API directly.</span></span> <span data-ttu-id="d34f4-137">Regardless of how the endpoint is called, each and every call must include the required information for spelling corrections to work properly.</span><span class="sxs-lookup"><span data-stu-id="d34f4-137">Regardless of how the endpoint is called, each and every call must include the required information for spelling corrections to work properly.</span></span>

<span data-ttu-id="d34f4-138">The endpoint URL has several values that need to be passed correctly.</span><span class="sxs-lookup"><span data-stu-id="d34f4-138">The endpoint URL has several values that need to be passed correctly.</span></span> <span data-ttu-id="d34f4-139">The Bing Spell Check API v7 key is just another one of these.</span><span class="sxs-lookup"><span data-stu-id="d34f4-139">The Bing Spell Check API v7 key is just another one of these.</span></span> <span data-ttu-id="d34f4-140">You must set the **spellCheck** parameter to true and you must set the value of **bing-spell-check-subscription-key** to the key value:</span><span class="sxs-lookup"><span data-stu-id="d34f4-140">You must set the **spellCheck** parameter to true and you must set the value of **bing-spell-check-subscription-key** to the key value:</span></span>

`https://{region}.api.cognitive.microsoft.com/luis/v2.0/apps/{appID}?subscription-key={luisKey}&spellCheck=**true**&bing-spell-check-subscription-key=**{bingKey}**&verbose=true&timezoneOffset=0&q={utterance}`

## <a name="send-misspelled-utterance-to-luis"></a><span data-ttu-id="d34f4-141">Send misspelled utterance to LUIS</span><span class="sxs-lookup"><span data-stu-id="d34f4-141">Send misspelled utterance to LUIS</span></span>
1. <span data-ttu-id="d34f4-142">In a web browser, copy the preceding string and replace the `region`, `appId`, `luisKey`, and `bingKey` with your own values.</span><span class="sxs-lookup"><span data-stu-id="d34f4-142">In a web browser, copy the preceding string and replace the `region`, `appId`, `luisKey`, and `bingKey` with your own values.</span></span> <span data-ttu-id="d34f4-143">Make sure to use the endpoint region, if it is different from your publishing [region](luis-reference-regions.md).</span><span class="sxs-lookup"><span data-stu-id="d34f4-143">Make sure to use the endpoint region, if it is different from your publishing [region](luis-reference-regions.md).</span></span>

2. <span data-ttu-id="d34f4-144">Add a misspelled utterance such as "How far is the mountainn?".</span><span class="sxs-lookup"><span data-stu-id="d34f4-144">Add a misspelled utterance such as "How far is the mountainn?".</span></span> <span data-ttu-id="d34f4-145">In English, `mountain`, with one `n`, is the correct spelling.</span><span class="sxs-lookup"><span data-stu-id="d34f4-145">In English, `mountain`, with one `n`, is the correct spelling.</span></span> 

3. <span data-ttu-id="d34f4-146">Select enter to send the query to LUIS.</span><span class="sxs-lookup"><span data-stu-id="d34f4-146">Select enter to send the query to LUIS.</span></span>

4. <span data-ttu-id="d34f4-147">LUIS responds with a JSON result for `How far is the mountain?`.</span><span class="sxs-lookup"><span data-stu-id="d34f4-147">LUIS responds with a JSON result for `How far is the mountain?`.</span></span> <span data-ttu-id="d34f4-148">If Bing Spell Check API v7 detects a misspelling, the `query` field in the LUIS app's JSON response contains the original query, and the `alteredQuery` field contains the corrected query sent to LUIS.</span><span class="sxs-lookup"><span data-stu-id="d34f4-148">If Bing Spell Check API v7 detects a misspelling, the `query` field in the LUIS app's JSON response contains the original query, and the `alteredQuery` field contains the corrected query sent to LUIS.</span></span>

```
{
  "query": "How far is the mountainn?",
  "alteredQuery": "How far is the mountain?",
  "topScoringIntent": {
    "intent": "Concierge",
    "score": 0.183866
  },
  "entities": []
}
```

## <a name="ignore-spelling-mistakes"></a><span data-ttu-id="d34f4-149">Ignore spelling mistakes</span><span class="sxs-lookup"><span data-stu-id="d34f4-149">Ignore spelling mistakes</span></span>
<span data-ttu-id="d34f4-150">If you don't want to use the Bing Spell Check API v7 service, you can label utterances that have spelling mistakes so that LUIS can learn proper spelling as well as typos.</span><span class="sxs-lookup"><span data-stu-id="d34f4-150">If you don't want to use the Bing Spell Check API v7 service, you can label utterances that have spelling mistakes so that LUIS can learn proper spelling as well as typos.</span></span> <span data-ttu-id="d34f4-151">This option requires more labeling effort than using a spell checker.</span><span class="sxs-lookup"><span data-stu-id="d34f4-151">This option requires more labeling effort than using a spell checker.</span></span>

## <a name="publishing-page"></a><span data-ttu-id="d34f4-152">Publishing page</span><span class="sxs-lookup"><span data-stu-id="d34f4-152">Publishing page</span></span>
<span data-ttu-id="d34f4-153">The [publishing](luis-how-to-publish-app.md) page has an **Enable Bing spell checker** checkbox.</span><span class="sxs-lookup"><span data-stu-id="d34f4-153">The [publishing](luis-how-to-publish-app.md) page has an **Enable Bing spell checker** checkbox.</span></span> <span data-ttu-id="d34f4-154">This is a convenience to create the key and understand how the endpoint URL changes.</span><span class="sxs-lookup"><span data-stu-id="d34f4-154">This is a convenience to create the key and understand how the endpoint URL changes.</span></span> <span data-ttu-id="d34f4-155">You still have to use the correct endpoint parameters in order to have spelling corrected for each utterance.</span><span class="sxs-lookup"><span data-stu-id="d34f4-155">You still have to use the correct endpoint parameters in order to have spelling corrected for each utterance.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="d34f4-156">Learn more about example utterances</span><span class="sxs-lookup"><span data-stu-id="d34f4-156">Learn more about example utterances</span></span>](luis-how-to-add-example-utterances.md)
