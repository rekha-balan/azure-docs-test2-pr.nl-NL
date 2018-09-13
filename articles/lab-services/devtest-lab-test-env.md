---
title: Use Azure DevTest Labs for VM and PaaS test environments | Microsoft Docs
description: Learn how to use Azure DevTest Labs for VM and PaaS test environment scenarios.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.assetid: d4e2c334-643a-40c9-9051-625b8f39fc86
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 58ab6d502ec5397604c562aedffddb9f48cbb699
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856309"
---
# <a name="use-azure-devtest-labs-for-vm-and-paas-test-environments"></a><span data-ttu-id="ca73f-103">Use Azure DevTest Labs for VM and PaaS test environments</span><span class="sxs-lookup"><span data-stu-id="ca73f-103">Use Azure DevTest Labs for VM and PaaS test environments</span></span>

<span data-ttu-id="ca73f-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span><span class="sxs-lookup"><span data-stu-id="ca73f-104">You can use Azure DevTest Labs to implement many key scenarios, but a primary scenario involves using DevTest Labs to host machines for testers.</span></span> 

<span data-ttu-id="ca73f-105">In this scenario, DevTest Labs provides these benefits:</span><span class="sxs-lookup"><span data-stu-id="ca73f-105">In this scenario, DevTest Labs provides these benefits:</span></span>

- <span data-ttu-id="ca73f-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span><span class="sxs-lookup"><span data-stu-id="ca73f-106">Testers can test the latest version of their application by quickly provisioning Windows and Linux environments using reusable templates and artifacts.</span></span>
- <span data-ttu-id="ca73f-107">Testers can scale up their load testing by provisioning multiple test agents.</span><span class="sxs-lookup"><span data-stu-id="ca73f-107">Testers can scale up their load testing by provisioning multiple test agents.</span></span>
- <span data-ttu-id="ca73f-108">Administrators can control costs by ensuring that:</span><span class="sxs-lookup"><span data-stu-id="ca73f-108">Administrators can control costs by ensuring that:</span></span>
  - <span data-ttu-id="ca73f-109">Testers cannot get more VMs than they need.</span><span class="sxs-lookup"><span data-stu-id="ca73f-109">Testers cannot get more VMs than they need.</span></span>
  - <span data-ttu-id="ca73f-110">VMs are shut down when not in use.</span><span class="sxs-lookup"><span data-stu-id="ca73f-110">VMs are shut down when not in use.</span></span>

![Use DevTest Labs for training](./media/devtest-lab-developer-lab/devtest-lab-developer-lab.png)

<span data-ttu-id="ca73f-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-112">In this article, you learn about various Azure DevTest Labs features used to meet tester requirements and the detailed steps to follow to set up a lab.</span></span>

