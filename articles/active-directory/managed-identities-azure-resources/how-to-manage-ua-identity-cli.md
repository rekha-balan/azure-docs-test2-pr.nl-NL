---
title: How to manage a user-assigned managed identity using Azure CLI
description: Step by step instructions on how to create, list and delete a user-assigned managed identity using the Azure CLI.
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
ms.date: 04/16/2018
ms.author: daveba
ms.openlocfilehash: 1ba164cdf6d7665077616edc20d133c6912b186f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858042"
---
# <a name="create-list-or-delete-a-user-assigned-managed-identity-using-the-azure-cli"></a><span data-ttu-id="f097b-103">Create, list or delete a user-assigned managed identity using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f097b-103">Create, list or delete a user-assigned managed identity using the Azure CLI</span></span>

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

<span data-ttu-id="f097b-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f097b-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span></span> <span data-ttu-id="f097b-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="f097b-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span></span> 

<span data-ttu-id="f097b-106">In this article, you learn how to create, list and delete a user-assigned managed identity using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f097b-106">In this article, you learn how to create, list and delete a user-assigned managed identity using Azure CLI.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f097b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f097b-107">Prerequisites</span></span>

- <span data-ttu-id="f097b-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f097b-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="f097b-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="f097b-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="f097b-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="f097b-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="f097b-111">To perform the management operations in this article, your account needs the following role assignments:</span><span class="sxs-lookup"><span data-stu-id="f097b-111">To perform the management operations in this article, your account needs the following role assignments:</span></span>
    - <span data-ttu-id="f097b-112">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f097b-112">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span></span>
    - <span data-ttu-id="f097b-113">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f097b-113">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span></span>
- <span data-ttu-id="f097b-114">To run the CLI script examples, you have three options:</span><span class="sxs-lookup"><span data-stu-id="f097b-114">To run the CLI script examples, you have three options:</span></span>
    - <span data-ttu-id="f097b-115">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span><span class="sxs-lookup"><span data-stu-id="f097b-115">Use [Azure Cloud Shell](../../cloud-shell/overview.md) from the Azure portal (see next section).</span></span>
    - <span data-ttu-id="f097b-116">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span><span class="sxs-lookup"><span data-stu-id="f097b-116">Use the embedded Azure Cloud Shell via the "Try It" button, located in the top right corner of each code block.</span></span>
    - <span data-ttu-id="f097b-117">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.13 or later) if you prefer to use a local CLI console.</span><span class="sxs-lookup"><span data-stu-id="f097b-117">[Install the latest version of CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) (2.0.13 or later) if you prefer to use a local CLI console.</span></span> <span data-ttu-id="f097b-118">Sign in to Azure using `az login`, using an account that is associated with the Azure subscription under which you would like to deploy the user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f097b-118">Sign in to Azure using `az login`, using an account that is associated with the Azure subscription under which you would like to deploy the user-assigned managed identity.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="create-a-user-assigned-managed-identity"></a><span data-ttu-id="f097b-119">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f097b-119">Create a user-assigned managed identity</span></span> 

