---
title: Manage basic lab policies in Azure DevTest Labs | Microsoft Docs
description: Learn how to set some of the basic policies (settings) for a lab in DevTest Labs
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
ms.date: 03/16/2017
ms.author: tarcher
ms.openlocfilehash: 614dd60783364362982bd04b4946ca6acfc9c808
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552023"
---
# <a name="manage-basic-policies-for-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="659d4-103">Manage basic policies for a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="659d4-103">Manage basic policies for a lab in Azure DevTest Labs</span></span>

<span data-ttu-id="659d4-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span><span class="sxs-lookup"><span data-stu-id="659d4-104">Azure DevTest Labs enables you to control cost and minimize waste in your labs by managing policies (settings) for each lab.</span></span> <span data-ttu-id="659d4-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span><span class="sxs-lookup"><span data-stu-id="659d4-105">In this article, you get started with policies by learning how to set two of the most critical policies - limiting the number of virtual machines (VM) that can be created or claimed by a single user, and configuring auto-shutdown.</span></span> <span data-ttu-id="659d4-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="659d4-106">To view how to set every lab policy, see the article, [Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md).</span></span>  

## <a name="accessing-a-labs-policies-in-azure-devtest-labs"></a><span data-ttu-id="659d4-107">Accessing a lab's policies in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="659d4-107">Accessing a lab's policies in Azure DevTest Labs</span></span>
<span data-ttu-id="659d4-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span><span class="sxs-lookup"><span data-stu-id="659d4-108">The following steps guide you through setting up policies for a lab in Azure DevTest Labs:</span></span>

<span data-ttu-id="659d4-109">To view (and change) the policies for a lab, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="659d4-109">To view (and change) the policies for a lab, follow these steps:</span></span>

1. <span data-ttu-id="659d4-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="659d4-110">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

1. <span data-ttu-id="659d4-111">Select **More services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="659d4-111">Select **More services**, and then select **DevTest Labs** from the list.</span></span>

1. <span data-ttu-id="659d4-112">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="659d4-112">From the list of labs, select the desired lab.</span></span>   

1. <span data-ttu-id="659d4-113">Select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="659d4-113">Select **Configuration and policies**.</span></span>

    ![Policy settings blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/policies-menu.png)

1. <span data-ttu-id="659d4-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span><span class="sxs-lookup"><span data-stu-id="659d4-115">The **Configuration and policies** blade contains a menu of settings that you can specify.</span></span> <span data-ttu-id="659d4-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span><span class="sxs-lookup"><span data-stu-id="659d4-116">This article covers only the settings for **Virtual machines per user** and **Auto-shutdown**.</span></span> <span data-ttu-id="659d4-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span><span class="sxs-lookup"><span data-stu-id="659d4-117">To learn about the remaining settings, see [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md).</span></span> 
   
## <a name="set-virtual-machines-per-user"></a><span data-ttu-id="659d4-118">Set virtual machines per user</span><span class="sxs-lookup"><span data-stu-id="659d4-118">Set virtual machines per user</span></span>
<span data-ttu-id="659d4-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span><span class="sxs-lookup"><span data-stu-id="659d4-119">The policy for **Virtual machines per user** allows you to specify the maximum number of VMs that can be created by an individual user.</span></span> <span data-ttu-id="659d4-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span><span class="sxs-lookup"><span data-stu-id="659d4-120">If a user attempts to create or claim a VM when the user limit has been met, an error message indicates that the VM cannot be created/claimed.</span></span> 

1. <span data-ttu-id="659d4-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span><span class="sxs-lookup"><span data-stu-id="659d4-121">On the lab's **Configuration and policies** menu, select **Virtual machines per user**.</span></span>
   
    ![Virtual machines per user](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/max-vms-per-user.png)

1. <span data-ttu-id="659d4-123">Select **Yes** to limit the number of VMs per user.</span><span class="sxs-lookup"><span data-stu-id="659d4-123">Select **Yes** to limit the number of VMs per user.</span></span> <span data-ttu-id="659d4-124">If you do not want to limit the number of VMs per user, select **No**.</span><span class="sxs-lookup"><span data-stu-id="659d4-124">If you do not want to limit the number of VMs per user, select **No**.</span></span> <span data-ttu-id="659d4-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span><span class="sxs-lookup"><span data-stu-id="659d4-125">If you select **Yes**, enter a numeric value indicating the maximum number of VMs that can be created or claimed by a user.</span></span> 

1. <span data-ttu-id="659d4-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span><span class="sxs-lookup"><span data-stu-id="659d4-126">Select **Yes** to limit the number of VMs that can use SSD (solid-state disk).</span></span> <span data-ttu-id="659d4-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span><span class="sxs-lookup"><span data-stu-id="659d4-127">If you do not want to limit the number of VMs that can use SSD, select **No**.</span></span> <span data-ttu-id="659d4-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span><span class="sxs-lookup"><span data-stu-id="659d4-128">If you select **Yes**, enter a value indicating the maximum number of VMs that can be created using SSD.</span></span> 

1. <span data-ttu-id="659d4-129">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="659d4-129">Select **Save**.</span></span>

## <a name="set-auto-shutdown"></a><span data-ttu-id="659d4-130">Set auto-shutdown</span><span class="sxs-lookup"><span data-stu-id="659d4-130">Set auto-shutdown</span></span>
<span data-ttu-id="659d4-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span><span class="sxs-lookup"><span data-stu-id="659d4-131">The auto-shutdown policy helps to minimize lab waste by allowing you to specify the time that this lab's VMs shut down.</span></span>

1. <span data-ttu-id="659d4-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span><span class="sxs-lookup"><span data-stu-id="659d4-132">On the lab's **Configuration and policies** blade, select **Auto-shutdown**.</span></span>
   
    ![Auto-shutdown](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-set-lab-policy/auto-shutdown.png)

1. <span data-ttu-id="659d4-134">Select **On** to enable this policy, and **Off** to disable it.</span><span class="sxs-lookup"><span data-stu-id="659d4-134">Select **On** to enable this policy, and **Off** to disable it.</span></span>

1. <span data-ttu-id="659d4-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="659d4-135">If you enable this policy, specify the time (and time zone) to shut down all VMs in the current lab.</span></span>

1. <span data-ttu-id="659d4-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span><span class="sxs-lookup"><span data-stu-id="659d4-136">Specify **Yes** or **No** for the option to send a notification 15 minutes prior to the specified auto-shutdown time.</span></span> <span data-ttu-id="659d4-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span><span class="sxs-lookup"><span data-stu-id="659d4-137">If you specify **Yes**, enter a webhook URL endpoint to receive the notification.</span></span> <span data-ttu-id="659d4-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="659d4-138">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 

1. <span data-ttu-id="659d4-139">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="659d4-139">Select **Save**.</span></span>

    <span data-ttu-id="659d4-140">By default, once enabled, this policy applies to all VMs in the current lab.</span><span class="sxs-lookup"><span data-stu-id="659d4-140">By default, once enabled, this policy applies to all VMs in the current lab.</span></span> <span data-ttu-id="659d4-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span><span class="sxs-lookup"><span data-stu-id="659d4-141">To remove this setting from a specific VM, open the VM's blade and change its **Auto-shutdown** setting</span></span> 

## <a name="next-steps"></a><span data-ttu-id="659d4-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="659d4-142">Next steps</span></span>

- <span data-ttu-id="659d4-143">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span><span class="sxs-lookup"><span data-stu-id="659d4-143">[Define lab policies in Azure DevTest Labs](devtest-lab-set-lab-policy.md) - Learn how to modify other lab policies</span></span> 



