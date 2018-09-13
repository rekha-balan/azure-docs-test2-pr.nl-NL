---
title: Deploying a new web service in Azure Machine Learning | Microsoft Docs
description: The workflow of deploying an ARM based web service
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: a358b04f-0d08-4d50-820e-eeac971854cf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: v-donglo
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: machine-learning-publish-a-machine-learning-web-service
ms.openlocfilehash: 878ed813d67ccf3bb27e8a907a07a777b79392f7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555067"
---
# <a name="deploy-a-new-web-service"></a><span data-ttu-id="9311b-103">Deploy a new web service</span><span class="sxs-lookup"><span data-stu-id="9311b-103">Deploy a new web service</span></span>
<span data-ttu-id="9311b-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span><span class="sxs-lookup"><span data-stu-id="9311b-104">Microsoft Azure Machine learning now provides web services that are based on [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) allowing for new billing plan options and deploying your web service to multiple regions.</span></span>

<span data-ttu-id="9311b-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span><span class="sxs-lookup"><span data-stu-id="9311b-105">The general workflow to deploy a web service using Microsoft Azure Machine Learning Web Services is:</span></span>

* <span data-ttu-id="9311b-106">Create a predictive experiment</span><span class="sxs-lookup"><span data-stu-id="9311b-106">Create a predictive experiment</span></span>
* <span data-ttu-id="9311b-107">deploy it</span><span class="sxs-lookup"><span data-stu-id="9311b-107">deploy it</span></span>
* <span data-ttu-id="9311b-108">configure its name</span><span class="sxs-lookup"><span data-stu-id="9311b-108">configure its name</span></span>
* <span data-ttu-id="9311b-109">billing plan</span><span class="sxs-lookup"><span data-stu-id="9311b-109">billing plan</span></span>
* <span data-ttu-id="9311b-110">test it</span><span class="sxs-lookup"><span data-stu-id="9311b-110">test it</span></span>
* <span data-ttu-id="9311b-111">consume it.</span><span class="sxs-lookup"><span data-stu-id="9311b-111">consume it.</span></span>

<span data-ttu-id="9311b-112">The following graphic illustrates the workflow.</span><span class="sxs-lookup"><span data-stu-id="9311b-112">The following graphic illustrates the workflow.</span></span>

![Web service deployment workflow][1]

## <a name="deploy-web-service-from-studio"></a><span data-ttu-id="9311b-114">Deploy web service from Studio</span><span class="sxs-lookup"><span data-stu-id="9311b-114">Deploy web service from Studio</span></span>
<span data-ttu-id="9311b-115">To deploy an experiment as a new web service.</span><span class="sxs-lookup"><span data-stu-id="9311b-115">To deploy an experiment as a new web service.</span></span> <span data-ttu-id="9311b-116">Sign into the Machine Learning Studio and create a new predictive web service.</span><span class="sxs-lookup"><span data-stu-id="9311b-116">Sign into the Machine Learning Studio and create a new predictive web service.</span></span> 

<span data-ttu-id="9311b-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span><span class="sxs-lookup"><span data-stu-id="9311b-117">**Note**: If you have already deployed an experiment as a classic web service you cannot deploy it as a new web service.</span></span>

<span data-ttu-id="9311b-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span><span class="sxs-lookup"><span data-stu-id="9311b-118">Click **Run** at the bottom of the experiment canvas and then click **Deploy Web Service** and **Deploy Web Service [New]**.</span></span> <span data-ttu-id="9311b-119">The deployment page of the Machine Learning Web Service manager will open.</span><span class="sxs-lookup"><span data-stu-id="9311b-119">The deployment page of the Machine Learning Web Service manager will open.</span></span>

