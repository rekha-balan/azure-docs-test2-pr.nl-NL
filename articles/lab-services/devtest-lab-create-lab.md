---
title: Create a lab in Azure DevTest Labs | Microsoft Docs
description: Create a lab in Azure DevTest Labs for virtual machines
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 8b6d3e70-6528-42a4-a2ef-449575d0f928
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: a1e52a8ff7a2018c54c7b88b80bab3c2897b1fb4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870657"
---
# <a name="create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f32bb-103">Create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f32bb-103">Create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f32bb-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span><span class="sxs-lookup"><span data-stu-id="f32bb-104">A lab in Azure DevTest Labs is the infrastructure that encompasses a group of resources, such as Virtual Machines (VMs), that lets you better manage those resources by specifying limits and quotas.</span></span> <span data-ttu-id="f32bb-105">This article walks you through the process of creating a lab using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f32bb-105">This article walks you through the process of creating a lab using the Azure portal.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f32bb-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f32bb-106">Prerequisites</span></span>
<span data-ttu-id="f32bb-107">To create a lab, you need:</span><span class="sxs-lookup"><span data-stu-id="f32bb-107">To create a lab, you need:</span></span>

* <span data-ttu-id="f32bb-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f32bb-108">An Azure subscription.</span></span> <span data-ttu-id="f32bb-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f32bb-109">To learn about Azure purchase options, see [How to buy Azure](https://azure.microsoft.com/pricing/purchase-options/) or [Free one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="f32bb-110">You must be the owner of the subscription to create the lab.</span><span class="sxs-lookup"><span data-stu-id="f32bb-110">You must be the owner of the subscription to create the lab.</span></span>

## <a name="steps-to-create-a-lab-in-azure-devtest-labs"></a><span data-ttu-id="f32bb-111">Steps to create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="f32bb-111">Steps to create a lab in Azure DevTest Labs</span></span>
<span data-ttu-id="f32bb-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="f32bb-112">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="f32bb-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="f32bb-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="f32bb-114">From the main menu on the left side, select **All Services** (at the top of the list).</span><span class="sxs-lookup"><span data-stu-id="f32bb-114">From the main menu on the left side, select **All Services** (at the top of the list).</span></span>

    ![All services menu option](./media/devtest-lab-create-lab/more-services-menu-option.png)

1. <span data-ttu-id="f32bb-116">From the list of available services, **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="f32bb-116">From the list of available services, **DevTest Labs**.</span></span>
1. <span data-ttu-id="f32bb-117">In the **DevTest Labs** area, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f32bb-117">In the **DevTest Labs** area, select **Add**.</span></span>
   
    ![Add a lab](./media/devtest-lab-create-lab/add-lab-button.png)

1. <span data-ttu-id="f32bb-119">Under **Create a DevTest Lab**:</span><span class="sxs-lookup"><span data-stu-id="f32bb-119">Under **Create a DevTest Lab**:</span></span>
   
    1. <span data-ttu-id="f32bb-120">Enter a **Lab Name** for the new lab.</span><span class="sxs-lookup"><span data-stu-id="f32bb-120">Enter a **Lab Name** for the new lab.</span></span>
    2. <span data-ttu-id="f32bb-121">Select the **Subscription** to associate with the lab.</span><span class="sxs-lookup"><span data-stu-id="f32bb-121">Select the **Subscription** to associate with the lab.</span></span>
    3. <span data-ttu-id="f32bb-122">Select a **Location** in which to store the lab.</span><span class="sxs-lookup"><span data-stu-id="f32bb-122">Select a **Location** in which to store the lab.</span></span>
    4. <span data-ttu-id="f32bb-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span><span class="sxs-lookup"><span data-stu-id="f32bb-123">Select **Auto-shutdown** to specify if you want to enable - and define the parameters for - the automatic shutting down of all the lab's VMs.</span></span> <span data-ttu-id="f32bb-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span><span class="sxs-lookup"><span data-stu-id="f32bb-124">The auto-shutdown feature is mainly a cost-saving feature whereby you can specify when you want the VM to automatically be shut down.</span></span> <span data-ttu-id="f32bb-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span><span class="sxs-lookup"><span data-stu-id="f32bb-125">You can change auto-shutdown settings after creating the lab by following the steps outlined in the article [Manage all policies for a lab in Azure DevTest Labs](./devtest-lab-set-lab-policy.md#set-auto-shutdown).</span></span>
    1. <span data-ttu-id="f32bb-126">Enter **NAME** and **VALUE** information for **Tags** if you want to create custom tagging that is added to every resource you will create in the lab.</span><span class="sxs-lookup"><span data-stu-id="f32bb-126">Enter **NAME** and **VALUE** information for **Tags** if you want to create custom tagging that is added to every resource you will create in the lab.</span></span> <span data-ttu-id="f32bb-127">Tags are useful to help you manage and organize lab resources by category.</span><span class="sxs-lookup"><span data-stu-id="f32bb-127">Tags are useful to help you manage and organize lab resources by category.</span></span> <span data-ttu-id="f32bb-128">For more information about tags, including how to add tags after creating the lab, see [Add tags to a lab](devtest-lab-add-tag.md).</span><span class="sxs-lookup"><span data-stu-id="f32bb-128">For more information about tags, including how to add tags after creating the lab, see [Add tags to a lab](devtest-lab-add-tag.md).</span></span>
    5. <span data-ttu-id="f32bb-129">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span><span class="sxs-lookup"><span data-stu-id="f32bb-129">Select **Pin to Dashboard** if you want a shortcut of the lab to appear on the portal dashboard.</span></span>
    6. <span data-ttu-id="f32bb-130">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span><span class="sxs-lookup"><span data-stu-id="f32bb-130">Select **Automation options** to get Azure Resource Manager templates for configuration automation.</span></span> 
    7. <span data-ttu-id="f32bb-131">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f32bb-131">Select **Create**.</span></span> <span data-ttu-id="f32bb-132">You can monitor the status of the lab creation process by watching the **Notifications** area.</span><span class="sxs-lookup"><span data-stu-id="f32bb-132">You can monitor the status of the lab creation process by watching the **Notifications** area.</span></span> <span data-ttu-id="f32bb-133">Once completed, refresh the page to see the newly created lab in the list of labs.</span><span class="sxs-lookup"><span data-stu-id="f32bb-133">Once completed, refresh the page to see the newly created lab in the list of labs.</span></span>  
    
    ![Create a lab section of DevTest Labs](./media/devtest-lab-create-lab/create-devtestlab-blade.png)

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="next-steps"></a><span data-ttu-id="f32bb-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="f32bb-135">Next steps</span></span>
<span data-ttu-id="f32bb-136">Once you've created your lab, here are some next steps to consider:</span><span class="sxs-lookup"><span data-stu-id="f32bb-136">Once you've created your lab, here are some next steps to consider:</span></span>

* [<span data-ttu-id="f32bb-137">Secure access to a lab</span><span class="sxs-lookup"><span data-stu-id="f32bb-137">Secure access to a lab</span></span>](devtest-lab-add-devtest-user.md)
* [<span data-ttu-id="f32bb-138">Set lab policies</span><span class="sxs-lookup"><span data-stu-id="f32bb-138">Set lab policies</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="f32bb-139">Create a lab template</span><span class="sxs-lookup"><span data-stu-id="f32bb-139">Create a lab template</span></span>](devtest-lab-create-template.md)
* [<span data-ttu-id="f32bb-140">Create custom artifacts for your VMs</span><span class="sxs-lookup"><span data-stu-id="f32bb-140">Create custom artifacts for your VMs</span></span>](devtest-lab-artifact-author.md)
* [<span data-ttu-id="f32bb-141">Add a VM to a lab</span><span class="sxs-lookup"><span data-stu-id="f32bb-141">Add a VM to a lab</span></span>](devtest-lab-add-vm.md)

