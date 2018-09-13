---
title: Use Azure portal to deploy Azure resources | Microsoft Docs
description: Use Azure portal and Azure Resource Manage to deploy your resources.
services: azure-resource-manager,azure-portal
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 2c98a4aa-8d9f-4a0a-b764-214dbe8ed009
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: tomfitz
ms.openlocfilehash: d30262fc92f79e0d2cf1eef8db6b2d527346f97c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549863"
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="57ec9-103">Deploy resources with Resource Manager templates and Azure portal</span><span class="sxs-lookup"><span data-stu-id="57ec9-103">Deploy resources with Resource Manager templates and Azure portal</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

<span data-ttu-id="57ec9-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="57ec9-108">This topic shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="57ec9-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-109">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

<span data-ttu-id="57ec9-110">Currently, not every service supports the portal or Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57ec9-110">Currently, not every service supports the portal or Resource Manager.</span></span> <span data-ttu-id="57ec9-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="57ec9-111">For those services, you need to use the [classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="57ec9-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span><span class="sxs-lookup"><span data-stu-id="57ec9-112">For the status of each service, see [Azure portal availability chart](https://azure.microsoft.com/features/azure-portal/availability/).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="57ec9-113">Create resource group</span><span class="sxs-lookup"><span data-stu-id="57ec9-113">Create resource group</span></span>
1. <span data-ttu-id="57ec9-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="57ec9-114">To create an empty resource group, select **New** > **Management** > **Resource Group**.</span></span>
   
    ![create empty resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/create-empty-group.png)
2. <span data-ttu-id="57ec9-116">Give it a name and location, and, if necessary, select a subscription.</span><span class="sxs-lookup"><span data-stu-id="57ec9-116">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="57ec9-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span><span class="sxs-lookup"><span data-stu-id="57ec9-117">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="57ec9-118">For compliance reasons, you may want to specify where that metadata is stored.</span><span class="sxs-lookup"><span data-stu-id="57ec9-118">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="57ec9-119">In general, we recommend that you specify a location where most of your resources will reside.</span><span class="sxs-lookup"><span data-stu-id="57ec9-119">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="57ec9-120">Using the same location can simplify your template.</span><span class="sxs-lookup"><span data-stu-id="57ec9-120">Using the same location can simplify your template.</span></span>
   
    ![set group values](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/set-group-properties.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="57ec9-122">Deploy resources from Marketplace</span><span class="sxs-lookup"><span data-stu-id="57ec9-122">Deploy resources from Marketplace</span></span>
<span data-ttu-id="57ec9-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="57ec9-123">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="57ec9-124">The Marketplace provides pre-defined solutions for common scenarios.</span><span class="sxs-lookup"><span data-stu-id="57ec9-124">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="57ec9-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span><span class="sxs-lookup"><span data-stu-id="57ec9-125">To start a deployment, select **New** and the type of resource you would like to deploy.</span></span> <span data-ttu-id="57ec9-126">Then, look for the particular version of the resource you would like to deploy.</span><span class="sxs-lookup"><span data-stu-id="57ec9-126">Then, look for the particular version of the resource you would like to deploy.</span></span>
   
    ![deploy resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/deploy-resource.png)
2. <span data-ttu-id="57ec9-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span><span class="sxs-lookup"><span data-stu-id="57ec9-128">If you do not see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span>
   
    ![search marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/search-resource.png)
3. <span data-ttu-id="57ec9-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span><span class="sxs-lookup"><span data-stu-id="57ec9-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="57ec9-131">Those options are not shown here, as they vary based on resource type.</span><span class="sxs-lookup"><span data-stu-id="57ec9-131">Those options are not shown here, as they vary based on resource type.</span></span> <span data-ttu-id="57ec9-132">For all types, you must select a destination resource group.</span><span class="sxs-lookup"><span data-stu-id="57ec9-132">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="57ec9-133">The following image shows how to create a web app and deploy it to the resource group you created.</span><span class="sxs-lookup"><span data-stu-id="57ec9-133">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>
   
    ![create resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/select-existing-group.png)
   
    <span data-ttu-id="57ec9-135">Alternatively, you can decide to create a resource group when deploying your resources.</span><span class="sxs-lookup"><span data-stu-id="57ec9-135">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="57ec9-136">Select **Create new** and give the resource group a name.</span><span class="sxs-lookup"><span data-stu-id="57ec9-136">Select **Create new** and give the resource group a name.</span></span>
   
    ![create new resource group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/select-new-group.png)
4. <span data-ttu-id="57ec9-138">Your deployment begins.</span><span class="sxs-lookup"><span data-stu-id="57ec9-138">Your deployment begins.</span></span> <span data-ttu-id="57ec9-139">The deployment could take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="57ec9-139">The deployment could take a few minutes.</span></span> <span data-ttu-id="57ec9-140">When the deployment has finished, you see a notification.</span><span class="sxs-lookup"><span data-stu-id="57ec9-140">When the deployment has finished, you see a notification.</span></span>
   
    ![view notification](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/view-notification.png)
5. <span data-ttu-id="57ec9-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span><span class="sxs-lookup"><span data-stu-id="57ec9-142">After deploying your resources, you can add more resources to the resource group by using the **Add** command on the resource group blade.</span></span>
   
    ![add resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="57ec9-144">Deploy resources from custom template</span><span class="sxs-lookup"><span data-stu-id="57ec9-144">Deploy resources from custom template</span></span>
<span data-ttu-id="57ec9-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="57ec9-145">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="57ec9-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-146">To learn about creating templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

1. <span data-ttu-id="57ec9-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span><span class="sxs-lookup"><span data-stu-id="57ec9-147">To deploy a customized template through the portal, select **New**, and start searching for **Template Deployment** until you can select it from the options.</span></span>
   
    ![search template deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/search-template.png)
2. <span data-ttu-id="57ec9-149">Select **Template Deployment** from the available resources.</span><span class="sxs-lookup"><span data-stu-id="57ec9-149">Select **Template Deployment** from the available resources.</span></span>
   
    ![select template deployment](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/select-template.png)
3. <span data-ttu-id="57ec9-151">After launching the template deployment, open the blank template that is available for customizing.</span><span class="sxs-lookup"><span data-stu-id="57ec9-151">After launching the template deployment, open the blank template that is available for customizing.</span></span>
   
    ![create template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/show-custom-template.png)
   
    <span data-ttu-id="57ec9-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="57ec9-153">In the editor, add the JSON syntax that defines the resources you want to deploy.</span></span> <span data-ttu-id="57ec9-154">Select **Save** when done.</span><span class="sxs-lookup"><span data-stu-id="57ec9-154">Select **Save** when done.</span></span> <span data-ttu-id="57ec9-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-155">For guidance on writing the JSON syntax, see [Resource Manager template walkthrough](resource-manager-template-walkthrough.md).</span></span>
   
    ![edit template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/edit-template.png)
4. <span data-ttu-id="57ec9-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="57ec9-157">Or, you can select a pre-existing template from the [Azure quickstart templates](https://azure.microsoft.com/documentation/templates/).</span></span> <span data-ttu-id="57ec9-158">These templates are contributed by the community.</span><span class="sxs-lookup"><span data-stu-id="57ec9-158">These templates are contributed by the community.</span></span> <span data-ttu-id="57ec9-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span><span class="sxs-lookup"><span data-stu-id="57ec9-159">They cover many common scenarios, and someone may have added a template that is similar to what you are trying to deploy.</span></span> <span data-ttu-id="57ec9-160">You can search the templates to find something that matches your scenario.</span><span class="sxs-lookup"><span data-stu-id="57ec9-160">You can search the templates to find something that matches your scenario.</span></span>
   
    ![select quickstart template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/select-quickstart-template.png)
   
    <span data-ttu-id="57ec9-162">You can view the selected template in the editor.</span><span class="sxs-lookup"><span data-stu-id="57ec9-162">You can view the selected template in the editor.</span></span>
5. <span data-ttu-id="57ec9-163">After providing all the other values, select **Create** to deploy the template.</span><span class="sxs-lookup"><span data-stu-id="57ec9-163">After providing all the other values, select **Create** to deploy the template.</span></span> 
   
    ![deploy template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/create-custom-deploy.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="57ec9-165">Deploy resources from a template saved to your account</span><span class="sxs-lookup"><span data-stu-id="57ec9-165">Deploy resources from a template saved to your account</span></span>
<span data-ttu-id="57ec9-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span><span class="sxs-lookup"><span data-stu-id="57ec9-166">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="57ec9-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-167">For more information about working with these saved templates, [Get started with private templates on the Azure portal](../marketplace-consumer/mytemplates-getstarted.md).</span></span>

1. <span data-ttu-id="57ec9-168">To find your saved templates, select **Browse** > **Templates**.</span><span class="sxs-lookup"><span data-stu-id="57ec9-168">To find your saved templates, select **Browse** > **Templates**.</span></span>
   
    ![browse templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/browse-templates.png)
2. <span data-ttu-id="57ec9-170">From the list of templates saved to your account, select the one you wish to work on.</span><span class="sxs-lookup"><span data-stu-id="57ec9-170">From the list of templates saved to your account, select the one you wish to work on.</span></span>
   
    ![saved templates](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/saved-templates.png)
3. <span data-ttu-id="57ec9-172">Select **Deploy** to redeploy this saved template.</span><span class="sxs-lookup"><span data-stu-id="57ec9-172">Select **Deploy** to redeploy this saved template.</span></span>
   
    ![deploy saved template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="57ec9-174">Next Steps</span><span class="sxs-lookup"><span data-stu-id="57ec9-174">Next Steps</span></span>
* <span data-ttu-id="57ec9-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-175">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="57ec9-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-176">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="57ec9-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-177">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="57ec9-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="57ec9-178">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="57ec9-179">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="57ec9-179">For a four part series about automating deployment, see [Automating application deployments to Azure Virtual Machines](../virtual-machines/windows/dotnet-core-1-landing.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="57ec9-180">This series covers application architecture, access and security, availability and scale, and application deployment.</span><span class="sxs-lookup"><span data-stu-id="57ec9-180">This series covers application architecture, access and security, availability and scale, and application deployment.</span></span>


















