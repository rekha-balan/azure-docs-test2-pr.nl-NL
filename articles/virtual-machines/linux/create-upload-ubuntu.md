---
title: Create and upload an Ubuntu Linux VHD in Azure
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains an Ubuntu Linux operating system.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 3e097959-84fc-4f6a-8cc8-35e087fd1542
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 1cb80ebcc725f744786372de9fa794c2ddae8f46
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555008"
---
# <a name="prepare-an-ubuntu-virtual-machine-for-azure"></a><span data-ttu-id="db184-103">Prepare an Ubuntu virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="db184-103">Prepare an Ubuntu virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="official-ubuntu-cloud-images"></a><span data-ttu-id="db184-104">Official Ubuntu cloud images</span><span class="sxs-lookup"><span data-stu-id="db184-104">Official Ubuntu cloud images</span></span>
<span data-ttu-id="db184-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span><span class="sxs-lookup"><span data-stu-id="db184-105">Ubuntu now publishes official Azure VHDs for download at [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/).</span></span> <span data-ttu-id="db184-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span><span class="sxs-lookup"><span data-stu-id="db184-106">If you need to build your own specialized Ubuntu image for Azure, rather than use the manual procedure below it is recommended to start with these known working VHDs and customize as needed.</span></span> <span data-ttu-id="db184-107">The latest image releases can always be found at the following locations:</span><span class="sxs-lookup"><span data-stu-id="db184-107">The latest image releases can always be found at the following locations:</span></span>

