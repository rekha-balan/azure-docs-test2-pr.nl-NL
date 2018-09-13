---
ms.assetid: ''
title: Azure Key Vault - How to use soft delete with CLI
description: Use case examples of soft-delete with CLI code snips
author: bryanla
manager: mbaldwin
ms.service: key-vault
ms.topic: conceptual
ms.workload: identity
ms.date: 08/04/2017
ms.author: bryanla
ms.openlocfilehash: 0554e2e184ce3f3140d3b9e90eb33c20774ed789
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870581"
---
# <a name="how-to-use-key-vault-soft-delete-with-cli"></a><span data-ttu-id="96494-103">How to use Key Vault soft-delete with CLI</span><span class="sxs-lookup"><span data-stu-id="96494-103">How to use Key Vault soft-delete with CLI</span></span>

<span data-ttu-id="96494-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span><span class="sxs-lookup"><span data-stu-id="96494-104">Azure Key Vault's soft delete feature allows recovery of deleted vaults and vault objects.</span></span> <span data-ttu-id="96494-105">Specifically, soft-delete addresses the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="96494-105">Specifically, soft-delete addresses the following scenarios:</span></span>

- <span data-ttu-id="96494-106">Support for recoverable deletion of a key vault</span><span class="sxs-lookup"><span data-stu-id="96494-106">Support for recoverable deletion of a key vault</span></span>
- <span data-ttu-id="96494-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span><span class="sxs-lookup"><span data-stu-id="96494-107">Support for recoverable deletion of key vault objects; keys, secrets, and, certificates</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96494-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="96494-108">Prerequisites</span></span>

- <span data-ttu-id="96494-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span><span class="sxs-lookup"><span data-stu-id="96494-109">Azure CLI 2.0 - If you don't have this setup for your environment, see [Manage Key Vault using CLI 2.0](key-vault-manage-with-cli2.md).</span></span>

<span data-ttu-id="96494-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span><span class="sxs-lookup"><span data-stu-id="96494-110">For Key Vault specific reference information for CLI, see [Azure CLI 2.0 Key Vault reference](https://docs.microsoft.com/cli/azure/keyvault).</span></span>

## <a name="required-permissions"></a><span data-ttu-id="96494-111">Required permissions</span><span class="sxs-lookup"><span data-stu-id="96494-111">Required permissions</span></span>

<span data-ttu-id="96494-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span><span class="sxs-lookup"><span data-stu-id="96494-112">Key Vault operations are separately managed via role-based access control (RBAC) permissions as follows:</span></span>

| <span data-ttu-id="96494-113">Operation</span><span class="sxs-lookup"><span data-stu-id="96494-113">Operation</span></span> | <span data-ttu-id="96494-114">Description</span><span class="sxs-lookup"><span data-stu-id="96494-114">Description</span></span> | <span data-ttu-id="96494-115">User permission</span><span class="sxs-lookup"><span data-stu-id="96494-115">User permission</span></span> |
|:--|:--|:--|
|<span data-ttu-id="96494-116">List</span><span class="sxs-lookup"><span data-stu-id="96494-116">List</span></span>|<span data-ttu-id="96494-117">Lists deleted key vaults.</span><span class="sxs-lookup"><span data-stu-id="96494-117">Lists deleted key vaults.</span></span>|<span data-ttu-id="96494-118">Microsoft.KeyVault/deletedVaults/read</span><span class="sxs-lookup"><span data-stu-id="96494-118">Microsoft.KeyVault/deletedVaults/read</span></span>|
|<span data-ttu-id="96494-119">Recover</span><span class="sxs-lookup"><span data-stu-id="96494-119">Recover</span></span>|<span data-ttu-id="96494-120">Restores a deleted key vault.</span><span class="sxs-lookup"><span data-stu-id="96494-120">Restores a deleted key vault.</span></span>|<span data-ttu-id="96494-121">Microsoft.KeyVault/vaults/write</span><span class="sxs-lookup"><span data-stu-id="96494-121">Microsoft.KeyVault/vaults/write</span></span>|
|<span data-ttu-id="96494-122">Purge</span><span class="sxs-lookup"><span data-stu-id="96494-122">Purge</span></span>|<span data-ttu-id="96494-123">Permanently removes a deleted key vault and all its contents.</span><span class="sxs-lookup"><span data-stu-id="96494-123">Permanently removes a deleted key vault and all its contents.</span></span>|<span data-ttu-id="96494-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span><span class="sxs-lookup"><span data-stu-id="96494-124">Microsoft.KeyVault/locations/deletedVaults/purge/action</span></span>|

