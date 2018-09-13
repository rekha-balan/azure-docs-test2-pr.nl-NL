---
title: Delete a lab or VM in a lab in Azure DevTest Labs | Microsoft Docs
description: This article shows you how to delete a lab or VM in a lab.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2018
ms.author: spelluru
ms.openlocfilehash: 99caf04698226de8daa9cfb8f60662e5cb0f8b49
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857571"
---
# <a name="delete-a-lab-or-vm-in-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="0f75d-103">Delete a lab or VM in a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="0f75d-103">Delete a lab or VM in a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="0f75d-104">This article shows you how to delete a lab or VM in a lab.</span><span class="sxs-lookup"><span data-stu-id="0f75d-104">This article shows you how to delete a lab or VM in a lab.</span></span>

## <a name="delete-a-lab"></a><span data-ttu-id="0f75d-105">Delete a lab</span><span class="sxs-lookup"><span data-stu-id="0f75d-105">Delete a lab</span></span>
<span data-ttu-id="0f75d-106">When you delete a DevTest Labs instance from a resource group, the DevTest Labs service performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f75d-106">When you delete a DevTest Labs instance from a resource group, the DevTest Labs service performs the following actions:</span></span> 

- <span data-ttu-id="0f75d-107">All the resources that were automatically created at the time of lab creation are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="0f75d-107">All the resources that were automatically created at the time of lab creation are automatically deleted.</span></span> <span data-ttu-id="0f75d-108">The resource group itself is not deleted.</span><span class="sxs-lookup"><span data-stu-id="0f75d-108">The resource group itself is not deleted.</span></span> <span data-ttu-id="0f75d-109">If you had manually created any resources this resource group, the service doesn't delete them.</span><span class="sxs-lookup"><span data-stu-id="0f75d-109">If you had manually created any resources this resource group, the service doesn't delete them.</span></span> 
- <span data-ttu-id="0f75d-110">All VMs in the lab and resource groups associated with these VMs are automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="0f75d-110">All VMs in the lab and resource groups associated with these VMs are automatically deleted.</span></span> <span data-ttu-id="0f75d-111">When you create a VM in a lab, the service creates resources (disk, network interface, public IP address, etc.) for the VM in a separate resource group.</span><span class="sxs-lookup"><span data-stu-id="0f75d-111">When you create a VM in a lab, the service creates resources (disk, network interface, public IP address, etc.) for the VM in a separate resource group.</span></span> <span data-ttu-id="0f75d-112">However, if you manually create any additional resources in these resource groups, the DevTest Labs service does not delete those resources and the resource group.</span><span class="sxs-lookup"><span data-stu-id="0f75d-112">However, if you manually create any additional resources in these resource groups, the DevTest Labs service does not delete those resources and the resource group.</span></span> 

<span data-ttu-id="0f75d-113">To delete a lab, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f75d-113">To delete a lab, do the following actions:</span></span> 

1. <span data-ttu-id="0f75d-114">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f75d-114">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f75d-115">Select **All resource** from menu on the left, select **DevTest Labs** for the type of service, and select the lab.</span><span class="sxs-lookup"><span data-stu-id="0f75d-115">Select **All resource** from menu on the left, select **DevTest Labs** for the type of service, and select the lab.</span></span>

    ![Select your lab](media\devtest-lab-delete-lab-vm\select-lab.png)
3. <span data-ttu-id="0f75d-117">On the **DevTest Lab** page, click **Delete** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="0f75d-117">On the **DevTest Lab** page, click **Delete** on the toolbar.</span></span> 

    ![Delete button](media\devtest-lab-delete-lab-vm\delete-button.png)
4. <span data-ttu-id="0f75d-119">On the **Confirmation** page, enter the **name** of your lab, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0f75d-119">On the **Confirmation** page, enter the **name** of your lab, and select **Delete**.</span></span> 

    ![Confirm](media\devtest-lab-delete-lab-vm\confirm-delete.png)
5. <span data-ttu-id="0f75d-121">To see the status of the operation, select **Notifications** icon (Bell).</span><span class="sxs-lookup"><span data-stu-id="0f75d-121">To see the status of the operation, select **Notifications** icon (Bell).</span></span> 

    ![Notifications](media\devtest-lab-delete-lab-vm\delete-status.png)

 
