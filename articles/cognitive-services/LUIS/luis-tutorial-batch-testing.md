---
title: Use batch testing to improve LUIS predictions  | Microsoft Docs
titleSuffix: Azure
description: Load batch test, review results, and improve LUIS predictions with changes.
services: cognitive-services
author: diberry
manager: cjgronlund
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: article
ms.date: 08/02/2018
ms.author: diberry
ms.openlocfilehash: 5abaeaee87d54e82df29e75b89c83522b8746730
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968782"
---
# <a name="improve-app-with-batch-test"></a><span data-ttu-id="eace7-103">Improve app with batch test</span><span class="sxs-lookup"><span data-stu-id="eace7-103">Improve app with batch test</span></span>

<span data-ttu-id="eace7-104">This tutorial demonstrates how to use batch testing to find utterance prediction issues.</span><span class="sxs-lookup"><span data-stu-id="eace7-104">This tutorial demonstrates how to use batch testing to find utterance prediction issues.</span></span>  

<span data-ttu-id="eace7-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="eace7-105">In this tutorial, you learn how to:</span></span>

<!-- green checkmark -->
> [!div class="checklist"]
* <span data-ttu-id="eace7-106">Create a batch test file</span><span class="sxs-lookup"><span data-stu-id="eace7-106">Create a batch test file</span></span> 
* <span data-ttu-id="eace7-107">Run a batch test</span><span class="sxs-lookup"><span data-stu-id="eace7-107">Run a batch test</span></span>
* <span data-ttu-id="eace7-108">Review test results</span><span class="sxs-lookup"><span data-stu-id="eace7-108">Review test results</span></span>
* <span data-ttu-id="eace7-109">Fix errors</span><span class="sxs-lookup"><span data-stu-id="eace7-109">Fix errors</span></span> 
* <span data-ttu-id="eace7-110">Retest the batch</span><span class="sxs-lookup"><span data-stu-id="eace7-110">Retest the batch</span></span>

[!INCLUDE [LUIS Free account](../../../includes/cognitive-services-luis-free-key-short.md)]

## <a name="before-you-begin"></a><span data-ttu-id="eace7-111">Before you begin</span><span class="sxs-lookup"><span data-stu-id="eace7-111">Before you begin</span></span>

