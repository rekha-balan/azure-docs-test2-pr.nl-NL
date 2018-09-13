---
title: Manage basic lab policies in Azure DevTest Labs | Microsoft Docs
description: Learn how to set some of the basic policies (settings) for a lab in DevTest Labs
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
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 40b8fb360be7b08540e25886aaebe7f911607b6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857217"
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="50987-103">Manage basic policies for a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="50987-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="50987-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span><span class="sxs-lookup"><span data-stu-id="50987-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="50987-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span><span class="sxs-lookup"><span data-stu-id="50987-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="50987-106">To view how to set every lab policy, see [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="50987-106">To view how to set every lab policy, see [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="50987-107">Accessing a lab's policies in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="50987-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="50987-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="50987-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="50987-109">To view (and change) the policies for a lab, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="50987-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="50987-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="50987-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="50987-111">Select **All services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="50987-111">Select **All services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="50987-112">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="50987-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="50987-113">Select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="50987-113">Select **Configuration and policies**.</span></span>

    ![Policy settings pane](./media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="50987-115">The **Configuration and policies** pane contains a menu of settings that you can specify.</span><span class="sxs-lookup"><span data-stu-id="50987-115">The **Configuration and policies** pane contains a menu of settings that you can specify.</span></span> <span data-ttu-id="50987-116">This article covers only the settings for **Virtual machines per user**, **Auto-shutdown**, and **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="50987-116">This article covers only the settings for **Virtual machines per user**, **Auto-shutdown**, and **Auto-start**.</span></span> <span data-ttu-id="50987-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="50987-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="50987-118">Set virtual machines per user</span><span class="sxs-lookup"><span data-stu-id="50987-118">Set virtual machines per user</span></span>
<span data-ttu-id="50987-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span><span class="sxs-lookup"><span data-stu-id="50987-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="50987-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span><span class="sxs-lookup"><span data-stu-id="50987-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="50987-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span><span class="sxs-lookup"><span data-stu-id="50987-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](./media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="50987-123">Select **Yes** to limit the number of VMs per user.</span><span class="sxs-lookup"><span data-stu-id="50987-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="50987-124">If you do not want to limit the number of VMs per user, select **No**.</span><span class="sxs-lookup"><span data-stu-id="50987-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="50987-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="50987-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="50987-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="50987-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="50987-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="50987-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="50987-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="50987-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="50987-129">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="50987-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="50987-130">Set auto-shutdown</span><span class="sxs-lookup"><span data-stu-id="50987-130">Set auto-shutdown</span></span>
<span data-ttu-id="50987-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span><span class="sxs-lookup"><span data-stu-id="50987-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="50987-132">On the lab's **Configuration and policies** pane, select **Auto-shutdown**.</span><span class="sxs-lookup"><span data-stu-id="50987-132">On the lab's **Configuration and policies** pane, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](./media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="50987-134">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="50987-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="50987-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="50987-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="50987-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span><span class="sxs-lookup"><span data-stu-id="50987-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="50987-137">If you choose **Yes**, enter a webhook URL endpoint or email address specifying where you want the notification to be posted or sent.</span><span class="sxs-lookup"><span data-stu-id="50987-137">If you choose **Yes**, enter a webhook URL endpoint or email address specifying where you want the notification to be posted or sent.</span></span> <span data-ttu-id="50987-138">The user receives notification and is given the option to delay the shutdown.</span><span class="sxs-lookup"><span data-stu-id="50987-138">The user receives notification and is given the option to delay the shutdown.</span></span>

   <span data-ttu-id="50987-139">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="50987-139">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="50987-140">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="50987-140">Select **Save**.</span></span>

<span data-ttu-id="50987-141">By default, once enabled, this policy applies to all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="50987-141">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="50987-142">To remove this setting from a specific VM, open the VM's management pane and change its **Auto-shutdown** setting.</span><span class="sxs-lookup"><span data-stu-id="50987-142">To remove this setting from a specific VM, open the VM's management pane and change its **Auto-shutdown** setting.</span></span>

## <a name="set-auto-start"></a><span data-ttu-id="50987-143">Set auto-start</span><span class="sxs-lookup"><span data-stu-id="50987-143">Set auto-start</span></span>
<span data-ttu-id="50987-144">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span><span class="sxs-lookup"><span data-stu-id="50987-144">The auto-start policy allows you to specify when the VMs in the current lab should be started.</span></span>  

1. <span data-ttu-id="50987-145">On the lab's **Configuration and policies** pane, select **Auto-start**.</span><span class="sxs-lookup"><span data-stu-id="50987-145">On the lab's **Configuration and policies** pane, select **Auto-start**.</span></span>
   
    ![Auto-start](./media/devtest-lab-set-lab-policy/auto-start.png)

2. <span data-ttu-id="50987-147">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="50987-147">Select **On** to enable this policy, and **Off** to disable it.</span></span>

3. <span data-ttu-id="50987-148">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span><span class="sxs-lookup"><span data-stu-id="50987-148">If you enable this policy, specify the scheduled start time, time zone, and the days of the week for which the time applies.</span></span> 

4. <span data-ttu-id="50987-149">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="50987-149">Select **Save**.</span></span>

<span data-ttu-id="50987-150">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="50987-150">Once enabled, this policy is not automatically applied to any VMs in the current lab.</span></span> <span data-ttu-id="50987-151">To apply this setting to an existing VM, open the VM's management pane and change its **Auto-start** setting.</span><span class="sxs-lookup"><span data-stu-id="50987-151">To apply this setting to an existing VM, open the VM's management pane and change its **Auto-start** setting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50987-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="50987-152">Next steps</span></span>

- <span data-ttu-id="50987-153">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies.</span><span class="sxs-lookup"><span data-stu-id="50987-153">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies.</span></span>
