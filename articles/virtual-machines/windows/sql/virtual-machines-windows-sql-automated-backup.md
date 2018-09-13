---
title: Automated Backup for SQL Server 2014 Azure Virtual Machines | Microsoft Docs
description: Explains the Automated Backup feature for SQL Server 2014 VMs running in Azure. This article is specific to VMs using the Resource Manager.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-resource-manager
ms.assetid: bdc63fd1-db49-4e76-87d5-b5c6a890e53c
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/30/2017
ms.author: jroth
ms.openlocfilehash: 7a0394d72551d34c8da0a168ab2c903358bf0847
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563926"
---
# <a name="automated-backup-for-sql-server-2014-virtual-machines-resource-manager"></a><span data-ttu-id="0dc14-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="0dc14-104">Automated Backup for SQL Server 2014 Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-automated-backup.md)
> * [Classic](../classic/sql-automated-backup.md)
> 
> 

<span data-ttu-id="0dc14-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0dc14-107">Automated Backup automatically configures [Managed Backup to Microsoft Azure](https://msdn.microsoft.com/library/dn449496.aspx) for all existing and new databases on an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> <span data-ttu-id="0dc14-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="0dc14-108">This enables you to configure regular database backups that utilize durable Azure blob storage.</span></span> <span data-ttu-id="0dc14-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-109">Automated Backup depends on the [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="0dc14-110">To view the classic version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-110">To view the classic version of this article, see [Automated Backup for SQL Server in Azure Virtual Machines Classic](../classic/sql-automated-backup.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dc14-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0dc14-111">Prerequisites</span></span>
<span data-ttu-id="0dc14-112">To use Automated Backup, consider the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="0dc14-112">To use Automated Backup, consider the following prerequisites:</span></span>

<span data-ttu-id="0dc14-113">**Operating System**:</span><span class="sxs-lookup"><span data-stu-id="0dc14-113">**Operating System**:</span></span>

- <span data-ttu-id="0dc14-114">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="0dc14-114">Windows Server 2012</span></span>
- <span data-ttu-id="0dc14-115">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="0dc14-115">Windows Server 2012 R2</span></span>

<span data-ttu-id="0dc14-116">**SQL Server version/edition**:</span><span class="sxs-lookup"><span data-stu-id="0dc14-116">**SQL Server version/edition**:</span></span>

- <span data-ttu-id="0dc14-117">SQL Server 2014 Standard</span><span class="sxs-lookup"><span data-stu-id="0dc14-117">SQL Server 2014 Standard</span></span>
- <span data-ttu-id="0dc14-118">SQL Server 2014 Enterprise</span><span class="sxs-lookup"><span data-stu-id="0dc14-118">SQL Server 2014 Enterprise</span></span>

> [!IMPORTANT]
> Automated Backup works with SQL Server 2014. If you are using SQL Server 2016, you can use Automated Backup v2 to back up your databases. For more information, see [Automated Backup v2 for SQL Server 2016 Azure Virtual Machines](virtual-machines-windows-sql-automated-backup-v2.md).

<span data-ttu-id="0dc14-122">**Database configuration**:</span><span class="sxs-lookup"><span data-stu-id="0dc14-122">**Database configuration**:</span></span>

- <span data-ttu-id="0dc14-123">Target databases must use the full recovery model.</span><span class="sxs-lookup"><span data-stu-id="0dc14-123">Target databases must use the full recovery model.</span></span>

<span data-ttu-id="0dc14-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span><span class="sxs-lookup"><span data-stu-id="0dc14-124">For more information about the impact of the full recovery model on backups, see [Backup Under the Full Recovery Model](https://technet.microsoft.com/library/ms190217.aspx).</span></span>

<span data-ttu-id="0dc14-125">**Azure deployment model**:</span><span class="sxs-lookup"><span data-stu-id="0dc14-125">**Azure deployment model**:</span></span>

- <span data-ttu-id="0dc14-126">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0dc14-126">Resource Manager</span></span>

<span data-ttu-id="0dc14-127">**Azure PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="0dc14-127">**Azure PowerShell**:</span></span>

- <span data-ttu-id="0dc14-128">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs) if you plan to configure Automated Backup with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0dc14-128">[Install the latest Azure PowerShell commands](/powershell/azureps-cmdlets-docs) if you plan to configure Automated Backup with PowerShell.</span></span>

> [!NOTE]
> Automated Backup relies on the SQL Server IaaS Agent Extension. Current SQL virtual machine gallery images add this extension by default. For more information, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).

