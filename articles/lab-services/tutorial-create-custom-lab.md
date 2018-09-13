---
title: Create a lab using Azure DevTest Labs | Microsoft Docs
description: In this quickstart, you create a lab by using Azure DevTest Labs.
services: devtest-lab, lab-services, virtual-machines
documentationcenter: na
author: spelluru
manager: ''
editor: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 05/17/2018
ms.author: spelluru
ms.openlocfilehash: 5a93feec7996fc0ebf742b8d62b159dca5f1c1ed
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857327"
---
# <a name="tutorial-set-up-a-lab-by-using-azure-devtest-labs"></a><span data-ttu-id="334f7-103">Tutorial: Set up a lab by using Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="334f7-103">Tutorial: Set up a lab by using Azure DevTest Labs</span></span>
<span data-ttu-id="334f7-104">In this tutorial, you create a lab by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="334f7-104">In this tutorial, you create a lab by using the Azure portal.</span></span> <span data-ttu-id="334f7-105">A lab admin sets up a lab in an organization, creates VMs in the lab, and configures policies.</span><span class="sxs-lookup"><span data-stu-id="334f7-105">A lab admin sets up a lab in an organization, creates VMs in the lab, and configures policies.</span></span> <span data-ttu-id="334f7-106">Lab users (for example: developer and testers) claim VMs in the lab, connect to them, and use them.</span><span class="sxs-lookup"><span data-stu-id="334f7-106">Lab users (for example: developer and testers) claim VMs in the lab, connect to them, and use them.</span></span> 

<span data-ttu-id="334f7-107">In this tutorial, you do the following actions:</span><span class="sxs-lookup"><span data-stu-id="334f7-107">In this tutorial, you do the following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="334f7-108">Create a lab</span><span class="sxs-lookup"><span data-stu-id="334f7-108">Create a lab</span></span>
> * <span data-ttu-id="334f7-109">Add virtual machines (VM) to the lab</span><span class="sxs-lookup"><span data-stu-id="334f7-109">Add virtual machines (VM) to the lab</span></span>
> * <span data-ttu-id="334f7-110">Add a user to the Lab User role</span><span class="sxs-lookup"><span data-stu-id="334f7-110">Add a user to the Lab User role</span></span>

<span data-ttu-id="334f7-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="334f7-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="create-a-lab"></a><span data-ttu-id="334f7-112">Create a lab</span><span class="sxs-lookup"><span data-stu-id="334f7-112">Create a lab</span></span>
<span data-ttu-id="334f7-113">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="334f7-113">The following steps illustrate how to use the Azure portal to create a lab in Azure DevTest Labs.</span></span> 

1. <span data-ttu-id="334f7-114">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="334f7-114">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="334f7-115">From the main menu on the left side, select **Create a resource** (at the top of the list), point to **Developer tools**, and click **DevTest Labs**.</span><span class="sxs-lookup"><span data-stu-id="334f7-115">From the main menu on the left side, select **Create a resource** (at the top of the list), point to **Developer tools**, and click **DevTest Labs**.</span></span> 

    ![New DevTest Lab menu](./media/tutorial-create-custom-lab/new-custom-lab-menu.png)
1. <span data-ttu-id="334f7-117">In the **Create a DevTest Lab** window, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="334f7-117">In the **Create a DevTest Lab** window, do the following actions:</span></span> 
    1. <span data-ttu-id="334f7-118">For **Lab name**, enter a name for the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-118">For **Lab name**, enter a name for the lab.</span></span> 
    2. <span data-ttu-id="334f7-119">For **Subscription**, select the subscription in which you want to create the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-119">For **Subscription**, select the subscription in which you want to create the lab.</span></span> 
    3. <span data-ttu-id="334f7-120">For **Resource group**, select **Create new**, and enter a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="334f7-120">For **Resource group**, select **Create new**, and enter a name for the resource group.</span></span> 
    4. <span data-ttu-id="334f7-121">For **Location**, select the location/region in which you want the lab to be created.</span><span class="sxs-lookup"><span data-stu-id="334f7-121">For **Location**, select the location/region in which you want the lab to be created.</span></span> 
    5. <span data-ttu-id="334f7-122">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="334f7-122">Select **Create**.</span></span> 
    6. <span data-ttu-id="334f7-123">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="334f7-123">Select **Pin to dashboard**.</span></span> <span data-ttu-id="334f7-124">After you create the lab, the lab shows up in the dashboard.</span><span class="sxs-lookup"><span data-stu-id="334f7-124">After you create the lab, the lab shows up in the dashboard.</span></span> 

        ![Create a lab section of DevTest Labs](./media/tutorial-create-custom-lab/create-custom-lab-blade.png)

