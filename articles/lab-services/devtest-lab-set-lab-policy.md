---
title: Manage lab policies in Azure DevTest Labs | Microsoft Docs
description: Learn how to define lab policies such as VM sizes, maximum VMs per user, and shutdown automation.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.assetid: 7756aa64-49ca-45a0-9f90-0fd101c7be85
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 212afbd605e3a16da7be2c04492ec41875ff5b75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857810"
---
# <a name="manage-all-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="01752-103">Manage all policies for a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="01752-103">Manage all policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="01752-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span><span class="sxs-lookup"><span data-stu-id="01752-104">Azure DevTest Labs lets you control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="01752-105">This article explains in step-by-step detail how to set each policy.</span><span class="sxs-lookup"><span data-stu-id="01752-105">This article explains in step-by-step detail how to set each policy.</span></span>  

## <a name="set-allowed-virtual-machine-sizes"></a><span data-ttu-id="01752-106">Set allowed virtual machine sizes</span><span class="sxs-lookup"><span data-stu-id="01752-106">Set allowed virtual machine sizes</span></span>
<span data-ttu-id="01752-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span><span class="sxs-lookup"><span data-stu-id="01752-107">The policy for setting the allowed VM sizes helps to minimize lab waste by enabling you to specify which VM sizes are allowed in the lab.</span></span> <span data-ttu-id="01752-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span><span class="sxs-lookup"><span data-stu-id="01752-108">If this policy is activated, only VM sizes from this list can be used to create VMs.</span></span>