<span data-ttu-id="eace7-112">If you don't have the Human Resources app from the [review endpoint utterances](luis-tutorial-review-endpoint-utterances.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span><span class="sxs-lookup"><span data-stu-id="eace7-112">If you don't have the Human Resources app from the [review endpoint utterances](luis-tutorial-review-endpoint-utterances.md) tutorial, [import](luis-how-to-start-new-app.md#import-new-app) the JSON into a new app in the [LUIS](luis-reference-regions.md#luis-website) website.</span></span> <span data-ttu-id="eace7-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-review-HumanResources.json) Github repository.</span><span class="sxs-lookup"><span data-stu-id="eace7-113">The app to import is found in the [LUIS-Samples](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/quickstarts/custom-domain-review-HumanResources.json) Github repository.</span></span>

<span data-ttu-id="eace7-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `batchtest`.</span><span class="sxs-lookup"><span data-stu-id="eace7-114">If you want to keep the original Human Resources app, clone the version on the [Settings](luis-how-to-manage-versions.md#clone-a-version) page, and name it `batchtest`.</span></span> <span data-ttu-id="eace7-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span><span class="sxs-lookup"><span data-stu-id="eace7-115">Cloning is a great way to play with various LUIS features without affecting the original version.</span></span> 

<span data-ttu-id="eace7-116">Train the app.</span><span class="sxs-lookup"><span data-stu-id="eace7-116">Train the app.</span></span>

## <a name="purpose-of-batch-testing"></a><span data-ttu-id="eace7-117">Purpose of batch testing</span><span class="sxs-lookup"><span data-stu-id="eace7-117">Purpose of batch testing</span></span>

<span data-ttu-id="eace7-118">Batch testing allows you to validate the active, trained model's state with a known set of labeled utterances and entities.</span><span class="sxs-lookup"><span data-stu-id="eace7-118">Batch testing allows you to validate the active, trained model's state with a known set of labeled utterances and entities.</span></span> <span data-ttu-id="eace7-119">In the JSON-formatted batch file, add the utterances and set the entity labels you need predicted inside the utterance.</span><span class="sxs-lookup"><span data-stu-id="eace7-119">In the JSON-formatted batch file, add the utterances and set the entity labels you need predicted inside the utterance.</span></span> 

<span data-ttu-id="eace7-120"><!--The recommended test strategy for LUIS uses three separate sets of data: example utterances provided to the model, batch test utterances, and endpoint utterances. --> When using an app other than this tutorial, make sure you are *not* using the example utterances already added to an intent.</span><span class="sxs-lookup"><span data-stu-id="eace7-120"><!--The recommended test strategy for LUIS uses three separate sets of data: example utterances provided to the model, batch test utterances, and endpoint utterances. --> When using an app other than this tutorial, make sure you are *not* using the example utterances already added to an intent.</span></span> <span data-ttu-id="eace7-121">To verify your batch test utterances against the example utterances, [export](luis-how-to-start-new-app.md#export-app) the app.</span><span class="sxs-lookup"><span data-stu-id="eace7-121">To verify your batch test utterances against the example utterances, [export](luis-how-to-start-new-app.md#export-app) the app.</span></span> <span data-ttu-id="eace7-122">Compare the app example utterance's to the batch test utterances.</span><span class="sxs-lookup"><span data-stu-id="eace7-122">Compare the app example utterance's to the batch test utterances.</span></span> 

<span data-ttu-id="eace7-123">Requirements for batch testing:</span><span class="sxs-lookup"><span data-stu-id="eace7-123">Requirements for batch testing:</span></span>

* <span data-ttu-id="eace7-124">Maximum of 1000 utterances per test.</span><span class="sxs-lookup"><span data-stu-id="eace7-124">Maximum of 1000 utterances per test.</span></span> 
* <span data-ttu-id="eace7-125">No duplicates.</span><span class="sxs-lookup"><span data-stu-id="eace7-125">No duplicates.</span></span> 
* <span data-ttu-id="eace7-126">Entity types allowed: only machined-learned entities of simple, hierarchical (parent-only), and composite.</span><span class="sxs-lookup"><span data-stu-id="eace7-126">Entity types allowed: only machined-learned entities of simple, hierarchical (parent-only), and composite.</span></span> <span data-ttu-id="eace7-127">Batch testing is only useful for machined-learned intents and entities.</span><span class="sxs-lookup"><span data-stu-id="eace7-127">Batch testing is only useful for machined-learned intents and entities.</span></span>

## <a name="create-a-batch-file-with-utterances"></a><span data-ttu-id="eace7-128">Create a batch file with utterances</span><span class="sxs-lookup"><span data-stu-id="eace7-128">Create a batch file with utterances</span></span>

1. <span data-ttu-id="eace7-129">Create `HumanResources-jobs-batch.json` in a text editor such as [VSCode](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="eace7-129">Create `HumanResources-jobs-batch.json` in a text editor such as [VSCode](https://code.visualstudio.com/).</span></span> 

2. <span data-ttu-id="eace7-130">In the JSON-formatted batch file, add utterances with the **Intent** you want predicted in the test.</span><span class="sxs-lookup"><span data-stu-id="eace7-130">In the JSON-formatted batch file, add utterances with the **Intent** you want predicted in the test.</span></span> 

   [!code-json[Add the intents to the batch test file](~/samples-luis/documentation-samples/tutorial-batch-testing/HumanResources-jobs-batch.json "Add the intents to the batch test file")]

## <a name="run-the-batch"></a><span data-ttu-id="eace7-131">Run the batch</span><span class="sxs-lookup"><span data-stu-id="eace7-131">Run the batch</span></span>

1. <span data-ttu-id="eace7-132">Select **Test** in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="eace7-132">Select **Test** in the top navigation bar.</span></span> 

2. <span data-ttu-id="eace7-133">Select **Batch testing panel** in the right-side panel.</span><span class="sxs-lookup"><span data-stu-id="eace7-133">Select **Batch testing panel** in the right-side panel.</span></span> 

    <span data-ttu-id="eace7-134">[![Screenshot of LUIS app with Batch test panel highlighted](./media/luis-tutorial-batch-testing/hr-batch-testing-panel-link.png)](./media/luis-tutorial-batch-testing/hr-batch-testing-panel-link.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="eace7-134">[![Screenshot of LUIS app with Batch test panel highlighted](./media/luis-tutorial-batch-testing/hr-batch-testing-panel-link.png)](./media/luis-tutorial-batch-testing/hr-batch-testing-panel-link.png#lightbox)</span></span>

3. <span data-ttu-id="eace7-135">Select **Import dataset**.</span><span class="sxs-lookup"><span data-stu-id="eace7-135">Select **Import dataset**.</span></span>

    <span data-ttu-id="eace7-136">[![Screenshot of LUIS app with Import dataset highlighted](./media/luis-tutorial-batch-testing/hr-import-dataset-button.png)](./media/luis-tutorial-batch-testing/hr-import-dataset-button.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="eace7-136">[![Screenshot of LUIS app with Import dataset highlighted](./media/luis-tutorial-batch-testing/hr-import-dataset-button.png)](./media/luis-tutorial-batch-testing/hr-import-dataset-button.png#lightbox)</span></span>

4. <span data-ttu-id="eace7-137">Choose the file system location of the `HumanResources-jobs-batch.json` file.</span><span class="sxs-lookup"><span data-stu-id="eace7-137">Choose the file system location of the `HumanResources-jobs-batch.json` file.</span></span>

5. <span data-ttu-id="eace7-138">Name the dataset `intents only` and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="eace7-138">Name the dataset `intents only` and select **Done**.</span></span>

    ![Select file](./media/luis-tutorial-batch-testing/hr-import-new-dataset-ddl.png)

6. <span data-ttu-id="eace7-140">Select the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="eace7-140">Select the **Run** button.</span></span> <span data-ttu-id="eace7-141">Wait until the test is done.</span><span class="sxs-lookup"><span data-stu-id="eace7-141">Wait until the test is done.</span></span>

7. <span data-ttu-id="eace7-142">Select **See results**.</span><span class="sxs-lookup"><span data-stu-id="eace7-142">Select **See results**.</span></span>

8. <span data-ttu-id="eace7-143">Review results in the graph and legend.</span><span class="sxs-lookup"><span data-stu-id="eace7-143">Review results in the graph and legend.</span></span>

    <span data-ttu-id="eace7-144">[![Screenshot of LUIS app with batch test results](./media/luis-tutorial-batch-testing/hr-intents-only-results-1.png)](./media/luis-tutorial-batch-testing/hr-intents-only-results-1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="eace7-144">[![Screenshot of LUIS app with batch test results](./media/luis-tutorial-batch-testing/hr-intents-only-results-1.png)](./media/luis-tutorial-batch-testing/hr-intents-only-results-1.png#lightbox)</span></span>

## <a name="review-batch-results"></a><span data-ttu-id="eace7-145">Review batch results</span><span class="sxs-lookup"><span data-stu-id="eace7-145">Review batch results</span></span>

<span data-ttu-id="eace7-146">The batch chart displays four quadrants of results.</span><span class="sxs-lookup"><span data-stu-id="eace7-146">The batch chart displays four quadrants of results.</span></span> <span data-ttu-id="eace7-147">To the right of the chart is a filter.</span><span class="sxs-lookup"><span data-stu-id="eace7-147">To the right of the chart is a filter.</span></span> <span data-ttu-id="eace7-148">By default, the filter is set to the first intent in the list.</span><span class="sxs-lookup"><span data-stu-id="eace7-148">By default, the filter is set to the first intent in the list.</span></span> <span data-ttu-id="eace7-149">The filter contains all the intents and only simple, hierarchical (parent-only), and composite entities.</span><span class="sxs-lookup"><span data-stu-id="eace7-149">The filter contains all the intents and only simple, hierarchical (parent-only), and composite entities.</span></span> <span data-ttu-id="eace7-150">When you select a [section of the chart](luis-concept-batch-test.md#batch-test-results) or a point within the chart, the associated utterance(s) display below the chart.</span><span class="sxs-lookup"><span data-stu-id="eace7-150">When you select a [section of the chart](luis-concept-batch-test.md#batch-test-results) or a point within the chart, the associated utterance(s) display below the chart.</span></span> 

<span data-ttu-id="eace7-151">While hovering over the chart, a mouse wheel can enlarge or reduce the display in the chart.</span><span class="sxs-lookup"><span data-stu-id="eace7-151">While hovering over the chart, a mouse wheel can enlarge or reduce the display in the chart.</span></span> <span data-ttu-id="eace7-152">This is useful when there are many points on the chart clustered tightly together.</span><span class="sxs-lookup"><span data-stu-id="eace7-152">This is useful when there are many points on the chart clustered tightly together.</span></span> 

<span data-ttu-id="eace7-153">The chart is in four quadrants, with two of the sections displayed in red.</span><span class="sxs-lookup"><span data-stu-id="eace7-153">The chart is in four quadrants, with two of the sections displayed in red.</span></span> <span data-ttu-id="eace7-154">**These are the sections to focus on**.</span><span class="sxs-lookup"><span data-stu-id="eace7-154">**These are the sections to focus on**.</span></span> 

### <a name="getjobinformation-test-results"></a><span data-ttu-id="eace7-155">GetJobInformation test results</span><span class="sxs-lookup"><span data-stu-id="eace7-155">GetJobInformation test results</span></span>

<span data-ttu-id="eace7-156">The **GetJobInformation** test results displayed in the filter show that 2 of the four predictions were successful.</span><span class="sxs-lookup"><span data-stu-id="eace7-156">The **GetJobInformation** test results displayed in the filter show that 2 of the four predictions were successful.</span></span> <span data-ttu-id="eace7-157">Select the name **False positive** above the top right quadrant to see the utterances below the chart.</span><span class="sxs-lookup"><span data-stu-id="eace7-157">Select the name **False positive** above the top right quadrant to see the utterances below the chart.</span></span> 

![LUIS batch test utterances](./media/luis-tutorial-batch-testing/hr-applyforjobs-false-positive-results.png)

<span data-ttu-id="eace7-159">Why are two of the utterances predicted as **ApplyForJob**, instead of the correct intent **GetJobInformation**?</span><span class="sxs-lookup"><span data-stu-id="eace7-159">Why are two of the utterances predicted as **ApplyForJob**, instead of the correct intent **GetJobInformation**?</span></span> <span data-ttu-id="eace7-160">The two intents are very closely related in terms of word choice and word arrangement.</span><span class="sxs-lookup"><span data-stu-id="eace7-160">The two intents are very closely related in terms of word choice and word arrangement.</span></span> <span data-ttu-id="eace7-161">Additionally, there are almost three times as many examples for **ApplyForJob** than **GetJobInformation**.</span><span class="sxs-lookup"><span data-stu-id="eace7-161">Additionally, there are almost three times as many examples for **ApplyForJob** than **GetJobInformation**.</span></span> <span data-ttu-id="eace7-162">This unevenness of example utterances weighs in **ApplyForJob** intent's favor.</span><span class="sxs-lookup"><span data-stu-id="eace7-162">This unevenness of example utterances weighs in **ApplyForJob** intent's favor.</span></span> 

<span data-ttu-id="eace7-163">Notice that both intents have the same count of errors.</span><span class="sxs-lookup"><span data-stu-id="eace7-163">Notice that both intents have the same count of errors.</span></span> <span data-ttu-id="eace7-164">An incorrect prediction in one intent affects the other intent as well.</span><span class="sxs-lookup"><span data-stu-id="eace7-164">An incorrect prediction in one intent affects the other intent as well.</span></span> <span data-ttu-id="eace7-165">They both have errors because the utterances were incorrectly predicted for one intent, and also incorrectly not predicted for another intent.</span><span class="sxs-lookup"><span data-stu-id="eace7-165">They both have errors because the utterances were incorrectly predicted for one intent, and also incorrectly not predicted for another intent.</span></span> 

![LUIS batch test filter errors](./media/luis-tutorial-batch-testing/hr-intent-error-count.png)

<span data-ttu-id="eace7-167">The utterances corresponding the top point in the **False positive** section are `Can I apply for any database jobs with this resume?` and `Can I apply for any database jobs with this resume?`.</span><span class="sxs-lookup"><span data-stu-id="eace7-167">The utterances corresponding the top point in the **False positive** section are `Can I apply for any database jobs with this resume?` and `Can I apply for any database jobs with this resume?`.</span></span> <span data-ttu-id="eace7-168">For the first utterance, the word `resume` has only been used in **ApplyForJob**.</span><span class="sxs-lookup"><span data-stu-id="eace7-168">For the first utterance, the word `resume` has only been used in **ApplyForJob**.</span></span> <span data-ttu-id="eace7-169">For the second utterance, the word `apply` has only been used in the **ApplyForJob** intent.</span><span class="sxs-lookup"><span data-stu-id="eace7-169">For the second utterance, the word `apply` has only been used in the **ApplyForJob** intent.</span></span>

## <a name="fix-the-app-based-on-batch-results"></a><span data-ttu-id="eace7-170">Fix the app based on batch results</span><span class="sxs-lookup"><span data-stu-id="eace7-170">Fix the app based on batch results</span></span>

<span data-ttu-id="eace7-171">The goal of this section is to have all the utterances correctly predicted for **GetJobInformation** by fixing the app.</span><span class="sxs-lookup"><span data-stu-id="eace7-171">The goal of this section is to have all the utterances correctly predicted for **GetJobInformation** by fixing the app.</span></span> 

<span data-ttu-id="eace7-172">A seemingly quick fix would be to add these batch file utterances to the correct intent.</span><span class="sxs-lookup"><span data-stu-id="eace7-172">A seemingly quick fix would be to add these batch file utterances to the correct intent.</span></span> <span data-ttu-id="eace7-173">That is not what you want to do though.</span><span class="sxs-lookup"><span data-stu-id="eace7-173">That is not what you want to do though.</span></span> <span data-ttu-id="eace7-174">You want LUIS to correctly predict these utterances without adding them as examples.</span><span class="sxs-lookup"><span data-stu-id="eace7-174">You want LUIS to correctly predict these utterances without adding them as examples.</span></span> 

<span data-ttu-id="eace7-175">You might also wonder about removing utterances from **ApplyForJob** until the utterance quantity is the same as **GetJobInformation**.</span><span class="sxs-lookup"><span data-stu-id="eace7-175">You might also wonder about removing utterances from **ApplyForJob** until the utterance quantity is the same as **GetJobInformation**.</span></span> <span data-ttu-id="eace7-176">That may fix the test results but would hinder LUIS from predicting that intent accurately next time.</span><span class="sxs-lookup"><span data-stu-id="eace7-176">That may fix the test results but would hinder LUIS from predicting that intent accurately next time.</span></span> 

<span data-ttu-id="eace7-177">The first fix is to add more utterances to **GetJobInformation**.</span><span class="sxs-lookup"><span data-stu-id="eace7-177">The first fix is to add more utterances to **GetJobInformation**.</span></span> <span data-ttu-id="eace7-178">The second fix is to reduce the weight of words like `resume` and `apply` toward the **ApplyForJob** intent.</span><span class="sxs-lookup"><span data-stu-id="eace7-178">The second fix is to reduce the weight of words like `resume` and `apply` toward the **ApplyForJob** intent.</span></span> 

### <a name="add-more-utterances-to-getjobinformation"></a><span data-ttu-id="eace7-179">Add more utterances to **GetJobInformation**</span><span class="sxs-lookup"><span data-stu-id="eace7-179">Add more utterances to **GetJobInformation**</span></span>

1. <span data-ttu-id="eace7-180">Close the batch test panel by selecting the **Test** button in the top navigation panel.</span><span class="sxs-lookup"><span data-stu-id="eace7-180">Close the batch test panel by selecting the **Test** button in the top navigation panel.</span></span> 

2. <span data-ttu-id="eace7-181">Select **GetJobInformation** from the intents list.</span><span class="sxs-lookup"><span data-stu-id="eace7-181">Select **GetJobInformation** from the intents list.</span></span> 

3. <span data-ttu-id="eace7-182">Add more utterances that are varied for length, word choice, and word arrangement, making sure to include the terms `resume`, `c.v.`, and `apply`:</span><span class="sxs-lookup"><span data-stu-id="eace7-182">Add more utterances that are varied for length, word choice, and word arrangement, making sure to include the terms `resume`, `c.v.`, and `apply`:</span></span>

    |<span data-ttu-id="eace7-183">Example utterances for **GetJobInformation** intent</span><span class="sxs-lookup"><span data-stu-id="eace7-183">Example utterances for **GetJobInformation** intent</span></span>|
    |--|
    |<span data-ttu-id="eace7-184">Does the new job in the warehouse for a stocker require that I apply with a resume?</span><span class="sxs-lookup"><span data-stu-id="eace7-184">Does the new job in the warehouse for a stocker require that I apply with a resume?</span></span>|
    |<span data-ttu-id="eace7-185">Where are the roofing jobs today?</span><span class="sxs-lookup"><span data-stu-id="eace7-185">Where are the roofing jobs today?</span></span>|
    |<span data-ttu-id="eace7-186">I heard there was a medical coding job that requires a resume.</span><span class="sxs-lookup"><span data-stu-id="eace7-186">I heard there was a medical coding job that requires a resume.</span></span>|
    |<span data-ttu-id="eace7-187">I would like a job helping college kids write their c.v.s.</span><span class="sxs-lookup"><span data-stu-id="eace7-187">I would like a job helping college kids write their c.v.s.</span></span> |
    |<span data-ttu-id="eace7-188">Here is my resume, looking for a new post at the community college using computers.</span><span class="sxs-lookup"><span data-stu-id="eace7-188">Here is my resume, looking for a new post at the community college using computers.</span></span>|
    |<span data-ttu-id="eace7-189">What positions are available in child and home care?</span><span class="sxs-lookup"><span data-stu-id="eace7-189">What positions are available in child and home care?</span></span>|
    |<span data-ttu-id="eace7-190">Is there an intern desk at the newspaper?</span><span class="sxs-lookup"><span data-stu-id="eace7-190">Is there an intern desk at the newspaper?</span></span>|
    |<span data-ttu-id="eace7-191">My C.v.</span><span class="sxs-lookup"><span data-stu-id="eace7-191">My C.v.</span></span> <span data-ttu-id="eace7-192">shows I'm good at analyzing procurement, budgets, and lost money.</span><span class="sxs-lookup"><span data-stu-id="eace7-192">shows I'm good at analyzing procurement, budgets, and lost money.</span></span> <span data-ttu-id="eace7-193">Is there anything for this type of work?</span><span class="sxs-lookup"><span data-stu-id="eace7-193">Is there anything for this type of work?</span></span>|
    |<span data-ttu-id="eace7-194">Where are the earth drilling jobs right now?</span><span class="sxs-lookup"><span data-stu-id="eace7-194">Where are the earth drilling jobs right now?</span></span>|
    |<span data-ttu-id="eace7-195">I've worked 8 years as an EMS driver.</span><span class="sxs-lookup"><span data-stu-id="eace7-195">I've worked 8 years as an EMS driver.</span></span> <span data-ttu-id="eace7-196">Any new jobs?</span><span class="sxs-lookup"><span data-stu-id="eace7-196">Any new jobs?</span></span>|
    |<span data-ttu-id="eace7-197">New food handling jobs require application?</span><span class="sxs-lookup"><span data-stu-id="eace7-197">New food handling jobs require application?</span></span>|
    |<span data-ttu-id="eace7-198">How many new yard work jobs are available?</span><span class="sxs-lookup"><span data-stu-id="eace7-198">How many new yard work jobs are available?</span></span>|
    |<span data-ttu-id="eace7-199">Is there a new HR post for labor relations and negotiations?</span><span class="sxs-lookup"><span data-stu-id="eace7-199">Is there a new HR post for labor relations and negotiations?</span></span>|
    |<span data-ttu-id="eace7-200">I have a masters in library and archive management.</span><span class="sxs-lookup"><span data-stu-id="eace7-200">I have a masters in library and archive management.</span></span> <span data-ttu-id="eace7-201">Any new positions?</span><span class="sxs-lookup"><span data-stu-id="eace7-201">Any new positions?</span></span>|
    |<span data-ttu-id="eace7-202">Are there any babysitting jobs for 13 year olds in the city today?</span><span class="sxs-lookup"><span data-stu-id="eace7-202">Are there any babysitting jobs for 13 year olds in the city today?</span></span>|

    <span data-ttu-id="eace7-203">Do not label the **Job** entity in the utterances.</span><span class="sxs-lookup"><span data-stu-id="eace7-203">Do not label the **Job** entity in the utterances.</span></span> <span data-ttu-id="eace7-204">This section of the tutorial is focused on intent prediction only.</span><span class="sxs-lookup"><span data-stu-id="eace7-204">This section of the tutorial is focused on intent prediction only.</span></span>

4. <span data-ttu-id="eace7-205">Train the app by selecting **Train** in the top right navigation.</span><span class="sxs-lookup"><span data-stu-id="eace7-205">Train the app by selecting **Train** in the top right navigation.</span></span>

## <a name="verify-the-fix-worked"></a><span data-ttu-id="eace7-206">Verify the fix worked</span><span class="sxs-lookup"><span data-stu-id="eace7-206">Verify the fix worked</span></span>

<span data-ttu-id="eace7-207">In order to verify that the utterances in the batch test are correctly predicted, run the batch test again.</span><span class="sxs-lookup"><span data-stu-id="eace7-207">In order to verify that the utterances in the batch test are correctly predicted, run the batch test again.</span></span>

1. <span data-ttu-id="eace7-208">Select **Test** in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="eace7-208">Select **Test** in the top navigation bar.</span></span> <span data-ttu-id="eace7-209">If the batch results are still open, select **Back to list**.</span><span class="sxs-lookup"><span data-stu-id="eace7-209">If the batch results are still open, select **Back to list**.</span></span>  

2. <span data-ttu-id="eace7-210">Select the ellipsis (***...***) button to the right of the batch name and select **Run Dataset**.</span><span class="sxs-lookup"><span data-stu-id="eace7-210">Select the ellipsis (***...***) button to the right of the batch name and select **Run Dataset**.</span></span> <span data-ttu-id="eace7-211">Wait until the batch test is done.</span><span class="sxs-lookup"><span data-stu-id="eace7-211">Wait until the batch test is done.</span></span> <span data-ttu-id="eace7-212">Notice that the **See results** button is now green.</span><span class="sxs-lookup"><span data-stu-id="eace7-212">Notice that the **See results** button is now green.</span></span> <span data-ttu-id="eace7-213">This means the entire batch ran successfully.</span><span class="sxs-lookup"><span data-stu-id="eace7-213">This means the entire batch ran successfully.</span></span>

3. <span data-ttu-id="eace7-214">Select **See results**.</span><span class="sxs-lookup"><span data-stu-id="eace7-214">Select **See results**.</span></span> <span data-ttu-id="eace7-215">The intents should all have green icons to the left of the intent names.</span><span class="sxs-lookup"><span data-stu-id="eace7-215">The intents should all have green icons to the left of the intent names.</span></span> 

    ![Screenshot of LUIS with batch results button highlighted](./media/luis-tutorial-batch-testing/hr-batch-test-intents-no-errors.png)

## <a name="create-batch-file-with-entities"></a><span data-ttu-id="eace7-217">Create batch file with entities</span><span class="sxs-lookup"><span data-stu-id="eace7-217">Create batch file with entities</span></span> 

<span data-ttu-id="eace7-218">In order to verify entities in a batch test, the entities need to be labeled in the batch JSON file.</span><span class="sxs-lookup"><span data-stu-id="eace7-218">In order to verify entities in a batch test, the entities need to be labeled in the batch JSON file.</span></span> <span data-ttu-id="eace7-219">Only the machine-learned entities are used: simple, hierarchical (parent-only), and composite entities.</span><span class="sxs-lookup"><span data-stu-id="eace7-219">Only the machine-learned entities are used: simple, hierarchical (parent-only), and composite entities.</span></span> <span data-ttu-id="eace7-220">Do not add non-machine-learned entities because they are always found either through regular expressions, or explicit text matches.</span><span class="sxs-lookup"><span data-stu-id="eace7-220">Do not add non-machine-learned entities because they are always found either through regular expressions, or explicit text matches.</span></span>

<span data-ttu-id="eace7-221">The variation of entities for total word ([token](luis-glossary.md#token)) count can impact the prediction quality.</span><span class="sxs-lookup"><span data-stu-id="eace7-221">The variation of entities for total word ([token](luis-glossary.md#token)) count can impact the prediction quality.</span></span> <span data-ttu-id="eace7-222">Make sure the training data supplied to the intent with labeled utterances includes a variety of lengths of entity.</span><span class="sxs-lookup"><span data-stu-id="eace7-222">Make sure the training data supplied to the intent with labeled utterances includes a variety of lengths of entity.</span></span> 

<span data-ttu-id="eace7-223">When first writing and testing batch files, it is best to start with a few utterances and entities that you know work, as well as a few that you think may be incorrectly predicted.</span><span class="sxs-lookup"><span data-stu-id="eace7-223">When first writing and testing batch files, it is best to start with a few utterances and entities that you know work, as well as a few that you think may be incorrectly predicted.</span></span> <span data-ttu-id="eace7-224">This helps you focus in on the problem areas quickly.</span><span class="sxs-lookup"><span data-stu-id="eace7-224">This helps you focus in on the problem areas quickly.</span></span> <span data-ttu-id="eace7-225">After testing the **GetJobInformation** and **ApplyForJob** intents using several different Job names, which were not predicted, this batch test file was developed to see if there is a prediction problem with certain values for **Job** entity.</span><span class="sxs-lookup"><span data-stu-id="eace7-225">After testing the **GetJobInformation** and **ApplyForJob** intents using several different Job names, which were not predicted, this batch test file was developed to see if there is a prediction problem with certain values for **Job** entity.</span></span> 

<span data-ttu-id="eace7-226">The value of a **Job** entity, provided in the test utterances, is usually one or two words, with a few examples being more words.</span><span class="sxs-lookup"><span data-stu-id="eace7-226">The value of a **Job** entity, provided in the test utterances, is usually one or two words, with a few examples being more words.</span></span> <span data-ttu-id="eace7-227">If _your own_ human resources app typically has job names of many words, the example utterances labeled with **Job** entity in this app would not work well.</span><span class="sxs-lookup"><span data-stu-id="eace7-227">If _your own_ human resources app typically has job names of many words, the example utterances labeled with **Job** entity in this app would not work well.</span></span>

1. <span data-ttu-id="eace7-228">Create `HumanResources-entities-batch.json` in a text editor such as [VSCode](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="eace7-228">Create `HumanResources-entities-batch.json` in a text editor such as [VSCode](https://code.visualstudio.com/).</span></span> <span data-ttu-id="eace7-229">Or download [the file](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/tutorial-batch-testing/HumanResources-entities-batch.json) from the LUIS-Samples Github repository.</span><span class="sxs-lookup"><span data-stu-id="eace7-229">Or download [the file](https://github.com/Microsoft/LUIS-Samples/blob/master/documentation-samples/tutorial-batch-testing/HumanResources-entities-batch.json) from the LUIS-Samples Github repository.</span></span>


2. <span data-ttu-id="eace7-230">In the JSON-formatted batch file, add an array of objects that include utterances with the **Intent** you want predicted in the test as well as locations of any entities in the utterance.</span><span class="sxs-lookup"><span data-stu-id="eace7-230">In the JSON-formatted batch file, add an array of objects that include utterances with the **Intent** you want predicted in the test as well as locations of any entities in the utterance.</span></span> <span data-ttu-id="eace7-231">Since an entity is token-based, make sure to start and stop each entity on a character.</span><span class="sxs-lookup"><span data-stu-id="eace7-231">Since an entity is token-based, make sure to start and stop each entity on a character.</span></span> <span data-ttu-id="eace7-232">Do not begin or end the utterance on a space.</span><span class="sxs-lookup"><span data-stu-id="eace7-232">Do not begin or end the utterance on a space.</span></span> <span data-ttu-id="eace7-233">This causes an error during the batch file import.</span><span class="sxs-lookup"><span data-stu-id="eace7-233">This causes an error during the batch file import.</span></span>  

   [!code-json[Add the intents and entities to the batch test file](~/samples-luis/documentation-samples/tutorial-batch-testing/HumanResources-entities-batch.json "Add the intents and entities to the batch test file")]


## <a name="run-the-batch-with-entities"></a><span data-ttu-id="eace7-234">Run the batch with entities</span><span class="sxs-lookup"><span data-stu-id="eace7-234">Run the batch with entities</span></span>

1. <span data-ttu-id="eace7-235">Select **Test** in the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="eace7-235">Select **Test** in the top navigation bar.</span></span> 

2. <span data-ttu-id="eace7-236">Select **Batch testing panel** in the right-side panel.</span><span class="sxs-lookup"><span data-stu-id="eace7-236">Select **Batch testing panel** in the right-side panel.</span></span> 

3. <span data-ttu-id="eace7-237">Select **Import dataset**.</span><span class="sxs-lookup"><span data-stu-id="eace7-237">Select **Import dataset**.</span></span>

4. <span data-ttu-id="eace7-238">Choose the file system location of the `HumanResources-entities-batch.json` file.</span><span class="sxs-lookup"><span data-stu-id="eace7-238">Choose the file system location of the `HumanResources-entities-batch.json` file.</span></span>

5. <span data-ttu-id="eace7-239">Name the dataset `entities` and select **Done**.</span><span class="sxs-lookup"><span data-stu-id="eace7-239">Name the dataset `entities` and select **Done**.</span></span>

6. <span data-ttu-id="eace7-240">Select the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="eace7-240">Select the **Run** button.</span></span> <span data-ttu-id="eace7-241">Wait until the test is done.</span><span class="sxs-lookup"><span data-stu-id="eace7-241">Wait until the test is done.</span></span>

7. <span data-ttu-id="eace7-242">Select **See results**.</span><span class="sxs-lookup"><span data-stu-id="eace7-242">Select **See results**.</span></span>

## <a name="review-entity-batch-results"></a><span data-ttu-id="eace7-243">Review entity batch results</span><span class="sxs-lookup"><span data-stu-id="eace7-243">Review entity batch results</span></span>

<span data-ttu-id="eace7-244">The chart opens with all the intents correctly predicted.</span><span class="sxs-lookup"><span data-stu-id="eace7-244">The chart opens with all the intents correctly predicted.</span></span> <span data-ttu-id="eace7-245">Scroll down in the right-side filter to find the erroring entity predictions.</span><span class="sxs-lookup"><span data-stu-id="eace7-245">Scroll down in the right-side filter to find the erroring entity predictions.</span></span> 

1. <span data-ttu-id="eace7-246">Select the **Job** entity in the filter.</span><span class="sxs-lookup"><span data-stu-id="eace7-246">Select the **Job** entity in the filter.</span></span>

    ![Erroring entity predictions in filter](./media/luis-tutorial-batch-testing/hr-entities-filter-errors.png)

    <span data-ttu-id="eace7-248">The chart changes to display the entity predictions.</span><span class="sxs-lookup"><span data-stu-id="eace7-248">The chart changes to display the entity predictions.</span></span> 

2. <span data-ttu-id="eace7-249">Select **False Negative** in the lower, left quadrant of the chart.</span><span class="sxs-lookup"><span data-stu-id="eace7-249">Select **False Negative** in the lower, left quadrant of the chart.</span></span> <span data-ttu-id="eace7-250">Then use the keyboard combination control + E to switch into the token view.</span><span class="sxs-lookup"><span data-stu-id="eace7-250">Then use the keyboard combination control + E to switch into the token view.</span></span> 

    <span data-ttu-id="eace7-251">[![Token view of entity predictions](./media/luis-tutorial-batch-testing/token-view-entities.png)](./media/luis-tutorial-batch-testing/token-view-entities.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="eace7-251">[![Token view of entity predictions](./media/luis-tutorial-batch-testing/token-view-entities.png)](./media/luis-tutorial-batch-testing/token-view-entities.png#lightbox)</span></span>
    
    <span data-ttu-id="eace7-252">Reviewing the utterances below the chart reveals a consistent error when the Job name includes `SQL`.</span><span class="sxs-lookup"><span data-stu-id="eace7-252">Reviewing the utterances below the chart reveals a consistent error when the Job name includes `SQL`.</span></span> <span data-ttu-id="eace7-253">Reviewing the example utterances and the Job phrase list, SQL is only used once, and only as part of a larger job name, `sql/oracle database administrator`.</span><span class="sxs-lookup"><span data-stu-id="eace7-253">Reviewing the example utterances and the Job phrase list, SQL is only used once, and only as part of a larger job name, `sql/oracle database administrator`.</span></span>

## <a name="fix-the-app-based-on-entity-batch-results"></a><span data-ttu-id="eace7-254">Fix the app based on entity batch results</span><span class="sxs-lookup"><span data-stu-id="eace7-254">Fix the app based on entity batch results</span></span>

<span data-ttu-id="eace7-255">Fixing the app requires LUIS to correctly determine the variations of SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="eace7-255">Fixing the app requires LUIS to correctly determine the variations of SQL jobs.</span></span> <span data-ttu-id="eace7-256">There are several options for that fix.</span><span class="sxs-lookup"><span data-stu-id="eace7-256">There are several options for that fix.</span></span> 

* <span data-ttu-id="eace7-257">Explicitly add more example utterances, which use SQL and label those words as a Job entity.</span><span class="sxs-lookup"><span data-stu-id="eace7-257">Explicitly add more example utterances, which use SQL and label those words as a Job entity.</span></span> 
* <span data-ttu-id="eace7-258">Explicitly add more SQL jobs to the phrase list</span><span class="sxs-lookup"><span data-stu-id="eace7-258">Explicitly add more SQL jobs to the phrase list</span></span>

<span data-ttu-id="eace7-259">These tasks are left for you to do.</span><span class="sxs-lookup"><span data-stu-id="eace7-259">These tasks are left for you to do.</span></span>

<span data-ttu-id="eace7-260">Adding a [pattern](luis-concept-patterns.md) before the entity is correctly predicted, is not going to fix the problem.</span><span class="sxs-lookup"><span data-stu-id="eace7-260">Adding a [pattern](luis-concept-patterns.md) before the entity is correctly predicted, is not going to fix the problem.</span></span> <span data-ttu-id="eace7-261">This is because the pattern won't match until all the entities in the pattern are detected.</span><span class="sxs-lookup"><span data-stu-id="eace7-261">This is because the pattern won't match until all the entities in the pattern are detected.</span></span> 

## <a name="what-has-this-tutorial-accomplished"></a><span data-ttu-id="eace7-262">What has this tutorial accomplished?</span><span class="sxs-lookup"><span data-stu-id="eace7-262">What has this tutorial accomplished?</span></span>

<span data-ttu-id="eace7-263">The app prediction accuracy has increased by finding errors in the batch and correcting the model.</span><span class="sxs-lookup"><span data-stu-id="eace7-263">The app prediction accuracy has increased by finding errors in the batch and correcting the model.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="eace7-264">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="eace7-264">Clean up resources</span></span>

[!INCLUDE [LUIS How to clean up resources](../../../includes/cognitive-services-luis-tutorial-how-to-clean-up-resources.md)]

## <a name="next-steps"></a><span data-ttu-id="eace7-265">Next steps</span><span class="sxs-lookup"><span data-stu-id="eace7-265">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eace7-266">Learn about patterns</span><span class="sxs-lookup"><span data-stu-id="eace7-266">Learn about patterns</span></span>](luis-tutorial-pattern.md)

