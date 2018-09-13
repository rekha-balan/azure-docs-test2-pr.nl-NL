---
title: How does Site Recovery work? | Microsoft Docs
description: This article provides an overview of Site Recovery architecture
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: jwhit
editor: ''
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ms.openlocfilehash: e42a440cdcc318df318188f55de19eaf626507df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556283"
---
# <a name="how-does-azure-site-recovery-work"></a>How does Azure Site Recovery work?

This article describes underlying architecture of the [Azure Site Recovery](site-recovery-overview.md) service, and the components that make it work.

Post any comments at the bottom of this article, or in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-to-azure"></a>Replicate to Azure

You can replicate the following to Azure:

- **VMware**: On-premises VMware VMs running on a [supported host](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). You can replicate VMware VMs running [supported operating systems](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
- **Hyper-V**: On-premises Hyper-V VMs running on [supported hosts](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Physical machines**: On-premises physical servers running Windows or Linux on [supported operating systems](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). You can replicate Hyper-V VMs running any guest operating system [supported by Hyper-V and Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-to-azure"></a>VMware to Azure

Here's what you need for replicating VMware VMs to Azure.

Area | Component | Details
--- | --- | ---
**Azure** | In Azure you need an Azure account, an Azure storage account, and an Azure network. | Storage and network can be Resource Manager accounts, or classic accounts.<br/><br/>  Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs. The Azure VMs connect to the Azure virtual network when they're created.
**Configuration server** | A single management server (VMWare VM) runs all on-premises components - configuration server, process server, master target server | The configuration server coordinates communications between on-premises and Azure, and manages data replication.
 **Process server**:  | Installed by default on the configuration server. | Acts as a replication gateway. Receives replication data, optimizes it with caching, compression, and encryption, and sends it to Azure storage.<br/><br/> The process server also handles push installation of the Mobility service to protected machines, and performs automatic discovery of VMware VMs.<br/><br/> As your deployment grows you can add additional separate dedicated process servers to handle increasing volumes of replication traffic.
 **Master target server** | Installed by default on the on-premises configuration server. | Handles replication data during failback from Azure.<br/><br/> If volumes of failback traffic are high, you can deploy a separate master target server for failback.
**VMware servers** | VMware VMs are hosted on vSphere ESXi servers, and we recommend a vCenter server to manage the hosts. | You add VMware servers to your Recovery Services vault.<br/><br/> I
**Replicated machines** | The Mobility service will be installed on each VMware VM you want to replicate. It can be installed manually on each machine, or with a push installation from the process server.

**Figure 1: VMware to Azure components**

![Components](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Replication process

1. You set up the deployment, including Azure components, and a Recovery Services vault. In the vault you specify the replication source and target, set up the configuration server, add VMware servers, create a replication policy, deploy the Mobility service, enable replication, and run a test failover.
2.  Machines start replicating in accordance with the replication policy, and an initial copy of the data is replicated to Azure storage.
4. Replication of delta changes to Azure begins after the initial replication finishes. Tracked changes for a machine are held in a .hrl file.
    - Replicating machines communicate with the configuration server on port HTTPS 443 inbound, for replication management.
    - Replicating machines send replication data to the process server on port HTTPS 9443 inbound (can be configured).
    - The configuration server orchestrates replication management with Azure over port HTTPS 443 outbound.
    - The process server receives data from source machines, optimizes and encrypts it, and sends it to Azure storage over port 443 outbound.
    - If you enable multi-VM consistency, then machines in the replication group communicate with each other over port 20004. Multi-VM is used if you group multiple machines into replication groups that share crash-consistent and app-consistent recovery points when they fail over. This is useful if machines are running the same workload and need to be consistent.
5. Traffic is replicated to Azure storage public endpoints, over the internet. Alternately, you can use Azure ExpressRoute [public peering](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering). Replicating traffic over a site-to-site VPN from an on-premises site to Azure isn't supported.

**Figure 2: VMware to Azure replication**

![Enhanced](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Failover and failback

1. After you verify that test failover is working as expected, you can run unplanned failovers to Azure as required. Planned failover isn't supported.
2. You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md), to fail over multiple VMs.
3. When you run a failover, replica VMs are created in Azure. You commit a failover to start accessing the workload from the replica Azure VM.
4. When your primary on-premises site is available again, you can fail back. You set up a failback infrastructure, start replicating the machine from the secondary site to the primary, and run an unplanned failover from the secondary site. After you commit this failover, data will be back on-premises, and you need to enable replication to Azure again. [Learn more](site-recovery-failback-azure-to-vmware.md)

There are a few failback requirements:


- **Temporary process server in Azure**: If you want to fail back from Azure after failover you'll need to set up an Azure VM configured as a process server, to handle replication from Azure. You can delete this VM after failback finishes.
- **VPN connection**: For failback you'll need a VPN connection (or Azure ExpressRoute) set up from the Azure network to the on-premises site.
- **Separate on-premises master target server**: The on-premises master target server handles failback. The master target server is installed by default on the management server, but if you're failing back larger volumes of traffic you should set up a separate on-premises master target server for this purpose.
- **Failback policy**: To replicate back to your on-premises site, you need a failback policy. This is automatically created when you created your replication policy.

**Figure 3: VMware/physical failback**

![Failback](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/enhanced-failback.png)

## <a name="physical-to-azure"></a>Physical to Azure

When you replicate physical on-premises servers to Azure, replication uses also the same components and processes as [VMware to Azure](#vmware-replication-to-azure), but note these differences:

- You can use a physical server for the configuration server, instead of a VMware VM
- You will need an on-premises VMware infrastructure for failback. You can't fail back to a physical machine.

## <a name="hyper-v-to-azure"></a>Hyper-V to Azure

Here's what you need for replicating Hyper-V VMs to Azure.

**Area** | **Component** | **Details**
--- | --- | ---
**Azure** | In Azure you need a Microsoft Azure account, an Azure storage account, and a Azure network. | Storage and network can be Resource Manager-based, or classic accounts.<br/><br/> Replicated data is stored in the storage account, and Azure VMs are created with the replicated data when failover from your on-premises site occurs.<br/><br/> The Azure VMs connect to the Azure virtual network when they're created.
**VMM server** | Hyper-V hosts located in VMM clouds | If Hyper-V hosts are managed in VMM clouds, you register the VMM server in the Recovery Services vault.<br/><br/> On the VMM server you install the Site Recovery Provider to orchestrate replication with Azure.<br/><br/> You need logical and VM networks set up to configure network mapping. A VM network should be linked to a logical network that's associated with the cloud.
**Hyper-V host** | Hyper-V servers can be deployed with or without VMM server. | If there's no VMM server, the Site Recovery Provider is installed on the host to orchestrate replication with Site Recovery over the internet. If there's a VMM server, the Provider is installed on it, and not on the host.<br/><br/> The Recovery Services agent is installed on the host to handle data replication.<br/><br/> Communications from both the Provider and the agent are secure and encrypted. Replicated data in Azure storage is also encrypted.
**Hyper-V VMs** | You need one or more VMs on the Hyper-V host server. | Nothing needs to explicitly installed on VMs


### <a name="replication-process"></a>Replication process

1. You set up the Azure components. We recommend you set up storage and network accounts before you begin Site Recovery deployment.
2. You create a Replication Services vault for Site Recovery, and configure vault settings, including:
    - Source and target settings. If you're not managing Hyper-V hosts in a VMM cloud, for the target you create a Hyper-V site container, and add Hyper-V hosts to it. If Hyper-V hosts are managed in VMM, the source is the VMM cloud. The target is Azure.
    - Installation of the Azure Site Recovery Provider and the Microsoft Azure Recovery Services agent. If you have VMM the Provider will be installed on it, and the agent on each Hyper-V host. If you don't have VMM, both the Provider and agent are installed on each host.
    - You create a replication policy for the Hyper-V site or VMM cloud. The policy is applied to all VMs located on hosts in the site or cloud.
    - You enable replication for Hyper-V VMs. Initial replication occurs in accordance with the replication policy settings.
4. Data changes are tracked, and replication of delta changes to Azure begins after the initial replication finishes. Tracked changes for an item are held in a .hrl file.
5. You run a test failover to make sure everything's working.

### <a name="failover-and-failback-process"></a>Failover and failback process

1. You can run a planned or unplanned [failover](site-recovery-failover.md) from on-premises Hyper-V VMs to Azure. If you run a planned failover, then source VMs are shut down to ensure no data loss.
2. You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.
4. After you run the failover, you should be able to see the created replica VMs in Azure. You can assign a public IP address to the VM if required.
5. You then commit the failover to start accessing the workload from the replica Azure VM.
6. When your primary on-premises site is available again, you can [fail back](site-recovery-failback-from-azure-to-hyper-v.md). You kick off a planned failover from Azure to the primary site. For a planned failover you can select to failback to the same VM or to an alternate location, and synchronize changes between Azure and on-premises, to ensure no data loss. When VMs are created on-premises, you commit the failover.

**Figure 4: Hyper-V site to Azure replication**

![Components](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figure 5: Hyper-V in VMM clouds to Azure replication**

![Components](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-to-a-secondary-site"></a>Replicate to a secondary site

You can replicate the following to your secondary site:

- **VMware**: On-premises VMware VMs running on a [supported host](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). You can replicate VMware VMs running [supported operating systems](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
- **Physical machines**: On-premises physical servers running Windows or Linux on [supported operating systems](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: On-premises Hyper-V VMs running on [supported Hyper-V hosts](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) managed in VMM clouds. [supported hosts](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). You can replicate Hyper-V VMs running any guest operating system [supported by Hyper-V and Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-to-a-secondary-site"></a>VMware/physical to a secondary site

You replicate VMware VMs or physical servers to a secondary site using InMage Scout.

### <a name="components"></a>Components

**Area** | **Component** | **Details**
--- | --- | ---
**Azure** | InMage Scout. | To obtain InMage Scout you need an Azure subscription.<br/><br/> After you create a Recovery Services vault, you download InMage Scout and install the latest updates to set up the deployment.
**Process server** | Located in primary site | You deploy the process server to handle caching, compression, and data optimization.<br/><br/> It also handles push installation of the Unified Agent to machines you want to protect.
**Configuration server** | Located in secondary site | The configuration server manages, configure, and monitor your deployment, either using the management website or the vContinuum console.
**vContinuum server** | Optional. Installed in the same location as the configuration server. | It provides a console for managing and monitoring your protected environment.
**Master target server** | Located in the secondary site | The master target server holds replicated data. It receives data from the process server, creates a replica machine in the secondary site, and holds the data retention points.<br/><br/> The number of master target servers you need depends on the number of machines you're protecting.<br/><br/> If you want to fail back to the primary site, you need a master target server there too. The Unified Agent is installed on this server.
**VMware ESX/ESXi and vCenter server** |  VMs are hosted on ESX/ESXi hosts. Hosts are managed with a vCenter server | You need a VMware infrastructure to replicate VMware VMs.
**VMs/physical servers** |  Unified Agent installed on VMware VMs and physical servers you want to replicate. | The agent acts as a communication provider between all of the components.


### <a name="replication-process"></a>Replication process

1. You set up the component servers in each site (configuration, process, master target), and install the Unified Agent on machines that you want to replicate.
2. After initial replication, the agent on each machine sends delta replication changes to the process server.
3. The process server optimizes the data, and transfers it to the master target server on the secondary site. The configuration server manages the replication process.

**Figure 6: VMware to VMware replication**

![VMware to VMware](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-to-a-secondary-site"></a>Hyper-V to a secondary site

Here's what you need for replicating Hyper-V VMs to a secondary site.


**Area** | **Component** | **Details**
--- | --- | ---
**Azure** | You need a Microsoft Azure account. |
**VMM server** | We recommend a VMM server in the primary site, and one in the secondary site | Each VMM server should be connected to the internet.<br/><br/> Each server should have at least one VMM private cloud, with the Hyper-V capability profile set.<br/><br/> You install the Azure Site Recovery Provider on the VMM server. The Provider coordinates and orchestrates replication with the Site Recovery service over the internet. Communications between the Provider and Azure are secure and encrypted.
**Hyper-V server** |  One or more Hyper-V host servers in the primary and secondary VMM clouds.<br/><br/> Servers should be connected to the internet.<br/><br/> Data is replicated between the primary and secondary Hyper-V host servers over the LAN or VPN, using Kerberos or certificate authentication.  
**Hyper-V VMs** | Located on the source Hyper-V host server. | The source host server should have at least one VM that you want to replicate.

### <a name="replication-process"></a>Replication process

1. You set up the Azure account.
2. You create a Replication Services vault for Site Recovery, and configure vault settings, including:

    - The replication source and target (primary and secondary sites).
    - Installation of the Azure Site Recovery Provider and the Microsoft Azure Recovery Services agent. The Provider is installed on VMM servers, and the agent on each Hyper-V host.
    - You create a replication policy for source VMM cloud. The policy is applied to all VMs located on hosts in the cloud.
    - You enable replication for Hyper-V VMs. Initial replication occurs in accordance with the replication policy settings.
4. Data changes are tracked, and replication of delta changes to begins after the initial replication finishes. Tracked changes for an item are held in a .hrl file.
5. You run a test failover to make sure everything's working.

**Figure 7: VMM to VMM replication**

![On-premises to on-premises](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Failover and failback

1. You can run a planned or unplanned [failover](site-recovery-failover.md) between on-premises sites. If you run a planned failover, then source VMs are shut down to ensure no data loss.
2. You can fail over a single machine, or create [recovery plans](site-recovery-create-recovery-plans.md) to orchestrate failover of multiple machines.
4. If you perform an unplanned failover to a secondary site, after the failover machines in the secondary location aren't enabled for protection or replication. If you ran a planned failover, after the failover, machines in the secondary location are protected.
5. Then, you commit the failover to start accessing the workload from the replica VM.
6. When your primary site is available again, you initiate reverse replication to replicate from the secondary site to the primary. Reverse replication brings the virtual machines into a protected state, but the secondary datacenter is still the active location.
7. To make the primary site into the active location again, you initiate a planned failover from secondary to primary, followed by another reverse replication.


## <a name="next-steps"></a>Next steps

- [Learn more](site-recovery-hyper-v-azure-architecture.md) about the Hyper-V replication workflow.
- [Check prerequisites](site-recovery-prereq.md)







