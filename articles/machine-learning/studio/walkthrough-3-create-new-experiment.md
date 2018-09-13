---
title: 'Step 3: Create a new Machine Learning experiment | Microsoft Docs'
description: 'Step 3 of the Develop a predictive solution walkthrough: Create a new training experiment in Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 660e3c27-55ef-4c33-a4e9-dff4d1224630
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.openlocfilehash: 95000f9fb57b95bf1edcda9abfba3668b5f5b523
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865734"
---
# <a name="walkthrough-step-3-create-a-new-azure-machine-learning-experiment"></a><span data-ttu-id="f049c-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span><span class="sxs-lookup"><span data-stu-id="f049c-103">Walkthrough Step 3: Create a new Azure Machine Learning experiment</span></span>
<span data-ttu-id="f049c-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="f049c-104">This is the third step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="f049c-105">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="f049c-105">Create a Machine Learning workspace</span></span>](walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="f049c-106">Upload existing data</span><span class="sxs-lookup"><span data-stu-id="f049c-106">Upload existing data</span></span>](walkthrough-2-upload-data.md)
3. <span data-ttu-id="f049c-107">**Create a new experiment**</span><span class="sxs-lookup"><span data-stu-id="f049c-107">**Create a new experiment**</span></span>
4. [<span data-ttu-id="f049c-108">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="f049c-108">Train and evaluate the models</span></span>](walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="f049c-109">Deploy the Web service</span><span class="sxs-lookup"><span data-stu-id="f049c-109">Deploy the Web service</span></span>](walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="f049c-110">Access the Web service</span><span class="sxs-lookup"><span data-stu-id="f049c-110">Access the Web service</span></span>](walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="f049c-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span><span class="sxs-lookup"><span data-stu-id="f049c-111">The next step in this walkthrough is to create an experiment in Machine Learning Studio that uses the dataset we uploaded.</span></span>  

1. <span data-ttu-id="f049c-112">In Studio, click **+NEW** at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="f049c-112">In Studio, click **+NEW** at the bottom of the window.</span></span>
2. <span data-ttu-id="f049c-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span><span class="sxs-lookup"><span data-stu-id="f049c-113">Select **EXPERIMENT**, and then select "Blank Experiment".</span></span> 

    ![Create a new experiment][0]

2. <span data-ttu-id="f049c-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span><span class="sxs-lookup"><span data-stu-id="f049c-115">Select the default experiment name at the top of the canvas and rename it to something meaningful.</span></span>

    ![Rename experiment][5]
   
   > [!TIP]
   > <span data-ttu-id="f049c-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span><span class="sxs-lookup"><span data-stu-id="f049c-117">It's a good practice to fill in **Summary** and **Description** for the experiment in the **Properties** pane.</span></span> <span data-ttu-id="f049c-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span><span class="sxs-lookup"><span data-stu-id="f049c-118">These properties give you the chance to document the experiment so that anyone who looks at it later will understand your goals and methodology.</span></span>
   > 
   > ![Experiment properties][6]
   > 
3. <span data-ttu-id="f049c-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span><span class="sxs-lookup"><span data-stu-id="f049c-120">In the module palette to the left of the experiment canvas, expand **Saved Datasets**.</span></span>
4. <span data-ttu-id="f049c-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span><span class="sxs-lookup"><span data-stu-id="f049c-121">Find the dataset you created under **My Datasets** and drag it onto the canvas.</span></span> <span data-ttu-id="f049c-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span><span class="sxs-lookup"><span data-stu-id="f049c-122">You can also find the dataset by entering the name in the **Search** box above the palette.</span></span>  

    ![Add the dataset to the experiment][7]

## <a name="prepare-the-data"></a><span data-ttu-id="f049c-124">Prepare the data</span><span class="sxs-lookup"><span data-stu-id="f049c-124">Prepare the data</span></span>
<span data-ttu-id="f049c-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="f049c-125">You can view the first 100 rows of the data and some statistical information for the whole dataset: Click the output port of the dataset (the small circle at the bottom) and select **Visualize**.</span></span>  

<span data-ttu-id="f049c-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span><span class="sxs-lookup"><span data-stu-id="f049c-126">Because the data file didn't come with column headings, Studio has provided generic headings (Col1, Col2, *etc.*).</span></span> <span data-ttu-id="f049c-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span><span class="sxs-lookup"><span data-stu-id="f049c-127">Good headings aren't essential to creating a model, but they make it easier to work with the data in the experiment.</span></span> <span data-ttu-id="f049c-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span><span class="sxs-lookup"><span data-stu-id="f049c-128">Also, when we eventually publish this model in a web service, the headings help identify the columns to the user of the service.</span></span>  

<span data-ttu-id="f049c-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-129">We can add column headings using the [Edit Metadata][edit-metadata] module.</span></span>
<span data-ttu-id="f049c-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span><span class="sxs-lookup"><span data-stu-id="f049c-130">You use the [Edit Metadata][edit-metadata] module to change metadata associated with a dataset.</span></span> <span data-ttu-id="f049c-131">In this case, we use it to provide more friendly names for column headings.</span><span class="sxs-lookup"><span data-stu-id="f049c-131">In this case, we use it to provide more friendly names for column headings.</span></span> 

<span data-ttu-id="f049c-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span><span class="sxs-lookup"><span data-stu-id="f049c-132">To use [Edit Metadata][edit-metadata], you first specify which columns to modify (in this case, all of them.) Next, you specify the action to be performed on those columns (in this case, changing column headings.)</span></span>

1. <span data-ttu-id="f049c-133">In the module palette, type "metadata" in the **Search** box.</span><span class="sxs-lookup"><span data-stu-id="f049c-133">In the module palette, type "metadata" in the **Search** box.</span></span> <span data-ttu-id="f049c-134">The [Edit Metadata][edit-metadata] appears in the module list.</span><span class="sxs-lookup"><span data-stu-id="f049c-134">The [Edit Metadata][edit-metadata] appears in the module list.</span></span>

2. <span data-ttu-id="f049c-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span><span class="sxs-lookup"><span data-stu-id="f049c-135">Click and drag the [Edit Metadata][edit-metadata] module onto the canvas and drop it below the dataset we added earlier.</span></span>

3. <span data-ttu-id="f049c-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span><span class="sxs-lookup"><span data-stu-id="f049c-136">Connect the dataset to the [Edit Metadata][edit-metadata]: click the output port of the dataset (the small circle at the bottom of the dataset), drag to the input port of [Edit Metadata][edit-metadata] (the small circle at the top of the module), then release the mouse button.</span></span> <span data-ttu-id="f049c-137">The dataset and module remain connected even if you move either around on the canvas.</span><span class="sxs-lookup"><span data-stu-id="f049c-137">The dataset and module remain connected even if you move either around on the canvas.</span></span>
   
   <span data-ttu-id="f049c-138">The experiment should now look something like this:</span><span class="sxs-lookup"><span data-stu-id="f049c-138">The experiment should now look something like this:</span></span>  
   
   ![Adding Edit Metadata][1]
   
   <span data-ttu-id="f049c-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span><span class="sxs-lookup"><span data-stu-id="f049c-140">The red exclamation mark indicates that we haven't set the properties for this module yet.</span></span> <span data-ttu-id="f049c-141">We'll do that next.</span><span class="sxs-lookup"><span data-stu-id="f049c-141">We'll do that next.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f049c-142">You can add a comment to a module by double-clicking the module and entering text.</span><span class="sxs-lookup"><span data-stu-id="f049c-142">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="f049c-143">This can help you see at a glance what the module is doing in your experiment.</span><span class="sxs-lookup"><span data-stu-id="f049c-143">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="f049c-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span><span class="sxs-lookup"><span data-stu-id="f049c-144">In this case, double-click the [Edit Metadata][edit-metadata] module and type the comment "Add column headings".</span></span> <span data-ttu-id="f049c-145">Click anywhere else on the canvas to close the text box.</span><span class="sxs-lookup"><span data-stu-id="f049c-145">Click anywhere else on the canvas to close the text box.</span></span> <span data-ttu-id="f049c-146">To display the comment, click the down-arrow on the module.</span><span class="sxs-lookup"><span data-stu-id="f049c-146">To display the comment, click the down-arrow on the module.</span></span>
   > 
   > ![Edit Metadata module with comment added][8]
   > 
4. <span data-ttu-id="f049c-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span><span class="sxs-lookup"><span data-stu-id="f049c-148">Select [Edit Metadata][edit-metadata], and in the **Properties** pane to the right of the canvas, click **Launch column selector**.</span></span>

5. <span data-ttu-id="f049c-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span><span class="sxs-lookup"><span data-stu-id="f049c-149">In the **Select columns** dialog, select all the rows in **Available Columns** and click > to move them to **Selected Columns**.</span></span>
   <span data-ttu-id="f049c-150">The dialog should look like this:</span><span class="sxs-lookup"><span data-stu-id="f049c-150">The dialog should look like this:</span></span>

   ![Column Selector with all columns selected][2]

6. <span data-ttu-id="f049c-152">Click the **OK** check mark.</span><span class="sxs-lookup"><span data-stu-id="f049c-152">Click the **OK** check mark.</span></span>

7. <span data-ttu-id="f049c-153">Back in the **Properties** pane, look for the **New column names** parameter.</span><span class="sxs-lookup"><span data-stu-id="f049c-153">Back in the **Properties** pane, look for the **New column names** parameter.</span></span> <span data-ttu-id="f049c-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span><span class="sxs-lookup"><span data-stu-id="f049c-154">In this field, enter a list of names for the 21 columns in the dataset, separated by commas and in column order.</span></span> <span data-ttu-id="f049c-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span><span class="sxs-lookup"><span data-stu-id="f049c-155">You can obtain the columns names from the dataset documentation on the UCI website, or for convenience you can copy and paste the following list:</span></span>  
   
       Status of checking account, Duration in months, Credit history, Purpose, Credit amount, Savings account/bond, Present employment since, Installment rate in percentage of disposable income, Personal status and sex, Other debtors, Present residence since, Property, Age in years, Other installment plans, Housing, Number of existing credits, Job, Number of people providing maintenance for, Telephone, Foreign worker, Credit risk  
   
   <span data-ttu-id="f049c-156">The Properties pane looks like this:</span><span class="sxs-lookup"><span data-stu-id="f049c-156">The Properties pane looks like this:</span></span>
   
   ![Properties for Edit Metadata][3]

> [!TIP]
> <span data-ttu-id="f049c-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span><span class="sxs-lookup"><span data-stu-id="f049c-158">If you want to verify the column headings, run the experiment (click **RUN** below the experiment canvas).</span></span> <span data-ttu-id="f049c-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="f049c-159">When it finishes running (a green check mark appears on [Edit Metadata][edit-metadata]), click the output port of the [Edit Metadata][edit-metadata] module, and select **Visualize**.</span></span> <span data-ttu-id="f049c-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span><span class="sxs-lookup"><span data-stu-id="f049c-160">You can view the output of any module in the same way to view the progress of the data through the experiment.</span></span>
> 
> 

## <a name="create-training-and-test-datasets"></a><span data-ttu-id="f049c-161">Create training and test datasets</span><span class="sxs-lookup"><span data-stu-id="f049c-161">Create training and test datasets</span></span>
<span data-ttu-id="f049c-162">We need some data to train the model and some to test it.</span><span class="sxs-lookup"><span data-stu-id="f049c-162">We need some data to train the model and some to test it.</span></span>
<span data-ttu-id="f049c-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span><span class="sxs-lookup"><span data-stu-id="f049c-163">So in the next step of the experiment, we split the dataset into two separate datasets: one for training our model and one for testing it.</span></span>

<span data-ttu-id="f049c-164">To do this, we use the [Split Data][split] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-164">To do this, we use the [Split Data][split] module.</span></span>  

1. <span data-ttu-id="f049c-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-165">Find the [Split Data][split] module, drag it onto the canvas, and connect it to the [Edit Metadata][edit-metadata] module.</span></span>

2. <span data-ttu-id="f049c-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span><span class="sxs-lookup"><span data-stu-id="f049c-166">By default, the split ratio is 0.5 and the **Randomized split** parameter is set.</span></span> <span data-ttu-id="f049c-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span><span class="sxs-lookup"><span data-stu-id="f049c-167">This means that a random half of the data is output through one port of the [Split Data][split] module, and half through the other.</span></span> <span data-ttu-id="f049c-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span><span class="sxs-lookup"><span data-stu-id="f049c-168">You can adjust these parameters, as well as the **Random seed** parameter, to change the split between training and testing data.</span></span> <span data-ttu-id="f049c-169">For this example, we leave them as-is.</span><span class="sxs-lookup"><span data-stu-id="f049c-169">For this example, we leave them as-is.</span></span>
   
   > [!TIP]
   > <span data-ttu-id="f049c-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span><span class="sxs-lookup"><span data-stu-id="f049c-170">The property **Fraction of rows in the first output dataset** determines how much of the data is output through the *left* output port.</span></span> <span data-ttu-id="f049c-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span><span class="sxs-lookup"><span data-stu-id="f049c-171">For instance, if you set the ratio to 0.7, then 70% of the data is output through the left port and 30% through the right port.</span></span>  
   > 
   > 

3. <span data-ttu-id="f049c-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span><span class="sxs-lookup"><span data-stu-id="f049c-172">Double-click the [Split Data][split] module and enter the comment, "Training/testing data split 50%".</span></span> 

<span data-ttu-id="f049c-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span><span class="sxs-lookup"><span data-stu-id="f049c-173">We can use the outputs of the [Split Data][split] module however we like, but let's choose to use the left output as training data and the right output as testing data.</span></span>  

<span data-ttu-id="f049c-174">As mentioned in the [previous step](walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span><span class="sxs-lookup"><span data-stu-id="f049c-174">As mentioned in the [previous step](walkthrough-2-upload-data.md), the cost of misclassifying a high credit risk as low is five times higher than the cost of misclassifying a low credit risk as high.</span></span> <span data-ttu-id="f049c-175">To account for this, we generate a new dataset that reflects this cost function.</span><span class="sxs-lookup"><span data-stu-id="f049c-175">To account for this, we generate a new dataset that reflects this cost function.</span></span> <span data-ttu-id="f049c-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span><span class="sxs-lookup"><span data-stu-id="f049c-176">In the new dataset, each high risk example is replicated five times, while each low risk example is not replicated.</span></span>   

<span data-ttu-id="f049c-177">We can do this replication using R code:</span><span class="sxs-lookup"><span data-stu-id="f049c-177">We can do this replication using R code:</span></span>  

1. <span data-ttu-id="f049c-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="f049c-178">Find and drag the [Execute R Script][execute-r-script] module onto the experiment canvas.</span></span> 

2. <span data-ttu-id="f049c-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-179">Connect the left output port of the [Split Data][split] module to the first input port ("Dataset1") of the [Execute R Script][execute-r-script] module.</span></span>

3. <span data-ttu-id="f049c-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span><span class="sxs-lookup"><span data-stu-id="f049c-180">Double-click the [Execute R Script][execute-r-script] module and enter the comment, "Set cost adjustment".</span></span>

4. <span data-ttu-id="f049c-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span><span class="sxs-lookup"><span data-stu-id="f049c-181">In the **Properties** pane, delete the default text in the **R Script** parameter and enter this script:</span></span>
   
       dataset1 <- maml.mapInputPort(1)
       data.set<-dataset1[dataset1[,21]==1,]
       pos<-dataset1[dataset1[,21]==2,]
       for (i in 1:5) data.set<-rbind(data.set,pos)
       maml.mapOutputPort("data.set")

    ![R script in the Execute R Script module][9]

<span data-ttu-id="f049c-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span><span class="sxs-lookup"><span data-stu-id="f049c-183">We need to do this same replication operation for each output of the [Split Data][split] module so that the training and testing data have the same cost adjustment.</span></span> <span data-ttu-id="f049c-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-184">The easiest way to do this is by duplicating the [Execute R Script][execute-r-script] module we just made and connecting it to the other output port of the [Split Data][split] module.</span></span>

1. <span data-ttu-id="f049c-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span><span class="sxs-lookup"><span data-stu-id="f049c-185">Right-click the [Execute R Script][execute-r-script] module and select **Copy**.</span></span>

2. <span data-ttu-id="f049c-186">Right-click the experiment canvas and select **Paste**.</span><span class="sxs-lookup"><span data-stu-id="f049c-186">Right-click the experiment canvas and select **Paste**.</span></span>

3. <span data-ttu-id="f049c-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span><span class="sxs-lookup"><span data-stu-id="f049c-187">Drag the new module into position, and then connect the right output port of the [Split Data][split] module to the first input port of this new [Execute R Script][execute-r-script] module.</span></span> 

4. <span data-ttu-id="f049c-188">At the bottom of the canvas, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="f049c-188">At the bottom of the canvas, click **Run**.</span></span> 

> [!TIP]
> <span data-ttu-id="f049c-189">The copy of the Execute R Script module contains the same script as the original module.</span><span class="sxs-lookup"><span data-stu-id="f049c-189">The copy of the Execute R Script module contains the same script as the original module.</span></span> <span data-ttu-id="f049c-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span><span class="sxs-lookup"><span data-stu-id="f049c-190">When you copy and paste a module on the canvas, the copy retains all the properties of the original.</span></span>  
> 
> 

<span data-ttu-id="f049c-191">Our experiment now looks something like this:</span><span class="sxs-lookup"><span data-stu-id="f049c-191">Our experiment now looks something like this:</span></span>

![Adding Split module and R scripts][4]

<span data-ttu-id="f049c-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](extend-your-experiment-with-r.md).</span><span class="sxs-lookup"><span data-stu-id="f049c-193">For more information on using R scripts in your experiments, see [Extend your experiment with R](extend-your-experiment-with-r.md).</span></span>

<span data-ttu-id="f049c-194">**Next: [Train and evaluate the models](walkthrough-4-train-and-evaluate-models.md)**</span><span class="sxs-lookup"><span data-stu-id="f049c-194">**Next: [Train and evaluate the models](walkthrough-4-train-and-evaluate-models.md)**</span></span>

[0]: ./media/walkthrough-3-create-new-experiment/create-new-experiment.png
[5]: ./media/walkthrough-3-create-new-experiment/rename-experiment.png
[6]: ./media/walkthrough-3-create-new-experiment/experiment-properties.png
[7]: ./media/walkthrough-3-create-new-experiment/add-dataset-to-experiment.png
[8]: ./media/walkthrough-3-create-new-experiment/edit-metadata-with-comment.png
[9]: ./media/walkthrough-3-create-new-experiment/execute-r-script.png
[1]: ./media/walkthrough-3-create-new-experiment/experiment-with-edit-metadata-module.png
[2]: ./media/walkthrough-3-create-new-experiment/select-columns.png
[3]: ./media/walkthrough-3-create-new-experiment/edit-metadata-properties.png
[4]: ./media/walkthrough-3-create-new-experiment/experiment.png


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
