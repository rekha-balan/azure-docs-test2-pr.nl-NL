---
title: High Availability and Disaster Recovery for SQL Server | Microsoft Docs
description: A discussion of the various types of HADR strategies for SQL Server running in Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 404a1f4a6079033533e592920389a16549b00ff7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564367"
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>High availability and disaster recovery for SQL Server in Azure Virtual Machines
## <a name="overview"></a>Overview
Microsoft Azure virtual machines (VMs) with SQL Server can help lower the cost of a high availability and disaster recovery (HADR) database solution. Most SQL Server HADR solutions are supported in Azure virtual machines, both as Azure-only and as hybrid solutions. In an Azure-only solution, the entire HADR system runs in Azure. In a hybrid configuration, part of the solution runs in Azure and the other part runs on-premises in your organization. The flexibility of the Azure environment enables you to move partially or completely to Azure to satisfy the budget and HADR requirements of your SQL Server database systems.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-the-need-for-an-hadr-solution"></a>Understanding the need for an HADR solution
It is up to you to ensure that your database system possesses the HADR capabilities that the service-level agreement (SLA) requires. The fact that Azure provides high availability mechanisms, such as service healing for cloud services and failure recovery detection for Virtual Machines, does not itself guarantee you can meet the desired SLA. These mechanisms protect the high availability of the VMs but not the high availability of SQL Server running inside the VMs. It is possible for the SQL Server instance to fail while the VM is online and healthy. Moreover, even the high availability mechanisms provided by Azure allow for downtime of the VMs due to events such as recovery from software or hardware failures and operating system upgrades.