## <a name="implementing-test-environments-with-azure-devtest-labs"></a><span data-ttu-id="ca73f-113">Implementing test environments with Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca73f-113">Implementing test environments with Azure DevTest Labs</span></span>
1. <span data-ttu-id="ca73f-114">**Create the lab**</span><span class="sxs-lookup"><span data-stu-id="ca73f-114">**Create the lab**</span></span> 
   
    <span data-ttu-id="ca73f-115">Labs are the starting point in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="ca73f-115">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="ca73f-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span><span class="sxs-lookup"><span data-stu-id="ca73f-116">Once you create a lab, you can perform tasks such as adding users (testers) to the lab, setting policies to control costs, defining VM images that can create quickly, and more.</span></span>  
   
    <span data-ttu-id="ca73f-117">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-117">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-118">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-118">Task</span></span> | <span data-ttu-id="ca73f-119">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-119">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-120">Create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca73f-120">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="ca73f-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ca73f-121">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="ca73f-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span><span class="sxs-lookup"><span data-stu-id="ca73f-122">**Create VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="ca73f-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-123">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available in the lab.</span></span> <span data-ttu-id="ca73f-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-124">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need, and saving the VM as a custom image in the lab.</span></span>

    <span data-ttu-id="ca73f-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span><span class="sxs-lookup"><span data-stu-id="ca73f-125">If you will be using custom images, consider using an image factory to create and distribute your images.</span></span> <span data-ttu-id="ca73f-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span><span class="sxs-lookup"><span data-stu-id="ca73f-126">An image factory is a configuration-as-code solution that regularly builds and distributes your configured images automatically.</span></span> <span data-ttu-id="ca73f-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span><span class="sxs-lookup"><span data-stu-id="ca73f-127">This saves the time required to manually configure the system after a VM has been created with the base OS.</span></span>
  
    <span data-ttu-id="ca73f-128">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-128">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-129">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-129">Task</span></span> | <span data-ttu-id="ca73f-130">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-130">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-131">Configure Azure Marketplace images</span><span class="sxs-lookup"><span data-stu-id="ca73f-131">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="ca73f-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span><span class="sxs-lookup"><span data-stu-id="ca73f-132">Learn how you can whitelist Azure Marketplace images, making available for selection only the images you want for the testers.</span></span>|
   | [<span data-ttu-id="ca73f-133">Create a custom image</span><span class="sxs-lookup"><span data-stu-id="ca73f-133">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="ca73f-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span><span class="sxs-lookup"><span data-stu-id="ca73f-134">Create a custom image by pre-installing the software you need so that testers can quickly create a VM using the custom image.</span></span>|
   | [<span data-ttu-id="ca73f-135">Learn about image factory</span><span class="sxs-lookup"><span data-stu-id="ca73f-135">Learn about image factory</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2017/04/17/video-custom-image-factory-with-azure-devtest-labs/) |<span data-ttu-id="ca73f-136">Watch a video that describes how to set up and use an image factory.</span><span class="sxs-lookup"><span data-stu-id="ca73f-136">Watch a video that describes how to set up and use an image factory.</span></span>|

3. <span data-ttu-id="ca73f-137">**Create reusable templates for test machines**</span><span class="sxs-lookup"><span data-stu-id="ca73f-137">**Create reusable templates for test machines**</span></span> 
   
    <span data-ttu-id="ca73f-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span><span class="sxs-lookup"><span data-stu-id="ca73f-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="ca73f-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="ca73f-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="ca73f-140">Each tester can see the formula in the lab and use it to create a VM.</span><span class="sxs-lookup"><span data-stu-id="ca73f-140">Each tester can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="ca73f-141">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-142">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-142">Task</span></span> | <span data-ttu-id="ca73f-143">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-144">Manage DevTest Labs formulas to create VMs</span><span class="sxs-lookup"><span data-stu-id="ca73f-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="ca73f-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="ca73f-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span>|

3. <span data-ttu-id="ca73f-146">**Create multi-VM test environments**</span><span class="sxs-lookup"><span data-stu-id="ca73f-146">**Create multi-VM test environments**</span></span> 
   
    <span data-ttu-id="ca73f-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span><span class="sxs-lookup"><span data-stu-id="ca73f-147">You can use Azure Resource Manager templates to define the infrastructure and configuration of your Azure solution and repeatedly deploy multiple test VMs in a consistent state.</span></span>

    <span data-ttu-id="ca73f-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span><span class="sxs-lookup"><span data-stu-id="ca73f-148">Azure PaaS resources can be provisioned in an environment from a Resource Manager template and appear in cost tracking.</span></span> <span data-ttu-id="ca73f-149">However, VM auto shutdown does not apply to PaaS resources.</span><span class="sxs-lookup"><span data-stu-id="ca73f-149">However, VM auto shutdown does not apply to PaaS resources.</span></span>

    <span data-ttu-id="ca73f-150">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-151">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-151">Task</span></span> | <span data-ttu-id="ca73f-152">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="ca73f-153">Create multi-VM environments and PaaS resources with Azure Resource Manager templates</span></span>](devtest-lab-create-environment-from-arm.md) |<span data-ttu-id="ca73f-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span><span class="sxs-lookup"><span data-stu-id="ca73f-154">Learn how you can deploy multiple VMs in a consistent state for your test environment.</span></span>|

4. <span data-ttu-id="ca73f-155">**Create artifacts to enable flexible VM customization**</span><span class="sxs-lookup"><span data-stu-id="ca73f-155">**Create artifacts to enable flexible VM customization**</span></span>

   <span data-ttu-id="ca73f-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span><span class="sxs-lookup"><span data-stu-id="ca73f-156">Artifacts are used to deploy and configure your application after a VM is provisioned.</span></span> <span data-ttu-id="ca73f-157">Artifacts can be:</span><span class="sxs-lookup"><span data-stu-id="ca73f-157">Artifacts can be:</span></span>

   - <span data-ttu-id="ca73f-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ca73f-158">Tools that you want to install on the VM - such as agents, Fiddler, and Visual Studio.</span></span>
   - <span data-ttu-id="ca73f-159">Actions that you want to run on the VM - such as cloning a repo.</span><span class="sxs-lookup"><span data-stu-id="ca73f-159">Actions that you want to run on the VM - such as cloning a repo.</span></span>
   - <span data-ttu-id="ca73f-160">Applications that you want to test.</span><span class="sxs-lookup"><span data-stu-id="ca73f-160">Applications that you want to test.</span></span>

   <span data-ttu-id="ca73f-161">Many artifacts are already available out-of-the-box.</span><span class="sxs-lookup"><span data-stu-id="ca73f-161">Many artifacts are already available out-of-the-box.</span></span> <span data-ttu-id="ca73f-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span><span class="sxs-lookup"><span data-stu-id="ca73f-162">But if you want more customization for your specific needs, you can create your own custom artifacts.</span></span>

   <span data-ttu-id="ca73f-163">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-163">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-164">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-164">Task</span></span> | <span data-ttu-id="ca73f-165">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-165">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-166">Create custom artifacts for your DevTest Labs VM</span><span class="sxs-lookup"><span data-stu-id="ca73f-166">Create custom artifacts for your DevTest Labs VM</span></span>](devtest-lab-artifact-author.md) |<span data-ttu-id="ca73f-167">Create your own custom artifacts for the virtual machines in your lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-167">Create your own custom artifacts for the virtual machines in your lab.</span></span>|
   | [<span data-ttu-id="ca73f-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca73f-168">Add a Git repository to store custom artifacts and Azure Resource Manager templates for use in Azure DevTest Labs</span></span>](devtest-lab-add-artifact-repo.md) |<span data-ttu-id="ca73f-169">Learn how to store your custom artifacts in your own private Git repo.</span><span class="sxs-lookup"><span data-stu-id="ca73f-169">Learn how to store your custom artifacts in your own private Git repo.</span></span>|

