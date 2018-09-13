---
title: Restore a single table from Azure SQL Database backup | Microsoft Docs
description: Learn how to restore a single table from Azure SQL Database backup.
services: sql-database
documentationcenter: ''
author: dalechen
manager: cshepard
editor: ''
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: restore
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/20/2017
ms.author: daleche
ms.openlocfilehash: c10861efcdfafad127d00a072b65eb0e6b3ab805
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550194"
---
# <a name="how-to-restore-a-single-table-from-an-azure-sql-database-backup"></a>How to restore a single table from an Azure SQL Database backup
You may encounter a situation in which you accidentally modified some data in a SQL database and now you want to recover the single affected table. This article describes how to restore a single table in a database from one of the SQL Database [automatic backups](sql-database-automated-backups.md).

## <a name="preparation-steps-rename-the-table-and-restore-a-copy-of-the-database"></a>Preparation steps: Rename the table and restore a copy of the database
1. Identify the table in your Azure SQL database that you want to replace with the restored copy. Use Microsoft SQL Management Studio to rename the table. For example, rename the table as &lt;table name&gt;_old.
   
   > [!NOTE]
   > To avoid being blocked, make sure that there's no activity running on the table that you are renaming. If you encounter issues, make sure that perform this procedure during a maintenance window.
   >

2. Restore a backup of your database to a point in time that you want to recover to using the [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.
   
   > [!NOTE]
   > The name of the restored database will be in the DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**. This step doesn't overwrite the existing database name on the server. This is a safety measure, and it's intended to allow you to verify the restored database before they drop their current database and rename the restored database for production use.
   
## <a name="copying-the-table-from-the-restored-database-by-using-the-sql-database-migration-tool"></a>Copying the table from the restored database by using the SQL Database Migration tool

1. Download and install the [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).
2. Open the SQL Database Migration Wizard, on the **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.

   ![SQL Database Migration wizard - Select Process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. In the **Connect to Server** dialog box, apply the following settings:

   * Server name: **Your SQL server**
   * Authentication: **SQL Server Authentication**
   * Login: **Your login**
   * Password: **Your password**
   * Database: **Master DB (List all databases)**
   
   > [!NOTE]
   > By default the wizard saves your login information. If you don't want it to, select **Forget Login Information**.
   >
   
     ![SQL Database Migration wizard - Select Source - step 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. In the **Select Source** dialog box, select the restored database name from the **Preparation steps** section as your source, and then click **Next**.
   
    ![SQL Database Migration wizard - Select Source - step 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. In the **Choose Objects** dialog box, select the **Select specific database objects** option, and then select the table(or tables) that you want to migrate to the target server.
   ![SQL Database Migration wizard - Choose Objects](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)
6. On the **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready to generate a SQL script. You also have the option to save the TSQL Script for later use.
   ![SQL Database Migration wizard - Script Wizard Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)
7. On the **Results Summary** page, click **Next**.
   ![SQL Database Migration wizard - Results Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)
8. On the **Setup Target Server Connection** page, click **Connect to Server**, and then enter the details as follows:
   
   * **Server Name**: Target server instance
   * **Authentication**: **SQL Server authentication**. Enter your login credentials.
   * **Database**: **Master DB (List all databases)**. This option lists all the databases on the target server.
     
     ![SQL Database Migration wizard - Setup Target Server Connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. Click **Connect**, select the target database that you want to move the table to, and then click **Next**. This should finish running the previously generated script, and you should see the newly moved table copied to the target database.

## <a name="verification-step"></a>Verification step

- Query and test the newly copied table to make sure that the data is intact. Upon confirmation, you can drop the renamed table form **Preparation steps** section. (for example, &lt;table name&gt;_old).

## <a name="next-steps"></a>Next steps
[SQL Database automatic backups](sql-database-automated-backups.md)








