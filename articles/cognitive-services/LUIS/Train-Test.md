---
title: Train and test your LUIS app | Microsoft Docs
description: Use Language Understanding Intelligent Services (LUIS) to continuously work on your application to refine it and improve its language understanding.
services: cognitive-services
author: cahann
manager: hsalama
ms.service: cognitive-services
ms.technology: luis
ms.topic: article
ms.date: 03/01/2017
ms.author: cahann
ms.openlocfilehash: 852c2e65debf27eb06caaac98b684b98c448782f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551790"
---
# <a name="train-and-test-your-app"></a><span data-ttu-id="4db00-103">Train and test your app</span><span class="sxs-lookup"><span data-stu-id="4db00-103">Train and test your app</span></span>

## <a name="train-to-teach-your-app"></a><span data-ttu-id="4db00-104">Train to teach your app</span><span class="sxs-lookup"><span data-stu-id="4db00-104">Train to teach your app</span></span>
<span data-ttu-id="4db00-105">You should continuously work on your application to refine it and improve its language understanding.</span><span class="sxs-lookup"><span data-stu-id="4db00-105">You should continuously work on your application to refine it and improve its language understanding.</span></span> <span data-ttu-id="4db00-106">Whenever you make updates by adding, editing or deleting entities, intents or utterances in your current model, you’ll need to train your app before testing and publishing.</span><span class="sxs-lookup"><span data-stu-id="4db00-106">Whenever you make updates by adding, editing or deleting entities, intents or utterances in your current model, you’ll need to train your app before testing and publishing.</span></span> <span data-ttu-id="4db00-107">When you "train" a model, LUIS generalizes from the examples you have labeled, and builds model to recognize the relevant intents and entities in the future, thus improving its classification accuracy.</span><span class="sxs-lookup"><span data-stu-id="4db00-107">When you "train" a model, LUIS generalizes from the examples you have labeled, and builds model to recognize the relevant intents and entities in the future, thus improving its classification accuracy.</span></span> 

<span data-ttu-id="4db00-108">**To train your current model:**</span><span class="sxs-lookup"><span data-stu-id="4db00-108">**To train your current model:**</span></span>

1. <span data-ttu-id="4db00-109">Access your app (e.g. TravelAgent) by clicking its name on **My Apps** page.</span><span class="sxs-lookup"><span data-stu-id="4db00-109">Access your app (e.g. TravelAgent) by clicking its name on **My Apps** page.</span></span> 

2. <span data-ttu-id="4db00-110">In your app, click **Train & Test** in the left panel.</span><span class="sxs-lookup"><span data-stu-id="4db00-110">In your app, click **Train & Test** in the left panel.</span></span> 
3. <span data-ttu-id="4db00-111">On the **Test App** page, click **Train Application** to train the current model on the latest updates.</span><span class="sxs-lookup"><span data-stu-id="4db00-111">On the **Test App** page, click **Train Application** to train the current model on the latest updates.</span></span>

    ![Train & Test App page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Train_Test-app.JPG)

    >[!NOTE]
    ><span data-ttu-id="4db00-113">If you have one or more intents in your app which do not contain example utterances, you'll not be able to train your app until you add utterances for all your intents.</span><span class="sxs-lookup"><span data-stu-id="4db00-113">If you have one or more intents in your app which do not contain example utterances, you'll not be able to train your app until you add utterances for all your intents.</span></span> <span data-ttu-id="4db00-114">For more information, see [Add example utterances](Add-example-utterances.md).</span><span class="sxs-lookup"><span data-stu-id="4db00-114">For more information, see [Add example utterances](Add-example-utterances.md).</span></span>

## <a name="test-your-app"></a><span data-ttu-id="4db00-115">Test your app</span><span class="sxs-lookup"><span data-stu-id="4db00-115">Test your app</span></span>
<span data-ttu-id="4db00-116">LUIS provides two types of testing; interactive testing and batch testing.</span><span class="sxs-lookup"><span data-stu-id="4db00-116">LUIS provides two types of testing; interactive testing and batch testing.</span></span> <span data-ttu-id="4db00-117">You can use any of them by using the corresponding tab on the **Test App** page.</span><span class="sxs-lookup"><span data-stu-id="4db00-117">You can use any of them by using the corresponding tab on the **Test App** page.</span></span>

