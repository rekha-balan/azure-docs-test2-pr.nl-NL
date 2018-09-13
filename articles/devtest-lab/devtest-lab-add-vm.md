---
title: Add a VM to a lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to add a virtual machine to a lab in Azure DevTest Labs
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: tarcher
ms.openlocfilehash: 9d29c13766120b2083f932ffa6ae187a329ad3bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556578"
---
# <a name="add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="06afb-103">Add a VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="06afb-103">Add a VM to a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="06afb-104">You add a VM to a lab from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span><span class="sxs-lookup"><span data-stu-id="06afb-104">You add a VM to a lab from a *base* that is either a [custom image](devtest-lab-create-template.md), [formula](devtest-lab-manage-formulas.md), or [Marketplace image](devtest-lab-configure-marketplace-images.md).</span></span> <span data-ttu-id="06afb-105">This tutorial walks you through using the Azure portal to add a VM to a lab in DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="06afb-105">This tutorial walks you through using the Azure portal to add a VM to a lab in DevTest Labs.</span></span>

> [!NOTE]
> <span data-ttu-id="06afb-106">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how to make the VM claimable so that it is available for use by any user in the lab.</span><span class="sxs-lookup"><span data-stu-id="06afb-106">[Add a claimable VM](devtest-lab-add-claimable-vm.md) shows you how to make the VM claimable so that it is available for use by any user in the lab.</span></span>
>
>

## <a name="steps-to-add-a-vm-to-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="06afb-107">Steps to add a VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="06afb-107">Steps to add a VM to a lab in Azure DevTest Labs</span></span>
1. <span data-ttu-id="06afb-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="06afb-108">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="06afb-109">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="06afb-109">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
1. <span data-ttu-id="06afb-110">From the list of labs, select the lab in which you want to create the VM.</span><span class="sxs-lookup"><span data-stu-id="06afb-110">From the list of labs, select the lab in which you want to create the VM.</span></span>  
1. <span data-ttu-id="06afb-111">On the lab's **Overview** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="06afb-111">On the lab's **Overview** blade, select **+ Add**.</span></span>  

    ![Add VM button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-home-blade-add-vm.png)

1. <span data-ttu-id="06afb-113">On the **Choose a base** blade, select a base for the VM.</span><span class="sxs-lookup"><span data-stu-id="06afb-113">On the **Choose a base** blade, select a base for the VM.</span></span>
1. <span data-ttu-id="06afb-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span><span class="sxs-lookup"><span data-stu-id="06afb-114">On the **Virtual machine** blade, enter a name for the new virtual machine in the **Virtual machine name** text box.</span></span>

    ![Lab VM blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-add-vm/devtestlab-lab-vm-blade.png)

1. <span data-ttu-id="06afb-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="06afb-116">Enter a **User Name** that is granted administrator privileges on the virtual machine.</span></span>  
1. <span data-ttu-id="06afb-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span><span class="sxs-lookup"><span data-stu-id="06afb-117">If you want to use a password stored in your [secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store), select **Use a saved secret**, and specify a key value that corresponds to your secret (password).</span></span> <span data-ttu-id="06afb-118">Otherwise, enter a password in the text field labeled **Type a value**.</span><span class="sxs-lookup"><span data-stu-id="06afb-118">Otherwise, enter a password in the text field labeled **Type a value**.</span></span>
1. <span data-ttu-id="06afb-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span><span class="sxs-lookup"><span data-stu-id="06afb-119">The **Virtual machine disk type** determines which storage disk type is allowed for the virtual machines in the lab.</span></span>
1. <span data-ttu-id="06afb-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span><span class="sxs-lookup"><span data-stu-id="06afb-120">Select **Virtual machine size** and select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span>
1. <span data-ttu-id="06afb-121">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span><span class="sxs-lookup"><span data-stu-id="06afb-121">Select **Artifacts** and - from the list of artifacts - select and configure the artifacts that you want to add to the base image.</span></span>
    <span data-ttu-id="06afb-122">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm-with-artifacts.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span><span class="sxs-lookup"><span data-stu-id="06afb-122">**Note:** If you're new to DevTest Labs or configuring artifacts, refer to the [Add an existing artifact to a VM](./devtest-lab-add-vm-with-artifacts.md#add-an-existing-artifact-to-a-vm) section, and then return here when finished.</span></span>
1. <span data-ttu-id="06afb-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span><span class="sxs-lookup"><span data-stu-id="06afb-123">Select **Advanced settings** to configure the VM's network options and expiration options.</span></span> 

   <span data-ttu-id="06afb-124">To set an expiration option, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="06afb-124">To set an expiration option, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="06afb-125">By default, the VM will never expire.</span><span class="sxs-lookup"><span data-stu-id="06afb-125">By default, the VM will never expire.</span></span> 
1. <span data-ttu-id="06afb-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](./devtest-lab-add-vm-with-artifacts.md#save-azure-resource-manager-template) section, and return here when finished.</span><span class="sxs-lookup"><span data-stu-id="06afb-126">If you want to view or copy the Azure Resource Manager template, refer to the [Save Azure Resource Manager template](./devtest-lab-add-vm-with-artifacts.md#save-azure-resource-manager-template) section, and return here when finished.</span></span>
1. <span data-ttu-id="06afb-127">Select **Create** to add the specified VM to the lab.</span><span class="sxs-lookup"><span data-stu-id="06afb-127">Select **Create** to add the specified VM to the lab.</span></span>
1. <span data-ttu-id="06afb-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span><span class="sxs-lookup"><span data-stu-id="06afb-128">The lab blade displays the status of the VM's creation - first as **Creating**, then as **Running** after the VM has been started.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06afb-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="06afb-129">Next steps</span></span>
* <span data-ttu-id="06afb-130">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span><span class="sxs-lookup"><span data-stu-id="06afb-130">Once the VM has been created, you can connect to the VM by selecting **Connect** on the VM's blade.</span></span>
* <span data-ttu-id="06afb-131">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span><span class="sxs-lookup"><span data-stu-id="06afb-131">Explore the [DevTest Labs Azure Resource Manager QuickStart template gallery](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)</span></span>


