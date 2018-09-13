---
title: Interpret model results in Machine Learning | Microsoft Docs
description: How to choose the optimal parameter set for an algorithm using and visualizing score model outputs.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 820a686ec28843eba01cebd7fdc5e4a117d1a5ed
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549101"
---
# <a name="interpret-model-results-in-azure-machine-learning"></a><span data-ttu-id="633ed-103">Interpret model results in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="633ed-103">Interpret model results in Azure Machine Learning</span></span>
<span data-ttu-id="633ed-104">This topic explains how to visualize and interpret prediction results in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="633ed-104">This topic explains how to visualize and interpret prediction results in Azure Machine Learning Studio.</span></span> <span data-ttu-id="633ed-105">After you have trained a model and done predictions on top of it ("scored the model"), you need to understand and interpret the prediction result.</span><span class="sxs-lookup"><span data-stu-id="633ed-105">After you have trained a model and done predictions on top of it ("scored the model"), you need to understand and interpret the prediction result.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="633ed-106">There are four major kinds of machine learning models in Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="633ed-106">There are four major kinds of machine learning models in Azure Machine Learning:</span></span>

* <span data-ttu-id="633ed-107">Classification</span><span class="sxs-lookup"><span data-stu-id="633ed-107">Classification</span></span>
* <span data-ttu-id="633ed-108">Clustering</span><span class="sxs-lookup"><span data-stu-id="633ed-108">Clustering</span></span>
* <span data-ttu-id="633ed-109">Regression</span><span class="sxs-lookup"><span data-stu-id="633ed-109">Regression</span></span>
* <span data-ttu-id="633ed-110">Recommender systems</span><span class="sxs-lookup"><span data-stu-id="633ed-110">Recommender systems</span></span>

<span data-ttu-id="633ed-111">The modules used for prediction on top of these models are:</span><span class="sxs-lookup"><span data-stu-id="633ed-111">The modules used for prediction on top of these models are:</span></span>

* <span data-ttu-id="633ed-112">[Score Model][score-model] module for classification and regression</span><span class="sxs-lookup"><span data-stu-id="633ed-112">[Score Model][score-model] module for classification and regression</span></span>
* <span data-ttu-id="633ed-113">[Assign to Clusters][assign-to-clusters] module for clustering</span><span class="sxs-lookup"><span data-stu-id="633ed-113">[Assign to Clusters][assign-to-clusters] module for clustering</span></span>
* <span data-ttu-id="633ed-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span><span class="sxs-lookup"><span data-stu-id="633ed-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span></span>

