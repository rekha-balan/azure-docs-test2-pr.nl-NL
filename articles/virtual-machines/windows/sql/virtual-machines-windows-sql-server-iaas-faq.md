---
title: SQL Server on Azure Virtual Machines FAQ | Microsoft Docs
description: This article provides answers to frequently asked questions about running SQL Server on Azure VMs.
services: virtual-machines-windows
documentationcenter: ''
author: v-shysun
manager: felixwu
editor: ''
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 498291fbf49e8bc119d93bb2dd4118e62ebdc71c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549665"
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Frequently asked questions for SQL Server on Azure Virtual Machines
This topic provides answers to some of the most common questions about running [SQL Server on Azure Virtual Machines](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Frequently Asked Questions
1. **How do I create an Azure virtual machine with SQL Server?**
   
    The easiest solution is to create a Virtual Machine that includes SQL Server. For a tutorial on signing up for Azure and creating a SQL VM from the portal, see [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md). You can select a virtual machine image that uses pay-per-minute SQL Server licensing, or you can use an image that allows you to bring your own SQL Server license. You also have the option of manually installing SQL Server on a VM and reusing an on-premises license. If you bring your own license, you must have [License Mobility through Software Assurance on Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. **What is the difference between SQL VMs and the SQL Database service?**
   
    Conceptually, running SQL Server on an Azure virtual machine is not that different from running SQL Server in a remote datacenter. In contrast, [SQL Database](../../../sql-database/sql-database-technical-overview.md) offers database-as-a-service. With SQL Database, you do not have access to the machines that host your databases. For a full comparison, see [Choose a cloud SQL Server option: Azure SQL (PaaS) Database or SQL Server on Azure VMs (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).
3. **How can I migrate my on-premises SQL Server database to the Cloud?**
   
    First create an Azure virtual machine with a SQL Server instance. Then migrate your on-premises databases to that instance. For data migration strategies, see [Migrate a SQL Server database to SQL Server in an Azure VM](virtual-machines-windows-migrate-sql.md).
4. **Can I change the installed features or install a second instance of SQL Server on the same VM?**
   
    Yes. The SQL Server installation media is located in a folder on the **C** drive. Run **Setup.exe** from that location to add new SQL Server instances or to change other installed features of SQL Server on the machine.
5. **How do I upgrade to a new version/edition of the SQL Server in an Azure VM?**
   
    Currently, there is no in-place upgrade for SQL Server running in an Azure VM. Create a new Azure virtual machine with the desired SQL Server version/edition, and then migrate your databases to the new server using standard [data migration techniques](virtual-machines-windows-migrate-sql.md).
6. **How can I install my licensed copy of SQL Server on an Azure VM?**
   
    There are two ways to do this. You can provision one of the [virtual machine images that supports licenses](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Another option is to copy the SQL Server installation media to a Windows Server VM, and then install SQL Server on the VM. For licensing reasons, you must have [License Mobility through Software Assurance on Azure](https://azure.microsoft.com/pricing/license-mobility/).
7. **Can I change a VM to use my own SQL Server license if it was created from one of the pay-as-you-go gallery images?**

    No. You can not switch from pay-per-minute licensing to using your own license. Create a new Azure virtual machine using one of the [BYOL images](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), and then migrate your databases to the new server using standard [data migration techniques](virtual-machines-windows-migrate-sql.md).

7. **Are SQL Server Failover Cluster Instances (FCI) supported on Azure VMs?**

   Yes. You can [create a Windows Failover Cluster on Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) and use Storage Spaces Direct (S2D) for the cluster storage. Alternatively, you can use third-party clustering or storage solutions as described in [High availability and disaster recovery for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

7. **Do I have to pay to license SQL Server on an Azure VM if it is only being used for standby/failover?**
   
    You do not have to pay to license one SQL Server participating as a passive secondary replica in an HA deployment, if you have Software Assurance and use License Mobility as described in [Virtual Machine Licensing FAQ](http://azure.microsoft.com/pricing/licensing-faq/).
    
8. **How are updates and service packs applied on a SQL Server VM?**
   
    Virtual machines give you control over the host machine, including when and how you apply updates. For the operating system, you can manually apply windows updates, or you can enable a scheduling service called [Automated Patching](virtual-machines-windows-sql-automated-patching.md). Automated Patching installs any updates that are marked important, including SQL Server updates in that category. Other optional updates to SQL Server must be installed manually.
9. **Is it possible to set up configurations not shown in the virtual machine gallery (For example Windows 2008 R2 + SQL Server 2012)?**
   
    No. For virtual machine gallery images that include SQL Server, you must select one of the provided images.
10. **How do I install SQL Data tools on my Azure VM?**
    
     Download and install the SQL Data tools from [Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013 ](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Resources
For an overview of SQL Server on Azure Virtual Machines, watch the video [Azure VM is the best platform for SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). You can also get a good introduction in the topic, [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).

Other resources include:

* [Provision a SQL Server virtual machine in the Azure Portal](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrating a Database to SQL Server on an Azure VM](virtual-machines-windows-migrate-sql.md)
* [High Availability and Disaster Recovery for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md)
* [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md)
* [Application Patterns and Development Strategies for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md)

