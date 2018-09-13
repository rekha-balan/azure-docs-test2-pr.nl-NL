---
title: Create an Azure DevTest Labs custom image from a VHD file | Microsoft Docs
description: Learn how to create a custom image in Azure DevTest Labs from a VHD file using the Azure portal
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: b795bc61-7c28-40e6-82fc-96d629ee0568
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: a961565815ca0d89dc98a8d6a3e14b338b649398
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865467"
---
# <a name="create-a-custom-image-from-a-vhd-file"></a><span data-ttu-id="f69e7-103">Create a custom image from a VHD file</span><span class="sxs-lookup"><span data-stu-id="f69e7-103">Create a custom image from a VHD file</span></span>

[!INCLUDE [devtest-lab-create-custom-image-from-vhd-selector](../../includes/devtest-lab-create-custom-image-from-vhd-selector.md)]

[!INCLUDE [devtest-lab-custom-image-definition](../../includes/devtest-lab-custom-image-definition.md)]

[!INCLUDE [devtest-lab-upload-vhd-options](../../includes/devtest-lab-upload-vhd-options.md)]

## <a name="step-by-step-instructions"></a><span data-ttu-id="f69e7-104">Step-by-step instructions</span><span class="sxs-lookup"><span data-stu-id="f69e7-104">Step-by-step instructions</span></span>

<span data-ttu-id="f69e7-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="f69e7-105">The following steps walk you through creating a custom image from a VHD file using the Azure portal:</span></span>

1. <span data-ttu-id="f69e7-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f69e7-106">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="f69e7-107">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="f69e7-107">Select **All services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="f69e7-108">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="f69e7-108">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="f69e7-109">On the lab's main pane, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="f69e7-109">On the lab's main pane, select **Configuration and policies**.</span></span> 

1. <span data-ttu-id="f69e7-110">On the **Configuration and policies** pane, select **Custom images**.</span><span class="sxs-lookup"><span data-stu-id="f69e7-110">On the **Configuration and policies** pane, select **Custom images**.</span></span>

1. <span data-ttu-id="f69e7-111">On the **Custom images** pane, select **+Add**.</span><span class="sxs-lookup"><span data-stu-id="f69e7-111">On the **Custom images** pane, select **+Add**.</span></span>

    ![Add Custom image](./media/devtest-lab-create-template/add-custom-image.png)

1. <span data-ttu-id="f69e7-113">Enter the name of the custom image.</span><span class="sxs-lookup"><span data-stu-id="f69e7-113">Enter the name of the custom image.</span></span> <span data-ttu-id="f69e7-114">This name is displayed in the list of base images when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="f69e7-114">This name is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="f69e7-115">Enter the description of the custom image.</span><span class="sxs-lookup"><span data-stu-id="f69e7-115">Enter the description of the custom image.</span></span> <span data-ttu-id="f69e7-116">This description is displayed in the list of base images when creating a VM.</span><span class="sxs-lookup"><span data-stu-id="f69e7-116">This description is displayed in the list of base images when creating a VM.</span></span>

1. <span data-ttu-id="f69e7-117">For **OS type**, select either **Windows** or **Linux**.</span><span class="sxs-lookup"><span data-stu-id="f69e7-117">For **OS type**, select either **Windows** or **Linux**.</span></span>

    - <span data-ttu-id="f69e7-118">If you select **Windows**, specify via the checkbox whether *sysprep* has been run on the machine.</span><span class="sxs-lookup"><span data-stu-id="f69e7-118">If you select **Windows**, specify via the checkbox whether *sysprep* has been run on the machine.</span></span> 
    - <span data-ttu-id="f69e7-119">If you select **Linux**, specify via the checkbox whether *deprovision* has been run on the machine.</span><span class="sxs-lookup"><span data-stu-id="f69e7-119">If you select **Linux**, specify via the checkbox whether *deprovision* has been run on the machine.</span></span> 

