---
title: Azure Linux VM Agent Overview | Microsoft Docs
description: Learn how to install and configure Linux Agent (waagent) to manage your virtual machine's interaction with Azure Fabric Controller.
services: virtual-machines-linux
documentationcenter: ''
author: szarkos
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: e41de979-6d56-40b0-8916-895bf215ded6
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: szark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 405b24e3b44ad7b03df2d56f0a43d44c516c63f8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552744"
---
# <a name="understanding-and-using-the-azure-linux-agent"></a><span data-ttu-id="61404-103">Understanding and using the Azure Linux Agent</span><span class="sxs-lookup"><span data-stu-id="61404-103">Understanding and using the Azure Linux Agent</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a><span data-ttu-id="61404-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="61404-104">Introduction</span></span>
<span data-ttu-id="61404-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span><span class="sxs-lookup"><span data-stu-id="61404-105">The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller.</span></span> <span data-ttu-id="61404-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span><span class="sxs-lookup"><span data-stu-id="61404-106">It provides the following functionality for Linux and FreeBSD IaaS deployments:</span></span>

> [!NOTE]
> <span data-ttu-id="61404-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span><span class="sxs-lookup"><span data-stu-id="61404-107">See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.</span></span>
> 
> 

* <span data-ttu-id="61404-108">**Image Provisioning**</span><span class="sxs-lookup"><span data-stu-id="61404-108">**Image Provisioning**</span></span>
  
  * <span data-ttu-id="61404-109">Creation of a user account</span><span class="sxs-lookup"><span data-stu-id="61404-109">Creation of a user account</span></span>
  * <span data-ttu-id="61404-110">Configuring SSH authentication types</span><span class="sxs-lookup"><span data-stu-id="61404-110">Configuring SSH authentication types</span></span>
  * <span data-ttu-id="61404-111">Deployment of SSH public keys and key pairs</span><span class="sxs-lookup"><span data-stu-id="61404-111">Deployment of SSH public keys and key pairs</span></span>
  * <span data-ttu-id="61404-112">Setting the host name</span><span class="sxs-lookup"><span data-stu-id="61404-112">Setting the host name</span></span>
  * <span data-ttu-id="61404-113">Publishing the host name to the platform DNS</span><span class="sxs-lookup"><span data-stu-id="61404-113">Publishing the host name to the platform DNS</span></span>
  * <span data-ttu-id="61404-114">Reporting SSH host key fingerprint to the platform</span><span class="sxs-lookup"><span data-stu-id="61404-114">Reporting SSH host key fingerprint to the platform</span></span>
  * <span data-ttu-id="61404-115">Resource Disk Management</span><span class="sxs-lookup"><span data-stu-id="61404-115">Resource Disk Management</span></span>
  * <span data-ttu-id="61404-116">Formatting and mounting the resource disk</span><span class="sxs-lookup"><span data-stu-id="61404-116">Formatting and mounting the resource disk</span></span>
  * <span data-ttu-id="61404-117">Configuring swap space</span><span class="sxs-lookup"><span data-stu-id="61404-117">Configuring swap space</span></span>
* <span data-ttu-id="61404-118">**Networking**</span><span class="sxs-lookup"><span data-stu-id="61404-118">**Networking**</span></span>
  
  * <span data-ttu-id="61404-119">Manages routes to improve compatibility with platform DHCP servers</span><span class="sxs-lookup"><span data-stu-id="61404-119">Manages routes to improve compatibility with platform DHCP servers</span></span>
  * <span data-ttu-id="61404-120">Ensures the stability of the network interface name</span><span class="sxs-lookup"><span data-stu-id="61404-120">Ensures the stability of the network interface name</span></span>
* <span data-ttu-id="61404-121">**Kernel**</span><span class="sxs-lookup"><span data-stu-id="61404-121">**Kernel**</span></span>
  
  * <span data-ttu-id="61404-122">Configures virtual NUMA (disable for kernel <2.6.37)</span><span class="sxs-lookup"><span data-stu-id="61404-122">Configures virtual NUMA (disable for kernel <2.6.37)</span></span>
  * <span data-ttu-id="61404-123">Consumes Hyper-V entropy for /dev/random</span><span class="sxs-lookup"><span data-stu-id="61404-123">Consumes Hyper-V entropy for /dev/random</span></span>
  * <span data-ttu-id="61404-124">Configures SCSI timeouts for the root device (which could be remote)</span><span class="sxs-lookup"><span data-stu-id="61404-124">Configures SCSI timeouts for the root device (which could be remote)</span></span>
