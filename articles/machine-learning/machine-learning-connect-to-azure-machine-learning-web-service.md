---
title: Connect to a Machine Learning Web Service | Microsoft Docs
description: With C# or Python, connect to an Azure Machine Learning Web service using an authorization key.
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 59b07bab-b60f-48c4-a385-a162e50ec7c2
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: garye
ms.openlocfilehash: 2dfcdf2207d1437a917c493075e3245bd58381ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554214"
---
# <a name="connect-to-an-azure-machine-learning-web-service"></a><span data-ttu-id="99f39-103">Connect to an Azure Machine Learning Web Service</span><span class="sxs-lookup"><span data-stu-id="99f39-103">Connect to an Azure Machine Learning Web Service</span></span>
<span data-ttu-id="99f39-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span><span class="sxs-lookup"><span data-stu-id="99f39-104">The Azure Machine Learning developer experience is a Web service API to make predictions from input data in real time or in batch mode.</span></span> <span data-ttu-id="99f39-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-105">You use Azure Machine Learning Studio to create predictions and deploy an Azure Machine Learning Web service.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="99f39-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span><span class="sxs-lookup"><span data-stu-id="99f39-106">To learn about how to create and deploy a Machine Learning Web service using Machine Learning Studio:</span></span>

* <span data-ttu-id="99f39-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="99f39-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](machine-learning-create-experiment.md).</span></span>
* <span data-ttu-id="99f39-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="99f39-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="99f39-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="99f39-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

## <a name="azure-machine-learning-web-service"></a><span data-ttu-id="99f39-110">Azure Machine Learning Web service</span><span class="sxs-lookup"><span data-stu-id="99f39-110">Azure Machine Learning Web service</span></span>
<span data-ttu-id="99f39-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span><span class="sxs-lookup"><span data-stu-id="99f39-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="99f39-112">A Machine Learning Web service call returns prediction results to an external application.</span><span class="sxs-lookup"><span data-stu-id="99f39-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="99f39-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span><span class="sxs-lookup"><span data-stu-id="99f39-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="99f39-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span><span class="sxs-lookup"><span data-stu-id="99f39-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="99f39-115">Azure Machine Learning has two types of services:</span><span class="sxs-lookup"><span data-stu-id="99f39-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="99f39-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="99f39-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="99f39-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span><span class="sxs-lookup"><span data-stu-id="99f39-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="99f39-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="99f39-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="99f39-119">Get an Azure Machine Learning authorization key</span><span class="sxs-lookup"><span data-stu-id="99f39-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="99f39-120">When you deploy your experiment, API keys are generated for the Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="99f39-121">You can retrieve the keys from several locations.</span><span class="sxs-lookup"><span data-stu-id="99f39-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="99f39-122">From the Microsoft Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="99f39-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="99f39-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="99f39-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="99f39-124">To retrieve the API key for a New Machine Learning Web service:</span><span class="sxs-lookup"><span data-stu-id="99f39-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="99f39-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span><span class="sxs-lookup"><span data-stu-id="99f39-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="99f39-126">Click the Web service for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="99f39-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="99f39-127">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="99f39-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="99f39-128">Copy and save the **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="99f39-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="99f39-129">To retrieve the API key for a Classic Machine Learning Web service:</span><span class="sxs-lookup"><span data-stu-id="99f39-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="99f39-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span><span class="sxs-lookup"><span data-stu-id="99f39-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="99f39-131">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="99f39-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="99f39-132">Click the endpoint for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="99f39-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="99f39-133">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="99f39-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="99f39-134">Copy and save the **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="99f39-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="99f39-135">Classic Web service</span><span class="sxs-lookup"><span data-stu-id="99f39-135">Classic Web service</span></span>
 <span data-ttu-id="99f39-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="99f39-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio or the Azure classic portal.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="99f39-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="99f39-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="99f39-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span><span class="sxs-lookup"><span data-stu-id="99f39-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="99f39-139">Click a Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-139">Click a Web service.</span></span> <span data-ttu-id="99f39-140">The **API key** is on the **DASHBOARD** tab.</span><span class="sxs-lookup"><span data-stu-id="99f39-140">The **API key** is on the **DASHBOARD** tab.</span></span>

#### <a name="azure-classic-portal"></a><span data-ttu-id="99f39-141">Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="99f39-141">Azure classic portal</span></span>
1. <span data-ttu-id="99f39-142">Click **MACHINE LEARNING** on the left.</span><span class="sxs-lookup"><span data-stu-id="99f39-142">Click **MACHINE LEARNING** on the left.</span></span>
2. <span data-ttu-id="99f39-143">Click the workspace in which your Web service is located.</span><span class="sxs-lookup"><span data-stu-id="99f39-143">Click the workspace in which your Web service is located.</span></span>
3. <span data-ttu-id="99f39-144">Click **WEB SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="99f39-144">Click **WEB SERVICES**.</span></span>
4. <span data-ttu-id="99f39-145">Click a Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-145">Click a Web service.</span></span>
5. <span data-ttu-id="99f39-146">Click an endpoint.</span><span class="sxs-lookup"><span data-stu-id="99f39-146">Click an endpoint.</span></span> <span data-ttu-id="99f39-147">The “API KEY” is down at the lower-right.</span><span class="sxs-lookup"><span data-stu-id="99f39-147">The “API KEY” is down at the lower-right.</span></span>

