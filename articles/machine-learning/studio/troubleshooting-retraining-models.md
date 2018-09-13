---
title: Troubleshoot retraining an Azure Machine Learning Classic web service | Microsoft Docs
description: Identify and correct common issues encounted when you are retraining the model for an Azure Machine Learning Web Service.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/01/2017
ms.openlocfilehash: 989bf010320501050a37fbf2f0799f50a5a3e2ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856755"
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="c0b0b-103">Troubleshooting the retraining of an Azure Machine Learning Classic web service</span><span class="sxs-lookup"><span data-stu-id="c0b0b-103">Troubleshooting the retraining of an Azure Machine Learning Classic web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="c0b0b-104">Retraining overview</span><span class="sxs-lookup"><span data-stu-id="c0b0b-104">Retraining overview</span></span>
<span data-ttu-id="c0b0b-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="c0b0b-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="c0b0b-107">For a complete walkthrough of the retraining process of a Classic web service, see [Retrain Machine Learning Models Programmatically](retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="c0b0b-107">For a complete walkthrough of the retraining process of a Classic web service, see [Retrain Machine Learning Models Programmatically](retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="c0b0b-108">Retraining process</span><span class="sxs-lookup"><span data-stu-id="c0b0b-108">Retraining process</span></span>
<span data-ttu-id="c0b0b-109">When you need to retrain the web service, you must add some additional pieces:</span><span class="sxs-lookup"><span data-stu-id="c0b0b-109">When you need to retrain the web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="c0b0b-110">A web service deployed from the Training Experiment.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-110">A web service deployed from the Training Experiment.</span></span> <span data-ttu-id="c0b0b-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Attach the web service output to the train model.][image1]
* <span data-ttu-id="c0b0b-113">A new endpoint added to your scoring web service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-113">A new endpoint added to your scoring web service.</span></span>  <span data-ttu-id="c0b0b-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure Machine Learning Web Services portal.</span></span>

<span data-ttu-id="c0b0b-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="c0b0b-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="c0b0b-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span><span class="sxs-lookup"><span data-stu-id="c0b0b-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="c0b0b-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span><span class="sxs-lookup"><span data-stu-id="c0b0b-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="c0b0b-119">You can use the sample C# code on the API help page to make the call.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="c0b0b-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="c0b0b-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span><span class="sxs-lookup"><span data-stu-id="c0b0b-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="c0b0b-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="c0b0b-123">Common obstacles</span><span class="sxs-lookup"><span data-stu-id="c0b0b-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="c0b0b-124">Check to see if you have the correct PATCH URL</span><span class="sxs-lookup"><span data-stu-id="c0b0b-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="c0b0b-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring web service.</span></span> <span data-ttu-id="c0b0b-126">There are a number of ways to obtain the PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="c0b0b-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="c0b0b-127">**Option 1: Programatically**</span><span class="sxs-lookup"><span data-stu-id="c0b0b-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="c0b0b-128">To get the correct PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="c0b0b-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="c0b0b-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="c0b0b-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation in the output of the addEndpoint sample.][image2]
3. <span data-ttu-id="c0b0b-132">Paste the URL into a browser to navigate to a page that provides help links for the web service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-132">Paste the URL into a browser to navigate to a page that provides help links for the web service.</span></span>
4. <span data-ttu-id="c0b0b-133">Click the **Update Resource** link to open the patch help page.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="c0b0b-134">**Option 2: Use the Azure Machine Learning Web Services portal**</span><span class="sxs-lookup"><span data-stu-id="c0b0b-134">**Option 2: Use the Azure Machine Learning Web Services portal**</span></span>

1. <span data-ttu-id="c0b0b-135">Sign in to the [Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-135">Sign in to the [Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span></span>
2. <span data-ttu-id="c0b0b-136">Click **Web Services** or **Classic Web Services** at the top.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-136">Click **Web Services** or **Classic Web Services** at the top.</span></span>
4. <span data-ttu-id="c0b0b-137">Click the scoring web service you are working with (if you didn't modify the default name of the web service, it will end in "[Scoring Exp.]").</span><span class="sxs-lookup"><span data-stu-id="c0b0b-137">Click the scoring web service you are working with (if you didn't modify the default name of the web service, it will end in "[Scoring Exp.]").</span></span>
5. <span data-ttu-id="c0b0b-138">Click **+NEW**.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-138">Click **+NEW**.</span></span>
6. <span data-ttu-id="c0b0b-139">After the endpoint is added, click the endpoint name.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-139">After the endpoint is added, click the endpoint name.</span></span>
7. <span data-ttu-id="c0b0b-140">Under the **Patch** URL, click **API Help** to open the patching help page.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-140">Under the **Patch** URL, click **API Help** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="c0b0b-141">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: "Sorry, but this feature is not supported or available in this context.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-141">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: "Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="c0b0b-142">This Web Service has no updatable resources.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-142">This Web Service has no updatable resources.</span></span> <span data-ttu-id="c0b0b-143">We apologize for the inconvenience and are working on improving this workflow."</span><span class="sxs-lookup"><span data-stu-id="c0b0b-143">We apologize for the inconvenience and are working on improving this workflow."</span></span>
> 
> 

<span data-ttu-id="c0b0b-144">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-144">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![Patch URL.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="c0b0b-146">Check to see that you are updating the correct scoring endpoint</span><span class="sxs-lookup"><span data-stu-id="c0b0b-146">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="c0b0b-147">Do not patch the training web service: The patch operation must be performed on the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-147">Do not patch the training web service: The patch operation must be performed on the scoring web service.</span></span>
* <span data-ttu-id="c0b0b-148">Do not patch the default endpoint on the web service: The patch operation must be performed on the new scoring web service endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-148">Do not patch the default endpoint on the web service: The patch operation must be performed on the new scoring web service endpoint that you added.</span></span>

<span data-ttu-id="c0b0b-149">You can verify which web service the endpoint is on by visiting the Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-149">You can verify which web service the endpoint is on by visiting the Web Services portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="c0b0b-150">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-150">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="c0b0b-151">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-151">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate web services listed.</span></span> <span data-ttu-id="c0b0b-152">The Predictive Web Service should end with "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="c0b0b-152">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="c0b0b-153">Sign in to the [Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-153">Sign in to the [Azure Machine Learning Web Services](https://services.azureml.net/) portal.</span></span>
2. <span data-ttu-id="c0b0b-154">Click **Web Services** or **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-154">Click **Web Services** or **Classic Web Services**.</span></span>
3. <span data-ttu-id="c0b0b-155">Select your Predictive Web Service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-155">Select your Predictive Web Service.</span></span>
4. <span data-ttu-id="c0b0b-156">Verify that your new endpoint was added to the web service.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-156">Verify that your new endpoint was added to the web service.</span></span>

### <a name="check-that-your-workspace-is-in-the-same-region-as-the-web-service"></a><span data-ttu-id="c0b0b-157">Check that your workspace is in the same region as the web service</span><span class="sxs-lookup"><span data-stu-id="c0b0b-157">Check that your workspace is in the same region as the web service</span></span>
1. <span data-ttu-id="c0b0b-158">Sign in to [Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c0b0b-158">Sign in to [Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="c0b0b-159">At the top, click the drop-down list of your workspaces.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-159">At the top, click the drop-down list of your workspaces.</span></span>

   ![Machine learning region UI.][image4]

3. <span data-ttu-id="c0b0b-161">Verify the region that your workspace is in.</span><span class="sxs-lookup"><span data-stu-id="c0b0b-161">Verify the region that your workspace is in.</span></span>

<!-- Image Links -->

[image1]: ./media/troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: ./media/troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: ./media/troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: ./media/troubleshooting-retraining-a-model/check-workspace-region.png
[image5]: ./media/troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: ./media/troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/troubleshooting-retraining-a-model/web-services-tab.png
