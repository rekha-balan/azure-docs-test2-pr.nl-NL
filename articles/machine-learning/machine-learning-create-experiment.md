---
title: A simple experiment in Machine Learning Studio | Microsoft Docs
description: This machine learning tutorial walks you through an easy data science experiment. We'll predict the price of a car using a regression algorithm.
keywords: experiment,linear regression,machine learning algorithms,machine learning tutorial,predictive modeling techniques,data science experiment
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: b73cc7bb28156d32c8b012e2d027594c4c9a03d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564737"
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="1ce59-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="1ce59-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="1ce59-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span><span class="sxs-lookup"><span data-stu-id="1ce59-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="1ce59-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="1ce59-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span><span class="sxs-lookup"><span data-stu-id="1ce59-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce59-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span><span class="sxs-lookup"><span data-stu-id="1ce59-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="1ce59-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span><span class="sxs-lookup"><span data-stu-id="1ce59-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="1ce59-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span><span class="sxs-lookup"><span data-stu-id="1ce59-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="1ce59-112">This video series is a great introduction to machine learning using everyday language and concepts.</span><span class="sxs-lookup"><span data-stu-id="1ce59-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="1ce59-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span><span class="sxs-lookup"><span data-stu-id="1ce59-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="1ce59-114">What is Machine Learning Studio?</span><span class="sxs-lookup"><span data-stu-id="1ce59-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="1ce59-115">- This is a high-level overview of Studio.</span><span class="sxs-lookup"><span data-stu-id="1ce59-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="1ce59-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1ce59-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="1ce59-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span><span class="sxs-lookup"><span data-stu-id="1ce59-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="1ce59-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span><span class="sxs-lookup"><span data-stu-id="1ce59-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="1ce59-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span><span class="sxs-lookup"><span data-stu-id="1ce59-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="1ce59-120">How does Machine Learning Studio help?</span><span class="sxs-lookup"><span data-stu-id="1ce59-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="1ce59-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span><span class="sxs-lookup"><span data-stu-id="1ce59-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="1ce59-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="1ce59-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1ce59-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="1ce59-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span><span class="sxs-lookup"><span data-stu-id="1ce59-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="1ce59-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span><span class="sxs-lookup"><span data-stu-id="1ce59-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="1ce59-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span><span class="sxs-lookup"><span data-stu-id="1ce59-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="1ce59-127">Open Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="1ce59-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="1ce59-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="1ce59-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="1ce59-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="1ce59-130">Otherwise, click **Sign up here** and choose between free and paid options.</span><span class="sxs-lookup"><span data-stu-id="1ce59-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="1ce59-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/>
<span data-ttu-id="1ce59-132">***Sign in to Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="1ce59-132">***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="1ce59-133">Five steps to create an experiment</span><span class="sxs-lookup"><span data-stu-id="1ce59-133">Five steps to create an experiment</span></span>

<span data-ttu-id="1ce59-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span><span class="sxs-lookup"><span data-stu-id="1ce59-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="1ce59-135">**Create a model**</span><span class="sxs-lookup"><span data-stu-id="1ce59-135">**Create a model**</span></span>
    - <span data-ttu-id="1ce59-136">[Step 1: Get data]</span><span class="sxs-lookup"><span data-stu-id="1ce59-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="1ce59-137">[Step 2: Prepare the data]</span><span class="sxs-lookup"><span data-stu-id="1ce59-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="1ce59-138">[Step 3: Define features]</span><span class="sxs-lookup"><span data-stu-id="1ce59-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="1ce59-139">**Train the model**</span><span class="sxs-lookup"><span data-stu-id="1ce59-139">**Train the model**</span></span>
    - <span data-ttu-id="1ce59-140">[Step 4: Choose and apply a learning algorithm]</span><span class="sxs-lookup"><span data-stu-id="1ce59-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="1ce59-141">**Score and test the model**</span><span class="sxs-lookup"><span data-stu-id="1ce59-141">**Score and test the model**</span></span>
    - <span data-ttu-id="1ce59-142">[Step 5: Predict new automobile prices]</span><span class="sxs-lookup"><span data-stu-id="1ce59-142">[Step 5: Predict new automobile prices]</span></span>

