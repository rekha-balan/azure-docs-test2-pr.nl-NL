---
title: Create and upload a Red Hat Enterprise Linux VHD for use in Azure | Microsoft Docs
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains a Red Hat Linux operating system.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: 6c6b8f72-32d3-47fa-be94-6cb54537c69f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/10/2017
ms.author: szark
ms.openlocfilehash: 9ad7fc7cf9d841462aaf70a9ebd931516ee4de5e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564029"
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure"></a><span data-ttu-id="a034d-103">Prepare a Red Hat-based virtual machine for Azure</span><span class="sxs-lookup"><span data-stu-id="a034d-103">Prepare a Red Hat-based virtual machine for Azure</span></span>
<span data-ttu-id="a034d-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure.</span></span> <span data-ttu-id="a034d-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span><span class="sxs-lookup"><span data-stu-id="a034d-105">The versions of RHEL that are covered in this article are 6.7+ and 7.1+.</span></span> <span data-ttu-id="a034d-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span><span class="sxs-lookup"><span data-stu-id="a034d-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span> <span data-ttu-id="a034d-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/articles/1989673).</span><span class="sxs-lookup"><span data-stu-id="a034d-107">For more information about eligibility requirements for participating in Red Hat's Cloud Access program, see [Red Hat's Cloud Access website](http://www.redhat.com/en/technologies/cloud-computing/cloud-access) and [Running RHEL on Azure](https://access.redhat.com/articles/1989673).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="a034d-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="a034d-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a034d-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a034d-109">Prerequisites</span></span>
<span data-ttu-id="a034d-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="a034d-110">This section assumes that you have already obtained an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="a034d-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="a034d-111">For more details about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

<span data-ttu-id="a034d-112">**RHEL installation notes**</span><span class="sxs-lookup"><span data-stu-id="a034d-112">**RHEL installation notes**</span></span>

* <span data-ttu-id="a034d-113">Azure does not support the VHDX format.</span><span class="sxs-lookup"><span data-stu-id="a034d-113">Azure does not support the VHDX format.</span></span> <span data-ttu-id="a034d-114">Azure supports only fixed VHD.</span><span class="sxs-lookup"><span data-stu-id="a034d-114">Azure supports only fixed VHD.</span></span> <span data-ttu-id="a034d-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a034d-115">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="a034d-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-116">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="a034d-117">Azure supports only generation 1 virtual machines.</span><span class="sxs-lookup"><span data-stu-id="a034d-117">Azure supports only generation 1 virtual machines.</span></span> <span data-ttu-id="a034d-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-118">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="a034d-119">You can't change a virtual machine's generation.</span><span class="sxs-lookup"><span data-stu-id="a034d-119">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="a034d-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="a034d-120">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="a034d-121">The maximum size that's allowed for the VHD is 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="a034d-121">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="a034d-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span><span class="sxs-lookup"><span data-stu-id="a034d-122">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="a034d-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a034d-123">This practice will avoid LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span> <span data-ttu-id="a034d-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span><span class="sxs-lookup"><span data-stu-id="a034d-124">[LVM](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [RAID](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) may be used on data disks.</span></span>
* <span data-ttu-id="a034d-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span><span class="sxs-lookup"><span data-stu-id="a034d-125">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="a034d-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-126">At first boot on Azure, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="a034d-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-127">The Azure Linux Agent must be able to mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="a034d-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-128">Versions of the Linux kernel that are earlier than 2.6.37 do not support non-uniform memory access (NUMA) on Hyper-V with larger virtual machine sizes.</span></span> <span data-ttu-id="a034d-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span><span class="sxs-lookup"><span data-stu-id="a034d-129">This issue primarily impacts older distributions that use the upstream Red Hat 2.6.32 kernel and was fixed in RHEL 6.6 (kernel-2.6.32-504).</span></span> <span data-ttu-id="a034d-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span><span class="sxs-lookup"><span data-stu-id="a034d-130">Systems that run custom kernels that are older than 2.6.37 or RHEL-based kernels that are older than 2.6.32-504 must set the `numa=off` boot parameter on the kernel command line in grub.conf.</span></span> <span data-ttu-id="a034d-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="a034d-131">For more information, see Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>
* <span data-ttu-id="a034d-132">Do not configure a swap partition on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-132">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="a034d-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-133">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span>  <span data-ttu-id="a034d-134">More information about this can be found in the following steps.</span><span class="sxs-lookup"><span data-stu-id="a034d-134">More information about this can be found in the following steps.</span></span>
* <span data-ttu-id="a034d-135">All VHDs must have sizes that are multiples of 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a034d-135">All VHDs must have sizes that are multiples of 1 MB.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="a034d-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="a034d-136">Prepare a RHEL 6 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="a034d-137">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-137">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="a034d-138">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-138">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="a034d-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span><span class="sxs-lookup"><span data-stu-id="a034d-139">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="a034d-140">Uninstall this package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-140">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

