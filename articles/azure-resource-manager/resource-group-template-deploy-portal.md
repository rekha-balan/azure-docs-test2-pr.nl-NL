---
title: Use Azure portal to deploy Azure resources | Microsoft Docs
description: Use Azure portal and Azure Resource Manage to deploy your resources.
services: azure-resource-manager,azure-portal
documentationcenter: ''
author: tfitzmac
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/03/2018
ms.author: tomfitz
ms.openlocfilehash: c16d584f17aa2c209c9c0ec94d35f6fe78ba1907
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44771673"
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-portal"></a><span data-ttu-id="86916-103">Deploy resources with Resource Manager templates and Azure portal</span><span class="sxs-lookup"><span data-stu-id="86916-103">Deploy resources with Resource Manager templates and Azure portal</span></span>

<span data-ttu-id="86916-104">This article shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="86916-104">This article shows how to use the [Azure portal](https://portal.azure.com) with [Azure Resource Manager](resource-group-overview.md) to deploy your Azure resources.</span></span> <span data-ttu-id="86916-105">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="86916-105">To learn about managing your resources, see [Manage Azure resources through portal](resource-group-portal.md).</span></span>

## <a name="create-resource-group"></a><span data-ttu-id="86916-106">Create resource group</span><span class="sxs-lookup"><span data-stu-id="86916-106">Create resource group</span></span>

1. <span data-ttu-id="86916-107">To create an empty resource group, select **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="86916-107">To create an empty resource group, select **Resource groups**.</span></span>

   ![Select resource groups](./media/resource-group-template-deploy-portal/select-resource-groups.png)

1. <span data-ttu-id="86916-109">Under Resource groups, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="86916-109">Under Resource groups, select **Add**.</span></span>

   ![Add resource group](./media/resource-group-template-deploy-portal/add-resource-group.png)

1. <span data-ttu-id="86916-111">Give it a name and location, and, if necessary, select a subscription.</span><span class="sxs-lookup"><span data-stu-id="86916-111">Give it a name and location, and, if necessary, select a subscription.</span></span> <span data-ttu-id="86916-112">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span><span class="sxs-lookup"><span data-stu-id="86916-112">You need to provide a location for the resource group because the resource group stores metadata about the resources.</span></span> <span data-ttu-id="86916-113">For compliance reasons, you may want to specify where that metadata is stored.</span><span class="sxs-lookup"><span data-stu-id="86916-113">For compliance reasons, you may want to specify where that metadata is stored.</span></span> <span data-ttu-id="86916-114">In general, we recommend that you specify a location where most of your resources will reside.</span><span class="sxs-lookup"><span data-stu-id="86916-114">In general, we recommend that you specify a location where most of your resources will reside.</span></span> <span data-ttu-id="86916-115">Using the same location can simplify your template.</span><span class="sxs-lookup"><span data-stu-id="86916-115">Using the same location can simplify your template.</span></span>

   ![Set group values](./media/resource-group-template-deploy-portal/set-group-properties.png)

   <span data-ttu-id="86916-117">When you have finished setting the properties, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="86916-117">When you have finished setting the properties, select **Create**.</span></span>

1. <span data-ttu-id="86916-118">To see your new resource group, select **Refresh**.</span><span class="sxs-lookup"><span data-stu-id="86916-118">To see your new resource group, select **Refresh**.</span></span>

   ![Refresh resource groups](./media/resource-group-template-deploy-portal/refresh-resource-groups.png)

## <a name="deploy-resources-from-marketplace"></a><span data-ttu-id="86916-120">Deploy resources from Marketplace</span><span class="sxs-lookup"><span data-stu-id="86916-120">Deploy resources from Marketplace</span></span>

<span data-ttu-id="86916-121">After you create a resource group, you can deploy resources to it from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="86916-121">After you create a resource group, you can deploy resources to it from the Marketplace.</span></span> <span data-ttu-id="86916-122">The Marketplace provides pre-defined solutions for common scenarios.</span><span class="sxs-lookup"><span data-stu-id="86916-122">The Marketplace provides pre-defined solutions for common scenarios.</span></span>

1. <span data-ttu-id="86916-123">To start a deployment, select **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="86916-123">To start a deployment, select **Create a resource**.</span></span>

   ![New resource](./media/resource-group-template-deploy-portal/new-resources.png)

1. <span data-ttu-id="86916-125">Find the type of resource you would like to deploy.</span><span class="sxs-lookup"><span data-stu-id="86916-125">Find the type of resource you would like to deploy.</span></span>

   ![Select resource type](./media/resource-group-template-deploy-portal/select-resource-type.png)

1. <span data-ttu-id="86916-127">If you don't see the particular solution you would like to deploy, you can search the Marketplace for it.</span><span class="sxs-lookup"><span data-stu-id="86916-127">If you don't see the particular solution you would like to deploy, you can search the Marketplace for it.</span></span> <span data-ttu-id="86916-128">For example, to find a Wordpress solution, start typing **Wordpress** and select the option you want.</span><span class="sxs-lookup"><span data-stu-id="86916-128">For example, to find a Wordpress solution, start typing **Wordpress** and select the option you want.</span></span>

   ![Search marketplace](./media/resource-group-template-deploy-portal/search-resource.png)

1. <span data-ttu-id="86916-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span><span class="sxs-lookup"><span data-stu-id="86916-130">Depending on the type of selected resource, you have a collection of relevant properties to set before deployment.</span></span> <span data-ttu-id="86916-131">For all types, you must select a destination resource group.</span><span class="sxs-lookup"><span data-stu-id="86916-131">For all types, you must select a destination resource group.</span></span> <span data-ttu-id="86916-132">The following image shows how to create a web app and deploy it to the resource group you created.</span><span class="sxs-lookup"><span data-stu-id="86916-132">The following image shows how to create a web app and deploy it to the resource group you created.</span></span>

   ![Create resource group](./media/resource-group-template-deploy-portal/select-existing-group.png)

   <span data-ttu-id="86916-134">Alternatively, you can decide to create a resource group when deploying your resources.</span><span class="sxs-lookup"><span data-stu-id="86916-134">Alternatively, you can decide to create a resource group when deploying your resources.</span></span> <span data-ttu-id="86916-135">Select **Create new** and give the resource group a name.</span><span class="sxs-lookup"><span data-stu-id="86916-135">Select **Create new** and give the resource group a name.</span></span>

   ![Create new resource group](./media/resource-group-template-deploy-portal/select-new-group.png)

1. <span data-ttu-id="86916-137">Your deployment begins.</span><span class="sxs-lookup"><span data-stu-id="86916-137">Your deployment begins.</span></span> <span data-ttu-id="86916-138">The deployment could take a few minutes.</span><span class="sxs-lookup"><span data-stu-id="86916-138">The deployment could take a few minutes.</span></span> <span data-ttu-id="86916-139">When the deployment has finished, you see a notification.</span><span class="sxs-lookup"><span data-stu-id="86916-139">When the deployment has finished, you see a notification.</span></span>

   ![View notification](./media/resource-group-template-deploy-portal/view-notification.png)

1. <span data-ttu-id="86916-141">After deploying your resources, you can add more resources to the resource group by selecting **Add**.</span><span class="sxs-lookup"><span data-stu-id="86916-141">After deploying your resources, you can add more resources to the resource group by selecting **Add**.</span></span>

   ![Add resource](./media/resource-group-template-deploy-portal/add-resource.png)

## <a name="deploy-resources-from-custom-template"></a><span data-ttu-id="86916-143">Deploy resources from custom template</span><span class="sxs-lookup"><span data-stu-id="86916-143">Deploy resources from custom template</span></span>

<span data-ttu-id="86916-144">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span><span class="sxs-lookup"><span data-stu-id="86916-144">If you want to execute a deployment but not use any of the templates in the Marketplace, you can create a customized template that defines the infrastructure for your solution.</span></span> <span data-ttu-id="86916-145">To learn about creating templates, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="86916-145">To learn about creating templates, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

> [!NOTE]
> <span data-ttu-id="86916-146">The portal interface doesn't support referencing a [secret from a Key Vault](resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="86916-146">The portal interface doesn't support referencing a [secret from a Key Vault](resource-manager-keyvault-parameter.md).</span></span> <span data-ttu-id="86916-147">Instead, use [PowerShell](resource-group-template-deploy.md) or [Azure CLI](resource-group-template-deploy-cli.md) to deploy your template locally or from an external URI.</span><span class="sxs-lookup"><span data-stu-id="86916-147">Instead, use [PowerShell](resource-group-template-deploy.md) or [Azure CLI](resource-group-template-deploy-cli.md) to deploy your template locally or from an external URI.</span></span>

1. <span data-ttu-id="86916-148">To deploy a customized template through the portal, select **Create a resource**, and search for **Template Deployment** until you can select it from the options.</span><span class="sxs-lookup"><span data-stu-id="86916-148">To deploy a customized template through the portal, select **Create a resource**, and search for **Template Deployment** until you can select it from the options.</span></span>

   ![Search template deployment](./media/resource-group-template-deploy-portal/search-template.png)

1. <span data-ttu-id="86916-150">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="86916-150">Select **Create**.</span></span>

   ![Select create](./media/resource-group-template-deploy-portal/show-template-option.png)

1. <span data-ttu-id="86916-152">You see several options for creating a template.</span><span class="sxs-lookup"><span data-stu-id="86916-152">You see several options for creating a template.</span></span> <span data-ttu-id="86916-153">Select **Build your own template in the editor**.</span><span class="sxs-lookup"><span data-stu-id="86916-153">Select **Build your own template in the editor**.</span></span>

   ![View options](./media/resource-group-template-deploy-portal/see-options.png)

1. <span data-ttu-id="86916-155">You have a blank template that is available for customizing.</span><span class="sxs-lookup"><span data-stu-id="86916-155">You have a blank template that is available for customizing.</span></span>

   ![Create template](./media/resource-group-template-deploy-portal/blank-template.png)

1. <span data-ttu-id="86916-157">You can edit the JSON syntax manually, or select a pre-built template from the [Quickstart template gallery](https://azure.microsoft.com/resources/templates/).</span><span class="sxs-lookup"><span data-stu-id="86916-157">You can edit the JSON syntax manually, or select a pre-built template from the [Quickstart template gallery](https://azure.microsoft.com/resources/templates/).</span></span> <span data-ttu-id="86916-158">However, for this article, you use the **Add resource** option.</span><span class="sxs-lookup"><span data-stu-id="86916-158">However, for this article, you use the **Add resource** option.</span></span>

   ![Edit template](./media/resource-group-template-deploy-portal/select-add-resource.png)

1. <span data-ttu-id="86916-160">Select **Storage account** and provide a name.</span><span class="sxs-lookup"><span data-stu-id="86916-160">Select **Storage account** and provide a name.</span></span> <span data-ttu-id="86916-161">When finished providing values, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="86916-161">When finished providing values, select **OK**.</span></span>

   ![Select storage account](./media/resource-group-template-deploy-portal/add-storage-account.png)

1. <span data-ttu-id="86916-163">The editor automatically adds JSON for the resource type.</span><span class="sxs-lookup"><span data-stu-id="86916-163">The editor automatically adds JSON for the resource type.</span></span> <span data-ttu-id="86916-164">Notice that it includes a parameter for defining the type of storage account.</span><span class="sxs-lookup"><span data-stu-id="86916-164">Notice that it includes a parameter for defining the type of storage account.</span></span> <span data-ttu-id="86916-165">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="86916-165">Select **Save**.</span></span>

   ![Show template](./media/resource-group-template-deploy-portal/show-json.png)

1. <span data-ttu-id="86916-167">Now, you have the option to deploy the resources defined in the template.</span><span class="sxs-lookup"><span data-stu-id="86916-167">Now, you have the option to deploy the resources defined in the template.</span></span> <span data-ttu-id="86916-168">To deploy, agree to the terms and conditions, and select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="86916-168">To deploy, agree to the terms and conditions, and select **Purchase**.</span></span>

   ![Deploy template](./media/resource-group-template-deploy-portal/provide-custom-template-values.png)

## <a name="deploy-resources-from-a-template-saved-to-your-account"></a><span data-ttu-id="86916-170">Deploy resources from a template saved to your account</span><span class="sxs-lookup"><span data-stu-id="86916-170">Deploy resources from a template saved to your account</span></span>

<span data-ttu-id="86916-171">The portal enables you to save a template to your Azure account, and redeploy it later.</span><span class="sxs-lookup"><span data-stu-id="86916-171">The portal enables you to save a template to your Azure account, and redeploy it later.</span></span> <span data-ttu-id="86916-172">For more information on templates, see [Create and deploy your first Azure Resource Manager template](resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="86916-172">For more information on templates, see [Create and deploy your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>

1. <span data-ttu-id="86916-173">To find your saved templates, select **More services**.</span><span class="sxs-lookup"><span data-stu-id="86916-173">To find your saved templates, select **More services**.</span></span>

   ![More services](./media/resource-group-template-deploy-portal/more-services.png)

1. <span data-ttu-id="86916-175">Search for **templates** and select that option.</span><span class="sxs-lookup"><span data-stu-id="86916-175">Search for **templates** and select that option.</span></span>

   ![Search templates](./media/resource-group-template-deploy-portal/find-templates.png)

1. <span data-ttu-id="86916-177">From the list of templates saved to your account, select the one you wish to work on.</span><span class="sxs-lookup"><span data-stu-id="86916-177">From the list of templates saved to your account, select the one you wish to work on.</span></span>

   ![Saved templates](./media/resource-group-template-deploy-portal/saved-templates.png)

1. <span data-ttu-id="86916-179">Select **Deploy** to redeploy this saved template.</span><span class="sxs-lookup"><span data-stu-id="86916-179">Select **Deploy** to redeploy this saved template.</span></span>

   ![Deploy saved template](./media/resource-group-template-deploy-portal/deploy-saved-template.png)

## <a name="next-steps"></a><span data-ttu-id="86916-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="86916-181">Next steps</span></span>
* <span data-ttu-id="86916-182">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="86916-182">To view audit logs, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="86916-183">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="86916-183">To troubleshoot deployment errors, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
* <span data-ttu-id="86916-184">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="86916-184">To retrieve a template from a deployment or resource group, see [Export Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="86916-185">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span><span class="sxs-lookup"><span data-stu-id="86916-185">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span></span>
