---
title: Troubleshoot retraining an Azure Machine Learning Classic web service | Microsoft Docs
description: Identify and correct common issues encounted when you are retraining the model for an Azure Machine Learning Web Service.
services: machine-learning
documentationcenter: ''
author: VDonGlover
manager: raymondl
editor: ''
ms.assetid: 75cac53c-185c-437d-863a-5d66d871921e
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 7f336c881c80b11d3cb627e4095b6d19de55c137
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550766"
---
# <a name="troubleshooting-the-retraining-of-an-azure-machine-learning-classic-web-service"></a><span data-ttu-id="2ea95-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span><span class="sxs-lookup"><span data-stu-id="2ea95-103">Troubleshooting the retraining of an Azure Machine Learning Classic Web service</span></span>
## <a name="retraining-overview"></a><span data-ttu-id="2ea95-104">Retraining overview</span><span class="sxs-lookup"><span data-stu-id="2ea95-104">Retraining overview</span></span>
<span data-ttu-id="2ea95-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span><span class="sxs-lookup"><span data-stu-id="2ea95-105">When you deploy a predictive experiment as a scoring web service it is a static model.</span></span> <span data-ttu-id="2ea95-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span><span class="sxs-lookup"><span data-stu-id="2ea95-106">As new data becomes available or when the consumer of the API has their own data, the model needs to be retrained.</span></span> 

<span data-ttu-id="2ea95-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="2ea95-107">For a complete walkthrough of the retraining process of a Classic Web service, see [Retrain Machine Learning Models Programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

## <a name="retraining-process"></a><span data-ttu-id="2ea95-108">Retraining process</span><span class="sxs-lookup"><span data-stu-id="2ea95-108">Retraining process</span></span>
<span data-ttu-id="2ea95-109">When you need to retrain the Web service, you must add some additional pieces:</span><span class="sxs-lookup"><span data-stu-id="2ea95-109">When you need to retrain the Web service, you must add some additional pieces:</span></span>

* <span data-ttu-id="2ea95-110">A Web service deployed from the Training Experiment.</span><span class="sxs-lookup"><span data-stu-id="2ea95-110">A Web service deployed from the Training Experiment.</span></span> <span data-ttu-id="2ea95-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="2ea95-111">The experiment must have a **Web Service Output** module attached to the output of the **Train Model** module.</span></span>  
  
    ![Attach the web service output to the train model.][image1]
* <span data-ttu-id="2ea95-113">A new endpoint added to your scoring Web service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-113">A new endpoint added to your scoring Web service.</span></span>  <span data-ttu-id="2ea95-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="2ea95-114">You can add the endpoint programmatically using the sample code referenced in the Retrain Machine Learning models programmatically topic or through the Azure classic portal.</span></span>

<span data-ttu-id="2ea95-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span><span class="sxs-lookup"><span data-stu-id="2ea95-115">You can then use the sample C# code from the Training Web Service's API help page to retrain model.</span></span> <span data-ttu-id="2ea95-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="2ea95-116">Once you have evaluated the results and are satisfied with them, you update the trained model scoring web service using the new endpoint that you added.</span></span>

<span data-ttu-id="2ea95-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span><span class="sxs-lookup"><span data-stu-id="2ea95-117">With all the pieces in place, the major steps you must take to retrain the model are as follows:</span></span>

1. <span data-ttu-id="2ea95-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span><span class="sxs-lookup"><span data-stu-id="2ea95-118">Call the Training Web Service:  The call is to the Batch Execution Service (BES), not the Request Response Service (RRS).</span></span> <span data-ttu-id="2ea95-119">You can use the sample C# code on the API help page to make the call.</span><span class="sxs-lookup"><span data-stu-id="2ea95-119">You can use the sample C# code on the API help page to make the call.</span></span> 
2. <span data-ttu-id="2ea95-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-120">Find the values for the *BaseLocation*, *RelativeLocation*, and *SasBlobToken*: These values are returned in the output from your call to the Training Web Service.</span></span> 
   <span data-ttu-id="2ea95-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span><span class="sxs-lookup"><span data-stu-id="2ea95-121">![showing the output of the retraining sample and the BaseLocation, RelativeLocation, and  SasBlobToken values.][image6]</span></span>
3. <span data-ttu-id="2ea95-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-122">Update the added endpoint from the scoring web service with the new trained model: Using the sample code provided in the Retrain Machine Learning models programmatically, update the new endpoint you added to the scoring model with the newly trained model from the Training Web Service.</span></span>