* <span data-ttu-id="61404-125">**Diagnostics**</span><span class="sxs-lookup"><span data-stu-id="61404-125">**Diagnostics**</span></span>
  
  * <span data-ttu-id="61404-126">Console redirection to the serial port</span><span class="sxs-lookup"><span data-stu-id="61404-126">Console redirection to the serial port</span></span>
* <span data-ttu-id="61404-127">**SCVMM Deployments**</span><span class="sxs-lookup"><span data-stu-id="61404-127">**SCVMM Deployments**</span></span>
  
  * <span data-ttu-id="61404-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span><span class="sxs-lookup"><span data-stu-id="61404-128">Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment</span></span>
* <span data-ttu-id="61404-129">**VM Extension**</span><span class="sxs-lookup"><span data-stu-id="61404-129">**VM Extension**</span></span>
  
  * <span data-ttu-id="61404-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span><span class="sxs-lookup"><span data-stu-id="61404-130">Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation</span></span>
  * <span data-ttu-id="61404-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span><span class="sxs-lookup"><span data-stu-id="61404-131">VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)</span></span>

## <a name="communication"></a><span data-ttu-id="61404-132">Communication</span><span class="sxs-lookup"><span data-stu-id="61404-132">Communication</span></span>
<span data-ttu-id="61404-133">The information flow from the platform to the agent occurs via two channels:</span><span class="sxs-lookup"><span data-stu-id="61404-133">The information flow from the platform to the agent occurs via two channels:</span></span>

* <span data-ttu-id="61404-134">A boot-time attached DVD for IaaS deployments.</span><span class="sxs-lookup"><span data-stu-id="61404-134">A boot-time attached DVD for IaaS deployments.</span></span> <span data-ttu-id="61404-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span><span class="sxs-lookup"><span data-stu-id="61404-135">This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.</span></span>
* <span data-ttu-id="61404-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span><span class="sxs-lookup"><span data-stu-id="61404-136">A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.</span></span>

## <a name="requirements"></a><span data-ttu-id="61404-137">Requirements</span><span class="sxs-lookup"><span data-stu-id="61404-137">Requirements</span></span>
<span data-ttu-id="61404-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span><span class="sxs-lookup"><span data-stu-id="61404-138">The following systems have been tested and are known to work with the Azure Linux Agent:</span></span>

> [!NOTE]
> <span data-ttu-id="61404-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span><span class="sxs-lookup"><span data-stu-id="61404-139">This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)</span></span>
> 
> 

* <span data-ttu-id="61404-140">CoreOS</span><span class="sxs-lookup"><span data-stu-id="61404-140">CoreOS</span></span>
* <span data-ttu-id="61404-141">CentOS 6.3+</span><span class="sxs-lookup"><span data-stu-id="61404-141">CentOS 6.3+</span></span>
* <span data-ttu-id="61404-142">Red Hat Enterprise Linux 6.7+</span><span class="sxs-lookup"><span data-stu-id="61404-142">Red Hat Enterprise Linux 6.7+</span></span>
* <span data-ttu-id="61404-143">Debian 7.0+</span><span class="sxs-lookup"><span data-stu-id="61404-143">Debian 7.0+</span></span>
* <span data-ttu-id="61404-144">Ubuntu 12.04+</span><span class="sxs-lookup"><span data-stu-id="61404-144">Ubuntu 12.04+</span></span>
* <span data-ttu-id="61404-145">openSUSE 12.3+</span><span class="sxs-lookup"><span data-stu-id="61404-145">openSUSE 12.3+</span></span>
* <span data-ttu-id="61404-146">SLES 11 SP3+</span><span class="sxs-lookup"><span data-stu-id="61404-146">SLES 11 SP3+</span></span>
* <span data-ttu-id="61404-147">Oracle Linux 6.4+</span><span class="sxs-lookup"><span data-stu-id="61404-147">Oracle Linux 6.4+</span></span>

<span data-ttu-id="61404-148">Other Supported Systems:</span><span class="sxs-lookup"><span data-stu-id="61404-148">Other Supported Systems:</span></span>

* <span data-ttu-id="61404-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span><span class="sxs-lookup"><span data-stu-id="61404-149">FreeBSD 10+ (Azure Linux Agent v2.0.10+)</span></span>

<span data-ttu-id="61404-150">The Linux agent depends on some system packages in order to function properly:</span><span class="sxs-lookup"><span data-stu-id="61404-150">The Linux agent depends on some system packages in order to function properly:</span></span>

