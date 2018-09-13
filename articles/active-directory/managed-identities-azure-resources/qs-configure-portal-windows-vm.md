---
title: How to configure managed Identities for Azure resources on an Azure VM using the Azure portal
description: Step by step instructions for configuring managed identities for Azure resources on an Azure VM using the Azure portal.
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
ms.date: 09/19/2017
ms.author: daveba
ms.openlocfilehash: 77953884253002c6da7b0151151d97bb65a6c659
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857856"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-vm-using-the-azure-portal"></a><span data-ttu-id="bc060-103">Configure managed identities for Azure resources on a VM using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc060-103">Configure managed identities for Azure resources on a VM using the Azure portal</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="bc060-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bc060-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="bc060-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="bc060-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="bc060-106">In this article, you learn how to enable and disable system and user-assigned managed identities for an Azure Virtual Machine (VM), using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc060-106">In this article, you learn how to enable and disable system and user-assigned managed identities for an Azure Virtual Machine (VM), using the Azure portal.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bc060-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc060-107">Prerequisites</span></span>

- <span data-ttu-id="bc060-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc060-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span>
- <span data-ttu-id="bc060-109">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="bc060-109">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="bc060-110">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="bc060-110">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="bc060-111">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="bc060-111">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="bc060-112">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to enable and remove system-assigned managed identity from an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-112">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to enable and remove system-assigned managed identity from an Azure VM.</span></span>

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="bc060-113">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="bc060-113">System-assigned managed identity</span></span>

<span data-ttu-id="bc060-114">In this section, you learn how to enable and disable the system-assigned managed identity for VM using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc060-114">In this section, you learn how to enable and disable the system-assigned managed identity for VM using the Azure portal.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-a-vm"></a><span data-ttu-id="bc060-115">Enable system-assigned managed identity during creation of a VM</span><span class="sxs-lookup"><span data-stu-id="bc060-115">Enable system-assigned managed identity during creation of a VM</span></span>

<span data-ttu-id="bc060-116">Currently, the Azure portal does not support enabling system-assigned identity during the creation of a VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-116">Currently, the Azure portal does not support enabling system-assigned identity during the creation of a VM.</span></span> <span data-ttu-id="bc060-117">Instead, refer to one of the following VM creation Quickstart articles to first create a VM, and then proceed to the next section for details on enabling system-assigned identity on the VM:</span><span class="sxs-lookup"><span data-stu-id="bc060-117">Instead, refer to one of the following VM creation Quickstart articles to first create a VM, and then proceed to the next section for details on enabling system-assigned identity on the VM:</span></span>

