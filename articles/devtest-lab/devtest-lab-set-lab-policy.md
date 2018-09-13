---
title: Manage lab policies in Azure DevTest Labs | Microsoft Docs
description: Learn how to define lab policies such as VM sizes, maximum VMs per user, and shutdown automation.
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: ''
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: tarcher
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ca0eed3dd81d33a0bb656ad9205b981982cf8839
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552024"
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="d31ba-103">Manage all policies for a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="d31ba-103">Manage all policies for a lab in Azure DevTest Labs</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/How-to-set-VM-policies-in-a-DevTest-Lab/player]
> 
> 

<span data-ttu-id="d31ba-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="d31ba-105">This article explains in step-by-step detail how to set each policy.</span><span class="sxs-lookup"><span data-stu-id="d31ba-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="d31ba-106">Set allowed virtual machine sizes</span><span class="sxs-lookup"><span data-stu-id="d31ba-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="d31ba-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="d31ba-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span><span class="sxs-lookup"><span data-stu-id="d31ba-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="d31ba-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-109">On the lab's **Configuration and policies** blade, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="d31ba-111">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="d31ba-111">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="d31ba-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-112">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="d31ba-113">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-113">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="d31ba-114">Set virtual machines per user</span><span class="sxs-lookup"><span data-stu-id="d31ba-114">Set virtual machines per user</span></span>
<span data-ttu-id="d31ba-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span><span class="sxs-lookup"><span data-stu-id="d31ba-115">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="d31ba-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span><span class="sxs-lookup"><span data-stu-id="d31ba-116">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="d31ba-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-117">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="d31ba-119">Select **Yes** to limit the number of VMs per user.</span><span class="sxs-lookup"><span data-stu-id="d31ba-119">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="d31ba-120">If you do not want to limit the number of VMs per user, select **No**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-120">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="d31ba-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="d31ba-121">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="d31ba-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="d31ba-122">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="d31ba-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-123">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="d31ba-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="d31ba-124">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="d31ba-125">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-125">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="d31ba-126">Set virtual machines per lab</span><span class="sxs-lookup"><span data-stu-id="d31ba-126">Set virtual machines per lab</span></span>
<span data-ttu-id="d31ba-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-127">The policy for **Virtual machines per lab** allows you to specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="d31ba-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span><span class="sxs-lookup"><span data-stu-id="d31ba-128">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="d31ba-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-129">On the lab's **Configuration and policies** menu, select **Virtual machines per lab**.</span></span>
   
    ![Virtual machines per lab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="d31ba-131">Select **Yes** to limit the number of VMs per lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-131">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="d31ba-132">If you do not want to limit the number of VMs per lab, select **No**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-132">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="d31ba-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="d31ba-133">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="d31ba-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="d31ba-134">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="d31ba-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-135">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="d31ba-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="d31ba-136">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="d31ba-137">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-137">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="d31ba-138">Set auto-shutdown</span><span class="sxs-lookup"><span data-stu-id="d31ba-138">Set auto-shutdown</span></span>
<span data-ttu-id="d31ba-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span><span class="sxs-lookup"><span data-stu-id="d31ba-139">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="d31ba-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-140">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="d31ba-142">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="d31ba-142">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="d31ba-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-143">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="d31ba-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span><span class="sxs-lookup"><span data-stu-id="d31ba-144">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="d31ba-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span><span class="sxs-lookup"><span data-stu-id="d31ba-145">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="d31ba-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="d31ba-146">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="d31ba-147">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-147">Select **Save**.</span></span>

    <span data-ttu-id="d31ba-148">By default, once enabled, this policy applies to all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-148">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="d31ba-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span><span class="sxs-lookup"><span data-stu-id="d31ba-149">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="set-auto-start"></a><span data-ttu-id="d31ba-150">Set auto-start</span><span class="sxs-lookup"><span data-stu-id="d31ba-150">Set auto-start</span></span>
<span data-ttu-id="d31ba-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span><span class="sxs-lookup"><span data-stu-id="d31ba-151">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="d31ba-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-152">On the lab's **Configuration and policies** blade, select **Auto-start**.</span></span>
   
    ![Auto-start](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="d31ba-154">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="d31ba-154">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="d31ba-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span><span class="sxs-lookup"><span data-stu-id="d31ba-155">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="d31ba-156">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="d31ba-156">Select **Save**.</span></span>

    <span data-ttu-id="d31ba-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-157">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="d31ba-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span><span class="sxs-lookup"><span data-stu-id="d31ba-158">To apply this setting to a specific VM, open the VM's blade and change its **Auto-start** setting</span></span> 

## <a name="set-expiration-date"></a><span data-ttu-id="d31ba-159">Set expiration date</span><span class="sxs-lookup"><span data-stu-id="d31ba-159">Set expiration date</span></span>
<span data-ttu-id="d31ba-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="d31ba-160">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="d31ba-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="d31ba-161">In **Advanced settings**, choose the calendar icon to specify a date on which the VM will be automatically deleted.</span></span>  <span data-ttu-id="d31ba-162">By default, the VM will never expire.</span><span class="sxs-lookup"><span data-stu-id="d31ba-162">By default, the VM will never expire.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="d31ba-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="d31ba-163">Next steps</span></span>
<span data-ttu-id="d31ba-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span><span class="sxs-lookup"><span data-stu-id="d31ba-164">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="d31ba-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span><span class="sxs-lookup"><span data-stu-id="d31ba-165">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="d31ba-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span><span class="sxs-lookup"><span data-stu-id="d31ba-166">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="d31ba-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span><span class="sxs-lookup"><span data-stu-id="d31ba-167">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="d31ba-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span><span class="sxs-lookup"><span data-stu-id="d31ba-168">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="d31ba-169">This article illustrates how to create a custom image from a VHD file.</span><span class="sxs-lookup"><span data-stu-id="d31ba-169">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="d31ba-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span><span class="sxs-lookup"><span data-stu-id="d31ba-170">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="d31ba-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="d31ba-171">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="d31ba-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span><span class="sxs-lookup"><span data-stu-id="d31ba-172">[Create a VM in a lab](devtest-lab-add-vm-with-artifacts.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>






