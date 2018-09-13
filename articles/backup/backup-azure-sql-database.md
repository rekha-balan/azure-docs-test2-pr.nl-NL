---
title: Back up SQL Server databases to Azure | Microsoft Docs
description: This tutorial explains how to back up SQL Server to Azure. The article also explains SQL Server recovery.
services: backup
documentationcenter: ''
author: markgalioto
manager: carmonm
editor: ''
keywords: ''
ms.assetid: ''
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2018
ms.author: markgal;anuragm
ms.custom: ''
ms.openlocfilehash: c3321fb64c423b1b3c80f48fb97a70cc7dbc83f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966249"
---
# <a name="back-up-sql-server-databases-to-azure"></a><span data-ttu-id="2b217-104">Back up SQL Server databases to Azure</span><span class="sxs-lookup"><span data-stu-id="2b217-104">Back up SQL Server databases to Azure</span></span>

<span data-ttu-id="2b217-105">SQL Server databases are critical workloads that require a low recovery point objective (RPO) and long-term retention.</span><span class="sxs-lookup"><span data-stu-id="2b217-105">SQL Server databases are critical workloads that require a low recovery point objective (RPO) and long-term retention.</span></span> <span data-ttu-id="2b217-106">Azure Backup provides a SQL Server backup solution that requires zero infrastructure: no complex backup server, no management agent, and no backup storage to manage.</span><span class="sxs-lookup"><span data-stu-id="2b217-106">Azure Backup provides a SQL Server backup solution that requires zero infrastructure: no complex backup server, no management agent, and no backup storage to manage.</span></span> <span data-ttu-id="2b217-107">Azure Backup provides centralized management for your backups across all servers that are running SQL Server, or even different workloads.</span><span class="sxs-lookup"><span data-stu-id="2b217-107">Azure Backup provides centralized management for your backups across all servers that are running SQL Server, or even different workloads.</span></span>

<span data-ttu-id="2b217-108">In this article, you learn:</span><span class="sxs-lookup"><span data-stu-id="2b217-108">In this article, you learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b217-109">The prerequisites to back up a SQL Server instance to Azure.</span><span class="sxs-lookup"><span data-stu-id="2b217-109">The prerequisites to back up a SQL Server instance to Azure.</span></span>
> * <span data-ttu-id="2b217-110">How to create and use a Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-110">How to create and use a Recovery Services vault.</span></span>
> * <span data-ttu-id="2b217-111">How to configure SQL Server database backups.</span><span class="sxs-lookup"><span data-stu-id="2b217-111">How to configure SQL Server database backups.</span></span>
> * <span data-ttu-id="2b217-112">How to set a backup (or retention) policy for the recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-112">How to set a backup (or retention) policy for the recovery points.</span></span>
> * <span data-ttu-id="2b217-113">How to restore the database.</span><span class="sxs-lookup"><span data-stu-id="2b217-113">How to restore the database.</span></span>

