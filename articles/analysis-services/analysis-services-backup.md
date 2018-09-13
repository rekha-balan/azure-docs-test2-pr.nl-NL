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
# <a name="backup-and-restore"></a>Backup and restore

Backing up tabular model databases in Azure Analysis Services is much the same as for on-premises Analysis Services. The primary difference is where you store your backup files. Backup files must be saved to a container in an [Azure storage account](../storage/storage-create-storage-account.md). You can use a storage account and container you already have, or they can be created when configuring storage settings for your server.

> [!NOTE]
> Creating a storage account can result in a new billable service. To learn more, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/blobs/).
> 
> 

Backups are saved with a .abf extension. For in-memory tabular models, both model data and metadata are stored. For Direct Query tabular models, only model metadata is stored. Backups can be compressed and encrypted, depending on the options you choose. 



## <a name="configure-storage-settings"></a>Configure storage settings
Before backing up, you need to configure storage settings for your server.


### <a name="to-configure-storage-settings"></a>To configure storage settings
1.  In Azure portal > **Settings**, click **Backup**.

    ![Backups in Settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-backups.png)

2.  Click **Enabled**, then click **Storage Settings**.

    ![Enable](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-enable.png)

3. Select your storage account or create a new one.

4. Select a container or create a new one.

    ![Select container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-container.png)

5. Save your backup settings. You must save your changes whenever you change storage settings, or enable or disable backup.

    ![Save backup settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/analysis-services/media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>Backup

### <a name="to-backup-by-using-ssms"></a>To backup by using SSMS

1. In SSMS, right-click a database > **Back Up**.

2. In **Backup Database** > **Backup file**, click **Browse**.

3. In the **Save file as** dialog, verify the folder path, and then type a name for the backup file. By default, the file name is given a .abf extension. 

4. In the **Backup Database** dialog, select options.

    **Allow file overwrite** - Select this option to overwrite backup files of the same name. If this option is not selected, the file you are saving cannot have the same name as a file that already exists in the same location.

    **Apply compression** - Select this option to compress the backup file. Compressed backup files save disk space, but require slightly higher CPU utilization. 

    **Encrypt backup file** - Select this option to encrypt the backup file. This option requires a user-supplied password to secure the backup file. The password prevents reading of the backup data any other means than a restore operation. If you choose to encrypt backups, store the password in a safe location.

5. Click **OK** to create and save the backup file.


### <a name="powershell"></a>PowerShell
Use [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) cmdlet.

## <a name="restore"></a>Restore
When restoring, your backup file must be in the storage account you've configured for your server. If you need to move a backup file from an on-premises location to your storage account, use [Microsoft Azure Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer) or the [AzCopy](../storage/storage-use-azcopy.md) command-line utility. 

If you're restoring a tabular 1200 model database from an on-premises SQL Server Analysis Services server, you must first remove all of the domain users from the model's roles, and add them back to the roles as Azure Active Directory users. The roles will be the same.

### <a name="to-restore-by-using-ssms"></a>To restore by using SSMS

1. In SSMS, right-click a database > **Restore**.

2. In the **Backup Database** dialog, in **Backup file**, click **Browse**.

3. In the **Locate Database Files** dialog, select the file you want to restore.

4. In **Restore database**, select the database.

5. Specify options. Security options must match the backup options you used when backing up.


### <a name="powershell"></a>PowerShell

Use [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) cmdlet.


## <a name="related-information"></a>Related information

[Azure storage accounts](../storage/storage-create-storage-account.md)  
[High availablility](analysis-services-bcdr.md)     
[Manage Azure Analysis Services](analysis-services-manage.md)




