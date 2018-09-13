---
title: Test your LUIS app inside the LUIS portal
titleSuffix: Azure Cognitive Services
description: Use Language Understanding (LUIS) to continuously work on your application to refine it and improve its language understanding.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: f697e55e095baf113b7e622c4e7447b78444d4ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968999"
---
# <a name="test-your-luis-app"></a><span data-ttu-id="591fc-103">Test your LUIS app</span><span class="sxs-lookup"><span data-stu-id="591fc-103">Test your LUIS app</span></span>
<a name="train-your-app"></a>
<span data-ttu-id="591fc-104">[Testing](luis-concept-test.md) an app is an iterative process.</span><span class="sxs-lookup"><span data-stu-id="591fc-104">[Testing](luis-concept-test.md) an app is an iterative process.</span></span> <span data-ttu-id="591fc-105">After training your LUIS app, test it with sample utterances to see if the intents and entities are recognized correctly.</span><span class="sxs-lookup"><span data-stu-id="591fc-105">After training your LUIS app, test it with sample utterances to see if the intents and entities are recognized correctly.</span></span> <span data-ttu-id="591fc-106">If they're not, make updates to the LUIS app, train, and test again.</span><span class="sxs-lookup"><span data-stu-id="591fc-106">If they're not, make updates to the LUIS app, train, and test again.</span></span> 

<!-- anchors for H2 name changes -->
<a name="test-your-app"></a>
<a name="access-the-test-page"></a>
<a name="luis-interactive-testing"></a>
## <a name="test-an-utterance"></a><span data-ttu-id="591fc-107">Test an utterance</span><span class="sxs-lookup"><span data-stu-id="591fc-107">Test an utterance</span></span>

1. <span data-ttu-id="591fc-108">Access your app by selecting its name on the **My Apps** page.</span><span class="sxs-lookup"><span data-stu-id="591fc-108">Access your app by selecting its name on the **My Apps** page.</span></span> 

2. <span data-ttu-id="591fc-109">To access the **Test** slide-out panel, select **Test** in your application's top panel.</span><span class="sxs-lookup"><span data-stu-id="591fc-109">To access the **Test** slide-out panel, select **Test** in your application's top panel.</span></span>

    ![Train & Test App page](./media/luis-how-to-interactive-test/test.png)

3. <span data-ttu-id="591fc-111">Enter an utterance in the text box and select Enter.</span><span class="sxs-lookup"><span data-stu-id="591fc-111">Enter an utterance in the text box and select Enter.</span></span> <span data-ttu-id="591fc-112">You can type as many test utterances as you want in the **Test**, but only one utterance at a time.</span><span class="sxs-lookup"><span data-stu-id="591fc-112">You can type as many test utterances as you want in the **Test**, but only one utterance at a time.</span></span>

4. <span data-ttu-id="591fc-113">The utterance, its top intent, and score are added to the list of utterances under the text box.</span><span class="sxs-lookup"><span data-stu-id="591fc-113">The utterance, its top intent, and score are added to the list of utterances under the text box.</span></span>

    ![Interactive testing identifies the wrong intent](./media/luis-how-to-interactive-test/test-weather-1.png)

## <a name="clear-test-panel"></a><span data-ttu-id="591fc-115">Clear test panel</span><span class="sxs-lookup"><span data-stu-id="591fc-115">Clear test panel</span></span>
<span data-ttu-id="591fc-116">To clear all the entered test utterances and their results from the test console, select **Start over** at the upper-left corner of the **Test panel**.</span><span class="sxs-lookup"><span data-stu-id="591fc-116">To clear all the entered test utterances and their results from the test console, select **Start over** at the upper-left corner of the **Test panel**.</span></span> 

## <a name="close-test-panel"></a><span data-ttu-id="591fc-117">Close test panel</span><span class="sxs-lookup"><span data-stu-id="591fc-117">Close test panel</span></span>
<span data-ttu-id="591fc-118">To close the **Test** panel, select the **Test** button again.</span><span class="sxs-lookup"><span data-stu-id="591fc-118">To close the **Test** panel, select the **Test** button again.</span></span>

## <a name="inspect-score"></a><span data-ttu-id="591fc-119">Inspect score</span><span class="sxs-lookup"><span data-stu-id="591fc-119">Inspect score</span></span>
<span data-ttu-id="591fc-120">You inspect details of the test result in the **Inspect** panel.</span><span class="sxs-lookup"><span data-stu-id="591fc-120">You inspect details of the test result in the **Inspect** panel.</span></span> 
 
