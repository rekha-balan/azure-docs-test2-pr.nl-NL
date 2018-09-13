---
title: How to configure system and user-assigned managed identities on an Azure VMSS using REST
description: Step by step instructions for configuring a system and user-assigned managed identities on an Azure VMSS using CURL to make REST API calls.
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
ms.date: 06/25/2018
ms.author: daveba
ms.openlocfilehash: a2af4b37e78a30d425b7fe3a12ca049e4a26d68b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856155"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-virtual-machine-scale-set-using-rest-api-calls"></a><span data-ttu-id="a90b2-103">Configure managed identities for Azure resources on a virtual machine scale set using REST API calls</span><span class="sxs-lookup"><span data-stu-id="a90b2-103">Configure managed identities for Azure resources on a virtual machine scale set using REST API calls</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="a90b2-104">Managed identities for Azure resources provides Azure services with an automatically managed system identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a90b2-104">Managed identities for Azure resources provides Azure services with an automatically managed system identity in Azure Active Directory.</span></span> <span data-ttu-id="a90b2-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="a90b2-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="a90b2-106">In this article, using CURL to make calls to the Azure Resource Manager REST endpoint, you learn how to perform the following managed identities for Azure resources operations on an virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="a90b2-106">In this article, using CURL to make calls to the Azure Resource Manager REST endpoint, you learn how to perform the following managed identities for Azure resources operations on an virtual machine scale set:</span></span>

- <span data-ttu-id="a90b2-107">Enable and disable the system-assigned managed identity on an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-107">Enable and disable the system-assigned managed identity on an Azure virtual machine scale set</span></span>
- <span data-ttu-id="a90b2-108">Add and remove a user-assigned managed identity on an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-108">Add and remove a user-assigned managed identity on an Azure virtual machine scale set</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a90b2-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a90b2-109">Prerequisites</span></span>

- <span data-ttu-id="a90b2-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="a90b2-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="a90b2-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="a90b2-111">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="a90b2-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="a90b2-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="a90b2-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="a90b2-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="a90b2-114">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="a90b2-114">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="a90b2-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from an virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a90b2-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system and/or user-assigned managed identity from an virtual machine scale set.</span></span>
    - <span data-ttu-id="a90b2-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="a90b2-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned identity from and to a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a90b2-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned identity from and to a virtual machine scale set.</span></span>
- <span data-ttu-id="a90b2-118">If you are using Windows, install the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or use the [Azure Cloud Shell](../../cloud-shell/overview.md) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a90b2-118">If you are using Windows, install the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or use the [Azure Cloud Shell](../../cloud-shell/overview.md) in the Azure portal.</span></span>
- <span data-ttu-id="a90b2-119">[Install the Azure CLI local console](/cli/azure/install-azure-cli), if you use the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or a [Linux distribution OS](/cli/azure/install-azure-cli-apt?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="a90b2-119">[Install the Azure CLI local console](/cli/azure/install-azure-cli), if you use the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about) or a [Linux distribution OS](/cli/azure/install-azure-cli-apt?view=azure-cli-latest).</span></span>
- <span data-ttu-id="a90b2-120">If you are using Azure CLI local console, sign in to Azure using `az login` with an account that is associated with the Azure subscription you would like to manage system or user-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="a90b2-120">If you are using Azure CLI local console, sign in to Azure using `az login` with an account that is associated with the Azure subscription you would like to manage system or user-assigned managed identities.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="a90b2-121">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="a90b2-121">System-assigned managed identity</span></span>

<span data-ttu-id="a90b2-122">In this section, you learn how to enable and disable system-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="a90b2-122">In this section, you learn how to enable and disable system-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-a-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-123">Enable system-assigned managed identity during creation of a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-123">Enable system-assigned managed identity during creation of a virtual machine scale set</span></span>

<span data-ttu-id="a90b2-124">To create a virtual machine scale set with system-assigned managed identity enabled, you need create a virtual machine scale set and retrieve an access token to use CURL to call the Resource Manager endpoint with the system-assigned managed identity type value.</span><span class="sxs-lookup"><span data-stu-id="a90b2-124">To create a virtual machine scale set with system-assigned managed identity enabled, you need create a virtual machine scale set and retrieve an access token to use CURL to call the Resource Manager endpoint with the system-assigned managed identity type value.</span></span>

