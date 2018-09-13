---
title: How to configure system and user-assigned managed identities on an Azure VM using Azure CLI
description: Step by step instructions for configuring system and user-assigned managed identities on an Azure VM using Azure CLI.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/14/2017
ms.author: daveba
ms.openlocfilehash: a0fadc959fd7faa94b0a8415cf860608c08f47f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858050"
---
# <a name="configure-managed-identities-for-azure-resources-on-an-azure-vm-using-azure-cli"></a><span data-ttu-id="a8b33-103">Configure managed identities for Azure resources on an Azure VM using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a8b33-103">Configure managed identities for Azure resources on an Azure VM using Azure CLI</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="a8b33-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8b33-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="a8b33-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="a8b33-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="a8b33-106">In this article, using the Azure CLI, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span><span class="sxs-lookup"><span data-stu-id="a8b33-106">In this article, using the Azure CLI, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span></span>

- <span data-ttu-id="a8b33-107">Enable and disable the system-assigned managed identity on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-107">Enable and disable the system-assigned managed identity on an Azure VM</span></span>
- <span data-ttu-id="a8b33-108">Add and remove a user-assigned managed identity on an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-108">Add and remove a user-assigned managed identity on an Azure VM</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8b33-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a8b33-109">Prerequisites</span></span>

- <span data-ttu-id="a8b33-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8b33-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="a8b33-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="a8b33-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="a8b33-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="a8b33-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="a8b33-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="a8b33-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="a8b33-114">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="a8b33-114">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="a8b33-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="a8b33-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span></span>
    - <span data-ttu-id="a8b33-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a8b33-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="a8b33-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span><span class="sxs-lookup"><span data-stu-id="a8b33-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span></span>
