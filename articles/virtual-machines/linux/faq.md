---
title: Frequently asked questions for Linux VMs in Azure | Microsoft Docs
description: Provides answers to some of the common questions about Linux virtual machines created with the Resource Manager model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2018
ms.author: cynthn
ms.openlocfilehash: c8fb34bf7ad1ef85d0b84a1f9f9e907bba46797d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44820981"
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="b7715-103">Frequently asked question about Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="b7715-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="b7715-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="b7715-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="b7715-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b7715-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="b7715-106">What can I run on an Azure VM?</span><span class="sxs-lookup"><span data-stu-id="b7715-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="b7715-107">All subscribers can run server software on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b7715-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="b7715-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="b7715-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="b7715-109">How much storage can I use with a virtual machine?</span><span class="sxs-lookup"><span data-stu-id="b7715-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="b7715-110">Each data disk can be up to 4 TB (4,095 GB).</span><span class="sxs-lookup"><span data-stu-id="b7715-110">Each data disk can be up to 4 TB (4,095 GB).</span></span> <span data-ttu-id="b7715-111">The number of data disks you can use depends on the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b7715-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="b7715-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7715-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="b7715-113">Azure Managed Disks are the recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data.</span><span class="sxs-lookup"><span data-stu-id="b7715-113">Azure Managed Disks are the recommended disk storage offerings for use with Azure Virtual Machines for persistent storage of data.</span></span> <span data-ttu-id="b7715-114">You can use multiple Managed Disks with each Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="b7715-114">You can use multiple Managed Disks with each Virtual Machine.</span></span> <span data-ttu-id="b7715-115">Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.</span><span class="sxs-lookup"><span data-stu-id="b7715-115">Managed Disks offer two types of durable storage options: Premium and Standard Managed Disks.</span></span> <span data-ttu-id="b7715-116">For pricing information, see [Managed Disks Pricing](https://azure.microsoft.com/pricing/details/managed-disks).</span><span class="sxs-lookup"><span data-stu-id="b7715-116">For pricing information, see [Managed Disks Pricing](https://azure.microsoft.com/pricing/details/managed-disks).</span></span>

