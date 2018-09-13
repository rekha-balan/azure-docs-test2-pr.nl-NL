---
title: Frequently asked questions for Linux VMs in Azure | Microsoft Docs
description: Provides answers to some of the common questions about Linux virtual machines created with the Resource Manager model.
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: e32b732e6306f539e279cbbf4951ab03bd95a7b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563056"
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="6857c-103">Frequently asked question about Linux Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="6857c-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="6857c-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="6857c-104">This article addresses some common questions about Linux virtual machines created in Azure using the Resource Manager deployment model.</span></span> <span data-ttu-id="6857c-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6857c-105">For the Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="6857c-106">What can I run on an Azure VM?</span><span class="sxs-lookup"><span data-stu-id="6857c-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="6857c-107">All subscribers can run server software on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6857c-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="6857c-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="6857c-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="6857c-109">How much storage can I use with a virtual machine?</span><span class="sxs-lookup"><span data-stu-id="6857c-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="6857c-110">Each data disk can be up to 1 TB.</span><span class="sxs-lookup"><span data-stu-id="6857c-110">Each data disk can be up to 1 TB.</span></span> <span data-ttu-id="6857c-111">The number of data disks you can use depends on the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6857c-111">The number of data disks you can use depends on the size of the virtual machine.</span></span> <span data-ttu-id="6857c-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6857c-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="6857c-113">An Azure storage account provides storage for the operating system disk and any data disks.</span><span class="sxs-lookup"><span data-stu-id="6857c-113">An Azure storage account provides storage for the operating system disk and any data disks.</span></span> <span data-ttu-id="6857c-114">Each disk is a .vhd file stored as a page blob.</span><span class="sxs-lookup"><span data-stu-id="6857c-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="6857c-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span><span class="sxs-lookup"><span data-stu-id="6857c-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="6857c-116">How can I access my virtual machine?</span><span class="sxs-lookup"><span data-stu-id="6857c-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="6857c-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="6857c-117">Establish a remote connection to log on to the virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="6857c-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6857c-118">See the instructions on how to connect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="6857c-119">By default, SSH allows a maximum of 10 concurrent connections.</span><span class="sxs-lookup"><span data-stu-id="6857c-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="6857c-120">You can increase this number by editing the configuration file.</span><span class="sxs-lookup"><span data-stu-id="6857c-120">You can increase this number by editing the configuration file.</span></span>