- <span data-ttu-id="a8b33-118">To run the CLI script examples, you have three options:</span><span class="sxs-lookup"><span data-stu-id="a8b33-118">To run the CLI script examples, you have three options:</span></span>
    - <span data-ttu-id="a8b33-119">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span><span class="sxs-lookup"><span data-stu-id="a8b33-119">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span></span>
    - <span data-ttu-id="a8b33-120">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span><span class="sxs-lookup"><span data-stu-id="a8b33-120">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span></span>
    - <span data-ttu-id="a8b33-121">[Install the latest version of Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="a8b33-121">[Install the latest version of Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) if you prefer to use a local CLI console.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="a8b33-122">The commands have been updated to reflect the latest release of the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8b33-122">The commands have been updated to reflect the latest release of the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>     
        

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="a8b33-123">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="a8b33-123">System-assigned managed identity</span></span>

<span data-ttu-id="a8b33-124">In this section, you learn how to enable and disable the system-assigned managed identity on an Azure VM using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a8b33-124">In this section, you learn how to enable and disable the system-assigned managed identity on an Azure VM using Azure CLI.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-an-azure-vm"></a><span data-ttu-id="a8b33-125">Enable system-assigned managed identity during creation of an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-125">Enable system-assigned managed identity during creation of an Azure VM</span></span>

<span data-ttu-id="a8b33-126">To create an Azure VM with the system-assigned managed identity enabled:</span><span class="sxs-lookup"><span data-stu-id="a8b33-126">To create an Azure VM with the system-assigned managed identity enabled:</span></span>

1. <span data-ttu-id="a8b33-127">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span><span class="sxs-lookup"><span data-stu-id="a8b33-127">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span></span> <span data-ttu-id="a8b33-128">Use an account that is associated with the Azure subscription under which you would like to deploy the VM:</span><span class="sxs-lookup"><span data-stu-id="a8b33-128">Use an account that is associated with the Azure subscription under which you would like to deploy the VM:</span></span>

   ```azurecli-interactive
   az login
   ```

2. <span data-ttu-id="a8b33-129">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your VM and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-129">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your VM and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span></span> <span data-ttu-id="a8b33-130">You can skip this step if you already have resource group you would like to use instead:</span><span class="sxs-lookup"><span data-stu-id="a8b33-130">You can skip this step if you already have resource group you would like to use instead:</span></span>

   ```azurecli-interactive 
   az group create --name myResourceGroup --location westus
   ```

3. <span data-ttu-id="a8b33-131">Create a VM using [az vm create](/cli/azure/vm/#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-131">Create a VM using [az vm create](/cli/azure/vm/#az-vm-create).</span></span> <span data-ttu-id="a8b33-132">The following example creates a VM named *myVM* with a system-assigned managed identity, as requested by the `--assign-identity` parameter.</span><span class="sxs-lookup"><span data-stu-id="a8b33-132">The following example creates a VM named *myVM* with a system-assigned managed identity, as requested by the `--assign-identity` parameter.</span></span> <span data-ttu-id="a8b33-133">The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in.</span><span class="sxs-lookup"><span data-stu-id="a8b33-133">The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in.</span></span> <span data-ttu-id="a8b33-134">Update these values as appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="a8b33-134">Update these values as appropriate for your environment:</span></span> 

   ```azurecli-interactive 
   az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --generate-ssh-keys --assign-identity --admin-username azureuser --admin-password myPassword12
   ```

### <a name="enable-system-assigned-managed-identity-on-an-existing-azure-vm"></a><span data-ttu-id="a8b33-135">Enable system-assigned managed identity on an existing Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-135">Enable system-assigned managed identity on an existing Azure VM</span></span>

<span data-ttu-id="a8b33-136">If you need to enable the system-assigned managed identity on an existing VM:</span><span class="sxs-lookup"><span data-stu-id="a8b33-136">If you need to enable the system-assigned managed identity on an existing VM:</span></span>

1. <span data-ttu-id="a8b33-137">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span><span class="sxs-lookup"><span data-stu-id="a8b33-137">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span></span> <span data-ttu-id="a8b33-138">Use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="a8b33-138">Use an account that is associated with the Azure subscription that contains the VM.</span></span>

   ```azurecli-interactive
   az login
   ```

2. <span data-ttu-id="a8b33-139">Use [az vm identity assign](/cli/azure/vm/identity/#az-vm-identity-assign) with the `identity assign` command enable the system-assigned identity to an existing VM:</span><span class="sxs-lookup"><span data-stu-id="a8b33-139">Use [az vm identity assign](/cli/azure/vm/identity/#az-vm-identity-assign) with the `identity assign` command enable the system-assigned identity to an existing VM:</span></span>

   ```azurecli-interactive
   az vm identity assign -g myResourceGroup -n myVm
   ```

### <a name="disable-system-assigned-identity-from-an-azure-vm"></a><span data-ttu-id="a8b33-140">Disable system-assigned identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-140">Disable system-assigned identity from an Azure VM</span></span>

<span data-ttu-id="a8b33-141">If you have a Virtual Machine that no longer needs the system-assigned identity, but still needs user-assigned identities, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a8b33-141">If you have a Virtual Machine that no longer needs the system-assigned identity, but still needs user-assigned identities, use the following command:</span></span>

```azurecli-interactive
az vm update -n myVM -g myResourceGroup --set identity.type='UserAssigned' 
```

<span data-ttu-id="a8b33-142">If you have a virtual machine that no longer needs system-assigned identity and it has no user-assigned identities, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a8b33-142">If you have a virtual machine that no longer needs system-assigned identity and it has no user-assigned identities, use the following command:</span></span>

> [!NOTE]
> <span data-ttu-id="a8b33-143">The value `none` is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="a8b33-143">The value `none` is case sensitive.</span></span> <span data-ttu-id="a8b33-144">It must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="a8b33-144">It must be lowercase.</span></span> 

```azurecli-interactive
az vm update -n myVM -g myResourceGroup --set identity.type="none"
```

<span data-ttu-id="a8b33-145">To remove the managed identity for Azure resources VM extension (planned for deprecation in January 2019), user `-n ManagedIdentityExtensionForWindows` or `-n ManagedIdentityExtensionForLinux` switch (depending on the type of VM) with [az vm extension delete](https://docs.microsoft.com/cli/azure/vm/#assign-identity):</span><span class="sxs-lookup"><span data-stu-id="a8b33-145">To remove the managed identity for Azure resources VM extension (planned for deprecation in January 2019), user `-n ManagedIdentityExtensionForWindows` or `-n ManagedIdentityExtensionForLinux` switch (depending on the type of VM) with [az vm extension delete](https://docs.microsoft.com/cli/azure/vm/#assign-identity):</span></span>

```azurecli-interactive
az vm identity --resource-group myResourceGroup --vm-name myVm -n ManagedIdentityExtensionForWindows
```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="a8b33-146">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="a8b33-146">User-assigned managed identity</span></span>

<span data-ttu-id="a8b33-147">In this section, you will learn how to add and remove a user-assigned managed identity from an Azure VM using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a8b33-147">In this section, you will learn how to add and remove a user-assigned managed identity from an Azure VM using Azure CLI.</span></span>

### <a name="assign-a-user-assigned-managed-identity-during-the-creation-of-an-azure-vm"></a><span data-ttu-id="a8b33-148">Assign a user-assigned managed identity during the creation of an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-148">Assign a user-assigned managed identity during the creation of an Azure VM</span></span>

<span data-ttu-id="a8b33-149">This section walks you through creation of a VM with assignment of a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a8b33-149">This section walks you through creation of a VM with assignment of a user-assigned managed identity.</span></span> <span data-ttu-id="a8b33-150">If you already have a VM you want to use, skip this section and proceed to the next.</span><span class="sxs-lookup"><span data-stu-id="a8b33-150">If you already have a VM you want to use, skip this section and proceed to the next.</span></span>

1. <span data-ttu-id="a8b33-151">You can skip this step if you already have a resource group you would like to use.</span><span class="sxs-lookup"><span data-stu-id="a8b33-151">You can skip this step if you already have a resource group you would like to use.</span></span> <span data-ttu-id="a8b33-152">Create a [resource group](~/articles/azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/cli/azure/group/#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-152">Create a [resource group](~/articles/azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/cli/azure/group/#az-group-create).</span></span> <span data-ttu-id="a8b33-153">Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="a8b33-153">Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values.</span></span> <span data-ttu-id="a8b33-154">:</span><span class="sxs-lookup"><span data-stu-id="a8b33-154">:</span></span>

   ```azurecli-interactive 
   az group create --name <RESOURCE GROUP> --location <LOCATION>
   ```

2. <span data-ttu-id="a8b33-155">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-155">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span></span>  <span data-ttu-id="a8b33-156">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="a8b33-156">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span></span>    
    
   [!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

   ```azurecli-interactive
   az identity create -g myResourceGroup -n myUserAssignedIdentity
   ```
   <span data-ttu-id="a8b33-157">The response contains details for the user-assigned managed identity created, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="a8b33-157">The response contains details for the user-assigned managed identity created, similar to the following.</span></span> <span data-ttu-id="a8b33-158">The resource id value assigned to the user-assigned managed identity is used in the following step.</span><span class="sxs-lookup"><span data-stu-id="a8b33-158">The resource id value assigned to the user-assigned managed identity is used in the following step.</span></span>

   ```json
   {
       "clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
       "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<myUserAssignedIdentity>/credentials?tid=5678&oid=9012&aid=73444643-8088-4d70-9532-c3a0fdc190fz",
       "id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>",
       "location": "westcentralus",
       "name": "<USER ASSIGNED IDENTITY NAME>",
       "principalId": "e5fdfdc1-ed84-4d48-8551-fe9fb9dedfll",
       "resourceGroup": "<RESOURCE GROUP>",
       "tags": {},
       "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
       "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
   }
   ```

3. <span data-ttu-id="a8b33-159">Create a VM using [az vm create](/cli/azure/vm/#az-vm-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-159">Create a VM using [az vm create](/cli/azure/vm/#az-vm-create).</span></span> <span data-ttu-id="a8b33-160">The following example creates a VM associated with the new user-assigned identity, as specified by the `--assign-identity` parameter.</span><span class="sxs-lookup"><span data-stu-id="a8b33-160">The following example creates a VM associated with the new user-assigned identity, as specified by the `--assign-identity` parameter.</span></span> <span data-ttu-id="a8b33-161">Be sure to replace the `<RESOURCE GROUP>`, `<VM NAME>`, `<USER NAME>`, `<PASSWORD>`, and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="a8b33-161">Be sure to replace the `<RESOURCE GROUP>`, `<VM NAME>`, `<USER NAME>`, `<PASSWORD>`, and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values.</span></span> 

   ```azurecli-interactive 
   az vm create --resource-group <RESOURCE GROUP> --name <VM NAME> --image UbuntuLTS --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <USER ASSIGNED IDENTITY NAME>
   ```

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-azure-vm"></a><span data-ttu-id="a8b33-162">Assign a user-assigned managed identity to an existing Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-162">Assign a user-assigned managed identity to an existing Azure VM</span></span>

1. <span data-ttu-id="a8b33-163">Create a user-assigned identity using [az identity create](/cli/azure/identity#az-identity-create).</span><span class="sxs-lookup"><span data-stu-id="a8b33-163">Create a user-assigned identity using [az identity create](/cli/azure/identity#az-identity-create).</span></span>  <span data-ttu-id="a8b33-164">The `-g` parameter specifies the resource group where the user-assigned identity is created, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="a8b33-164">The `-g` parameter specifies the resource group where the user-assigned identity is created, and the `-n` parameter specifies its name.</span></span> <span data-ttu-id="a8b33-165">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="a8b33-165">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a8b33-166">Creating user-assigned managed identities with special characters (i.e. underscore) in the name is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="a8b33-166">Creating user-assigned managed identities with special characters (i.e. underscore) in the name is not currently supported.</span></span> <span data-ttu-id="a8b33-167">Please use alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="a8b33-167">Please use alphanumeric characters.</span></span> <span data-ttu-id="a8b33-168">Check back for updates.</span><span class="sxs-lookup"><span data-stu-id="a8b33-168">Check back for updates.</span></span>  <span data-ttu-id="a8b33-169">For more information see [FAQs and known issues](known-issues.md)</span><span class="sxs-lookup"><span data-stu-id="a8b33-169">For more information see [FAQs and known issues](known-issues.md)</span></span>

    ```azurecli-interactive
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```
   <span data-ttu-id="a8b33-170">The response contains details for the user-assigned managed identity created, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="a8b33-170">The response contains details for the user-assigned managed identity created, similar to the following.</span></span> 

   ```json
   {
        "clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
        "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>/credentials?tid=5678&oid=9012&aid=73444643-8088-4d70-9532-c3a0fdc190fz",
        "id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>",
        "location": "westcentralus",
        "name": "<USER ASSIGNED IDENTITY NAME>",
        "principalId": "e5fdfdc1-ed84-4d48-8551-fe9fb9dedfll",
        "resourceGroup": "<RESOURCE GROUP>",
        "tags": {},
        "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
        "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
   }
   ```

2. <span data-ttu-id="a8b33-171">Assign the user-assigned identity to your VM using [az vm identity assign](/cli/azure/vm#az-vm-identity-assign).</span><span class="sxs-lookup"><span data-stu-id="a8b33-171">Assign the user-assigned identity to your VM using [az vm identity assign](/cli/azure/vm#az-vm-identity-assign).</span></span> <span data-ttu-id="a8b33-172">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="a8b33-172">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span></span> <span data-ttu-id="a8b33-173">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's resource `name` property, as created in the previous step:</span><span class="sxs-lookup"><span data-stu-id="a8b33-173">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's resource `name` property, as created in the previous step:</span></span>

    ```azurecli-interactive
    az vm identity assign -g <RESOURCE GROUP> -n <VM NAME> --identities <USER ASSIGNED IDENTITY>
    ```

### <a name="remove-a-user-assigned-managed-identity-from-an-azure-vm"></a><span data-ttu-id="a8b33-174">Remove a user-assigned managed identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="a8b33-174">Remove a user-assigned managed identity from an Azure VM</span></span>

<span data-ttu-id="a8b33-175">To remove a user-assigned managed identity from a VM use [az vm identity remove](/cli/azure/vm#az-vm-identity-remove).</span><span class="sxs-lookup"><span data-stu-id="a8b33-175">To remove a user-assigned managed identity from a VM use [az vm identity remove](/cli/azure/vm#az-vm-identity-remove).</span></span> <span data-ttu-id="a8b33-176">If this is the only user-assigned managed identity assigned to the virtual machine, `UserAssigned` will be removed from the identity type value.</span><span class="sxs-lookup"><span data-stu-id="a8b33-176">If this is the only user-assigned managed identity assigned to the virtual machine, `UserAssigned` will be removed from the identity type value.</span></span>  <span data-ttu-id="a8b33-177">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="a8b33-177">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span></span> <span data-ttu-id="a8b33-178">The `<USER ASSIGNED IDENTITY>` will be the user-assigned identity's `name` property, which can be found in the identity section of the virtual machine using `az vm identity show`:</span><span class="sxs-lookup"><span data-stu-id="a8b33-178">The `<USER ASSIGNED IDENTITY>` will be the user-assigned identity's `name` property, which can be found in the identity section of the virtual machine using `az vm identity show`:</span></span>

```azurecli-interactive
az vm identity remove -g <RESOURCE GROUP> -n <VM NAME> --identities <USER ASSIGNED IDENTITY>
```

<span data-ttu-id="a8b33-179">If your VM does not have a system-assigned managed identity and you want to remove all user-assigned identities from it, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a8b33-179">If your VM does not have a system-assigned managed identity and you want to remove all user-assigned identities from it, use the following command:</span></span>

> [!NOTE]
> <span data-ttu-id="a8b33-180">The value `none` is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="a8b33-180">The value `none` is case sensitive.</span></span> <span data-ttu-id="a8b33-181">It must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="a8b33-181">It must be lowercase.</span></span>

```azurecli-interactive
az vm update -n myVM -g myResourceGroup --set identity.type="none" identity.userAssignedIdentities=null
```

<span data-ttu-id="a8b33-182">If your VM has both system-assigned and user-assigned identities, you can remove all the user-assigned identities by switching to use only system-assigned.</span><span class="sxs-lookup"><span data-stu-id="a8b33-182">If your VM has both system-assigned and user-assigned identities, you can remove all the user-assigned identities by switching to use only system-assigned.</span></span> <span data-ttu-id="a8b33-183">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="a8b33-183">Use the following command:</span></span>

```azurecli-interactive
az vm update -n myVM -g myResourceGroup --set identity.type='SystemAssigned' identity.userAssignedIdentities=null 
```

## <a name="next-steps"></a><span data-ttu-id="a8b33-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="a8b33-184">Next steps</span></span>
- [<span data-ttu-id="a8b33-185">Managed identities for Azure resources overview</span><span class="sxs-lookup"><span data-stu-id="a8b33-185">Managed identities for Azure resources overview</span></span>](overview.md)
- <span data-ttu-id="a8b33-186">For the full Azure VM creation Quickstarts, see:</span><span class="sxs-lookup"><span data-stu-id="a8b33-186">For the full Azure VM creation Quickstarts, see:</span></span> 
  - [<span data-ttu-id="a8b33-187">Create a Windows virtual machine with CLI</span><span class="sxs-lookup"><span data-stu-id="a8b33-187">Create a Windows virtual machine with CLI</span></span>](../../virtual-machines/windows/quick-create-cli.md)  
  - [<span data-ttu-id="a8b33-188">Create a Linux virtual machine with CLI</span><span class="sxs-lookup"><span data-stu-id="a8b33-188">Create a Linux virtual machine with CLI</span></span>](../../virtual-machines/linux/quick-create-cli.md) 

















