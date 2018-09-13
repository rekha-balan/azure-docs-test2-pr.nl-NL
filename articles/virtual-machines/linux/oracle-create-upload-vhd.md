---
title: Create and upload an Oracle Linux VHD | Microsoft Docs
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains an Oracle Linux operating system.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-service-management,azure-resource-manager
ms.assetid: dd96f771-26eb-4391-9a89-8c8b6d691822
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: szark
ms.openlocfilehash: 02bc245abb5c937d1be674ecb1e1a75d1dbb15bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555850"
---
# <a name="prepare-an-oracle-linux-virtual-machine-for-azure"></a><span data-ttu-id="bf638-103">Prepare an Oracle Linux virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="bf638-103">Prepare an Oracle Linux virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="bf638-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bf638-104">Prerequisites</span></span>
<span data-ttu-id="bf638-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="bf638-105">This article assumes that you have already installed an Oracle Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="bf638-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="bf638-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="bf638-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf638-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="oracle-linux-installation-notes"></a><span data-ttu-id="bf638-108">Oracle Linux installation notes</span><span class="sxs-lookup"><span data-stu-id="bf638-108">Oracle Linux installation notes</span></span>
* <span data-ttu-id="bf638-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="bf638-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-110">Oracle's Red Hat compatible kernel and their UEK3 (Unbreakable Enterprise Kernel) are both supported on Hyper-V and Azure.</span></span> <span data-ttu-id="bf638-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span><span class="sxs-lookup"><span data-stu-id="bf638-111">For best results, please be sure to update to the latest kernel while preparing your Oracle Linux VHD.</span></span>
* <span data-ttu-id="bf638-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span><span class="sxs-lookup"><span data-stu-id="bf638-112">Oracle's UEK2 is not supported on Hyper-V and Azure as it does not include the required drivers.</span></span>
* <span data-ttu-id="bf638-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span><span class="sxs-lookup"><span data-stu-id="bf638-113">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="bf638-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bf638-114">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="bf638-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span><span class="sxs-lookup"><span data-stu-id="bf638-115">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="bf638-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="bf638-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="bf638-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="bf638-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="bf638-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span><span class="sxs-lookup"><span data-stu-id="bf638-118">NUMA is not supported for larger VM sizes due to a bug in Linux kernel versions below 2.6.37.</span></span> <span data-ttu-id="bf638-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span><span class="sxs-lookup"><span data-stu-id="bf638-119">This issue primarily impacts distributions using the upstream Red Hat 2.6.32 kernel.</span></span> <span data-ttu-id="bf638-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span><span class="sxs-lookup"><span data-stu-id="bf638-120">Manual installation of the Azure Linux agent (waagent) will automatically disable NUMA in the GRUB configuration for the Linux kernel.</span></span> <span data-ttu-id="bf638-121">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="bf638-121">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bf638-122">Do not configure a swap partition on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="bf638-122">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="bf638-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="bf638-123">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="bf638-124">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="bf638-124">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="bf638-125">All of the VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="bf638-125">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>
* <span data-ttu-id="bf638-126">Make sure that the `Addons` repository is enabled.</span><span class="sxs-lookup"><span data-stu-id="bf638-126">Make sure that the `Addons` repository is enabled.</span></span> <span data-ttu-id="bf638-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span><span class="sxs-lookup"><span data-stu-id="bf638-127">Edit the file `/etc/yum.repo.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repo.d/public-yum-ol7.repo`(Oracle Linux ), and change the line `enabled=0` to `enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

## <a name="oracle-linux-64"></a><span data-ttu-id="bf638-128">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="bf638-128">Oracle Linux 6.4+</span></span>
<span data-ttu-id="bf638-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-129">You must complete specific configuration steps in the operating system for the virtual machine to run in Azure.</span></span>

1. <span data-ttu-id="bf638-130">In the center pane of Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bf638-130">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="bf638-131">Click **Connect** to open the window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bf638-131">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="bf638-132">Uninstall NetworkManager by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-132">Uninstall NetworkManager by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager
   
    <span data-ttu-id="bf638-133">**Note:** If the package is not already installed, this command will fail with an error message.</span><span class="sxs-lookup"><span data-stu-id="bf638-133">**Note:** If the package is not already installed, this command will fail with an error message.</span></span> <span data-ttu-id="bf638-134">This is expected.</span><span class="sxs-lookup"><span data-stu-id="bf638-134">This is expected.</span></span>
4. <span data-ttu-id="bf638-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="bf638-135">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
5. <span data-ttu-id="bf638-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="bf638-136">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
6. <span data-ttu-id="bf638-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span><span class="sxs-lookup"><span data-stu-id="bf638-137">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bf638-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="bf638-138">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
7. <span data-ttu-id="bf638-139">Ensure the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-139">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # chkconfig network on
8. <span data-ttu-id="bf638-140">Install python-pyasn1 by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-140">Install python-pyasn1 by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
9. <span data-ttu-id="bf638-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bf638-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="bf638-142">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300 numa=off
   
   <span data-ttu-id="bf638-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="bf638-143">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="bf638-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span><span class="sxs-lookup"><span data-stu-id="bf638-144">This will disable NUMA due to a bug in Oracle's Red Hat compatible kernel.</span></span>
   
   <span data-ttu-id="bf638-145">In addition to the above, it is recommended to *remove* the following parameters:</span><span class="sxs-lookup"><span data-stu-id="bf638-145">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
   <span data-ttu-id="bf638-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="bf638-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="bf638-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span><span class="sxs-lookup"><span data-stu-id="bf638-147">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="bf638-148">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="bf638-148">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bf638-149">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="bf638-149">This is usually the default.</span></span>