<span data-ttu-id="633ed-115">This document explains how to interpret prediction results for each of these modules.</span><span class="sxs-lookup"><span data-stu-id="633ed-115">This document explains how to interpret prediction results for each of these modules.</span></span> <span data-ttu-id="633ed-116">For an overview of these modules, see [How to choose parameters to optimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span><span class="sxs-lookup"><span data-stu-id="633ed-116">For an overview of these modules, see [How to choose parameters to optimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span></span>

<span data-ttu-id="633ed-117">This topic addresses prediction interpretation but not model evaluation.</span><span class="sxs-lookup"><span data-stu-id="633ed-117">This topic addresses prediction interpretation but not model evaluation.</span></span> <span data-ttu-id="633ed-118">For more information about how to evaluate your model, see [How to evaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span><span class="sxs-lookup"><span data-stu-id="633ed-118">For more information about how to evaluate your model, see [How to evaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span></span>

<span data-ttu-id="633ed-119">If you are new to Azure Machine Learning and need help creating a simple experiment to get started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="633ed-119">If you are new to Azure Machine Learning and need help creating a simple experiment to get started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span></span>

## <a name="classification"></a><span data-ttu-id="633ed-120">Classification</span><span class="sxs-lookup"><span data-stu-id="633ed-120">Classification</span></span>
<span data-ttu-id="633ed-121">There are two subcategories of classification problems:</span><span class="sxs-lookup"><span data-stu-id="633ed-121">There are two subcategories of classification problems:</span></span>

* <span data-ttu-id="633ed-122">Problems with only two classes (two-class or binary classification)</span><span class="sxs-lookup"><span data-stu-id="633ed-122">Problems with only two classes (two-class or binary classification)</span></span>
* <span data-ttu-id="633ed-123">Problems with more than two classes (multi-class classification)</span><span class="sxs-lookup"><span data-stu-id="633ed-123">Problems with more than two classes (multi-class classification)</span></span>

<span data-ttu-id="633ed-124">Azure Machine Learning has different modules to deal with each of these types of classification, but the methods for interpreting their prediction results are similar.</span><span class="sxs-lookup"><span data-stu-id="633ed-124">Azure Machine Learning has different modules to deal with each of these types of classification, but the methods for interpreting their prediction results are similar.</span></span>

### <a name="two-class-classification"></a><span data-ttu-id="633ed-125">Two-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-125">Two-class classification</span></span>
<span data-ttu-id="633ed-126">**Example experiment**</span><span class="sxs-lookup"><span data-stu-id="633ed-126">**Example experiment**</span></span>

<span data-ttu-id="633ed-127">An example of a two-class classification problem is the classification of iris flowers.</span><span class="sxs-lookup"><span data-stu-id="633ed-127">An example of a two-class classification problem is the classification of iris flowers.</span></span> <span data-ttu-id="633ed-128">The task is to classify iris flowers based on their features.</span><span class="sxs-lookup"><span data-stu-id="633ed-128">The task is to classify iris flowers based on their features.</span></span> <span data-ttu-id="633ed-129">The Iris data set provided in Azure Machine Learning is a subset of the popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span><span class="sxs-lookup"><span data-stu-id="633ed-129">The Iris data set provided in Azure Machine Learning is a subset of the popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span></span> <span data-ttu-id="633ed-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span><span class="sxs-lookup"><span data-stu-id="633ed-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span></span>

![Screenshot of iris experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/1.png)

<span data-ttu-id="633ed-132">Figure 1.</span><span class="sxs-lookup"><span data-stu-id="633ed-132">Figure 1.</span></span> <span data-ttu-id="633ed-133">Iris two-class classification problem experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-133">Iris two-class classification problem experiment</span></span>

<span data-ttu-id="633ed-134">An experiment has been performed to solve this problem, as shown in Figure 1.</span><span class="sxs-lookup"><span data-stu-id="633ed-134">An experiment has been performed to solve this problem, as shown in Figure 1.</span></span> <span data-ttu-id="633ed-135">A two-class boosted decision tree model has been trained and scored.</span><span class="sxs-lookup"><span data-stu-id="633ed-135">A two-class boosted decision tree model has been trained and scored.</span></span> <span data-ttu-id="633ed-136">Now you can visualize the prediction results from the [Score Model][score-model] module by clicking the output port of the [Score Model][score-model] module and then clicking **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="633ed-136">Now you can visualize the prediction results from the [Score Model][score-model] module by clicking the output port of the [Score Model][score-model] module and then clicking **Visualize**.</span></span>

![Score model module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/1_1.png)

<span data-ttu-id="633ed-138">This brings up the scoring results as shown in Figure 2.</span><span class="sxs-lookup"><span data-stu-id="633ed-138">This brings up the scoring results as shown in Figure 2.</span></span>

![Results of iris two-class classification experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/2.png)

<span data-ttu-id="633ed-140">Figure 2.</span><span class="sxs-lookup"><span data-stu-id="633ed-140">Figure 2.</span></span> <span data-ttu-id="633ed-141">Visualize a score model result in two-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-141">Visualize a score model result in two-class classification</span></span>

<span data-ttu-id="633ed-142">**Result interpretation**</span><span class="sxs-lookup"><span data-stu-id="633ed-142">**Result interpretation**</span></span>

<span data-ttu-id="633ed-143">There are six columns in the results table.</span><span class="sxs-lookup"><span data-stu-id="633ed-143">There are six columns in the results table.</span></span> <span data-ttu-id="633ed-144">The left four columns are the four features.</span><span class="sxs-lookup"><span data-stu-id="633ed-144">The left four columns are the four features.</span></span> <span data-ttu-id="633ed-145">The right two columns, Scored Labels and Scored Probabilities, are the prediction results.</span><span class="sxs-lookup"><span data-stu-id="633ed-145">The right two columns, Scored Labels and Scored Probabilities, are the prediction results.</span></span> <span data-ttu-id="633ed-146">The Scored Probabilities column shows the probability that a flower belongs to the positive class (Class 1).</span><span class="sxs-lookup"><span data-stu-id="633ed-146">The Scored Probabilities column shows the probability that a flower belongs to the positive class (Class 1).</span></span> <span data-ttu-id="633ed-147">For example, the first number in the column (0.028571) means there is 0.028571 probability that the first flower belongs to Class 1.</span><span class="sxs-lookup"><span data-stu-id="633ed-147">For example, the first number in the column (0.028571) means there is 0.028571 probability that the first flower belongs to Class 1.</span></span> <span data-ttu-id="633ed-148">The Scored Labels column shows the predicted class for each flower.</span><span class="sxs-lookup"><span data-stu-id="633ed-148">The Scored Labels column shows the predicted class for each flower.</span></span> <span data-ttu-id="633ed-149">This is based on the Scored Probabilities column.</span><span class="sxs-lookup"><span data-stu-id="633ed-149">This is based on the Scored Probabilities column.</span></span> <span data-ttu-id="633ed-150">If the scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span><span class="sxs-lookup"><span data-stu-id="633ed-150">If the scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span></span> <span data-ttu-id="633ed-151">Otherwise, it is predicted as Class 0.</span><span class="sxs-lookup"><span data-stu-id="633ed-151">Otherwise, it is predicted as Class 0.</span></span>

<span data-ttu-id="633ed-152">**Web service publication**</span><span class="sxs-lookup"><span data-stu-id="633ed-152">**Web service publication**</span></span>

<span data-ttu-id="633ed-153">After the prediction results have been understood and judged sound, the experiment can be published as a web service so that you can deploy it in various applications and call it to obtain class predictions on any new iris flower.</span><span class="sxs-lookup"><span data-stu-id="633ed-153">After the prediction results have been understood and judged sound, the experiment can be published as a web service so that you can deploy it in various applications and call it to obtain class predictions on any new iris flower.</span></span> <span data-ttu-id="633ed-154">To learn how to change a training experiment into a scoring experiment and publish it as a web service, see [Publish the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="633ed-154">To learn how to change a training experiment into a scoring experiment and publish it as a web service, see [Publish the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span> <span data-ttu-id="633ed-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span><span class="sxs-lookup"><span data-stu-id="633ed-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span></span>

![Screenshot of scoring experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/3.png)

<span data-ttu-id="633ed-157">Figure 3.</span><span class="sxs-lookup"><span data-stu-id="633ed-157">Figure 3.</span></span> <span data-ttu-id="633ed-158">Scoring the iris two-class classification problem experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-158">Scoring the iris two-class classification problem experiment</span></span>

<span data-ttu-id="633ed-159">Now you need to set the input and output for the web service.</span><span class="sxs-lookup"><span data-stu-id="633ed-159">Now you need to set the input and output for the web service.</span></span> <span data-ttu-id="633ed-160">The input is the right input port of [Score Model][score-model], which is the Iris flower features input.</span><span class="sxs-lookup"><span data-stu-id="633ed-160">The input is the right input port of [Score Model][score-model], which is the Iris flower features input.</span></span> <span data-ttu-id="633ed-161">The choice of the output depends on whether you are interested in the predicted class (scored label), the scored probability, or both.</span><span class="sxs-lookup"><span data-stu-id="633ed-161">The choice of the output depends on whether you are interested in the predicted class (scored label), the scored probability, or both.</span></span> <span data-ttu-id="633ed-162">In this example, it is assumed that you are interested in both.</span><span class="sxs-lookup"><span data-stu-id="633ed-162">In this example, it is assumed that you are interested in both.</span></span> <span data-ttu-id="633ed-163">To select the desired output columns, use a [Select Columns in Data set][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="633ed-163">To select the desired output columns, use a [Select Columns in Data set][select-columns] module.</span></span> <span data-ttu-id="633ed-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span><span class="sxs-lookup"><span data-stu-id="633ed-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span></span> <span data-ttu-id="633ed-165">After setting the output port of [Select Columns in Data set][select-columns] and running it again, you should be ready to publish the scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span><span class="sxs-lookup"><span data-stu-id="633ed-165">After setting the output port of [Select Columns in Data set][select-columns] and running it again, you should be ready to publish the scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span></span> <span data-ttu-id="633ed-166">The final experiment looks like Figure 4.</span><span class="sxs-lookup"><span data-stu-id="633ed-166">The final experiment looks like Figure 4.</span></span>

![The iris two-class classification experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/4.png)

<span data-ttu-id="633ed-168">Figure 4.</span><span class="sxs-lookup"><span data-stu-id="633ed-168">Figure 4.</span></span> <span data-ttu-id="633ed-169">Final scoring experiment of an iris two-class classification problem</span><span class="sxs-lookup"><span data-stu-id="633ed-169">Final scoring experiment of an iris two-class classification problem</span></span>

<span data-ttu-id="633ed-170">After you run the web service and enter some feature values of a test instance, the result returns two numbers.</span><span class="sxs-lookup"><span data-stu-id="633ed-170">After you run the web service and enter some feature values of a test instance, the result returns two numbers.</span></span> <span data-ttu-id="633ed-171">The first number is the scored label, and the second is the scored probability.</span><span class="sxs-lookup"><span data-stu-id="633ed-171">The first number is the scored label, and the second is the scored probability.</span></span> <span data-ttu-id="633ed-172">This flower is predicted as Class 1 with 0.9655 probability.</span><span class="sxs-lookup"><span data-stu-id="633ed-172">This flower is predicted as Class 1 with 0.9655 probability.</span></span>

![Test interpreting score model](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/4_1.png)

![Scoring test results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/5.png)

<span data-ttu-id="633ed-175">Figure 5.</span><span class="sxs-lookup"><span data-stu-id="633ed-175">Figure 5.</span></span> <span data-ttu-id="633ed-176">Web service result of iris two-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-176">Web service result of iris two-class classification</span></span>

### <a name="multi-class-classification"></a><span data-ttu-id="633ed-177">Multi-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-177">Multi-class classification</span></span>
<span data-ttu-id="633ed-178">**Example experiment**</span><span class="sxs-lookup"><span data-stu-id="633ed-178">**Example experiment**</span></span>

<span data-ttu-id="633ed-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span><span class="sxs-lookup"><span data-stu-id="633ed-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span></span> <span data-ttu-id="633ed-180">The classifier attempts to predict a certain letter (class) based on some hand-written attribute values extracted from the hand-written images.</span><span class="sxs-lookup"><span data-stu-id="633ed-180">The classifier attempts to predict a certain letter (class) based on some hand-written attribute values extracted from the hand-written images.</span></span>

![Letter recognition example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/5_1.png)

<span data-ttu-id="633ed-182">In the training data, there are 16 features extracted from hand-written letter images.</span><span class="sxs-lookup"><span data-stu-id="633ed-182">In the training data, there are 16 features extracted from hand-written letter images.</span></span> <span data-ttu-id="633ed-183">The 26 letters form our 26 classes.</span><span class="sxs-lookup"><span data-stu-id="633ed-183">The 26 letters form our 26 classes.</span></span> <span data-ttu-id="633ed-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on the same feature set on a test data set.</span><span class="sxs-lookup"><span data-stu-id="633ed-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on the same feature set on a test data set.</span></span>

![Letter recognition multiclass classification experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/6.png)

<span data-ttu-id="633ed-186">Figure 6.</span><span class="sxs-lookup"><span data-stu-id="633ed-186">Figure 6.</span></span> <span data-ttu-id="633ed-187">Letter recognition multiclass classification problem experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-187">Letter recognition multiclass classification problem experiment</span></span>

<span data-ttu-id="633ed-188">Visualizing the results from the [Score Model][score-model] module by clicking the output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span><span class="sxs-lookup"><span data-stu-id="633ed-188">Visualizing the results from the [Score Model][score-model] module by clicking the output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span></span>

![Score model results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/7.png)

<span data-ttu-id="633ed-190">Figure 7.</span><span class="sxs-lookup"><span data-stu-id="633ed-190">Figure 7.</span></span> <span data-ttu-id="633ed-191">Visualize score model results in a multi-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-191">Visualize score model results in a multi-class classification</span></span>

<span data-ttu-id="633ed-192">**Result interpretation**</span><span class="sxs-lookup"><span data-stu-id="633ed-192">**Result interpretation**</span></span>

<span data-ttu-id="633ed-193">The left 16 columns represent the feature values of the test set.</span><span class="sxs-lookup"><span data-stu-id="633ed-193">The left 16 columns represent the feature values of the test set.</span></span> <span data-ttu-id="633ed-194">The columns with names like Scored Probabilities for Class "XX" are just like the Scored Probabilities column in the two-class case.</span><span class="sxs-lookup"><span data-stu-id="633ed-194">The columns with names like Scored Probabilities for Class "XX" are just like the Scored Probabilities column in the two-class case.</span></span> <span data-ttu-id="633ed-195">They show the probability that the corresponding entry falls into a certain class.</span><span class="sxs-lookup"><span data-stu-id="633ed-195">They show the probability that the corresponding entry falls into a certain class.</span></span> <span data-ttu-id="633ed-196">For example, for the first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span><span class="sxs-lookup"><span data-stu-id="633ed-196">For example, for the first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span></span> <span data-ttu-id="633ed-197">The last column (Scored Labels) is the same as Scored Labels in the two-class case.</span><span class="sxs-lookup"><span data-stu-id="633ed-197">The last column (Scored Labels) is the same as Scored Labels in the two-class case.</span></span> <span data-ttu-id="633ed-198">It selects the class with the largest scored probability as the predicted class of the corresponding entry.</span><span class="sxs-lookup"><span data-stu-id="633ed-198">It selects the class with the largest scored probability as the predicted class of the corresponding entry.</span></span> <span data-ttu-id="633ed-199">For example, for the first entry, the scored label is “F” since it has the largest probability to be an “F” (0.916995).</span><span class="sxs-lookup"><span data-stu-id="633ed-199">For example, for the first entry, the scored label is “F” since it has the largest probability to be an “F” (0.916995).</span></span>

<span data-ttu-id="633ed-200">**Web service publication**</span><span class="sxs-lookup"><span data-stu-id="633ed-200">**Web service publication**</span></span>

<span data-ttu-id="633ed-201">You can also get the scored label for each entry and the probability of the scored label.</span><span class="sxs-lookup"><span data-stu-id="633ed-201">You can also get the scored label for each entry and the probability of the scored label.</span></span> <span data-ttu-id="633ed-202">The basic logic is to find the largest probability among all the scored probabilities.</span><span class="sxs-lookup"><span data-stu-id="633ed-202">The basic logic is to find the largest probability among all the scored probabilities.</span></span> <span data-ttu-id="633ed-203">To do this, you need to use the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="633ed-203">To do this, you need to use the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="633ed-204">The R code is shown in Figure 8, and the result of the experiment is shown in Figure 9.</span><span class="sxs-lookup"><span data-stu-id="633ed-204">The R code is shown in Figure 8, and the result of the experiment is shown in Figure 9.</span></span>

![R code example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/8.png)

<span data-ttu-id="633ed-206">Figure 8.</span><span class="sxs-lookup"><span data-stu-id="633ed-206">Figure 8.</span></span> <span data-ttu-id="633ed-207">R code for extracting Scored Labels and the associated probabilities of the labels</span><span class="sxs-lookup"><span data-stu-id="633ed-207">R code for extracting Scored Labels and the associated probabilities of the labels</span></span>

![Experiment result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/9.png)

<span data-ttu-id="633ed-209">Figure 9.</span><span class="sxs-lookup"><span data-stu-id="633ed-209">Figure 9.</span></span> <span data-ttu-id="633ed-210">Final scoring experiment of the letter-recognition multiclass classification problem</span><span class="sxs-lookup"><span data-stu-id="633ed-210">Final scoring experiment of the letter-recognition multiclass classification problem</span></span>

<span data-ttu-id="633ed-211">After you publish and run the web service and enter some input feature values, the returned result looks like Figure 10.</span><span class="sxs-lookup"><span data-stu-id="633ed-211">After you publish and run the web service and enter some input feature values, the returned result looks like Figure 10.</span></span> <span data-ttu-id="633ed-212">This hand-written letter, with its extracted 16 features, is predicted to be a “T” with 0.9715 probability.</span><span class="sxs-lookup"><span data-stu-id="633ed-212">This hand-written letter, with its extracted 16 features, is predicted to be a “T” with 0.9715 probability.</span></span>

![Test interpreting score module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/9_1.png)

![Test result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/10.png)

<span data-ttu-id="633ed-215">Figure 10.</span><span class="sxs-lookup"><span data-stu-id="633ed-215">Figure 10.</span></span> <span data-ttu-id="633ed-216">Web service result of multiclass classification</span><span class="sxs-lookup"><span data-stu-id="633ed-216">Web service result of multiclass classification</span></span>

## <a name="regression"></a><span data-ttu-id="633ed-217">Regression</span><span class="sxs-lookup"><span data-stu-id="633ed-217">Regression</span></span>
<span data-ttu-id="633ed-218">Regression problems are different from classification problems.</span><span class="sxs-lookup"><span data-stu-id="633ed-218">Regression problems are different from classification problems.</span></span> <span data-ttu-id="633ed-219">In a classification problem, you're trying to predict discrete classes, such as which class an iris flower belongs to.</span><span class="sxs-lookup"><span data-stu-id="633ed-219">In a classification problem, you're trying to predict discrete classes, such as which class an iris flower belongs to.</span></span> <span data-ttu-id="633ed-220">But as you can see in the following example of a regression problem, you're trying to predict a continuous variable, such as the price of a car.</span><span class="sxs-lookup"><span data-stu-id="633ed-220">But as you can see in the following example of a regression problem, you're trying to predict a continuous variable, such as the price of a car.</span></span>

<span data-ttu-id="633ed-221">**Example experiment**</span><span class="sxs-lookup"><span data-stu-id="633ed-221">**Example experiment**</span></span>

<span data-ttu-id="633ed-222">Use automobile price prediction as your example for regression.</span><span class="sxs-lookup"><span data-stu-id="633ed-222">Use automobile price prediction as your example for regression.</span></span> <span data-ttu-id="633ed-223">You are trying to predict the price of a car based on its features, including make, fuel type, body type, and drive wheel.</span><span class="sxs-lookup"><span data-stu-id="633ed-223">You are trying to predict the price of a car based on its features, including make, fuel type, body type, and drive wheel.</span></span> <span data-ttu-id="633ed-224">The experiment is shown in Figure 11.</span><span class="sxs-lookup"><span data-stu-id="633ed-224">The experiment is shown in Figure 11.</span></span>

![Automobile price regression experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/11.png)

<span data-ttu-id="633ed-226">Figure 11.</span><span class="sxs-lookup"><span data-stu-id="633ed-226">Figure 11.</span></span> <span data-ttu-id="633ed-227">Automobile price regression problem experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-227">Automobile price regression problem experiment</span></span>

<span data-ttu-id="633ed-228">Visualizing the [Score Model][score-model] module, the result looks like Figure 12.</span><span class="sxs-lookup"><span data-stu-id="633ed-228">Visualizing the [Score Model][score-model] module, the result looks like Figure 12.</span></span>

![Scoring results for automobile price prediction problem](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/12.png)

<span data-ttu-id="633ed-230">Figure 12.</span><span class="sxs-lookup"><span data-stu-id="633ed-230">Figure 12.</span></span> <span data-ttu-id="633ed-231">Scoring result for the automobile price prediction problem</span><span class="sxs-lookup"><span data-stu-id="633ed-231">Scoring result for the automobile price prediction problem</span></span>

<span data-ttu-id="633ed-232">**Result interpretation**</span><span class="sxs-lookup"><span data-stu-id="633ed-232">**Result interpretation**</span></span>

<span data-ttu-id="633ed-233">Scored Labels is the result column in this scoring result.</span><span class="sxs-lookup"><span data-stu-id="633ed-233">Scored Labels is the result column in this scoring result.</span></span> <span data-ttu-id="633ed-234">The numbers are the predicted price for each car.</span><span class="sxs-lookup"><span data-stu-id="633ed-234">The numbers are the predicted price for each car.</span></span>

<span data-ttu-id="633ed-235">**Web service publication**</span><span class="sxs-lookup"><span data-stu-id="633ed-235">**Web service publication**</span></span>

<span data-ttu-id="633ed-236">You can publish the regression experiment into a web service and call it for automobile price prediction in the same way as in the two-class classification use case.</span><span class="sxs-lookup"><span data-stu-id="633ed-236">You can publish the regression experiment into a web service and call it for automobile price prediction in the same way as in the two-class classification use case.</span></span>

![Scoring experiment for automobile price regression problem](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/13.png)

<span data-ttu-id="633ed-238">Figure 13.</span><span class="sxs-lookup"><span data-stu-id="633ed-238">Figure 13.</span></span> <span data-ttu-id="633ed-239">Scoring experiment of an automobile price regression problem</span><span class="sxs-lookup"><span data-stu-id="633ed-239">Scoring experiment of an automobile price regression problem</span></span>

<span data-ttu-id="633ed-240">Running the web service, the returned result looks like Figure 14.</span><span class="sxs-lookup"><span data-stu-id="633ed-240">Running the web service, the returned result looks like Figure 14.</span></span> <span data-ttu-id="633ed-241">The predicted price for this car is $15,085.52.</span><span class="sxs-lookup"><span data-stu-id="633ed-241">The predicted price for this car is $15,085.52.</span></span>

![Test interpreting scoring module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/13_1.png)

![Scoring module results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/14.png)

<span data-ttu-id="633ed-244">Figure 14.</span><span class="sxs-lookup"><span data-stu-id="633ed-244">Figure 14.</span></span> <span data-ttu-id="633ed-245">Web service result of an automobile price regression problem</span><span class="sxs-lookup"><span data-stu-id="633ed-245">Web service result of an automobile price regression problem</span></span>

## <a name="clustering"></a><span data-ttu-id="633ed-246">Clustering</span><span class="sxs-lookup"><span data-stu-id="633ed-246">Clustering</span></span>
<span data-ttu-id="633ed-247">**Example experiment**</span><span class="sxs-lookup"><span data-stu-id="633ed-247">**Example experiment**</span></span>

<span data-ttu-id="633ed-248">Let’s use the Iris data set again to build a clustering experiment.</span><span class="sxs-lookup"><span data-stu-id="633ed-248">Let’s use the Iris data set again to build a clustering experiment.</span></span> <span data-ttu-id="633ed-249">Here you can filter out the class labels in the data set so that it only has features and can be used for clustering.</span><span class="sxs-lookup"><span data-stu-id="633ed-249">Here you can filter out the class labels in the data set so that it only has features and can be used for clustering.</span></span> <span data-ttu-id="633ed-250">In this iris use case, specify the number of clusters to be two during the training process, which means you would cluster the flowers into two classes.</span><span class="sxs-lookup"><span data-stu-id="633ed-250">In this iris use case, specify the number of clusters to be two during the training process, which means you would cluster the flowers into two classes.</span></span> <span data-ttu-id="633ed-251">The experiment is shown in Figure 15.</span><span class="sxs-lookup"><span data-stu-id="633ed-251">The experiment is shown in Figure 15.</span></span>

![Iris clustering problem experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/15.png)

<span data-ttu-id="633ed-253">Figure 15.</span><span class="sxs-lookup"><span data-stu-id="633ed-253">Figure 15.</span></span> <span data-ttu-id="633ed-254">Iris clustering problem experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-254">Iris clustering problem experiment</span></span>

<span data-ttu-id="633ed-255">Clustering differs from classification in that the training data set doesn’t have ground-truth labels by itself.</span><span class="sxs-lookup"><span data-stu-id="633ed-255">Clustering differs from classification in that the training data set doesn’t have ground-truth labels by itself.</span></span> <span data-ttu-id="633ed-256">Clustering groups the training data set instances into distinct clusters.</span><span class="sxs-lookup"><span data-stu-id="633ed-256">Clustering groups the training data set instances into distinct clusters.</span></span> <span data-ttu-id="633ed-257">During the training process, the model labels the entries by learning the differences between their features.</span><span class="sxs-lookup"><span data-stu-id="633ed-257">During the training process, the model labels the entries by learning the differences between their features.</span></span> <span data-ttu-id="633ed-258">After that, the trained model can be used to further classify future entries.</span><span class="sxs-lookup"><span data-stu-id="633ed-258">After that, the trained model can be used to further classify future entries.</span></span> <span data-ttu-id="633ed-259">There are two parts of the result we are interested in within a clustering problem.</span><span class="sxs-lookup"><span data-stu-id="633ed-259">There are two parts of the result we are interested in within a clustering problem.</span></span> <span data-ttu-id="633ed-260">The first part is labeling the training data set, and the second is classifying a new data set with the trained model.</span><span class="sxs-lookup"><span data-stu-id="633ed-260">The first part is labeling the training data set, and the second is classifying a new data set with the trained model.</span></span>

<span data-ttu-id="633ed-261">The first part of the result can be visualized by clicking the left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="633ed-261">The first part of the result can be visualized by clicking the left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span></span> <span data-ttu-id="633ed-262">The visualization is shown in Figure 16.</span><span class="sxs-lookup"><span data-stu-id="633ed-262">The visualization is shown in Figure 16.</span></span>

![Clustering result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/16.png)

<span data-ttu-id="633ed-264">Figure 16.</span><span class="sxs-lookup"><span data-stu-id="633ed-264">Figure 16.</span></span> <span data-ttu-id="633ed-265">Visualize clustering result for the training data set</span><span class="sxs-lookup"><span data-stu-id="633ed-265">Visualize clustering result for the training data set</span></span>

<span data-ttu-id="633ed-266">The result of the second part, clustering new entries with the trained clustering model, is shown in Figure 17.</span><span class="sxs-lookup"><span data-stu-id="633ed-266">The result of the second part, clustering new entries with the trained clustering model, is shown in Figure 17.</span></span>

![Visualize clustering result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/17.png)

<span data-ttu-id="633ed-268">Figure 17.</span><span class="sxs-lookup"><span data-stu-id="633ed-268">Figure 17.</span></span> <span data-ttu-id="633ed-269">Visualize clustering result on a new data set</span><span class="sxs-lookup"><span data-stu-id="633ed-269">Visualize clustering result on a new data set</span></span>

<span data-ttu-id="633ed-270">**Result interpretation**</span><span class="sxs-lookup"><span data-stu-id="633ed-270">**Result interpretation**</span></span>

<span data-ttu-id="633ed-271">Although the results of the two parts stem from different experiment stages, they look the same and are interpreted in the same way.</span><span class="sxs-lookup"><span data-stu-id="633ed-271">Although the results of the two parts stem from different experiment stages, they look the same and are interpreted in the same way.</span></span> <span data-ttu-id="633ed-272">The first four columns are features.</span><span class="sxs-lookup"><span data-stu-id="633ed-272">The first four columns are features.</span></span> <span data-ttu-id="633ed-273">The last column, Assignments, is the prediction result.</span><span class="sxs-lookup"><span data-stu-id="633ed-273">The last column, Assignments, is the prediction result.</span></span> <span data-ttu-id="633ed-274">The entries assigned the same number are predicted to be in the same cluster, that is, they share similarities in some way (this experiment uses the default Euclidean distance metric).</span><span class="sxs-lookup"><span data-stu-id="633ed-274">The entries assigned the same number are predicted to be in the same cluster, that is, they share similarities in some way (this experiment uses the default Euclidean distance metric).</span></span> <span data-ttu-id="633ed-275">Because you specified the number of clusters to be 2, the entries in Assignments are labeled either 0 or 1.</span><span class="sxs-lookup"><span data-stu-id="633ed-275">Because you specified the number of clusters to be 2, the entries in Assignments are labeled either 0 or 1.</span></span>

<span data-ttu-id="633ed-276">**Web service publication**</span><span class="sxs-lookup"><span data-stu-id="633ed-276">**Web service publication**</span></span>

<span data-ttu-id="633ed-277">You can publish the clustering experiment into a web service and call it for clustering predictions the same way as in the two-class classification use case.</span><span class="sxs-lookup"><span data-stu-id="633ed-277">You can publish the clustering experiment into a web service and call it for clustering predictions the same way as in the two-class classification use case.</span></span>

![Scoring experiment for iris clustering problem](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/18.png)

<span data-ttu-id="633ed-279">Figure 18.</span><span class="sxs-lookup"><span data-stu-id="633ed-279">Figure 18.</span></span> <span data-ttu-id="633ed-280">Scoring experiment of an iris clustering problem</span><span class="sxs-lookup"><span data-stu-id="633ed-280">Scoring experiment of an iris clustering problem</span></span>

<span data-ttu-id="633ed-281">After you run the web service, the returned result looks like Figure 19.</span><span class="sxs-lookup"><span data-stu-id="633ed-281">After you run the web service, the returned result looks like Figure 19.</span></span> <span data-ttu-id="633ed-282">This flower is predicted to be in cluster 0.</span><span class="sxs-lookup"><span data-stu-id="633ed-282">This flower is predicted to be in cluster 0.</span></span>

![Test interpret scoring module](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/18_1.png)

![Scoring module result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/19.png)

<span data-ttu-id="633ed-285">Figure 19.</span><span class="sxs-lookup"><span data-stu-id="633ed-285">Figure 19.</span></span> <span data-ttu-id="633ed-286">Web service result of iris two-class classification</span><span class="sxs-lookup"><span data-stu-id="633ed-286">Web service result of iris two-class classification</span></span>

## <a name="recommender-system"></a><span data-ttu-id="633ed-287">Recommender system</span><span class="sxs-lookup"><span data-stu-id="633ed-287">Recommender system</span></span>
<span data-ttu-id="633ed-288">**Example experiment**</span><span class="sxs-lookup"><span data-stu-id="633ed-288">**Example experiment**</span></span>

<span data-ttu-id="633ed-289">For recommender systems, you can use the restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span><span class="sxs-lookup"><span data-stu-id="633ed-289">For recommender systems, you can use the restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span></span> <span data-ttu-id="633ed-290">The input data consists of three parts:</span><span class="sxs-lookup"><span data-stu-id="633ed-290">The input data consists of three parts:</span></span>

* <span data-ttu-id="633ed-291">Restaurant ratings from customers</span><span class="sxs-lookup"><span data-stu-id="633ed-291">Restaurant ratings from customers</span></span>
* <span data-ttu-id="633ed-292">Customer feature data</span><span class="sxs-lookup"><span data-stu-id="633ed-292">Customer feature data</span></span>
* <span data-ttu-id="633ed-293">Restaurant feature data</span><span class="sxs-lookup"><span data-stu-id="633ed-293">Restaurant feature data</span></span>

<span data-ttu-id="633ed-294">There are several things we can do with the [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="633ed-294">There are several things we can do with the [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span></span>

* <span data-ttu-id="633ed-295">Predict ratings for a given user and item</span><span class="sxs-lookup"><span data-stu-id="633ed-295">Predict ratings for a given user and item</span></span>
* <span data-ttu-id="633ed-296">Recommend items to a given user</span><span class="sxs-lookup"><span data-stu-id="633ed-296">Recommend items to a given user</span></span>
* <span data-ttu-id="633ed-297">Find users related to a given user</span><span class="sxs-lookup"><span data-stu-id="633ed-297">Find users related to a given user</span></span>
* <span data-ttu-id="633ed-298">Find items related to a given item</span><span class="sxs-lookup"><span data-stu-id="633ed-298">Find items related to a given item</span></span>

<span data-ttu-id="633ed-299">You can choose what you want to do by selecting from the four options in the **Recommender prediction kind** menu.</span><span class="sxs-lookup"><span data-stu-id="633ed-299">You can choose what you want to do by selecting from the four options in the **Recommender prediction kind** menu.</span></span> <span data-ttu-id="633ed-300">Here you can walk through all four scenarios.</span><span class="sxs-lookup"><span data-stu-id="633ed-300">Here you can walk through all four scenarios.</span></span>

![Matchbox recommender](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/19_1.png)

<span data-ttu-id="633ed-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span><span class="sxs-lookup"><span data-stu-id="633ed-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span></span> <span data-ttu-id="633ed-303">For information about how to use those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span><span class="sxs-lookup"><span data-stu-id="633ed-303">For information about how to use those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span></span>

![Recommender system experiment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/20.png)

<span data-ttu-id="633ed-305">Figure 20.</span><span class="sxs-lookup"><span data-stu-id="633ed-305">Figure 20.</span></span> <span data-ttu-id="633ed-306">Recommender system experiment</span><span class="sxs-lookup"><span data-stu-id="633ed-306">Recommender system experiment</span></span>

<span data-ttu-id="633ed-307">**Result interpretation**</span><span class="sxs-lookup"><span data-stu-id="633ed-307">**Result interpretation**</span></span>

<span data-ttu-id="633ed-308">**Predict ratings for a given user and item**</span><span class="sxs-lookup"><span data-stu-id="633ed-308">**Predict ratings for a given user and item**</span></span>

<span data-ttu-id="633ed-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking the recommender system to predict the rating for a given user and item.</span><span class="sxs-lookup"><span data-stu-id="633ed-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking the recommender system to predict the rating for a given user and item.</span></span> <span data-ttu-id="633ed-310">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span><span class="sxs-lookup"><span data-stu-id="633ed-310">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span></span>

![Score result of the recommender system -- rating prediction](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/21.png)

<span data-ttu-id="633ed-312">Figure 21.</span><span class="sxs-lookup"><span data-stu-id="633ed-312">Figure 21.</span></span> <span data-ttu-id="633ed-313">Visualize the score result of the recommender system--rating prediction</span><span class="sxs-lookup"><span data-stu-id="633ed-313">Visualize the score result of the recommender system--rating prediction</span></span>

<span data-ttu-id="633ed-314">The first two columns are the user-item pairs provided by the input data.</span><span class="sxs-lookup"><span data-stu-id="633ed-314">The first two columns are the user-item pairs provided by the input data.</span></span> <span data-ttu-id="633ed-315">The third column is the predicted rating of a user for a certain item.</span><span class="sxs-lookup"><span data-stu-id="633ed-315">The third column is the predicted rating of a user for a certain item.</span></span> <span data-ttu-id="633ed-316">For example, in the first row, customer U1048 is predicted to rate restaurant 135026 as 2.</span><span class="sxs-lookup"><span data-stu-id="633ed-316">For example, in the first row, customer U1048 is predicted to rate restaurant 135026 as 2.</span></span>

<span data-ttu-id="633ed-317">**Recommend items to a given user**</span><span class="sxs-lookup"><span data-stu-id="633ed-317">**Recommend items to a given user**</span></span>

<span data-ttu-id="633ed-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking the recommender system to recommend items to a given user.</span><span class="sxs-lookup"><span data-stu-id="633ed-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking the recommender system to recommend items to a given user.</span></span> <span data-ttu-id="633ed-319">The last parameter to choose in this scenario is *Recommended item selection*.</span><span class="sxs-lookup"><span data-stu-id="633ed-319">The last parameter to choose in this scenario is *Recommended item selection*.</span></span> <span data-ttu-id="633ed-320">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span><span class="sxs-lookup"><span data-stu-id="633ed-320">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="633ed-321">For this prediction stage, we choose **From All Items**.</span><span class="sxs-lookup"><span data-stu-id="633ed-321">For this prediction stage, we choose **From All Items**.</span></span> <span data-ttu-id="633ed-322">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span><span class="sxs-lookup"><span data-stu-id="633ed-322">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span></span>

![Score result of recommender system -- item recommendation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/22.png)

<span data-ttu-id="633ed-324">Figure 22.</span><span class="sxs-lookup"><span data-stu-id="633ed-324">Figure 22.</span></span> <span data-ttu-id="633ed-325">Visualize score result of the recommender system--item recommendation</span><span class="sxs-lookup"><span data-stu-id="633ed-325">Visualize score result of the recommender system--item recommendation</span></span>

<span data-ttu-id="633ed-326">The first of the six columns represents the given user IDs to recommend items for, as provided by the input data.</span><span class="sxs-lookup"><span data-stu-id="633ed-326">The first of the six columns represents the given user IDs to recommend items for, as provided by the input data.</span></span> <span data-ttu-id="633ed-327">The other five columns represent the items recommended to the user in descending order of relevance.</span><span class="sxs-lookup"><span data-stu-id="633ed-327">The other five columns represent the items recommended to the user in descending order of relevance.</span></span> <span data-ttu-id="633ed-328">For example, in the first row, the most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span><span class="sxs-lookup"><span data-stu-id="633ed-328">For example, in the first row, the most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span></span>

<span data-ttu-id="633ed-329">**Find users related to a given user**</span><span class="sxs-lookup"><span data-stu-id="633ed-329">**Find users related to a given user**</span></span>

<span data-ttu-id="633ed-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking the recommender system to find related users to a given user.</span><span class="sxs-lookup"><span data-stu-id="633ed-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking the recommender system to find related users to a given user.</span></span> <span data-ttu-id="633ed-331">Related users are the users who have similar preferences.</span><span class="sxs-lookup"><span data-stu-id="633ed-331">Related users are the users who have similar preferences.</span></span> <span data-ttu-id="633ed-332">The last parameter to choose in this scenario is *Related user selection*.</span><span class="sxs-lookup"><span data-stu-id="633ed-332">The last parameter to choose in this scenario is *Related user selection*.</span></span> <span data-ttu-id="633ed-333">The option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span><span class="sxs-lookup"><span data-stu-id="633ed-333">The option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="633ed-334">Choose **From All Users** for this prediction stage.</span><span class="sxs-lookup"><span data-stu-id="633ed-334">Choose **From All Users** for this prediction stage.</span></span> <span data-ttu-id="633ed-335">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span><span class="sxs-lookup"><span data-stu-id="633ed-335">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span></span>

![Score result of recommender system --related users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/23.png)

<span data-ttu-id="633ed-337">Figure 23.</span><span class="sxs-lookup"><span data-stu-id="633ed-337">Figure 23.</span></span> <span data-ttu-id="633ed-338">Visualize score results of the recommender system--related users</span><span class="sxs-lookup"><span data-stu-id="633ed-338">Visualize score results of the recommender system--related users</span></span>

<span data-ttu-id="633ed-339">The first of the six columns shows the given user IDs needed to find related users, as provided by input data.</span><span class="sxs-lookup"><span data-stu-id="633ed-339">The first of the six columns shows the given user IDs needed to find related users, as provided by input data.</span></span> <span data-ttu-id="633ed-340">The other five columns store the predicted related users of the user in descending order of relevance.</span><span class="sxs-lookup"><span data-stu-id="633ed-340">The other five columns store the predicted related users of the user in descending order of relevance.</span></span> <span data-ttu-id="633ed-341">For example, in the first row, the most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span><span class="sxs-lookup"><span data-stu-id="633ed-341">For example, in the first row, the most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span></span>

<span data-ttu-id="633ed-342">**Find items related to a given item**</span><span class="sxs-lookup"><span data-stu-id="633ed-342">**Find items related to a given item**</span></span>

<span data-ttu-id="633ed-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking the recommender system to find related items to a given item.</span><span class="sxs-lookup"><span data-stu-id="633ed-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking the recommender system to find related items to a given item.</span></span> <span data-ttu-id="633ed-344">Related items are the items most likely to be liked by the same user.</span><span class="sxs-lookup"><span data-stu-id="633ed-344">Related items are the items most likely to be liked by the same user.</span></span> <span data-ttu-id="633ed-345">The last parameter to choose in this scenario is *Related item selection*.</span><span class="sxs-lookup"><span data-stu-id="633ed-345">The last parameter to choose in this scenario is *Related item selection*.</span></span> <span data-ttu-id="633ed-346">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span><span class="sxs-lookup"><span data-stu-id="633ed-346">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="633ed-347">We choose **From All Items** for this prediction stage.</span><span class="sxs-lookup"><span data-stu-id="633ed-347">We choose **From All Items** for this prediction stage.</span></span> <span data-ttu-id="633ed-348">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span><span class="sxs-lookup"><span data-stu-id="633ed-348">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span></span>

![Score result of recommender system --related items](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/24.png)

<span data-ttu-id="633ed-350">Figure 24.</span><span class="sxs-lookup"><span data-stu-id="633ed-350">Figure 24.</span></span> <span data-ttu-id="633ed-351">Visualize score results of the recommender system--related items</span><span class="sxs-lookup"><span data-stu-id="633ed-351">Visualize score results of the recommender system--related items</span></span>

<span data-ttu-id="633ed-352">The first of the six columns represents the given item IDs needed to find related items, as provided by the input data.</span><span class="sxs-lookup"><span data-stu-id="633ed-352">The first of the six columns represents the given item IDs needed to find related items, as provided by the input data.</span></span> <span data-ttu-id="633ed-353">The other five columns store the predicted related items of the item in descending order in terms of relevance.</span><span class="sxs-lookup"><span data-stu-id="633ed-353">The other five columns store the predicted related items of the item in descending order in terms of relevance.</span></span> <span data-ttu-id="633ed-354">For example, in the first row, the most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span><span class="sxs-lookup"><span data-stu-id="633ed-354">For example, in the first row, the most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span></span>

<span data-ttu-id="633ed-355">**Web service publication**</span><span class="sxs-lookup"><span data-stu-id="633ed-355">**Web service publication**</span></span>

<span data-ttu-id="633ed-356">The process of publishing these experiments as web services to get predictions is similar for each of the four scenarios.</span><span class="sxs-lookup"><span data-stu-id="633ed-356">The process of publishing these experiments as web services to get predictions is similar for each of the four scenarios.</span></span> <span data-ttu-id="633ed-357">Here we take the second scenario (recommend items to a given user) as an example.</span><span class="sxs-lookup"><span data-stu-id="633ed-357">Here we take the second scenario (recommend items to a given user) as an example.</span></span> <span data-ttu-id="633ed-358">You can follow the same procedure with the other three.</span><span class="sxs-lookup"><span data-stu-id="633ed-358">You can follow the same procedure with the other three.</span></span>

<span data-ttu-id="633ed-359">Saving the trained recommender system as a trained model and filtering the input data to a single user ID column as requested, you can hook up the experiment as in Figure 25 and publish it as a web service.</span><span class="sxs-lookup"><span data-stu-id="633ed-359">Saving the trained recommender system as a trained model and filtering the input data to a single user ID column as requested, you can hook up the experiment as in Figure 25 and publish it as a web service.</span></span>

![Scoring experiment of the restaurant recommendation problem](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/25.png)

<span data-ttu-id="633ed-361">Figure 25.</span><span class="sxs-lookup"><span data-stu-id="633ed-361">Figure 25.</span></span> <span data-ttu-id="633ed-362">Scoring experiment of the restaurant recommendation problem</span><span class="sxs-lookup"><span data-stu-id="633ed-362">Scoring experiment of the restaurant recommendation problem</span></span>

<span data-ttu-id="633ed-363">Running the web service, the returned result looks like Figure 26.</span><span class="sxs-lookup"><span data-stu-id="633ed-363">Running the web service, the returned result looks like Figure 26.</span></span> <span data-ttu-id="633ed-364">The five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span><span class="sxs-lookup"><span data-stu-id="633ed-364">The five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span></span>

![Sample of recommender system service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/25_1.png)

![Sample experiment results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-interpret-model-results/26.png)

<span data-ttu-id="633ed-367">Figure 26.</span><span class="sxs-lookup"><span data-stu-id="633ed-367">Figure 26.</span></span> <span data-ttu-id="633ed-368">Web service result of restaurant recommendation problem</span><span class="sxs-lookup"><span data-stu-id="633ed-368">Web service result of restaurant recommendation problem</span></span>

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/


































