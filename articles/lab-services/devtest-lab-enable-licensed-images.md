---
title: Enable a licensed image in your lab in Azure DevTest Labs | Microsoft Docs
description: Learn how to enable a licensed image in Azure DevTest Labs using the Azure portal
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 221390d2-8d3b-4e1f-b454-43d33f8072b7
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 0e5de93f8a10d27c28b3f07567f9b6fa7e41d482
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870514"
---
# <a name="enable-a-licensed-image-in-your-lab-in-azure-devtest-labs"></a><span data-ttu-id="2319d-103">Enable a licensed image in your lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2319d-103">Enable a licensed image in your lab in Azure DevTest Labs</span></span>

<span data-ttu-id="2319d-104">In Azure DevTest Labs, a licensed image is one that includes terms and conditions – typically from a third party – that must be accepted before the image is accessible to users in the lab.</span><span class="sxs-lookup"><span data-stu-id="2319d-104">In Azure DevTest Labs, a licensed image is one that includes terms and conditions – typically from a third party – that must be accepted before the image is accessible to users in the lab.</span></span> <span data-ttu-id="2319d-105">The following sections describe how to work with licensed images so that they are available to use for creating virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2319d-105">The following sections describe how to work with licensed images so that they are available to use for creating virtual machines.</span></span>

## <a name="determining-whether-a-licensed-image-is-available-to-users"></a><span data-ttu-id="2319d-106">Determining whether a licensed image is available to users</span><span class="sxs-lookup"><span data-stu-id="2319d-106">Determining whether a licensed image is available to users</span></span>
<span data-ttu-id="2319d-107">The first step to allowing users to create VMs from a licensed image is to make sure that the terms and conditions have been accepted for the licensed image.</span><span class="sxs-lookup"><span data-stu-id="2319d-107">The first step to allowing users to create VMs from a licensed image is to make sure that the terms and conditions have been accepted for the licensed image.</span></span> <span data-ttu-id="2319d-108">The following steps show how you can view the offer status of a licensed image and, if necessary, accept its terms and conditions.</span><span class="sxs-lookup"><span data-stu-id="2319d-108">The following steps show how you can view the offer status of a licensed image and, if necessary, accept its terms and conditions.</span></span>

1. <span data-ttu-id="2319d-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="2319d-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="2319d-110">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="2319d-110">Select **All services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="2319d-111">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="2319d-111">From the list of labs, select the desired lab.</span></span>  

1. <span data-ttu-id="2319d-112">In the left panel under **SETTINGS**, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="2319d-112">In the left panel under **SETTINGS**, select **Configuration and policies**.</span></span>

1. <span data-ttu-id="2319d-113">In the left panel under **VIRTUAL MACHINE BASES**, select **Marketplace images**.</span><span class="sxs-lookup"><span data-stu-id="2319d-113">In the left panel under **VIRTUAL MACHINE BASES**, select **Marketplace images**.</span></span> 

    ![Marketplace images menu item](./media/devtest-lab-create-custom-image-from-licensed-image/devtest-lab-marketplace-images.png)

    <span data-ttu-id="2319d-115">A list of all available marketplace images is shown, including the **OFFER STATUS** for each image.</span><span class="sxs-lookup"><span data-stu-id="2319d-115">A list of all available marketplace images is shown, including the **OFFER STATUS** for each image.</span></span>

    ![List of marketplace images showing offer status for each image](./media/devtest-lab-create-custom-image-from-licensed-image/devtest-lab-offer-status.png)

    <span data-ttu-id="2319d-117">A licensed image shows an offer status of</span><span class="sxs-lookup"><span data-stu-id="2319d-117">A licensed image shows an offer status of</span></span> 
    
    - <span data-ttu-id="2319d-118">**Terms accepted:** the licensed image is available to users to create VMs.</span><span class="sxs-lookup"><span data-stu-id="2319d-118">**Terms accepted:** the licensed image is available to users to create VMs.</span></span> 
    - <span data-ttu-id="2319d-119">**Terms review needed:** the licensed image is not currently available to users.</span><span class="sxs-lookup"><span data-stu-id="2319d-119">**Terms review needed:** the licensed image is not currently available to users.</span></span> <span data-ttu-id="2319d-120">The terms and conditions of the license must be accepted before lab users can use it to create VMs.</span><span class="sxs-lookup"><span data-stu-id="2319d-120">The terms and conditions of the license must be accepted before lab users can use it to create VMs.</span></span> 

## <a name="making-a-licensed-image-available-to-lab-users"></a><span data-ttu-id="2319d-121">Making a licensed image available to lab users</span><span class="sxs-lookup"><span data-stu-id="2319d-121">Making a licensed image available to lab users</span></span>
<span data-ttu-id="2319d-122">To make sure a licensed image is available to lab users, a lab owner with admin permissions must first accept the terms and conditions for that licensed image.</span><span class="sxs-lookup"><span data-stu-id="2319d-122">To make sure a licensed image is available to lab users, a lab owner with admin permissions must first accept the terms and conditions for that licensed image.</span></span> <span data-ttu-id="2319d-123">Enabling programmatic deployment for the subscription associated with a licensed image automatically accepts the legal terms and privacy statements for that image.</span><span class="sxs-lookup"><span data-stu-id="2319d-123">Enabling programmatic deployment for the subscription associated with a licensed image automatically accepts the legal terms and privacy statements for that image.</span></span> <span data-ttu-id="2319d-124">[Working with Marketplace Images on Azure Resource Manager](https://azure.microsoft.com/blog/working-with-marketplace-images-on-azure-resource-manager/) provides additional information about programmatic deployment of marketplace images.</span><span class="sxs-lookup"><span data-stu-id="2319d-124">[Working with Marketplace Images on Azure Resource Manager](https://azure.microsoft.com/blog/working-with-marketplace-images-on-azure-resource-manager/) provides additional information about programmatic deployment of marketplace images.</span></span>

<span data-ttu-id="2319d-125">You can enable programmatic deployment for a licensed image by following these steps:</span><span class="sxs-lookup"><span data-stu-id="2319d-125">You can enable programmatic deployment for a licensed image by following these steps:</span></span>

1. <span data-ttu-id="2319d-126">In the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), go to the list of **Marketplace images**.</span><span class="sxs-lookup"><span data-stu-id="2319d-126">In the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), go to the list of **Marketplace images**.</span></span>