<span data-ttu-id="4db00-118">**To access the Test App page:**</span><span class="sxs-lookup"><span data-stu-id="4db00-118">**To access the Test App page:**</span></span>

1. <span data-ttu-id="4db00-119">Access your app (e.g. TravelAgent) by clicking its name on **My Apps** page,</span><span class="sxs-lookup"><span data-stu-id="4db00-119">Access your app (e.g. TravelAgent) by clicking its name on **My Apps** page,</span></span> 
2. <span data-ttu-id="4db00-120">Click **Train & Test** in your application's left panel to access the **Test App** page.</span><span class="sxs-lookup"><span data-stu-id="4db00-120">Click **Train & Test** in your application's left panel to access the **Test App** page.</span></span> 

- <span data-ttu-id="4db00-121">If you haven't already trained your current model on recent updates, then your test page will look like this screenshot:</span><span class="sxs-lookup"><span data-stu-id="4db00-121">If you haven't already trained your current model on recent updates, then your test page will look like this screenshot:</span></span>

    ![Train app before testing](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-trainfirst.JPG)
- <span data-ttu-id="4db00-123">If your model is trained, your test page will look like this screenshot:</span><span class="sxs-lookup"><span data-stu-id="4db00-123">If your model is trained, your test page will look like this screenshot:</span></span>

    ![Train & Test App page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Train_Test-app.JPG)

 
### <a name="interactive-testing"></a><span data-ttu-id="4db00-125">Interactive Testing</span><span class="sxs-lookup"><span data-stu-id="4db00-125">Interactive Testing</span></span>
<span data-ttu-id="4db00-126">Interactive testing enables you to test both the current and published versions of your app and compare their results in one screen.</span><span class="sxs-lookup"><span data-stu-id="4db00-126">Interactive testing enables you to test both the current and published versions of your app and compare their results in one screen.</span></span> <span data-ttu-id="4db00-127">Interactive testing runs by default on the current trained model only.</span><span class="sxs-lookup"><span data-stu-id="4db00-127">Interactive testing runs by default on the current trained model only.</span></span> <span data-ttu-id="4db00-128">For a published model, interactive testing is disabled and needs your action to enable it, because it is counted in hits and will be deducted from your key balance.</span><span class="sxs-lookup"><span data-stu-id="4db00-128">For a published model, interactive testing is disabled and needs your action to enable it, because it is counted in hits and will be deducted from your key balance.</span></span> 

<span data-ttu-id="4db00-129">The **Interactive Testing** tab is divided into two sections (as in the screenshot):</span><span class="sxs-lookup"><span data-stu-id="4db00-129">The **Interactive Testing** tab is divided into two sections (as in the screenshot):</span></span>

![Train & Test App page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Train_Test-app.JPG)

* <span data-ttu-id="4db00-131">**The test view**, on the left side of the screen, where you can type the test utterance in the text box and press Enter to submit it to your app.</span><span class="sxs-lookup"><span data-stu-id="4db00-131">**The test view**, on the left side of the screen, where you can type the test utterance in the text box and press Enter to submit it to your app.</span></span> 

* <span data-ttu-id="4db00-132">**The result view**, on the right side of the screen, where your LUIS app returns the test result; i.e. the predicted interpretation of the utterance.</span><span class="sxs-lookup"><span data-stu-id="4db00-132">**The result view**, on the right side of the screen, where your LUIS app returns the test result; i.e. the predicted interpretation of the utterance.</span></span> 

<span data-ttu-id="4db00-133">In an interactive test, you submit individual test utterances and view the returned result for each utterance separately.</span><span class="sxs-lookup"><span data-stu-id="4db00-133">In an interactive test, you submit individual test utterances and view the returned result for each utterance separately.</span></span> 

<span data-ttu-id="4db00-134">**To perform interactive testing on the current model:**</span><span class="sxs-lookup"><span data-stu-id="4db00-134">**To perform interactive testing on the current model:**</span></span>

