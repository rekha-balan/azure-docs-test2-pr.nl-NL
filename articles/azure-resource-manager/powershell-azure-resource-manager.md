---
title: Manage Azure solutions with PowerShell | Microsoft Docs
description: Use Azure PowerShell and Resource Manager to manage your resources.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: tomfitz
ms.openlocfilehash: 407e9a1e4a50b875fa65e61d3e9aae245dd907e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660779"
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="3b6a7-103">Manage resources with Azure PowerShell and Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3b6a7-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [Portal](resource-group-portal.md)
> * [Azure CLI](xplat-cli-azure-resource-manager.md)
> * [Azure PowerShell](powershell-azure-resource-manager.md)
> * [REST API](resource-manager-rest-api.md)
>
>

<span data-ttu-id="3b6a7-108">In this topic, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-108">In this topic, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="3b6a7-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="3b6a7-110">This topic focuses on management tasks.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="3b6a7-111">You will:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-111">You will:</span></span>

1. <span data-ttu-id="3b6a7-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-112">Create a resource group</span></span>
2. <span data-ttu-id="3b6a7-113">Add a resource to the resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="3b6a7-114">Add a tag to the resource</span><span class="sxs-lookup"><span data-stu-id="3b6a7-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="3b6a7-115">Query resources based on names or tag values</span><span class="sxs-lookup"><span data-stu-id="3b6a7-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="3b6a7-116">Apply and remove a lock on the resource</span><span class="sxs-lookup"><span data-stu-id="3b6a7-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="3b6a7-117">Create a Resource Manager template from your resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-117">Create a Resource Manager template from your resource group</span></span>
7. <span data-ttu-id="3b6a7-118">Delete a resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-118">Delete a resource group</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="3b6a7-119">Get started with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b6a7-119">Get started with Azure PowerShell</span></span>

<span data-ttu-id="3b6a7-120">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-120">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="3b6a7-121">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-121">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="3b6a7-122">You can update the version through the same method you used to install it.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-122">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="3b6a7-123">For example, if you used the Web Platform Installer, launch it again and look for an update.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-123">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="3b6a7-124">To check your version of the Azure Resources module, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-124">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="3b6a7-125">This topic was updated for version 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-125">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="3b6a7-126">If you have an earlier version, your experience might not match the steps shown in this topic.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-126">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="3b6a7-127">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/en-us/powershell/resourcemanager/azurerm.resources/v3.3.0/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-127">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/en-us/powershell/resourcemanager/azurerm.resources/v3.3.0/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="3b6a7-128">Log in to your Azure account</span><span class="sxs-lookup"><span data-stu-id="3b6a7-128">Log in to your Azure account</span></span>
<span data-ttu-id="3b6a7-129">Before working on your solution, you must log in to your account.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-129">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="3b6a7-130">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-130">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="3b6a7-131">The cmdlet prompts you for the login credentials for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-131">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="3b6a7-132">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-132">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="3b6a7-133">The cmdlet returns information about your account and the subscription to use for the tasks.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-133">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="3b6a7-134">If you have more than one subscription, you can switch to a different subscription.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-134">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="3b6a7-135">First, let's see all the subscriptions for your account.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-135">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="3b6a7-136">It returns enabled and disabled subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-136">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="3b6a7-137">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-137">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="3b6a7-138">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-138">Create a resource group</span></span>
<span data-ttu-id="3b6a7-139">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-139">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="3b6a7-140">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-140">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="3b6a7-141">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-141">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="3b6a7-142">The output is in the following format:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-142">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="3b6a7-143">If you need to retrieve the resource group later, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-143">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="3b6a7-144">To get all the resource groups in your subscription, do not specify a name:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-144">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="3b6a7-145">Add resources to a resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-145">Add resources to a resource group</span></span>
<span data-ttu-id="3b6a7-146">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-146">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="3b6a7-147">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-147">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="3b6a7-148">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-148">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="3b6a7-149">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-149">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="3b6a7-150">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-150">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="3b6a7-151">Templates enable you to reliably and repeatedly deploy your solution.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-151">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="3b6a7-152">This topic does not show how to deploy a Resource Manager template to your subscription.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-152">This topic does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="3b6a7-153">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-153">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span> <span data-ttu-id="3b6a7-154">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-154">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="3b6a7-155">The following cmdlet creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-155">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="3b6a7-156">Instead of using the name shown in the example, provide a unique name for the storage account.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-156">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="3b6a7-157">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-157">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="3b6a7-158">If you use the name shown in the example, you receive an error because that name is already in use.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-158">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="3b6a7-159">If you need to retrieve this resource later, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-159">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="3b6a7-160">Add a tag</span><span class="sxs-lookup"><span data-stu-id="3b6a7-160">Add a tag</span></span>