[Step 1: Get data]: #step-1-get-data
[Step 2: Prepare the data]: #step-2-prepare-the-data
[Step 3: Define features]: #step-3-define-features
[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm
[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="1ce59-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1ce59-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1ce59-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span><span class="sxs-lookup"><span data-stu-id="1ce59-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="1ce59-150">Step 1: Get data</span><span class="sxs-lookup"><span data-stu-id="1ce59-150">Step 1: Get data</span></span>

<span data-ttu-id="1ce59-151">The first thing you need to perform machine learning is data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="1ce59-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span><span class="sxs-lookup"><span data-stu-id="1ce59-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="1ce59-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span><span class="sxs-lookup"><span data-stu-id="1ce59-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="1ce59-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span><span class="sxs-lookup"><span data-stu-id="1ce59-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="1ce59-155">Here's how to get the dataset into your experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="1ce59-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="1ce59-157">The experiment is given a default name that you can see at the top of the canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="1ce59-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="1ce59-159">The name doesn't need to be unique.</span><span class="sxs-lookup"><span data-stu-id="1ce59-159">The name doesn't need to be unique.</span></span>

    ![Rename the experiment][rename-experiment]

2. <span data-ttu-id="1ce59-161">To the left of the experiment canvas is a palette of datasets and modules.</span><span class="sxs-lookup"><span data-stu-id="1ce59-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="1ce59-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="1ce59-163">Drag this dataset to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="1ce59-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="1ce59-165">***Find the automobile dataset and drag it onto the experiment canvas***</span><span class="sxs-lookup"><span data-stu-id="1ce59-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="1ce59-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="1ce59-167">![Click the output port and select "Visualize"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/>
<span data-ttu-id="1ce59-168">***Click the output port and select "Visualize"***</span><span class="sxs-lookup"><span data-stu-id="1ce59-168">***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="1ce59-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span><span class="sxs-lookup"><span data-stu-id="1ce59-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="1ce59-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span><span class="sxs-lookup"><span data-stu-id="1ce59-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="1ce59-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span><span class="sxs-lookup"><span data-stu-id="1ce59-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="1ce59-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span><span class="sxs-lookup"><span data-stu-id="1ce59-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="1ce59-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span><span class="sxs-lookup"><span data-stu-id="1ce59-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="1ce59-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/>
<span data-ttu-id="1ce59-175">***View the automobile data in the data visualization window***</span><span class="sxs-lookup"><span data-stu-id="1ce59-175">***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="1ce59-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="1ce59-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="1ce59-177">Step 2: Prepare the data</span><span class="sxs-lookup"><span data-stu-id="1ce59-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="1ce59-178">A dataset usually requires some preprocessing before it can be analyzed.</span><span class="sxs-lookup"><span data-stu-id="1ce59-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="1ce59-179">For example, you might have noticed the missing values present in the columns of various rows.</span><span class="sxs-lookup"><span data-stu-id="1ce59-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="1ce59-180">These missing values need to be cleaned so the model can analyze the data correctly.</span><span class="sxs-lookup"><span data-stu-id="1ce59-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="1ce59-181">In our case, we'll remove any rows that have missing values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="1ce59-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span><span class="sxs-lookup"><span data-stu-id="1ce59-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="1ce59-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span><span class="sxs-lookup"><span data-stu-id="1ce59-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="1ce59-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="1ce59-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="1ce59-186">This module allows us to select which columns of data we want to include or exclude in the model.</span><span class="sxs-lookup"><span data-stu-id="1ce59-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="1ce59-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="1ce59-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="1ce59-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span><span class="sxs-lookup"><span data-stu-id="1ce59-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="1ce59-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span><span class="sxs-lookup"><span data-stu-id="1ce59-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="1ce59-191">On the left, click **With rules**</span><span class="sxs-lookup"><span data-stu-id="1ce59-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="1ce59-192">Under **Begin With**, click **All columns**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="1ce59-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span><span class="sxs-lookup"><span data-stu-id="1ce59-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="1ce59-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span><span class="sxs-lookup"><span data-stu-id="1ce59-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="1ce59-195">A list of columns is displayed.</span><span class="sxs-lookup"><span data-stu-id="1ce59-195">A list of columns is displayed.</span></span> <span data-ttu-id="1ce59-196">Select **normalized-losses**, and it's added to the text box.</span><span class="sxs-lookup"><span data-stu-id="1ce59-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="1ce59-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span><span class="sxs-lookup"><span data-stu-id="1ce59-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="1ce59-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="1ce59-199">***Launch the column selector and exclude the "normalized-losses" column***</span><span class="sxs-lookup"><span data-stu-id="1ce59-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="1ce59-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="1ce59-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="1ce59-202">***The properties pane shows that the "normalized-losses" column is excluded***</span><span class="sxs-lookup"><span data-stu-id="1ce59-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="1ce59-203">You can add a comment to a module by double-clicking the module and entering text.</span><span class="sxs-lookup"><span data-stu-id="1ce59-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="1ce59-204">This can help you see at a glance what the module is doing in your experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="1ce59-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span><span class="sxs-lookup"><span data-stu-id="1ce59-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="1ce59-206">![Double-click a module to add a comment][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="1ce59-207">***Double-click a module to add a comment***</span><span class="sxs-lookup"><span data-stu-id="1ce59-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="1ce59-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="1ce59-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="1ce59-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="1ce59-211">Double-click the module and type the comment "Remove missing value rows."</span><span class="sxs-lookup"><span data-stu-id="1ce59-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="1ce59-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="1ce59-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span><span class="sxs-lookup"><span data-stu-id="1ce59-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="1ce59-214">Run the experiment by clicking **RUN** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1ce59-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="1ce59-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span><span class="sxs-lookup"><span data-stu-id="1ce59-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="1ce59-216">Notice also the **Finished running** status in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="1ce59-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="1ce59-217">![After running it, the experiment should look something like this][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/>
<span data-ttu-id="1ce59-218">***After running it, the experiment should look something like this***</span><span class="sxs-lookup"><span data-stu-id="1ce59-218">***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="1ce59-219">Why did we run the experiment now?</span><span class="sxs-lookup"><span data-stu-id="1ce59-219">Why did we run the experiment now?</span></span> <span data-ttu-id="1ce59-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="1ce59-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span><span class="sxs-lookup"><span data-stu-id="1ce59-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="1ce59-222">All we have done in the experiment up to this point is clean the data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="1ce59-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="1ce59-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="1ce59-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span><span class="sxs-lookup"><span data-stu-id="1ce59-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="1ce59-226">Step 3: Define features</span><span class="sxs-lookup"><span data-stu-id="1ce59-226">Step 3: Define features</span></span>

<span data-ttu-id="1ce59-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span><span class="sxs-lookup"><span data-stu-id="1ce59-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="1ce59-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span><span class="sxs-lookup"><span data-stu-id="1ce59-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="1ce59-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span><span class="sxs-lookup"><span data-stu-id="1ce59-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="1ce59-230">Some features are better for predicting the target than others.</span><span class="sxs-lookup"><span data-stu-id="1ce59-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="1ce59-231">Also, some features have a strong correlation with other features and can be removed.</span><span class="sxs-lookup"><span data-stu-id="1ce59-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="1ce59-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span><span class="sxs-lookup"><span data-stu-id="1ce59-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="1ce59-233">Let's build a model that uses a subset of the features in our dataset.</span><span class="sxs-lookup"><span data-stu-id="1ce59-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="1ce59-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span><span class="sxs-lookup"><span data-stu-id="1ce59-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="1ce59-235">But to start, let's try the following features:</span><span class="sxs-lookup"><span data-stu-id="1ce59-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="1ce59-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="1ce59-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="1ce59-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="1ce59-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span><span class="sxs-lookup"><span data-stu-id="1ce59-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="1ce59-240">Double-click the module and type "Select features for prediction."</span><span class="sxs-lookup"><span data-stu-id="1ce59-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="1ce59-241">Click **Launch column selector** in the **Properties** pane.</span><span class="sxs-lookup"><span data-stu-id="1ce59-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="1ce59-242">Click **With rules**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-242">Click **With rules**.</span></span>

4. <span data-ttu-id="1ce59-243">Under **Begin With**, click **No columns**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="1ce59-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span><span class="sxs-lookup"><span data-stu-id="1ce59-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="1ce59-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span><span class="sxs-lookup"><span data-stu-id="1ce59-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="1ce59-246">Click the check mark (OK) button.</span><span class="sxs-lookup"><span data-stu-id="1ce59-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="1ce59-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="1ce59-248">***Select the columns (features) to include in the prediction***</span><span class="sxs-lookup"><span data-stu-id="1ce59-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="1ce59-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span><span class="sxs-lookup"><span data-stu-id="1ce59-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="1ce59-250">Later, you can return and try again with a different selection of features.</span><span class="sxs-lookup"><span data-stu-id="1ce59-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="1ce59-251">Step 4: Choose and apply a learning algorithm</span><span class="sxs-lookup"><span data-stu-id="1ce59-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="1ce59-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span><span class="sxs-lookup"><span data-stu-id="1ce59-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="1ce59-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span><span class="sxs-lookup"><span data-stu-id="1ce59-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="1ce59-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span><span class="sxs-lookup"><span data-stu-id="1ce59-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="1ce59-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span><span class="sxs-lookup"><span data-stu-id="1ce59-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="1ce59-256">Regression is used to predict a number.</span><span class="sxs-lookup"><span data-stu-id="1ce59-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="1ce59-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span><span class="sxs-lookup"><span data-stu-id="1ce59-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="1ce59-258">For this example, we'll use a simple *linear regression* model.</span><span class="sxs-lookup"><span data-stu-id="1ce59-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="1ce59-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span><span class="sxs-lookup"><span data-stu-id="1ce59-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="1ce59-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span><span class="sxs-lookup"><span data-stu-id="1ce59-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="1ce59-261">We train the model by giving it a set of data that includes the price.</span><span class="sxs-lookup"><span data-stu-id="1ce59-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="1ce59-262">The model scans the data and look for correlations between an automobile's features and its price.</span><span class="sxs-lookup"><span data-stu-id="1ce59-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="1ce59-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span><span class="sxs-lookup"><span data-stu-id="1ce59-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="1ce59-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span><span class="sxs-lookup"><span data-stu-id="1ce59-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="1ce59-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="1ce59-266">Click the [Split Data][split] module to select it.</span><span class="sxs-lookup"><span data-stu-id="1ce59-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="1ce59-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span><span class="sxs-lookup"><span data-stu-id="1ce59-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="1ce59-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span><span class="sxs-lookup"><span data-stu-id="1ce59-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="1ce59-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="1ce59-270">***Set the split fraction of the "Split Data" module to 0.75***</span><span class="sxs-lookup"><span data-stu-id="1ce59-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="1ce59-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span><span class="sxs-lookup"><span data-stu-id="1ce59-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="1ce59-272">This parameter controls the seeding of the pseudo-random number generator.</span><span class="sxs-lookup"><span data-stu-id="1ce59-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="1ce59-273">Run the experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-273">Run the experiment.</span></span> <span data-ttu-id="1ce59-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span><span class="sxs-lookup"><span data-stu-id="1ce59-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="1ce59-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="1ce59-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span><span class="sxs-lookup"><span data-stu-id="1ce59-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="1ce59-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="1ce59-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span><span class="sxs-lookup"><span data-stu-id="1ce59-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="1ce59-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="1ce59-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="1ce59-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="1ce59-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span><span class="sxs-lookup"><span data-stu-id="1ce59-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="1ce59-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span><span class="sxs-lookup"><span data-stu-id="1ce59-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="1ce59-284">This is the value that our model is going to predict.</span><span class="sxs-lookup"><span data-stu-id="1ce59-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="1ce59-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span><span class="sxs-lookup"><span data-stu-id="1ce59-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="1ce59-286">![Select the price column for the "Train Model" module][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="1ce59-287">***Select the price column for the "Train Model" module***</span><span class="sxs-lookup"><span data-stu-id="1ce59-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="1ce59-288">Run the experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-288">Run the experiment.</span></span>

<span data-ttu-id="1ce59-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span><span class="sxs-lookup"><span data-stu-id="1ce59-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="1ce59-290">![After running, the experiment should now look something like this][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/>
<span data-ttu-id="1ce59-291">***After running, the experiment should now look something like this***</span><span class="sxs-lookup"><span data-stu-id="1ce59-291">***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="1ce59-292">Step 5: Predict new automobile prices</span><span class="sxs-lookup"><span data-stu-id="1ce59-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="1ce59-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span><span class="sxs-lookup"><span data-stu-id="1ce59-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="1ce59-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="1ce59-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="1ce59-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="1ce59-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="1ce59-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span><span class="sxs-lookup"><span data-stu-id="1ce59-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="1ce59-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="1ce59-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span><span class="sxs-lookup"><span data-stu-id="1ce59-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="1ce59-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span><span class="sxs-lookup"><span data-stu-id="1ce59-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="1ce59-300">The output shows the predicted values for price and the known values from the test data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="1ce59-301">![Output of the "Score Model" module][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="1ce59-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="1ce59-302">***Output of the "Score Model" module***</span><span class="sxs-lookup"><span data-stu-id="1ce59-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="1ce59-303">Finally, we test the quality of the results.</span><span class="sxs-lookup"><span data-stu-id="1ce59-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="1ce59-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span><span class="sxs-lookup"><span data-stu-id="1ce59-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="1ce59-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span><span class="sxs-lookup"><span data-stu-id="1ce59-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="1ce59-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span><span class="sxs-lookup"><span data-stu-id="1ce59-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="1ce59-307">Run the experiment.</span><span class="sxs-lookup"><span data-stu-id="1ce59-307">Run the experiment.</span></span>

<span data-ttu-id="1ce59-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="1ce59-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="1ce59-309">![Evaluation results for the experiment][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/>
<span data-ttu-id="1ce59-310">***Evaluation results for the experiment***</span><span class="sxs-lookup"><span data-stu-id="1ce59-310">***Evaluation results for the experiment***</span></span>

<span data-ttu-id="1ce59-311">The following statistics are shown for our model:</span><span class="sxs-lookup"><span data-stu-id="1ce59-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="1ce59-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span><span class="sxs-lookup"><span data-stu-id="1ce59-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="1ce59-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span><span class="sxs-lookup"><span data-stu-id="1ce59-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="1ce59-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="1ce59-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="1ce59-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="1ce59-317">For each of the error statistics, smaller is better.</span><span class="sxs-lookup"><span data-stu-id="1ce59-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="1ce59-318">A smaller value indicates that the predictions more closely match the actual values.</span><span class="sxs-lookup"><span data-stu-id="1ce59-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="1ce59-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span><span class="sxs-lookup"><span data-stu-id="1ce59-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="1ce59-320">Final experiment</span><span class="sxs-lookup"><span data-stu-id="1ce59-320">Final experiment</span></span>

<span data-ttu-id="1ce59-321">The final experiment should look something like this:</span><span class="sxs-lookup"><span data-stu-id="1ce59-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="1ce59-322">![The final experiment][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="1ce59-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/>
<span data-ttu-id="1ce59-323">***The final experiment***</span><span class="sxs-lookup"><span data-stu-id="1ce59-323">***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ce59-324">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ce59-324">Next steps</span></span>

<span data-ttu-id="1ce59-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span><span class="sxs-lookup"><span data-stu-id="1ce59-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="1ce59-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span><span class="sxs-lookup"><span data-stu-id="1ce59-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="1ce59-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span><span class="sxs-lookup"><span data-stu-id="1ce59-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="1ce59-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span><span class="sxs-lookup"><span data-stu-id="1ce59-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="1ce59-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="1ce59-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="1ce59-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1ce59-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="1ce59-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="1ce59-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="1ce59-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span><span class="sxs-lookup"><span data-stu-id="1ce59-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="1ce59-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span><span class="sxs-lookup"><span data-stu-id="1ce59-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="1ce59-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span><span class="sxs-lookup"><span data-stu-id="1ce59-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="1ce59-335">Want to learn more?</span><span class="sxs-lookup"><span data-stu-id="1ce59-335">Want to learn more?</span></span> <span data-ttu-id="1ce59-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="1ce59-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[connect-train-model]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/





