* <span data-ttu-id="61404-151">Python 2.6+</span><span class="sxs-lookup"><span data-stu-id="61404-151">Python 2.6+</span></span>
* <span data-ttu-id="61404-152">OpenSSL 1.0+</span><span class="sxs-lookup"><span data-stu-id="61404-152">OpenSSL 1.0+</span></span>
* <span data-ttu-id="61404-153">OpenSSH 5.3+</span><span class="sxs-lookup"><span data-stu-id="61404-153">OpenSSH 5.3+</span></span>
* <span data-ttu-id="61404-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span><span class="sxs-lookup"><span data-stu-id="61404-154">Filesystem utilities: sfdisk, fdisk, mkfs, parted</span></span>
* <span data-ttu-id="61404-155">Password tools: chpasswd, sudo</span><span class="sxs-lookup"><span data-stu-id="61404-155">Password tools: chpasswd, sudo</span></span>
* <span data-ttu-id="61404-156">Text processing tools: sed, grep</span><span class="sxs-lookup"><span data-stu-id="61404-156">Text processing tools: sed, grep</span></span>
* <span data-ttu-id="61404-157">Network tools: ip-route</span><span class="sxs-lookup"><span data-stu-id="61404-157">Network tools: ip-route</span></span>
* <span data-ttu-id="61404-158">Kernel support for mounting UDF filesystems.</span><span class="sxs-lookup"><span data-stu-id="61404-158">Kernel support for mounting UDF filesystems.</span></span>

## <a name="installation"></a><span data-ttu-id="61404-159">Installation</span><span class="sxs-lookup"><span data-stu-id="61404-159">Installation</span></span>
<span data-ttu-id="61404-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="61404-160">Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent.</span></span> <span data-ttu-id="61404-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span><span class="sxs-lookup"><span data-stu-id="61404-161">All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.</span></span>

<span data-ttu-id="61404-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span><span class="sxs-lookup"><span data-stu-id="61404-162">Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.</span></span>

## <a name="command-line-options"></a><span data-ttu-id="61404-163">Command Line Options</span><span class="sxs-lookup"><span data-stu-id="61404-163">Command Line Options</span></span>
### <a name="flags"></a><span data-ttu-id="61404-164">Flags</span><span class="sxs-lookup"><span data-stu-id="61404-164">Flags</span></span>
* <span data-ttu-id="61404-165">verbose: Increase verbosity of specified command</span><span class="sxs-lookup"><span data-stu-id="61404-165">verbose: Increase verbosity of specified command</span></span>
* <span data-ttu-id="61404-166">force: Skip interactive confirmation for some commands</span><span class="sxs-lookup"><span data-stu-id="61404-166">force: Skip interactive confirmation for some commands</span></span>

### <a name="commands"></a><span data-ttu-id="61404-167">Commands</span><span class="sxs-lookup"><span data-stu-id="61404-167">Commands</span></span>
* <span data-ttu-id="61404-168">help: Lists the supported commands and flags.</span><span class="sxs-lookup"><span data-stu-id="61404-168">help: Lists the supported commands and flags.</span></span>
* <span data-ttu-id="61404-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span><span class="sxs-lookup"><span data-stu-id="61404-169">deprovision: Attempt to clean the system and make it suitable for re-provisioning.</span></span> <span data-ttu-id="61404-170">This operation deleted the following:</span><span class="sxs-lookup"><span data-stu-id="61404-170">This operation deleted the following:</span></span>
  
  * <span data-ttu-id="61404-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span><span class="sxs-lookup"><span data-stu-id="61404-171">All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="61404-172">Nameserver configuration in /etc/resolv.conf</span><span class="sxs-lookup"><span data-stu-id="61404-172">Nameserver configuration in /etc/resolv.conf</span></span>
  * <span data-ttu-id="61404-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span><span class="sxs-lookup"><span data-stu-id="61404-173">Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)</span></span>
  * <span data-ttu-id="61404-174">Cached DHCP client leases</span><span class="sxs-lookup"><span data-stu-id="61404-174">Cached DHCP client leases</span></span>
  * <span data-ttu-id="61404-175">Resets host name to localhost.localdomain</span><span class="sxs-lookup"><span data-stu-id="61404-175">Resets host name to localhost.localdomain</span></span>

> [!WARNING]
> <span data-ttu-id="61404-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span><span class="sxs-lookup"><span data-stu-id="61404-176">Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.</span></span>
> 
> 

