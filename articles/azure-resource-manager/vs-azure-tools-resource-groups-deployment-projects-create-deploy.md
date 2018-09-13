---
title: Visual Studio Azure resource group projects | Microsoft Docs
description: Use Visual Studio to create a Azure resource group project and deploy the resources to Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: b3206b3d457499d2712d30445f4600b7ba588d69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670960"
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="eed6f-103">Creating and deploying Azure resource groups through Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eed6f-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="eed6f-104">With Visual Studio and the [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code to Azure.</span><span class="sxs-lookup"><span data-stu-id="eed6f-104">With Visual Studio and the [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code to Azure.</span></span> <span data-ttu-id="eed6f-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span><span class="sxs-lookup"><span data-stu-id="eed6f-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span></span> <span data-ttu-id="eed6f-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="eed6f-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span></span> <span data-ttu-id="eed6f-107">The **Azure Resource Group** deployment project enables you to deploy all the needed resources in a single, repeatable operation.</span><span class="sxs-lookup"><span data-stu-id="eed6f-107">The **Azure Resource Group** deployment project enables you to deploy all the needed resources in a single, repeatable operation.</span></span> <span data-ttu-id="eed6f-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="eed6f-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define the resources that you deploy to Azure.</span><span class="sxs-lookup"><span data-stu-id="eed6f-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define the resources that you deploy to Azure.</span></span> <span data-ttu-id="eed6f-110">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-110">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="eed6f-111">Visual Studio enables you to edit these templates, and provides tools that simplify working with templates.</span><span class="sxs-lookup"><span data-stu-id="eed6f-111">Visual Studio enables you to edit these templates, and provides tools that simplify working with templates.</span></span>

<span data-ttu-id="eed6f-112">In this article, you deploy a web app and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="eed6f-112">In this article, you deploy a web app and SQL Database.</span></span> <span data-ttu-id="eed6f-113">However, the steps are almost the same for any type resource.</span><span class="sxs-lookup"><span data-stu-id="eed6f-113">However, the steps are almost the same for any type resource.</span></span> <span data-ttu-id="eed6f-114">You can as easily deploy a Virtual Machine and its related resources.</span><span class="sxs-lookup"><span data-stu-id="eed6f-114">You can as easily deploy a Virtual Machine and its related resources.</span></span> <span data-ttu-id="eed6f-115">Visual Studio provides many different starter templates for deploying common scenarios.</span><span class="sxs-lookup"><span data-stu-id="eed6f-115">Visual Studio provides many different starter templates for deploying common scenarios.</span></span>

<span data-ttu-id="eed6f-116">This article shows Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="eed6f-116">This article shows Visual Studio 2017.</span></span> <span data-ttu-id="eed6f-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span><span class="sxs-lookup"><span data-stu-id="eed6f-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span></span> <span data-ttu-id="eed6f-118">You can use versions of the Azure SDK from 2.6 or later; however, your experience of the user interface may be different than the user interface shown in this article.</span><span class="sxs-lookup"><span data-stu-id="eed6f-118">You can use versions of the Azure SDK from 2.6 or later; however, your experience of the user interface may be different than the user interface shown in this article.</span></span> <span data-ttu-id="eed6f-119">We strongly recommend that you install the latest version of the [Azure SDK](https://azure.microsoft.com/downloads/) before starting the steps.</span><span class="sxs-lookup"><span data-stu-id="eed6f-119">We strongly recommend that you install the latest version of the [Azure SDK](https://azure.microsoft.com/downloads/) before starting the steps.</span></span> 

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="eed6f-120">Create Azure Resource Group project</span><span class="sxs-lookup"><span data-stu-id="eed6f-120">Create Azure Resource Group project</span></span>
<span data-ttu-id="eed6f-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="eed6f-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span></span> <span data-ttu-id="eed6f-123">Then choose **Cloud**, and **Azure Resource Group** project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-123">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![Cloud Deployment Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="eed6f-125">Choose the template that you want to deploy to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eed6f-125">Choose the template that you want to deploy to Azure Resource Manager.</span></span> <span data-ttu-id="eed6f-126">Notice there are many different options based on the type of project you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="eed6f-126">Notice there are many different options based on the type of project you wish to deploy.</span></span> <span data-ttu-id="eed6f-127">For this article, choose the **Web app + SQL** template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-127">For this article, choose the **Web app + SQL** template.</span></span>
   
    ![Choose a template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="eed6f-129">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span><span class="sxs-lookup"><span data-stu-id="eed6f-129">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eed6f-130">Visual Studio retrieves a list of available templates online.</span><span class="sxs-lookup"><span data-stu-id="eed6f-130">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="eed6f-131">The list may change.</span><span class="sxs-lookup"><span data-stu-id="eed6f-131">The list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="eed6f-132">Visual Studio creates a resource group deployment project for the web app and SQL database.</span><span class="sxs-lookup"><span data-stu-id="eed6f-132">Visual Studio creates a resource group deployment project for the web app and SQL database.</span></span>
3. <span data-ttu-id="eed6f-133">To see what you created, look at the node in the deployment project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-133">To see what you created, look at the node in the deployment project.</span></span>
   
    ![show nodes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="eed6f-135">Since we chose the Web app + SQL template for this example, you see the following files:</span><span class="sxs-lookup"><span data-stu-id="eed6f-135">Since we chose the Web app + SQL template for this example, you see the following files:</span></span> 
   
   | <span data-ttu-id="eed6f-136">File name</span><span class="sxs-lookup"><span data-stu-id="eed6f-136">File name</span></span> | <span data-ttu-id="eed6f-137">Description</span><span class="sxs-lookup"><span data-stu-id="eed6f-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="eed6f-138">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="eed6f-138">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="eed6f-139">A PowerShell script that invokes PowerShell commands to deploy to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="eed6f-139">A PowerShell script that invokes PowerShell commands to deploy to Azure Resource Manager.</span></span><br /><span data-ttu-id="eed6f-140">**Note** Visual Studio uses this PowerShell script to deploy your template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-140">**Note** Visual Studio uses this PowerShell script to deploy your template.</span></span> <span data-ttu-id="eed6f-141">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span><span class="sxs-lookup"><span data-stu-id="eed6f-141">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="eed6f-142">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="eed6f-142">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="eed6f-143">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-143">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span></span> <span data-ttu-id="eed6f-144">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span><span class="sxs-lookup"><span data-stu-id="eed6f-144">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span></span> |
   | <span data-ttu-id="eed6f-145">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="eed6f-145">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="eed6f-146">A parameters file that contains values needed by the template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-146">A parameters file that contains values needed by the template.</span></span> <span data-ttu-id="eed6f-147">You pass in parameter values to customize each deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-147">You pass in parameter values to customize each deployment.</span></span> |
   
    <span data-ttu-id="eed6f-148">All resource group deployment projects contain these basic files.</span><span class="sxs-lookup"><span data-stu-id="eed6f-148">All resource group deployment projects contain these basic files.</span></span> <span data-ttu-id="eed6f-149">Other projects may contain additional files to support other functionality.</span><span class="sxs-lookup"><span data-stu-id="eed6f-149">Other projects may contain additional files to support other functionality.</span></span>

## <a name="customize-the-resource-manager-template"></a><span data-ttu-id="eed6f-150">Customize the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="eed6f-150">Customize the Resource Manager template</span></span>
<span data-ttu-id="eed6f-151">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="eed6f-151">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span></span> <span data-ttu-id="eed6f-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span><span class="sxs-lookup"><span data-stu-id="eed6f-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span></span> <span data-ttu-id="eed6f-153">The JSON files use a schema that you reference at the top of each file.</span><span class="sxs-lookup"><span data-stu-id="eed6f-153">The JSON files use a schema that you reference at the top of each file.</span></span> <span data-ttu-id="eed6f-154">If you want to understand the schema, you can download and analyze it.</span><span class="sxs-lookup"><span data-stu-id="eed6f-154">If you want to understand the schema, you can download and analyze it.</span></span> <span data-ttu-id="eed6f-155">The schema defines what elements are valid, the types and formats of fields, the possible values of enumerated values, and so on.</span><span class="sxs-lookup"><span data-stu-id="eed6f-155">The schema defines what elements are valid, the types and formats of fields, the possible values of enumerated values, and so on.</span></span> <span data-ttu-id="eed6f-156">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-156">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="eed6f-157">To work on your template, open **WebSiteSQLDatabase.json**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-157">To work on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="eed6f-158">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-158">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span></span> <span data-ttu-id="eed6f-159">The **JSON Outline** window makes it easy to see the elements defined in your template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-159">The **JSON Outline** window makes it easy to see the elements defined in your template.</span></span>

![show JSON outline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="eed6f-161">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span><span class="sxs-lookup"><span data-stu-id="eed6f-161">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span></span>

![navigate JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="eed6f-163">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-163">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![add resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="eed6f-165">For this tutorial, select **Storage Account** and give it a name.</span><span class="sxs-lookup"><span data-stu-id="eed6f-165">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="eed6f-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span><span class="sxs-lookup"><span data-stu-id="eed6f-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![add storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="eed6f-168">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="eed6f-168">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span></span>

![show outline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="eed6f-170">The **storageType** parameter is pre-defined with allowed types and a default type.</span><span class="sxs-lookup"><span data-stu-id="eed6f-170">The **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="eed6f-171">You can leave these values or edit them for your scenario.</span><span class="sxs-lookup"><span data-stu-id="eed6f-171">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="eed6f-172">If you do not want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span><span class="sxs-lookup"><span data-stu-id="eed6f-172">If you do not want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span></span> 

    "storageType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS"
      ]
    }

<span data-ttu-id="eed6f-173">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-173">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span></span> <span data-ttu-id="eed6f-174">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-174">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span></span> <span data-ttu-id="eed6f-175">Notice that intellisense shows the available values and provides a description of that value.</span><span class="sxs-lookup"><span data-stu-id="eed6f-175">Notice that intellisense shows the available values and provides a description of that value.</span></span>

![show intellisense](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="eed6f-177">You can set **numberOfWorkers** to 1.</span><span class="sxs-lookup"><span data-stu-id="eed6f-177">You can set **numberOfWorkers** to 1.</span></span>

    "properties": {
      "name": "[parameters('hostingPlanName')]",
      "numberOfWorkers": 1
    }

## <a name="deploy-the-resource-group-project-to-azure"></a><span data-ttu-id="eed6f-178">Deploy the Resource Group project to Azure</span><span class="sxs-lookup"><span data-stu-id="eed6f-178">Deploy the Resource Group project to Azure</span></span>
<span data-ttu-id="eed6f-179">You are now ready to deploy your project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-179">You are now ready to deploy your project.</span></span> <span data-ttu-id="eed6f-180">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="eed6f-180">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span></span> <span data-ttu-id="eed6f-181">The resource group is a logical grouping of resources that share a common lifecycle.</span><span class="sxs-lookup"><span data-stu-id="eed6f-181">The resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="eed6f-182">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-182">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![Deploy, New Deployment menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="eed6f-184">The **Deploy to Resource Group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="eed6f-184">The **Deploy to Resource Group** dialog box appears.</span></span>
   
    ![Deploy To Resource Group Dialog Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="eed6f-186">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="eed6f-186">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="eed6f-187">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-187">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![Deploy To Resource Group Dialog Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="eed6f-189">The **Create Resource Group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="eed6f-189">The **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="eed6f-190">Give your group a name and location, and select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="eed6f-190">Give your group a name and location, and select the **Create** button.</span></span>
   
    ![Create Resource Group Dialog Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="eed6f-192">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span><span class="sxs-lookup"><span data-stu-id="eed6f-192">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span></span>
   
    ![Edit Parameters button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="eed6f-194">Provide values for the empty parameters and select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="eed6f-194">Provide values for the empty parameters and select the **Save** button.</span></span> <span data-ttu-id="eed6f-195">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-195">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="eed6f-196">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span><span class="sxs-lookup"><span data-stu-id="eed6f-196">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span></span> 
   
    <span data-ttu-id="eed6f-197">**administratorLogin** specifies the user name for the SQL Server administrator.</span><span class="sxs-lookup"><span data-stu-id="eed6f-197">**administratorLogin** specifies the user name for the SQL Server administrator.</span></span> <span data-ttu-id="eed6f-198">Do not use common admin names like **sa** or **admin**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-198">Do not use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="eed6f-199">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span><span class="sxs-lookup"><span data-stu-id="eed6f-199">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="eed6f-200">The **Save passwords as plain text in the parameters file** option is not secure; therefore, do not select this option.</span><span class="sxs-lookup"><span data-stu-id="eed6f-200">The **Save passwords as plain text in the parameters file** option is not secure; therefore, do not select this option.</span></span> <span data-ttu-id="eed6f-201">Since the password is not saved as plain text, you need to provide this password again during deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-201">Since the password is not saved as plain text, you need to provide this password again during deployment.</span></span> 
   
    <span data-ttu-id="eed6f-202">**databaseName** specifies a name for the database to create.</span><span class="sxs-lookup"><span data-stu-id="eed6f-202">**databaseName** specifies a name for the database to create.</span></span> 
   
    ![Edit Parameters Dialog Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="eed6f-204">Choose the **Deploy** button to deploy the project to Azure.</span><span class="sxs-lookup"><span data-stu-id="eed6f-204">Choose the **Deploy** button to deploy the project to Azure.</span></span> <span data-ttu-id="eed6f-205">A PowerShell console opens outside of the Visual Studio instance.</span><span class="sxs-lookup"><span data-stu-id="eed6f-205">A PowerShell console opens outside of the Visual Studio instance.</span></span> <span data-ttu-id="eed6f-206">Enter the SQL Server administrator password in the PowerShell console when prompted.</span><span class="sxs-lookup"><span data-stu-id="eed6f-206">Enter the SQL Server administrator password in the PowerShell console when prompted.</span></span> <span data-ttu-id="eed6f-207">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span><span class="sxs-lookup"><span data-stu-id="eed6f-207">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span></span> <span data-ttu-id="eed6f-208">Look for this console and select it to provide the password.</span><span class="sxs-lookup"><span data-stu-id="eed6f-208">Look for this console and select it to provide the password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="eed6f-209">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="eed6f-209">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="eed6f-210">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span><span class="sxs-lookup"><span data-stu-id="eed6f-210">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span></span> <span data-ttu-id="eed6f-211">If prompted, install them.</span><span class="sxs-lookup"><span data-stu-id="eed6f-211">If prompted, install them.</span></span>
   > 
   > 
6. <span data-ttu-id="eed6f-212">The deployment may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="eed6f-212">The deployment may take a few minutes.</span></span> <span data-ttu-id="eed6f-213">In the **Output** windows, you see the status of the deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-213">In the **Output** windows, you see the status of the deployment.</span></span> <span data-ttu-id="eed6f-214">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span><span class="sxs-lookup"><span data-stu-id="eed6f-214">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' to resource group 'DemoSiteGroup'.
7. <span data-ttu-id="eed6f-215">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="eed6f-215">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span></span> <span data-ttu-id="eed6f-216">To see the resource group, select **Resource groups** and the resource group you deployed to.</span><span class="sxs-lookup"><span data-stu-id="eed6f-216">To see the resource group, select **Resource groups** and the resource group you deployed to.</span></span>
   
    ![select group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="eed6f-218">You see all the deployed resources.</span><span class="sxs-lookup"><span data-stu-id="eed6f-218">You see all the deployed resources.</span></span> <span data-ttu-id="eed6f-219">Notice that the name of the storage account is not exactly what you specified when adding that resource.</span><span class="sxs-lookup"><span data-stu-id="eed6f-219">Notice that the name of the storage account is not exactly what you specified when adding that resource.</span></span> <span data-ttu-id="eed6f-220">The storage account must be unique.</span><span class="sxs-lookup"><span data-stu-id="eed6f-220">The storage account must be unique.</span></span> <span data-ttu-id="eed6f-221">The template automatically adds a string of characters to the name you provided to provide a unique name.</span><span class="sxs-lookup"><span data-stu-id="eed6f-221">The template automatically adds a string of characters to the name you provided to provide a unique name.</span></span> 
   
    ![show resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="eed6f-223">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-223">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="eed6f-224">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span><span class="sxs-lookup"><span data-stu-id="eed6f-224">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span></span>
   
    ![Azure resource group deployed](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="eed6f-226">Deploy code with your infrastructure</span><span class="sxs-lookup"><span data-stu-id="eed6f-226">Deploy code with your infrastructure</span></span>
<span data-ttu-id="eed6f-227">At this point, you have deployed the infrastructure for your app, but there is no actual code deployed with the project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-227">At this point, you have deployed the infrastructure for your app, but there is no actual code deployed with the project.</span></span> <span data-ttu-id="eed6f-228">This article shows how to deploy a web app and SQL Database tables during deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-228">This article shows how to deploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="eed6f-229">If you are deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span><span class="sxs-lookup"><span data-stu-id="eed6f-229">If you are deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span></span> <span data-ttu-id="eed6f-230">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span><span class="sxs-lookup"><span data-stu-id="eed6f-230">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span></span>

1. <span data-ttu-id="eed6f-231">Add a project to your Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="eed6f-231">Add a project to your Visual Studio solution.</span></span> <span data-ttu-id="eed6f-232">Right-click the solution, and select **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-232">Right-click the solution, and select **Add** > **New Project**.</span></span>
   
    ![add project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="eed6f-234">Add an **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-234">Add an **ASP.NET Web Application**.</span></span> 
   
    ![add web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="eed6f-236">Select **MVC**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-236">Select **MVC**.</span></span>
   
    ![select MVC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="eed6f-238">After Visual Studio creates your web app, you see both projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="eed6f-238">After Visual Studio creates your web app, you see both projects in the solution.</span></span>
   
    ![show projects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="eed6f-240">Now, you need to make sure your resource group project is aware of the new project.</span><span class="sxs-lookup"><span data-stu-id="eed6f-240">Now, you need to make sure your resource group project is aware of the new project.</span></span> <span data-ttu-id="eed6f-241">Go back to your resource group project (AzureResourceGroup1).</span><span class="sxs-lookup"><span data-stu-id="eed6f-241">Go back to your resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="eed6f-242">Right-click **References** and select **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-242">Right-click **References** and select **Add Reference**.</span></span>
   
    ![add reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="eed6f-244">Select the web app project that you created.</span><span class="sxs-lookup"><span data-stu-id="eed6f-244">Select the web app project that you created.</span></span>
   
    ![add reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="eed6f-246">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span><span class="sxs-lookup"><span data-stu-id="eed6f-246">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="eed6f-247">You see these properties in the **Properties** window for the reference.</span><span class="sxs-lookup"><span data-stu-id="eed6f-247">You see these properties in the **Properties** window for the reference.</span></span>
   
      ![see reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="eed6f-249">The properties are:</span><span class="sxs-lookup"><span data-stu-id="eed6f-249">The properties are:</span></span>
   
   * <span data-ttu-id="eed6f-250">The **Additional Properties** contains the web deployment package staging location that is pushed to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="eed6f-250">The **Additional Properties** contains the web deployment package staging location that is pushed to the Azure Storage.</span></span> <span data-ttu-id="eed6f-251">Note the folder (ExampleApp) and file (package.zip).</span><span class="sxs-lookup"><span data-stu-id="eed6f-251">Note the folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="eed6f-252">You need to know these values because you provide them as parameters when deploying the app.</span><span class="sxs-lookup"><span data-stu-id="eed6f-252">You need to know these values because you provide them as parameters when deploying the app.</span></span> 
   * <span data-ttu-id="eed6f-253">The **Include File Path** contains the path where the package is created.</span><span class="sxs-lookup"><span data-stu-id="eed6f-253">The **Include File Path** contains the path where the package is created.</span></span> <span data-ttu-id="eed6f-254">The **Include Targets** contains the command that deployment executes.</span><span class="sxs-lookup"><span data-stu-id="eed6f-254">The **Include Targets** contains the command that deployment executes.</span></span> 
   * <span data-ttu-id="eed6f-255">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span><span class="sxs-lookup"><span data-stu-id="eed6f-255">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="eed6f-256">You do not need a publish profile as the deployment gets the necessary information from the properties to create the package.</span><span class="sxs-lookup"><span data-stu-id="eed6f-256">You do not need a publish profile as the deployment gets the necessary information from the properties to create the package.</span></span>
7. <span data-ttu-id="eed6f-257">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span><span class="sxs-lookup"><span data-stu-id="eed6f-257">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span></span>
   
    ![add resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="eed6f-259">This time select **Web Deploy for Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="eed6f-259">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![add web deploy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="eed6f-261">Redeploy your resource group project to the resource group.</span><span class="sxs-lookup"><span data-stu-id="eed6f-261">Redeploy your resource group project to the resource group.</span></span> <span data-ttu-id="eed6f-262">This time there are some new parameters.</span><span class="sxs-lookup"><span data-stu-id="eed6f-262">This time there are some new parameters.</span></span> <span data-ttu-id="eed6f-263">You do not need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span><span class="sxs-lookup"><span data-stu-id="eed6f-263">You do not need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="eed6f-264">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span><span class="sxs-lookup"><span data-stu-id="eed6f-264">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span></span> <span data-ttu-id="eed6f-265">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span><span class="sxs-lookup"><span data-stu-id="eed6f-265">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![add web deploy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="eed6f-267">For the **Artifact storage account**, select the one deployed with this resource group.</span><span class="sxs-lookup"><span data-stu-id="eed6f-267">For the **Artifact storage account**, select the one deployed with this resource group.</span></span>
10. <span data-ttu-id="eed6f-268">After the deployment has finished, select your web app in the portal.</span><span class="sxs-lookup"><span data-stu-id="eed6f-268">After the deployment has finished, select your web app in the portal.</span></span> <span data-ttu-id="eed6f-269">Select the URL to browse to the site.</span><span class="sxs-lookup"><span data-stu-id="eed6f-269">Select the URL to browse to the site.</span></span>
    
     ![browse site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="eed6f-271">Notice that you have successfully deployed the default ASP.NET app.</span><span class="sxs-lookup"><span data-stu-id="eed6f-271">Notice that you have successfully deployed the default ASP.NET app.</span></span>
    
     ![show deployed app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a><span data-ttu-id="eed6f-273">Next steps</span><span class="sxs-lookup"><span data-stu-id="eed6f-273">Next steps</span></span>
* <span data-ttu-id="eed6f-274">To learn about managing your resources through the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-274">To learn about managing your resources through the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="eed6f-275">To learn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eed6f-275">To learn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>































