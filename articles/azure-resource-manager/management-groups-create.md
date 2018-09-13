---
title: Create management groups to organize Azure resources  | Microsoft Docs
description: Learn how to create Azure management groups to manage multiple resources.
author: rthorn17
manager: rithorn
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2018
ms.author: rithorn
ms.openlocfilehash: 114c3c03b49468b6130243bbf9f881a5de42740f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864785"
---
# <a name="create-management-groups-for-resource-organization-and-management"></a>Create management groups for resource organization and management

Management groups are containers that help you manage access, policy, and compliance across multiple subscriptions. Create these containers to build an effective and efficient hierarchy that can be used with [Azure Policy](../azure-policy/azure-policy-introduction.md) and [Azure Role Based Access Controls](../role-based-access-control/overview.md). For more information on management groups, see [Organize your resources with Azure management groups ](management-groups-overview.md).

The first management group created in the directory could take up to 15 minutes to complete. There are processes that run the first time to set up the management groups service within Azure for your directory. You receive a notification when the process is complete.  

## <a name="create-a-management-group"></a>Create a management group

You can create the management group by using the portal, PowerShell, or Azure CLI. Currently, you can't use Resource Manager templates to create management groups.

### <a name="create-in-portal"></a>Create in portal

1. Log into the [Azure portal](http://portal.azure.com).
2. Select **All services** > **Management groups**.
3. On the main page, select **New Management group.**

    ![Main Group](media/management-groups/main.png)
4.  Fill in the management group ID field.
    - The **Management Group ID** is the directory unique identifier that is used to submit commands on this management group. This identifier is not editable after creation as it is used throughout the Azure system to identify this group.
    - The display name field is the name that is displayed within the Azure portal. A separate display name is an optional field when creating the management group and can be changed at any time.  

    ![Create](media/management-groups/create_context_menu.png)  
5.  Select **Save**

### <a name="create-in-powershell"></a>Create in PowerShell

Within PowerShell, you use the Add-AzureRmManagementGroups cmdlets:

```azurepowershell-interactive
C:\> New-AzureRmManagementGroup -GroupName Contoso
```

The **GroupName** is a unique identifier being created. This ID is used by other commands to reference this group and it cannot be changed later.

If you wanted the management group to show a different name within the Azure portal, you would add the **DisplayName** parameter with the string. For example, if you wanted to create a management group with the GroupName of Contoso and the display name of "Contoso Group", you would use the following cmdlet:

```azurepowershell-interactive
C:\> New-AzureRmManagementGroup -GroupName Contoso -DisplayName "Contoso Group" -ParentId ContosoTenant
```

Use the **ParentId** parameter to have this management group be created under a different management.  

### <a name="create-in-azure-cli"></a>Create in Azure CLI

On Azure CLI, you use the az account management-group create command.

```azure-cli
C:\ az account management-group create --group-name <YourGroupName>
```

---

## <a name="next-steps"></a>Next steps 
To Learn more about management groups, see: 
- [Organize your resources with Azure management groups ](management-groups-overview.md)
- [How to change, delete, or manage your management groups](management-groups-manage.md)
- [Install the Azure Powershell module](https://www.powershellgallery.com/packages/AzureRM.ManagementGroups/0.0.1-preview)
- [Review the REST API Spec](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/managementgroups/resource-manager/Microsoft.Management/preview)
- [Install the Azure CLI Extension](https://docs.microsoft.com/cli/azure/extension?view=azure-cli-latest#az-extension-list-available)
