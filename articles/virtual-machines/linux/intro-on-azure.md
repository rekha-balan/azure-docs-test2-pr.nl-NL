---
title: Introduction to Linux in Azure | Microsoft Docs
description: Learn about using Linux virtual machines on Azure.
services: virtual-machines-linux
documentationcenter: python
author: szarkos
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: b13bf305-87bf-4df3-815e-e8f6337aa6ea
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: a7a8394f220073f0004a83ff253c5fd3a79226d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550847"
---
# <a name="introduction-to-linux-on-azure"></a><span data-ttu-id="28bc0-103">Introduction to Linux on Azure</span><span class="sxs-lookup"><span data-stu-id="28bc0-103">Introduction to Linux on Azure</span></span>
<span data-ttu-id="28bc0-104">This topic provides an overview of some aspects of using Linux virtual machines in the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="28bc0-104">This topic provides an overview of some aspects of using Linux virtual machines in the Azure cloud.</span></span> <span data-ttu-id="28bc0-105">Deploying a Linux virtual machine is a straightforward process using an image from the gallery.</span><span class="sxs-lookup"><span data-stu-id="28bc0-105">Deploying a Linux virtual machine is a straightforward process using an image from the gallery.</span></span>

## <a name="authentication-usernames-passwords-and-ssh-keys"></a><span data-ttu-id="28bc0-106">Authentication: Usernames, Passwords and SSH Keys</span><span class="sxs-lookup"><span data-stu-id="28bc0-106">Authentication: Usernames, Passwords and SSH Keys</span></span>
<span data-ttu-id="28bc0-107">When creating a Linux virtual machine using the Azure classic portal, you are asked to provide a username, password or an SSH public key.</span><span class="sxs-lookup"><span data-stu-id="28bc0-107">When creating a Linux virtual machine using the Azure classic portal, you are asked to provide a username, password or an SSH public key.</span></span> <span data-ttu-id="28bc0-108">The choice of a username for deploying a Linux virtual machine on Azure is subject to the following constraint: names of system accounts (UID <100) already present in the virtual machine are not allowed, 'root' for example.</span><span class="sxs-lookup"><span data-stu-id="28bc0-108">The choice of a username for deploying a Linux virtual machine on Azure is subject to the following constraint: names of system accounts (UID <100) already present in the virtual machine are not allowed, 'root' for example.</span></span>

