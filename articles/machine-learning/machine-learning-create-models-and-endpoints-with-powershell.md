---
title: Create multiple models from one experiment | Microsoft Docs
description: Use PowerShell to create multiple Machine Learning models and web service endpoints with the same algorithm but different training datasets.
services: machine-learning
documentationcenter: ''
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1076b8eb-5a0d-4ac5-8601-8654d9be229f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: garye;haining
ms.openlocfilehash: eed639a6a3217d49b24ac922741cd105bb4e58f0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550626"
---
# <a name="create-many-machine-learning-models-and-web-service-endpoints-from-one-experiment-using-powershell"></a><span data-ttu-id="ae894-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae894-103">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>
<span data-ttu-id="ae894-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span><span class="sxs-lookup"><span data-stu-id="ae894-104">Here's a common machine learning problem: You want to create many models that have the same training workflow and use the same algorithm, but have different training datasets as input.</span></span> <span data-ttu-id="ae894-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span><span class="sxs-lookup"><span data-stu-id="ae894-105">This article shows you how to do this at scale in Azure Machine Learning Studio using just a single experiment.</span></span>

<span data-ttu-id="ae894-106">For example, let's say you own a global bike rental franchise business.</span><span class="sxs-lookup"><span data-stu-id="ae894-106">For example, let's say you own a global bike rental franchise business.</span></span> <span data-ttu-id="ae894-107">You want to build a regression model to predict the rental demand based on historic data.</span><span class="sxs-lookup"><span data-stu-id="ae894-107">You want to build a regression model to predict the rental demand based on historic data.</span></span> <span data-ttu-id="ae894-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span><span class="sxs-lookup"><span data-stu-id="ae894-108">You have 1,000 rental locations across the world and you've collected a dataset for each location that includes important features such as date, time, weather, and traffic that are specific to each location.</span></span>

<span data-ttu-id="ae894-109">You could train your model once using a merged version of all the datasets across all locations.</span><span class="sxs-lookup"><span data-stu-id="ae894-109">You could train your model once using a merged version of all the datasets across all locations.</span></span> <span data-ttu-id="ae894-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span><span class="sxs-lookup"><span data-stu-id="ae894-110">But because each of your locations has a unique environment, a better approach would be to train your regression model separately using the dataset for each location.</span></span> <span data-ttu-id="ae894-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span><span class="sxs-lookup"><span data-stu-id="ae894-111">That way, each trained model could take into account the different store sizes, volume, geography, population, bike-friendly traffic environment, *etc.*.</span></span>

<span data-ttu-id="ae894-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span><span class="sxs-lookup"><span data-stu-id="ae894-112">That may be the best approach, but you don't want to create 1,000 training experiments in Azure Machine Learning with each one representing a unique location.</span></span> <span data-ttu-id="ae894-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span><span class="sxs-lookup"><span data-stu-id="ae894-113">Besides being an overwhelming task, it's also seems pretty inefficient since each experiment would have all the same components except for the training dataset.</span></span>

<span data-ttu-id="ae894-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span><span class="sxs-lookup"><span data-stu-id="ae894-114">Fortunately, we can accomplish this by using the [Azure Machine Learning retraining API](machine-learning-retrain-models-programmatically.md) and automating the task with [Azure Machine Learning PowerShell](machine-learning-powershell-module.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ae894-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span><span class="sxs-lookup"><span data-stu-id="ae894-115">To make our sample run faster, we'll reduce the number of locations from 1,000 to 10.</span></span> <span data-ttu-id="ae894-116">But the same principles and procedures apply to 1,000 locations.</span><span class="sxs-lookup"><span data-stu-id="ae894-116">But the same principles and procedures apply to 1,000 locations.</span></span> <span data-ttu-id="ae894-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span><span class="sxs-lookup"><span data-stu-id="ae894-117">The only difference is that if you want to train from 1,000 datasets you probably want to think of running the following PowerShell scripts in parallel.</span></span> <span data-ttu-id="ae894-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span><span class="sxs-lookup"><span data-stu-id="ae894-118">How to do that is beyond the scope of this article, but you can find examples of PowerShell multi-threading on the Internet.</span></span>  
> 
> 