* <span data-ttu-id="61404-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span><span class="sxs-lookup"><span data-stu-id="61404-177">deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data.</span></span> <span data-ttu-id="61404-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span><span class="sxs-lookup"><span data-stu-id="61404-178">This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.</span></span>
* <span data-ttu-id="61404-179">version: Displays the version of waagent</span><span class="sxs-lookup"><span data-stu-id="61404-179">version: Displays the version of waagent</span></span>
* <span data-ttu-id="61404-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span><span class="sxs-lookup"><span data-stu-id="61404-180">serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console.</span></span> <span data-ttu-id="61404-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span><span class="sxs-lookup"><span data-stu-id="61404-181">This ensures that kernel bootup logs are sent to the serial port and made available for debugging.</span></span>
* <span data-ttu-id="61404-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span><span class="sxs-lookup"><span data-stu-id="61404-182">daemon: Run waagent as a daemon to manage interaction with the platform.</span></span> <span data-ttu-id="61404-183">This argument is specified to waagent in the waagent init script.</span><span class="sxs-lookup"><span data-stu-id="61404-183">This argument is specified to waagent in the waagent init script.</span></span>
* <span data-ttu-id="61404-184">start: Run waagent as a background process</span><span class="sxs-lookup"><span data-stu-id="61404-184">start: Run waagent as a background process</span></span>

## <a name="configuration"></a><span data-ttu-id="61404-185">Configuration</span><span class="sxs-lookup"><span data-stu-id="61404-185">Configuration</span></span>
<span data-ttu-id="61404-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span><span class="sxs-lookup"><span data-stu-id="61404-186">A configuration file (/etc/waagent.conf) controls the actions of waagent.</span></span> <span data-ttu-id="61404-187">A sample configuration file is shown below:</span><span class="sxs-lookup"><span data-stu-id="61404-187">A sample configuration file is shown below:</span></span>

    Provisioning.Enabled=y
    Provisioning.DeleteRootPassword=n
    Provisioning.RegenerateSshHostKeyPair=y
    Provisioning.SshHostKeyPairType=rsa
    Provisioning.MonitorHostName=y
    Provisioning.DecodeCustomData=n
    Provisioning.ExecuteCustomData=n
    Provisioning.PasswordCryptId=6
    Provisioning.PasswordCryptSaltLength=10
    ResourceDisk.Format=y
    ResourceDisk.Filesystem=ext4
    ResourceDisk.MountPoint=/mnt/resource
    ResourceDisk.MountOptions=None
    ResourceDisk.EnableSwap=n
    ResourceDisk.SwapSizeMB=0
    LBProbeResponder=y
    Logs.Verbose=n
    OS.RootDeviceScsiTimeout=300
    OS.OpensslPath=None
    HttpProxy.Host=None
    HttpProxy.Port=None

<span data-ttu-id="61404-188">The various configuration options are described in detail below.</span><span class="sxs-lookup"><span data-stu-id="61404-188">The various configuration options are described in detail below.</span></span> <span data-ttu-id="61404-189">Configuration options are of three types; Boolean, String or Integer.</span><span class="sxs-lookup"><span data-stu-id="61404-189">Configuration options are of three types; Boolean, String or Integer.</span></span> <span data-ttu-id="61404-190">The Boolean configuration options can be specified as "y" or "n".</span><span class="sxs-lookup"><span data-stu-id="61404-190">The Boolean configuration options can be specified as "y" or "n".</span></span> <span data-ttu-id="61404-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span><span class="sxs-lookup"><span data-stu-id="61404-191">The special keyword "None" may be used for some string type configuration entries as detailed below.</span></span>

<span data-ttu-id="61404-192">**Provisioning.Enabled:**</span><span class="sxs-lookup"><span data-stu-id="61404-192">**Provisioning.Enabled:**</span></span>  
<span data-ttu-id="61404-193">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-193">Type: Boolean</span></span>  
<span data-ttu-id="61404-194">Default: y</span><span class="sxs-lookup"><span data-stu-id="61404-194">Default: y</span></span>

<span data-ttu-id="61404-195">This allows the user to enable or disable the provisioning functionality in the agent.</span><span class="sxs-lookup"><span data-stu-id="61404-195">This allows the user to enable or disable the provisioning functionality in the agent.</span></span> <span data-ttu-id="61404-196">Valid values are "y" or "n".</span><span class="sxs-lookup"><span data-stu-id="61404-196">Valid values are "y" or "n".</span></span> <span data-ttu-id="61404-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span><span class="sxs-lookup"><span data-stu-id="61404-197">If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.</span></span>

> [!NOTE]
> <span data-ttu-id="61404-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span><span class="sxs-lookup"><span data-stu-id="61404-198">The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.</span></span>
> 
> 

