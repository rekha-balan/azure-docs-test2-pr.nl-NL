---
title: Create an Azure DevTest Labs custom image from a VM | Microsoft Docs
description: Learn how to create a custom image in Azure DevTest Labs from a provisioned VM using the Azure portal
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 22f1579b2df2acdc736ed4c1d5cee64d096c320a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868665"
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="fb89d-103">Create a custom image from a VM</span><span class="sxs-lookup"><span data-stu-id="fb89d-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="fb89d-104">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="fb89d-104">Step-by-step instructions</span></span>

<span data-ttu-id="fb89d-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span><span class="sxs-lookup"><span data-stu-id="fb89d-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="fb89d-106">The following steps illustrate how to create a custom image from a VM:</span><span class="sxs-lookup"><span data-stu-id="fb89d-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="fb89d-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="fb89d-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="fb89d-108">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="fb89d-108">Select **All services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="fb89d-109">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="fb89d-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="fb89d-110">On the lab's main pane, select **My virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="fb89d-110">On the lab's main pane, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="fb89d-111">On the **My virtual machines** pane, select the VM from which you want to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="fb89d-111">On the **My virtual machines** pane, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="fb89d-112">On the VM's management pane, select **Create custom image (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="fb89d-112">On the VM's management pane, select **Create custom image (VHD)**.</span></span>

    ![Create custom image menu item](./media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="fb89d-114">On the **Custom image** pane, enter a name and description for your custom image.</span><span class="sxs-lookup"><span data-stu-id="fb89d-114">On the **Custom image** pane, enter a name and description for your custom image.</span></span> <span data-ttu-id="fb89d-115">This information is displayed in the list of bases when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="fb89d-115">This information is displayed in the list of bases when you create a VM.</span></span> <span data-ttu-id="fb89d-116">The custom image will include the OS disk and all the data disks attached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fb89d-116">The custom image will include the OS disk and all the data disks attached to the virtual machine.</span></span>

    ![Create custom image pane](./media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="fb89d-118">Select whether sysprep was run on the VM.</span><span class="sxs-lookup"><span data-stu-id="fb89d-118">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="fb89d-119">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span><span class="sxs-lookup"><span data-stu-id="fb89d-119">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="fb89d-120">Select **OK** when finished to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="fb89d-120">Select **OK** when finished to create the custom image.</span></span>

<span data-ttu-id="fb89d-121">After a few minutes, the custom image is created and is stored inside the lab’s storage account.</span><span class="sxs-lookup"><span data-stu-id="fb89d-121">After a few minutes, the custom image is created and is stored inside the lab’s storage account.</span></span> <span data-ttu-id="fb89d-122">When a lab user wants to create a new VM, the image is available in the list of base images.</span><span class="sxs-lookup"><span data-stu-id="fb89d-122">When a lab user wants to create a new VM, the image is available in the list of base images.</span></span>

![Custom image available in list of base images](./media/devtest-lab-create-template/custom-image-available-as-base.png)


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="fb89d-124">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="fb89d-124">Related blog posts</span></span>

- [<span data-ttu-id="fb89d-125">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="fb89d-125">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="fb89d-126">Copying Custom Images between Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="fb89d-126">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a><span data-ttu-id="fb89d-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="fb89d-127">Next steps</span></span>

- [<span data-ttu-id="fb89d-128">Add a VM to your lab</span><span class="sxs-lookup"><span data-stu-id="fb89d-128">Add a VM to your lab</span></span>](devtest-lab-add-vm.md)
