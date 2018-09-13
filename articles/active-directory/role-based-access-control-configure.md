---
title: Role-Based Access Control in the Azure portal | Microsoft Docs
description: Get started in access management with Role-Based Access Control in the Azure Portal. Use role assignments to assign permissions to your resources.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: 8078f366-a2c4-4fbb-a44b-fc39fd89df81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/27/2017
ms.author: kgremban
ms.openlocfilehash: 1c995e4a80c8bda5d5f4991dd26897ff557dabce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562889"
---
# <a name="use-role-based-access-control-to-manage-access-to-your-azure-subscription-resources"></a><span data-ttu-id="f0035-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span><span class="sxs-lookup"><span data-stu-id="f0035-104">Use Role-Based Access Control to manage access to your Azure subscription resources</span></span>
> [!div class="op_single_selector"]
> * [Manage access by user or group](role-based-access-control-manage-assignments.md)
> * [Manage access by resource](role-based-access-control-configure.md)

<span data-ttu-id="f0035-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span><span class="sxs-lookup"><span data-stu-id="f0035-107">Azure Role-Based Access Control (RBAC) enables fine-grained access management for Azure.</span></span> <span data-ttu-id="f0035-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span><span class="sxs-lookup"><span data-stu-id="f0035-108">Using RBAC, you can grant only the amount of access that users need to perform their jobs.</span></span> <span data-ttu-id="f0035-109">This article helps you get up and running with RBAC in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f0035-109">This article helps you get up and running with RBAC in the Azure portal.</span></span> <span data-ttu-id="f0035-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="f0035-110">If you want more details about how RBAC helps you manage access, see [What is Role-Based Access Control](role-based-access-control-what-is.md).</span></span>

<span data-ttu-id="f0035-111">Within each subscription, you can grant up to 2000 role assignments.</span><span class="sxs-lookup"><span data-stu-id="f0035-111">Within each subscription, you can grant up to 2000 role assignments.</span></span> 

## <a name="view-access"></a><span data-ttu-id="f0035-112">View access</span><span class="sxs-lookup"><span data-stu-id="f0035-112">View access</span></span>
<span data-ttu-id="f0035-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f0035-113">You can see who has access to a resource, resource group, or subscription from its main blade in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f0035-114">For example, we want to see who has access to one of our resource groups:</span><span class="sxs-lookup"><span data-stu-id="f0035-114">For example, we want to see who has access to one of our resource groups:</span></span>

1. <span data-ttu-id="f0035-115">Select **Resource groups** in the navigation bar on the left.</span><span class="sxs-lookup"><span data-stu-id="f0035-115">Select **Resource groups** in the navigation bar on the left.</span></span>  
    <span data-ttu-id="f0035-116">![Resource groups - icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/resourcegroups_icon.png)</span><span class="sxs-lookup"><span data-stu-id="f0035-116">![Resource groups - icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/resourcegroups_icon.png)</span></span>
2. <span data-ttu-id="f0035-117">Select the name of the resource group from the **Resource groups** blade.</span><span class="sxs-lookup"><span data-stu-id="f0035-117">Select the name of the resource group from the **Resource groups** blade.</span></span>
3. <span data-ttu-id="f0035-118">Select **Access control (IAM)** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="f0035-118">Select **Access control (IAM)** from the left menu.</span></span>  
4. <span data-ttu-id="f0035-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span><span class="sxs-lookup"><span data-stu-id="f0035-119">The Access control blade lists all users, groups, and applications that have been granted access to the resource group.</span></span>  
   
    ![Users blade - inherited vs assigned access screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/view-access.png)

<span data-ttu-id="f0035-121">Notice that some users were **Assigned** access while others **Inherited** it.</span><span class="sxs-lookup"><span data-stu-id="f0035-121">Notice that some users were **Assigned** access while others **Inherited** it.</span></span> <span data-ttu-id="f0035-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span><span class="sxs-lookup"><span data-stu-id="f0035-122">Access is either assigned specifically to the resource group or inherited from an assignment to the parent subscription.</span></span>

> [!NOTE]
> Classic subscription admins and co-admins are considered owners of the subscription in the new RBAC model.

## <a name="add-access"></a><span data-ttu-id="f0035-124">Add Access</span><span class="sxs-lookup"><span data-stu-id="f0035-124">Add Access</span></span>
<span data-ttu-id="f0035-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span><span class="sxs-lookup"><span data-stu-id="f0035-125">You grant access from within the resource, resource group, or subscription that is the scope of the role assignment.</span></span>

1. <span data-ttu-id="f0035-126">Select **Add** on the Access control blade.</span><span class="sxs-lookup"><span data-stu-id="f0035-126">Select **Add** on the Access control blade.</span></span>  
2. <span data-ttu-id="f0035-127">Select the role that you wish to assign from the **Select a role** blade.</span><span class="sxs-lookup"><span data-stu-id="f0035-127">Select the role that you wish to assign from the **Select a role** blade.</span></span>
3. <span data-ttu-id="f0035-128">Select the user, group, or application in your directory that you wish to grant access to.</span><span class="sxs-lookup"><span data-stu-id="f0035-128">Select the user, group, or application in your directory that you wish to grant access to.</span></span> <span data-ttu-id="f0035-129">You can search the directory with display names, email addresses, and object identifiers.</span><span class="sxs-lookup"><span data-stu-id="f0035-129">You can search the directory with display names, email addresses, and object identifiers.</span></span>  
   
    ![Add users blade - search screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/grant-access2.png)
