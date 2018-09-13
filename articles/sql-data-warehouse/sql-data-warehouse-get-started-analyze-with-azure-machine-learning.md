---
title: Analyze data with Azure Machine Learning | Microsoft Docs
description: Use Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: ''
ms.assetid: 95635460-150f-4a50-be9c-5ddc5797f8a9
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 03/02/2017
ms.author: kevin
ms.openlocfilehash: 5a4c514f57043e449d807ee8a9a86171618c18c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555235"
---
# <a name="analyze-data-with-azure-machine-learning"></a><span data-ttu-id="484f4-103">Analyze data with Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="484f4-103">Analyze data with Azure Machine Learning</span></span>
> [!div class="op_single_selector"]
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md) 
> * [SSMS](sql-data-warehouse-query-ssms.md)
> 
> 

<span data-ttu-id="484f4-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="484f4-109">This tutorial uses Azure Machine Learning to build a predictive machine learning model based on data stored in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="484f4-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span><span class="sxs-lookup"><span data-stu-id="484f4-110">Specifically, this builds a targeted marketing campaign for Adventure Works, the bike shop, by predicting if a customer is likely to buy a bike or not.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Integrating-Azure-Machine-Learning-with-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="484f4-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="484f4-111">Prerequisites</span></span>
<span data-ttu-id="484f4-112">To step through this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="484f4-112">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="484f4-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span><span class="sxs-lookup"><span data-stu-id="484f4-113">A SQL Data Warehouse pre-loaded with AdventureWorksDW sample data.</span></span> <span data-ttu-id="484f4-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span><span class="sxs-lookup"><span data-stu-id="484f4-114">To provision this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse] and choose to load the sample data.</span></span> <span data-ttu-id="484f4-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span><span class="sxs-lookup"><span data-stu-id="484f4-115">If you already have a data warehouse but do not have sample data, you can [load sample data manually][load sample data manually].</span></span>

## <a name="1-get-the-data"></a><span data-ttu-id="484f4-116">1. Get the data</span><span class="sxs-lookup"><span data-stu-id="484f4-116">1. Get the data</span></span>
<span data-ttu-id="484f4-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span><span class="sxs-lookup"><span data-stu-id="484f4-117">The data is in the dbo.vTargetMail view in the AdventureWorksDW database.</span></span> <span data-ttu-id="484f4-118">To read this data:</span><span class="sxs-lookup"><span data-stu-id="484f4-118">To read this data:</span></span>

1. <span data-ttu-id="484f4-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span><span class="sxs-lookup"><span data-stu-id="484f4-119">Sign into [Azure Machine Learning studio][Azure Machine Learning studio] and click on my experiments.</span></span>
2. <span data-ttu-id="484f4-120">Click **+NEW** and select **Blank Experiment**.</span><span class="sxs-lookup"><span data-stu-id="484f4-120">Click **+NEW** and select **Blank Experiment**.</span></span>
3. <span data-ttu-id="484f4-121">Enter a name for your experiment: Targeted Marketing.</span><span class="sxs-lookup"><span data-stu-id="484f4-121">Enter a name for your experiment: Targeted Marketing.</span></span>
4. <span data-ttu-id="484f4-122">Drag the **Reader** module from the modules pane into the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-122">Drag the **Reader** module from the modules pane into the canvas.</span></span>
5. <span data-ttu-id="484f4-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span><span class="sxs-lookup"><span data-stu-id="484f4-123">Specify the details of your SQL Data Warehouse database in the Properties pane.</span></span>
6. <span data-ttu-id="484f4-124">Specify the database **query** to read the data of interest.</span><span class="sxs-lookup"><span data-stu-id="484f4-124">Specify the database **query** to read the data of interest.</span></span>

```sql
SELECT [CustomerKey]
  ,[GeographyKey]
  ,[CustomerAlternateKey]
  ,[MaritalStatus]
  ,[Gender]
  ,cast ([YearlyIncome] as int) as SalaryYear
  ,[TotalChildren]
  ,[NumberChildrenAtHome]
  ,[EnglishEducation]
  ,[EnglishOccupation]
  ,[HouseOwnerFlag]
  ,[NumberCarsOwned]
  ,[CommuteDistance]
  ,[Region]
  ,[Age]
  ,[BikeBuyer]
FROM [dbo].[vTargetMail]
```

<span data-ttu-id="484f4-125">Run the experiment by clicking **Run** under the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-125">Run the experiment by clicking **Run** under the experiment canvas.</span></span>
<span data-ttu-id="484f4-126">![Run the experiment][1]</span><span class="sxs-lookup"><span data-stu-id="484f4-126">![Run the experiment][1]</span></span>

<span data-ttu-id="484f4-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span><span class="sxs-lookup"><span data-stu-id="484f4-127">After the experiment finishes running successfully, click the output port at the bottom of the Reader module and select **Visualize** to see the imported data.</span></span>
<span data-ttu-id="484f4-128">![View imported data][3]</span><span class="sxs-lookup"><span data-stu-id="484f4-128">![View imported data][3]</span></span>

