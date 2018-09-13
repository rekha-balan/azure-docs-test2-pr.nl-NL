---
title: Make Virtual Machine Scale Sets available in Azure Stack | Microsoft Docs
description: Learn how a cloud operator can add Virtual Machine Scale Sets to the Azure Stack Marketplace
services: azure-stack
author: brenduns
manager: femila
editor: ''
ms.service: azure-stack
ms.topic: article
ms.date: 09/05/2018
ms.author: brenduns
ms.reviewer: kivenkat
ms.openlocfilehash: 3fbc3047688fed877280ca2d0f079ddea66bceb8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871527"
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="eb59d-103">Make Virtual Machine Scale Sets available in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="eb59d-103">Make Virtual Machine Scale Sets available in Azure Stack</span></span>

<span data-ttu-id="eb59d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="eb59d-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>
  
<span data-ttu-id="eb59d-105">Virtual machine scale sets are an Azure Stack compute resource.</span><span class="sxs-lookup"><span data-stu-id="eb59d-105">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="eb59d-106">You can use them to deploy and manage a set of identical virtual machines.</span><span class="sxs-lookup"><span data-stu-id="eb59d-106">You can use them to deploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="eb59d-107">With all virtual machines configured the same, scale sets don’t require pre-provisioning of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="eb59d-107">With all virtual machines configured the same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="eb59d-108">It's easier to build large-scale services that target big compute, big data, and containerized workloads.</span><span class="sxs-lookup"><span data-stu-id="eb59d-108">It's easier to build large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="eb59d-109">This article guides you through the process to make scale sets available in the Azure Stack Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb59d-109">This article guides you through the process to make scale sets available in the Azure Stack Marketplace.</span></span> <span data-ttu-id="eb59d-110">After you complete this procedure, your users can add virtual machine scale sets to their subscriptions.</span><span class="sxs-lookup"><span data-stu-id="eb59d-110">After you complete this procedure, your users can add virtual machine scale sets to their subscriptions.</span></span>

