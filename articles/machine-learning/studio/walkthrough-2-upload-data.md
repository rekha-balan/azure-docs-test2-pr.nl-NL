---
title: 'Step 2: Upload data into a Machine Learning experiment | Microsoft Docs'
description: 'Step 2 of the Develop a predictive solution walkthrough: Upload stored public data into Azure Machine Learning Studio.'
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: 9f4bc52e-9919-4dea-90ea-5cf7cc506d85
ms.service: machine-learning
ms.component: studio
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/23/2017
ms.openlocfilehash: dfa6ae8011da0299c270035b8b781d70a8e80119
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857455"
---
# <a name="walkthrough-step-2-upload-existing-data-into-an-azure-machine-learning-experiment"></a><span data-ttu-id="e4223-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span><span class="sxs-lookup"><span data-stu-id="e4223-103">Walkthrough Step 2: Upload existing data into an Azure Machine Learning experiment</span></span>
<span data-ttu-id="e4223-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span><span class="sxs-lookup"><span data-stu-id="e4223-104">This is the second step of the walkthrough, [Develop a predictive analytics solution in Azure Machine Learning](walkthrough-develop-predictive-solution.md)</span></span>

1. [<span data-ttu-id="e4223-105">Create a Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="e4223-105">Create a Machine Learning workspace</span></span>](walkthrough-1-create-ml-workspace.md)
2. <span data-ttu-id="e4223-106">**Upload existing data**</span><span class="sxs-lookup"><span data-stu-id="e4223-106">**Upload existing data**</span></span>
3. [<span data-ttu-id="e4223-107">Create a new experiment</span><span class="sxs-lookup"><span data-stu-id="e4223-107">Create a new experiment</span></span>](walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="e4223-108">Train and evaluate the models</span><span class="sxs-lookup"><span data-stu-id="e4223-108">Train and evaluate the models</span></span>](walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="e4223-109">Deploy the Web service</span><span class="sxs-lookup"><span data-stu-id="e4223-109">Deploy the Web service</span></span>](walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="e4223-110">Access the Web service</span><span class="sxs-lookup"><span data-stu-id="e4223-110">Access the Web service</span></span>](walkthrough-6-access-web-service.md)

- - -
<span data-ttu-id="e4223-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span><span class="sxs-lookup"><span data-stu-id="e4223-111">To develop a predictive model for credit risk, we need data that we can use to train and then test the model.</span></span> <span data-ttu-id="e4223-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span><span class="sxs-lookup"><span data-stu-id="e4223-112">For this walkthrough, we'll use the "UCI Statlog (German Credit Data) Data Set" from the UC Irvine Machine Learning repository.</span></span> <span data-ttu-id="e4223-113">You can find it here:</span><span class="sxs-lookup"><span data-stu-id="e4223-113">You can find it here:</span></span>  
<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)</a>

<span data-ttu-id="e4223-114">We'll use the file named **german.data**.</span><span class="sxs-lookup"><span data-stu-id="e4223-114">We'll use the file named **german.data**.</span></span> <span data-ttu-id="e4223-115">Download this file to your local hard drive.</span><span class="sxs-lookup"><span data-stu-id="e4223-115">Download this file to your local hard drive.</span></span>  

<span data-ttu-id="e4223-116">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span><span class="sxs-lookup"><span data-stu-id="e4223-116">The **german.data** dataset contains rows of 20 variables for 1000 past applicants for credit.</span></span> <span data-ttu-id="e4223-117">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span><span class="sxs-lookup"><span data-stu-id="e4223-117">These 20 variables represent the dataset's set of features (the *feature vector*), which provides identifying characteristics for each credit applicant.</span></span> <span data-ttu-id="e4223-118">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-118">An additional column in each row represents the applicant's calculated credit risk, with 700 applicants identified as a low credit risk and 300 as a high risk.</span></span>