4. <span data-ttu-id="a034d-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-141">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="a034d-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-142">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="a034d-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span><span class="sxs-lookup"><span data-stu-id="a034d-143">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="a034d-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a034d-144">These rules cause problems when you clone a virtual machine in Microsoft Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules
        
        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="a034d-145">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-145">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

8. <span data-ttu-id="a034d-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-146">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="a034d-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-147">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-148">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-148">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

10. <span data-ttu-id="a034d-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-149">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-150">To do this modification, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="a034d-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-151">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="a034d-152">In addition, we recommended that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-152">In addition, we recommended that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="a034d-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-153">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span>  <span data-ttu-id="a034d-154">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-154">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span><span class="sxs-lookup"><span data-stu-id="a034d-155">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more.</span></span> <span data-ttu-id="a034d-156">This configuration might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-156">This configuration might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="a034d-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-157">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="a034d-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="a034d-158">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

11. <span data-ttu-id="a034d-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span><span class="sxs-lookup"><span data-stu-id="a034d-159">Ensure that the secure shell (SSH) server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="a034d-160">Modify /etc/ssh/sshd_config to include the following line:</span><span class="sxs-lookup"><span data-stu-id="a034d-160">Modify /etc/ssh/sshd_config to include the following line:</span></span>

        ClientAliveInterval 180

12. <span data-ttu-id="a034d-161">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-161">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on


    <span data-ttu-id="a034d-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span><span class="sxs-lookup"><span data-stu-id="a034d-162">Installing the WALinuxAgent package removes the NetworkManager and NetworkManager-gnome packages if they were not already removed in step 3.</span></span>

13. <span data-ttu-id="a034d-163">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-163">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="a034d-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-164">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-165">Note that the local resource disk is a temporary disk and that it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-166">After you install the Azure Linux Agent in the previous step, modify the following parameters in /etc/waagent.conf appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

14. <span data-ttu-id="a034d-167">Unregister the subscription (if necessary) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-167">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

15. <span data-ttu-id="a034d-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-168">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

16. <span data-ttu-id="a034d-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="a034d-169">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a034d-170">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-170">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="a034d-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="a034d-171">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="a034d-172">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-172">In Hyper-V Manager, select the virtual machine.</span></span>

2. <span data-ttu-id="a034d-173">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-173">Click **Connect** to open a console window for the virtual machine.</span></span>

3. <span data-ttu-id="a034d-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-174">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

4. <span data-ttu-id="a034d-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-175">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

5. <span data-ttu-id="a034d-176">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-176">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="a034d-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-177">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="a034d-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-178">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-179">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="a034d-180">For example:</span><span class="sxs-lookup"><span data-stu-id="a034d-180">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a034d-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-181">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a034d-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="a034d-182">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a034d-183">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-183">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="a034d-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-184">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="a034d-185">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-185">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-186">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

8. <span data-ttu-id="a034d-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="a034d-187">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

9. <span data-ttu-id="a034d-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span><span class="sxs-lookup"><span data-stu-id="a034d-188">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="a034d-189">Modify `/etc/ssh/sshd_config` to include the following line:</span><span class="sxs-lookup"><span data-stu-id="a034d-189">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

10. <span data-ttu-id="a034d-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-190">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-191">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-191">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

11. <span data-ttu-id="a034d-192">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-192">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

12. <span data-ttu-id="a034d-193">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-193">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="a034d-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-194">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-195">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-196">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="a034d-197">If you want to unregister the subscription, run the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-197">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="a034d-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-198">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="a034d-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="a034d-199">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span> <span data-ttu-id="a034d-200">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-200">Your Linux VHD is now ready to be uploaded to Azure.</span></span>


## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="a034d-201">Prepare a Red Hat-based virtual machine from KVM</span><span class="sxs-lookup"><span data-stu-id="a034d-201">Prepare a Red Hat-based virtual machine from KVM</span></span>
### <a name="prepare-a-rhel-6-virtual-machine-from-kvm"></a><span data-ttu-id="a034d-202">Prepare a RHEL 6 virtual machine from KVM</span><span class="sxs-lookup"><span data-stu-id="a034d-202">Prepare a RHEL 6 virtual machine from KVM</span></span>

1. <span data-ttu-id="a034d-203">Download the KVM image of RHEL 6 from the Red Hat website.</span><span class="sxs-lookup"><span data-stu-id="a034d-203">Download the KVM image of RHEL 6 from the Red Hat website.</span></span>