1. <span data-ttu-id="01752-109">In the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab and then select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="01752-109">In the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), select a lab and then select **Configuration and policies**.</span></span>

    ![Access the lab's configuration and policies](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="01752-111">On the lab's **Configuration and policies** pane, select **Allowed virtual machines sizes**.</span><span class="sxs-lookup"><span data-stu-id="01752-111">On the lab's **Configuration and policies** pane, select **Allowed virtual machines sizes**.</span></span>
   
    ![Allowed virtual machines sizes](./media/devtest-lab-set-lab-policy/allowed-vm-sizes.png)

1. <span data-ttu-id="01752-113">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="01752-113">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="01752-114">If you enable this policy, select one or more VM sizes that can be created in your lab.</span><span class="sxs-lookup"><span data-stu-id="01752-114">If you enable this policy, select one or more VM sizes that can be created in your lab.</span></span>

1. <span data-ttu-id="01752-115">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="01752-115">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="01752-116">Set virtual machines per user</span><span class="sxs-lookup"><span data-stu-id="01752-116">Set virtual machines per user</span></span>
<span data-ttu-id="01752-117">The policy for **Virtual machines per user** lets you specify the maximum number of VMs that can be created by an individual user.</span><span class="sxs-lookup"><span data-stu-id="01752-117">The policy for **Virtual machines per user** lets you specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="01752-118">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span><span class="sxs-lookup"><span data-stu-id="01752-118">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="01752-119">On the lab's **Configuration and policies** pane, select **Virtual machines per user**.</span><span class="sxs-lookup"><span data-stu-id="01752-119">On the lab's **Configuration and policies** pane, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="01752-121">Select **Yes** to limit the number of VMs per user.</span><span class="sxs-lookup"><span data-stu-id="01752-121">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="01752-122">If you do not want to limit the number of VMs per user, select **No**.</span><span class="sxs-lookup"><span data-stu-id="01752-122">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="01752-123">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="01752-123">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="01752-124">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="01752-124">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="01752-125">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="01752-125">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="01752-126">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="01752-126">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="01752-127">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="01752-127">Select **Save**.</span></span>

## <a name="set-virtual-machines-per-lab"></a><span data-ttu-id="01752-128">Set virtual machines per lab</span><span class="sxs-lookup"><span data-stu-id="01752-128">Set virtual machines per lab</span></span>
<span data-ttu-id="01752-129">The policy for **Virtual machines per lab** lets you specify the maximum number of VMs that can be created for the current lab.</span><span class="sxs-lookup"><span data-stu-id="01752-129">The policy for **Virtual machines per lab** lets you specify the maximum number of VMs that can be created for the current lab.</span></span> <span data-ttu-id="01752-130">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span><span class="sxs-lookup"><span data-stu-id="01752-130">If a user attempts to create a VM when the lab limit has been met, an error message indicates that the VM cannot be created.</span></span> 

1. <span data-ttu-id="01752-131">On the lab's **Configuration and policies** pane, select **Virtual machines per lab**.</span><span class="sxs-lookup"><span data-stu-id="01752-131">On the lab's **Configuration and policies** pane, select **Virtual machines per lab**.</span></span>
   
    ![Virtual machines per lab](./media/devtest-lab-set-lab-policy/max-vms-per-lab.png)

1. <span data-ttu-id="01752-133">Select **Yes** to limit the number of VMs per lab.</span><span class="sxs-lookup"><span data-stu-id="01752-133">Select **Yes** to limit the number of VMs per lab.</span></span> <span data-ttu-id="01752-134">If you do not want to limit the number of VMs per lab, select **No**.</span><span class="sxs-lookup"><span data-stu-id="01752-134">If you do not want to limit the number of VMs per lab, select **No**.</span></span> <span data-ttu-id="01752-135">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="01752-135">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="01752-136">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="01752-136">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="01752-137">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="01752-137">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="01752-138">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="01752-138">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="01752-139">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="01752-139">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="01752-140">Set auto-shutdown</span><span class="sxs-lookup"><span data-stu-id="01752-140">Set auto-shutdown</span></span>
<span data-ttu-id="01752-141">The auto-shutdown policy helps minimize lab waste by letting you specify the time that this lab's VMs shut down.</span><span class="sxs-lookup"><span data-stu-id="01752-141">The auto-shutdown policy helps minimize lab waste by letting you specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="01752-142">On the lab's **Configuration and policies** pane, select **Auto-shutdown**.</span><span class="sxs-lookup"><span data-stu-id="01752-142">On the lab's **Configuration and policies** pane, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="01752-144">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="01752-144">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="01752-145">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="01752-145">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="01752-146">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span><span class="sxs-lookup"><span data-stu-id="01752-146">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="01752-147">If you choose **Yes**, enter a webhook URL endpoint or an email address specifying where you want the notification to be posted or sent.</span><span class="sxs-lookup"><span data-stu-id="01752-147">If you choose **Yes**, enter a webhook URL endpoint or an email address specifying where you want the notification to be posted or sent.</span></span> <span data-ttu-id="01752-148">The user receives notification and is given the option to delay the shutdown.</span><span class="sxs-lookup"><span data-stu-id="01752-148">The user receives notification and is given the option to delay the shutdown.</span></span>

   <span data-ttu-id="01752-149">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="01752-149">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="01752-150">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="01752-150">Select **Save**.</span></span>

<span data-ttu-id="01752-151">By default, once enabled, this policy applies to all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="01752-151">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="01752-152">To remove this setting from a specific VM, open the VM's management pane and change its **Auto-shutdown** setting.</span><span class="sxs-lookup"><span data-stu-id="01752-152">To remove this setting from a specific VM, open the VM's management pane and change its **Auto-shutdown** setting.</span></span>

## <a name="set-auto-start"></a><span data-ttu-id="01752-153">Set auto-start</span><span class="sxs-lookup"><span data-stu-id="01752-153">Set auto-start</span></span>
<span data-ttu-id="01752-154">The auto-start policy lets you specify when the VMs in the current lab should be started.</span><span class="sxs-lookup"><span data-stu-id="01752-154">The auto-start policy lets you specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="01752-155">On the lab's **Configuration and policies** pane, select **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="01752-155">On the lab's **Configuration and policies** pane, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="01752-157">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="01752-157">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="01752-158">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span><span class="sxs-lookup"><span data-stu-id="01752-158">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="01752-159">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="01752-159">Select **Save**.</span></span>

<span data-ttu-id="01752-160">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="01752-160">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="01752-161">To apply this setting to a specific VM, open the VM's management pane and change its **Auto-start** setting.</span><span class="sxs-lookup"><span data-stu-id="01752-161">To apply this setting to a specific VM, open the VM's management pane and change its **Auto-start** setting.</span></span>

## <a name="set-expiration-date"></a><span data-ttu-id="01752-162">Set expiration date</span><span class="sxs-lookup"><span data-stu-id="01752-162">Set expiration date</span></span>
<span data-ttu-id="01752-163">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="01752-163">You can set an expiration date when you [create the VM](devtest-lab-add-vm.md).</span></span> <span data-ttu-id="01752-164">In **Advanced settings**, choose the calendar icon to specify a date on which the VM is automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="01752-164">In **Advanced settings**, choose the calendar icon to specify a date on which the VM is automatically deleted.</span></span> <span data-ttu-id="01752-165">By default, the VM never expires.</span><span class="sxs-lookup"><span data-stu-id="01752-165">By default, the VM never expires.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="01752-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="01752-166">Next steps</span></span>
<span data-ttu-id="01752-167">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span><span class="sxs-lookup"><span data-stu-id="01752-167">Once you've defined and applied the various VM policy settings for your lab, here are some things to try next:</span></span>

* <span data-ttu-id="01752-168">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span><span class="sxs-lookup"><span data-stu-id="01752-168">[Understand shared IP addresses](devtest-lab-shared-ip.md) - Explains how shared IP addresses are used in DevTest Labs to minimize the number of public IP addresses required to connect to your lab VMs.</span></span>
* <span data-ttu-id="01752-169">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span><span class="sxs-lookup"><span data-stu-id="01752-169">[Configure cost management](devtest-lab-configure-cost-management.md) - Illustrates how to use the **Monthly Estimated Cost Trend** chart</span></span>  
  <span data-ttu-id="01752-170">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span><span class="sxs-lookup"><span data-stu-id="01752-170">to view the current month's estimated cost-to-date and the projected end-of-month cost.</span></span>
* <span data-ttu-id="01752-171">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span><span class="sxs-lookup"><span data-stu-id="01752-171">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="01752-172">This article illustrates how to create a custom image from a VHD file.</span><span class="sxs-lookup"><span data-stu-id="01752-172">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="01752-173">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span><span class="sxs-lookup"><span data-stu-id="01752-173">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - Azure DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="01752-174">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="01752-174">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="01752-175">[Create a VM in a lab](devtest-lab-add-vm.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span><span class="sxs-lookup"><span data-stu-id="01752-175">[Create a VM in a lab](devtest-lab-add-vm.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

