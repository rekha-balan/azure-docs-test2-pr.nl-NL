---
title: How to configure system and user-assigned managed identities on an Azure VMSS using Azure CLI
description: Step by step instructions for configuring system and user-assigned managed identities on an Azure VMSS, using Azure CLI.
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
ms.date: 02/15/2018
ms.author: daveba
ms.openlocfilehash: 8f24c79a51610d1840092674614619b61a93c8e8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869484"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-virtual-machine-scale-set-using-azure-cli"></a><span data-ttu-id="2ff1a-103">Configure managed identities for Azure resources on a virtual machine scale set using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2ff1a-103">Configure managed identities for Azure resources on a virtual machine scale set using Azure CLI</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="2ff1a-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="2ff1a-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="2ff1a-106">In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure Virtual Machine Scale Set (VMSS), using the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-106">In this article, you learn how to perform the following managed identities for Azure resources operations on an Azure Virtual Machine Scale Set (VMSS), using the Azure CLI:</span></span>
- <span data-ttu-id="2ff1a-107">Enable and disable the system-assigned managed identity on an Azure VMSS</span><span class="sxs-lookup"><span data-stu-id="2ff1a-107">Enable and disable the system-assigned managed identity on an Azure VMSS</span></span>
- <span data-ttu-id="2ff1a-108">Add and remove a user-assigned managed identity on an Azure VMSS</span><span class="sxs-lookup"><span data-stu-id="2ff1a-108">Add and remove a user-assigned managed identity on an Azure VMSS</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2ff1a-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ff1a-109">Prerequisites</span></span>

- <span data-ttu-id="2ff1a-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="2ff1a-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="2ff1a-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="2ff1a-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="2ff1a-114">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-114">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="2ff1a-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from a virtual machine scale set.</span></span>
    - <span data-ttu-id="2ff1a-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="2ff1a-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span></span>
