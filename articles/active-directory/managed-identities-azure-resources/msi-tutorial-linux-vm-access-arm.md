---
title: Use a Linux VM user-assigned managed identity to access Azure Resource Manager
description: A tutorial that walks you through the process of using a user-assigned managed identity on a Linux VM to access Azure Resource Manager.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: daveba
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/22/2017
ms.author: daveba
ROBOTS: NOINDEX,NOFOLLOW
ms.openlocfilehash: 4abde91e04048d64a17f861825d1fb7779873155
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867843"
---
# <a name="tutorial-use-a-user-assigned-managed-identity-on-a-linux-vm-to-access-azure-resource-manager"></a><span data-ttu-id="10264-103">Tutorial: Use a user-assigned managed identity on a Linux VM to access Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-103">Tutorial: Use a user-assigned managed identity on a Linux VM to access Azure Resource Manager</span></span>

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

<span data-ttu-id="10264-104">This tutorial explains how to create a user-assigned managed identity, assign it to a Linux Virtual Machine (VM), and then use that identity to access the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="10264-104">This tutorial explains how to create a user-assigned managed identity, assign it to a Linux Virtual Machine (VM), and then use that identity to access the Azure Resource Manager API.</span></span> <span data-ttu-id="10264-105">Managed identities for Azure resources are automatically managed by Azure.</span><span class="sxs-lookup"><span data-stu-id="10264-105">Managed identities for Azure resources are automatically managed by Azure.</span></span> <span data-ttu-id="10264-106">They enable authentication to services that support Azure AD authentication, without needing to embed credentials into your code.</span><span class="sxs-lookup"><span data-stu-id="10264-106">They enable authentication to services that support Azure AD authentication, without needing to embed credentials into your code.</span></span> 

<span data-ttu-id="10264-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="10264-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="10264-108">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="10264-108">Create a user-assigned managed identity</span></span>
> * <span data-ttu-id="10264-109">Assign the user-assigned managed identity to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="10264-109">Assign the user-assigned managed identity to a Linux VM</span></span> 
> * <span data-ttu-id="10264-110">Grant the user-assigned managed identity access to a Resource Group in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-110">Grant the user-assigned managed identity access to a Resource Group in Azure Resource Manager</span></span> 
> * <span data-ttu-id="10264-111">Get an access token using the user-assigned managed identity and use it to call Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-111">Get an access token using the user-assigned managed identity and use it to call Azure Resource Manager</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="10264-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="10264-112">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

[!INCLUDE [msi-tut-prereqs](../../../includes/active-directory-msi-tut-prereqs.md)]

