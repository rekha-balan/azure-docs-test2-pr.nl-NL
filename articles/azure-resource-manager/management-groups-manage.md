---
title: How to change, delete, or manage your management groups - Azure | Microsoft Docs
description: Learn how to maintain and update your management group hierarchy.
author: rthorn17
manager: rithorn
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2018
ms.author: rithorn
ms.openlocfilehash: f7677d8b545c28522c370f3af422a55f3a656646
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856453"
---
# <a name="manage-your-resources-with-management-groups"></a><span data-ttu-id="5e178-103">Manage your resources with management groups</span><span class="sxs-lookup"><span data-stu-id="5e178-103">Manage your resources with management groups</span></span>

<span data-ttu-id="5e178-104">Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="5e178-104">Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions.</span></span> <span data-ttu-id="5e178-105">You can change, delete, and manage these containers to have hierarchies that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls (RBAC)](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e178-105">You can change, delete, and manage these containers to have hierarchies that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls (RBAC)](../role-based-access-control/overview.md).</span></span> <span data-ttu-id="5e178-106">To learn more about management groups, see [Organize your resources with Azure management groups](management-groups-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e178-106">To learn more about management groups, see [Organize your resources with Azure management groups](management-groups-overview.md).</span></span>

<span data-ttu-id="5e178-107">To make changes to a management group, you must have an Owner or Contributor role on the management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-107">To make changes to a management group, you must have an Owner or Contributor role on the management group.</span></span> <span data-ttu-id="5e178-108">To see what permissions you have, select the management group and then select **IAM**.</span><span class="sxs-lookup"><span data-stu-id="5e178-108">To see what permissions you have, select the management group and then select **IAM**.</span></span> <span data-ttu-id="5e178-109">To learn more about RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e178-109">To learn more about RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="change-the-name-of-a-management-group"></a><span data-ttu-id="5e178-110">Change the name of a management group</span><span class="sxs-lookup"><span data-stu-id="5e178-110">Change the name of a management group</span></span>

<span data-ttu-id="5e178-111">You can change the name of the management group by using the portal, PowerShell, or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5e178-111">You can change the name of the management group by using the portal, PowerShell, or Azure CLI.</span></span>

### <a name="change-the-name-in-the-portal"></a><span data-ttu-id="5e178-112">Change the name in the portal</span><span class="sxs-lookup"><span data-stu-id="5e178-112">Change the name in the portal</span></span>

1. <span data-ttu-id="5e178-113">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-113">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-114">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-114">Select **All services** > **Management groups**</span></span>  
3. <span data-ttu-id="5e178-115">Select the management group you would like to rename.</span><span class="sxs-lookup"><span data-stu-id="5e178-115">Select the management group you would like to rename.</span></span>
4. <span data-ttu-id="5e178-116">Select the **Rename group** option at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="5e178-116">Select the **Rename group** option at the top of the page.</span></span>

    ![Rename Group](media/management-groups/detail_action_small.png)
5. <span data-ttu-id="5e178-118">When the menu opens, enter the new name you would like to have displayed.</span><span class="sxs-lookup"><span data-stu-id="5e178-118">When the menu opens, enter the new name you would like to have displayed.</span></span>

    ![Rename Group](media/management-groups/rename_context.png)
6. <span data-ttu-id="5e178-120">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="5e178-120">Select **Save**.</span></span>

### <a name="change-the-name-in-powershell"></a><span data-ttu-id="5e178-121">Change the name in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e178-121">Change the name in PowerShell</span></span>

<span data-ttu-id="5e178-122">To update the display name use **Update-AzureRmManagementGroup**.</span><span class="sxs-lookup"><span data-stu-id="5e178-122">To update the display name use **Update-AzureRmManagementGroup**.</span></span> <span data-ttu-id="5e178-123">For example, to change a management groups name from "Contoso IT" to "Contoso Group", you run the following command:</span><span class="sxs-lookup"><span data-stu-id="5e178-123">For example, to change a management groups name from "Contoso IT" to "Contoso Group", you run the following command:</span></span> 

```azurepowershell-inetractive
C:\> Update-AzureRmManagementGroup -GroupName ContosoIt -DisplayName "Contoso Group"  
``` 

### <a name="change-the-name-in-azure-cli"></a><span data-ttu-id="5e178-124">Change the name in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e178-124">Change the name in Azure CLI</span></span>

<span data-ttu-id="5e178-125">For Azure CLI, use the update command.</span><span class="sxs-lookup"><span data-stu-id="5e178-125">For Azure CLI, use the update command.</span></span>

```azurecli-interactive
az account management-group update --name Contoso --display-name "Contoso Group" 
```

---

## <a name="delete-a-management-group"></a><span data-ttu-id="5e178-126">Delete a management group</span><span class="sxs-lookup"><span data-stu-id="5e178-126">Delete a management group</span></span>

<span data-ttu-id="5e178-127">To delete a management group, the following requirements must be met:</span><span class="sxs-lookup"><span data-stu-id="5e178-127">To delete a management group, the following requirements must be met:</span></span>

1. <span data-ttu-id="5e178-128">There are no child management groups or subscriptions under the management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-128">There are no child management groups or subscriptions under the management group.</span></span>
    - <span data-ttu-id="5e178-129">To move a subscription out of a management group, see [Move subscription to another management group](#Move-subscriptions-in-the-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="5e178-129">To move a subscription out of a management group, see [Move subscription to another management group](#Move-subscriptions-in-the-hierarchy).</span></span>
    - <span data-ttu-id="5e178-130">To move a management group to another management group, see [Move management groups in the hierarchy](#Move-management-groups-in-the-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="5e178-130">To move a management group to another management group, see [Move management groups in the hierarchy](#Move-management-groups-in-the-hierarchy).</span></span>
2. <span data-ttu-id="5e178-131">You have write permissions on the management group Owner or Contributor role on the management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-131">You have write permissions on the management group Owner or Contributor role on the management group.</span></span> <span data-ttu-id="5e178-132">To see what permissions you have, select the management group and then select **IAM**.</span><span class="sxs-lookup"><span data-stu-id="5e178-132">To see what permissions you have, select the management group and then select **IAM**.</span></span> <span data-ttu-id="5e178-133">To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e178-133">To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span></span>  

### <a name="delete-in-the-portal"></a><span data-ttu-id="5e178-134">Delete in the portal</span><span class="sxs-lookup"><span data-stu-id="5e178-134">Delete in the portal</span></span>

1. <span data-ttu-id="5e178-135">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-135">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-136">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-136">Select **All services** > **Management groups**</span></span>  
3. <span data-ttu-id="5e178-137">Select the management group you would like to delete.</span><span class="sxs-lookup"><span data-stu-id="5e178-137">Select the management group you would like to delete.</span></span>
4. <span data-ttu-id="5e178-138">Select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="5e178-138">Select **Delete**.</span></span>
    - <span data-ttu-id="5e178-139">If the icon is disabled, hovering your mouse selector over the icon shows you the reason.</span><span class="sxs-lookup"><span data-stu-id="5e178-139">If the icon is disabled, hovering your mouse selector over the icon shows you the reason.</span></span>

    ![delete Group](media/management-groups/delete.png)
5. <span data-ttu-id="5e178-141">There's a window that opens confirming you want to delete the management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-141">There's a window that opens confirming you want to delete the management group.</span></span>

    ![delete Group](media/management-groups/delete_confirm.png)
6. <span data-ttu-id="5e178-143">Select **Yes**</span><span class="sxs-lookup"><span data-stu-id="5e178-143">Select **Yes**</span></span>


### <a name="delete-in-powershell"></a><span data-ttu-id="5e178-144">Delete in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e178-144">Delete in PowerShell</span></span>

<span data-ttu-id="5e178-145">Use the **Remove-AzureRmManagementGroup** command within PowerShell to delete management groups.</span><span class="sxs-lookup"><span data-stu-id="5e178-145">Use the **Remove-AzureRmManagementGroup** command within PowerShell to delete management groups.</span></span> 

```azurepowershell-interactive
Remove-AzureRmManagementGroup -GroupName Contoso
```

### <a name="delete-in-azure-cli"></a><span data-ttu-id="5e178-146">Delete in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e178-146">Delete in Azure CLI</span></span>

<span data-ttu-id="5e178-147">With Azure CLI, use the command az account management-group delete.</span><span class="sxs-lookup"><span data-stu-id="5e178-147">With Azure CLI, use the command az account management-group delete.</span></span>

```azurecli-interactive
az account management-group delete --name Contoso
```
---

## <a name="view-management-groups"></a><span data-ttu-id="5e178-148">View management groups</span><span class="sxs-lookup"><span data-stu-id="5e178-148">View management groups</span></span>

<span data-ttu-id="5e178-149">You can view any management group you have a direct or inherited RBAC role on.</span><span class="sxs-lookup"><span data-stu-id="5e178-149">You can view any management group you have a direct or inherited RBAC role on.</span></span>  

### <a name="view-in-the-portal"></a><span data-ttu-id="5e178-150">View in the portal</span><span class="sxs-lookup"><span data-stu-id="5e178-150">View in the portal</span></span>

1. <span data-ttu-id="5e178-151">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-151">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-152">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-152">Select **All services** > **Management groups**</span></span> 
3. <span data-ttu-id="5e178-153">The management group hierarchy page loads where you can explore all the management groups and subscriptions you have access to.</span><span class="sxs-lookup"><span data-stu-id="5e178-153">The management group hierarchy page loads where you can explore all the management groups and subscriptions you have access to.</span></span> <span data-ttu-id="5e178-154">Selecting the group name takes you down a level in the hierarchy.</span><span class="sxs-lookup"><span data-stu-id="5e178-154">Selecting the group name takes you down a level in the hierarchy.</span></span> <span data-ttu-id="5e178-155">The navigation works the same as a file explorer does.</span><span class="sxs-lookup"><span data-stu-id="5e178-155">The navigation works the same as a file explorer does.</span></span> 
    <span data-ttu-id="5e178-156">![Main](media/management-groups/main.png)</span><span class="sxs-lookup"><span data-stu-id="5e178-156">![Main](media/management-groups/main.png)</span></span>
4. <span data-ttu-id="5e178-157">To see the details of the management group, select the **(details)** link next to the title of the management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-157">To see the details of the management group, select the **(details)** link next to the title of the management group.</span></span> <span data-ttu-id="5e178-158">If this link isn't available, you don't have permissions to view that management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-158">If this link isn't available, you don't have permissions to view that management group.</span></span>  

### <a name="view-in-powershell"></a><span data-ttu-id="5e178-159">View in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e178-159">View in PowerShell</span></span>

<span data-ttu-id="5e178-160">You use the Get-AzureRmManagementGroup command to retrieve all groups.</span><span class="sxs-lookup"><span data-stu-id="5e178-160">You use the Get-AzureRmManagementGroup command to retrieve all groups.</span></span>  

```azurepowershell-interactive
Get-AzureRmManagementGroup
```
<span data-ttu-id="5e178-161">For a single management group's information, use the -GroupName parameter</span><span class="sxs-lookup"><span data-stu-id="5e178-161">For a single management group's information, use the -GroupName parameter</span></span>

```azurepowershell-interactive
Get-AzureRmManagementGroup -GroupName Contoso
```

### <a name="view-in-azure-cli"></a><span data-ttu-id="5e178-162">View in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e178-162">View in Azure CLI</span></span>

<span data-ttu-id="5e178-163">You use the list command to retrieve all groups.</span><span class="sxs-lookup"><span data-stu-id="5e178-163">You use the list command to retrieve all groups.</span></span>  

```azurecli-interactive
az account management-group list
```
<span data-ttu-id="5e178-164">For a single management group's information, use the show command</span><span class="sxs-lookup"><span data-stu-id="5e178-164">For a single management group's information, use the show command</span></span>

```azurecli-interactive
az account management-group show --name Contoso
```
---

## <a name="move-subscriptions-in-the-hierarchy"></a><span data-ttu-id="5e178-165">Move subscriptions in the hierarchy</span><span class="sxs-lookup"><span data-stu-id="5e178-165">Move subscriptions in the hierarchy</span></span>

<span data-ttu-id="5e178-166">One reason to create a management group is to bundle subscriptions together.</span><span class="sxs-lookup"><span data-stu-id="5e178-166">One reason to create a management group is to bundle subscriptions together.</span></span> <span data-ttu-id="5e178-167">Only management groups and subscriptions can be made children of another management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-167">Only management groups and subscriptions can be made children of another management group.</span></span> <span data-ttu-id="5e178-168">A subscription that moves to a management group inherits all user access and policies from the parent management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-168">A subscription that moves to a management group inherits all user access and policies from the parent management group.</span></span>

<span data-ttu-id="5e178-169">To move the subscription, there are a couple permissions you must have:</span><span class="sxs-lookup"><span data-stu-id="5e178-169">To move the subscription, there are a couple permissions you must have:</span></span>

- <span data-ttu-id="5e178-170">"Owner" role on the child subscription.</span><span class="sxs-lookup"><span data-stu-id="5e178-170">"Owner" role on the child subscription.</span></span>
- <span data-ttu-id="5e178-171">"Owner" or "Contributor" role on the new parent management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-171">"Owner" or "Contributor" role on the new parent management group.</span></span>
- <span data-ttu-id="5e178-172">"Owner" or "Contributor" role on the old parent management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-172">"Owner" or "Contributor" role on the old parent management group.</span></span>

<span data-ttu-id="5e178-173">To see what permissions you have, select the management group and then select **IAM**.</span><span class="sxs-lookup"><span data-stu-id="5e178-173">To see what permissions you have, select the management group and then select **IAM**.</span></span> <span data-ttu-id="5e178-174">To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e178-174">To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).</span></span>

### <a name="move-subscriptions-in-the-portal"></a><span data-ttu-id="5e178-175">Move subscriptions in the portal</span><span class="sxs-lookup"><span data-stu-id="5e178-175">Move subscriptions in the portal</span></span>

<span data-ttu-id="5e178-176">**Add an existing Subscription to a management group**</span><span class="sxs-lookup"><span data-stu-id="5e178-176">**Add an existing Subscription to a management group**</span></span>

1. <span data-ttu-id="5e178-177">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-177">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-178">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-178">Select **All services** > **Management groups**</span></span>
3. <span data-ttu-id="5e178-179">Select the management group you're planning to be the parent.</span><span class="sxs-lookup"><span data-stu-id="5e178-179">Select the management group you're planning to be the parent.</span></span>
4. <span data-ttu-id="5e178-180">At the top of the page, select **Add subscription**.</span><span class="sxs-lookup"><span data-stu-id="5e178-180">At the top of the page, select **Add subscription**.</span></span>
5. <span data-ttu-id="5e178-181">Select the subscription in the list with the correct ID.</span><span class="sxs-lookup"><span data-stu-id="5e178-181">Select the subscription in the list with the correct ID.</span></span>

    ![Children](media/management-groups/add_context_sub.png)
1. <span data-ttu-id="5e178-183">Select "Save"</span><span class="sxs-lookup"><span data-stu-id="5e178-183">Select "Save"</span></span>

<span data-ttu-id="5e178-184">**Move a subscription to another management group**</span><span class="sxs-lookup"><span data-stu-id="5e178-184">**Move a subscription to another management group**</span></span>

1. <span data-ttu-id="5e178-185">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-185">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-186">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-186">Select **All services** > **Management groups**</span></span> 
3. <span data-ttu-id="5e178-187">Select the management group you're planning that is the current parent.</span><span class="sxs-lookup"><span data-stu-id="5e178-187">Select the management group you're planning that is the current parent.</span></span>  
4. <span data-ttu-id="5e178-188">Select the ellipse at the end of the row for the subscription in the list you want to move.</span><span class="sxs-lookup"><span data-stu-id="5e178-188">Select the ellipse at the end of the row for the subscription in the list you want to move.</span></span>

    ![Move](media/management-groups/move_small.png)
5. <span data-ttu-id="5e178-190">Select **Move**</span><span class="sxs-lookup"><span data-stu-id="5e178-190">Select **Move**</span></span>
6. <span data-ttu-id="5e178-191">On the menu that opens, select the **Parent management group**.</span><span class="sxs-lookup"><span data-stu-id="5e178-191">On the menu that opens, select the **Parent management group**.</span></span>

    ![Move](media/management-groups/move_small_context.png)
7. <span data-ttu-id="5e178-193">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="5e178-193">Select **Save**</span></span>

### <a name="move-subscriptions-in-powershell"></a><span data-ttu-id="5e178-194">Move subscriptions in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e178-194">Move subscriptions in PowerShell</span></span>

<span data-ttu-id="5e178-195">To move a subscription in PowerShell, you use the Add-AzureRmManagementGroupSubscription command.</span><span class="sxs-lookup"><span data-stu-id="5e178-195">To move a subscription in PowerShell, you use the Add-AzureRmManagementGroupSubscription command.</span></span>  

```azurepowershell-interactive
New-AzureRmManagementGroupSubscription -GroupName Contoso -SubscriptionId 12345678-1234-1234-1234-123456789012
```

<span data-ttu-id="5e178-196">To remove the link between and subscription and the management group use the Remove-AzureRmManagementGroupSubscription command.</span><span class="sxs-lookup"><span data-stu-id="5e178-196">To remove the link between and subscription and the management group use the Remove-AzureRmManagementGroupSubscription command.</span></span>

```azurepowershell-interactive
Remove-AzureRmManagementGroupSubscription -GroupName Contoso -SubscriptionId 12345678-1234-1234-1234-123456789012
```

### <a name="move-subscriptions-in-azure-cli"></a><span data-ttu-id="5e178-197">Move subscriptions in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e178-197">Move subscriptions in Azure CLI</span></span>

<span data-ttu-id="5e178-198">To move a subscription in CLI, you use the add command.</span><span class="sxs-lookup"><span data-stu-id="5e178-198">To move a subscription in CLI, you use the add command.</span></span>

```azurecli-interactive
az account management-group subscription add --name Contoso --subscription 12345678-1234-1234-1234-123456789012
```

<span data-ttu-id="5e178-199">To remove the subscription from the management group, use the subscription remove command.</span><span class="sxs-lookup"><span data-stu-id="5e178-199">To remove the subscription from the management group, use the subscription remove command.</span></span>  

```azurecli-interactive
az account management-group subscription remove --name Contoso --subscription 12345678-1234-1234-1234-123456789012
```

---

## <a name="move-management-groups-in-the-hierarchy"></a><span data-ttu-id="5e178-200">Move management groups in the hierarchy</span><span class="sxs-lookup"><span data-stu-id="5e178-200">Move management groups in the hierarchy</span></span>  

<span data-ttu-id="5e178-201">When you move a parent management group, all the child resources that include management groups, subscriptions, resource groups, and resources move with the parent.</span><span class="sxs-lookup"><span data-stu-id="5e178-201">When you move a parent management group, all the child resources that include management groups, subscriptions, resource groups, and resources move with the parent.</span></span>   

### <a name="move-management-groups-in-the-portal"></a><span data-ttu-id="5e178-202">Move management groups in the portal</span><span class="sxs-lookup"><span data-stu-id="5e178-202">Move management groups in the portal</span></span>

1. <span data-ttu-id="5e178-203">Log into the [Azure portal](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5e178-203">Log into the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="5e178-204">Select **All services** > **Management groups**</span><span class="sxs-lookup"><span data-stu-id="5e178-204">Select **All services** > **Management groups**</span></span>
3. <span data-ttu-id="5e178-205">Select the management group you're planning to be the parent.</span><span class="sxs-lookup"><span data-stu-id="5e178-205">Select the management group you're planning to be the parent.</span></span>
5. <span data-ttu-id="5e178-206">At the top of the page, select **Add management group**.</span><span class="sxs-lookup"><span data-stu-id="5e178-206">At the top of the page, select **Add management group**.</span></span>
6. <span data-ttu-id="5e178-207">In the menu that opens, select if you want a new or use an existing management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-207">In the menu that opens, select if you want a new or use an existing management group.</span></span>
    - <span data-ttu-id="5e178-208">Selecting new will create a new management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-208">Selecting new will create a new management group.</span></span>
    - <span data-ttu-id="5e178-209">Selecting an existing will present you with a drop-down of all the management groups you can move to this management group.</span><span class="sxs-lookup"><span data-stu-id="5e178-209">Selecting an existing will present you with a drop-down of all the management groups you can move to this management group.</span></span>  

    ![move](media/management-groups/add_context_MG.png)
7. <span data-ttu-id="5e178-211">Select **Save**</span><span class="sxs-lookup"><span data-stu-id="5e178-211">Select **Save**</span></span>

### <a name="move-management-groups-in-powershell"></a><span data-ttu-id="5e178-212">Move management groups in PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e178-212">Move management groups in PowerShell</span></span>

<span data-ttu-id="5e178-213">Use the Update-AzureRmManagementGroup command in PowerShell to move a management group under a different group.</span><span class="sxs-lookup"><span data-stu-id="5e178-213">Use the Update-AzureRmManagementGroup command in PowerShell to move a management group under a different group.</span></span>  

```powershell
Update-AzureRmManagementGroup -GroupName Contoso  -ParentName ContosoIT
```  

### <a name="move-management-groups-in-azure-cli"></a><span data-ttu-id="5e178-214">Move management groups in Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5e178-214">Move management groups in Azure CLI</span></span>

<span data-ttu-id="5e178-215">Use the update command to move a management group with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5e178-215">Use the update command to move a management group with Azure CLI.</span></span>

```azurecli-interactive
az account management-group update --name Contoso --parent "Contoso Tenant"
```

---

## <a name="next-steps"></a><span data-ttu-id="5e178-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e178-216">Next steps</span></span>

<span data-ttu-id="5e178-217">To Learn more about management groups, see:</span><span class="sxs-lookup"><span data-stu-id="5e178-217">To Learn more about management groups, see:</span></span>

- [<span data-ttu-id="5e178-218">Organize your resources with Azure management groups</span><span class="sxs-lookup"><span data-stu-id="5e178-218">Organize your resources with Azure management groups</span></span>](management-groups-overview.md)
- [<span data-ttu-id="5e178-219">Create management groups to organize Azure resources</span><span class="sxs-lookup"><span data-stu-id="5e178-219">Create management groups to organize Azure resources</span></span>](management-groups-create.md)
- [<span data-ttu-id="5e178-220">Install the Azure Powershell module</span><span class="sxs-lookup"><span data-stu-id="5e178-220">Install the Azure Powershell module</span></span>](https://www.powershellgallery.com/packages/AzureRM.ManagementGroups/0.0.1-preview)
- [<span data-ttu-id="5e178-221">Review the REST API Spec</span><span class="sxs-lookup"><span data-stu-id="5e178-221">Review the REST API Spec</span></span>](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/managementgroups/resource-manager/Microsoft.Management/preview)
- [<span data-ttu-id="5e178-222">Install the Azure CLI Extension</span><span class="sxs-lookup"><span data-stu-id="5e178-222">Install the Azure CLI Extension</span></span>](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-list-available)
