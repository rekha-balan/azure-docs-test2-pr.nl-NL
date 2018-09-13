---
title: Manage formulas in Azure DevTest Labs to create VMs | Microsoft Docs
description: Learn how to update and remove Azure DevTest Labs formulas
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 841dd95a-657f-4d80-ba26-59a9b5104fe4
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: b7a68f545f60829e5da83f0734c57a4d210cb843
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967978"
---
# <a name="manage-azure-devtest-labs-formulas"></a><span data-ttu-id="b3db2-103">Manage Azure DevTest Labs formulas</span><span class="sxs-lookup"><span data-stu-id="b3db2-103">Manage Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="b3db2-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span><span class="sxs-lookup"><span data-stu-id="b3db2-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> <span data-ttu-id="b3db2-105">This article also guides you through managing existing formulas.</span><span class="sxs-lookup"><span data-stu-id="b3db2-105">This article also guides you through managing existing formulas.</span></span>

## <a name="create-a-formula"></a><span data-ttu-id="b3db2-106">Create a formula</span><span class="sxs-lookup"><span data-stu-id="b3db2-106">Create a formula</span></span>
<span data-ttu-id="b3db2-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span><span class="sxs-lookup"><span data-stu-id="b3db2-107">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="b3db2-108">There are two ways to create formulas:</span><span class="sxs-lookup"><span data-stu-id="b3db2-108">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="b3db2-109">From a base - Use when you want to define all the characteristics of the formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-109">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="b3db2-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span><span class="sxs-lookup"><span data-stu-id="b3db2-110">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="b3db2-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="b3db2-111">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="b3db2-112">Create a formula from a base</span><span class="sxs-lookup"><span data-stu-id="b3db2-112">Create a formula from a base</span></span>
<span data-ttu-id="b3db2-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-113">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="b3db2-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b3db2-114">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="b3db2-115">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="b3db2-115">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="b3db2-116">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="b3db2-116">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="b3db2-117">On the lab's blade, select **Formulas (reusable bases)**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-117">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formula menu](./media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="b3db2-119">On the **Formulas** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-119">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Add a formula](./media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="b3db2-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-121">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Base list](./media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="b3db2-123">On the **Create formula** blade, specify the following values:</span><span class="sxs-lookup"><span data-stu-id="b3db2-123">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="b3db2-124">**Formula name** - Enter a name for your formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-124">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="b3db2-125">This value is displayed in the list of base images when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="b3db2-125">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="b3db2-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span><span class="sxs-lookup"><span data-stu-id="b3db2-126">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="b3db2-127">**Description** - Enter a meaningful description for your formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-127">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="b3db2-128">This value is available from the formula's context menu when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="b3db2-128">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="b3db2-129">**User name** - Enter a user name that is granted administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="b3db2-129">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="b3db2-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span><span class="sxs-lookup"><span data-stu-id="b3db2-130">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="b3db2-131">To learn about saving secrets in a key vault and using them when creating lab resources, see [Store secrets in Azure Key Vault](devtest-lab-store-secrets-in-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="b3db2-131">To learn about saving secrets in a key vault and using them when creating lab resources, see [Store secrets in Azure Key Vault](devtest-lab-store-secrets-in-key-vault.md).</span></span>
    * <span data-ttu-id="b3db2-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span><span class="sxs-lookup"><span data-stu-id="b3db2-132">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="b3db2-133">\*\* Virtual machine size\*\* - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span><span class="sxs-lookup"><span data-stu-id="b3db2-133">\*\* Virtual machine size\*\* - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="b3db2-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span><span class="sxs-lookup"><span data-stu-id="b3db2-134">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="b3db2-135">For more information about artifacts, see [Create custom artifacts for your Azure DevTest Labs virtual machine](devtest-lab-artifact-author.md).</span><span class="sxs-lookup"><span data-stu-id="b3db2-135">For more information about artifacts, see [Create custom artifacts for your Azure DevTest Labs virtual machine](devtest-lab-artifact-author.md).</span></span>
    * <span data-ttu-id="b3db2-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span><span class="sxs-lookup"><span data-stu-id="b3db2-136">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="b3db2-137">**Virtual network** - Specify the desired virtual network.</span><span class="sxs-lookup"><span data-stu-id="b3db2-137">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="b3db2-138">**Subnet** - Specify the desired subnet.</span><span class="sxs-lookup"><span data-stu-id="b3db2-138">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="b3db2-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b3db2-139">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="b3db2-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="b3db2-140">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="b3db2-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span><span class="sxs-lookup"><span data-stu-id="b3db2-141">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="b3db2-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span><span class="sxs-lookup"><span data-stu-id="b3db2-142">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="b3db2-143">**Image** - This field displays name of the base image you selected on the previous blade.</span><span class="sxs-lookup"><span data-stu-id="b3db2-143">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Create formula](./media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="b3db2-145">Select **Create** to create the formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-145">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="b3db2-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span><span class="sxs-lookup"><span data-stu-id="b3db2-146">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="b3db2-147">Create a formula from a VM</span><span class="sxs-lookup"><span data-stu-id="b3db2-147">Create a formula from a VM</span></span>
<span data-ttu-id="b3db2-148">The following steps guide you through the process of creating a formula based on an existing VM.</span><span class="sxs-lookup"><span data-stu-id="b3db2-148">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="b3db2-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span><span class="sxs-lookup"><span data-stu-id="b3db2-149">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="b3db2-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b3db2-150">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="b3db2-151">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="b3db2-151">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="b3db2-152">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="b3db2-152">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="b3db2-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-153">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Labs VMs](./media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="b3db2-155">On the VM's blade, select **Create formula (reusable base)**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-155">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Create formula](./media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="b3db2-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-157">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Create formula blade](./media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="b3db2-159">Select **OK** to create the formula.</span><span class="sxs-lookup"><span data-stu-id="b3db2-159">Select **OK** to create the formula.</span></span>

## <a name="modify-a-formula"></a><span data-ttu-id="b3db2-160">Modify a formula</span><span class="sxs-lookup"><span data-stu-id="b3db2-160">Modify a formula</span></span>
<span data-ttu-id="b3db2-161">To modify a formula, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b3db2-161">To modify a formula, follow these steps:</span></span>

1. <span data-ttu-id="b3db2-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b3db2-162">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="b3db2-163">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="b3db2-163">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="b3db2-164">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="b3db2-164">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="b3db2-165">On the lab's blade, select **Formulas (reusable bases)**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-165">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formula menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="b3db2-167">On the **Lab formulas** blade, select the formula you wish to modify.</span><span class="sxs-lookup"><span data-stu-id="b3db2-167">On the **Lab formulas** blade, select the formula you wish to modify.</span></span>
6. <span data-ttu-id="b3db2-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-168">On the **Update formula** blade, make the desired edits, and select **Update**.</span></span>

## <a name="delete-a-formula"></a><span data-ttu-id="b3db2-169">Delete a formula</span><span class="sxs-lookup"><span data-stu-id="b3db2-169">Delete a formula</span></span>
<span data-ttu-id="b3db2-170">To delete a formula, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="b3db2-170">To delete a formula, follow these steps:</span></span>

1. <span data-ttu-id="b3db2-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b3db2-171">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="b3db2-172">Select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="b3db2-172">Select **All Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="b3db2-173">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="b3db2-173">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="b3db2-174">On the lab **Settings** blade, select **Formulas**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-174">On the lab **Settings** blade, select **Formulas**.</span></span>
   
    ![Formula menu](./media/devtest-lab-manage-formulas/lab-settings-formulas.png)
5. <span data-ttu-id="b3db2-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="b3db2-176">On the **Lab formulas** blade, select the ellipsis to the right of the formula you wish to delete.</span></span>
   
    ![Formula menu](./media/devtest-lab-manage-formulas/lab-formulas-blade.png)
6. <span data-ttu-id="b3db2-178">On the formula's context menu, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b3db2-178">On the formula's context menu, select **Delete**.</span></span>
   
    ![Formula context menu](./media/devtest-lab-manage-formulas/formula-delete-context-menu.png)
7. <span data-ttu-id="b3db2-180">Select **Yes** to the deletion confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="b3db2-180">Select **Yes** to the deletion confirmation dialog.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="b3db2-181">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="b3db2-181">Related blog posts</span></span>
* [<span data-ttu-id="b3db2-182">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="b3db2-182">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="b3db2-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="b3db2-183">Next steps</span></span>
<span data-ttu-id="b3db2-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b3db2-184">Once you have created a formula for use when creating a VM, the next step is to [add a VM to your lab](devtest-lab-add-vm.md).</span></span>