<span data-ttu-id="eb59d-111">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span><span class="sxs-lookup"><span data-stu-id="eb59d-111">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="eb59d-112">For more information, see the following videos:</span><span class="sxs-lookup"><span data-stu-id="eb59d-112">For more information, see the following videos:</span></span>
* [<span data-ttu-id="eb59d-113">Mark Russinovich talks Azure scale sets</span><span class="sxs-lookup"><span data-stu-id="eb59d-113">Mark Russinovich talks Azure scale sets</span></span>](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [<span data-ttu-id="eb59d-114">Virtual Machine Scale Sets with Guy Bowerman</span><span class="sxs-lookup"><span data-stu-id="eb59d-114">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="eb59d-115">On Azure Stack, virtual machine scale sets don't support auto-scale.</span><span class="sxs-lookup"><span data-stu-id="eb59d-115">On Azure Stack, virtual machine scale sets don't support auto-scale.</span></span> <span data-ttu-id="eb59d-116">You can add more instances to a scale set using Resource Manager templates, CLI, or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eb59d-116">You can add more instances to a scale set using Resource Manager templates, CLI, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb59d-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="eb59d-117">Prerequisites</span></span>

- <span data-ttu-id="eb59d-118">**The Marketplace**</span><span class="sxs-lookup"><span data-stu-id="eb59d-118">**The Marketplace**</span></span>  
    <span data-ttu-id="eb59d-119">Register Azure Stack with global Azure to enable the availability of items in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb59d-119">Register Azure Stack with global Azure to enable the availability of items in the Marketplace.</span></span> <span data-ttu-id="eb59d-120">Follow the instructions in [Register Azure Stack with Azure](azure-stack-registration.md).</span><span class="sxs-lookup"><span data-stu-id="eb59d-120">Follow the instructions in [Register Azure Stack with Azure](azure-stack-registration.md).</span></span>
- <span data-ttu-id="eb59d-121">**Operating system image**</span><span class="sxs-lookup"><span data-stu-id="eb59d-121">**Operating system image**</span></span>  
  <span data-ttu-id="eb59d-122">Before a virtual machine scale set (VMSS) can be created, you must download the VM images for use in the VMSS from the [Azure Stack Marketplace](azure-stack-download-azure-marketplace-item.md).</span><span class="sxs-lookup"><span data-stu-id="eb59d-122">Before a virtual machine scale set (VMSS) can be created, you must download the VM images for use in the VMSS from the [Azure Stack Marketplace](azure-stack-download-azure-marketplace-item.md).</span></span> <span data-ttu-id="eb59d-123">The images must already be present before a user can create a new VMSS.</span><span class="sxs-lookup"><span data-stu-id="eb59d-123">The images must already be present before a user can create a new VMSS.</span></span> 


## <a name="use-the-azure-stack-portal"></a><span data-ttu-id="eb59d-124">Use the Azure Stack portal</span><span class="sxs-lookup"><span data-stu-id="eb59d-124">Use the Azure Stack portal</span></span> 

>[!NOTE]  
> <span data-ttu-id="eb59d-125">The information in this section applies when you use  Azure Stack version 1808 or later.</span><span class="sxs-lookup"><span data-stu-id="eb59d-125">The information in this section applies when you use  Azure Stack version 1808 or later.</span></span> <span data-ttu-id="eb59d-126">If your version is 1807 or earlier, see [Add the Virtual Machine Scale Set (Prior to 1808)](#add-the-virtual-machine-scale-set-(prior-to-version-1808)).</span><span class="sxs-lookup"><span data-stu-id="eb59d-126">If your version is 1807 or earlier, see [Add the Virtual Machine Scale Set (Prior to 1808)](#add-the-virtual-machine-scale-set-(prior-to-version-1808)).</span></span>

1. <span data-ttu-id="eb59d-127">Sign in to the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="eb59d-127">Sign in to the Azure Stack portal.</span></span> <span data-ttu-id="eb59d-128">Then, go to **All services** > **Virtual machine scale sets**, and then under *COMPUTE*, select **Virtual machine scale sets**.</span><span class="sxs-lookup"><span data-stu-id="eb59d-128">Then, go to **All services** > **Virtual machine scale sets**, and then under *COMPUTE*, select **Virtual machine scale sets**.</span></span> 
   <span data-ttu-id="eb59d-129">![Select virtual machine scale sets](media/azure-stack-compute-add-scalesets/all-services.png)</span><span class="sxs-lookup"><span data-stu-id="eb59d-129">![Select virtual machine scale sets](media/azure-stack-compute-add-scalesets/all-services.png)</span></span>

2. <span data-ttu-id="eb59d-130">Select Create ***Virtual machine scale sets***.</span><span class="sxs-lookup"><span data-stu-id="eb59d-130">Select Create ***Virtual machine scale sets***.</span></span>
   <span data-ttu-id="eb59d-131">![Create a virtual machine scale set](media/azure-stack-compute-add-scalesets/create-scale-set.png)</span><span class="sxs-lookup"><span data-stu-id="eb59d-131">![Create a virtual machine scale set](media/azure-stack-compute-add-scalesets/create-scale-set.png)</span></span>

3. <span data-ttu-id="eb59d-132">Fill in the empty fields, choose from the dropdowns for *Operating system disk image*, *Subscription*, and *Instance size*.</span><span class="sxs-lookup"><span data-stu-id="eb59d-132">Fill in the empty fields, choose from the dropdowns for *Operating system disk image*, *Subscription*, and *Instance size*.</span></span> <span data-ttu-id="eb59d-133">Select **Yes** for *Use managed disks*.</span><span class="sxs-lookup"><span data-stu-id="eb59d-133">Select **Yes** for *Use managed disks*.</span></span> <span data-ttu-id="eb59d-134">Then, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="eb59d-134">Then, select **Create**.</span></span>
    <span data-ttu-id="eb59d-135">![Configure and create](media/azure-stack-compute-add-scalesets/create.png)</span><span class="sxs-lookup"><span data-stu-id="eb59d-135">![Configure and create](media/azure-stack-compute-add-scalesets/create.png)</span></span>

4. <span data-ttu-id="eb59d-136">To see your new virtual machine scale set, go to **All resources**, search for the virtual machine scale set name, and then select its name in the search.</span><span class="sxs-lookup"><span data-stu-id="eb59d-136">To see your new virtual machine scale set, go to **All resources**, search for the virtual machine scale set name, and then select its name in the search.</span></span> 
   <span data-ttu-id="eb59d-137">![View the scale set](media/azure-stack-compute-add-scalesets/search.png)</span><span class="sxs-lookup"><span data-stu-id="eb59d-137">![View the scale set](media/azure-stack-compute-add-scalesets/search.png)</span></span>



## <a name="add-the-virtual-machine-scale-set-prior-to-version-1808"></a><span data-ttu-id="eb59d-138">Add the Virtual Machine Scale Set (prior to version 1808)</span><span class="sxs-lookup"><span data-stu-id="eb59d-138">Add the Virtual Machine Scale Set (prior to version 1808)</span></span>
>[!NOTE]  
> <span data-ttu-id="eb59d-139">The information in this section applies when you use a version of Azure Stack prior to 1808.</span><span class="sxs-lookup"><span data-stu-id="eb59d-139">The information in this section applies when you use a version of Azure Stack prior to 1808.</span></span> <span data-ttu-id="eb59d-140">If you use version 1808 or later, see [Use the Azure Stack portal](#use-the-azure-stack-portal).</span><span class="sxs-lookup"><span data-stu-id="eb59d-140">If you use version 1808 or later, see [Use the Azure Stack portal](#use-the-azure-stack-portal).</span></span>

1. <span data-ttu-id="eb59d-141">Open the Azure Stack Marketplace and connect to Azure.</span><span class="sxs-lookup"><span data-stu-id="eb59d-141">Open the Azure Stack Marketplace and connect to Azure.</span></span> <span data-ttu-id="eb59d-142">Select **Marketplace management**> **+ Add from Azure**.</span><span class="sxs-lookup"><span data-stu-id="eb59d-142">Select **Marketplace management**> **+ Add from Azure**.</span></span>

    ![Marketplace management](media/azure-stack-compute-add-scalesets/image01.png)

2. <span data-ttu-id="eb59d-144">Add and download the Virtual Machine Scale Set marketplace item.</span><span class="sxs-lookup"><span data-stu-id="eb59d-144">Add and download the Virtual Machine Scale Set marketplace item.</span></span>

    ![Virtual Machine Scale Set](media/azure-stack-compute-add-scalesets/image02.png)

## <a name="update-images-in-a-virtual-machine-scale-set"></a><span data-ttu-id="eb59d-146">Update images in a Virtual Machine Scale Set</span><span class="sxs-lookup"><span data-stu-id="eb59d-146">Update images in a Virtual Machine Scale Set</span></span>

<span data-ttu-id="eb59d-147">After you create a virtual machine scale set, users can update images in the scale set without the scale set having to be recreated.</span><span class="sxs-lookup"><span data-stu-id="eb59d-147">After you create a virtual machine scale set, users can update images in the scale set without the scale set having to be recreated.</span></span> <span data-ttu-id="eb59d-148">The process to update an image depends on the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="eb59d-148">The process to update an image depends on the following scenarios:</span></span>

1. <span data-ttu-id="eb59d-149">Virtual machine scale set deployment template **specifies latest** for *version*:</span><span class="sxs-lookup"><span data-stu-id="eb59d-149">Virtual machine scale set deployment template **specifies latest** for *version*:</span></span>  

   <span data-ttu-id="eb59d-150">When the *version* is set as **latest** in the *imageReference* section of the template for a scale set, scale up operations on the scale set use the newest available version of the image for the scale set instances.</span><span class="sxs-lookup"><span data-stu-id="eb59d-150">When the *version* is set as **latest** in the *imageReference* section of the template for a scale set, scale up operations on the scale set use the newest available version of the image for the scale set instances.</span></span> <span data-ttu-id="eb59d-151">After a scale up is complete, you can delete older virtual machine scale sets instances.</span><span class="sxs-lookup"><span data-stu-id="eb59d-151">After a scale up is complete, you can delete older virtual machine scale sets instances.</span></span>  <span data-ttu-id="eb59d-152">(The values for *publisher*, *offer*, and *sku* remain unchanged).</span><span class="sxs-lookup"><span data-stu-id="eb59d-152">(The values for *publisher*, *offer*, and *sku* remain unchanged).</span></span> 

   <span data-ttu-id="eb59d-153">The following JSON example specifies *latest*:</span><span class="sxs-lookup"><span data-stu-id="eb59d-153">The following JSON example specifies *latest*:</span></span>  

    ```Json  
    "imageReference": {
        "publisher": "[parameters('osImagePublisher')]",
        "offer": "[parameters('osImageOffer')]",
        "sku": "[parameters('osImageSku')]",
        "version": "latest"
        }
    ```

   <span data-ttu-id="eb59d-154">Before scale up can use a new image, you must download that new image:</span><span class="sxs-lookup"><span data-stu-id="eb59d-154">Before scale up can use a new image, you must download that new image:</span></span>  

   - <span data-ttu-id="eb59d-155">When the image on the Marketplace is a newer version than the image in the scale set: Download the new image that replaces the older image.</span><span class="sxs-lookup"><span data-stu-id="eb59d-155">When the image on the Marketplace is a newer version than the image in the scale set: Download the new image that replaces the older image.</span></span> <span data-ttu-id="eb59d-156">After the image is replaced, a user can proceed to scale up.</span><span class="sxs-lookup"><span data-stu-id="eb59d-156">After the image is replaced, a user can proceed to scale up.</span></span> 

   - <span data-ttu-id="eb59d-157">When the image version on the Marketplace is the same as the image in the scale set: Delete the image that is in use in the scale set, and then download the new image.</span><span class="sxs-lookup"><span data-stu-id="eb59d-157">When the image version on the Marketplace is the same as the image in the scale set: Delete the image that is in use in the scale set, and then download the new image.</span></span> <span data-ttu-id="eb59d-158">During the time between the removal of the original image and the download of the new image, you cannot scale up.</span><span class="sxs-lookup"><span data-stu-id="eb59d-158">During the time between the removal of the original image and the download of the new image, you cannot scale up.</span></span> 
      
     <span data-ttu-id="eb59d-159">This process is required  to resyndicate images that make use of the sparse file format, introduced with version 1803.</span><span class="sxs-lookup"><span data-stu-id="eb59d-159">This process is required  to resyndicate images that make use of the sparse file format, introduced with version 1803.</span></span> 
 

2. <span data-ttu-id="eb59d-160">Virtual machine scale set deployment template **does not specify latest** for *version* and specifies a version number instead:</span><span class="sxs-lookup"><span data-stu-id="eb59d-160">Virtual machine scale set deployment template **does not specify latest** for *version* and specifies a version number instead:</span></span>  

    <span data-ttu-id="eb59d-161">If you download an image with a newer version (which changes the available version), the scale set can't scale up.</span><span class="sxs-lookup"><span data-stu-id="eb59d-161">If you download an image with a newer version (which changes the available version), the scale set can't scale up.</span></span> <span data-ttu-id="eb59d-162">This is by design as the image version specified in the scale set template must be available.</span><span class="sxs-lookup"><span data-stu-id="eb59d-162">This is by design as the image version specified in the scale set template must be available.</span></span>  

<span data-ttu-id="eb59d-163">For more information, see [operating system disks and images](.\user\azure-stack-compute-overview.md#operating-system-disks-and-images).</span><span class="sxs-lookup"><span data-stu-id="eb59d-163">For more information, see [operating system disks and images](.\user\azure-stack-compute-overview.md#operating-system-disks-and-images).</span></span>  


## <a name="scale-a-virtual-machine-scale-set"></a><span data-ttu-id="eb59d-164">Scale a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="eb59d-164">Scale a virtual machine scale set</span></span>
<span data-ttu-id="eb59d-165">You can scale the size of a *virtual machine scale set* to make it larger or smaller.</span><span class="sxs-lookup"><span data-stu-id="eb59d-165">You can scale the size of a *virtual machine scale set* to make it larger or smaller.</span></span>  

1. <span data-ttu-id="eb59d-166">In the portal, select your scale set and then select **Scaling**.</span><span class="sxs-lookup"><span data-stu-id="eb59d-166">In the portal, select your scale set and then select **Scaling**.</span></span>
2. <span data-ttu-id="eb59d-167">Use the slide-bar to set the new level of scaling for this virtual machine scale set, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="eb59d-167">Use the slide-bar to set the new level of scaling for this virtual machine scale set, and then select **Save**.</span></span>
     <span data-ttu-id="eb59d-168">![Scale the set](media/azure-stack-compute-add-scalesets/scale.png)</span><span class="sxs-lookup"><span data-stu-id="eb59d-168">![Scale the set](media/azure-stack-compute-add-scalesets/scale.png)</span></span>





## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="eb59d-169">Remove a Virtual Machine Scale Set</span><span class="sxs-lookup"><span data-stu-id="eb59d-169">Remove a Virtual Machine Scale Set</span></span>

<span data-ttu-id="eb59d-170">To remove a virtual machine scale set gallery item, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="eb59d-170">To remove a virtual machine scale set gallery item, run the following PowerShell command:</span></span>

```PowerShell  
    Remove-AzsGalleryItem
````

> [!NOTE]
> <span data-ttu-id="eb59d-171">The gallery item may not be removed immediately.</span><span class="sxs-lookup"><span data-stu-id="eb59d-171">The gallery item may not be removed immediately.</span></span> <span data-ttu-id="eb59d-172">You night need to refresh the portal several times before the item shows as removed from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="eb59d-172">You night need to refresh the portal several times before the item shows as removed from the Marketplace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb59d-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="eb59d-173">Next steps</span></span>
[<span data-ttu-id="eb59d-174">Frequently asked questions for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="eb59d-174">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)