- <span data-ttu-id="4db00-135">On the **Test App** page, **Interactive Testing** tab, type "book me a flight to Boston tomorrow" as your test utterance in the text box and press Enter.</span><span class="sxs-lookup"><span data-stu-id="4db00-135">On the **Test App** page, **Interactive Testing** tab, type "book me a flight to Boston tomorrow" as your test utterance in the text box and press Enter.</span></span> <span data-ttu-id="4db00-136">You'll get the following result:</span><span class="sxs-lookup"><span data-stu-id="4db00-136">You'll get the following result:</span></span>

    ![Interactive testing of current model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-interactive-current.JPG)

 <span data-ttu-id="4db00-138">The testing result includes the top scoring intent identified in the utterance, with its certainty score, as well as other intents existing in your model with their certainty scores.</span><span class="sxs-lookup"><span data-stu-id="4db00-138">The testing result includes the top scoring intent identified in the utterance, with its certainty score, as well as other intents existing in your model with their certainty scores.</span></span> <span data-ttu-id="4db00-139">The identified entities will also be displayed within the utterance and you can control their view by selecting your preferred view from the **Labels view** list at the top of the test console.</span><span class="sxs-lookup"><span data-stu-id="4db00-139">The identified entities will also be displayed within the utterance and you can control their view by selecting your preferred view from the **Labels view** list at the top of the test console.</span></span>

<span data-ttu-id="4db00-140">**To perform interactive testing on current and published models:**</span><span class="sxs-lookup"><span data-stu-id="4db00-140">**To perform interactive testing on current and published models:**</span></span>

1. <span data-ttu-id="4db00-141">On the **Test App** page, **Interactive Testing** tab, click **Enable published model** check box and then click **Yes** in the following confirmation message:</span><span class="sxs-lookup"><span data-stu-id="4db00-141">On the **Test App** page, **Interactive Testing** tab, click **Enable published model** check box and then click **Yes** in the following confirmation message:</span></span>

    ![Confirm Published Model Test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-ConfirmPublishedTest.JPG)

    >[!NOTE] 
    ><span data-ttu-id="4db00-143">If you do not have a published version of your application, the **Enable published model** check box will be disabled.</span><span class="sxs-lookup"><span data-stu-id="4db00-143">If you do not have a published version of your application, the **Enable published model** check box will be disabled.</span></span> 

2. <span data-ttu-id="4db00-144">Type "book me a flight to Boston tomorrow" as your test utterance and press Enter.</span><span class="sxs-lookup"><span data-stu-id="4db00-144">Type "book me a flight to Boston tomorrow" as your test utterance and press Enter.</span></span> <span data-ttu-id="4db00-145">The result view on the right side will be split horizontally into two parts (as in the following screenshot) to display results of the test utterance in both the current and published models.</span><span class="sxs-lookup"><span data-stu-id="4db00-145">The result view on the right side will be split horizontally into two parts (as in the following screenshot) to display results of the test utterance in both the current and published models.</span></span> 

    ![Interactive testing of both current & published models](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-interactive-both.JPG)
3. <span data-ttu-id="4db00-147">To view the test result of your published app in JSON format, click **Raw JSON view**.</span><span class="sxs-lookup"><span data-stu-id="4db00-147">To view the test result of your published app in JSON format, click **Raw JSON view**.</span></span> <span data-ttu-id="4db00-148">This will look like the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="4db00-148">This will look like the following screenshot.</span></span>

    ![Published model test result in JSON format](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-JSON-result.JPG)

<span data-ttu-id="4db00-150">In case of interactive testing on both trained and published models together, an entity may have a different prediction in each model.</span><span class="sxs-lookup"><span data-stu-id="4db00-150">In case of interactive testing on both trained and published models together, an entity may have a different prediction in each model.</span></span> <span data-ttu-id="4db00-151">In the test result, this entity will be distinguished by a red underline.</span><span class="sxs-lookup"><span data-stu-id="4db00-151">In the test result, this entity will be distinguished by a red underline.</span></span> <span data-ttu-id="4db00-152">If you hover over the underlined entity, you can view the entity prediction in both trained and published models.</span><span class="sxs-lookup"><span data-stu-id="4db00-152">If you hover over the underlined entity, you can view the entity prediction in both trained and published models.</span></span>

![Different entity prediction in both models](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/TestApp-interactive-both-diffentity.JPG)