## <a name="set-up-the-training-experiment"></a><span data-ttu-id="ae894-119">Set up the training experiment</span><span class="sxs-lookup"><span data-stu-id="ae894-119">Set up the training experiment</span></span>
<span data-ttu-id="ae894-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span><span class="sxs-lookup"><span data-stu-id="ae894-120">We're going to use an example [training experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Training-Experiment-1) that we've already created in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="ae894-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span><span class="sxs-lookup"><span data-stu-id="ae894-121">Open this experiment in your [Azure Machine Learning Studio](https://studio.azureml.net) workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="ae894-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span><span class="sxs-lookup"><span data-stu-id="ae894-122">In order to follow along with this example, you may want to use a standard workspace rather than a free workspace.</span></span> <span data-ttu-id="ae894-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span><span class="sxs-lookup"><span data-stu-id="ae894-123">We'll be creating one endpoint for each customer - for a total of 10 endpoints - and that will require a standard workspace since a free workspace is limited to 3 endpoints.</span></span> <span data-ttu-id="ae894-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span><span class="sxs-lookup"><span data-stu-id="ae894-124">If you only have a free workspace, just modify the scripts below to allow for only 3 locations.</span></span>
> 
> 

<span data-ttu-id="ae894-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ae894-125">The experiment uses an **Import Data** module to import the training dataset *customer001.csv* from an Azure storage account.</span></span> <span data-ttu-id="ae894-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span><span class="sxs-lookup"><span data-stu-id="ae894-126">Let's assume we have collected training datasets from all bike rental locations and stored them in the same blob storage location with file names ranging from *rentalloc001.csv* to *rentalloc10.csv*.</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-models-and-endpoints-with-powershell/reader-module.png)

<span data-ttu-id="ae894-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="ae894-128">Note that a **Web Service Output** module has been added to the **Train Model** module.</span></span>
<span data-ttu-id="ae894-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span><span class="sxs-lookup"><span data-stu-id="ae894-129">When this experiment is deployed as a web service, the endpoint associated with that output will return the trained model in the format of a .ilearner file.</span></span>

<span data-ttu-id="ae894-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span><span class="sxs-lookup"><span data-stu-id="ae894-130">Also note that we set up a web service parameter for the URL that the **Import Data** module uses.</span></span> <span data-ttu-id="ae894-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span><span class="sxs-lookup"><span data-stu-id="ae894-131">This allows us to use the parameter to specify individual training datasets to train the model for each location.</span></span>
<span data-ttu-id="ae894-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span><span class="sxs-lookup"><span data-stu-id="ae894-132">There are other ways we could have done this, such as using a SQL query with a web service parameter to get data from a SQL Azure database, or simply using a  **Web Service Input** module to pass in a dataset to the web service.</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-models-and-endpoints-with-powershell/web-service-output.png)

<span data-ttu-id="ae894-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span><span class="sxs-lookup"><span data-stu-id="ae894-134">Now, let's run this training experiment using the default value *rental001.csv* as the training dataset.</span></span> <span data-ttu-id="ae894-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span><span class="sxs-lookup"><span data-stu-id="ae894-135">If you view the output of the **Evaluate** module (click the output and select **Visualize**), you can see we get a decent performance of *AUC* = 0.91.</span></span> <span data-ttu-id="ae894-136">At this point, we're ready to deploy a web service out of this training experiment.</span><span class="sxs-lookup"><span data-stu-id="ae894-136">At this point, we're ready to deploy a web service out of this training experiment.</span></span>

## <a name="deploy-the-training-and-scoring-web-services"></a><span data-ttu-id="ae894-137">Deploy the training and scoring web services</span><span class="sxs-lookup"><span data-stu-id="ae894-137">Deploy the training and scoring web services</span></span>
<span data-ttu-id="ae894-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span><span class="sxs-lookup"><span data-stu-id="ae894-138">To deploy the training web service, click the **Set Up Web Service** button below the experiment canvas and select **Deploy Web Service**.</span></span> <span data-ttu-id="ae894-139">Call this web service ""Bike Rental Training".</span><span class="sxs-lookup"><span data-stu-id="ae894-139">Call this web service ""Bike Rental Training".</span></span>

<span data-ttu-id="ae894-140">Now we need to deploy the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="ae894-140">Now we need to deploy the scoring web service.</span></span>
<span data-ttu-id="ae894-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span><span class="sxs-lookup"><span data-stu-id="ae894-141">To do this, we can click **Set Up Web Service** below the canvas and select **Predictive Web Service**.</span></span> <span data-ttu-id="ae894-142">This creates a scoring experiment.</span><span class="sxs-lookup"><span data-stu-id="ae894-142">This creates a scoring experiment.</span></span>
<span data-ttu-id="ae894-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span><span class="sxs-lookup"><span data-stu-id="ae894-143">We'll need to make a few minor adjustments to make it work as a web service, such as removing the label column "cnt" from the input data and limiting the output to only the instance id and the corresponding predicted value.</span></span>

<span data-ttu-id="ae894-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span><span class="sxs-lookup"><span data-stu-id="ae894-144">To save yourself that work, you can simply open the [predictive experiment](https://gallery.cortanaintelligence.com/Experiment/Bike-Rental-Predicative-Experiment-1) in the Gallery that's already been prepared.</span></span>

<span data-ttu-id="ae894-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span><span class="sxs-lookup"><span data-stu-id="ae894-145">To deploy the web service, run the predictive experiment, then click the **Deploy Web Service** button below the canvas.</span></span> <span data-ttu-id="ae894-146">Name the scoring web service "Bike Rental Scoring"".</span><span class="sxs-lookup"><span data-stu-id="ae894-146">Name the scoring web service "Bike Rental Scoring"".</span></span>

## <a name="create-10-identical-web-service-endpoints-with-powershell"></a><span data-ttu-id="ae894-147">Create 10 identical web service endpoints with PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae894-147">Create 10 identical web service endpoints with PowerShell</span></span>
<span data-ttu-id="ae894-148">This web service comes with a default endpoint.</span><span class="sxs-lookup"><span data-stu-id="ae894-148">This web service comes with a default endpoint.</span></span> <span data-ttu-id="ae894-149">But we're not as interested in the default endpoint since it can't be updated.</span><span class="sxs-lookup"><span data-stu-id="ae894-149">But we're not as interested in the default endpoint since it can't be updated.</span></span> <span data-ttu-id="ae894-150">What we need to do is to create 10 additional endpoints, one for each location.</span><span class="sxs-lookup"><span data-stu-id="ae894-150">What we need to do is to create 10 additional endpoints, one for each location.</span></span> <span data-ttu-id="ae894-151">We'll do this with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae894-151">We'll do this with PowerShell.</span></span>

<span data-ttu-id="ae894-152">First, we set up our PowerShell environment:</span><span class="sxs-lookup"><span data-stu-id="ae894-152">First, we set up our PowerShell environment:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and is properly set to point to the valid Workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

<span data-ttu-id="ae894-153">Then, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="ae894-153">Then, run the following PowerShell command:</span></span>

    # Create 10 endpoints on the scoring web service.
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpointName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

<span data-ttu-id="ae894-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span><span class="sxs-lookup"><span data-stu-id="ae894-154">Now we've created 10 endpoints and they all contain the same trained model trained on *customer001.csv*.</span></span> <span data-ttu-id="ae894-155">You can view them in the Azure Management Portal.</span><span class="sxs-lookup"><span data-stu-id="ae894-155">You can view them in the Azure Management Portal.</span></span>

![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-create-models-and-endpoints-with-powershell/created-endpoints.png)

## <a name="update-the-endpoints-to-use-separate-training-datasets-using-powershell"></a><span data-ttu-id="ae894-157">Update the endpoints to use separate training datasets using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae894-157">Update the endpoints to use separate training datasets using PowerShell</span></span>
<span data-ttu-id="ae894-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span><span class="sxs-lookup"><span data-stu-id="ae894-158">The next step is to update the endpoints with models uniquely trained on each customer's individual data.</span></span> <span data-ttu-id="ae894-159">But first we need to produce these models from the **Bike Rental Training** web service.</span><span class="sxs-lookup"><span data-stu-id="ae894-159">But first we need to produce these models from the **Bike Rental Training** web service.</span></span> <span data-ttu-id="ae894-160">Let's go back to the **Bike Rental Training** web service.</span><span class="sxs-lookup"><span data-stu-id="ae894-160">Let's go back to the **Bike Rental Training** web service.</span></span> <span data-ttu-id="ae894-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span><span class="sxs-lookup"><span data-stu-id="ae894-161">We need to call its BES endpoint 10 times with 10 different training datasets in order to produce 10 different models.</span></span> <span data-ttu-id="ae894-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span><span class="sxs-lookup"><span data-stu-id="ae894-162">We'll use the **InovkeAmlWebServiceBESEndpoint** PowerShell cmdlet to do this.</span></span>

<span data-ttu-id="ae894-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span><span class="sxs-lookup"><span data-stu-id="ae894-163">You will also need to provide credentials for your blob storage account into `$configContent`, namely, at the fields `AccountName`, `AccountKey` and `RelativeLocation`.</span></span> <span data-ttu-id="ae894-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span><span class="sxs-lookup"><span data-stu-id="ae894-164">The `AccountName` can be one of your account names, as seen in the **Classic Azure Management Portal** (*Storage* tab).</span></span> <span data-ttu-id="ae894-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span><span class="sxs-lookup"><span data-stu-id="ae894-165">Once you click on a storage account, its `AccountKey` can be found by pressing the **Manage Access Keys** button at the bottom and copying the *Primary Access Key*.</span></span> <span data-ttu-id="ae894-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span><span class="sxs-lookup"><span data-stu-id="ae894-166">The `RelativeLocation` is the path relative to your storage where a new model will be stored.</span></span> <span data-ttu-id="ae894-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span><span class="sxs-lookup"><span data-stu-id="ae894-167">For instance, the path `hai/retrain/bike_rental/` in the script below points to a container named `hai`, and `/retrain/bike_rental/` are subfolders.</span></span> <span data-ttu-id="ae894-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/storage-explorers.md) that allow you to do so.</span><span class="sxs-lookup"><span data-stu-id="ae894-168">Currently, you cannot create subfolders through the portal UI, but there are [several Azure Storage Explorers](../storage/storage-explorers.md) that allow you to do so.</span></span> <span data-ttu-id="ae894-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span><span class="sxs-lookup"><span data-stu-id="ae894-169">It is recommended that you create a new container in your storage to store the new trained models (.ilearner files) as follows: from your storage page, click on the **Add** button at the bottom and name it `retrain`.</span></span> <span data-ttu-id="ae894-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span><span class="sxs-lookup"><span data-stu-id="ae894-170">In summary, the necassary changes to the script below pertain to `AccountName`, `AccountKey` and `RelativeLocation` (:`"retrain/model' + $seq + '.ilearner"`).</span></span>

    # Invoke the retraining API 10 times
    # This is the default (and the only) endpoint on the training web service
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