<span data-ttu-id="b7715-117">Azure storage accounts can also provide storage for the operating system disk and any data disks.</span><span class="sxs-lookup"><span data-stu-id="b7715-117">Azure storage accounts can also provide storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="b7715-118">Each disk is a .vhd file stored as a page blob.</span><span class="sxs-lookup"><span data-stu-id="b7715-118">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="b7715-119">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="b7715-119">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="b7715-120">How can I access my virtual machine?</span><span class="sxs-lookup"><span data-stu-id="b7715-120">How can I access my virtual machine?</span></span>
<span data-ttu-id="b7715-121">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="b7715-121">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="b7715-122">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7715-122">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="b7715-123">By default, SSH allows a maximum of 10 concurrent connections.</span><span class="sxs-lookup"><span data-stu-id="b7715-123">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="b7715-124">You can increase this number by editing the configuration file.</span><span class="sxs-lookup"><span data-stu-id="b7715-124">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="b7715-125">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7715-125">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="b7715-126">Can I use the temporary disk (/dev/sdb1) to store data?</span><span class="sxs-lookup"><span data-stu-id="b7715-126">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="b7715-127">Don't use the temporary disk (/dev/sdb1) to store data.</span><span class="sxs-lookup"><span data-stu-id="b7715-127">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="b7715-128">It is only there for temporary storage.</span><span class="sxs-lookup"><span data-stu-id="b7715-128">It is only there for temporary storage.</span></span> <span data-ttu-id="b7715-129">You risk losing data that can’t be recovered.</span><span class="sxs-lookup"><span data-stu-id="b7715-129">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="b7715-130">Can I copy or clone an existing Azure VM?</span><span class="sxs-lookup"><span data-stu-id="b7715-130">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="b7715-131">Yes.</span><span class="sxs-lookup"><span data-stu-id="b7715-131">Yes.</span></span> <span data-ttu-id="b7715-132">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b7715-132">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="b7715-133">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="b7715-133">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="b7715-134">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b7715-134">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="b7715-135">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b7715-135">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="b7715-136">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b7715-136">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="b7715-137">Can I add a NIC to my VM after it's created?</span><span class="sxs-lookup"><span data-stu-id="b7715-137">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="b7715-138">Yes, this is now possible.</span><span class="sxs-lookup"><span data-stu-id="b7715-138">Yes, this is now possible.</span></span> <span data-ttu-id="b7715-139">The VM first needs to be stopped deallocated.</span><span class="sxs-lookup"><span data-stu-id="b7715-139">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="b7715-140">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span><span class="sxs-lookup"><span data-stu-id="b7715-140">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="b7715-141">Are there any computer name requirements?</span><span class="sxs-lookup"><span data-stu-id="b7715-141">Are there any computer name requirements?</span></span>
<span data-ttu-id="b7715-142">Yes.</span><span class="sxs-lookup"><span data-stu-id="b7715-142">Yes.</span></span> <span data-ttu-id="b7715-143">The computer name can be a maximum of 64 characters in length.</span><span class="sxs-lookup"><span data-stu-id="b7715-143">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="b7715-144">See [Naming conventions rules and restrictions](/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span><span class="sxs-lookup"><span data-stu-id="b7715-144">See [Naming conventions rules and restrictions](/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="b7715-145">Are there any resource group name requirements?</span><span class="sxs-lookup"><span data-stu-id="b7715-145">Are there any resource group name requirements?</span></span>
<span data-ttu-id="b7715-146">Yes.</span><span class="sxs-lookup"><span data-stu-id="b7715-146">Yes.</span></span> <span data-ttu-id="b7715-147">The resource group name can be a maximum of 90 characters in length.</span><span class="sxs-lookup"><span data-stu-id="b7715-147">The resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="b7715-148">See [Naming conventions rules and restrictions](/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span><span class="sxs-lookup"><span data-stu-id="b7715-148">See [Naming conventions rules and restrictions](/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="b7715-149">What are the username requirements when creating a VM?</span><span class="sxs-lookup"><span data-stu-id="b7715-149">What are the username requirements when creating a VM?</span></span>

<span data-ttu-id="b7715-150">Usernames should be 1 - 32 characters in length.</span><span class="sxs-lookup"><span data-stu-id="b7715-150">Usernames should be 1 - 32 characters in length.</span></span>

<span data-ttu-id="b7715-151">The following usernames are not allowed:</span><span class="sxs-lookup"><span data-stu-id="b7715-151">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-152">administrator</span><span class="sxs-lookup"><span data-stu-id="b7715-152">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-153">admin</span><span class="sxs-lookup"><span data-stu-id="b7715-153">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-154">user</span><span class="sxs-lookup"><span data-stu-id="b7715-154">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-155">user1</span><span class="sxs-lookup"><span data-stu-id="b7715-155">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-156">test</span><span class="sxs-lookup"><span data-stu-id="b7715-156">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-157">user2</span><span class="sxs-lookup"><span data-stu-id="b7715-157">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-158">test1</span><span class="sxs-lookup"><span data-stu-id="b7715-158">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-159">user3</span><span class="sxs-lookup"><span data-stu-id="b7715-159">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-160">admin1</span><span class="sxs-lookup"><span data-stu-id="b7715-160">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-161">1</span><span class="sxs-lookup"><span data-stu-id="b7715-161">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-162">123</span><span class="sxs-lookup"><span data-stu-id="b7715-162">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-163">a</span><span class="sxs-lookup"><span data-stu-id="b7715-163">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-164">actuser</span><span class="sxs-lookup"><span data-stu-id="b7715-164">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="b7715-165">adm</span><span class="sxs-lookup"><span data-stu-id="b7715-165">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-166">admin2</span><span class="sxs-lookup"><span data-stu-id="b7715-166">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-167">aspnet</span><span class="sxs-lookup"><span data-stu-id="b7715-167">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-168">backup</span><span class="sxs-lookup"><span data-stu-id="b7715-168">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-169">console</span><span class="sxs-lookup"><span data-stu-id="b7715-169">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-170">david</span><span class="sxs-lookup"><span data-stu-id="b7715-170">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-171">guest</span><span class="sxs-lookup"><span data-stu-id="b7715-171">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-172">john</span><span class="sxs-lookup"><span data-stu-id="b7715-172">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-173">owner</span><span class="sxs-lookup"><span data-stu-id="b7715-173">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-174">root</span><span class="sxs-lookup"><span data-stu-id="b7715-174">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-175">server</span><span class="sxs-lookup"><span data-stu-id="b7715-175">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-176">sql</span><span class="sxs-lookup"><span data-stu-id="b7715-176">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-177">support</span><span class="sxs-lookup"><span data-stu-id="b7715-177">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-178">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="b7715-178">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-179">sys</span><span class="sxs-lookup"><span data-stu-id="b7715-179">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="b7715-180">test2</span><span class="sxs-lookup"><span data-stu-id="b7715-180">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-181">test3</span><span class="sxs-lookup"><span data-stu-id="b7715-181">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-182">user4</span><span class="sxs-lookup"><span data-stu-id="b7715-182">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="b7715-183">user5</span><span class="sxs-lookup"><span data-stu-id="b7715-183">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="b7715-184">What are the password requirements when creating a VM?</span><span class="sxs-lookup"><span data-stu-id="b7715-184">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="b7715-185">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span><span class="sxs-lookup"><span data-stu-id="b7715-185">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="b7715-186">Have lower characters</span><span class="sxs-lookup"><span data-stu-id="b7715-186">Have lower characters</span></span>
* <span data-ttu-id="b7715-187">Have upper characters</span><span class="sxs-lookup"><span data-stu-id="b7715-187">Have upper characters</span></span>
* <span data-ttu-id="b7715-188">Have a digit</span><span class="sxs-lookup"><span data-stu-id="b7715-188">Have a digit</span></span>
* <span data-ttu-id="b7715-189">Have a special character (Regex match [\W_])</span><span class="sxs-lookup"><span data-stu-id="b7715-189">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="b7715-190">The following passwords are not allowed:</span><span class="sxs-lookup"><span data-stu-id="b7715-190">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="b7715-191">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="b7715-191">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="b7715-192">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="b7715-192">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="b7715-193">Password!</span><span class="sxs-lookup"><span data-stu-id="b7715-193">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="b7715-194">Password1</span><span class="sxs-lookup"><span data-stu-id="b7715-194">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="b7715-195">Password22</span><span class="sxs-lookup"><span data-stu-id="b7715-195">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="b7715-196">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="b7715-196">iloveyou!</span></span></td>
    </tr>
</table>