4. <span data-ttu-id="f0035-131">Select **OK** to create the assignment.</span><span class="sxs-lookup"><span data-stu-id="f0035-131">Select **OK** to create the assignment.</span></span> <span data-ttu-id="f0035-132">The **Adding user** popup tracks the progress.</span><span class="sxs-lookup"><span data-stu-id="f0035-132">The **Adding user** popup tracks the progress.</span></span>  
    <span data-ttu-id="f0035-133">![Adding user progress bar - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/addinguser_popup.png)</span><span class="sxs-lookup"><span data-stu-id="f0035-133">![Adding user progress bar - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/addinguser_popup.png)</span></span>

<span data-ttu-id="f0035-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span><span class="sxs-lookup"><span data-stu-id="f0035-134">After successfully adding a role assignment, it will appear on the **Users** blade.</span></span>

## <a name="remove-access"></a><span data-ttu-id="f0035-135">Remove Access</span><span class="sxs-lookup"><span data-stu-id="f0035-135">Remove Access</span></span>
1. <span data-ttu-id="f0035-136">Use the check boxes on the Access control blade to select one or more role assignments.</span><span class="sxs-lookup"><span data-stu-id="f0035-136">Use the check boxes on the Access control blade to select one or more role assignments.</span></span>
2. <span data-ttu-id="f0035-137">Select **Remove**.</span><span class="sxs-lookup"><span data-stu-id="f0035-137">Select **Remove**.</span></span>  
3. <span data-ttu-id="f0035-138">A box will pop up asking you to confirm the action.</span><span class="sxs-lookup"><span data-stu-id="f0035-138">A box will pop up asking you to confirm the action.</span></span> <span data-ttu-id="f0035-139">Select **Yes** to remove the role assignments.</span><span class="sxs-lookup"><span data-stu-id="f0035-139">Select **Yes** to remove the role assignments.</span></span>

<span data-ttu-id="f0035-140">Inherited assignments cannot be removed.</span><span class="sxs-lookup"><span data-stu-id="f0035-140">Inherited assignments cannot be removed.</span></span> <span data-ttu-id="f0035-141">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span><span class="sxs-lookup"><span data-stu-id="f0035-141">If you need to remove an inherited assignment, you need to do it at the scope where the role assignment was created.</span></span> <span data-ttu-id="f0035-142">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span><span class="sxs-lookup"><span data-stu-id="f0035-142">In the **Scope** column, next to **Inherited** there is a link that takes you to the resources where this role was assigned.</span></span> <span data-ttu-id="f0035-143">Go to the resource listed there to remove the role assignment.</span><span class="sxs-lookup"><span data-stu-id="f0035-143">Go to the resource listed there to remove the role assignment.</span></span>

![Users blade - inherited access disables remove button screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/remove-access2.png)

## <a name="other-tools-to-manage-access"></a><span data-ttu-id="f0035-145">Other tools to manage access</span><span class="sxs-lookup"><span data-stu-id="f0035-145">Other tools to manage access</span></span>
<span data-ttu-id="f0035-146">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f0035-146">You can assign roles and manage access with Azure RBAC commands in tools other than the Azure portal.</span></span>  <span data-ttu-id="f0035-147">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span><span class="sxs-lookup"><span data-stu-id="f0035-147">Follow the links to learn more about the prerequisites and get started with the Azure RBAC commands.</span></span>

* [<span data-ttu-id="f0035-148">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0035-148">Azure PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
* [<span data-ttu-id="f0035-149">Azure Command-Line Interface</span><span class="sxs-lookup"><span data-stu-id="f0035-149">Azure Command-Line Interface</span></span>](role-based-access-control-manage-access-azure-cli.md)
* [<span data-ttu-id="f0035-150">REST API</span><span class="sxs-lookup"><span data-stu-id="f0035-150">REST API</span></span>](role-based-access-control-manage-access-rest.md)

## <a name="next-steps"></a><span data-ttu-id="f0035-151">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f0035-151">Next Steps</span></span>
* [<span data-ttu-id="f0035-152">Create an access change history report</span><span class="sxs-lookup"><span data-stu-id="f0035-152">Create an access change history report</span></span>](role-based-access-control-access-change-history-report.md)
* <span data-ttu-id="f0035-153">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span><span class="sxs-lookup"><span data-stu-id="f0035-153">See the [RBAC built-in roles](role-based-access-built-in-roles.md)</span></span>
* <span data-ttu-id="f0035-154">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span><span class="sxs-lookup"><span data-stu-id="f0035-154">Define your own [Custom roles in Azure RBAC](role-based-access-control-custom-roles.md)</span></span>