## <a name="add-a-vm-to-the-lab"></a><span data-ttu-id="334f7-126">Add a VM to the lab</span><span class="sxs-lookup"><span data-stu-id="334f7-126">Add a VM to the lab</span></span>

1. <span data-ttu-id="334f7-127">On the **DevTest Lab** page, select **+ Add** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="334f7-127">On the **DevTest Lab** page, select **+ Add** on the toolbar.</span></span> 

    ![Add button](./media/tutorial-create-custom-lab/add-vm-to-lab-button.png)
1. <span data-ttu-id="334f7-129">On the **Choose a base** page, search with **Ubuntu** keyword, and select one of the base images in the list.</span><span class="sxs-lookup"><span data-stu-id="334f7-129">On the **Choose a base** page, search with **Ubuntu** keyword, and select one of the base images in the list.</span></span> 
1. <span data-ttu-id="334f7-130">On the **Virtual machine** page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="334f7-130">On the **Virtual machine** page, do the following actions:</span></span> 
    1. <span data-ttu-id="334f7-131">For **Virtual machine name**, enter a name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="334f7-131">For **Virtual machine name**, enter a name for the virtual machine.</span></span> 
    2. <span data-ttu-id="334f7-132">For **User name**, enter a name for the user that has access to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="334f7-132">For **User name**, enter a name for the user that has access to the virtual machine.</span></span> 
    3. <span data-ttu-id="334f7-133">For **Type a value**, enter the password for the user.</span><span class="sxs-lookup"><span data-stu-id="334f7-133">For **Type a value**, enter the password for the user.</span></span> 
    4. <span data-ttu-id="334f7-134">Select **Advanced settings**.</span><span class="sxs-lookup"><span data-stu-id="334f7-134">Select **Advanced settings**.</span></span>
    5. <span data-ttu-id="334f7-135">For **Make this machine claimable**, select **Yes**.</span><span class="sxs-lookup"><span data-stu-id="334f7-135">For **Make this machine claimable**, select **Yes**.</span></span>
    6. <span data-ttu-id="334f7-136">Confirm that the **instance count** is set to **1**.</span><span class="sxs-lookup"><span data-stu-id="334f7-136">Confirm that the **instance count** is set to **1**.</span></span> <span data-ttu-id="334f7-137">If you set it to **2**, 2 VMs are created with names: `<base image name>00' and <base image name>01`.</span><span class="sxs-lookup"><span data-stu-id="334f7-137">If you set it to **2**, 2 VMs are created with names: `<base image name>00' and <base image name>01`.</span></span> <span data-ttu-id="334f7-138">For example: `win10vm00` and `win10vm01`.</span><span class="sxs-lookup"><span data-stu-id="334f7-138">For example: `win10vm00` and `win10vm01`.</span></span> 
    7. <span data-ttu-id="334f7-139">To close the **Advanced** page, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="334f7-139">To close the **Advanced** page, click **OK**.</span></span> 
    8. <span data-ttu-id="334f7-140">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="334f7-140">Select **Create**.</span></span> 

        ![Choose a base](./media/tutorial-create-custom-lab/new-virtual-machine.png)
    9. <span data-ttu-id="334f7-142">You see the status of the VM in the list of **Claimable virtual machines** list.</span><span class="sxs-lookup"><span data-stu-id="334f7-142">You see the status of the VM in the list of **Claimable virtual machines** list.</span></span> <span data-ttu-id="334f7-143">Creation of the virtual machine may take approximately 25 minutes.</span><span class="sxs-lookup"><span data-stu-id="334f7-143">Creation of the virtual machine may take approximately 25 minutes.</span></span> <span data-ttu-id="334f7-144">The VM is created in a separate Azure resource group, whose name starts with the name of the current resource group that has the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-144">The VM is created in a separate Azure resource group, whose name starts with the name of the current resource group that has the lab.</span></span> <span data-ttu-id="334f7-145">For example, if the lab is in `labrg`, the VM may be created in the resource group `labrg3988722144002`.</span><span class="sxs-lookup"><span data-stu-id="334f7-145">For example, if the lab is in `labrg`, the VM may be created in the resource group `labrg3988722144002`.</span></span> 

        ![VM creation status](./media/tutorial-create-custom-lab/vm-creation-status.png)
1. <span data-ttu-id="334f7-147">After the VM is created, you see it in the list of **Claimable virtual machines** in the list.</span><span class="sxs-lookup"><span data-stu-id="334f7-147">After the VM is created, you see it in the list of **Claimable virtual machines** in the list.</span></span> 

## <a name="add-a-user-to-the-lab-user-role"></a><span data-ttu-id="334f7-148">Add a user to the Lab User role</span><span class="sxs-lookup"><span data-stu-id="334f7-148">Add a user to the Lab User role</span></span>

