---
title: Create and upload a Red Hat Enterprise Linux VHD for use in Azure Stack | Microsoft Docs
description: Learn to create and upload an Azure virtual hard disk (VHD) that contains a Red Hat Linux operating system.
services: azure-stack
documentationcenter: ''
author: JeffGoldner
manager: BradleyB
editor: ''
tags: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2018
ms.author: jeffgo
ms.openlocfilehash: c7f91b8e890eba8426455fce7861327aa43f4155
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865868"
---
# <a name="prepare-a-red-hat-based-virtual-machine-for-azure-stack"></a><span data-ttu-id="aa3d6-103">Prepare a Red Hat-based virtual machine for Azure Stack</span><span class="sxs-lookup"><span data-stu-id="aa3d6-103">Prepare a Red Hat-based virtual machine for Azure Stack</span></span>

<span data-ttu-id="aa3d6-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-104">In this article, you will learn how to prepare a Red Hat Enterprise Linux (RHEL) virtual machine for use in Azure Stack.</span></span> <span data-ttu-id="aa3d6-105">The versions of RHEL that are covered in this article are 7.1+.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-105">The versions of RHEL that are covered in this article are 7.1+.</span></span> <span data-ttu-id="aa3d6-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-106">The hypervisors for preparation that are covered in this article are Hyper-V, kernel-based virtual machine (KVM), and VMware.</span></span>

