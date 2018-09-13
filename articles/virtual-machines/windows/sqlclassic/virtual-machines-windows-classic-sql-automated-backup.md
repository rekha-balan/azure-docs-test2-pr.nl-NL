---
title: Automated Backup for SQL Server Virtual Machines (Classic) | Microsoft Docs
description: 'Explains the Automated Backup feature for SQL Server running in Azure Virtual Machines using Resource Manager. '
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-service-management
ms.assetid: 3333e830-8a60-42f5-9f44-8e02e9868d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/18/2017
ms.author: jroth
ms.openlocfilehash: 5771c7d1716f126570759cd4a3c53ebd3d30adf4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551035"
---
# <a name="automated-backup-for-sql-server-in-azure-virtual-machines-classic"></a><span data-ttu-id="a54f2-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span><span class="sxs-lookup"><span data-stu-id="a54f2-103">Automated Backup for SQL Server in Azure Virtual Machines (Classic)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md)
> * [Classic](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="a54f2-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a54f2-106">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="a54f2-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="a54f2-107">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="a54f2-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a54f2-108">Automated Backup depends on the [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. To view the Resource Manager version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Resource Manager](../sql/virtual-machines-windows-sql-automated-backup.md).

## <a name="prerequisites"></a><span data-ttu-id="a54f2-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a54f2-113">Prerequisites</span></span>
<span data-ttu-id="a54f2-114">To use Automated Backup, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="a54f2-114">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="a54f2-115">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="a54f2-115">**Operating System**:</span></span>

* <span data-ttu-id="a54f2-116">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a54f2-116">Windows Server 2012</span></span>
* <span data-ttu-id="a54f2-117">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a54f2-117">Windows Server 2012 R2</span></span>

<span data-ttu-id="a54f2-118">**SQL Server version/edition**:</span><span class="sxs-lookup"><span data-stu-id="a54f2-118">**SQL Server version/edition**:</span></span>

* <span data-ttu-id="a54f2-119">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="a54f2-119">SQL Server 2014 Standard</span></span>
* <span data-ttu-id="a54f2-120">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="a54f2-120">SQL Server 2014 Enterprise</span></span>

> [!NOTE]
> SQL Server 2016 is not yet supported for Automated Backup.
> 
> 

<span data-ttu-id="a54f2-122">**Database configuration**:</span><span class="sxs-lookup"><span data-stu-id="a54f2-122">**Database configuration**:</span></span>

* <span data-ttu-id="a54f2-123">Target databases must use the full recovery model.</span><span class="sxs-lookup"><span data-stu-id="a54f2-123">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="a54f2-124">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="a54f2-124">**Azure PowerShell**:</span></span>

* <span data-ttu-id="a54f2-125">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="a54f2-125">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="a54f2-126">**SQL Server IaaS Extension**:</span><span class="sxs-lookup"><span data-stu-id="a54f2-126">**SQL Server IaaS Extension**:</span></span>

* <span data-ttu-id="a54f2-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a54f2-127">[Install the SQL Server IaaS Extension](../classic/sql-server-agent-extension.md).</span></span>

## <a name="settings"></a><span data-ttu-id="a54f2-128">Settings</span><span class="sxs-lookup"><span data-stu-id="a54f2-128">Settings</span></span>
<span data-ttu-id="a54f2-129">The following table describes the options that can be configured for Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="a54f2-129">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="a54f2-130">For classic VMs, you must use PowerShell to configure these settings.</span><span class="sxs-lookup"><span data-stu-id="a54f2-130">For classic VMs, you must use PowerShell to configure these settings.</span></span>

| <span data-ttu-id="a54f2-131">Setting</span><span class="sxs-lookup"><span data-stu-id="a54f2-131">Setting</span></span> | <span data-ttu-id="a54f2-132">Range (Default)</span><span class="sxs-lookup"><span data-stu-id="a54f2-132">Range (Default)</span></span> | <span data-ttu-id="a54f2-133">Description</span><span class="sxs-lookup"><span data-stu-id="a54f2-133">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a54f2-134">**Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="a54f2-134">**Automated Backup**</span></span> |<span data-ttu-id="a54f2-135">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="a54f2-135">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a54f2-136">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a54f2-136">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="a54f2-137">**Retention Period**</span><span class="sxs-lookup"><span data-stu-id="a54f2-137">**Retention Period**</span></span> |<span data-ttu-id="a54f2-138">1-30 days (30 days)</span><span class="sxs-lookup"><span data-stu-id="a54f2-138">1-30 days (30 days)</span></span> |<span data-ttu-id="a54f2-139">The number of days to retain a backup.</span><span class="sxs-lookup"><span data-stu-id="a54f2-139">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="a54f2-140">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="a54f2-140">**Storage Account**</span></span> |<span data-ttu-id="a54f2-141">Azure storage account (the storage account created for the specified VM)</span><span class="sxs-lookup"><span data-stu-id="a54f2-141">Azure storage account (the storage account created for the specified VM)</span></span> |<span data-ttu-id="a54f2-142">An Azure storage account to use for storing Automated Backup files in blob storage.</span><span class="sxs-lookup"><span data-stu-id="a54f2-142">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="a54f2-143">A container is created at this location to store all backup files.</span><span class="sxs-lookup"><span data-stu-id="a54f2-143">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="a54f2-144">The backup file naming convention includes the date, time, and machine name.</span><span class="sxs-lookup"><span data-stu-id="a54f2-144">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="a54f2-145">**Encryption**</span><span class="sxs-lookup"><span data-stu-id="a54f2-145">**Encryption**</span></span> |<span data-ttu-id="a54f2-146">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="a54f2-146">Enable/Disable (Disabled)</span></span> |<span data-ttu-id="a54f2-147">Enables or disables encryption.</span><span class="sxs-lookup"><span data-stu-id="a54f2-147">Enables or disables encryption.</span></span> <span data-ttu-id="a54f2-148">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span><span class="sxs-lookup"><span data-stu-id="a54f2-148">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same automaticbackup container using the same naming convention.</span></span> <span data-ttu-id="a54f2-149">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span><span class="sxs-lookup"><span data-stu-id="a54f2-149">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="a54f2-150">**Password**</span><span class="sxs-lookup"><span data-stu-id="a54f2-150">**Password**</span></span> |<span data-ttu-id="a54f2-151">Password text (None)</span><span class="sxs-lookup"><span data-stu-id="a54f2-151">Password text (None)</span></span> |<span data-ttu-id="a54f2-152">A password for encryption keys.</span><span class="sxs-lookup"><span data-stu-id="a54f2-152">A password for encryption keys.</span></span> <span data-ttu-id="a54f2-153">This is only required if encryption is enabled.</span><span class="sxs-lookup"><span data-stu-id="a54f2-153">This is only required if encryption is enabled.</span></span> <span data-ttu-id="a54f2-154">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span><span class="sxs-lookup"><span data-stu-id="a54f2-154">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> | <span data-ttu-id="a54f2-155">**Backup system databases**</span><span class="sxs-lookup"><span data-stu-id="a54f2-155">**Backup system databases**</span></span> | <span data-ttu-id="a54f2-156">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="a54f2-156">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="a54f2-157">Take full backups of Master, Model, and MSDB</span><span class="sxs-lookup"><span data-stu-id="a54f2-157">Take full backups of Master, Model, and MSDB</span></span> |
| <span data-ttu-id="a54f2-158">**Configure backup schedule**</span><span class="sxs-lookup"><span data-stu-id="a54f2-158">**Configure backup schedule**</span></span> | <span data-ttu-id="a54f2-159">Manual/Automated (Automated)</span><span class="sxs-lookup"><span data-stu-id="a54f2-159">Manual/Automated (Automated)</span></span> | <span data-ttu-id="a54f2-160">Select **Automated** to automatically take full and log backups based on log growth.</span><span class="sxs-lookup"><span data-stu-id="a54f2-160">Select **Automated** to automatically take full and log backups based on log growth.</span></span> <span data-ttu-id="a54f2-161">Select **Manual** to specify the schedule for full and log backups.</span><span class="sxs-lookup"><span data-stu-id="a54f2-161">Select **Manual** to specify the schedule for full and log backups.</span></span> |

## <a name="configuration-with-powershell"></a><span data-ttu-id="a54f2-162">Configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="a54f2-162">Configuration with PowerShell</span></span>
<span data-ttu-id="a54f2-163">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span><span class="sxs-lookup"><span data-stu-id="a54f2-163">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="a54f2-164">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span><span class="sxs-lookup"><span data-stu-id="a54f2-164">The **New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account specified by the $storageaccount variable.</span></span> <span data-ttu-id="a54f2-165">These backups will be retained for 10 days.</span><span class="sxs-lookup"><span data-stu-id="a54f2-165">These backups will be retained for 10 days.</span></span> <span data-ttu-id="a54f2-166">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span><span class="sxs-lookup"><span data-stu-id="a54f2-166">The **Set-AzureVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="a54f2-167">It could take several minutes to install and configure the SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="a54f2-167">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="a54f2-168">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span><span class="sxs-lookup"><span data-stu-id="a54f2-168">To enable encryption, modify the previous script to pass the EnableEncryption parameter along with a password (secure string) for the CertificatePassword parameter.</span></span> <span data-ttu-id="a54f2-169">The following script enables the Automated Backup settings in the previous example and adds encryption.</span><span class="sxs-lookup"><span data-stu-id="a54f2-169">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $storageaccount = "<storageaccountname>"
    $storageaccountkey = (Get-AzureStorageKey -StorageAccountName $storageaccount).Primary
    $storagecontext = New-AzureStorageContext -StorageAccountName $storageaccount -StorageAccountKey $storageaccountkey
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = New-AzureVMSqlServerAutoBackupConfig -StorageContext $storagecontext -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword

    Get-AzureVM -ServiceName <vmservicename> -Name <vmname> | Set-AzureVMSqlServerExtension -AutoBackupSettings $autobackupconfig | Update-AzureVM

<span data-ttu-id="a54f2-170">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span><span class="sxs-lookup"><span data-stu-id="a54f2-170">To disable automatic backup, run the same script without the **-Enable** parameter to the **New-AzureVMSqlServerAutoBackupConfig**.</span></span> <span data-ttu-id="a54f2-171">As with installation, it can take several minutes to disable Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="a54f2-171">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> Disabling and uninstalling the SQL Server IaaS Agent does not remove the previously configured Managed Backup settings. You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a54f2-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="a54f2-174">Next steps</span></span>
<span data-ttu-id="a54f2-175">Automated Backup configures Managed Backup on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="a54f2-175">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="a54f2-176">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span><span class="sxs-lookup"><span data-stu-id="a54f2-176">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="a54f2-177">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a54f2-177">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-backup-recovery.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).</span></span>

<span data-ttu-id="a54f2-178">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="a54f2-178">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](../classic/sql-server-agent-extension.md).</span></span>

<span data-ttu-id="a54f2-179">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a54f2-179">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

