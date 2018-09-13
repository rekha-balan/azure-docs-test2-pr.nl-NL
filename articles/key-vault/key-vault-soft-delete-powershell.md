---
ms.assetid: ''
title: Azure Key Vault - How to use soft-delete with PowerShell
description: Use case examples of soft-delete with PowerShell code snips
services: key-vault
author: bryanla
manager: mbaldwin
ms.service: key-vault
ms.topic: conceptual
ms.workload: identity
ms.date: 08/21/2017
ms.author: bryanla
ms.openlocfilehash: 93105210267ebadf4273db56e2e147b1b34485e3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864815"
---
# <a name="how-to-use-key-vault-soft-delete-with-powershell"></a><span data-ttu-id="63cd9-103">How to use Key Vault soft-delete with PowerShell</span><span class="sxs-lookup"><span data-stu-id="63cd9-103">How to use Key Vault soft-delete with PowerShell</span></span>

<span data-ttu-id="63cd9-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span><span class="sxs-lookup"><span data-stu-id="63cd9-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="63cd9-105">Specifically, soft-delete addresses the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="63cd9-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="63cd9-106">Support for recoverable deletion of a key vault</span><span class="sxs-lookup"><span data-stu-id="63cd9-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="63cd9-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span><span class="sxs-lookup"><span data-stu-id="63cd9-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63cd9-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="63cd9-108">Prerequisites</span></span>

- <span data-ttu-id="63cd9-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="63cd9-109">Azure PowerShell 4.0.0 or later - If you don't have this already setup, install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span> 

>[!NOTE]
> <span data-ttu-id="63cd9-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span><span class="sxs-lookup"><span data-stu-id="63cd9-110">There is an outdated version of our Key Vault PowerShell output formatting file that **may** be loaded into your environment instead of the correct version.</span></span> <span data-ttu-id="63cd9-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span><span class="sxs-lookup"><span data-stu-id="63cd9-111">We are anticipating an updated version of PowerShell to contain the needed correction for the output formatting and will update this topic at that time.</span></span> <span data-ttu-id="63cd9-112">The current workaround, should you encounter this formatting problem, is:</span><span class="sxs-lookup"><span data-stu-id="63cd9-112">The current workaround, should you encounter this formatting problem, is:</span></span>
> - <span data-ttu-id="63cd9-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span><span class="sxs-lookup"><span data-stu-id="63cd9-113">Use the following query if you notice you're not seeing the soft-delete enabled property described in this topic: `$vault = Get-AzureRmKeyVault -VaultName myvault; $vault.EnableSoftDelete`.</span></span>


<span data-ttu-id="63cd9-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="63cd9-114">For Key Vault specific refernece information for PowerShell, see [Azure Key Vault PowerShell reference](https://docs.microsoft.com/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="63cd9-115">Required permissions</span><span class="sxs-lookup"><span data-stu-id="63cd9-115">Required permissions</span></span>

<span data-ttu-id="63cd9-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span><span class="sxs-lookup"><span data-stu-id="63cd9-116">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="63cd9-117">Operation</span><span class="sxs-lookup"><span data-stu-id="63cd9-117">Operation</span></span> | <span data-ttu-id="63cd9-118">Description</span><span class="sxs-lookup"><span data-stu-id="63cd9-118">Description</span></span> | <span data-ttu-id="63cd9-119">User permission</span><span class="sxs-lookup"><span data-stu-id="63cd9-119">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="63cd9-120">List</span><span class="sxs-lookup"><span data-stu-id="63cd9-120">List</span></span>|<span data-ttu-id="63cd9-121">Lists deleted key vaults.</span><span class="sxs-lookup"><span data-stu-id="63cd9-121">Lists deleted key vaults.</span></span>|<span data-ttu-id="63cd9-122">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="63cd9-122">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="63cd9-123">Recover</span><span class="sxs-lookup"><span data-stu-id="63cd9-123">Recover</span></span>|<span data-ttu-id="63cd9-124">Restores a deleted key vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-124">Restores a deleted key vault.</span></span>|<span data-ttu-id="63cd9-125">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="63cd9-125">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="63cd9-126">Purge</span><span class="sxs-lookup"><span data-stu-id="63cd9-126">Purge</span></span>|<span data-ttu-id="63cd9-127">Permanently removes a deleted key vault and all its contents.</span><span class="sxs-lookup"><span data-stu-id="63cd9-127">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="63cd9-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="63cd9-128">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="63cd9-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="63cd9-129">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="63cd9-130">Enabling soft-delete</span><span class="sxs-lookup"><span data-stu-id="63cd9-130">Enabling soft-delete</span></span>

