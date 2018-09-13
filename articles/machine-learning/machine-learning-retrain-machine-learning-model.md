---
title: Retrain a Machine Learning Model | Microsoft Docs
description: Learn how to retrain a model and update the Web service to use the newly trained model in Azure Machine Learning.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: d1cb6088-4f7c-4c32-94f2-f7523dad9059
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 2719f8d2e88c8fe0c8e3a2aabbe567e21074ce96
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551987"
---
# <a name="retrain-a-machine-learning-model"></a><span data-ttu-id="e45d5-103">Retrain a Machine Learning Model</span><span class="sxs-lookup"><span data-stu-id="e45d5-103">Retrain a Machine Learning Model</span></span>
<span data-ttu-id="e45d5-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span><span class="sxs-lookup"><span data-stu-id="e45d5-104">As part of the process of operationalization of machine learning models in Azure Machine Learning, your model is trained and saved.</span></span> <span data-ttu-id="e45d5-105">You then use it to create a predicative Web service.</span><span class="sxs-lookup"><span data-stu-id="e45d5-105">You then use it to create a predicative Web service.</span></span> <span data-ttu-id="e45d5-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="e45d5-106">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span> 

<span data-ttu-id="e45d5-107">Models you create using Machine Learning are typically not static.</span><span class="sxs-lookup"><span data-stu-id="e45d5-107">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e45d5-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span><span class="sxs-lookup"><span data-stu-id="e45d5-108">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> 

<span data-ttu-id="e45d5-109">Retraining may occur frequently.</span><span class="sxs-lookup"><span data-stu-id="e45d5-109">Retraining may occur frequently.</span></span> <span data-ttu-id="e45d5-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="e45d5-110">With the Programmatic Retraining API feature, you can programmatically retrain the model using the Retraining APIs and update the Web service with the newly trained model.</span></span> 

<span data-ttu-id="e45d5-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span><span class="sxs-lookup"><span data-stu-id="e45d5-111">This document describes the retraining process, and shows you how to use the Retraining APIs.</span></span>

## <a name="why-retrain-defining-the-problem"></a><span data-ttu-id="e45d5-112">Why retrain: defining the problem</span><span class="sxs-lookup"><span data-stu-id="e45d5-112">Why retrain: defining the problem</span></span>
<span data-ttu-id="e45d5-113">As part of the machine learning training process, a model is trained using a set of data.</span><span class="sxs-lookup"><span data-stu-id="e45d5-113">As part of the machine learning training process, a model is trained using a set of data.</span></span> <span data-ttu-id="e45d5-114">Models you create using Machine Learning are typically not static.</span><span class="sxs-lookup"><span data-stu-id="e45d5-114">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="e45d5-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span><span class="sxs-lookup"><span data-stu-id="e45d5-115">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span>

<span data-ttu-id="e45d5-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span><span class="sxs-lookup"><span data-stu-id="e45d5-116">In these scenarios, a programmatic API provides a convenient way to allow you or the consumer of your APIs to create a client that can, on a one-time or regular basis, retrain the model using their own data.</span></span> <span data-ttu-id="e45d5-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="e45d5-117">They can then evaluate the results of retraining, and update the Web service API to use the newly trained model.</span></span>

> [!NOTE]
> <span data-ttu-id="e45d5-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span><span class="sxs-lookup"><span data-stu-id="e45d5-118">If you have an existing Training Experiment and New Web service, you may want to check out Retrain an existing Predictive Web service instead of following the walkthrough mentioned in the following section.</span></span>
> 
> 

## <a name="end-to-end-workflow"></a><span data-ttu-id="e45d5-119">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="e45d5-119">End-to-end workflow</span></span>
<span data-ttu-id="e45d5-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span><span class="sxs-lookup"><span data-stu-id="e45d5-120">The process involves the following components: A Training Experiment and a Predictive Experiment published as a Web service.</span></span> <span data-ttu-id="e45d5-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span><span class="sxs-lookup"><span data-stu-id="e45d5-121">To enable retraining of a trained model, the Training Experiment must be published as a Web service with the output of a trained model.</span></span> <span data-ttu-id="e45d5-122">This enables API access to the model for retraining.</span><span class="sxs-lookup"><span data-stu-id="e45d5-122">This enables API access to the model for retraining.</span></span> 

<span data-ttu-id="e45d5-123">The following steps apply to both New and Classic Web services:</span><span class="sxs-lookup"><span data-stu-id="e45d5-123">The following steps apply to both New and Classic Web services:</span></span>

<span data-ttu-id="e45d5-124">Create the initial Predictive Web service:</span><span class="sxs-lookup"><span data-stu-id="e45d5-124">Create the initial Predictive Web service:</span></span>

* <span data-ttu-id="e45d5-125">Create a training experiment</span><span class="sxs-lookup"><span data-stu-id="e45d5-125">Create a training experiment</span></span>
* <span data-ttu-id="e45d5-126">Create a predictive web experiment</span><span class="sxs-lookup"><span data-stu-id="e45d5-126">Create a predictive web experiment</span></span>
* <span data-ttu-id="e45d5-127">Deploy a predictive web service</span><span class="sxs-lookup"><span data-stu-id="e45d5-127">Deploy a predictive web service</span></span>

<span data-ttu-id="e45d5-128">Retrain the Web service:</span><span class="sxs-lookup"><span data-stu-id="e45d5-128">Retrain the Web service:</span></span>

