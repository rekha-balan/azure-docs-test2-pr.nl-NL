---
title: 'Azure Machine Learning Web Services: Deployment and consumption | Microsoft Docs'
description: Resources for deploying and consuming web services.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.assetid: 47635376-d1f4-4ea4-a6af-bd1f99f69a69
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 6db98921b48abd1e7c62a010e9ad7a7492484bd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554111"
---
# <a name="azure-machine-learning-web-services-deployment-and-consumption"></a><span data-ttu-id="35297-103">Azure Machine Learning Web Services: Deployment and consumption</span><span class="sxs-lookup"><span data-stu-id="35297-103">Azure Machine Learning Web Services: Deployment and consumption</span></span>
<span data-ttu-id="35297-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span><span class="sxs-lookup"><span data-stu-id="35297-104">You can use Azure Machine Learning to deploy machine-learning workflows and models as web services.</span></span> <span data-ttu-id="35297-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span><span class="sxs-lookup"><span data-stu-id="35297-105">These web services can then be used to call the machine-learning models from applications over the Internet to do predictions in real time or in batch mode.</span></span> <span data-ttu-id="35297-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span><span class="sxs-lookup"><span data-stu-id="35297-106">Because the web services are RESTful, you can call them from various programming languages and platforms, such as .NET and Java, and from applications, such as Excel.</span></span>

<span data-ttu-id="35297-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span><span class="sxs-lookup"><span data-stu-id="35297-107">The next sections provide links to walkthroughs, code, and documentation to help get you started.</span></span>

## <a name="deploy-a-web-service"></a><span data-ttu-id="35297-108">Deploy a web service</span><span class="sxs-lookup"><span data-stu-id="35297-108">Deploy a web service</span></span>
### <a name="with-azure-machine-learning-studio"></a><span data-ttu-id="35297-109">With Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="35297-109">With Azure Machine Learning Studio</span></span>
<span data-ttu-id="35297-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span><span class="sxs-lookup"><span data-stu-id="35297-110">Machine Learning Studio and the Microsoft Azure Machine Learning Web Services portal help you deploy and manage a web service without writing code.</span></span>

<span data-ttu-id="35297-111">The following links provide general Information about how to deploy a new web service:</span><span class="sxs-lookup"><span data-stu-id="35297-111">The following links provide general Information about how to deploy a new web service:</span></span>

