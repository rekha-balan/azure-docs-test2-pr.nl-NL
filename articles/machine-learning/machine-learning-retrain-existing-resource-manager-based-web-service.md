---
title: Retrain an existing predictive web service | Microsoft Docs
description: Learn how to retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/11/2017
ms.author: v-donglo
ms.openlocfilehash: 286b8deeacd1678fe746e2c3227b2246329b6c7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550954"
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="8b88a-103">Retrain an existing predictive web service</span><span class="sxs-lookup"><span data-stu-id="8b88a-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="8b88a-104">This document describes the retraining process for the following scenario:</span><span class="sxs-lookup"><span data-stu-id="8b88a-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="8b88a-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span><span class="sxs-lookup"><span data-stu-id="8b88a-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="8b88a-106">You have new data that you want your predictive web service to use to perform its scoring.</span><span class="sxs-lookup"><span data-stu-id="8b88a-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE] 
> <span data-ttu-id="8b88a-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="8b88a-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="8b88a-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="8b88a-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="8b88a-109">Starting with your existing web service and experiments, you need to follow these steps:</span><span class="sxs-lookup"><span data-stu-id="8b88a-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="8b88a-110">Update the model.</span><span class="sxs-lookup"><span data-stu-id="8b88a-110">Update the model.</span></span>
   1. <span data-ttu-id="8b88a-111">Modify your training experiment to allow for web service inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="8b88a-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="8b88a-112">Deploy the training experiment as a retraining web service.</span><span class="sxs-lookup"><span data-stu-id="8b88a-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="8b88a-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span><span class="sxs-lookup"><span data-stu-id="8b88a-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="8b88a-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="8b88a-115">Sign in to your Azure Resource Manager account.</span><span class="sxs-lookup"><span data-stu-id="8b88a-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="8b88a-116">Get the web service definition.</span><span class="sxs-lookup"><span data-stu-id="8b88a-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="8b88a-117">Export the web service definition as JSON.</span><span class="sxs-lookup"><span data-stu-id="8b88a-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="8b88a-118">Update the reference to the ilearner blob in the JSON.</span><span class="sxs-lookup"><span data-stu-id="8b88a-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="8b88a-119">Import the JSON into a web service definition.</span><span class="sxs-lookup"><span data-stu-id="8b88a-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="8b88a-120">Update the web service with a new web service definition.</span><span class="sxs-lookup"><span data-stu-id="8b88a-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="8b88a-121">Deploy the training experiment</span><span class="sxs-lookup"><span data-stu-id="8b88a-121">Deploy the training experiment</span></span>
<span data-ttu-id="8b88a-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span><span class="sxs-lookup"><span data-stu-id="8b88a-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="8b88a-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="8b88a-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span><span class="sxs-lookup"><span data-stu-id="8b88a-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="8b88a-125">To update your training experiment:</span><span class="sxs-lookup"><span data-stu-id="8b88a-125">To update your training experiment:</span></span>

1. <span data-ttu-id="8b88a-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span><span class="sxs-lookup"><span data-stu-id="8b88a-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="8b88a-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span><span class="sxs-lookup"><span data-stu-id="8b88a-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="8b88a-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span><span class="sxs-lookup"><span data-stu-id="8b88a-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="8b88a-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span><span class="sxs-lookup"><span data-stu-id="8b88a-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="8b88a-130">Run your experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-130">Run your experiment.</span></span>

<span data-ttu-id="8b88a-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span><span class="sxs-lookup"><span data-stu-id="8b88a-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>  