<span data-ttu-id="2b217-114">Before you start the procedures in this article, you should have a SQL Server instance that's running in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b217-114">Before you start the procedures in this article, you should have a SQL Server instance that's running in Azure.</span></span> <span data-ttu-id="2b217-115">[Use SQL Marketplace virtual machines to quickly create a SQL Server instance](../sql-database/sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2b217-115">[Use SQL Marketplace virtual machines to quickly create a SQL Server instance](../sql-database/sql-database-get-started-portal.md).</span></span>

## <a name="public-preview-limitations"></a><span data-ttu-id="2b217-116">Public Preview limitations</span><span class="sxs-lookup"><span data-stu-id="2b217-116">Public Preview limitations</span></span>

<span data-ttu-id="2b217-117">The following items are known limitations for the Public Preview:</span><span class="sxs-lookup"><span data-stu-id="2b217-117">The following items are known limitations for the Public Preview:</span></span>

- <span data-ttu-id="2b217-118">The SQL virtual machine (VM) requires internet connectivity to access Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="2b217-118">The SQL virtual machine (VM) requires internet connectivity to access Azure public IP addresses.</span></span> <span data-ttu-id="2b217-119">For details, see [Establish network connectivity](backup-azure-sql-database.md#establish-network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="2b217-119">For details, see [Establish network connectivity](backup-azure-sql-database.md#establish-network-connectivity).</span></span>
- <span data-ttu-id="2b217-120">Protect up to 2,000 SQL databases in one Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-120">Protect up to 2,000 SQL databases in one Recovery Services vault.</span></span> <span data-ttu-id="2b217-121">Additional SQL databases should be stored in a separate Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-121">Additional SQL databases should be stored in a separate Recovery Services vault.</span></span>
- <span data-ttu-id="2b217-122">[Backups of distributed availability groups](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups?view=sql-server-2017) have limitations.</span><span class="sxs-lookup"><span data-stu-id="2b217-122">[Backups of distributed availability groups](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/distributed-availability-groups?view=sql-server-2017) have limitations.</span></span>
- <span data-ttu-id="2b217-123">SQL Server Always On Failover Cluster Instances (FCIs) aren't supported.</span><span class="sxs-lookup"><span data-stu-id="2b217-123">SQL Server Always On Failover Cluster Instances (FCIs) aren't supported.</span></span>
- <span data-ttu-id="2b217-124">Use the Azure portal to configure Azure Backup to protect SQL Server databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-124">Use the Azure portal to configure Azure Backup to protect SQL Server databases.</span></span> <span data-ttu-id="2b217-125">Azure PowerShell, the Azure CLI, and the REST APIs aren't currently supported.</span><span class="sxs-lookup"><span data-stu-id="2b217-125">Azure PowerShell, the Azure CLI, and the REST APIs aren't currently supported.</span></span>

<span data-ttu-id="2b217-126">Please refer to [FAQ section](https://docs.microsoft.com/azure/backup/backup-azure-sql-database#faq) for more details on support/not supported scenarios.</span><span class="sxs-lookup"><span data-stu-id="2b217-126">Please refer to [FAQ section](https://docs.microsoft.com/azure/backup/backup-azure-sql-database#faq) for more details on support/not supported scenarios.</span></span>

## <a name="support-for-azure-geos"></a><span data-ttu-id="2b217-127">Support for Azure geos</span><span class="sxs-lookup"><span data-stu-id="2b217-127">Support for Azure geos</span></span>

<span data-ttu-id="2b217-128">Azure Backup is supported for the following geos:</span><span class="sxs-lookup"><span data-stu-id="2b217-128">Azure Backup is supported for the following geos:</span></span>

- <span data-ttu-id="2b217-129">Australia South East (ASE)</span><span class="sxs-lookup"><span data-stu-id="2b217-129">Australia South East (ASE)</span></span> 
- <span data-ttu-id="2b217-130">Brazil South (BRS)</span><span class="sxs-lookup"><span data-stu-id="2b217-130">Brazil South (BRS)</span></span>
- <span data-ttu-id="2b217-131">Canada Central (CNC)</span><span class="sxs-lookup"><span data-stu-id="2b217-131">Canada Central (CNC)</span></span>
- <span data-ttu-id="2b217-132">Canada East (CE)</span><span class="sxs-lookup"><span data-stu-id="2b217-132">Canada East (CE)</span></span>
- <span data-ttu-id="2b217-133">Central US (CUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-133">Central US (CUS)</span></span>
- <span data-ttu-id="2b217-134">East Asia (EA)</span><span class="sxs-lookup"><span data-stu-id="2b217-134">East Asia (EA)</span></span>
- <span data-ttu-id="2b217-135">East Australia (AE)</span><span class="sxs-lookup"><span data-stu-id="2b217-135">East Australia (AE)</span></span> 
- <span data-ttu-id="2b217-136">East US (EUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-136">East US (EUS)</span></span>
- <span data-ttu-id="2b217-137">East US 2 (EUS2)</span><span class="sxs-lookup"><span data-stu-id="2b217-137">East US 2 (EUS2)</span></span>
- <span data-ttu-id="2b217-138">India Central (INC)</span><span class="sxs-lookup"><span data-stu-id="2b217-138">India Central (INC)</span></span> 
- <span data-ttu-id="2b217-139">India South (INS)</span><span class="sxs-lookup"><span data-stu-id="2b217-139">India South (INS)</span></span>
- <span data-ttu-id="2b217-140">Japan East (JPE)</span><span class="sxs-lookup"><span data-stu-id="2b217-140">Japan East (JPE)</span></span>
- <span data-ttu-id="2b217-141">Japan West (JPW)</span><span class="sxs-lookup"><span data-stu-id="2b217-141">Japan West (JPW)</span></span>
- <span data-ttu-id="2b217-142">Korea Central (KRC)</span><span class="sxs-lookup"><span data-stu-id="2b217-142">Korea Central (KRC)</span></span>
- <span data-ttu-id="2b217-143">Korea South (KRS)</span><span class="sxs-lookup"><span data-stu-id="2b217-143">Korea South (KRS)</span></span>
- <span data-ttu-id="2b217-144">North Central US (NCUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-144">North Central US (NCUS)</span></span> 
- <span data-ttu-id="2b217-145">North Europe (NE)</span><span class="sxs-lookup"><span data-stu-id="2b217-145">North Europe (NE)</span></span> 
- <span data-ttu-id="2b217-146">South Central US (SCUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-146">South Central US (SCUS)</span></span> 
- <span data-ttu-id="2b217-147">South East Asia (SEA)</span><span class="sxs-lookup"><span data-stu-id="2b217-147">South East Asia (SEA)</span></span>
- <span data-ttu-id="2b217-148">UK South (UKS)</span><span class="sxs-lookup"><span data-stu-id="2b217-148">UK South (UKS)</span></span> 
- <span data-ttu-id="2b217-149">UK West (UKW)</span><span class="sxs-lookup"><span data-stu-id="2b217-149">UK West (UKW)</span></span> 
- <span data-ttu-id="2b217-150">West Central US (WCUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-150">West Central US (WCUS)</span></span>
- <span data-ttu-id="2b217-151">West Europe (WE)</span><span class="sxs-lookup"><span data-stu-id="2b217-151">West Europe (WE)</span></span> 
- <span data-ttu-id="2b217-152">West US (WUS)</span><span class="sxs-lookup"><span data-stu-id="2b217-152">West US (WUS)</span></span>
- <span data-ttu-id="2b217-153">West US 2 (WUS 2)</span><span class="sxs-lookup"><span data-stu-id="2b217-153">West US 2 (WUS 2)</span></span> 

## <a name="support-for-operating-systems-and-sql-server-versions"></a><span data-ttu-id="2b217-154">Support for operating systems and SQL Server versions</span><span class="sxs-lookup"><span data-stu-id="2b217-154">Support for operating systems and SQL Server versions</span></span>

<span data-ttu-id="2b217-155">This section describes Azure Backup support for operating systems and versions of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2b217-155">This section describes Azure Backup support for operating systems and versions of SQL Server.</span></span> <span data-ttu-id="2b217-156">SQL Marketplace Azure virtual machines and non-Marketplace virtual machines (where SQL Server is manually installed) are supported.</span><span class="sxs-lookup"><span data-stu-id="2b217-156">SQL Marketplace Azure virtual machines and non-Marketplace virtual machines (where SQL Server is manually installed) are supported.</span></span>

### <a name="supported-operating-systems"></a><span data-ttu-id="2b217-157">Supported operating systems</span><span class="sxs-lookup"><span data-stu-id="2b217-157">Supported operating systems</span></span>

- <span data-ttu-id="2b217-158">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="2b217-158">Windows Server 2012</span></span>
- <span data-ttu-id="2b217-159">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="2b217-159">Windows Server 2012 R2</span></span>
- <span data-ttu-id="2b217-160">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="2b217-160">Windows Server 2016</span></span>

<span data-ttu-id="2b217-161">Linux isn't currently supported.</span><span class="sxs-lookup"><span data-stu-id="2b217-161">Linux isn't currently supported.</span></span>

### <a name="supported-sql-server-versions-and-editions"></a><span data-ttu-id="2b217-162">Supported SQL Server versions and editions</span><span class="sxs-lookup"><span data-stu-id="2b217-162">Supported SQL Server versions and editions</span></span>

- <span data-ttu-id="2b217-163">SQL Server 2012 Enterprise, Standard, Web, Developer, Express</span><span class="sxs-lookup"><span data-stu-id="2b217-163">SQL Server 2012 Enterprise, Standard, Web, Developer, Express</span></span>
- <span data-ttu-id="2b217-164">SQL Server 2014 Enterprise, Standard, Web, Developer, Express</span><span class="sxs-lookup"><span data-stu-id="2b217-164">SQL Server 2014 Enterprise, Standard, Web, Developer, Express</span></span>
- <span data-ttu-id="2b217-165">SQL Server 2016 Enterprise, Standard, Web, Developer, Express</span><span class="sxs-lookup"><span data-stu-id="2b217-165">SQL Server 2016 Enterprise, Standard, Web, Developer, Express</span></span>
- <span data-ttu-id="2b217-166">SQL Server 2017 Enterprise, Standard, Web, Developer, Express</span><span class="sxs-lookup"><span data-stu-id="2b217-166">SQL Server 2017 Enterprise, Standard, Web, Developer, Express</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b217-167">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2b217-167">Prerequisites</span></span>

<span data-ttu-id="2b217-168">Before you back up your SQL Server database, check the following conditions:</span><span class="sxs-lookup"><span data-stu-id="2b217-168">Before you back up your SQL Server database, check the following conditions:</span></span>

- <span data-ttu-id="2b217-169">Identify or [create a Recovery Services vault](backup-azure-sql-database.md#create-a-recovery-services-vault) in the same region or locale as the virtual machine that hosts your SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="2b217-169">Identify or [create a Recovery Services vault](backup-azure-sql-database.md#create-a-recovery-services-vault) in the same region or locale as the virtual machine that hosts your SQL Server instance.</span></span>
- <span data-ttu-id="2b217-170">[Check the permissions on the virtual machine](backup-azure-sql-database.md#set-permissions-for-non-marketplace-sql-vms) that are needed to back up the SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-170">[Check the permissions on the virtual machine](backup-azure-sql-database.md#set-permissions-for-non-marketplace-sql-vms) that are needed to back up the SQL databases.</span></span>
- <span data-ttu-id="2b217-171">Verify that the [SQL virtual machine has network connectivity](backup-azure-sql-database.md#establish-network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="2b217-171">Verify that the [SQL virtual machine has network connectivity](backup-azure-sql-database.md#establish-network-connectivity).</span></span>

> [!NOTE]
> <span data-ttu-id="2b217-172">You can have only one backup solution at a time to back up SQL Server databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-172">You can have only one backup solution at a time to back up SQL Server databases.</span></span> <span data-ttu-id="2b217-173">Disable all other SQL backups before you use this feature; otherwise, the backups will interfere and fail.</span><span class="sxs-lookup"><span data-stu-id="2b217-173">Disable all other SQL backups before you use this feature; otherwise, the backups will interfere and fail.</span></span> <span data-ttu-id="2b217-174">You can enable Azure Backup for IaaS VM along with SQL backup without any conflict.</span><span class="sxs-lookup"><span data-stu-id="2b217-174">You can enable Azure Backup for IaaS VM along with SQL backup without any conflict.</span></span>
>

<span data-ttu-id="2b217-175">If these conditions exist in your environment, continue to [Configure backup for SQL Server databases](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span><span class="sxs-lookup"><span data-stu-id="2b217-175">If these conditions exist in your environment, continue to [Configure backup for SQL Server databases](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span></span> <span data-ttu-id="2b217-176">If any of the prerequisites don't exist, continue reading.</span><span class="sxs-lookup"><span data-stu-id="2b217-176">If any of the prerequisites don't exist, continue reading.</span></span>


## <a name="establish-network-connectivity"></a><span data-ttu-id="2b217-177">Establish network connectivity</span><span class="sxs-lookup"><span data-stu-id="2b217-177">Establish network connectivity</span></span>

<span data-ttu-id="2b217-178">For all operations, the SQL virtual machine needs connectivity to Azure public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="2b217-178">For all operations, the SQL virtual machine needs connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="2b217-179">SQL virtual machine operations (such as database discovery, configure backups, schedule backups, restore recovery points, and so on) fail without connectivity to the public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="2b217-179">SQL virtual machine operations (such as database discovery, configure backups, schedule backups, restore recovery points, and so on) fail without connectivity to the public IP addresses.</span></span> <span data-ttu-id="2b217-180">Use either of the following options to provide a clear path for backup traffic:</span><span class="sxs-lookup"><span data-stu-id="2b217-180">Use either of the following options to provide a clear path for backup traffic:</span></span>

- <span data-ttu-id="2b217-181">Whitelist the Azure datacenter IP ranges: To whitelist the Azure datacenter IP ranges, use the [Download Center page for details on the IP ranges and instructions](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2b217-181">Whitelist the Azure datacenter IP ranges: To whitelist the Azure datacenter IP ranges, use the [Download Center page for details on the IP ranges and instructions](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> 
- <span data-ttu-id="2b217-182">Deploy an HTTP proxy server to route traffic: When you back up a SQL database in a VM, the backup extension on the VM uses the HTTPS APIs to send management commands to Azure Backup and data to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2b217-182">Deploy an HTTP proxy server to route traffic: When you back up a SQL database in a VM, the backup extension on the VM uses the HTTPS APIs to send management commands to Azure Backup and data to Azure Storage.</span></span> <span data-ttu-id="2b217-183">The backup extension also uses Azure Active Directory (Azure AD) for authentication.</span><span class="sxs-lookup"><span data-stu-id="2b217-183">The backup extension also uses Azure Active Directory (Azure AD) for authentication.</span></span> <span data-ttu-id="2b217-184">Route the backup extension traffic for these three services through the HTTP proxy.</span><span class="sxs-lookup"><span data-stu-id="2b217-184">Route the backup extension traffic for these three services through the HTTP proxy.</span></span> <span data-ttu-id="2b217-185">The extension's the only component that's configured for access to the public internet.</span><span class="sxs-lookup"><span data-stu-id="2b217-185">The extension's the only component that's configured for access to the public internet.</span></span>

<span data-ttu-id="2b217-186">The tradeoffs between the options are manageability, granular control, and cost.</span><span class="sxs-lookup"><span data-stu-id="2b217-186">The tradeoffs between the options are manageability, granular control, and cost.</span></span>

> [!NOTE]
> <span data-ttu-id="2b217-187">Service tags for Azure Backup should be available by General Availability.</span><span class="sxs-lookup"><span data-stu-id="2b217-187">Service tags for Azure Backup should be available by General Availability.</span></span>
>

| <span data-ttu-id="2b217-188">Option</span><span class="sxs-lookup"><span data-stu-id="2b217-188">Option</span></span> | <span data-ttu-id="2b217-189">Advantages</span><span class="sxs-lookup"><span data-stu-id="2b217-189">Advantages</span></span> | <span data-ttu-id="2b217-190">Disadvantages</span><span class="sxs-lookup"><span data-stu-id="2b217-190">Disadvantages</span></span> |
| ------ | ---------- | ------------- |
| <span data-ttu-id="2b217-191">Whitelist IP ranges</span><span class="sxs-lookup"><span data-stu-id="2b217-191">Whitelist IP ranges</span></span> | <span data-ttu-id="2b217-192">No additional costs.</span><span class="sxs-lookup"><span data-stu-id="2b217-192">No additional costs.</span></span> <br/> <span data-ttu-id="2b217-193">For access to open in an NSG, use the **Set-AzureNetworkSecurityRule** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b217-193">For access to open in an NSG, use the **Set-AzureNetworkSecurityRule** cmdlet.</span></span> | <span data-ttu-id="2b217-194">Complex to manage because the affected IP ranges change over time.</span><span class="sxs-lookup"><span data-stu-id="2b217-194">Complex to manage because the affected IP ranges change over time.</span></span> <br/><span data-ttu-id="2b217-195">Provides access to the whole of Azure, not just Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="2b217-195">Provides access to the whole of Azure, not just Azure Storage.</span></span>|
| <span data-ttu-id="2b217-196">Use an HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="2b217-196">Use an HTTP proxy</span></span>   | <span data-ttu-id="2b217-197">Granular control in the proxy over the storage URLs is allowed.</span><span class="sxs-lookup"><span data-stu-id="2b217-197">Granular control in the proxy over the storage URLs is allowed.</span></span> <br/><span data-ttu-id="2b217-198">Single point of internet access to VMs.</span><span class="sxs-lookup"><span data-stu-id="2b217-198">Single point of internet access to VMs.</span></span> <br/> <span data-ttu-id="2b217-199">Not subject to Azure IP address changes.</span><span class="sxs-lookup"><span data-stu-id="2b217-199">Not subject to Azure IP address changes.</span></span> | <span data-ttu-id="2b217-200">Additional costs to run a VM with the proxy software.</span><span class="sxs-lookup"><span data-stu-id="2b217-200">Additional costs to run a VM with the proxy software.</span></span> |

## <a name="set-permissions-for-non-marketplace-sql-vms"></a><span data-ttu-id="2b217-201">Set permissions for non-Marketplace SQL VMs</span><span class="sxs-lookup"><span data-stu-id="2b217-201">Set permissions for non-Marketplace SQL VMs</span></span>

<span data-ttu-id="2b217-202">To back up a virtual machine, Azure Backup requires the **AzureBackupWindowsWorkload** extension to be installed.</span><span class="sxs-lookup"><span data-stu-id="2b217-202">To back up a virtual machine, Azure Backup requires the **AzureBackupWindowsWorkload** extension to be installed.</span></span> <span data-ttu-id="2b217-203">If you use Azure Marketplace virtual machines, continue to [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases).</span><span class="sxs-lookup"><span data-stu-id="2b217-203">If you use Azure Marketplace virtual machines, continue to [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases).</span></span> <span data-ttu-id="2b217-204">If the virtual machine that hosts your SQL databases isn't created from the Azure Marketplace, complete the following procedure to install the extension and set the appropriate permissions.</span><span class="sxs-lookup"><span data-stu-id="2b217-204">If the virtual machine that hosts your SQL databases isn't created from the Azure Marketplace, complete the following procedure to install the extension and set the appropriate permissions.</span></span> <span data-ttu-id="2b217-205">In addition to the **AzureBackupWindowsWorkload** extension, Azure Backup requires SQL sysadmin privileges to protect SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-205">In addition to the **AzureBackupWindowsWorkload** extension, Azure Backup requires SQL sysadmin privileges to protect SQL databases.</span></span> <span data-ttu-id="2b217-206">To discover databases on the virtual machine, Azure Backup creates the account **NT Service\AzureWLBackupPluginSvc**.</span><span class="sxs-lookup"><span data-stu-id="2b217-206">To discover databases on the virtual machine, Azure Backup creates the account **NT Service\AzureWLBackupPluginSvc**.</span></span> <span data-ttu-id="2b217-207">For Azure Backup to discover SQL databases, the **NT Service\AzureWLBackupPluginSvc** account must have SQL and SQL sysadmin permissions.</span><span class="sxs-lookup"><span data-stu-id="2b217-207">For Azure Backup to discover SQL databases, the **NT Service\AzureWLBackupPluginSvc** account must have SQL and SQL sysadmin permissions.</span></span> <span data-ttu-id="2b217-208">The following procedure explains how to provide these permissions.</span><span class="sxs-lookup"><span data-stu-id="2b217-208">The following procedure explains how to provide these permissions.</span></span>

<span data-ttu-id="2b217-209">To configure permissions:</span><span class="sxs-lookup"><span data-stu-id="2b217-209">To configure permissions:</span></span>

1. <span data-ttu-id="2b217-210">In the [Azure portal](https://portal.azure.com), open the Recovery Services vault that you use to protect the SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-210">In the [Azure portal](https://portal.azure.com), open the Recovery Services vault that you use to protect the SQL databases.</span></span>

2. <span data-ttu-id="2b217-211">On the **Recovery Services vault** dashboard, select **Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-211">On the **Recovery Services vault** dashboard, select **Backup**.</span></span> <span data-ttu-id="2b217-212">The **Backup Goal** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-212">The **Backup Goal** menu opens.</span></span>

   ![Select Backup to open the Backup Goal menu](./media/backup-azure-sql-database/open-backup-menu.png)

3. <span data-ttu-id="2b217-214">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b217-214">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span></span>

4. <span data-ttu-id="2b217-215">Expand the **What do you want to backup** drop-down list box and select **SQL Server in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-215">Expand the **What do you want to backup** drop-down list box and select **SQL Server in Azure VM**.</span></span>

    ![Select SQL Server in Azure VM for the backup](./media/backup-azure-sql-database/choose-sql-database-backup-goal.png)

    <span data-ttu-id="2b217-217">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-217">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span></span> <span data-ttu-id="2b217-218">The **Discover DBs in VMs** step start a search for Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2b217-218">The **Discover DBs in VMs** step start a search for Azure virtual machines.</span></span>

    ![Review the two Backup Goal steps](./media/backup-azure-sql-database/backup-goal-menu-step-one.png)

5. <span data-ttu-id="2b217-220">Under **Discover DBs in VMs**, select **Start Discovery** to search for unprotected virtual machines in the subscription.</span><span class="sxs-lookup"><span data-stu-id="2b217-220">Under **Discover DBs in VMs**, select **Start Discovery** to search for unprotected virtual machines in the subscription.</span></span> <span data-ttu-id="2b217-221">It can take a while to search all of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2b217-221">It can take a while to search all of the virtual machines.</span></span> <span data-ttu-id="2b217-222">The search time depends on the number of unprotected virtual machines in the subscription.</span><span class="sxs-lookup"><span data-stu-id="2b217-222">The search time depends on the number of unprotected virtual machines in the subscription.</span></span>

    ![Backup is pending during search for DBs in VMs](./media/backup-azure-sql-database/discovering-sql-databases.png)
 
    <span data-ttu-id="2b217-224">After an unprotected virtual machine is discovered, it appears in the list.</span><span class="sxs-lookup"><span data-stu-id="2b217-224">After an unprotected virtual machine is discovered, it appears in the list.</span></span> <span data-ttu-id="2b217-225">Unprotected virtual machines are listed by their virtual machine name and resource group.</span><span class="sxs-lookup"><span data-stu-id="2b217-225">Unprotected virtual machines are listed by their virtual machine name and resource group.</span></span> <span data-ttu-id="2b217-226">It's possible for multiple virtual machines to have the same name.</span><span class="sxs-lookup"><span data-stu-id="2b217-226">It's possible for multiple virtual machines to have the same name.</span></span> <span data-ttu-id="2b217-227">However, virtual machines with the same name belong to different resource groups.</span><span class="sxs-lookup"><span data-stu-id="2b217-227">However, virtual machines with the same name belong to different resource groups.</span></span> <span data-ttu-id="2b217-228">If an expected virtual machine isn't listed, see if the virtual machine's already protected to a vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-228">If an expected virtual machine isn't listed, see if the virtual machine's already protected to a vault.</span></span>

6. <span data-ttu-id="2b217-229">In the list of virtual machines, select the VM that has the SQL database to back up, and then select **Discover DBs**.</span><span class="sxs-lookup"><span data-stu-id="2b217-229">In the list of virtual machines, select the VM that has the SQL database to back up, and then select **Discover DBs**.</span></span> 

    <span data-ttu-id="2b217-230">The discovery process installs the **AzureBackupWindowsWorkload** extension on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-230">The discovery process installs the **AzureBackupWindowsWorkload** extension on the virtual machine.</span></span> <span data-ttu-id="2b217-231">The extension allows the Azure Backup service to communicate with the virtual machine so it can back up the SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-231">The extension allows the Azure Backup service to communicate with the virtual machine so it can back up the SQL databases.</span></span> <span data-ttu-id="2b217-232">After the extension installs, Azure Backup creates the Windows virtual service account **NT Service\AzureWLBackupPluginSvc** on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-232">After the extension installs, Azure Backup creates the Windows virtual service account **NT Service\AzureWLBackupPluginSvc** on the virtual machine.</span></span> <span data-ttu-id="2b217-233">The virtual service account requires SQL sysadmin permission.</span><span class="sxs-lookup"><span data-stu-id="2b217-233">The virtual service account requires SQL sysadmin permission.</span></span> <span data-ttu-id="2b217-234">During the virtual service account installation process, if you receive the error `UserErrorSQLNoSysadminMembership`, see [Fix SQL sysadmin permissions](backup-azure-sql-database.md#fix-sql-sysadmin-permissions).</span><span class="sxs-lookup"><span data-stu-id="2b217-234">During the virtual service account installation process, if you receive the error `UserErrorSQLNoSysadminMembership`, see [Fix SQL sysadmin permissions](backup-azure-sql-database.md#fix-sql-sysadmin-permissions).</span></span>

    <span data-ttu-id="2b217-235">The **Notifications** area shows the progress of the database discovery.</span><span class="sxs-lookup"><span data-stu-id="2b217-235">The **Notifications** area shows the progress of the database discovery.</span></span> <span data-ttu-id="2b217-236">It can take a while for the job to complete.</span><span class="sxs-lookup"><span data-stu-id="2b217-236">It can take a while for the job to complete.</span></span> <span data-ttu-id="2b217-237">The job time depends on how many databases are on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-237">The job time depends on how many databases are on the virtual machine.</span></span> <span data-ttu-id="2b217-238">When the selected databases are discovered, a success message appears.</span><span class="sxs-lookup"><span data-stu-id="2b217-238">When the selected databases are discovered, a success message appears.</span></span>

    ![Deployment success message](./media/backup-azure-sql-database/notifications-db-discovered.png)

<span data-ttu-id="2b217-240">After you associate the database with the Recovery Services vault, the next step is to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span><span class="sxs-lookup"><span data-stu-id="2b217-240">After you associate the database with the Recovery Services vault, the next step is to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span></span>

### <a name="fix-sql-sysadmin-permissions"></a><span data-ttu-id="2b217-241">Fix SQL sysadmin permissions</span><span class="sxs-lookup"><span data-stu-id="2b217-241">Fix SQL sysadmin permissions</span></span>

<span data-ttu-id="2b217-242">During the installation process, if you receive the error `UserErrorSQLNoSysadminMembership`, use an account with SQL Server sysadmin permissions to sign in to SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="2b217-242">During the installation process, if you receive the error `UserErrorSQLNoSysadminMembership`, use an account with SQL Server sysadmin permissions to sign in to SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="2b217-243">Unless you need special permissions, Windows authentication should work.</span><span class="sxs-lookup"><span data-stu-id="2b217-243">Unless you need special permissions, Windows authentication should work.</span></span>

1. <span data-ttu-id="2b217-244">On the SQL Server, open the Security/Logins folder.</span><span class="sxs-lookup"><span data-stu-id="2b217-244">On the SQL Server, open the Security/Logins folder.</span></span>

    ![Open the Security/Logins folder to see accounts](./media/backup-azure-sql-database/security-login-list.png)

2. <span data-ttu-id="2b217-246">Right-click the Logins folder and select **New Login**.</span><span class="sxs-lookup"><span data-stu-id="2b217-246">Right-click the Logins folder and select **New Login**.</span></span> <span data-ttu-id="2b217-247">In the **Login - New** dialog box, select **Search**.</span><span class="sxs-lookup"><span data-stu-id="2b217-247">In the **Login - New** dialog box, select **Search**.</span></span>

    ![In the Login - New dialog box, select Search](./media/backup-azure-sql-database/new-login-search.png)

3. <span data-ttu-id="2b217-249">The Windows virtual service account **NT Service\AzureWLBackupPluginSvc** was created during the virtual machine registration and SQL discovery phase.</span><span class="sxs-lookup"><span data-stu-id="2b217-249">The Windows virtual service account **NT Service\AzureWLBackupPluginSvc** was created during the virtual machine registration and SQL discovery phase.</span></span> <span data-ttu-id="2b217-250">Enter the account name as shown in the **Enter the object name to select** box.</span><span class="sxs-lookup"><span data-stu-id="2b217-250">Enter the account name as shown in the **Enter the object name to select** box.</span></span> <span data-ttu-id="2b217-251">Select **Check Names** to resolve the name.</span><span class="sxs-lookup"><span data-stu-id="2b217-251">Select **Check Names** to resolve the name.</span></span> 

    ![Select Check Names to resolve the unknown service name](./media/backup-azure-sql-database/check-name.png)

4. <span data-ttu-id="2b217-253">Select **OK** to close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="2b217-253">Select **OK** to close the dialog box.</span></span>

5. <span data-ttu-id="2b217-254">In the **Server Roles** box, make sure the **sysadmin** role is selected.</span><span class="sxs-lookup"><span data-stu-id="2b217-254">In the **Server Roles** box, make sure the **sysadmin** role is selected.</span></span> <span data-ttu-id="2b217-255">Select **OK** to close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="2b217-255">Select **OK** to close the dialog box.</span></span>

    ![Make sure the sysadmin server role is selected](./media/backup-azure-sql-database/sysadmin-server-role.png)

    <span data-ttu-id="2b217-257">The required permissions should now exist.</span><span class="sxs-lookup"><span data-stu-id="2b217-257">The required permissions should now exist.</span></span>

6. <span data-ttu-id="2b217-258">Although you fixed the permissions error, you need to associate the database with the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-258">Although you fixed the permissions error, you need to associate the database with the Recovery Services vault.</span></span> <span data-ttu-id="2b217-259">In the Azure portal, in the **Protected Servers** list, right-click the server that's in an error state and select **Rediscover DBs**.</span><span class="sxs-lookup"><span data-stu-id="2b217-259">In the Azure portal, in the **Protected Servers** list, right-click the server that's in an error state and select **Rediscover DBs**.</span></span>

    ![Verify the server has appropriate permissions](./media/backup-azure-sql-database/check-erroneous-server.png)

    <span data-ttu-id="2b217-261">The **Notifications** area shows the progress of the database discovery.</span><span class="sxs-lookup"><span data-stu-id="2b217-261">The **Notifications** area shows the progress of the database discovery.</span></span> <span data-ttu-id="2b217-262">It can take a while for the job to complete.</span><span class="sxs-lookup"><span data-stu-id="2b217-262">It can take a while for the job to complete.</span></span> <span data-ttu-id="2b217-263">The job time depends on how many databases are on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-263">The job time depends on how many databases are on the virtual machine.</span></span> <span data-ttu-id="2b217-264">When the selected databases are found, a success message appears.</span><span class="sxs-lookup"><span data-stu-id="2b217-264">When the selected databases are found, a success message appears.</span></span>

    ![Deployment success message](./media/backup-azure-sql-database/notifications-db-discovered.png)

<span data-ttu-id="2b217-266">After you associate the database with the Recovery Services vault, the next step is to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span><span class="sxs-lookup"><span data-stu-id="2b217-266">After you associate the database with the Recovery Services vault, the next step is to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span></span>

[!INCLUDE [How to create a Recovery Services vault](../../includes/backup-create-rs-vault.md)]

## <a name="discover-sql-server-databases"></a><span data-ttu-id="2b217-267">Discover SQL Server databases</span><span class="sxs-lookup"><span data-stu-id="2b217-267">Discover SQL Server databases</span></span>

<span data-ttu-id="2b217-268">Azure Backup discovers all databases on a SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="2b217-268">Azure Backup discovers all databases on a SQL Server instance.</span></span> <span data-ttu-id="2b217-269">You can protect the databases according to your backup requirements.</span><span class="sxs-lookup"><span data-stu-id="2b217-269">You can protect the databases according to your backup requirements.</span></span> <span data-ttu-id="2b217-270">Use the following procedure to identify the virtual machine that hosts the SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-270">Use the following procedure to identify the virtual machine that hosts the SQL databases.</span></span> <span data-ttu-id="2b217-271">After you identify the virtual machine, Azure Backup installs a lightweight extension to discover the SQL Server databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-271">After you identify the virtual machine, Azure Backup installs a lightweight extension to discover the SQL Server databases.</span></span>

1. <span data-ttu-id="2b217-272">Sign in to your subscription in the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2b217-272">Sign in to your subscription in the [Azure portal](https://portal.azure.com/).</span></span>

2. <span data-ttu-id="2b217-273">On the left menu, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="2b217-273">On the left menu, select **All services**.</span></span>

    ![Select All services](./media/backup-azure-sql-database/click-all-services.png) <br/>

3. <span data-ttu-id="2b217-275">In the **All services** dialog box, enter **Recovery Services**.</span><span class="sxs-lookup"><span data-stu-id="2b217-275">In the **All services** dialog box, enter **Recovery Services**.</span></span> <span data-ttu-id="2b217-276">As you type, your input filters the list of resources.</span><span class="sxs-lookup"><span data-stu-id="2b217-276">As you type, your input filters the list of resources.</span></span> <span data-ttu-id="2b217-277">Select **Recovery Services vaults** in the list.</span><span class="sxs-lookup"><span data-stu-id="2b217-277">Select **Recovery Services vaults** in the list.</span></span>

    ![Enter and choose Recovery Services vaults](./media/backup-azure-sql-database/all-services.png) <br/>

    <span data-ttu-id="2b217-279">The list of Recovery Services vaults in the subscription appears.</span><span class="sxs-lookup"><span data-stu-id="2b217-279">The list of Recovery Services vaults in the subscription appears.</span></span> 

4. <span data-ttu-id="2b217-280">In the list of Recovery Services vaults, select the vault to use to protect your SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-280">In the list of Recovery Services vaults, select the vault to use to protect your SQL databases.</span></span>

5. <span data-ttu-id="2b217-281">On the **Recovery Services vault** dashboard, select **Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-281">On the **Recovery Services vault** dashboard, select **Backup**.</span></span> <span data-ttu-id="2b217-282">The **Backup Goal** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-282">The **Backup Goal** menu opens.</span></span>

   ![Select Backup to open the Backup Goal menu](./media/backup-azure-sql-database/open-backup-menu.png)

6. <span data-ttu-id="2b217-284">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b217-284">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span></span>

7. <span data-ttu-id="2b217-285">Expand the **What do you want to back up** drop-down list box and select **SQL Server in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-285">Expand the **What do you want to back up** drop-down list box and select **SQL Server in Azure VM**.</span></span>

    ![Select SQL Server in Azure VM for the backup](./media/backup-azure-sql-database/choose-sql-database-backup-goal.png)

    <span data-ttu-id="2b217-287">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-287">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span></span>
    
    ![Review the two Backup Goal steps](./media/backup-azure-sql-database/backup-goal-menu-step-one.png)

8. <span data-ttu-id="2b217-289">Under **Discover DBs in VMs**, select **Start Discovery** to search for unprotected virtual machines in the subscription.</span><span class="sxs-lookup"><span data-stu-id="2b217-289">Under **Discover DBs in VMs**, select **Start Discovery** to search for unprotected virtual machines in the subscription.</span></span> <span data-ttu-id="2b217-290">It can take a while to search through all of the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2b217-290">It can take a while to search through all of the virtual machines.</span></span> <span data-ttu-id="2b217-291">The search time depends on the number of unprotected virtual machines in the subscription.</span><span class="sxs-lookup"><span data-stu-id="2b217-291">The search time depends on the number of unprotected virtual machines in the subscription.</span></span>

    ![Backup is pending during search for DBs in VMs](./media/backup-azure-sql-database/discovering-sql-databases.png)
 
    <span data-ttu-id="2b217-293">After an unprotected virtual machine is discovered, it appears in the list.</span><span class="sxs-lookup"><span data-stu-id="2b217-293">After an unprotected virtual machine is discovered, it appears in the list.</span></span> <span data-ttu-id="2b217-294">Multiple virtual machines can have the same name.</span><span class="sxs-lookup"><span data-stu-id="2b217-294">Multiple virtual machines can have the same name.</span></span> <span data-ttu-id="2b217-295">However, virtual machines with the same name belong to different resource groups.</span><span class="sxs-lookup"><span data-stu-id="2b217-295">However, virtual machines with the same name belong to different resource groups.</span></span> <span data-ttu-id="2b217-296">Unprotected virtual machines are listed by their virtual machine name and resource group.</span><span class="sxs-lookup"><span data-stu-id="2b217-296">Unprotected virtual machines are listed by their virtual machine name and resource group.</span></span> <span data-ttu-id="2b217-297">If an expected virtual machine isn't listed, see if that virtual machine's already protected to a vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-297">If an expected virtual machine isn't listed, see if that virtual machine's already protected to a vault.</span></span>

9. <span data-ttu-id="2b217-298">In the list of virtual machines, select the VM that has the SQL database to back up, and then select **Discover DBs**.</span><span class="sxs-lookup"><span data-stu-id="2b217-298">In the list of virtual machines, select the VM that has the SQL database to back up, and then select **Discover DBs**.</span></span>

    <span data-ttu-id="2b217-299">Azure Backup discovers all SQL databases on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-299">Azure Backup discovers all SQL databases on the virtual machine.</span></span> <span data-ttu-id="2b217-300">For information about what happens during the database discovery phase, see [Background operations](backup-azure-sql-database.md#background-operations).</span><span class="sxs-lookup"><span data-stu-id="2b217-300">For information about what happens during the database discovery phase, see [Background operations](backup-azure-sql-database.md#background-operations).</span></span> <span data-ttu-id="2b217-301">After the SQL databases are discovered, you're ready to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span><span class="sxs-lookup"><span data-stu-id="2b217-301">After the SQL databases are discovered, you're ready to [configure the backup job](backup-azure-sql-database.md#configure-backup-for-sql-server-databases).</span></span>

### <a name="background-operations"></a><span data-ttu-id="2b217-302">Background operations</span><span class="sxs-lookup"><span data-stu-id="2b217-302">Background operations</span></span>

<span data-ttu-id="2b217-303">When you use the **Discover DBs** tool, Azure Backup executes the following operations in the background:</span><span class="sxs-lookup"><span data-stu-id="2b217-303">When you use the **Discover DBs** tool, Azure Backup executes the following operations in the background:</span></span>

- <span data-ttu-id="2b217-304">Register the virtual machine with the Recovery Services vault for workload backup.</span><span class="sxs-lookup"><span data-stu-id="2b217-304">Register the virtual machine with the Recovery Services vault for workload backup.</span></span> <span data-ttu-id="2b217-305">All databases on the registered virtual machine can be backed up to this Recovery Services vault only.</span><span class="sxs-lookup"><span data-stu-id="2b217-305">All databases on the registered virtual machine can be backed up to this Recovery Services vault only.</span></span> 

- <span data-ttu-id="2b217-306">Install the **AzureBackupWindowsWorkload** extension on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-306">Install the **AzureBackupWindowsWorkload** extension on the virtual machine.</span></span> <span data-ttu-id="2b217-307">Back up of a SQL database is an agentless solution.</span><span class="sxs-lookup"><span data-stu-id="2b217-307">Back up of a SQL database is an agentless solution.</span></span> <span data-ttu-id="2b217-308">The extension is installed on the virtual machine and no agent's installed on the SQL database.</span><span class="sxs-lookup"><span data-stu-id="2b217-308">The extension is installed on the virtual machine and no agent's installed on the SQL database.</span></span>

- <span data-ttu-id="2b217-309">Create the service account **NT Service\AzureWLBackupPluginSvc** on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-309">Create the service account **NT Service\AzureWLBackupPluginSvc** on the virtual machine.</span></span> <span data-ttu-id="2b217-310">All backup and restore operations use the service account.</span><span class="sxs-lookup"><span data-stu-id="2b217-310">All backup and restore operations use the service account.</span></span> <span data-ttu-id="2b217-311">**NT Service\AzureWLBackupPluginSvc** needs SQL sysadmin permissions.</span><span class="sxs-lookup"><span data-stu-id="2b217-311">**NT Service\AzureWLBackupPluginSvc** needs SQL sysadmin permissions.</span></span> <span data-ttu-id="2b217-312">All SQL Marketplace virtual machines come with the **SqlIaaSExtension** installed.</span><span class="sxs-lookup"><span data-stu-id="2b217-312">All SQL Marketplace virtual machines come with the **SqlIaaSExtension** installed.</span></span> <span data-ttu-id="2b217-313">The **AzureBackupWindowsWorkload** extension uses the **SQLIaaSExtension** to automatically get the required permissions.</span><span class="sxs-lookup"><span data-stu-id="2b217-313">The **AzureBackupWindowsWorkload** extension uses the **SQLIaaSExtension** to automatically get the required permissions.</span></span> <span data-ttu-id="2b217-314">If your virtual machine doesn't have the **SqlIaaSExtension** installed, the Discover DB operation fails with the error message `UserErrorSQLNoSysAdminMembership`.</span><span class="sxs-lookup"><span data-stu-id="2b217-314">If your virtual machine doesn't have the **SqlIaaSExtension** installed, the Discover DB operation fails with the error message `UserErrorSQLNoSysAdminMembership`.</span></span> <span data-ttu-id="2b217-315">To add the sysadmin permission for backup, follow the instructions in [Set up Azure Backup permissions for non-Marketplace SQL VMs](backup-azure-sql-database.md#set-permissions-for-non-marketplace-sql-vms).</span><span class="sxs-lookup"><span data-stu-id="2b217-315">To add the sysadmin permission for backup, follow the instructions in [Set up Azure Backup permissions for non-Marketplace SQL VMs](backup-azure-sql-database.md#set-permissions-for-non-marketplace-sql-vms).</span></span>

    ![Select the VM and database](./media/backup-azure-sql-database/registration-errors.png)

## <a name="configure-backup-for-sql-server-databases"></a><span data-ttu-id="2b217-317">Configure backup for SQL Server databases</span><span class="sxs-lookup"><span data-stu-id="2b217-317">Configure backup for SQL Server databases</span></span>

<span data-ttu-id="2b217-318">Azure Backup provides management services to protect your SQL Server databases and manage backup jobs.</span><span class="sxs-lookup"><span data-stu-id="2b217-318">Azure Backup provides management services to protect your SQL Server databases and manage backup jobs.</span></span> <span data-ttu-id="2b217-319">The management and monitoring functions depend on your Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-319">The management and monitoring functions depend on your Recovery Services vault.</span></span> 

> [!NOTE]
> <span data-ttu-id="2b217-320">You can have only one backup solution at a time to back up SQL Server databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-320">You can have only one backup solution at a time to back up SQL Server databases.</span></span> <span data-ttu-id="2b217-321">Disable all other SQL backups before you use this feature; otherwise, the backups will interfere and fail.</span><span class="sxs-lookup"><span data-stu-id="2b217-321">Disable all other SQL backups before you use this feature; otherwise, the backups will interfere and fail.</span></span> <span data-ttu-id="2b217-322">You can enable Azure Backup for IaaS VM along with SQL backup without any conflict.</span><span class="sxs-lookup"><span data-stu-id="2b217-322">You can enable Azure Backup for IaaS VM along with SQL backup without any conflict.</span></span>
>

<span data-ttu-id="2b217-323">To configure protection for a SQL database:</span><span class="sxs-lookup"><span data-stu-id="2b217-323">To configure protection for a SQL database:</span></span>

1. <span data-ttu-id="2b217-324">Open the Recovery Services vault that's registered with the SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-324">Open the Recovery Services vault that's registered with the SQL virtual machine.</span></span>

2. <span data-ttu-id="2b217-325">On the **Recovery Services vault** dashboard, select **Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-325">On the **Recovery Services vault** dashboard, select **Backup**.</span></span> <span data-ttu-id="2b217-326">The **Backup Goal** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-326">The **Backup Goal** menu opens.</span></span>

   ![Select Backup to open the Backup Goal menu](./media/backup-azure-sql-database/open-backup-menu.png)

3. <span data-ttu-id="2b217-328">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span><span class="sxs-lookup"><span data-stu-id="2b217-328">On the **Backup Goal** menu, set **Where is your workload running** to the default: **Azure**.</span></span>

4. <span data-ttu-id="2b217-329">Expand the **What do you want to back up** drop-down list box and select **SQL Server in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-329">Expand the **What do you want to back up** drop-down list box and select **SQL Server in Azure VM**.</span></span>

    ![Select SQL Server in Azure VM for the backup](./media/backup-azure-sql-database/choose-sql-database-backup-goal.png)

    <span data-ttu-id="2b217-331">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-331">The **Backup Goal** menu displays two steps: **Discover DBs in VMs** and **Configure Backup**.</span></span>
    
    <span data-ttu-id="2b217-332">If you completed the steps in this article in order, you've discovered the unprotected virtual machines and this vault is registered with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-332">If you completed the steps in this article in order, you've discovered the unprotected virtual machines and this vault is registered with a virtual machine.</span></span> <span data-ttu-id="2b217-333">Now you're ready to configure protection for the SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-333">Now you're ready to configure protection for the SQL databases.</span></span>
    
5. <span data-ttu-id="2b217-334">On the **Backup Goal** menu, select **Configure Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-334">On the **Backup Goal** menu, select **Configure Backup**.</span></span>

    ![Select Configure Backup](./media/backup-azure-sql-database/backup-goal-configure-backup.png)

    <span data-ttu-id="2b217-336">The Azure Backup service displays all SQL Server instances with standalone databases and SQL Server Always On availability groups.</span><span class="sxs-lookup"><span data-stu-id="2b217-336">The Azure Backup service displays all SQL Server instances with standalone databases and SQL Server Always On availability groups.</span></span> <span data-ttu-id="2b217-337">To view the standalone databases in the SQL Server instance, select the chevron to the left of the instance name.</span><span class="sxs-lookup"><span data-stu-id="2b217-337">To view the standalone databases in the SQL Server instance, select the chevron to the left of the instance name.</span></span> <span data-ttu-id="2b217-338">The following images show examples of a standalone instance and an Always On availability group.</span><span class="sxs-lookup"><span data-stu-id="2b217-338">The following images show examples of a standalone instance and an Always On availability group.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2b217-339">For a SQL Server Always On availability group, the SQL backup preference is honored.</span><span class="sxs-lookup"><span data-stu-id="2b217-339">For a SQL Server Always On availability group, the SQL backup preference is honored.</span></span> <span data-ttu-id="2b217-340">But, due to a SQL platform limitation, full and differential backups need to happen from the primary node.</span><span class="sxs-lookup"><span data-stu-id="2b217-340">But, due to a SQL platform limitation, full and differential backups need to happen from the primary node.</span></span> <span data-ttu-id="2b217-341">Log back up happens according to your backup preference.</span><span class="sxs-lookup"><span data-stu-id="2b217-341">Log back up happens according to your backup preference.</span></span> <span data-ttu-id="2b217-342">Due to this limitation, the primary node must always be registered for availability groups.</span><span class="sxs-lookup"><span data-stu-id="2b217-342">Due to this limitation, the primary node must always be registered for availability groups.</span></span>
    >

    ![List of databases in the SQL instance](./media/backup-azure-sql-database/discovered-databases.png)

    <span data-ttu-id="2b217-344">Select the chevron to the left of the Always On availability group to view the list of databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-344">Select the chevron to the left of the Always On availability group to view the list of databases.</span></span>

    ![List of databases in the Always On availability group](./media/backup-azure-sql-database/discovered-database-availability-group.png)

6. <span data-ttu-id="2b217-346">In the list of databases, select all of the databases to protect, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b217-346">In the list of databases, select all of the databases to protect, and then select **OK**.</span></span>

    ![Select multiple databases to protect](./media/backup-azure-sql-database/select-multiple-database-protection.png)

    <span data-ttu-id="2b217-348">Select up to 50 databases at a time.</span><span class="sxs-lookup"><span data-stu-id="2b217-348">Select up to 50 databases at a time.</span></span> <span data-ttu-id="2b217-349">To protect more than 50 databases, make several passes.</span><span class="sxs-lookup"><span data-stu-id="2b217-349">To protect more than 50 databases, make several passes.</span></span> <span data-ttu-id="2b217-350">After you protect the first 50 databases, repeat this step to protect the next set of databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-350">After you protect the first 50 databases, repeat this step to protect the next set of databases.</span></span>

    > [!Note] 
    > <span data-ttu-id="2b217-351">To optimize backup loads, Azure Backup breaks large backup jobs into multiple batches.</span><span class="sxs-lookup"><span data-stu-id="2b217-351">To optimize backup loads, Azure Backup breaks large backup jobs into multiple batches.</span></span> <span data-ttu-id="2b217-352">The maximum number of databases in one backup job is 50.</span><span class="sxs-lookup"><span data-stu-id="2b217-352">The maximum number of databases in one backup job is 50.</span></span>
    >
    >

7. <span data-ttu-id="2b217-353">To create or choose a backup policy, on the **Backup** menu, select **Backup policy**.</span><span class="sxs-lookup"><span data-stu-id="2b217-353">To create or choose a backup policy, on the **Backup** menu, select **Backup policy**.</span></span> <span data-ttu-id="2b217-354">The **Backup policy** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-354">The **Backup policy** menu opens.</span></span>

    ![Select Backup policy](./media/backup-azure-sql-database/select-backup-policy.png)

8. <span data-ttu-id="2b217-356">In the **Choose backup policy** drop-down list box, choose a backup policy, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b217-356">In the **Choose backup policy** drop-down list box, choose a backup policy, and then select **OK**.</span></span> <span data-ttu-id="2b217-357">For information on how to create a backup policy, see [Define a backup policy](backup-azure-sql-database.md#define-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="2b217-357">For information on how to create a backup policy, see [Define a backup policy](backup-azure-sql-database.md#define-a-backup-policy).</span></span>

   > [!NOTE]
   > <span data-ttu-id="2b217-358">During Preview, you can't edit Backup policies.</span><span class="sxs-lookup"><span data-stu-id="2b217-358">During Preview, you can't edit Backup policies.</span></span> <span data-ttu-id="2b217-359">If you want a different policy than what's available in the list, you must create that policy.</span><span class="sxs-lookup"><span data-stu-id="2b217-359">If you want a different policy than what's available in the list, you must create that policy.</span></span> <span data-ttu-id="2b217-360">For information on creating a new backup policy, see the section, [Define a backup policy](backup-azure-sql-database.md#define-a-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="2b217-360">For information on creating a new backup policy, see the section, [Define a backup policy](backup-azure-sql-database.md#define-a-backup-policy).</span></span>

    ![Choose a backup policy from the list](./media/backup-azure-sql-database/select-backup-policy-steptwo.png)

    <span data-ttu-id="2b217-362">On the **Backup policy** menu, in the **Choose backup policy** drop-down list box, you can:</span><span class="sxs-lookup"><span data-stu-id="2b217-362">On the **Backup policy** menu, in the **Choose backup policy** drop-down list box, you can:</span></span> 
    - <span data-ttu-id="2b217-363">Select the default policy: **HourlyLogBackup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-363">Select the default policy: **HourlyLogBackup**.</span></span>
    - <span data-ttu-id="2b217-364">Choose an existing backup policy previously created for SQL.</span><span class="sxs-lookup"><span data-stu-id="2b217-364">Choose an existing backup policy previously created for SQL.</span></span>
    - <span data-ttu-id="2b217-365">[Define a new policy](backup-azure-sql-database.md#define-a-backup-policy) based on your RPO and retention range.</span><span class="sxs-lookup"><span data-stu-id="2b217-365">[Define a new policy](backup-azure-sql-database.md#define-a-backup-policy) based on your RPO and retention range.</span></span> 

    > [!Note]
    > <span data-ttu-id="2b217-366">Azure Backup supports long-term retention that's based on the grandfather-father-son backup scheme.</span><span class="sxs-lookup"><span data-stu-id="2b217-366">Azure Backup supports long-term retention that's based on the grandfather-father-son backup scheme.</span></span> <span data-ttu-id="2b217-367">The scheme optimizes back-end storage consumption while meeting compliance needs.</span><span class="sxs-lookup"><span data-stu-id="2b217-367">The scheme optimizes back-end storage consumption while meeting compliance needs.</span></span>
    >

9. <span data-ttu-id="2b217-368">After you choose a backup policy, on the **Backup menu**, select **Enable backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-368">After you choose a backup policy, on the **Backup menu**, select **Enable backup**.</span></span>

    ![Enable the chosen backup policy](./media/backup-azure-sql-database/enable-backup-button.png)

    <span data-ttu-id="2b217-370">Track the configuration progress in the **Notifications** area of the portal.</span><span class="sxs-lookup"><span data-stu-id="2b217-370">Track the configuration progress in the **Notifications** area of the portal.</span></span>

    ![Notification area](./media/backup-azure-sql-database/notifications-area.png)


### <a name="define-a-backup-policy"></a><span data-ttu-id="2b217-372">Define a backup policy</span><span class="sxs-lookup"><span data-stu-id="2b217-372">Define a backup policy</span></span>

<span data-ttu-id="2b217-373">A backup policy defines a matrix of when backups are taken and how long they're retained.</span><span class="sxs-lookup"><span data-stu-id="2b217-373">A backup policy defines a matrix of when backups are taken and how long they're retained.</span></span> <span data-ttu-id="2b217-374">Use Azure Backup to schedule three types of backup for SQL databases:</span><span class="sxs-lookup"><span data-stu-id="2b217-374">Use Azure Backup to schedule three types of backup for SQL databases:</span></span>

* <span data-ttu-id="2b217-375">Full backup: A full database backup backs up the entire database.</span><span class="sxs-lookup"><span data-stu-id="2b217-375">Full backup: A full database backup backs up the entire database.</span></span> <span data-ttu-id="2b217-376">A full backup contains all of the data in a specific database, or a set of filegroups or files, and enough logs to recover that data.</span><span class="sxs-lookup"><span data-stu-id="2b217-376">A full backup contains all of the data in a specific database, or a set of filegroups or files, and enough logs to recover that data.</span></span> <span data-ttu-id="2b217-377">At most, you can trigger one full backup per day.</span><span class="sxs-lookup"><span data-stu-id="2b217-377">At most, you can trigger one full backup per day.</span></span> <span data-ttu-id="2b217-378">You can choose to take a full backup on a daily or weekly interval.</span><span class="sxs-lookup"><span data-stu-id="2b217-378">You can choose to take a full backup on a daily or weekly interval.</span></span> 
* <span data-ttu-id="2b217-379">Differential backup: A differential backup is based on the most recent, previous full data backup.</span><span class="sxs-lookup"><span data-stu-id="2b217-379">Differential backup: A differential backup is based on the most recent, previous full data backup.</span></span> <span data-ttu-id="2b217-380">A differential backup captures only the data that's changed since the full backup.</span><span class="sxs-lookup"><span data-stu-id="2b217-380">A differential backup captures only the data that's changed since the full backup.</span></span> <span data-ttu-id="2b217-381">At most, you can trigger one differential backup per day.</span><span class="sxs-lookup"><span data-stu-id="2b217-381">At most, you can trigger one differential backup per day.</span></span> <span data-ttu-id="2b217-382">You can't configure a full backup and a differential backup on the same day.</span><span class="sxs-lookup"><span data-stu-id="2b217-382">You can't configure a full backup and a differential backup on the same day.</span></span>
* <span data-ttu-id="2b217-383">Transaction log backup: A log backup enables point-in-time restoration up to a specific second.</span><span class="sxs-lookup"><span data-stu-id="2b217-383">Transaction log backup: A log backup enables point-in-time restoration up to a specific second.</span></span> <span data-ttu-id="2b217-384">At most, you can configure transactional log backups every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="2b217-384">At most, you can configure transactional log backups every 15 minutes.</span></span>

<span data-ttu-id="2b217-385">The policy's created at the Recovery Services vault level.</span><span class="sxs-lookup"><span data-stu-id="2b217-385">The policy's created at the Recovery Services vault level.</span></span> <span data-ttu-id="2b217-386">Multiple vaults can use the same backup policy, but you must apply the backup policy to each vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-386">Multiple vaults can use the same backup policy, but you must apply the backup policy to each vault.</span></span> <span data-ttu-id="2b217-387">When you create a backup policy, the daily full backup is the default.</span><span class="sxs-lookup"><span data-stu-id="2b217-387">When you create a backup policy, the daily full backup is the default.</span></span> <span data-ttu-id="2b217-388">You can add a differential backup, but only if you configure full backups to occur weekly.</span><span class="sxs-lookup"><span data-stu-id="2b217-388">You can add a differential backup, but only if you configure full backups to occur weekly.</span></span> <span data-ttu-id="2b217-389">The following procedure explains how to create a backup policy for a SQL Server instance in an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-389">The following procedure explains how to create a backup policy for a SQL Server instance in an Azure virtual machine.</span></span> 

> [!NOTE]
> <span data-ttu-id="2b217-390">In Preview, you can't edit a Backup policy.</span><span class="sxs-lookup"><span data-stu-id="2b217-390">In Preview, you can't edit a Backup policy.</span></span> <span data-ttu-id="2b217-391">Instead, you must create a new policy with the desired details.</span><span class="sxs-lookup"><span data-stu-id="2b217-391">Instead, you must create a new policy with the desired details.</span></span>  
 
<span data-ttu-id="2b217-392">To create a backup policy:</span><span class="sxs-lookup"><span data-stu-id="2b217-392">To create a backup policy:</span></span>

1. <span data-ttu-id="2b217-393">In the Recovery Services vault that protects the SQL database, click **Backup policies**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="2b217-393">In the Recovery Services vault that protects the SQL database, click **Backup policies**, and then click **Add**.</span></span> 

   ![Open the create new backup policy dialog](./media/backup-azure-sql-database/new-policy-workflow.png)

   <span data-ttu-id="2b217-395">The **Add** menu appears.</span><span class="sxs-lookup"><span data-stu-id="2b217-395">The **Add** menu appears.</span></span>

2. <span data-ttu-id="2b217-396">In the **Add** menu, click **SQL Server in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-396">In the **Add** menu, click **SQL Server in Azure VM**.</span></span>

   ![Choose a policy type for the new backup policy](./media/backup-azure-sql-database/policy-type-details.png)

   <span data-ttu-id="2b217-398">Selecting SQL Server in Azure VM defines the policy type, and opens the Backup policy menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-398">Selecting SQL Server in Azure VM defines the policy type, and opens the Backup policy menu.</span></span> <span data-ttu-id="2b217-399">The **Backup policy** menu shows the fields that are necessary for a new SQL Server backup policy.</span><span class="sxs-lookup"><span data-stu-id="2b217-399">The **Backup policy** menu shows the fields that are necessary for a new SQL Server backup policy.</span></span>

3. <span data-ttu-id="2b217-400">In **Policy name**, enter a name for the new policy.</span><span class="sxs-lookup"><span data-stu-id="2b217-400">In **Policy name**, enter a name for the new policy.</span></span>

4. <span data-ttu-id="2b217-401">A Full backup is mandatory; you can't turn off the **Full Backup** option.</span><span class="sxs-lookup"><span data-stu-id="2b217-401">A Full backup is mandatory; you can't turn off the **Full Backup** option.</span></span> <span data-ttu-id="2b217-402">Click **Full Backup** to view and edit the policy.</span><span class="sxs-lookup"><span data-stu-id="2b217-402">Click **Full Backup** to view and edit the policy.</span></span> <span data-ttu-id="2b217-403">Even if you don't change the Backup policy, you should view the policy details.</span><span class="sxs-lookup"><span data-stu-id="2b217-403">Even if you don't change the Backup policy, you should view the policy details.</span></span>

    ![New backup policy fields](./media/backup-azure-sql-database/full-backup-policy.png)

    <span data-ttu-id="2b217-405">In the **Full Backup policy** menu, for **Backup Frequency**, choose **Daily** or **Weekly**.</span><span class="sxs-lookup"><span data-stu-id="2b217-405">In the **Full Backup policy** menu, for **Backup Frequency**, choose **Daily** or **Weekly**.</span></span> <span data-ttu-id="2b217-406">For **Daily**, select the hour and time zone when the backup job begins.</span><span class="sxs-lookup"><span data-stu-id="2b217-406">For **Daily**, select the hour and time zone when the backup job begins.</span></span> <span data-ttu-id="2b217-407">You can't create differential backups for daily full backups.</span><span class="sxs-lookup"><span data-stu-id="2b217-407">You can't create differential backups for daily full backups.</span></span>

   ![Daily interval setting](./media/backup-azure-sql-database/daily-interval.png)

    <span data-ttu-id="2b217-409">For **Weekly**, select the day of the week, hour, and time zone when the backup job begins.</span><span class="sxs-lookup"><span data-stu-id="2b217-409">For **Weekly**, select the day of the week, hour, and time zone when the backup job begins.</span></span>

   ![Weekly interval setting](./media/backup-azure-sql-database/weekly-interval.png)

5. <span data-ttu-id="2b217-411">By default, all **Retention Range** options are selected: daily, weekly, monthly, and yearly.</span><span class="sxs-lookup"><span data-stu-id="2b217-411">By default, all **Retention Range** options are selected: daily, weekly, monthly, and yearly.</span></span> <span data-ttu-id="2b217-412">Deselect any undesired retention range limits.</span><span class="sxs-lookup"><span data-stu-id="2b217-412">Deselect any undesired retention range limits.</span></span> <span data-ttu-id="2b217-413">Set the intervals to use.</span><span class="sxs-lookup"><span data-stu-id="2b217-413">Set the intervals to use.</span></span> <span data-ttu-id="2b217-414">In the **Full Backup policy** menu, select **OK** to accept the settings.</span><span class="sxs-lookup"><span data-stu-id="2b217-414">In the **Full Backup policy** menu, select **OK** to accept the settings.</span></span>

   ![Retention range interval settings](./media/backup-azure-sql-database/retention-range-interval.png)

    <span data-ttu-id="2b217-416">Recovery points are tagged for retention based on their retention range.</span><span class="sxs-lookup"><span data-stu-id="2b217-416">Recovery points are tagged for retention based on their retention range.</span></span> <span data-ttu-id="2b217-417">For example, if you select a daily full backup, only one full backup is triggered each day.</span><span class="sxs-lookup"><span data-stu-id="2b217-417">For example, if you select a daily full backup, only one full backup is triggered each day.</span></span> <span data-ttu-id="2b217-418">The backup for a specific day is tagged and retained based on the weekly retention range and your weekly retention setting.</span><span class="sxs-lookup"><span data-stu-id="2b217-418">The backup for a specific day is tagged and retained based on the weekly retention range and your weekly retention setting.</span></span> <span data-ttu-id="2b217-419">The monthly and yearly retention ranges behave in a similar way.</span><span class="sxs-lookup"><span data-stu-id="2b217-419">The monthly and yearly retention ranges behave in a similar way.</span></span>

6. <span data-ttu-id="2b217-420">To add a differential backup policy, select **Differential Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-420">To add a differential backup policy, select **Differential Backup**.</span></span> <span data-ttu-id="2b217-421">The **Differential Backup policy** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-421">The **Differential Backup policy** menu opens.</span></span> 

   ![Open the differential backup policy menu](./media/backup-azure-sql-database/backup-policy-menu-choices.png)

    <span data-ttu-id="2b217-423">On the **Differential Backup policy** menu, select **Enable** to open the frequency and retention controls.</span><span class="sxs-lookup"><span data-stu-id="2b217-423">On the **Differential Backup policy** menu, select **Enable** to open the frequency and retention controls.</span></span> <span data-ttu-id="2b217-424">At most, you can trigger one differential backup per day.</span><span class="sxs-lookup"><span data-stu-id="2b217-424">At most, you can trigger one differential backup per day.</span></span>
    
    > [!Important] 
    > <span data-ttu-id="2b217-425">Differential backups can be retained for a maximum of 180 days.</span><span class="sxs-lookup"><span data-stu-id="2b217-425">Differential backups can be retained for a maximum of 180 days.</span></span> <span data-ttu-id="2b217-426">If you need longer retention, you must use full backups.</span><span class="sxs-lookup"><span data-stu-id="2b217-426">If you need longer retention, you must use full backups.</span></span>
    >

   ![Edit the differential backup policy](./media/backup-azure-sql-database/enable-differential-backup-policy.png)

    <span data-ttu-id="2b217-428">Select **OK** to save the policy and return to the main **Backup policy** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-428">Select **OK** to save the policy and return to the main **Backup policy** menu.</span></span>

7. <span data-ttu-id="2b217-429">To add a transactional log backup policy, select **Log Backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-429">To add a transactional log backup policy, select **Log Backup**.</span></span> <span data-ttu-id="2b217-430">The **Log Backup** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-430">The **Log Backup** menu opens.</span></span>

    <span data-ttu-id="2b217-431">In the **Log Backup** menu, select **Enable**, and then set the frequency and retention controls.</span><span class="sxs-lookup"><span data-stu-id="2b217-431">In the **Log Backup** menu, select **Enable**, and then set the frequency and retention controls.</span></span> <span data-ttu-id="2b217-432">Log backups can occur as often as every 15 minutes, and can be retained for up to 35 days.</span><span class="sxs-lookup"><span data-stu-id="2b217-432">Log backups can occur as often as every 15 minutes, and can be retained for up to 35 days.</span></span> <span data-ttu-id="2b217-433">Select **OK** to save the policy and return to the main **Backup policy** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-433">Select **OK** to save the policy and return to the main **Backup policy** menu.</span></span>

   ![Edit the log backup policy](./media/backup-azure-sql-database/log-backup-policy-editor.png)

8. <span data-ttu-id="2b217-435">On the **Backup policy** menu, choose whether to enable **SQL Backup Compression**.</span><span class="sxs-lookup"><span data-stu-id="2b217-435">On the **Backup policy** menu, choose whether to enable **SQL Backup Compression**.</span></span> <span data-ttu-id="2b217-436">Compression is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="2b217-436">Compression is disabled by default.</span></span>

    <span data-ttu-id="2b217-437">On the back end, Azure Backup uses SQL native backup compression.</span><span class="sxs-lookup"><span data-stu-id="2b217-437">On the back end, Azure Backup uses SQL native backup compression.</span></span>

9. <span data-ttu-id="2b217-438">After you complete the edits to the backup policy, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="2b217-438">After you complete the edits to the backup policy, select **OK**.</span></span> 

   ![Accept the new backup policy](./media/backup-azure-sql-database/backup-policy-click-ok.png)

## <a name="restore-a-sql-database"></a><span data-ttu-id="2b217-440">Restore a SQL database</span><span class="sxs-lookup"><span data-stu-id="2b217-440">Restore a SQL database</span></span>
<span data-ttu-id="2b217-441">Azure Backup provides functionality to restore individual databases to a specific date or time (to the second) by using transaction log backups.</span><span class="sxs-lookup"><span data-stu-id="2b217-441">Azure Backup provides functionality to restore individual databases to a specific date or time (to the second) by using transaction log backups.</span></span> <span data-ttu-id="2b217-442">Azure Backup automatically determines the appropriate full differential and the chain of log backups that are required to restore your data based on your restore times.</span><span class="sxs-lookup"><span data-stu-id="2b217-442">Azure Backup automatically determines the appropriate full differential and the chain of log backups that are required to restore your data based on your restore times.</span></span>

<span data-ttu-id="2b217-443">You can also select a specific full or differential backup to restore to a specific recovery point, rather than a specific time.</span><span class="sxs-lookup"><span data-stu-id="2b217-443">You can also select a specific full or differential backup to restore to a specific recovery point, rather than a specific time.</span></span>

### <a name="pre-requisite-before-triggering-a-restore"></a><span data-ttu-id="2b217-444">Pre-requisite before triggering a restore</span><span class="sxs-lookup"><span data-stu-id="2b217-444">Pre-requisite before triggering a restore</span></span>

1. <span data-ttu-id="2b217-445">You can restore the database to an instance of a SQL Server in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="2b217-445">You can restore the database to an instance of a SQL Server in the same Azure region.</span></span> <span data-ttu-id="2b217-446">The destination server must be registered to the same Recovery Services vault as the source.</span><span class="sxs-lookup"><span data-stu-id="2b217-446">The destination server must be registered to the same Recovery Services vault as the source.</span></span>  
2. <span data-ttu-id="2b217-447">To restore a TDE encrypted database to another SQL Server, please first restore the certificate to the destination server by following steps documented [here](https://docs.microsoft.com/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="2b217-447">To restore a TDE encrypted database to another SQL Server, please first restore the certificate to the destination server by following steps documented [here](https://docs.microsoft.com/sql/relational-databases/security/encryption/move-a-tde-protected-database-to-another-sql-server?view=sql-server-2017).</span></span>
3. <span data-ttu-id="2b217-448">Before you trigger a restore of the "master" database, start the SQL Server instance in single-user mode with startup option `-m AzureWorkloadBackup`.</span><span class="sxs-lookup"><span data-stu-id="2b217-448">Before you trigger a restore of the "master" database, start the SQL Server instance in single-user mode with startup option `-m AzureWorkloadBackup`.</span></span> <span data-ttu-id="2b217-449">The argument to the `-m` option is the name of the client.</span><span class="sxs-lookup"><span data-stu-id="2b217-449">The argument to the `-m` option is the name of the client.</span></span> <span data-ttu-id="2b217-450">Only this client is allowed to open the connection.</span><span class="sxs-lookup"><span data-stu-id="2b217-450">Only this client is allowed to open the connection.</span></span> <span data-ttu-id="2b217-451">For all system databases (model, master, msdb), stop the SQL Agent service before you trigger the restore.</span><span class="sxs-lookup"><span data-stu-id="2b217-451">For all system databases (model, master, msdb), stop the SQL Agent service before you trigger the restore.</span></span> <span data-ttu-id="2b217-452">Close any applications that might try to steal a connection to any of these databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-452">Close any applications that might try to steal a connection to any of these databases.</span></span>

### <a name="steps-to-restore-a-database"></a><span data-ttu-id="2b217-453">Steps to restore a database:</span><span class="sxs-lookup"><span data-stu-id="2b217-453">Steps to restore a database:</span></span>

1. <span data-ttu-id="2b217-454">Open the Recovery Services vault that's registered with the SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-454">Open the Recovery Services vault that's registered with the SQL virtual machine.</span></span>

2. <span data-ttu-id="2b217-455">On the **Recovery Services vault** dashboard, under **Usage**, select **Backup Items** to open the **Backup Items** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-455">On the **Recovery Services vault** dashboard, under **Usage**, select **Backup Items** to open the **Backup Items** menu.</span></span>

    ![Open the Backup Items menu](./media/backup-azure-sql-database/restore-sql-vault-dashboard.png)<span data-ttu-id="2b217-457">.</span><span class="sxs-lookup"><span data-stu-id="2b217-457">.</span></span>

3. <span data-ttu-id="2b217-458">On the **Backup Items** menu, under **Backup Management Type**, select **SQL in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-458">On the **Backup Items** menu, under **Backup Management Type**, select **SQL in Azure VM**.</span></span> 

    ![Select SQL in Azure VM](./media/backup-azure-sql-database/sql-restore-backup-items.png)

    <span data-ttu-id="2b217-460">The **Backup Items** menu shows the list of SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-460">The **Backup Items** menu shows the list of SQL databases.</span></span> 

4. <span data-ttu-id="2b217-461">In the list of SQL databases, select the database to restore.</span><span class="sxs-lookup"><span data-stu-id="2b217-461">In the list of SQL databases, select the database to restore.</span></span>

    ![Select the database to restore](./media/backup-azure-sql-database/sql-restore-sql-in-vm.png)

    <span data-ttu-id="2b217-463">When you select the database, its menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-463">When you select the database, its menu opens.</span></span> <span data-ttu-id="2b217-464">The menu provides the backup details for the database, including:</span><span class="sxs-lookup"><span data-stu-id="2b217-464">The menu provides the backup details for the database, including:</span></span>

    * <span data-ttu-id="2b217-465">The oldest and latest restore points.</span><span class="sxs-lookup"><span data-stu-id="2b217-465">The oldest and latest restore points.</span></span>
    * <span data-ttu-id="2b217-466">Log backup status for the last 24 hours (for databases in full and bulk-logged recovery model, if configured for transactional log backups).</span><span class="sxs-lookup"><span data-stu-id="2b217-466">Log backup status for the last 24 hours (for databases in full and bulk-logged recovery model, if configured for transactional log backups).</span></span>

5. <span data-ttu-id="2b217-467">On the menu for the selected database, select **Restore DB**.</span><span class="sxs-lookup"><span data-stu-id="2b217-467">On the menu for the selected database, select **Restore DB**.</span></span> <span data-ttu-id="2b217-468">The **Restore** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-468">The **Restore** menu opens.</span></span>

    ![Select Restore DB](./media/backup-azure-sql-database/restore-db-button.png)

    <span data-ttu-id="2b217-470">When the **Restore** menu opens, the **Restore Configuration** menu also opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-470">When the **Restore** menu opens, the **Restore Configuration** menu also opens.</span></span> <span data-ttu-id="2b217-471">The **Restore Configuration** menu is the first step to configure the restoration.</span><span class="sxs-lookup"><span data-stu-id="2b217-471">The **Restore Configuration** menu is the first step to configure the restoration.</span></span> <span data-ttu-id="2b217-472">Use this menu to select where to restore the data.</span><span class="sxs-lookup"><span data-stu-id="2b217-472">Use this menu to select where to restore the data.</span></span> <span data-ttu-id="2b217-473">The options are:</span><span class="sxs-lookup"><span data-stu-id="2b217-473">The options are:</span></span>
    - <span data-ttu-id="2b217-474">**Alternate Location**: Restore the database to an alternate location and retain the original source database.</span><span class="sxs-lookup"><span data-stu-id="2b217-474">**Alternate Location**: Restore the database to an alternate location and retain the original source database.</span></span>
    - <span data-ttu-id="2b217-475">**Overwrite DB**: Restore the data to the same SQL Server instance as the original source.</span><span class="sxs-lookup"><span data-stu-id="2b217-475">**Overwrite DB**: Restore the data to the same SQL Server instance as the original source.</span></span> <span data-ttu-id="2b217-476">The effect of this option is to overwrite the original database.</span><span class="sxs-lookup"><span data-stu-id="2b217-476">The effect of this option is to overwrite the original database.</span></span>

    > [!Important]
    > <span data-ttu-id="2b217-477">If the selected database belongs to an Always On availability group, SQL Server doesn't allow the database to be overwritten.</span><span class="sxs-lookup"><span data-stu-id="2b217-477">If the selected database belongs to an Always On availability group, SQL Server doesn't allow the database to be overwritten.</span></span> <span data-ttu-id="2b217-478">In this case, only the **Alternate Location** option is enabled.</span><span class="sxs-lookup"><span data-stu-id="2b217-478">In this case, only the **Alternate Location** option is enabled.</span></span>
    >

    ![Restore Configuration menu](./media/backup-azure-sql-database/restore-restore-configuration-menu.png)

### <a name="restore-to-an-alternate-location"></a><span data-ttu-id="2b217-480">Restore to an alternate location</span><span class="sxs-lookup"><span data-stu-id="2b217-480">Restore to an alternate location</span></span>

<span data-ttu-id="2b217-481">This procedure walks you through restoring data to an alternate location.</span><span class="sxs-lookup"><span data-stu-id="2b217-481">This procedure walks you through restoring data to an alternate location.</span></span> <span data-ttu-id="2b217-482">To overwrite the database during the restore, continue to [Restore and overwrite the database](backup-azure-sql-database.md#restore-and-overwrite-the-database).</span><span class="sxs-lookup"><span data-stu-id="2b217-482">To overwrite the database during the restore, continue to [Restore and overwrite the database](backup-azure-sql-database.md#restore-and-overwrite-the-database).</span></span> <span data-ttu-id="2b217-483">At this stage, your Recovery Services vault is open and the **Restore Configuration** menu is visible.</span><span class="sxs-lookup"><span data-stu-id="2b217-483">At this stage, your Recovery Services vault is open and the **Restore Configuration** menu is visible.</span></span> <span data-ttu-id="2b217-484">If you're not at this stage, start by [restoring a SQL database](backup-azure-sql-database.md#restore-a-sql-database).</span><span class="sxs-lookup"><span data-stu-id="2b217-484">If you're not at this stage, start by [restoring a SQL database](backup-azure-sql-database.md#restore-a-sql-database).</span></span>

> [!NOTE]
> <span data-ttu-id="2b217-485">You can restore the database to an instance of a SQL Server in the same Azure region.</span><span class="sxs-lookup"><span data-stu-id="2b217-485">You can restore the database to an instance of a SQL Server in the same Azure region.</span></span> <span data-ttu-id="2b217-486">The destination server needs to be registered to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-486">The destination server needs to be registered to the Recovery Services vault.</span></span> 
>

<span data-ttu-id="2b217-487">On the **Restore Configuration** menu, the **Server** drop-down list box shows only the SQL Server instances that are registered with the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-487">On the **Restore Configuration** menu, the **Server** drop-down list box shows only the SQL Server instances that are registered with the Recovery Services vault.</span></span> <span data-ttu-id="2b217-488">If the server that you want isn't in the list, see [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases) to find the server.</span><span class="sxs-lookup"><span data-stu-id="2b217-488">If the server that you want isn't in the list, see [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases) to find the server.</span></span> <span data-ttu-id="2b217-489">During the discovery process, new servers are registered to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-489">During the discovery process, new servers are registered to the Recovery Services vault.</span></span>

1. <span data-ttu-id="2b217-490">In the **Restore Configuration** menu:</span><span class="sxs-lookup"><span data-stu-id="2b217-490">In the **Restore Configuration** menu:</span></span>

    * <span data-ttu-id="2b217-491">Under **Where to Restore**, select **Alternate Location**.</span><span class="sxs-lookup"><span data-stu-id="2b217-491">Under **Where to Restore**, select **Alternate Location**.</span></span>
    * <span data-ttu-id="2b217-492">Open the **Server** drop-down list box and choose the SQL Server instance to restore the database.</span><span class="sxs-lookup"><span data-stu-id="2b217-492">Open the **Server** drop-down list box and choose the SQL Server instance to restore the database.</span></span>
    * <span data-ttu-id="2b217-493">Open the **Instance** drop-down list box and choose a SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="2b217-493">Open the **Instance** drop-down list box and choose a SQL Server instance.</span></span>
    * <span data-ttu-id="2b217-494">In the **Restored DB Name** box, enter the name of the target database.</span><span class="sxs-lookup"><span data-stu-id="2b217-494">In the **Restored DB Name** box, enter the name of the target database.</span></span>
    * <span data-ttu-id="2b217-495">As applicable, select **Overwrite if the DB with the same name already exists on selected SQL instance**.</span><span class="sxs-lookup"><span data-stu-id="2b217-495">As applicable, select **Overwrite if the DB with the same name already exists on selected SQL instance**.</span></span>
    * <span data-ttu-id="2b217-496">Select **OK** to complete the configuration of the destination and continue to choose a restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-496">Select **OK** to complete the configuration of the destination and continue to choose a restore point.</span></span>

    ![Provide values for the Restore Configuration menu](./media/backup-azure-sql-database/restore-configuration-menu.png)

2. <span data-ttu-id="2b217-498">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-498">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span></span> <span data-ttu-id="2b217-499">To restore to a specific point-in-time log, continue with this step.</span><span class="sxs-lookup"><span data-stu-id="2b217-499">To restore to a specific point-in-time log, continue with this step.</span></span> <span data-ttu-id="2b217-500">To restore a full and differential restore point, continue to step 3.</span><span class="sxs-lookup"><span data-stu-id="2b217-500">To restore a full and differential restore point, continue to step 3.</span></span>

    ![Select restore point menu](./media/backup-azure-sql-database/recovery-point-menu.png)

    <span data-ttu-id="2b217-502">The point-in-time restore is available only for log backups for databases with a full and bulk-logged recovery model.</span><span class="sxs-lookup"><span data-stu-id="2b217-502">The point-in-time restore is available only for log backups for databases with a full and bulk-logged recovery model.</span></span> <span data-ttu-id="2b217-503">To restore to a specific point in time:</span><span class="sxs-lookup"><span data-stu-id="2b217-503">To restore to a specific point in time:</span></span>

    1. <span data-ttu-id="2b217-504">Select **Logs (Point in Time)** as the restore type.</span><span class="sxs-lookup"><span data-stu-id="2b217-504">Select **Logs (Point in Time)** as the restore type.</span></span>

        ![Choose the restore point type](./media/backup-azure-sql-database/recovery-point-logs.png)

    2. <span data-ttu-id="2b217-506">Under **Restore Date/Time**, select the mini calendar to open the **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="2b217-506">Under **Restore Date/Time**, select the mini calendar to open the **Calendar**.</span></span> <span data-ttu-id="2b217-507">On the **Calendar**, the bold dates have recovery points and the current date is highlighted.</span><span class="sxs-lookup"><span data-stu-id="2b217-507">On the **Calendar**, the bold dates have recovery points and the current date is highlighted.</span></span> <span data-ttu-id="2b217-508">Select a date with recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-508">Select a date with recovery points.</span></span> <span data-ttu-id="2b217-509">Dates without recovery points can't be selected.</span><span class="sxs-lookup"><span data-stu-id="2b217-509">Dates without recovery points can't be selected.</span></span>

        ![Open the Calendar](./media/backup-azure-sql-database/recovery-point-logs-calendar.png)

        <span data-ttu-id="2b217-511">After you select a date, the timeline graph displays the available recovery points in a continuous range.</span><span class="sxs-lookup"><span data-stu-id="2b217-511">After you select a date, the timeline graph displays the available recovery points in a continuous range.</span></span>

    3. <span data-ttu-id="2b217-512">Use the timeline graph or the **Time** dialog box to specify a specific time for the recovery point.</span><span class="sxs-lookup"><span data-stu-id="2b217-512">Use the timeline graph or the **Time** dialog box to specify a specific time for the recovery point.</span></span> <span data-ttu-id="2b217-513">Select **OK** to complete the restore point step.</span><span class="sxs-lookup"><span data-stu-id="2b217-513">Select **OK** to complete the restore point step.</span></span>
    
       ![Open the Calendar](./media/backup-azure-sql-database/recovery-point-logs-graph.png)

        <span data-ttu-id="2b217-515">The **Select restore point** menu closes, and the **Advanced Configuration** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-515">The **Select restore point** menu closes, and the **Advanced Configuration** menu opens.</span></span>

       ![Advanced configuration menu](./media/backup-azure-sql-database/restore-point-advanced-configuration.png)

    4. <span data-ttu-id="2b217-517">On the **Advanced Configuration** menu:</span><span class="sxs-lookup"><span data-stu-id="2b217-517">On the **Advanced Configuration** menu:</span></span>

        * <span data-ttu-id="2b217-518">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2b217-518">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span></span>
        * <span data-ttu-id="2b217-519">To change the restore location on the destination server, enter a new path in the **Target** column.</span><span class="sxs-lookup"><span data-stu-id="2b217-519">To change the restore location on the destination server, enter a new path in the **Target** column.</span></span>
        * <span data-ttu-id="2b217-520">Select **OK** to approve the settings.</span><span class="sxs-lookup"><span data-stu-id="2b217-520">Select **OK** to approve the settings.</span></span> <span data-ttu-id="2b217-521">Close the **Advanced Configuration** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-521">Close the **Advanced Configuration** menu.</span></span>

    5. <span data-ttu-id="2b217-522">On the **Restore** menu, select **Restore** to start the restore job.</span><span class="sxs-lookup"><span data-stu-id="2b217-522">On the **Restore** menu, select **Restore** to start the restore job.</span></span> <span data-ttu-id="2b217-523">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-523">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span></span>

       ![Restore job progress](./media/backup-azure-sql-database/restore-job-notification.png)

3. <span data-ttu-id="2b217-525">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-525">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span></span> <span data-ttu-id="2b217-526">To restore a point-in-time log, go back to step 2.</span><span class="sxs-lookup"><span data-stu-id="2b217-526">To restore a point-in-time log, go back to step 2.</span></span> <span data-ttu-id="2b217-527">This step restores a specific full or differential restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-527">This step restores a specific full or differential restore point.</span></span> <span data-ttu-id="2b217-528">You can see all of the full and differential recovery points for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="2b217-528">You can see all of the full and differential recovery points for the last 30 days.</span></span> <span data-ttu-id="2b217-529">To see recovery points older than 30 days, select **Filter** to open the **Filter restore points** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-529">To see recovery points older than 30 days, select **Filter** to open the **Filter restore points** menu.</span></span> <span data-ttu-id="2b217-530">For a differential recovery point, Azure Backup first restores the appropriate full recovery point, and then applies the selected differential recovery point.</span><span class="sxs-lookup"><span data-stu-id="2b217-530">For a differential recovery point, Azure Backup first restores the appropriate full recovery point, and then applies the selected differential recovery point.</span></span>

    ![Select restore point menu](./media/backup-azure-sql-database/recovery-point-menu.png)

    1. <span data-ttu-id="2b217-532">In the **Select restore point** menu, select **Full & Differential**.</span><span class="sxs-lookup"><span data-stu-id="2b217-532">In the **Select restore point** menu, select **Full & Differential**.</span></span>

       ![Select full and differential](./media/backup-azure-sql-database/recovery-point-logs-fd.png)

        <span data-ttu-id="2b217-534">The menu shows the list of available recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-534">The menu shows the list of available recovery points.</span></span>

    2. <span data-ttu-id="2b217-535">Select a recovery point from the list, and select **OK** to complete the restore point procedure.</span><span class="sxs-lookup"><span data-stu-id="2b217-535">Select a recovery point from the list, and select **OK** to complete the restore point procedure.</span></span> 

        ![Choose a full recovery point](./media/backup-azure-sql-database/choose-fd-recovery-point.png)

        <span data-ttu-id="2b217-537">The **Restore Point** menu closes, and the **Advanced Configuration** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-537">The **Restore Point** menu closes, and the **Advanced Configuration** menu opens.</span></span>

        ![Advanced Configuration menu](./media/backup-azure-sql-database/restore-point-advanced-configuration.png)

    3. <span data-ttu-id="2b217-539">On the **Advanced Configuration** menu:</span><span class="sxs-lookup"><span data-stu-id="2b217-539">On the **Advanced Configuration** menu:</span></span>

        * <span data-ttu-id="2b217-540">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2b217-540">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span></span> <span data-ttu-id="2b217-541">**Restore with NORECOVERY** is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="2b217-541">**Restore with NORECOVERY** is disabled by default.</span></span>
        * <span data-ttu-id="2b217-542">To change the restore location on the destination server, enter a new path in the **Target** column.</span><span class="sxs-lookup"><span data-stu-id="2b217-542">To change the restore location on the destination server, enter a new path in the **Target** column.</span></span>
        * <span data-ttu-id="2b217-543">Select **OK** to approve the settings.</span><span class="sxs-lookup"><span data-stu-id="2b217-543">Select **OK** to approve the settings.</span></span> <span data-ttu-id="2b217-544">Close the **Advanced Configuration** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-544">Close the **Advanced Configuration** menu.</span></span>

    4. <span data-ttu-id="2b217-545">On the **Restore** menu, select **Restore** to start the restore job.</span><span class="sxs-lookup"><span data-stu-id="2b217-545">On the **Restore** menu, select **Restore** to start the restore job.</span></span> <span data-ttu-id="2b217-546">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-546">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span></span>

       ![Restore job progress](./media/backup-azure-sql-database/restore-job-notification.png)

### <a name="restore-and-overwrite-the-database"></a><span data-ttu-id="2b217-548">Restore and overwrite the database</span><span class="sxs-lookup"><span data-stu-id="2b217-548">Restore and overwrite the database</span></span>

<span data-ttu-id="2b217-549">This procedure walks you through restoring data and overwriting a database.</span><span class="sxs-lookup"><span data-stu-id="2b217-549">This procedure walks you through restoring data and overwriting a database.</span></span> <span data-ttu-id="2b217-550">To restore to an alternate location, continue to [Restore to an alternate location](backup-azure-sql-database.md#restore-to-an-alternate-location).</span><span class="sxs-lookup"><span data-stu-id="2b217-550">To restore to an alternate location, continue to [Restore to an alternate location](backup-azure-sql-database.md#restore-to-an-alternate-location).</span></span> <span data-ttu-id="2b217-551">At this stage, your Recovery Services vault is open and the **Restore Configuration** menu is visible (see the following image).</span><span class="sxs-lookup"><span data-stu-id="2b217-551">At this stage, your Recovery Services vault is open and the **Restore Configuration** menu is visible (see the following image).</span></span> <span data-ttu-id="2b217-552">If you're not at this stage, start by [restoring a SQL database](backup-azure-sql-database.md#restore-a-sql-database).</span><span class="sxs-lookup"><span data-stu-id="2b217-552">If you're not at this stage, start by [restoring a SQL database](backup-azure-sql-database.md#restore-a-sql-database).</span></span>

![Restore Configuration menu](./media/backup-azure-sql-database/restore-overwrite-db.png)

<span data-ttu-id="2b217-554">On the **Restore Configuration** menu, the **Server** drop-down list box shows only the SQL Server instances that are registered with the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-554">On the **Restore Configuration** menu, the **Server** drop-down list box shows only the SQL Server instances that are registered with the Recovery Services vault.</span></span> <span data-ttu-id="2b217-555">If the server that you want isn't in the list, see [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases) to find the server.</span><span class="sxs-lookup"><span data-stu-id="2b217-555">If the server that you want isn't in the list, see [Discover SQL Server databases](backup-azure-sql-database.md#discover-sql-server-databases) to find the server.</span></span> <span data-ttu-id="2b217-556">During the discovery process, new servers are registered to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-556">During the discovery process, new servers are registered to the Recovery Services vault.</span></span>

1. <span data-ttu-id="2b217-557">In the **Restore Configuration** menu, select **Overwrite DB**, and then select **OK** to complete the configuration of the destination.</span><span class="sxs-lookup"><span data-stu-id="2b217-557">In the **Restore Configuration** menu, select **Overwrite DB**, and then select **OK** to complete the configuration of the destination.</span></span> 

   ![Select Overwrite DB](./media/backup-azure-sql-database/restore-configuration-overwrite-db.png)

    <span data-ttu-id="2b217-559">The **Server**, **Instance**, and **Restored DB Name** settings aren't necessary.</span><span class="sxs-lookup"><span data-stu-id="2b217-559">The **Server**, **Instance**, and **Restored DB Name** settings aren't necessary.</span></span>

2. <span data-ttu-id="2b217-560">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-560">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span></span> <span data-ttu-id="2b217-561">To restore to a specific point-in-time log, continue with this step.</span><span class="sxs-lookup"><span data-stu-id="2b217-561">To restore to a specific point-in-time log, continue with this step.</span></span> <span data-ttu-id="2b217-562">To restore a full and differential restore point, continue to step 3.</span><span class="sxs-lookup"><span data-stu-id="2b217-562">To restore a full and differential restore point, continue to step 3.</span></span>

    ![select restore point menu](./media/backup-azure-sql-database/recovery-point-menu.png)

    <span data-ttu-id="2b217-564">The point-in-time restore is available only for log backups for databases with a full and bulk-logged recovery model.</span><span class="sxs-lookup"><span data-stu-id="2b217-564">The point-in-time restore is available only for log backups for databases with a full and bulk-logged recovery model.</span></span> <span data-ttu-id="2b217-565">To restore to a specific second:</span><span class="sxs-lookup"><span data-stu-id="2b217-565">To restore to a specific second:</span></span>

    1. <span data-ttu-id="2b217-566">Select **Logs (Point in Time)** as the restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-566">Select **Logs (Point in Time)** as the restore point.</span></span>

        ![Choose the restore point type](./media/backup-azure-sql-database/recovery-point-logs.png)

    2. <span data-ttu-id="2b217-568">Under **Restore Date/Time**, select the mini calendar to open the **Calendar**.</span><span class="sxs-lookup"><span data-stu-id="2b217-568">Under **Restore Date/Time**, select the mini calendar to open the **Calendar**.</span></span> <span data-ttu-id="2b217-569">On the **Calendar**, the bold dates have recovery points and the current date is highlighted.</span><span class="sxs-lookup"><span data-stu-id="2b217-569">On the **Calendar**, the bold dates have recovery points and the current date is highlighted.</span></span> <span data-ttu-id="2b217-570">Select a date with recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-570">Select a date with recovery points.</span></span> <span data-ttu-id="2b217-571">Dates without recovery points can't be selected.</span><span class="sxs-lookup"><span data-stu-id="2b217-571">Dates without recovery points can't be selected.</span></span>

        ![Open the Calendar](./media/backup-azure-sql-database/recovery-point-logs-calendar.png)

        <span data-ttu-id="2b217-573">After you select a date, the timeline graph displays the available recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-573">After you select a date, the timeline graph displays the available recovery points.</span></span>

    3. <span data-ttu-id="2b217-574">Use the timeline graph or the **Time** dialog box to specify a specific time for the recovery point.</span><span class="sxs-lookup"><span data-stu-id="2b217-574">Use the timeline graph or the **Time** dialog box to specify a specific time for the recovery point.</span></span> <span data-ttu-id="2b217-575">Select **OK** to complete the restore point step.</span><span class="sxs-lookup"><span data-stu-id="2b217-575">Select **OK** to complete the restore point step.</span></span>
    
       ![Open the Calendar](./media/backup-azure-sql-database/recovery-point-logs-graph.png)

        <span data-ttu-id="2b217-577">The **Select restore point** menu closes, and the **Advanced Configuration** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-577">The **Select restore point** menu closes, and the **Advanced Configuration** menu opens.</span></span>

       ![Advanced configuration menu](./media/backup-azure-sql-database/restore-point-advanced-configuration.png)

    4. <span data-ttu-id="2b217-579">On the **Advanced Configuration** menu:</span><span class="sxs-lookup"><span data-stu-id="2b217-579">On the **Advanced Configuration** menu:</span></span>

        * <span data-ttu-id="2b217-580">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2b217-580">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span></span>
        * <span data-ttu-id="2b217-581">To change the restore location on the destination server, enter a new path in the **Target** column.</span><span class="sxs-lookup"><span data-stu-id="2b217-581">To change the restore location on the destination server, enter a new path in the **Target** column.</span></span>
        * <span data-ttu-id="2b217-582">Select **OK** to approve the settings.</span><span class="sxs-lookup"><span data-stu-id="2b217-582">Select **OK** to approve the settings.</span></span> <span data-ttu-id="2b217-583">Close the **Advanced Configuration** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-583">Close the **Advanced Configuration** menu.</span></span>

    5. <span data-ttu-id="2b217-584">On the **Restore** menu, select **Restore** to start the restore job.</span><span class="sxs-lookup"><span data-stu-id="2b217-584">On the **Restore** menu, select **Restore** to start the restore job.</span></span> <span data-ttu-id="2b217-585">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-585">Track the progress of the restore in the **Notifications** area or select **Restore jobs** on the database menu.</span></span>

       ![Restore job progress](./media/backup-azure-sql-database/restore-job-notification.png)

3. <span data-ttu-id="2b217-587">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-587">On the **Select restore point** menu, choose **Logs (Point in Time)** or **Full & Differential** as the restore point.</span></span> <span data-ttu-id="2b217-588">To restore a point-in-time log, go back to step 2.</span><span class="sxs-lookup"><span data-stu-id="2b217-588">To restore a point-in-time log, go back to step 2.</span></span> <span data-ttu-id="2b217-589">This step restores a specific full or differential restore point.</span><span class="sxs-lookup"><span data-stu-id="2b217-589">This step restores a specific full or differential restore point.</span></span> <span data-ttu-id="2b217-590">You can see all of the full and differential recovery points for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="2b217-590">You can see all of the full and differential recovery points for the last 30 days.</span></span> <span data-ttu-id="2b217-591">To see recovery points older than 30 days, select **Filter** to open the **Filter restore points** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-591">To see recovery points older than 30 days, select **Filter** to open the **Filter restore points** menu.</span></span> <span data-ttu-id="2b217-592">For a differential recovery point, Azure Backup first restores the appropriate full recovery point, and then applies the selected differential recovery point.</span><span class="sxs-lookup"><span data-stu-id="2b217-592">For a differential recovery point, Azure Backup first restores the appropriate full recovery point, and then applies the selected differential recovery point.</span></span>

    ![Select restore point menu](./media/backup-azure-sql-database/recovery-point-menu.png)

    1. <span data-ttu-id="2b217-594">In the **Select restore point** menu, select **Full & Differential**.</span><span class="sxs-lookup"><span data-stu-id="2b217-594">In the **Select restore point** menu, select **Full & Differential**.</span></span>

       ![Select full and differential](./media/backup-azure-sql-database/recovery-point-logs-fd.png)

        <span data-ttu-id="2b217-596">The menu shows the list of available recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-596">The menu shows the list of available recovery points.</span></span>

    2. <span data-ttu-id="2b217-597">Select a recovery point from the list, and select **OK** to complete the restore point procedure.</span><span class="sxs-lookup"><span data-stu-id="2b217-597">Select a recovery point from the list, and select **OK** to complete the restore point procedure.</span></span> 

        ![Choose a full recovery point](./media/backup-azure-sql-database/choose-fd-recovery-point.png)

        <span data-ttu-id="2b217-599">The **Restore Point** menu closes, and the **Advanced Configuration** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-599">The **Restore Point** menu closes, and the **Advanced Configuration** menu opens.</span></span>

        ![Advanced Configuration menu](./media/backup-azure-sql-database/restore-point-advanced-configuration.png)

    3. <span data-ttu-id="2b217-601">On the **Advanced Configuration** menu:</span><span class="sxs-lookup"><span data-stu-id="2b217-601">On the **Advanced Configuration** menu:</span></span>

        * <span data-ttu-id="2b217-602">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="2b217-602">To keep the database non-operational after the restore, set **Restore with NORECOVERY** to **Enabled**.</span></span> <span data-ttu-id="2b217-603">**Restore with NORECOVERY** is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="2b217-603">**Restore with NORECOVERY** is disabled by default.</span></span>
        * <span data-ttu-id="2b217-604">To change the restore location on the destination server, enter a new path in the **Target** column.</span><span class="sxs-lookup"><span data-stu-id="2b217-604">To change the restore location on the destination server, enter a new path in the **Target** column.</span></span>
        * <span data-ttu-id="2b217-605">Select **OK** to approve the settings.</span><span class="sxs-lookup"><span data-stu-id="2b217-605">Select **OK** to approve the settings.</span></span> <span data-ttu-id="2b217-606">Close the **Advanced Configuration** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-606">Close the **Advanced Configuration** menu.</span></span>

    4. <span data-ttu-id="2b217-607">On the **Restore** menu, select **Restore** to start the restore job.</span><span class="sxs-lookup"><span data-stu-id="2b217-607">On the **Restore** menu, select **Restore** to start the restore job.</span></span> <span data-ttu-id="2b217-608">Track the progress of the restore in the **Notifications** area or by selecting **Restore jobs** on the database menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-608">Track the progress of the restore in the **Notifications** area or by selecting **Restore jobs** on the database menu.</span></span>

       ![Restore job progress](./media/backup-azure-sql-database/restore-job-notification.png)

## <a name="manage-azure-backup-operations-for-sql-on-azure-vms"></a><span data-ttu-id="2b217-610">Manage Azure Backup operations for SQL on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="2b217-610">Manage Azure Backup operations for SQL on Azure VMs</span></span>

<span data-ttu-id="2b217-611">This section provides information about the various Azure Backup management operations that are available for SQL on Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2b217-611">This section provides information about the various Azure Backup management operations that are available for SQL on Azure virtual machines.</span></span> <span data-ttu-id="2b217-612">The following high-level operations exist:</span><span class="sxs-lookup"><span data-stu-id="2b217-612">The following high-level operations exist:</span></span>

* <span data-ttu-id="2b217-613">Monitor jobs</span><span class="sxs-lookup"><span data-stu-id="2b217-613">Monitor jobs</span></span>
* <span data-ttu-id="2b217-614">Backup alerts</span><span class="sxs-lookup"><span data-stu-id="2b217-614">Backup alerts</span></span>
* <span data-ttu-id="2b217-615">Stop protection on a SQL database</span><span class="sxs-lookup"><span data-stu-id="2b217-615">Stop protection on a SQL database</span></span>
* <span data-ttu-id="2b217-616">Resume protection for a SQL database</span><span class="sxs-lookup"><span data-stu-id="2b217-616">Resume protection for a SQL database</span></span>
* <span data-ttu-id="2b217-617">Trigger an adhoc backup job</span><span class="sxs-lookup"><span data-stu-id="2b217-617">Trigger an adhoc backup job</span></span>
* <span data-ttu-id="2b217-618">Unregister a server that's running SQL Server</span><span class="sxs-lookup"><span data-stu-id="2b217-618">Unregister a server that's running SQL Server</span></span>

### <a name="monitor-backup-jobs"></a><span data-ttu-id="2b217-619">Monitor backup jobs</span><span class="sxs-lookup"><span data-stu-id="2b217-619">Monitor backup jobs</span></span>
<span data-ttu-id="2b217-620">Azure Backup is an enterprise class solution that provides advanced backup alerts and notifications for any failures.</span><span class="sxs-lookup"><span data-stu-id="2b217-620">Azure Backup is an enterprise class solution that provides advanced backup alerts and notifications for any failures.</span></span> <span data-ttu-id="2b217-621">(See [View backup alerts](backup-azure-sql-database.md#view-backup-alerts).) To monitor specific jobs, use any of the following options according to your requirements.</span><span class="sxs-lookup"><span data-stu-id="2b217-621">(See [View backup alerts](backup-azure-sql-database.md#view-backup-alerts).) To monitor specific jobs, use any of the following options according to your requirements.</span></span>

#### <a name="use-the-azure-portal-for-adhoc-operations"></a><span data-ttu-id="2b217-622">Use the Azure portal for adhoc operations</span><span class="sxs-lookup"><span data-stu-id="2b217-622">Use the Azure portal for adhoc operations</span></span>
<span data-ttu-id="2b217-623">Azure Backup shows all manually triggered, or adhoc, jobs in the **Backup jobs** portal.</span><span class="sxs-lookup"><span data-stu-id="2b217-623">Azure Backup shows all manually triggered, or adhoc, jobs in the **Backup jobs** portal.</span></span> <span data-ttu-id="2b217-624">The jobs that are available in the **Backup jobs** portal include:</span><span class="sxs-lookup"><span data-stu-id="2b217-624">The jobs that are available in the **Backup jobs** portal include:</span></span>
- <span data-ttu-id="2b217-625">All configure backup operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-625">All configure backup operations.</span></span>
- <span data-ttu-id="2b217-626">Manually triggered backup operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-626">Manually triggered backup operations.</span></span>
- <span data-ttu-id="2b217-627">Restore operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-627">Restore operations.</span></span>
- <span data-ttu-id="2b217-628">Registration and discover database operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-628">Registration and discover database operations.</span></span>
- <span data-ttu-id="2b217-629">Stop backup operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-629">Stop backup operations.</span></span> 

![Backup jobs portal](./media/backup-azure-sql-database/jobs-list.png)

> [!NOTE]
> <span data-ttu-id="2b217-631">All scheduled backup jobs, including full, differential, and log backup, aren't shown in the **Backup jobs** portal.</span><span class="sxs-lookup"><span data-stu-id="2b217-631">All scheduled backup jobs, including full, differential, and log backup, aren't shown in the **Backup jobs** portal.</span></span> <span data-ttu-id="2b217-632">Use SQL Server Management Studio to monitor scheduled backup jobs, as described in the next section.</span><span class="sxs-lookup"><span data-stu-id="2b217-632">Use SQL Server Management Studio to monitor scheduled backup jobs, as described in the next section.</span></span>
>

#### <a name="use-sql-server-management-studio-for-backup-jobs"></a><span data-ttu-id="2b217-633">Use SQL Server Management Studio for backup jobs</span><span class="sxs-lookup"><span data-stu-id="2b217-633">Use SQL Server Management Studio for backup jobs</span></span>
<span data-ttu-id="2b217-634">Azure Backup uses SQL native APIs for all backup operations.</span><span class="sxs-lookup"><span data-stu-id="2b217-634">Azure Backup uses SQL native APIs for all backup operations.</span></span> <span data-ttu-id="2b217-635">Use the native APIs to fetch all job information from the [SQL backupset table](https://docs.microsoft.com/sql/relational-databases/system-tables/backupset-transact-sql?view=sql-server-2017) in the msdb database.</span><span class="sxs-lookup"><span data-stu-id="2b217-635">Use the native APIs to fetch all job information from the [SQL backupset table](https://docs.microsoft.com/sql/relational-databases/system-tables/backupset-transact-sql?view=sql-server-2017) in the msdb database.</span></span>

<span data-ttu-id="2b217-636">The following example is a query that fetches all backup jobs for a database named **DB1**.</span><span class="sxs-lookup"><span data-stu-id="2b217-636">The following example is a query that fetches all backup jobs for a database named **DB1**.</span></span> <span data-ttu-id="2b217-637">Customize the query for advanced monitoring.</span><span class="sxs-lookup"><span data-stu-id="2b217-637">Customize the query for advanced monitoring.</span></span>

```
select CAST (
Case type
                when 'D' 
                                 then 'Full'
                when  'I'
                               then 'Differential' 
                ELSE 'Log'
                END         
                AS varchar ) AS 'BackupType',
database_name, 
server_name,
machine_name,
backup_start_date,
backup_finish_date,
DATEDIFF(SECOND, backup_start_date, backup_finish_date) AS TimeTakenByBackupInSeconds,
backup_size AS BackupSizeInBytes
  from msdb.dbo.backupset where user_name = 'NT SERVICE\AzureWLBackupPluginSvc' AND database_name =  <DB1>  
 
```

### <a name="view-backup-alerts"></a><span data-ttu-id="2b217-638">View backup alerts</span><span class="sxs-lookup"><span data-stu-id="2b217-638">View backup alerts</span></span>

<span data-ttu-id="2b217-639">Because log backups occur every 15 minutes, occasionally, monitoring backup jobs can be tedious.</span><span class="sxs-lookup"><span data-stu-id="2b217-639">Because log backups occur every 15 minutes, occasionally, monitoring backup jobs can be tedious.</span></span> <span data-ttu-id="2b217-640">Azure Backup provides help in this situation.</span><span class="sxs-lookup"><span data-stu-id="2b217-640">Azure Backup provides help in this situation.</span></span> <span data-ttu-id="2b217-641">Email alerts are triggered for all backup failures.</span><span class="sxs-lookup"><span data-stu-id="2b217-641">Email alerts are triggered for all backup failures.</span></span> <span data-ttu-id="2b217-642">Alerts are consolidated at the database level by error code.</span><span class="sxs-lookup"><span data-stu-id="2b217-642">Alerts are consolidated at the database level by error code.</span></span> <span data-ttu-id="2b217-643">An email alert is sent only for the first backup failure for a database.</span><span class="sxs-lookup"><span data-stu-id="2b217-643">An email alert is sent only for the first backup failure for a database.</span></span> <span data-ttu-id="2b217-644">Sign in to the Azure portal to monitor all failures for a database.</span><span class="sxs-lookup"><span data-stu-id="2b217-644">Sign in to the Azure portal to monitor all failures for a database.</span></span> 

<span data-ttu-id="2b217-645">To monitor backup alerts:</span><span class="sxs-lookup"><span data-stu-id="2b217-645">To monitor backup alerts:</span></span>

1. <span data-ttu-id="2b217-646">Sign in to your Azure subscription in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b217-646">Sign in to your Azure subscription in the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="2b217-647">Open the Recovery Services vault that's registered with the SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-647">Open the Recovery Services vault that's registered with the SQL virtual machine.</span></span>

3. <span data-ttu-id="2b217-648">On the **Recovery Services vault** dashboard, select **Alerts and Events**.</span><span class="sxs-lookup"><span data-stu-id="2b217-648">On the **Recovery Services vault** dashboard, select **Alerts and Events**.</span></span> 

   ![Select Alerts and Events](./media/backup-azure-sql-database/vault-menu-alerts-events.png)

4. <span data-ttu-id="2b217-650">On the **Alerts and Events** menu, select **Backup Alerts** to view the list of alerts.</span><span class="sxs-lookup"><span data-stu-id="2b217-650">On the **Alerts and Events** menu, select **Backup Alerts** to view the list of alerts.</span></span>

   ![Select Backup Alerts](./media/backup-azure-sql-database/backup-alerts-dashboard.png)

### <a name="stop-protection-for-a-sql-server-database"></a><span data-ttu-id="2b217-652">Stop protection for a SQL Server database</span><span class="sxs-lookup"><span data-stu-id="2b217-652">Stop protection for a SQL Server database</span></span>

<span data-ttu-id="2b217-653">When you stop protection for a SQL Server database, Azure Backup requests whether to retain the recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-653">When you stop protection for a SQL Server database, Azure Backup requests whether to retain the recovery points.</span></span> <span data-ttu-id="2b217-654">There are two ways to stop protection for a SQL database:</span><span class="sxs-lookup"><span data-stu-id="2b217-654">There are two ways to stop protection for a SQL database:</span></span>

* <span data-ttu-id="2b217-655">Stop all future backup jobs and delete all recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-655">Stop all future backup jobs and delete all recovery points.</span></span>
* <span data-ttu-id="2b217-656">Stop all future backup jobs, but leave the recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-656">Stop all future backup jobs, but leave the recovery points.</span></span>

<span data-ttu-id="2b217-657">There's a cost to leave the recovery points.</span><span class="sxs-lookup"><span data-stu-id="2b217-657">There's a cost to leave the recovery points.</span></span> <span data-ttu-id="2b217-658">The recovery points for SQL incur the SQL protected instance pricing charge, plus the storage consumed.</span><span class="sxs-lookup"><span data-stu-id="2b217-658">The recovery points for SQL incur the SQL protected instance pricing charge, plus the storage consumed.</span></span> <span data-ttu-id="2b217-659">For more information about Azure Backup pricing for SQL, see the [Azure Backup pricing page](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="2b217-659">For more information about Azure Backup pricing for SQL, see the [Azure Backup pricing page](https://azure.microsoft.com/pricing/details/backup/).</span></span> 

<span data-ttu-id="2b217-660">To stop protection for a database:</span><span class="sxs-lookup"><span data-stu-id="2b217-660">To stop protection for a database:</span></span>

1. <span data-ttu-id="2b217-661">Open the Recovery Services vault that's registered with the SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-661">Open the Recovery Services vault that's registered with the SQL virtual machine.</span></span>

2. <span data-ttu-id="2b217-662">On the **Recovery Services vault** dashboard, under **Usage**, select **Backup Items** to open the **Backup Items** menu.</span><span class="sxs-lookup"><span data-stu-id="2b217-662">On the **Recovery Services vault** dashboard, under **Usage**, select **Backup Items** to open the **Backup Items** menu.</span></span>

    ![Open the Backup Items menu](./media/backup-azure-sql-database/restore-sql-vault-dashboard.png)<span data-ttu-id="2b217-664">.</span><span class="sxs-lookup"><span data-stu-id="2b217-664">.</span></span>

3. <span data-ttu-id="2b217-665">On the **Backup Items** menu, under **Backup Management Type**, select **SQL in Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="2b217-665">On the **Backup Items** menu, under **Backup Management Type**, select **SQL in Azure VM**.</span></span> 

    ![Select SQL in Azure VM](./media/backup-azure-sql-database/sql-restore-backup-items.png)

    <span data-ttu-id="2b217-667">The **Backup Items** menu shows the list of SQL databases.</span><span class="sxs-lookup"><span data-stu-id="2b217-667">The **Backup Items** menu shows the list of SQL databases.</span></span> 

4. <span data-ttu-id="2b217-668">In the list of SQL databases, select the database to stop protection.</span><span class="sxs-lookup"><span data-stu-id="2b217-668">In the list of SQL databases, select the database to stop protection.</span></span>

    ![Select the database to stop protection](./media/backup-azure-sql-database/sql-restore-sql-in-vm.png)

    <span data-ttu-id="2b217-670">When you select the database, its menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-670">When you select the database, its menu opens.</span></span>

5. <span data-ttu-id="2b217-671">On the menu for the selected database, select **Stop backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-671">On the menu for the selected database, select **Stop backup**.</span></span> 

    ![Select Stop backup](./media/backup-azure-sql-database/stop-db-button.png)

    <span data-ttu-id="2b217-673">The **Stop Backup** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-673">The **Stop Backup** menu opens.</span></span>

6. <span data-ttu-id="2b217-674">On the **Stop Backup** menu, choose to **Retain Backup Data** or **Delete Backup Data**.</span><span class="sxs-lookup"><span data-stu-id="2b217-674">On the **Stop Backup** menu, choose to **Retain Backup Data** or **Delete Backup Data**.</span></span> <span data-ttu-id="2b217-675">As an option, provide a reason for stopping the protection and a comment.</span><span class="sxs-lookup"><span data-stu-id="2b217-675">As an option, provide a reason for stopping the protection and a comment.</span></span>

    ![Stop Backup menu](./media/backup-azure-sql-database/stop-backup-button.png)

7. <span data-ttu-id="2b217-677">Select **Stop backup** to stop protection on the database.</span><span class="sxs-lookup"><span data-stu-id="2b217-677">Select **Stop backup** to stop protection on the database.</span></span> 

### <a name="resume-protection-for-a-sql-database"></a><span data-ttu-id="2b217-678">Resume protection for a SQL database</span><span class="sxs-lookup"><span data-stu-id="2b217-678">Resume protection for a SQL database</span></span>

<span data-ttu-id="2b217-679">If the **Retain Backup Data** option was selected when protection for the SQL database was stopped, you can resume protection.</span><span class="sxs-lookup"><span data-stu-id="2b217-679">If the **Retain Backup Data** option was selected when protection for the SQL database was stopped, you can resume protection.</span></span> <span data-ttu-id="2b217-680">If the backup data wasn't retained, protection can't resume.</span><span class="sxs-lookup"><span data-stu-id="2b217-680">If the backup data wasn't retained, protection can't resume.</span></span> 

1. <span data-ttu-id="2b217-681">To resume protection for the SQL database, open the backup item and select **Resume backup**.</span><span class="sxs-lookup"><span data-stu-id="2b217-681">To resume protection for the SQL database, open the backup item and select **Resume backup**.</span></span>

    ![Select Resume backup to resume database protection](./media/backup-azure-sql-database/resume-backup-button.png)

   <span data-ttu-id="2b217-683">The **Backup policy** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-683">The **Backup policy** menu opens.</span></span>

2. <span data-ttu-id="2b217-684">On the **Backup policy** menu, select a policy, and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="2b217-684">On the **Backup policy** menu, select a policy, and then select **Save**.</span></span>

### <a name="trigger-an-adhoc-backup"></a><span data-ttu-id="2b217-685">Trigger an adhoc backup</span><span class="sxs-lookup"><span data-stu-id="2b217-685">Trigger an adhoc backup</span></span>

<span data-ttu-id="2b217-686">Trigger adhoc backups as needed.</span><span class="sxs-lookup"><span data-stu-id="2b217-686">Trigger adhoc backups as needed.</span></span> <span data-ttu-id="2b217-687">There are four types of adhoc backups:</span><span class="sxs-lookup"><span data-stu-id="2b217-687">There are four types of adhoc backups:</span></span>

* <span data-ttu-id="2b217-688">Full backup</span><span class="sxs-lookup"><span data-stu-id="2b217-688">Full backup</span></span>
* <span data-ttu-id="2b217-689">Copy-only full backup</span><span class="sxs-lookup"><span data-stu-id="2b217-689">Copy-only full backup</span></span>
* <span data-ttu-id="2b217-690">Differential backup</span><span class="sxs-lookup"><span data-stu-id="2b217-690">Differential backup</span></span>
* <span data-ttu-id="2b217-691">Log backup</span><span class="sxs-lookup"><span data-stu-id="2b217-691">Log backup</span></span>

<span data-ttu-id="2b217-692">For details on each type, see [Types of SQL backups](https://docs.microsoft.com/sql/relational-databases/backup-restore/backup-overview-sql-server?view=sql-server-2017#types-of-backups).</span><span class="sxs-lookup"><span data-stu-id="2b217-692">For details on each type, see [Types of SQL backups](https://docs.microsoft.com/sql/relational-databases/backup-restore/backup-overview-sql-server?view=sql-server-2017#types-of-backups).</span></span>

### <a name="unregister-a-sql-server-instance"></a><span data-ttu-id="2b217-693">Unregister a SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="2b217-693">Unregister a SQL Server instance</span></span>

<span data-ttu-id="2b217-694">To unregister a SQL Server instance after you remove protection, but before you delete the vault:</span><span class="sxs-lookup"><span data-stu-id="2b217-694">To unregister a SQL Server instance after you remove protection, but before you delete the vault:</span></span>

1. <span data-ttu-id="2b217-695">Open the Recovery Services vault that's registered with the SQL virtual machine.</span><span class="sxs-lookup"><span data-stu-id="2b217-695">Open the Recovery Services vault that's registered with the SQL virtual machine.</span></span>

2. <span data-ttu-id="2b217-696">On the **Recovery Services vault** dashboard, under  **Manage**, select **Backup Infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="2b217-696">On the **Recovery Services vault** dashboard, under  **Manage**, select **Backup Infrastructure**.</span></span>  

   ![Select Backup Infrastructure](./media/backup-azure-sql-database/backup-infrastructure-button.png)

3. <span data-ttu-id="2b217-698">Under **Management Servers**, select **Protected Servers**.</span><span class="sxs-lookup"><span data-stu-id="2b217-698">Under **Management Servers**, select **Protected Servers**.</span></span>

   ![Select Protected Servers](./media/backup-azure-sql-database/protected-servers.png)

    <span data-ttu-id="2b217-700">The **Protected Servers** menu opens.</span><span class="sxs-lookup"><span data-stu-id="2b217-700">The **Protected Servers** menu opens.</span></span> 

4. <span data-ttu-id="2b217-701">On the **Protected Servers** menu, select the server to unregister.</span><span class="sxs-lookup"><span data-stu-id="2b217-701">On the **Protected Servers** menu, select the server to unregister.</span></span> <span data-ttu-id="2b217-702">To delete the vault, you must unregister all servers.</span><span class="sxs-lookup"><span data-stu-id="2b217-702">To delete the vault, you must unregister all servers.</span></span>

5. <span data-ttu-id="2b217-703">On the **Protected Servers** menu, right-click the protected server, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="2b217-703">On the **Protected Servers** menu, right-click the protected server, and select **Delete**.</span></span> 

   ![Select Delete](./media/backup-azure-sql-database/delete-protected-server.png)

## <a name="faq"></a><span data-ttu-id="2b217-705">FAQ</span><span class="sxs-lookup"><span data-stu-id="2b217-705">FAQ</span></span>

<span data-ttu-id="2b217-706">The following section provides additional information about SQL database backup.</span><span class="sxs-lookup"><span data-stu-id="2b217-706">The following section provides additional information about SQL database backup.</span></span>

### <a name="can-i-throttle-the-speed-of-the-sql-server-backup-policy"></a><span data-ttu-id="2b217-707">Can I throttle the speed of the SQL Server backup policy?</span><span class="sxs-lookup"><span data-stu-id="2b217-707">Can I throttle the speed of the SQL Server backup policy?</span></span>

<span data-ttu-id="2b217-708">Yes.</span><span class="sxs-lookup"><span data-stu-id="2b217-708">Yes.</span></span> <span data-ttu-id="2b217-709">You can throttle the rate at which the backup policy executes to minimize the impact on a SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="2b217-709">You can throttle the rate at which the backup policy executes to minimize the impact on a SQL Server instance.</span></span>

<span data-ttu-id="2b217-710">To change the setting:</span><span class="sxs-lookup"><span data-stu-id="2b217-710">To change the setting:</span></span>

1. <span data-ttu-id="2b217-711">On the SQL Server instance, in the C:\Program Files\Azure Workload Backup\bin folder, open the **TaskThrottlerSettings.json** file.</span><span class="sxs-lookup"><span data-stu-id="2b217-711">On the SQL Server instance, in the C:\Program Files\Azure Workload Backup\bin folder, open the **TaskThrottlerSettings.json** file.</span></span>

2. <span data-ttu-id="2b217-712">In the TaskThrottlerSettings.json file, change the **DefaultBackupTasksThreshold** setting to a lower value (for example, 5).</span><span class="sxs-lookup"><span data-stu-id="2b217-712">In the TaskThrottlerSettings.json file, change the **DefaultBackupTasksThreshold** setting to a lower value (for example, 5).</span></span>

3. <span data-ttu-id="2b217-713">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="2b217-713">Save your changes.</span></span> <span data-ttu-id="2b217-714">Close the file.</span><span class="sxs-lookup"><span data-stu-id="2b217-714">Close the file.</span></span>

4. <span data-ttu-id="2b217-715">On the SQL Server instance, open **Task Manager**.</span><span class="sxs-lookup"><span data-stu-id="2b217-715">On the SQL Server instance, open **Task Manager**.</span></span> <span data-ttu-id="2b217-716">Restart the **Azure Backup Workload Coordinator Service**.</span><span class="sxs-lookup"><span data-stu-id="2b217-716">Restart the **Azure Backup Workload Coordinator Service**.</span></span>

### <a name="can-i-run-a-full-backup-from-a-secondary-replica"></a><span data-ttu-id="2b217-717">Can I run a full backup from a secondary replica?</span><span class="sxs-lookup"><span data-stu-id="2b217-717">Can I run a full backup from a secondary replica?</span></span>

<span data-ttu-id="2b217-718">No.</span><span class="sxs-lookup"><span data-stu-id="2b217-718">No.</span></span> <span data-ttu-id="2b217-719">This feature isn't supported.</span><span class="sxs-lookup"><span data-stu-id="2b217-719">This feature isn't supported.</span></span>

### <a name="do-successful-backup-jobs-create-alerts"></a><span data-ttu-id="2b217-720">Do successful backup jobs create alerts?</span><span class="sxs-lookup"><span data-stu-id="2b217-720">Do successful backup jobs create alerts?</span></span>

<span data-ttu-id="2b217-721">No.</span><span class="sxs-lookup"><span data-stu-id="2b217-721">No.</span></span> <span data-ttu-id="2b217-722">Successful backup jobs don't generate alerts.</span><span class="sxs-lookup"><span data-stu-id="2b217-722">Successful backup jobs don't generate alerts.</span></span> <span data-ttu-id="2b217-723">Alerts are sent only for backup jobs that fail.</span><span class="sxs-lookup"><span data-stu-id="2b217-723">Alerts are sent only for backup jobs that fail.</span></span>

### <a name="can-i-see-details-for-scheduled-backup-jobs-in-the-jobs-menu"></a><span data-ttu-id="2b217-724">Can I see details for scheduled backup jobs in the Jobs menu?</span><span class="sxs-lookup"><span data-stu-id="2b217-724">Can I see details for scheduled backup jobs in the Jobs menu?</span></span>

<span data-ttu-id="2b217-725">No.</span><span class="sxs-lookup"><span data-stu-id="2b217-725">No.</span></span> <span data-ttu-id="2b217-726">The **Backup Jobs** menu shows adhoc job details, but not scheduled backup jobs.</span><span class="sxs-lookup"><span data-stu-id="2b217-726">The **Backup Jobs** menu shows adhoc job details, but not scheduled backup jobs.</span></span> <span data-ttu-id="2b217-727">If any scheduled backup jobs fail, the details are available in the failed job alerts.</span><span class="sxs-lookup"><span data-stu-id="2b217-727">If any scheduled backup jobs fail, the details are available in the failed job alerts.</span></span> <span data-ttu-id="2b217-728">To monitor all scheduled and adhoc backup jobs, use [SQL Server Management Studio](backup-azure-sql-database.md#use-sql-server-management-studio-for-backup-jobs).</span><span class="sxs-lookup"><span data-stu-id="2b217-728">To monitor all scheduled and adhoc backup jobs, use [SQL Server Management Studio](backup-azure-sql-database.md#use-sql-server-management-studio-for-backup-jobs).</span></span>

### <a name="when-i-select-a-sql-server-instance-are-future-databases-automatically-added"></a><span data-ttu-id="2b217-729">When I select a SQL Server instance are future databases automatically added?</span><span class="sxs-lookup"><span data-stu-id="2b217-729">When I select a SQL Server instance are future databases automatically added?</span></span>

<span data-ttu-id="2b217-730">No.</span><span class="sxs-lookup"><span data-stu-id="2b217-730">No.</span></span> <span data-ttu-id="2b217-731">When you configure protection for a SQL Server instance, if you select the server level option, all databases are added.</span><span class="sxs-lookup"><span data-stu-id="2b217-731">When you configure protection for a SQL Server instance, if you select the server level option, all databases are added.</span></span> <span data-ttu-id="2b217-732">If you add databases to a SQL Server instance after you configure protection, you must manually add the new databases to protect them.</span><span class="sxs-lookup"><span data-stu-id="2b217-732">If you add databases to a SQL Server instance after you configure protection, you must manually add the new databases to protect them.</span></span> <span data-ttu-id="2b217-733">The databases aren't automatically included in the configured protection.</span><span class="sxs-lookup"><span data-stu-id="2b217-733">The databases aren't automatically included in the configured protection.</span></span>

### <a name="if-i-change-the-recovery-model-how-do-i-restart-protection"></a><span data-ttu-id="2b217-734">If I change the recovery model, how do I restart protection?</span><span class="sxs-lookup"><span data-stu-id="2b217-734">If I change the recovery model, how do I restart protection?</span></span>

<span data-ttu-id="2b217-735">Trigger a full backup.</span><span class="sxs-lookup"><span data-stu-id="2b217-735">Trigger a full backup.</span></span> <span data-ttu-id="2b217-736">Log backups begin as expected.</span><span class="sxs-lookup"><span data-stu-id="2b217-736">Log backups begin as expected.</span></span>

### <a name="can-i-protect-sql-always-on-availability-groups-where-the-primary-replica-is-on-premises"></a><span data-ttu-id="2b217-737">Can I protect SQL Always On Availability Groups where the primary replica is on premises</span><span class="sxs-lookup"><span data-stu-id="2b217-737">Can I protect SQL Always On Availability Groups where the primary replica is on premises</span></span>

<span data-ttu-id="2b217-738">No.</span><span class="sxs-lookup"><span data-stu-id="2b217-738">No.</span></span> <span data-ttu-id="2b217-739">Azure Backup protects SQL Servers running in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b217-739">Azure Backup protects SQL Servers running in Azure.</span></span> <span data-ttu-id="2b217-740">If an Availability Group (AG) is spread between Azure and on-premises machines, the AG can be protected only if the primary replica is running in Azure.</span><span class="sxs-lookup"><span data-stu-id="2b217-740">If an Availability Group (AG) is spread between Azure and on-premises machines, the AG can be protected only if the primary replica is running in Azure.</span></span> <span data-ttu-id="2b217-741">Additionally, Azure Backup only protects the nodes running in the same Azure region as the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="2b217-741">Additionally, Azure Backup only protects the nodes running in the same Azure region as the Recovery Services vault.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b217-742">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b217-742">Next steps</span></span>

<span data-ttu-id="2b217-743">To learn more about Azure Backup, see the Azure PowerShell sample to back up encrypted virtual machines.</span><span class="sxs-lookup"><span data-stu-id="2b217-743">To learn more about Azure Backup, see the Azure PowerShell sample to back up encrypted virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2b217-744">Back up an encrypted VM</span><span class="sxs-lookup"><span data-stu-id="2b217-744">Back up an encrypted VM</span></span>](./scripts/backup-powershell-sample-backup-encrypted-vm.md)
