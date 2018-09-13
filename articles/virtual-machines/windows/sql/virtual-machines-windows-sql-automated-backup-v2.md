---
title: Automated Backup v2 for SQL Server 2016 Azure Virtual Machines | Microsoft Docs
description: Explains the Automated Backup feature for SQL Server 2016 VMs running in Azure. This article is specific to VMs using the Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-resource-manager
ms.assetid: ebd23868-821c-475b-b867-06d4a2e310c7
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 04/05/2017
ms.author: jroth
ms.openlocfilehash: 17943bd23c2eaaa7f52815d690453fc81292aec0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550989"
---
# <a name="automated-backup-v2-for-sql-server-2016-azure-virtual-machines-resource-manager"></a><span data-ttu-id="e3850-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="e3850-104">Automated Backup v2 for SQL Server 2016 Azure Virtual Machines (Resource Manager)</span></span>

<span data-ttu-id="e3850-105">Automated Backup v2 automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span><span class="sxs-lookup"><span data-stu-id="e3850-105">Automated Backup v2 automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2016 Standard, Enterprise, or Developer editions.</span></span> <span data-ttu-id="e3850-106">This enables you to configure regular database backups that utilize durable Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="e3850-106">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="e3850-107">Automated Backup v2 depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-107">Automated Backup v2 depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a><span data-ttu-id="e3850-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e3850-108">Prerequisites</span></span>
<span data-ttu-id="e3850-109">To use Automated Backup v2, review the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="e3850-109">To use Automated Backup v2, review the following prerequisites:</span></span>

<span data-ttu-id="e3850-110">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="e3850-110">**Operating System**:</span></span>

- <span data-ttu-id="e3850-111">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="e3850-111">Windows Server 2012 R2</span></span>
- <span data-ttu-id="e3850-112">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="e3850-112">Windows Server 2016</span></span>

<span data-ttu-id="e3850-113">**SQL Server version/edition**:</span><span class="sxs-lookup"><span data-stu-id="e3850-113">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="e3850-114">SQL Server 2016 Standard</span><span class="sxs-lookup"><span data-stu-id="e3850-114">SQL Server 2016 Standard</span></span>
- <span data-ttu-id="e3850-115">SQL Server 2016 Enterprise</span><span class="sxs-lookup"><span data-stu-id="e3850-115">SQL Server 2016 Enterprise</span></span>
- <span data-ttu-id="e3850-116">SQL Server 2016 Developer</span><span class="sxs-lookup"><span data-stu-id="e3850-116">SQL Server 2016 Developer</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3850-117">Automated Backup v2 works with SQL Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e3850-117">Automated Backup v2 works with SQL Server 2016.</span></span> <span data-ttu-id="e3850-118">If you are using SQL Server 2014, you can use Automated Backup v1 to back up your databases.</span><span class="sxs-lookup"><span data-stu-id="e3850-118">If you are using SQL Server 2014, you can use Automated Backup v1 to back up your databases.</span></span> <span data-ttu-id="e3850-119">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-119">For more information, see [Automated Backup for SQL Server 2014 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).</span></span>

<span data-ttu-id="e3850-120">**Database configuration**:</span><span class="sxs-lookup"><span data-stu-id="e3850-120">**Database configuration**:</span></span>

- <span data-ttu-id="e3850-121">Target databases must use the full recovery model.</span><span class="sxs-lookup"><span data-stu-id="e3850-121">Target databases must use the full recovery model.</span></span>
- <span data-ttu-id="e3850-122">System databases do not have to use full recovery model.</span><span class="sxs-lookup"><span data-stu-id="e3850-122">System databases do not have to use full recovery model.</span></span> <span data-ttu-id="e3850-123">However, if you require log backups to be taken for Model or MSDB, you must use full recovery model.</span><span class="sxs-lookup"><span data-stu-id="e3850-123">However, if you require log backups to be taken for Model or MSDB, you must use full recovery model.</span></span>

<span data-ttu-id="e3850-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="e3850-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>

<span data-ttu-id="e3850-125">**Azure deployment model**:</span><span class="sxs-lookup"><span data-stu-id="e3850-125">**Azure deployment model**:</span></span>

- <span data-ttu-id="e3850-126">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e3850-126">Resource Manager</span></span>

