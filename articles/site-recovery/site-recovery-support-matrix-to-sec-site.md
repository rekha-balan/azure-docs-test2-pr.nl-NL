---
title: Support matrix for replication to a secondary site with Azure Site Recovery | Microsoft Docs
description: Summarizes the supported operating systems and components for Azure Site Recovery
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: jwhit
editor: ''
ms.assetid: ''
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/08/2017
ms.author: raynew
ms.openlocfilehash: d53d4cfdc7b673d2816fa9372dedbed540380cce
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549660"
---
# <a name="support-matrix-for-replication-to-a-secondary-site-with-azure-site-recovery"></a>Support matrix for replication to a secondary site with Azure Site Recovery

> [!div class="op_single_selector"]
> * [Replicate to Azure](site-recovery-support-matrix-to-azure.md)
> * [Replicate to an on-premises location](site-recovery-support-matrix-to-sec-site.md)

This article summarizes what's supported when you use Azure Site Recovery to replicate to a secondary on-premises site.

## <a name="deployment-options"></a>Deployment options

**Deployment** | **VMware/physical server** | **Hyper-V (with/without SCVMM)
--- | --- | --- | ---
**Azure portal** | On-premises VMware VMs to secondary VMware site.<br/><br/> Download the [InMage Scout user guide](http://download.microsoft.com/download/E/0/8/E08B3BCE-3631-4CED-8E65-E3E7D252D06D/InMage_Scout_Standard_User_Guide_8.0.1.pdf) (not available in the Azure portal). | On-premises Hyper-V VMs in VMM clouds to a secondary VMM cloud.<br></br> Not supported without SCVMM  <br/><br/> Standard Hyper-V Replication only. SAN not supported.
**Classic portal** | Maintenance mode only. New vaults can't be created. | Maintenance mode only<br></br> Not supported without SCVMM
**PowerShell** | Not supported | Supported<br></br> Not supported without SCVMM

## <a name="on-premises-servers"></a>On-premises servers

### <a name="virtualization-servers"></a>Virtualization servers

**Deployment** | **Support**
--- | ---
**VMware VM/physical server** | vSphere 6.0, 5.5, or 5.1 with latest update
**Hyper-V (with VMM)** | VMM 2016 and VMM 2012 R2

  >[!Note]
  > VMM 2016 clouds with a mixture of Windows Server 2016 and 2012 R2 hosts aren't currently supported.

### <a name="host-servers"></a>Host servers

**Deployment** | **Support**
--- | ---
**VMware VM/physical server** | vCenter 5.5 or 6.0 (support for 5.5 features only)
**Hyper-V (no VMM)** | Not a supported configuration for replicating to a secondary site
**Hyper-V with VMM** | Windows Server 2016 and Windows Server 2012 R2 with the latest updates.<br/><br/> Windows Server 2016 hosts should be managed by VMM 2016.

## <a name="support-for-replicated-machine-os-versions"></a>Support for replicated machine OS versions
The following table summarizes operating system support in various deployment scenarios encountered while using Azure Site Recovery. This support is applicable for any workload running on the mentioned OS.

**VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
64-bit Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 with at least SP1<br/><br/> Red Hat Enterprise Linux 6.7, 7.1, 7.2 <br/><br/> Centos 6.5, 6.6, 6.7, 7.0, 7.1, 7.2 <br/><br/> Oracle Enterprise Linux 6.4 or 6.5 running the Red Hat compatible kernel, or Unbreakable Enterprise Kernel Release 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 | Any guest operating system [supported by Hyper-V](https://technet.microsoft.com/library/mt126277.aspx)

>[!Note]
>Only Linux machines with the following storage can be replicated: File system (EXT3, ETX4, ReiserFS, XFS); Multipath software-device Mapper; Volume manager (LVM2).
>Physical servers with HP CCISS controller storage are not supported.
>The ReiserFS file system is supported only on SUSE Linux Enterprise Server 11 SP3.

## <a name="network-configuration"></a>Network configuration

### <a name="hosts"></a>Hosts

**Configuration** | **VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
NIC teaming | Yes | Yes
VLAN | Yes | Yes
IPv4 | Yes | Yes
IPv6 | No | No

### <a name="guest-vms"></a>Guest VMs

**Configuration** | **VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
NIC teaming | No | No
IPv4 | Yes | Yes
IPv6 | No | No
Static IP (Windows) | Yes | Yes
Static IP (Linux) | Yes | Yes
Multi-NIC | Yes | Yes


## <a name="storage"></a>Storage

### <a name="host-storage"></a>Host storage

**Storage (host)** | **VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
NFS | Yes | N/A
SMB 3.0 | N/A | Yes
SAN (ISCSI) | Yes | Yes
Multi-path (MPIO) | Yes | Yes

### <a name="guest-or-physical-server-storage"></a>Guest or physical server storage

**Configuration** | **VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
VMDK | Yes | N/A
VHD/VHDX | N/A | Yes (up to 16 disks)
Gen 2 VM | N/A | Yes
Shared cluster disk | Yes  | No
Encrypted disk | No | No
UEFI| No | N/A
NFS | No | No
SMB 3.0 | No | No
RDM | Yes | N/A
Disk > 1 TB | No | Yes
Volume with striped disk > 1 TB<br/><br/> LVM | Yes | Yes
Storage Spaces | No | Yes
Hot add/remove disk | No | No
Exclude disk | No | Yes
Multi-path (MPIO) | N/A | Yes

## <a name="vaults"></a>Vaults

**Action** | **VMware/physical server** | **Hyper-V (with VMM)**
--- | --- | ---
Move vaults across resource groups (within or across subscriptions) | No | No
Move storage, network, Azure VMs across resource groups (within or across subscriptions) | No | No

## <a name="provider-and-agent"></a>Provider and agent

**Name** | **Description** | **Latest version** | **Details**
--- | --- | --- | --- | ---
**Azure Site Recovery Provider** | Coordinates communications between on-premises servers and Azure <br/><br/> Installed on on-premises VMM servers, or on Hyper-V servers if there's no VMM server | 5.1.19 ([available from portal](http://aka.ms/downloaddra)) | [Latest features and fixes](https://support.microsoft.com/kb/3155002)
**Mobility service** | Coordinates replication between on-premises VMware servers or physical servers, and the secondary site<br/><br/> Installed on VMware VM or physical servers that you want to replicate  | N/A (available from portal) | N/A


## <a name="next-steps"></a>Next steps

Learn about [deployment prerequisites](site-recovery-prereq.md).
