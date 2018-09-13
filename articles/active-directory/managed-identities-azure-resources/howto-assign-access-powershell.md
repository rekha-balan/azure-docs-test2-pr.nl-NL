---
title: How to assign an MSI access to an Azure resource, using PowerShell
description: Step by step instructions for assigning an MSI on one resource, access to another resource, using PowerShell.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 09/14/2017
ms.author: daveba
ms.openlocfilehash: 936d549469df2cf4c303f0c3fd185f07281bb69b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869100"
---
# <a name="assign-a-managed-service-identity-msi-access-to-a-resource-using-powershell"></a><span data-ttu-id="908db-103">Assign a Managed Service Identity (MSI) access to a resource using PowerShell</span><span class="sxs-lookup"><span data-stu-id="908db-103">Assign a Managed Service Identity (MSI) access to a resource using PowerShell</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="908db-104">Once you've configured an Azure resource with an MSI, you can give the MSI access to another resource, just like any security principal.</span><span class="sxs-lookup"><span data-stu-id="908db-104">Once you've configured an Azure resource with an MSI, you can give the MSI access to another resource, just like any security principal.</span></span> <span data-ttu-id="908db-105">This example shows you how to give an Azure virtual machine's MSI access to an Azure storage account, using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="908db-105">This example shows you how to give an Azure virtual machine's MSI access to an Azure storage account, using PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="908db-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="908db-106">Prerequisites</span></span>

[!INCLUDE [msi-qs-configure-prereqs](../../../includes/active-directory-msi-qs-configure-prereqs.md)]

<span data-ttu-id="908db-107">Also, install [Azure PowerShell version 4.3.1](https://www.powershellgallery.com/packages/AzureRM/4.3.1) if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="908db-107">Also, install [Azure PowerShell version 4.3.1](https://www.powershellgallery.com/packages/AzureRM/4.3.1) if you haven't already.</span></span>

## <a name="use-rbac-to-assign-the-msi-access-to-another-resource"></a><span data-ttu-id="908db-108">Use RBAC to assign the MSI access to another resource</span><span class="sxs-lookup"><span data-stu-id="908db-108">Use RBAC to assign the MSI access to another resource</span></span>

<span data-ttu-id="908db-109">After you've enabled MSI on an Azure resource, [such as an Azure VM](qs-configure-powershell-windows-vm.md):</span><span class="sxs-lookup"><span data-stu-id="908db-109">After you've enabled MSI on an Azure resource, [such as an Azure VM](qs-configure-powershell-windows-vm.md):</span></span>

1. <span data-ttu-id="908db-110">Sign in to Azure using the `Connect-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="908db-110">Sign in to Azure using the `Connect-AzureRmAccount` cmdlet.</span></span> <span data-ttu-id="908db-111">Use an account that is associated with the Azure subscription under which you have configured the MSI:</span><span class="sxs-lookup"><span data-stu-id="908db-111">Use an account that is associated with the Azure subscription under which you have configured the MSI:</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```
2. <span data-ttu-id="908db-112">In this example, we are giving an Azure VM access to a storage account.</span><span class="sxs-lookup"><span data-stu-id="908db-112">In this example, we are giving an Azure VM access to a storage account.</span></span> <span data-ttu-id="908db-113">First we use [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm) to get the service principal for the VM named "myVM", which was created when we enabled MSI.</span><span class="sxs-lookup"><span data-stu-id="908db-113">First we use [Get-AzureRMVM](/powershell/module/azurerm.compute/get-azurermvm) to get the service principal for the VM named "myVM", which was created when we enabled MSI.</span></span> <span data-ttu-id="908db-114">Then, we use [New-AzureRmRoleAssignment](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment) to give the VM "Reader" access to a storage account called "myStorageAcct":</span><span class="sxs-lookup"><span data-stu-id="908db-114">Then, we use [New-AzureRmRoleAssignment](/powershell/module/AzureRM.Resources/New-AzureRmRoleAssignment) to give the VM "Reader" access to a storage account called "myStorageAcct":</span></span>

    ```powershell
    $spID = (Get-AzureRMVM -ResourceGroupName myRG -Name myVM).identity.principalid
    New-AzureRmRoleAssignment -ObjectId $spID -RoleDefinitionName "Reader" -Scope "/subscriptions/<mySubscriptionID>/resourceGroups/<myResourceGroup>/providers/Microsoft.Storage/storageAccounts/<myStorageAcct>"
    ```

## <a name="troubleshooting"></a><span data-ttu-id="908db-115">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="908db-115">Troubleshooting</span></span>

<span data-ttu-id="908db-116">If the MSI for the resource does not show up in the list of available identities, verify that the MSI has been enabled correctly.</span><span class="sxs-lookup"><span data-stu-id="908db-116">If the MSI for the resource does not show up in the list of available identities, verify that the MSI has been enabled correctly.</span></span> <span data-ttu-id="908db-117">In our case, we can go back to the Azure VM in the [Azure portal](https://portal.azure.com) and:</span><span class="sxs-lookup"><span data-stu-id="908db-117">In our case, we can go back to the Azure VM in the [Azure portal](https://portal.azure.com) and:</span></span>

- <span data-ttu-id="908db-118">Look at the "Configuration" page and ensure MSI enabled = "Yes."</span><span class="sxs-lookup"><span data-stu-id="908db-118">Look at the "Configuration" page and ensure MSI enabled = "Yes."</span></span>
- <span data-ttu-id="908db-119">Look at the "Extensions" page and ensure the MSI extension deployed successfully.</span><span class="sxs-lookup"><span data-stu-id="908db-119">Look at the "Extensions" page and ensure the MSI extension deployed successfully.</span></span>

<span data-ttu-id="908db-120">If either is incorrect, you may need to redeploy the MSI on your resource again, or troubleshoot the deployment failure.</span><span class="sxs-lookup"><span data-stu-id="908db-120">If either is incorrect, you may need to redeploy the MSI on your resource again, or troubleshoot the deployment failure.</span></span>

## <a name="related-content"></a><span data-ttu-id="908db-121">Related content</span><span class="sxs-lookup"><span data-stu-id="908db-121">Related content</span></span>

- <span data-ttu-id="908db-122">For an overview of MSI, see [Managed Service Identity overview](overview.md).</span><span class="sxs-lookup"><span data-stu-id="908db-122">For an overview of MSI, see [Managed Service Identity overview](overview.md).</span></span>
- <span data-ttu-id="908db-123">To enable MSI on an Azure VM, see [Configure an Azure VM Managed Service Identity (MSI) using PowerShell](qs-configure-powershell-windows-vm.md).</span><span class="sxs-lookup"><span data-stu-id="908db-123">To enable MSI on an Azure VM, see [Configure an Azure VM Managed Service Identity (MSI) using PowerShell](qs-configure-powershell-windows-vm.md).</span></span>

<span data-ttu-id="908db-124">Use the following comments section to provide feedback and help us refine and shape our content.</span><span class="sxs-lookup"><span data-stu-id="908db-124">Use the following comments section to provide feedback and help us refine and shape our content.</span></span>