## <a name="settings"></a><span data-ttu-id="0dc14-132">Settings</span><span class="sxs-lookup"><span data-stu-id="0dc14-132">Settings</span></span>
<span data-ttu-id="0dc14-133">The following table describes the options that can be configured for Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="0dc14-133">The following table describes the options that can be configured for Automated Backup.</span></span> <span data-ttu-id="0dc14-134">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span><span class="sxs-lookup"><span data-stu-id="0dc14-134">The actual configuration steps vary depending on whether you use the Azure portal or Azure Windows PowerShell commands.</span></span>

| <span data-ttu-id="0dc14-135">Setting</span><span class="sxs-lookup"><span data-stu-id="0dc14-135">Setting</span></span> | <span data-ttu-id="0dc14-136">Range (Default)</span><span class="sxs-lookup"><span data-stu-id="0dc14-136">Range (Default)</span></span> | <span data-ttu-id="0dc14-137">Description</span><span class="sxs-lookup"><span data-stu-id="0dc14-137">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0dc14-138">**Automated Backup**</span><span class="sxs-lookup"><span data-stu-id="0dc14-138">**Automated Backup**</span></span> | <span data-ttu-id="0dc14-139">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="0dc14-139">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="0dc14-140">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="0dc14-140">Enables or disables Automated Backup for an Azure VM running SQL Server 2014 Standard or Enterprise.</span></span> |
| <span data-ttu-id="0dc14-141">**Retention Period**</span><span class="sxs-lookup"><span data-stu-id="0dc14-141">**Retention Period**</span></span> | <span data-ttu-id="0dc14-142">1-30 days (30 days)</span><span class="sxs-lookup"><span data-stu-id="0dc14-142">1-30 days (30 days)</span></span> | <span data-ttu-id="0dc14-143">The number of days to retain a backup.</span><span class="sxs-lookup"><span data-stu-id="0dc14-143">The number of days to retain a backup.</span></span> |
| <span data-ttu-id="0dc14-144">**Storage Account**</span><span class="sxs-lookup"><span data-stu-id="0dc14-144">**Storage Account**</span></span> | <span data-ttu-id="0dc14-145">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="0dc14-145">Azure storage account</span></span> | <span data-ttu-id="0dc14-146">An Azure storage account to use for storing Automated Backup files in blob storage.</span><span class="sxs-lookup"><span data-stu-id="0dc14-146">An Azure storage account to use for storing Automated Backup files in blob storage.</span></span> <span data-ttu-id="0dc14-147">A container is created at this location to store all backup files.</span><span class="sxs-lookup"><span data-stu-id="0dc14-147">A container is created at this location to store all backup files.</span></span> <span data-ttu-id="0dc14-148">The backup file naming convention includes the date, time, and machine name.</span><span class="sxs-lookup"><span data-stu-id="0dc14-148">The backup file naming convention includes the date, time, and machine name.</span></span> |
| <span data-ttu-id="0dc14-149">**Encryption**</span><span class="sxs-lookup"><span data-stu-id="0dc14-149">**Encryption**</span></span> | <span data-ttu-id="0dc14-150">Enable/Disable (Disabled)</span><span class="sxs-lookup"><span data-stu-id="0dc14-150">Enable/Disable (Disabled)</span></span> | <span data-ttu-id="0dc14-151">Enables or disables encryption.</span><span class="sxs-lookup"><span data-stu-id="0dc14-151">Enables or disables encryption.</span></span> <span data-ttu-id="0dc14-152">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span><span class="sxs-lookup"><span data-stu-id="0dc14-152">When encryption is enabled, the certificates used to restore the backup are located in the specified storage account in the same `automaticbackup` container using the same naming convention.</span></span> <span data-ttu-id="0dc14-153">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span><span class="sxs-lookup"><span data-stu-id="0dc14-153">If the password changes, a new certificate is generated with that password, but the old certificate remains to restore prior backups.</span></span> |
| <span data-ttu-id="0dc14-154">**Password**</span><span class="sxs-lookup"><span data-stu-id="0dc14-154">**Password**</span></span> | <span data-ttu-id="0dc14-155">Password text</span><span class="sxs-lookup"><span data-stu-id="0dc14-155">Password text</span></span> | <span data-ttu-id="0dc14-156">A password for encryption keys.</span><span class="sxs-lookup"><span data-stu-id="0dc14-156">A password for encryption keys.</span></span> <span data-ttu-id="0dc14-157">This is only required if encryption is enabled.</span><span class="sxs-lookup"><span data-stu-id="0dc14-157">This is only required if encryption is enabled.</span></span> <span data-ttu-id="0dc14-158">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span><span class="sxs-lookup"><span data-stu-id="0dc14-158">In order to restore an encrypted backup, you must have the correct password and related certificate that was used at the time the backup was taken.</span></span> |