1. <span data-ttu-id="2319d-127">Identify a licensed image for which you want users to have access but whose terms have not been accepted.</span><span class="sxs-lookup"><span data-stu-id="2319d-127">Identify a licensed image for which you want users to have access but whose terms have not been accepted.</span></span> <span data-ttu-id="2319d-128">For example, you might see a Data Science Virtual Machine that shows a status of either **Terms accepted** or **Terms review needed**.</span><span class="sxs-lookup"><span data-stu-id="2319d-128">For example, you might see a Data Science Virtual Machine that shows a status of either **Terms accepted** or **Terms review needed**.</span></span>

    ![Configure Programmatic Deployment window](./media/devtest-lab-create-custom-image-from-licensed-image/devtest-lab-licensed-images.png)

   > [!NOTE]
   > <span data-ttu-id="2319d-130">Data Science VMs are Azure Virtual Machine images, pre-installed, configured, and tested with several popular tools that are commonly used for data analytics, machine learning and AI training.</span><span class="sxs-lookup"><span data-stu-id="2319d-130">Data Science VMs are Azure Virtual Machine images, pre-installed, configured, and tested with several popular tools that are commonly used for data analytics, machine learning and AI training.</span></span> <span data-ttu-id="2319d-131">[Introduction to Azure Data Science Virtual Machine for Linux and Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview) provides a great deal of information about DSVMs.</span><span class="sxs-lookup"><span data-stu-id="2319d-131">[Introduction to Azure Data Science Virtual Machine for Linux and Windows](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview) provides a great deal of information about DSVMs.</span></span>
   >
   >

1. <span data-ttu-id="2319d-132">In the **OFFER STATUS** column for the image, select **Terms review needed**.</span><span class="sxs-lookup"><span data-stu-id="2319d-132">In the **OFFER STATUS** column for the image, select **Terms review needed**.</span></span>

1. <span data-ttu-id="2319d-133">In the Configure Programmatic Deployment window, select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="2319d-133">In the Configure Programmatic Deployment window, select **Enable**.</span></span>

    ![Configure Programmatic Deployment window](./media/devtest-lab-create-custom-image-from-licensed-image/devtest-lab-enable-programmatic-deployment.png)

   > [!IMPORTANT]
   > <span data-ttu-id="2319d-135">You might see multiple subscriptions listed in the Configure Programmatic Deployment window.</span><span class="sxs-lookup"><span data-stu-id="2319d-135">You might see multiple subscriptions listed in the Configure Programmatic Deployment window.</span></span> <span data-ttu-id="2319d-136">Make sure you are enabling programmatic deployment only for the intended subscription.</span><span class="sxs-lookup"><span data-stu-id="2319d-136">Make sure you are enabling programmatic deployment only for the intended subscription.</span></span>
   >
   >


1. <span data-ttu-id="2319d-137">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2319d-137">Select **Save**.</span></span> 

    <span data-ttu-id="2319d-138">In the list of marketplace images, that image now shows **Terms accepted** and is available for users to create virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2319d-138">In the list of marketplace images, that image now shows **Terms accepted** and is available for users to create virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="2319d-139">Users can create a custom image from a licensed image.</span><span class="sxs-lookup"><span data-stu-id="2319d-139">Users can create a custom image from a licensed image.</span></span> <span data-ttu-id="2319d-140">See [Create a custom image from a VHD file](devtest-lab-create-template.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="2319d-140">See [Create a custom image from a VHD file](devtest-lab-create-template.md) for more information.</span></span>
>
>


## <a name="related-blog-posts"></a><span data-ttu-id="2319d-141">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="2319d-141">Related blog posts</span></span>

- [<span data-ttu-id="2319d-142">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="2319d-142">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)
- [<span data-ttu-id="2319d-143">Copying Custom Images between Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="2319d-143">Copying Custom Images between Azure DevTest Labs</span></span>](http://www.visualstudiogeeks.com/blog/DevOps/How-To-Move-CustomImages-VHD-Between-AzureDevTestLabs#copying-custom-images-between-azure-devtest-labs)

## <a name="next-steps"></a><span data-ttu-id="2319d-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="2319d-144">Next steps</span></span>

- [<span data-ttu-id="2319d-145">Create a custom image from a VM</span><span class="sxs-lookup"><span data-stu-id="2319d-145">Create a custom image from a VM</span></span>](devtest-lab-create-custom-image-from-vm-using-portal.md)
- [<span data-ttu-id="2319d-146">Create a custom image from a VHD file</span><span class="sxs-lookup"><span data-stu-id="2319d-146">Create a custom image from a VHD file</span></span>](devtest-lab-create-template.md)
- [<span data-ttu-id="2319d-147">Add a VM to your lab</span><span class="sxs-lookup"><span data-stu-id="2319d-147">Add a VM to your lab</span></span>](devtest-lab-add-vm.md)