> [!NOTE]
> <span data-ttu-id="e3850-127">Automated Backup relies on the **SQL Server IaaS Agent Extension**.</span><span class="sxs-lookup"><span data-stu-id="e3850-127">Automated Backup relies on the **SQL Server IaaS Agent Extension**.</span></span> <span data-ttu-id="e3850-128">Current SQL virtual machine gallery images add this extension by default.</span><span class="sxs-lookup"><span data-stu-id="e3850-128">Current SQL virtual machine gallery images add this extension by default.</span></span> <span data-ttu-id="e3850-129">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-129">For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="e3850-130">Settings</span><span class="sxs-lookup"><span data-stu-id="e3850-130">Settings</span></span>
<span data-ttu-id="e3850-131">The following table describes the options that can be configured for Automated Backup v2.</span><span class="sxs-lookup"><span data-stu-id="e3850-131">The following table describes the options that can be configured for Automated Backup v2.</span></span> <span data-ttu-id="e3850-132">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="e3850-132">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

### <a name="basic-settings"></a><span data-ttu-id="e3850-133">Basic Settings</span><span class="sxs-lookup"><span data-stu-id="e3850-133">Basic Settings</span></span>

| <span data-ttu-id="e3850-134">Setting</span><span class="sxs-lookup"><span data-stu-id="e3850-134">Setting</span></span> | <span data-ttu-id="e3850-135">Range (Default)</span><span class="sxs-lookup"><span data-stu-id="e3850-135">Range (Default)</span></span> | <span data-ttu-id="e3850-136">Description</span><span class="sxs-lookup"><span data-stu-id="e3850-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3850-137">**Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="e3850-137">**Automated Backup**</span></span> | <span data-ttu-id="e3850-138">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="e3850-138">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e3850-139">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="e3850-139">Enables or disables Automated Backup for an Azure VM running SQL Server 2016 Standard or Enterprise.</span></span> |
| <span data-ttu-id="e3850-140">**Retention Period**</span><span class="sxs-lookup"><span data-stu-id="e3850-140">**Retention Period**</span></span> | <span data-ttu-id="e3850-141">1-30 days (30 days)</span><span class="sxs-lookup"><span data-stu-id="e3850-141">1-30 days (30 days)</span></span> | <span data-ttu-id="e3850-142">The number of days to retain backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-142">The number of days to retain backups.</span></span> |
| <span data-ttu-id="e3850-143">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="e3850-143">**Storage Account**</span></span> | <span data-ttu-id="e3850-144">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="e3850-144">Azure storage account</span></span> | <span data-ttu-id="e3850-145">An Azure storage account to use for storing Automated Backup files in blob storage.</span><span class="sxs-lookup"><span data-stu-id="e3850-145">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="e3850-146">A container is created at this location to store all backup files.</span><span class="sxs-lookup"><span data-stu-id="e3850-146">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="e3850-147">The backup file naming convention includes the date, time, and database GUID.</span><span class="sxs-lookup"><span data-stu-id="e3850-147">The backup file naming convention includes the date, time, and database GUID.</span></span> |
| <span data-ttu-id="e3850-148">**Encryption**</span><span class="sxs-lookup"><span data-stu-id="e3850-148">**Encryption**</span></span> |<span data-ttu-id="e3850-149">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="e3850-149">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e3850-150">Enables or disables encryption.</span><span class="sxs-lookup"><span data-stu-id="e3850-150">Enables or disables encryption.</span></span> <span data-ttu-id="e3850-151">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same **automaticbackup** container using the same naming convention.</span><span class="sxs-lookup"><span data-stu-id="e3850-151">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same **automaticbackup** container using the same naming convention.</span></span> <span data-ttu-id="e3850-152">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-152">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="e3850-153">**Password**</span><span class="sxs-lookup"><span data-stu-id="e3850-153">**Password**</span></span> |<span data-ttu-id="e3850-154">Password text</span><span class="sxs-lookup"><span data-stu-id="e3850-154">Password text</span></span> | <span data-ttu-id="e3850-155">A password for encryption keys.</span><span class="sxs-lookup"><span data-stu-id="e3850-155">A password for encryption keys.</span></span> <span data-ttu-id="e3850-156">This is only required if encryption is enabled.</span><span class="sxs-lookup"><span data-stu-id="e3850-156">This is only required if encryption is enabled.</span></span> <span data-ttu-id="e3850-157">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span><span class="sxs-lookup"><span data-stu-id="e3850-157">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

### <a name="advanced-settings"></a><span data-ttu-id="e3850-158">Advanced Settings</span><span class="sxs-lookup"><span data-stu-id="e3850-158">Advanced Settings</span></span>

