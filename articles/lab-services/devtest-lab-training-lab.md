---
title: Use Azure DevTest Labs for training | Microsoft Docs
description: Learn how to use Azure DevTest Labs for training scenarios.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.assetid: 57ff4e30-7e33-453f-9867-e19b3fdb9fe2
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: 85eddaaf101c3e85eca7514b04660163d23c1c80
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870516"
---
# <a name="use-azure-devtest-labs-for-training"></a><span data-ttu-id="9d746-103">Use Azure DevTest Labs for training</span><span class="sxs-lookup"><span data-stu-id="9d746-103">Use Azure DevTest Labs for training</span></span>
<span data-ttu-id="9d746-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span><span class="sxs-lookup"><span data-stu-id="9d746-104">Azure DevTest Labs can be used to implement many key scenarios in addition to dev/test.</span></span> <span data-ttu-id="9d746-105">One of those scenarios is to set up a lab for training.</span><span class="sxs-lookup"><span data-stu-id="9d746-105">One of those scenarios is to set up a lab for training.</span></span> <span data-ttu-id="9d746-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span><span class="sxs-lookup"><span data-stu-id="9d746-106">Azure DevTest Labs allows you to create a lab where you can provide custom templates that each trainee can use to create identical and isolated environments for training.</span></span> <span data-ttu-id="9d746-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span><span class="sxs-lookup"><span data-stu-id="9d746-107">You can apply policies to ensure that training environments are available to each trainee only when they need them and contain enough resources - such as virtual machines - required for the training.</span></span> <span data-ttu-id="9d746-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span><span class="sxs-lookup"><span data-stu-id="9d746-108">Finally, you can easily share the lab with trainees, which they can access in one click.</span></span>

![Use DevTest Labs for training](./media/devtest-lab-training-lab/devtest-lab-training.png)

<span data-ttu-id="9d746-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span><span class="sxs-lookup"><span data-stu-id="9d746-110">Azure DevTest Labs meets the following requirements that are required to conduct training in any virtual environment:</span></span> 

* <span data-ttu-id="9d746-111">Trainees cannot see VMs created by other trainees</span><span class="sxs-lookup"><span data-stu-id="9d746-111">Trainees cannot see VMs created by other trainees</span></span>
* <span data-ttu-id="9d746-112">Every training machine should be identical</span><span class="sxs-lookup"><span data-stu-id="9d746-112">Every training machine should be identical</span></span>
* <span data-ttu-id="9d746-113">Trainees can quickly provision their training environments</span><span class="sxs-lookup"><span data-stu-id="9d746-113">Trainees can quickly provision their training environments</span></span>
* <span data-ttu-id="9d746-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span><span class="sxs-lookup"><span data-stu-id="9d746-114">Control cost by ensuring that trainees cannot get more VMs than they need for the training and also shutdown VMs when they are not using them</span></span>
* <span data-ttu-id="9d746-115">Easily share the training lab with each trainee</span><span class="sxs-lookup"><span data-stu-id="9d746-115">Easily share the training lab with each trainee</span></span>
* <span data-ttu-id="9d746-116">Reuse the training lab again and again</span><span class="sxs-lookup"><span data-stu-id="9d746-116">Reuse the training lab again and again</span></span>

<span data-ttu-id="9d746-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span><span class="sxs-lookup"><span data-stu-id="9d746-117">In this article, you learn about various Azure DevTest Labs features that can be used to meet the previously described training requirements and detailed steps that you can follow to set up a lab for training.</span></span>  

## <a name="implementing-training-with-azure-devtest-labs"></a><span data-ttu-id="9d746-118">Implementing training with Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9d746-118">Implementing training with Azure DevTest Labs</span></span>
1. <span data-ttu-id="9d746-119">**Create the lab**</span><span class="sxs-lookup"><span data-stu-id="9d746-119">**Create the lab**</span></span> 
   
    <span data-ttu-id="9d746-120">Labs are the starting point in Azure DevTest Labs.</span><span class="sxs-lookup"><span data-stu-id="9d746-120">Labs are the starting point in Azure DevTest Labs.</span></span> <span data-ttu-id="9d746-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span><span class="sxs-lookup"><span data-stu-id="9d746-121">Once you create a lab, you can perform tasks such as add users (trainees) to the lab, set policies to control costs, define VM images that can create quickly, and more.</span></span>   
   
    <span data-ttu-id="9d746-122">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-122">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-123">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-123">Task</span></span> | <span data-ttu-id="9d746-124">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-124">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-125">Create a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9d746-125">Create a lab in Azure DevTest Labs</span></span>](devtest-lab-create-lab.md) |<span data-ttu-id="9d746-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d746-126">Learn how to create a lab in Azure DevTest Labs in the Azure portal.</span></span> |
