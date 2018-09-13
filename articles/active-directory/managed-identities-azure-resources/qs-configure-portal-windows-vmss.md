---
title: How to configure managed Identities for Azure resources on a virtual machine scale set
description: Step by step instructions for configuring managed identities for Azure resources on a virtual machine scale set using the Azure portal.
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
ms.date: 02/20/2018
ms.author: daveba
ms.openlocfilehash: 0a6440b7fffe1aec26ba4755f21fa2f56935887e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856904"
---
# <a name="configure-managed-identities-for-azure-resources-on-a-virtual-machine-scale-set-using-the-azure-portal"></a><span data-ttu-id="f96d7-103">Configure managed identities for Azure resources on a virtual machine scale set using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f96d7-103">Configure managed identities for Azure resources on a virtual machine scale set using the Azure portal</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="f96d7-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f96d7-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="f96d7-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="f96d7-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="f96d7-106">In this article, using PowerShell, you learn how to perform the following managed identities for Azure resources operations on a virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="f96d7-106">In this article, using PowerShell, you learn how to perform the following managed identities for Azure resources operations on a virtual machine scale set:</span></span>

- <span data-ttu-id="f96d7-107">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f96d7-107">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span>
- <span data-ttu-id="f96d7-108">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="f96d7-108">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="f96d7-109">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="f96d7-109">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="f96d7-110">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="f96d7-110">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="f96d7-111">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to enable and remove system-assigned managed identity from a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-111">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to enable and remove system-assigned managed identity from a virtual machine scale set.</span></span>

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="f96d7-112">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f96d7-112">System-assigned managed identity</span></span>

<span data-ttu-id="f96d7-113">In this section, you will learn how to enable and disable the system-assigned managed identity using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f96d7-113">In this section, you will learn how to enable and disable the system-assigned managed identity using the Azure portal.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-a-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-114">Enable system-assigned managed identity during creation of a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-114">Enable system-assigned managed identity during creation of a virtual machine scale set</span></span>

<span data-ttu-id="f96d7-115">Currently, the Azure portal does not support enabling system-assigned managed identity during the creation of a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-115">Currently, the Azure portal does not support enabling system-assigned managed identity during the creation of a virtual machine scale set.</span></span> <span data-ttu-id="f96d7-116">Instead, refer to the following virtual machine scale set creation Quickstart article to first create a virtual machine scale set, and then proceed to the next section for details on enabling system-assigned managed identity on a virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="f96d7-116">Instead, refer to the following virtual machine scale set creation Quickstart article to first create a virtual machine scale set, and then proceed to the next section for details on enabling system-assigned managed identity on a virtual machine scale set:</span></span>