| <span data-ttu-id="e3850-159">Setting</span><span class="sxs-lookup"><span data-stu-id="e3850-159">Setting</span></span> | <span data-ttu-id="e3850-160">Range (Default)</span><span class="sxs-lookup"><span data-stu-id="e3850-160">Range (Default)</span></span> | <span data-ttu-id="e3850-161">Description</span><span class="sxs-lookup"><span data-stu-id="e3850-161">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e3850-162">**System Database Backups**</span><span class="sxs-lookup"><span data-stu-id="e3850-162">**System Database Backups**</span></span> | <span data-ttu-id="e3850-163">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="e3850-163">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="e3850-164">When enabled, this feature will also back up the system databases: Master, MSDB, and Model.</span><span class="sxs-lookup"><span data-stu-id="e3850-164">When enabled, this feature will also back up the system databases: Master, MSDB, and Model.</span></span> <span data-ttu-id="e3850-165">For the MSDB and Model databases, verify that they are in full recovery mode if you want log backups to be taken.</span><span class="sxs-lookup"><span data-stu-id="e3850-165">For the MSDB and Model databases, verify that they are in full recovery mode if you want log backups to be taken.</span></span> <span data-ttu-id="e3850-166">Log backups are never taken for Master.</span><span class="sxs-lookup"><span data-stu-id="e3850-166">Log backups are never taken for Master.</span></span> <span data-ttu-id="e3850-167">And no backups are taken for TempDB.</span><span class="sxs-lookup"><span data-stu-id="e3850-167">And no backups are taken for TempDB.</span></span> |
| <span data-ttu-id="e3850-168">**Backup Schedule**</span><span class="sxs-lookup"><span data-stu-id="e3850-168">**Backup Schedule**</span></span> | <span data-ttu-id="e3850-169">Manual/Automated (Automated)</span><span class="sxs-lookup"><span data-stu-id="e3850-169">Manual/Automated (Automated)</span></span> | <span data-ttu-id="e3850-170">By default, the backup schedule will be automatically determined based on the log growth.</span><span class="sxs-lookup"><span data-stu-id="e3850-170">By default, the backup schedule will be automatically determined based on the log growth.</span></span> <span data-ttu-id="e3850-171">Manual backup schedule allows the user to specify the time window for backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-171">Manual backup schedule allows the user to specify the time window for backups.</span></span> <span data-ttu-id="e3850-172">In this case, backups will only ever take place at the specified frequency and during the specified time window of a given day.</span><span class="sxs-lookup"><span data-stu-id="e3850-172">In this case, backups will only ever take place at the specified frequency and during the specified time window of a given day.</span></span> |
| <span data-ttu-id="e3850-173">**Full backup frequency**</span><span class="sxs-lookup"><span data-stu-id="e3850-173">**Full backup frequency**</span></span> | <span data-ttu-id="e3850-174">Daily/Weekly</span><span class="sxs-lookup"><span data-stu-id="e3850-174">Daily/Weekly</span></span> | <span data-ttu-id="e3850-175">Frequency of full backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-175">Frequency of full backups.</span></span> <span data-ttu-id="e3850-176">In both cases, full backups will begin during the next scheduled time window.</span><span class="sxs-lookup"><span data-stu-id="e3850-176">In both cases, full backups will begin during the next scheduled time window.</span></span> <span data-ttu-id="e3850-177">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span><span class="sxs-lookup"><span data-stu-id="e3850-177">When weekly is selected, backups could span multiple days until all databases have successfully backed up.</span></span> |
| <span data-ttu-id="e3850-178">**Full backup start time**</span><span class="sxs-lookup"><span data-stu-id="e3850-178">**Full backup start time**</span></span> | <span data-ttu-id="e3850-179">00:00 – 23:00 (01:00)</span><span class="sxs-lookup"><span data-stu-id="e3850-179">00:00 – 23:00 (01:00)</span></span> | <span data-ttu-id="e3850-180">Start time of a given day during which full backups can take place.</span><span class="sxs-lookup"><span data-stu-id="e3850-180">Start time of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e3850-181">**Full backup time window**</span><span class="sxs-lookup"><span data-stu-id="e3850-181">**Full backup time window**</span></span> | <span data-ttu-id="e3850-182">1 – 23 hours (1 hour)</span><span class="sxs-lookup"><span data-stu-id="e3850-182">1 – 23 hours (1 hour)</span></span> | <span data-ttu-id="e3850-183">Duration of the time window of a given day during which full backups can take place.</span><span class="sxs-lookup"><span data-stu-id="e3850-183">Duration of the time window of a given day during which full backups can take place.</span></span> |
| <span data-ttu-id="e3850-184">**Log backup frequency**</span><span class="sxs-lookup"><span data-stu-id="e3850-184">**Log backup frequency**</span></span> | <span data-ttu-id="e3850-185">5 – 60 minutes (60 minutes)</span><span class="sxs-lookup"><span data-stu-id="e3850-185">5 – 60 minutes (60 minutes)</span></span> | <span data-ttu-id="e3850-186">Frequency of log backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-186">Frequency of log backups.</span></span> |

