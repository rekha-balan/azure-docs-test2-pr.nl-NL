---
title: Create and upload a SUSE Linux VHD in Azure
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains a SUSE Linux operating system.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 066d01a6-2a54-4718-bcd0-90fe7a5303a1
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: szark
ms.openlocfilehash: da3152d995d70110e6434034061ec20ec7615383
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553089"
---
# <a name="prepare-a-sles-or-opensuse-virtual-machine-for-azure"></a><span data-ttu-id="6f7e0-103">Prepare a SLES or openSUSE virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="6f7e0-103">Prepare a SLES or openSUSE virtual machine for Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="6f7e0-104">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6f7e0-104">Prerequisites</span></span>
<span data-ttu-id="6f7e0-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-105">This article assumes that you have already installed a SUSE or openSUSE Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="6f7e0-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-106">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="6f7e0-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-107">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="sles--opensuse-installation-notes"></a><span data-ttu-id="6f7e0-108">SLES / openSUSE installation notes</span><span class="sxs-lookup"><span data-stu-id="6f7e0-108">SLES / openSUSE installation notes</span></span>
* <span data-ttu-id="6f7e0-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-109">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="6f7e0-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-110">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="6f7e0-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-111">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span>
* <span data-ttu-id="6f7e0-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-112">When installing the Linux system it is recommended that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="6f7e0-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-113">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another VM for troubleshooting.</span></span> <span data-ttu-id="6f7e0-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-114">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks if preferred.</span></span>
* <span data-ttu-id="6f7e0-115">Do not configure a swap partition on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-115">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="6f7e0-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-116">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="6f7e0-117">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-117">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="6f7e0-118">All of the VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-118">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="use-suse-studio"></a><span data-ttu-id="6f7e0-119">Use SUSE Studio</span><span class="sxs-lookup"><span data-stu-id="6f7e0-119">Use SUSE Studio</span></span>
<span data-ttu-id="6f7e0-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-120">[SUSE Studio](http://www.susestudio.com) can easily create and manage your SLES and openSUSE images for Azure and Hyper-V.</span></span> <span data-ttu-id="6f7e0-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-121">This is the recommended approach for customizing your own SLES and openSUSE images.</span></span>

<span data-ttu-id="6f7e0-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-122">As an alternative to building your own VHD, SUSE also publishes BYOS (Bring Your Own Subscription) images for SLES at [VMDepot](https://vmdepot.msopentech.com/User/Show?user=1007).</span></span>

## <a name="prepare-suse-linux-enterprise-server-11-sp4"></a><span data-ttu-id="6f7e0-123">Prepare SUSE Linux Enterprise Server 11 SP4</span><span class="sxs-lookup"><span data-stu-id="6f7e0-123">Prepare SUSE Linux Enterprise Server 11 SP4</span></span>
1. <span data-ttu-id="6f7e0-124">In the center pane of Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-124">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="6f7e0-125">Click **Connect** to open the window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-125">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="6f7e0-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-126">Register your SUSE Linux Enterprise system to allow it to download updates and install packages.</span></span>
4. <span data-ttu-id="6f7e0-127">Update the system with the latest patches:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-127">Update the system with the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="6f7e0-128">Install the Azure Linux Agent from the SLES repository:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-128">Install the Azure Linux Agent from the SLES repository:</span></span>
   
        # sudo zypper install WALinuxAgent
6. <span data-ttu-id="6f7e0-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-129">Check if waagent is set to "on" in chkconfig, and if not, enable it for autostart:</span></span>
   
        # sudo chkconfig waagent on
7. <span data-ttu-id="6f7e0-130">Check if waagent service is running, and if not, start it:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-130">Check if waagent service is running, and if not, start it:</span></span> 
   
        # sudo service waagent start
8. <span data-ttu-id="6f7e0-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-131">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="6f7e0-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-132">To do this open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
   
    <span data-ttu-id="6f7e0-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-133">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
9. <span data-ttu-id="6f7e0-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-134">Confirm that /boot/grub/menu.lst and /etc/fstab both reference the disk using its UUID (by-uuid) instead of the disk ID (by-id).</span></span> 
   
    <span data-ttu-id="6f7e0-135">Get disk UUID</span><span class="sxs-lookup"><span data-stu-id="6f7e0-135">Get disk UUID</span></span>
   
        # ls /dev/disk/by-uuid/
   
    <span data-ttu-id="6f7e0-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span><span class="sxs-lookup"><span data-stu-id="6f7e0-136">If /dev/disk/by-id/ is used, update both /boot/grub/menu.lst and /etc/fstab with the proper by-uuid value</span></span>
   
    <span data-ttu-id="6f7e0-137">Before change</span><span class="sxs-lookup"><span data-stu-id="6f7e0-137">Before change</span></span>
   
        root=/dev/disk/by-id/SCSI-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxxx-part1
   
    <span data-ttu-id="6f7e0-138">After change</span><span class="sxs-lookup"><span data-stu-id="6f7e0-138">After change</span></span>
   
        root=/dev/disk/by-uuid/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
10. <span data-ttu-id="6f7e0-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-139">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="6f7e0-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-140">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
    
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules
11. <span data-ttu-id="6f7e0-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-141">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
    
     <span data-ttu-id="6f7e0-142">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="6f7e0-142">DHCLIENT_SET_HOSTNAME="no"</span></span>
12. <span data-ttu-id="6f7e0-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-143">In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
    
     <span data-ttu-id="6f7e0-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="6f7e0-144">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="6f7e0-145">Only use this together with 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="6f7e0-145">Only use this together with 'Defaults targetpw'!</span></span>
13. <span data-ttu-id="6f7e0-146">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-146">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="6f7e0-147">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-147">This is usually the default.</span></span>
14. <span data-ttu-id="6f7e0-148">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-148">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="6f7e0-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-149">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="6f7e0-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-150">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="6f7e0-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-151">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="6f7e0-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-152">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
15. <span data-ttu-id="6f7e0-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-153">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="6f7e0-154">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="6f7e0-154">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="6f7e0-155">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="6f7e0-155">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="6f7e0-156">logout</span><span class="sxs-lookup"><span data-stu-id="6f7e0-156">logout</span></span>
16. <span data-ttu-id="6f7e0-157">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-157">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6f7e0-158">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-158">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

- - -
## <a name="prepare-opensuse-131"></a><span data-ttu-id="6f7e0-159">Prepare openSUSE 13.1+</span><span class="sxs-lookup"><span data-stu-id="6f7e0-159">Prepare openSUSE 13.1+</span></span>
1. <span data-ttu-id="6f7e0-160">In the center pane of Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-160">In the center pane of Hyper-V Manager, select the virtual machine.</span></span>
2. <span data-ttu-id="6f7e0-161">Click **Connect** to open the window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-161">Click **Connect** to open the window for the virtual machine.</span></span>
3. <span data-ttu-id="6f7e0-162">On the shell, run the command '`zypper lr`'.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-162">On the shell, run the command '`zypper lr`'.</span></span> <span data-ttu-id="6f7e0-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span><span class="sxs-lookup"><span data-stu-id="6f7e0-163">If this command returns output similar to the following, then the repositories are configured as expected--no adjustments are necessary (note that version numbers may vary):</span></span>
   
        # | Alias                 | Name                  | Enabled | Refresh
        --+-----------------------+-----------------------+---------+--------
        1 | Cloud:Tools_13.1      | Cloud:Tools_13.1      | Yes     | Yes
        2 | openSUSE_13.1_OSS     | openSUSE_13.1_OSS     | Yes     | Yes
        3 | openSUSE_13.1_Updates | openSUSE_13.1_Updates | Yes     | Yes
   
    <span data-ttu-id="6f7e0-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-164">If the command returns "No repositories defined..." then use the following commands to add these repos:</span></span>
   
        # sudo zypper ar -f http://download.opensuse.org/repositories/Cloud:Tools/openSUSE_13.1 Cloud:Tools_13.1
        # sudo zypper ar -f http://download.opensuse.org/distribution/13.1/repo/oss openSUSE_13.1_OSS
        # sudo zypper ar -f http://download.opensuse.org/update/13.1 openSUSE_13.1_Updates
   
    <span data-ttu-id="6f7e0-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-165">You can then verify the repositories have been added by running the command '`zypper lr`' again.</span></span> <span data-ttu-id="6f7e0-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-166">In case one of the relevant update repositories is not enabled, enable it with following command:</span></span>
   
        # sudo zypper mr -e [NUMBER OF REPOSITORY]
4. <span data-ttu-id="6f7e0-167">Update the kernel to the latest available version:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-167">Update the kernel to the latest available version:</span></span>
   
        # sudo zypper up kernel-default
   
    <span data-ttu-id="6f7e0-168">Or to update the system with all the latest patches:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-168">Or to update the system with all the latest patches:</span></span>
   
        # sudo zypper update
5. <span data-ttu-id="6f7e0-169">Install the Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-169">Install the Azure Linux Agent.</span></span>
   
   # <a name="sudo-zypper-install-walinuxagent"></a><span data-ttu-id="6f7e0-170">sudo zypper install WALinuxAgent</span><span class="sxs-lookup"><span data-stu-id="6f7e0-170">sudo zypper install WALinuxAgent</span></span>
6. <span data-ttu-id="6f7e0-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-171">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="6f7e0-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-172">To do this, open "/boot/grub/menu.lst" in a text editor and ensure that the default kernel includes the following parameters:</span></span>
   
     <span data-ttu-id="6f7e0-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span><span class="sxs-lookup"><span data-stu-id="6f7e0-173">console=ttyS0 earlyprintk=ttyS0 rootdelay=300</span></span>
   
   <span data-ttu-id="6f7e0-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-174">This will ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="6f7e0-175">In addition, remove the following parameters from the kernel boot line if they exist:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-175">In addition, remove the following parameters from the kernel boot line if they exist:</span></span>
   
     <span data-ttu-id="6f7e0-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span><span class="sxs-lookup"><span data-stu-id="6f7e0-176">libata.atapi_enabled=0 reserve=0x1f0,0x8</span></span>
7. <span data-ttu-id="6f7e0-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-177">It is recommended to edit the file "/etc/sysconfig/network/dhcp" and change the `DHCLIENT_SET_HOSTNAME` parameter to the following:</span></span>
   
     <span data-ttu-id="6f7e0-178">DHCLIENT_SET_HOSTNAME="no"</span><span class="sxs-lookup"><span data-stu-id="6f7e0-178">DHCLIENT_SET_HOSTNAME="no"</span></span>
8. <span data-ttu-id="6f7e0-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-179">**Important:** In "/etc/sudoers", comment out or remove the following lines if they exist:</span></span>
   
     <span data-ttu-id="6f7e0-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span><span class="sxs-lookup"><span data-stu-id="6f7e0-180">Defaults targetpw   # ask for the password of the target user i.e. root ALL    ALL=(ALL) ALL   # WARNING!</span></span> <span data-ttu-id="6f7e0-181">Only use this together with 'Defaults targetpw'!</span><span class="sxs-lookup"><span data-stu-id="6f7e0-181">Only use this together with 'Defaults targetpw'!</span></span>
9. <span data-ttu-id="6f7e0-182">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-182">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="6f7e0-183">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-183">This is usually the default.</span></span>
10. <span data-ttu-id="6f7e0-184">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-184">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="6f7e0-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-185">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="6f7e0-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-186">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="6f7e0-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-187">After installing the Azure Linux Agent (see previous step), modify the following parameters in /etc/waagent.conf appropriately:</span></span>
    
     <span data-ttu-id="6f7e0-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-188">ResourceDisk.Format=y  ResourceDisk.Filesystem=ext4  ResourceDisk.MountPoint=/mnt/resource  ResourceDisk.EnableSwap=y  ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.</span></span>
11. <span data-ttu-id="6f7e0-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-189">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
    # <a name="sudo-waagent--force--deprovision"></a><span data-ttu-id="6f7e0-190">sudo waagent -force -deprovision</span><span class="sxs-lookup"><span data-stu-id="6f7e0-190">sudo waagent -force -deprovision</span></span>
    # <a name="export-histsize0"></a><span data-ttu-id="6f7e0-191">export HISTSIZE=0</span><span class="sxs-lookup"><span data-stu-id="6f7e0-191">export HISTSIZE=0</span></span>
    # <a name="logout"></a><span data-ttu-id="6f7e0-192">logout</span><span class="sxs-lookup"><span data-stu-id="6f7e0-192">logout</span></span>
12. <span data-ttu-id="6f7e0-193">Ensure the Azure Linux Agent runs at startup:</span><span class="sxs-lookup"><span data-stu-id="6f7e0-193">Ensure the Azure Linux Agent runs at startup:</span></span>
    
        # sudo systemctl enable waagent.service
13. <span data-ttu-id="6f7e0-194">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-194">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="6f7e0-195">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-195">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6f7e0-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f7e0-196">Next steps</span></span>
<span data-ttu-id="6f7e0-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="6f7e0-197">You're now ready to use your SUSE Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="6f7e0-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6f7e0-198">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

