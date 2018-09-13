---
title: Get started with private Templates | Microsoft Docs
description: Add, manage and share your private templates using the Azure portal, the Azure CLI, or PowerShell.
services: marketplace-customer
documentationcenter: ''
author: VybavaRamadoss
manager: asimm
editor: ''
tags: marketplace, azure-resource-manager
keywords: ''
ms.assetid: 6ec20778-b578-4885-acb5-104b0e51ea1a
ms.service: marketplace
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: vybavar
ms.openlocfilehash: 6c6352a4b396e7009007db032f789d30f72d14d7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563326"
---
# <a name="get-started-with-private-templates-on-the-azure-portal"></a><span data-ttu-id="948ff-103">Get started with private Templates on the Azure Portal</span><span class="sxs-lookup"><span data-stu-id="948ff-103">Get started with private Templates on the Azure Portal</span></span>
<span data-ttu-id="948ff-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span><span class="sxs-lookup"><span data-stu-id="948ff-104">An [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) template is a declarative template used to define your deployment.</span></span> <span data-ttu-id="948ff-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span><span class="sxs-lookup"><span data-stu-id="948ff-105">You can define the resources to deploy for a solution, and specify parameters and variables that enable you to input values for different environments.</span></span> <span data-ttu-id="948ff-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span><span class="sxs-lookup"><span data-stu-id="948ff-106">The template consists of JSON and expressions which you can use to construct values for your deployment.</span></span>

<span data-ttu-id="948ff-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span><span class="sxs-lookup"><span data-stu-id="948ff-107">You can use the new **Templates** capability in the [Azure Portal](https://portal.azure.com) along with the **Microsoft.Gallery** resource provider as an extension of the [Azure Marketplace](https://azure.microsoft.com/marketplace/) to enable users to create, manage and deploy private templates from a personal library.</span></span>

<span data-ttu-id="948ff-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="948ff-108">This document walks you through adding, managing and sharing a private **Template** using the Azure Portal.</span></span>

## <a name="guidance"></a><span data-ttu-id="948ff-109">Guidance</span><span class="sxs-lookup"><span data-stu-id="948ff-109">Guidance</span></span>
<span data-ttu-id="948ff-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span><span class="sxs-lookup"><span data-stu-id="948ff-110">The following suggestions will help you take full advantage of **Templates** when working with your solutions:</span></span>

* <span data-ttu-id="948ff-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span><span class="sxs-lookup"><span data-stu-id="948ff-111">A **Template** is an encapsulating resource that contains an Resource Manager template and additional metadata.</span></span> <span data-ttu-id="948ff-112">It behaves very similarly to an item in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="948ff-112">It behaves very similarly to an item in the Marketplace.</span></span> <span data-ttu-id="948ff-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span><span class="sxs-lookup"><span data-stu-id="948ff-113">The key difference is that it is a private item as opposed to the public Marketplace items.</span></span>
* <span data-ttu-id="948ff-114">The **Templates** library works well for users who need to customize their deployments.</span><span class="sxs-lookup"><span data-stu-id="948ff-114">The **Templates** library works well for users who need to customize their deployments.</span></span>
* <span data-ttu-id="948ff-115">**Templates** work well for users who need a simple repository within Azure.</span><span class="sxs-lookup"><span data-stu-id="948ff-115">**Templates** work well for users who need a simple repository within Azure.</span></span>
* <span data-ttu-id="948ff-116">Start with an existing Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="948ff-116">Start with an existing Resource Manager template.</span></span> <span data-ttu-id="948ff-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="948ff-117">Find templates in [github](https://github.com/Azure/azure-quickstart-templates) or [Export template](../azure-resource-manager/resource-manager-export-template.md) from an existing resource group.</span></span>
* <span data-ttu-id="948ff-118">**Templates** are tied to the user who publishes them.</span><span class="sxs-lookup"><span data-stu-id="948ff-118">**Templates** are tied to the user who publishes them.</span></span> <span data-ttu-id="948ff-119">The publisher name is visible to everyone who has read access to it.</span><span class="sxs-lookup"><span data-stu-id="948ff-119">The publisher name is visible to everyone who has read access to it.</span></span>
* <span data-ttu-id="948ff-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span><span class="sxs-lookup"><span data-stu-id="948ff-120">**Templates** are Resource Manager resources and cannot be renamed once published.</span></span>

## <a name="add-a-template-resource"></a><span data-ttu-id="948ff-121">Add a Template resource</span><span class="sxs-lookup"><span data-stu-id="948ff-121">Add a Template resource</span></span>
<span data-ttu-id="948ff-122">There are two ways to create a **Template** resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="948ff-122">There are two ways to create a **Template** resource in the Azure portal.</span></span>