[<span data-ttu-id="10264-113">Sign in to Azure portal</span><span class="sxs-lookup"><span data-stu-id="10264-113">Sign in to Azure portal</span></span>](https://portal.azure.com)

[<span data-ttu-id="10264-114">Create a Linux virtual machine</span><span class="sxs-lookup"><span data-stu-id="10264-114">Create a Linux virtual machine</span></span>](/azure/virtual-machines/linux/quick-create-portal)

<span data-ttu-id="10264-115">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="10264-115">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="10264-116">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="10264-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="10264-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10264-117">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-user-assigned-managed-identity"></a><span data-ttu-id="10264-118">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="10264-118">Create a user-assigned managed identity</span></span>

1. <span data-ttu-id="10264-119">If you are using the CLI console (instead of an Azure Cloud Shell session), start by signing in to Azure.</span><span class="sxs-lookup"><span data-stu-id="10264-119">If you are using the CLI console (instead of an Azure Cloud Shell session), start by signing in to Azure.</span></span> <span data-ttu-id="10264-120">Use an account that is associated with the Azure subscription under which you would like to create the new user-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="10264-120">Use an account that is associated with the Azure subscription under which you would like to create the new user-assigned managed identity:</span></span>

    ```azurecli
    az login
    ```

2. <span data-ttu-id="10264-121">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span><span class="sxs-lookup"><span data-stu-id="10264-121">Create a user-assigned managed identity using [az identity create](/cli/azure/identity#az-identity-create).</span></span> <span data-ttu-id="10264-122">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="10264-122">The `-g` parameter specifies the resource group where the user-assigned managed identity is created, and the `-n` parameter specifies its name.</span></span> <span data-ttu-id="10264-123">Be sure to replace the `<RESOURCE GROUP>` and `<UAMI NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="10264-123">Be sure to replace the `<RESOURCE GROUP>` and `<UAMI NAME>` parameter values with your own values:</span></span>
    
[!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]


```azurecli-interactive
az identity create -g <RESOURCE GROUP> -n <UAMI NAME>
```

<span data-ttu-id="10264-124">The response contains details for the user-assigned managed identity created, similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="10264-124">The response contains details for the user-assigned managed identity created, similar to the following example.</span></span> <span data-ttu-id="10264-125">Note the `id` value for your user-assigned managed identity, as it will be used in the next step:</span><span class="sxs-lookup"><span data-stu-id="10264-125">Note the `id` value for your user-assigned managed identity, as it will be used in the next step:</span></span>

```json
{
"clientId": "73444643-8088-4d70-9532-c3a0fdc190fz",
"clientSecretUrl": "https://control-westcentralus.identity.azure.net/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>/credentials?tid=5678&oid=9012&aid=12344643-8088-4d70-9532-c3a0fdc190fz",
"id": "/subscriptions/<SUBSCRIPTON ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>",
"location": "westcentralus",
"name": "<UAMI NAME>",
"principalId": "9012",
"resourceGroup": "<RESOURCE GROUP>",
"tags": {},
"tenantId": "733a8f0e-ec41-4e69-8ad8-971fc4b533bl",
"type": "Microsoft.ManagedIdentity/userAssignedIdentities"
}
```

## <a name="assign-a-user-assigned-managed-identity-to-your-linux-vm"></a><span data-ttu-id="10264-126">Assign a user-assigned managed identity to your Linux VM</span><span class="sxs-lookup"><span data-stu-id="10264-126">Assign a user-assigned managed identity to your Linux VM</span></span>

<span data-ttu-id="10264-127">A user-assigned managed identity can be used by clients on multiple Azure resources.</span><span class="sxs-lookup"><span data-stu-id="10264-127">A user-assigned managed identity can be used by clients on multiple Azure resources.</span></span> <span data-ttu-id="10264-128">Use the following commands to assign the user-assigned managed identity to a single VM.</span><span class="sxs-lookup"><span data-stu-id="10264-128">Use the following commands to assign the user-assigned managed identity to a single VM.</span></span> <span data-ttu-id="10264-129">Use the `Id` property returned in the previous step for the `-IdentityID` parameter.</span><span class="sxs-lookup"><span data-stu-id="10264-129">Use the `Id` property returned in the previous step for the `-IdentityID` parameter.</span></span>

<span data-ttu-id="10264-130">Assign the user-assigned managed identity to your Linux VM using [az vm assign-identity](/cli/azure/vm#az-vm-assign-identity).</span><span class="sxs-lookup"><span data-stu-id="10264-130">Assign the user-assigned managed identity to your Linux VM using [az vm assign-identity](/cli/azure/vm#az-vm-assign-identity).</span></span> <span data-ttu-id="10264-131">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="10264-131">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span></span> <span data-ttu-id="10264-132">Use the `id` property returned in the previous step for the `--identities` parameter value.</span><span class="sxs-lookup"><span data-stu-id="10264-132">Use the `id` property returned in the previous step for the `--identities` parameter value.</span></span>

```azurecli-interactive
az vm assign-identity -g <RESOURCE GROUP> -n <VM NAME> --identities "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<UAMI NAME>"
```

## <a name="grant-your-user-assigned-managed-identity-access-to-a-resource-group-in-azure-resource-manager"></a><span data-ttu-id="10264-133">Grant your user-assigned managed identity access to a Resource Group in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-133">Grant your user-assigned managed identity access to a Resource Group in Azure Resource Manager</span></span> 

<span data-ttu-id="10264-134">Managed identities for Azure resources provides identities that your code can use to request access tokens to authenticate to resource APIs that support Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="10264-134">Managed identities for Azure resources provides identities that your code can use to request access tokens to authenticate to resource APIs that support Azure AD authentication.</span></span> <span data-ttu-id="10264-135">In this tutorial, your code will access the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="10264-135">In this tutorial, your code will access the Azure Resource Manager API.</span></span>  

<span data-ttu-id="10264-136">Before your code can access the API, you need to grant the identity access to a resource in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10264-136">Before your code can access the API, you need to grant the identity access to a resource in Azure Resource Manager.</span></span> <span data-ttu-id="10264-137">In this case, the Resource Group in which the VM is contained.</span><span class="sxs-lookup"><span data-stu-id="10264-137">In this case, the Resource Group in which the VM is contained.</span></span> <span data-ttu-id="10264-138">Update the value for `<SUBSCRIPTION ID>` and `<RESOURCE GROUP>` as appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="10264-138">Update the value for `<SUBSCRIPTION ID>` and `<RESOURCE GROUP>` as appropriate for your environment.</span></span> <span data-ttu-id="10264-139">Additionally, replace `<UAMI PRINCIPALID>` with the `principalId` property returned by the `az identity create` command in [Create a user-assigned managed identity](#create-a-user-assigned-managed-identity):</span><span class="sxs-lookup"><span data-stu-id="10264-139">Additionally, replace `<UAMI PRINCIPALID>` with the `principalId` property returned by the `az identity create` command in [Create a user-assigned managed identity](#create-a-user-assigned-managed-identity):</span></span>

```azurecli-interactive
az role assignment create --assignee <UAMI PRINCIPALID> --role 'Reader' --scope "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESOURCE GROUP> "
```

<span data-ttu-id="10264-140">The response contains details for the role assignment created, similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="10264-140">The response contains details for the role assignment created, similar to the following example:</span></span>

```json
{
  "id": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>/providers/Microsoft.Authorization/roleAssignments/b402bd74-157f-425c-bf7d-zed3a3a581ll",
  "name": "b402bd74-157f-425c-bf7d-zed3a3a581ll",
  "properties": {
    "principalId": "f5fdfdc1-ed84-4d48-8551-999fb9dedfbl",
    "roleDefinitionId": "/subscriptions/<SUBSCRIPTION ID>/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
    "scope": "/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>"
  },
  "resourceGroup": "<RESOURCE GROUP>",
  "type": "Microsoft.Authorization/roleAssignments"
}

```

## <a name="get-an-access-token-using-the-vms-identity-and-use-it-to-call-resource-manager"></a><span data-ttu-id="10264-141">Get an access token using the VM's identity and use it to call Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-141">Get an access token using the VM's identity and use it to call Resource Manager</span></span> 

<span data-ttu-id="10264-142">For the remainder of the tutorial, we will work from the VM we created earlier.</span><span class="sxs-lookup"><span data-stu-id="10264-142">For the remainder of the tutorial, we will work from the VM we created earlier.</span></span>

<span data-ttu-id="10264-143">To complete these steps, you need an SSH client.</span><span class="sxs-lookup"><span data-stu-id="10264-143">To complete these steps, you need an SSH client.</span></span> <span data-ttu-id="10264-144">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="10264-144">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span></span> 

1. <span data-ttu-id="10264-145">Sign in to the Azure [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="10264-145">Sign in to the Azure [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="10264-146">In the portal, navigate to **Virtual Machines** and go to the Linux virtual machine and in the **Overview**, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="10264-146">In the portal, navigate to **Virtual Machines** and go to the Linux virtual machine and in the **Overview**, click **Connect**.</span></span> <span data-ttu-id="10264-147">Copy the string to connect to your VM.</span><span class="sxs-lookup"><span data-stu-id="10264-147">Copy the string to connect to your VM.</span></span>
3. <span data-ttu-id="10264-148">Connect to the VM with the SSH client of your choice.</span><span class="sxs-lookup"><span data-stu-id="10264-148">Connect to the VM with the SSH client of your choice.</span></span> <span data-ttu-id="10264-149">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span><span class="sxs-lookup"><span data-stu-id="10264-149">If you are using Windows, you can use the SSH client in the [Windows Subsystem for Linux](https://msdn.microsoft.com/commandline/wsl/about).</span></span> <span data-ttu-id="10264-150">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](~/articles/virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](~/articles/virtual-machines/linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="10264-150">If you need assistance configuring your SSH client's keys, see [How to Use SSH keys with Windows on Azure](~/articles/virtual-machines/linux/ssh-from-windows.md), or [How to create and use an SSH public and private key pair for Linux VMs in Azure](~/articles/virtual-machines/linux/mac-create-ssh-keys.md).</span></span>
4. <span data-ttu-id="10264-151">In the terminal window, using CURL, make a request to the Azure Instance Metadata Service (IMDS) identity endpoint to get an access token for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10264-151">In the terminal window, using CURL, make a request to the Azure Instance Metadata Service (IMDS) identity endpoint to get an access token for Azure Resource Manager.</span></span>  

   <span data-ttu-id="10264-152">The CURL request to acquire an access token is shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="10264-152">The CURL request to acquire an access token is shown in the following example.</span></span> <span data-ttu-id="10264-153">Be sure to replace `<CLIENT ID>` with the `clientId` property returned by the `az identity create` command in [Create a user-assigned managed identity](#create-a-user-assigned-managed-identity):</span><span class="sxs-lookup"><span data-stu-id="10264-153">Be sure to replace `<CLIENT ID>` with the `clientId` property returned by the `az identity create` command in [Create a user-assigned managed identity](#create-a-user-assigned-managed-identity):</span></span> 
    
   ```bash
   curl -H Metadata:true "http://169.254.169.254/metadata/identity/oauth2/token?api-version=2018-02-01&resource=https%3A%2F%2Fmanagement.azure.com/&client_id=<UAMI CLIENT ID>"   
   ```
    
    > [!NOTE]
    > <span data-ttu-id="10264-154">The value of the `resource` parameter must be an exact match for what is expected by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10264-154">The value of the `resource` parameter must be an exact match for what is expected by Azure AD.</span></span> <span data-ttu-id="10264-155">When using the Resource Manager resource ID, you must include the trailing slash on the URI.</span><span class="sxs-lookup"><span data-stu-id="10264-155">When using the Resource Manager resource ID, you must include the trailing slash on the URI.</span></span> 
    
    <span data-ttu-id="10264-156">The response includes the access token you need to access Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="10264-156">The response includes the access token you need to access Azure Resource Manager.</span></span> 
    
    <span data-ttu-id="10264-157">Response example:</span><span class="sxs-lookup"><span data-stu-id="10264-157">Response example:</span></span>  

    ```bash
    {
    "access_token":"eyJ0eXAiOi...",
    "refresh_token":"",
    "expires_in":"3599",
    "expires_on":"1504130527",
    "not_before":"1504126627",
    "resource":"https://management.azure.com",
    "token_type":"Bearer"
    } 
    ```

5. <span data-ttu-id="10264-158">Use the access token to access Azure Resource Manager, and read the properties of the Resource Group to which you previously granted your user-assigned managed identity access.</span><span class="sxs-lookup"><span data-stu-id="10264-158">Use the access token to access Azure Resource Manager, and read the properties of the Resource Group to which you previously granted your user-assigned managed identity access.</span></span> <span data-ttu-id="10264-159">Be sure to replace `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="10264-159">Be sure to replace `<SUBSCRIPTION ID>`, `<RESOURCE GROUP>` with the values you specified earlier, and `<ACCESS TOKEN>` with the token returned in the previous step.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10264-160">The URL is case-sensitive, so be sure to use the exact same case you used earlier when you named the Resource Group, and the uppercase "G" in `resourceGroups`.</span><span class="sxs-lookup"><span data-stu-id="10264-160">The URL is case-sensitive, so be sure to use the exact same case you used earlier when you named the Resource Group, and the uppercase "G" in `resourceGroups`.</span></span>  

    ```bash 
    curl https://management.azure.com/subscriptions/<SUBSCRIPTION ID>/resourceGroups/<RESOURCE GROUP>?api-version=2016-09-01 -H "Authorization: Bearer <ACCESS TOKEN>" 
    ```

    <span data-ttu-id="10264-161">The response contains the specific Resource Group information, similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="10264-161">The response contains the specific Resource Group information, similar to the following example:</span></span> 

    ```bash
    {
    "id":"/subscriptions/<SUBSCRIPTION ID>/resourceGroups/DevTest",
    "name":"DevTest",
    "location":"westus",
    "properties":{"provisioningState":"Succeeded"}
    } 
    ```
    
## <a name="next-steps"></a><span data-ttu-id="10264-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="10264-162">Next steps</span></span>

<span data-ttu-id="10264-163">In this tutorial, you learned how to create a user-assigned managed identity and attach it to a Linux virtual machine to access the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="10264-163">In this tutorial, you learned how to create a user-assigned managed identity and attach it to a Linux virtual machine to access the Azure Resource Manager API.</span></span>  <span data-ttu-id="10264-164">To learn more about Azure Resource Manager see:</span><span class="sxs-lookup"><span data-stu-id="10264-164">To learn more about Azure Resource Manager see:</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="10264-165">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="10264-165">Azure Resource Manager</span></span>](/azure/azure-resource-manager/resource-group-overview)

