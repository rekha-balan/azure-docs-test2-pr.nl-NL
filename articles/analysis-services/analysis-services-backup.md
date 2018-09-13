---
title: Azure Analysis Services database backup and restore | Microsoft Docs
description: Describes how to backup and restore an Azure Analysis Services database.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
ms.assetid: ''
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: owend
ms.openlocfilehash: 5f09ccec5ab4f62fdfc4a4fb6efddccbe2672cb0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549840"
---
# <a name="backup-and-restore"></a><span data-ttu-id="dead2-103">Backup and restore</span><span class="sxs-lookup"><span data-stu-id="dead2-103">Backup and restore</span></span>

<span data-ttu-id="dead2-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="dead2-104">Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services.</span></span> <span data-ttu-id="dead2-105">The primary difference is where you store your backup files.</span><span class="sxs-lookup"><span data-stu-id="dead2-105">The primary difference is where you store your backup files.</span></span> <span data-ttu-id="dead2-106">Backup files must be saved to a container in an [Azure storage account](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="dead2-106">Backup files must be saved to a container in an [Azure storage account](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="dead2-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span><span class="sxs-lookup"><span data-stu-id="dead2-107">You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.</span></span>

> [!NOTE]
> <span data-ttu-id="dead2-108">Creating a storage account can result in a new billable service.</span><span class="sxs-lookup"><span data-stu-id="dead2-108">Creating a storage account can result in a new billable service.</span></span> <span data-ttu-id="dead2-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span><span class="sxs-lookup"><span data-stu-id="dead2-109">To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).</span></span>
> 
> 

<span data-ttu-id="dead2-110">Backups are saved with a .abf extension.</span><span class="sxs-lookup"><span data-stu-id="dead2-110">Backups are saved with a .abf extension.</span></span> <span data-ttu-id="dead2-111">For in-memory tabular models, both model data and metadata are stored.</span><span class="sxs-lookup"><span data-stu-id="dead2-111">For in-memory tabular models, both model data and metadata are stored.</span></span> <span data-ttu-id="dead2-112">For Direct Query tabular models, only model metadata is stored.</span><span class="sxs-lookup"><span data-stu-id="dead2-112">For Direct Query tabular models, only model metadata is stored.</span></span> <span data-ttu-id="dead2-113">Backups can be compressed and encrypted, depending on the options you choose.</span><span class="sxs-lookup"><span data-stu-id="dead2-113">Backups can be compressed and encrypted, depending on the options you choose.</span></span> 



## <a name="configure-storage-settings"></a><span data-ttu-id="dead2-114">Configure storage settings</span><span class="sxs-lookup"><span data-stu-id="dead2-114">Configure storage settings</span></span>
<span data-ttu-id="dead2-115">Before backing up, you need to configure storage settings for your server.</span><span class="sxs-lookup"><span data-stu-id="dead2-115">Before backing up, you need to configure storage settings for your server.</span></span>


### <a name="to-configure-storage-settings"></a><span data-ttu-id="dead2-116">To configure storage settings</span><span class="sxs-lookup"><span data-stu-id="dead2-116">To configure storage settings</span></span>
1.  <span data-ttu-id="dead2-117">In Azure portal > **Settings**, click **Backup**.</span><span class="sxs-lookup"><span data-stu-id="dead2-117">In Azure portal > **Settings**, click **Backup**.</span></span>

    ![Backups in Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-backups.png)

2.  <span data-ttu-id="dead2-119">Click **Enabled**, then click **Storage Settings**.</span><span class="sxs-lookup"><span data-stu-id="dead2-119">Click **Enabled**, then click **Storage Settings**.</span></span>

    ![Enable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-enable.png)

3. <span data-ttu-id="dead2-121">Select your storage account or create a new one.</span><span class="sxs-lookup"><span data-stu-id="dead2-121">Select your storage account or create a new one.</span></span>