>[!NOTE]
><span data-ttu-id="4db00-154">About the interactive testing console:</span><span class="sxs-lookup"><span data-stu-id="4db00-154">About the interactive testing console:</span></span>
 >- <span data-ttu-id="4db00-155">You can type as many test utterances as you want in the test view; only one utterance at a time.</span><span class="sxs-lookup"><span data-stu-id="4db00-155">You can type as many test utterances as you want in the test view; only one utterance at a time.</span></span>
 >- <span data-ttu-id="4db00-156">The result view shows the result of the latest utterance.</span><span class="sxs-lookup"><span data-stu-id="4db00-156">The result view shows the result of the latest utterance.</span></span> 
 >- <span data-ttu-id="4db00-157">To review the result of a previous utterance, just click it in the test view and its result will be displayed on the right.</span><span class="sxs-lookup"><span data-stu-id="4db00-157">To review the result of a previous utterance, just click it in the test view and its result will be displayed on the right.</span></span> 
 >- <span data-ttu-id="4db00-158">To clear all the entered test utterances and their results from the test console, click **Reset Console** on the top right corner of the console.</span><span class="sxs-lookup"><span data-stu-id="4db00-158">To clear all the entered test utterances and their results from the test console, click **Reset Console** on the top right corner of the console.</span></span> 


### <a name="batch-testing"></a><span data-ttu-id="4db00-159">Batch Testing</span><span class="sxs-lookup"><span data-stu-id="4db00-159">Batch Testing</span></span>
<span data-ttu-id="4db00-160">Batch testing enables you to run a comprehensive test on your current trained model to measure its performance in language understanding.</span><span class="sxs-lookup"><span data-stu-id="4db00-160">Batch testing enables you to run a comprehensive test on your current trained model to measure its performance in language understanding.</span></span> <span data-ttu-id="4db00-161">In batch testing, you submit a large number of test utterances collectively in a batch file, known as "dataset".</span><span class="sxs-lookup"><span data-stu-id="4db00-161">In batch testing, you submit a large number of test utterances collectively in a batch file, known as "dataset".</span></span> <span data-ttu-id="4db00-162">The dataset file should be written in JSON format and contains a maximum of 1000 utterances.</span><span class="sxs-lookup"><span data-stu-id="4db00-162">The dataset file should be written in JSON format and contains a maximum of 1000 utterances.</span></span> <span data-ttu-id="4db00-163">All you need to do is to import this file to your app and run it to perform the test.</span><span class="sxs-lookup"><span data-stu-id="4db00-163">All you need to do is to import this file to your app and run it to perform the test.</span></span> <span data-ttu-id="4db00-164">Your LUIS app will return the result, enabling you to access detailed analysis of all utterances included in the batch.</span><span class="sxs-lookup"><span data-stu-id="4db00-164">Your LUIS app will return the result, enabling you to access detailed analysis of all utterances included in the batch.</span></span>

<span data-ttu-id="4db00-165">You can import up to 10 dataset files to a single LUIS app.</span><span class="sxs-lookup"><span data-stu-id="4db00-165">You can import up to 10 dataset files to a single LUIS app.</span></span> <span data-ttu-id="4db00-166">It is recommended that the utterances included in the dataset should be different from the example utterances you previously added while building your app.</span><span class="sxs-lookup"><span data-stu-id="4db00-166">It is recommended that the utterances included in the dataset should be different from the example utterances you previously added while building your app.</span></span> 
 
<span data-ttu-id="4db00-167">The following procedures will guide you on how to import a dataset file, run a batch test on your current trained app using the imported dataset, and finally to access the test results in a detailed visualized view.</span><span class="sxs-lookup"><span data-stu-id="4db00-167">The following procedures will guide you on how to import a dataset file, run a batch test on your current trained app using the imported dataset, and finally to access the test results in a detailed visualized view.</span></span>

<span data-ttu-id="4db00-168">**To import a dataset file:**</span><span class="sxs-lookup"><span data-stu-id="4db00-168">**To import a dataset file:**</span></span>