2. <span data-ttu-id="9d746-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span><span class="sxs-lookup"><span data-stu-id="9d746-127">**Create training VMs in minutes using ready-made marketplace images and custom images**</span></span> 
   
    <span data-ttu-id="9d746-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-128">You can pick ready-made images from a wide variety of images in the Azure Marketplace and make them available for the trainees in the lab.</span></span> <span data-ttu-id="9d746-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-129">If the ready-made images don't meet your requirements, you can create a custom image by creating a lab VM using a ready-made image from Azure Marketplace, installing all the software that you need for the training, and saving the VM as custom image in the lab.</span></span> 
   
    <span data-ttu-id="9d746-130">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-130">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-131">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-131">Task</span></span> | <span data-ttu-id="9d746-132">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-132">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-133">Configure Azure Marketplace images</span><span class="sxs-lookup"><span data-stu-id="9d746-133">Configure Azure Marketplace images</span></span>](devtest-lab-configure-marketplace-images.md) |<span data-ttu-id="9d746-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span><span class="sxs-lookup"><span data-stu-id="9d746-134">Learn how you can whitelist Azure Marketplace images; making available for selection only the images you want for the training.</span></span> |
   | [<span data-ttu-id="9d746-135">Create a custom image</span><span class="sxs-lookup"><span data-stu-id="9d746-135">Create a custom image</span></span>](devtest-lab-create-template.md) |<span data-ttu-id="9d746-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span><span class="sxs-lookup"><span data-stu-id="9d746-136">Create a custom image by pre-installing the software you need for the training so that trainees can quickly create a VM using the custom image.</span></span> |
3. <span data-ttu-id="9d746-137">**Create reusable templates for training machines**</span><span class="sxs-lookup"><span data-stu-id="9d746-137">**Create reusable templates for training machines**</span></span> 
   
    <span data-ttu-id="9d746-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span><span class="sxs-lookup"><span data-stu-id="9d746-138">A formula in Azure DevTest Labs is a list of default property values used to create a VM.</span></span> <span data-ttu-id="9d746-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="9d746-139">You can create a formula in the lab by picking an image, a VM size (a combination of CPU and RAM), and a virtual network.</span></span> <span data-ttu-id="9d746-140">Each trainee can see the formula in the lab and use it to create a VM.</span><span class="sxs-lookup"><span data-stu-id="9d746-140">Each trainee can see the formula in the lab and use it to create a VM.</span></span> 
   
    <span data-ttu-id="9d746-141">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-141">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-142">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-142">Task</span></span> | <span data-ttu-id="9d746-143">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-143">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-144">Manage DevTest Labs formulas to create VMs</span><span class="sxs-lookup"><span data-stu-id="9d746-144">Manage DevTest Labs formulas to create VMs</span></span>](devtest-lab-manage-formulas.md) |<span data-ttu-id="9d746-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="9d746-145">Learn how you can create a formula by picking up an image, VM size (combination of CPU and RAM), and a virtual network.</span></span> |
