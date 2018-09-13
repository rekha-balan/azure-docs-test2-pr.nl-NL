---
title: Create custom roles for Azure RBAC | Microsoft Docs
description: Learn how to define custom roles with Azure Role-Based Access Control for more precise identity management in your Azure subscription.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: ''
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/21/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2e4fe247e8331525744bd3f4e60c67c73dd10e71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670311"
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="93c97-103">Create custom roles for Azure Role-Based Access Control</span><span class="sxs-lookup"><span data-stu-id="93c97-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="93c97-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span><span class="sxs-lookup"><span data-stu-id="93c97-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of the built-in roles meet your specific access needs.</span></span> <span data-ttu-id="93c97-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="93c97-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and the [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="93c97-106">Just like built-in roles, custom roles can be assigned to users, groups, and applications at subscription, resource group, and resource scopes.</span><span class="sxs-lookup"><span data-stu-id="93c97-106">Just like built-in roles, custom roles can be assigned to users, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="93c97-107">Custom roles are stored in an Azure AD tenant and can be shared across all subscriptions that use that tenant as the Azure AD directory for the subscription.</span><span class="sxs-lookup"><span data-stu-id="93c97-107">Custom roles are stored in an Azure AD tenant and can be shared across all subscriptions that use that tenant as the Azure AD directory for the subscription.</span></span>

<span data-ttu-id="93c97-108">Each tenant can create up to 2000 custom roles.</span><span class="sxs-lookup"><span data-stu-id="93c97-108">Each tenant can create up to 2000 custom roles.</span></span> 

<span data-ttu-id="93c97-109">The following is an example of a custom role for monitoring and restarting virtual machines:</span><span class="sxs-lookup"><span data-stu-id="93c97-109">The following is an example of a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="93c97-110">Actions</span><span class="sxs-lookup"><span data-stu-id="93c97-110">Actions</span></span>
<span data-ttu-id="93c97-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span><span class="sxs-lookup"><span data-stu-id="93c97-111">The **Actions** property of a custom role specifies the Azure operations to which the role grants access.</span></span> <span data-ttu-id="93c97-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span><span class="sxs-lookup"><span data-stu-id="93c97-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="93c97-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="93c97-113">Operation strings follow the format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="93c97-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span><span class="sxs-lookup"><span data-stu-id="93c97-114">Operation strings that contain wildcards (\*) grant access to all operations that match the operation string.</span></span> <span data-ttu-id="93c97-115">For instance:</span><span class="sxs-lookup"><span data-stu-id="93c97-115">For instance:</span></span>

* <span data-ttu-id="93c97-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span><span class="sxs-lookup"><span data-stu-id="93c97-116">`*/read` grants access to read operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="93c97-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span><span class="sxs-lookup"><span data-stu-id="93c97-117">`Microsoft.Compute/*` grants access to all operations for all resource types in the Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="93c97-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span><span class="sxs-lookup"><span data-stu-id="93c97-118">`Microsoft.Network/*/read` grants access to read operations for all resource types in the Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="93c97-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span><span class="sxs-lookup"><span data-stu-id="93c97-119">`Microsoft.Compute/virtualMachines/*` grants access to all operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="93c97-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span><span class="sxs-lookup"><span data-stu-id="93c97-120">`Microsoft.Web/sites/restart/Action` grants access to restart websites.</span></span>