<span data-ttu-id="f097b-120">To create a user-assigned managed identity, use the [az identity create](/cli/azure/identity#az-identity-create) command.</span><span class="sxs-lookup"><span data-stu-id="f097b-120">To create a user-assigned managed identity, use the [az identity create](/cli/azure/identity#az-identity-create) command.</span></span> <span data-ttu-id="f097b-121">The `-g` parameter specifies the resource group where to create the user-assigned managed identity, and the `-n` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="f097b-121">The `-g` parameter specifies the resource group where to create the user-assigned managed identity, and the `-n` parameter specifies its name.</span></span> <span data-ttu-id="f097b-122">Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="f097b-122">Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span></span>

[!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

 ```azurecli-interactive
az identity create -g <RESOURCE GROUP> -n <USER ASSIGNED IDENTITY NAME>
```
## <a name="list-user-assigned-managed-identities"></a><span data-ttu-id="f097b-123">List user-assigned managed identities</span><span class="sxs-lookup"><span data-stu-id="f097b-123">List user-assigned managed identities</span></span>

<span data-ttu-id="f097b-124">To list user-assigned managed identities, use the [az identity list](/cli/azure/identity#az-identity-list) command.</span><span class="sxs-lookup"><span data-stu-id="f097b-124">To list user-assigned managed identities, use the [az identity list](/cli/azure/identity#az-identity-list) command.</span></span> <span data-ttu-id="f097b-125">Replace the `<RESOURCE GROUP>` with your own value:</span><span class="sxs-lookup"><span data-stu-id="f097b-125">Replace the `<RESOURCE GROUP>` with your own value:</span></span>

```azurecli-interactive
az identity list -g <RESOURCE GROUP>
```
<span data-ttu-id="f097b-126">In the json response, user-assigned managed identities have `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for key, `type`.</span><span class="sxs-lookup"><span data-stu-id="f097b-126">In the json response, user-assigned managed identities have `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for key, `type`.</span></span>

`"type": "Microsoft.ManagedIdentity/userAssignedIdentities"`

## <a name="delete-a-user-assigned-managed-identity"></a><span data-ttu-id="f097b-127">Delete a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f097b-127">Delete a user-assigned managed identity</span></span>

<span data-ttu-id="f097b-128">To delete a user-assigned managed identity, use the [az identity delete](/cli/azure/identity#az-identity-delete) command.</span><span class="sxs-lookup"><span data-stu-id="f097b-128">To delete a user-assigned managed identity, use the [az identity delete](/cli/azure/identity#az-identity-delete) command.</span></span>  <span data-ttu-id="f097b-129">The -n parameter specifies its name and the -g parameter specifies the resource group where the user-assigned managed identity was created.</span><span class="sxs-lookup"><span data-stu-id="f097b-129">The -n parameter specifies its name and the -g parameter specifies the resource group where the user-assigned managed identity was created.</span></span> <span data-ttu-id="f097b-130">Replace the `<USER ASSIGNED IDENTITY NAME>` and `<RESOURCE GROUP>` parameters values with your own values:</span><span class="sxs-lookup"><span data-stu-id="f097b-130">Replace the `<USER ASSIGNED IDENTITY NAME>` and `<RESOURCE GROUP>` parameters values with your own values:</span></span>

 ```azurecli-interactive
az identity delete -n <USER ASSIGNED IDENTITY NAME> -g <RESOURCE GROUP>
```
> [!NOTE]
> <span data-ttu-id="f097b-131">Deleting a user-assigned managed identity will not remove the reference, from any resource it was assigned to.</span><span class="sxs-lookup"><span data-stu-id="f097b-131">Deleting a user-assigned managed identity will not remove the reference, from any resource it was assigned to.</span></span> <span data-ttu-id="f097b-132">Please remove those from VM/VMSS using the `az vm/vmss identity remove` command</span><span class="sxs-lookup"><span data-stu-id="f097b-132">Please remove those from VM/VMSS using the `az vm/vmss identity remove` command</span></span>

## <a name="next-steps"></a><span data-ttu-id="f097b-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="f097b-133">Next steps</span></span>

<span data-ttu-id="f097b-134">For a full list of Azure CLI identity commands, see [az identity](/cli/azure/identity).</span><span class="sxs-lookup"><span data-stu-id="f097b-134">For a full list of Azure CLI identity commands, see [az identity](/cli/azure/identity).</span></span>

<span data-ttu-id="f097b-135">For information on how to assign a user-assigned managed identity to an Azure VM see, [Configure managed identities for Azure resources on an Azure VM using Azure CLI](qs-configure-cli-windows-vm.md#user-assigned-managed-identity)</span><span class="sxs-lookup"><span data-stu-id="f097b-135">For information on how to assign a user-assigned managed identity to an Azure VM see, [Configure managed identities for Azure resources on an Azure VM using Azure CLI](qs-configure-cli-windows-vm.md#user-assigned-managed-identity)</span></span>


 
