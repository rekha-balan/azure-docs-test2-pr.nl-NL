---
title: Batch test with 1000 example utterances
titleSuffix: Azure Cognitive Services
description: Use Language Understanding (LUIS) batch testing sets to find utterances with incorrect intents and entities.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 09/06/2018
ms.author: diberry
ms.openlocfilehash: e5820b7d65cb989411657670ae19ef1bdca2122d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869297"
---
# <a name="batch-testing-with-a-set-of-example-utterances"></a><span data-ttu-id="9a0c4-103">Batch testing with a set of example utterances</span><span class="sxs-lookup"><span data-stu-id="9a0c4-103">Batch testing with a set of example utterances</span></span>
 <span data-ttu-id="9a0c4-104">Batch testing is a comprehensive test on your current trained model to measure its performance in LUIS.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-104">Batch testing is a comprehensive test on your current trained model to measure its performance in LUIS.</span></span> 

<a name="batch-testing"></a>
## <a name="import-a-dataset-file-for-batch-testing"></a><span data-ttu-id="9a0c4-105">Import a dataset file for batch testing</span><span class="sxs-lookup"><span data-stu-id="9a0c4-105">Import a dataset file for batch testing</span></span>

1. <span data-ttu-id="9a0c4-106">Select **Test** in the top bar, and then select **Batch testing panel**.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-106">Select **Test** in the top bar, and then select **Batch testing panel**.</span></span>

    ![Batch Testing Link](./media/luis-how-to-batch-test/batch-testing-link.png)

