---
title: How to create, list and delete a user-assigned managed identity using Azure PowerShell
description: Step by step instructions on how to create, list and delete user-assigned managed identity using Azure PowerShell.
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
ms.openlocfilehash: c7191f60b8780e8ccee9b330aa21d8174f0f0148
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867836"
---
# <a name="create-list-or-delete-a-user-assigned-managed-identity-using-azure-powershell"></a><span data-ttu-id="cd2a4-103">Create, list or delete a user-assigned managed identity using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd2a4-103">Create, list or delete a user-assigned managed identity using Azure PowerShell</span></span>

[!INCLUDE [preview-notice](~/includes/active-directory-msi-preview-notice-ua.md)]

<span data-ttu-id="cd2a4-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-104">Managed identities for Azure resources provides Azure services with a managed identity in Azure Active Directory.</span></span> <span data-ttu-id="cd2a4-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-105">You can use this identity to authenticate to services that support Azure AD authentication, without needing credentials in your code.</span></span> 

<span data-ttu-id="cd2a4-106">In this article, you learn how to create, list and delete a user-assigned managed identity using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-106">In this article, you learn how to create, list and delete a user-assigned managed identity using Azure PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd2a4-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cd2a4-107">Prerequisites</span></span>

- <span data-ttu-id="cd2a4-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd2a4-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="cd2a4-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="cd2a4-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="cd2a4-111">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-111">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span></span>
- <span data-ttu-id="cd2a4-112">If you choose to install and use PowerShell locally, this tutorial requires Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-112">If you choose to install and use PowerShell locally, this tutorial requires Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="cd2a4-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-113">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="cd2a4-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="cd2a4-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> 
- <span data-ttu-id="cd2a4-115">If you are running PowerShell locally, you also need to:</span><span class="sxs-lookup"><span data-stu-id="cd2a4-115">If you are running PowerShell locally, you also need to:</span></span> 
    - <span data-ttu-id="cd2a4-116">Run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-116">Run `Login-AzureRmAccount` to create a connection with Azure.</span></span>
    - <span data-ttu-id="cd2a4-117">Install the [latest version of PowerShellGet](/powershell/gallery/installing-psget#for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget).</span><span class="sxs-lookup"><span data-stu-id="cd2a4-117">Install the [latest version of PowerShellGet](/powershell/gallery/installing-psget#for-systems-with-powershell-50-or-newer-you-can-install-the-latest-powershellget).</span></span>
    - <span data-ttu-id="cd2a4-118">Run `Install-Module -Name PowerShellGet -AllowPrerelease` to get the pre-release version of the `PowerShellGet` module (you may need to `Exit` out of the current PowerShell session after you run this command to install the `AzureRM.ManagedServiceIdentity` module).</span><span class="sxs-lookup"><span data-stu-id="cd2a4-118">Run `Install-Module -Name PowerShellGet -AllowPrerelease` to get the pre-release version of the `PowerShellGet` module (you may need to `Exit` out of the current PowerShell session after you run this command to install the `AzureRM.ManagedServiceIdentity` module).</span></span>
    - <span data-ttu-id="cd2a4-119">Run `Install-Module -Name AzureRM.ManagedServiceIdentity -AllowPrerelease` to install the prerelease version of the `AzureRM.ManagedServiceIdentity` module to perform the user-assigned managed identity operations in this article.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-119">Run `Install-Module -Name AzureRM.ManagedServiceIdentity -AllowPrerelease` to install the prerelease version of the `AzureRM.ManagedServiceIdentity` module to perform the user-assigned managed identity operations in this article.</span></span>
- <span data-ttu-id="cd2a4-120">To perform the management operations in this article, your account needs the following role assignments:</span><span class="sxs-lookup"><span data-stu-id="cd2a4-120">To perform the management operations in this article, your account needs the following role assignments:</span></span>
    - <span data-ttu-id="cd2a4-121">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-121">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create, read (list), update, and delete a user-assigned managed identity.</span></span>
    - <span data-ttu-id="cd2a4-122">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-122">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to read (list) the properties of a user-assigned managed identity.</span></span>

## <a name="create-a-user-assigned-managed-identity"></a><span data-ttu-id="cd2a4-123">Create a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="cd2a4-123">Create a user-assigned managed identity</span></span>

<span data-ttu-id="cd2a4-124">To create a user-assigned managed identity, use the [New-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/new-azurermuserassignedidentity) command.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-124">To create a user-assigned managed identity, use the [New-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/new-azurermuserassignedidentity) command.</span></span> <span data-ttu-id="cd2a4-125">The `ResourceGroupName` parameter specifies the resource group where to create the user-assigned managed identity, and the `-Name` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-125">The `ResourceGroupName` parameter specifies the resource group where to create the user-assigned managed identity, and the `-Name` parameter specifies its name.</span></span> <span data-ttu-id="cd2a4-126">Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span><span class="sxs-lookup"><span data-stu-id="cd2a4-126">Replace the `<RESOURCE GROUP>` and `<USER ASSIGNED IDENTITY NAME>` parameter values with your own values:</span></span>

[!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

 ```azurepowershell-interactive
New-AzureRmUserAssignedIdentity -ResourceGroupName <RESOURCEGROUP> -Name <USER ASSIGNED IDENTITY NAME>
```
## <a name="list-user-assigned-managed-identities"></a><span data-ttu-id="cd2a4-127">List user-assigned managed identities</span><span class="sxs-lookup"><span data-stu-id="cd2a4-127">List user-assigned managed identities</span></span>

<span data-ttu-id="cd2a4-128">To list user-assigned managed identities, use the [Get-AzureRmUserAssigned](/powershell/module/azurerm.managedserviceidentity/get-azurermuserassignedidentity) command.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-128">To list user-assigned managed identities, use the [Get-AzureRmUserAssigned](/powershell/module/azurerm.managedserviceidentity/get-azurermuserassignedidentity) command.</span></span>  <span data-ttu-id="cd2a4-129">The `-ResourceGroupName` parameter specifies the resource group where the user-assigned managed identity was created.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-129">The `-ResourceGroupName` parameter specifies the resource group where the user-assigned managed identity was created.</span></span> <span data-ttu-id="cd2a4-130">Replace the `<RESOURCE GROUP>` with your own value:</span><span class="sxs-lookup"><span data-stu-id="cd2a4-130">Replace the `<RESOURCE GROUP>` with your own value:</span></span>

```azurepowershell-interactive
Get-AzureRmUserAssignedIdentity -ResourceGroupName <RESOURCE GROUP>
```
<span data-ttu-id="cd2a4-131">In the response, user-assigned managed identities have `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for key, `Type`.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-131">In the response, user-assigned managed identities have `"Microsoft.ManagedIdentity/userAssignedIdentities"` value returned for key, `Type`.</span></span>

`Type :Microsoft.ManagedIdentity/userAssignedIdentities`

## <a name="delete-a-user-assigned-managed-identity"></a><span data-ttu-id="cd2a4-132">Delete a user-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="cd2a4-132">Delete a user-assigned managed identity</span></span>

<span data-ttu-id="cd2a4-133">To delete a user-assigned managed identity, use the [Remove-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/remove-azurermuserassignedidentity) command.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-133">To delete a user-assigned managed identity, use the [Remove-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/remove-azurermuserassignedidentity) command.</span></span>  <span data-ttu-id="cd2a4-134">The `-ResourceGroupName` parameter specifies the resource group where the user-assigned identity was created and the `-Name` parameter specifies its name.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-134">The `-ResourceGroupName` parameter specifies the resource group where the user-assigned identity was created and the `-Name` parameter specifies its name.</span></span> <span data-ttu-id="cd2a4-135">Replace the `<RESOURCE GROUP>` and the `<USER ASSIGNED IDENTITY NAME>` parameters values with your own values:</span><span class="sxs-lookup"><span data-stu-id="cd2a4-135">Replace the `<RESOURCE GROUP>` and the `<USER ASSIGNED IDENTITY NAME>` parameters values with your own values:</span></span>

 ```azurepowershell-interactive
Remove-AzurRmUserAssignedIdentity -ResourceGroupName <RESOURCE GROUP> -Name <USER ASSIGNED IDENTITY NAME>
```
> [!NOTE]
> <span data-ttu-id="cd2a4-136">Deleting a user-assigned managed identity will not remove the reference, from any resource it was assigned to.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-136">Deleting a user-assigned managed identity will not remove the reference, from any resource it was assigned to.</span></span> <span data-ttu-id="cd2a4-137">Identity assignments need to be removed separately.</span><span class="sxs-lookup"><span data-stu-id="cd2a4-137">Identity assignments need to be removed separately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd2a4-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd2a4-138">Next steps</span></span>

<span data-ttu-id="cd2a4-139">For a full list and more details of the Azure PowerShell managed identities for Azure resources commands, see [AzureRM.ManagedServiceIdentity](/powershell/module/azurerm.managedserviceidentity#managed_service_identity).</span><span class="sxs-lookup"><span data-stu-id="cd2a4-139">For a full list and more details of the Azure PowerShell managed identities for Azure resources commands, see [AzureRM.ManagedServiceIdentity](/powershell/module/azurerm.managedserviceidentity#managed_service_identity).</span></span>