2. <span data-ttu-id="a034d-204">Set a root password.</span><span class="sxs-lookup"><span data-stu-id="a034d-204">Set a root password.</span></span>

    <span data-ttu-id="a034d-205">Generate an encrypted password, and copy the output of the command:</span><span class="sxs-lookup"><span data-stu-id="a034d-205">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="a034d-206">Set a root password with guestfish:</span><span class="sxs-lookup"><span data-stu-id="a034d-206">Set a root password with guestfish:</span></span>
        
        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="a034d-207">Change the second field of the root user from "!!"</span><span class="sxs-lookup"><span data-stu-id="a034d-207">Change the second field of the root user from "!!"</span></span> <span data-ttu-id="a034d-208">to the encrypted password.</span><span class="sxs-lookup"><span data-stu-id="a034d-208">to the encrypted password.</span></span>

3. <span data-ttu-id="a034d-209">Create a virtual machine in KVM from the qcow2 image.</span><span class="sxs-lookup"><span data-stu-id="a034d-209">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="a034d-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span><span class="sxs-lookup"><span data-stu-id="a034d-210">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="a034d-211">Then, start the virtual machine, and sign in as root.</span><span class="sxs-lookup"><span data-stu-id="a034d-211">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="a034d-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-212">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="a034d-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-213">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

6. <span data-ttu-id="a034d-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span><span class="sxs-lookup"><span data-stu-id="a034d-214">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="a034d-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a034d-215">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

7. <span data-ttu-id="a034d-216">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-216">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

8. <span data-ttu-id="a034d-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-217">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

9. <span data-ttu-id="a034d-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-218">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-219">To do this configuration, open `/boot/grub/menu.lst` in a text editor, and ensure that the default kernel includes the following parameters:</span></span>
    
        console=ttyS0 earlyprintk=ttyS0 rootdelay=300
    
    <span data-ttu-id="a034d-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-220">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span>
    
    <span data-ttu-id="a034d-221">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-221">In addition, we recommend that you remove the following parameters:</span></span>
    
        rhgb quiet crashkernel=auto
    
    <span data-ttu-id="a034d-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-222">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="a034d-223">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-223">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-224">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

    >[!Important]
    <span data-ttu-id="a034d-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-225">RHEL 6.5 and earlier must also set the `numa=off` kernel parameter.</span></span> <span data-ttu-id="a034d-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span><span class="sxs-lookup"><span data-stu-id="a034d-226">See Red Hat [KB 436883](https://access.redhat.com/solutions/436883).</span></span>

10. <span data-ttu-id="a034d-227">Add Hyper-V modules to initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-227">Add Hyper-V modules to initramfs:</span></span>  

    <span data-ttu-id="a034d-228">Edit `/etc/dracut.conf`, and add the following content:</span><span class="sxs-lookup"><span data-stu-id="a034d-228">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="a034d-229">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-229">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="a034d-230">Uninstall cloud-init:</span><span class="sxs-lookup"><span data-stu-id="a034d-230">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="a034d-231">Ensure that the SSH server is installed and configured to start at boot time:</span><span class="sxs-lookup"><span data-stu-id="a034d-231">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # chkconfig sshd on

    <span data-ttu-id="a034d-232">Modify /etc/ssh/sshd_config to include the following lines:</span><span class="sxs-lookup"><span data-stu-id="a034d-232">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="a034d-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-233">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-234">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-234">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

14. <span data-ttu-id="a034d-235">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-235">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

        # chkconfig waagent on

15. <span data-ttu-id="a034d-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-236">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-237">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-238">After you install the Azure Linux Agent in the previous step, modify the following parameters in **/etc/waagent.conf** appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="a034d-239">Unregister the subscription (if necessary) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-239">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="a034d-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-240">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="a034d-241">Shut down the virtual machine in KVM.</span><span class="sxs-lookup"><span data-stu-id="a034d-241">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="a034d-242">Convert the qcow2 image to the VHD format.</span><span class="sxs-lookup"><span data-stu-id="a034d-242">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="a034d-243">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="a034d-243">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-6.8.qcow2 rhel-6.8.raw

    <span data-ttu-id="a034d-244">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a034d-244">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="a034d-245">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="a034d-245">Otherwise, round up the size to align with 1 MB:</span></span>

                # MB=$((1024*1024))

                # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \

            gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

                # rounded_size=$((($size/$MB + 1)*$MB))

                # qemu-img resize rhel-6.8.raw $rounded_size


    <span data-ttu-id="a034d-246">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="a034d-246">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd


### <a name="prepare-a-rhel-7-virtual-machine-from-kvm"></a><span data-ttu-id="a034d-247">Prepare a RHEL 7 virtual machine from KVM</span><span class="sxs-lookup"><span data-stu-id="a034d-247">Prepare a RHEL 7 virtual machine from KVM</span></span>

1. <span data-ttu-id="a034d-248">Download the KVM image of RHEL 7 from the Red Hat website.</span><span class="sxs-lookup"><span data-stu-id="a034d-248">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="a034d-249">This procedure uses RHEL 7 as the example.</span><span class="sxs-lookup"><span data-stu-id="a034d-249">This procedure uses RHEL 7 as the example.</span></span>

2. <span data-ttu-id="a034d-250">Set a root password.</span><span class="sxs-lookup"><span data-stu-id="a034d-250">Set a root password.</span></span>

    <span data-ttu-id="a034d-251">Generate an encrypted password, and copy the output of the command:</span><span class="sxs-lookup"><span data-stu-id="a034d-251">Generate an encrypted password, and copy the output of the command:</span></span>

        # openssl passwd -1 changeme

    <span data-ttu-id="a034d-252">Set a root password with guestfish:</span><span class="sxs-lookup"><span data-stu-id="a034d-252">Set a root password with guestfish:</span></span>

        # guestfish --rw -a <image-name>
        > <fs> run
        > <fs> list-filesystems
        > <fs> mount /dev/sda1 /
        > <fs> vi /etc/shadow
        > <fs> exit

   <span data-ttu-id="a034d-253">Change the second field of root user from "!!"</span><span class="sxs-lookup"><span data-stu-id="a034d-253">Change the second field of root user from "!!"</span></span> <span data-ttu-id="a034d-254">to the encrypted password.</span><span class="sxs-lookup"><span data-stu-id="a034d-254">to the encrypted password.</span></span>

3. <span data-ttu-id="a034d-255">Create a virtual machine in KVM from the qcow2 image.</span><span class="sxs-lookup"><span data-stu-id="a034d-255">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="a034d-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span><span class="sxs-lookup"><span data-stu-id="a034d-256">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="a034d-257">Then, start the virtual machine, and sign in as root.</span><span class="sxs-lookup"><span data-stu-id="a034d-257">Then, start the virtual machine, and sign in as root.</span></span>

4. <span data-ttu-id="a034d-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-258">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

5. <span data-ttu-id="a034d-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-259">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

6. <span data-ttu-id="a034d-260">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-260">Ensure that the network service will start at boot time by running the following command:</span></span>

        # chkconfig network on

7. <span data-ttu-id="a034d-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-261">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

        # subscription-manager register --auto-attach --username=XXX --password=XXX

8. <span data-ttu-id="a034d-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-262">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-263">To do this configuration, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="a034d-264">For example:</span><span class="sxs-lookup"><span data-stu-id="a034d-264">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a034d-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-265">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a034d-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="a034d-266">The command also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a034d-267">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-267">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="a034d-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-268">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="a034d-269">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-269">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-270">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="a034d-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="a034d-271">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # grub2-mkconfig -o /boot/grub2/grub.cfg

10. <span data-ttu-id="a034d-272">Add Hyper-V modules into initramfs.</span><span class="sxs-lookup"><span data-stu-id="a034d-272">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="a034d-273">Edit `/etc/dracut.conf` and add content:</span><span class="sxs-lookup"><span data-stu-id="a034d-273">Edit `/etc/dracut.conf` and add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="a034d-274">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-274">Rebuild initramfs:</span></span>

        # dracut -f -v

11. <span data-ttu-id="a034d-275">Uninstall cloud-init:</span><span class="sxs-lookup"><span data-stu-id="a034d-275">Uninstall cloud-init:</span></span>

        # yum remove cloud-init

12. <span data-ttu-id="a034d-276">Ensure that the SSH server is installed and configured to start at boot time:</span><span class="sxs-lookup"><span data-stu-id="a034d-276">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

        # systemctl enable sshd

    <span data-ttu-id="a034d-277">Modify /etc/ssh/sshd_config to include the following lines:</span><span class="sxs-lookup"><span data-stu-id="a034d-277">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

        PasswordAuthentication yes
        ClientAliveInterval 180

13. <span data-ttu-id="a034d-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-278">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-279">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-279">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

14. <span data-ttu-id="a034d-280">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-280">Install the Azure Linux Agent by running the following command:</span></span>

        # yum install WALinuxAgent

    <span data-ttu-id="a034d-281">Enable the waagent service:</span><span class="sxs-lookup"><span data-stu-id="a034d-281">Enable the waagent service:</span></span>

        # systemctl enable waagent.service

