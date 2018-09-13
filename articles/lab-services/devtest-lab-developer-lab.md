---
title: Use Azure DevTest Labs for developers | Microsoft Docs
description: Learn how to use Azure DevTest Labs for developer scenarios.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 22e070e5-3d1a-49fe-9d4c-5e07cb0b7fe2
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 96432abe619ea23c1a06735567d00660e5430550
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857403"
---
# <a name="use-azure-devtest-labs-for-developers"></a><span data-ttu-id="605a3-103">Use Azure DevTest Labs for developers</span><span class="sxs-lookup"><span data-stu-id="605a3-103">Use Azure DevTest Labs for developers</span></span>
<span data-ttu-id="605a3-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span><span class="sxs-lookup"><span data-stu-id="605a3-104">Azure DevTest Labs can be used to implement many key scenarios, but one of the primary scenarios involves using DevTest Labs to host development machines for developers.</span></span> <span data-ttu-id="605a3-105">In this scenario, DevTest Labs provides these benefits:</span><span class="sxs-lookup"><span data-stu-id="605a3-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="605a3-106">Developers can quickly provision their development machines on demand.</span><span class="sxs-lookup"><span data-stu-id="605a3-106">Developers can quickly provision their development machines on demand.</span></span>
- <span data-ttu-id="605a3-107">Developers can easily customize their development machines whenever needed.</span><span class="sxs-lookup"><span data-stu-id="605a3-107">Developers can easily customize their development machines whenever needed.</span></span>
- <span data-ttu-id="605a3-108">Administrators can control costs by ensuring that:</span><span class="sxs-lookup"><span data-stu-id="605a3-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="605a3-109">Developers cannot get more VMs than they need for development.</span><span class="sxs-lookup"><span data-stu-id="605a3-109">Developers cannot get more VMs than they need for development.</span></span>
  - <span data-ttu-id="605a3-110">VMs are shut down when not in use.</span><span class="sxs-lookup"><span data-stu-id="605a3-110">VMs are shut down when not in use.</span></span> 