5. <span data-ttu-id="ca73f-170">**Control costs**</span><span class="sxs-lookup"><span data-stu-id="ca73f-170">**Control costs**</span></span>
   
    <span data-ttu-id="ca73f-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-171">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a tester in the lab.</span></span> 
   
    <span data-ttu-id="ca73f-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-172">If your test team has a set work schedule and you want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="ca73f-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="ca73f-173">Finally, when app development is complete, you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="ca73f-174">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-174">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-175">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-175">Task</span></span> | <span data-ttu-id="ca73f-176">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-176">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-177">Define lab policies</span><span class="sxs-lookup"><span data-stu-id="ca73f-177">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="ca73f-178">Control costs by setting policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-178">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="ca73f-179">Delete all the lab VMs using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ca73f-179">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-do-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="ca73f-180">Delete all the labs in one operation when testing is complete.</span><span class="sxs-lookup"><span data-stu-id="ca73f-180">Delete all the labs in one operation when testing is complete.</span></span>|

1. <span data-ttu-id="ca73f-181">**Add a virtual network to a Lab**</span><span class="sxs-lookup"><span data-stu-id="ca73f-181">**Add a virtual network to a Lab**</span></span> 
   
    <span data-ttu-id="ca73f-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span><span class="sxs-lookup"><span data-stu-id="ca73f-182">DevTest Labs creates a new virtual network (VNET) whenever a lab is created.</span></span> <span data-ttu-id="ca73f-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span><span class="sxs-lookup"><span data-stu-id="ca73f-183">If you have configured your own VNET – for example, by using ExpressRoute or site-to-site VPN – you can add this VNET to your lab's virtual network settings so that it is available when creating VMs.</span></span>

    <span data-ttu-id="ca73f-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span><span class="sxs-lookup"><span data-stu-id="ca73f-184">In addition, there is an Azure Active Directory domain join artifact available that joins a VM to a domain when the VM is being created.</span></span> 
   
    <span data-ttu-id="ca73f-185">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-185">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-186">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-186">Task</span></span> | <span data-ttu-id="ca73f-187">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-187">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-188">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca73f-188">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md) |<span data-ttu-id="ca73f-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ca73f-189">Learn how to configure a virtual network in Azure DevTest Labs using the Azure portal.</span></span>|

6. <span data-ttu-id="ca73f-190">**Share the lab with each tester**</span><span class="sxs-lookup"><span data-stu-id="ca73f-190">**Share the lab with each tester**</span></span>
   
    <span data-ttu-id="ca73f-191">Labs can be directly accessed using a link that you share with your testers.</span><span class="sxs-lookup"><span data-stu-id="ca73f-191">Labs can be directly accessed using a link that you share with your testers.</span></span> <span data-ttu-id="ca73f-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="ca73f-192">They don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="ca73f-193">Testers cannot see VMs created by other testers.</span><span class="sxs-lookup"><span data-stu-id="ca73f-193">Testers cannot see VMs created by other testers.</span></span>  
   
    <span data-ttu-id="ca73f-194">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-194">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-195">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-195">Task</span></span> | <span data-ttu-id="ca73f-196">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-196">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-197">Add a tester to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="ca73f-197">Add a tester to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="ca73f-198">Use the Azure portal to add testers to your lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-198">Use the Azure portal to add testers to your lab.</span></span>|
   | [<span data-ttu-id="ca73f-199">Add testers to the lab using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="ca73f-199">Add testers to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="ca73f-200">Use PowerShell to automate adding testers to your lab.</span><span class="sxs-lookup"><span data-stu-id="ca73f-200">Use PowerShell to automate adding testers to your lab.</span></span> |
   | [<span data-ttu-id="ca73f-201">Get a link to the lab</span><span class="sxs-lookup"><span data-stu-id="ca73f-201">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="ca73f-202">Learn how testers can directly access a lab via a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="ca73f-202">Learn how testers can directly access a lab via a hyperlink.</span></span>|

7. <span data-ttu-id="ca73f-203">**Automate lab creation for more teams**</span><span class="sxs-lookup"><span data-stu-id="ca73f-203">**Automate lab creation for more teams**</span></span> 
   
    <span data-ttu-id="ca73f-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span><span class="sxs-lookup"><span data-stu-id="ca73f-204">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="ca73f-205">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="ca73f-205">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="ca73f-206">Task</span><span class="sxs-lookup"><span data-stu-id="ca73f-206">Task</span></span> | <span data-ttu-id="ca73f-207">What you learn</span><span class="sxs-lookup"><span data-stu-id="ca73f-207">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="ca73f-208">Create a lab using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="ca73f-208">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-a-resource-manager-template) |<span data-ttu-id="ca73f-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="ca73f-209">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