15. <span data-ttu-id="a034d-282">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-282">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="a034d-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-283">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-284">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-285">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

16. <span data-ttu-id="a034d-286">Unregister the subscription (if necessary) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-286">Unregister the subscription (if necessary) by running the following command:</span></span>

        # subscription-manager unregister

17. <span data-ttu-id="a034d-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-287">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

18. <span data-ttu-id="a034d-288">Shut down the virtual machine in KVM.</span><span class="sxs-lookup"><span data-stu-id="a034d-288">Shut down the virtual machine in KVM.</span></span>

19. <span data-ttu-id="a034d-289">Convert the qcow2 image to the VHD format.</span><span class="sxs-lookup"><span data-stu-id="a034d-289">Convert the qcow2 image to the VHD format.</span></span>

    <span data-ttu-id="a034d-290">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="a034d-290">First convert the image to raw format:</span></span>

        # qemu-img convert -f qcow2 -O raw rhel-7.3.qcow2 rhel-7.3.raw

    <span data-ttu-id="a034d-291">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a034d-291">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="a034d-292">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="a034d-292">Otherwise, round up the size to align with 1 MB:</span></span>

                # MB=$((1024*1024))

                # size=$(qemu-img info -f raw --output json "rhel-7.3.raw" | \

            gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

                # rounded_size=$((($size/$MB + 1)*$MB))
        
                # qemu-img resize rhel-7.3.raw $rounded_size

    <span data-ttu-id="a034d-293">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="a034d-293">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="a034d-294">Prepare a Red Hat-based virtual machine from VMware</span><span class="sxs-lookup"><span data-stu-id="a034d-294">Prepare a Red Hat-based virtual machine from VMware</span></span>
### <a name="prerequisites"></a><span data-ttu-id="a034d-295">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a034d-295">Prerequisites</span></span>
<span data-ttu-id="a034d-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span><span class="sxs-lookup"><span data-stu-id="a034d-296">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="a034d-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="a034d-297">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="a034d-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span><span class="sxs-lookup"><span data-stu-id="a034d-298">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="a034d-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="a034d-299">This will avoid LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="a034d-300">LVM or RAID can be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="a034d-300">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="a034d-301">Do not configure a swap partition on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-301">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="a034d-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-302">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="a034d-303">You can find more information about this in the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="a034d-303">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="a034d-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span><span class="sxs-lookup"><span data-stu-id="a034d-304">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-6-virtual-machine-from-vmware"></a><span data-ttu-id="a034d-305">Prepare a RHEL 6 virtual machine from VMware</span><span class="sxs-lookup"><span data-stu-id="a034d-305">Prepare a RHEL 6 virtual machine from VMware</span></span>
1. <span data-ttu-id="a034d-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span><span class="sxs-lookup"><span data-stu-id="a034d-306">In RHEL 6, NetworkManager can interfere with the Azure Linux agent.</span></span> <span data-ttu-id="a034d-307">Uninstall this package by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-307">Uninstall this package by running the following command:</span></span>
   
        # sudo rpm -e --nodeps NetworkManager

2. <span data-ttu-id="a034d-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-308">Create a file named **network** in the /etc/sysconfig/ directory that contains the following text:</span></span>

        NETWORKING=yes
        HOSTNAME=localhost.localdomain

3. <span data-ttu-id="a034d-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-309">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no

4. <span data-ttu-id="a034d-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span><span class="sxs-lookup"><span data-stu-id="a034d-310">Move (or remove) the udev rules to avoid generating static rules for the Ethernet interface.</span></span> <span data-ttu-id="a034d-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span><span class="sxs-lookup"><span data-stu-id="a034d-311">These rules cause problems when you clone a virtual machine in Azure or Hyper-V:</span></span>

        # sudo ln -s /dev/null /etc/udev/rules.d/75-persistent-net-generator.rules

        # sudo rm -f /etc/udev/rules.d/70-persistent-net.rules

5. <span data-ttu-id="a034d-312">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-312">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

6. <span data-ttu-id="a034d-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-313">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

7. <span data-ttu-id="a034d-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-314">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-315">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-315">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-6-server-extras-rpms

8. <span data-ttu-id="a034d-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-316">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-317">To do this, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="a034d-318">For example:</span><span class="sxs-lookup"><span data-stu-id="a034d-318">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a034d-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-319">This will also ensure that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a034d-320">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="a034d-320">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a034d-321">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-321">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="a034d-322">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-322">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="a034d-323">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-323">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-324">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-324">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