## <a name="configuration-in-the-portal"></a><span data-ttu-id="0dc14-159">Configuration in the Portal</span><span class="sxs-lookup"><span data-stu-id="0dc14-159">Configuration in the Portal</span></span>
<span data-ttu-id="0dc14-160">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span><span class="sxs-lookup"><span data-stu-id="0dc14-160">You can use the Azure portal to configure Automated Backup during provisioning or for existing SQL Server 2014 VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="0dc14-161">New VMs</span><span class="sxs-lookup"><span data-stu-id="0dc14-161">New VMs</span></span>
<span data-ttu-id="0dc14-162">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="0dc14-162">Use the Azure portal to configure Automated Backup when you create a new SQL Server 2014 Virtual Machine in the Resource Manager deployment model.</span></span>

<span data-ttu-id="0dc14-163">In the **SQL Server settings** blade, select **Automated backup**.</span><span class="sxs-lookup"><span data-stu-id="0dc14-163">In the **SQL Server settings** blade, select **Automated backup**.</span></span> <span data-ttu-id="0dc14-164">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span><span class="sxs-lookup"><span data-stu-id="0dc14-164">The following Azure portal screenshot shows the **SQL Automated Backup** blade.</span></span>

![SQL Automated Backup configuration in Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup/azure-sql-arm-autobackup.png)

<span data-ttu-id="0dc14-166">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-166">For context, see the complete topic on [provisioning a SQL Server virtual machine in Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="0dc14-167">Existing VMs</span><span class="sxs-lookup"><span data-stu-id="0dc14-167">Existing VMs</span></span>
<span data-ttu-id="0dc14-168">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0dc14-168">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="0dc14-169">Then select the **SQL Server configuration** section of the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="0dc14-169">Then select the **SQL Server configuration** section of the **Settings** blade.</span></span>

![SQL Automated Backup for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-existing-vms.png)

<span data-ttu-id="0dc14-171">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span><span class="sxs-lookup"><span data-stu-id="0dc14-171">In the **SQL Server configuration** blade, click the **Edit** button in the Automated backup section.</span></span>

![Configure SQL Automated Backup for existing VMs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/sql/media/virtual-machines-windows-sql-automated-backup/azure-sql-rm-autobackup-configuration.png)

<span data-ttu-id="0dc14-173">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span><span class="sxs-lookup"><span data-stu-id="0dc14-173">When finished, click the **OK** button on the bottom of the **SQL Server configuration** blade to save your changes.</span></span>

<span data-ttu-id="0dc14-174">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span><span class="sxs-lookup"><span data-stu-id="0dc14-174">If you are enabling Automated Backup for the first time, Azure configures the SQL Server IaaS Agent in the background.</span></span> <span data-ttu-id="0dc14-175">During this time, the Azure portal might not show that Automated Backup is configured.</span><span class="sxs-lookup"><span data-stu-id="0dc14-175">During this time, the Azure portal might not show that Automated Backup is configured.</span></span> <span data-ttu-id="0dc14-176">Wait several minutes for the agent to be installed, configured.</span><span class="sxs-lookup"><span data-stu-id="0dc14-176">Wait several minutes for the agent to be installed, configured.</span></span> <span data-ttu-id="0dc14-177">After that the Azure portal will reflect the new settings.</span><span class="sxs-lookup"><span data-stu-id="0dc14-177">After that the Azure portal will reflect the new settings.</span></span>

> [!NOTE]
> You can also configure Automated Backup using a template. For more information, see [Azure quickstart template for Automated Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-autobackup-update).
> 
> 

## <a name="configuration-with-powershell"></a><span data-ttu-id="0dc14-180">Configuration with PowerShell</span><span class="sxs-lookup"><span data-stu-id="0dc14-180">Configuration with PowerShell</span></span>
<span data-ttu-id="0dc14-181">After provisioning your SQL VM, use PowerShell to configure Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="0dc14-181">After provisioning your SQL VM, use PowerShell to configure Automated Backup.</span></span> <span data-ttu-id="0dc14-182">Before you begin, you must:</span><span class="sxs-lookup"><span data-stu-id="0dc14-182">Before you begin, you must:</span></span>