11. <span data-ttu-id="bf638-150">Install the Azure Linux Agent by running the following command.</span><span class="sxs-lookup"><span data-stu-id="bf638-150">Install the Azure Linux Agent by running the following command.</span></span> <span data-ttu-id="bf638-151">The latest version is 2.0.15.</span><span class="sxs-lookup"><span data-stu-id="bf638-151">The latest version is 2.0.15.</span></span>
    
        # sudo yum install WALinuxAgent
    
    <span data-ttu-id="bf638-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span><span class="sxs-lookup"><span data-stu-id="bf638-152">Note that installing the WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 2.</span></span>
12. <span data-ttu-id="bf638-153">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="bf638-153">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="bf638-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-154">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bf638-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="bf638-155">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bf638-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span><span class="sxs-lookup"><span data-stu-id="bf638-156">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
13. <span data-ttu-id="bf638-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="bf638-157">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
14. <span data-ttu-id="bf638-158">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="bf638-158">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bf638-159">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-159">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="oracle-linux-70"></a><span data-ttu-id="bf638-160">Oracle Linux 7.0+</span><span class="sxs-lookup"><span data-stu-id="bf638-160">Oracle Linux 7.0+</span></span>
<span data-ttu-id="bf638-161">**Changes in Oracle Linux 7**</span><span class="sxs-lookup"><span data-stu-id="bf638-161">**Changes in Oracle Linux 7**</span></span>

<span data-ttu-id="bf638-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span><span class="sxs-lookup"><span data-stu-id="bf638-162">Preparing an Oracle Linux 7 virtual machine for Azure is very similar to Oracle Linux 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="bf638-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-163">Both the Red Hat compatible kernel and Oracle's UEK3 are supported in Azure.</span></span>  <span data-ttu-id="bf638-164">The UEK3 kernel is recommended.</span><span class="sxs-lookup"><span data-stu-id="bf638-164">The UEK3 kernel is recommended.</span></span>
* <span data-ttu-id="bf638-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span><span class="sxs-lookup"><span data-stu-id="bf638-165">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="bf638-166">This package is installed by default and we recommend that it is not removed.</span><span class="sxs-lookup"><span data-stu-id="bf638-166">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="bf638-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span><span class="sxs-lookup"><span data-stu-id="bf638-167">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="bf638-168">XFS is now the default file system.</span><span class="sxs-lookup"><span data-stu-id="bf638-168">XFS is now the default file system.</span></span> <span data-ttu-id="bf638-169">The ext4 file system can still be used if desired.</span><span class="sxs-lookup"><span data-stu-id="bf638-169">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="bf638-170">**Configuration steps**</span><span class="sxs-lookup"><span data-stu-id="bf638-170">**Configuration steps**</span></span>

1. <span data-ttu-id="bf638-171">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bf638-171">In Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="bf638-172">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bf638-172">Click **Connect** to open a console window for the virtual machine.</span></span>
3. <span data-ttu-id="bf638-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="bf638-173">Create a file named **network** in the `/etc/sysconfig/` directory that contains the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain
4. <span data-ttu-id="bf638-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="bf638-174">Create a file named **ifcfg-eth0** in the `/etc/sysconfig/network-scripts/` directory that contains the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
5. <span data-ttu-id="bf638-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span><span class="sxs-lookup"><span data-stu-id="bf638-175">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="bf638-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="bf638-176">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
6. <span data-ttu-id="bf638-177">Ensure the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-177">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on
7. <span data-ttu-id="bf638-178">Install the python-pyasn1 package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-178">Install the python-pyasn1 package by running the following command:</span></span>
   
        # sudo yum install python-pyasn1
8. <span data-ttu-id="bf638-179">Run the following command to clear the current yum metadata and install any updates:</span><span class="sxs-lookup"><span data-stu-id="bf638-179">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all
        # sudo yum -y update
9. <span data-ttu-id="bf638-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-180">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="bf638-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span><span class="sxs-lookup"><span data-stu-id="bf638-181">To do this open "/etc/default/grub" in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="bf638-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="bf638-182">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="bf638-183">It also turns off the new OEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="bf638-183">It also turns off the new OEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="bf638-184">In addition to the above, it is recommended to *remove* the following parameters:</span><span class="sxs-lookup"><span data-stu-id="bf638-184">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
       rhgb quiet crashkernel=auto
   
   <span data-ttu-id="bf638-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="bf638-185">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>
   
   <span data-ttu-id="bf638-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span><span class="sxs-lookup"><span data-stu-id="bf638-186">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>
10. <span data-ttu-id="bf638-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="bf638-187">Once you are done editing "/etc/default/grub" per above, run the following command to rebuild the grub configuration:</span></span>
    
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg
11. <span data-ttu-id="bf638-188">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="bf638-188">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="bf638-189">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="bf638-189">This is usually the default.</span></span>
12. <span data-ttu-id="bf638-190">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="bf638-190">Install the Azure Linux Agent by running the following command:</span></span>
    
        # sudo yum install WALinuxAgent
        # sudo systemctl enable waagent
13. <span data-ttu-id="bf638-191">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="bf638-191">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="bf638-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-192">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="bf638-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="bf638-193">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="bf638-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span><span class="sxs-lookup"><span data-stu-id="bf638-194">After installing the Azure Linux Agent (see the previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.
14. <span data-ttu-id="bf638-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="bf638-195">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout
15. <span data-ttu-id="bf638-196">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="bf638-196">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="bf638-197">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-197">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf638-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="bf638-198">Next steps</span></span>
<span data-ttu-id="bf638-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf638-199">You're now ready to use your Oracle Linux .vhd to create new virtual machines in Azure.</span></span> <span data-ttu-id="bf638-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf638-200">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