<span data-ttu-id="e4223-119">The UCI website provides a description of the attributes of the feature vector for this data.</span><span class="sxs-lookup"><span data-stu-id="e4223-119">The UCI website provides a description of the attributes of the feature vector for this data.</span></span> <span data-ttu-id="e4223-120">This includes financial information, credit history, employment status, and personal information.</span><span class="sxs-lookup"><span data-stu-id="e4223-120">This includes financial information, credit history, employment status, and personal information.</span></span> <span data-ttu-id="e4223-121">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-121">For each applicant, a binary rating has been given indicating whether they are a low or high credit risk.</span></span> 

<span data-ttu-id="e4223-122">We'll use this data to train a predictive analytics model.</span><span class="sxs-lookup"><span data-stu-id="e4223-122">We'll use this data to train a predictive analytics model.</span></span> <span data-ttu-id="e4223-123">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-123">When we're done, our model should be able to accept a feature vector for a new individual and predict whether he or she is a low or high credit risk.</span></span>  

<span data-ttu-id="e4223-124">Here's an interesting twist.</span><span class="sxs-lookup"><span data-stu-id="e4223-124">Here's an interesting twist.</span></span> <span data-ttu-id="e4223-125">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-125">The description of the dataset on the UCI website mentions what it costs if we misclassify a person's credit risk.</span></span>
<span data-ttu-id="e4223-126">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span><span class="sxs-lookup"><span data-stu-id="e4223-126">If the model predicts a high credit risk for someone who is actually a low credit risk, the model has made a misclassification.</span></span>
<span data-ttu-id="e4223-127">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-127">But the reverse misclassification is five times more costly to the financial institution: if the model predicts a low credit risk for someone who is actually a high credit risk.</span></span>

<span data-ttu-id="e4223-128">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span><span class="sxs-lookup"><span data-stu-id="e4223-128">So, we want to train our model so that the cost of this latter type of misclassification is five times higher than misclassifying the other way.</span></span>
<span data-ttu-id="e4223-129">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span><span class="sxs-lookup"><span data-stu-id="e4223-129">One simple way to do this when training the model in our experiment is by duplicating (five times) those entries that represent someone with a high credit risk.</span></span> <span data-ttu-id="e4223-130">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span><span class="sxs-lookup"><span data-stu-id="e4223-130">Then, if the model misclassifies someone as a low credit risk when they're actually a high risk, the model does that same misclassification five times, once for each duplicate.</span></span> <span data-ttu-id="e4223-131">This will increase the cost of this error in the training results.</span><span class="sxs-lookup"><span data-stu-id="e4223-131">This will increase the cost of this error in the training results.</span></span>


## <a name="convert-the-dataset-format"></a><span data-ttu-id="e4223-132">Convert the dataset format</span><span class="sxs-lookup"><span data-stu-id="e4223-132">Convert the dataset format</span></span>
<span data-ttu-id="e4223-133">The original dataset uses a blank-separated format.</span><span class="sxs-lookup"><span data-stu-id="e4223-133">The original dataset uses a blank-separated format.</span></span> <span data-ttu-id="e4223-134">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span><span class="sxs-lookup"><span data-stu-id="e4223-134">Machine Learning Studio works better with a comma-separated value (CSV) file, so we'll convert the dataset by replacing spaces with commas.</span></span>  

<span data-ttu-id="e4223-135">There are many ways to convert this data.</span><span class="sxs-lookup"><span data-stu-id="e4223-135">There are many ways to convert this data.</span></span> <span data-ttu-id="e4223-136">One way is by using the following Windows PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="e4223-136">One way is by using the following Windows PowerShell command:</span></span>   

    cat german.data | %{$_ -replace " ",","} | sc german.csv  

<span data-ttu-id="e4223-137">Another way is by using the Unix sed command:</span><span class="sxs-lookup"><span data-stu-id="e4223-137">Another way is by using the Unix sed command:</span></span>  

    sed 's/ /,/g' german.data > german.csv  

<span data-ttu-id="e4223-138">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span><span class="sxs-lookup"><span data-stu-id="e4223-138">In either case, we have created a comma-separated version of the data in a file named **german.csv** that we can use in our experiment.</span></span>