* <span data-ttu-id="28bc0-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-109">See [Create a Virtual Machine Running Linux](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
* <span data-ttu-id="28bc0-110">See [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-110">See [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="obtaining-superuser-privileges-using-sudo"></a><span data-ttu-id="28bc0-111">Obtaining Superuser Privileges Using `sudo`</span><span class="sxs-lookup"><span data-stu-id="28bc0-111">Obtaining Superuser Privileges Using `sudo`</span></span>
<span data-ttu-id="28bc0-112">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span><span class="sxs-lookup"><span data-stu-id="28bc0-112">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="28bc0-113">This account is configured by the Azure Linux Agent to be able to elevate privileges to root (superuser account) using the `sudo` utility.</span><span class="sxs-lookup"><span data-stu-id="28bc0-113">This account is configured by the Azure Linux Agent to be able to elevate privileges to root (superuser account) using the `sudo` utility.</span></span> <span data-ttu-id="28bc0-114">Once logged in using this user account, you will be able to run commands as root using the command syntax</span><span class="sxs-lookup"><span data-stu-id="28bc0-114">Once logged in using this user account, you will be able to run commands as root using the command syntax</span></span>

    # sudo <COMMAND>

<span data-ttu-id="28bc0-115">You can optionally obtain a root shell using **sudo -s**.</span><span class="sxs-lookup"><span data-stu-id="28bc0-115">You can optionally obtain a root shell using **sudo -s**.</span></span>

* <span data-ttu-id="28bc0-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-116">See [Using root privileges on Linux virtual machines in Azure](use-root-privileges.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="firewall-configuration"></a><span data-ttu-id="28bc0-117">Firewall Configuration</span><span class="sxs-lookup"><span data-stu-id="28bc0-117">Firewall Configuration</span></span>
<span data-ttu-id="28bc0-118">Azure provides an inbound packet filter that restricts connectivity to ports specified in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="28bc0-118">Azure provides an inbound packet filter that restricts connectivity to ports specified in the Azure classic portal.</span></span> <span data-ttu-id="28bc0-119">By default, the only allowed port is SSH.</span><span class="sxs-lookup"><span data-stu-id="28bc0-119">By default, the only allowed port is SSH.</span></span> <span data-ttu-id="28bc0-120">You may open up access to additional ports on your Linux virtual machine by configuring endpoints in the Azure classic portal:</span><span class="sxs-lookup"><span data-stu-id="28bc0-120">You may open up access to additional ports on your Linux virtual machine by configuring endpoints in the Azure classic portal:</span></span>

* <span data-ttu-id="28bc0-121">See: [How to Set Up Endpoints to a Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-121">See: [How to Set Up Endpoints to a Virtual Machine](../windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="28bc0-122">The Linux images in the Azure Gallery do not enable the *iptables* firewall by default.</span><span class="sxs-lookup"><span data-stu-id="28bc0-122">The Linux images in the Azure Gallery do not enable the *iptables* firewall by default.</span></span> <span data-ttu-id="28bc0-123">If desired, the firewall may be configured to provide additional filtering.</span><span class="sxs-lookup"><span data-stu-id="28bc0-123">If desired, the firewall may be configured to provide additional filtering.</span></span>

## <a name="hostname-changes"></a><span data-ttu-id="28bc0-124">Hostname Changes</span><span class="sxs-lookup"><span data-stu-id="28bc0-124">Hostname Changes</span></span>
<span data-ttu-id="28bc0-125">When you initially deploy an instance of a Linux image, you are required to provide a host name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="28bc0-125">When you initially deploy an instance of a Linux image, you are required to provide a host name for the virtual machine.</span></span> <span data-ttu-id="28bc0-126">Once the virtual machine is running, this hostname is published to the platform DNS servers so that multiple virtual machines connected to each other can perform IP address lookups using hostnames.</span><span class="sxs-lookup"><span data-stu-id="28bc0-126">Once the virtual machine is running, this hostname is published to the platform DNS servers so that multiple virtual machines connected to each other can perform IP address lookups using hostnames.</span></span>

<span data-ttu-id="28bc0-127">If hostname changes are desired after a virtual machine has been deployed, please use the command</span><span class="sxs-lookup"><span data-stu-id="28bc0-127">If hostname changes are desired after a virtual machine has been deployed, please use the command</span></span>

    # sudo hostname <newname>

<span data-ttu-id="28bc0-128">The Azure Linux Agent includes functionality to automatically detect this name change and appropriately configure the virtual machine to persist this change and publish this change to the platform DNS servers.</span><span class="sxs-lookup"><span data-stu-id="28bc0-128">The Azure Linux Agent includes functionality to automatically detect this name change and appropriately configure the virtual machine to persist this change and publish this change to the platform DNS servers.</span></span>

* [<span data-ttu-id="28bc0-129">Azure Linux Agent User Guide</span><span class="sxs-lookup"><span data-stu-id="28bc0-129">Azure Linux Agent User Guide</span></span>](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="cloud-init"></a><span data-ttu-id="28bc0-130">Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="28bc0-130">Cloud-Init</span></span>
<span data-ttu-id="28bc0-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="28bc0-131">**Ubuntu** and **CoreOS** images utilize cloud-init on Azure, which provides additional capabilities for bootstrapping a virtual machine.</span></span>

* [<span data-ttu-id="28bc0-132">How to Inject Custom Data</span><span class="sxs-lookup"><span data-stu-id="28bc0-132">How to Inject Custom Data</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="28bc0-133">Custom Data and Cloud-Init on Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="28bc0-133">Custom Data and Cloud-Init on Microsoft Azure</span></span>](https://azure.microsoft.com/blog/2014/04/21/custom-data-and-cloud-init-on-windows-azure/)
* [<span data-ttu-id="28bc0-134">Create Azure Swap Partitions Using Cloud-Init</span><span class="sxs-lookup"><span data-stu-id="28bc0-134">Create Azure Swap Partitions Using Cloud-Init</span></span>](https://wiki.ubuntu.com/AzureSwapPartitions)
* [<span data-ttu-id="28bc0-135">How to Use CoreOS on Azure</span><span class="sxs-lookup"><span data-stu-id="28bc0-135">How to Use CoreOS on Azure</span></span>](https://coreos.com/os/docs/latest/booting-on-azure.html)

## <a name="virtual-machine-image-capture"></a><span data-ttu-id="28bc0-136">Virtual Machine Image Capture</span><span class="sxs-lookup"><span data-stu-id="28bc0-136">Virtual Machine Image Capture</span></span>
<span data-ttu-id="28bc0-137">Azure provides the ability to capture the state of an existing virtual machine into an image that can subsequently be used to deploy additional virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="28bc0-137">Azure provides the ability to capture the state of an existing virtual machine into an image that can subsequently be used to deploy additional virtual machine instances.</span></span> <span data-ttu-id="28bc0-138">The Azure Linux Agent may be used to rollback some of the customization that was performed during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="28bc0-138">The Azure Linux Agent may be used to rollback some of the customization that was performed during the provisioning process.</span></span> <span data-ttu-id="28bc0-139">You may follow the steps below to capture a virtual machine as an image:</span><span class="sxs-lookup"><span data-stu-id="28bc0-139">You may follow the steps below to capture a virtual machine as an image:</span></span>

1. <span data-ttu-id="28bc0-140">Run **waagent -deprovision** to undo provisioning customization.</span><span class="sxs-lookup"><span data-stu-id="28bc0-140">Run **waagent -deprovision** to undo provisioning customization.</span></span> <span data-ttu-id="28bc0-141">Or **waagent -deprovision+user** to optionally, delete the user account specified during provisioning and all associated data.</span><span class="sxs-lookup"><span data-stu-id="28bc0-141">Or **waagent -deprovision+user** to optionally, delete the user account specified during provisioning and all associated data.</span></span>
2. <span data-ttu-id="28bc0-142">Shut down/power off the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="28bc0-142">Shut down/power off the virtual machine.</span></span>
3. <span data-ttu-id="28bc0-143">Click *Capture* in the Azure classic portal or use the Powershell or CLI tools to capture the virtual machine as an image.</span><span class="sxs-lookup"><span data-stu-id="28bc0-143">Click *Capture* in the Azure classic portal or use the Powershell or CLI tools to capture the virtual machine as an image.</span></span>
   
   * <span data-ttu-id="28bc0-144">See: [How to Capture a Linux Virtual Machine to Use as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-144">See: [How to Capture a Linux Virtual Machine to Use as a Template](classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

## <a name="attaching-disks"></a><span data-ttu-id="28bc0-145">Attaching Disks</span><span class="sxs-lookup"><span data-stu-id="28bc0-145">Attaching Disks</span></span>
<span data-ttu-id="28bc0-146">Each virtual machine has a temporary, local *resource disk* attached.</span><span class="sxs-lookup"><span data-stu-id="28bc0-146">Each virtual machine has a temporary, local *resource disk* attached.</span></span> <span data-ttu-id="28bc0-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in the virtual machine for transient and **temporary** storage of data.</span><span class="sxs-lookup"><span data-stu-id="28bc0-147">Because data on a resource disk may not be durable across reboots, it is often used by applications and processes running in the virtual machine for transient and **temporary** storage of data.</span></span> <span data-ttu-id="28bc0-148">It is also used to store the page or swap files for the operating system.</span><span class="sxs-lookup"><span data-stu-id="28bc0-148">It is also used to store the page or swap files for the operating system.</span></span>

<span data-ttu-id="28bc0-149">On Linux, the resource disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span><span class="sxs-lookup"><span data-stu-id="28bc0-149">On Linux, the resource disk is typically managed by the Azure Linux Agent and automatically mounted to **/mnt/resource** (or **/mnt** on Ubuntu images).</span></span>

> [!NOTE]
> <span data-ttu-id="28bc0-150">Note that the resource disk is a **temporary** disk, and might be deleted and reformatted when the VM is rebooted.</span><span class="sxs-lookup"><span data-stu-id="28bc0-150">Note that the resource disk is a **temporary** disk, and might be deleted and reformatted when the VM is rebooted.</span></span>
> 
> 

<span data-ttu-id="28bc0-151">On Linux the data disk might be named by the kernel as `/dev/sdc`, and users will need to partition, format and mount that resource.</span><span class="sxs-lookup"><span data-stu-id="28bc0-151">On Linux the data disk might be named by the kernel as `/dev/sdc`, and users will need to partition, format and mount that resource.</span></span> <span data-ttu-id="28bc0-152">This is covered step-by-step in the tutorial: [How to Attach a Data Disk to a Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="28bc0-152">This is covered step-by-step in the tutorial: [How to Attach a Data Disk to a Virtual Machine](../windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

* <span data-ttu-id="28bc0-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="28bc0-153">**See also:** [Configure Software RAID on Linux](configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) & [Configure LVM on a Linux VM in Azure](configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