## <a name="understanding-full-backup-frequency"></a><span data-ttu-id="e3850-187">Understanding full backup frequency</span><span class="sxs-lookup"><span data-stu-id="e3850-187">Understanding full backup frequency</span></span>
<span data-ttu-id="e3850-188">It is important to understand the difference between daily and weekly full backups.</span><span class="sxs-lookup"><span data-stu-id="e3850-188">It is important to understand the difference between daily and weekly full backups.</span></span> <span data-ttu-id="e3850-189">In this effort, we will walk through two example scenarios.</span><span class="sxs-lookup"><span data-stu-id="e3850-189">In this effort, we will walk through two example scenarios.</span></span>

### <a name="scenario-1-weekly-backups"></a><span data-ttu-id="e3850-190">Scenario 1: Weekly backups</span><span class="sxs-lookup"><span data-stu-id="e3850-190">Scenario 1: Weekly backups</span></span>
<span data-ttu-id="e3850-191">You have a SQL Server VM which contains a number of very large databases.</span><span class="sxs-lookup"><span data-stu-id="e3850-191">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e3850-192">On Monday, you enable Automated Backup v2 with the following settings:</span><span class="sxs-lookup"><span data-stu-id="e3850-192">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="e3850-193">Backup schedule: **Manual**</span><span class="sxs-lookup"><span data-stu-id="e3850-193">Backup schedule: **Manual**</span></span>
- <span data-ttu-id="e3850-194">Full backup frequency: **Weekly**</span><span class="sxs-lookup"><span data-stu-id="e3850-194">Full backup frequency: **Weekly**</span></span>
- <span data-ttu-id="e3850-195">Full backup start time: **01:00**</span><span class="sxs-lookup"><span data-stu-id="e3850-195">Full backup start time: **01:00**</span></span>
- <span data-ttu-id="e3850-196">Full backup time window: **1 hour**</span><span class="sxs-lookup"><span data-stu-id="e3850-196">Full backup time window: **1 hour**</span></span>

<span data-ttu-id="e3850-197">This means that the next available backup window is Tuesday at 1 AM for 1 hour.</span><span class="sxs-lookup"><span data-stu-id="e3850-197">This means that the next available backup window is Tuesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e3850-198">At that time, Automated Backup will begin backing up your databases one at a time.</span><span class="sxs-lookup"><span data-stu-id="e3850-198">At that time, Automated Backup will begin backing up your databases one at a time.</span></span> <span data-ttu-id="e3850-199">In this scenario, your databases are large enough that full backups will complete for the first couple databases.</span><span class="sxs-lookup"><span data-stu-id="e3850-199">In this scenario, your databases are large enough that full backups will complete for the first couple databases.</span></span> <span data-ttu-id="e3850-200">However, after one hour not all of the databases have been backed up.</span><span class="sxs-lookup"><span data-stu-id="e3850-200">However, after one hour not all of the databases have been backed up.</span></span>

<span data-ttu-id="e3850-201">When this happens, Automated Backup will begin backing up the remaining databases the next day, Wednesday at 1 AM for 1 hour.</span><span class="sxs-lookup"><span data-stu-id="e3850-201">When this happens, Automated Backup will begin backing up the remaining databases the next day, Wednesday at 1 AM for 1 hour.</span></span> <span data-ttu-id="e3850-202">If not all databases have been backed up in that time, it will try again the next day at the same time.</span><span class="sxs-lookup"><span data-stu-id="e3850-202">If not all databases have been backed up in that time, it will try again the next day at the same time.</span></span> <span data-ttu-id="e3850-203">This will continue until all databases have been successfully backed up.</span><span class="sxs-lookup"><span data-stu-id="e3850-203">This will continue until all databases have been successfully backed up.</span></span>

<span data-ttu-id="e3850-204">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span><span class="sxs-lookup"><span data-stu-id="e3850-204">Once it reaches Tuesday again, Automated Backup will begin backing up all databases once again.</span></span>