* <span data-ttu-id="db184-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/precise/release/ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="db184-108">Ubuntu 12.04/Precise: [ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/precise/release/ubuntu-12.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="db184-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="db184-109">Ubuntu 14.04/Trusty: [ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/trusty/release/ubuntu-14.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>
* <span data-ttu-id="db184-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span><span class="sxs-lookup"><span data-stu-id="db184-110">Ubuntu 16.04/Xenial: [ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip](http://cloud-images.ubuntu.com/releases/xenial/release/ubuntu-16.04-server-cloudimg-amd64-disk1.vhd.zip)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db184-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="db184-111">Prerequisites</span></span>
<span data-ttu-id="db184-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="db184-112">This article assumes that you have already installed an Ubuntu Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="db184-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="db184-113">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="db184-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="db184-114">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="db184-115">**Ubuntu installation notes**</span><span class="sxs-lookup"><span data-stu-id="db184-115">**Ubuntu installation notes**</span></span>

* <span data-ttu-id="db184-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span><span class="sxs-lookup"><span data-stu-id="db184-116">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="db184-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span><span class="sxs-lookup"><span data-stu-id="db184-117">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="db184-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="db184-118">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="db184-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span><span class="sxs-lookup"><span data-stu-id="db184-119">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="db184-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="db184-120">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="db184-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="db184-121">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="db184-122">Do not configure a swap partition on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="db184-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="db184-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="db184-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="db184-124">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="db184-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="db184-125">All of the VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="db184-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="manual-steps"></a><span data-ttu-id="db184-126">Manual steps</span><span class="sxs-lookup"><span data-stu-id="db184-126">Manual steps</span></span>
> [!NOTE]
> <span data-ttu-id="db184-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span><span class="sxs-lookup"><span data-stu-id="db184-127">Before attempting to create your own custom Ubuntu image for Azure, please consider using the pre-built and tested images from [http://cloud-images.ubuntu.com/](http://cloud-images.ubuntu.com/) instead.</span></span>
> 
> 

1. <span data-ttu-id="db184-128">In the center pane of Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db184-128">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="db184-129">Click **Connect** to open the window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="db184-129">Click **Connect** to open the window for the virtual machine.</span></span>

3. <span data-ttu-id="db184-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span><span class="sxs-lookup"><span data-stu-id="db184-130">Replace the current repositories in the image to use Ubuntu's Azure repos.</span></span> <span data-ttu-id="db184-131">The steps vary slightly depending on the Ubuntu version.</span><span class="sxs-lookup"><span data-stu-id="db184-131">The steps vary slightly depending on the Ubuntu version.</span></span>
   
    <span data-ttu-id="db184-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span><span class="sxs-lookup"><span data-stu-id="db184-132">Before editing `/etc/apt/sources.list`, it is recommended to make a backup:</span></span>
   
        # sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak

    <span data-ttu-id="db184-133">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="db184-133">Ubuntu 12.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="db184-134">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="db184-134">Ubuntu 14.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

    <span data-ttu-id="db184-135">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="db184-135">Ubuntu 16.04:</span></span>
   
        # sudo sed -i 's/[a-z][a-z].archive.ubuntu.com/azure.archive.ubuntu.com/g' /etc/apt/sources.list
        # sudo apt-get update

4. <span data-ttu-id="db184-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span><span class="sxs-lookup"><span data-stu-id="db184-136">The Ubuntu Azure images are now following the *hardware enablement* (HWE) kernel.</span></span> <span data-ttu-id="db184-137">Update the operating system to the latest kernel by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="db184-137">Update the operating system to the latest kernel by running the following commands:</span></span>

    <span data-ttu-id="db184-138">Ubuntu 12.04:</span><span class="sxs-lookup"><span data-stu-id="db184-138">Ubuntu 12.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-generic-lts-trusty linux-cloud-tools-generic-lts-trusty
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot
   
    <span data-ttu-id="db184-139">Ubuntu 14.04:</span><span class="sxs-lookup"><span data-stu-id="db184-139">Ubuntu 14.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-image-virtual-lts-vivid linux-lts-vivid-tools-common
        # sudo apt-get install hv-kvp-daemon-init
        (recommended) sudo apt-get dist-upgrade
   
        # sudo reboot

    <span data-ttu-id="db184-140">Ubuntu 16.04:</span><span class="sxs-lookup"><span data-stu-id="db184-140">Ubuntu 16.04:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install linux-generic-hwe-16.04 linux-cloud-tools-generic-hwe-16.04
        (recommended) sudo apt-get dist-upgrade

        # sudo reboot

    <span data-ttu-id="db184-141">**See also:**</span><span class="sxs-lookup"><span data-stu-id="db184-141">**See also:**</span></span>
    - [https://wiki.ubuntu.com/Kernel/LTSEnablementStack](https://wiki.ubuntu.com/Kernel/LTSEnablementStack)
    - [https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack](https://wiki.ubuntu.com/Kernel/RollingLTSEnablementStack)


5. <span data-ttu-id="db184-142">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="db184-142">Modify the kernel boot line for Grub to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="db184-143">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span><span class="sxs-lookup"><span data-stu-id="db184-143">To do this open `/etc/default/grub` in a text editor, find the variable called `GRUB_CMDLINE_LINUX_DEFAULT` (or add it if needed) and edit it to include the following parameters:</span></span>
   
        GRUB_CMDLINE_LINUX_DEFAULT="console=tty1 console=ttyS0,115200n8 earlyprintk=ttyS0,115200 rootdelay=300"

    <span data-ttu-id="db184-144">Save and close this file, and then run `sudo update-grub`.</span><span class="sxs-lookup"><span data-stu-id="db184-144">Save and close this file, and then run `sudo update-grub`.</span></span> <span data-ttu-id="db184-145">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="db184-145">This will ensure all console messages are sent to the first serial port, which can assist Azure technical support with debugging issues.</span></span>

6. <span data-ttu-id="db184-146">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="db184-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="db184-147">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="db184-147">This is usually the default.</span></span>

7. <span data-ttu-id="db184-148">Install the Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="db184-148">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install walinuxagent

    >[!Note]
    <span data-ttu-id="db184-149">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span><span class="sxs-lookup"><span data-stu-id="db184-149">The `walinuxagent` package may remove the `NetworkManager` and `NetworkManager-gnome` packages, if they are installed.</span></span>

8. <span data-ttu-id="db184-150">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="db184-150">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

9. <span data-ttu-id="db184-151">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="db184-151">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="db184-152">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="db184-152">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db184-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="db184-153">Next steps</span></span>
<span data-ttu-id="db184-154">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="db184-154">You're now ready to use your Ubuntu Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="db184-155">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="db184-155">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

## <a name="references"></a><span data-ttu-id="db184-156">References</span><span class="sxs-lookup"><span data-stu-id="db184-156">References</span></span>
<span data-ttu-id="db184-157">Ubuntu hardware enablement (HWE) kernel:</span><span class="sxs-lookup"><span data-stu-id="db184-157">Ubuntu hardware enablement (HWE) kernel:</span></span>

* [http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html](http://blog.utlemming.org/2015/01/ubuntu-1404-azure-images-now-tracking.html)
* [http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html](http://blog.utlemming.org/2015/02/1204-azure-cloud-images-now-using-hwe.html)