- [<span data-ttu-id="bc060-118">Create a Windows virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc060-118">Create a Windows virtual machine with the Azure portal</span></span>](../../virtual-machines/windows/quick-create-portal.md#create-virtual-machine)
- [<span data-ttu-id="bc060-119">Create a Linux virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc060-119">Create a Linux virtual machine with the Azure portal</span></span>](../../virtual-machines/linux/quick-create-portal.md#create-virtual-machine)  

### <a name="enable-system-assigned-managed-identity-on-an-existing-vm"></a><span data-ttu-id="bc060-120">Enable system-assigned managed identity on an existing VM</span><span class="sxs-lookup"><span data-stu-id="bc060-120">Enable system-assigned managed identity on an existing VM</span></span>

<span data-ttu-id="bc060-121">To enable the system-assigned managed identity on a VM that was originally provisioned without it:</span><span class="sxs-lookup"><span data-stu-id="bc060-121">To enable the system-assigned managed identity on a VM that was originally provisioned without it:</span></span>

1. <span data-ttu-id="bc060-122">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-122">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span></span>

2. <span data-ttu-id="bc060-123">Navigate to the desired Virtual Machine and select **Identity**.</span><span class="sxs-lookup"><span data-stu-id="bc060-123">Navigate to the desired Virtual Machine and select **Identity**.</span></span>

3. <span data-ttu-id="bc060-124">Under **System assigned**, **Status**, select **On** and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="bc060-124">Under **System assigned**, **Status**, select **On** and then click **Save**:</span></span>

   ![Configuration page screenshot](./media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade.png)  

### <a name="remove-system-assigned-managed-identity-from-a-vm"></a><span data-ttu-id="bc060-126">Remove system-assigned managed identity from a VM</span><span class="sxs-lookup"><span data-stu-id="bc060-126">Remove system-assigned managed identity from a VM</span></span>

<span data-ttu-id="bc060-127">If you have a Virtual Machine that no longer needs system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="bc060-127">If you have a Virtual Machine that no longer needs system-assigned managed identity:</span></span>

1. <span data-ttu-id="bc060-128">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-128">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span></span> 

2. <span data-ttu-id="bc060-129">Navigate to the desired Virtual Machine and select **Identity**.</span><span class="sxs-lookup"><span data-stu-id="bc060-129">Navigate to the desired Virtual Machine and select **Identity**.</span></span>

3. <span data-ttu-id="bc060-130">Under **System assigned**, **Status**, select **Off** and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="bc060-130">Under **System assigned**, **Status**, select **Off** and then click **Save**:</span></span>

   ![Configuration page screenshot](./media/msi-qs-configure-portal-windows-vm/create-windows-vm-portal-configuration-blade-disable.png)

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="bc060-132">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="bc060-132">User-assigned managed identity</span></span>

 <span data-ttu-id="bc060-133">In this section, you learn how to add and remove a user-assigned managed identity from a VM using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bc060-133">In this section, you learn how to add and remove a user-assigned managed identity from a VM using the Azure portal.</span></span>

### <a name="assign-a-user-assigned-identity-during-the-creation-of-a-vm"></a><span data-ttu-id="bc060-134">Assign a user-assigned identity during the creation of a VM</span><span class="sxs-lookup"><span data-stu-id="bc060-134">Assign a user-assigned identity during the creation of a VM</span></span>

<span data-ttu-id="bc060-135">Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-135">Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a VM.</span></span> <span data-ttu-id="bc060-136">Instead, refer to one of the following VM creation Quickstart articles to first create a VM, and then proceed to the next section for details on assigning a user-assigned managed identity to the VM:</span><span class="sxs-lookup"><span data-stu-id="bc060-136">Instead, refer to one of the following VM creation Quickstart articles to first create a VM, and then proceed to the next section for details on assigning a user-assigned managed identity to the VM:</span></span>

- [<span data-ttu-id="bc060-137">Create a Windows virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc060-137">Create a Windows virtual machine with the Azure portal</span></span>](../../virtual-machines/windows/quick-create-portal.md#create-virtual-machine)
- [<span data-ttu-id="bc060-138">Create a Linux virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="bc060-138">Create a Linux virtual machine with the Azure portal</span></span>](../../virtual-machines/linux/quick-create-portal.md#create-virtual-machine)

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-vm"></a><span data-ttu-id="bc060-139">Assign a user-assigned managed identity to an existing VM</span><span class="sxs-lookup"><span data-stu-id="bc060-139">Assign a user-assigned managed identity to an existing VM</span></span>

1. <span data-ttu-id="bc060-140">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-140">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span></span>
2. <span data-ttu-id="bc060-141">Navigate to the desired VM and click **Identity**, **User assigned** and then **\+Add**.</span><span class="sxs-lookup"><span data-stu-id="bc060-141">Navigate to the desired VM and click **Identity**, **User assigned** and then **\+Add**.</span></span>

   ![Add user-assigned managed identity to VM](./media/msi-qs-configure-portal-windows-vm/add-user-assigned-identity-vm-screenshot1.png)

3. <span data-ttu-id="bc060-143">Click the user-assigned identity you want to add to the VM and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="bc060-143">Click the user-assigned identity you want to add to the VM and then click **Add**.</span></span>

    ![Add user-assigned managed identity to VM](./media/msi-qs-configure-portal-windows-vm/add-user-assigned-identity-vm-screenshot2.png)

### <a name="remove-a-user-assigned-managed-identity-from-a-vm"></a><span data-ttu-id="bc060-145">Remove a user-assigned managed identity from a VM</span><span class="sxs-lookup"><span data-stu-id="bc060-145">Remove a user-assigned managed identity from a VM</span></span>

1. <span data-ttu-id="bc060-146">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="bc060-146">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span></span>
2. <span data-ttu-id="bc060-147">Navigate to the desired VM and click **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).</span><span class="sxs-lookup"><span data-stu-id="bc060-147">Navigate to the desired VM and click **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).</span></span>

   ![Remove user-assigned managed identity from a VM](./media/msi-qs-configure-portal-windows-vm/remove-user-assigned-identity-vm-screenshot.png)

## <a name="next-steps"></a><span data-ttu-id="bc060-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc060-149">Next steps</span></span>

- <span data-ttu-id="bc060-150">Using the Azure portal, give an Azure VM's managed identity [access to another Azure resource](howto-assign-access-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bc060-150">Using the Azure portal, give an Azure VM's managed identity [access to another Azure resource](howto-assign-access-portal.md).</span></span>