<span data-ttu-id="63cd9-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-131">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="63cd9-132">Existing key vault</span><span class="sxs-lookup"><span data-stu-id="63cd9-132">Existing key vault</span></span>

<span data-ttu-id="63cd9-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span><span class="sxs-lookup"><span data-stu-id="63cd9-133">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="63cd9-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span><span class="sxs-lookup"><span data-stu-id="63cd9-134">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```powershell
($resource = Get-AzureRmResource -ResourceId (Get-AzureRmKeyVault -VaultName "ContosoVault").ResourceId).Properties | Add-Member -MemberType "NoteProperty" -Name "enableSoftDelete" -Value "true"

Set-AzureRmResource -resourceid $resource.ResourceId -Properties $resource.Properties
```

### <a name="new-key-vault"></a><span data-ttu-id="63cd9-135">New key vault</span><span class="sxs-lookup"><span data-stu-id="63cd9-135">New key vault</span></span>

<span data-ttu-id="63cd9-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span><span class="sxs-lookup"><span data-stu-id="63cd9-136">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```powershell
New-AzureRmKeyVault -VaultName "ContosoVault" -ResourceGroupName "ContosoRG" -Location "westus" -EnableSoftDelete
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="63cd9-137">Verify soft-delete enablement</span><span class="sxs-lookup"><span data-stu-id="63cd9-137">Verify soft-delete enablement</span></span>

<span data-ttu-id="63cd9-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span><span class="sxs-lookup"><span data-stu-id="63cd9-138">To verify that a key vault has soft-delete enabled, run the *get* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="63cd9-139">attribute and its setting, true or false.</span><span class="sxs-lookup"><span data-stu-id="63cd9-139">attribute and its setting, true or false.</span></span>

```powershell
Get-AzureRmKeyVault -VaultName "ContosoVault"
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="63cd9-140">Deleting a key vault protected by soft-delete</span><span class="sxs-lookup"><span data-stu-id="63cd9-140">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="63cd9-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span><span class="sxs-lookup"><span data-stu-id="63cd9-141">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName 'ContosoVault'
```

> [!IMPORTANT]
><span data-ttu-id="63cd9-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span><span class="sxs-lookup"><span data-stu-id="63cd9-142">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="63cd9-143">How soft-delete protects your key vaults</span><span class="sxs-lookup"><span data-stu-id="63cd9-143">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="63cd9-144">With soft-delete enabled:</span><span class="sxs-lookup"><span data-stu-id="63cd9-144">With soft-delete enabled:</span></span>

- <span data-ttu-id="63cd9-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span><span class="sxs-lookup"><span data-stu-id="63cd9-145">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="63cd9-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span><span class="sxs-lookup"><span data-stu-id="63cd9-146">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="63cd9-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span><span class="sxs-lookup"><span data-stu-id="63cd9-147">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="63cd9-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span><span class="sxs-lookup"><span data-stu-id="63cd9-148">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```powershell
PS C:\> Get-AzureRmKeyVault -InRemovedStateVault 

Name           : ContosoVault
Location             : westus
Id                   : /subscriptions/xxx/providers/Microsoft.KeyVault/locations/westus/deletedVaults/ContosoVault
Resource ID          : /subscriptions/xxx/resourceGroups/ContosoVault/providers/Microsoft.KeyVault/vaults/ContosoVault
Deletion Date        : 5/9/2017 12:14:14 AM
Scheduled Purge Date : 8/7/2017 12:14:14 AM
Tags                 :
```

<span data-ttu-id="63cd9-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-149">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="63cd9-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span><span class="sxs-lookup"><span data-stu-id="63cd9-150">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="63cd9-151">The *Id* field can be used to identify the resource when recovering, or purging.</span><span class="sxs-lookup"><span data-stu-id="63cd9-151">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="63cd9-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-152">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="63cd9-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span><span class="sxs-lookup"><span data-stu-id="63cd9-153">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="63cd9-154">Recovering a key vault</span><span class="sxs-lookup"><span data-stu-id="63cd9-154">Recovering a key vault</span></span>