## <a id="connect"></a><span data-ttu-id="99f39-148">Connect to a Machine Learning Web service</span><span class="sxs-lookup"><span data-stu-id="99f39-148">Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="99f39-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span><span class="sxs-lookup"><span data-stu-id="99f39-149">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="99f39-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span><span class="sxs-lookup"><span data-stu-id="99f39-150">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="99f39-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-151">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="99f39-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="99f39-152">See [Azure Machine Learning Walkthrough- Deploy Web Service](machine-learning-walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="99f39-153">The Machine Learning API help contains details about a prediction Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-153">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="99f39-154">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="99f39-154">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="99f39-155">Click the endpoint for which you want to view the API Help Page.</span><span class="sxs-lookup"><span data-stu-id="99f39-155">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="99f39-156">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="99f39-156">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="99f39-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span><span class="sxs-lookup"><span data-stu-id="99f39-157">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="99f39-158">**To view Machine Learning API help for a New Web service**</span><span class="sxs-lookup"><span data-stu-id="99f39-158">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="99f39-159">In the Azure Machine Learning Web Services Portal:</span><span class="sxs-lookup"><span data-stu-id="99f39-159">In the Azure Machine Learning Web Services Portal:</span></span>

1. <span data-ttu-id="99f39-160">Click **WEB SERVICES** on the top menu.</span><span class="sxs-lookup"><span data-stu-id="99f39-160">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="99f39-161">Click the Web service for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="99f39-161">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="99f39-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span><span class="sxs-lookup"><span data-stu-id="99f39-162">Click **Consume** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="99f39-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span><span class="sxs-lookup"><span data-stu-id="99f39-163">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="99f39-164">C# Sample</span><span class="sxs-lookup"><span data-stu-id="99f39-164">C# Sample</span></span>
<span data-ttu-id="99f39-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span><span class="sxs-lookup"><span data-stu-id="99f39-165">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="99f39-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span><span class="sxs-lookup"><span data-stu-id="99f39-166">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="99f39-167">You authenticate to the Machine Learning service with an API key.</span><span class="sxs-lookup"><span data-stu-id="99f39-167">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="99f39-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span><span class="sxs-lookup"><span data-stu-id="99f39-168">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="99f39-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="99f39-169">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="99f39-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span><span class="sxs-lookup"><span data-stu-id="99f39-170">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="99f39-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="99f39-171">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="99f39-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="99f39-172">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="99f39-173">**To run the code sample**</span><span class="sxs-lookup"><span data-stu-id="99f39-173">**To run the code sample**</span></span>

1. <span data-ttu-id="99f39-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span><span class="sxs-lookup"><span data-stu-id="99f39-174">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="99f39-175">Assign apiKey with the key from a Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-175">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="99f39-176">See **Get an Azure Machine Learning authorization key** above.</span><span class="sxs-lookup"><span data-stu-id="99f39-176">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="99f39-177">Assign serviceUri with the Request URI.</span><span class="sxs-lookup"><span data-stu-id="99f39-177">Assign serviceUri with the Request URI.</span></span>

### <a name="python-sample"></a><span data-ttu-id="99f39-178">Python Sample</span><span class="sxs-lookup"><span data-stu-id="99f39-178">Python Sample</span></span>
<span data-ttu-id="99f39-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span><span class="sxs-lookup"><span data-stu-id="99f39-179">To connect to a Machine Learning Web service, use the **urllib2** library passing ScoreData.</span></span> <span data-ttu-id="99f39-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span><span class="sxs-lookup"><span data-stu-id="99f39-180">ScoreData contains a FeatureVector, an n-dimensional  vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="99f39-181">You authenticate to the Machine Learning service with an API key.</span><span class="sxs-lookup"><span data-stu-id="99f39-181">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="99f39-182">**To run the code sample**</span><span class="sxs-lookup"><span data-stu-id="99f39-182">**To run the code sample**</span></span>

1. <span data-ttu-id="99f39-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span><span class="sxs-lookup"><span data-stu-id="99f39-183">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="99f39-184">Assign apiKey with the key from a Web service.</span><span class="sxs-lookup"><span data-stu-id="99f39-184">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="99f39-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span><span class="sxs-lookup"><span data-stu-id="99f39-185">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="99f39-186">Assign serviceUri with the Request URI.</span><span class="sxs-lookup"><span data-stu-id="99f39-186">Assign serviceUri with the Request URI.</span></span>