1. <span data-ttu-id="a90b2-125">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span><span class="sxs-lookup"><span data-stu-id="a90b2-125">Create a [resource group](../../azure-resource-manager/resource-group-overview.md#terminology) for containment and deployment of your virtual machine scale set and its related resources, using [az group create](/cli/azure/group/#az-group-create).</span></span> <span data-ttu-id="a90b2-126">You can skip this step if you already have resource group you would like to use instead:</span><span class="sxs-lookup"><span data-stu-id="a90b2-126">You can skip this step if you already have resource group you would like to use instead:</span></span>

   ```azurecli-interactive 
   az group create --name myResourceGroup --location westus
   ```

2. <span data-ttu-id="a90b2-127">Create a [network interface](/cli/azure/network/nic?view=azure-cli-latest#az-network-nic-create) for your virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="a90b2-127">Create a [network interface](/cli/azure/network/nic?view=azure-cli-latest#az-network-nic-create) for your virtual machine scale set:</span></span>

   ```azurecli-interactive
    az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
   ```

3.  <span data-ttu-id="a90b2-128">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-128">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ``` 

4. <span data-ttu-id="a90b2-129">Create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="a90b2-129">Create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint.</span></span> <span data-ttu-id="a90b2-130">The following example creates a virtual machine scale set named *myVMSS* in the *myResourceGroup* with a system-assigned managed identity, as identified in the request body by the value `"identity":{"type":"SystemAssigned"}`.</span><span class="sxs-lookup"><span data-stu-id="a90b2-130">The following example creates a virtual machine scale set named *myVMSS* in the *myResourceGroup* with a system-assigned managed identity, as identified in the request body by the value `"identity":{"type":"SystemAssigned"}`.</span></span> <span data-ttu-id="a90b2-131">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-131">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span></span>
 
    ```bash   
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus","identity":{"type":"SystemAssigned"},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"Standard_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
    ```

### <a name="enable-system-assigned-managed-identity-on-a-existing-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-132">Enable system-assigned managed identity on a existing virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-132">Enable system-assigned managed identity on a existing virtual machine scale set</span></span>

<span data-ttu-id="a90b2-133">To enable system-assigned managed identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type.</span><span class="sxs-lookup"><span data-stu-id="a90b2-133">To enable system-assigned managed identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type.</span></span>

1. <span data-ttu-id="a90b2-134">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-134">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ```

2. <span data-ttu-id="a90b2-135">Use the following CURL command to call the Azure Resource Manager REST endpoint to enable system-assigned managed identity on your virtual machine scale set as identified in the request body by the value `{"identity":{"type":"SystemAssigned"}` for a virtual machine scale set named *myVMSS*.</span><span class="sxs-lookup"><span data-stu-id="a90b2-135">Use the following CURL command to call the Azure Resource Manager REST endpoint to enable system-assigned managed identity on your virtual machine scale set as identified in the request body by the value `{"identity":{"type":"SystemAssigned"}` for a virtual machine scale set named *myVMSS*.</span></span>  <span data-ttu-id="a90b2-136">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-136">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="a90b2-137">To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`.</span><span class="sxs-lookup"><span data-stu-id="a90b2-137">To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`.</span></span> <span data-ttu-id="a90b2-138">If you have any user-assigned managed identities assigned to the virtual machine scale set as identified in the `identity` value in the response, skip to step 3 that shows you how to retain user-assigned managed identities while enabling system-assigned managed identity on your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a90b2-138">If you have any user-assigned managed identities assigned to the virtual machine scale set as identified in the `identity` value in the response, skip to step 3 that shows you how to retain user-assigned managed identities while enabling system-assigned managed identity on your virtual machine scale set.</span></span>

   ```bash
    curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

3. <span data-ttu-id="a90b2-139">To enable system-assigned managed identity on a virtual machine scale set with existing user-assigned managed identities, you need to add `SystemAssigned` to the `type` value.</span><span class="sxs-lookup"><span data-stu-id="a90b2-139">To enable system-assigned managed identity on a virtual machine scale set with existing user-assigned managed identities, you need to add `SystemAssigned` to the `type` value.</span></span>  
   
   <span data-ttu-id="a90b2-140">For example, if your virtual machine scale set has the user-assigned managed identities `ID1` and `ID2` assigned to it, and you would like to add system-assigned managed identity to the virtual machine scale set, use the following CURL call.</span><span class="sxs-lookup"><span data-stu-id="a90b2-140">For example, if your virtual machine scale set has the user-assigned managed identities `ID1` and `ID2` assigned to it, and you would like to add system-assigned managed identity to the virtual machine scale set, use the following CURL call.</span></span> <span data-ttu-id="a90b2-141">Replace `<ACCESS TOKEN>` and `<SUBSCRIPTION ID>` with values appropriate to your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-141">Replace `<ACCESS TOKEN>` and `<SUBSCRIPTION ID>` with values appropriate to your environment.</span></span>

   <span data-ttu-id="a90b2-142">API version `2018-06-01` stores user-assigned managed identities in the `userAssignedIdentities` value in a dictionary format as opposed to the `identityIds` value in an array format used in API version `2017-12-01` and earlier versions.</span><span class="sxs-lookup"><span data-stu-id="a90b2-142">API version `2018-06-01` stores user-assigned managed identities in the `userAssignedIdentities` value in a dictionary format as opposed to the `identityIds` value in an array format used in API version `2017-12-01` and earlier versions.</span></span>
   
   <span data-ttu-id="a90b2-143">**API VERSION 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="a90b2-143">**API VERSION 2018-06-01**</span></span>

   ```bash
   curl -v 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned,UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```
   
   <span data-ttu-id="a90b2-144">**API VERSION 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="a90b2-144">**API VERSION 2017-12-01 and earlier**</span></span>

   ```bash
   curl -v 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned","UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

### <a name="disable-system-assigned-managed-identity-from-a-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-145">Disable system-assigned managed identity from a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-145">Disable system-assigned managed identity from a virtual machine scale set</span></span>

<span data-ttu-id="a90b2-146">To disable a system-assigned identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type to `None`.</span><span class="sxs-lookup"><span data-stu-id="a90b2-146">To disable a system-assigned identity on an existing virtual machine scale set, you need to acquire an access token and then use CURL to call the Resource Manager REST endpoint to update the identity type to `None`.</span></span>

1. <span data-ttu-id="a90b2-147">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-147">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ```

2. <span data-ttu-id="a90b2-148">Update the virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint to disable system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-148">Update the virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint to disable system-assigned managed identity.</span></span>  <span data-ttu-id="a90b2-149">The following example disables system-assigned managed identity as identified in the request body by the value `{"identity":{"type":"None"}}` from a virtual machine scale set named *myVMSS*.</span><span class="sxs-lookup"><span data-stu-id="a90b2-149">The following example disables system-assigned managed identity as identified in the request body by the value `{"identity":{"type":"None"}}` from a virtual machine scale set named *myVMSS*.</span></span>  <span data-ttu-id="a90b2-150">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-150">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="a90b2-151">To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`.</span><span class="sxs-lookup"><span data-stu-id="a90b2-151">To ensure you don't delete any existing user-assigned managed identities that are assigned to the virtual machine scale set, you need to list the user-assigned managed identities by using this CURL command: `curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"`.</span></span> <span data-ttu-id="a90b2-152">If you have any user-assigned managed identity assigned to the virtual machine scale set, skip to step 3 that shows you how retain the user-assigned managed identities while removing the system-assigned managed identity from your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a90b2-152">If you have any user-assigned managed identity assigned to the virtual machine scale set, skip to step 3 that shows you how retain the user-assigned managed identities while removing the system-assigned managed identity from your virtual machine scale set.</span></span>

   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

3. <span data-ttu-id="a90b2-153">To remove system-assigned managed identity from a virtual machine scale set that has user-assigned managed identities, remove `SystemAssigned` from the `{"identity":{"type:" "}}` value while keeping the `UserAssigned` value and the `userAssignedIdentities` dictionary values if you are using **API version 2018-06-01**.</span><span class="sxs-lookup"><span data-stu-id="a90b2-153">To remove system-assigned managed identity from a virtual machine scale set that has user-assigned managed identities, remove `SystemAssigned` from the `{"identity":{"type:" "}}` value while keeping the `UserAssigned` value and the `userAssignedIdentities` dictionary values if you are using **API version 2018-06-01**.</span></span> <span data-ttu-id="a90b2-154">If you are using **API version 2017-12-01** or earlier, keep the `identityIds` array.</span><span class="sxs-lookup"><span data-stu-id="a90b2-154">If you are using **API version 2017-12-01** or earlier, keep the `identityIds` array.</span></span>

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="a90b2-155">user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="a90b2-155">user-assigned managed identity</span></span>

<span data-ttu-id="a90b2-156">In this section, you learn how to add and remove user-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="a90b2-156">In this section, you learn how to add and remove user-assigned managed identity on a virtual machine scale set using CURL to make calls to the Azure Resource Manager REST endpoint.</span></span>

### <a name="assign-a-user-assigned-managed-identity-during-the-creation-of-a-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-157">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-157">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span></span>

1. <span data-ttu-id="a90b2-158">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-158">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ```

2. <span data-ttu-id="a90b2-159">Create a [network interface](/cli/azure/network/nic?view=azure-cli-latest#az-network-nic-create) for your virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="a90b2-159">Create a [network interface](/cli/azure/network/nic?view=azure-cli-latest#az-network-nic-create) for your virtual machine scale set:</span></span>

   ```azurecli-interactive
    az network nic create -g myResourceGroup --vnet-name myVnet --subnet mySubnet -n myNic
   ```

3.  <span data-ttu-id="a90b2-160">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-160">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ``` 

4. <span data-ttu-id="a90b2-161">Create a user-assigned managed identity using the instructions found here: [Create a user-assigned managed identity](how-to-manage-ua-identity-rest.md#create-a-user-assigned-managed-identity).</span><span class="sxs-lookup"><span data-stu-id="a90b2-161">Create a user-assigned managed identity using the instructions found here: [Create a user-assigned managed identity](how-to-manage-ua-identity-rest.md#create-a-user-assigned-managed-identity).</span></span>

5. <span data-ttu-id="a90b2-162">Create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="a90b2-162">Create a virtual machine scale set using CURL to call the Azure Resource Manager REST endpoint.</span></span> <span data-ttu-id="a90b2-163">The following example creates a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup* with a user-assigned managed identity `ID1`, as identified in the request body by the value `"identity":{"type":"UserAssigned"}`.</span><span class="sxs-lookup"><span data-stu-id="a90b2-163">The following example creates a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup* with a user-assigned managed identity `ID1`, as identified in the request body by the value `"identity":{"type":"UserAssigned"}`.</span></span> <span data-ttu-id="a90b2-164">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-164">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span></span>
 
   <span data-ttu-id="a90b2-165">**API VERSION 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="a90b2-165">**API VERSION 2018-06-01**</span></span>

   ```bash   
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus",{"identity":{"type":"UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}}},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"Standard_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
   ```

   <span data-ttu-id="a90b2-166">**API VERSION 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="a90b2-166">**API VERSION 2017-12-01 and earlier**</span></span>

   ```bash   
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PUT -d '{"sku":{"tier":"Standard","capacity":3,"name":"Standard_D1_v2"},"location":"eastus",{"identity":{"type":"UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}},"properties":{"overprovision":true,"virtualMachineProfile":{"storageProfile":{"imageReference":{"sku":"2016-Datacenter","publisher":"MicrosoftWindowsServer","version":"latest","offer":"WindowsServer"},"osDisk":{"caching":"ReadWrite","managedDisk":{"storageAccountType":"Standard_LRS"},"createOption":"FromImage"}},"osProfile":{"computerNamePrefix":"myVMSS","adminUsername":"azureuser","adminPassword":"myPassword12"},"networkProfile":{"networkInterfaceConfigurations":[{"name":"myVMSS","properties":{"primary":true,"enableIPForwarding":true,"ipConfigurations":[{"name":"myVMSS","properties":{"subnet":{"id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"}}}]}}]}},"upgradePolicy":{"mode":"Manual"}}}' -H "Content-Type: application/json" -H "Authorization: Bearer <ACCESS TOKEN>"
   ```

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-azure-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-167">Assign a user-assigned managed identity to an existing Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-167">Assign a user-assigned managed identity to an existing Azure virtual machine scale set</span></span>

1. <span data-ttu-id="a90b2-168">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-168">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ```

2.  <span data-ttu-id="a90b2-169">Create a user-assigned managed identity using the instructions found here, [Create a user-assigned managed identity](how-to-manage-ua-identity-rest.md#create-a-user-assigned-managed-identity).</span><span class="sxs-lookup"><span data-stu-id="a90b2-169">Create a user-assigned managed identity using the instructions found here, [Create a user-assigned managed identity](how-to-manage-ua-identity-rest.md#create-a-user-assigned-managed-identity).</span></span>

3. <span data-ttu-id="a90b2-170">To ensure you don't delete existing user or system-assigned managed identities that are assigned to the virtual machine scale set, you need to list the identity types assigned to the virtual machine scale set by using the following CURL command.</span><span class="sxs-lookup"><span data-stu-id="a90b2-170">To ensure you don't delete existing user or system-assigned managed identities that are assigned to the virtual machine scale set, you need to list the identity types assigned to the virtual machine scale set by using the following CURL command.</span></span> <span data-ttu-id="a90b2-171">If you have managed identities assigned to the virtual machine scale set, they are listed in the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="a90b2-171">If you have managed identities assigned to the virtual machine scale set, they are listed in the `identity` value.</span></span>
 
   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>"
   ```

4. <span data-ttu-id="a90b2-172">If you don't have any user or system-assigned managed identities assigned to your virtual machine scale set, use the following CURL command to call the Azure Resource Manager REST endpoint to assign the first user-assigned managed identity to the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a90b2-172">If you don't have any user or system-assigned managed identities assigned to your virtual machine scale set, use the following CURL command to call the Azure Resource Manager REST endpoint to assign the first user-assigned managed identity to the virtual machine scale set.</span></span>  <span data-ttu-id="a90b2-173">If you have a user or system-assigned managed identity(s) assigned to the virtual machine scale set, skip to step 5 that shows you how to add multiple user-assigned managed identities to a virtual machine scale set while also maintaining the system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-173">If you have a user or system-assigned managed identity(s) assigned to the virtual machine scale set, skip to step 5 that shows you how to add multiple user-assigned managed identities to a virtual machine scale set while also maintaining the system-assigned managed identity.</span></span>

   <span data-ttu-id="a90b2-174">The following example assigns a user-assigned managed identity, `ID1` to a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a90b2-174">The following example assigns a user-assigned managed identity, `ID1` to a virtual machine scale set named *myVMSS* in the resource group *myResourceGroup*.</span></span>  <span data-ttu-id="a90b2-175">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="a90b2-175">Replace `<ACCESS TOKEN>` with the value you received in the previous step when you requested a Bearer access token and the `<SUBSCRIPTION ID>` value as appropriate for your environment.</span></span>

   <span data-ttu-id="a90b2-176">**API VERSION 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="a90b2-176">**API VERSION 2018-06-01**</span></span>

    ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-12-01' -X PATCH -d '{"identity":{"type":"userAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```   
    
   <span data-ttu-id="a90b2-177">**API VERSION 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="a90b2-177">**API VERSION 2017-12-01 and earlier**</span></span>

   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"userAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

5. <span data-ttu-id="a90b2-178">If you have an existing user-assigned or system-assigned managed identity assigned to your virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="a90b2-178">If you have an existing user-assigned or system-assigned managed identity assigned to your virtual machine scale set:</span></span>
   
   <span data-ttu-id="a90b2-179">**API VERSION 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="a90b2-179">**API VERSION 2018-06-01**</span></span>

   <span data-ttu-id="a90b2-180">Add the user-assigned managed identity to the `userAssignedIdentities` dictionary value.</span><span class="sxs-lookup"><span data-stu-id="a90b2-180">Add the user-assigned managed identity to the `userAssignedIdentities` dictionary value.</span></span>

   <span data-ttu-id="a90b2-181">For example, if you have system-assigned managed identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale and would like to add the user-assigned managed identity `ID2` to it:</span><span class="sxs-lookup"><span data-stu-id="a90b2-181">For example, if you have system-assigned managed identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale and would like to add the user-assigned managed identity `ID2` to it:</span></span>

   ```bash
   curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{},"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

   <span data-ttu-id="a90b2-182">**API VERSION 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="a90b2-182">**API VERSION 2017-12-01 and earlier**</span></span>

   <span data-ttu-id="a90b2-183">Retain the user-assigned managed identities you would like to keep in the `identityIds` array value while adding the new user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-183">Retain the user-assigned managed identities you would like to keep in the `identityIds` array value while adding the new user-assigned managed identity.</span></span>

   <span data-ttu-id="a90b2-184">For example, if you have system-assigned identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale set and would like to add the user-assigned managed identity `ID2` to it:</span><span class="sxs-lookup"><span data-stu-id="a90b2-184">For example, if you have system-assigned identity and the user-assigned managed identity `ID1` currently assigned to your virtual machine scale set and would like to add the user-assigned managed identity `ID2` to it:</span></span> 

   ```bash
   curl  'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1","/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID2"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

### <a name="remove-a-user-assigned-managed-identity-from-a-virtual-machine-scale-set"></a><span data-ttu-id="a90b2-185">Remove a user-assigned managed identity from a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a90b2-185">Remove a user-assigned managed identity from a virtual machine scale set</span></span>

1. <span data-ttu-id="a90b2-186">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="a90b2-186">Retrieve a Bearer access token, which you will use in the next step in the Authorization header to create your virtual machine scale set with a system-assigned managed identity.</span></span>

   ```azurecli-interactive
   az account get-access-token
   ```

2. <span data-ttu-id="a90b2-187">To ensure you don't delete any existing user-assigned managed identities that you would like to keep assigned to the virtual machine scale set or remove the system-assigned managed identity, you need to list the managed identities by using the following CURL command:</span><span class="sxs-lookup"><span data-stu-id="a90b2-187">To ensure you don't delete any existing user-assigned managed identities that you would like to keep assigned to the virtual machine scale set or remove the system-assigned managed identity, you need to list the managed identities by using the following CURL command:</span></span> 
   
   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Compute/virtualMachineScaleSets/<VMSS NAME>?api-version=2018-06-01' -H "Authorization: Bearer <ACCESS TOKEN>" 
   ```
   
   <span data-ttu-id="a90b2-188">If you have managed identities assigned to the VM, they are listed in the response in the `identity` value.</span><span class="sxs-lookup"><span data-stu-id="a90b2-188">If you have managed identities assigned to the VM, they are listed in the response in the `identity` value.</span></span> 
    
   <span data-ttu-id="a90b2-189">For example, if you have user-assigned managed identities `ID1` and `ID2` assigned to your virtual machine scale set, and you only want to keep `ID1` assigned and retain the system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="a90b2-189">For example, if you have user-assigned managed identities `ID1` and `ID2` assigned to your virtual machine scale set, and you only want to keep `ID1` assigned and retain the system-assigned managed identity:</span></span>

   <span data-ttu-id="a90b2-190">**API VERSION 2018-06-01**</span><span class="sxs-lookup"><span data-stu-id="a90b2-190">**API VERSION 2018-06-01**</span></span>

   <span data-ttu-id="a90b2-191">Add `null` to the user-assigned managed identity you would like to remove:</span><span class="sxs-lookup"><span data-stu-id="a90b2-191">Add `null` to the user-assigned managed identity you would like to remove:</span></span>

   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned, UserAssigned", "userAssignedIdentities":{"/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1":{}}}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

   <span data-ttu-id="a90b2-192">**API VERSION 2017-12-01 and earlier**</span><span class="sxs-lookup"><span data-stu-id="a90b2-192">**API VERSION 2017-12-01 and earlier**</span></span>

   <span data-ttu-id="a90b2-193">Retain only the user-assigned managed identity(s) you would like to keep in the `identityIds` array:</span><span class="sxs-lookup"><span data-stu-id="a90b2-193">Retain only the user-assigned managed identity(s) you would like to keep in the `identityIds` array:</span></span>   

   ```bash
   curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2017-12-01' -X PATCH -d '{"identity":{"type":"SystemAssigned","UserAssigned", "identityIds":["/subscriptions/<SUBSCRIPTION ID>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/ID1"]}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
   ```

<span data-ttu-id="a90b2-194">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned using the following command:</span><span class="sxs-lookup"><span data-stu-id="a90b2-194">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned using the following command:</span></span>

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"SystemAssigned"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
```
    
<span data-ttu-id="a90b2-195">If your virtual machine scale set has only user-assigned managed identities and you would like to remove them all, use the following command:</span><span class="sxs-lookup"><span data-stu-id="a90b2-195">If your virtual machine scale set has only user-assigned managed identities and you would like to remove them all, use the following command:</span></span>

```bash
curl 'https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/myVMSS?api-version=2018-06-01' -X PATCH -d '{"identity":{"type":"None"}}' -H "Content-Type: application/json" -H Authorization:"Bearer <ACCESS TOKEN>"
```

## <a name="next-steps"></a><span data-ttu-id="a90b2-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="a90b2-196">Next steps</span></span>

<span data-ttu-id="a90b2-197">For information on how to create, list, or delete user-assigned managed identities using REST see:</span><span class="sxs-lookup"><span data-stu-id="a90b2-197">For information on how to create, list, or delete user-assigned managed identities using REST see:</span></span>

- [<span data-ttu-id="a90b2-198">Create, list or delete a user-assigned managed identity using REST API calls</span><span class="sxs-lookup"><span data-stu-id="a90b2-198">Create, list or delete a user-assigned managed identity using REST API calls</span></span>](how-to-manage-ua-identity-rest.md)