4. <span data-ttu-id="9d746-146">**Control costs**</span><span class="sxs-lookup"><span data-stu-id="9d746-146">**Control costs**</span></span>
   
    <span data-ttu-id="9d746-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-147">Azure DevTest Labs allows you to set a policy in the lab to specify the maximum number of VMs that can be created by a trainee in the lab.</span></span> 
   
    <span data-ttu-id="9d746-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-148">If you are conducting multi-day training and want to stop all the VMs at a particular time of the day and then automatically restart them the following day, you can easily accomplish that by setting auto-shutdown and auto-start policies in the lab.</span></span> 
   
    <span data-ttu-id="9d746-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="9d746-149">Finally, when training is complete you can delete all the VMs at once by running a single PowerShell script.</span></span> 
   
    <span data-ttu-id="9d746-150">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-150">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-151">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-151">Task</span></span> | <span data-ttu-id="9d746-152">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-152">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-153">Define lab policies</span><span class="sxs-lookup"><span data-stu-id="9d746-153">Define lab policies</span></span>](devtest-lab-set-lab-policy.md) |<span data-ttu-id="9d746-154">Control costs by setting policies in the lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-154">Control costs by setting policies in the lab.</span></span> |
   | [<span data-ttu-id="9d746-155">Delete all the lab VMs using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="9d746-155">Delete all the lab VMs using a PowerShell script</span></span>](devtest-lab-faq.md#how-do-i-automate-the-process-of-deleting-all-the-vms-in-my-lab) |<span data-ttu-id="9d746-156">Delete all the labs in one operation when the training is complete.</span><span class="sxs-lookup"><span data-stu-id="9d746-156">Delete all the labs in one operation when the training is complete.</span></span> |
5. <span data-ttu-id="9d746-157">**Share the lab with each trainee**</span><span class="sxs-lookup"><span data-stu-id="9d746-157">**Share the lab with each trainee**</span></span>
   
    <span data-ttu-id="9d746-158">Labs can be directly accessed using a link that you share with your trainees.</span><span class="sxs-lookup"><span data-stu-id="9d746-158">Labs can be directly accessed using a link that you share with your trainees.</span></span> <span data-ttu-id="9d746-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span><span class="sxs-lookup"><span data-stu-id="9d746-159">Your trainees don't even have to have an Azure account, as long as they have a [Microsoft account](devtest-lab-faq.md#what-is-a-microsoft-account).</span></span> <span data-ttu-id="9d746-160">Trainees cannot see VMs created by other trainees.</span><span class="sxs-lookup"><span data-stu-id="9d746-160">Trainees cannot see VMs created by other trainees.</span></span>  
   
    <span data-ttu-id="9d746-161">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-161">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-162">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-162">Task</span></span> | <span data-ttu-id="9d746-163">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-163">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-164">Add a trainee to a lab in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9d746-164">Add a trainee to a lab in Azure DevTest Labs</span></span>](devtest-lab-add-devtest-user.md) |<span data-ttu-id="9d746-165">Use the Azure portal to add trainees to your training lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-165">Use the Azure portal to add trainees to your training lab.</span></span> |
   | [<span data-ttu-id="9d746-166">Add trainees to the lab using a PowerShell script</span><span class="sxs-lookup"><span data-stu-id="9d746-166">Add trainees to the lab using a PowerShell script</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell) |<span data-ttu-id="9d746-167">Use PowerShell to automate adding trainees to your training lab.</span><span class="sxs-lookup"><span data-stu-id="9d746-167">Use PowerShell to automate adding trainees to your training lab.</span></span> |
   | [<span data-ttu-id="9d746-168">Get a link to the lab</span><span class="sxs-lookup"><span data-stu-id="9d746-168">Get a link to the lab</span></span>](devtest-lab-faq.md#how-do-i-share-a-direct-link-to-my-lab) |<span data-ttu-id="9d746-169">Learn how a lab can be directly accessed via a hyperlink.</span><span class="sxs-lookup"><span data-stu-id="9d746-169">Learn how a lab can be directly accessed via a hyperlink.</span></span> |
6. <span data-ttu-id="9d746-170">**Reuse the lab again and again**</span><span class="sxs-lookup"><span data-stu-id="9d746-170">**Reuse the lab again and again**</span></span> 
   
    <span data-ttu-id="9d746-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span><span class="sxs-lookup"><span data-stu-id="9d746-171">You can automate lab creation, including custom settings, by creating a Resource Manager template and using it to create identical labs again and again.</span></span> 
   
    <span data-ttu-id="9d746-172">Learn more by clicking on the links in the following table:</span><span class="sxs-lookup"><span data-stu-id="9d746-172">Learn more by clicking on the links in the following table:</span></span>
   
   | <span data-ttu-id="9d746-173">Task</span><span class="sxs-lookup"><span data-stu-id="9d746-173">Task</span></span> | <span data-ttu-id="9d746-174">What you learn</span><span class="sxs-lookup"><span data-stu-id="9d746-174">What you learn</span></span> |
   | --- | --- |
   | [<span data-ttu-id="9d746-175">Create a lab using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="9d746-175">Create a lab using a Resource Manager template</span></span>](devtest-lab-faq.md#how-do-i-create-a-lab-from-a-resource-manager-template) |<span data-ttu-id="9d746-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="9d746-176">Create labs in Azure DevTest Labs using Resource Manager templates.</span></span> |

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