2. <span data-ttu-id="9a0c4-108">Select **Import dataset**.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-108">Select **Import dataset**.</span></span> <span data-ttu-id="9a0c4-109">The **Import new dataset** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-109">The **Import new dataset** dialog box appears.</span></span> <span data-ttu-id="9a0c4-110">Select **Choose File** and locate a JSON file with the correct [JSON format](luis-concept-batch-test.md#batch-file-format) that contains *no more than 1,000* utterances to test.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-110">Select **Choose File** and locate a JSON file with the correct [JSON format](luis-concept-batch-test.md#batch-file-format) that contains *no more than 1,000* utterances to test.</span></span>

    <span data-ttu-id="9a0c4-111">Import errors are reported in a red notification bar at the top of the browser.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-111">Import errors are reported in a red notification bar at the top of the browser.</span></span> <span data-ttu-id="9a0c4-112">When an import has errors, no dataset is created.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-112">When an import has errors, no dataset is created.</span></span> <span data-ttu-id="9a0c4-113">For more information, see [Common errors](luis-concept-batch-test.md#common-errors-importing-a-batch).</span><span class="sxs-lookup"><span data-stu-id="9a0c4-113">For more information, see [Common errors](luis-concept-batch-test.md#common-errors-importing-a-batch).</span></span>

3. <span data-ttu-id="9a0c4-114">In the **Dataset Name** field, enter a name for your dataset file.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-114">In the **Dataset Name** field, enter a name for your dataset file.</span></span> <span data-ttu-id="9a0c4-115">The dataset file includes an **array of utterances** including the *labeled intent* and *entities*.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-115">The dataset file includes an **array of utterances** including the *labeled intent* and *entities*.</span></span> <span data-ttu-id="9a0c4-116">Review the [example batch file](luis-concept-batch-test.md#batch-file-format) for syntax.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-116">Review the [example batch file](luis-concept-batch-test.md#batch-file-format) for syntax.</span></span> 

4. <span data-ttu-id="9a0c4-117">Select **Done**.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-117">Select **Done**.</span></span> <span data-ttu-id="9a0c4-118">The dataset file is added.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-118">The dataset file is added.</span></span>

## <a name="run-rename-export-or-delete-dataset"></a><span data-ttu-id="9a0c4-119">Run, rename, export, or delete dataset</span><span class="sxs-lookup"><span data-stu-id="9a0c4-119">Run, rename, export, or delete dataset</span></span>
<span data-ttu-id="9a0c4-120">To run, rename, export, or delete the dataset, use the ellipsis (***...***) button at the end of the dataset row.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-120">To run, rename, export, or delete the dataset, use the ellipsis (***...***) button at the end of the dataset row.</span></span>

![Dataset Actions](./media/luis-how-to-batch-test/batch-testing-options.png)

## <a name="run-a-batch-test-on-your-trained-app"></a><span data-ttu-id="9a0c4-122">Run a batch test on your trained app</span><span class="sxs-lookup"><span data-stu-id="9a0c4-122">Run a batch test on your trained app</span></span>

<span data-ttu-id="9a0c4-123">To run the test, select the dataset name.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-123">To run the test, select the dataset name.</span></span> <span data-ttu-id="9a0c4-124">When the test completes, this row displays the test result of the dataset.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-124">When the test completes, this row displays the test result of the dataset.</span></span>

![Batch Test Result](./media/luis-how-to-batch-test/run-test.png)

<span data-ttu-id="9a0c4-126">The downloadable dataset is the same file that was uploaded for batch testing.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-126">The downloadable dataset is the same file that was uploaded for batch testing.</span></span>

|<span data-ttu-id="9a0c4-127">State</span><span class="sxs-lookup"><span data-stu-id="9a0c4-127">State</span></span>|<span data-ttu-id="9a0c4-128">Meaning</span><span class="sxs-lookup"><span data-stu-id="9a0c4-128">Meaning</span></span>|
|--|--|
|![Successful test green circle icon](./media/luis-how-to-batch-test/batch-test-result-green.png)|<span data-ttu-id="9a0c4-130">All utterances are successful.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-130">All utterances are successful.</span></span>|
|![Failing test red x icon](./media/luis-how-to-batch-test/batch-test-result-red.png)|<span data-ttu-id="9a0c4-132">At least one utterance intent did not match the prediction.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-132">At least one utterance intent did not match the prediction.</span></span>|
|![Ready to test icon](./media/luis-how-to-batch-test/batch-test-result-blue.png)|<span data-ttu-id="9a0c4-134">Test is ready to run.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-134">Test is ready to run.</span></span>|

<a name="access-batch-test-result-details-in-a-visualized-view"></a>
## <a name="view-batch-test-results"></a><span data-ttu-id="9a0c4-135">View batch test results</span><span class="sxs-lookup"><span data-stu-id="9a0c4-135">View batch test results</span></span> 
<span data-ttu-id="9a0c4-136">To review the batch test results, select **See results**.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-136">To review the batch test results, select **See results**.</span></span>

![Batch test results](./media/luis-how-to-batch-test/run-test-results.png)

<!-- Select the **See results** link that appears after you run the test. A scatter graph known as an error matrix displays. The data points represent the utterances in the dataset. Green points indicate correct prediction, and red ones indicate incorrect prediction. The filtering panel on the right side of the screen displays a list of all intents and entities in the app, with a green point for intents/entities that were predicted correctly in all dataset utterances, and a red point for those items with errors. Also, for each intent/entity, you can see the number of correct predictions out of the total utterances.-->


<a name="filter-chart-results-by-intent-or-entity"></a>  
## <a name="filter-chart-results"></a><span data-ttu-id="9a0c4-138">Filter chart results</span><span class="sxs-lookup"><span data-stu-id="9a0c4-138">Filter chart results</span></span>

<span data-ttu-id="9a0c4-139">To filter the chart by a specific intent or entity, select the intent or entity in the right-side filtering panel.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-139">To filter the chart by a specific intent or entity, select the intent or entity in the right-side filtering panel.</span></span> <span data-ttu-id="9a0c4-140">The data points and their distribution update in the graph according to your selection.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-140">The data points and their distribution update in the graph according to your selection.</span></span> 
 
![Visualized Batch Test Result](./media/luis-how-to-batch-test/filter-by-entity.png) 

## <a name="view-single-point-utterance-data"></a><span data-ttu-id="9a0c4-142">View single-point utterance data</span><span class="sxs-lookup"><span data-stu-id="9a0c4-142">View single-point utterance data</span></span>
<span data-ttu-id="9a0c4-143">In the chart, hover over a data point to see the certainty score of its prediction.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-143">In the chart, hover over a data point to see the certainty score of its prediction.</span></span> <span data-ttu-id="9a0c4-144">Select a data point to retrieve its corresponding utterance in the utterances list at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-144">Select a data point to retrieve its corresponding utterance in the utterances list at the bottom of the page.</span></span> 

![Selected utterance](./media/luis-how-to-batch-test/selected-utterance.png)


<a name="relabel-utterances-and-retrain"></a>
<a name="false-test-results"></a>
## <a name="view-section-data"></a><span data-ttu-id="9a0c4-146">View section data</span><span class="sxs-lookup"><span data-stu-id="9a0c4-146">View section data</span></span>
<span data-ttu-id="9a0c4-147">In the four-section chart, select the section name, such as **False Positive** at the top-right of the chart.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-147">In the four-section chart, select the section name, such as **False Positive** at the top-right of the chart.</span></span> <span data-ttu-id="9a0c4-148">Below the chart, all utterances in that section display below the chart in a list.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-148">Below the chart, all utterances in that section display below the chart in a list.</span></span> 

![Selected utterances by section](./media/luis-how-to-batch-test/selected-utterances-by-section.png)

<span data-ttu-id="9a0c4-150">In this preceding image, the utterance `switch on` is labeled with the TurnAllOn intent, but received the prediction of None intent.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-150">In this preceding image, the utterance `switch on` is labeled with the TurnAllOn intent, but received the prediction of None intent.</span></span> <span data-ttu-id="9a0c4-151">This is an indication that the TurnAllOn intent needs more example utterances in order to make the expected prediction.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-151">This is an indication that the TurnAllOn intent needs more example utterances in order to make the expected prediction.</span></span> 

<span data-ttu-id="9a0c4-152">The two sections of the chart in red indicate utterances that did not match the expected prediction.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-152">The two sections of the chart in red indicate utterances that did not match the expected prediction.</span></span> <span data-ttu-id="9a0c4-153">These indicate utterances which LUIS needs more training.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-153">These indicate utterances which LUIS needs more training.</span></span> 

<span data-ttu-id="9a0c4-154">The two sections of the chart in green did match the expected prediction.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-154">The two sections of the chart in green did match the expected prediction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a0c4-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a0c4-155">Next steps</span></span>

<span data-ttu-id="9a0c4-156">If testing indicates that your LUIS app doesn't recognize the correct intents and entities, you can work to improve your LUIS app's performance by labeling more utterances or adding features.</span><span class="sxs-lookup"><span data-stu-id="9a0c4-156">If testing indicates that your LUIS app doesn't recognize the correct intents and entities, you can work to improve your LUIS app's performance by labeling more utterances or adding features.</span></span> 

* [<span data-ttu-id="9a0c4-157">Label suggested utterances with LUIS</span><span class="sxs-lookup"><span data-stu-id="9a0c4-157">Label suggested utterances with LUIS</span></span>](luis-how-to-review-endoint-utt.md) 
* [<span data-ttu-id="9a0c4-158">Use features to improve your LUIS app's performance</span><span class="sxs-lookup"><span data-stu-id="9a0c4-158">Use features to improve your LUIS app's performance</span></span>](luis-how-to-add-features.md) 
* [<span data-ttu-id="9a0c4-159">Understand batch testing with this tutorial</span><span class="sxs-lookup"><span data-stu-id="9a0c4-159">Understand batch testing with this tutorial</span></span>](luis-tutorial-batch-testing.md)
* <span data-ttu-id="9a0c4-160">[Learn batch testing concepts](luis-concept-batch-test.md).</span><span class="sxs-lookup"><span data-stu-id="9a0c4-160">[Learn batch testing concepts](luis-concept-batch-test.md).</span></span>