<span data-ttu-id="96494-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="96494-125">For more information on permissions and access control, see [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

## <a name="enabling-soft-delete"></a><span data-ttu-id="96494-126">Enabling soft-delete</span><span class="sxs-lookup"><span data-stu-id="96494-126">Enabling soft-delete</span></span>

<span data-ttu-id="96494-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span><span class="sxs-lookup"><span data-stu-id="96494-127">To be able to recover a deleted key vault or objects stored in a key vault, you must first enable soft-delete for that key vault.</span></span>

### <a name="existing-key-vault"></a><span data-ttu-id="96494-128">Existing key vault</span><span class="sxs-lookup"><span data-stu-id="96494-128">Existing key vault</span></span>

<span data-ttu-id="96494-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span><span class="sxs-lookup"><span data-stu-id="96494-129">For an existing key vault named ContosoVault, enable soft-delete as follows.</span></span> 

>[!NOTE]
><span data-ttu-id="96494-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span><span class="sxs-lookup"><span data-stu-id="96494-130">Currently you need to use Azure Resource Manager resource manipulation to directly write the *enableSoftDelete* property to the Key Vault resource.</span></span>

```azurecli
az resource update --id $(az keyvault show --name ContosoVault -o tsv | awk '{print $1}') --set properties.enableSoftDelete=true
```

### <a name="new-key-vault"></a><span data-ttu-id="96494-131">New key vault</span><span class="sxs-lookup"><span data-stu-id="96494-131">New key vault</span></span>

<span data-ttu-id="96494-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span><span class="sxs-lookup"><span data-stu-id="96494-132">Enabling soft-delete for a new key vault is done at creation time by adding the soft-delete enable flag to your create command.</span></span>

```azurecli
az keyvault create --name ContosoVault --resource-group ContosoRG --enable-soft-delete true --location westus
```

### <a name="verify-soft-delete-enablement"></a><span data-ttu-id="96494-133">Verify soft-delete enablement</span><span class="sxs-lookup"><span data-stu-id="96494-133">Verify soft-delete enablement</span></span>

<span data-ttu-id="96494-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span><span class="sxs-lookup"><span data-stu-id="96494-134">To verify that a key vault has soft-delete enabled, run the *show* command and look for the 'Soft Delete Enabled?'</span></span> <span data-ttu-id="96494-135">attribute and its setting, true or false.</span><span class="sxs-lookup"><span data-stu-id="96494-135">attribute and its setting, true or false.</span></span>

```azurecli
az keyvault show --name ContosoVault
```

## <a name="deleting-a-key-vault-protected-by-soft-delete"></a><span data-ttu-id="96494-136">Deleting a key vault protected by soft-delete</span><span class="sxs-lookup"><span data-stu-id="96494-136">Deleting a key vault protected by soft-delete</span></span>

<span data-ttu-id="96494-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span><span class="sxs-lookup"><span data-stu-id="96494-137">The command to delete (or remove) a key vault remains the same, but its behavior changes depending on whether you have enabled soft-delete or not.</span></span>

```azurecli
az keyvault delete --name ContosoVault
```

> [!IMPORTANT]
><span data-ttu-id="96494-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span><span class="sxs-lookup"><span data-stu-id="96494-138">If you run the previous command for a key vault that does not have soft-delete enabled, you will permanently delete this key vault and all its content without any options for recovery.</span></span>

### <a name="how-soft-delete-protects-your-key-vaults"></a><span data-ttu-id="96494-139">How soft-delete protects your key vaults</span><span class="sxs-lookup"><span data-stu-id="96494-139">How soft-delete protects your key vaults</span></span>

<span data-ttu-id="96494-140">With soft-delete enabled:</span><span class="sxs-lookup"><span data-stu-id="96494-140">With soft-delete enabled:</span></span>

- <span data-ttu-id="96494-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span><span class="sxs-lookup"><span data-stu-id="96494-141">When a key vault is deleted, it is removed from its resource group and placed in a reserved namespace that is only associated with the location where it was created.</span></span> 
- <span data-ttu-id="96494-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span><span class="sxs-lookup"><span data-stu-id="96494-142">Objects in a deleted key vault, such as keys, secrets and, certificates, are inaccessible and remain so while their containing key vault is in the deleted state.</span></span> 
- <span data-ttu-id="96494-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span><span class="sxs-lookup"><span data-stu-id="96494-143">The DNS name for a key vault in a deleted state is still reserved so, a new key vault with same name cannot be created.</span></span>  