1. <span data-ttu-id="4db00-169">On the **Test App** page, click **Batch Testing**, and then click **Import dataset**.</span><span class="sxs-lookup"><span data-stu-id="4db00-169">On the **Test App** page, click **Batch Testing**, and then click **Import dataset**.</span></span> <span data-ttu-id="4db00-170">The **Import dataset** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="4db00-170">The **Import dataset** dialog box appears.</span></span>

    ![Import Dataset File](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-importset.JPG)

2. <span data-ttu-id="4db00-172">In **Dataset name**, type a name for your dataset file (For example "DataSet1").</span><span class="sxs-lookup"><span data-stu-id="4db00-172">In **Dataset name**, type a name for your dataset file (For example "DataSet1").</span></span>

3. <span data-ttu-id="4db00-173">To learn more about the supported syntax for dataset files to be imported, click **learn about the supported dataset syntax link**.</span><span class="sxs-lookup"><span data-stu-id="4db00-173">To learn more about the supported syntax for dataset files to be imported, click **learn about the supported dataset syntax link**.</span></span> <span data-ttu-id="4db00-174">The **Import dataset** dialog box will be expanded displaying the allowed syntax.</span><span class="sxs-lookup"><span data-stu-id="4db00-174">The **Import dataset** dialog box will be expanded displaying the allowed syntax.</span></span> <span data-ttu-id="4db00-175">To collapse the dialog and hide syntax, just click the link again.</span><span class="sxs-lookup"><span data-stu-id="4db00-175">To collapse the dialog and hide syntax, just click the link again.</span></span>

    ![Dataset Allowed Syntax](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-datasetSyntx.JPG)

4. <span data-ttu-id="4db00-177">Click **Choose File** to choose the dataset file you want to import, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4db00-177">Click **Choose File** to choose the dataset file you want to import, and then click **Save**.</span></span> <span data-ttu-id="4db00-178">The dataset file will be added.</span><span class="sxs-lookup"><span data-stu-id="4db00-178">The dataset file will be added.</span></span>

    ![List of datasets](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-datasetList.JPG)

5. <span data-ttu-id="4db00-180">To rename, delete or download the imported dataset, you can use these buttons respectively: **Rename Dataset** ![Rename Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Rename-Intent-btn.JPG), **Delete Dataset** ![Delete Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) and **Download Dataset JSON** ![Download Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-downloadDataset.JPG).</span><span class="sxs-lookup"><span data-stu-id="4db00-180">To rename, delete or download the imported dataset, you can use these buttons respectively: **Rename Dataset** ![Rename Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/Rename-Intent-btn.JPG), **Delete Dataset** ![Delete Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/trashbin-button.JPG) and **Download Dataset JSON** ![Download Dataset button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-downloadDataset.JPG).</span></span>

<span data-ttu-id="4db00-181">**To run a batch test on your trained app:**</span><span class="sxs-lookup"><span data-stu-id="4db00-181">**To run a batch test on your trained app:**</span></span>

- <span data-ttu-id="4db00-182">Click **Test** next to the dataset you've just imported.</span><span class="sxs-lookup"><span data-stu-id="4db00-182">Click **Test** next to the dataset you've just imported.</span></span> <span data-ttu-id="4db00-183">Soon, the test result of the dataset will be displayed.</span><span class="sxs-lookup"><span data-stu-id="4db00-183">Soon, the test result of the dataset will be displayed.</span></span>

    ![Batch Test Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-result.JPG)

    <span data-ttu-id="4db00-185">In the above screenshot:</span><span class="sxs-lookup"><span data-stu-id="4db00-185">In the above screenshot:</span></span>
 
    - <span data-ttu-id="4db00-186">**Status** of the dataset shows whether or not the dataset result contains errors.</span><span class="sxs-lookup"><span data-stu-id="4db00-186">**Status** of the dataset shows whether or not the dataset result contains errors.</span></span> <span data-ttu-id="4db00-187">In the above example, an error sign is displayed indicating that there are errors in one or more utterances.</span><span class="sxs-lookup"><span data-stu-id="4db00-187">In the above example, an error sign is displayed indicating that there are errors in one or more utterances.</span></span> <span data-ttu-id="4db00-188">If the test result contains no errors, a green sign will be displayed instead.</span><span class="sxs-lookup"><span data-stu-id="4db00-188">If the test result contains no errors, a green sign will be displayed instead.</span></span> 
    - <span data-ttu-id="4db00-189">**Utterance Count** is the total number of utterances included in the dataset file.</span><span class="sxs-lookup"><span data-stu-id="4db00-189">**Utterance Count** is the total number of utterances included in the dataset file.</span></span>
    - <span data-ttu-id="4db00-190">**Last Test Date** is the date of the latest test run for this dataset.</span><span class="sxs-lookup"><span data-stu-id="4db00-190">**Last Test Date** is the date of the latest test run for this dataset.</span></span> 
    - <span data-ttu-id="4db00-191">**Last Test Success** displays the percentage of correct predictions resulting from the test.</span><span class="sxs-lookup"><span data-stu-id="4db00-191">**Last Test Success** displays the percentage of correct predictions resulting from the test.</span></span>

