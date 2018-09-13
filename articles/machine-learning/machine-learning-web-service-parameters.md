---
title: Use Azure Machine Learning Web Service Parameters | Microsoft Docs
description: How to use Azure Machine Learning Web Service Parameters to modify the behavior of your model when the web service is accessed.
services: machine-learning
documentationcenter: ''
author: raymondlaghaeian
manager: jhubbard
editor: cgronlun
ms.assetid: c49187db-b976-4731-89d6-11a0bf653db1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2017
ms.author: raymondl;garye
ms.openlocfilehash: ae6ea2a0f37b3f3e7cc862190af778c3138ff183
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564637"
---
# <a name="use-azure-machine-learning-web-service-parameters"></a><span data-ttu-id="97cdd-103">Use Azure Machine Learning Web Service Parameters</span><span class="sxs-lookup"><span data-stu-id="97cdd-103">Use Azure Machine Learning Web Service Parameters</span></span>
<span data-ttu-id="97cdd-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span><span class="sxs-lookup"><span data-stu-id="97cdd-104">An Azure Machine Learning web service is created by publishing an experiment that contains modules with configurable parameters.</span></span> <span data-ttu-id="97cdd-105">In some cases, you may want to change the module behavior while the web service is running.</span><span class="sxs-lookup"><span data-stu-id="97cdd-105">In some cases, you may want to change the module behavior while the web service is running.</span></span> <span data-ttu-id="97cdd-106">*Web Service Parameters* allow you to do this task.</span><span class="sxs-lookup"><span data-stu-id="97cdd-106">*Web Service Parameters* allow you to do this task.</span></span> 

<span data-ttu-id="97cdd-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span><span class="sxs-lookup"><span data-stu-id="97cdd-107">A common example is setting up the [Import Data][reader] module so that the user of the published web service can specify a different data source when the web service is accessed.</span></span> <span data-ttu-id="97cdd-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span><span class="sxs-lookup"><span data-stu-id="97cdd-108">Or configuring the [Export Data][writer] module so that a different destination can be specified.</span></span> <span data-ttu-id="97cdd-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span><span class="sxs-lookup"><span data-stu-id="97cdd-109">Some other examples include changing the number of bits for the [Feature Hashing][feature-hashing] module or the number of desired features for the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> 

<span data-ttu-id="97cdd-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span><span class="sxs-lookup"><span data-stu-id="97cdd-110">You can set Web Service Parameters and associate them with one or more module parameters in your experiment, and you can specify whether they are required or optional.</span></span> <span data-ttu-id="97cdd-111">The user of the web service can then provide values for these parameters when they call the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-111">The user of the web service can then provide values for these parameters when they call the web service.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-to-set-and-use-web-service-parameters"></a><span data-ttu-id="97cdd-112">How to set and use Web Service Parameters</span><span class="sxs-lookup"><span data-stu-id="97cdd-112">How to set and use Web Service Parameters</span></span>
<span data-ttu-id="97cdd-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span><span class="sxs-lookup"><span data-stu-id="97cdd-113">You define a Web Service Parameter by clicking the icon next to the parameter for a module and selecting "Set as web service parameter".</span></span> <span data-ttu-id="97cdd-114">This creates a new Web Service Parameter and connects it to that module parameter.</span><span class="sxs-lookup"><span data-stu-id="97cdd-114">This creates a new Web Service Parameter and connects it to that module parameter.</span></span> <span data-ttu-id="97cdd-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span><span class="sxs-lookup"><span data-stu-id="97cdd-115">Then, when the web service is accessed, the user can specify a value for the Web Service Parameter and it is applied to the module parameter.</span></span>

<span data-ttu-id="97cdd-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span><span class="sxs-lookup"><span data-stu-id="97cdd-116">Once you define a Web Service Parameter, it's available to any other module parameter in the experiment.</span></span> <span data-ttu-id="97cdd-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span><span class="sxs-lookup"><span data-stu-id="97cdd-117">If you define a Web Service Parameter associated with a parameter for one module, you can use that same Web Service Parameter for any other module, as long as the parameter expects the same type of value.</span></span> <span data-ttu-id="97cdd-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span><span class="sxs-lookup"><span data-stu-id="97cdd-118">For example, if the Web Service Parameter is a numeric value, then it can only be used for module parameters that expect a numeric value.</span></span> <span data-ttu-id="97cdd-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span><span class="sxs-lookup"><span data-stu-id="97cdd-119">When the user sets a value for the Web Service Parameter, it will be applied to all associated module parameters.</span></span>

<span data-ttu-id="97cdd-120">You can decide whether to provide a default value for the Web Service Parameter.</span><span class="sxs-lookup"><span data-stu-id="97cdd-120">You can decide whether to provide a default value for the Web Service Parameter.</span></span> <span data-ttu-id="97cdd-121">If you do, then the parameter is optional for the user of the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-121">If you do, then the parameter is optional for the user of the web service.</span></span> <span data-ttu-id="97cdd-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span><span class="sxs-lookup"><span data-stu-id="97cdd-122">If you don't provide a default value, then the user is required to enter a value when the web service is accessed.</span></span>

<span data-ttu-id="97cdd-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-123">The API documentation for the web service includes information for the web service user on how to specify the Web Service Parameter programmatically when accessing the web service.</span></span>

> [!NOTE]
> <span data-ttu-id="97cdd-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="97cdd-124">The API documentation for a classic web service is provided through the **API help page** link in the web service **DASHBOARD** in Machine Learning Studio.</span></span> <span data-ttu-id="97cdd-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-125">The API documentation for a new web service is provided through the [Azure Machine Learning Web Services](https://services.azureml.net/Quickstart) portal on the **Consume** and **Swagger API** pages for your web service.</span></span>
> 
> 

