---
title: Retrain an existing predictive web service | Microsoft Docs
description: Learn how to retrain a model and update the web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: cc4c26a2-5672-4255-a767-cfd971e46775
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2017
ms.openlocfilehash: b06e3d742a0bed778dc7671128980708ba379e39
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856366"
---
# <a name="retrain-an-existing-predictive-web-service"></a><span data-ttu-id="f05f1-103">Retrain an existing predictive web service</span><span class="sxs-lookup"><span data-stu-id="f05f1-103">Retrain an existing predictive web service</span></span>
<span data-ttu-id="f05f1-104">This document describes the retraining process for the following scenario:</span><span class="sxs-lookup"><span data-stu-id="f05f1-104">This document describes the retraining process for the following scenario:</span></span>

* <span data-ttu-id="f05f1-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span><span class="sxs-lookup"><span data-stu-id="f05f1-105">You have a training experiment and a predictive experiment that you have deployed as an operationalized web service.</span></span>
* <span data-ttu-id="f05f1-106">You have new data that you want your predictive web service to use to perform its scoring.</span><span class="sxs-lookup"><span data-stu-id="f05f1-106">You have new data that you want your predictive web service to use to perform its scoring.</span></span>

> [!NOTE]
> <span data-ttu-id="f05f1-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="f05f1-107">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="f05f1-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="f05f1-108">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](manage-new-webservice.md).</span></span>

<span data-ttu-id="f05f1-109">Starting with your existing web service and experiments, you need to follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f05f1-109">Starting with your existing web service and experiments, you need to follow these steps:</span></span>

1. <span data-ttu-id="f05f1-110">Update the model.</span><span class="sxs-lookup"><span data-stu-id="f05f1-110">Update the model.</span></span>
   1. <span data-ttu-id="f05f1-111">Modify your training experiment to allow for web service inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="f05f1-111">Modify your training experiment to allow for web service inputs and outputs.</span></span>
   2. <span data-ttu-id="f05f1-112">Deploy the training experiment as a retraining web service.</span><span class="sxs-lookup"><span data-stu-id="f05f1-112">Deploy the training experiment as a retraining web service.</span></span>
   3. <span data-ttu-id="f05f1-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span><span class="sxs-lookup"><span data-stu-id="f05f1-113">Use the training experiment's Batch Execution Service (BES) to retrain the model.</span></span>
2. <span data-ttu-id="f05f1-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-114">Use the Azure Machine Learning PowerShell cmdlets to update the predictive experiment.</span></span>
   1. <span data-ttu-id="f05f1-115">Sign in to your Azure Resource Manager account.</span><span class="sxs-lookup"><span data-stu-id="f05f1-115">Sign in to your Azure Resource Manager account.</span></span>
   2. <span data-ttu-id="f05f1-116">Get the web service definition.</span><span class="sxs-lookup"><span data-stu-id="f05f1-116">Get the web service definition.</span></span>
   3. <span data-ttu-id="f05f1-117">Export the web service definition as JSON.</span><span class="sxs-lookup"><span data-stu-id="f05f1-117">Export the web service definition as JSON.</span></span>
   4. <span data-ttu-id="f05f1-118">Update the reference to the ilearner blob in the JSON.</span><span class="sxs-lookup"><span data-stu-id="f05f1-118">Update the reference to the ilearner blob in the JSON.</span></span>
   5. <span data-ttu-id="f05f1-119">Import the JSON into a web service definition.</span><span class="sxs-lookup"><span data-stu-id="f05f1-119">Import the JSON into a web service definition.</span></span>
   6. <span data-ttu-id="f05f1-120">Update the web service with a new web service definition.</span><span class="sxs-lookup"><span data-stu-id="f05f1-120">Update the web service with a new web service definition.</span></span>

## <a name="deploy-the-training-experiment"></a><span data-ttu-id="f05f1-121">Deploy the training experiment</span><span class="sxs-lookup"><span data-stu-id="f05f1-121">Deploy the training experiment</span></span>
<span data-ttu-id="f05f1-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span><span class="sxs-lookup"><span data-stu-id="f05f1-122">To deploy the training experiment as a retraining web service, you must add web service inputs and outputs to the model.</span></span> <span data-ttu-id="f05f1-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-123">By connecting a *Web Service Output* module to the experiment's *[Train Model][train-model]* module, you enable the training experiment to produce a new trained model that you can use in your predictive experiment.</span></span> <span data-ttu-id="f05f1-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span><span class="sxs-lookup"><span data-stu-id="f05f1-124">If you have an *Evaluate Model* module, you can also attach web service output to get the evaluation results as output.</span></span>