* <span data-ttu-id="35297-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="35297-112">For an overview about how to deploy a new web service that's based on Azure Resource Manager, see [Deploy a new web service](machine-learning-webservice-deploy-a-web-service.md).</span></span>
* <span data-ttu-id="35297-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="35297-113">For a walkthrough about how to deploy a web service, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="35297-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="35297-114">For a full walkthrough about how to create and deploy a web service, see [Walkthrough Step 1: Create a Machine Learning workspace](machine-learning-walkthrough-1-create-ml-workspace.md).</span></span>
* <span data-ttu-id="35297-115">For specific examples that deploy a web service, see:</span><span class="sxs-lookup"><span data-stu-id="35297-115">For specific examples that deploy a web service, see:</span></span>

  * [<span data-ttu-id="35297-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="35297-116">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
  * [<span data-ttu-id="35297-117">How to deploy a web service to multiple regions</span><span class="sxs-lookup"><span data-stu-id="35297-117">How to deploy a web service to multiple regions</span></span>](machine-learning-how-to-deploy-to-multiple-regions.md)

### <a name="with-web-services-resource-provider-apis-azure-resource-manager-apis"></a><span data-ttu-id="35297-118">With web services resource provider APIs (Azure Resource Manager APIs)</span><span class="sxs-lookup"><span data-stu-id="35297-118">With web services resource provider APIs (Azure Resource Manager APIs)</span></span>
<span data-ttu-id="35297-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span><span class="sxs-lookup"><span data-stu-id="35297-119">The Azure Machine Learning resource provider for web services enables deployment and management of web services by using REST API calls.</span></span> <span data-ttu-id="35297-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span><span class="sxs-lookup"><span data-stu-id="35297-120">For additional details, see the [Machine Learning Web Service (REST)](/rest/api/machinelearning/index) reference.</span></span>

<!-- [Machine Learning Web Service (REST)](https://msdn.microsoft.com/library/azure/mt767538.aspx) reference. -->


### <a name="with-powershell-cmdlets"></a><span data-ttu-id="35297-121">With PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="35297-121">With PowerShell cmdlets</span></span>
<span data-ttu-id="35297-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="35297-122">Azure Machine Learning resource provider for web services enables deployment and management of web services by using PowerShell cmdlets.</span></span>

<span data-ttu-id="35297-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="35297-123">To use the cmdlets, you must first sign in to your Azure account from within the PowerShell environment by using the [Add-AzureRmAccount](https://msdn.microsoft.com/library/mt619267.aspx) cmdlet.</span></span> <span data-ttu-id="35297-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span><span class="sxs-lookup"><span data-stu-id="35297-124">If you are unfamiliar with how to call PowerShell commands that are based on Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md#log-in-to-your-azure-account).</span></span>

<span data-ttu-id="35297-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span><span class="sxs-lookup"><span data-stu-id="35297-125">To export your predictive experiment, use [this sample code](https://github.com/ritwik20/AzureML-WebServices).</span></span> <span data-ttu-id="35297-126">After you create the .exe file from the code, you can type:</span><span class="sxs-lookup"><span data-stu-id="35297-126">After you create the .exe file from the code, you can type:</span></span>

    C:\<folder>\GetWSD <experiment-url> <workspace-auth-token>

<span data-ttu-id="35297-127">Running the application creates a web service JSON template.</span><span class="sxs-lookup"><span data-stu-id="35297-127">Running the application creates a web service JSON template.</span></span> <span data-ttu-id="35297-128">To use the template to deploy a web service, you must add the following information:</span><span class="sxs-lookup"><span data-stu-id="35297-128">To use the template to deploy a web service, you must add the following information:</span></span>

* <span data-ttu-id="35297-129">Storage account name and key</span><span class="sxs-lookup"><span data-stu-id="35297-129">Storage account name and key</span></span>

    <span data-ttu-id="35297-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="35297-130">You can get the storage account name and key from either the [Azure portal](https://portal.azure.com/) or the [Azure classic portal](http://manage.windowsazure.com/).</span></span>
* <span data-ttu-id="35297-131">Commitment plan ID</span><span class="sxs-lookup"><span data-stu-id="35297-131">Commitment plan ID</span></span>

    <span data-ttu-id="35297-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span><span class="sxs-lookup"><span data-stu-id="35297-132">You can get the plan ID from the [Azure Machine Learning Web Services](https://services.azureml.net) portal by signing in and clicking a plan name.</span></span>

<span data-ttu-id="35297-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span><span class="sxs-lookup"><span data-stu-id="35297-133">Add them to the JSON template as children of the *Properties* node at the same level as the *MachineLearningWorkspace* node.</span></span>

<span data-ttu-id="35297-134">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="35297-134">Here's an example:</span></span>

    "StorageAccount": {
            "name": "YourStorageAccountName",
            "key": "YourStorageAccountKey"
    },
    "CommitmentPlan": {
        "id": "subscriptions/YouSubscriptionID/resourceGroups/YourResourceGroupID/providers/Microsoft.MachineLearning/commitmentPlans/YourPlanName"
    }

<span data-ttu-id="35297-135">See the following articles and sample code for additional details:</span><span class="sxs-lookup"><span data-stu-id="35297-135">See the following articles and sample code for additional details:</span></span>

* <span data-ttu-id="35297-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span><span class="sxs-lookup"><span data-stu-id="35297-136">[Azure Machine Learning Cmdlets](https://msdn.microsoft.com/library/azure/mt767952.aspx) reference on MSDN</span></span>
* <span data-ttu-id="35297-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span><span class="sxs-lookup"><span data-stu-id="35297-137">Sample [walkthrough](https://github.com/raymondlaghaeian/azureml-webservices-arm-powershell/blob/master/sample-commands.txt) on GitHub</span></span>

## <a name="consume-the-web-services"></a><span data-ttu-id="35297-138">Consume the web services</span><span class="sxs-lookup"><span data-stu-id="35297-138">Consume the web services</span></span>
### <a name="from-the-azure-machine-learning-web-services-ui-testing"></a><span data-ttu-id="35297-139">From the Azure Machine Learning Web Services UI (Testing)</span><span class="sxs-lookup"><span data-stu-id="35297-139">From the Azure Machine Learning Web Services UI (Testing)</span></span>
<span data-ttu-id="35297-140">You can test your web service from the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="35297-140">You can test your web service from the Azure Machine Learning Web Services portal.</span></span> <span data-ttu-id="35297-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span><span class="sxs-lookup"><span data-stu-id="35297-141">This includes testing the Request-Response service (RRS) and Batch Execution service (BES) interfaces.</span></span>

* [<span data-ttu-id="35297-142">Deploy a new web service</span><span class="sxs-lookup"><span data-stu-id="35297-142">Deploy a new web service</span></span>](machine-learning-webservice-deploy-a-web-service.md)
* [<span data-ttu-id="35297-143">Deploy an Azure Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="35297-143">Deploy an Azure Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
* [<span data-ttu-id="35297-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span><span class="sxs-lookup"><span data-stu-id="35297-144">Walkthrough Step 5: Deploy the Azure Machine Learning web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)

### <a name="from-excel"></a><span data-ttu-id="35297-145">From Excel</span><span class="sxs-lookup"><span data-stu-id="35297-145">From Excel</span></span>
<span data-ttu-id="35297-146">You can download an Excel template that consumes the web service:</span><span class="sxs-lookup"><span data-stu-id="35297-146">You can download an Excel template that consumes the web service:</span></span>

* [<span data-ttu-id="35297-147">Consuming an Azure Machine Learning web service from Excel</span><span class="sxs-lookup"><span data-stu-id="35297-147">Consuming an Azure Machine Learning web service from Excel</span></span>](machine-learning-consuming-from-excel.md)
* [<span data-ttu-id="35297-148">Excel add-in for Azure Machine Learning Web Services</span><span class="sxs-lookup"><span data-stu-id="35297-148">Excel add-in for Azure Machine Learning Web Services</span></span>](machine-learning-excel-add-in-for-web-services.md)

### <a name="from-a-rest-based-client"></a><span data-ttu-id="35297-149">From a REST-based client</span><span class="sxs-lookup"><span data-stu-id="35297-149">From a REST-based client</span></span>
<span data-ttu-id="35297-150">Azure Machine Learning Web Services are RESTful APIs.</span><span class="sxs-lookup"><span data-stu-id="35297-150">Azure Machine Learning Web Services are RESTful APIs.</span></span> <span data-ttu-id="35297-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span><span class="sxs-lookup"><span data-stu-id="35297-151">You can consume these APIs from various platforms, such as .NET, Python, R, Java, etc. The **Consume** page for your web service on the [Microsoft Azure Machine Learning Web Services portal](https://services.azureml.net) has sample code that can help you get started.</span></span> <span data-ttu-id="35297-152">For more information, see [How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment](machine-learning-consume-web-services.md).</span><span class="sxs-lookup"><span data-stu-id="35297-152">For more information, see [How to consume an Azure Machine Learning web service that has been deployed from a Machine Learning experiment](machine-learning-consume-web-services.md).</span></span>