<span data-ttu-id="3b6a7-161">Tags enable you to organize your resources according to different properties.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-161">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="3b6a7-162">For example, you may have several resources in different resource groups that belong to the same department.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-162">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="3b6a7-163">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-163">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="3b6a7-164">Or, you can mark whether a resource is used in a production or test environment.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-164">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="3b6a7-165">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-165">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="3b6a7-166">The following cmdlet applies two tags to your storage account:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-166">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="3b6a7-167">Tags are updated as a single object.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-167">Tags are updated as a single object.</span></span> <span data-ttu-id="3b6a7-168">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-168">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="3b6a7-169">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-169">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="3b6a7-170">Search for resources</span><span class="sxs-lookup"><span data-stu-id="3b6a7-170">Search for resources</span></span>

<span data-ttu-id="3b6a7-171">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-171">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="3b6a7-172">To get a resource by name, provide the **ResourceNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-172">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="3b6a7-173">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-173">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="3b6a7-174">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-174">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="3b6a7-175">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-175">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="3b6a7-176">Lock a resource</span><span class="sxs-lookup"><span data-stu-id="3b6a7-176">Lock a resource</span></span>

<span data-ttu-id="3b6a7-177">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-177">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="3b6a7-178">You can specify either a **CanNotDelete** or **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-178">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="3b6a7-179">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-179">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="3b6a7-180">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-180">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="3b6a7-181">To apply a lock, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-181">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="3b6a7-182">The locked resource in the preceding example cannot be deleted until the lock is removed.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-182">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="3b6a7-183">To remove a lock, use:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-183">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="3b6a7-184">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-184">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="export-resource-manager-template"></a><span data-ttu-id="3b6a7-185">Export Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="3b6a7-185">Export Resource Manager template</span></span>
<span data-ttu-id="3b6a7-186">For an existing resource group (deployed through PowerShell or one of the other methods like the portal), you can view the Resource Manager template for the resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-186">For an existing resource group (deployed through PowerShell or one of the other methods like the portal), you can view the Resource Manager template for the resource group.</span></span> <span data-ttu-id="3b6a7-187">Exporting the template offers two benefits:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-187">Exporting the template offers two benefits:</span></span>

1. <span data-ttu-id="3b6a7-188">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-188">You can easily automate future deployments of the solution because all the infrastructure is defined in the template.</span></span>
2. <span data-ttu-id="3b6a7-189">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-189">You can become familiar with template syntax by looking at the JavaScript Object Notation (JSON) that represents your solution.</span></span>

> [!NOTE]
> The export template feature is in preview, and not all resource types currently support exporting a template. When attempting to export a template, you may see an error that states some resources were not exported. If needed, you can manually define these resources in your template after downloading it.
>
>

<span data-ttu-id="3b6a7-193">To view the template for a resource group, run the **Export-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-193">To view the template for a resource group, run the **Export-AzureRmResourceGroup** cmdlet.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName TestRG1 -Path c:\Azure\Templates\Downloads\TestRG1.json
```

<span data-ttu-id="3b6a7-194">There are many options and scenarios for exporting a Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-194">There are many options and scenarios for exporting a Resource Manager template.</span></span> <span data-ttu-id="3b6a7-195">For more information, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-195">For more information, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="3b6a7-196">Remove resources or resource group</span><span class="sxs-lookup"><span data-stu-id="3b6a7-196">Remove resources or resource group</span></span>
<span data-ttu-id="3b6a7-197">You can remove a resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-197">You can remove a resource or resource group.</span></span> <span data-ttu-id="3b6a7-198">When you remove a resource group, you also remove all the resources within that resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-198">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="3b6a7-199">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-199">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="3b6a7-200">This cmdlet deletes the resource, but does not delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-200">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="3b6a7-201">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-201">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="3b6a7-202">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-202">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="3b6a7-203">If the operation successfully deletes the resource or resource group, it returns **True**.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-203">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="3b6a7-204">Run Resource Manager scripts with Azure Automation</span><span class="sxs-lookup"><span data-stu-id="3b6a7-204">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="3b6a7-205">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-205">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="3b6a7-206">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-206">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="3b6a7-207">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-207">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="3b6a7-208">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span><span class="sxs-lookup"><span data-stu-id="3b6a7-208">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="3b6a7-209">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-209">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="3b6a7-210">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-210">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="3b6a7-211">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-211">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="3b6a7-212">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-212">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b6a7-213">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3b6a7-213">Next Steps</span></span>
* <span data-ttu-id="3b6a7-214">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-214">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3b6a7-215">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-215">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="3b6a7-216">You can move existing resources to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="3b6a7-216">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="3b6a7-217">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-217">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="3b6a7-218">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="3b6a7-218">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

