---
title: Prepare an Debian Linux VHD in Azure | Microsoft Docs
description: Learn how to create Debian 7 & 8 VHD files for deployment in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: a6de7a7c-cc70-44e7-aed0-2ae6884d401a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: e9b1aa5e9ba9b3f9f6674b3a8eaa44e1b5d97009
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556018"
---
# <a name="prepare-a-debian-vhd-for-azure"></a><span data-ttu-id="455c5-103">Prepare a Debian VHD for Azure</span><span class="sxs-lookup"><span data-stu-id="455c5-103">Prepare a Debian VHD for Azure</span></span>
## <a name="prerequisites"></a><span data-ttu-id="455c5-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="455c5-104">Prerequisites</span></span>
<span data-ttu-id="455c5-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="455c5-105">This section assumes that you have already installed a Debian Linux operating system from an .iso file downloaded from the [Debian website](https://www.debian.org/distrib/) to a virtual hard disk.</span></span> <span data-ttu-id="455c5-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span><span class="sxs-lookup"><span data-stu-id="455c5-106">Multiple tools exist to create .vhd files; Hyper-V is only one example.</span></span> <span data-ttu-id="455c5-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="455c5-107">For instructions using Hyper-V, see [Install the Hyper-V Role and Configure a Virtual Machine](https://technet.microsoft.com/library/hh846766.aspx).</span></span>

## <a name="installation-notes"></a><span data-ttu-id="455c5-108">Installation notes</span><span class="sxs-lookup"><span data-stu-id="455c5-108">Installation notes</span></span>
* <span data-ttu-id="455c5-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span><span class="sxs-lookup"><span data-stu-id="455c5-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="455c5-110">The newer VHDX format is not supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="455c5-110">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="455c5-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="455c5-111">You can convert the disk to VHD format using Hyper-V Manager or the **convert-vhd** cmdlet.</span></span>
* <span data-ttu-id="455c5-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span><span class="sxs-lookup"><span data-stu-id="455c5-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="455c5-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="455c5-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="455c5-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="455c5-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="455c5-115">Do not configure a swap partition on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="455c5-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="455c5-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="455c5-116">The Azure Linux agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="455c5-117">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="455c5-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="455c5-118">All of the VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="455c5-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-azure-manage-to-create-debian-vhds"></a><span data-ttu-id="455c5-119">Use Azure-Manage to create Debian VHDs</span><span class="sxs-lookup"><span data-stu-id="455c5-119">Use Azure-Manage to create Debian VHDs</span></span>
<span data-ttu-id="455c5-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span><span class="sxs-lookup"><span data-stu-id="455c5-120">There are tools available for generating Debian VHDs for Azure, such as the [azure-manage](https://github.com/credativ/azure-manage) scripts from [credativ](http://www.credativ.com/).</span></span> <span data-ttu-id="455c5-121">This is the recommended approach versus creating an image from scratch.</span><span class="sxs-lookup"><span data-stu-id="455c5-121">This is the recommended approach versus creating an image from scratch.</span></span> <span data-ttu-id="455c5-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span><span class="sxs-lookup"><span data-stu-id="455c5-122">For example, to create a Debian 8 VHD run the following commands to download azure-manage (and dependencies) and run the azure_build_image script:</span></span>

    # sudo apt-get update
    # sudo apt-get install git qemu-utils mbr kpartx debootstrap

    # sudo apt-get install python3-pip python3-dateutil python3-cryptography
    # sudo pip3 install azure-storage azure-servicemanagement-legacy azure-common pytest pyyaml
    # git clone https://github.com/credativ/azure-manage.git
    # cd azure-manage
    # sudo pip3 install .

    # sudo azure_build_image --option release=jessie --option image_size_gb=30 --option image_prefix=debian-jessie-azure section


## <a name="manually-prepare-a-debian-vhd"></a><span data-ttu-id="455c5-123">Manually prepare a Debian VHD</span><span class="sxs-lookup"><span data-stu-id="455c5-123">Manually prepare a Debian VHD</span></span>
1. <span data-ttu-id="455c5-124">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="455c5-124">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="455c5-125">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="455c5-125">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="455c5-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span><span class="sxs-lookup"><span data-stu-id="455c5-126">Comment out the line for **deb cdrom** in `/etc/apt/source.list` if you set up the VM against an ISO file.</span></span>
4. <span data-ttu-id="455c5-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="455c5-127">Edit the `/etc/default/grub` file and modify the **GRUB_CMDLINE_LINUX** parameter as follows to include additional kernel parameters for Azure.</span></span>
   
        GRUB_CMDLINE_LINUX="console=tty0 console=ttyS0,115200 earlyprintk=ttyS0,115200 rootdelay=30"
5. <span data-ttu-id="455c5-128">Rebuild the grub and run:</span><span class="sxs-lookup"><span data-stu-id="455c5-128">Rebuild the grub and run:</span></span>
   
        # sudo update-grub
6. <span data-ttu-id="455c5-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span><span class="sxs-lookup"><span data-stu-id="455c5-129">Add Debian's Azure repositories to /etc/apt/sources.list for either Debian 7 or 8:</span></span>
   
    <span data-ttu-id="455c5-130">**Debian 7.x "Wheezy"**</span><span class="sxs-lookup"><span data-stu-id="455c5-130">**Debian 7.x "Wheezy"**</span></span>
   
        deb http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb-src http://debian-archive.trafficmanager.net/debian wheezy-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure wheezy main
        deb-src http://debian-archive.trafficmanager.net/debian-azure wheezy main

    <span data-ttu-id="455c5-131">**Debian 8.x "Jessie"**</span><span class="sxs-lookup"><span data-stu-id="455c5-131">**Debian 8.x "Jessie"**</span></span>

        deb http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb-src http://debian-archive.trafficmanager.net/debian jessie-backports main
        deb http://debian-archive.trafficmanager.net/debian-azure jessie main
        deb-src http://debian-archive.trafficmanager.net/debian-azure jessie main


1. <span data-ttu-id="455c5-132">Install the Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="455c5-132">Install the Azure Linux Agent:</span></span>
   
        # sudo apt-get update
        # sudo apt-get install waagent
2. <span data-ttu-id="455c5-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span><span class="sxs-lookup"><span data-stu-id="455c5-133">For Debian 7, it is required to run the 3.16-based kernel from the wheezy-backports repository.</span></span> <span data-ttu-id="455c5-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span><span class="sxs-lookup"><span data-stu-id="455c5-134">First create a file called /etc/apt/preferences.d/linux.pref with the following contents:</span></span>
   
        Package: linux-image-amd64 initramfs-tools
        Pin: release n=wheezy-backports
        Pin-Priority: 500
   
    <span data-ttu-id="455c5-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span><span class="sxs-lookup"><span data-stu-id="455c5-135">Then run "sudo apt-get install linux-image-amd64" to install the new kernel.</span></span>
3. <span data-ttu-id="455c5-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span><span class="sxs-lookup"><span data-stu-id="455c5-136">Deprovision the virtual machine and prepare it for provisioning on Azure and run:</span></span>
   
        # sudo waagent –force -deprovision
        # export HISTSIZE=0
        # logout
4. <span data-ttu-id="455c5-137">Click **Action** -> Shut Down in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="455c5-137">Click **Action** -> Shut Down in Hyper-V Manager.</span></span> <span data-ttu-id="455c5-138">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="455c5-138">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="455c5-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="455c5-139">Next steps</span></span>
<span data-ttu-id="455c5-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="455c5-140">You're now ready to use your Debian virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="455c5-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="455c5-141">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

