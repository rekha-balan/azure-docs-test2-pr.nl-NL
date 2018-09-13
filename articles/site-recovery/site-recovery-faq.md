---
title: 'Azure Site Recovery: Frequently asked questions | Microsoft Docs'
description: This article discusses popular questions about Azure Site Recovery.
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: cfreeman
editor: ''
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: get-started-article
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 378697ef1702ba16380a286963a110baaca9fc38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556432"
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: Frequently asked questions (FAQ)
This article includes frequently asked questions about Azure Site Recovery. If you have questions after reading this article, post them on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>General
### <a name="what-does-site-recovery-do"></a>What does Site Recovery do?
Site Recovery contributes to your business continuity and disaster recovery (BCDR) strategy, by orchestrating and automating replication from on-premises virtual machines and physical servers to Azure, or to a secondary datacenter. [Learn more](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>What can Site Recovery protect?
* **Hyper-V virtual machines**: Site Recovery can protect any workload running on a Hyper-V VM.
* **Physical servers**: Site Recovery can protect physical servers running Windows or Linux.
* **VMware virtual machines**: Site Recovery can protect any workload running in a VMware VM.

### <a name="does-site-recovery-support-the-azure-resource-manager-model"></a>Does Site Recovery support the Azure Resource Manager model?
In addition to Site Recovery in the Azure classic portal, Site Recovery is available in the Azure portal with support for Resource Manager. For most deployment scenarios Site Recovery in the Azure portal provides a streamlined deployment experience and you can replicate VMs and physical servers into classic storage or Resource Manager storage. Here are the supported deployments:

* [Replicate VMware VMs or physical servers to Azure in the Azure portal](site-recovery-vmware-to-azure.md)
* [Replicate Hyper-V VMs in VMM clouds to Azure in the Azure portal](site-recovery-vmm-to-azure.md)
* [Replicate Hyper-V VMs (without VMM) to Azure in the Azure portal](site-recovery-hyper-v-site-to-azure.md)
* [Replicate Hyper-V VMs in VMM clouds to a secondary site in the Azure portal](site-recovery-vmm-to-vmm.md)

### <a name="what-do-i-need-in-hyper-v-to-orchestrate-replication-with-site-recovery"></a>What do I need in Hyper-V to orchestrate replication with Site Recovery?
For the Hyper-V host server what you need depends on the deployment scenario. Check out the Hyper-V prerequisites in:

* [Replicating Hyper-V VMs (without VMM) to Azure](site-recovery-hyper-v-site-to-azure.md)
* [Replicating Hyper-V VMs (with VMM) to Azure](site-recovery-vmm-to-azure.md)
* [Replicating Hyper-V VMs to a secondary datacenter](site-recovery-vmm-to-vmm.md)
* If you're replicating to a secondary datacenter read about [Supported guest operating systems for Hyper-V VMs](https://technet.microsoft.com/library/mt126277.aspx).
* If you're replicating to Azure, Site Recovery supports all the guest operating systems that are [supported by Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Can I protect VMs when Hyper-V is running on a client operating system?
No, VMs must be located on a Hyper-V host server that's running on a supported Windows server machine. If you need to protect a client computer you could replicate it as a physical machine to [Azure](site-recovery-vmware-to-azure.md) or a [secondary datacenter](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>What workloads can I protect with Site Recovery?
You can use Site Recovery to protect most workloads running on a supported VM or physical server. Site Recovery provides support for application-aware replication, so that apps can be recovered to an intelligent state. It integrates with Microsoft applications such as SharePoint, Exchange, Dynamics, SQL Server and Active Directory, and works closely with leading vendors, including Oracle, SAP, IBM and Red Hat. [Learn more](site-recovery-workload.md) about workload protection.

### <a name="do-hyper-v-hosts-need-to-be-in-vmm-clouds"></a>Do Hyper-V hosts need to be in VMM clouds?
If you want to replicate to a secondary datacenter, then Hyper-V VMs must be on Hyper-V hosts servers located in a VMM cloud. If you want to replicate to Azure, then you can replicate VMs on Hyper-V host servers with or without VMM clouds. [Read more](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Can I deploy Site Recovery with VMM if I only have one VMM server?

Yes. You can either replicate VMs in Hyper-V servers in the VMM cloud to Azure, or you can replicate between VMM clouds on the same server. For on-premises to on-premises replication, we recommend that you have a VMM server in both the primary and secondary sites.  

### <a name="what-physical-servers-can-i-protect"></a>What physical servers can I protect?
You can replicate physical servers running Windows and Linux to Azure or to a secondary site. [Learn about](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) operating system requirements.  The same requirements apply whether you're replicating physical servers to Azure, or to a secondary site.


Note that physical servers will run as VMs in Azure if your on-premises server goes down. Failback to an on-premises physical server isn't currently supported. For a machine protected as physical, you can only failback to a VMware virtual machine.

### <a name="what-vmware-vms-can-i-protect"></a>What VMware VMs can I protect?

To protect VMware VMs you'll need a vSphere hypervisor, and virtual machines running VMware tools. We also recommend that you have a VMware vCenter server to manage the hypervisors. [Learn more](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) about exact requirements for replicating VMware servers and VMs to Azure, or to a secondary site.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Can I manage disaster recovery for my branch offices with Site Recovery?
Yes. When you use Site Recovery to orchestrate replication and failover in your branch offices, you'll get a unified orchestration and view of all your branch office workloads in a central location. You can easily run failovers and administer disaster recovery of all branches from your head office, without visiting the branches.

## <a name="pricing"></a>Pricing

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>What charges do I incur while using Azure Site Recovery?
When you use Site Recovery, you incur charges for the Site Recovery license, Azure storage, storage transactions, and outbound data transfer. [Learn more](https://azure.microsoft.com/pricing/details/site-recovery).

The Site Recovery license is per protected instance, where an instance is a VM, or a physical server.

- If a VM disk replicates to a standard storage account, the Azure storage charge is for the storage consumption. For example, if the source disk size is 1 TB, and 400 GB is used, Site Recovery creates a 1 TB VHD in Azure, but the storage charged is 400 GB (plus the amount of storage space used for replication logs).
- If a VM disk replicates to a premium storage account, the Azure storage charge is for the provisioned storage size, rounded out for the nearest premium storage disk option. For example, if the source disk size is 50 GB, Site Recovery creates a 50 GB disk in Azure, and Azure maps this to the nearest premium storage disk (P10).  Costs are calculated on P10, and not on the 50 GB disk size.  [Learn more](https://aka.ms/premium-storage-pricing).  If you're using premium storage, a standard storage account for replication logging is also required, and the amount of standard storage space used for these logs is also billed.

Costs are also incurred during test failover, where the VM, storage, egress, and storage transactions costs will be applied.



## <a name="security"></a>Security
### <a name="is-replication-data-sent-to-the-site-recovery-service"></a>Is replication data sent to the Site Recovery service?
No, Site Recovery doesn't intercept replicated data, and doesn't have any information about what's running on your virtual machines or physical servers.
Replication data is exchanged between on-premises Hyper-V hosts, VMware hypervisors, or physical servers and Azure storage or your secondary site. Site Recovery has no ability to intercept that data. Only the metadata needed to orchestrate replication and failover is sent to the Site Recovery service.  

Site Recovery is ISO 27001:2013, 27018, HIPAA, DPA certified, and is in the process of SOC2 and FedRAMP JAB assessments.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-the-same-geographic-region-can-site-recovery-help-us"></a>For compliance reasons, even our on-premises metadata must remain within the same geographic region. Can Site Recovery help us?
Yes. When you create a Site Recovery vault in a region, we ensure that all metadata that we need to enable and orchestrate replication and failover remains within that region's geographic boundary.

### <a name="does-site-recovery-encrypt-replication"></a>Does Site Recovery encrypt replication?
For virtual machines and physical servers, replicating between on-premises sites encryption-in-transit is supported. For virtual machines and physical servers replicating to Azure, both encryption-in-transit and encryption-at-rest (in Azure) are supported.

## <a name="replication"></a>Replication

### <a name="can-i-replicate-over-a-site-to-site-vpn-to-azure"></a>Can I replicate over a site-to-site VPN to Azure?
Azure Site Recovery replicates data to an Azure storage account, over a public endpoint. Replication isn't over a site-to-site VPN. You can create a site-to-site VPN, with an Azure virtual network. This doesn't interfere with Site Recovery replication.

### <a name="can-i-use-expressroute-to-replicate-virtual-machines-to-azure"></a>Can I use ExpressRoute to replicate virtual machines to Azure?
Yes, ExpressRoute can be used to replicate virtual machines to Azure. Azure Site Recovery replicates data to an Azure Storage Account over a public endpoint. You need to set up [public peering](../expressroute/expressroute-circuit-peerings.md#public-peering) to use ExpressRoute for Site Recovery replication. After the virtual machines have been failed over to an Azure virtual network you can access them using the [private peering](../expressroute/expressroute-circuit-peerings.md#private-peering) setup with the Azure virtual network.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-to-azure"></a>Are there any prerequisites for replicating virtual machines to Azure?
Virtual machines you want to replicate to Azure should comply with [Azure requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-to-azure"></a>Can I replicate Hyper-V generation 2 virtual machines to Azure?
Yes. Site Recovery converts from generation 2 to generation 1 during failover. At failback the machine is converted back to generation 2. [Read more](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-to-azure-how-do-i-pay-for-azure-vms"></a>If I replicate to Azure how do I pay for Azure VMs?
During regular replication, data is replicated to geo-redundant Azure storage and you don’t need to pay any Azure IaaS virtual machine charges, providing a significant advantage. When you run a failover to Azure, Site Recovery automatically creates Azure IaaS virtual machines, and after that you'll be billed for the compute resources that you consume in Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Can I automate Site Recovery scenarios with an SDK?
Yes. You can automate Site Recovery workflows using the Rest API, PowerShell, or the Azure SDK. Currently supported scenarios for deploying Site Recovery using PowerShell:

* [Replicate Hyper-V VMs in VMMs clouds to Azure PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Replicate Hyper-V VMs without VMM to Azure PowerShell Resource Manager](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-to-azure-what-kind-of-storage-account-do-i-need"></a>If I replicate to Azure what kind of storage account do I need?
* **Azure classic portal**: If you're deploying Site Recovery in the Azure classic portal, you'll need a [standard geo-redundant storage account](../storage/storage-redundancy.md#geo-redundant-storage). Premium storage isn't currently supported. The account must be in the same region as the Site Recovery vault.
* **Azure portal**: If you're deploying Site Recovery in the Azure portal, you'll need an LRS or GRS storage account. We recommend GRS so that data is resilient if a regional outage occurs, or if the primary region can't be recovered. The account must be in the same region as the Recovery Services vault. Premium storage is now supported for VMware VM, Hyper-V VM, and physical server replication, when you deploy Site Recovery in the Azure portal.

### <a name="how-often-can-i-replicate-data"></a>How often can I replicate data?
* **Hyper-V:** Hyper-V VMs can be replicated every 30 seconds (except for premium storage), 5 minutes or 15 minutes. If you've set up SAN replication then replication is synchronous.
* **VMware and physical servers:** A replication frequency isn't relevant here. Replication is continuous.

### <a name="can-i-extend-replication-from-existing-recovery-site-to-another-tertiary-site"></a>Can I extend replication from existing recovery site to another tertiary site?
Extended or chained replication isn't supported. Request this feature in [feedback forum](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-the-first-time-i-replicate-to-azure"></a>Can I do an offline replication the first time I replicate to Azure?
This isn't supported. Request this feature in the [feedback forum](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Can I exclude specific disks from replication?
This is supported when you're [replicating VMware VMs and Hyper-V VMs](site-recovery-exclude-disk.md) to Azure, using the Azure portal.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Can I replicate virtual machines with dynamic disks?
Dynamic disks are supported when replicating Hyper-V virtual machines. They are also supported when replicating VMware VMs and physical machines to Azure. The operating system disk must be a basic disk.

### <a name="can-i-add-a-new-machine-to-an-existing-replication-group"></a>Can I add a new machine to an existing replication group?
Adding new machines to existing replication groups is supported. To do so, select the replication group (from 'Replicated items' blade) and right click/select context menu on the replication group and select the appropriate option.

![Add to replication group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/site-recovery/media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Can I throttle bandwidth allotted for Hyper-V replication traffic?
Yes. You can read more about throttling bandwidth in the deployment articles:

* [Capacity planning for replicating VMware VMs and physical servers](site-recovery-plan-capacity-vmware.md)
* [Capacity planning for replicating Hyper-V VMs in VMM clouds](site-recovery-vmm-to-azure.md#capacity-planning)
* [Capacity planning for replicating Hyper-V VMs without VMM](site-recovery-hyper-v-site-to-azure.md#capacity-planning)

## <a name="failover"></a>Failover
### <a name="if-im-failing-over-to-azure-how-do-i-access-the-azure-virtual-machines-after-failover"></a>If I'm failing over to Azure, how do I access the Azure virtual machines after failover?
You can access the Azure VMs over a secure Internet connection, over a site-to-site VPN, or over Azure ExpressRoute. You'll need to prepare a number of things in order to connect. [Learn more](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-to-azure-how-does-azure-make-sure-my-data-is-resilient"></a>If I fail over to Azure how does Azure make sure my data is resilient?
Azure is designed for resilience. Site Recovery is already engineered for failover to a secondary Azure datacenter, in accordance with the Azure SLA if the need arises. If this happens, we make sure your metadata and vaults remain within the same geographic region that you chose for your vault.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>If I'm replicating between two datacenters what happens if my primary datacenter experiences an unexpected outage?
You can trigger an unplanned failover from the secondary site. Site Recovery doesn't need connectivity from the primary site to perform the failover.

### <a name="is-failover-automatic"></a>Is failover automatic?
Failover isn't automatic. You initiate failovers with single click in the portal, or you can use [Site Recovery PowerShell](https://docs.microsoft.com/en-us/powershell/resourcemanager/azurerm.siterecovery/v3.2.0/azurerm.siterecovery) to trigger a failover. Failing back is a simple action in the Site Recovery portal.

To automate you could use on-premises Orchestrator or Operations Manager to detect a virtual machine failure, and then trigger the failover using the SDK.

* [Read more](site-recovery-create-recovery-plans.md) about recovery plans.
* [Read more](site-recovery-failover.md) about failover.
* [Read more](site-recovery-failback-azure-to-vmware.md) about failing back VMware VMs and physical servers

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-to-a-different-host"></a>If my on-premises host is not responding or crashed, can I failover back to a different host?
Yes, you can use the alternate location recovery to failback to a different host from Azure. Read more about the options in the below links for VMware and Hyper-v virtual machines.

* [For VMware virtual machines](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [For Hyper-v virtual machines](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Service providers
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>I'm a service provider. Does Site Recovery work for dedicated and shared infrastructure models?
Yes, Site Recovery supports both dedicated and shared infrastructure models.

### <a name="for-a-service-provider-is-the-identity-of-my-tenant-shared-with-the-site-recovery-service"></a>For a service provider, is the identity of my tenant shared with the Site Recovery service?
No. Tenant identity remains anonymous. Your tenants don't need access to the Site Recovery portal. Only the service provider administrator interacts with the portal.

### <a name="will-tenant-application-data-ever-go-to-azure"></a>Will tenant application data ever go to Azure?
When replicating between service provider-owned sites, application data never goes to Azure. Data is encrypted in-transit, and replicated directly between the service provider sites.

If you're replicating to Azure, application data is sent to Azure storage but not to the Site Recovery service. Data is encrypted in-transit, and remains encrypted in Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Will my tenants receive a bill for any Azure services?
No. Azure's billing relationship is directly with the service provider. Service providers are responsible for generating specific bills for their tenants.

### <a name="if-im-replicating-to-azure-do-we-need-to-run-virtual-machines-in-azure-at-all-times"></a>If I'm replicating to Azure, do we need to run virtual machines in Azure at all times?
No, Data is replicated to an Azure storage account in your subscription. When you perform a test failover (DR drill) or an actual failover, Site Recovery automatically creates virtual machines in your subscription.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-to-azure"></a>Do you ensure tenant-level isolation when I replicate to Azure?
Yes.

### <a name="what-platforms-do-you-currently-support"></a>What platforms do you currently support?
We support Azure Pack, Cloud Platform System, and System Center based (2012 and higher) deployments. [Learn more](https://technet.microsoft.com/library/dn850370.aspx) about Azure Pack and Site Recovery integration.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Do you support single Azure Pack and single VMM server deployments?
Yes, you can replicate Hyper-V virtual machines to Azure, or between service provider sites.  Note that if you replicate between service provider sites, Azure runbook integration isn't available.

## <a name="next-steps"></a>Next steps
* Read the [Site Recovery overview](site-recovery-overview.md)
* Learn about [Site Recovery architecture](site-recovery-components.md)  

