---
title: Create formulas in Azure DevTest Labs | Microsoft Docs
description: Learn how to create Azure DevTest Labs formulas, and use them to create new VMs.
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
ms.date: 03/07/2017
ms.author: tarcher
ms.openlocfilehash: c24224a2f1e3411e22355483aa00c3ccd32ca166
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669767"
---
# <a name="create-azure-devtest-labs-formulas"></a><span data-ttu-id="96131-103">Create Azure DevTest Labs formulas</span><span class="sxs-lookup"><span data-stu-id="96131-103">Create Azure DevTest Labs formulas</span></span>

[!INCLUDE [devtest-lab-formula-definition](../../includes/devtest-lab-formula-definition.md)]

<span data-ttu-id="96131-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span><span class="sxs-lookup"><span data-stu-id="96131-104">This article illustrates how to create a formula from either a base (custom image, Marketplace image, or another formula) or an existing VM.</span></span> 

## <a name="create-a-formula"></a><span data-ttu-id="96131-105">Create a formula</span><span class="sxs-lookup"><span data-stu-id="96131-105">Create a formula</span></span>
<span data-ttu-id="96131-106">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span><span class="sxs-lookup"><span data-stu-id="96131-106">Anyone with DevTest Labs *Users* permissions is able to create VMs using a formula as a base.</span></span> <span data-ttu-id="96131-107">There are two ways to create formulas:</span><span class="sxs-lookup"><span data-stu-id="96131-107">There are two ways to create formulas:</span></span> 

* <span data-ttu-id="96131-108">From a base - Use when you want to define all the characteristics of the formula.</span><span class="sxs-lookup"><span data-stu-id="96131-108">From a base - Use when you want to define all the characteristics of the formula.</span></span>
* <span data-ttu-id="96131-109">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span><span class="sxs-lookup"><span data-stu-id="96131-109">From an existing lab VM - Use when you want to create a formula based on the settings of an existing VM.</span></span>

<span data-ttu-id="96131-110">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span><span class="sxs-lookup"><span data-stu-id="96131-110">For more information about adding users and permissions, see [Add owners and users in Azure DevTest Labs](./devtest-lab-add-devtest-user.md).</span></span>

### <a name="create-a-formula-from-a-base"></a><span data-ttu-id="96131-111">Create a formula from a base</span><span class="sxs-lookup"><span data-stu-id="96131-111">Create a formula from a base</span></span>
<span data-ttu-id="96131-112">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span><span class="sxs-lookup"><span data-stu-id="96131-112">The following steps guide you through the process of creating a formula from a custom image, Marketplace image, or another formula.</span></span>

1. <span data-ttu-id="96131-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="96131-113">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

2. <span data-ttu-id="96131-114">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="96131-114">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>

3. <span data-ttu-id="96131-115">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="96131-115">From the list of labs, select the desired lab.</span></span>  

4. <span data-ttu-id="96131-116">On the lab's blade, select **Formulas (reusable bases)**.</span><span class="sxs-lookup"><span data-stu-id="96131-116">On the lab's blade, select **Formulas (reusable bases)**.</span></span>
   
    ![Formula menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/lab-settings-formulas.png)

5. <span data-ttu-id="96131-118">On the **Formulas** blade, select **+ Add**.</span><span class="sxs-lookup"><span data-stu-id="96131-118">On the **Formulas** blade, select **+ Add**.</span></span>
   
    ![Add a formula](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/add-formula.png)

6. <span data-ttu-id="96131-120">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span><span class="sxs-lookup"><span data-stu-id="96131-120">On the **Choose a base** blade, select the base (custom image, Marketplace image, or formula) from which you want to create the formula.</span></span>
   
    ![Base list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/base-list.png)