<span data-ttu-id="63cd9-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span><span class="sxs-lookup"><span data-stu-id="63cd9-155">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="63cd9-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span><span class="sxs-lookup"><span data-stu-id="63cd9-156">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```powershell
Undo-AzureRmKeyVaultRemoval -VaultName ContosoVault -ResourceGroupName ContosoRG -Location westus
```

<span data-ttu-id="63cd9-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span><span class="sxs-lookup"><span data-stu-id="63cd9-157">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="63cd9-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span><span class="sxs-lookup"><span data-stu-id="63cd9-158">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="63cd9-159">Key Vault objects and soft-delete</span><span class="sxs-lookup"><span data-stu-id="63cd9-159">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="63cd9-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span><span class="sxs-lookup"><span data-stu-id="63cd9-160">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="63cd9-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span><span class="sxs-lookup"><span data-stu-id="63cd9-161">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="63cd9-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span><span class="sxs-lookup"><span data-stu-id="63cd9-162">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="63cd9-163">For example, to request to list deleted keys in a key vault, use the following command:</span><span class="sxs-lookup"><span data-stu-id="63cd9-163">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```powershell
Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
```

### <a name="transition-state"></a><span data-ttu-id="63cd9-164">Transition state</span><span class="sxs-lookup"><span data-stu-id="63cd9-164">Transition state</span></span> 

<span data-ttu-id="63cd9-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span><span class="sxs-lookup"><span data-stu-id="63cd9-165">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="63cd9-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span><span class="sxs-lookup"><span data-stu-id="63cd9-166">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="63cd9-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="63cd9-167">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```powershell
  Get-AzureKeyVaultKey -VaultName ContosoVault -InRemovedState
  Vault Name           : ContosoVault
  Name                 : ContosoFirstKey
  Id                   : https://ContosoVault.vault.azure.net:443/keys/ContosoFirstKey
  Deleted Date         : 2/14/2017 8:20:52 PM
  Scheduled Purge Date : 5/15/2017 8:20:52 PM
  Enabled              : True
  Expires              :
  Not Before           :
  Created              : 2/14/2017 8:16:07 PM
  Updated              : 2/14/2017 8:16:07 PM
  Tags                 :
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="63cd9-168">Using soft-delete with key vault objects</span><span class="sxs-lookup"><span data-stu-id="63cd9-168">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="63cd9-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span><span class="sxs-lookup"><span data-stu-id="63cd9-169">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="63cd9-170">Keys</span><span class="sxs-lookup"><span data-stu-id="63cd9-170">Keys</span></span>

<span data-ttu-id="63cd9-171">To recover a deleted key:</span><span class="sxs-lookup"><span data-stu-id="63cd9-171">To recover a deleted key:</span></span>

```powershell
Undo-AzureKeyVaultKeyRemoval -VaultName ContosoVault -Name ContosoFirstKey
```

<span data-ttu-id="63cd9-172">To permanently delete a key:</span><span class="sxs-lookup"><span data-stu-id="63cd9-172">To permanently delete a key:</span></span>

```powershell
Remove-AzureKeyVaultKey -VaultName ContosoVault -Name ContosoFirstKey -InRemovedState
```

>[!NOTE]
><span data-ttu-id="63cd9-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="63cd9-173">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="63cd9-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span><span class="sxs-lookup"><span data-stu-id="63cd9-174">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="63cd9-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span><span class="sxs-lookup"><span data-stu-id="63cd9-175">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="63cd9-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span><span class="sxs-lookup"><span data-stu-id="63cd9-176">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="63cd9-177">You must explicitly grant **purge** permission.</span><span class="sxs-lookup"><span data-stu-id="63cd9-177">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="63cd9-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span><span class="sxs-lookup"><span data-stu-id="63cd9-178">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="63cd9-179">Set a key vault access policy</span><span class="sxs-lookup"><span data-stu-id="63cd9-179">Set a key vault access policy</span></span>

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -UserPrincipalName user@contoso.com -PermissionsToKeys get,create,delete,list,update,import,backup,restore,recover,purge
```

>[!NOTE] 
> <span data-ttu-id="63cd9-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span><span class="sxs-lookup"><span data-stu-id="63cd9-180">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="63cd9-181">Secrets</span><span class="sxs-lookup"><span data-stu-id="63cd9-181">Secrets</span></span>

<span data-ttu-id="63cd9-182">Like keys, secrets in a key vault are operated on with their own commands.</span><span class="sxs-lookup"><span data-stu-id="63cd9-182">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="63cd9-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span><span class="sxs-lookup"><span data-stu-id="63cd9-183">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="63cd9-184">Delete a secret named SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="63cd9-184">Delete a secret named SQLPassword:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -name SQLPassword
```