<span data-ttu-id="61404-199">**Provisioning.DeleteRootPassword:**</span><span class="sxs-lookup"><span data-stu-id="61404-199">**Provisioning.DeleteRootPassword:**</span></span>  
<span data-ttu-id="61404-200">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-200">Type: Boolean</span></span>  
<span data-ttu-id="61404-201">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-201">Default: n</span></span>

<span data-ttu-id="61404-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="61404-202">If set, the root password in the /etc/shadow file is erased during the provisioning process.</span></span>

<span data-ttu-id="61404-203">**Provisioning.RegenerateSshHostKeyPair:**</span><span class="sxs-lookup"><span data-stu-id="61404-203">**Provisioning.RegenerateSshHostKeyPair:**</span></span>  
<span data-ttu-id="61404-204">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-204">Type: Boolean</span></span>  
<span data-ttu-id="61404-205">Default: y</span><span class="sxs-lookup"><span data-stu-id="61404-205">Default: y</span></span>

<span data-ttu-id="61404-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span><span class="sxs-lookup"><span data-stu-id="61404-206">If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/.</span></span> <span data-ttu-id="61404-207">And a single fresh key pair is generated.</span><span class="sxs-lookup"><span data-stu-id="61404-207">And a single fresh key pair is generated.</span></span>

<span data-ttu-id="61404-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span><span class="sxs-lookup"><span data-stu-id="61404-208">The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry.</span></span> <span data-ttu-id="61404-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span><span class="sxs-lookup"><span data-stu-id="61404-209">Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).</span></span>

<span data-ttu-id="61404-210">**Provisioning.SshHostKeyPairType:**</span><span class="sxs-lookup"><span data-stu-id="61404-210">**Provisioning.SshHostKeyPairType:**</span></span>  
<span data-ttu-id="61404-211">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-211">Type: String</span></span>  
<span data-ttu-id="61404-212">Default: rsa</span><span class="sxs-lookup"><span data-stu-id="61404-212">Default: rsa</span></span>

<span data-ttu-id="61404-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="61404-213">This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine.</span></span> <span data-ttu-id="61404-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="61404-214">The typically supported values are "rsa", "dsa" and "ecdsa".</span></span> <span data-ttu-id="61404-215">Note that "putty.exe" on Windows does not support "ecdsa".</span><span class="sxs-lookup"><span data-stu-id="61404-215">Note that "putty.exe" on Windows does not support "ecdsa".</span></span> <span data-ttu-id="61404-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span><span class="sxs-lookup"><span data-stu-id="61404-216">So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".</span></span>

<span data-ttu-id="61404-217">**Provisioning.MonitorHostName:**</span><span class="sxs-lookup"><span data-stu-id="61404-217">**Provisioning.MonitorHostName:**</span></span>  
<span data-ttu-id="61404-218">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-218">Type: Boolean</span></span>  
<span data-ttu-id="61404-219">Default: y</span><span class="sxs-lookup"><span data-stu-id="61404-219">Default: y</span></span>

<span data-ttu-id="61404-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span><span class="sxs-lookup"><span data-stu-id="61404-220">If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change.</span></span> <span data-ttu-id="61404-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="61404-221">In order to push the name change to the DNS servers, networking will be restarted in the virtual machine.</span></span> <span data-ttu-id="61404-222">This will result in brief loss of Internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="61404-222">This will result in brief loss of Internet connectivity.</span></span>

<span data-ttu-id="61404-223">**Provisioning.DecodeCustomData**</span><span class="sxs-lookup"><span data-stu-id="61404-223">**Provisioning.DecodeCustomData**</span></span>  
<span data-ttu-id="61404-224">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-224">Type: Boolean</span></span>  
<span data-ttu-id="61404-225">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-225">Default: n</span></span>

<span data-ttu-id="61404-226">If set, waagent will decode CustomData from Base64.</span><span class="sxs-lookup"><span data-stu-id="61404-226">If set, waagent will decode CustomData from Base64.</span></span>

<span data-ttu-id="61404-227">**Provisioning.ExecuteCustomData**</span><span class="sxs-lookup"><span data-stu-id="61404-227">**Provisioning.ExecuteCustomData**</span></span>  
<span data-ttu-id="61404-228">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-228">Type: Boolean</span></span>  
<span data-ttu-id="61404-229">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-229">Default: n</span></span>

<span data-ttu-id="61404-230">If set, waagent will execute CustomData after provisioning.</span><span class="sxs-lookup"><span data-stu-id="61404-230">If set, waagent will execute CustomData after provisioning.</span></span>