9. <span data-ttu-id="a034d-325">Add Hyper-V modules to initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-325">Add Hyper-V modules to initramfs:</span></span>

    <span data-ttu-id="a034d-326">Edit `/etc/dracut.conf`, and add the following content:</span><span class="sxs-lookup"><span data-stu-id="a034d-326">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="a034d-327">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-327">Rebuild initramfs:</span></span>

        # dracut -f -v

10. <span data-ttu-id="a034d-328">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span><span class="sxs-lookup"><span data-stu-id="a034d-328">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="a034d-329">Modify `/etc/ssh/sshd_config` to include the following line:</span><span class="sxs-lookup"><span data-stu-id="a034d-329">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    <span data-ttu-id="a034d-330">ClientAliveInterval 180</span><span class="sxs-lookup"><span data-stu-id="a034d-330">ClientAliveInterval 180</span></span>

11. <span data-ttu-id="a034d-331">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-331">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo chkconfig waagent on

12. <span data-ttu-id="a034d-332">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-332">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="a034d-333">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-333">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-334">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-334">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-335">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-335">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

13. <span data-ttu-id="a034d-336">Unregister the subscription (if necessary) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-336">Unregister the subscription (if necessary) by running the following command:</span></span>

        # sudo subscription-manager unregister

14. <span data-ttu-id="a034d-337">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-337">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

15. <span data-ttu-id="a034d-338">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span><span class="sxs-lookup"><span data-stu-id="a034d-338">Shut down the virtual machine, and convert the VMDK file to a .vhd file.</span></span>

    <span data-ttu-id="a034d-339">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="a034d-339">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-6.8.vmdk rhel-6.8.raw

    <span data-ttu-id="a034d-340">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a034d-340">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="a034d-341">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="a034d-341">Otherwise, round up the size to align with 1 MB:</span></span>

                # MB=$((1024*1024))

                # size=$(qemu-img info -f raw --output json "rhel-6.8.raw" | \

            gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

                # rounded_size=$((($size/$MB + 1)*$MB))

                # qemu-img resize rhel-6.8.raw $rounded_size

    <span data-ttu-id="a034d-342">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="a034d-342">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-6.8.raw rhel-6.8.vhd

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="a034d-343">Prepare a RHEL 7 virtual machine from VMware</span><span class="sxs-lookup"><span data-stu-id="a034d-343">Prepare a RHEL 7 virtual machine from VMware</span></span>
1. <span data-ttu-id="a034d-344">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-344">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>
   
        NETWORKING=yes
        HOSTNAME=localhost.localdomain

2. <span data-ttu-id="a034d-345">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="a034d-345">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>
   
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no

3. <span data-ttu-id="a034d-346">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-346">Ensure that the network service will start at boot time by running the following command:</span></span>

        # sudo chkconfig network on

4. <span data-ttu-id="a034d-347">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-347">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

        # sudo subscription-manager register --auto-attach --username=XXX --password=XXX

5. <span data-ttu-id="a034d-348">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-348">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="a034d-349">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="a034d-349">To do this modification, open `/etc/default/grub` in a text editor, and edit the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="a034d-350">For example:</span><span class="sxs-lookup"><span data-stu-id="a034d-350">For example:</span></span>
   
        GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
   
   <span data-ttu-id="a034d-351">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="a034d-351">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="a034d-352">It also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="a034d-352">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="a034d-353">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="a034d-353">In addition, we recommend that you remove the following parameters:</span></span>
   
        rhgb quiet crashkernel=auto
   
    <span data-ttu-id="a034d-354">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="a034d-354">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="a034d-355">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="a034d-355">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="a034d-356">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="a034d-356">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

6. <span data-ttu-id="a034d-357">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="a034d-357">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

        # sudo grub2-mkconfig -o /boot/grub2/grub.cfg

7. <span data-ttu-id="a034d-358">Add Hyper-V modules to initramfs.</span><span class="sxs-lookup"><span data-stu-id="a034d-358">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="a034d-359">Edit `/etc/dracut.conf`, add content:</span><span class="sxs-lookup"><span data-stu-id="a034d-359">Edit `/etc/dracut.conf`, add content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

    <span data-ttu-id="a034d-360">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-360">Rebuild initramfs:</span></span>

        # dracut -f -v

8. <span data-ttu-id="a034d-361">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="a034d-361">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="a034d-362">This setting is usually the default.</span><span class="sxs-lookup"><span data-stu-id="a034d-362">This setting is usually the default.</span></span> <span data-ttu-id="a034d-363">Modify `/etc/ssh/sshd_config` to include the following line:</span><span class="sxs-lookup"><span data-stu-id="a034d-363">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

        ClientAliveInterval 180