1. <span data-ttu-id="334f7-149">Select **Configuration and policies** in the left menu.</span><span class="sxs-lookup"><span data-stu-id="334f7-149">Select **Configuration and policies** in the left menu.</span></span> 

    ![Configuration and policies](./media/tutorial-create-custom-lab/configuration-and-policies-menu.png)
1. <span data-ttu-id="334f7-151">Select **Access control (IAM)** from the menu, and select **+ Add** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="334f7-151">Select **Access control (IAM)** from the menu, and select **+ Add** on the toolbar.</span></span> 

    ![Access control - Add user button](./media/tutorial-create-custom-lab/access-control-add.png)
1. <span data-ttu-id="334f7-153">On the **Add permissions** page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="334f7-153">On the **Add permissions** page, do the following actions:</span></span>
    1. <span data-ttu-id="334f7-154">For **Role**, select **DevTest Labs User**.</span><span class="sxs-lookup"><span data-stu-id="334f7-154">For **Role**, select **DevTest Labs User**.</span></span> 
    2. <span data-ttu-id="334f7-155">Select the **user** you want to add.</span><span class="sxs-lookup"><span data-stu-id="334f7-155">Select the **user** you want to add.</span></span> 
    3. <span data-ttu-id="334f7-156">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="334f7-156">Select **Save**.</span></span>

        ![Add permissions](./media/tutorial-create-custom-lab/add-lab-user.png)
4. <span data-ttu-id="334f7-158">To close **Configuration and policies - Access control (IAM)**, select **X** in the right corner.</span><span class="sxs-lookup"><span data-stu-id="334f7-158">To close **Configuration and policies - Access control (IAM)**, select **X** in the right corner.</span></span> 

## <a name="cleanup-resources"></a><span data-ttu-id="334f7-159">Cleanup resources</span><span class="sxs-lookup"><span data-stu-id="334f7-159">Cleanup resources</span></span>
<span data-ttu-id="334f7-160">The next tutorial shows how a lab user can claim and connect to a VM in the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-160">The next tutorial shows how a lab user can claim and connect to a VM in the lab.</span></span> <span data-ttu-id="334f7-161">If you don't want to do that tutorial, and clean up the resources created as part of this tutorial, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="334f7-161">If you don't want to do that tutorial, and clean up the resources created as part of this tutorial, follow these steps:</span></span> 

1. <span data-ttu-id="334f7-162">In the Azure portal, select **Resource groups** in the menu.</span><span class="sxs-lookup"><span data-stu-id="334f7-162">In the Azure portal, select **Resource groups** in the menu.</span></span> 
2. <span data-ttu-id="334f7-163">Select your resource group in which you created the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-163">Select your resource group in which you created the lab.</span></span> 
3. <span data-ttu-id="334f7-164">Select **Delete resource group** from the toolbar.</span><span class="sxs-lookup"><span data-stu-id="334f7-164">Select **Delete resource group** from the toolbar.</span></span> <span data-ttu-id="334f7-165">Deleting a resource group deletes all the resources in the group including the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-165">Deleting a resource group deletes all the resources in the group including the lab.</span></span> 
4. <span data-ttu-id="334f7-166">Repeat these steps to delete the additional resource group created for you with the name `<your resource group name><random numbers>`.</span><span class="sxs-lookup"><span data-stu-id="334f7-166">Repeat these steps to delete the additional resource group created for you with the name `<your resource group name><random numbers>`.</span></span> <span data-ttu-id="334f7-167">For example: `splab3988722144001`.</span><span class="sxs-lookup"><span data-stu-id="334f7-167">For example: `splab3988722144001`.</span></span> <span data-ttu-id="334f7-168">The VMs are created in this resource group rather than in the resource group in which the lab exists.</span><span class="sxs-lookup"><span data-stu-id="334f7-168">The VMs are created in this resource group rather than in the resource group in which the lab exists.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="334f7-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="334f7-169">Next steps</span></span>
<span data-ttu-id="334f7-170">In this tutorial, you created a lab with a VM and gave a user access to the lab.</span><span class="sxs-lookup"><span data-stu-id="334f7-170">In this tutorial, you created a lab with a VM and gave a user access to the lab.</span></span> <span data-ttu-id="334f7-171">To learn about how to access the lab as a lab user, advance to the next tutorial:</span><span class="sxs-lookup"><span data-stu-id="334f7-171">To learn about how to access the lab as a lab user, advance to the next tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="334f7-172">Tutorial: Access the lab</span><span class="sxs-lookup"><span data-stu-id="334f7-172">Tutorial: Access the lab</span></span>](tutorial-use-custom-lab.md)