<span data-ttu-id="4db00-192">**To access test result details in a visualized view:**</span><span class="sxs-lookup"><span data-stu-id="4db00-192">**To access test result details in a visualized view:**</span></span>
 
1. <span data-ttu-id="4db00-193">Click the **See results** link that appears as a result of running the test (see the above screenshot).</span><span class="sxs-lookup"><span data-stu-id="4db00-193">Click the **See results** link that appears as a result of running the test (see the above screenshot).</span></span> <span data-ttu-id="4db00-194">A scatter graph (confusion matrix) is displayed, where the data points represent the utterances in the dataset.</span><span class="sxs-lookup"><span data-stu-id="4db00-194">A scatter graph (confusion matrix) is displayed, where the data points represent the utterances in the dataset.</span></span> <span data-ttu-id="4db00-195">Green points indicate correct prediction and red ones indicate incorrect prediction.</span><span class="sxs-lookup"><span data-stu-id="4db00-195">Green points indicate correct prediction and red ones indicate incorrect prediction.</span></span> 

    ![Visualized Batch Test Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-resultgraph.JPG) 

    >[!NOTE]
    ><span data-ttu-id="4db00-197">The filtering panel on the right side of the screen displays a list of all intents and entities in the app, with a green point for intents/entities which were predicted correctly in all dataset utterances, and a red one for those with errors.</span><span class="sxs-lookup"><span data-stu-id="4db00-197">The filtering panel on the right side of the screen displays a list of all intents and entities in the app, with a green point for intents/entities which were predicted correctly in all dataset utterances, and a red one for those with errors.</span></span> <span data-ttu-id="4db00-198">Also, for each intent/entity, you can see the number of correct predictions out of the total utterances.</span><span class="sxs-lookup"><span data-stu-id="4db00-198">Also, for each intent/entity, you can see the number of correct predictions out of the total utterances.</span></span> <span data-ttu-id="4db00-199">For example, in the above screenshot, the entity "Location (4/9)" has 4 correct predictions out of 9, so it has 5 errors.</span><span class="sxs-lookup"><span data-stu-id="4db00-199">For example, in the above screenshot, the entity "Location (4/9)" has 4 correct predictions out of 9, so it has 5 errors.</span></span>
  