9. <span data-ttu-id="a034d-364">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="a034d-364">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="a034d-365">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-365">Enable the extras repository by running the following command:</span></span>

        # subscription-manager repos --enable=rhel-7-server-extras-rpms

10. <span data-ttu-id="a034d-366">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-366">Install the Azure Linux Agent by running the following command:</span></span>

        # sudo yum install WALinuxAgent

        # sudo systemctl enable waagent.service

11. <span data-ttu-id="a034d-367">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-367">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="a034d-368">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-368">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="a034d-369">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="a034d-369">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="a034d-370">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="a034d-370">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

        ResourceDisk.Format=y
        ResourceDisk.Filesystem=ext4
        ResourceDisk.MountPoint=/mnt/resource
        ResourceDisk.EnableSwap=y
        ResourceDisk.SwapSizeMB=2048    ## NOTE: set this to whatever you need it to be.

12. <span data-ttu-id="a034d-371">If you want to unregister the subscription, run the following command:</span><span class="sxs-lookup"><span data-stu-id="a034d-371">If you want to unregister the subscription, run the following command:</span></span>

        # sudo subscription-manager unregister

13. <span data-ttu-id="a034d-372">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="a034d-372">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

        # sudo waagent -force -deprovision

        # export HISTSIZE=0

        # logout

14. <span data-ttu-id="a034d-373">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span><span class="sxs-lookup"><span data-stu-id="a034d-373">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    <span data-ttu-id="a034d-374">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="a034d-374">First convert the image to raw format:</span></span>

        # qemu-img convert -f vmdk -O raw rhel-7.3.vmdk rhel-7.3.raw

    <span data-ttu-id="a034d-375">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="a034d-375">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="a034d-376">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="a034d-376">Otherwise, round up the size to align with 1 MB:</span></span>

                # MB=$((1024*1024))

                # size=$(qemu-img info -f raw --output json "rhel-7.3.raw" | \

            gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')

                # rounded_size=$((($size/$MB + 1)*$MB))
                
                # qemu-img resize rhel-7.3.raw $rounded_size

    <span data-ttu-id="a034d-377">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="a034d-377">Convert the raw disk to a fixed-sized VHD:</span></span>

        # qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.3.raw rhel-7.3.vhd

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="a034d-378">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span><span class="sxs-lookup"><span data-stu-id="a034d-378">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>
### <a name="prepare-a-rhel-7-virtual-machine-from-a-kickstart-file"></a><span data-ttu-id="a034d-379">Prepare a RHEL 7 virtual machine from a kickstart file</span><span class="sxs-lookup"><span data-stu-id="a034d-379">Prepare a RHEL 7 virtual machine from a kickstart file</span></span>

1.  <span data-ttu-id="a034d-380">Create a kickstart file that includes the following content, and save the file.</span><span class="sxs-lookup"><span data-stu-id="a034d-380">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="a034d-381">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="a034d-381">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

        # Kickstart for provisioning a RHEL 7 Azure VM

        # System authorization information
          auth --enableshadow --passalgo=sha512

        # Use graphical install
        text

        # Do not run the Setup Agent on first boot
        firstboot --disable

        # Keyboard layouts
        keyboard --vckeymap=us --xlayouts='us'

        # System language
        lang en_US.UTF-8

        # Network information
        network  --bootproto=dhcp

        # Root password
        rootpw --plaintext "to_be_disabled"

        # System services
        services --enabled="sshd,waagent,NetworkManager"

        # System timezone
        timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

        # Partition clearing information
        clearpart --all --initlabel

        # Clear the MBR
        zerombr

        # Disk partitioning information
        part /boot --fstype="xfs" --size=500
        part / --fstyp="xfs" --size=1 --grow --asprimary

        # System bootloader configuration
        bootloader --location=mbr

        # Firewall configuration
        firewall --disabled

        # Enable SELinux
        selinux --enforcing

        # Don't configure X
        skipx

        # Power down the machine after install
        poweroff

        %packages
        @base
        @console-internet
        chrony
        sudo
        parted
        -dracut-config-rescue

        %end

        %post --log=/var/log/anaconda/post-install.log

        #!/bin/bash

        # Register Red Hat Subscription
        subscription-manager register --username=XXX --password=XXX --auto-attach --force

        # Install latest repo update
        yum update -y

        # Enable extras repo
        subscription-manager repos --enable=rhel-7-server-extras-rpms

        # Install WALinuxAgent
        yum install -y WALinuxAgent

        # Unregister Red Hat subscription
        subscription-manager unregister

        # Enable waaagent at boot-up
        systemctl enable waagent

        # Disable the root account
        usermod root -p '!!'

        # Configure swap in WALinuxAgent
        sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
        sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

        # Set the cmdline
        sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

        # Enable SSH keepalive
        sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

        # Build the grub cfg
        grub2-mkconfig -o /boot/grub2/grub.cfg

        # Configure network
        cat << EOF > /etc/sysconfig/network-scripts/ifcfg-eth0
        DEVICE=eth0
        ONBOOT=yes
        BOOTPROTO=dhcp
        TYPE=Ethernet
        USERCTL=no
        PEERDNS=yes
        IPV6INIT=no
        NM_CONTROLLED=no
        EOF

        # Deprovision and prepare for Azure
        waagent -force -deprovision

        %end