In addition, Geo Redundant Storage (GRS) in Azure, which is implemented with a feature called geo-replication, may not be an adequate disaster recovery solution for your databases. Because geo-replication sends data asynchronously, recent updates can be lost in the event of disaster. More information regarding geo-replication limitations are covered in the [Geo-replication not supported for data and log files on separate disks](#geo-replication-support) section.

## <a name="hadr-deployment-architectures"></a>HADR deployment architectures
SQL Server HADR technologies that are supported in Azure include:

* [Always On Availability Groups](https://technet.microsoft.com/library/hh510230.aspx)
* [Always On Failover Cluster Instances](https://technet.microsoft.com/library/ms189134.aspx)
* [Log Shipping](https://technet.microsoft.com/library/ms187103.aspx)
* [SQL Server Backup and Restore with Azure Blob Storage Service](https://msdn.microsoft.com/library/jj919148.aspx)
* [Database Mirroring](https://technet.microsoft.com/library/ms189852.aspx) - Deprecated in SQL Server 2016

It is possible to combine the technologies together to implement a SQL Server solution that has both high availability and disaster recovery capabilities. Depending on the technology you use, a hybrid deployment may require a VPN tunnel with the Azure virtual network. The sections below show you some of the example deployment architectures.

## <a name="azure-only-high-availability-solutions"></a>Azure-only: High availability solutions

You can have a high availability solution for SQL Server at a database level with Always On Availability Groups, or at an instance level with Always On Failover Cluster Instances. You can also create redundancy at both levels by creating Always On Availability Groups on a SQL Server Failover Cluster Instance. 

| Technology | Example Architectures |
| --- | --- |
| **Always On Availability Groups** |Availability replicas running in Azure VMs in the same region provide high availability. You need to configure a domain controller VM, because Windows failover clustering requires an Active Directory domain.<br/> ![Always On Availability Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>For more information, see [Configure Always On Availability Groups in Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Always On Failover Cluster Instances** |Failover Cluster Instances (FCI), which require shared storage, can be created in 3 different ways.<br/><br/>1. A two-node failover cluster running in Azure VMs with attached storage using [Windows Server 2016 Storage Spaces Direct \(S2D\)](virtual-machines-windows-portal-sql-create-failover-cluster.md) to provide a software-based virtual SAN.<br/><br/>2. A two-node failover cluster running in Azure VMs with storage supported by a third-party clustering solution. For a specific example that uses SIOS DataKeeper, see [High availability for a file share using failover clustering and 3rd party software SIOS Datakeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. A two-node failover cluster running in Azure VMs with remote iSCSI Target shared block storage via ExpressRoute. For example, NetApp Private Storage (NPS) exposes an iSCSI target via ExpressRoute with Equinix to Azure VMs.<br/><br/>For third-party shared storage and data replication solutions, you should contact the vendor for any issues related to accessing data on failover.<br/><br/>Note that using FCI on top of [Azure File storage](https://azure.microsoft.com/services/storage/files/) is not supported yet, because this solution does not utilize Premium Storage. We are working to support this soon. |

## <a name="azure-only-disaster-recovery-solutions"></a>Azure-only: Disaster recovery solutions
You can have a disaster recovery solution for your SQL Server databases in Azure using Always On Availability Groups, database mirroring, or backup and restore with storage blobs.

| Technology | Example Architectures |
| --- | --- |
| **Always On Availability Groups** |Availability replicas running across multiple datacenters in Azure VMs for disaster recovery. This cross-region solution protects against complete site outage. <br/> ![Always On Availability Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>Within a region, all replicas should be within the same cloud service and the same VNet. Because each region will have a separate VNet, these solutions require VNet to VNet connectivity. For more information, see [Configure a VNet-to-VNet connection using the Azure portal](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). For detailed instructions, see [Configure a SQL Server Always On Availability Group on Azure Virtual Machines in Different Regions](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Database Mirroring** |Principal and mirror and servers running in different datacenters for disaster recovery. You must deploy using server certificates because an active directory domain cannot span multiple datacenters.<br/>![Database Mirroring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Backup and Restore with Azure Blob Storage Service** |Production databases backed up directly to blob storage in a different datacenter for disaster recovery.<br/>![Backup and Restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>For more information, see [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>Hybrid IT: Disaster recovery solutions
You can have a disaster recovery solution for your SQL Server databases in a hybrid-IT environment using Always On Availability Groups, database mirroring, log shipping, and backup and restore with Azure blog storage.

| Technology | Example Architectures |
| --- | --- |
| **Always On Availability Groups** |Some availability replicas running in Azure VMs and other replicas running on-premises for cross-site disaster recovery. The production site can be either on-premises or in an Azure datacenter.<br/>![Always On Availability Groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Because all availability replicas must be in the same failover cluster, the cluster must span both networks (a multi-subnet failover cluster cluster). This configuration requires a VPN connection between Azure and the on-premises network.<br/><br/>For successful disaster recovery of your databases, you should also install a replica domain controller at the disaster recovery site.<br/><br/>It is possible to use the Add Replica Wizard in SSMS to add an Azure replica to an existing Always On Availability Group. For more information, see Tutorial: Extend your Always On Availability Group to Azure. |
| **Database Mirroring** |One partner running in an Azure VM and the other running on-premises for cross-site disaster recovery using server certificates. Partners do not need to be in the same Active Directory domain, and no VPN connection is required.<br/>![Database Mirroring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Another database mirroring scenario involves one partner running in an Azure VM and the other running on-premises in the same Active Directory domain for cross-site disaster recovery. A [VPN connection between the Azure virtual network and the on-premises network](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) is required.<br/><br/>For successful disaster recovery of your databases, you should also install a replica domain controller at the disaster recovery site. |
| **Log Shipping** |One server running in an Azure VM and the other running on-premises for cross-site disaster recovery. Log shipping depends on Windows file sharing, so a VPN connection between the Azure virtual network and the on-premises network is required.<br/>![Log Shipping](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>For successful disaster recovery of your databases, you should also install a replica domain controller at the disaster recovery site. |
| **Backup and Restore with Azure Blob Storage Service** |On-premises production databases backed up directly to Azure blob storage for disaster recovery.<br/>![Backup and Restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>For more information, see [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Important considerations for SQL Server HADR in Azure
Azure VMs, storage, and networking have different operational characteristics than an on-premises, non-virtualized IT infrastructure. A successful implementation of a HADR SQL Server solution in Azure requires that you understand these differences and design your solution to accommodate them.

### <a name="high-availability-nodes-in-an-availability-set"></a>High availability nodes in an availability set
Availability sets in Azure enable you to place the high availability nodes into separate Fault Domains (FDs) and Update Domains (UDs). For Azure VMs to be placed in the same availability set, you must deploy them in the same cloud service. Only nodes in the same cloud service can participate in the same availability set. For more information, see [Manage the Availability of Virtual Machines](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Failover cluster behavior in Azure networking
The non-RFC-compliant DHCP service in Azure can cause the creation of certain failover cluster configurations to fail, due to the cluster network name being assigned a duplicate IP address, such as the same IP address as one of the cluster nodes. This is an issue when you implement Always On Availability Groups, which depends on the Windows failover cluster feature.

Consider the scenario when a two-node cluster is created and brought online:

1. The cluster comes online, then NODE1 requests a dynamically assigned IP address for the cluster network name.
2. No IP address other than NODE1’s own IP address is given by the DHCP service, since the DHCP service recognizes that the request comes from NODE1 itself.
3. Windows detects that a duplicate address is assigned both to NODE1 and to the failover cluster network name, and the default cluster group fails to come online.
4. The default cluster group moves to NODE2, which treats NODE1’s IP address as the cluster IP address and brings the default cluster group online.
5. When NODE2 attempts to establish connectivity with NODE1, packets directed at NODE1 never leave NODE2 because it resolves NODE1’s IP address to itself. NODE2 cannot establish connectivity with NODE1, then loses quorum and shuts down the cluster.
6. In the meantime, NODE1 can send packets to NODE2, but NODE2 cannot reply. NODE1 loses quorum and shuts down the cluster.

This scenario can be avoided by assigning an unused static IP address, such as a link-local IP address like 169.254.1.1, to the cluster network name in order to bring the cluster network name online. To simplify this process, see [Configuring Windows Failover Cluster in Azure for Always On Availability Groups](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

For more information, see [Configure Always On Availability Groups in Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Availability group listener support
Availability group listeners are supported on Azure VMs running Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016. This support is made possible by the use of load-balanced endpoints enabled on the Azure VMs that are availability group nodes. You must follow special configuration steps for the listeners to work for both client applications that are running in Azure as well as those running on-premises.

There are two main options for setting up your listener: external (public) or internal. The external (public) listener uses an internet facing load balancer and is associated with a public Virtual IP (VIP) that is accessible over the internet. An internal listener uses an internal load balancer and only supports clients within the same Virtual Network. For either load balancer type, you must enable Direct Server Return. 

If the Availability Group spans multiple Azure subnets (such as a deployment that crosses Azure regions), the client connection string must include "**MultisubnetFailover=True**". This results in parallel connection attempts to the replicas in the different subnets. For instructions on setting up a listener, see

* [Configure an ILB listener for Always On Availability Groups in Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Configure an external listener for Always On Availability Groups in Azure](../classic/ps-sql-ext-listener.md).

You can still connect to each availability replica separately by connecting directly to the service instance. Also, since Always On Availability Groups are backward compatible with database mirroring clients, you can connect to the availability replicas like database mirroring partners as long as the replicas are configured similar to database mirroring:

* One primary replica and one secondary replica
* The secondary replica is configured as non-readable (**Readable Secondary** option set to **No**)

An example client connection string that corresponds to this database mirroring-like configuration using ADO.NET or SQL Server Native Client is below:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

For more information on client connectivity, see:

* [Using Connection String Keywords with SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Connect Clients to a Database Mirroring Session (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Connecting to Availability Group Listener in Hybrid IT](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Availability Group Listeners, Client Connectivity, and Application Failover (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Using Database-Mirroring Connection Strings with Availability Groups](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Network latency in hybrid IT
You should deploy your HADR solution with the assumption that there may be periods of time with high network latency between your on-premises network and Azure. When deploying replicas to Azure, you should use asynchronous commit instead of synchronous commit for the synchronization mode. When deploying database mirroring servers both on-premises and in Azure, use the high-performance mode instead of the high-safety mode.

### <a name="geo-replication-support"></a>Geo-replication support
Geo-replication in Azure disks does not support the data file and log file of the same database to be stored on separate disks. GRS replicates changes on each disk independently and asynchronously. This mechanism guarantees the write order within a single disk on the geo-replicated copy, but not across geo-replicated copies of multiple disks. If you configure a database to store its data file and its log file on separate disks, the recovered disks after a disaster may contain a more up-to-date copy of the data file than the log file, which breaks the write-ahead log in SQL Server and the ACID properties of transactions. If you do not have the option to disable geo-replication on the storage account, you should keep all data and log files for a given database on the same disk. If you must use more than one disk due to the size of the database, you need to deploy one of the disaster recovery solutions listed above to ensure data redundancy.

## <a name="next-steps"></a>Next steps
If you need to create an Azure virtual machine with SQL Server, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).

To get the best performance from SQL Server running on an Azure VM, see the guidance in [Performance Best Practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Other resources
* [Install a new Active Directory forest in Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Create Failover Cluster for Always On Availability Groups in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)








