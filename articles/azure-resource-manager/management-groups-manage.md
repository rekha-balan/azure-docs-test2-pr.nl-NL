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
# <a name="manage-your-resources-with-management-groups"></a>Manage your resources with management groups

Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions. You can change, delete, and manage these containers to have hierarchies that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls (RBAC)](../role-based-access-control/overview.md). To learn more about management groups, see [Organize your resources with Azure management groups](management-groups-overview.md).

To make changes to a management group, you must have an Owner or Contributor role on the management group. To see what permissions you have, select the management group and then select **IAM**. To learn more about RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="change-the-name-of-a-management-group"></a>Change the name of a management group

You can change the name of the management group by using the portal, PowerShell, or Azure CLI.

### <a name="change-the-name-in-the-portal"></a>Change the name in the portal

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups**  
3. Select the management group you would like to rename.
4. Select the **Rename group** option at the top of the page.

    ![Rename Group](media/management-groups/detail_action_small.png)
5. When the menu opens, enter the new name you would like to have displayed.

    ![Rename Group](media/management-groups/rename_context.png)
6. Select **Save**.

### <a name="change-the-name-in-powershell"></a>Change the name in PowerShell

To update the display name use **Update-AzureRmManagementGroup**. For example, to change a management groups name from "Contoso IT" to "Contoso Group", you run the following command: 

```azurepowershell-inetractive
C:\> Update-AzureRmManagementGroup -GroupName ContosoIt -DisplayName "Contoso Group"  
``` 

### <a name="change-the-name-in-azure-cli"></a>Change the name in Azure CLI

For Azure CLI, use the update command.

```azurecli-interactive
az account management-group update --name Contoso --display-name "Contoso Group" 
```

---

## <a name="delete-a-management-group"></a>Delete a management group

To delete a management group, the following requirements must be met:

1. There are no child management groups or subscriptions under the management group.
    - To move a subscription out of a management group, see [Move subscription to another management group](#Move-subscriptions-in-the-hierarchy).
    - To move a management group to another management group, see [Move management groups in the hierarchy](#Move-management-groups-in-the-hierarchy).
2. You have write permissions on the management group Owner or Contributor role on the management group. To see what permissions you have, select the management group and then select **IAM**. To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).  

### <a name="delete-in-the-portal"></a>Delete in the portal

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups**  
3. Select the management group you would like to delete.
4. Select **Delete**.
    - If the icon is disabled, hovering your mouse selector over the icon shows you the reason.

    ![delete Group](media/management-groups/delete.png)
5. There's a window that opens confirming you want to delete the management group.

    ![delete Group](media/management-groups/delete_confirm.png)
6. Select **Yes**


### <a name="delete-in-powershell"></a>Delete in PowerShell

Use the **Remove-AzureRmManagementGroup** command within PowerShell to delete management groups. 

```azurepowershell-interactive
Remove-AzureRmManagementGroup -GroupName Contoso
```

### <a name="delete-in-azure-cli"></a>Delete in Azure CLI

With Azure CLI, use the command az account management-group delete.

```azurecli-interactive
az account management-group delete --name Contoso
```
---

## <a name="view-management-groups"></a>View management groups

You can view any management group you have a direct or inherited RBAC role on.  

### <a name="view-in-the-portal"></a>View in the portal

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups** 
3. The management group hierarchy page loads where you can explore all the management groups and subscriptions you have access to. Selecting the group name takes you down a level in the hierarchy. The navigation works the same as a file explorer does. 
    ![Main](media/management-groups/main.png)
4. To see the details of the management group, select the **(details)** link next to the title of the management group. If this link isn't available, you don't have permissions to view that management group.  

### <a name="view-in-powershell"></a>View in PowerShell

You use the Get-AzureRmManagementGroup command to retrieve all groups.  

```azurepowershell-interactive
Get-AzureRmManagementGroup
```
For a single management group's information, use the -GroupName parameter

```azurepowershell-interactive
Get-AzureRmManagementGroup -GroupName Contoso
```

### <a name="view-in-azure-cli"></a>View in Azure CLI

You use the list command to retrieve all groups.  

```azurecli-interactive
az account management-group list
```
For a single management group's information, use the show command

```azurecli-interactive
az account management-group show --name Contoso
```
---

## <a name="move-subscriptions-in-the-hierarchy"></a>Move subscriptions in the hierarchy

One reason to create a management group is to bundle subscriptions together. Only management groups and subscriptions can be made children of another management group. A subscription that moves to a management group inherits all user access and policies from the parent management group.

To move the subscription, there are a couple permissions you must have:

- "Owner" role on the child subscription.
- "Owner" or "Contributor" role on the new parent management group.
- "Owner" or "Contributor" role on the old parent management group.

To see what permissions you have, select the management group and then select **IAM**. To learn more on RBAC Roles, see [Manage access and permissions with RBAC](../role-based-access-control/overview.md).

### <a name="move-subscriptions-in-the-portal"></a>Move subscriptions in the portal

**Add an existing Subscription to a management group**

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups**
3. Select the management group you're planning to be the parent.
4. At the top of the page, select **Add subscription**.
5. Select the subscription in the list with the correct ID.

    ![Children](media/management-groups/add_context_sub.png)
1. Select "Save"

**Move a subscription to another management group**

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups** 
3. Select the management group you're planning that is the current parent.  
4. Select the ellipse at the end of the row for the subscription in the list you want to move.

    ![Move](media/management-groups/move_small.png)
5. Select **Move**
6. On the menu that opens, select the **Parent management group**.

    ![Move](media/management-groups/move_small_context.png)
7. Select **Save**

### <a name="move-subscriptions-in-powershell"></a>Move subscriptions in PowerShell

To move a subscription in PowerShell, you use the Add-AzureRmManagementGroupSubscription command.  

```azurepowershell-interactive
New-AzureRmManagementGroupSubscription -GroupName Contoso -SubscriptionId 12345678-1234-1234-1234-123456789012
```

To remove the link between and subscription and the management group use the Remove-AzureRmManagementGroupSubscription command.

```azurepowershell-interactive
Remove-AzureRmManagementGroupSubscription -GroupName Contoso -SubscriptionId 12345678-1234-1234-1234-123456789012
```

### <a name="move-subscriptions-in-azure-cli"></a>Move subscriptions in Azure CLI

To move a subscription in CLI, you use the add command.

```azurecli-interactive
az account management-group subscription add --name Contoso --subscription 12345678-1234-1234-1234-123456789012
```

To remove the subscription from the management group, use the subscription remove command.  

```azurecli-interactive
az account management-group subscription remove --name Contoso --subscription 12345678-1234-1234-1234-123456789012
```

---

## <a name="move-management-groups-in-the-hierarchy"></a>Move management groups in the hierarchy  

When you move a parent management group, all the child resources that include management groups, subscriptions, resource groups, and resources move with the parent.   

### <a name="move-management-groups-in-the-portal"></a>Move management groups in the portal

1. Log into the [Azure portal](https://portal.azure.com)
2. Select **All services** > **Management groups**
3. Select the management group you're planning to be the parent.
5. At the top of the page, select **Add management group**.
6. In the menu that opens, select if you want a new or use an existing management group.
    - Selecting new will create a new management group.
    - Selecting an existing will present you with a drop-down of all the management groups you can move to this management group.  

    ![move](media/management-groups/add_context_MG.png)
7. Select **Save**

### <a name="move-management-groups-in-powershell"></a>Move management groups in PowerShell

Use the Update-AzureRmManagementGroup command in PowerShell to move a management group under a different group.  

```powershell
Update-AzureRmManagementGroup -GroupName Contoso  -ParentName ContosoIT
```  

### <a name="move-management-groups-in-azure-cli"></a>Move management groups in Azure CLI

Use the update command to move a management group with Azure CLI.

```azurecli-interactive
az account management-group update --name Contoso --parent "Contoso Tenant"
```

---

## <a name="next-steps"></a>Next steps

To Learn more about management groups, see:

- [Organize your resources with Azure management groups](management-groups-overview.md)
- [Create management groups to organize Azure resources](management-groups-create.md)
- [Install the Azure Powershell module](https://www.powershellgallery.com/packages/AzureRM.ManagementGroups/0.0.1-preview)
- [Review the REST API Spec](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/managementgroups/resource-manager/Microsoft.Management/preview)
- [Install the Azure CLI Extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-list-available)