## <a name="machine-learning-web-service-manager-deploy-experiment-page"></a><span data-ttu-id="9311b-120">Machine Learning Web Service Manager Deploy Experiment Page</span><span class="sxs-lookup"><span data-stu-id="9311b-120">Machine Learning Web Service Manager Deploy Experiment Page</span></span>
<span data-ttu-id="9311b-121">On the Deploy Experiment page, enter a name for the web service.</span><span class="sxs-lookup"><span data-stu-id="9311b-121">On the Deploy Experiment page, enter a name for the web service.</span></span>
<span data-ttu-id="9311b-122">Select a pricing plan.</span><span class="sxs-lookup"><span data-stu-id="9311b-122">Select a pricing plan.</span></span> <span data-ttu-id="9311b-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span><span class="sxs-lookup"><span data-stu-id="9311b-123">If you have an existing pricing plan you can select it, otherwise you must create a new price plan for the service.</span></span> 

1. <span data-ttu-id="9311b-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span><span class="sxs-lookup"><span data-stu-id="9311b-124">In the **Price Plan** drop down, select an existing plan or select the **Select new plan** option.</span></span>
2. <span data-ttu-id="9311b-125">In **Plan Name**, type a name that will identify the plan on your bill.</span><span class="sxs-lookup"><span data-stu-id="9311b-125">In **Plan Name**, type a name that will identify the plan on your bill.</span></span>
3. <span data-ttu-id="9311b-126">Select one of the **Monthly Plan Tiers**.</span><span class="sxs-lookup"><span data-stu-id="9311b-126">Select one of the **Monthly Plan Tiers**.</span></span> <span data-ttu-id="9311b-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span><span class="sxs-lookup"><span data-stu-id="9311b-127">Note that the plan tiers default to the plans for your default region and your web service is deployed to that region.</span></span>

<span data-ttu-id="9311b-128">Click **Deploy** and the Quickstart page for your web service opens.</span><span class="sxs-lookup"><span data-stu-id="9311b-128">Click **Deploy** and the Quickstart page for your web service opens.</span></span>

## <a name="quickstart-page"></a><span data-ttu-id="9311b-129">Quickstart page</span><span class="sxs-lookup"><span data-stu-id="9311b-129">Quickstart page</span></span>
<span data-ttu-id="9311b-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span><span class="sxs-lookup"><span data-stu-id="9311b-130">The web service Quickstart page gives you access and guidance on the most common tasks you will perform after creating a new web service.</span></span> <span data-ttu-id="9311b-131">From here you can easily access both the **Test** page and **Consume** page.</span><span class="sxs-lookup"><span data-stu-id="9311b-131">From here you can easily access both the **Test** page and **Consume** page.</span></span>

## <a name="testing-your-web-service"></a><span data-ttu-id="9311b-132">Testing your web service</span><span class="sxs-lookup"><span data-stu-id="9311b-132">Testing your web service</span></span>
<span data-ttu-id="9311b-133">From the Quickstart page, click Test web service under common tasks.</span><span class="sxs-lookup"><span data-stu-id="9311b-133">From the Quickstart page, click Test web service under common tasks.</span></span>   

<span data-ttu-id="9311b-134">To test the web service as a Request-Response Service (RRS):</span><span class="sxs-lookup"><span data-stu-id="9311b-134">To test the web service as a Request-Response Service (RRS):</span></span>

* <span data-ttu-id="9311b-135">Click **Test** on the menu bar.</span><span class="sxs-lookup"><span data-stu-id="9311b-135">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="9311b-136">Click **Request-Response**.</span><span class="sxs-lookup"><span data-stu-id="9311b-136">Click **Request-Response**.</span></span>
* <span data-ttu-id="9311b-137">Enter appropriate values for the input columns of your experiment.</span><span class="sxs-lookup"><span data-stu-id="9311b-137">Enter appropriate values for the input columns of your experiment.</span></span>
* <span data-ttu-id="9311b-138">Click Test **Request-Response**.</span><span class="sxs-lookup"><span data-stu-id="9311b-138">Click Test **Request-Response**.</span></span>

<span data-ttu-id="9311b-139">You results will display on the right hand side of the page.</span><span class="sxs-lookup"><span data-stu-id="9311b-139">You results will display on the right hand side of the page.</span></span>