- [<span data-ttu-id="f96d7-117">Create a Virtual Machine Scale Set in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f96d7-117">Create a Virtual Machine Scale Set in the Azure portal</span></span>](../../virtual-machine-scale-sets/quick-create-portal.md)  

### <a name="enable-system-assigned-managed-identity-on-an-existing-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-118">Enable system-assigned managed identity on an existing virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-118">Enable system-assigned managed identity on an existing virtual machine scale set</span></span>

<span data-ttu-id="f96d7-119">To enable the system-assigned managed identity on a virtual machine scale set that was originally provisioned without it:</span><span class="sxs-lookup"><span data-stu-id="f96d7-119">To enable the system-assigned managed identity on a virtual machine scale set that was originally provisioned without it:</span></span>

1. <span data-ttu-id="f96d7-120">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-120">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span></span>

2. <span data-ttu-id="f96d7-121">Navigate to the desired virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-121">Navigate to the desired virtual machine scale set.</span></span>

3. <span data-ttu-id="f96d7-122">Under **System assigned**, **Status**, select **On** and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="f96d7-122">Under **System assigned**, **Status**, select **On** and then click **Save**:</span></span>

   ![Configuration page screenshot](./media/msi-qs-configure-portal-windows-vmss/create-windows-vmss-portal-configuration-blade.png)<span data-ttu-id="f96d7-124">](./media/msi-qs-configure-portal-windows-vmss/create-windows-vmss-portal-configuration-blade.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="f96d7-124">](./media/msi-qs-configure-portal-windows-vmss/create-windows-vmss-portal-configuration-blade.png#lightbox)</span></span>  

### <a name="remove-system-assigned-managed-identity-from-a-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-125">Remove system-assigned managed identity from a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-125">Remove system-assigned managed identity from a virtual machine scale set</span></span>

<span data-ttu-id="f96d7-126">If you have a virtual machine scale set that no longer needs a system-assigned managed identity:</span><span class="sxs-lookup"><span data-stu-id="f96d7-126">If you have a virtual machine scale set that no longer needs a system-assigned managed identity:</span></span>

1. <span data-ttu-id="f96d7-127">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-127">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span></span> <span data-ttu-id="f96d7-128">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-128">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set.</span></span>

2. <span data-ttu-id="f96d7-129">Navigate to the desired virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-129">Navigate to the desired virtual machine scale set.</span></span>

3. <span data-ttu-id="f96d7-130">Under **System assigned**, **Status**, select **Off** and then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="f96d7-130">Under **System assigned**, **Status**, select **Off** and then click **Save**:</span></span>

   ![Configuration page screenshot](./media/msi-qs-configure-portal-windows-vmss/disable-windows-vmss-portal-configuration-blade.png)

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="f96d7-132">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f96d7-132">User-assigned managed identity</span></span>

<span data-ttu-id="f96d7-133">In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f96d7-133">In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using the Azure portal.</span></span>

### <a name="assign-a-user-assigned-managed-identity-during-the-creation-of-a-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-134">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-134">Assign a user-assigned managed identity during the creation of a virtual machine scale set</span></span>

<span data-ttu-id="f96d7-135">Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-135">Currently, the Azure portal does not support assigning a user-assigned managed identity during the creation of a virtual machine scale set.</span></span> <span data-ttu-id="f96d7-136">Instead, refer to the following virtual machine scale set creation Quickstart article to first create a virtual machine scale set, and then proceed to the next section for details on assigning a user-assigned managed identity to it:</span><span class="sxs-lookup"><span data-stu-id="f96d7-136">Instead, refer to the following virtual machine scale set creation Quickstart article to first create a virtual machine scale set, and then proceed to the next section for details on assigning a user-assigned managed identity to it:</span></span>

- [<span data-ttu-id="f96d7-137">Create a Virtual Machine Scale Set in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f96d7-137">Create a Virtual Machine Scale Set in the Azure portal</span></span>](../../virtual-machine-scale-sets/quick-create-portal.md)

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-138">Assign a user-assigned managed identity to an existing virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-138">Assign a user-assigned managed identity to an existing virtual machine scale set</span></span>

1. <span data-ttu-id="f96d7-139">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f96d7-139">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the virtual machine scale set.</span></span>
2. <span data-ttu-id="f96d7-140">Navigate to the desired virtual machine scale set and click **Identity**, **User assigned** and then **\+Add**.</span><span class="sxs-lookup"><span data-stu-id="f96d7-140">Navigate to the desired virtual machine scale set and click **Identity**, **User assigned** and then **\+Add**.</span></span>

   ![Add user-assigned identity to VMSS](./media/msi-qs-configure-portal-windows-vm/add-user-assigned-identity-vmss-screenshot1.png)

3. <span data-ttu-id="f96d7-142">Click the user-assigned identity you want to add to the virtual machine scale set and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f96d7-142">Click the user-assigned identity you want to add to the virtual machine scale set and then click **Add**.</span></span>
   
   ![Add user-assigned identity to VMSS](./media/msi-qs-configure-portal-windows-vm/add-user-assigned-identity-vm-screenshot2.png)

### <a name="remove-a-user-assigned-managed-identity-from-a-virtual-machine-scale-set"></a><span data-ttu-id="f96d7-144">Remove a user-assigned managed identity from a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f96d7-144">Remove a user-assigned managed identity from a virtual machine scale set</span></span>

1. <span data-ttu-id="f96d7-145">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="f96d7-145">Sign in to the [Azure portal](https://portal.azure.com) using an account associated with the Azure subscription that contains the VM.</span></span>
2. <span data-ttu-id="f96d7-146">Navigate to the desired virtual machine scale set and click **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).</span><span class="sxs-lookup"><span data-stu-id="f96d7-146">Navigate to the desired virtual machine scale set and click **Identity**, **User assigned**, the name of the user-assigned managed identity you want to delete and then click **Remove** (click **Yes** in the confirmation pane).</span></span>

   ![Remove user-assigned identity from a VMSS](./media/msi-qs-configure-portal-windows-vm/remove-user-assigned-identity-vmss-screenshot.png)


## <a name="next-steps"></a><span data-ttu-id="f96d7-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="f96d7-148">Next steps</span></span>

- <span data-ttu-id="f96d7-149">Using the Azure portal, give an Azure virtual machine scale set managed identity [access to another Azure resource](howto-assign-access-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f96d7-149">Using the Azure portal, give an Azure virtual machine scale set managed identity [access to another Azure resource](howto-assign-access-portal.md).</span></span>


