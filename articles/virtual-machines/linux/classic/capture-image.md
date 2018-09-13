---
title: Capture an image of a Linux VM | Microsoft Docs
description: Learn how to capture an image of a Linux-based Azure virtual machine (VM) created with the classic deployment model.
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 90cdf13b9b6f5dd0fa6ad9463bb9f3e0a4f807d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555787"
---
# <a name="how-to-capture-a-classic-linux-virtual-machine-as-an-image"></a><span data-ttu-id="28320-103">How to capture a classic Linux virtual machine as an image</span><span class="sxs-lookup"><span data-stu-id="28320-103">How to capture a classic Linux virtual machine as an image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="28320-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="28320-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="28320-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="28320-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="28320-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="28320-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="28320-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28320-107">Learn how to [perform these steps using the Resource Manager model](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="28320-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span><span class="sxs-lookup"><span data-stu-id="28320-108">This article shows you how to capture a classic Azure virtual machine (VM) running Linux as an image to create other virtual machines.</span></span> <span data-ttu-id="28320-109">This image includes the OS disk and data disks attached to the VM.</span><span class="sxs-lookup"><span data-stu-id="28320-109">This image includes the OS disk and data disks attached to the VM.</span></span> <span data-ttu-id="28320-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span><span class="sxs-lookup"><span data-stu-id="28320-110">It doesn't include networking configuration, so you need to configure that when you create the other VM from the image.</span></span>

<span data-ttu-id="28320-111">Azure stores the image under **Images**, along with any images you've uploaded.</span><span class="sxs-lookup"><span data-stu-id="28320-111">Azure stores the image under **Images**, along with any images you've uploaded.</span></span> <span data-ttu-id="28320-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span><span class="sxs-lookup"><span data-stu-id="28320-112">For more information about images, see [About Virtual Machine Images in Azure][About Virtual Machine Images in Azure].</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28320-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="28320-113">Before you begin</span></span>
<span data-ttu-id="28320-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span><span class="sxs-lookup"><span data-stu-id="28320-114">These steps assume that you've already created an Azure VM using the Classic deployment model and configured the operating system, including attaching any data disks.</span></span> <span data-ttu-id="28320-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="28320-115">If you need to create a VM, read [How to Create a Linux Virtual Machine][How to Create a Linux Virtual Machine].</span></span>

## <a name="capture-the-virtual-machine"></a><span data-ttu-id="28320-116">Capture the virtual machine</span><span class="sxs-lookup"><span data-stu-id="28320-116">Capture the virtual machine</span></span>
1. <span data-ttu-id="28320-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span><span class="sxs-lookup"><span data-stu-id="28320-117">[Connect to the VM](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) using an SSH client of your choice.</span></span>
2. <span data-ttu-id="28320-118">In the SSH window, type the following command.</span><span class="sxs-lookup"><span data-stu-id="28320-118">In the SSH window, type the following command.</span></span> <span data-ttu-id="28320-119">The output from `waagent` may vary slightly depending on the version of this utility:</span><span class="sxs-lookup"><span data-stu-id="28320-119">The output from `waagent` may vary slightly depending on the version of this utility:</span></span>

    ```bash
    sudo waagent -deprovision+user
    ```

    <span data-ttu-id="28320-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="28320-120">The preceding command attempts to clean the system and make it suitable for reprovisioning.</span></span> <span data-ttu-id="28320-121">This operation performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="28320-121">This operation performs the following tasks:</span></span>

   * <span data-ttu-id="28320-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span><span class="sxs-lookup"><span data-stu-id="28320-122">Removes SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="28320-123">Clears nameserver configuration in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="28320-123">Clears nameserver configuration in /etc/resolv.conf</span></span>
   * <span data-ttu-id="28320-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span><span class="sxs-lookup"><span data-stu-id="28320-124">Removes the `root` user password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
   * <span data-ttu-id="28320-125">Removes cached DHCP client leases</span><span class="sxs-lookup"><span data-stu-id="28320-125">Removes cached DHCP client leases</span></span>
   * <span data-ttu-id="28320-126">Resets host name to localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="28320-126">Resets host name to localhost.localdomain</span></span>
   * <span data-ttu-id="28320-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span><span class="sxs-lookup"><span data-stu-id="28320-127">Deletes the last provisioned user account (obtained from /var/lib/waagent) **and associated data**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="28320-128">Deprovisioning deletes files and data to "generalize" the image.</span><span class="sxs-lookup"><span data-stu-id="28320-128">Deprovisioning deletes files and data to "generalize" the image.</span></span> <span data-ttu-id="28320-129">Only run this command on a VM that you intend to capture as a new image template.</span><span class="sxs-lookup"><span data-stu-id="28320-129">Only run this command on a VM that you intend to capture as a new image template.</span></span> <span data-ttu-id="28320-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span><span class="sxs-lookup"><span data-stu-id="28320-130">It does not guarantee that the image is cleared of all sensitive information or is suitable for redistribution to third parties.</span></span>

