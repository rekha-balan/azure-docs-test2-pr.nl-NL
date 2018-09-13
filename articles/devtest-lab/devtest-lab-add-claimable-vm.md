---
title: Add a claimable VM to a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to add a claimable virtual machine to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: f671e66e-9630-4e30-a131-a6bad9ed9c11
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: tarcher
ms.openlocfilehash: 217e090dd40ac27e50aafae832bbc01e397251be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550483"
---
# <a name="add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="82929-103">Add a claimable VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82929-103">Add a claimable VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="82929-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="82929-104">You add a claimable VM to a lab in a similar manner to how you [add a standard VM](devtest-lab-add-vm.md) – from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="82929-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span><span class="sxs-lookup"><span data-stu-id="82929-105">This tutorial walks you through using the Azure portal to add a claimable VM to a lab in DevTest Labs, and shows the process a user follows to claim the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="82929-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span><span class="sxs-lookup"><span data-stu-id="82929-106">If you deploy lab VMs through [Azure Resource Manager templates](devtest-lab-create-environment-from-arm.md), you can create claimable VMs by setting the **allowClaim** property to true in the properties section.</span></span>
>
>

## <a name="steps-to-add-a-claimable-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="82929-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82929-107">Steps to add a claimable VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="82929-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="82929-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="82929-109">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="82929-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="82929-110">From the list of labs, select the lab in which you want to create the VM.</span><span class="sxs-lookup"><span data-stu-id="82929-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="82929-111">On the lab's **Overview** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="82929-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Add VM button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="82929-113">On the **Choose a base** blade, select a base for the VM.</span><span class="sxs-lookup"><span data-stu-id="82929-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="82929-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span><span class="sxs-lookup"><span data-stu-id="82929-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Lab VM blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="82929-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="82929-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="82929-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span><span class="sxs-lookup"><span data-stu-id="82929-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="82929-118">Otherwise, enter a password in the text field labeled **Type a value**.</span><span class="sxs-lookup"><span data-stu-id="82929-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="82929-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="82929-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="82929-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span><span class="sxs-lookup"><span data-stu-id="82929-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="82929-121">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span><span class="sxs-lookup"><span data-stu-id="82929-121">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="82929-122">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm-with-artifacts.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span><span class="sxs-lookup"><span data-stu-id="82929-122">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm-with-artifacts.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="82929-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span><span class="sxs-lookup"><span data-stu-id="82929-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> <span data-ttu-id="82929-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span><span class="sxs-lookup"><span data-stu-id="82929-124">Under **Claim options**, choose **Yes** to make the machine claimable.</span></span>

  ![Choose to make the VM claimable.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-claim-VM-option.png)

1. <span data-ttu-id="82929-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](./devtest-lab-add-vm-with-artifacts.md#save-azure-resource-manager-template) section, and return here when finished.</span><span class="sxs-lookup"><span data-stu-id="82929-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](./devtest-lab-add-vm-with-artifacts.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="82929-127">Select **Create** to add the specified VM to the lab.</span><span class="sxs-lookup"><span data-stu-id="82929-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="82929-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span><span class="sxs-lookup"><span data-stu-id="82929-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>


## <a name="using-a-claimable-vm"></a><span data-ttu-id="82929-129">Using a claimable VM</span><span class="sxs-lookup"><span data-stu-id="82929-129">Using a claimable VM</span></span>

<span data-ttu-id="82929-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span><span class="sxs-lookup"><span data-stu-id="82929-130">A user can claim any VM from the list of "Claimable virtual machines" by doing one of these steps:</span></span>

* <span data-ttu-id="82929-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span><span class="sxs-lookup"><span data-stu-id="82929-131">From the list of "Claimable virtual machines" at the bottom of the lab's Overview blade, right-click on one of the VMs in the list and choose **Claim machine**.</span></span>

 ![Request a specific claimable VM.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-claim-VM.png)


* <span data-ttu-id="82929-133">At the top of the **Overview** blade, choose **Claim any**.</span><span class="sxs-lookup"><span data-stu-id="82929-133">At the top of the **Overview** blade, choose **Claim any**.</span></span> <span data-ttu-id="82929-134">A random virtual machine is assigned from the list of claimable VMs.</span><span class="sxs-lookup"><span data-stu-id="82929-134">A random virtual machine is assigned from the list of claimable VMs.</span></span>

 ![Request any claimable VM.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-claim-any.png)


<span data-ttu-id="82929-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span><span class="sxs-lookup"><span data-stu-id="82929-136">After a user claims a VM, it is moved up into their list of "My virtual machines" and is no longer claimable by any other user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82929-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="82929-137">Next steps</span></span>
* <span data-ttu-id="82929-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span><span class="sxs-lookup"><span data-stu-id="82929-138">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="82929-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="82929-139">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>