<span data-ttu-id="96494-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span><span class="sxs-lookup"><span data-stu-id="96494-144">You may view deleted state key vaults, associated with your subscription, using the following command:</span></span>

```azurecli
az keyvault list-deleted
```

<span data-ttu-id="96494-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span><span class="sxs-lookup"><span data-stu-id="96494-145">The *Resource ID* in the output refers to the original resource ID of this vault.</span></span> <span data-ttu-id="96494-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span><span class="sxs-lookup"><span data-stu-id="96494-146">Since this key vault is now in a deleted state, no resource exists with that resource ID.</span></span> <span data-ttu-id="96494-147">The *Id* field can be used to identify the resource when recovering, or purging.</span><span class="sxs-lookup"><span data-stu-id="96494-147">The *Id* field can be used to identify the resource when recovering, or purging.</span></span> <span data-ttu-id="96494-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span><span class="sxs-lookup"><span data-stu-id="96494-148">The *Scheduled Purge Date* field indicates when the vault will be permanently deleted (purged) if no action is taken for this deleted vault.</span></span> <span data-ttu-id="96494-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span><span class="sxs-lookup"><span data-stu-id="96494-149">The default retention period, used to calculate the *Scheduled Purge Date*, is 90 days.</span></span>

## <a name="recovering-a-key-vault"></a><span data-ttu-id="96494-150">Recovering a key vault</span><span class="sxs-lookup"><span data-stu-id="96494-150">Recovering a key vault</span></span>

<span data-ttu-id="96494-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span><span class="sxs-lookup"><span data-stu-id="96494-151">To recover a key vault, you need to specify the key vault name, resource group, and location.</span></span> <span data-ttu-id="96494-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span><span class="sxs-lookup"><span data-stu-id="96494-152">Note the location and the resource group of the deleted key vault as you need these for a key vault recovery process.</span></span>

```azurecli
az keyvault recover --location westus --resource-group ContosoRG --name ContosoVault
```

<span data-ttu-id="96494-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span><span class="sxs-lookup"><span data-stu-id="96494-153">When a key vault is recovered, the result is a new resource with the key vault's original resource ID.</span></span> <span data-ttu-id="96494-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span><span class="sxs-lookup"><span data-stu-id="96494-154">If the resource group where the key vault existed has been removed, a new resource group with same name must be created before the key vault can be recovered.</span></span>

## <a name="key-vault-objects-and-soft-delete"></a><span data-ttu-id="96494-155">Key Vault objects and soft-delete</span><span class="sxs-lookup"><span data-stu-id="96494-155">Key Vault objects and soft-delete</span></span>

<span data-ttu-id="96494-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span><span class="sxs-lookup"><span data-stu-id="96494-156">For a key, 'ContosoFirstKey', in a key vault named 'ContosoVault' with soft-delete enabled, here's how you would delete that key.</span></span>

```azurecli
az keyvault key delete --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="96494-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span><span class="sxs-lookup"><span data-stu-id="96494-157">With your key vault enabled for soft-delete, a deleted key still appears like it's deleted except, when you explicitly list or retrieve deleted keys.</span></span> <span data-ttu-id="96494-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span><span class="sxs-lookup"><span data-stu-id="96494-158">Most operations on a key in the deleted state will fail except for listing a deleted key, recovering it or purging it.</span></span> 

<span data-ttu-id="96494-159">For example, to request to list deleted keys in a key vault, use the following command:</span><span class="sxs-lookup"><span data-stu-id="96494-159">For example, to request to list deleted keys in a key vault, use the following command:</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="transition-state"></a><span data-ttu-id="96494-160">Transition state</span><span class="sxs-lookup"><span data-stu-id="96494-160">Transition state</span></span> 

<span data-ttu-id="96494-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span><span class="sxs-lookup"><span data-stu-id="96494-161">When you delete a key in a key vault with soft-delete enabled, it may take a few seconds for the transition to complete.</span></span> <span data-ttu-id="96494-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span><span class="sxs-lookup"><span data-stu-id="96494-162">During this transition state, it may appear that the key is not in the active state or the deleted state.</span></span> <span data-ttu-id="96494-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span><span class="sxs-lookup"><span data-stu-id="96494-163">This command will list all deleted keys in your key vault named 'ContosoVault'.</span></span>

```azurecli
az keyvault key list-deleted --vault-name ContosoVault
```

### <a name="using-soft-delete-with-key-vault-objects"></a><span data-ttu-id="96494-164">Using soft-delete with key vault objects</span><span class="sxs-lookup"><span data-stu-id="96494-164">Using soft-delete with key vault objects</span></span>

<span data-ttu-id="96494-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span><span class="sxs-lookup"><span data-stu-id="96494-165">Just like key vaults, a deleted key, secret or, certificate will remain in deleted state for up to 90 days unless you recover it or purge it.</span></span> 

#### <a name="keys"></a><span data-ttu-id="96494-166">Keys</span><span class="sxs-lookup"><span data-stu-id="96494-166">Keys</span></span>

<span data-ttu-id="96494-167">To recover a deleted key:</span><span class="sxs-lookup"><span data-stu-id="96494-167">To recover a deleted key:</span></span>

```azurecli
az keyvault key recover --name ContosoFirstKey --vault-name ContosoVault
```

<span data-ttu-id="96494-168">To permanently delete a key:</span><span class="sxs-lookup"><span data-stu-id="96494-168">To permanently delete a key:</span></span>

```azurecli
az keyvault key purge --name ContosoFirstKey --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="96494-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="96494-169">Purging a key will permanently delete it, meaning it will not be recoverable.</span></span>