4. <span data-ttu-id="dead2-122">Select a container or create a new one.</span><span class="sxs-lookup"><span data-stu-id="dead2-122">Select a container or create a new one.</span></span>

    ![Select container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-container.png)

5. <span data-ttu-id="dead2-124">Save your backup settings.</span><span class="sxs-lookup"><span data-stu-id="dead2-124">Save your backup settings.</span></span> <span data-ttu-id="dead2-125">You must save your changes whenever you change storage settings, or enable or disable backup.</span><span class="sxs-lookup"><span data-stu-id="dead2-125">You must save your changes whenever you change storage settings, or enable or disable backup.</span></span>

    ![Save backup settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a><span data-ttu-id="dead2-127">Backup</span><span class="sxs-lookup"><span data-stu-id="dead2-127">Backup</span></span>

### <a name="to-backup-by-using-ssms"></a><span data-ttu-id="dead2-128">To backup by using SSMS</span><span class="sxs-lookup"><span data-stu-id="dead2-128">To backup by using SSMS</span></span>

1. <span data-ttu-id="dead2-129">In SSMS, right-click a database > **Back Up**.</span><span class="sxs-lookup"><span data-stu-id="dead2-129">In SSMS, right-click a database > **Back Up**.</span></span>

2. <span data-ttu-id="dead2-130">In **Backup Database** > **Backup file**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="dead2-130">In **Backup Database** > **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="dead2-131">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span><span class="sxs-lookup"><span data-stu-id="dead2-131">In the **Save file as** dialog, verify the folder path, and then type a name for the backup file.</span></span> <span data-ttu-id="dead2-132">By default, the file name is given a .abf extension.</span><span class="sxs-lookup"><span data-stu-id="dead2-132">By default, the file name is given a .abf extension.</span></span> 

4. <span data-ttu-id="dead2-133">In the **Backup Database** dialog, select options.</span><span class="sxs-lookup"><span data-stu-id="dead2-133">In the **Backup Database** dialog, select options.</span></span>

    <span data-ttu-id="dead2-134">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span><span class="sxs-lookup"><span data-stu-id="dead2-134">**Allow file overwrite** - Select this option to overwrite backup files of the same name.</span></span> <span data-ttu-id="dead2-135">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span><span class="sxs-lookup"><span data-stu-id="dead2-135">If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.</span></span>

    <span data-ttu-id="dead2-136">**Apply compression** - Select this option to compress the backup file.</span><span class="sxs-lookup"><span data-stu-id="dead2-136">**Apply compression** - Select this option to compress the backup file.</span></span> <span data-ttu-id="dead2-137">Compressed backup files save disk space, but require slightly higher CPU utilization.</span><span class="sxs-lookup"><span data-stu-id="dead2-137">Compressed backup files save disk space, but require slightly higher CPU utilization.</span></span> 

    <span data-ttu-id="dead2-138">**Encrypt backup file** - Select this option to encrypt the backup file.</span><span class="sxs-lookup"><span data-stu-id="dead2-138">**Encrypt backup file** - Select this option to encrypt the backup file.</span></span> <span data-ttu-id="dead2-139">This option requires a user-supplied password to secure the backup file.</span><span class="sxs-lookup"><span data-stu-id="dead2-139">This option requires a user-supplied password to secure the backup file.</span></span> <span data-ttu-id="dead2-140">The password prevents reading of the backup data any other means than a restore operation.</span><span class="sxs-lookup"><span data-stu-id="dead2-140">The password prevents reading of the backup data any other means than a restore operation.</span></span> <span data-ttu-id="dead2-141">If you choose to encrypt backups, store the password in a safe location.</span><span class="sxs-lookup"><span data-stu-id="dead2-141">If you choose to encrypt backups, store the password in a safe location.</span></span>

5. <span data-ttu-id="dead2-142">Click **OK** to create and save the backup file.</span><span class="sxs-lookup"><span data-stu-id="dead2-142">Click **OK** to create and save the backup file.</span></span>


### <a name="powershell"></a><span data-ttu-id="dead2-143">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dead2-143">PowerShell</span></span>
<span data-ttu-id="dead2-144">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dead2-144">Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.</span></span>

## <a name="restore"></a><span data-ttu-id="dead2-145">Restore</span><span class="sxs-lookup"><span data-stu-id="dead2-145">Restore</span></span>
<span data-ttu-id="dead2-146">When restoring, your backup file must be in the storage account you've configured for your server.</span><span class="sxs-lookup"><span data-stu-id="dead2-146">When restoring, your backup file must be in the storage account you've configured for your server.</span></span> <span data-ttu-id="dead2-147">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/storage-use-azcopy.md) command-line utility.</span><span class="sxs-lookup"><span data-stu-id="dead2-147">If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/storage-use-azcopy.md) command-line utility.</span></span> 

