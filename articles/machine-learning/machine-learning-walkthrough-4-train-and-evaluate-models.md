---
title: 'Step 4: Train and evaluate the predictive analytic models | Microsoft Docs'
description: 'Step 4 of the Develop a predictive solution walkthrough: Train, score, and evaluate multiple models in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: d905f6b3-9201-4117-b769-5f9ed5ee1cac
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 7552e5635b2a910af35a48dce5c104219eacecb3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554694"
---
# <a name="walkthrough-step-4-train-and-evaluate-the-predictive-analytic-models"></a><span data-ttu-id="a7f35-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span><span class="sxs-lookup"><span data-stu-id="a7f35-103">Walkthrough Step 4: Train and evaluate the predictive analytic models</span></span>
<span data-ttu-id="a7f35-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="a7f35-104">This topic contains the fourth step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](machine-learning-walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="a7f35-105">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="a7f35-105">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="a7f35-106">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="a7f35-106">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="a7f35-107">Create a new experiment</span><span class="sxs-lookup"><span data-stu-id="a7f35-107">Create a new experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. <span data-ttu-id="a7f35-108">**Train and evaluate the models**</span><span class="sxs-lookup"><span data-stu-id="a7f35-108">**Train and evaluate the models**</span></span>
5. [<span data-ttu-id="a7f35-109">Deploy the Web service</span><span class="sxs-lookup"><span data-stu-id="a7f35-109">Deploy the Web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="a7f35-110">Access the Web service</span><span class="sxs-lookup"><span data-stu-id="a7f35-110">Access the Web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="a7f35-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span><span class="sxs-lookup"><span data-stu-id="a7f35-111">One of the benefits of using Azure Machine Learning Studio for creating machine learning models is the ability to try more than one type of model at a time in a single experiment and compare the results.</span></span> <span data-ttu-id="a7f35-112">This type of experimentation helps you find the best solution for your problem.</span><span class="sxs-lookup"><span data-stu-id="a7f35-112">This type of experimentation helps you find the best solution for your problem.</span></span>

<span data-ttu-id="a7f35-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span><span class="sxs-lookup"><span data-stu-id="a7f35-113">In the experiment we're developing in this walkthrough, we'll create two different types of models and then compare their scoring results to decide which algorithm we want to use in our final experiment.</span></span>  

<span data-ttu-id="a7f35-114">There are various models we could choose from.</span><span class="sxs-lookup"><span data-stu-id="a7f35-114">There are various models we could choose from.</span></span> <span data-ttu-id="a7f35-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span><span class="sxs-lookup"><span data-stu-id="a7f35-115">To see the models available, expand the **Machine Learning** node in the module palette, and then expand **Initialize Model** and the nodes beneath it.</span></span> <span data-ttu-id="a7f35-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span><span class="sxs-lookup"><span data-stu-id="a7f35-116">For the purposes of this experiment, we'll select the [Two-Class Support Vector Machine][two-class-support-vector-machine] (SVM) and the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] modules.</span></span>    

> [!TIP]
> <span data-ttu-id="a7f35-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span><span class="sxs-lookup"><span data-stu-id="a7f35-117">To get help deciding which Machine Learning algorithm best suits the particular problem you're trying to solve, see [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md).</span></span>
> 
> 

## <a name="train-the-models"></a><span data-ttu-id="a7f35-118">Train the models</span><span class="sxs-lookup"><span data-stu-id="a7f35-118">Train the models</span></span>

<span data-ttu-id="a7f35-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span><span class="sxs-lookup"><span data-stu-id="a7f35-119">We'll add both the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module and [Two-Class Support Vector Machine][two-class-support-vector-machine] module in this experiment.</span></span>

### <a name="two-class-boosted-decision-tree"></a><span data-ttu-id="a7f35-120">Two-Class Boosted Decision Tree</span><span class="sxs-lookup"><span data-stu-id="a7f35-120">Two-Class Boosted Decision Tree</span></span>

<span data-ttu-id="a7f35-121">First, let's set up the boosted decision tree model.</span><span class="sxs-lookup"><span data-stu-id="a7f35-121">First, let's set up the boosted decision tree model.</span></span>

1. <span data-ttu-id="a7f35-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-122">Find the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="a7f35-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-123">Find the [Train Model][train-model] module, drag it onto the canvas, and then connect the output of the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Train Model][train-model] module.</span></span>
   
   <span data-ttu-id="a7f35-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span><span class="sxs-lookup"><span data-stu-id="a7f35-124">The [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module initializes the generic model, and [Train Model][train-model] uses training data to train the model.</span></span> 