3. <span data-ttu-id="28320-131">Type **y** to continue.</span><span class="sxs-lookup"><span data-stu-id="28320-131">Type **y** to continue.</span></span> <span data-ttu-id="28320-132">You can add the `-force` parameter to avoid this confirmation step.</span><span class="sxs-lookup"><span data-stu-id="28320-132">You can add the `-force` parameter to avoid this confirmation step.</span></span>
4. <span data-ttu-id="28320-133">Type **Exit** to close the SSH client.</span><span class="sxs-lookup"><span data-stu-id="28320-133">Type **Exit** to close the SSH client.</span></span>

   > [!NOTE]
   > <span data-ttu-id="28320-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span><span class="sxs-lookup"><span data-stu-id="28320-134">The remaining steps assume you have already [installed the Azure CLI](../../../cli-install-nodejs.md) on your client computer.</span></span> <span data-ttu-id="28320-135">All the following steps can also be done in the [Azure classic portal][Azure classic portal].</span><span class="sxs-lookup"><span data-stu-id="28320-135">All the following steps can also be done in the [Azure classic portal][Azure classic portal].</span></span>

5. <span data-ttu-id="28320-136">From your client computer, open Azure CLI and login to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="28320-136">From your client computer, open Azure CLI and login to your Azure subscription.</span></span> <span data-ttu-id="28320-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="28320-137">For details, read [Connect to an Azure subscription from the Azure CLI](../../../xplat-cli-connect.md).</span></span>
6. <span data-ttu-id="28320-138">Make sure you are in Service Management mode:</span><span class="sxs-lookup"><span data-stu-id="28320-138">Make sure you are in Service Management mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

7. <span data-ttu-id="28320-139">Shut down the VM that is already deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="28320-139">Shut down the VM that is already deprovisioned.</span></span> <span data-ttu-id="28320-140">The following example shuts down the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="28320-140">The following example shuts down the VM named `myVM`:</span></span>

    ```azurecli
    azure vm shutdown myVM
    ```

   > [!NOTE]
   > <span data-ttu-id="28320-141">You can view a list all the VMs created in your subscription by using `azure vm list`</span><span class="sxs-lookup"><span data-stu-id="28320-141">You can view a list all the VMs created in your subscription by using `azure vm list`</span></span>

8. <span data-ttu-id="28320-142">When the VM is stopped, capture the image.</span><span class="sxs-lookup"><span data-stu-id="28320-142">When the VM is stopped, capture the image.</span></span> <span data-ttu-id="28320-143">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span><span class="sxs-lookup"><span data-stu-id="28320-143">The following example captures the VM named `myVM` and creates a generalized image named `myNewVM`:</span></span>

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    <span data-ttu-id="28320-144">The `-t` subcommand deletes the original virtual machine.</span><span class="sxs-lookup"><span data-stu-id="28320-144">The `-t` subcommand deletes the original virtual machine.</span></span>

9. <span data-ttu-id="28320-145">The new image is now available in the list of images that can be used to configure any new VM.</span><span class="sxs-lookup"><span data-stu-id="28320-145">The new image is now available in the list of images that can be used to configure any new VM.</span></span> <span data-ttu-id="28320-146">You can view it with the command:</span><span class="sxs-lookup"><span data-stu-id="28320-146">You can view it with the command:</span></span>

   ```azurecli
   azure vm image list
   ```

   <span data-ttu-id="28320-147">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span><span class="sxs-lookup"><span data-stu-id="28320-147">On the [Azure portal](http://portal.azure.com), the new image appears in the **VM images (classic)** that belongs to the **Compute** services.</span></span> <span data-ttu-id="28320-148">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span><span class="sxs-lookup"><span data-stu-id="28320-148">You can access **VM images (classic)** by clicking _More services_ at the bottom of the Azure service list, and then looking in the **Compute** services.</span></span>   

   ![Image capture successful](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/classic/media/capture-image/vmcapturedimageavailable.png)

## <a name="next-steps"></a><span data-ttu-id="28320-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="28320-150">Next steps</span></span>
<span data-ttu-id="28320-151">The image is ready to be used to create VMs.</span><span class="sxs-lookup"><span data-stu-id="28320-151">The image is ready to be used to create VMs.</span></span> <span data-ttu-id="28320-152">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span><span class="sxs-lookup"><span data-stu-id="28320-152">You can use the Azure CLI command `azure vm create` and supply the image name you created.</span></span> <span data-ttu-id="28320-153">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="28320-153">For more information, see [Using the Azure CLI with Classic deployment model](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

<span data-ttu-id="28320-154">Alternatively, use the [Azure classic portal][Azure classic portal] to create a custom VM by using the **From Gallery** method and selecting the image you created.</span><span class="sxs-lookup"><span data-stu-id="28320-154">Alternatively, use the [Azure classic portal][Azure classic portal] to create a custom VM by using the **From Gallery** method and selecting the image you created.</span></span> <span data-ttu-id="28320-155">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span><span class="sxs-lookup"><span data-stu-id="28320-155">For more information, see [How to Create a Custom VM][How to Create a Custom Virtual Machine].</span></span>

<span data-ttu-id="28320-156">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28320-156">**See also:** [Azure Linux Agent User Guide](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

[Azure classic portal]:http://manage.windowsazure.com
[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How to Create a Custom Virtual Machine]:create-custom.md
[How to Attach a Data Disk to a Virtual Machine]:attach-disk.md
[How to Create a Linux Virtual Machine]:create-custom.md

