---
title: Access a lab in Azure DevTest Labs | Microsoft Docs
description: In this tutorial, you access the lab that's created by using Azure DevTest Labs, claim virtual machines, use them, and then unclaim them.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: cd623767c9627810afb64ca9185c991c5c9f3858
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856150"
---
# <a name="tutorial-access-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="52445-103">Tutorial: Access a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="52445-103">Tutorial: Access a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="52445-104">In this tutorial, you use the lab that was created in the [Tutorial: Create a lab in Azure DevTest Labs](tutorial-create-custom-lab.md) .</span><span class="sxs-lookup"><span data-stu-id="52445-104">In this tutorial, you use the lab that was created in the [Tutorial: Create a lab in Azure DevTest Labs](tutorial-create-custom-lab.md) .</span></span>

<span data-ttu-id="52445-105">In this tutorial, you do the following actions:</span><span class="sxs-lookup"><span data-stu-id="52445-105">In this tutorial, you do the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="52445-106">Claim a virtual machine (VM) in the lab</span><span class="sxs-lookup"><span data-stu-id="52445-106">Claim a virtual machine (VM) in the lab</span></span>
> * <span data-ttu-id="52445-107">Connect to the VM</span><span class="sxs-lookup"><span data-stu-id="52445-107">Connect to the VM</span></span>
> * <span data-ttu-id="52445-108">Unclaim the VM</span><span class="sxs-lookup"><span data-stu-id="52445-108">Unclaim the VM</span></span>

<span data-ttu-id="52445-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="52445-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="access-the-lab"></a><span data-ttu-id="52445-110">Access the lab</span><span class="sxs-lookup"><span data-stu-id="52445-110">Access the lab</span></span>

1. <span data-ttu-id="52445-111">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="52445-111">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="52445-112">Select **All resources** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="52445-112">Select **All resources** on the left menu.</span></span> 
3. <span data-ttu-id="52445-113">Select **DevTest Labs** for resource type.</span><span class="sxs-lookup"><span data-stu-id="52445-113">Select **DevTest Labs** for resource type.</span></span> 
4. <span data-ttu-id="52445-114">Select the lab.</span><span class="sxs-lookup"><span data-stu-id="52445-114">Select the lab.</span></span> 

    ![Select the lab](./media/tutorial-use-custom-lab/search-for-select-custom-lab.png)

## <a name="claim-a-vm"></a><span data-ttu-id="52445-116">Claim a VM</span><span class="sxs-lookup"><span data-stu-id="52445-116">Claim a VM</span></span>

1. <span data-ttu-id="52445-117">In the list of **Claimable virtual machines**, select **...** (ellipsis), and select **Claim machine**.</span><span class="sxs-lookup"><span data-stu-id="52445-117">In the list of **Claimable virtual machines**, select **...** (ellipsis), and select **Claim machine**.</span></span>

    ![Claim virtual machine](./media/tutorial-use-custom-lab/claim-virtual-machine.png)
1. <span data-ttu-id="52445-119">Confirm that you see the VM in the list **My virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="52445-119">Confirm that you see the VM in the list **My virtual machines**.</span></span>

    ![My virtual machine](./media/tutorial-use-custom-lab/my-virtual-machines.png)

## <a name="connect-to-the-vm"></a><span data-ttu-id="52445-121">Connect to the VM</span><span class="sxs-lookup"><span data-stu-id="52445-121">Connect to the VM</span></span>

1. <span data-ttu-id="52445-122">Select your VM in the list.</span><span class="sxs-lookup"><span data-stu-id="52445-122">Select your VM in the list.</span></span> <span data-ttu-id="52445-123">You see the **Virtual Machine page** for your VM.</span><span class="sxs-lookup"><span data-stu-id="52445-123">You see the **Virtual Machine page** for your VM.</span></span> <span data-ttu-id="52445-124">Select **Connect** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="52445-124">Select **Connect** on the toolbar.</span></span>

    ![Connect to virtual machine](./media/tutorial-use-custom-lab/connect-button.png)
2. <span data-ttu-id="52445-126">Save the downloaded **RDP** file your hard disk and use it to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="52445-126">Save the downloaded **RDP** file your hard disk and use it to connect to the virtual machine.</span></span> <span data-ttu-id="52445-127">Specify the user name and password you mentioned when the VM was created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="52445-127">Specify the user name and password you mentioned when the VM was created in the previous section.</span></span> 

## <a name="unclaim-the-vm"></a><span data-ttu-id="52445-128">Unclaim the VM</span><span class="sxs-lookup"><span data-stu-id="52445-128">Unclaim the VM</span></span>
<span data-ttu-id="52445-129">After you are done with using the VM, unclaim the VM by following these steps:</span><span class="sxs-lookup"><span data-stu-id="52445-129">After you are done with using the VM, unclaim the VM by following these steps:</span></span> 

1. <span data-ttu-id="52445-130">On the virtual machine page, and select **Unclaim** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="52445-130">On the virtual machine page, and select **Unclaim** on the toolbar.</span></span> 

    ![Unclaim VM](./media/tutorial-use-custom-lab/unclaim-vm-menu.png)
1. <span data-ttu-id="52445-132">The VM is shut down before it's unclaimed.</span><span class="sxs-lookup"><span data-stu-id="52445-132">The VM is shut down before it's unclaimed.</span></span> 

    ![Unclaim status](./media/tutorial-use-custom-lab/unclaim-status.png) 
1. <span data-ttu-id="52445-134">After the unclaim operation is done, you see the VM in the list of **Claimable virtual machines** list at the bottom.</span><span class="sxs-lookup"><span data-stu-id="52445-134">After the unclaim operation is done, you see the VM in the list of **Claimable virtual machines** list at the bottom.</span></span> 
    
## <a name="next-steps"></a><span data-ttu-id="52445-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="52445-135">Next steps</span></span>
<span data-ttu-id="52445-136">This tutorial showed you how to access and use a lab that was created by using Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="52445-136">This tutorial showed you how to access and use a lab that was created by using Azure DevTest Labs.</span></span> <span data-ttu-id="52445-137">For more information about accessing and using VMs in a lab, see</span><span class="sxs-lookup"><span data-stu-id="52445-137">For more information about accessing and using VMs in a lab, see</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="52445-138">How to: Use VMs in a lab</span><span class="sxs-lookup"><span data-stu-id="52445-138">How to: Use VMs in a lab</span></span>](devtest-lab-add-vm.md)

