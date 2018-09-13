---
title: Create and upload a CentOS-based Linux VHD in Azure
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains a CentOS-based Linux operating system.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 0e518e92-e981-43f4-b12c-9cba1064c4bb
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: d67fc75f9efcdfe5e92024537ea85e26359ebe6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553017"
---
# <a name="prepare-a-centos-based-virtual-machine-for-azure"></a><span data-ttu-id="59037-103">Prepare a CentOS-based virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="59037-103">Prepare a CentOS-based virtual machine for Azure</span></span>
* [<span data-ttu-id="59037-104">Prepare a CentOS 6.x virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="59037-104">Prepare a CentOS 6.x virtual machine for Azure</span></span>](#centos-6x)
* [<span data-ttu-id="59037-105">Prepare a CentOS 7.0+ virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="59037-105">Prepare a CentOS 7.0+ virtual machine for Azure</span></span>](#centos-70)

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="59037-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="59037-106">Prerequisites</span></span>
<span data-ttu-id="59037-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="59037-107">This article assumes that you have already installed a CentOS (or similar derivative) Linux operating system to a virtual hard disk.</span></span> <span data-ttu-id="59037-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="59037-108">Multiple tools exist to create .vhd files, for example a virtualization solution such as Hyper-V.</span></span> <span data-ttu-id="59037-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="59037-109">For instructions, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="59037-110">**CentOS installation notes**</span><span class="sxs-lookup"><span data-stu-id="59037-110">**CentOS installation notes**</span></span>

* <span data-ttu-id="59037-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-111">Please see also [General Linux Installation Notes](create-upload-generic.md#general-linux-installation-notes) for more tips on preparing Linux for Azure.</span></span>
* <span data-ttu-id="59037-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span><span class="sxs-lookup"><span data-stu-id="59037-112">The VHDX format is not supported in Azure, only **fixed VHD**.</span></span>  <span data-ttu-id="59037-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="59037-113">You can convert the disk to VHD format using Hyper-V Manager or the convert-vhd cmdlet.</span></span> <span data-ttu-id="59037-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span><span class="sxs-lookup"><span data-stu-id="59037-114">If you are using VirtualBox this means selecting **Fixed size** as opposed to the default dynamically allocated when creating the disk.</span></span>
* <span data-ttu-id="59037-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span><span class="sxs-lookup"><span data-stu-id="59037-115">When installing the Linux system it is *recommended* that you use standard partitions rather than LVM (often the default for many installations).</span></span> <span data-ttu-id="59037-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="59037-116">This will avoid LVM name conflicts with cloned VMs, particularly if an OS disk ever needs to be attached to another identical VM for troubleshooting.</span></span> <span data-ttu-id="59037-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span><span class="sxs-lookup"><span data-stu-id="59037-117">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="59037-118">Kernel support for mounting UDF file systems is required.</span><span class="sxs-lookup"><span data-stu-id="59037-118">Kernel support for mounting UDF file systems is required.</span></span> <span data-ttu-id="59037-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span><span class="sxs-lookup"><span data-stu-id="59037-119">At first boot on Azure the provisioning configuration is passed to the Linux VM via UDF-formatted media that is attached to the guest.</span></span> <span data-ttu-id="59037-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span><span class="sxs-lookup"><span data-stu-id="59037-120">The Azure Linux agent must be able to mount the UDF file system to read its configuration and provision the VM.</span></span>
* <span data-ttu-id="59037-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span><span class="sxs-lookup"><span data-stu-id="59037-121">Linux kernel versions below 2.6.37 do not support NUMA on Hyper-V with larger VM sizes.</span></span> <span data-ttu-id="59037-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="59037-122">This issue primarily impacts older distributions using the upstream Red Hat 2.6.32 kernel, and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="59037-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span><span class="sxs-lookup"><span data-stu-id="59037-123">Systems running custom kernels older than 2.6.37, or RHEL-based kernels older than 2.6.32-504 must set the boot parameter `numa=off` on the kernel command-line in grub.conf.</span></span> <span data-ttu-id="59037-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="59037-124">For more information see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="59037-125">Do not configure a swap partition on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="59037-125">Do not configure a swap partition on the OS disk.</span></span> <span data-ttu-id="59037-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="59037-126">The Linux agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="59037-127">More information about this can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="59037-127">More information about this can be found in the steps below.</span></span>
* <span data-ttu-id="59037-128">All of the VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="59037-128">All of the VHDs must have sizes that are multiples of 1 MB.</span></span>

## <a name="centos-6x"></a><span data-ttu-id="59037-129">CentOS 6.x</span><span class="sxs-lookup"><span data-stu-id="59037-129">CentOS 6.x</span></span>

1. <span data-ttu-id="59037-130">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="59037-130">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="59037-131">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="59037-131">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="59037-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span><span class="sxs-lookup"><span data-stu-id="59037-132">In CentOS 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="59037-133">Uninstall this package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="59037-133">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="59037-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span><span class="sxs-lookup"><span data-stu-id="59037-134">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="59037-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span><span class="sxs-lookup"><span data-stu-id="59037-135">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="59037-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span><span class="sxs-lookup"><span data-stu-id="59037-136">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="59037-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="59037-137">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="59037-138">Ensure the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="59037-138">Ensure the network service will start at boot time by running the following command:</span></span>
   
        # sudo chkconfig network on

8. <span data-ttu-id="59037-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span><span class="sxs-lookup"><span data-stu-id="59037-139">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="59037-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span><span class="sxs-lookup"><span data-stu-id="59037-140">This will also add the **[openlogic]** repository that includes additional packages such as the Azure Linux agent:</span></span>

        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
        
        #contrib - packages by Centos Users
        [contrib]
        name=CentOS-$releasever - Contrib
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/contrib/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

    >[!Note]
    <span data-ttu-id="59037-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span><span class="sxs-lookup"><span data-stu-id="59037-141">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>


9. <span data-ttu-id="59037-142">Add the following line to /etc/yum.conf:</span><span class="sxs-lookup"><span data-stu-id="59037-142">Add the following line to /etc/yum.conf:</span></span>
    
        http_caching=packages

10. <span data-ttu-id="59037-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span><span class="sxs-lookup"><span data-stu-id="59037-143">Run the following command to clear the current yum metadata and update the system with the latest packages:</span></span>
    
        # yum clean all

    <span data-ttu-id="59037-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span><span class="sxs-lookup"><span data-stu-id="59037-144">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="59037-145">A reboot may be required after running this command.</span><span class="sxs-lookup"><span data-stu-id="59037-145">A reboot may be required after running this command.</span></span>

11. <span data-ttu-id="59037-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span><span class="sxs-lookup"><span data-stu-id="59037-146">(Optional) Install the drivers for the Linux Integration Services (LIS).</span></span>
   
    >[!IMPORTANT]
    <span data-ttu-id="59037-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span><span class="sxs-lookup"><span data-stu-id="59037-147">The step is **required** for CentOS 6.3 and earlier, and optional for later releases.</span></span>

        # sudo rpm -e hypervkvpd  ## (may return error if not installed, that's OK)
        # sudo yum install microsoft-hyper-v

    <span data-ttu-id="59037-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span><span class="sxs-lookup"><span data-stu-id="59037-148">Alternatively, you can follow the manual installation instructions on the [LIS download page](https://go.microsoft.com/fwlink/?linkid=403033) to install the RPM onto your VM.</span></span>
 
12. <span data-ttu-id="59037-149">Install the Azure Linux Agent and dependencies:</span><span class="sxs-lookup"><span data-stu-id="59037-149">Install the Azure Linux Agent and dependencies:</span></span>
    
        # sudo yum install python-pyasn1 WALinuxAgent
    
    <span data-ttu-id="59037-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span><span class="sxs-lookup"><span data-stu-id="59037-150">The WALinuxAgent package will remove the NetworkManager and NetworkManager-gnome packages if they were not already removed as described in step 3.</span></span>


13. <span data-ttu-id="59037-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-151">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="59037-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="59037-152">To do this, open `/boot/grub/menu.lst` in a text editor and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="59037-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="59037-153">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="59037-154">In addition to the above, it is recommended to *remove* the following parameters:</span><span class="sxs-lookup"><span data-stu-id="59037-154">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="59037-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="59037-155">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="59037-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span><span class="sxs-lookup"><span data-stu-id="59037-156">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

    >[!Important]
    <span data-ttu-id="59037-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span><span class="sxs-lookup"><span data-stu-id="59037-157">CentOS 6.5 and earlier must also set the kernel parameter `numa=off`.</span></span> <span data-ttu-id="59037-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="59037-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

14. <span data-ttu-id="59037-159">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="59037-159">Ensure that the SSH server is installed and configured to start at boot time.</span></span>  <span data-ttu-id="59037-160">This is usually the default.</span><span class="sxs-lookup"><span data-stu-id="59037-160">This is usually the default.</span></span>

15. <span data-ttu-id="59037-161">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="59037-161">Do not create swap space on the OS disk.</span></span>
    
    <span data-ttu-id="59037-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-162">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="59037-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="59037-163">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="59037-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="59037-164">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
    
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="59037-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="59037-165">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
    
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

17. <span data-ttu-id="59037-166">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="59037-166">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="59037-167">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


- - -
## <a name="centos-70"></a><span data-ttu-id="59037-168">CentOS 7.0+</span><span class="sxs-lookup"><span data-stu-id="59037-168">CentOS 7.0+</span></span>
<span data-ttu-id="59037-169">**Changes in CentOS 7 (and similar derivatives)**</span><span class="sxs-lookup"><span data-stu-id="59037-169">**Changes in CentOS 7 (and similar derivatives)**</span></span>

<span data-ttu-id="59037-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span><span class="sxs-lookup"><span data-stu-id="59037-170">Preparing a CentOS 7 virtual machine for Azure is very similar to CentOS 6, however there are several important differences worth noting:</span></span>

* <span data-ttu-id="59037-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span><span class="sxs-lookup"><span data-stu-id="59037-171">The NetworkManager package no longer conflicts with the Azure Linux agent.</span></span> <span data-ttu-id="59037-172">This package is installed by default and we recommend that it is not removed.</span><span class="sxs-lookup"><span data-stu-id="59037-172">This package is installed by default and we recommend that it is not removed.</span></span>
* <span data-ttu-id="59037-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span><span class="sxs-lookup"><span data-stu-id="59037-173">GRUB2 is now used as the default bootloader, so the procedure for editing kernel parameters has changed (see below).</span></span>
* <span data-ttu-id="59037-174">XFS is now the default file system.</span><span class="sxs-lookup"><span data-stu-id="59037-174">XFS is now the default file system.</span></span> <span data-ttu-id="59037-175">The ext4 file system can still be used if desired.</span><span class="sxs-lookup"><span data-stu-id="59037-175">The ext4 file system can still be used if desired.</span></span>

<span data-ttu-id="59037-176">**Configuration Steps**</span><span class="sxs-lookup"><span data-stu-id="59037-176">**Configuration Steps**</span></span>

1. <span data-ttu-id="59037-177">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="59037-177">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="59037-178">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="59037-178">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="59037-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span><span class="sxs-lookup"><span data-stu-id="59037-179">Create or edit the file `/etc/sysconfig/network` and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="59037-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span><span class="sxs-lookup"><span data-stu-id="59037-180">Create or edit the file `/etc/sysconfig/network-scripts/ifcfg-eth0` and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="59037-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span><span class="sxs-lookup"><span data-stu-id="59037-181">Modify udev rules to avoid generating static rules for the Ethernet interface(s).</span></span> <span data-ttu-id="59037-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="59037-182">These rules can cause problems when cloning a virtual machine in Microsoft Azure or Hyper-V:</span></span>
   
        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

6. <span data-ttu-id="59037-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span><span class="sxs-lookup"><span data-stu-id="59037-183">If you would like to use the OpenLogic mirrors that are hosted within the Azure datacenters, then replace the `/etc/yum.repos.d/CentOS-Base.repo` file with the following repositories.</span></span>  <span data-ttu-id="59037-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span><span class="sxs-lookup"><span data-stu-id="59037-184">This will also add the **[openlogic]** repository that includes packages for the Azure Linux agent:</span></span>
   
        [openlogic]
        name=CentOS-$releasever - openlogic packages for $basearch
        baseurl=http://olcentgbl.trafficmanager.net/openlogic/$releasever/openlogic/$basearch/
        enabled=1
        gpgcheck=0
        
        [base]
        name=CentOS-$releasever - Base
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/os/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #released updates
        [updates]
        name=CentOS-$releasever - Updates
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/updates/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that may be useful
        [extras]
        name=CentOS-$releasever - Extras
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/extras/$basearch/
        gpgcheck=1
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
        
        #additional packages that extend functionality of existing packages
        [centosplus]
        name=CentOS-$releasever - Plus
        #mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus&infra=$infra
        baseurl=http://olcentgbl.trafficmanager.net/centos/$releasever/centosplus/$basearch/
        gpgcheck=1
        enabled=0
        gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7

    >[!Note]
    <span data-ttu-id="59037-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span><span class="sxs-lookup"><span data-stu-id="59037-185">The rest of this guide will assume you are using at least the `[openlogic]` repo, which will be used to install the Azure Linux agent below.</span></span>

7. <span data-ttu-id="59037-186">Run the following command to clear the current yum metadata and install any updates:</span><span class="sxs-lookup"><span data-stu-id="59037-186">Run the following command to clear the current yum metadata and install any updates:</span></span>
   
        # sudo yum clean all

    <span data-ttu-id="59037-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span><span class="sxs-lookup"><span data-stu-id="59037-187">Unless you are creating an image for an older version of CentOS, it is recommended to update all the packages to the latest:</span></span>

        # sudo yum -y update

    <span data-ttu-id="59037-188">A reboot maybe required after running this command.</span><span class="sxs-lookup"><span data-stu-id="59037-188">A reboot maybe required after running this command.</span></span>

8. <span data-ttu-id="59037-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-189">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="59037-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span><span class="sxs-lookup"><span data-stu-id="59037-190">To do this, open `/etc/default/grub` in a text editor and edit the `GRUB_CMDLINE_LINUX` parameter, for example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="59037-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="59037-191">This will also ensure all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="59037-192">It also turns off the new CentOS 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="59037-192">It also turns off the new CentOS 7 naming conventions for NICs.</span></span> <span data-ttu-id="59037-193">In addition to the above, it is recommended to *remove* the following parameters:</span><span class="sxs-lookup"><span data-stu-id="59037-193">In addition to the above, it is recommended to *remove* the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="59037-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="59037-194">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="59037-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span><span class="sxs-lookup"><span data-stu-id="59037-195">The `crashkernel` option may be left configured if desired, but note that this parameter will reduce the amount of available memory in the VM by 128MB or more, which may be problematic on the smaller VM sizes.</span></span>

9. <span data-ttu-id="59037-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="59037-196">Once you are done editing `/etc/default/grub` per above, run the following command to rebuild the grub configuration:</span></span>
   
        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="59037-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span><span class="sxs-lookup"><span data-stu-id="59037-197">If building the image from **VMWare, VirtualBox or KVM:** Ensure the Hyper-V drivers are included in the initramfs:</span></span>
   
   <span data-ttu-id="59037-198">Edit `/etc/dracut.conf`, add content:</span><span class="sxs-lookup"><span data-stu-id="59037-198">Edit `/etc/dracut.conf`, add content:</span></span>
   
        add_drivers+=”hv_vmbus hv_netvsc hv_storvsc”
   
   <span data-ttu-id="59037-199">Rebuild the initramfs:</span><span class="sxs-lookup"><span data-stu-id="59037-199">Rebuild the initramfs:</span></span>
   
        # sudo dracut –f -v

11. <span data-ttu-id="59037-200">Install the Azure Linux Agent and dependencies:</span><span class="sxs-lookup"><span data-stu-id="59037-200">Install the Azure Linux Agent and dependencies:</span></span>

        # sudo yum install python-pyasn1 WALinuxAgent
        # sudo systemctl enable waagent

12. <span data-ttu-id="59037-201">Do not create swap space on the OS disk.</span><span class="sxs-lookup"><span data-stu-id="59037-201">Do not create swap space on the OS disk.</span></span>
   
   <span data-ttu-id="59037-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-202">The Azure Linux Agent can automatically configure swap space using the local resource disk that is attached to the VM after provisioning on Azure.</span></span> <span data-ttu-id="59037-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="59037-203">Note that the local resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span> <span data-ttu-id="59037-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="59037-204">After installing the Azure Linux Agent (see previous step), modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>
   
        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="59037-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="59037-205">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>
   
        # sudo waagent -force -deprovision
        # export HISTSIZE=0
        # logout

14. <span data-ttu-id="59037-206">Click **Action -> Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="59037-206">Click **Action -> Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="59037-207">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-207">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59037-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="59037-208">Next steps</span></span>
<span data-ttu-id="59037-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="59037-209">You're now ready to use your CentOS Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="59037-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="59037-210">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