<span data-ttu-id="61404-231">**Provisioning.PasswordCryptId**</span><span class="sxs-lookup"><span data-stu-id="61404-231">**Provisioning.PasswordCryptId**</span></span>  
<span data-ttu-id="61404-232">Type:String</span><span class="sxs-lookup"><span data-stu-id="61404-232">Type:String</span></span>  
<span data-ttu-id="61404-233">Default:6</span><span class="sxs-lookup"><span data-stu-id="61404-233">Default:6</span></span>

<span data-ttu-id="61404-234">Algorithm used by crypt when generating password hash.</span><span class="sxs-lookup"><span data-stu-id="61404-234">Algorithm used by crypt when generating password hash.</span></span>  
 <span data-ttu-id="61404-235">1 - MD5</span><span class="sxs-lookup"><span data-stu-id="61404-235">1 - MD5</span></span>  
 <span data-ttu-id="61404-236">2a - Blowfish</span><span class="sxs-lookup"><span data-stu-id="61404-236">2a - Blowfish</span></span>  
 <span data-ttu-id="61404-237">5 - SHA-256</span><span class="sxs-lookup"><span data-stu-id="61404-237">5 - SHA-256</span></span>  
 <span data-ttu-id="61404-238">6 - SHA-512</span><span class="sxs-lookup"><span data-stu-id="61404-238">6 - SHA-512</span></span>  

<span data-ttu-id="61404-239">**Provisioning.PasswordCryptSaltLength**</span><span class="sxs-lookup"><span data-stu-id="61404-239">**Provisioning.PasswordCryptSaltLength**</span></span>  
<span data-ttu-id="61404-240">Type:String</span><span class="sxs-lookup"><span data-stu-id="61404-240">Type:String</span></span>  
<span data-ttu-id="61404-241">Default:10</span><span class="sxs-lookup"><span data-stu-id="61404-241">Default:10</span></span>

<span data-ttu-id="61404-242">Length of random salt used when generating password hash.</span><span class="sxs-lookup"><span data-stu-id="61404-242">Length of random salt used when generating password hash.</span></span>

<span data-ttu-id="61404-243">**ResourceDisk.Format:**</span><span class="sxs-lookup"><span data-stu-id="61404-243">**ResourceDisk.Format:**</span></span>  
<span data-ttu-id="61404-244">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-244">Type: Boolean</span></span>  
<span data-ttu-id="61404-245">Default: y</span><span class="sxs-lookup"><span data-stu-id="61404-245">Default: y</span></span>

<span data-ttu-id="61404-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span><span class="sxs-lookup"><span data-stu-id="61404-246">If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs".</span></span> <span data-ttu-id="61404-247">A single partition of type Linux (83) will be made available on the disk.</span><span class="sxs-lookup"><span data-stu-id="61404-247">A single partition of type Linux (83) will be made available on the disk.</span></span> <span data-ttu-id="61404-248">Note that this partition will not be formatted if it can be successfully mounted.</span><span class="sxs-lookup"><span data-stu-id="61404-248">Note that this partition will not be formatted if it can be successfully mounted.</span></span>

<span data-ttu-id="61404-249">**ResourceDisk.Filesystem:**</span><span class="sxs-lookup"><span data-stu-id="61404-249">**ResourceDisk.Filesystem:**</span></span>  
<span data-ttu-id="61404-250">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-250">Type: String</span></span>  
<span data-ttu-id="61404-251">Default: ext4</span><span class="sxs-lookup"><span data-stu-id="61404-251">Default: ext4</span></span>

<span data-ttu-id="61404-252">This specifies the filesystem type for the resource disk.</span><span class="sxs-lookup"><span data-stu-id="61404-252">This specifies the filesystem type for the resource disk.</span></span> <span data-ttu-id="61404-253">Supported values vary by Linux distribution.</span><span class="sxs-lookup"><span data-stu-id="61404-253">Supported values vary by Linux distribution.</span></span> <span data-ttu-id="61404-254">If the string is X, then mkfs.X should be present on the Linux image.</span><span class="sxs-lookup"><span data-stu-id="61404-254">If the string is X, then mkfs.X should be present on the Linux image.</span></span> <span data-ttu-id="61404-255">SLES 11 images should typically use 'ext3'.</span><span class="sxs-lookup"><span data-stu-id="61404-255">SLES 11 images should typically use 'ext3'.</span></span> <span data-ttu-id="61404-256">FreeBSD images should use 'ufs2' here.</span><span class="sxs-lookup"><span data-stu-id="61404-256">FreeBSD images should use 'ufs2' here.</span></span>

