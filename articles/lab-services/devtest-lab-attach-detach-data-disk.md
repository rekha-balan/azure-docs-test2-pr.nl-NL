---
title: Attach or detach a data disk to a virtual machine in Azure DevTest Labs  | Microsoft Docs
description: Learn how to attach or detach a data disk to a virtual machine in Azure DevTest Labs
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 9616bf38-7db8-4915-a32a-e4f40a7a56ad
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 193b66cf8bdaaefed5f073bec3ecb9050d076f19
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967015"
---
# <a name="attach-or-detach-a-data-disk-to-a-virtual-machine-in-azure-devtest-labs"></a><span data-ttu-id="8fef1-103">Attach or detach a data disk to a virtual machine in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8fef1-103">Attach or detach a data disk to a virtual machine in Azure DevTest Labs</span></span>
<span data-ttu-id="8fef1-104">[Azure Managed Disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) manages the storage accounts associated with virtual machine data disks.</span><span class="sxs-lookup"><span data-stu-id="8fef1-104">[Azure Managed Disks](https://docs.microsoft.com/azure/virtual-machines/windows/managed-disks-overview) manages the storage accounts associated with virtual machine data disks.</span></span> <span data-ttu-id="8fef1-105">A user attaches a new data disk to a VM, specifies the type and size of disk that's needed, and Azure creates and manages the disk automatically.</span><span class="sxs-lookup"><span data-stu-id="8fef1-105">A user attaches a new data disk to a VM, specifies the type and size of disk that's needed, and Azure creates and manages the disk automatically.</span></span> <span data-ttu-id="8fef1-106">The data disk can then be detached from the VM and either reattached later to the same VM, or attached to a different VM that belongs to the same user.</span><span class="sxs-lookup"><span data-stu-id="8fef1-106">The data disk can then be detached from the VM and either reattached later to the same VM, or attached to a different VM that belongs to the same user.</span></span>

<span data-ttu-id="8fef1-107">This functionality is handy for managing storage or software outside of each individual virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8fef1-107">This functionality is handy for managing storage or software outside of each individual virtual machine.</span></span> <span data-ttu-id="8fef1-108">If the storage or software already exists inside a data disk, it can be easily attached, detached, and reattached to any VM that is owned by the user that owns that data disk.</span><span class="sxs-lookup"><span data-stu-id="8fef1-108">If the storage or software already exists inside a data disk, it can be easily attached, detached, and reattached to any VM that is owned by the user that owns that data disk.</span></span>

## <a name="attach-a-data-disk"></a><span data-ttu-id="8fef1-109">Attach a data disk</span><span class="sxs-lookup"><span data-stu-id="8fef1-109">Attach a data disk</span></span>
<span data-ttu-id="8fef1-110">Before you attach a data disk to a VM, review these tips:</span><span class="sxs-lookup"><span data-stu-id="8fef1-110">Before you attach a data disk to a VM, review these tips:</span></span>

- <span data-ttu-id="8fef1-111">The size of the VM controls how many data disks you can attach.</span><span class="sxs-lookup"><span data-stu-id="8fef1-111">The size of the VM controls how many data disks you can attach.</span></span> <span data-ttu-id="8fef1-112">For details, see [Sizes for virtual machines](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span><span class="sxs-lookup"><span data-stu-id="8fef1-112">For details, see [Sizes for virtual machines](https://docs.microsoft.com/azure/virtual-machines/windows/sizes).</span></span>
- <span data-ttu-id="8fef1-113">You can only attach a data disk to a VM that is running.</span><span class="sxs-lookup"><span data-stu-id="8fef1-113">You can only attach a data disk to a VM that is running.</span></span> <span data-ttu-id="8fef1-114">Make sure the VM is running before you try to attach a data disk.</span><span class="sxs-lookup"><span data-stu-id="8fef1-114">Make sure the VM is running before you try to attach a data disk.</span></span>

### <a name="attach-a-new-disk"></a><span data-ttu-id="8fef1-115">Attach a new disk</span><span class="sxs-lookup"><span data-stu-id="8fef1-115">Attach a new disk</span></span>
<span data-ttu-id="8fef1-116">Follow these steps to create and attach a new managed data disk to a VM in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="8fef1-116">Follow these steps to create and attach a new managed data disk to a VM in Azure DevTest Labs.</span></span>

1. <span data-ttu-id="8fef1-117">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="8fef1-117">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="8fef1-118">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="8fef1-118">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="8fef1-119">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="8fef1-119">From the list of labs, select the desired lab.</span></span> 
1. <span data-ttu-id="8fef1-120">From the list of **My virtual machines**, select a running VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-120">From the list of **My virtual machines**, select a running VM.</span></span>
1. <span data-ttu-id="8fef1-121">From the menu on the left, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-121">From the menu on the left, select **Disks**.</span></span>

    ![Select data disks for a virtual machine](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-data-disk.png)
1. <span data-ttu-id="8fef1-123">Choose **Attach new** to create a new data disk and attach it to the VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-123">Choose **Attach new** to create a new data disk and attach it to the VM.</span></span>

    ![Attach new data disk to a virtual machine](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-new.png)
1. <span data-ttu-id="8fef1-125">Complete the **Attach new disk** pane by entering a data disk name, type, and size.</span><span class="sxs-lookup"><span data-stu-id="8fef1-125">Complete the **Attach new disk** pane by entering a data disk name, type, and size.</span></span>

    ![Complete the "attach new disk" form](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-new-form.png)
1. <span data-ttu-id="8fef1-127">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-127">Select **OK**.</span></span>

<span data-ttu-id="8fef1-128">After a few moments, the new data disk is created and attached to the VM and appears in the list of **DATA DISKS** for that VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-128">After a few moments, the new data disk is created and attached to the VM and appears in the list of **DATA DISKS** for that VM.</span></span>

### <a name="attach-an-existing-disk"></a><span data-ttu-id="8fef1-129">Attach an existing disk</span><span class="sxs-lookup"><span data-stu-id="8fef1-129">Attach an existing disk</span></span>
<span data-ttu-id="8fef1-130">Follow these steps to reattach an existing available data disk to a running VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-130">Follow these steps to reattach an existing available data disk to a running VM.</span></span> 

1. <span data-ttu-id="8fef1-131">Select a running VM for which you want to reattach a data disk.</span><span class="sxs-lookup"><span data-stu-id="8fef1-131">Select a running VM for which you want to reattach a data disk.</span></span>
1. <span data-ttu-id="8fef1-132">From the menu on the left, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-132">From the menu on the left, select **Disks**.</span></span>
1. <span data-ttu-id="8fef1-133">Select **Attach existing** to attach an available data disk to the VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-133">Select **Attach existing** to attach an available data disk to the VM.</span></span>

    ![Attach existing data disk to a virtual machine](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-existing2.png)

1. <span data-ttu-id="8fef1-135">From the **Attach existing disk** pane, select OK.</span><span class="sxs-lookup"><span data-stu-id="8fef1-135">From the **Attach existing disk** pane, select OK.</span></span>

    ![Attach existing data disk to a virtual machine](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-existing.png)

<span data-ttu-id="8fef1-137">After a few moments, the data disk is attached to the VM and appears in the list of **DATA DISKS** for that VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-137">After a few moments, the data disk is attached to the VM and appears in the list of **DATA DISKS** for that VM.</span></span>

## <a name="detach-a-data-disk"></a><span data-ttu-id="8fef1-138">Detach a data disk</span><span class="sxs-lookup"><span data-stu-id="8fef1-138">Detach a data disk</span></span>
<span data-ttu-id="8fef1-139">When you no longer need a data disk that's attached to a VM, you can easily detach it.</span><span class="sxs-lookup"><span data-stu-id="8fef1-139">When you no longer need a data disk that's attached to a VM, you can easily detach it.</span></span> <span data-ttu-id="8fef1-140">Detaching removes the disk from the VM, but keeps it in storage for use later.</span><span class="sxs-lookup"><span data-stu-id="8fef1-140">Detaching removes the disk from the VM, but keeps it in storage for use later.</span></span>

<span data-ttu-id="8fef1-141">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine or to another one.</span><span class="sxs-lookup"><span data-stu-id="8fef1-141">If you want to use the existing data on the disk again, you can reattach it to the same virtual machine or to another one.</span></span>

### <a name="detach-from-the-vms-management-pane"></a><span data-ttu-id="8fef1-142">Detach from the VM's management pane</span><span class="sxs-lookup"><span data-stu-id="8fef1-142">Detach from the VM's management pane</span></span>
1. <span data-ttu-id="8fef1-143">From your list of virtual machines, select a VM that has a data disk attached.</span><span class="sxs-lookup"><span data-stu-id="8fef1-143">From your list of virtual machines, select a VM that has a data disk attached.</span></span>
1. <span data-ttu-id="8fef1-144">From the menu on the left, select **Disks**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-144">From the menu on the left, select **Disks**.</span></span>

    ![Select data disks for a virtual machine](./media/devtest-lab-attach-detach-data-disk/devtest-lab-attach-data-disk.png) 
1. <span data-ttu-id="8fef1-146">From the list of **DATA DISKS**, select the data disk that you want to detach.</span><span class="sxs-lookup"><span data-stu-id="8fef1-146">From the list of **DATA DISKS**, select the data disk that you want to detach.</span></span>
1. <span data-ttu-id="8fef1-147">Select **Detach** from the top of the disk's details pane.</span><span class="sxs-lookup"><span data-stu-id="8fef1-147">Select **Detach** from the top of the disk's details pane.</span></span>

    ![Detach a data disk](./media/devtest-lab-attach-detach-data-disk/devtest-lab-detach-data-disk2.png)
1. <span data-ttu-id="8fef1-149">Select **Yes** to confirm that you want to detach the data disk.</span><span class="sxs-lookup"><span data-stu-id="8fef1-149">Select **Yes** to confirm that you want to detach the data disk.</span></span>

<span data-ttu-id="8fef1-150">The disk is detached and is available to attach to another VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-150">The disk is detached and is available to attach to another VM.</span></span> 
### <a name="detach-from-the-labs-main-pane"></a><span data-ttu-id="8fef1-151">Detach from the lab's main pane</span><span class="sxs-lookup"><span data-stu-id="8fef1-151">Detach from the lab's main pane</span></span>
1. <span data-ttu-id="8fef1-152">On your lab's main pane, select **My data disks**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-152">On your lab's main pane, select **My data disks**.</span></span>

    ![Access the lab's data disks](./media/devtest-lab-attach-detach-data-disk/devtest-lab-my-data-disks.png)
1. <span data-ttu-id="8fef1-154">Right-click the data disk you want to detach – or select its ellipsis (...) – and choose **Detach**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-154">Right-click the data disk you want to detach – or select its ellipsis (...) – and choose **Detach**.</span></span>

    ![Detach a data disk](./media/devtest-lab-attach-detach-data-disk/devtest-lab-detach-data-disk.png)
1. <span data-ttu-id="8fef1-156">Select **Yes** to confirm that you want to detach it.</span><span class="sxs-lookup"><span data-stu-id="8fef1-156">Select **Yes** to confirm that you want to detach it.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8fef1-157">If a data disk is already detached, you can choose to remove it from your list of available data disks by selecting **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8fef1-157">If a data disk is already detached, you can choose to remove it from your list of available data disks by selecting **Delete**.</span></span>
   >
   >

## <a name="upgrade-an-unmanaged-data-disk"></a><span data-ttu-id="8fef1-158">Upgrade an unmanaged data disk</span><span class="sxs-lookup"><span data-stu-id="8fef1-158">Upgrade an unmanaged data disk</span></span>
<span data-ttu-id="8fef1-159">If you have an existing VM that uses unmanaged data disks, you can easily convert the VM to use managed disks.</span><span class="sxs-lookup"><span data-stu-id="8fef1-159">If you have an existing VM that uses unmanaged data disks, you can easily convert the VM to use managed disks.</span></span> <span data-ttu-id="8fef1-160">This process converts both the OS disk and any attached data disks.</span><span class="sxs-lookup"><span data-stu-id="8fef1-160">This process converts both the OS disk and any attached data disks.</span></span>

<span data-ttu-id="8fef1-161">To upgrade an unmanaged data disk, follow the steps outlined in this article to [detach the data disk](#detach-a-data-disk) from an unmanaged VM.</span><span class="sxs-lookup"><span data-stu-id="8fef1-161">To upgrade an unmanaged data disk, follow the steps outlined in this article to [detach the data disk](#detach-a-data-disk) from an unmanaged VM.</span></span> <span data-ttu-id="8fef1-162">Then, [reattach the disk](#attach-an-existing-disk) to a managed VM to automatically upgrade the data disk from unmanaged to managed.</span><span class="sxs-lookup"><span data-stu-id="8fef1-162">Then, [reattach the disk](#attach-an-existing-disk) to a managed VM to automatically upgrade the data disk from unmanaged to managed.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="8fef1-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fef1-163">Next steps</span></span>
<span data-ttu-id="8fef1-164">Learn how to manage data disks for [claimable virtual machines](devtest-lab-add-claimable-vm.md#unclaim-a-vm).</span><span class="sxs-lookup"><span data-stu-id="8fef1-164">Learn how to manage data disks for [claimable virtual machines](devtest-lab-add-claimable-vm.md#unclaim-a-vm).</span></span>