![Use DevTest Labs for training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="605a3-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-112">In this article, you learn about various Azure DevTest Labs features that can be used to meet developer requirements and the detailed steps that you can follow to set up a lab.</span></span>

## <a name="implementing-developer-environments-with-azure-devtest-labs"></a><span data-ttu-id="605a3-113">Implementing developer environments with Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="605a3-113">Implementing developer environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="605a3-114">**Create the lab**</span><span class="sxs-lookup"><span data-stu-id="605a3-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="605a3-115">Labs are the starting point in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="605a3-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="605a3-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span><span class="sxs-lookup"><span data-stu-id="605a3-116">Once you create a lab, you can perform tasks such as adding users (developers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="605a3-117">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-118">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-118">Task</span></span> | <span data-ttu-id="605a3-119">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-120">Create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="605a3-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="605a3-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="605a3-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="605a3-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span><span class="sxs-lookup"><span data-stu-id="605a3-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="605a3-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="605a3-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="605a3-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span><span class="sxs-lookup"><span data-stu-id="605a3-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="605a3-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span><span class="sxs-lookup"><span data-stu-id="605a3-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="605a3-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span><span class="sxs-lookup"><span data-stu-id="605a3-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="605a3-128">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-129">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-129">Task</span></span> | <span data-ttu-id="605a3-130">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-131">Configure Azure Marketplace images</span><span class="sxs-lookup"><span data-stu-id="605a3-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="605a3-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span><span class="sxs-lookup"><span data-stu-id="605a3-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the developers.</span></span>|
   | [<span data-ttu-id="605a3-133">Create a custom image</span><span class="sxs-lookup"><span data-stu-id="605a3-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="605a3-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span><span class="sxs-lookup"><span data-stu-id="605a3-134">Create a custom image by pre-installing the software you need so that developers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="605a3-135">Learn about image factory</span><span class="sxs-lookup"><span data-stu-id="605a3-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="605a3-136">Watch a video that describes how to set up and use an image factory.</span><span class="sxs-lookup"><span data-stu-id="605a3-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="605a3-137">**Create reusable templates for developer machines**</span><span class="sxs-lookup"><span data-stu-id="605a3-137">**Create reusable templates for developer machines**</span></span> 
   
    <span data-ttu-id="605a3-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span><span class="sxs-lookup"><span data-stu-id="605a3-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="605a3-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="605a3-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="605a3-140">Each developer can see the formula in the lab and use it to create a VM.</span><span class="sxs-lookup"><span data-stu-id="605a3-140">Each developer can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="605a3-141">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-142">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-142">Task</span></span> | <span data-ttu-id="605a3-143">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-144">Manage DevTest Labs formulas to create VMs</span><span class="sxs-lookup"><span data-stu-id="605a3-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="605a3-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="605a3-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

4. <span data-ttu-id="605a3-146">**Create artifacts to enable flexible VM customization**</span><span class="sxs-lookup"><span data-stu-id="605a3-146">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="605a3-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span><span class="sxs-lookup"><span data-stu-id="605a3-147">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="605a3-148">Artifacts can be:</span><span class="sxs-lookup"><span data-stu-id="605a3-148">Artifacts can be:</span></span>

   - <span data-ttu-id="605a3-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="605a3-149">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="605a3-150">Actions that you want to run on the VM - such as cloning a repo.</span><span class="sxs-lookup"><span data-stu-id="605a3-150">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="605a3-151">Applications that you want to test.</span><span class="sxs-lookup"><span data-stu-id="605a3-151">Applications that you want to test.</span></span>

   <span data-ttu-id="605a3-152">Many artifacts are already available out-of-the-box.</span><span class="sxs-lookup"><span data-stu-id="605a3-152">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="605a3-153">You can create your own custom artifacts if you want more customization for your specific needs.</span><span class="sxs-lookup"><span data-stu-id="605a3-153">You can create your own custom artifacts if you want more customization for your specific needs.</span></span>

   <span data-ttu-id="605a3-154">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-154">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-155">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-155">Task</span></span> | <span data-ttu-id="605a3-156">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-156">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-157">Create custom artifacts for your DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="605a3-157">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="605a3-158">Create your own custom artifacts for the virtual machines in your lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-158">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="605a3-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="605a3-159">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="605a3-160">Learn how to store your custom artifacts in your own private Git repo.</span><span class="sxs-lookup"><span data-stu-id="605a3-160">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="605a3-161">**Control costs**</span><span class="sxs-lookup"><span data-stu-id="605a3-161">**Control costs**</span></span>
   
    <span data-ttu-id="605a3-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-162">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a developer in the lab.</span></span> 
   
    <span data-ttu-id="605a3-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-163">If your developer team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="605a3-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="605a3-164">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="605a3-165">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-165">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-166">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-166">Task</span></span> | <span data-ttu-id="605a3-167">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-167">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-168">Define lab policies</span><span class="sxs-lookup"><span data-stu-id="605a3-168">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="605a3-169">Control costs by setting policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-169">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="605a3-170">Delete all the lab VMs using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="605a3-170">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-do-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="605a3-171">Delete all the labs in one operation when development is complete.</span><span class="sxs-lookup"><span data-stu-id="605a3-171">Delete all the labs in one operation when development is complete.</span></span>|

1. <span data-ttu-id="605a3-172">**Add a virtual network to a VM**</span><span class="sxs-lookup"><span data-stu-id="605a3-172">**Add a virtual network to a VM**</span></span> 
   
    <span data-ttu-id="605a3-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span><span class="sxs-lookup"><span data-stu-id="605a3-173">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="605a3-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span><span class="sxs-lookup"><span data-stu-id="605a3-174">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="605a3-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span><span class="sxs-lookup"><span data-stu-id="605a3-175">In addition, there is an Azure Active Directory domain join artifact available that will join a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="605a3-176">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-176">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-177">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-177">Task</span></span> | <span data-ttu-id="605a3-178">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-178">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-179">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="605a3-179">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="605a3-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="605a3-180">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="605a3-181">**Share the lab with each developer**</span><span class="sxs-lookup"><span data-stu-id="605a3-181">**Share the lab with each developer**</span></span>
   
    <span data-ttu-id="605a3-182">Labs can be directly accessed using a link that you share with your developers.</span><span class="sxs-lookup"><span data-stu-id="605a3-182">Labs can be directly accessed using a link that you share with your developers.</span></span> <span data-ttu-id="605a3-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="605a3-183">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="605a3-184">Developers cannot see VMs created by other developers.</span><span class="sxs-lookup"><span data-stu-id="605a3-184">Developers cannot see VMs created by other developers.</span></span>  
   
    <span data-ttu-id="605a3-185">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-186">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-186">Task</span></span> | <span data-ttu-id="605a3-187">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-188">Add a developer to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="605a3-188">Add a developer to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="605a3-189">Use the Azure portal to add developers to your lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-189">Use the Azure portal to add developers to your lab.</span></span>|
   | [<span data-ttu-id="605a3-190">Add developers to the lab using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="605a3-190">Add developers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="605a3-191">Use PowerShell to automate adding developers to your lab.</span><span class="sxs-lookup"><span data-stu-id="605a3-191">Use PowerShell to automate adding developers to your lab.</span></span> |
   | [<span data-ttu-id="605a3-192">Get a link to the lab</span><span class="sxs-lookup"><span data-stu-id="605a3-192">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="605a3-193">Learn how developers can directly access a lab via a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="605a3-193">Learn how developers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="605a3-194">**Automate lab creation for more teams**</span><span class="sxs-lookup"><span data-stu-id="605a3-194">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="605a3-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span><span class="sxs-lookup"><span data-stu-id="605a3-195">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="605a3-196">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="605a3-196">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="605a3-197">Task</span><span class="sxs-lookup"><span data-stu-id="605a3-197">Task</span></span> | <span data-ttu-id="605a3-198">What you learn</span><span class="sxs-lookup"><span data-stu-id="605a3-198">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="605a3-199">Create a lab using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="605a3-199">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-a-resource-manager-template) |<span data-ttu-id="605a3-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="605a3-200">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