<span data-ttu-id="96494-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span><span class="sxs-lookup"><span data-stu-id="96494-170">The **recover** and **purge** actions have their own permissions associated in a key vault access policy.</span></span> <span data-ttu-id="96494-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span><span class="sxs-lookup"><span data-stu-id="96494-171">For a user or service principal to be able to execute a **recover** or **purge** action they must have the respective permission for that object (key or secret) in the key vault access policy.</span></span> <span data-ttu-id="96494-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span><span class="sxs-lookup"><span data-stu-id="96494-172">By default, the **purge** permission is not added to a key vault's access policy when the 'all' shortcut is used to grant all permissions to a user.</span></span> <span data-ttu-id="96494-173">You must explicitly grant **purge** permission.</span><span class="sxs-lookup"><span data-stu-id="96494-173">You must explicitly grant **purge** permission.</span></span> <span data-ttu-id="96494-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span><span class="sxs-lookup"><span data-stu-id="96494-174">For example, the following command grants user@contoso.com permission to perform several operations on keys in *ContosoVault* including **purge**.</span></span>

#### <a name="set-a-key-vault-access-policy"></a><span data-ttu-id="96494-175">Set a key vault access policy</span><span class="sxs-lookup"><span data-stu-id="96494-175">Set a key vault access policy</span></span>

```azurecli
az keyvault set-policy --name ContosoVault --key-permissions get create delete list update import backup restore recover purge
```

>[!NOTE] 
> <span data-ttu-id="96494-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span><span class="sxs-lookup"><span data-stu-id="96494-176">If you have an existing key vault that has just had soft-delete enabled, you may not have **recover** and **purge** permissions.</span></span>

#### <a name="secrets"></a><span data-ttu-id="96494-177">Secrets</span><span class="sxs-lookup"><span data-stu-id="96494-177">Secrets</span></span>

<span data-ttu-id="96494-178">Like keys, secrets in a key vault are operated on with their own commands.</span><span class="sxs-lookup"><span data-stu-id="96494-178">Like keys, secrets in a key vault are operated on with their own commands.</span></span> <span data-ttu-id="96494-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span><span class="sxs-lookup"><span data-stu-id="96494-179">Following, are the commands for deleting, listing, recovering, and purging secrets.</span></span>

- <span data-ttu-id="96494-180">Delete a secret named SQLPassword:</span><span class="sxs-lookup"><span data-stu-id="96494-180">Delete a secret named SQLPassword:</span></span> 
```azurecli
az keyvault secret delete --vault-name ContosoVault -name SQLPassword
```

- <span data-ttu-id="96494-181">List all deleted secrets in a key vault:</span><span class="sxs-lookup"><span data-stu-id="96494-181">List all deleted secrets in a key vault:</span></span> 
```azurecli
az keyvault secret list-deleted --vault-name ContosoVault
```

- <span data-ttu-id="96494-182">Recover a secret in the deleted state:</span><span class="sxs-lookup"><span data-stu-id="96494-182">Recover a secret in the deleted state:</span></span> 
```azurecli
az keyvault secret recover --name SQLPassword --vault-name ContosoVault
```

- <span data-ttu-id="96494-183">Purge a secret in deleted state:</span><span class="sxs-lookup"><span data-stu-id="96494-183">Purge a secret in deleted state:</span></span> 
```azurecli
az keyvault secret purge --name SQLPAssword --vault-name ContosoVault
```

>[!NOTE]
><span data-ttu-id="96494-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="96494-184">Purging a secret will permanently delete it, meaning it will not be recoverable.</span></span>