- <span data-ttu-id="2ff1a-118">To run the CLI script examples, you have three options:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-118">To run the CLI script examples, you have three options:</span></span>
    - <span data-ttu-id="2ff1a-119">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-119">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span></span>
    - <span data-ttu-id="2ff1a-120">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-120">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span></span>
    - <span data-ttu-id="2ff1a-121">[Install the latest version of Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-121">[Install the latest version of Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli) if you prefer to use a local CLI console.</span></span> 
      
      > [!NOTE]
      > <span data-ttu-id="2ff1a-122">The commands have been updated to reflect the latest release of the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-122">The commands have been updated to reflect the latest release of the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="2ff1a-123">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="2ff1a-123">System-assigned managed identity</span></span>

<span data-ttu-id="2ff1a-124">In this section, you learn how to enable and disable the system-assigned managed identity for an Azure VMSS using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-124">In this section, you learn how to enable and disable the system-assigned managed identity for an Azure VMSS using Azure CLI.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-125">Enable system-assigned managed identity during creation of an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-125">Enable system-assigned managed identity during creation of an Azure virtual machine scale set</span></span>

<span data-ttu-id="2ff1a-126">To create a virtual machine scale set with the system-assigned managed identity enabled:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-126">To create a virtual machine scale set with the system-assigned managed identity enabled:</span></span>

1. <span data-ttu-id="2ff1a-127">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-127">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span></span> <span data-ttu-id="2ff1a-128">Use an account that is associated with the Azure subscription under which you would like to deploy the virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-128">Use an account that is associated with the Azure subscription under which you would like to deploy the virtual machine scale set:</span></span>

   ```azurecli-interactive
   az login
   ```

2. <span data-ttu-id="2ff1a-129">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-129">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span></span> <span data-ttu-id="2ff1a-130">You can skip this step if you already have a resource group you would like to use instead:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-130">You can skip this step if you already have a resource group you would like to use instead:</span></span>

   ```azurecli-interactive 
   az group create --name myResourceGroup --location westus
   ```

3. <span data-ttu-id="2ff1a-131">Create a virtual machine scale set using [az vmss create](/cli/azure/vmss/#az-vmss-create) .</span><span class="sxs-lookup"><span data-stu-id="2ff1a-131">Create a virtual machine scale set using [az vmss create](/cli/azure/vmss/#az-vmss-create) .</span></span> <span data-ttu-id="2ff1a-132">The following example creates a virtual machine scale set named *myVMSS* with a system-assigned managed identity, as requested by the `--assign-identity` parameter.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-132">The following example creates a virtual machine scale set named *myVMSS* with a system-assigned managed identity, as requested by the `--assign-identity` parameter.</span></span> <span data-ttu-id="2ff1a-133">The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-133">The `--admin-username` and `--admin-password` parameters specify the administrative user name and password account for virtual machine sign-in.</span></span> <span data-ttu-id="2ff1a-134">Update these values as appropriate for your environment:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-134">Update these values as appropriate for your environment:</span></span> 

   ```azurecli-interactive 
   az vmss create --resource-group myResourceGroup --name myVMSS --image win2016datacenter --upgrade-policy-mode automatic --custom-data cloud-init.txt --admin-username azureuser --admin-password myPassword12 --assign-identity --generate-ssh-keys
   ```

### <a name="enable-system-assigned-managed-identity-on-an-existing-azure-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-135">Enable system-assigned managed identity on an existing Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-135">Enable system-assigned managed identity on an existing Azure virtual machine scale set</span></span>

<span data-ttu-id="2ff1a-136">If you need to enable the system-assigned managed identity on an existing Azure virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-136">If you need to enable the system-assigned managed identity on an existing Azure virtual machine scale set:</span></span>

1. <span data-ttu-id="2ff1a-137">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-137">If you're using the Azure CLI in a local console, first sign in to Azure using [az login](/cli/azure/reference-index#az-login).</span></span> <span data-ttu-id="2ff1a-138">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-138">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span>

   ```azurecli-interactive
   az login
   ```

2. <span data-ttu-id="2ff1a-139">Use [az vmss identity assign](/cli/azure/vmss/identity/#az-vmss-identity-assign) command to enable a system-assigned managed identity to an existing VM:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-139">Use [az vmss identity assign](/cli/azure/vmss/identity/#az-vmss-identity-assign) command to enable a system-assigned managed identity to an existing VM:</span></span>

   ```azurecli-interactive
   az vmss identity assign -g myResourceGroup -n myVMSS
   ```

### <a name="disable-system-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-140">Disable system-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-140">Disable system-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="2ff1a-141">If you have a virtual machine scale set that no longer needs the system-assigned managed identity, but still needs user-assigned managed identities, use the following command:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-141">If you have a virtual machine scale set that no longer needs the system-assigned managed identity, but still needs user-assigned managed identities, use the following command:</span></span>

```azurecli-interactive
az vmss update -n myVM -g myResourceGroup --set identity.type='UserAssigned' 
```

<span data-ttu-id="2ff1a-142">If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following command:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-142">If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following command:</span></span>

> [!NOTE]
> <span data-ttu-id="2ff1a-143">The value `none` is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-143">The value `none` is case sensitive.</span></span> <span data-ttu-id="2ff1a-144">It must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-144">It must be lowercase.</span></span> 

```azurecli-interactive
az vmss update -n myVM -g myResourceGroup --set identity.type="none"
```

<span data-ttu-id="2ff1a-145">To remove the managed identities for Azure resources VM extension (planned for deprecation in January 2019), use [az vmss identity remove](/cli/azure/vmss/identity/#az-vmss-remove-identity) command to remove the system-assigned managed identity from a VMSS:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-145">To remove the managed identities for Azure resources VM extension (planned for deprecation in January 2019), use [az vmss identity remove](/cli/azure/vmss/identity/#az-vmss-remove-identity) command to remove the system-assigned managed identity from a VMSS:</span></span>

```azurecli-interactive
az vmss extension delete -n ManagedIdentityExtensionForWindows -g myResourceGroup -vmss-name myVMSS
```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="2ff1a-146">user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="2ff1a-146">user-assigned managed identity</span></span>

<span data-ttu-id="2ff1a-147">In this section, you learn how to enable and remove a user-assigned managed identity using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-147">In this section, you learn how to enable and remove a user-assigned managed identity using Azure CLI.</span></span>

### <a name="assign-a-user-assigned-managed-identity-during-the-creation-of-a-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-148">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-148">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span></span>

<span data-ttu-id="2ff1a-149">This section walks you through creation of an VMSS and assignment of a user-assigned managed identity to the VMSS.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-149">This section walks you through creation of an VMSS and assignment of a user-assigned managed identity to the VMSS.</span></span> <span data-ttu-id="2ff1a-150">If you already have a VMSS you want to use, skip this section and proceed to the next.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-150">If you already have a VMSS you want to use, skip this section and proceed to the next.</span></span>

1. <span data-ttu-id="2ff1a-151">You can skip this step if you already have a resource group you would like to use.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-151">You can skip this step if you already have a resource group you would like to use.</span></span> <span data-ttu-id="2ff1a-152">Create a [resource group](~/articles/azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/cli/azure/group/#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-152">Create a [resource group](~/articles/azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your user-assigned managed identity, using [az group create](/cli/azure/group/#az-group-create).</span></span> <span data-ttu-id="2ff1a-153">Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-153">Be sure to replace the `<RESOURCE GROUP>` and `<LOCATION>` parameter values with your own values.</span></span> <span data-ttu-id="2ff1a-154">:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-154">:</span></span>

   ```azurecli-interactive 
   az group create --name <RESOURCE GROUP> --location <LOCATION>
   ```

2. <span data-ttu-id="2ff1a-155">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-155">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span></span>  <span data-ttu-id="2ff1a-156">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-156">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span></span> <span data-ttu-id="2ff1a-157">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-157">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span></span>

   [!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

   ```azurecli-interactive
   az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
   ```
   <span data-ttu-id="2ff1a-158">The response contains details for the user-assigned managed identity created, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-158">The response contains details for the user-assigned managed identity created, similar to the following.</span></span> <span data-ttu-id="2ff1a-159">The resource `id` value assigned to the user-assigned managed identity is used in the following step.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-159">The resource `id` value assigned to the user-assigned managed identity is used in the following step.</span></span>

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

3. <span data-ttu-id="2ff1a-160">Create a VMSS using [az vmss create](/cli/azure/vmss/#az-vmss-create).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-160">Create a VMSS using [az vmss create](/cli/azure/vmss/#az-vmss-create).</span></span> <span data-ttu-id="2ff1a-161">The following example creates a VMSS associated with the new user-assigned managed identity, as specified by the `--assign-identity` parameter.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-161">The following example creates a VMSS associated with the new user-assigned managed identity, as specified by the `--assign-identity` parameter.</span></span> <span data-ttu-id="2ff1a-162">Be sure to replace the `<RESOURCE GROUP>`, `<VMSS NAME>`, `<USER NAME>`, `<PASSWORD>`, and `<USER ASSIGNED IDENTITY>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-162">Be sure to replace the `<RESOURCE GROUP>`, `<VMSS NAME>`, `<USER NAME>`, `<PASSWORD>`, and `<USER ASSIGNED IDENTITY>` parameter values with your own values.</span></span> 

   ```azurecli-interactive 
   az vmss create --resource-group <RESOURCE GROUP> --name <VMSS NAME> --image UbuntuLTS --admin-username <USER NAME> --admin-password <PASSWORD> --assign-identity <USER ASSIGNED IDENTITY>
   ```

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-163">Assign a user-assigned managed identity to an existing virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-163">Assign a user-assigned managed identity to an existing virtual machine scale set</span></span>

1. <span data-ttu-id="2ff1a-164">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-164">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span></span>  <span data-ttu-id="2ff1a-165">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-165">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span></span> <span data-ttu-id="2ff1a-166">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-166">Be sure to replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2ff1a-167">Creating user-assigned managed identities with special characters (i.e. underscore) in the name is not currently supported.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-167">Creating user-assigned managed identities with special characters (i.e. underscore) in the name is not currently supported.</span></span> <span data-ttu-id="2ff1a-168">Please use alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-168">Please use alphanumeric characters.</span></span> <span data-ttu-id="2ff1a-169">Check back for updates.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-169">Check back for updates.</span></span>  <span data-ttu-id="2ff1a-170">For more information see [FAQs and known issues](known-issues.md)</span><span class="sxs-lookup"><span data-stu-id="2ff1a-170">For more information see [FAQs and known issues](known-issues.md)</span></span>

    ```azurecli-interactive
    az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
    ```
<span data-ttu-id="2ff1a-171">The response contains details for the user-assigned managed identity created, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-171">The response contains details for the user-assigned managed identity created, similar to the following.</span></span>

   ```json
   {
        "clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
        "clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY >/credentials?tid=5678&oid=9012&aid=73444643-8088-4d70-9532-c3a0fdc190fz",
        "id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY>",
        "location": "westcentralus",
        "name": "<USER ASSIGNED IDENTITY>",
        "principalId": "e5fdfdc1-ed84-4d48-8551-fe9fb9dedfll",
        "resourceGroup": "<RESOURCE GROUP>",
        "tags": {},
        "tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
        "type": "Microsoft.ManagedIdentity/userAssignedIdentities"    
   }
   ```

2. <span data-ttu-id="2ff1a-172">Assign the user-assigned managed identity to your VMSS using [az vmss identity assign](/cli/azure/vmss/identity#az-vm-assign-identity).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-172">Assign the user-assigned managed identity to your VMSS using [az vmss identity assign](/cli/azure/vmss/identity#az-vm-assign-identity).</span></span> <span data-ttu-id="2ff1a-173">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-173">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span></span> <span data-ttu-id="2ff1a-174">The `<USER ASSIGNED IDENTITY>` is the user-assigned identity's resource `name` property, as created in the previous step:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-174">The `<USER ASSIGNED IDENTITY>` is the user-assigned identity's resource `name` property, as created in the previous step:</span></span>

    ```azurecli-interactive
    az vmss identity assign -g <RESOURCE GROUP> -n <VMSS NAME> --identities <USER ASSIGNED IDENTITY>
    ```

### <a name="remove-a-user-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="2ff1a-175">Remove a user-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="2ff1a-175">Remove a user-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="2ff1a-176">To remove a user-assigned managed identity from a virtual machine scale set use [az vmss identity remove](/cli/azure/vmss/identity#az-vmss-identity-remove).</span><span class="sxs-lookup"><span data-stu-id="2ff1a-176">To remove a user-assigned managed identity from a virtual machine scale set use [az vmss identity remove](/cli/azure/vmss/identity#az-vmss-identity-remove).</span></span> <span data-ttu-id="2ff1a-177">If this is the only user-assigned managed identity assigned to the virtual machine scale set, `UserAssigned` will be removed from the identity type value.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-177">If this is the only user-assigned managed identity assigned to the virtual machine scale set, `UserAssigned` will be removed from the identity type value.</span></span>  <span data-ttu-id="2ff1a-178">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-178">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span></span> <span data-ttu-id="2ff1a-179">The `<USER ASSIGNED IDENTITY>` will be the user-assigned managed identity's `name` property, which can be found in the identity section of the virtual machine scale set using `az vmss identity show`:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-179">The `<USER ASSIGNED IDENTITY>` will be the user-assigned managed identity's `name` property, which can be found in the identity section of the virtual machine scale set using `az vmss identity show`:</span></span>

```azurecli-interactive
az vmss identity remove -g <RESOURCE GROUP> -n <VMSS NAME> --identities <USER ASSIGNED IDENTITY>
```

<span data-ttu-id="2ff1a-180">If your virtual machine scale set does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-180">If your virtual machine scale set does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span></span>

> [!NOTE]
> <span data-ttu-id="2ff1a-181">The value `none` is case sensitive.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-181">The value `none` is case sensitive.</span></span> <span data-ttu-id="2ff1a-182">It must be lowercase.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-182">It must be lowercase.</span></span>

```azurecli-interactive
az vmss update -n myVMSS -g myResourceGroup --set identity.type="none" identity.userAssignedIdentities=null
```

<span data-ttu-id="2ff1a-183">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned identities by switching to use only system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="2ff1a-183">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned identities by switching to use only system-assigned managed identity.</span></span> <span data-ttu-id="2ff1a-184">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-184">Use the following command:</span></span>

```azurecli-interactive
az vmss update -n myVMSS -g myResourceGroup --set identity.type='SystemAssigned' identity.userAssignedIdentities=null 
```

## <a name="next-steps"></a><span data-ttu-id="2ff1a-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ff1a-185">Next steps</span></span>

- [<span data-ttu-id="2ff1a-186">Managed identities for Azure resources overview</span><span class="sxs-lookup"><span data-stu-id="2ff1a-186">Managed identities for Azure resources overview</span></span>](overview.md)
- <span data-ttu-id="2ff1a-187">For the full Azure virtual machine scale set creation Quickstart, see:</span><span class="sxs-lookup"><span data-stu-id="2ff1a-187">For the full Azure virtual machine scale set creation Quickstart, see:</span></span> 

  - [<span data-ttu-id="2ff1a-188">Create a Virtual Machine Scale Set with CLI</span><span class="sxs-lookup"><span data-stu-id="2ff1a-188">Create a Virtual Machine Scale Set with CLI</span></span>](../../virtual-machines/linux/tutorial-create-vmss.md#create-a-scale-set)

















