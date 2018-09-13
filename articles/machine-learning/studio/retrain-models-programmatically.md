---
title: Retrain Machine Learning models programmatically | Microsoft Docs
description: Learn how to programmatically retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 7ae4f977-e6bf-4d04-9dde-28a66ce7b664
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.openlocfilehash: b2090b39991363ee2a5b2e12945d97dc0fa9f2b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867973"
---
# <a name="retrain-machine-learning-models-programmatically"></a><span data-ttu-id="c7d2e-103">Retrain Machine Learning models programmatically</span><span class="sxs-lookup"><span data-stu-id="c7d2e-103">Retrain Machine Learning models programmatically</span></span>
<span data-ttu-id="c7d2e-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-104">In this walkthrough, you will learn how to programmatically retrain an Azure Machine Learning Web Service using C# and the Machine Learning Batch Execution service.</span></span>

<span data-ttu-id="c7d2e-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span><span class="sxs-lookup"><span data-stu-id="c7d2e-105">Once you have retrained the model, the following walkthroughs show how to update the model in your predictive web service:</span></span>

* <span data-ttu-id="c7d2e-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-106">If you deployed a Classic web service in the Machine Learning Web Services portal, see [Retrain a Classic web service](retrain-a-classic-web-service.md).</span></span> 
* <span data-ttu-id="c7d2e-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-107">If you deployed a New web service, see [Retrain a New web service using the Machine Learning Management cmdlets](retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="c7d2e-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](retrain-machine-learning-model.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-108">For an overview of the retraining process, see [Retrain a Machine Learning Model](retrain-machine-learning-model.md).</span></span>

<span data-ttu-id="c7d2e-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](retrain-existing-resource-manager-based-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-109">If you want to start with your existing New Azure Resource Manager based web service, see [Retrain an existing Predictive web service](retrain-existing-resource-manager-based-web-service.md).</span></span>

## <a name="create-a-training-experiment"></a><span data-ttu-id="c7d2e-110">Create a training experiment</span><span class="sxs-lookup"><span data-stu-id="c7d2e-110">Create a training experiment</span></span>
<span data-ttu-id="c7d2e-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-111">For this example, you will use "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset" from the Microsoft Azure Machine Learning samples.</span></span> 

<span data-ttu-id="c7d2e-112">To create the experiment:</span><span class="sxs-lookup"><span data-stu-id="c7d2e-112">To create the experiment:</span></span>

1. <span data-ttu-id="c7d2e-113">Sign into to Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-113">Sign into to Microsoft Azure Machine Learning Studio.</span></span> 
2. <span data-ttu-id="c7d2e-114">On the bottom right corner of the dashboard, click **New**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-114">On the bottom right corner of the dashboard, click **New**.</span></span>
3. <span data-ttu-id="c7d2e-115">From the Microsoft Samples, select Sample 5.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-115">From the Microsoft Samples, select Sample 5.</span></span>
4. <span data-ttu-id="c7d2e-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span><span class="sxs-lookup"><span data-stu-id="c7d2e-116">To rename the experiment, at the top of the experiment canvas, select the experiment name "Sample 5: Train, Test, Evaluate for Binary Classification: Adult Dataset".</span></span>
5. <span data-ttu-id="c7d2e-117">Type Census Model.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-117">Type Census Model.</span></span>
6. <span data-ttu-id="c7d2e-118">At the bottom of the experiment canvas, click **Run**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-118">At the bottom of the experiment canvas, click **Run**.</span></span>
7. <span data-ttu-id="c7d2e-119">Click **Set Up web service** and select **Retraining web service**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-119">Click **Set Up web service** and select **Retraining web service**.</span></span> 

<span data-ttu-id="c7d2e-120">The following shows the initial experiment.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-120">The following shows the initial experiment.</span></span>
   
   ![Initial experiment.][2]


## <a name="create-a-predictive-experiment-and-publish-as-a-web-service"></a><span data-ttu-id="c7d2e-122">Create a predictive experiment and publish as a web service</span><span class="sxs-lookup"><span data-stu-id="c7d2e-122">Create a predictive experiment and publish as a web service</span></span>
<span data-ttu-id="c7d2e-123">Next you create a Predicative Experiment.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-123">Next you create a Predicative Experiment.</span></span>

1. <span data-ttu-id="c7d2e-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-124">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Predictive Web Service**.</span></span> <span data-ttu-id="c7d2e-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-125">This saves the model as a Trained Model and adds web service Input and Output modules.</span></span> 
2. <span data-ttu-id="c7d2e-126">Click **Run**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-126">Click **Run**.</span></span> 
3. <span data-ttu-id="c7d2e-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-127">After the experiment has finished running, click **Deploy Web Service [Classic]** or **Deploy Web Service [New]**.</span></span>

> [!NOTE] 
> <span data-ttu-id="c7d2e-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-128">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="c7d2e-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-129">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span></span> 

## <a name="deploy-the-training-experiment-as-a-training-web-service"></a><span data-ttu-id="c7d2e-130">Deploy the training experiment as a Training web service</span><span class="sxs-lookup"><span data-stu-id="c7d2e-130">Deploy the training experiment as a Training web service</span></span>
<span data-ttu-id="c7d2e-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-131">To retrain the trained model, you must deploy the training experiment that you created as a Retraining web service.</span></span> <span data-ttu-id="c7d2e-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-132">This web service needs a *Web Service Output* module connected to the *[Train Model][train-model]* module, to be able to produce new trained models.</span></span>

1. <span data-ttu-id="c7d2e-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-133">To return to the training experiment, click the Experiments icon in the left pane, then click the experiment named Census Model.</span></span>  
2. <span data-ttu-id="c7d2e-134">In the Search Experiment Items search box, type web service.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-134">In the Search Experiment Items search box, type web service.</span></span> 
3. <span data-ttu-id="c7d2e-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-135">Drag a *Web Service Input* module onto the experiment canvas and connect its output to the *Clean Missing Data* module.</span></span>  <span data-ttu-id="c7d2e-136">This ensures that your retraining data is processed the same way as your original training data.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-136">This ensures that your retraining data is processed the same way as your original training data.</span></span>
4. <span data-ttu-id="c7d2e-137">Drag two *web service Output* modules onto the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-137">Drag two *web service Output* modules onto the experiment canvas.</span></span> <span data-ttu-id="c7d2e-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-138">Connect the output of the *Train Model* module to one and the output of the *Evaluate Model* module to the other.</span></span> <span data-ttu-id="c7d2e-139">The web service output for **Train Model** gives us the new trained model.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-139">The web service output for **Train Model** gives us the new trained model.</span></span> <span data-ttu-id="c7d2e-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-140">The output attached to **Evaluate Model** returns that module’s output, which is the performance results.</span></span>
5. <span data-ttu-id="c7d2e-141">Click **Run**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-141">Click **Run**.</span></span> 

<span data-ttu-id="c7d2e-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-142">Next you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span> <span data-ttu-id="c7d2e-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-143">To accomplish this, your next set of actions are dependent on whether you are working with a Classic web service or a New web service.</span></span>  

<span data-ttu-id="c7d2e-144">**Classic web service**</span><span class="sxs-lookup"><span data-stu-id="c7d2e-144">**Classic web service**</span></span>

<span data-ttu-id="c7d2e-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-145">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [Classic]**.</span></span> <span data-ttu-id="c7d2e-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-146">The Web Service **Dashboard** is displayed with the API Key and the API help page for Batch Execution.</span></span> <span data-ttu-id="c7d2e-147">Only the Batch Execution method can be used for creating Trained Models.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-147">Only the Batch Execution method can be used for creating Trained Models.</span></span>

<span data-ttu-id="c7d2e-148">**New web service**</span><span class="sxs-lookup"><span data-stu-id="c7d2e-148">**New web service**</span></span>

<span data-ttu-id="c7d2e-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-149">At the bottom of the experiment canvas, click **Set Up Web Service** and select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="c7d2e-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-150">The Web Service Azure Machine Learning Web Services portal opens to the Deploy web service page.</span></span> <span data-ttu-id="c7d2e-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-151">Type a name for your web service and choose a payment plan, then click **Deploy**.</span></span> <span data-ttu-id="c7d2e-152">Only the Batch Execution method can be used for creating Trained Models</span><span class="sxs-lookup"><span data-stu-id="c7d2e-152">Only the Batch Execution method can be used for creating Trained Models</span></span>

<span data-ttu-id="c7d2e-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span><span class="sxs-lookup"><span data-stu-id="c7d2e-153">In either case, after experiment has completed running, the resulting workflow should look as follows:</span></span>

![Resulting workflow after run.][4]



## <a name="retrain-the-model-with-new-data-using-bes"></a><span data-ttu-id="c7d2e-155">Retrain the model with new data using BES</span><span class="sxs-lookup"><span data-stu-id="c7d2e-155">Retrain the model with new data using BES</span></span>
<span data-ttu-id="c7d2e-156">For this example, you are using C# to create the retraining application.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-156">For this example, you are using C# to create the retraining application.</span></span> <span data-ttu-id="c7d2e-157">You can also use the Python or R sample code to accomplish this task.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-157">You can also use the Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="c7d2e-158">To call the Retraining APIs:</span><span class="sxs-lookup"><span data-stu-id="c7d2e-158">To call the Retraining APIs:</span></span>

1. <span data-ttu-id="c7d2e-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-159">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="c7d2e-160">Sign in to the Machine Learning Web Service portal.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-160">Sign in to the Machine Learning Web Service portal.</span></span>
3. <span data-ttu-id="c7d2e-161">If you are working with a Classic web service, click **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-161">If you are working with a Classic web service, click **Classic Web Services**.</span></span>
   1. <span data-ttu-id="c7d2e-162">Click the web service you are working with.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-162">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="c7d2e-163">Click the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-163">Click the default endpoint.</span></span>
   3. <span data-ttu-id="c7d2e-164">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-164">Click **Consume**.</span></span>
   4. <span data-ttu-id="c7d2e-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-165">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
   5. <span data-ttu-id="c7d2e-166">Continue to step 5 of this procedure.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-166">Continue to step 5 of this procedure.</span></span>
4. <span data-ttu-id="c7d2e-167">If you are working with a New web service, click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-167">If you are working with a New web service, click **Web Services**.</span></span>
   1. <span data-ttu-id="c7d2e-168">Click the web service you are working with.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-168">Click the web service you are working with.</span></span>
   2. <span data-ttu-id="c7d2e-169">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-169">Click **Consume**.</span></span>
   3. <span data-ttu-id="c7d2e-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-170">At the bottom of the Consume page, in the **Sample Code** section, click **Batch**.</span></span>
5. <span data-ttu-id="c7d2e-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-171">Copy the sample C# code for batch execution and paste it into the Program.cs file, making sure the namespace remains intact.</span></span>

<span data-ttu-id="c7d2e-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-172">Add the Nuget package Microsoft.AspNet.WebApi.Client as specified in the comments.</span></span> <span data-ttu-id="c7d2e-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-173">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the client library for Microsoft Azure storage services.</span></span> <span data-ttu-id="c7d2e-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-174">For more information, see [Windows Storage Services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="c7d2e-175">Update the apikey declaration</span><span class="sxs-lookup"><span data-stu-id="c7d2e-175">Update the apikey declaration</span></span>
<span data-ttu-id="c7d2e-176">Locate the **apikey** declaration.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-176">Locate the **apikey** declaration.</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="c7d2e-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-177">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="c7d2e-178">Update the Azure Storage information</span><span class="sxs-lookup"><span data-stu-id="c7d2e-178">Update the Azure Storage information</span></span>
<span data-ttu-id="c7d2e-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-179">The BES sample code uploads a file from a local drive (For example "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="c7d2e-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-180">To accomplish this task, you must retrieve the Storage account name, key, and container information for your Storage account from the classic Azure portal and the update corresponding values in the code.</span></span> 

1. <span data-ttu-id="c7d2e-181">Sign in to the classic Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-181">Sign in to the classic Azure portal.</span></span>
2. <span data-ttu-id="c7d2e-182">In the left navigation column, click **Storage**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-182">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="c7d2e-183">From the list of storage accounts, select one to store the retrained model.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-183">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="c7d2e-184">At the bottom of the page, click **Manage Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-184">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="c7d2e-185">Copy and save the **Primary Access Key** and close the dialog.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-185">Copy and save the **Primary Access Key** and close the dialog.</span></span> 
6. <span data-ttu-id="c7d2e-186">At the top of the page, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-186">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="c7d2e-187">Select an existing container or create a new one and save the name.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-187">Select an existing container or create a new one and save the name.</span></span>

<span data-ttu-id="c7d2e-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-188">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations and update the values you saved from the Azure portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure Storage Account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage Key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage Container name

<span data-ttu-id="c7d2e-189">You also must ensure the input file is available at the location you specify in the code.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-189">You also must ensure the input file is available at the location you specify in the code.</span></span> 

### <a name="specify-the-output-location"></a><span data-ttu-id="c7d2e-190">Specify the output location</span><span class="sxs-lookup"><span data-stu-id="c7d2e-190">Specify the output location</span></span>
<span data-ttu-id="c7d2e-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-191">When specifying the output location in the Request Payload, the extension of the file specified in *RelativeLocation* must be specified as ilearner.</span></span> 

<span data-ttu-id="c7d2e-192">See the following example:</span><span class="sxs-lookup"><span data-stu-id="c7d2e-192">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you would like to use for your output file, and valid file extension (usually .csv for scoring results, or .ilearner for trained models)*/
            }
        },

> [!NOTE]
> <span data-ttu-id="c7d2e-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-193">The names of your output locations may be different from the ones in this walkthrough based on the order in which you added the web service output modules.</span></span> <span data-ttu-id="c7d2e-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-194">Since you set up this training experiment with two outputs, the results include storage location information for both of them.</span></span>  
> 
> 

![Retraining output][6]

<span data-ttu-id="c7d2e-196">Diagram 4: Retraining output.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-196">Diagram 4: Retraining output.</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="c7d2e-197">Evaluate the Retraining Results</span><span class="sxs-lookup"><span data-stu-id="c7d2e-197">Evaluate the Retraining Results</span></span>
<span data-ttu-id="c7d2e-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-198">When you run the application, the output includes the URL and SAS token necessary to access the evaluation results.</span></span>

<span data-ttu-id="c7d2e-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-199">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL in the browser address bar.</span></span>  

<span data-ttu-id="c7d2e-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-200">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="c7d2e-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span><span class="sxs-lookup"><span data-stu-id="c7d2e-201">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results, you will use them during the retraining process.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7d2e-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7d2e-202">Next steps</span></span>
<span data-ttu-id="c7d2e-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-203">If you deployed the predictive web service by clicking **Deploy Web Service [Classic]**, see [Retrain a Classic web service](retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="c7d2e-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c7d2e-204">If you deployed the predictive web service by clicking **Deploy Web Service [New]**, see [Retrain a New web service using the Machine Learning Management cmdlets](retrain-new-web-service-using-powershell.md).</span></span>

<!-- Retrain a New web service using the Machine Learning Management REST API -->


[1]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE01.png
[2]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE02.png
[3]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE03.png
[4]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE04.png
[5]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE05.png
[6]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE06.png
[7]: ./media/retrain-models-programmatically/machine-learning-retrain-models-programmatically-IMAGE07.png


<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