<span data-ttu-id="e3850-205">This scenario shows that Automated Backup will only operate within the specified time window, and each database will be backed up once per week.</span><span class="sxs-lookup"><span data-stu-id="e3850-205">This scenario shows that Automated Backup will only operate within the specified time window, and each database will be backed up once per week.</span></span> <span data-ttu-id="e3850-206">This also shows that it is possible for backups to span multiple days in the case where it is not possible to complete all backups in a single day.</span><span class="sxs-lookup"><span data-stu-id="e3850-206">This also shows that it is possible for backups to span multiple days in the case where it is not possible to complete all backups in a single day.</span></span>

### <a name="scenario-2-daily-backups"></a><span data-ttu-id="e3850-207">Scenario 2: Daily backups</span><span class="sxs-lookup"><span data-stu-id="e3850-207">Scenario 2: Daily backups</span></span>
<span data-ttu-id="e3850-208">You have a SQL Server VM which contains a number of very large databases.</span><span class="sxs-lookup"><span data-stu-id="e3850-208">You have a SQL Server VM which contains a number of very large databases.</span></span>

<span data-ttu-id="e3850-209">On Monday, you enable Automated Backup v2 with the following settings:</span><span class="sxs-lookup"><span data-stu-id="e3850-209">On Monday, you enable Automated Backup v2 with the following settings:</span></span>

- <span data-ttu-id="e3850-210">Backup schedule: Manual</span><span class="sxs-lookup"><span data-stu-id="e3850-210">Backup schedule: Manual</span></span>
- <span data-ttu-id="e3850-211">Full backup frequency: Daily</span><span class="sxs-lookup"><span data-stu-id="e3850-211">Full backup frequency: Daily</span></span>
- <span data-ttu-id="e3850-212">Full backup start time: 22:00</span><span class="sxs-lookup"><span data-stu-id="e3850-212">Full backup start time: 22:00</span></span>
- <span data-ttu-id="e3850-213">Full backup time window: 6 hours</span><span class="sxs-lookup"><span data-stu-id="e3850-213">Full backup time window: 6 hours</span></span>

<span data-ttu-id="e3850-214">This means that the next available backup window is Monday at 10 PM for 6 hours.</span><span class="sxs-lookup"><span data-stu-id="e3850-214">This means that the next available backup window is Monday at 10 PM for 6 hours.</span></span> <span data-ttu-id="e3850-215">At that time, Automated Backup will begin backing up your databases one at a time.</span><span class="sxs-lookup"><span data-stu-id="e3850-215">At that time, Automated Backup will begin backing up your databases one at a time.</span></span>

<span data-ttu-id="e3850-216">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span><span class="sxs-lookup"><span data-stu-id="e3850-216">Then, on Tuesday at 10 for 6 hours, full backups of all databases will start again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3850-217">When scheduling daily backups, it is recommended that you schedule a wide time window to ensure all databases can be backed up within this time.</span><span class="sxs-lookup"><span data-stu-id="e3850-217">When scheduling daily backups, it is recommended that you schedule a wide time window to ensure all databases can be backed up within this time.</span></span> <span data-ttu-id="e3850-218">This is especially important in the case where you have a large amount of data to back up.</span><span class="sxs-lookup"><span data-stu-id="e3850-218">This is especially important in the case where you have a large amount of data to back up.</span></span>

## <a name="configuration-in-the-portal"></a><span data-ttu-id="e3850-219">Configuration in the Portal</span><span class="sxs-lookup"><span data-stu-id="e3850-219">Configuration in the Portal</span></span>
<span data-ttu-id="e3850-220">You can use the Azure portal to configure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span><span class="sxs-lookup"><span data-stu-id="e3850-220">You can use the Azure portal to configure Automated Backup v2 during provisioning or for existing SQL Server 2016 VMs.</span></span> 

### <a name="new-vms"></a><span data-ttu-id="e3850-221">New VMs</span><span class="sxs-lookup"><span data-stu-id="e3850-221">New VMs</span></span>
<span data-ttu-id="e3850-222">Use the Azure portal to configure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="e3850-222">Use the Azure portal to configure Automated Backup v2 when you create a new SQL Server 2016 Virtual Machine in the Resource Manager deployment model.</span></span> 

<span data-ttu-id="e3850-223">In the **SQL Server settings** blade, select **Automated backup**.</span><span class="sxs-lookup"><span data-stu-id="e3850-223">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="e3850-224">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="e3850-224">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![SQL Automated Backup configuration in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup-v2/automated-backup-blade.png)

> [!NOTE]
> <span data-ttu-id="e3850-226">Automated Backup v2 is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="e3850-226">Automated Backup v2 is disabled by default.</span></span>