- <span data-ttu-id="0dc14-183">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span><span class="sxs-lookup"><span data-stu-id="0dc14-183">[Download and install the latest Azure PowerShell](http://aka.ms/webpi-azps).</span></span>
- <span data-ttu-id="0dc14-184">Open Windows PowerShell and associate it with your account.</span><span class="sxs-lookup"><span data-stu-id="0dc14-184">Open Windows PowerShell and associate it with your account.</span></span> <span data-ttu-id="0dc14-185">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span><span class="sxs-lookup"><span data-stu-id="0dc14-185">You can do this by following the steps in the [Configure your subscription](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-ps-sql-create#configure-your-subscription) section of the provisioning topic.</span></span>

<span data-ttu-id="0dc14-186">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span><span class="sxs-lookup"><span data-stu-id="0dc14-186">In the following PowerShell example, Automated Backup is configured for an existing SQL Server 2014 VM.</span></span> <span data-ttu-id="0dc14-187">The **AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account associated with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0dc14-187">The **AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig** command configures the Automated Backup settings to store backups in the Azure storage account associated with the virtual machine.</span></span> <span data-ttu-id="0dc14-188">These backups will be retained for 10 days.</span><span class="sxs-lookup"><span data-stu-id="0dc14-188">These backups will be retained for 10 days.</span></span> <span data-ttu-id="0dc14-189">The **Set-AzureRmVMSqlServerExtension** command updates the specified Azure VM with these settings.</span><span class="sxs-lookup"><span data-stu-id="0dc14-189">The **Set-AzureRmVMSqlServerExtension** command updates the specified Azure VM with these settings.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $autobackupconfig = AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig -Enable -RetentionPeriodInDays 10 -ResourceGroupName $resourcegroupname

    Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="0dc14-190">It could take several minutes to install and configure the SQL Server IaaS Agent.</span><span class="sxs-lookup"><span data-stu-id="0dc14-190">It could take several minutes to install and configure the SQL Server IaaS Agent.</span></span>

<span data-ttu-id="0dc14-191">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span><span class="sxs-lookup"><span data-stu-id="0dc14-191">To enable encryption, modify the previous script to pass the **EnableEncryption** parameter along with a password (secure string) for the **CertificatePassword** parameter.</span></span> <span data-ttu-id="0dc14-192">The following script enables the Automated Backup settings in the previous example and adds encryption.</span><span class="sxs-lookup"><span data-stu-id="0dc14-192">The following script enables the Automated Backup settings in the previous example and adds encryption.</span></span>

    $vmname = "vmname"
    $resourcegroupname = "resourcegroupname"
    $password = "P@ssw0rd"
    $encryptionpassword = $password | ConvertTo-SecureString -AsPlainText -Force  
    $autobackupconfig = AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig -Enable -RetentionPeriod 10 -EnableEncryption -CertificatePassword $encryptionpassword -ResourceGroupName $resourcegroupname

    Set-AzureRmVMSqlServerExtension -AutoBackupSettings $autobackupconfig -VMName $vmname -ResourceGroupName $resourcegroupname

<span data-ttu-id="0dc14-193">To disable automatic backup, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig** command.</span><span class="sxs-lookup"><span data-stu-id="0dc14-193">To disable automatic backup, run the same script without the **-Enable** parameter to the **AzureRM.Compute\New-AzureVMSqlServerAutoBackupConfig** command.</span></span> <span data-ttu-id="0dc14-194">The absence of the **-Enable** parameter signals the command to disable the feature.</span><span class="sxs-lookup"><span data-stu-id="0dc14-194">The absence of the **-Enable** parameter signals the command to disable the feature.</span></span> <span data-ttu-id="0dc14-195">As with installation, it can take several minutes to disable Automated Backup.</span><span class="sxs-lookup"><span data-stu-id="0dc14-195">As with installation, it can take several minutes to disable Automated Backup.</span></span>

> [!NOTE]
> Removing the SQL Server IaaS Agent does not remove the previously configured Automated Backup settings. You should disable Automated Backup before disabling or uninstalling the SQL Server IaaS Agent.
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0dc14-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="0dc14-198">Next steps</span></span>
<span data-ttu-id="0dc14-199">Automated Backup configures Managed Backup on Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="0dc14-199">Automated Backup configures Managed Backup on Azure VMs.</span></span> <span data-ttu-id="0dc14-200">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span><span class="sxs-lookup"><span data-stu-id="0dc14-200">So it is important to [review the documentation for Managed Backup](https://msdn.microsoft.com/library/dn449496.aspx) to understand the behavior and implications.</span></span>

<span data-ttu-id="0dc14-201">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-201">You can find additional backup and restore guidance for SQL Server on Azure VMs in the following topic: [Backup and Restore for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md).</span></span>

<span data-ttu-id="0dc14-202">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-202">For information about other available automation tasks, see [SQL Server IaaS Agent Extension](virtual-machines-windows-sql-server-agent-extension.md).</span></span>

<span data-ttu-id="0dc14-203">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dc14-203">For more information about running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>