<span data-ttu-id="6857c-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6857c-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-the-temporary-disk-devsdb1-to-store-data"></a><span data-ttu-id="6857c-122">Can I use the temporary disk (/dev/sdb1) to store data?</span><span class="sxs-lookup"><span data-stu-id="6857c-122">Can I use the temporary disk (/dev/sdb1) to store data?</span></span>
<span data-ttu-id="6857c-123">Don't use the temporary disk (/dev/sdb1) to store data.</span><span class="sxs-lookup"><span data-stu-id="6857c-123">Don't use the temporary disk (/dev/sdb1) to store data.</span></span> <span data-ttu-id="6857c-124">It is only there for temporary storage.</span><span class="sxs-lookup"><span data-stu-id="6857c-124">It is only there for temporary storage.</span></span> <span data-ttu-id="6857c-125">You risk losing data that can’t be recovered.</span><span class="sxs-lookup"><span data-stu-id="6857c-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="6857c-126">Can I copy or clone an existing Azure VM?</span><span class="sxs-lookup"><span data-stu-id="6857c-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="6857c-127">Yes.</span><span class="sxs-lookup"><span data-stu-id="6857c-127">Yes.</span></span> <span data-ttu-id="6857c-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6857c-128">For instructions, see [How to create a copy of a Linux virtual machine in the Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="6857c-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="6857c-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="6857c-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="6857c-130">The two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="6857c-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6857c-131">This registration is done automatically when a virtual machine is deployed through the Azure portal to any other region using Azure Resource Manager.</span></span> <span data-ttu-id="6857c-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6857c-132">After a virtual machine is deployed to any other Azure region, the new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-to-my-vm-after-its-created"></a><span data-ttu-id="6857c-133">Can I add a NIC to my VM after it's created?</span><span class="sxs-lookup"><span data-stu-id="6857c-133">Can I add a NIC to my VM after it's created?</span></span>
<span data-ttu-id="6857c-134">Yes, this is now possible.</span><span class="sxs-lookup"><span data-stu-id="6857c-134">Yes, this is now possible.</span></span> <span data-ttu-id="6857c-135">The VM first needs to be stopped deallocated.</span><span class="sxs-lookup"><span data-stu-id="6857c-135">The VM first needs to be stopped deallocated.</span></span> <span data-ttu-id="6857c-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span><span class="sxs-lookup"><span data-stu-id="6857c-136">Then you can add or remove a NIC (unless it's the last NIC on the VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="6857c-137">Are there any computer name requirements?</span><span class="sxs-lookup"><span data-stu-id="6857c-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="6857c-138">Yes.</span><span class="sxs-lookup"><span data-stu-id="6857c-138">Yes.</span></span> <span data-ttu-id="6857c-139">The computer name can be a maximum of 64 characters in length.</span><span class="sxs-lookup"><span data-stu-id="6857c-139">The computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="6857c-140">See [Infrastructure naming guidelines](infrastructure-naming-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span><span class="sxs-lookup"><span data-stu-id="6857c-140">See [Infrastructure naming guidelines](infrastructure-naming-guidelines.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="what-are-the-username-requirements-when-creating-a-vm"></a><span data-ttu-id="6857c-141">What are the username requirements when creating a VM?</span><span class="sxs-lookup"><span data-stu-id="6857c-141">What are the username requirements when creating a VM?</span></span>
<span data-ttu-id="6857c-142">Usernames must be 1 - 64 characters in length.</span><span class="sxs-lookup"><span data-stu-id="6857c-142">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="6857c-143">The following usernames are not allowed:</span><span class="sxs-lookup"><span data-stu-id="6857c-143">The following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-144">administrator</span><span class="sxs-lookup"><span data-stu-id="6857c-144">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-145">admin</span><span class="sxs-lookup"><span data-stu-id="6857c-145">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-146">user</span><span class="sxs-lookup"><span data-stu-id="6857c-146">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-147">user1</span><span class="sxs-lookup"><span data-stu-id="6857c-147">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-148">test</span><span class="sxs-lookup"><span data-stu-id="6857c-148">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-149">user2</span><span class="sxs-lookup"><span data-stu-id="6857c-149">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-150">test1</span><span class="sxs-lookup"><span data-stu-id="6857c-150">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-151">user3</span><span class="sxs-lookup"><span data-stu-id="6857c-151">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-152">admin1</span><span class="sxs-lookup"><span data-stu-id="6857c-152">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-153">1</span><span class="sxs-lookup"><span data-stu-id="6857c-153">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-154">123</span><span class="sxs-lookup"><span data-stu-id="6857c-154">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-155">a</span><span class="sxs-lookup"><span data-stu-id="6857c-155">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-156">actuser</span><span class="sxs-lookup"><span data-stu-id="6857c-156">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="6857c-157">adm</span><span class="sxs-lookup"><span data-stu-id="6857c-157">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-158">admin2</span><span class="sxs-lookup"><span data-stu-id="6857c-158">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-159">aspnet</span><span class="sxs-lookup"><span data-stu-id="6857c-159">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-160">backup</span><span class="sxs-lookup"><span data-stu-id="6857c-160">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-161">console</span><span class="sxs-lookup"><span data-stu-id="6857c-161">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-162">david</span><span class="sxs-lookup"><span data-stu-id="6857c-162">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-163">guest</span><span class="sxs-lookup"><span data-stu-id="6857c-163">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-164">john</span><span class="sxs-lookup"><span data-stu-id="6857c-164">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-165">owner</span><span class="sxs-lookup"><span data-stu-id="6857c-165">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-166">root</span><span class="sxs-lookup"><span data-stu-id="6857c-166">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-167">server</span><span class="sxs-lookup"><span data-stu-id="6857c-167">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-168">sql</span><span class="sxs-lookup"><span data-stu-id="6857c-168">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-169">support</span><span class="sxs-lookup"><span data-stu-id="6857c-169">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-170">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="6857c-170">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-171">sys</span><span class="sxs-lookup"><span data-stu-id="6857c-171">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="6857c-172">test2</span><span class="sxs-lookup"><span data-stu-id="6857c-172">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-173">test3</span><span class="sxs-lookup"><span data-stu-id="6857c-173">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-174">user4</span><span class="sxs-lookup"><span data-stu-id="6857c-174">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="6857c-175">user5</span><span class="sxs-lookup"><span data-stu-id="6857c-175">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-the-password-requirements-when-creating-a-vm"></a><span data-ttu-id="6857c-176">What are the password requirements when creating a VM?</span><span class="sxs-lookup"><span data-stu-id="6857c-176">What are the password requirements when creating a VM?</span></span>
<span data-ttu-id="6857c-177">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span><span class="sxs-lookup"><span data-stu-id="6857c-177">Passwords must be 6 - 72 characters in length and meet 3 out of the following 4 complexity requirements:</span></span>

* <span data-ttu-id="6857c-178">Have lower characters</span><span class="sxs-lookup"><span data-stu-id="6857c-178">Have lower characters</span></span>
* <span data-ttu-id="6857c-179">Have upper characters</span><span class="sxs-lookup"><span data-stu-id="6857c-179">Have upper characters</span></span>
* <span data-ttu-id="6857c-180">Have a digit</span><span class="sxs-lookup"><span data-stu-id="6857c-180">Have a digit</span></span>
* <span data-ttu-id="6857c-181">Have a special character (Regex match [\W_])</span><span class="sxs-lookup"><span data-stu-id="6857c-181">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="6857c-182">The following passwords are not allowed:</span><span class="sxs-lookup"><span data-stu-id="6857c-182">The following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="6857c-183">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="6857c-183">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="6857c-184">Pa$$word</span><span class="sxs-lookup"><span data-stu-id="6857c-184">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="6857c-185">Password!</span><span class="sxs-lookup"><span data-stu-id="6857c-185">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="6857c-186">Password1</span><span class="sxs-lookup"><span data-stu-id="6857c-186">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="6857c-187">Password22</span><span class="sxs-lookup"><span data-stu-id="6857c-187">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="6857c-188">iloveyou!</span><span class="sxs-lookup"><span data-stu-id="6857c-188">iloveyou!</span></span></td>
    </tr>
</table>