<span data-ttu-id="e3850-227">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-227">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="e3850-228">Existing VMs</span><span class="sxs-lookup"><span data-stu-id="e3850-228">Existing VMs</span></span>
<span data-ttu-id="e3850-229">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e3850-229">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="e3850-230">Then select the **SQL Server configuration** section of the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="e3850-230">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL Automated Backup for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration.png)

<span data-ttu-id="e3850-232">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span><span class="sxs-lookup"><span data-stu-id="e3850-232">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configure SQL Automated Backup for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup-v2/sql-server-configuration-edit.png)

<span data-ttu-id="e3850-234">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span><span class="sxs-lookup"><span data-stu-id="e3850-234">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="e3850-235">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span><span class="sxs-lookup"><span data-stu-id="e3850-235">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="e3850-236">During this time, the Azure portal might not show that Automated Backup is configured.</span><span class="sxs-lookup"><span data-stu-id="e3850-236">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="e3850-237">Wait several minutes for the agent to be installed, configured.</span><span class="sxs-lookup"><span data-stu-id="e3850-237">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="e3850-238">After that the Azure portal will reflect the new settings.</span><span class="sxs-lookup"><span data-stu-id="e3850-238">After that the Azure portal will reflect the new settings.</span></span>

## <a name="configuration-with-powershell"></a><span data-ttu-id="e3850-239">Configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="e3850-239">Configuration with PowerShell</span></span>
<span data-ttu-id="e3850-240">You can use PowerShell to configure Automated Backup v2.</span><span class="sxs-lookup"><span data-stu-id="e3850-240">You can use PowerShell to configure Automated Backup v2.</span></span> <span data-ttu-id="e3850-241">Before you begin, you must:</span><span class="sxs-lookup"><span data-stu-id="e3850-241">Before you begin, you must:</span></span>

- <span data-ttu-id="e3850-242">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="e3850-242">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="e3850-243">Open Windows PowerShell and associate it with your account.</span><span class="sxs-lookup"><span data-stu-id="e3850-243">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="e3850-244">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span><span class="sxs-lookup"><span data-stu-id="e3850-244">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

### <a name="install-the-sql-iaas-extension"></a><span data-ttu-id="e3850-245">Install the SQL IaaS Extension</span><span class="sxs-lookup"><span data-stu-id="e3850-245">Install the SQL IaaS Extension</span></span>
<span data-ttu-id="e3850-246">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span><span class="sxs-lookup"><span data-stu-id="e3850-246">If you provisioned a SQL Server virtual machine from the Azure portal, the SQL Server IaaS Extension should already be installed.</span></span> <span data-ttu-id="e3850-247">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span><span class="sxs-lookup"><span data-stu-id="e3850-247">You can determine if it is installed for your VM by calling **Get-AzureRmVM** command and examining the **Extensions** property.</span></span>

```powershell
$vmname = "vmname"
$resourcegroupname = "resourcegroupname"

(Get-AzureRmVM -Name $vmname -ResourceGroupName $resourcegroupname).Extensions 
```

<span data-ttu-id="e3850-248">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span><span class="sxs-lookup"><span data-stu-id="e3850-248">If the SQL Server IaaS Agent extension is installed, you should see it listed as “SqlIaaSAgent” or “SQLIaaSExtension”.</span></span> <span data-ttu-id="e3850-249">**ProvisioningState** for the extension should also show “Succeeded”.</span><span class="sxs-lookup"><span data-stu-id="e3850-249">**ProvisioningState** for the extension should also show “Succeeded”.</span></span> 

<span data-ttu-id="e3850-250">If it is not installed or failed to be provisioned, you can install it with the following command.</span><span class="sxs-lookup"><span data-stu-id="e3850-250">If it is not installed or failed to be provisioned, you can install it with the following command.</span></span> <span data-ttu-id="e3850-251">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span><span class="sxs-lookup"><span data-stu-id="e3850-251">In addition to the VM name and resource group, you must also specify the region (**$region**) that your VM is located in.</span></span>

```powershell
$region = “EASTUS2”
Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region 
```

### <a name="a-idverifysettings-verify-current-settings"></a><span data-ttu-id="e3850-252"><a id="verifysettings"> Verify current settings</span><span class="sxs-lookup"><span data-stu-id="e3850-252"><a id="verifysettings"> Verify current settings</span></span>
<span data-ttu-id="e3850-253">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span><span class="sxs-lookup"><span data-stu-id="e3850-253">If you enabled automated backup during provisioning, you can use PowerShell to check your current configuration.</span></span> <span data-ttu-id="e3850-254">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span><span class="sxs-lookup"><span data-stu-id="e3850-254">Run the **Get-AzureRmVMSqlServerExtension** command and examine the **AutoBackupSettings** property:</span></span>