2. <span data-ttu-id="a034d-382">Place the kickstart file where the installation system can access it.</span><span class="sxs-lookup"><span data-stu-id="a034d-382">Place the kickstart file where the installation system can access it.</span></span>

3. <span data-ttu-id="a034d-383">In Hyper-V Manager, create a new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-383">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="a034d-384">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span><span class="sxs-lookup"><span data-stu-id="a034d-384">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

4. <span data-ttu-id="a034d-385">Open the virtual machine settings:</span><span class="sxs-lookup"><span data-stu-id="a034d-385">Open the virtual machine settings:</span></span>

    <span data-ttu-id="a034d-386">a.</span><span class="sxs-lookup"><span data-stu-id="a034d-386">a.</span></span>  <span data-ttu-id="a034d-387">Attach a new virtual hard disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-387">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="a034d-388">Make sure to select **VHD Format** and **Fixed Size**.</span><span class="sxs-lookup"><span data-stu-id="a034d-388">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="a034d-389">b.</span><span class="sxs-lookup"><span data-stu-id="a034d-389">b.</span></span>  <span data-ttu-id="a034d-390">Attach the installation ISO to the DVD drive.</span><span class="sxs-lookup"><span data-stu-id="a034d-390">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="a034d-391">c.</span><span class="sxs-lookup"><span data-stu-id="a034d-391">c.</span></span>  <span data-ttu-id="a034d-392">Set the BIOS to boot from CD.</span><span class="sxs-lookup"><span data-stu-id="a034d-392">Set the BIOS to boot from CD.</span></span>

5. <span data-ttu-id="a034d-393">Start the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="a034d-393">Start the virtual machine.</span></span> <span data-ttu-id="a034d-394">When the installation guide appears, press **Tab** to configure the boot options.</span><span class="sxs-lookup"><span data-stu-id="a034d-394">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

6. <span data-ttu-id="a034d-395">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a034d-395">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

7. <span data-ttu-id="a034d-396">Wait for the installation to finish.</span><span class="sxs-lookup"><span data-stu-id="a034d-396">Wait for the installation to finish.</span></span> <span data-ttu-id="a034d-397">When it's finished, the virtual machine will be shut down automatically.</span><span class="sxs-lookup"><span data-stu-id="a034d-397">When it's finished, the virtual machine will be shut down automatically.</span></span> <span data-ttu-id="a034d-398">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-398">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="a034d-399">Known issues</span><span class="sxs-lookup"><span data-stu-id="a034d-399">Known issues</span></span>
### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="a034d-400">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span><span class="sxs-lookup"><span data-stu-id="a034d-400">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="a034d-401">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span><span class="sxs-lookup"><span data-stu-id="a034d-401">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="a034d-402">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span><span class="sxs-lookup"><span data-stu-id="a034d-402">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="a034d-403">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span><span class="sxs-lookup"><span data-stu-id="a034d-403">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="a034d-404">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span><span class="sxs-lookup"><span data-stu-id="a034d-404">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="a034d-405">Edit `/etc/dracut.conf`, and add the following content:</span><span class="sxs-lookup"><span data-stu-id="a034d-405">Edit `/etc/dracut.conf`, and add the following content:</span></span>

        add_drivers+="hv_vmbus hv_netvsc hv_storvsc"

<span data-ttu-id="a034d-406">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="a034d-406">Rebuild initramfs:</span></span>

        # dracut -f -v

<span data-ttu-id="a034d-407">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="a034d-407">For more details, see the information about [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a034d-408">Next steps</span><span class="sxs-lookup"><span data-stu-id="a034d-408">Next steps</span></span>
<span data-ttu-id="a034d-409">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a034d-409">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure.</span></span> <span data-ttu-id="a034d-410">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a034d-410">If this is the first time that you're uploading the .vhd file to Azure, see steps 2 and 3 in [Creating and uploading a virtual hard disk that contains the Linux operating system](classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<span data-ttu-id="a034d-411">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="a034d-411">For more details about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