7. <span data-ttu-id="96131-122">On the **Create formula** blade, specify the following values:</span><span class="sxs-lookup"><span data-stu-id="96131-122">On the **Create formula** blade, specify the following values:</span></span>
   
    * <span data-ttu-id="96131-123">**Formula name** - Enter a name for your formula.</span><span class="sxs-lookup"><span data-stu-id="96131-123">**Formula name** - Enter a name for your formula.</span></span> <span data-ttu-id="96131-124">This value is displayed in the list of base images when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="96131-124">This value is displayed in the list of base images when you create a VM.</span></span> <span data-ttu-id="96131-125">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span><span class="sxs-lookup"><span data-stu-id="96131-125">The name is validated as you type it, and if not valid, a message indicates the requirements for a valid name.</span></span>
    * <span data-ttu-id="96131-126">**Description** - Enter a meaningful description for your formula.</span><span class="sxs-lookup"><span data-stu-id="96131-126">**Description** - Enter a meaningful description for your formula.</span></span> <span data-ttu-id="96131-127">This value is available from the formula's context menu when you create a VM.</span><span class="sxs-lookup"><span data-stu-id="96131-127">This value is available from the formula's context menu when you create a VM.</span></span>
    * <span data-ttu-id="96131-128">**User name** - Enter a user name that is granted administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="96131-128">**User name** - Enter a user name that is granted administrator privileges.</span></span>
    * <span data-ttu-id="96131-129">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span><span class="sxs-lookup"><span data-stu-id="96131-129">**Password** - Enter - or select from the dropdown - a value that is associated with the secret (password) that you want to use for the specified user.</span></span> <span data-ttu-id="96131-130">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span><span class="sxs-lookup"><span data-stu-id="96131-130">For more information about the secrets, see [Azure DevTest Labs: Personal secret store](https://azure.microsoft.com/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store/).</span></span>
    * <span data-ttu-id="96131-131">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span><span class="sxs-lookup"><span data-stu-id="96131-131">**Virtual machine disk type** - Specify either HDD (hard-disk drive) or SSD (solid-state drive) to indicate which storage disk type is allowed for the virtual machines provisioned using this base image.</span></span>
    * <span data-ttu-id="96131-132">\*\* Virtual machine size\*\* - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span><span class="sxs-lookup"><span data-stu-id="96131-132">\*\* Virtual machine size\*\* - Select one of the predefined items that specify the processor cores, RAM size, and the hard drive size of the VM to create.</span></span> 
    * <span data-ttu-id="96131-133">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span><span class="sxs-lookup"><span data-stu-id="96131-133">**Artifacts** - Select to open the **Add artifacts** blade, in which you select and configure the artifacts that you want to add to the base image.</span></span> <span data-ttu-id="96131-134">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="96131-134">For more information about artifacts, see [Manage VM artifacts in Azure DevTest Labs](./devtest-lab-add-vm-with-artifacts.md).</span></span>
    * <span data-ttu-id="96131-135">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span><span class="sxs-lookup"><span data-stu-id="96131-135">**Advanced settings** - Select to open the **Advanced** blade where you configure the following settings:</span></span>
        * <span data-ttu-id="96131-136">**Virtual network** - Specify the desired virtual network.</span><span class="sxs-lookup"><span data-stu-id="96131-136">**Virtual network** - Specify the desired virtual network.</span></span>
        * <span data-ttu-id="96131-137">**Subnet** - Specify the desired subnet.</span><span class="sxs-lookup"><span data-stu-id="96131-137">**Subnet** - Specify the desired subnet.</span></span>    
        * <span data-ttu-id="96131-138">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span><span class="sxs-lookup"><span data-stu-id="96131-138">**IP address configuration** - Specify if you want the Public, Private, or Shared IP addresses.</span></span> <span data-ttu-id="96131-139">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span><span class="sxs-lookup"><span data-stu-id="96131-139">For more information about shared IP addresses, see [Understand shared IP addresses in Azure DevTest Labs](./devtest-lab-shared-ip.md).</span></span>
        * <span data-ttu-id="96131-140">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span><span class="sxs-lookup"><span data-stu-id="96131-140">**Make this machine claimable** - Making a machine "claimable" means that it will not be assigned ownership at the time of creation.</span></span> <span data-ttu-id="96131-141">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span><span class="sxs-lookup"><span data-stu-id="96131-141">Instead lab users will be able to take ownership ("claim") the machine in the lab's blade.</span></span>     
    * <span data-ttu-id="96131-142">**Image** - This field displays name of the base image you selected on the previous blade.</span><span class="sxs-lookup"><span data-stu-id="96131-142">**Image** - This field displays name of the base image you selected on the previous blade.</span></span> 
     
       ![Create formula](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/create-formula.png)

8. <span data-ttu-id="96131-144">Select **Create** to create the formula.</span><span class="sxs-lookup"><span data-stu-id="96131-144">Select **Create** to create the formula.</span></span>

9. <span data-ttu-id="96131-145">When the formula has been created, it displays in the list on the **Formulas** blade.</span><span class="sxs-lookup"><span data-stu-id="96131-145">When the formula has been created, it displays in the list on the **Formulas** blade.</span></span>

### <a name="create-a-formula-from-a-vm"></a><span data-ttu-id="96131-146">Create a formula from a VM</span><span class="sxs-lookup"><span data-stu-id="96131-146">Create a formula from a VM</span></span>
<span data-ttu-id="96131-147">The following steps guide you through the process of creating a formula based on an existing VM.</span><span class="sxs-lookup"><span data-stu-id="96131-147">The following steps guide you through the process of creating a formula based on an existing VM.</span></span> 

> [!NOTE]
> <span data-ttu-id="96131-148">To create a formula from a VM, the VM must have been created after March 30, 2016.</span><span class="sxs-lookup"><span data-stu-id="96131-148">To create a formula from a VM, the VM must have been created after March 30, 2016.</span></span> 
> 
> 

1. <span data-ttu-id="96131-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="96131-149">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
2. <span data-ttu-id="96131-150">Select **More Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="96131-150">Select **More Services**, and then select **DevTest Labs** from the list.</span></span>
3. <span data-ttu-id="96131-151">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="96131-151">From the list of labs, select the desired lab.</span></span>  
4. <span data-ttu-id="96131-152">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span><span class="sxs-lookup"><span data-stu-id="96131-152">On the lab's **Overview** blade, select the VM from which you wish to create the formula.</span></span>
   
    ![Labs VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/my-vms.png)
5. <span data-ttu-id="96131-154">On the VM's blade, select **Create formula (reusable base)**.</span><span class="sxs-lookup"><span data-stu-id="96131-154">On the VM's blade, select **Create formula (reusable base)**.</span></span>
   
    ![Create formula](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/create-formula-menu.png)
6. <span data-ttu-id="96131-156">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span><span class="sxs-lookup"><span data-stu-id="96131-156">On the **Create formula** blade, enter a **Name** and **Description** for your new formula.</span></span>
   
    ![Create formula blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-create-formulas/create-formula-blade.png)
7. <span data-ttu-id="96131-158">Select **OK** to create the formula.</span><span class="sxs-lookup"><span data-stu-id="96131-158">Select **OK** to create the formula.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="96131-159">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="96131-159">Related blog posts</span></span>
* [<span data-ttu-id="96131-160">Custom images or formulas?</span><span class="sxs-lookup"><span data-stu-id="96131-160">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="96131-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="96131-161">Next steps</span></span>
- [<span data-ttu-id="96131-162">Add a VM to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="96131-162">Add a VM to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-vm.md)
- [<span data-ttu-id="96131-163">Manage Azure DevTest Labs formulas</span><span class="sxs-lookup"><span data-stu-id="96131-163">Manage Azure DevTest Labs formulas</span></span>](devtest-lab-manage-formulas.md)