<span data-ttu-id="8b88a-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="8b88a-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span><span class="sxs-lookup"><span data-stu-id="8b88a-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="8b88a-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="8b88a-135">You can only use the Batch Execution method for creating trained models.</span><span class="sxs-lookup"><span data-stu-id="8b88a-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="8b88a-136">Retrain the model with new data by using BES</span><span class="sxs-lookup"><span data-stu-id="8b88a-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="8b88a-137">For this example, we're using C# to create the retraining application.</span><span class="sxs-lookup"><span data-stu-id="8b88a-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="8b88a-138">You can also use Python or R sample code to accomplish this task.</span><span class="sxs-lookup"><span data-stu-id="8b88a-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="8b88a-139">To call the retraining APIs:</span><span class="sxs-lookup"><span data-stu-id="8b88a-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="8b88a-140">Create a C# console application in Visual Studio (**New** > **Project** > **Windows Desktop** > **Console Application**).</span><span class="sxs-lookup"><span data-stu-id="8b88a-140">Create a C# console application in Visual Studio (**New** > **Project** > **Windows Desktop** > **Console Application**).</span></span>
2. <span data-ttu-id="8b88a-141">Sign in to the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="8b88a-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="8b88a-142">Click the web service that you're working with.</span><span class="sxs-lookup"><span data-stu-id="8b88a-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="8b88a-143">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-143">Click **Consume**.</span></span>
5. <span data-ttu-id="8b88a-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="8b88a-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="8b88a-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="8b88a-146">Make sure that the namespace remains intact.</span><span class="sxs-lookup"><span data-stu-id="8b88a-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="8b88a-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span><span class="sxs-lookup"><span data-stu-id="8b88a-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="8b88a-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="8b88a-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="8b88a-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="8b88a-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Consume page][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="8b88a-151">Update the apikey declaration</span><span class="sxs-lookup"><span data-stu-id="8b88a-151">Update the apikey declaration</span></span>
<span data-ttu-id="8b88a-152">Locate the **apikey** declaration:</span><span class="sxs-lookup"><span data-stu-id="8b88a-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="8b88a-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span><span class="sxs-lookup"><span data-stu-id="8b88a-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="8b88a-154">Update the Azure Storage information</span><span class="sxs-lookup"><span data-stu-id="8b88a-154">Update the Azure Storage information</span></span>
<span data-ttu-id="8b88a-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="8b88a-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>  

<span data-ttu-id="8b88a-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="8b88a-156">To update the Azure Storage information, you must retrieve the storage account name, key, and container information for your storage account from the Azure classic portal, and then update the correspondi After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Resulting workflow after run][4]<span data-ttu-id="8b88a-158">ng values in the code.</span><span class="sxs-lookup"><span data-stu-id="8b88a-158">ng values in the code.</span></span>

1. <span data-ttu-id="8b88a-159">Sign in to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="8b88a-159">Sign in to the Azure classic portal.</span></span>
2. <span data-ttu-id="8b88a-160">In the left navigation column, click **Storage**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-160">In the left navigation column, click **Storage**.</span></span>
3. <span data-ttu-id="8b88a-161">From the list of storage accounts, select one to store the retrained model.</span><span class="sxs-lookup"><span data-stu-id="8b88a-161">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="8b88a-162">At the bottom of the page, click **Manage Access Keys**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-162">At the bottom of the page, click **Manage Access Keys**.</span></span>
5. <span data-ttu-id="8b88a-163">Copy and save the **Primary Access Key** and close the dialog.</span><span class="sxs-lookup"><span data-stu-id="8b88a-163">Copy and save the **Primary Access Key** and close the dialog.</span></span>
6. <span data-ttu-id="8b88a-164">At the top of the page, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="8b88a-164">At the top of the page, click **Containers**.</span></span>
7. <span data-ttu-id="8b88a-165">Select an existing container, or create a new one and save the name.</span><span class="sxs-lookup"><span data-stu-id="8b88a-165">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="8b88a-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span><span class="sxs-lookup"><span data-stu-id="8b88a-166">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the classic portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="8b88a-167">You also must ensure that the input file is available at the location that you specify in the code.</span><span class="sxs-lookup"><span data-stu-id="8b88a-167">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="8b88a-168">Specify the output location</span><span class="sxs-lookup"><span data-stu-id="8b88a-168">Specify the output location</span></span>
<span data-ttu-id="8b88a-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="8b88a-169">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="8b88a-170">See the following example:</span><span class="sxs-lookup"><span data-stu-id="8b88a-170">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="8b88a-171">The following is an example of retraining output: ![Retraining output][6]</span><span class="sxs-lookup"><span data-stu-id="8b88a-171">The following is an example of retraining output: ![Retraining output][6]</span></span>

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="8b88a-172">Evaluate the retraining results</span><span class="sxs-lookup"><span data-stu-id="8b88a-172">Evaluate the retraining results</span></span>
<span data-ttu-id="8b88a-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span><span class="sxs-lookup"><span data-stu-id="8b88a-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="8b88a-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span><span class="sxs-lookup"><span data-stu-id="8b88a-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>  

<span data-ttu-id="8b88a-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span><span class="sxs-lookup"><span data-stu-id="8b88a-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="8b88a-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span><span class="sxs-lookup"><span data-stu-id="8b88a-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="8b88a-177">Retrain the web service</span><span class="sxs-lookup"><span data-stu-id="8b88a-177">Retrain the web service</span></span>
<span data-ttu-id="8b88a-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span><span class="sxs-lookup"><span data-stu-id="8b88a-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="8b88a-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span><span class="sxs-lookup"><span data-stu-id="8b88a-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="8b88a-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="8b88a-181">Sign in to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b88a-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="8b88a-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8b88a-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="8b88a-183">Get the Web Service Definition object</span><span class="sxs-lookup"><span data-stu-id="8b88a-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="8b88a-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8b88a-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="8b88a-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b88a-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="8b88a-186">Locate the web service, and then look at its web service ID.</span><span class="sxs-lookup"><span data-stu-id="8b88a-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="8b88a-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="8b88a-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="8b88a-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="8b88a-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="8b88a-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="8b88a-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="8b88a-190">Select the web service.</span><span class="sxs-lookup"><span data-stu-id="8b88a-190">Select the web service.</span></span> <span data-ttu-id="8b88a-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="8b88a-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="8b88a-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="8b88a-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="8b88a-193">Export the Web Service Definition object as JSON</span><span class="sxs-lookup"><span data-stu-id="8b88a-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="8b88a-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span><span class="sxs-lookup"><span data-stu-id="8b88a-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767935.aspx) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="8b88a-195">Update the reference to the ilearner blob</span><span class="sxs-lookup"><span data-stu-id="8b88a-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="8b88a-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span><span class="sxs-lookup"><span data-stu-id="8b88a-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="8b88a-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span><span class="sxs-lookup"><span data-stu-id="8b88a-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

     "asset3": {
        "name": "Retrain Sample [trained model]",
        "type": "Resource",
        "locationInfo": {
          "uri": "https://mltestaccount.blob.core.windows.net/azuremlassetscontainer/baca7bca650f46218633552c0bcbba0e.ilearner"
        },
        "outputPorts": {
          "Results dataset": {
            "type": "Dataset"
          }
        }
      },

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="8b88a-198">Import the JSON into a Web Service Definition object</span><span class="sxs-lookup"><span data-stu-id="8b88a-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="8b88a-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-199">You must use the [Import-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767925.aspx) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="8b88a-200">Update the web service</span><span class="sxs-lookup"><span data-stu-id="8b88a-200">Update the web service</span></span>
<span data-ttu-id="8b88a-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="8b88a-201">Finally, use the [Update-AzureRmMlWebService](https://msdn.microsoft.com/library/azure/mt767922.aspx) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/