## <a name="upload-the-dataset-to-machine-learning-studio"></a><span data-ttu-id="e4223-139">Upload the dataset to Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e4223-139">Upload the dataset to Machine Learning Studio</span></span>
<span data-ttu-id="e4223-140">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e4223-140">Once the data has been converted to CSV format, we need to upload it into Machine Learning Studio.</span></span> 

1. <span data-ttu-id="e4223-141">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span><span class="sxs-lookup"><span data-stu-id="e4223-141">Open the Machine Learning Studio home page ([https://studio.azureml.net](https://studio.azureml.net)).</span></span> 

2. <span data-ttu-id="e4223-142">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span><span class="sxs-lookup"><span data-stu-id="e4223-142">Click the menu ![Menu][1] in the upper-left corner of the window, click **Azure Machine Learning**, select **Studio**, and sign in.</span></span>

3. <span data-ttu-id="e4223-143">Click **+NEW** at the bottom of the window.</span><span class="sxs-lookup"><span data-stu-id="e4223-143">Click **+NEW** at the bottom of the window.</span></span>

4. <span data-ttu-id="e4223-144">Select **DATASET**.</span><span class="sxs-lookup"><span data-stu-id="e4223-144">Select **DATASET**.</span></span>

5. <span data-ttu-id="e4223-145">Select **FROM LOCAL FILE**.</span><span class="sxs-lookup"><span data-stu-id="e4223-145">Select **FROM LOCAL FILE**.</span></span>

    ![Add a dataset from a local file][2]

6. <span data-ttu-id="e4223-147">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span><span class="sxs-lookup"><span data-stu-id="e4223-147">In the **Upload a new dataset** dialog, click **Browse** and find the **german.csv** file you created.</span></span>

7. <span data-ttu-id="e4223-148">Enter a name for the dataset.</span><span class="sxs-lookup"><span data-stu-id="e4223-148">Enter a name for the dataset.</span></span> <span data-ttu-id="e4223-149">For this walkthrough, call it "UCI German Credit Card Data".</span><span class="sxs-lookup"><span data-stu-id="e4223-149">For this walkthrough, call it "UCI German Credit Card Data".</span></span>

8. <span data-ttu-id="e4223-150">For data type, select **Generic CSV File With no header (.nh.csv)**.</span><span class="sxs-lookup"><span data-stu-id="e4223-150">For data type, select **Generic CSV File With no header (.nh.csv)**.</span></span>

9. <span data-ttu-id="e4223-151">Add a description if you’d like.</span><span class="sxs-lookup"><span data-stu-id="e4223-151">Add a description if you’d like.</span></span>

10. <span data-ttu-id="e4223-152">Click the **OK** check mark.</span><span class="sxs-lookup"><span data-stu-id="e4223-152">Click the **OK** check mark.</span></span>  

    ![Upload the dataset][3]

<span data-ttu-id="e4223-154">This uploads the data into a dataset module that we can use in an experiment.</span><span class="sxs-lookup"><span data-stu-id="e4223-154">This uploads the data into a dataset module that we can use in an experiment.</span></span>

<span data-ttu-id="e4223-155">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span><span class="sxs-lookup"><span data-stu-id="e4223-155">You can manage datasets that you've uploaded to Studio by clicking the **DATASETS** tab to the left of the Studio window.</span></span>

![Manage datasets][4]

<span data-ttu-id="e4223-157">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="e4223-157">For more information about importing other types of data into an experiment, see [Import your training data into Azure Machine Learning Studio](import-data.md).</span></span>

<span data-ttu-id="e4223-158">**Next: [Create a new experiment](walkthrough-3-create-new-experiment.md)**</span><span class="sxs-lookup"><span data-stu-id="e4223-158">**Next: [Create a new experiment](walkthrough-3-create-new-experiment.md)**</span></span>

[1]: media/walkthrough-2-upload-data/menu.png
[2]: media/walkthrough-2-upload-data/add-dataset.png
[3]: media/walkthrough-2-upload-data/upload-dataset.png
[4]: media/walkthrough-2-upload-data/dataset-list.png