<span data-ttu-id="f05f1-125">To update your training experiment:</span><span class="sxs-lookup"><span data-stu-id="f05f1-125">To update your training experiment:</span></span>

1. <span data-ttu-id="f05f1-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span><span class="sxs-lookup"><span data-stu-id="f05f1-126">Connect a *Web Service Input* module to your data input (for example, a *Clean Missing Data* module).</span></span> <span data-ttu-id="f05f1-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span><span class="sxs-lookup"><span data-stu-id="f05f1-127">Typically, you want to ensure that your input data is processed in the same way as your original training data.</span></span>
2. <span data-ttu-id="f05f1-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span><span class="sxs-lookup"><span data-stu-id="f05f1-128">Connect a *Web Service Output* module to the output of your *Train Model* module.</span></span>
3. <span data-ttu-id="f05f1-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span><span class="sxs-lookup"><span data-stu-id="f05f1-129">If you have an *Evaluate Model* module and you want to output the evaluation results, connect a *Web Service Output* module to the output of your *Evaluate Model* module.</span></span>

<span data-ttu-id="f05f1-130">Run your experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-130">Run your experiment.</span></span>

<span data-ttu-id="f05f1-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span><span class="sxs-lookup"><span data-stu-id="f05f1-131">Next, you must deploy the training experiment as a web service that produces a trained model and model evaluation results.</span></span>

<span data-ttu-id="f05f1-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-132">At the bottom of the experiment canvas, click **Set Up Web Service**, and then select **Deploy Web Service [New]**.</span></span> <span data-ttu-id="f05f1-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span><span class="sxs-lookup"><span data-stu-id="f05f1-133">The Azure Machine Learning Web Services portal opens to the **Deploy Web Service** page.</span></span> <span data-ttu-id="f05f1-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-134">Type a name for your web service, choose a payment plan, and then click **Deploy**.</span></span> <span data-ttu-id="f05f1-135">You can only use the Batch Execution method for creating trained models.</span><span class="sxs-lookup"><span data-stu-id="f05f1-135">You can only use the Batch Execution method for creating trained models.</span></span>

## <a name="retrain-the-model-with-new-data-by-using-bes"></a><span data-ttu-id="f05f1-136">Retrain the model with new data by using BES</span><span class="sxs-lookup"><span data-stu-id="f05f1-136">Retrain the model with new data by using BES</span></span>
<span data-ttu-id="f05f1-137">For this example, we're using C# to create the retraining application.</span><span class="sxs-lookup"><span data-stu-id="f05f1-137">For this example, we're using C# to create the retraining application.</span></span> <span data-ttu-id="f05f1-138">You can also use Python or R sample code to accomplish this task.</span><span class="sxs-lookup"><span data-stu-id="f05f1-138">You can also use Python or R sample code to accomplish this task.</span></span>

<span data-ttu-id="f05f1-139">To call the retraining APIs:</span><span class="sxs-lookup"><span data-stu-id="f05f1-139">To call the retraining APIs:</span></span>

1. <span data-ttu-id="f05f1-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-140">Create a C# console application in Visual Studio: **New** > **Project** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
2. <span data-ttu-id="f05f1-141">Sign in to the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="f05f1-141">Sign in to the Machine Learning Web Services portal.</span></span>
3. <span data-ttu-id="f05f1-142">Click the web service that you're working with.</span><span class="sxs-lookup"><span data-stu-id="f05f1-142">Click the web service that you're working with.</span></span>
4. <span data-ttu-id="f05f1-143">Click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-143">Click **Consume**.</span></span>
5. <span data-ttu-id="f05f1-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-144">At the bottom of the **Consume** page, in the **Sample Code** section, click **Batch**.</span></span>
6. <span data-ttu-id="f05f1-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="f05f1-145">Copy the sample C# code for batch execution and paste it into the Program.cs file.</span></span> <span data-ttu-id="f05f1-146">Make sure that the namespace remains intact.</span><span class="sxs-lookup"><span data-stu-id="f05f1-146">Make sure that the namespace remains intact.</span></span>