### <a name="method-1--create-a-new-template-resource-from-a-running-resource-group"></a><span data-ttu-id="948ff-123">Method 1 : Create a new Template resource from a running resource group</span><span class="sxs-lookup"><span data-stu-id="948ff-123">Method 1 : Create a new Template resource from a running resource group</span></span>
1. <span data-ttu-id="948ff-124">Navigate to an existing resource group on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="948ff-124">Navigate to an existing resource group on the Azure Portal.</span></span> <span data-ttu-id="948ff-125">Select **Export template** in **Settings**.</span><span class="sxs-lookup"><span data-stu-id="948ff-125">Select **Export template** in **Settings**.</span></span>
2. <span data-ttu-id="948ff-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span><span class="sxs-lookup"><span data-stu-id="948ff-126">Once the Resource Manager template is exported, use the **Save Template** button to save it to the **Templates** repository.</span></span> <span data-ttu-id="948ff-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="948ff-127">Find complete details for Export template [here](../azure-resource-manager/resource-manager-export-template.md).</span></span>
   <br /><br />
   <span data-ttu-id="948ff-128">![Resource group export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/rg-export-portal1.PNG)</span><span class="sxs-lookup"><span data-stu-id="948ff-128">![Resource group export](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/rg-export-portal1.PNG)</span></span>  <br />
3. <span data-ttu-id="948ff-129">Select the **Save to Template** command button.</span><span class="sxs-lookup"><span data-stu-id="948ff-129">Select the **Save to Template** command button.</span></span>
   <br /><br />
4. <span data-ttu-id="948ff-130">Enter the following information:</span><span class="sxs-lookup"><span data-stu-id="948ff-130">Enter the following information:</span></span>
   
   * <span data-ttu-id="948ff-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span><span class="sxs-lookup"><span data-stu-id="948ff-131">Name – Name of the template object (NOTE: This is an Azure Resource Manager based name.</span></span> <span data-ttu-id="948ff-132">All naming restrictions apply and it cannot be changed once created).</span><span class="sxs-lookup"><span data-stu-id="948ff-132">All naming restrictions apply and it cannot be changed once created).</span></span>
   * <span data-ttu-id="948ff-133">Description – Quick summary about the template.</span><span class="sxs-lookup"><span data-stu-id="948ff-133">Description – Quick summary about the template.</span></span>
     
     ![Save Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/save-template-portal1.PNG)  <br />
5. <span data-ttu-id="948ff-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="948ff-135">Click **Save**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="948ff-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span><span class="sxs-lookup"><span data-stu-id="948ff-136">The Export template blade shows notifications when the exported Resource Manager template has errors, but you will still be able to save this Resource Manager template to the Templates.</span></span> <span data-ttu-id="948ff-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="948ff-137">Ensure that you check and fix any Resource Manager template issues before redeploying the exported Resource Manager template.</span></span>
   > 
   > 

### <a name="method-2--add-a-new-template-resource-from-browse"></a><span data-ttu-id="948ff-138">Method 2 : Add a new Template resource from browse</span><span class="sxs-lookup"><span data-stu-id="948ff-138">Method 2 : Add a new Template resource from browse</span></span>
<span data-ttu-id="948ff-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span><span class="sxs-lookup"><span data-stu-id="948ff-139">You can also add a new **Template** from scratch using the +Add command button in **Browse > Templates**.</span></span> <span data-ttu-id="948ff-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span><span class="sxs-lookup"><span data-stu-id="948ff-140">You will need to provide a Name, Description and the Resource Manager template JSON.</span></span>

![Add Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/add-template-portal1.PNG)  <br />

> [!NOTE]
> <span data-ttu-id="948ff-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span><span class="sxs-lookup"><span data-stu-id="948ff-142">Microsoft.Gallery is a Tenant based Azure resource provider.</span></span> <span data-ttu-id="948ff-143">The Template resource is tied to the user who created it.</span><span class="sxs-lookup"><span data-stu-id="948ff-143">The Template resource is tied to the user who created it.</span></span> <span data-ttu-id="948ff-144">It is not tied to any specific subscription.</span><span class="sxs-lookup"><span data-stu-id="948ff-144">It is not tied to any specific subscription.</span></span> <span data-ttu-id="948ff-145">A subscription needs to be chosen only when deploying a Template.</span><span class="sxs-lookup"><span data-stu-id="948ff-145">A subscription needs to be chosen only when deploying a Template.</span></span>
> 
> 

