---
title: Visual Studio Azure resource group projects | Microsoft Docs
description: Use Visual Studio to create a Azure resource group project and deploy the resources to Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/02/2018
ms.author: tomfitz
ms.openlocfilehash: a32229859d7904523c8cd218ed1324abb3381337
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791094"
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="fadfc-103">Creating and deploying Azure resource groups through Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fadfc-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="fadfc-104">With Visual Studio, you can create a project that deploys your infrastructure and code to Azure.</span><span class="sxs-lookup"><span data-stu-id="fadfc-104">With Visual Studio, you can create a project that deploys your infrastructure and code to Azure.</span></span> <span data-ttu-id="fadfc-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span><span class="sxs-lookup"><span data-stu-id="fadfc-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span></span> <span data-ttu-id="fadfc-106">Visual Studio provides many different starter templates for deploying common scenarios.</span><span class="sxs-lookup"><span data-stu-id="fadfc-106">Visual Studio provides many different starter templates for deploying common scenarios.</span></span> <span data-ttu-id="fadfc-107">In this article, you deploy a web app and SQL Database.</span><span class="sxs-lookup"><span data-stu-id="fadfc-107">In this article, you deploy a web app and SQL Database.</span></span>  

<span data-ttu-id="fadfc-108">This article shows how to use [Visual Studio 2017 with the Azure development and ASP.NET workloads installed](/dotnet/azure/dotnet-tools).</span><span class="sxs-lookup"><span data-stu-id="fadfc-108">This article shows how to use [Visual Studio 2017 with the Azure development and ASP.NET workloads installed](/dotnet/azure/dotnet-tools).</span></span> <span data-ttu-id="fadfc-109">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span><span class="sxs-lookup"><span data-stu-id="fadfc-109">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span></span>

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="fadfc-110">Create Azure Resource Group project</span><span class="sxs-lookup"><span data-stu-id="fadfc-110">Create Azure Resource Group project</span></span>
<span data-ttu-id="fadfc-111">In this section, you create an Azure Resource Group project with a **Web app + SQL** template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-111">In this section, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="fadfc-112">In Visual Studio, choose **File**, **New Project**, choose either **C#** or **Visual Basic** (which language you choose has no impact on the later stages as these projects have only JSON and PowerShell content).</span><span class="sxs-lookup"><span data-stu-id="fadfc-112">In Visual Studio, choose **File**, **New Project**, choose either **C#** or **Visual Basic** (which language you choose has no impact on the later stages as these projects have only JSON and PowerShell content).</span></span> <span data-ttu-id="fadfc-113">Then choose **Cloud**, and **Azure Resource Group** project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-113">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![Cloud Deployment Project](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="fadfc-115">Choose the template that you want to deploy to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fadfc-115">Choose the template that you want to deploy to Azure Resource Manager.</span></span> <span data-ttu-id="fadfc-116">Notice there are many different options based on the type of project you wish to deploy.</span><span class="sxs-lookup"><span data-stu-id="fadfc-116">Notice there are many different options based on the type of project you wish to deploy.</span></span> <span data-ttu-id="fadfc-117">For this article, choose the **Web app + SQL** template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-117">For this article, choose the **Web app + SQL** template.</span></span>
   
    ![Choose a template](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="fadfc-119">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span><span class="sxs-lookup"><span data-stu-id="fadfc-119">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fadfc-120">Visual Studio retrieves a list of available templates online.</span><span class="sxs-lookup"><span data-stu-id="fadfc-120">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="fadfc-121">The list may change.</span><span class="sxs-lookup"><span data-stu-id="fadfc-121">The list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="fadfc-122">Visual Studio creates a resource group deployment project for the web app and SQL database.</span><span class="sxs-lookup"><span data-stu-id="fadfc-122">Visual Studio creates a resource group deployment project for the web app and SQL database.</span></span>
3. <span data-ttu-id="fadfc-123">To see what you created, look at the node in the deployment project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-123">To see what you created, look at the node in the deployment project.</span></span>
   
    ![show nodes](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="fadfc-125">Since you chose the Web app + SQL template for this example, you see the following files:</span><span class="sxs-lookup"><span data-stu-id="fadfc-125">Since you chose the Web app + SQL template for this example, you see the following files:</span></span> 
   
   | <span data-ttu-id="fadfc-126">File name</span><span class="sxs-lookup"><span data-stu-id="fadfc-126">File name</span></span> | <span data-ttu-id="fadfc-127">Description</span><span class="sxs-lookup"><span data-stu-id="fadfc-127">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="fadfc-128">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="fadfc-128">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="fadfc-129">A PowerShell script that runs PowerShell commands to deploy to Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fadfc-129">A PowerShell script that runs PowerShell commands to deploy to Azure Resource Manager.</span></span><br /><span data-ttu-id="fadfc-130">**Note** Visual Studio uses this PowerShell script to deploy your template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-130">**Note** Visual Studio uses this PowerShell script to deploy your template.</span></span> <span data-ttu-id="fadfc-131">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span><span class="sxs-lookup"><span data-stu-id="fadfc-131">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="fadfc-132">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="fadfc-132">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="fadfc-133">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-133">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span></span> <span data-ttu-id="fadfc-134">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span><span class="sxs-lookup"><span data-stu-id="fadfc-134">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span></span> |
   | <span data-ttu-id="fadfc-135">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="fadfc-135">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="fadfc-136">A parameters file that has values needed by the template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-136">A parameters file that has values needed by the template.</span></span> <span data-ttu-id="fadfc-137">You pass in parameter values to customize each deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-137">You pass in parameter values to customize each deployment.</span></span> |
   
    <span data-ttu-id="fadfc-138">All resource group deployment projects have these basic files.</span><span class="sxs-lookup"><span data-stu-id="fadfc-138">All resource group deployment projects have these basic files.</span></span> <span data-ttu-id="fadfc-139">Other projects may have additional files to support other functionality.</span><span class="sxs-lookup"><span data-stu-id="fadfc-139">Other projects may have additional files to support other functionality.</span></span>

## <a name="customize-the-resource-manager-template"></a><span data-ttu-id="fadfc-140">Customize the Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="fadfc-140">Customize the Resource Manager template</span></span>
<span data-ttu-id="fadfc-141">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="fadfc-141">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span></span> <span data-ttu-id="fadfc-142">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span><span class="sxs-lookup"><span data-stu-id="fadfc-142">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span></span> <span data-ttu-id="fadfc-143">The JSON files use a schema that you reference at the top of each file.</span><span class="sxs-lookup"><span data-stu-id="fadfc-143">The JSON files use a schema that you reference at the top of each file.</span></span> <span data-ttu-id="fadfc-144">If you want to understand the schema, you can download and analyze it.</span><span class="sxs-lookup"><span data-stu-id="fadfc-144">If you want to understand the schema, you can download and analyze it.</span></span> <span data-ttu-id="fadfc-145">The schema defines what elements are valid, the types and formats of fields, and the possible values for a property.</span><span class="sxs-lookup"><span data-stu-id="fadfc-145">The schema defines what elements are valid, the types and formats of fields, and the possible values for a property.</span></span> <span data-ttu-id="fadfc-146">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fadfc-146">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="fadfc-147">To work on your template, open **WebSiteSQLDatabase.json**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-147">To work on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="fadfc-148">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-148">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span></span> <span data-ttu-id="fadfc-149">The **JSON Outline** window makes it easy to see the elements defined in your template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-149">The **JSON Outline** window makes it easy to see the elements defined in your template.</span></span>

![show JSON outline](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="fadfc-151">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span><span class="sxs-lookup"><span data-stu-id="fadfc-151">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span></span>

![navigate JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="fadfc-153">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-153">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![add resource](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="fadfc-155">For this tutorial, select **Storage Account** and give it a name.</span><span class="sxs-lookup"><span data-stu-id="fadfc-155">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="fadfc-156">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span><span class="sxs-lookup"><span data-stu-id="fadfc-156">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![add storage](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="fadfc-158">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="fadfc-158">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span></span>

![show outline](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="fadfc-160">The **storageType** parameter is pre-defined with allowed types and a default type.</span><span class="sxs-lookup"><span data-stu-id="fadfc-160">The **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="fadfc-161">You can leave these values or edit them for your scenario.</span><span class="sxs-lookup"><span data-stu-id="fadfc-161">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="fadfc-162">If you don't want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span><span class="sxs-lookup"><span data-stu-id="fadfc-162">If you don't want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span></span> 

```json
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
```

<span data-ttu-id="fadfc-163">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-163">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span></span> <span data-ttu-id="fadfc-164">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-164">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span></span> <span data-ttu-id="fadfc-165">Notice that intellisense shows the available values and provides a description of that value.</span><span class="sxs-lookup"><span data-stu-id="fadfc-165">Notice that intellisense shows the available values and provides a description of that value.</span></span>

![show intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="fadfc-167">You can set **numberOfWorkers** to 1.</span><span class="sxs-lookup"><span data-stu-id="fadfc-167">You can set **numberOfWorkers** to 1.</span></span>

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-the-resource-group-project-to-azure"></a><span data-ttu-id="fadfc-168">Deploy the Resource Group project to Azure</span><span class="sxs-lookup"><span data-stu-id="fadfc-168">Deploy the Resource Group project to Azure</span></span>
<span data-ttu-id="fadfc-169">You're now ready to deploy your project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-169">You're now ready to deploy your project.</span></span> <span data-ttu-id="fadfc-170">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="fadfc-170">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span></span> <span data-ttu-id="fadfc-171">The resource group is a logical grouping of resources that share a common lifecycle.</span><span class="sxs-lookup"><span data-stu-id="fadfc-171">The resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="fadfc-172">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-172">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![Deploy, New Deployment menu item](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="fadfc-174">The **Deploy to Resource Group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="fadfc-174">The **Deploy to Resource Group** dialog box appears.</span></span>
   
    ![Deploy To Resource Group Dialog Box](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="fadfc-176">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="fadfc-176">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="fadfc-177">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-177">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![Deploy To Resource Group Dialog Box](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="fadfc-179">The **Create Resource Group** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="fadfc-179">The **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="fadfc-180">Give your group a name and location, and select the **Create** button.</span><span class="sxs-lookup"><span data-stu-id="fadfc-180">Give your group a name and location, and select the **Create** button.</span></span>
   
    ![Create Resource Group Dialog Box](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="fadfc-182">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span><span class="sxs-lookup"><span data-stu-id="fadfc-182">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span></span>
   
    ![Edit Parameters button](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="fadfc-184">Provide values for the empty parameters and select the **Save** button.</span><span class="sxs-lookup"><span data-stu-id="fadfc-184">Provide values for the empty parameters and select the **Save** button.</span></span> <span data-ttu-id="fadfc-185">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-185">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="fadfc-186">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span><span class="sxs-lookup"><span data-stu-id="fadfc-186">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span></span> 
   
    <span data-ttu-id="fadfc-187">**administratorLogin** specifies the user name for the SQL Server administrator.</span><span class="sxs-lookup"><span data-stu-id="fadfc-187">**administratorLogin** specifies the user name for the SQL Server administrator.</span></span> <span data-ttu-id="fadfc-188">Don't use common admin names like **sa** or **admin**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-188">Don't use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="fadfc-189">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span><span class="sxs-lookup"><span data-stu-id="fadfc-189">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="fadfc-190">The **Save passwords as plain text in the parameters file** option isn't secure; therefore, don't select this option.</span><span class="sxs-lookup"><span data-stu-id="fadfc-190">The **Save passwords as plain text in the parameters file** option isn't secure; therefore, don't select this option.</span></span> <span data-ttu-id="fadfc-191">Since the password isn't saved as plain text, you need to provide this password again during deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-191">Since the password isn't saved as plain text, you need to provide this password again during deployment.</span></span> 
   
    <span data-ttu-id="fadfc-192">**databaseName** specifies a name for the database to create.</span><span class="sxs-lookup"><span data-stu-id="fadfc-192">**databaseName** specifies a name for the database to create.</span></span> 
   
    ![Edit Parameters Dialog Box](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="fadfc-194">Choose the **Deploy** button to deploy the project to Azure.</span><span class="sxs-lookup"><span data-stu-id="fadfc-194">Choose the **Deploy** button to deploy the project to Azure.</span></span> <span data-ttu-id="fadfc-195">A PowerShell console opens outside of the Visual Studio instance.</span><span class="sxs-lookup"><span data-stu-id="fadfc-195">A PowerShell console opens outside of the Visual Studio instance.</span></span> <span data-ttu-id="fadfc-196">Enter the SQL Server administrator password in the PowerShell console when prompted.</span><span class="sxs-lookup"><span data-stu-id="fadfc-196">Enter the SQL Server administrator password in the PowerShell console when prompted.</span></span> <span data-ttu-id="fadfc-197">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span><span class="sxs-lookup"><span data-stu-id="fadfc-197">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span></span> <span data-ttu-id="fadfc-198">Look for this console and select it to provide the password.</span><span class="sxs-lookup"><span data-stu-id="fadfc-198">Look for this console and select it to provide the password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fadfc-199">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="fadfc-199">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="fadfc-200">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span><span class="sxs-lookup"><span data-stu-id="fadfc-200">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span></span> <span data-ttu-id="fadfc-201">If prompted, install them.</span><span class="sxs-lookup"><span data-stu-id="fadfc-201">If prompted, install them.</span></span> <span data-ttu-id="fadfc-202">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="fadfc-202">For more information, see [Install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span>
   > 
   > 
6. <span data-ttu-id="fadfc-203">The deployment may take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="fadfc-203">The deployment may take a few minutes.</span></span> <span data-ttu-id="fadfc-204">In the **Output** windows, you see the status of the deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-204">In the **Output** windows, you see the status of the deployment.</span></span> <span data-ttu-id="fadfc-205">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span><span class="sxs-lookup"><span data-stu-id="fadfc-205">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' to resource group 'DemoSiteGroup'.
7. <span data-ttu-id="fadfc-206">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span><span class="sxs-lookup"><span data-stu-id="fadfc-206">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span></span> <span data-ttu-id="fadfc-207">To see the resource group, select **Resource groups** and the resource group you deployed to.</span><span class="sxs-lookup"><span data-stu-id="fadfc-207">To see the resource group, select **Resource groups** and the resource group you deployed to.</span></span>
   
    ![select group](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="fadfc-209">You see all the deployed resources.</span><span class="sxs-lookup"><span data-stu-id="fadfc-209">You see all the deployed resources.</span></span> <span data-ttu-id="fadfc-210">Notice that the name of the storage account isn't exactly what you specified when adding that resource.</span><span class="sxs-lookup"><span data-stu-id="fadfc-210">Notice that the name of the storage account isn't exactly what you specified when adding that resource.</span></span> <span data-ttu-id="fadfc-211">The storage account must be unique.</span><span class="sxs-lookup"><span data-stu-id="fadfc-211">The storage account must be unique.</span></span> <span data-ttu-id="fadfc-212">The template automatically adds a string of characters to the name you provided to provide a unique name.</span><span class="sxs-lookup"><span data-stu-id="fadfc-212">The template automatically adds a string of characters to the name you provided to provide a unique name.</span></span> 
   
    ![show resources](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="fadfc-214">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-214">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="fadfc-215">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span><span class="sxs-lookup"><span data-stu-id="fadfc-215">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span></span>
   
    ![Azure resource group deployed](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="fadfc-217">Deploy code with your infrastructure</span><span class="sxs-lookup"><span data-stu-id="fadfc-217">Deploy code with your infrastructure</span></span>
<span data-ttu-id="fadfc-218">At this point, you've deployed the infrastructure for your app, but there's no actual code deployed with the project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-218">At this point, you've deployed the infrastructure for your app, but there's no actual code deployed with the project.</span></span> <span data-ttu-id="fadfc-219">This article shows how to deploy a web app and SQL Database tables during deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-219">This article shows how to deploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="fadfc-220">If you're deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span><span class="sxs-lookup"><span data-stu-id="fadfc-220">If you're deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span></span> <span data-ttu-id="fadfc-221">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span><span class="sxs-lookup"><span data-stu-id="fadfc-221">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span></span>

1. <span data-ttu-id="fadfc-222">Add a project to your Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="fadfc-222">Add a project to your Visual Studio solution.</span></span> <span data-ttu-id="fadfc-223">Right-click the solution, and select **Add** > **New Project**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-223">Right-click the solution, and select **Add** > **New Project**.</span></span>
   
    ![add project](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="fadfc-225">Add an **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-225">Add an **ASP.NET Web Application**.</span></span> 
   
    ![add web app](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="fadfc-227">Select **MVC**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-227">Select **MVC**.</span></span>
   
    ![select MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="fadfc-229">After Visual Studio creates your web app, you see both projects in the solution.</span><span class="sxs-lookup"><span data-stu-id="fadfc-229">After Visual Studio creates your web app, you see both projects in the solution.</span></span>
   
    ![show projects](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="fadfc-231">Now, you need to make sure your resource group project is aware of the new project.</span><span class="sxs-lookup"><span data-stu-id="fadfc-231">Now, you need to make sure your resource group project is aware of the new project.</span></span> <span data-ttu-id="fadfc-232">Go back to your resource group project (AzureResourceGroup1).</span><span class="sxs-lookup"><span data-stu-id="fadfc-232">Go back to your resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="fadfc-233">Right-click **References** and select **Add Reference**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-233">Right-click **References** and select **Add Reference**.</span></span>
   
    ![add reference](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="fadfc-235">Select the web app project that you created.</span><span class="sxs-lookup"><span data-stu-id="fadfc-235">Select the web app project that you created.</span></span>
   
    ![add reference](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="fadfc-237">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span><span class="sxs-lookup"><span data-stu-id="fadfc-237">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="fadfc-238">You see these properties in the **Properties** window for the reference.</span><span class="sxs-lookup"><span data-stu-id="fadfc-238">You see these properties in the **Properties** window for the reference.</span></span>
   
      ![see reference](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="fadfc-240">The properties are:</span><span class="sxs-lookup"><span data-stu-id="fadfc-240">The properties are:</span></span>
   
   * <span data-ttu-id="fadfc-241">The **Additional Properties** has the web deployment package staging location that is pushed to the Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="fadfc-241">The **Additional Properties** has the web deployment package staging location that is pushed to the Azure Storage.</span></span> <span data-ttu-id="fadfc-242">Note the folder (ExampleApp) and file (package.zip).</span><span class="sxs-lookup"><span data-stu-id="fadfc-242">Note the folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="fadfc-243">You need to know these values because you provide them as parameters when deploying the app.</span><span class="sxs-lookup"><span data-stu-id="fadfc-243">You need to know these values because you provide them as parameters when deploying the app.</span></span> 
   * <span data-ttu-id="fadfc-244">The **Include File Path** has the path where the package is created.</span><span class="sxs-lookup"><span data-stu-id="fadfc-244">The **Include File Path** has the path where the package is created.</span></span> <span data-ttu-id="fadfc-245">The **Include Targets** has the command that deployment executes.</span><span class="sxs-lookup"><span data-stu-id="fadfc-245">The **Include Targets** has the command that deployment executes.</span></span> 
   * <span data-ttu-id="fadfc-246">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span><span class="sxs-lookup"><span data-stu-id="fadfc-246">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="fadfc-247">You don't need a publish profile as the deployment gets the necessary information from the properties to create the package.</span><span class="sxs-lookup"><span data-stu-id="fadfc-247">You don't need a publish profile as the deployment gets the necessary information from the properties to create the package.</span></span>
7. <span data-ttu-id="fadfc-248">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-248">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span></span>
   
    ![add resource](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="fadfc-250">This time select **Web Deploy for Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="fadfc-250">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![add web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="fadfc-252">Redeploy your resource group project to the resource group.</span><span class="sxs-lookup"><span data-stu-id="fadfc-252">Redeploy your resource group project to the resource group.</span></span> <span data-ttu-id="fadfc-253">This time there are some new parameters.</span><span class="sxs-lookup"><span data-stu-id="fadfc-253">This time there are some new parameters.</span></span> <span data-ttu-id="fadfc-254">You don't need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span><span class="sxs-lookup"><span data-stu-id="fadfc-254">You don't need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="fadfc-255">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span><span class="sxs-lookup"><span data-stu-id="fadfc-255">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span></span> <span data-ttu-id="fadfc-256">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span><span class="sxs-lookup"><span data-stu-id="fadfc-256">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![add web deploy](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="fadfc-258">For the **Artifact storage account**, select the one deployed with this resource group.</span><span class="sxs-lookup"><span data-stu-id="fadfc-258">For the **Artifact storage account**, select the one deployed with this resource group.</span></span>
10. <span data-ttu-id="fadfc-259">After the deployment has finished, select your web app in the portal.</span><span class="sxs-lookup"><span data-stu-id="fadfc-259">After the deployment has finished, select your web app in the portal.</span></span> <span data-ttu-id="fadfc-260">Select the URL to browse to the site.</span><span class="sxs-lookup"><span data-stu-id="fadfc-260">Select the URL to browse to the site.</span></span>
    
     ![browse site](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="fadfc-262">Notice that you've successfully deployed the default ASP.NET app.</span><span class="sxs-lookup"><span data-stu-id="fadfc-262">Notice that you've successfully deployed the default ASP.NET app.</span></span>
    
     ![show deployed app](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="add-an-operations-dashboard-to-your-deployment"></a><span data-ttu-id="fadfc-264">Add an operations dashboard to your deployment</span><span class="sxs-lookup"><span data-stu-id="fadfc-264">Add an operations dashboard to your deployment</span></span>
<span data-ttu-id="fadfc-265">You aren't limited to only the resources that are available through the Visual Studio interface.</span><span class="sxs-lookup"><span data-stu-id="fadfc-265">You aren't limited to only the resources that are available through the Visual Studio interface.</span></span> <span data-ttu-id="fadfc-266">You can customize your deployment by adding a custom resource to your template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-266">You can customize your deployment by adding a custom resource to your template.</span></span> <span data-ttu-id="fadfc-267">To show adding a resource, you add an operational dashboard to manage the resource you deployed.</span><span class="sxs-lookup"><span data-stu-id="fadfc-267">To show adding a resource, you add an operational dashboard to manage the resource you deployed.</span></span>

1. <span data-ttu-id="fadfc-268">Open the WebsiteSqlDeploy.json file and add the following JSON after the storage account resource but before the closing `]` of the resources section.</span><span class="sxs-lookup"><span data-stu-id="fadfc-268">Open the WebsiteSqlDeploy.json file and add the following JSON after the storage account resource but before the closing `]` of the resources section.</span></span>

  ```json
    ,{
      "properties": {
        "lenses": {
          "0": {
            "order": 0,
            "parts": {
              "0": {
                "position": {
                  "x": 0,
                  "y": 0,
                  "colSpan": 4,
                  "rowSpan": 6
                },
                "metadata": {
                  "inputs": [
                    {
                      "name": "resourceGroup",
                      "isOptional": true
                    },
                    {
                      "name": "id",
                      "value": "[resourceGroup().id]",
                      "isOptional": true
                    }
                  ],
                  "type": "Extension/HubsExtension/PartType/ResourceGroupMapPinnedPart"
                }
              },
              "1": {
                "position": {
                  "x": 4,
                  "y": 0,
                  "rowSpan": 3,
                  "colSpan": 4
                },
                "metadata": {
                  "inputs": [],
                  "type": "Extension[azure]/HubsExtension/PartType/MarkdownPart",
                  "settings": {
                    "content": {
                      "settings": {
                        "content": "__Customizations__\n\nUse this dashboard to create and share the operational views of services critical to the application performing. To customize simply pin components to the dashboard and then publish when you're done. Others will see your changes when you publish and share the dashboard.\n\nYou can customize this text too. It supports plain text, __Markdown__, and even limited HTML like images <img width='10' src='https://portal.azure.com/favicon.ico'/> and <a href='https://azure.microsoft.com' target='_blank'>links</a> that open in a new tab.\n",
                        "title": "Operations",
                        "subtitle": "[resourceGroup().name]"
                      }
                    }
                  }
                }
              }
            }
          }
        },
        "metadata": {
          "model": {
            "timeRange": {
              "value": {
                "relative": {
                  "duration": 24,
                  "timeUnit": 1
                }
              },
              "type": "MsPortalFx.Composition.Configuration.ValueTypes.TimeRange"
            }
          }
        }
      },
      "apiVersion": "2015-08-01-preview",
      "name": "[concat('ARM-',resourceGroup().name)]",
      "type": "Microsoft.Portal/dashboards",
      "location": "[resourceGroup().location]",
      "tags": {
        "hidden-title": "[concat('OPS-',resourceGroup().name)]"
      }
    }
  ```

2. <span data-ttu-id="fadfc-269">Redeploy your resource group.</span><span class="sxs-lookup"><span data-stu-id="fadfc-269">Redeploy your resource group.</span></span> <span data-ttu-id="fadfc-270">Look at your dashboard on the Azure portal, and notice the shared dashboard has been added to your list of choices.</span><span class="sxs-lookup"><span data-stu-id="fadfc-270">Look at your dashboard on the Azure portal, and notice the shared dashboard has been added to your list of choices.</span></span>

   ![Custom Dashboard](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/view-custom-dashboards.png)

3. <span data-ttu-id="fadfc-272">Select the dashboard.</span><span class="sxs-lookup"><span data-stu-id="fadfc-272">Select the dashboard.</span></span>

   ![Custom Dashboard](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/Ops-DemoSiteGroup-dashboard.png)

<span data-ttu-id="fadfc-274">You can managed access to the dashboard by using RBAC groups.</span><span class="sxs-lookup"><span data-stu-id="fadfc-274">You can managed access to the dashboard by using RBAC groups.</span></span> <span data-ttu-id="fadfc-275">You can also customize the dashboard's appearance after it's deployed.</span><span class="sxs-lookup"><span data-stu-id="fadfc-275">You can also customize the dashboard's appearance after it's deployed.</span></span> <span data-ttu-id="fadfc-276">However, if you redeploy the resource group, the dashboard is reset to its default state in your template.</span><span class="sxs-lookup"><span data-stu-id="fadfc-276">However, if you redeploy the resource group, the dashboard is reset to its default state in your template.</span></span> <span data-ttu-id="fadfc-277">For more information about creating dashboards, see [Programmatically create Azure Dashboards](../azure-portal/azure-portal-dashboards-create-programmatically.md).</span><span class="sxs-lookup"><span data-stu-id="fadfc-277">For more information about creating dashboards, see [Programmatically create Azure Dashboards](../azure-portal/azure-portal-dashboards-create-programmatically.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fadfc-278">Next steps</span><span class="sxs-lookup"><span data-stu-id="fadfc-278">Next steps</span></span>

<span data-ttu-id="fadfc-279">In this quickstart, you learned how to create and deploy templates using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fadfc-279">In this quickstart, you learned how to create and deploy templates using Visual Studio.</span></span> <span data-ttu-id="fadfc-280">The next tutorial shows you how to find the information from template reference so you can create an encrypted Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="fadfc-280">The next tutorial shows you how to find the information from template reference so you can create an encrypted Azure Storage account.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fadfc-281">Create an encrypted storage account</span><span class="sxs-lookup"><span data-stu-id="fadfc-281">Create an encrypted storage account</span></span>](./resource-manager-tutorial-create-encrypted-storage-accounts.md)