## <a name="common-obstacles"></a><span data-ttu-id="2ea95-123">Common obstacles</span><span class="sxs-lookup"><span data-stu-id="2ea95-123">Common obstacles</span></span>
### <a name="check-to-see-if-you-have-the-correct-patch-url"></a><span data-ttu-id="2ea95-124">Check to see if you have the correct PATCH URL</span><span class="sxs-lookup"><span data-stu-id="2ea95-124">Check to see if you have the correct PATCH URL</span></span>
<span data-ttu-id="2ea95-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-125">The PATCH URL you are using must be the one associated with the new scoring endpoint you added to the scoring Web service.</span></span> <span data-ttu-id="2ea95-126">There are a number of ways to obtain the PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="2ea95-126">There are a number of ways to obtain the PATCH URL:</span></span>

<span data-ttu-id="2ea95-127">**Option 1: Programatically**</span><span class="sxs-lookup"><span data-stu-id="2ea95-127">**Option 1: Programatically**</span></span>

<span data-ttu-id="2ea95-128">To get the correct PATCH URL:</span><span class="sxs-lookup"><span data-stu-id="2ea95-128">To get the correct PATCH URL:</span></span>

1. <span data-ttu-id="2ea95-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span><span class="sxs-lookup"><span data-stu-id="2ea95-129">Run the [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) sample code.</span></span>
2. <span data-ttu-id="2ea95-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span><span class="sxs-lookup"><span data-stu-id="2ea95-130">From the output of AddEndpoint, find the *HelpLocation* value and copy the URL.</span></span>
   
   ![HelpLocation in the output of the addEndpoint sample.][image2]
3. <span data-ttu-id="2ea95-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-132">Paste the URL into a browser to navigate to a page that provides help links for the Web service.</span></span>
4. <span data-ttu-id="2ea95-133">Click the **Update Resource** link to open the patch help page.</span><span class="sxs-lookup"><span data-stu-id="2ea95-133">Click the **Update Resource** link to open the patch help page.</span></span>

<span data-ttu-id="2ea95-134">**Option 2: Use the Azure classic portal**</span><span class="sxs-lookup"><span data-stu-id="2ea95-134">**Option 2: Use the Azure classic portal**</span></span>

1. <span data-ttu-id="2ea95-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2ea95-135">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2ea95-136">Open the Machine Learning tab. ![Machine leaning tab.][image4]</span><span class="sxs-lookup"><span data-stu-id="2ea95-136">Open the Machine Learning tab. ![Machine leaning tab.][image4]</span></span>
3. <span data-ttu-id="2ea95-137">Click your workspace name, then **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="2ea95-137">Click your workspace name, then **Web Services**.</span></span>
4. <span data-ttu-id="2ea95-138">Click the scoring Web service you are working with.</span><span class="sxs-lookup"><span data-stu-id="2ea95-138">Click the scoring Web service you are working with.</span></span> <span data-ttu-id="2ea95-139">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span><span class="sxs-lookup"><span data-stu-id="2ea95-139">(If you did not modify the default name of the web service, it will end in [Scoring Exp.].)</span></span>
5. <span data-ttu-id="2ea95-140">Click **Add Endpoint**.</span><span class="sxs-lookup"><span data-stu-id="2ea95-140">Click **Add Endpoint**.</span></span>
6. <span data-ttu-id="2ea95-141">After the endpoint is added, click the endpoint name.</span><span class="sxs-lookup"><span data-stu-id="2ea95-141">After the endpoint is added, click the endpoint name.</span></span> <span data-ttu-id="2ea95-142">Then click **Update Resource** to open the patching help page.</span><span class="sxs-lookup"><span data-stu-id="2ea95-142">Then click **Update Resource** to open the patching help page.</span></span>

> [!NOTE]
> <span data-ttu-id="2ea95-143">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span><span class="sxs-lookup"><span data-stu-id="2ea95-143">If you have added the endpoint to the Training Web Service instead of the Predictive Web Service, you will receive the following error when you click the **Update Resource** link: Sorry, but this feature is not supported or available in this context.</span></span> <span data-ttu-id="2ea95-144">This Web Service has no updatable resources.</span><span class="sxs-lookup"><span data-stu-id="2ea95-144">This Web Service has no updatable resources.</span></span> <span data-ttu-id="2ea95-145">We apologize for the inconvenience and are working on improving this workflow.</span><span class="sxs-lookup"><span data-stu-id="2ea95-145">We apologize for the inconvenience and are working on improving this workflow.</span></span>
> 
> 