```powershell
(Get-AzureRmVMSqlServerExtension -VMName $vmname -ResourceGroupName $resourcegroupname).AutoBackupSettings
```

<span data-ttu-id="e3850-255">You should get output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="e3850-255">You should get output similar to the following:</span></span>

```
Enable                      : True
EnableEncryption            : False
RetentionPeriod             : 30
StorageUrl                  : https://test.blob.core.windows.net/
StorageAccessKey            :  
Password                    : 
BackupSystemDbs             : False
BackupScheduleType          : Manual
FullBackupFrequency         : WEEKLY
FullBackupStartTime         : 2
FullBackupWindowHours       : 2
LogBackupFrequency          : 60
```

<span data-ttu-id="e3850-256">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span><span class="sxs-lookup"><span data-stu-id="e3850-256">If your output shows that **Enable** is set to **False**, then you have to enable automated backup.</span></span> <span data-ttu-id="e3850-257">The good news is that you enable and configure Automated Backup in the same way.</span><span class="sxs-lookup"><span data-stu-id="e3850-257">The good news is that you enable and configure Automated Backup in the same way.</span></span> <span data-ttu-id="e3850-258">See the next section for this information.</span><span class="sxs-lookup"><span data-stu-id="e3850-258">See the next section for this information.</span></span>

> [!NOTE] 
> <span data-ttu-id="e3850-259">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span><span class="sxs-lookup"><span data-stu-id="e3850-259">If you check the settings immediately after making a change, it is possible that you will get back the old configuration values.</span></span> <span data-ttu-id="e3850-260">Wait a few minutes and check the settings again to make sure that your changes were applied.</span><span class="sxs-lookup"><span data-stu-id="e3850-260">Wait a few minutes and check the settings again to make sure that your changes were applied.</span></span>

### <a name="configure-automated-backup-v2"></a><span data-ttu-id="e3850-261">Configure Automated Backup v2</span><span class="sxs-lookup"><span data-stu-id="e3850-261">Configure Automated Backup v2</span></span>
<span data-ttu-id="e3850-262">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span><span class="sxs-lookup"><span data-stu-id="e3850-262">You can use PowerShell to enable Automated Backup as well as to modify its configuration and behavior at any time.</span></span> 

<span data-ttu-id="e3850-263">First, select or create a storage account for the backup files.</span><span class="sxs-lookup"><span data-stu-id="e3850-263">First, select or create a storage account for the backup files.</span></span> <span data-ttu-id="e3850-264">The following script selects a storage account or creates it if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="e3850-264">The following script selects a storage account or creates it if it does not exist.</span></span>

```powershell
$storage_accountname = “yourstorageaccount”
$storage_resourcegroupname = $resourcegroupname

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region } 
```

> [!NOTE]
> <span data-ttu-id="e3850-265">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e3850-265">Automated Backup does not support storing backups in premium storage, but it can take backups from VM disks which use Premium Storage.</span></span>