> [!NOTE]
> <span data-ttu-id="ae894-171">The BES endpoint is the only supported mode for this operation.</span><span class="sxs-lookup"><span data-stu-id="ae894-171">The BES endpoint is the only supported mode for this operation.</span></span> <span data-ttu-id="ae894-172">RRS cannot be used for producing trained models.</span><span class="sxs-lookup"><span data-stu-id="ae894-172">RRS cannot be used for producing trained models.</span></span>
> 
> 

<span data-ttu-id="ae894-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span><span class="sxs-lookup"><span data-stu-id="ae894-173">As you can see above, instead of constructing 10 different BES job configuration json files, we dynamically create the config string instead and feed it to the *jobConfigString* parameter of the **InvokeAmlWebServceBESEndpoint** cmdlet, since there is really no need to keep a copy on disk.</span></span>

<span data-ttu-id="ae894-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="ae894-174">If everything goes well, after a while you should see 10 .ilearner files, from *model001.ilearner* to *model010.ilearner*, in your Azure storage account.</span></span> <span data-ttu-id="ae894-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae894-175">Now we're ready to update our 10 scoring web service endpoints with these models using the **Patch-AmlWebServiceEndpoint** PowerShell cmdlet.</span></span> <span data-ttu-id="ae894-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span><span class="sxs-lookup"><span data-stu-id="ae894-176">Remember again that we can only patch the non-default endpoints we programmatically created earlier.</span></span>

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '<my_blob_sas_token>'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }

<span data-ttu-id="ae894-177">This should run fairly quickly.</span><span class="sxs-lookup"><span data-stu-id="ae894-177">This should run fairly quickly.</span></span> <span data-ttu-id="ae894-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span><span class="sxs-lookup"><span data-stu-id="ae894-178">When the execution finishes, we'll have successfully created 10 predictive web service endpoints, each containing a trained model uniquely trained on the dataset specific to a rental location, all from a single training experiment.</span></span> <span data-ttu-id="ae894-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span><span class="sxs-lookup"><span data-stu-id="ae894-179">To verify this, you can try calling these endpoints using the **InvokeAmlWebServiceRRSEndpoint** cmdlet, providing them with the same input data, and you should expect to see different prediction results since the models are trained with different training sets.</span></span>

## <a name="full-powershell-script"></a><span data-ttu-id="ae894-180">Full PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ae894-180">Full PowerShell script</span></span>
<span data-ttu-id="ae894-181">Here's the listing of the full source code:</span><span class="sxs-lookup"><span data-stu-id="ae894-181">Here's the listing of the full source code:</span></span>

    Import-Module .\AzureMLPS.dll
    # Assume the default configuration file exists and properly set to point to the valid workspace.
    $scoringSvc = Get-AmlWebService | where Name -eq 'Bike Rental Scoring'
    $trainingSvc = Get-AmlWebService | where Name -eq 'Bike Rental Training'

    # Create 10 endpoints on the scoring web service
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        Write-Host ('adding endpoint ' + $endpontName + '...')
        Add-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -Description $endpointName     
    }

    # Invoke the retraining API 10 times to produce 10 regression models in .ilearner format
    $trainingSvcEp = (Get-AmlWebServiceEndpoint -WebServiceId $trainingSvc.Id)[0];
    $submitJobRequestUrl = $trainingSvcEp.ApiLocation + '/jobs?api-version=2.0';
    $apiKey = $trainingSvcEp.PrimaryKey;
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $inputFileName = 'https://bostonmtc.blob.core.windows.net/hai/retrain/bike_rental/BikeRental' + $seq + '.csv';
        $configContent = '{ "GlobalParameters": { "URI": "' + $inputFileName + '" }, "Outputs": { "output1": { "ConnectionString": "DefaultEndpointsProtocol=https;AccountName=<myaccount>;AccountKey=<mykey>", "RelativeLocation": "hai/retrain/bike_rental/model' + $seq + '.ilearner" } } }';
        Write-Host ('training regression model on ' + $inputFileName + ' for rental location ' + $seq + '...');
        Invoke-AmlWebServiceBESEndpoint -JobConfigString $configContent -SubmitJobRequestUrl $submitJobRequestUrl -ApiKey $apiKey
    }

    # Patch the 10 endpoints with respective .ilearner models
    $baseLoc = 'http://bostonmtc.blob.core.windows.net/'
    $sasToken = '?test'
    For ($i = 1; $i -le 10; $i++){
        $seq = $i.ToString().PadLeft(3, '0');
        $endpointName = 'rentalloc' + $seq;
        $relativeLoc = 'hai/retrain/bike_rental/model' + $seq + '.ilearner';
        Write-Host ('Patching endpoint ' + $endpointName + '...');
        Patch-AmlWebServiceEndpoint -WebServiceId $scoringSvc.Id -EndpointName $endpointName -ResourceName 'Bike Rental [trained model]' -BaseLocation $baseLoc -RelativeLocation $relativeLoc -SasBlobToken $sasToken
    }