<span data-ttu-id="93c97-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span><span class="sxs-lookup"><span data-stu-id="93c97-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) to list operations of Azure resource providers.</span></span> <span data-ttu-id="93c97-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span><span class="sxs-lookup"><span data-stu-id="93c97-122">You may also use these commands to verify that an operation string is valid, and to expand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![PowerShell screenshot - Get-AzureRMProviderOperation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="93c97-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span><span class="sxs-lookup"><span data-stu-id="93c97-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="93c97-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="93c97-125">NotActions</span></span>
<span data-ttu-id="93c97-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span><span class="sxs-lookup"><span data-stu-id="93c97-126">Use the **NotActions** property if the set of operations that you wish to allow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="93c97-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span><span class="sxs-lookup"><span data-stu-id="93c97-127">The access granted by a custom role is computed by subtracting the **NotActions** operations from the **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="93c97-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user will be allowed to perform that operation.</span><span class="sxs-lookup"><span data-stu-id="93c97-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access to the same operation, the user will be allowed to perform that operation.</span></span> <span data-ttu-id="93c97-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span><span class="sxs-lookup"><span data-stu-id="93c97-129">**NotActions** is not a deny rule – it is simply a convenient way to create a set of allowed operations when specific operations need to be excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="93c97-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="93c97-130">AssignableScopes</span></span>
<span data-ttu-id="93c97-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span><span class="sxs-lookup"><span data-stu-id="93c97-131">The **AssignableScopes** property of the custom role specifies the scopes (subscriptions, resource groups, or resources) within which the custom role is available for assignment.</span></span> <span data-ttu-id="93c97-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span><span class="sxs-lookup"><span data-stu-id="93c97-132">You can make the custom role available for assignment in only the subscriptions or resource groups that require it, and not clutter user experience for the rest of the subscriptions or resource groups.</span></span>

<span data-ttu-id="93c97-133">Examples of valid assignable scopes include:</span><span class="sxs-lookup"><span data-stu-id="93c97-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="93c97-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span><span class="sxs-lookup"><span data-stu-id="93c97-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes the role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="93c97-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span><span class="sxs-lookup"><span data-stu-id="93c97-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes the role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="93c97-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span><span class="sxs-lookup"><span data-stu-id="93c97-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes the role available for assignment only in the Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="93c97-137">You must use at least one subscription, resource group, or resource ID.</span><span class="sxs-lookup"><span data-stu-id="93c97-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="93c97-138">Custom roles access control</span><span class="sxs-lookup"><span data-stu-id="93c97-138">Custom roles access control</span></span>
<span data-ttu-id="93c97-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span><span class="sxs-lookup"><span data-stu-id="93c97-139">The **AssignableScopes** property of the custom role also controls who can view, modify, and delete the role.</span></span>

* <span data-ttu-id="93c97-140">Who can create a custom role?</span><span class="sxs-lookup"><span data-stu-id="93c97-140">Who can create a custom role?</span></span>
    <span data-ttu-id="93c97-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span><span class="sxs-lookup"><span data-stu-id="93c97-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="93c97-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span><span class="sxs-lookup"><span data-stu-id="93c97-142">The user creating the role needs to be able to perform `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of the role.</span></span>
* <span data-ttu-id="93c97-143">Who can modify a custom role?</span><span class="sxs-lookup"><span data-stu-id="93c97-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="93c97-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span><span class="sxs-lookup"><span data-stu-id="93c97-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="93c97-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span><span class="sxs-lookup"><span data-stu-id="93c97-145">Users need to be able to perform the `Microsoft.Authorization/roleDefinition/write` operation on all the **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="93c97-146">Who can view custom roles?</span><span class="sxs-lookup"><span data-stu-id="93c97-146">Who can view custom roles?</span></span>
    <span data-ttu-id="93c97-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span><span class="sxs-lookup"><span data-stu-id="93c97-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="93c97-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span><span class="sxs-lookup"><span data-stu-id="93c97-148">Users who can perform the `Microsoft.Authorization/roleDefinition/read` operation at a scope can view the RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="93c97-149">See also</span><span class="sxs-lookup"><span data-stu-id="93c97-149">See also</span></span>
* <span data-ttu-id="93c97-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="93c97-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in the Azure portal.</span></span>
* <span data-ttu-id="93c97-151">Learn how to manage access with:</span><span class="sxs-lookup"><span data-stu-id="93c97-151">Learn how to manage access with:</span></span>
  * [<span data-ttu-id="93c97-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="93c97-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="93c97-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="93c97-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="93c97-154">REST API</span><span class="sxs-lookup"><span data-stu-id="93c97-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="93c97-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="93c97-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about the roles that come standard in RBAC.</span></span>