<span data-ttu-id="61404-257">**ResourceDisk.MountPoint:**</span><span class="sxs-lookup"><span data-stu-id="61404-257">**ResourceDisk.MountPoint:**</span></span>  
<span data-ttu-id="61404-258">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-258">Type: String</span></span>  
<span data-ttu-id="61404-259">Default: /mnt/resource</span><span class="sxs-lookup"><span data-stu-id="61404-259">Default: /mnt/resource</span></span> 

<span data-ttu-id="61404-260">This specifies the path at which the resource disk is mounted.</span><span class="sxs-lookup"><span data-stu-id="61404-260">This specifies the path at which the resource disk is mounted.</span></span> <span data-ttu-id="61404-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span><span class="sxs-lookup"><span data-stu-id="61404-261">Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.</span></span>

<span data-ttu-id="61404-262">**ResourceDisk.MountOptions**</span><span class="sxs-lookup"><span data-stu-id="61404-262">**ResourceDisk.MountOptions**</span></span>  
<span data-ttu-id="61404-263">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-263">Type: String</span></span>  
<span data-ttu-id="61404-264">Default: None</span><span class="sxs-lookup"><span data-stu-id="61404-264">Default: None</span></span>

<span data-ttu-id="61404-265">Specifies disk mount options to be passed to the mount -o command.</span><span class="sxs-lookup"><span data-stu-id="61404-265">Specifies disk mount options to be passed to the mount -o command.</span></span> <span data-ttu-id="61404-266">This is a comma separated list of values, ex.</span><span class="sxs-lookup"><span data-stu-id="61404-266">This is a comma separated list of values, ex.</span></span> <span data-ttu-id="61404-267">'nodev,nosuid'.</span><span class="sxs-lookup"><span data-stu-id="61404-267">'nodev,nosuid'.</span></span> <span data-ttu-id="61404-268">See mount(8) for details.</span><span class="sxs-lookup"><span data-stu-id="61404-268">See mount(8) for details.</span></span>

<span data-ttu-id="61404-269">**ResourceDisk.EnableSwap:**</span><span class="sxs-lookup"><span data-stu-id="61404-269">**ResourceDisk.EnableSwap:**</span></span>  
<span data-ttu-id="61404-270">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-270">Type: Boolean</span></span>  
<span data-ttu-id="61404-271">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-271">Default: n</span></span>

<span data-ttu-id="61404-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span><span class="sxs-lookup"><span data-stu-id="61404-272">If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.</span></span>

<span data-ttu-id="61404-273">**ResourceDisk.SwapSizeMB:**</span><span class="sxs-lookup"><span data-stu-id="61404-273">**ResourceDisk.SwapSizeMB:**</span></span>  
<span data-ttu-id="61404-274">Type: Integer</span><span class="sxs-lookup"><span data-stu-id="61404-274">Type: Integer</span></span>  
<span data-ttu-id="61404-275">Default: 0</span><span class="sxs-lookup"><span data-stu-id="61404-275">Default: 0</span></span>

<span data-ttu-id="61404-276">The size of the swap file in megabytes.</span><span class="sxs-lookup"><span data-stu-id="61404-276">The size of the swap file in megabytes.</span></span>

<span data-ttu-id="61404-277">**Logs.Verbose:**</span><span class="sxs-lookup"><span data-stu-id="61404-277">**Logs.Verbose:**</span></span>  
<span data-ttu-id="61404-278">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-278">Type: Boolean</span></span>  
<span data-ttu-id="61404-279">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-279">Default: n</span></span>

<span data-ttu-id="61404-280">If set, log verbosity is boosted.</span><span class="sxs-lookup"><span data-stu-id="61404-280">If set, log verbosity is boosted.</span></span> <span data-ttu-id="61404-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span><span class="sxs-lookup"><span data-stu-id="61404-281">Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.</span></span>

<span data-ttu-id="61404-282">**OS.EnableRDMA**</span><span class="sxs-lookup"><span data-stu-id="61404-282">**OS.EnableRDMA**</span></span>  
<span data-ttu-id="61404-283">Type: Boolean</span><span class="sxs-lookup"><span data-stu-id="61404-283">Type: Boolean</span></span>  
<span data-ttu-id="61404-284">Default: n</span><span class="sxs-lookup"><span data-stu-id="61404-284">Default: n</span></span>

<span data-ttu-id="61404-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span><span class="sxs-lookup"><span data-stu-id="61404-285">If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.</span></span>

