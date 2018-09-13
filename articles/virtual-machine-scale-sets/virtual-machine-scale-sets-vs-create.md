---
title: Deploy Virtual Machine Scale Set using Visual Studio | Microsoft Docs
description: Deploy Virtual Machine Scale Sets using Visual Studio and a Resource Manager template
services: virtual-machine-scale-sets
documentationcenter: ''
author: gbowerman
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d364172368d5cc069cb1ae47eef0cdabb51d1087
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549111"
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="94abc-103">How to create a Virtual Machine Scale Set with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="94abc-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="94abc-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span><span class="sxs-lookup"><span data-stu-id="94abc-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="94abc-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span><span class="sxs-lookup"><span data-stu-id="94abc-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="94abc-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="94abc-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="94abc-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94abc-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="94abc-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span><span class="sxs-lookup"><span data-stu-id="94abc-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="94abc-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span><span class="sxs-lookup"><span data-stu-id="94abc-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="94abc-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="94abc-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="94abc-111">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="94abc-111">Pre-requisites</span></span>
<span data-ttu-id="94abc-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span><span class="sxs-lookup"><span data-stu-id="94abc-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="94abc-113">Visual Studio 2013 or later</span><span class="sxs-lookup"><span data-stu-id="94abc-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="94abc-114">Azure SDK 2.7, 2.8 or 2.9</span><span class="sxs-lookup"><span data-stu-id="94abc-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="94abc-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span><span class="sxs-lookup"><span data-stu-id="94abc-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="94abc-116">Creating a Project</span><span class="sxs-lookup"><span data-stu-id="94abc-116">Creating a Project</span></span>
1. <span data-ttu-id="94abc-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span><span class="sxs-lookup"><span data-stu-id="94abc-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![File New][file_new]

2. <span data-ttu-id="94abc-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span><span class="sxs-lookup"><span data-stu-id="94abc-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![Create Project][create_project]

3. <span data-ttu-id="94abc-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span><span class="sxs-lookup"><span data-stu-id="94abc-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![Select Template][select_Template]

4. <span data-ttu-id="94abc-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span><span class="sxs-lookup"><span data-stu-id="94abc-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="94abc-125">Customize your project</span><span class="sxs-lookup"><span data-stu-id="94abc-125">Customize your project</span></span>
<span data-ttu-id="94abc-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span><span class="sxs-lookup"><span data-stu-id="94abc-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="94abc-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span><span class="sxs-lookup"><span data-stu-id="94abc-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="94abc-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span><span class="sxs-lookup"><span data-stu-id="94abc-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="94abc-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span><span class="sxs-lookup"><span data-stu-id="94abc-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="94abc-130">The front-end port range starts at 50000.</span><span class="sxs-lookup"><span data-stu-id="94abc-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="94abc-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span><span class="sxs-lookup"><span data-stu-id="94abc-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="94abc-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span><span class="sxs-lookup"><span data-stu-id="94abc-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="94abc-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span><span class="sxs-lookup"><span data-stu-id="94abc-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="94abc-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span><span class="sxs-lookup"><span data-stu-id="94abc-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON Explorer][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="94abc-136">Deploy the project</span><span class="sxs-lookup"><span data-stu-id="94abc-136">Deploy the project</span></span>
1. <span data-ttu-id="94abc-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span><span class="sxs-lookup"><span data-stu-id="94abc-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="94abc-138">Right-click on the project node and choose **Deploy | New Deployment**.</span><span class="sxs-lookup"><span data-stu-id="94abc-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![Deploy Template][5deploy_Template]
    
2. <span data-ttu-id="94abc-140">Select your subscription in the “Deploy to Resource Group” dialog.</span><span class="sxs-lookup"><span data-stu-id="94abc-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![Deploy Template][6deploy_Template]

3. <span data-ttu-id="94abc-142">From here, you can create an Azure Resource Group to deploy your Template to.</span><span class="sxs-lookup"><span data-stu-id="94abc-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![New Resource Group][new_resource]

4. <span data-ttu-id="94abc-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span><span class="sxs-lookup"><span data-stu-id="94abc-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="94abc-145">Provide the username and password for the OS, which is required to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="94abc-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="94abc-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span><span class="sxs-lookup"><span data-stu-id="94abc-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![Edit Parameters][edit_parameters]

5. <span data-ttu-id="94abc-148">Now click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="94abc-148">Now click **Deploy**.</span></span> <span data-ttu-id="94abc-149">The **Output** window shows the deployment progress.</span><span class="sxs-lookup"><span data-stu-id="94abc-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="94abc-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="94abc-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![Output Window][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="94abc-152">Exploring your Virtual Machine Scale Set</span><span class="sxs-lookup"><span data-stu-id="94abc-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="94abc-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span><span class="sxs-lookup"><span data-stu-id="94abc-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="94abc-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span><span class="sxs-lookup"><span data-stu-id="94abc-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="94abc-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="94abc-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![Cloud Explorer][cloud_explorer]

 <span data-ttu-id="94abc-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explorer and debug Azure resources, giving a window into the “instance view” and also showing PowerShell commands for the resources you are looking at.</span><span class="sxs-lookup"><span data-stu-id="94abc-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explorer and debug Azure resources, giving a window into the “instance view” and also showing PowerShell commands for the resources you are looking at.</span></span> <span data-ttu-id="94abc-158">While Virtual Machine Scale Sets are in preview, the Resource Explorer shows the most detail for your Virtual Machine Scale Sets.</span><span class="sxs-lookup"><span data-stu-id="94abc-158">While Virtual Machine Scale Sets are in preview, the Resource Explorer shows the most detail for your Virtual Machine Scale Sets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94abc-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="94abc-159">Next steps</span></span>
<span data-ttu-id="94abc-160">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span><span class="sxs-lookup"><span data-stu-id="94abc-160">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="94abc-161">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span><span class="sxs-lookup"><span data-stu-id="94abc-161">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="94abc-162">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span><span class="sxs-lookup"><span data-stu-id="94abc-162">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png











