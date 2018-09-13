---
title: What workloads can you protect with Azure Site Recovery?
description: Azure Site Recovery protects your workloads and applications by coordinating the replication, failover and recovery of on-premises virtual machines and physical servers to Azure or to a secondary on-premises site
services: site-recovery
documentationcenter: ''
author: rayne-wiselman
manager: cfreeman
editor: ''
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/06/2017
ms.author: raynew
ms.openlocfilehash: 4149c5e06f1a23864ca0f92f1b7b73f4f66949df
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552241"
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>What workloads can you protect with Azure Site Recovery?
This article describes workloads and applications you can replicate with the Azure Site Recovery service.

Post any comments or questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Overview
Organizations need a business continuity and disaster recovery (BCDR) strategy to keep workloads and data safe and available during planned and unplanned downtime, and recover to regular working conditions as soon as possible.

Site Recovery is an Azure service that contributes to your BCDR strategy. Using Site Recovery, you can deploy application-aware replication to the cloud, or to a secondary site. Whether your apps are Windows or Linux-based, running on physical servers, VMware or Hyper-V, you can use Site Recovery to orchestrate replication, perform disaster recovery testing, and run failovers and failback.

Site Recovery integrates with Microsoft applications, including SharePoint, Exchange, Dynamics, SQL Server and Active Directory. Microsoft also works closely with leading vendors including Oracle, SAP, IBM and Red Hat. You can customize replication solutions on an app-by-app basis.

## <a name="why-use-site-recovery-for-application-replication"></a>Why use Site Recovery for application replication?
Site Recovery contributes to application-level protection and recovery as follows:

* App-agnostic, providing replication for any workloads running on a supported machine.
* Near-synchronous replication, with RPOs as low as 30 seconds to meet the needs of most critical business apps.
* App-consistent snapshots, for single or multi-tier applications.
* Integration with SQL Server AlwaysOn, and partnership with other application-level replication technologies, including AD replication, SQL AlwaysOn, Exchange Database Availability Groups (DAGs) and Oracle Data Guard.
* Flexible recovery plans, that enable you to recover an entire application stack with a single click, and include to include external scripts and manual actions in the plan.
* Advanced network management in Site Recovery and Azure to simplify app network requirements, including the ability to reserve IP addresses, configure load-balancing, and integration with Azure Traffic Manager, for low RTO network switchovers.
* A rich automation library that provides production-ready, application-specific scripts that can be downloaded and integrated with recovery plans.

## <a name="workload-summary"></a>Workload summary
Site Recovery can replicate any app running on a supported machine. In addition we've partnered with product teams to carry out additional app-specific testing.

| **Workload** | **Replicate Hyper-V VMs to a secondary site** | **Replicate Hyper-V VMs to Azure** | **Replicate VMware VMs to a secondary site** | **Replicate VMware VMs to Azure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS |Y |Y |Y |Y |
| Web apps (IIS, SQL) |Y |Y |Y |Y |
| System Center Operations Manager |Y |Y |Y |Y |
| Sharepoint |Y |Y |Y |Y |
| SAP<br/><br/>Replicate SAP site to Azure for non-cluster |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |
| Exchange (non-DAG) |Y |Coming soon |Y |Y |
| Remote Desktop/VDI |Y |Y |Y |N/A |
| Linux (operating system and apps) |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |
| Dynamics AX |Y |Y |Y |Y |
| Dynamics CRM |Y |Coming soon |Y |Coming soon |
| Oracle |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |Y (tested by Microsoft) |
| Windows File Server |Y |Y |Y |Y |
| Citrix XenApp and XenDesktop |N/A |Y |N/A |Y |

## <a name="replicate-active-directory-and-dns"></a>Replicate Active Directory and DNS
An Active Directory and DNS infrastructure are essential to most enterprise apps. During disaster recovery, you'll need to protect and recover these infrastructure components, before recovering your workloads and apps.

You can use Site Recovery to create a complete automated disaster recovery plan for Active Directory and DNS. For example, if you want to fail over SharePoint and SAP from a primary to a secondary site, you can set up a recovery plan that fails over Active Directory first, and then an additional app-specific recovery plan to fail over the other apps that rely on Active Directory.

[Learn more](site-recovery-active-directory.md) about protecting Active Directory and DNS.

## <a name="protect-sql-server"></a>Protect SQL Server
SQL Server provides a data services foundation for data services for many business apps in an on-premises data center.  Site Recovery can be used together with SQL Server HA/DR technologies, to protect multi-tiered enterprise apps that use SQL Server. Site Recovery provides:

* A simple and cost-effective disaster recovery solution for SQL Server. Replicate multiple versions and editions of SQL Server standalone servers and clusters, to Azure or to a secondary site.  
* Integration with SQL AlwaysOn Availability Groups, to manage failover and failback with Azure Site Recovery recovery plans.
* End-to-end recovery plans for the all tiers in an application, including the SQL Server databases.
* Scaling of SQL Server for peak loads with Site Recovery, by “bursting” them into larger IaaS virtual machine sizes in Azure.
* Easy testing of SQL Server disaster recovery. You can run test failovers to analyze data and run compliance checks, without impacting your production environment.

[Learn more](site-recovery-sql.md) about protecting SQL server.

## <a name="protect-sharepoint"></a>Protect SharePoint
Azure Site Recovery helps protect SharePoint deployments, as follows:

* Eliminates the need and associated infrastructure costs for a stand-by farm for disaster recovery. Use Site Recovery to replicate an entire farm (Web, app and database tiers) to Azure or to a secondary site.
* Simplifies application deployment and management. Updates deployed to the primary site are automatically replicated, and are thus available after failover and recovery of a farm in a secondary site. Also lowers the management complexity and costs associated with keeping a stand-by farm up-to-date.
* Simplifies SharePoint application development and testing by creating a production-like copy on-demand replica environment for testing and debugging.
* Simplifies transition to the cloud by using Site Recovery to migrate SharePoint deployments to Azure.

[Learn more](https://gallery.technet.microsoft.com/SharePoint-DR-Solution-f6b4aeae) about protecting SharePoint.

## <a name="protect-dynamics-ax"></a>Protect Dynamics AX
Azure Site Recovery helps protect your Dynamics AX ERP solution, by:

* Orchestrating replication of your entire Dynamics AX environment (Web and AOS tiers, database tiers, SharePoint) to Azure, or to a secondary site.
* Simplifying migration of Dynamics AX deployments to the cloud (Azure).
* Simplifying Dynamics AX application development and testing by creating a production-like copy on-demand, for testing and debugging.

[Learn more](https://gallery.technet.microsoft.com/Dynamics-AX-DR-Solution-b2a76281) about protecting Dynamic AX.

## <a name="protect-rds"></a>Protect RDS
Remote Desktop Services (RDS) enables virtual desktop infrastructure (VDI), session-based desktops, and applications, allowing users to work anywhere. With Azure Site Recovery you can:

* Replicate managed or unmanaged pooled virtual desktops to a secondary site, and remote applications and sessions to a secondary site or Azure.
* Here's what you can replicate:

| **RDS** | **Replicate Hyper-V VMs to a secondary site** | **Replicate Hyper-V VMs to Azure** | **Replicate VMware VMs to a secondary site** | **Replicate VMware VMs to Azure** | **Replicate physical servers to a secondary site** | **Replicate physical servers to Azure** |
| --- | --- | --- | --- | --- | --- | --- |
| **Pooled Virtual Desktop (unmanaged)** |Yes |No |Yes |No |Yes |No |
| **Pooled Virtual Desktop (managed and without UPD)** |Yes |No |Yes |No |Yes |No |
| **Remote applications and Desktop sessions (without UPD)** |Yes |Yes |Yes |Yes |Yes |Yes |

[Learn more](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) about protecting RDS.

## <a name="protect-exchange"></a>Protect Exchange
Site Recovery helps protect Exchange, as follows:

* For small Exchange deployments, such as a single or standalone servers, Site Recovery can replicate and fail over to Azure or to a secondary site.
* For larger deployments, Site Recovery integrates with Exchange DAGS.
* Exchange DAGs are the recommended solution for Exchange disaster recovery in an enterprise.  Site Recovery recovery plans can include DAGs, to orchestrate DAG failover across sites.

[Learn more](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) about protecting Exchange.

## <a name="protect-sap"></a>Protect SAP
Use Site Recovery to protect your SAP deployment, as follows:

* Enable protection of the entire SAP deployment, by replicating different deployment layers to Azure, or to a secondary site.
* Simplify cloud migration, by using Site Recovery to migrate your SAP deployment to Azure.
* Simplify SAP development and testing, by creating a production-like copy on-demand for testing and debugging applications.

[Learn more](http://aka.ms/asr-sap) about protecting SAP.

## <a name="protect-iis"></a>Protect IIS
Use Site Recovery to protect your IIS deployment, as follows:

Azure Site Recovery provides disaster recovery by replicating the critical components in your environment to a cold remote site or a public cloud like Microsoft Azure. Since the virtual machine with the web server and the database are being replicated to the recovery site, there is no requirement to backup configuration files or certificates separately. The application mappings and bindings dependent on environment variables that are changed post failover can be updated through scripts integrated into the disaster recovery plans. Virtual Machines are brought up on the recovery site only in the event of a failover. Not only this, Azure Site Recovery also helps you orchestrate the end to end failover by providing you the following capabilities:

-   Sequencing the shutdown and startup of virtual machines in the various tiers.
-   Adding scripts to allow update of application dependencies and bindings on the virtual machines after they have been started up. The scripts can also be used to update the DNS server to point to the recovery site.
-   Allocate IP addresses to virtual machines pre-failover by mapping the primary and recovery networks and hence use scripts that do not need to be updated post failover.
-   Ability for a one-click failover for multiple web applications on the web servers, thus eliminating the scope for confusion in the event of a disaster.
-   Ability to test the recovery plans in an isolated environment for DR drills.

[Learn more](https://aka.ms/asr-iis) about protecting IIS web farm.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Protect Citrix XenApp and XenDesktop
Use Site Recovery to protect your Citrix XenApp and XenDesktop deployments, as follows:

* Enable protection of the Citrix XenApp and XenDesktop deployment, by replicating different deployment layers including (AD DNS server, SQL database server, Citrix Delivery Controller, StoreFront server, XenApp Master (VDA), Citrix XenApp License Server) to Azure.
* Simplify cloud migration, by using Site Recovery to migrate your Citrix XenApp and XenDesktop deployment to Azure.
* Simplify Citrix XenApp/XenDesktop testing, by creating a production-like copy on-demand for testing and debugging.
* This solution is only applicable for Windows Server operating system virtual desktops and not client virtual desktops as client virtual desktops are not yet supported for licensing in Azure. 
[Learn More](https://azure.microsoft.com/en-us/pricing/licensing-faq/) about licensing for client/server desktops in Azure.

[Learn more](https://aka.ms/citrix-xenapp-xendesktop-with-asr) about protecting Citrix XenApp and XenDesktop deployments.

## <a name="next-steps"></a>Next steps
[Check prerequisites](site-recovery-prereq.md) 