1. <span data-ttu-id="591fc-121">With the **Test** slide-out panel open, select **Inspect** for an utterance you want to compare.</span><span class="sxs-lookup"><span data-stu-id="591fc-121">With the **Test** slide-out panel open, select **Inspect** for an utterance you want to compare.</span></span> 

    ![Inspect button](./media/luis-how-to-interactive-test/inspect.png)

2. <span data-ttu-id="591fc-123">The **Inspection** panel appears.</span><span class="sxs-lookup"><span data-stu-id="591fc-123">The **Inspection** panel appears.</span></span> <span data-ttu-id="591fc-124">The panel includes the top scoring intent as well as any identified entities.</span><span class="sxs-lookup"><span data-stu-id="591fc-124">The panel includes the top scoring intent as well as any identified entities.</span></span> <span data-ttu-id="591fc-125">The panel shows the result of the selected utterance.</span><span class="sxs-lookup"><span data-stu-id="591fc-125">The panel shows the result of the selected utterance.</span></span>

    ![Inspect button](./media/luis-how-to-interactive-test/inspect-panel.png)

## <a name="correct-top-scoring-intent"></a><span data-ttu-id="591fc-127">Correct top scoring intent</span><span class="sxs-lookup"><span data-stu-id="591fc-127">Correct top scoring intent</span></span>

1. <span data-ttu-id="591fc-128">If the top scoring intent is incorrect, select the **Edit** button.</span><span class="sxs-lookup"><span data-stu-id="591fc-128">If the top scoring intent is incorrect, select the **Edit** button.</span></span>

2.  <span data-ttu-id="591fc-129">In the drop-down list, select the correct intent for the utterance.</span><span class="sxs-lookup"><span data-stu-id="591fc-129">In the drop-down list, select the correct intent for the utterance.</span></span>

    ![Select correct intent](./media/luis-how-to-interactive-test/intent-select.png)

## <a name="view-sentiment-results"></a><span data-ttu-id="591fc-131">View sentiment results</span><span class="sxs-lookup"><span data-stu-id="591fc-131">View sentiment results</span></span>