## <a name="2-clean-the-data"></a><span data-ttu-id="484f4-129">2. Clean the data</span><span class="sxs-lookup"><span data-stu-id="484f4-129">2. Clean the data</span></span>
<span data-ttu-id="484f4-130">To clean the data, drop some columns that are not relevant for the model.</span><span class="sxs-lookup"><span data-stu-id="484f4-130">To clean the data, drop some columns that are not relevant for the model.</span></span> <span data-ttu-id="484f4-131">To do this:</span><span class="sxs-lookup"><span data-stu-id="484f4-131">To do this:</span></span>

1. <span data-ttu-id="484f4-132">Drag the **Project Columns** module into the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-132">Drag the **Project Columns** module into the canvas.</span></span>
2. <span data-ttu-id="484f4-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span><span class="sxs-lookup"><span data-stu-id="484f4-133">Click **Launch column selector** in the Properties pane to specify which columns you wish to drop.</span></span>
   <span data-ttu-id="484f4-134">![Project Columns][4]</span><span class="sxs-lookup"><span data-stu-id="484f4-134">![Project Columns][4]</span></span>
3. <span data-ttu-id="484f4-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span><span class="sxs-lookup"><span data-stu-id="484f4-135">Exclude two columns: CustomerAlternateKey and GeographyKey.</span></span>
   <span data-ttu-id="484f4-136">![Remove unnecessary columns][5]</span><span class="sxs-lookup"><span data-stu-id="484f4-136">![Remove unnecessary columns][5]</span></span>

## <a name="3-build-the-model"></a><span data-ttu-id="484f4-137">3. Build the model</span><span class="sxs-lookup"><span data-stu-id="484f4-137">3. Build the model</span></span>
<span data-ttu-id="484f4-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span><span class="sxs-lookup"><span data-stu-id="484f4-138">We will split the data 80-20: 80% to train a machine learning model and 20% to test the model.</span></span> <span data-ttu-id="484f4-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span><span class="sxs-lookup"><span data-stu-id="484f4-139">We will make use of the “Two-Class” algorithms for this binary classification problem.</span></span>

1. <span data-ttu-id="484f4-140">Drag the **Split** module into the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-140">Drag the **Split** module into the canvas.</span></span>
2. <span data-ttu-id="484f4-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span><span class="sxs-lookup"><span data-stu-id="484f4-141">Enter 0.8 for Fraction of rows in the first output dataset in the Properties pane.</span></span>
   <span data-ttu-id="484f4-142">![Split data into training and test set][6]</span><span class="sxs-lookup"><span data-stu-id="484f4-142">![Split data into training and test set][6]</span></span>
3. <span data-ttu-id="484f4-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-143">Drag the **Two-Class Boosted Decision Tree** module into the canvas.</span></span>
4. <span data-ttu-id="484f4-144">Drag the **Train Model** module into the canvas and specify the inputs.</span><span class="sxs-lookup"><span data-stu-id="484f4-144">Drag the **Train Model** module into the canvas and specify the inputs.</span></span> <span data-ttu-id="484f4-145">Then, click **Launch column selector** in the Properties pane.</span><span class="sxs-lookup"><span data-stu-id="484f4-145">Then, click **Launch column selector** in the Properties pane.</span></span>
   * <span data-ttu-id="484f4-146">First input: ML algorithm.</span><span class="sxs-lookup"><span data-stu-id="484f4-146">First input: ML algorithm.</span></span>
   * <span data-ttu-id="484f4-147">Second input: Data to train the algorithm on.</span><span class="sxs-lookup"><span data-stu-id="484f4-147">Second input: Data to train the algorithm on.</span></span>
     <span data-ttu-id="484f4-148">![Connect the Train Model module][7]</span><span class="sxs-lookup"><span data-stu-id="484f4-148">![Connect the Train Model module][7]</span></span>
5. <span data-ttu-id="484f4-149">Select the **BikeBuyer** column as the column to predict.</span><span class="sxs-lookup"><span data-stu-id="484f4-149">Select the **BikeBuyer** column as the column to predict.</span></span>
   <span data-ttu-id="484f4-150">![Select Column to predict][8]</span><span class="sxs-lookup"><span data-stu-id="484f4-150">![Select Column to predict][8]</span></span>

## <a name="4-score-the-model"></a><span data-ttu-id="484f4-151">4. Score the model</span><span class="sxs-lookup"><span data-stu-id="484f4-151">4. Score the model</span></span>
<span data-ttu-id="484f4-152">Now, we will test how the model performs on test data.</span><span class="sxs-lookup"><span data-stu-id="484f4-152">Now, we will test how the model performs on test data.</span></span> <span data-ttu-id="484f4-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span><span class="sxs-lookup"><span data-stu-id="484f4-153">We will compare the algorithm of our choice with a different algorithm to see which performs better.</span></span>