1. <span data-ttu-id="f69e7-120">Select a **VHD** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f69e7-120">Select a **VHD** from the drop-down menu.</span></span> <span data-ttu-id="f69e7-121">This is the VHD that will be used to create the new custom image.</span><span class="sxs-lookup"><span data-stu-id="f69e7-121">This is the VHD that will be used to create the new custom image.</span></span> <span data-ttu-id="f69e7-122">If necessary, select to **Upload a VHD using PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f69e7-122">If necessary, select to **Upload a VHD using PowerShell**.</span></span>

1. <span data-ttu-id="f69e7-123">You can also enter a plan name, plan offer, and plan publisher if the image used to create the custom image is not a licensed image (published by Microsoft).</span><span class="sxs-lookup"><span data-stu-id="f69e7-123">You can also enter a plan name, plan offer, and plan publisher if the image used to create the custom image is not a licensed image (published by Microsoft).</span></span>

   - <span data-ttu-id="f69e7-124">**Plan name:** Enter the name of the Marketplace image (SKU) from which this custom image is created</span><span class="sxs-lookup"><span data-stu-id="f69e7-124">**Plan name:** Enter the name of the Marketplace image (SKU) from which this custom image is created</span></span> 
   - <span data-ttu-id="f69e7-125">**Plan offer:** Enter the product (offer) of the Marketplace image from which this custom image is created</span><span class="sxs-lookup"><span data-stu-id="f69e7-125">**Plan offer:** Enter the product (offer) of the Marketplace image from which this custom image is created</span></span> 
   - <span data-ttu-id="f69e7-126">**Plan publisher:** Enter the publisher of the Marketplace image from which this custom image is created</span><span class="sxs-lookup"><span data-stu-id="f69e7-126">**Plan publisher:** Enter the publisher of the Marketplace image from which this custom image is created</span></span>

   > [!NOTE]
   > <span data-ttu-id="f69e7-127">If the image you are using to create a custom image is **not** a licensed image, then these fields are empty and can be filled in if you choose.</span><span class="sxs-lookup"><span data-stu-id="f69e7-127">If the image you are using to create a custom image is **not** a licensed image, then these fields are empty and can be filled in if you choose.</span></span> <span data-ttu-id="f69e7-128">If the image **is** a licensed image, then the fields are auto populated with the plan information.</span><span class="sxs-lookup"><span data-stu-id="f69e7-128">If the image **is** a licensed image, then the fields are auto populated with the plan information.</span></span> <span data-ttu-id="f69e7-129">If you try to change them in this case, a warning message is displayed.</span><span class="sxs-lookup"><span data-stu-id="f69e7-129">If you try to change them in this case, a warning message is displayed.</span></span>
   >
   >

1. <span data-ttu-id="f69e7-130">Select **OK** to create the custom image.</span><span class="sxs-lookup"><span data-stu-id="f69e7-130">Select **OK** to create the custom image.</span></span>

<span data-ttu-id="f69e7-131">After a few minutes, the custom image is created and is stored inside the lab’s storage account.</span><span class="sxs-lookup"><span data-stu-id="f69e7-131">After a few minutes, the custom image is created and is stored inside the lab’s storage account.</span></span> <span data-ttu-id="f69e7-132">When a lab user wants to create a new VM, the image is available in the list of base images.</span><span class="sxs-lookup"><span data-stu-id="f69e7-132">When a lab user wants to create a new VM, the image is available in the list of base images.</span></span>

![Custom image available in list of base images](./media/devtest-lab-create-template/custom-image-available-as-base.png)


[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="f69e7-134">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="f69e7-134">Related blog posts</span></span>

- [<span data-ttu-id="f69e7-135">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="f69e7-135">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="f69e7-136">Copying Custom Images between Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f69e7-136">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a><span data-ttu-id="f69e7-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="f69e7-137">Next steps</span></span>

- [<span data-ttu-id="f69e7-138">Add a VM to your lab</span><span class="sxs-lookup"><span data-stu-id="f69e7-138">Add a VM to your lab</span></span>](./devtest-lab-add-vm.md)