<span data-ttu-id="e3850-266">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup v2 settings to store backups in the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="e3850-266">Then use the **New-AzureRmVMSqlServerAutoBackupConfig** command to enable and configure the Automated Backup v2 settings to store backups in the Azure storage account.</span></span> <span data-ttu-id="e3850-267">In this example, the backups are set to be retained for 10 days.</span><span class="sxs-lookup"><span data-stu-id="e3850-267">In this example, the backups are set to be retained for 10 days.</span></span> <span data-ttu-id="e3850-268">System database backups are enabled.</span><span class="sxs-lookup"><span data-stu-id="e3850-268">System database backups are enabled.</span></span> <span data-ttu-id="e3850-269">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span><span class="sxs-lookup"><span data-stu-id="e3850-269">Full backups are scheduled for weekly with a time window starting at 20:00 for two hours.</span></span> <span data-ttu-id="e3850-270">Log backups are scheduled for every 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="e3850-270">Log backups are scheduled for every 30 minutes.</span></span> <span data-ttu-id="e3850-271">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span><span class="sxs-lookup"><span data-stu-id="e3850-271">The second command, **Set-AzureRmVMSqlServerExtension**, updates the specified Azure VM with these settings.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname 
```

<span data-ttu-id="e3850-272">It could take several minutes to install and configure the SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="e3850-272">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span> 

<span data-ttu-id="e3850-273">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="e3850-273">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="e3850-274">The following script enables the Automated Backup settings in the previous example and adds encryption.</span><span class="sxs-lookup"><span data-stu-id="e3850-274">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

```powershell
$password = "P@ssw0rd"
$encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -EnableEncryption -CertificatePassword $encryptionpassword `
    -RetentionPeriodInDays 10 -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType Manual -FullBackupFrequency Weekly `
    -FullBackupStartHour 20 -FullBackupWindowInHours 2 `
    -LogBackupFrequencyInMinutes 30 

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="e3850-275">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span><span class="sxs-lookup"><span data-stu-id="e3850-275">To confirm your settings are applied, [verify the Automated Backup configuration](#verifysettings).</span></span>

### <a name="disable-automated-backup"></a><span data-ttu-id="e3850-276">Disable Automated Backup</span><span class="sxs-lookup"><span data-stu-id="e3850-276">Disable Automated Backup</span></span>
<span data-ttu-id="e3850-277">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span><span class="sxs-lookup"><span data-stu-id="e3850-277">To disable Automated Backup, run the same script without the **-Enable** parameter to the **New-AzureRmVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="e3850-278">The absence of the **-Enable** parameter signals the command to disable the feature.</span><span class="sxs-lookup"><span data-stu-id="e3850-278">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="e3850-279">As with installation, it can take several minutes to disable Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="e3850-279">As with installation, it can take several minutes to disable Automated Backup.</span></span>

```powershell
$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -ResourceGroupName $storage_resourcegroupname

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

### <a name="example-script"></a><span data-ttu-id="e3850-280">Example script</span><span class="sxs-lookup"><span data-stu-id="e3850-280">Example script</span></span>
<span data-ttu-id="e3850-281">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span><span class="sxs-lookup"><span data-stu-id="e3850-281">The following script provides a set of variables that you can customize to enable and configure Automated Backup for your VM.</span></span> <span data-ttu-id="e3850-282">In your case, you might need to customize the script based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="e3850-282">In your case, you might need to customize the script based on your requirements.</span></span> <span data-ttu-id="e3850-283">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span><span class="sxs-lookup"><span data-stu-id="e3850-283">For example, you would have to make changes if you wanted to disable the backup of system databases or enable encryption.</span></span>

```powershell
$vmname = "yourvmname"
$resourcegroupname = "vmresourcegroupname"
$region = “Azure region name such as EASTUS2”
$storage_accountname = “storageaccountname”
$storage_resourcegroupname = $resourcegroupname
$retentionperiod = 10
$backupscheduletype = "Manual"
$fullbackupfrequency = "Weekly"
$fullbackupstarthour = "20"
$fullbackupwindow = "2"
$logbackupfrequency = "30"

# ResourceGroupName is the resource group which is hosting the VM where you are deploying the SQL IaaS Extension 

Set-AzureRmVMSqlServerExtension -VMName $vmname `
    -ResourceGroupName $resourcegroupname -Name "SQLIaasExtension" `
    -Version "1.2" -Location $region

# Creates/use a storage account to store the backups

$storage = Get-AzureRmStorageAccount -ResourceGroupName $resourcegroupname `
    -Name $storage_accountname -ErrorAction SilentlyContinue
If (-Not $storage)
    { $storage = New-AzureRmStorageAccount -ResourceGroupName $storage_resourcegroupname `
    -Name $storage_accountname -SkuName Standard_GRS -Location $region }

# Configure Automated Backup settings

$autobackupconfig = New-AzureRmVMSqlServerAutoBackupConfig -Enable `
    -RetentionPeriodInDays $retentionperiod -StorageContext $storage.Context `
    -ResourceGroupName $storage_resourcegroupname -BackupSystemDbs `
    -BackupScheduleType $backupscheduletype -FullBackupFrequency $fullbackupfrequency `
    -FullBackupStartHour $fullbackupstarthour -FullBackupWindowInHours $fullbackupwindow `
    -LogBackupFrequencyInMinutes $logbackupfrequency

# Apply the Automated Backup settings to the VM

Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig `
    -VMName $vmname -ResourceGroupName $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="e3850-284">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3850-284">Next steps</span></span>
<span data-ttu-id="e3850-285">Automated Backup v2 configures Managed Backup on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="e3850-285">Automated Backup v2 configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="e3850-286">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span><span class="sxs-lookup"><span data-stu-id="e3850-286">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="e3850-287">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-287">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="e3850-288">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-288">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="e3850-289">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e3850-289">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>




