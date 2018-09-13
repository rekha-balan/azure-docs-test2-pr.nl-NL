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
# <a name="understanding-and-using-the-azure-linux-agent"></a>Understanding and using the Azure Linux Agent
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="introduction"></a>Introduction
The Microsoft Azure Linux Agent (waagent) manages Linux & FreeBSD provisioning, and VM interaction with the Azure Fabric Controller. It provides the following functionality for Linux and FreeBSD IaaS deployments:

> [!NOTE]
> See the Azure Linux agent [README](https://github.com/Azure/WALinuxAgent/blob/master/README.md) for additional details.
> 
> 

* **Image Provisioning**
  
  * Creation of a user account
  * Configuring SSH authentication types
  * Deployment of SSH public keys and key pairs
  * Setting the host name
  * Publishing the host name to the platform DNS
  * Reporting SSH host key fingerprint to the platform
  * Resource Disk Management
  * Formatting and mounting the resource disk
  * Configuring swap space
* **Networking**
  
  * Manages routes to improve compatibility with platform DHCP servers
  * Ensures the stability of the network interface name
* **Kernel**
  
  * Configures virtual NUMA (disable for kernel <2.6.37)
  * Consumes Hyper-V entropy for /dev/random
  * Configures SCSI timeouts for the root device (which could be remote)
* **Diagnostics**
  
  * Console redirection to the serial port
* **SCVMM Deployments**
  
  * Detects and bootstraps the VMM agent for Linux when running in a System Center Virtual Machine Manager 2012 R2 environment
* **VM Extension**
  
  * Inject component authored by Microsoft and Partners into Linux VM (IaaS) to enable software and configuration automation
  * VM Extension reference implementation on [https://github.com/Azure/azure-linux-extensions](https://github.com/Azure/azure-linux-extensions)

## <a name="communication"></a>Communication
The information flow from the platform to the agent occurs via two channels:

* A boot-time attached DVD for IaaS deployments. This DVD includes an OVF-compliant configuration file that includes all provisioning information other than the actual SSH keypairs.
* A TCP endpoint exposing a REST API used to obtain deployment and topology configuration.

## <a name="requirements"></a>Requirements
The following systems have been tested and are known to work with the Azure Linux Agent:

> [!NOTE]
> This list may differ from the official list of supported systems on the Microsoft Azure Platform, as described here: [http://support.microsoft.com/kb/2805216](http://support.microsoft.com/kb/2805216)
> 
> 

* CoreOS
* CentOS 6.3+
* Red Hat Enterprise Linux 6.7+
* Debian 7.0+
* Ubuntu 12.04+
* openSUSE 12.3+
* SLES 11 SP3+
* Oracle Linux 6.4+

Other Supported Systems:

* FreeBSD 10+ (Azure Linux Agent v2.0.10+)

The Linux agent depends on some system packages in order to function properly:

* Python 2.6+
* OpenSSL 1.0+
* OpenSSH 5.3+
* Filesystem utilities: sfdisk, fdisk, mkfs, parted
* Password tools: chpasswd, sudo
* Text processing tools: sed, grep
* Network tools: ip-route
* Kernel support for mounting UDF filesystems.

## <a name="installation"></a>Installation
Installation using an RPM or a DEB package from your distribution's package repository is the preferred method of installing and upgrading the Azure Linux Agent. All the [endorsed distribution providers](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) integrate the Azure Linux agent package into their images and repositories.

Refer to the documentation in the [Azure Linux Agent repo on GitHub](https://github.com/Azure/WALinuxAgent) for advanced installation options, such as installing from source or to custom locations or prefixes.

## <a name="command-line-options"></a>Command Line Options
### <a name="flags"></a>Flags
* verbose: Increase verbosity of specified command
* force: Skip interactive confirmation for some commands

### <a name="commands"></a>Commands
* help: Lists the supported commands and flags.
* deprovision: Attempt to clean the system and make it suitable for re-provisioning. This operation deleted the following:
  
  * All SSH host keys (if Provisioning.RegenerateSshHostKeyPair is 'y' in the configuration file)
  * Nameserver configuration in /etc/resolv.conf
  * Root password from /etc/shadow (if Provisioning.DeleteRootPassword is 'y' in the configuration file)
  * Cached DHCP client leases
  * Resets host name to localhost.localdomain

> [!WARNING]
> Deprovisioning does not guarantee that the image is cleared of all sensitive information and suitable for redistribution.
> 
> 

* deprovision+user: Performs everything under -deprovision (above) and also deletes the last provisioned user account (obtained from /var/lib/waagent) and associated data. This parameter is when de-provisioning an image that was previously provisioning on Azure so it may be captured and re-used.
* version: Displays the version of waagent
* serialconsole: Configures GRUB to mark ttyS0 (the first serial port) as the boot console. This ensures that kernel bootup logs are sent to the serial port and made available for debugging.
* daemon: Run waagent as a daemon to manage interaction with the platform. This argument is specified to waagent in the waagent init script.
* start: Run waagent as a background process

## <a name="configuration"></a>Configuration
A configuration file (/etc/waagent.conf) controls the actions of waagent. A sample configuration file is shown below:

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

The various configuration options are described in detail below. Configuration options are of three types; Boolean, String or Integer. The Boolean configuration options can be specified as "y" or "n". The special keyword "None" may be used for some string type configuration entries as detailed below.

**Provisioning.Enabled:**  
Type: Boolean  
Default: y

This allows the user to enable or disable the provisioning functionality in the agent. Valid values are "y" or "n". If provisioning is disabled, SSH host and user keys in the image are preserved and any configuration specified in the Azure provisioning API is ignored.

> [!NOTE]
> The `Provisioning.Enabled` parameter defaults to "n" on Ubuntu Cloud Images that use cloud-init for provisioning.
> 
> 

**Provisioning.DeleteRootPassword:**  
Type: Boolean  
Default: n

If set, the root password in the /etc/shadow file is erased during the provisioning process.

**Provisioning.RegenerateSshHostKeyPair:**  
Type: Boolean  
Default: y

If set, all SSH host key pairs (ecdsa, dsa and rsa) are deleted during the provisioning process from /etc/ssh/. And a single fresh key pair is generated.

The encryption type for the fresh key pair is configurable by the Provisioning.SshHostKeyPairType entry. Please note that some distributions will re-create SSH key pairs for any missing encryption types when the SSH daemon is restarted (for example, upon a reboot).

**Provisioning.SshHostKeyPairType:**  
Type: String  
Default: rsa

This can be set to an encryption algorithm type that is supported by the SSH daemon on the virtual machine. The typically supported values are "rsa", "dsa" and "ecdsa". Note that "putty.exe" on Windows does not support "ecdsa". So, if you intend to use putty.exe on Windows to connect to a Linux deployment, please use "rsa" or "dsa".

**Provisioning.MonitorHostName:**  
Type: Boolean  
Default: y

If set, waagent will monitor the Linux virtual machine for hostname changes (as returned by the "hostname" command) and automatically update the networking configuration in the image to reflect the change. In order to push the name change to the DNS servers, networking will be restarted in the virtual machine. This will result in brief loss of Internet connectivity.

**Provisioning.DecodeCustomData**  
Type: Boolean  
Default: n

If set, waagent will decode CustomData from Base64.

**Provisioning.ExecuteCustomData**  
Type: Boolean  
Default: n

If set, waagent will execute CustomData after provisioning.

**Provisioning.PasswordCryptId**  
Type:String  
Default:6

Algorithm used by crypt when generating password hash.  
 1 - MD5  
 2a - Blowfish  
 5 - SHA-256  
 6 - SHA-512  

**Provisioning.PasswordCryptSaltLength**  
Type:String  
Default:10

Length of random salt used when generating password hash.

**ResourceDisk.Format:**  
Type: Boolean  
Default: y

If set, the resource disk provided by the platform will be formatted and mounted by waagent if the filesystem type requested by the user in "ResourceDisk.Filesystem" is anything other than "ntfs". A single partition of type Linux (83) will be made available on the disk. Note that this partition will not be formatted if it can be successfully mounted.

**ResourceDisk.Filesystem:**  
Type: String  
Default: ext4

This specifies the filesystem type for the resource disk. Supported values vary by Linux distribution. If the string is X, then mkfs.X should be present on the Linux image. SLES 11 images should typically use 'ext3'. FreeBSD images should use 'ufs2' here.

**ResourceDisk.MountPoint:**  
Type: String  
Default: /mnt/resource 

This specifies the path at which the resource disk is mounted. Note that the resource disk is a *temporary* disk, and might be emptied when the VM is deprovisioned.

**ResourceDisk.MountOptions**  
Type: String  
Default: None

Specifies disk mount options to be passed to the mount -o command. This is a comma separated list of values, ex. 'nodev,nosuid'. See mount(8) for details.

**ResourceDisk.EnableSwap:**  
Type: Boolean  
Default: n

If set, a swap file (/swapfile) is created on the resource disk and added to the system swap space.

**ResourceDisk.SwapSizeMB:**  
Type: Integer  
Default: 0

The size of the swap file in megabytes.

**Logs.Verbose:**  
Type: Boolean  
Default: n

If set, log verbosity is boosted. Waagent logs to /var/log/waagent.log and leverages the system logrotate functionality to rotate logs.

**OS.EnableRDMA**  
Type: Boolean  
Default: n

If set, the agent will attempt to install and then load an RDMA kernel driver that matches the version of the firmware on the underlying hardware.

**OS.RootDeviceScsiTimeout:**  
Type: Integer  
Default: 300

This configures the SCSI timeout in seconds on the OS disk and data drives. If not set, the system defaults are used.

**OS.OpensslPath:**  
Type: String  
Default: None

This can be used to specify an alternate path for the openssl binary to use for cryptographic operations.

**HttpProxy.Host, HttpProxy.Port**  
Type: String  
Default: None

If set, the agent will use this proxy server to access the internet. 

## <a name="ubuntu-cloud-images"></a>Ubuntu Cloud Images
Note that Ubuntu Cloud Images utilize [cloud-init](https://launchpad.net/ubuntu/+source/cloud-init) to perform many configuration tasks that would otherwise be managed by the Azure Linux Agent.  Please note the following differences:

* **Provisioning.Enabled** defaults to "n" on Ubuntu Cloud Images that use cloud-init to perform provisioning tasks.
* The following configuration parameters have no effect on Ubuntu Cloud Images that use cloud-init to manage the resource disk and swap space:
  
  * **ResourceDisk.Format**
  * **ResourceDisk.Filesystem**
  * **ResourceDisk.MountPoint**
  * **ResourceDisk.EnableSwap**
  * **ResourceDisk.SwapSizeMB**
* Please see the following resources to configure the resource disk mount point and swap space on Ubuntu Cloud Images during provisioning:
  
  * [Ubuntu Wiki: Configure Swap Partitions](http://go.microsoft.com/fwlink/?LinkID=532955&clcid=0x409)
  * [Injecting Custom Data into an Azure Virtual Machine](../windows/classic/inject-custom-data.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