* <span data-ttu-id="e45d5-129">Update training experiment to allow for retraining</span><span class="sxs-lookup"><span data-stu-id="e45d5-129">Update training experiment to allow for retraining</span></span>
* <span data-ttu-id="e45d5-130">Deploy the retraining web service</span><span class="sxs-lookup"><span data-stu-id="e45d5-130">Deploy the retraining web service</span></span>
* <span data-ttu-id="e45d5-131">Use the Batch Execution Service code to retrain the model</span><span class="sxs-lookup"><span data-stu-id="e45d5-131">Use the Batch Execution Service code to retrain the model</span></span>

<span data-ttu-id="e45d5-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="e45d5-132">For a walkthrough of the preceding steps, see [Retrain Machine Learning models programmatically](machine-learning-retrain-models-programmatically.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="e45d5-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="e45d5-133">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="e45d5-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="e45d5-134">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="e45d5-135">If you deployed a Classic Web Service:</span><span class="sxs-lookup"><span data-stu-id="e45d5-135">If you deployed a Classic Web Service:</span></span>

* <span data-ttu-id="e45d5-136">Create a new Endpoint on the Predictive Web service</span><span class="sxs-lookup"><span data-stu-id="e45d5-136">Create a new Endpoint on the Predictive Web service</span></span>
* <span data-ttu-id="e45d5-137">Get the PATCH URL and code</span><span class="sxs-lookup"><span data-stu-id="e45d5-137">Get the PATCH URL and code</span></span>
* <span data-ttu-id="e45d5-138">Use the PATCH URL to point the new Endpoint at the retrained model</span><span class="sxs-lookup"><span data-stu-id="e45d5-138">Use the PATCH URL to point the new Endpoint at the retrained model</span></span> 

<span data-ttu-id="e45d5-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="e45d5-139">For a walkthrough of the preceding steps, see [Retrain a Classic Web service](machine-learning-retrain-a-classic-web-service.md).</span></span>

<span data-ttu-id="e45d5-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span><span class="sxs-lookup"><span data-stu-id="e45d5-140">If you run into difficulties retraining a Classic Web service, see [Troubleshooting the retraining of an Azure Machine Learning Classic Web service](machine-learning-troubleshooting-retraining-models.md).</span></span>

<span data-ttu-id="e45d5-141">If you deployed a New Web service:</span><span class="sxs-lookup"><span data-stu-id="e45d5-141">If you deployed a New Web service:</span></span>

* <span data-ttu-id="e45d5-142">Sign in to your Azure Resource Manager account</span><span class="sxs-lookup"><span data-stu-id="e45d5-142">Sign in to your Azure Resource Manager account</span></span>
* <span data-ttu-id="e45d5-143">Get the Web service definition</span><span class="sxs-lookup"><span data-stu-id="e45d5-143">Get the Web service definition</span></span>
* <span data-ttu-id="e45d5-144">Export the Web Service Definition as JSON</span><span class="sxs-lookup"><span data-stu-id="e45d5-144">Export the Web Service Definition as JSON</span></span>
* <span data-ttu-id="e45d5-145">Update the reference to the `ilearner` blob in the JSON</span><span class="sxs-lookup"><span data-stu-id="e45d5-145">Update the reference to the `ilearner` blob in the JSON</span></span>
* <span data-ttu-id="e45d5-146">Import the JSON into a Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="e45d5-146">Import the JSON into a Web Service Definition</span></span>
* <span data-ttu-id="e45d5-147">Update the Web service with new Web Service Definition</span><span class="sxs-lookup"><span data-stu-id="e45d5-147">Update the Web service with new Web Service Definition</span></span>

<span data-ttu-id="e45d5-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e45d5-148">For a walkthrough of the preceding steps, see [Retrain a New Web service using the Machine Learning Management PowerShell cmdlets](machine-learning-retrain-new-web-service-using-powershell.md).</span></span>

<span data-ttu-id="e45d5-149">The process for setting up retraining for a Classic Web service involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="e45d5-149">The process for setting up retraining for a Classic Web service involves the following steps:</span></span>

![Retraining process overview][1]

<span data-ttu-id="e45d5-151">The process for setting up retraining for a New Web service involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="e45d5-151">The process for setting up retraining for a New Web service involves the following steps:</span></span>

![Retraining process overview][7]

## <a name="other-resources"></a><span data-ttu-id="e45d5-153">Other Resources</span><span class="sxs-lookup"><span data-stu-id="e45d5-153">Other Resources</span></span>
* [<span data-ttu-id="e45d5-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e45d5-154">Retraining and Updating Azure Machine Learning models with Azure Data Factory</span></span>](https://azure.microsoft.com/blog/retraining-and-updating-azure-machine-learning-models-with-azure-data-factory/)
* [<span data-ttu-id="e45d5-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e45d5-155">Create many Machine Learning models and web service endpoints from one experiment using PowerShell</span></span>](machine-learning-create-models-and-endpoints-with-powershell.md)
* <span data-ttu-id="e45d5-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e45d5-156">The [AML Retraining Models Using APIs](https://www.youtube.com/watch?v=wwjglA8xllg) video shows you how to retrain Machine Learning models created in Azure Machine Learning using the Retraining APIs and PowerShell.</span></span>

<!--image links-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE01.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-retrain-machine-learning-model/machine-learning-retrain-models-programmatically-IMAGE07.png