<span data-ttu-id="9311b-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span><span class="sxs-lookup"><span data-stu-id="9311b-140">To test a Batch Execution Service (BES) web service, you will use a CSV file:</span></span>

* <span data-ttu-id="9311b-141">Click **Test** on the menu bar.</span><span class="sxs-lookup"><span data-stu-id="9311b-141">Click **Test** on the menu bar.</span></span>
* <span data-ttu-id="9311b-142">Click **Batch**.</span><span class="sxs-lookup"><span data-stu-id="9311b-142">Click **Batch**.</span></span>
* <span data-ttu-id="9311b-143">Under your input, click Browse and navigate to your sample data file.</span><span class="sxs-lookup"><span data-stu-id="9311b-143">Under your input, click Browse and navigate to your sample data file.</span></span>
* <span data-ttu-id="9311b-144">Click **Test**.</span><span class="sxs-lookup"><span data-stu-id="9311b-144">Click **Test**.</span></span>

<span data-ttu-id="9311b-145">The status of your test is displayed under **Test Batch Jobs**.</span><span class="sxs-lookup"><span data-stu-id="9311b-145">The status of your test is displayed under **Test Batch Jobs**.</span></span>

## <a name="consuming-your-web-service"></a><span data-ttu-id="9311b-146">Consuming your Web Service</span><span class="sxs-lookup"><span data-stu-id="9311b-146">Consuming your Web Service</span></span>
<span data-ttu-id="9311b-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span><span class="sxs-lookup"><span data-stu-id="9311b-147">When deployed as a web service, Azure Machine Learning experiments provide a REST API that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="9311b-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span><span class="sxs-lookup"><span data-stu-id="9311b-148">This is because the simple REST API accepts and responds with JSON formatted messages.</span></span> <span data-ttu-id="9311b-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span><span class="sxs-lookup"><span data-stu-id="9311b-149">The Azure Machine Learning portal provides code that can be used to call the web service in R, C#, and Python.</span></span>

<span data-ttu-id="9311b-150">On the Consuming page you can find:</span><span class="sxs-lookup"><span data-stu-id="9311b-150">On the Consuming page you can find:</span></span>

* <span data-ttu-id="9311b-151">The API key and URI's for consuming web service in apps.</span><span class="sxs-lookup"><span data-stu-id="9311b-151">The API key and URI's for consuming web service in apps.</span></span>
* <span data-ttu-id="9311b-152">Excel and web app templates to kick start your consumption process.</span><span class="sxs-lookup"><span data-stu-id="9311b-152">Excel and web app templates to kick start your consumption process.</span></span>
* <span data-ttu-id="9311b-153">Sample code in C#, python, and R to get you started.</span><span class="sxs-lookup"><span data-stu-id="9311b-153">Sample code in C#, python, and R to get you started.</span></span>

<span data-ttu-id="9311b-154">For more information on consuming web services, see [How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="9311b-154">For more information on consuming web services, see [How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment](machine-learning-consume-web-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9311b-155">Next Steps</span><span class="sxs-lookup"><span data-stu-id="9311b-155">Next Steps</span></span>
<span data-ttu-id="9311b-156">For more information on consuming web services, see:</span><span class="sxs-lookup"><span data-stu-id="9311b-156">For more information on consuming web services, see:</span></span>

[<span data-ttu-id="9311b-157">How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment</span><span class="sxs-lookup"><span data-stu-id="9311b-157">How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment</span></span>](machine-learning-consume-web-services.md)

[<span data-ttu-id="9311b-158">Azure Machine Learning Web Services: Deployment and consumption</span><span class="sxs-lookup"><span data-stu-id="9311b-158">Azure Machine Learning Web Services: Deployment and consumption</span></span>](machine-learning-deploy-consume-web-service-guide.md)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-webservice-deploy-a-web-service/armdeploymentworkflow.png


<!--links-->