## <a name="purging-and-key-vaults"></a><span data-ttu-id="96494-185">Purging and key vaults</span><span class="sxs-lookup"><span data-stu-id="96494-185">Purging and key vaults</span></span>

### <a name="key-vault-objects"></a><span data-ttu-id="96494-186">Key vault objects</span><span class="sxs-lookup"><span data-stu-id="96494-186">Key vault objects</span></span>

<span data-ttu-id="96494-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="96494-187">Purging a key, secret or, certificate will permanently delete it, meaning it will not be recoverable.</span></span> <span data-ttu-id="96494-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span><span class="sxs-lookup"><span data-stu-id="96494-188">The key vault that contained the deleted object will however remain intact as will all other objects in the key vault.</span></span> 

### <a name="key-vaults-as-containers"></a><span data-ttu-id="96494-189">Key vaults as containers</span><span class="sxs-lookup"><span data-stu-id="96494-189">Key vaults as containers</span></span>
<span data-ttu-id="96494-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="96494-190">When a key vault is purged, all of its contents, including keys, secrets, and certificates, are permanently deleted.</span></span> <span data-ttu-id="96494-191">To purge a key vault, use the `az keyvault purge` command.</span><span class="sxs-lookup"><span data-stu-id="96494-191">To purge a key vault, use the `az keyvault purge` command.</span></span> <span data-ttu-id="96494-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span><span class="sxs-lookup"><span data-stu-id="96494-192">You can find the location your subscription's deleted key vaults using the command `az keyvault list-deleted`.</span></span>

```azurecli
az keyvault purge --location westus --name ContosoVault
```

>[!NOTE]
><span data-ttu-id="96494-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span><span class="sxs-lookup"><span data-stu-id="96494-193">Purging a key vault will permanently delete it, meaning it will not be recoverable.</span></span>

### <a name="purge-permissions-required"></a><span data-ttu-id="96494-194">Purge permissions required</span><span class="sxs-lookup"><span data-stu-id="96494-194">Purge permissions required</span></span>
- <span data-ttu-id="96494-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span><span class="sxs-lookup"><span data-stu-id="96494-195">To purge a deleted key vault, such that the vault and all its contents are permanently removed, the user needs RBAC permission to perform a *Microsoft.KeyVault/locations/deletedVaults/purge/action* operation.</span></span> 
- <span data-ttu-id="96494-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span><span class="sxs-lookup"><span data-stu-id="96494-196">To list the deleted key, the vault a user needs RBAC permission to perform *Microsoft.KeyVault/deletedVaults/read* permission.</span></span> 
- <span data-ttu-id="96494-197">By default only a subscription administrator has these permissions.</span><span class="sxs-lookup"><span data-stu-id="96494-197">By default only a subscription administrator has these permissions.</span></span> 

### <a name="scheduled-purge"></a><span data-ttu-id="96494-198">Scheduled purge</span><span class="sxs-lookup"><span data-stu-id="96494-198">Scheduled purge</span></span>

<span data-ttu-id="96494-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span><span class="sxs-lookup"><span data-stu-id="96494-199">Listing your deleted key vault objects shows when they are schedled to be purged by Key Vault.</span></span> <span data-ttu-id="96494-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span><span class="sxs-lookup"><span data-stu-id="96494-200">The *Scheduled Purge Date* field indicates when a key vault object will be permanently deleted, if no action is taken.</span></span> <span data-ttu-id="96494-201">By default, the retention period for a deleted key vault object is 90 days.</span><span class="sxs-lookup"><span data-stu-id="96494-201">By default, the retention period for a deleted key vault object is 90 days.</span></span>

>[!NOTE]
><span data-ttu-id="96494-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="96494-202">A purged vault object, triggered by its *Scheduled Purge Date* field, is permanently deleted.</span></span> <span data-ttu-id="96494-203">It is not recoverable.</span><span class="sxs-lookup"><span data-stu-id="96494-203">It is not recoverable.</span></span>

## <a name="other-resources"></a><span data-ttu-id="96494-204">Other resources</span><span class="sxs-lookup"><span data-stu-id="96494-204">Other resources</span></span>

- <span data-ttu-id="96494-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span><span class="sxs-lookup"><span data-stu-id="96494-205">For an overview of Key Vault's soft-delete feature, see [Azure Key Vault soft-delete overview](key-vault-ovw-soft-delete.md).</span></span>
- <span data-ttu-id="96494-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="96494-206">For a general overview of Azure Key Vault usage, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>