<span data-ttu-id="dead2-148">If you're restoring a tabular 1200 model database from an on-premises SQL Server Analysis Services server, you must first remove all of the domain users from the model's roles, and add them back to the roles as Azure Active Directory users.</span><span class="sxs-lookup"><span data-stu-id="dead2-148">If you're restoring a tabular 1200 model database from an on-premises SQL Server Analysis Services server, you must first remove all of the domain users from the model's roles, and add them back to the roles as Azure Active Directory users.</span></span> <span data-ttu-id="dead2-149">The roles will be the same.</span><span class="sxs-lookup"><span data-stu-id="dead2-149">The roles will be the same.</span></span>

### <a name="to-restore-by-using-ssms"></a><span data-ttu-id="dead2-150">To restore by using SSMS</span><span class="sxs-lookup"><span data-stu-id="dead2-150">To restore by using SSMS</span></span>

1. <span data-ttu-id="dead2-151">In SSMS, right-click a database > **Restore**.</span><span class="sxs-lookup"><span data-stu-id="dead2-151">In SSMS, right-click a database > **Restore**.</span></span>

2. <span data-ttu-id="dead2-152">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="dead2-152">In the **Backup Database** dialog, in **Backup file**, click **Browse**.</span></span>

3. <span data-ttu-id="dead2-153">In the **Locate Database Files** dialog, select the file you want to restore.</span><span class="sxs-lookup"><span data-stu-id="dead2-153">In the **Locate Database Files** dialog, select the file you want to restore.</span></span>

4. <span data-ttu-id="dead2-154">In **Restore database**, select the database.</span><span class="sxs-lookup"><span data-stu-id="dead2-154">In **Restore database**, select the database.</span></span>

5. <span data-ttu-id="dead2-155">Specify options.</span><span class="sxs-lookup"><span data-stu-id="dead2-155">Specify options.</span></span> <span data-ttu-id="dead2-156">Security options must match the backup options you used when backing up.</span><span class="sxs-lookup"><span data-stu-id="dead2-156">Security options must match the backup options you used when backing up.</span></span>


### <a name="powershell"></a><span data-ttu-id="dead2-157">PowerShell</span><span class="sxs-lookup"><span data-stu-id="dead2-157">PowerShell</span></span>

<span data-ttu-id="dead2-158">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dead2-158">Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.</span></span>


## <a name="related-information"></a><span data-ttu-id="dead2-159">Related information</span><span class="sxs-lookup"><span data-stu-id="dead2-159">Related information</span></span>

[<span data-ttu-id="dead2-160">Azure storage accounts</span><span class="sxs-lookup"><span data-stu-id="dead2-160">Azure storage accounts</span></span>](../storage/storage-create-storage-account.md)  
<span data-ttu-id="dead2-161">[High availablility](analysis-services-bcdr.md)   </span><span class="sxs-lookup"><span data-stu-id="dead2-161">[High availablility](analysis-services-bcdr.md)   </span></span>  
[<span data-ttu-id="dead2-162">Manage Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="dead2-162">Manage Azure Analysis Services</span></span>](analysis-services-manage.md)




