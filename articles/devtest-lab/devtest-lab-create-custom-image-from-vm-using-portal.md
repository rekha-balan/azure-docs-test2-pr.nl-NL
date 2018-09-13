---
title: Create an Azure DevTest Labs custom image from a VM | Microsoft Docs
description: Learn how to create a custom image in Azure DevTest Labs from a provisioned VM using the Azure portal
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
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 8ae15373f6bdf8989a7afb203ee437944d2f3453
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552394"
---
# <a name="create-a-custom-image-from-a-vm"></a><span data-ttu-id="2446e-103">Create a custom image from a VM</span><span class="sxs-lookup"><span data-stu-id="2446e-103">Create a custom image from a VM</span></span>

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="2446e-104">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="2446e-104">Step-by-step instructions</span></span>

<span data-ttu-id="2446e-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span><span class="sxs-lookup"><span data-stu-id="2446e-105">You can create a custom image from a provisioned VM, and afterwards use that custom image to create identical VMs.</span></span> <span data-ttu-id="2446e-106">The following steps illustrate how to create a custom image from a VM:</span><span class="sxs-lookup"><span data-stu-id="2446e-106">The following steps illustrate how to create a custom image from a VM:</span></span>

1. <span data-ttu-id="2446e-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2446e-107">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2446e-108">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="2446e-108">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="2446e-109">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="2446e-109">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="2446e-110">On the lab's blade, select **My virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="2446e-110">On the lab's blade, select **My virtual machines**.</span></span>
 
1. <span data-ttu-id="2446e-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="2446e-111">On the **My virtual machines** blade, select the VM from which you want to create the custom image.</span></span>

1. <span data-ttu-id="2446e-112">On the VM's blade, select **Create custom image (VHD)**.</span><span class="sxs-lookup"><span data-stu-id="2446e-112">On the VM's blade, select **Create custom image (VHD)**.</span></span>

    ![Create custom image menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-template/create-custom-image.png)

1. <span data-ttu-id="2446e-114">On the **Create image** blade, enter a name and description for your custom image.</span><span class="sxs-lookup"><span data-stu-id="2446e-114">On the **Create image** blade, enter a name and description for your custom image.</span></span> <span data-ttu-id="2446e-115">This information is displayed in the list of bases when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="2446e-115">This information is displayed in the list of bases when you create a VM.</span></span>

    ![Create custom image blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-template/create-custom-image-blade.png)

1. <span data-ttu-id="2446e-117">Select whether sysprep was run on the VM.</span><span class="sxs-lookup"><span data-stu-id="2446e-117">Select whether sysprep was run on the VM.</span></span> <span data-ttu-id="2446e-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span><span class="sxs-lookup"><span data-stu-id="2446e-118">If the sysprep was not run on the VM, specify whether you want sysprep run when a VM is created from this custom image.</span></span>

1. <span data-ttu-id="2446e-119">Select **OK** when finished to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="2446e-119">Select **OK** when finished to create the custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="2446e-120">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="2446e-120">Related blog posts</span></span>

- [<span data-ttu-id="2446e-121">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="2446e-121">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="2446e-122">Copying Custom Images between Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2446e-122">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

##<a name="next-steps"></a><span data-ttu-id="2446e-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="2446e-123">Next steps</span></span>

- [<span data-ttu-id="2446e-124">Add a VM to your lab</span><span class="sxs-lookup"><span data-stu-id="2446e-124">Add a VM to your lab</span></span>](./devtest-lab-add-vm-with-artifacts.md)