## <a name="example"></a><span data-ttu-id="97cdd-126">Example</span><span class="sxs-lookup"><span data-stu-id="97cdd-126">Example</span></span>
<span data-ttu-id="97cdd-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="97cdd-127">As an example, let's assume we have an experiment with an [Export Data][writer] module that sends information to Azure blob storage.</span></span> <span data-ttu-id="97cdd-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span><span class="sxs-lookup"><span data-stu-id="97cdd-128">We'll define a Web Service Parameter named "Blob path" that allows the web service user to change the path to the blob storage when the service is accessed.</span></span>

1. <span data-ttu-id="97cdd-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span><span class="sxs-lookup"><span data-stu-id="97cdd-129">In Machine Learning Studio, click the [Export Data][writer] module to select it.</span></span> <span data-ttu-id="97cdd-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span><span class="sxs-lookup"><span data-stu-id="97cdd-130">Its properties are shown in the Properties pane to the right of the experiment canvas.</span></span>
2. <span data-ttu-id="97cdd-131">Specify the storage type:</span><span class="sxs-lookup"><span data-stu-id="97cdd-131">Specify the storage type:</span></span>
   
   * <span data-ttu-id="97cdd-132">Under **Please specify data destination**, select "Azure Blob Storage".</span><span class="sxs-lookup"><span data-stu-id="97cdd-132">Under **Please specify data destination**, select "Azure Blob Storage".</span></span>
   * <span data-ttu-id="97cdd-133">Under **Please specify authentication type**, select "Account".</span><span class="sxs-lookup"><span data-stu-id="97cdd-133">Under **Please specify authentication type**, select "Account".</span></span>
   * <span data-ttu-id="97cdd-134">Enter the account information for the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="97cdd-134">Enter the account information for the Azure blob storage.</span></span> 
     <p /><span data-ttu-id="97cdd-135">
3. Click the icon to the right of the \*\*Path to blob beginning with container parameter\**.</span><span class="sxs-lookup"><span data-stu-id="97cdd-135">
3. Click the icon to the right of the \*\*Path to blob beginning with container parameter\**.</span></span> <span data-ttu-id="97cdd-136">It looks like this:</span><span class="sxs-lookup"><span data-stu-id="97cdd-136">It looks like this:</span></span>
   
   ![Web Service Parameter icon][icon]
   
   <span data-ttu-id="97cdd-138">Select "Set as web service parameter".</span><span class="sxs-lookup"><span data-stu-id="97cdd-138">Select "Set as web service parameter".</span></span>
   
   <span data-ttu-id="97cdd-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span><span class="sxs-lookup"><span data-stu-id="97cdd-139">An entry is added under **Web Service Parameters** at the bottom of the Properties pane with the name "Path to blob beginning with container".</span></span> <span data-ttu-id="97cdd-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span><span class="sxs-lookup"><span data-stu-id="97cdd-140">This is the Web Service Parameter that is now associated with this [Export Data][writer] module parameter.</span></span>
4. <span data-ttu-id="97cdd-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span><span class="sxs-lookup"><span data-stu-id="97cdd-141">To rename the Web Service Parameter, click the name, enter "Blob path", and press the **Enter** key.</span></span> 
5. <span data-ttu-id="97cdd-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span><span class="sxs-lookup"><span data-stu-id="97cdd-142">To provide a default value for the Web Service Parameter, click the icon to the right of the name, select "Provide default value", enter a value (for example, "container1/output1.csv"), and press the **Enter** key.</span></span>
   
   ![Web Service Parameter][parameter]
6. <span data-ttu-id="97cdd-144">Click **Run**.</span><span class="sxs-lookup"><span data-stu-id="97cdd-144">Click **Run**.</span></span> 
7. <span data-ttu-id="97cdd-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-145">Click **Deploy Web Service** and select **Deploy Web Service [Classic]** or **Deploy Web Service [New]** to deploy the web service.</span></span>

> [!NOTE] 
> <span data-ttu-id="97cdd-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-146">To deploy a New web service you must have sufficient permissions in the subscription to which you deploying the web service.</span></span> <span data-ttu-id="97cdd-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="97cdd-147">For more information see, [Manage a Web service using the Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span> 

<span data-ttu-id="97cdd-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span><span class="sxs-lookup"><span data-stu-id="97cdd-148">The user of the web service can now specify a new destination for the [Export Data][writer] module when accessing the web service.</span></span>

## <a name="more-information"></a><span data-ttu-id="97cdd-149">More information</span><span class="sxs-lookup"><span data-stu-id="97cdd-149">More information</span></span>
<span data-ttu-id="97cdd-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span><span class="sxs-lookup"><span data-stu-id="97cdd-150">For a more detailed example, see the [Web Service Parameters](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx) entry in the [Machine Learning Blog](http://blogs.technet.com/b/machinelearning/archive/2014/11/25/azureml-web-service-parameters.aspx).</span></span>

<span data-ttu-id="97cdd-151">For more information on accessing a Machine Learning web service, see [How to consume a published machine learning web service](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="97cdd-151">For more information on accessing a Machine Learning web service, see [How to consume a published machine learning web service](machine-learning-consume-web-services.md).</span></span>

<!-- Images -->
[icon]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-web-service-parameters/icon.png
[parameter]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-web-service-parameters/parameter.png


<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[reader]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
[writer]: https://msdn.microsoft.com/library/azure/7a391181-b6a7-4ad4-b82d-e419c0d6522c/