## <a name="view-template-resources"></a><span data-ttu-id="948ff-146">View Template resources</span><span class="sxs-lookup"><span data-stu-id="948ff-146">View Template resources</span></span>
<span data-ttu-id="948ff-147">All **Templates** available to you can be seen at **Browse > Templates**.</span><span class="sxs-lookup"><span data-stu-id="948ff-147">All **Templates** available to you can be seen at **Browse > Templates**.</span></span> <span data-ttu-id="948ff-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span><span class="sxs-lookup"><span data-stu-id="948ff-148">This includes **Templates** you have created as well as ones that have been shared with you with varying levels of permissions.</span></span> <span data-ttu-id="948ff-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span><span class="sxs-lookup"><span data-stu-id="948ff-149">More details in the [access control](#access-control-for-a-tenant-resource-provider) section below.</span></span>

![View Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/view-template-portal1.PNG)  <br />

<span data-ttu-id="948ff-151">You can view the details of a **Template** by clicking into an item in the list.</span><span class="sxs-lookup"><span data-stu-id="948ff-151">You can view the details of a **Template** by clicking into an item in the list.</span></span>

![View Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/view-template-portal2c.png)  <br />

## <a name="edit-a-template-resource"></a><span data-ttu-id="948ff-153">Edit a Template resource</span><span class="sxs-lookup"><span data-stu-id="948ff-153">Edit a Template resource</span></span>
<span data-ttu-id="948ff-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span><span class="sxs-lookup"><span data-stu-id="948ff-154">You can initiate the edit flow for a **Template** by right clicking the item on the Browse list or by choosing the Edit command button.</span></span>

![Edit Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/edit-template-portal1a.PNG)  <br />

<span data-ttu-id="948ff-156">You can edit the description or Resource Manager template text.</span><span class="sxs-lookup"><span data-stu-id="948ff-156">You can edit the description or Resource Manager template text.</span></span> <span data-ttu-id="948ff-157">You cannot edit the name since it is an Resource Manager resource name.</span><span class="sxs-lookup"><span data-stu-id="948ff-157">You cannot edit the name since it is an Resource Manager resource name.</span></span> <span data-ttu-id="948ff-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span><span class="sxs-lookup"><span data-stu-id="948ff-158">When you edit the Resource Manager template JSON we will validate to ensure that it is valid JSON.</span></span> <span data-ttu-id="948ff-159">Choose **OK** and then **Save** to save your updated template.</span><span class="sxs-lookup"><span data-stu-id="948ff-159">Choose **OK** and then **Save** to save your updated template.</span></span>

![Edit Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/edit-template-portal2a.PNG)  <br />

<span data-ttu-id="948ff-161">Once the **Template** is saved you will see a confirmation notification.</span><span class="sxs-lookup"><span data-stu-id="948ff-161">Once the **Template** is saved you will see a confirmation notification.</span></span>

![Edit Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/edit-template-portal3b.png)  <br />

## <a name="deploy-a-template-resource"></a><span data-ttu-id="948ff-163">Deploy a Template resource</span><span class="sxs-lookup"><span data-stu-id="948ff-163">Deploy a Template resource</span></span>
<span data-ttu-id="948ff-164">You can deploy any **Template** that you have **Read** permissions on.</span><span class="sxs-lookup"><span data-stu-id="948ff-164">You can deploy any **Template** that you have **Read** permissions on.</span></span> <span data-ttu-id="948ff-165">The deployment flow launches the standard Azure Template deployment blade.</span><span class="sxs-lookup"><span data-stu-id="948ff-165">The deployment flow launches the standard Azure Template deployment blade.</span></span> <span data-ttu-id="948ff-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span><span class="sxs-lookup"><span data-stu-id="948ff-166">Fill out the values for the Resource Manager template parameters to proceed with the deployment.</span></span>

![Deploy Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/deploy-template-portal1b.png)  <br />

## <a name="share-a-template-resource"></a><span data-ttu-id="948ff-168">Share a Template resource</span><span class="sxs-lookup"><span data-stu-id="948ff-168">Share a Template resource</span></span>
<span data-ttu-id="948ff-169">A **Template** resource can be shared with your peers.</span><span class="sxs-lookup"><span data-stu-id="948ff-169">A **Template** resource can be shared with your peers.</span></span> <span data-ttu-id="948ff-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="948ff-170">Sharing behaves similarly to [role assignment for any resource on Azure](../active-directory/role-based-access-control-configure.md).</span></span> <span data-ttu-id="948ff-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span><span class="sxs-lookup"><span data-stu-id="948ff-171">The **Template** owner provides permissions to other users who can interact with a Template resource.</span></span> <span data-ttu-id="948ff-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span><span class="sxs-lookup"><span data-stu-id="948ff-172">The person or group of people you share the **Template** with will be able to see the Resource Manager template and its gallery properties.</span></span>

### <a name="access-control-for-the-microsoftgallery-resources"></a><span data-ttu-id="948ff-173">Access control for the Microsoft.Gallery resources</span><span class="sxs-lookup"><span data-stu-id="948ff-173">Access control for the Microsoft.Gallery resources</span></span>
| <span data-ttu-id="948ff-174">Role</span><span class="sxs-lookup"><span data-stu-id="948ff-174">Role</span></span> | <span data-ttu-id="948ff-175">Permissions</span><span class="sxs-lookup"><span data-stu-id="948ff-175">Permissions</span></span> |
| --- | --- |
| <span data-ttu-id="948ff-176">Owner</span><span class="sxs-lookup"><span data-stu-id="948ff-176">Owner</span></span> |<span data-ttu-id="948ff-177">Allows full control on the Template resource including Share</span><span class="sxs-lookup"><span data-stu-id="948ff-177">Allows full control on the Template resource including Share</span></span> |
| <span data-ttu-id="948ff-178">Reader</span><span class="sxs-lookup"><span data-stu-id="948ff-178">Reader</span></span> |<span data-ttu-id="948ff-179">Allows Read and Execute(Deploy) on the Template resource</span><span class="sxs-lookup"><span data-stu-id="948ff-179">Allows Read and Execute(Deploy) on the Template resource</span></span> |
| <span data-ttu-id="948ff-180">Contributor</span><span class="sxs-lookup"><span data-stu-id="948ff-180">Contributor</span></span> |<span data-ttu-id="948ff-181">Allows Edit and Delete permission on the Template resource.</span><span class="sxs-lookup"><span data-stu-id="948ff-181">Allows Edit and Delete permission on the Template resource.</span></span> <span data-ttu-id="948ff-182">User cannot Share the Template with others</span><span class="sxs-lookup"><span data-stu-id="948ff-182">User cannot Share the Template with others</span></span> |

<span data-ttu-id="948ff-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span><span class="sxs-lookup"><span data-stu-id="948ff-183">Select **Share** on the browse item by right clicking or on the view blade of a specific item.</span></span> <span data-ttu-id="948ff-184">This launches a Share experience.</span><span class="sxs-lookup"><span data-stu-id="948ff-184">This launches a Share experience.</span></span>

![Share Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/share-template-portal1a.png)  <br />

 <span data-ttu-id="948ff-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span><span class="sxs-lookup"><span data-stu-id="948ff-186">You can now choose a role and a user or group to provide access to a particular **Template**.</span></span> <span data-ttu-id="948ff-187">The available roles are Owner, Reader and Contributor.</span><span class="sxs-lookup"><span data-stu-id="948ff-187">The available roles are Owner, Reader and Contributor.</span></span> <span data-ttu-id="948ff-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span><span class="sxs-lookup"><span data-stu-id="948ff-188">More details in the [access control](#access-control-for-a-tenant-resource-provider) section above.</span></span>

![Share Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/share-template-portal2b.png)  <br />

![Share Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/share-template-portal3b.png)  <br />

<span data-ttu-id="948ff-191">Click **Select** and **Ok**.</span><span class="sxs-lookup"><span data-stu-id="948ff-191">Click **Select** and **Ok**.</span></span> <span data-ttu-id="948ff-192">You can now see the users or groups you added to the resource.</span><span class="sxs-lookup"><span data-stu-id="948ff-192">You can now see the users or groups you added to the resource.</span></span>

![Share Template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/marketplace-consumer/media/share-template-portal4b.png)  <br />

> [!NOTE]
> <span data-ttu-id="948ff-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span><span class="sxs-lookup"><span data-stu-id="948ff-194">A Template can only be shared with users and groups in the same Azure Active Directory tenant.</span></span> <span data-ttu-id="948ff-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span><span class="sxs-lookup"><span data-stu-id="948ff-195">If you share a Template with an email address that is not in your tenant, an invitation will be sent asking the user to join the tenant as a guest.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="948ff-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="948ff-196">Next steps</span></span>
* <span data-ttu-id="948ff-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span><span class="sxs-lookup"><span data-stu-id="948ff-197">To learn about creating Resource Manager templates, see [Authoring templates](../azure-resource-manager/resource-group-authoring-templates.md)</span></span>
* <span data-ttu-id="948ff-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="948ff-198">To understand the functions you can use in an Resource Manager template, see [Template functions](../azure-resource-manager/resource-group-template-functions.md)</span></span>
* <span data-ttu-id="948ff-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span><span class="sxs-lookup"><span data-stu-id="948ff-199">For guidance on designing your templates, see [Best practices for designing Azure Resource Manager templates](../azure-resource-manager/best-practices-resource-manager-design-templates.md)</span></span>