![New endpoint dashboard.][image3]

<span data-ttu-id="2ea95-147">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span><span class="sxs-lookup"><span data-stu-id="2ea95-147">The PATCH help page contains the PATCH URL you must use and provides sample code you can use to call it.</span></span>

![Patch URL.][image5]

### <a name="check-to-see-that-you-are-updating-the-correct-scoring-endpoint"></a><span data-ttu-id="2ea95-149">Check to see that you are updating the correct scoring endpoint</span><span class="sxs-lookup"><span data-stu-id="2ea95-149">Check to see that you are updating the correct scoring endpoint</span></span>
* <span data-ttu-id="2ea95-150">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-150">Do not patch the Training Web Service: The patch operation must be performed on the scoring Web service.</span></span>
* <span data-ttu-id="2ea95-151">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span><span class="sxs-lookup"><span data-stu-id="2ea95-151">Do not patch the default endpoint on Web service: The patch operation must be performed on the new scoring Web service endpoint that you added.</span></span>

<span data-ttu-id="2ea95-152">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="2ea95-152">You can verify which Web service the endpoint is on by visiting the Azure classic portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="2ea95-153">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-153">Be sure you are adding the endpoint to the Predictive Web Service, not the Training Web Service.</span></span> <span data-ttu-id="2ea95-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span><span class="sxs-lookup"><span data-stu-id="2ea95-154">If you have correctly deployed both a Training and a Predictive Web Service, you should see two separate Web services listed.</span></span> <span data-ttu-id="2ea95-155">The Predictive Web Service should end with "[predictive exp.]".</span><span class="sxs-lookup"><span data-stu-id="2ea95-155">The Predictive Web Service should end with "[predictive exp.]".</span></span>
> 
> 

1. <span data-ttu-id="2ea95-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2ea95-156">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2ea95-157">Open the Machine Learning tab. ![Machine learning workspace UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="2ea95-157">Open the Machine Learning tab. ![Machine learning workspace UI.][image4]</span></span>
3. <span data-ttu-id="2ea95-158">Select your workspace.</span><span class="sxs-lookup"><span data-stu-id="2ea95-158">Select your workspace.</span></span>
4. <span data-ttu-id="2ea95-159">Click **Web Services**.</span><span class="sxs-lookup"><span data-stu-id="2ea95-159">Click **Web Services**.</span></span>
5. <span data-ttu-id="2ea95-160">Select your Predictive Web Service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-160">Select your Predictive Web Service.</span></span>
6. <span data-ttu-id="2ea95-161">Verify that your new endpoint was added to the Web service.</span><span class="sxs-lookup"><span data-stu-id="2ea95-161">Verify that your new endpoint was added to the Web service.</span></span>

### <a name="check-the-workspace-that-your-web-service-is-in-to-ensure-it-is-in-the-correct-region"></a><span data-ttu-id="2ea95-162">Check the workspace that your web service is in to ensure it is in the correct region</span><span class="sxs-lookup"><span data-stu-id="2ea95-162">Check the workspace that your web service is in to ensure it is in the correct region</span></span>
1. <span data-ttu-id="2ea95-163">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2ea95-163">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2ea95-164">Select Machine Learning from the menu.</span><span class="sxs-lookup"><span data-stu-id="2ea95-164">Select Machine Learning from the menu.</span></span>
   <span data-ttu-id="2ea95-165">![Machine learning region UI.][image4]</span><span class="sxs-lookup"><span data-stu-id="2ea95-165">![Machine learning region UI.][image4]</span></span>
3. <span data-ttu-id="2ea95-166">Verify the location of your workspace.</span><span class="sxs-lookup"><span data-stu-id="2ea95-166">Verify the location of your workspace.</span></span>

<!-- Image Links -->

[image1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/ml-studio-tm-connnected-to-web-service-out.png
[image2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/addEndpoint-output.png
[image3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/azure-portal-update-resource.png
[image4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/azure-portal-machine-learning-tab.png
[image5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/ml-help-page-patch-url.png
[image6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-troubleshooting-retraining-a-model/retraining-output.png
[image7]: ./media/machine-learning-troubleshooting-retraining-a-model/web-services-tab.png






