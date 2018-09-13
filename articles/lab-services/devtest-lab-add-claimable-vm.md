---
title: Create and manage claimable VMs in a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to add a claimable virtual machine to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/01/2018
ms.author: spelluru
ms.openlocfilehash: 669dfab75f34a0d1f997dc34f600402d3c10669b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866573"
---
# <a name="create-and-manage-claimable-vms-in-azure-devtest-labs"></a><span data-ttu-id="1b70b-103">Create and manage claimable VMs in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1b70b-103">Create and manage claimable VMs in Azure DevTest Labs</span></span>
<span data-ttu-id="1b70b-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="1b70b-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="1b70b-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the processes a user follows to claim and unclaim the VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the processes a user follows to claim and unclaim the VM.</span></span>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="1b70b-106">Steps to add a claimable VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="1b70b-106">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="1b70b-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="1b70b-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="1b70b-108">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="1b70b-108">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="1b70b-109">From the list of labs, select the lab in which you want to create the claimable VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-109">From the list of labs, select the lab in which you want to create the claimable VM.</span></span>  
1. <span data-ttu-id="1b70b-110">On the lab's **Overview** pane, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="1b70b-110">On the lab's **Overview** pane, select **+ Add**.</span></span>  

    ![Add VM button](./media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="1b70b-112">On the **Choose a base** area, select a base for the VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-112">On the **Choose a base** area, select a base for the VM.</span></span>
1. <span data-ttu-id="1b70b-113">In the **Virtual machine** pane, enter a name for the new virtual machine in the **Virtual machine name** text box.</span><span class="sxs-lookup"><span data-stu-id="1b70b-113">In the **Virtual machine** pane, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Lab VM pane](./media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="1b70b-115">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1b70b-115">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="1b70b-116">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span><span class="sxs-lookup"><span data-stu-id="1b70b-116">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="1b70b-117">Otherwise, enter a password in the text field labeled **Type a value**.</span><span class="sxs-lookup"><span data-stu-id="1b70b-117">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="1b70b-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="1b70b-118">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="1b70b-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span><span class="sxs-lookup"><span data-stu-id="1b70b-119">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="1b70b-120">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span><span class="sxs-lookup"><span data-stu-id="1b70b-120">Select **Artifacts** and from the list of artifacts, select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="1b70b-121">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span><span class="sxs-lookup"><span data-stu-id="1b70b-121">If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](devtest-lab-add-vm.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="1b70b-122">Select **Advanced settings** to configure the VM's network options and expiration options.</span><span class="sxs-lookup"><span data-stu-id="1b70b-122">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="1b70b-123">Under **Claim options**, choose **Yes** to make the machine claimable.</span><span class="sxs-lookup"><span data-stu-id="1b70b-123">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Choose to make the VM claimable.](./media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="1b70b-125">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span><span class="sxs-lookup"><span data-stu-id="1b70b-125">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](devtest-lab-add-vm.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="1b70b-126">Select **Create** to add the specified VM to the lab.</span><span class="sxs-lookup"><span data-stu-id="1b70b-126">Select **Create** to add the specified VM to the lab.</span></span>

   <span data-ttu-id="1b70b-127">The status of the VM's creation is displayed, first as **Creating**, then as **Running** after the VM has been started.</span><span class="sxs-lookup"><span data-stu-id="1b70b-127">The status of the VM's creation is displayed, first as **Creating**, then as **Running** after the VM has been started.</span></span>

> [!NOTE]
> <span data-ttu-id="1b70b-128">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span><span class="sxs-lookup"><span data-stu-id="1b70b-128">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="using-a-claimable-vm"></a><span data-ttu-id="1b70b-129">Using a claimable VM</span><span class="sxs-lookup"><span data-stu-id="1b70b-129">Using a claimable VM</span></span>

<span data-ttu-id="1b70b-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1b70b-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="1b70b-131">From the list of "Claimable virtual machines" at the bottom of the lab's "Overview" pane, right-click on one of the VMs in the list and choose **Claim machine**.</span><span class="sxs-lookup"><span data-stu-id="1b70b-131">From the list of "Claimable virtual machines" at the bottom of the lab's "Overview" pane, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Request a specific claimable VM.](./media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="1b70b-133">At the top of the "Overview" pane, choose **Claim any**.</span><span class="sxs-lookup"><span data-stu-id="1b70b-133">At the top of the "Overview" pane, choose **Claim any**.</span></span> <span data-ttu-id="1b70b-134">A random virtual machine is assigned from the list of claimable VMs.</span><span class="sxs-lookup"><span data-stu-id="1b70b-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Request any claimable VM.](./media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="1b70b-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span><span class="sxs-lookup"><span data-stu-id="1b70b-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="unclaim-a-vm"></a><span data-ttu-id="1b70b-137">Unclaim a VM</span><span class="sxs-lookup"><span data-stu-id="1b70b-137">Unclaim a VM</span></span>

<span data-ttu-id="1b70b-138">When a user is finished using a claimed VM and wants to make it available to someone else, they can return the claimed VM to the list of claimable virtual machines by doing one of these steps:</span><span class="sxs-lookup"><span data-stu-id="1b70b-138">When a user is finished using a claimed VM and wants to make it available to someone else, they can return the claimed VM to the list of claimable virtual machines by doing one of these steps:</span></span>

- <span data-ttu-id="1b70b-139">From the list of "My virtual machines", right-click on one of the VMs in the list – or select its ellipsis (...) – and choose **Unclaim**.</span><span class="sxs-lookup"><span data-stu-id="1b70b-139">From the list of "My virtual machines", right-click on one of the VMs in the list – or select its ellipsis (...) – and choose **Unclaim**.</span></span>

  ![Unclaim a VM on the list of VM.](./media/devtest-lab-add-vm/devtestlab-unclaim-VM2.png)

- <span data-ttu-id="1b70b-141">In the list of "My virtual machines", select a VM to open its management pane, then select **Unclaim** from the top menu bar.</span><span class="sxs-lookup"><span data-stu-id="1b70b-141">In the list of "My virtual machines", select a VM to open its management pane, then select **Unclaim** from the top menu bar.</span></span>

  ![Unclaim a VM on the VM's management pane.](./media/devtest-lab-add-vm/devtestlab-unclaim-VM.png)

<span data-ttu-id="1b70b-143">When a user unclaims a VM, they no longer have any permissions for that specific lab VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-143">When a user unclaims a VM, they no longer have any permissions for that specific lab VM.</span></span>

### <a name="transferring-the-data-disk"></a><span data-ttu-id="1b70b-144">Transferring the data disk</span><span class="sxs-lookup"><span data-stu-id="1b70b-144">Transferring the data disk</span></span>
<span data-ttu-id="1b70b-145">If a claimable VM has a data disk attached to it and a user unclaims it, the data disk stays with the VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-145">If a claimable VM has a data disk attached to it and a user unclaims it, the data disk stays with the VM.</span></span> <span data-ttu-id="1b70b-146">When another user then claims that VM, that new user claims the data disk as well as the VM.</span><span class="sxs-lookup"><span data-stu-id="1b70b-146">When another user then claims that VM, that new user claims the data disk as well as the VM.</span></span>

<span data-ttu-id="1b70b-147">This is known as "transferring the data disk".</span><span class="sxs-lookup"><span data-stu-id="1b70b-147">This is known as "transferring the data disk".</span></span> <span data-ttu-id="1b70b-148">The data disk then becomes available in the new user's list of **My data disks** for them to manage.</span><span class="sxs-lookup"><span data-stu-id="1b70b-148">The data disk then becomes available in the new user's list of **My data disks** for them to manage.</span></span>

![Unclaim data disks.](./media/devtest-lab-add-vm/devtestlab-unclaim-datadisks.png)



## <a name="next-steps"></a><span data-ttu-id="1b70b-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b70b-150">Next steps</span></span>
* <span data-ttu-id="1b70b-151">Once it is created, you can connect to the VM by selecting **Connect** on its management pane.</span><span class="sxs-lookup"><span data-stu-id="1b70b-151">Once it is created, you can connect to the VM by selecting **Connect** on its management pane.</span></span>
* <span data-ttu-id="1b70b-152">Explore the [DevTest Labs Azure Resource Manager quickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span><span class="sxs-lookup"><span data-stu-id="1b70b-152">Explore the [DevTest Labs Azure Resource Manager quickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/Samples).</span></span>
