---
title: Manage Role-Based Access Control (RBAC) with Azure PowerShell | Microsoft Docs
description: How to manage RBAC with Azure PowerShell, including listing roles, assigning roles, and deleting role assignments.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/02/2017
ms.author: kgremban
ms.openlocfilehash: 8b1ea7b21f0e1db8ee060f76ac709646003fdb4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553774"
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="93d2e-103">Manage Role-Based Access Control with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="93d2e-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [PowerShell](role-based-access-control-manage-access-powershell.md)
> * [Azure CLI](role-based-access-control-manage-access-azure-cli.md)
> * [REST API](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="93d2e-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span><span class="sxs-lookup"><span data-stu-id="93d2e-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Management API to manage access to your subscription at a fine-grained level.</span></span> <span data-ttu-id="93d2e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span><span class="sxs-lookup"><span data-stu-id="93d2e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="93d2e-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="93d2e-109">Before you can use PowerShell to manage RBAC, you need the following prerequisites:</span></span>

* <span data-ttu-id="93d2e-110">Azure PowerShell version 0.8.8 or later.</span><span class="sxs-lookup"><span data-stu-id="93d2e-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="93d2e-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="93d2e-111">To install the latest version and associate it with your Azure subscription, see [how to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="93d2e-112">Azure Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="93d2e-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="93d2e-113">Install the [Azure Resource Manager cmdlets](https://msdn.microsoft.com/library/mt125356.aspx) in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="93d2e-113">Install the [Azure Resource Manager cmdlets](https://msdn.microsoft.com/library/mt125356.aspx) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="93d2e-114">List roles</span><span class="sxs-lookup"><span data-stu-id="93d2e-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="93d2e-115">List all available roles</span><span class="sxs-lookup"><span data-stu-id="93d2e-115">List all available roles</span></span>
<span data-ttu-id="93d2e-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="93d2e-116">To list RBAC roles that are available for assignment and to inspect the operations to which they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="93d2e-118">List actions of a role</span><span class="sxs-lookup"><span data-stu-id="93d2e-118">List actions of a role</span></span>
<span data-ttu-id="93d2e-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="93d2e-119">To list the actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell - Get-AzureRmRoleDefinition for a specific role - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="93d2e-121">See who has access</span><span class="sxs-lookup"><span data-stu-id="93d2e-121">See who has access</span></span>
<span data-ttu-id="93d2e-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="93d2e-122">To list RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="93d2e-123">List role assignments at a specific scope</span><span class="sxs-lookup"><span data-stu-id="93d2e-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="93d2e-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="93d2e-124">You can see all the access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="93d2e-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="93d2e-125">For example, to see the all the active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment for a resource group - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-to-a-user"></a><span data-ttu-id="93d2e-127">List roles assigned to a user</span><span class="sxs-lookup"><span data-stu-id="93d2e-127">List roles assigned to a user</span></span>
<span data-ttu-id="93d2e-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="93d2e-128">To list all the roles that are assigned to a specified user and the roles that are assigned to the groups to which the user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment for a user - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="93d2e-130">List classic service administrator and coadmin role assignments</span><span class="sxs-lookup"><span data-stu-id="93d2e-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="93d2e-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-131">To list access assignments for the classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="93d2e-132">Grant access</span><span class="sxs-lookup"><span data-stu-id="93d2e-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="93d2e-133">Search for object IDs</span><span class="sxs-lookup"><span data-stu-id="93d2e-133">Search for object IDs</span></span>
<span data-ttu-id="93d2e-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span><span class="sxs-lookup"><span data-stu-id="93d2e-134">To assign a role, you need to identify both the object (user, group, or application) and the scope.</span></span>

<span data-ttu-id="93d2e-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="93d2e-135">If you don't know the subscription ID, you can find it in the **Subscriptions** blade on the Azure portal.</span></span> <span data-ttu-id="93d2e-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](https://msdn.microsoft.com/library/dn495302.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="93d2e-136">To learn how to query for the subscription ID, see [Get-AzureSubscription](https://msdn.microsoft.com/library/dn495302.aspx) on MSDN.</span></span>

<span data-ttu-id="93d2e-137">To get the object ID for an Azure AD group, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-137">To get the object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="93d2e-138">To get the object ID for an Azure AD service principal or application, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-138">To get the object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="93d2e-139">Assign a role to an application at the subscription scope</span><span class="sxs-lookup"><span data-stu-id="93d2e-139">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="93d2e-140">To grant access to an application at the subscription scope, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-140">To grant access to an application at the subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - New-AzureRmRoleAssignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="93d2e-142">Assign a role to a user at the resource group scope</span><span class="sxs-lookup"><span data-stu-id="93d2e-142">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="93d2e-143">To grant access to a user at the resource group scope, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-143">To grant access to a user at the resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="93d2e-145">Assign a role to a group at the resource scope</span><span class="sxs-lookup"><span data-stu-id="93d2e-145">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="93d2e-146">To grant access to a group at the resource scope, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-146">To grant access to a group at the resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - New-AzureRmRoleAssignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="93d2e-148">Remove access</span><span class="sxs-lookup"><span data-stu-id="93d2e-148">Remove access</span></span>
<span data-ttu-id="93d2e-149">To remove access for users, groups, and applications, use:</span><span class="sxs-lookup"><span data-stu-id="93d2e-149">To remove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell - Remove-AzureRmRoleAssignment - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="93d2e-151">Create a custom role</span><span class="sxs-lookup"><span data-stu-id="93d2e-151">Create a custom role</span></span>
<span data-ttu-id="93d2e-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span><span class="sxs-lookup"><span data-stu-id="93d2e-152">To create a custom role, use the ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="93d2e-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span><span class="sxs-lookup"><span data-stu-id="93d2e-153">There are two methods of structuring the role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-from-particular-resource-provider"></a><span data-ttu-id="93d2e-154">Get Actions from Particular Resource Provider</span><span class="sxs-lookup"><span data-stu-id="93d2e-154">Get Actions from Particular Resource Provider</span></span>
<span data-ttu-id="93d2e-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span><span class="sxs-lookup"><span data-stu-id="93d2e-155">When You are creating custom roles from scratch, it is important to know all the possible operations from the resource providers.</span></span>
<span data-ttu-id="93d2e-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span><span class="sxs-lookup"><span data-stu-id="93d2e-156">Use the ```Get-AzureRMProviderOperation``` command to get this information.</span></span>
<span data-ttu-id="93d2e-157">For example, if you want to check all the available operations for virtual Machine use this command:</span><span class="sxs-lookup"><span data-stu-id="93d2e-157">For example, if you want to check all the available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="93d2e-158">Create role with PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="93d2e-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="93d2e-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span><span class="sxs-lookup"><span data-stu-id="93d2e-159">When you use PowerShell to create a custom role, you can start from scratch or use one of the [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="93d2e-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span><span class="sxs-lookup"><span data-stu-id="93d2e-160">The example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="93d2e-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-161">Edit the attributes to add the *Actions*, *notActions*, or *scopes* that you want, and then save the changes as a new role.</span></span>

<span data-ttu-id="93d2e-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span><span class="sxs-lookup"><span data-stu-id="93d2e-162">The following example starts with the *Virtual Machine Contributor* role and uses that to create a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="93d2e-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span><span class="sxs-lookup"><span data-stu-id="93d2e-163">The new role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="93d2e-164">The custom role can be used in two subscriptions.</span><span class="sxs-lookup"><span data-stu-id="93d2e-164">The custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="93d2e-166">Create role with JSON template</span><span class="sxs-lookup"><span data-stu-id="93d2e-166">Create role with JSON template</span></span>
<span data-ttu-id="93d2e-167">A JSON template can be used as the source definition for the custom role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-167">A JSON template can be used as the source definition for the custom role.</span></span> <span data-ttu-id="93d2e-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span><span class="sxs-lookup"><span data-stu-id="93d2e-168">The following example creates a custom role that allows read access to storage and compute resources, access to support, and adds that role to two subscriptions.</span></span> <span data-ttu-id="93d2e-169">Create a new file `C:\CustomRoles\customrole1.json` with the following content.</span><span class="sxs-lookup"><span data-stu-id="93d2e-169">Create a new file `C:\CustomRoles\customrole1.json` with the following content.</span></span> <span data-ttu-id="93d2e-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span><span class="sxs-lookup"><span data-stu-id="93d2e-170">The Id should be set to `null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="93d2e-171">To add the role to the subscriptions, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="93d2e-171">To add the role to the subscriptions, run the following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="93d2e-172">Modify a custom role</span><span class="sxs-lookup"><span data-stu-id="93d2e-172">Modify a custom role</span></span>
<span data-ttu-id="93d2e-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span><span class="sxs-lookup"><span data-stu-id="93d2e-173">Similar to creating a custom role, you can modify an existing custom role using either the PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="93d2e-174">Modify role with PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="93d2e-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="93d2e-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span><span class="sxs-lookup"><span data-stu-id="93d2e-175">To modify a custom role, first, use the `Get-AzureRmRoleDefinition` command to retrieve the role definition.</span></span> <span data-ttu-id="93d2e-176">Second, make the desired changes to the role definition.</span><span class="sxs-lookup"><span data-stu-id="93d2e-176">Second, make the desired changes to the role definition.</span></span> <span data-ttu-id="93d2e-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span><span class="sxs-lookup"><span data-stu-id="93d2e-177">Finally, use the `Set-AzureRmRoleDefinition` command to save the modified role definition.</span></span>

<span data-ttu-id="93d2e-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-178">The following example adds the `Microsoft.Insights/diagnosticSettings/*` operation to the *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="93d2e-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-180">The following example adds an Azure subscription to the assignable scopes of the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="93d2e-182">Modify role with JSON template</span><span class="sxs-lookup"><span data-stu-id="93d2e-182">Modify role with JSON template</span></span>
<span data-ttu-id="93d2e-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span><span class="sxs-lookup"><span data-stu-id="93d2e-183">Using the previous JSON template, you can easily modify an existing custom role to add or remove Actions.</span></span> <span data-ttu-id="93d2e-184">Update the JSON template and add the read action for networking as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="93d2e-184">Update the JSON template and add the read action for networking as shown in the following example.</span></span> <span data-ttu-id="93d2e-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span><span class="sxs-lookup"><span data-stu-id="93d2e-185">The definitions listed in the template are not cumulatively applied to an existing definition, meaning that the role appears exactly as you specify in the template.</span></span> <span data-ttu-id="93d2e-186">You also need to update the Id field with the ID of the role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-186">You also need to update the Id field with the ID of the role.</span></span> <span data-ttu-id="93d2e-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span><span class="sxs-lookup"><span data-stu-id="93d2e-187">If you aren't sure what this value is, you can use the `Get-AzureRmRoleDefinition` cmdlet to get this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access to Azure storage and compute resources and access to support",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="93d2e-188">To update the existing role, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="93d2e-188">To update the existing role, run the following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="93d2e-189">Delete a custom role</span><span class="sxs-lookup"><span data-stu-id="93d2e-189">Delete a custom role</span></span>
<span data-ttu-id="93d2e-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span><span class="sxs-lookup"><span data-stu-id="93d2e-190">To delete a custom role, use the `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="93d2e-191">The following example removes the *Virtual Machine Operator* custom role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-191">The following example removes the *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="93d2e-193">List custom roles</span><span class="sxs-lookup"><span data-stu-id="93d2e-193">List custom roles</span></span>
<span data-ttu-id="93d2e-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span><span class="sxs-lookup"><span data-stu-id="93d2e-194">To list the roles that are available for assignment at a scope, use the `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="93d2e-195">The following example lists all roles that are available for assignment in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="93d2e-195">The following example lists all roles that are available for assignment in the selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell - Get-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="93d2e-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span><span class="sxs-lookup"><span data-stu-id="93d2e-197">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

![RBAC PowerShell - Get-AzureRmRoleDefinition - screenshot](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="93d2e-199">See also</span><span class="sxs-lookup"><span data-stu-id="93d2e-199">See also</span></span>
* <span data-ttu-id="93d2e-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="93d2e-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>