<span data-ttu-id="591fc-132">If **Sentiment analysis** is configured on the **[Publish](luis-how-to-publish-app.md#enable-sentiment-analysis)** page, the test results include the sentiment found in the utterance.</span><span class="sxs-lookup"><span data-stu-id="591fc-132">If **Sentiment analysis** is configured on the **[Publish](luis-how-to-publish-app.md#enable-sentiment-analysis)** page, the test results include the sentiment found in the utterance.</span></span> 

![Image of Test pane with sentiment analysis](./media/luis-how-to-interactive-test/sentiment.png)

## <a name="correct-matched-patterns-intent"></a><span data-ttu-id="591fc-134">Correct matched pattern's intent</span><span class="sxs-lookup"><span data-stu-id="591fc-134">Correct matched pattern's intent</span></span>
<span data-ttu-id="591fc-135">If you are using [Patterns](luis-concept-patterns.md) and the utterance matched a pattern, but the wrong intent was predicted, select the **Edit** link by the pattern, then select the correct intent.</span><span class="sxs-lookup"><span data-stu-id="591fc-135">If you are using [Patterns](luis-concept-patterns.md) and the utterance matched a pattern, but the wrong intent was predicted, select the **Edit** link by the pattern, then select the correct intent.</span></span>

## <a name="compare-with-published-version"></a><span data-ttu-id="591fc-136">Compare with published version</span><span class="sxs-lookup"><span data-stu-id="591fc-136">Compare with published version</span></span>
<span data-ttu-id="591fc-137">You can test the active version of your app with the published [endpoint](luis-glossary.md#endpoint) version.</span><span class="sxs-lookup"><span data-stu-id="591fc-137">You can test the active version of your app with the published [endpoint](luis-glossary.md#endpoint) version.</span></span> <span data-ttu-id="591fc-138">In the **Inspect** panel, select **Compare with published**.</span><span class="sxs-lookup"><span data-stu-id="591fc-138">In the **Inspect** panel, select **Compare with published**.</span></span> <span data-ttu-id="591fc-139">Any testing against the published model is deducted from your Azure subscription quota balance.</span><span class="sxs-lookup"><span data-stu-id="591fc-139">Any testing against the published model is deducted from your Azure subscription quota balance.</span></span> 

![Compare with published](./media/luis-how-to-interactive-test/inspect-panel-compare.png)

## <a name="view-endpoint-json-in-test-panel"></a><span data-ttu-id="591fc-141">View endpoint JSON in test panel</span><span class="sxs-lookup"><span data-stu-id="591fc-141">View endpoint JSON in test panel</span></span>
<span data-ttu-id="591fc-142">You can view the endpoint JSON returned for the comparison by selecting the **Show JSON view**.</span><span class="sxs-lookup"><span data-stu-id="591fc-142">You can view the endpoint JSON returned for the comparison by selecting the **Show JSON view**.</span></span>

![Published JSON response](./media/luis-how-to-interactive-test/inspect-panel-compare-json.png)

<!--Service name is 'Bing Spell Check v7 API' in the portal-->
## <a name="additional-settings-in-test-panel"></a><span data-ttu-id="591fc-144">Additional settings in test panel</span><span class="sxs-lookup"><span data-stu-id="591fc-144">Additional settings in test panel</span></span>

### <a name="luis-endpoint"></a><span data-ttu-id="591fc-145">LUIS endpoint</span><span class="sxs-lookup"><span data-stu-id="591fc-145">LUIS endpoint</span></span>
<span data-ttu-id="591fc-146">If you have several LUIS endpoints, use the **Additional Settings** link on the Test's Published pane to change the endpoint used for testing.</span><span class="sxs-lookup"><span data-stu-id="591fc-146">If you have several LUIS endpoints, use the **Additional Settings** link on the Test's Published pane to change the endpoint used for testing.</span></span> <span data-ttu-id="591fc-147">If you are not sure which endpoint to use, select the default **Starter_Key**.</span><span class="sxs-lookup"><span data-stu-id="591fc-147">If you are not sure which endpoint to use, select the default **Starter_Key**.</span></span> 

![Test panel with Additional Settings link highlighted](./media/luis-how-to-interactive-test/interactive-with-spell-check-service-key.png)


### <a name="view-bing-spell-check-corrections-in-test-panel"></a><span data-ttu-id="591fc-149">View Bing Spell Check corrections in test panel</span><span class="sxs-lookup"><span data-stu-id="591fc-149">View Bing Spell Check corrections in test panel</span></span>
<span data-ttu-id="591fc-150">Requirements to view the spelling corrections:</span><span class="sxs-lookup"><span data-stu-id="591fc-150">Requirements to view the spelling corrections:</span></span> 

* <span data-ttu-id="591fc-151">Published app</span><span class="sxs-lookup"><span data-stu-id="591fc-151">Published app</span></span>
* <span data-ttu-id="591fc-152">Bing Spell Check [service key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api).</span><span class="sxs-lookup"><span data-stu-id="591fc-152">Bing Spell Check [service key](https://azure.microsoft.com/try/cognitive-services/?api=spellcheck-api).</span></span> <span data-ttu-id="591fc-153">The service key is not stored and needs to be reset for each browser session.</span><span class="sxs-lookup"><span data-stu-id="591fc-153">The service key is not stored and needs to be reset for each browser session.</span></span> 

<span data-ttu-id="591fc-154">Use the following procedure to include the [Bing Spell Check v7](https://azure.microsoft.com/services/cognitive-services/spell-check/) service  in the Test pane results.</span><span class="sxs-lookup"><span data-stu-id="591fc-154">Use the following procedure to include the [Bing Spell Check v7](https://azure.microsoft.com/services/cognitive-services/spell-check/) service  in the Test pane results.</span></span> 

1. <span data-ttu-id="591fc-155">In the **Test** pane, enter an utterance.</span><span class="sxs-lookup"><span data-stu-id="591fc-155">In the **Test** pane, enter an utterance.</span></span> <span data-ttu-id="591fc-156">When the utterance is predicted, select **[Inspect](#inspect-score)** underneath the utterance you entered.</span><span class="sxs-lookup"><span data-stu-id="591fc-156">When the utterance is predicted, select **[Inspect](#inspect-score)** underneath the utterance you entered.</span></span> 

2. <span data-ttu-id="591fc-157">When the **Inspect** panel opens, select **[Compare with Published](#compare-with-published-version)**.</span><span class="sxs-lookup"><span data-stu-id="591fc-157">When the **Inspect** panel opens, select **[Compare with Published](#compare-with-published-version)**.</span></span> 

3. <span data-ttu-id="591fc-158">When the **Published** panel opens, select **[Additional Settings](#additional-settings-in-test-panel)**.</span><span class="sxs-lookup"><span data-stu-id="591fc-158">When the **Published** panel opens, select **[Additional Settings](#additional-settings-in-test-panel)**.</span></span>

4. <span data-ttu-id="591fc-159">In the pop-up dialog, enter your **Bing Spell Check** service key.</span><span class="sxs-lookup"><span data-stu-id="591fc-159">In the pop-up dialog, enter your **Bing Spell Check** service key.</span></span> 
    <span data-ttu-id="591fc-160">![Enter Bing Spell Check service key](./media/luis-how-to-interactive-test/interactive-with-spell-check-service-key.png)</span><span class="sxs-lookup"><span data-stu-id="591fc-160">![Enter Bing Spell Check service key](./media/luis-how-to-interactive-test/interactive-with-spell-check-service-key.png)</span></span>

5. <span data-ttu-id="591fc-161">Enter a query with an incorrect spelling such as `book flite to seattle` and select enter.</span><span class="sxs-lookup"><span data-stu-id="591fc-161">Enter a query with an incorrect spelling such as `book flite to seattle` and select enter.</span></span> <span data-ttu-id="591fc-162">The incorrect spelling of the word `flite` is replaced in the query sent to LUIS and the resulting JSON shows both the original query, as `query`, and the corrected spelling in the query, as `alteredQuery`.</span><span class="sxs-lookup"><span data-stu-id="591fc-162">The incorrect spelling of the word `flite` is replaced in the query sent to LUIS and the resulting JSON shows both the original query, as `query`, and the corrected spelling in the query, as `alteredQuery`.</span></span>

    ![Corrected spelling JSON](./media/luis-how-to-interactive-test/interactive-with-spell-check-results.png)

<a name="json-file-with-no-duplicates"></a>
<a name="import-a-dataset-file-for-batch-testing"></a>
<a name="export-rename-delete-or-download-dataset"></a>
<a name="run-a-batch-test-on-your-trained-app"></a>
<a name="access-batch-test-result-details-in-a-visualized-view"></a>
<a name="filter-chart-results-by-intent-or-entity"></a>
<a name="investigate-false-sections"></a>
<a name="view single-point utterance data"></a>
<a name="relabel-utterances-and-retrain"></a>
<a name="false-test-results"></a>
## <a name="batch-testing"></a><span data-ttu-id="591fc-164">Batch testing</span><span class="sxs-lookup"><span data-stu-id="591fc-164">Batch testing</span></span>
<span data-ttu-id="591fc-165">See batch testing [concepts](luis-concept-batch-test.md) and learn [how to](luis-how-to-batch-test.md) test a batch of utterances.</span><span class="sxs-lookup"><span data-stu-id="591fc-165">See batch testing [concepts](luis-concept-batch-test.md) and learn [how to](luis-how-to-batch-test.md) test a batch of utterances.</span></span>

## <a name="next-steps"></a><span data-ttu-id="591fc-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="591fc-166">Next steps</span></span>

<span data-ttu-id="591fc-167">If testing indicates that your LUIS app doesn't recognize the correct intents and entities, you can work to improve your LUIS app's accuracy by labeling more utterances or adding features.</span><span class="sxs-lookup"><span data-stu-id="591fc-167">If testing indicates that your LUIS app doesn't recognize the correct intents and entities, you can work to improve your LUIS app's accuracy by labeling more utterances or adding features.</span></span> 

* [<span data-ttu-id="591fc-168">Label suggested utterances with LUIS</span><span class="sxs-lookup"><span data-stu-id="591fc-168">Label suggested utterances with LUIS</span></span>](luis-how-to-review-endoint-utt.md) 
* [<span data-ttu-id="591fc-169">Use features to improve your LUIS app's performance</span><span class="sxs-lookup"><span data-stu-id="591fc-169">Use features to improve your LUIS app's performance</span></span>](luis-how-to-add-features.md) 