<span data-ttu-id="aa3d6-107">For Red Hat Enterprise Linux support information, refer to [Red Hat and Azure Stack: Frequently Asked Questions](https://access.redhat.com/articles/3413531).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-107">For Red Hat Enterprise Linux support information, refer to [Red Hat and Azure Stack: Frequently Asked Questions](https://access.redhat.com/articles/3413531).</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="aa3d6-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="aa3d6-108">Prepare a Red Hat-based virtual machine from Hyper-V Manager</span></span>

<span data-ttu-id="aa3d6-109">This section assumes that you already have an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-109">This section assumes that you already have an ISO file from the Red Hat website and installed the RHEL image to a virtual hard disk (VHD).</span></span> <span data-ttu-id="aa3d6-110">For more information about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-110">For more information about how to use Hyper-V Manager to install an operating system image, see [Install the Hyper-V Role and Configure a Virtual Machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

### <a name="rhel-installation-notes"></a><span data-ttu-id="aa3d6-111">RHEL installation notes</span><span class="sxs-lookup"><span data-stu-id="aa3d6-111">RHEL installation notes</span></span>

* <span data-ttu-id="aa3d6-112">Azure Stack does not support the VHDX format.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-112">Azure Stack does not support the VHDX format.</span></span> <span data-ttu-id="aa3d6-113">Azure supports only fixed VHD.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-113">Azure supports only fixed VHD.</span></span> <span data-ttu-id="aa3d6-114">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-114">You can use Hyper-V Manager to convert the disk to VHD format, or you can use the convert-vhd cmdlet.</span></span> <span data-ttu-id="aa3d6-115">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-115">If you use VirtualBox, select **Fixed size** as opposed to the default dynamically allocated option when you create the disk.</span></span>
* <span data-ttu-id="aa3d6-116">Azure Stack supports only generation 1 virtual machines.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-116">Azure Stack supports only generation 1 virtual machines.</span></span> <span data-ttu-id="aa3d6-117">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-117">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed-size disk.</span></span> <span data-ttu-id="aa3d6-118">You can't change a virtual machine's generation.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-118">You can't change a virtual machine's generation.</span></span> <span data-ttu-id="aa3d6-119">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-119">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v).</span></span>
* <span data-ttu-id="aa3d6-120">The maximum size that's allowed for the VHD is 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-120">The maximum size that's allowed for the VHD is 1,023 GB.</span></span>
* <span data-ttu-id="aa3d6-121">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-121">When you install the Linux operating system, we recommend that you use standard partitions rather than Logical Volume Manager (LVM), which is often the default for many installations.</span></span> <span data-ttu-id="aa3d6-122">This practice avoids LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-122">This practice avoids LVM name conflicts with cloned virtual machines, particularly if you ever need to attach an operating system disk to another identical virtual machine for troubleshooting.</span></span>
* <span data-ttu-id="aa3d6-123">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-123">Kernel support for mounting Universal Disk Format (UDF) file systems is required.</span></span> <span data-ttu-id="aa3d6-124">At first boot, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-124">At first boot, the UDF-formatted media that is attached to the guest passes the provisioning configuration to the Linux virtual machine.</span></span> <span data-ttu-id="aa3d6-125">The Azure Linux Agent must mount the UDF file system to read its configuration and provision the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-125">The Azure Linux Agent must mount the UDF file system to read its configuration and provision the virtual machine.</span></span>
* <span data-ttu-id="aa3d6-126">Do not configure a swap partition on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-126">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="aa3d6-127">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-127">The Linux Agent can be configured to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="aa3d6-128">More information about can be found in the following steps.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-128">More information about can be found in the following steps.</span></span>
* <span data-ttu-id="aa3d6-129">All VHDs on Azure must have a virtual size aligned to 1 MB.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-129">All VHDs on Azure must have a virtual size aligned to 1 MB.</span></span> <span data-ttu-id="aa3d6-130">When converting from a raw disk to VHD, you must ensure that the raw disk size is a multiple of 1 MB before conversion.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-130">When converting from a raw disk to VHD, you must ensure that the raw disk size is a multiple of 1 MB before conversion.</span></span> <span data-ttu-id="aa3d6-131">More details can be found in the steps below.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-131">More details can be found in the steps below.</span></span>
* <span data-ttu-id="aa3d6-132">Azure Stack does not support cloud-init.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-132">Azure Stack does not support cloud-init.</span></span> <span data-ttu-id="aa3d6-133">Your VM must be configured with a supported version of the Windows Azure Linux Agent (WALA).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-133">Your VM must be configured with a supported version of the Windows Azure Linux Agent (WALA).</span></span>

### <a name="prepare-a-rhel-7-virtual-machine-from-hyper-v-manager"></a><span data-ttu-id="aa3d6-134">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="aa3d6-134">Prepare a RHEL 7 virtual machine from Hyper-V Manager</span></span>

1. <span data-ttu-id="aa3d6-135">In Hyper-V Manager, select the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-135">In Hyper-V Manager, select the virtual machine.</span></span>

1. <span data-ttu-id="aa3d6-136">Click **Connect** to open a console window for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-136">Click **Connect** to open a console window for the virtual machine.</span></span>

1. <span data-ttu-id="aa3d6-137">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-137">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>

    ```sh
    NETWORKING=yes
    HOSTNAME=localhost.localdomain
    ```

1. <span data-ttu-id="aa3d6-138">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text as needed:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-138">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text as needed:</span></span>

    ```sh
    DEVICE=eth0
    ONBOOT=yes
    BOOTPROTO=dhcp
    TYPE=Ethernet
    USERCTL=no
    PEERDNS=yes
    IPV6INIT=no
    NM_CONTROLLED=no
    ```

1. <span data-ttu-id="aa3d6-139">Ensure that the network service starts at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-139">Ensure that the network service starts at boot time by running the following command:</span></span>

    ```bash
    sudo systemctl enable network
    ```

1. <span data-ttu-id="aa3d6-140">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-140">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

    ```bash
    sudo subscription-manager register --auto-attach --username=XXX --password=XXX
    ```

1. <span data-ttu-id="aa3d6-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-141">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="aa3d6-142">To do this modification, open `/etc/default/grub` in a text editor, and modify the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-142">To do this modification, open `/etc/default/grub` in a text editor, and modify the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="aa3d6-143">For example:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-143">For example:</span></span>

    ```sh
    GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
    ```

   <span data-ttu-id="aa3d6-144">This ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-144">This ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="aa3d6-145">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-145">This configuration also turns off the new RHEL 7 naming conventions for NICs.</span></span>

   <span data-ttu-id="aa3d6-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-146">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="aa3d6-147">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-147">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="aa3d6-148">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-148">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span> <span data-ttu-id="aa3d6-149">We recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-149">We recommend that you remove the following parameters:</span></span>

    ```sh
    rhgb quiet crashkernel=auto
    ```

1. <span data-ttu-id="aa3d6-150">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-150">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

    ```bash
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    ```

1. <span data-ttu-id="aa3d6-151">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-151">Ensure that the SSH server is installed and configured to start at boot time, which is usually the default.</span></span> <span data-ttu-id="aa3d6-152">Modify `/etc/ssh/sshd_config` to include the following line:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-152">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    ```sh
    ClientAliveInterval 180
    ```

1. <span data-ttu-id="aa3d6-153">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-153">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="aa3d6-154">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-154">Enable the extras repository by running the following command:</span></span>

    ```bash
    subscription-manager repos --enable=rhel-7-server-extras-rpms
    ```

1. <span data-ttu-id="aa3d6-155">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-155">Install the Azure Linux Agent by running the following command:</span></span>

    ```bash
    sudo yum install WALinuxAgent
    sudo systemctl enable waagent.service
    ```

1. <span data-ttu-id="aa3d6-156">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-156">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="aa3d6-157">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-157">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="aa3d6-158">The local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-158">The local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="aa3d6-159">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-159">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

    ```sh
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    #NOTE: set this to whatever you need it to be.
    ```

1. <span data-ttu-id="aa3d6-160">If you want to unregister the subscription, run the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-160">If you want to unregister the subscription, run the following command:</span></span>

    ```bash
    sudo subscription-manager unregister
    ```

1. <span data-ttu-id="aa3d6-161">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-161">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span></span> <span data-ttu-id="aa3d6-162">You need to place that into the trusted root store.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-162">You need to place that into the trusted root store.</span></span> <span data-ttu-id="aa3d6-163">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-163">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span></span>

1. <span data-ttu-id="aa3d6-164">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-164">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

    ```bash
    sudo waagent -force -deprovision
    export HISTSIZE=0
    logout
    ```

1. <span data-ttu-id="aa3d6-165">Click **Action** > **Shut Down** in Hyper-V Manager.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-165">Click **Action** > **Shut Down** in Hyper-V Manager.</span></span>

1. <span data-ttu-id="aa3d6-166">Convert the VHD to a fixed size VHD using either the Hyper-V Manager "Edit disk" feature, or the Convert-VHD PowerShell command.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-166">Convert the VHD to a fixed size VHD using either the Hyper-V Manager "Edit disk" feature, or the Convert-VHD PowerShell command.</span></span> <span data-ttu-id="aa3d6-167">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-167">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="prepare-a-red-hat-based-virtual-machine-from-kvm"></a><span data-ttu-id="aa3d6-168">Prepare a Red Hat-based virtual machine from KVM</span><span class="sxs-lookup"><span data-stu-id="aa3d6-168">Prepare a Red Hat-based virtual machine from KVM</span></span>

1. <span data-ttu-id="aa3d6-169">Download the KVM image of RHEL 7 from the Red Hat website.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-169">Download the KVM image of RHEL 7 from the Red Hat website.</span></span> <span data-ttu-id="aa3d6-170">This procedure uses RHEL 7 as the example.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-170">This procedure uses RHEL 7 as the example.</span></span>

1. <span data-ttu-id="aa3d6-171">Set a root password.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-171">Set a root password.</span></span>

    <span data-ttu-id="aa3d6-172">Generate an encrypted password, and copy the output of the command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-172">Generate an encrypted password, and copy the output of the command:</span></span>

    ```bash
    openssl passwd -1 changeme
    ```

   <span data-ttu-id="aa3d6-173">Set a root password with guestfish:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-173">Set a root password with guestfish:</span></span>

    ```sh
    guestfish --rw -a <image-name>
    > <fs> run
    > <fs> list-filesystems
    > <fs> mount /dev/sda1 /
    > <fs> vi /etc/shadow
    > <fs> exit
    ```

   <span data-ttu-id="aa3d6-174">Change the second field of root user from "!!"</span><span class="sxs-lookup"><span data-stu-id="aa3d6-174">Change the second field of root user from "!!"</span></span> <span data-ttu-id="aa3d6-175">to the encrypted password.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-175">to the encrypted password.</span></span>

1. <span data-ttu-id="aa3d6-176">Create a virtual machine in KVM from the qcow2 image.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-176">Create a virtual machine in KVM from the qcow2 image.</span></span> <span data-ttu-id="aa3d6-177">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-177">Set the disk type to **qcow2**, and set the virtual network interface device model to **virtio**.</span></span> <span data-ttu-id="aa3d6-178">Then, start the virtual machine, and sign in as root.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-178">Then, start the virtual machine, and sign in as root.</span></span>

1. <span data-ttu-id="aa3d6-179">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-179">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>

    ```sh
    NETWORKING=yes
    HOSTNAME=localhost.localdomain
    ```

1. <span data-ttu-id="aa3d6-180">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-180">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>

    ```sh
    DEVICE=eth0
    ONBOOT=yes
    BOOTPROTO=dhcp
    TYPE=Ethernet
    USERCTL=no
    PEERDNS=yes
    IPV6INIT=no
    NM_CONTROLLED=no
    ```

1. <span data-ttu-id="aa3d6-181">Ensure that the network service starts at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-181">Ensure that the network service starts at boot time by running the following command:</span></span>

    ```bash
    sudo systemctl enable network
    ```

1. <span data-ttu-id="aa3d6-182">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-182">Register your Red Hat subscription to enable installation of packages from the RHEL repository by running the following command:</span></span>

    ```bash
    subscription-manager register --auto-attach --username=XXX --password=XXX
    ```

1. <span data-ttu-id="aa3d6-183">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-183">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="aa3d6-184">To do this configuration, open `/etc/default/grub` in a text editor, and modify  the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-184">To do this configuration, open `/etc/default/grub` in a text editor, and modify  the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="aa3d6-185">For example:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-185">For example:</span></span>

    ```sh
    GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
    ```

   <span data-ttu-id="aa3d6-186">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-186">This command also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="aa3d6-187">The command also turns off the new RHEL 7 naming conventions for NICs</span><span class="sxs-lookup"><span data-stu-id="aa3d6-187">The command also turns off the new RHEL 7 naming conventions for NICs</span></span>

   <span data-ttu-id="aa3d6-188">Graphical and quiet boot are not useful in a cloud environment where all the logs are sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-188">Graphical and quiet boot are not useful in a cloud environment where all the logs are sent to the serial port.</span></span> <span data-ttu-id="aa3d6-189">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-189">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="aa3d6-190">This parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-190">This parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span> <span data-ttu-id="aa3d6-191">We recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-191">We recommend that you remove the following parameters:</span></span>

    ```sh
    rhgb quiet crashkernel=auto
    ```

1. <span data-ttu-id="aa3d6-192">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-192">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

    ```bash
    grub2-mkconfig -o /boot/grub2/grub.cfg
    ```

1. <span data-ttu-id="aa3d6-193">Add Hyper-V modules into initramfs.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-193">Add Hyper-V modules into initramfs.</span></span>

    <span data-ttu-id="aa3d6-194">Edit `/etc/dracut.conf` and add content:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-194">Edit `/etc/dracut.conf` and add content:</span></span>

    ```sh
    add_drivers+="hv_vmbus hv_netvsc hv_storvsc"
    ```

    <span data-ttu-id="aa3d6-195">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-195">Rebuild initramfs:</span></span>

    ```bash
    dracut -f -v
    ```

1. <span data-ttu-id="aa3d6-196">Uninstall cloud-init:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-196">Uninstall cloud-init:</span></span>

    ```bash
    yum remove cloud-init
    ```

1. <span data-ttu-id="aa3d6-197">Ensure that the SSH server is installed and configured to start at boot time:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-197">Ensure that the SSH server is installed and configured to start at boot time:</span></span>

    ```bash
    systemctl enable sshd
    ```

    <span data-ttu-id="aa3d6-198">Modify /etc/ssh/sshd_config to include the following lines:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-198">Modify /etc/ssh/sshd_config to include the following lines:</span></span>

    ```sh
    PasswordAuthentication yes
    ClientAliveInterval 180
    ```

1. <span data-ttu-id="aa3d6-199">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-199">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="aa3d6-200">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-200">Enable the extras repository by running the following command:</span></span>

    ```bash
    subscription-manager repos --enable=rhel-7-server-extras-rpms
    ```

1. <span data-ttu-id="aa3d6-201">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-201">Install the Azure Linux Agent by running the following command:</span></span>

    ```bash
    yum install WALinuxAgent
    ```

    <span data-ttu-id="aa3d6-202">Enable the waagent service:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-202">Enable the waagent service:</span></span>

    ```bash
    systemctl enable waagent.service
    ```

1. <span data-ttu-id="aa3d6-203">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-203">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="aa3d6-204">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-204">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="aa3d6-205">The local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-205">The local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="aa3d6-206">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-206">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

    ```sh
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    #NOTE: set this to whatever you need it to be.
    ```

1. <span data-ttu-id="aa3d6-207">Unregister the subscription (if necessary) by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-207">Unregister the subscription (if necessary) by running the following command:</span></span>

    ```bash
    subscription-manager unregister
    ```

1. <span data-ttu-id="aa3d6-208">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-208">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span></span> <span data-ttu-id="aa3d6-209">You need to place that into the trusted root store.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-209">You need to place that into the trusted root store.</span></span> <span data-ttu-id="aa3d6-210">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-210">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span></span>

1. <span data-ttu-id="aa3d6-211">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-211">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

    ```bash
    sudo waagent -force -deprovision
    export HISTSIZE=0
    logout
    ```

1. <span data-ttu-id="aa3d6-212">Shut down the virtual machine in KVM.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-212">Shut down the virtual machine in KVM.</span></span>

1. <span data-ttu-id="aa3d6-213">Convert the qcow2 image to the VHD format.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-213">Convert the qcow2 image to the VHD format.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa3d6-214">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-214">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span></span> <span data-ttu-id="aa3d6-215">The issue has been fixed in QEMU 2.6.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-215">The issue has been fixed in QEMU 2.6.</span></span> <span data-ttu-id="aa3d6-216">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-216">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span></span> <span data-ttu-id="aa3d6-217">Reference: https://bugs.launchpad.net/qemu/+bug/1490611.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-217">Reference: https://bugs.launchpad.net/qemu/+bug/1490611.</span></span>

    <span data-ttu-id="aa3d6-218">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-218">First convert the image to raw format:</span></span>

    ```bash
    qemu-img convert -f qcow2 -O raw rhel-7.4.qcow2 rhel-7.4.raw
    ```

    <span data-ttu-id="aa3d6-219">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-219">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="aa3d6-220">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-220">Otherwise, round up the size to align with 1 MB:</span></span>

    ```bash
    MB=$((1024*1024))
    size=$(qemu-img info -f raw --output json "rhel-7.4.raw" | \
    gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
    rounded_size=$((($size/$MB + 1)*$MB))
    qemu-img resize rhel-7.4.raw $rounded_size
    ```

    <span data-ttu-id="aa3d6-221">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-221">Convert the raw disk to a fixed-sized VHD:</span></span>

    ```bash
    qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.4.raw rhel-7.4.vhd
    ```

    <span data-ttu-id="aa3d6-222">Or, with qemu version **2.6+** include the `force_size` option:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-222">Or, with qemu version **2.6+** include the `force_size` option:</span></span>

    ```bash
    qemu-img convert -f raw -o subformat=fixed,force_size -O vpc rhel-7.4.raw rhel-7.4.vhd
    ```

## <a name="prepare-a-red-hat-based-virtual-machine-from-vmware"></a><span data-ttu-id="aa3d6-223">Prepare a Red Hat-based virtual machine from VMware</span><span class="sxs-lookup"><span data-stu-id="aa3d6-223">Prepare a Red Hat-based virtual machine from VMware</span></span>

<span data-ttu-id="aa3d6-224">This section assumes that you have already installed a RHEL virtual machine in VMware.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-224">This section assumes that you have already installed a RHEL virtual machine in VMware.</span></span> <span data-ttu-id="aa3d6-225">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-225">For details about how to install an operating system in VMware, see [VMware Guest Operating System Installation Guide](http://partnerweb.vmware.com/GOSIG/home.html).</span></span>

* <span data-ttu-id="aa3d6-226">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-226">When you install the Linux operating system, we recommend that you use standard partitions rather than LVM, which is often the default for many installations.</span></span> <span data-ttu-id="aa3d6-227">This avoids LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-227">This avoids LVM name conflicts with cloned virtual machine, particularly if an operating system disk ever needs to be attached to another virtual machine for troubleshooting.</span></span> <span data-ttu-id="aa3d6-228">LVM or RAID can be used on data disks if preferred.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-228">LVM or RAID can be used on data disks if preferred.</span></span>
* <span data-ttu-id="aa3d6-229">Do not configure a swap partition on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-229">Do not configure a swap partition on the operating system disk.</span></span> <span data-ttu-id="aa3d6-230">You can configure the Linux agent to create a swap file on the temporary resource disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-230">You can configure the Linux agent to create a swap file on the temporary resource disk.</span></span> <span data-ttu-id="aa3d6-231">You can find more information about this in the steps that follow.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-231">You can find more information about this in the steps that follow.</span></span>
* <span data-ttu-id="aa3d6-232">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-232">When you create the virtual hard disk, select **Store virtual disk as a single file**.</span></span>

### <a name="prepare-a-rhel-7-virtual-machine-from-vmware"></a><span data-ttu-id="aa3d6-233">Prepare a RHEL 7 virtual machine from VMware</span><span class="sxs-lookup"><span data-stu-id="aa3d6-233">Prepare a RHEL 7 virtual machine from VMware</span></span>

1. <span data-ttu-id="aa3d6-234">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-234">Create or edit the `/etc/sysconfig/network` file, and add the following text:</span></span>

    ```sh
    NETWORKING=yes
    HOSTNAME=localhost.localdomain
    ```

1. <span data-ttu-id="aa3d6-235">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-235">Create or edit the `/etc/sysconfig/network-scripts/ifcfg-eth0` file, and add the following text:</span></span>

    ```sh
    DEVICE=eth0
    ONBOOT=yes
    BOOTPROTO=dhcp
    TYPE=Ethernet
    USERCTL=no
    PEERDNS=yes
    IPV6INIT=no
    NM_CONTROLLED=no
    ```

1. <span data-ttu-id="aa3d6-236">Ensure that the network service will start at boot time by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-236">Ensure that the network service will start at boot time by running the following command:</span></span>

    ```bash
    sudo chkconfig network on
    ```

1. <span data-ttu-id="aa3d6-237">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-237">Register your Red Hat subscription to enable the installation of packages from the RHEL repository by running the following command:</span></span>

    ```bash
    sudo subscription-manager register --auto-attach --username=XXX --password=XXX
    ```

1. <span data-ttu-id="aa3d6-238">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-238">Modify the kernel boot line in your grub configuration to include additional kernel parameters for Azure.</span></span> <span data-ttu-id="aa3d6-239">To do this modification, open `/etc/default/grub` in a text editor, and modify the `GRUB_CMDLINE_LINUX` parameter.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-239">To do this modification, open `/etc/default/grub` in a text editor, and modify the `GRUB_CMDLINE_LINUX` parameter.</span></span> <span data-ttu-id="aa3d6-240">For example:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-240">For example:</span></span>

    ```sh
    GRUB_CMDLINE_LINUX="rootdelay=300 console=ttyS0 earlyprintk=ttyS0 net.ifnames=0"
    ```

    <span data-ttu-id="aa3d6-241">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-241">This configuration also ensures that all console messages are sent to the first serial port, which can assist Azure support with debugging issues.</span></span> <span data-ttu-id="aa3d6-242">It also turns off the new RHEL 7 naming conventions for NICs.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-242">It also turns off the new RHEL 7 naming conventions for NICs.</span></span> <span data-ttu-id="aa3d6-243">In addition, we recommend that you remove the following parameters:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-243">In addition, we recommend that you remove the following parameters:</span></span>

    ```sh
    rhgb quiet crashkernel=auto
    ```

    <span data-ttu-id="aa3d6-244">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-244">Graphical and quiet boot are not useful in a cloud environment where we want all the logs to be sent to the serial port.</span></span> <span data-ttu-id="aa3d6-245">You can leave the `crashkernel` option configured if desired.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-245">You can leave the `crashkernel` option configured if desired.</span></span> <span data-ttu-id="aa3d6-246">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-246">Note that this parameter reduces the amount of available memory in the virtual machine by 128 MB or more, which might be problematic on smaller virtual machine sizes.</span></span>

1. <span data-ttu-id="aa3d6-247">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-247">After you are done editing `/etc/default/grub`, run the following command to rebuild the grub configuration:</span></span>

    ```bash
    sudo grub2-mkconfig -o /boot/grub2/grub.cfg
    ```

1. <span data-ttu-id="aa3d6-248">Add Hyper-V modules to initramfs.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-248">Add Hyper-V modules to initramfs.</span></span>

    <span data-ttu-id="aa3d6-249">Edit `/etc/dracut.conf`, add content:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-249">Edit `/etc/dracut.conf`, add content:</span></span>

    ```sh
    add_drivers+="hv_vmbus hv_netvsc hv_storvsc"
    ```

    <span data-ttu-id="aa3d6-250">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-250">Rebuild initramfs:</span></span>

    ```bash
    dracut -f -v
    ```

1. <span data-ttu-id="aa3d6-251">Ensure that the SSH server is installed and configured to start at boot time.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-251">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="aa3d6-252">This setting is usually the default.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-252">This setting is usually the default.</span></span> <span data-ttu-id="aa3d6-253">Modify `/etc/ssh/sshd_config` to include the following line:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-253">Modify `/etc/ssh/sshd_config` to include the following line:</span></span>

    ```sh
    ClientAliveInterval 180
    ```

1. <span data-ttu-id="aa3d6-254">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-254">The WALinuxAgent package, `WALinuxAgent-<version>`, has been pushed to the Red Hat extras repository.</span></span> <span data-ttu-id="aa3d6-255">Enable the extras repository by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-255">Enable the extras repository by running the following command:</span></span>

    ```bash
    subscription-manager repos --enable=rhel-7-server-extras-rpms
    ```

1. <span data-ttu-id="aa3d6-256">Install the Azure Linux Agent by running the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-256">Install the Azure Linux Agent by running the following command:</span></span>

    ```bash
    sudo yum install WALinuxAgent
    sudo systemctl enable waagent.service
    ```

1. <span data-ttu-id="aa3d6-257">Do not create swap space on the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-257">Do not create swap space on the operating system disk.</span></span>

    <span data-ttu-id="aa3d6-258">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-258">The Azure Linux Agent can automatically configure swap space by using the local resource disk that is attached to the virtual machine after the virtual machine is provisioned on Azure.</span></span> <span data-ttu-id="aa3d6-259">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-259">Note that the local resource disk is a temporary disk, and it might be emptied when the virtual machine is deprovisioned.</span></span> <span data-ttu-id="aa3d6-260">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-260">After you install the Azure Linux Agent in the previous step, modify the following parameters in `/etc/waagent.conf` appropriately:</span></span>

    ```sh
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.EnableSwap=y
    ResourceDisk.SwapSizeMB=2048    NOTE: set this to whatever you need it to be.
    ```

1. <span data-ttu-id="aa3d6-261">If you want to unregister the subscription, run the following command:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-261">If you want to unregister the subscription, run the following command:</span></span>

    ```bash
    sudo subscription-manager unregister
    ```

1. <span data-ttu-id="aa3d6-262">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-262">If you are using a system that was deployed using an Enterprise Certificate Authority, the RHEL virtual machine will not trust the Azure Stack root certificate.</span></span> <span data-ttu-id="aa3d6-263">You need to place that into the trusted root store.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-263">You need to place that into the trusted root store.</span></span> <span data-ttu-id="aa3d6-264">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-264">See [Adding trusted root certificates to the server](https://manuals.gfi.com/en/kerio/connect/content/server-configuration/ssl-certificates/adding-trusted-root-certificates-to-the-server-1605.html).</span></span>

1. <span data-ttu-id="aa3d6-265">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-265">Run the following commands to deprovision the virtual machine and prepare it for provisioning on Azure:</span></span>

    ```bash
    sudo waagent -force -deprovision
    export HISTSIZE=0
    logout
    ```

1. <span data-ttu-id="aa3d6-266">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-266">Shut down the virtual machine, and convert the VMDK file to the VHD format.</span></span>

    > [!NOTE]
    > <span data-ttu-id="aa3d6-267">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-267">There is a known bug in qemu-img versions >=2.2.1 that results in an improperly formatted VHD.</span></span> <span data-ttu-id="aa3d6-268">The issue has been fixed in QEMU 2.6.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-268">The issue has been fixed in QEMU 2.6.</span></span> <span data-ttu-id="aa3d6-269">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-269">It is recommended to use either qemu-img 2.2.0 or lower, or update to 2.6 or higher.</span></span> <span data-ttu-id="aa3d6-270">Reference: <https://bugs.launchpad.net/qemu/+bug/1490611>.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-270">Reference: <https://bugs.launchpad.net/qemu/+bug/1490611>.</span></span>

    <span data-ttu-id="aa3d6-271">First convert the image to raw format:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-271">First convert the image to raw format:</span></span>

    ```bash
    qemu-img convert -f qcow2 -O raw rhel-7.4.qcow2 rhel-7.4.raw
    ```

    <span data-ttu-id="aa3d6-272">Make sure that the size of the raw image is aligned with 1 MB.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-272">Make sure that the size of the raw image is aligned with 1 MB.</span></span> <span data-ttu-id="aa3d6-273">Otherwise, round up the size to align with 1 MB:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-273">Otherwise, round up the size to align with 1 MB:</span></span>

    ```bash
    MB=$((1024*1024))
    size=$(qemu-img info -f raw --output json "rhel-7.4.raw" | \
    gawk 'match($0, /"virtual-size": ([0-9]+),/, val) {print val[1]}')
    rounded_size=$((($size/$MB + 1)*$MB))
    qemu-img resize rhel-7.4.raw $rounded_size
    ```

    <span data-ttu-id="aa3d6-274">Convert the raw disk to a fixed-sized VHD:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-274">Convert the raw disk to a fixed-sized VHD:</span></span>

    ```bash
    qemu-img convert -f raw -o subformat=fixed -O vpc rhel-7.4.raw rhel-7.4.vhd
    ```

    <span data-ttu-id="aa3d6-275">Or, with qemu version **2.6+** include the `force_size` option:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-275">Or, with qemu version **2.6+** include the `force_size` option:</span></span>

    ```bash
    qemu-img convert -f raw -o subformat=fixed,force_size -O vpc rhel-7.4.raw rhel-7.4.vhd
    ```

## <a name="prepare-a-red-hat-based-virtual-machine-from-an-iso-by-using-a-kickstart-file-automatically"></a><span data-ttu-id="aa3d6-276">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span><span class="sxs-lookup"><span data-stu-id="aa3d6-276">Prepare a Red Hat-based virtual machine from an ISO by using a kickstart file automatically</span></span>

1. <span data-ttu-id="aa3d6-277">Create a kickstart file that includes the following content, and save the file.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-277">Create a kickstart file that includes the following content, and save the file.</span></span> <span data-ttu-id="aa3d6-278">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-278">For details about kickstart installation, see the [Kickstart Installation Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-kickstart-installations.html).</span></span>

    ```sh
    Kickstart for provisioning a RHEL 7 Azure VM

    System authorization information
    auth --enableshadow --passalgo=sha512

    Use graphical install
    text

    Do not run the Setup Agent on first boot
    firstboot --disable

    Keyboard layouts
    keyboard --vckeymap=us --xlayouts='us'

    System language
    lang en_US.UTF-8

    Network information
    network  --bootproto=dhcp

    Root password
    rootpw --plaintext "to_be_disabled"

    System services
    services --enabled="sshd,waagent,NetworkManager"

    System timezone
    timezone Etc/UTC --isUtc --ntpservers 0.rhel.pool.ntp.org,1.rhel.pool.ntp.org,2.rhel.pool.ntp.org,3.rhel.pool.ntp.org

    Partition clearing information
    clearpart --all --initlabel

    Clear the MBR
    zerombr

    Disk partitioning information
    part /boot --fstype="xfs" --size=500
    part / --fstyp="xfs" --size=1 --grow --asprimary

    System bootloader configuration
    bootloader --location=mbr

    Firewall configuration
    firewall --disabled

    Enable SELinux
    selinux --enforcing

    Don't configure X
    skipx

    Power down the machine after install
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

    Register Red Hat Subscription
    subscription-manager register --username=XXX --password=XXX --auto-attach --force

    Install latest repo update
    yum update -y

    Enable extras repo
    subscription-manager repos --enable=rhel-7-server-extras-rpms

    Install WALinuxAgent
    yum install -y WALinuxAgent

    Unregister Red Hat subscription
    subscription-manager unregister

    Enable waaagent at boot-up
    systemctl enable waagent

    Disable the root account
    usermod root -p '!!'

    Configure swap in WALinuxAgent
    sed -i 's/^\(ResourceDisk\.EnableSwap\)=[Nn]$/\1=y/g' /etc/waagent.conf
    sed -i 's/^\(ResourceDisk\.SwapSizeMB\)=[0-9]*$/\1=2048/g' /etc/waagent.conf

    Set the cmdline
    sed -i 's/^\(GRUB_CMDLINE_LINUX\)=".*"$/\1="console=tty1 console=ttyS0 earlyprintk=ttyS0 rootdelay=300"/g' /etc/default/grub

    Enable SSH keepalive
    sed -i 's/^#\(ClientAliveInterval\).*$/\1 180/g' /etc/ssh/sshd_config

    Build the grub cfg
    grub2-mkconfig -o /boot/grub2/grub.cfg

    Configure network
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

    Deprovision and prepare for Azure
    waagent -force -deprovision

    %end
    ```

1. <span data-ttu-id="aa3d6-279">Place the kickstart file where the installation system can access it.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-279">Place the kickstart file where the installation system can access it.</span></span>

1. <span data-ttu-id="aa3d6-280">In Hyper-V Manager, create a new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-280">In Hyper-V Manager, create a new virtual machine.</span></span> <span data-ttu-id="aa3d6-281">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-281">On the **Connect Virtual Hard Disk** page, select **Attach a virtual hard disk later**, and complete the New Virtual Machine Wizard.</span></span>

1. <span data-ttu-id="aa3d6-282">Open the virtual machine settings:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-282">Open the virtual machine settings:</span></span>

    <span data-ttu-id="aa3d6-283">a.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-283">a.</span></span> <span data-ttu-id="aa3d6-284">Attach a new virtual hard disk to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-284">Attach a new virtual hard disk to the virtual machine.</span></span> <span data-ttu-id="aa3d6-285">Make sure to select **VHD Format** and **Fixed Size**.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-285">Make sure to select **VHD Format** and **Fixed Size**.</span></span>

    <span data-ttu-id="aa3d6-286">b.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-286">b.</span></span> <span data-ttu-id="aa3d6-287">Attach the installation ISO to the DVD drive.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-287">Attach the installation ISO to the DVD drive.</span></span>

    <span data-ttu-id="aa3d6-288">c.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-288">c.</span></span> <span data-ttu-id="aa3d6-289">Set the BIOS to boot from CD.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-289">Set the BIOS to boot from CD.</span></span>

1. <span data-ttu-id="aa3d6-290">Start the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-290">Start the virtual machine.</span></span> <span data-ttu-id="aa3d6-291">When the installation guide appears, press **Tab** to configure the boot options.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-291">When the installation guide appears, press **Tab** to configure the boot options.</span></span>

1. <span data-ttu-id="aa3d6-292">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-292">Enter `inst.ks=<the location of the kickstart file>` at the end of the boot options, and press **Enter**.</span></span>

1. <span data-ttu-id="aa3d6-293">Wait for the installation to finish.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-293">Wait for the installation to finish.</span></span> <span data-ttu-id="aa3d6-294">When it's finished, the virtual machine is shut down automatically.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-294">When it's finished, the virtual machine is shut down automatically.</span></span> <span data-ttu-id="aa3d6-295">Your Linux VHD is now ready to be uploaded to Azure.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-295">Your Linux VHD is now ready to be uploaded to Azure.</span></span>

## <a name="known-issues"></a><span data-ttu-id="aa3d6-296">Known issues</span><span class="sxs-lookup"><span data-stu-id="aa3d6-296">Known issues</span></span>

### <a name="the-hyper-v-driver-could-not-be-included-in-the-initial-ram-disk-when-using-a-non-hyper-v-hypervisor"></a><span data-ttu-id="aa3d6-297">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span><span class="sxs-lookup"><span data-stu-id="aa3d6-297">The Hyper-V driver could not be included in the initial RAM disk when using a non-Hyper-V hypervisor</span></span>

<span data-ttu-id="aa3d6-298">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-298">In some cases, Linux installers might not include the drivers for Hyper-V in the initial RAM disk (initrd or initramfs) unless Linux detects that it is running in a Hyper-V environment.</span></span>

<span data-ttu-id="aa3d6-299">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-299">When you're using a different virtualization system (that is, Virtualbox, Xen, etc.) to prepare your Linux image, you might need to rebuild initrd to ensure that at least the hv_vmbus and hv_storvsc kernel modules are available on the initial RAM disk.</span></span> <span data-ttu-id="aa3d6-300">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-300">This is a known issue at least on systems that are based on the upstream Red Hat distribution.</span></span>

<span data-ttu-id="aa3d6-301">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-301">To resolve this issue, add Hyper-V modules to initramfs and rebuild it:</span></span>

<span data-ttu-id="aa3d6-302">Edit `/etc/dracut.conf`, and add the following content:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-302">Edit `/etc/dracut.conf`, and add the following content:</span></span>

    ```sh
    add_drivers+="hv_vmbus hv_netvsc hv_storvsc"
    ```

<span data-ttu-id="aa3d6-303">Rebuild initramfs:</span><span class="sxs-lookup"><span data-stu-id="aa3d6-303">Rebuild initramfs:</span></span>

    ```bash
    dracut -f -v
    ```

<span data-ttu-id="aa3d6-304">For more information, see [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-304">For more information, see [rebuilding initramfs](https://access.redhat.com/solutions/1958).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa3d6-305">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa3d6-305">Next steps</span></span>

<span data-ttu-id="aa3d6-306">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="aa3d6-306">You're now ready to use your Red Hat Enterprise Linux virtual hard disk to create new virtual machines in Azure Stack.</span></span> <span data-ttu-id="aa3d6-307">If this is the first time that you're uploading the VHD file to Azure Stack, see [Use the Marketplace toolkit to create and publish marketplace items](azure-stack-marketplace-publisher.md).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-307">If this is the first time that you're uploading the VHD file to Azure Stack, see [Use the Marketplace toolkit to create and publish marketplace items](azure-stack-marketplace-publisher.md).</span></span>

<span data-ttu-id="aa3d6-308">For more information about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span><span class="sxs-lookup"><span data-stu-id="aa3d6-308">For more information about the hypervisors that are certified to run Red Hat Enterprise Linux, see [the Red Hat website](https://access.redhat.com/certified-hypervisors).</span></span>