- <span data-ttu-id="63cd9-185">List all deleted secrets in a key vault:</span><span class="sxs-lookup"><span data-stu-id="63cd9-185">List all deleted secrets in a key vault:</span></span> 
```powershell
Get-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState
```

- <span data-ttu-id="63cd9-186">Recover a secret in the deleted state:</span><span class="sxs-lookup"><span data-stu-id="63cd9-186">Recover a secret in the deleted state:</span></span> 
```powershell
Undo-AzureKeyVaultSecretRemoval -VaultName ContosoVault -Name SQLPAssword
```

- <span data-ttu-id="63cd9-187">Purge a secret in deleted state:</span><span class="sxs-lookup"><span data-stu-id="63cd9-187">Purge a secret in deleted state:</span></span> 
```powershell
Remove-AzureKeyVaultSecret -VaultName ContosoVault -InRemovedState -name SQLPassword
```

>[!NOTE]
><span data-ttu-id="63cd9-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="63cd9-188">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="63cd9-189">Purging and key vaults</span><span class="sxs-lookup"><span data-stu-id="63cd9-189">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="63cd9-190">Key vault objects</span><span class="sxs-lookup"><span data-stu-id="63cd9-190">Key vault objects</span></span>

<span data-ttu-id="63cd9-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="63cd9-191">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="63cd9-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-192">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="63cd9-193">Key vaults as containers</span><span class="sxs-lookup"><span data-stu-id="63cd9-193">Key vaults as containers</span></span>
<span data-ttu-id="63cd9-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="63cd9-194">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="63cd9-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span><span class="sxs-lookup"><span data-stu-id="63cd9-195">To purge a key vault, use the `Remove-AzureRmKeyVault` command with the option `-InRemovedState` and by specifying the location of the deleted key vault with the `-Location location` argument.</span></span> <span data-ttu-id="63cd9-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span><span class="sxs-lookup"><span data-stu-id="63cd9-196">You can find the location of a deleted vault using the command `Get-AzureRmKeyVault -InRemovedState`.</span></span>

```powershell
Remove-AzureRmKeyVault -VaultName ContosoVault -InRemovedState -Location westus
```

>[!NOTE]
><span data-ttu-id="63cd9-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="63cd9-197">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="63cd9-198">Purge permissions required</span><span class="sxs-lookup"><span data-stu-id="63cd9-198">Purge permissions required</span></span>
- <span data-ttu-id="63cd9-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span><span class="sxs-lookup"><span data-stu-id="63cd9-199">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="63cd9-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span><span class="sxs-lookup"><span data-stu-id="63cd9-200">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="63cd9-201">By default only a subscription administrator has these permissions.</span><span class="sxs-lookup"><span data-stu-id="63cd9-201">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="63cd9-202">Scheduled purge</span><span class="sxs-lookup"><span data-stu-id="63cd9-202">Scheduled purge</span></span>

<span data-ttu-id="63cd9-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span><span class="sxs-lookup"><span data-stu-id="63cd9-203">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="63cd9-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span><span class="sxs-lookup"><span data-stu-id="63cd9-204">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="63cd9-205">By default, the retention period for a deleted key vault object is 90 days.</span><span class="sxs-lookup"><span data-stu-id="63cd9-205">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="63cd9-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="63cd9-206">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="63cd9-207">It is not recoverable.</span><span class="sxs-lookup"><span data-stu-id="63cd9-207">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="63cd9-208">Other resources</span><span class="sxs-lookup"><span data-stu-id="63cd9-208">Other resources</span></span>

- <span data-ttu-id="63cd9-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="63cd9-209">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="63cd9-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="63cd9-210">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