<span data-ttu-id="f05f1-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span><span class="sxs-lookup"><span data-stu-id="f05f1-147">Add the NuGet package Microsoft.AspNet.WebApi.Client, as specified in the comments.</span></span> <span data-ttu-id="f05f1-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span><span class="sxs-lookup"><span data-stu-id="f05f1-148">To add the reference to Microsoft.WindowsAzure.Storage.dll, you might first need to install the [client library for Azure Storage services](https://www.nuget.org/packages/WindowsAzure.Storage).</span></span>

<span data-ttu-id="f05f1-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="f05f1-149">The following screenshot shows the **Consume** page in the Azure Machine Learning Web Services portal.</span></span>

![Consume page][1]

### <a name="update-the-apikey-declaration"></a><span data-ttu-id="f05f1-151">Update the apikey declaration</span><span class="sxs-lookup"><span data-stu-id="f05f1-151">Update the apikey declaration</span></span>
<span data-ttu-id="f05f1-152">Locate the **apikey** declaration:</span><span class="sxs-lookup"><span data-stu-id="f05f1-152">Locate the **apikey** declaration:</span></span>

    const string apiKey = "abc123"; // Replace this with the API key for the web service

<span data-ttu-id="f05f1-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span><span class="sxs-lookup"><span data-stu-id="f05f1-153">In the **Basic consumption info** section of the **Consume** page, locate the primary key and copy it to the **apikey** declaration.</span></span>

### <a name="update-the-azure-storage-information"></a><span data-ttu-id="f05f1-154">Update the Azure Storage information</span><span class="sxs-lookup"><span data-stu-id="f05f1-154">Update the Azure Storage information</span></span>
<span data-ttu-id="f05f1-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f05f1-155">The BES sample code uploads a file from a local drive (for example, "C:\temp\CensusIpnput.csv") to Azure Storage, processes it, and writes the results back to Azure Storage.</span></span>

<span data-ttu-id="f05f1-156">After running your experiment, the resulting workflow should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f05f1-156">After running your experiment, the resulting workflow should be similar to the following:</span></span>

![Resulting workflow after run][4]

1. <span data-ttu-id="f05f1-158">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f05f1-158">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="f05f1-159">In the left navigation column, click **More services**, search for **Storage accounts**, and select it.</span><span class="sxs-lookup"><span data-stu-id="f05f1-159">In the left navigation column, click **More services**, search for **Storage accounts**, and select it.</span></span>
3. <span data-ttu-id="f05f1-160">From the list of storage accounts, select one to store the retrained model.</span><span class="sxs-lookup"><span data-stu-id="f05f1-160">From the list of storage accounts, select one to store the retrained model.</span></span>
4. <span data-ttu-id="f05f1-161">In the left navigation column, click **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-161">In the left navigation column, click **Access keys**.</span></span>
5. <span data-ttu-id="f05f1-162">Copy and save the **Primary Access Key**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-162">Copy and save the **Primary Access Key**.</span></span>
6. <span data-ttu-id="f05f1-163">In the left navigation column, click **Containers**.</span><span class="sxs-lookup"><span data-stu-id="f05f1-163">In the left navigation column, click **Containers**.</span></span>
7. <span data-ttu-id="f05f1-164">Select an existing container, or create a new one and save the name.</span><span class="sxs-lookup"><span data-stu-id="f05f1-164">Select an existing container, or create a new one and save the name.</span></span>

<span data-ttu-id="f05f1-165">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the portal.</span><span class="sxs-lookup"><span data-stu-id="f05f1-165">Locate the *StorageAccountName*, *StorageAccountKey*, and *StorageContainerName* declarations, and update the values that you saved from the portal.</span></span>

    const string StorageAccountName = "mystorageacct"; // Replace this with your Azure storage account name
    const string StorageAccountKey = "a_storage_account_key"; // Replace this with your Azure Storage key
    const string StorageContainerName = "mycontainer"; // Replace this with your Azure Storage container name

<span data-ttu-id="f05f1-166">You also must ensure that the input file is available at the location that you specify in the code.</span><span class="sxs-lookup"><span data-stu-id="f05f1-166">You also must ensure that the input file is available at the location that you specify in the code.</span></span>

### <a name="specify-the-output-location"></a><span data-ttu-id="f05f1-167">Specify the output location</span><span class="sxs-lookup"><span data-stu-id="f05f1-167">Specify the output location</span></span>
<span data-ttu-id="f05f1-168">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span><span class="sxs-lookup"><span data-stu-id="f05f1-168">When you specify the output location in the Request Payload, the extension of the file that is specified in *RelativeLocation* must be specified as `ilearner`.</span></span> <span data-ttu-id="f05f1-169">See the following example:</span><span class="sxs-lookup"><span data-stu-id="f05f1-169">See the following example:</span></span>

    Outputs = new Dictionary<string, AzureBlobDataReference>() {
        {
            "output1",
            new AzureBlobDataReference()
            {
                ConnectionString = storageConnectionString,
                RelativeLocation = string.Format("{0}/output1results.ilearner", StorageContainerName) /*Replace this with the location you want to use for your output file and a valid file extension (usually .csv for scoring results or .ilearner for trained models)*/
            }
        },

<span data-ttu-id="f05f1-170">The following is an example of retraining output:</span><span class="sxs-lookup"><span data-stu-id="f05f1-170">The following is an example of retraining output:</span></span>

![Retraining output][6]

## <a name="evaluate-the-retraining-results"></a><span data-ttu-id="f05f1-172">Evaluate the retraining results</span><span class="sxs-lookup"><span data-stu-id="f05f1-172">Evaluate the retraining results</span></span>
<span data-ttu-id="f05f1-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span><span class="sxs-lookup"><span data-stu-id="f05f1-173">When you run the application, the output includes the URL and shared access signatures token that are necessary to access the evaluation results.</span></span>

<span data-ttu-id="f05f1-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span><span class="sxs-lookup"><span data-stu-id="f05f1-174">You can see the performance results of the retrained model by combining the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results for *output2* (as shown in the preceding retraining output image) and pasting the complete URL into the browser address bar.</span></span>

<span data-ttu-id="f05f1-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span><span class="sxs-lookup"><span data-stu-id="f05f1-175">Examine the results to determine whether the newly trained model performs well enough to replace the existing one.</span></span>

<span data-ttu-id="f05f1-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span><span class="sxs-lookup"><span data-stu-id="f05f1-176">Copy the *BaseLocation*, *RelativeLocation*, and *SasBlobToken* from the output results.</span></span>

## <a name="retrain-the-web-service"></a><span data-ttu-id="f05f1-177">Retrain the web service</span><span class="sxs-lookup"><span data-stu-id="f05f1-177">Retrain the web service</span></span>
<span data-ttu-id="f05f1-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span><span class="sxs-lookup"><span data-stu-id="f05f1-178">When you retrain a new web service, you update the predictive web service definition to reference the new trained model.</span></span> <span data-ttu-id="f05f1-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span><span class="sxs-lookup"><span data-stu-id="f05f1-179">The web service definition is an internal representation of the trained model of the web service and is not directly modifiable.</span></span> <span data-ttu-id="f05f1-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-180">Make sure that you are retrieving the web service definition for your predictive experiment and not your training experiment.</span></span>

## <a name="sign-in-to-azure-resource-manager"></a><span data-ttu-id="f05f1-181">Sign in to Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f05f1-181">Sign in to Azure Resource Manager</span></span>
<span data-ttu-id="f05f1-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f05f1-182">You must first sign in to your Azure account from within the PowerShell environment by using the [Connect-AzureRmAccount](/powershell/module/azurerm.profile/connect-azurermaccount) cmdlet.</span></span>

## <a name="get-the-web-service-definition-object"></a><span data-ttu-id="f05f1-183">Get the Web Service Definition object</span><span class="sxs-lookup"><span data-stu-id="f05f1-183">Get the Web Service Definition object</span></span>
<span data-ttu-id="f05f1-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/get-azurermmlwebservice) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f05f1-184">Next, get the Web Service Definition object by calling the [Get-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/get-azurermmlwebservice) cmdlet.</span></span>

    $wsd = Get-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

<span data-ttu-id="f05f1-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span><span class="sxs-lookup"><span data-stu-id="f05f1-185">To determine the resource group name of an existing web service, run the Get-AzureRmMlWebService cmdlet without any parameters to display the web services in your subscription.</span></span> <span data-ttu-id="f05f1-186">Locate the web service, and then look at its web service ID.</span><span class="sxs-lookup"><span data-stu-id="f05f1-186">Locate the web service, and then look at its web service ID.</span></span> <span data-ttu-id="f05f1-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="f05f1-187">The name of the resource group is the fourth element in the ID, just after the *resourceGroups* element.</span></span> <span data-ttu-id="f05f1-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="f05f1-188">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    Properties : Microsoft.Azure.Management.MachineLearning.WebServices.Models.WebServicePropertiesForGraph
    Id : /subscriptions/<subscription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237
    Name : RetrainSamplePre.2016.8.17.0.3.51.237
    Location : South Central US
    Type : Microsoft.MachineLearning/webServices
    Tags : {}

<span data-ttu-id="f05f1-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="f05f1-189">Alternatively, to determine the resource group name of an existing web service, sign in to the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="f05f1-190">Select the web service.</span><span class="sxs-lookup"><span data-stu-id="f05f1-190">Select the web service.</span></span> <span data-ttu-id="f05f1-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span><span class="sxs-lookup"><span data-stu-id="f05f1-191">The resource group name is the fifth element of the URL of the web service, just after the *resourceGroups* element.</span></span> <span data-ttu-id="f05f1-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span><span class="sxs-lookup"><span data-stu-id="f05f1-192">In the following example, the resource group name is Default-MachineLearning-SouthCentralUS.</span></span>

    https://services.azureml.net/subscriptions/<subcription ID>/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/RetrainSamplePre.2016.8.17.0.3.51.237


## <a name="export-the-web-service-definition-object-as-json"></a><span data-ttu-id="f05f1-193">Export the Web Service Definition object as JSON</span><span class="sxs-lookup"><span data-stu-id="f05f1-193">Export the Web Service Definition object as JSON</span></span>
<span data-ttu-id="f05f1-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/export-azurermmlwebservice) cmdlet to export it to a JSON-format file.</span><span class="sxs-lookup"><span data-stu-id="f05f1-194">To modify the definition of the trained model to use the newly trained model, you must first use the [Export-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/export-azurermmlwebservice) cmdlet to export it to a JSON-format file.</span></span>

    Export-AzureRmMlWebService -WebService $wsd -OutputFile "C:\temp\mlservice_export.json"

## <a name="update-the-reference-to-the-ilearner-blob"></a><span data-ttu-id="f05f1-195">Update the reference to the ilearner blob</span><span class="sxs-lookup"><span data-stu-id="f05f1-195">Update the reference to the ilearner blob</span></span>
<span data-ttu-id="f05f1-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span><span class="sxs-lookup"><span data-stu-id="f05f1-196">In the assets, locate the [trained model], update the *uri* value in the *locationInfo* node with the URI of the ilearner blob.</span></span> <span data-ttu-id="f05f1-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span><span class="sxs-lookup"><span data-stu-id="f05f1-197">The URI is generated by combining the *BaseLocation* and the *RelativeLocation* from the output of the BES retraining call.</span></span>

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

## <a name="import-the-json-into-a-web-service-definition-object"></a><span data-ttu-id="f05f1-198">Import the JSON into a Web Service Definition object</span><span class="sxs-lookup"><span data-stu-id="f05f1-198">Import the JSON into a Web Service Definition object</span></span>
<span data-ttu-id="f05f1-199">You must use the [Import-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/import-azurermmlwebservice) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-199">You must use the [Import-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/import-azurermmlwebservice) cmdlet to convert the modified JSON file back into a Web Service Definition object that you can use to update the predicative experiment.</span></span>

    $wsd = Import-AzureRmMlWebService -InputFile "C:\temp\mlservice_export.json"


## <a name="update-the-web-service"></a><span data-ttu-id="f05f1-200">Update the web service</span><span class="sxs-lookup"><span data-stu-id="f05f1-200">Update the web service</span></span>
<span data-ttu-id="f05f1-201">Finally, use the [Update-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/update-azurermmlwebservice) cmdlet to update the predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="f05f1-201">Finally, use the [Update-AzureRmMlWebService](https://docs.microsoft.com/powershell/module/azurerm.machinelearning/update-azurermmlwebservice) cmdlet to update the predictive experiment.</span></span>

    Update-AzureRmMlWebService -Name 'RetrainSamplePre.2016.8.17.0.3.51.237' -ResourceGroupName 'Default-MachineLearning-SouthCentralUS'

[1]: ./media/retrain-existing-arm-web-service/machine-learning-retrain-models-consume-page.png
[4]: ./media/retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE04.png
[6]: ./media/retrain-existing-arm-web-service/machine-learning-retrain-models-programmatically-IMAGE06.png

<!-- Module References -->
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