## <a name="delete-a-vm-in-a-lab"></a><span data-ttu-id="0f75d-123">Delete a VM in a lab</span><span class="sxs-lookup"><span data-stu-id="0f75d-123">Delete a VM in a lab</span></span>
<span data-ttu-id="0f75d-124">If I delete a VM in a lab, some of the resources (not all) that were created at the time of lab creation are deleted.</span><span class="sxs-lookup"><span data-stu-id="0f75d-124">If I delete a VM in a lab, some of the resources (not all) that were created at the time of lab creation are deleted.</span></span> <span data-ttu-id="0f75d-125">The following resources are not deleted:</span><span class="sxs-lookup"><span data-stu-id="0f75d-125">The following resources are not deleted:</span></span> 

-   <span data-ttu-id="0f75d-126">Key vault in the main resource group</span><span class="sxs-lookup"><span data-stu-id="0f75d-126">Key vault in the main resource group</span></span>
-   <span data-ttu-id="0f75d-127">Availability set, load balancer, public IP address in the VM resource group.</span><span class="sxs-lookup"><span data-stu-id="0f75d-127">Availability set, load balancer, public IP address in the VM resource group.</span></span> <span data-ttu-id="0f75d-128">These resources are shared by multiple VMs in a resource group.</span><span class="sxs-lookup"><span data-stu-id="0f75d-128">These resources are shared by multiple VMs in a resource group.</span></span> 

<span data-ttu-id="0f75d-129">Virtual machine, network interface, and disk associated with the VM are deleted.</span><span class="sxs-lookup"><span data-stu-id="0f75d-129">Virtual machine, network interface, and disk associated with the VM are deleted.</span></span> 

<span data-ttu-id="0f75d-130">To delete a VM in a lab, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="0f75d-130">To delete a VM in a lab, do the following actions:</span></span> 

1. <span data-ttu-id="0f75d-131">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f75d-131">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f75d-132">Select **All resource** from menu on the left, select **DevTest Labs** for the type of service, and select the lab.</span><span class="sxs-lookup"><span data-stu-id="0f75d-132">Select **All resource** from menu on the left, select **DevTest Labs** for the type of service, and select the lab.</span></span>

    ![Select your lab](media\devtest-lab-delete-lab-vm\select-lab.png)
3. <span data-ttu-id="0f75d-134">Select **... (ellipsis)** for the VM in the list of VMs, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0f75d-134">Select **... (ellipsis)** for the VM in the list of VMs, and select **Delete**.</span></span> 

    ![Delete VM in menu](media\devtest-lab-delete-lab-vm\delete-vm-menu-in-list.png)
4. <span data-ttu-id="0f75d-136">On the **confirmation** dialog box, select **Ok**.</span><span class="sxs-lookup"><span data-stu-id="0f75d-136">On the **confirmation** dialog box, select **Ok**.</span></span> 
5. <span data-ttu-id="0f75d-137">To see the status of the operation, select **Notifications** icon (Bell).</span><span class="sxs-lookup"><span data-stu-id="0f75d-137">To see the status of the operation, select **Notifications** icon (Bell).</span></span> 

<span data-ttu-id="0f75d-138">To delete a VM from the **Virtual Machine page**, select **Delete** from the toolbar as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="0f75d-138">To delete a VM from the **Virtual Machine page**, select **Delete** from the toolbar as shown in the following image:</span></span>

![Delete VM from VM page](media\devtest-lab-delete-lab-vm\delete-from-vm-page.png) 


## <a name="next-steps"></a><span data-ttu-id="0f75d-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f75d-140">Next steps</span></span>
<span data-ttu-id="0f75d-141">If you want to create a lab, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="0f75d-141">If you want to create a lab, see the following articles:</span></span> 

- [<span data-ttu-id="0f75d-142">Create a lab</span><span class="sxs-lookup"><span data-stu-id="0f75d-142">Create a lab</span></span>](devtest-lab-create-lab.md)
- [<span data-ttu-id="0f75d-143">Add a VM to the lab</span><span class="sxs-lookup"><span data-stu-id="0f75d-143">Add a VM to the lab</span></span>](devtest-lab-add-vm.md)