2. <span data-ttu-id="4db00-200">To filter the view by a specific intent/entity, click on your target intent/entity in the filtering panel.</span><span class="sxs-lookup"><span data-stu-id="4db00-200">To filter the view by a specific intent/entity, click on your target intent/entity in the filtering panel.</span></span> <span data-ttu-id="4db00-201">The data points and their distribution will be updated according to your selection.</span><span class="sxs-lookup"><span data-stu-id="4db00-201">The data points and their distribution will be updated according to your selection.</span></span> <span data-ttu-id="4db00-202">For example, the following screenshot displays results for the "GetWeather" intent.</span><span class="sxs-lookup"><span data-stu-id="4db00-202">For example, the following screenshot displays results for the "GetWeather" intent.</span></span>
 
    ![Visualized Batch Test Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-resultgraph2.JPG) 

    >[!NOTE]
    ><span data-ttu-id="4db00-204">Hovering over a data point shows the certainty score of its prediction.</span><span class="sxs-lookup"><span data-stu-id="4db00-204">Hovering over a data point shows the certainty score of its prediction.</span></span>
 
    <span data-ttu-id="4db00-205">The graph contains 4 sections representing the possible cases of your application's prediction:</span><span class="sxs-lookup"><span data-stu-id="4db00-205">The graph contains 4 sections representing the possible cases of your application's prediction:</span></span>

    - <span data-ttu-id="4db00-206">**True Positive (TP):** The data points in this section represent utterances in which your app correctly predicted the existence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="4db00-206">**True Positive (TP):** The data points in this section represent utterances in which your app correctly predicted the existence of the target intent/entity.</span></span> 
    - <span data-ttu-id="4db00-207">**True Negative (TN):** The data points in this section represent utterances in which your app correctly predicted the absence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="4db00-207">**True Negative (TN):** The data points in this section represent utterances in which your app correctly predicted the absence of the target intent/entity.</span></span>
    - <span data-ttu-id="4db00-208">**False Positive (FP):** The data points in this section represent utterances in which your app incorrectly predicted the existence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="4db00-208">**False Positive (FP):** The data points in this section represent utterances in which your app incorrectly predicted the existence of the target intent/entity.</span></span>
    - <span data-ttu-id="4db00-209">**False Negative (FN):** The data points in this section represent utterances in which your app incorrectly predicted the absence of the target intent/entity.</span><span class="sxs-lookup"><span data-stu-id="4db00-209">**False Negative (FN):** The data points in this section represent utterances in which your app incorrectly predicted the absence of the target intent/entity.</span></span>

    <span data-ttu-id="4db00-210">This means that data points on the **False Positive** & **False Negative** sections indicate errors, which should be investigated.</span><span class="sxs-lookup"><span data-stu-id="4db00-210">This means that data points on the **False Positive** & **False Negative** sections indicate errors, which should be investigated.</span></span> <span data-ttu-id="4db00-211">On the other hand, if all data points are on the **True Positive** and **True Negative** sections, then your application's performance is perfect on this dataset.</span><span class="sxs-lookup"><span data-stu-id="4db00-211">On the other hand, if all data points are on the **True Positive** and **True Negative** sections, then your application's performance is perfect on this dataset.</span></span>
 
3. <span data-ttu-id="4db00-212">Click a data point to retrieve its corresponding utterance in the utterances table at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="4db00-212">Click a data point to retrieve its corresponding utterance in the utterances table at the bottom of the page.</span></span> <span data-ttu-id="4db00-213">To display all utterances in a section, click the section title (e.g. True Positive, False Negative, ..etc.)</span><span class="sxs-lookup"><span data-stu-id="4db00-213">To display all utterances in a section, click the section title (e.g. True Positive, False Negative, ..etc.)</span></span> 

    <span data-ttu-id="4db00-214">For example, the following screenshot shows the results for the "None" intent when one of its data points is clicked, so the utterance "weather forecast for tomorrow" is displayed.</span><span class="sxs-lookup"><span data-stu-id="4db00-214">For example, the following screenshot shows the results for the "None" intent when one of its data points is clicked, so the utterance "weather forecast for tomorrow" is displayed.</span></span> <span data-ttu-id="4db00-215">This utterance falls under the **True Negative** section as your app correctly predicted that the "None" intent is not present in this utterance.</span><span class="sxs-lookup"><span data-stu-id="4db00-215">This utterance falls under the **True Negative** section as your app correctly predicted that the "None" intent is not present in this utterance.</span></span> 

    ![Visualized Batch Test Result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/LUIS/Images/BatchTest-resultgraph3.JPG) 
  
<span data-ttu-id="4db00-217">Thus, a batch test helps you view the performance of each intent and entity in your current trained model on a specific set of utterances.</span><span class="sxs-lookup"><span data-stu-id="4db00-217">Thus, a batch test helps you view the performance of each intent and entity in your current trained model on a specific set of utterances.</span></span> <span data-ttu-id="4db00-218">This helps you take appropriate actions, when required, to improve performance, such as adding more example utterances to an intent if your app frequently fails to identify it.</span><span class="sxs-lookup"><span data-stu-id="4db00-218">This helps you take appropriate actions, when required, to improve performance, such as adding more example utterances to an intent if your app frequently fails to identify it.</span></span>



