3. <span data-ttu-id="a7f35-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span><span class="sxs-lookup"><span data-stu-id="a7f35-125">Connect the left output of the left [Execute R Script][execute-r-script] module to the right input port of the [Train Model][train-model] module (we decided in [Step 3](machine-learning-walkthrough-3-create-new-experiment.md) of this walkthrough to use the data coming from the left side of the Split Data module for training).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a7f35-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span><span class="sxs-lookup"><span data-stu-id="a7f35-126">We don't need two of the inputs and one of the outputs of the [Execute R Script][execute-r-script] module for this experiment, so we can leave them unattached.</span></span> 
   > 
   > 

<span data-ttu-id="a7f35-127">This portion of the experiment now looks something like this:</span><span class="sxs-lookup"><span data-stu-id="a7f35-127">This portion of the experiment now looks something like this:</span></span>  

![Training a model][1]

<span data-ttu-id="a7f35-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span><span class="sxs-lookup"><span data-stu-id="a7f35-129">Now we need to tell the [Train Model][train-model] module that we want the model to predict the Credit Risk value.</span></span>

1. <span data-ttu-id="a7f35-130">Select the [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-130">Select the [Train Model][train-model] module.</span></span> <span data-ttu-id="a7f35-131">In the **Properties** pane, click **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="a7f35-131">In the **Properties** pane, click **Launch column selector**.</span></span>

2. <span data-ttu-id="a7f35-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span><span class="sxs-lookup"><span data-stu-id="a7f35-132">In the **Select a single column** dialog, type "credit risk" in the search field under **Available Columns**, select "Credit risk" below, and click the right arrow button (**>**) to move "Credit risk" to **Selected Columns**.</span></span> 

    ![Select the Credit Risk column for the Train Model module][0]

3. <span data-ttu-id="a7f35-134">Click the **OK** check mark.</span><span class="sxs-lookup"><span data-stu-id="a7f35-134">Click the **OK** check mark.</span></span>

### <a name="two-class-support-vector-machine"></a><span data-ttu-id="a7f35-135">Two-Class Support Vector Machine</span><span class="sxs-lookup"><span data-stu-id="a7f35-135">Two-Class Support Vector Machine</span></span>

<span data-ttu-id="a7f35-136">Next, we set up the SVM model.</span><span class="sxs-lookup"><span data-stu-id="a7f35-136">Next, we set up the SVM model.</span></span>  

<span data-ttu-id="a7f35-137">First, a little explanation about SVM.</span><span class="sxs-lookup"><span data-stu-id="a7f35-137">First, a little explanation about SVM.</span></span> <span data-ttu-id="a7f35-138">Boosted decision trees work well with features of any type.</span><span class="sxs-lookup"><span data-stu-id="a7f35-138">Boosted decision trees work well with features of any type.</span></span> <span data-ttu-id="a7f35-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span><span class="sxs-lookup"><span data-stu-id="a7f35-139">However, since the SVM module generates a linear classifier, the model that it generates has the best test error when all numeric features have the same scale.</span></span> <span data-ttu-id="a7f35-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span><span class="sxs-lookup"><span data-stu-id="a7f35-140">To convert all numeric features to the same scale, we use a "Tanh" transformation (with the [Normalize Data][normalize-data] module).</span></span> <span data-ttu-id="a7f35-141">This transforms our numbers into the [0,1] range.</span><span class="sxs-lookup"><span data-stu-id="a7f35-141">This transforms our numbers into the [0,1] range.</span></span> <span data-ttu-id="a7f35-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span><span class="sxs-lookup"><span data-stu-id="a7f35-142">The SVM module converts string features to categorical features and then to binary 0/1 features, so we don't need to manually transform string features.</span></span> <span data-ttu-id="a7f35-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span><span class="sxs-lookup"><span data-stu-id="a7f35-143">Also, we don't want to transform the Credit Risk column (column 21) - it's numeric, but it's the value we're training the model to predict, so we need to leave it alone.</span></span>  

<span data-ttu-id="a7f35-144">To set up the SVM model, do the following:</span><span class="sxs-lookup"><span data-stu-id="a7f35-144">To set up the SVM model, do the following:</span></span>

1. <span data-ttu-id="a7f35-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-145">Find the [Two-Class Support Vector Machine][two-class-support-vector-machine] module in the module palette and drag it onto the canvas.</span></span>

2. <span data-ttu-id="a7f35-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span><span class="sxs-lookup"><span data-stu-id="a7f35-146">Right-click the [Train Model][train-model] module, select **Copy**, and then right-click the canvas and select **Paste**.</span></span> <span data-ttu-id="a7f35-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span><span class="sxs-lookup"><span data-stu-id="a7f35-147">The copy of the [Train Model][train-model] module has the same column selection as the original.</span></span>

3. <span data-ttu-id="a7f35-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-148">Connect the output of the [Two-Class Support Vector Machine][two-class-support-vector-machine] module to the left input port of the second [Train Model][train-model] module.</span></span>

4. <span data-ttu-id="a7f35-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-149">Find the [Normalize Data][normalize-data] module and drag it onto the canvas.</span></span>

5. <span data-ttu-id="a7f35-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span><span class="sxs-lookup"><span data-stu-id="a7f35-150">Connect the left output of the left [Execute R Script][execute-r-script] module to the input of this module (notice that the output port of a module may be connected to more than one other module).</span></span>

6. <span data-ttu-id="a7f35-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-151">Connect the left output port of the [Normalize Data][normalize-data] module to the right input port of the second [Train Model][train-model] module.</span></span>

<span data-ttu-id="a7f35-152">This portion of our experiment should now look something like this:</span><span class="sxs-lookup"><span data-stu-id="a7f35-152">This portion of our experiment should now look something like this:</span></span>  

![Training the second model][2]  

<span data-ttu-id="a7f35-154">Now configure the [Normalize Data][normalize-data] module:</span><span class="sxs-lookup"><span data-stu-id="a7f35-154">Now configure the [Normalize Data][normalize-data] module:</span></span>

1. <span data-ttu-id="a7f35-155">Click to select the [Normalize Data][normalize-data] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-155">Click to select the [Normalize Data][normalize-data] module.</span></span> <span data-ttu-id="a7f35-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span><span class="sxs-lookup"><span data-stu-id="a7f35-156">In the **Properties** pane, select **Tanh** for the **Transformation method** parameter.</span></span>

2. <span data-ttu-id="a7f35-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span><span class="sxs-lookup"><span data-stu-id="a7f35-157">Click **Launch column selector**, select "No columns" for **Begin With**, select **Include** in the first dropdown, select **column type** in the second dropdown, and select **Numeric** in the third dropdown.</span></span> <span data-ttu-id="a7f35-158">This specifies that all the numeric columns (and only numeric) are transformed.</span><span class="sxs-lookup"><span data-stu-id="a7f35-158">This specifies that all the numeric columns (and only numeric) are transformed.</span></span>

3. <span data-ttu-id="a7f35-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span><span class="sxs-lookup"><span data-stu-id="a7f35-159">Click the plus sign (+) to the right of this row - this creates a row of dropdowns.</span></span> <span data-ttu-id="a7f35-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span><span class="sxs-lookup"><span data-stu-id="a7f35-160">Select **Exclude** in the first dropdown, select **column names** in the second dropdown, and enter "Credit risk" in the text field.</span></span> <span data-ttu-id="a7f35-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span><span class="sxs-lookup"><span data-stu-id="a7f35-161">This specifies that the Credit Risk column should be ignored (we need to do this because this column is numeric and so would be transformed if we didn't exclude it).</span></span>

4. <span data-ttu-id="a7f35-162">Click the **OK** check mark.</span><span class="sxs-lookup"><span data-stu-id="a7f35-162">Click the **OK** check mark.</span></span>  

    ![Select columns for the Normalize Data module][5]

<span data-ttu-id="a7f35-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span><span class="sxs-lookup"><span data-stu-id="a7f35-164">The [Normalize Data][normalize-data] module is now set to perform a Tanh transformation on all numeric columns except for the Credit Risk column.</span></span>  

## <a name="score-and-evaluate-the-models"></a><span data-ttu-id="a7f35-165">Score and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="a7f35-165">Score and evaluate the models</span></span>

<span data-ttu-id="a7f35-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span><span class="sxs-lookup"><span data-stu-id="a7f35-166">We use the testing data that was separated out by the [Split Data][split] module to score our trained models.</span></span> <span data-ttu-id="a7f35-167">We can then compare the results of the two models to see which generated better results.</span><span class="sxs-lookup"><span data-stu-id="a7f35-167">We can then compare the results of the two models to see which generated better results.</span></span>  

### <a name="add-the-score-model-modules"></a><span data-ttu-id="a7f35-168">Add the Score Model modules</span><span class="sxs-lookup"><span data-stu-id="a7f35-168">Add the Score Model modules</span></span>

1. <span data-ttu-id="a7f35-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-169">Find the [Score Model][score-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="a7f35-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-170">Connect the [Train Model][train-model] module that's connected to the [Two-Class Boosted Decision Tree][two-class-boosted-decision-tree] module to the left input port of the [Score Model][score-model] module.</span></span>

3. <span data-ttu-id="a7f35-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-171">Connect the right [Execute R Script][execute-r-script] module (our testing data) to the right input port of the [Score Model][score-model] module.</span></span>

    ![Score Model module connected][6]
   
   <span data-ttu-id="a7f35-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span><span class="sxs-lookup"><span data-stu-id="a7f35-173">The [Score Model][score-model] module can now take the credit information from the testing data, run it through the model, and compare the predictions the model generates with the actual credit risk column in the testing data.</span></span>

4. <span data-ttu-id="a7f35-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span><span class="sxs-lookup"><span data-stu-id="a7f35-174">Copy and paste the [Score Model][score-model] module to create a second copy.</span></span>

5. <span data-ttu-id="a7f35-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-175">Connect the output of the SVM model (that is, the output port of the [Train Model][train-model] module that's connected to the [Two-Class Support Vector Machine][two-class-support-vector-machine] module) to the input port of the second [Score Model][score-model] module.</span></span>

6. <span data-ttu-id="a7f35-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span><span class="sxs-lookup"><span data-stu-id="a7f35-176">For the SVM model, we have to do the same transformation to the test data as we did to the training data.</span></span> <span data-ttu-id="a7f35-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-177">So copy and paste the [Normalize Data][normalize-data] module to create a second copy and connect it to the right [Execute R Script][execute-r-script] module.</span></span>

7. <span data-ttu-id="a7f35-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-178">Connect the left output of the second [Normalize Data][normalize-data] module to the right input port of the second [Score Model][score-model] module.</span></span>

    ![Both Score Model modules connected][7]

### <a name="add-the-evaluate-model-module"></a><span data-ttu-id="a7f35-180">Add the Evaluate Model module</span><span class="sxs-lookup"><span data-stu-id="a7f35-180">Add the Evaluate Model module</span></span>

<span data-ttu-id="a7f35-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-181">To evaluate the two scoring results and compare them, we use an [Evaluate Model][evaluate-model] module.</span></span>  

1. <span data-ttu-id="a7f35-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-182">Find the [Evaluate Model][evaluate-model] module and drag it onto the canvas.</span></span>

2. <span data-ttu-id="a7f35-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="a7f35-183">Connect the output port of the [Score Model][score-model] module associated with the boosted decision tree model to the left input port of the [Evaluate Model][evaluate-model] module.</span></span>

3. <span data-ttu-id="a7f35-184">Connect the other [Score Model][score-model] module to the right input port.</span><span class="sxs-lookup"><span data-stu-id="a7f35-184">Connect the other [Score Model][score-model] module to the right input port.</span></span>  

    ![Evaluate Model module connected][8]

### <a name="run-the-experiment-and-check-the-results"></a><span data-ttu-id="a7f35-186">Run the experiment and check the results</span><span class="sxs-lookup"><span data-stu-id="a7f35-186">Run the experiment and check the results</span></span>

<span data-ttu-id="a7f35-187">To run the experiment, click the **RUN** button below the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-187">To run the experiment, click the **RUN** button below the canvas.</span></span> <span data-ttu-id="a7f35-188">It may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="a7f35-188">It may take a few minutes.</span></span> <span data-ttu-id="a7f35-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span><span class="sxs-lookup"><span data-stu-id="a7f35-189">A spinning indicator on each module shows that it's running, and then a green check mark shows when the module is finished.</span></span> <span data-ttu-id="a7f35-190">When all the modules have a check mark, the experiment has finished running.</span><span class="sxs-lookup"><span data-stu-id="a7f35-190">When all the modules have a check mark, the experiment has finished running.</span></span>

<span data-ttu-id="a7f35-191">The experiment should now look something like this:</span><span class="sxs-lookup"><span data-stu-id="a7f35-191">The experiment should now look something like this:</span></span>  

![Evaluating both models][3]

<span data-ttu-id="a7f35-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="a7f35-193">To check the results, click the output port of the [Evaluate Model][evaluate-model] module and select **Visualize**.</span></span>  

<span data-ttu-id="a7f35-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span><span class="sxs-lookup"><span data-stu-id="a7f35-194">The [Evaluate Model][evaluate-model] module produces a pair of curves and metrics that allow you to compare the results of the two scored models.</span></span> <span data-ttu-id="a7f35-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span><span class="sxs-lookup"><span data-stu-id="a7f35-195">You can view the results as Receiver Operator Characteristic (ROC) curves, Precision/Recall curves, or Lift curves.</span></span> <span data-ttu-id="a7f35-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span><span class="sxs-lookup"><span data-stu-id="a7f35-196">Additional data displayed includes a confusion matrix, cumulative values for the area under the curve (AUC), and other metrics.</span></span> <span data-ttu-id="a7f35-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span><span class="sxs-lookup"><span data-stu-id="a7f35-197">You can change the threshold value by moving the slider left or right and see how it affects the set of metrics.</span></span>  

<span data-ttu-id="a7f35-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span><span class="sxs-lookup"><span data-stu-id="a7f35-198">To the right of the graph, click **Scored dataset** or **Scored dataset to compare** to highlight the associated curve and to display the associated metrics below.</span></span> <span data-ttu-id="a7f35-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span><span class="sxs-lookup"><span data-stu-id="a7f35-199">In the legend for the curves, "Scored dataset" corresponds to the left input port of the [Evaluate Model][evaluate-model] module - in our case, this is the boosted decision tree model.</span></span> <span data-ttu-id="a7f35-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span><span class="sxs-lookup"><span data-stu-id="a7f35-200">"Scored dataset to compare" corresponds to the right input port - the SVM model in our case.</span></span> <span data-ttu-id="a7f35-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span><span class="sxs-lookup"><span data-stu-id="a7f35-201">When you click one of these labels, the curve for that model is highlighted and the corresponding metrics are displayed, as shown in the following graphic.</span></span>  

![ROC curves for models][4]

<span data-ttu-id="a7f35-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span><span class="sxs-lookup"><span data-stu-id="a7f35-203">By examining these values, you can decide which model is closest to giving you the results you're looking for.</span></span> <span data-ttu-id="a7f35-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span><span class="sxs-lookup"><span data-stu-id="a7f35-204">You can go back and iterate on your experiment by changing parameter values in the different models.</span></span> 

<span data-ttu-id="a7f35-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span><span class="sxs-lookup"><span data-stu-id="a7f35-205">The science and art of interpreting these results and tuning the model performance is outside the scope of this walkthrough.</span></span> <span data-ttu-id="a7f35-206">For additional help, you might read the following articles:</span><span class="sxs-lookup"><span data-stu-id="a7f35-206">For additional help, you might read the following articles:</span></span>
- [<span data-ttu-id="a7f35-207">How to evaluate model performance in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7f35-207">How to evaluate model performance in Azure Machine Learning</span></span>](machine-learning-evaluate-model-performance.md)
- [<span data-ttu-id="a7f35-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7f35-208">Choose parameters to optimize your algorithms in Azure Machine Learning</span></span>](machine-learning-algorithm-parameters-optimize.md)
- [<span data-ttu-id="a7f35-209">Interpret model results in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a7f35-209">Interpret model results in Azure Machine Learning</span></span>](machine-learning-interpret-model-results.md)

> [!TIP]
> <span data-ttu-id="a7f35-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span><span class="sxs-lookup"><span data-stu-id="a7f35-210">Each time you run the experiment a record of that iteration is kept in the Run History.</span></span> <span data-ttu-id="a7f35-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-211">You can view these iterations, and return to any of them, by clicking **VIEW RUN HISTORY** below the canvas.</span></span> <span data-ttu-id="a7f35-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span><span class="sxs-lookup"><span data-stu-id="a7f35-212">You can also click **Prior Run** in the **Properties** pane to return to the iteration immediately preceding the one you have open.</span></span>
> 
> <span data-ttu-id="a7f35-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span><span class="sxs-lookup"><span data-stu-id="a7f35-213">You can make a copy of any iteration of your experiment by clicking **SAVE AS** below the canvas.</span></span> 
> <span data-ttu-id="a7f35-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span><span class="sxs-lookup"><span data-stu-id="a7f35-214">Use the experiment's **Summary** and **Description** properties to keep a record of what you've tried in your experiment iterations.</span></span>
> 
> <span data-ttu-id="a7f35-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span><span class="sxs-lookup"><span data-stu-id="a7f35-215">For more details, see [Manage experiment iterations in Azure Machine Learning Studio](machine-learning-manage-experiment-iterations.md).</span></span>  
> 
> 

- - -
<span data-ttu-id="a7f35-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span><span class="sxs-lookup"><span data-stu-id="a7f35-216">**Next: [Deploy the web service](machine-learning-walkthrough-5-publish-web-service.md)**</span></span>

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/train-model-select-column.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/experiment-with-train-model.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/svm-model-added.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/final-experiment.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/roc-curves.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/normalize-data-select-column.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/score-model-connected.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/both-score-models-added.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-walkthrough-4-train-and-evaluate-models/evaluate-model-added.png


<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[normalize-data]: https://msdn.microsoft.com/library/azure/986df333-6748-4b85-923d-871df70d6aaf/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
[two-class-boosted-decision-tree]: https://msdn.microsoft.com/library/azure/e3c522f8-53d9-4829-8ea4-5c6a6b75330c/
[two-class-support-vector-machine]: https://msdn.microsoft.com/library/azure/12d8479b-74b4-4e67-b8de-d32867380e20/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/