<span data-ttu-id="61404-286">**OS.RootDeviceScsiTimeout:**</span><span class="sxs-lookup"><span data-stu-id="61404-286">**OS.RootDeviceScsiTimeout:**</span></span>  
<span data-ttu-id="61404-287">Type: Integer</span><span class="sxs-lookup"><span data-stu-id="61404-287">Type: Integer</span></span>  
<span data-ttu-id="61404-288">Default: 300</span><span class="sxs-lookup"><span data-stu-id="61404-288">Default: 300</span></span>

<span data-ttu-id="61404-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span><span class="sxs-lookup"><span data-stu-id="61404-289">This configures the SCSI timeout in seconds on the OS disk and data drives.</span></span> <span data-ttu-id="61404-290">If not set, the system defaults are used.</span><span class="sxs-lookup"><span data-stu-id="61404-290">If not set, the system defaults are used.</span></span>

<span data-ttu-id="61404-291">**OS.OpensslPath:**</span><span class="sxs-lookup"><span data-stu-id="61404-291">**OS.OpensslPath:**</span></span>  
<span data-ttu-id="61404-292">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-292">Type: String</span></span>  
<span data-ttu-id="61404-293">Default: None</span><span class="sxs-lookup"><span data-stu-id="61404-293">Default: None</span></span>

<span data-ttu-id="61404-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span><span class="sxs-lookup"><span data-stu-id="61404-294">This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.</span></span>

<span data-ttu-id="61404-295">**HttpProxy.Host, HttpProxy.Port**</span><span class="sxs-lookup"><span data-stu-id="61404-295">**HttpProxy.Host, HttpProxy.Port**</span></span>  
<span data-ttu-id="61404-296">Type: String</span><span class="sxs-lookup"><span data-stu-id="61404-296">Type: String</span></span>  
<span data-ttu-id="61404-297">Default: None</span><span class="sxs-lookup"><span data-stu-id="61404-297">Default: None</span></span>

<span data-ttu-id="61404-298">If set, the agent will use this proxy server to access the internet.</span><span class="sxs-lookup"><span data-stu-id="61404-298">If set, the agent will use this proxy server to access the internet.</span></span> 

## <a name="ubuntu-cloud-images"></a><span data-ttu-id="61404-299">Ubuntu Cloud Images</span><span class="sxs-lookup"><span data-stu-id="61404-299">Ubuntu Cloud Images</span></span>
<span data-ttu-id="61404-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span><span class="sxs-lookup"><span data-stu-id="61404-300">Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.</span></span>  <span data-ttu-id="61404-301">Please note the following differences:</span><span class="sxs-lookup"><span data-stu-id="61404-301">Please note the following differences:</span></span>

* <span data-ttu-id="61404-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span><span class="sxs-lookup"><span data-stu-id="61404-302">**Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.</span></span>
* <span data-ttu-id="61404-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span><span class="sxs-lookup"><span data-stu-id="61404-303">The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:</span></span>
  
  * <span data-ttu-id="61404-304">**ResourceDisk.Format**</span><span class="sxs-lookup"><span data-stu-id="61404-304">**ResourceDisk.Format**</span></span>
  * <span data-ttu-id="61404-305">**ResourceDisk.Filesystem**</span><span class="sxs-lookup"><span data-stu-id="61404-305">**ResourceDisk.Filesystem**</span></span>
  * <span data-ttu-id="61404-306">**ResourceDisk.MountPoint**</span><span class="sxs-lookup"><span data-stu-id="61404-306">**ResourceDisk.MountPoint**</span></span>
  * <span data-ttu-id="61404-307">**ResourceDisk.EnableSwap**</span><span class="sxs-lookup"><span data-stu-id="61404-307">**ResourceDisk.EnableSwap**</span></span>
  * <span data-ttu-id="61404-308">**ResourceDisk.SwapSizeMB**</span><span class="sxs-lookup"><span data-stu-id="61404-308">**ResourceDisk.SwapSizeMB**</span></span>
* <span data-ttu-id="61404-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span><span class="sxs-lookup"><span data-stu-id="61404-309">Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:</span></span>
  
  * [<span data-ttu-id="61404-310">Ubuntu Wiki: Configure Swap Partitions</span><span class="sxs-lookup"><span data-stu-id="61404-310">Ubuntu Wiki: Configure Swap Partitions</span></span>](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [<span data-ttu-id="61404-311">Injecting Custom Data into an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="61404-311">Injecting Custom Data into an Azure Virtual Machine</span></span>](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