1. <span data-ttu-id="484f4-154">Drag **Score Model** module into the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-154">Drag **Score Model** module into the canvas.</span></span>
    <span data-ttu-id="484f4-155">First input: Trained model Second input: Test data ![Score the model][9]</span><span class="sxs-lookup"><span data-stu-id="484f4-155">First input: Trained model Second input: Test data ![Score the model][9]</span></span>
2. <span data-ttu-id="484f4-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-156">Drag the **Two-Class Bayes Point Machine** into the experiment canvas.</span></span> <span data-ttu-id="484f4-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span><span class="sxs-lookup"><span data-stu-id="484f4-157">We will compare how this algorithm performs in comparison to the Two-Class Boosted Decision Tree.</span></span>
3. <span data-ttu-id="484f4-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span><span class="sxs-lookup"><span data-stu-id="484f4-158">Copy and Paste the modules Train Model and Score Model in the canvas.</span></span>
4. <span data-ttu-id="484f4-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span><span class="sxs-lookup"><span data-stu-id="484f4-159">Drag the **Evaluate Model** module into the canvas to compare the two algorithms.</span></span>
5. <span data-ttu-id="484f4-160">**Run** the experiment.</span><span class="sxs-lookup"><span data-stu-id="484f4-160">**Run** the experiment.</span></span>
   <span data-ttu-id="484f4-161">![Run the experiment][10]</span><span class="sxs-lookup"><span data-stu-id="484f4-161">![Run the experiment][10]</span></span>
6. <span data-ttu-id="484f4-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span><span class="sxs-lookup"><span data-stu-id="484f4-162">Click the output port at the bottom of the Evaluate Model module and click Visualize.</span></span>
   <span data-ttu-id="484f4-163">![Visualize evaluation results][11]</span><span class="sxs-lookup"><span data-stu-id="484f4-163">![Visualize evaluation results][11]</span></span>

<span data-ttu-id="484f4-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span><span class="sxs-lookup"><span data-stu-id="484f4-164">The metrics provided are the ROC curve, precision-recall diagram and lift curve.</span></span> <span data-ttu-id="484f4-165">Looking at these metrics, we can see that the first model performed better than the second one.</span><span class="sxs-lookup"><span data-stu-id="484f4-165">Looking at these metrics, we can see that the first model performed better than the second one.</span></span> <span data-ttu-id="484f4-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span><span class="sxs-lookup"><span data-stu-id="484f4-166">To look at the what the first model predicted, click on output port of the Score Model and click Visualize.</span></span>
<span data-ttu-id="484f4-167">![Visualize score results][12]</span><span class="sxs-lookup"><span data-stu-id="484f4-167">![Visualize score results][12]</span></span>

<span data-ttu-id="484f4-168">You will see two more columns added to your test dataset.</span><span class="sxs-lookup"><span data-stu-id="484f4-168">You will see two more columns added to your test dataset.</span></span>

* <span data-ttu-id="484f4-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span><span class="sxs-lookup"><span data-stu-id="484f4-169">Scored Probabilities: the likelihood that a customer is a bike buyer.</span></span>
* <span data-ttu-id="484f4-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span><span class="sxs-lookup"><span data-stu-id="484f4-170">Scored Labels: the classification done by the model – bike buyer (1) or not (0).</span></span> <span data-ttu-id="484f4-171">This probability threshold for labeling is set to 50% and can be adjusted.</span><span class="sxs-lookup"><span data-stu-id="484f4-171">This probability threshold for labeling is set to 50% and can be adjusted.</span></span>

<span data-ttu-id="484f4-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span><span class="sxs-lookup"><span data-stu-id="484f4-172">Comparing the column BikeBuyer (actual) with the Scored Labels (prediction), you can see how well the model has performed.</span></span> <span data-ttu-id="484f4-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="484f4-173">As next steps, you can use this model to make predictions for new customers and publish this model as a web service or write results back to SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="484f4-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="484f4-174">Next steps</span></span>
<span data-ttu-id="484f4-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span><span class="sxs-lookup"><span data-stu-id="484f4-175">To learn more about building predictive machine learning models, refer to [Introduction to Machine Learning on Azure][Introduction to Machine Learning on Azure].</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img1_reader.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img2_visualize.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img3_readerdata.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img4_projectcolumns.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img5_columnselector.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img6_split.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img7_train.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img8_traincolumnselector.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img9_score.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img10_evaluate.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img11_evalresults.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-get-started-analyze-with-azure-machine-learning/img12_scoreresults.png


<!--Article references-->
[Azure Machine Learning studio]:https://studio.azureml.net/
[Introduction to Machine Learning on Azure]:https://azure.microsoft.com/documentation/articles/machine-learning-what-is-machine-learning/
[load sample data manually]: sql-data-warehouse-load-sample-databases.md
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md












