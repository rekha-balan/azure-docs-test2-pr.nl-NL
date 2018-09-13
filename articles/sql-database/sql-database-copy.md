---
title: Copy an Azure SQL database | Microsoft Docs
description: Create a copy of an Azure SQL database
services: sql-database
documentationcenter: ''
author: anosov1960
manager: jhubbard
editor: ''
ms.assetid: 5aaf6bcd-3839-49b5-8c77-cbdf786e359b
ms.service: sql-database
ms.custom: move data
ms.devlang: NA
ms.date: 04/05/2017
ms.author: sashan;carlrab
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: b2573d86c0f8059eed7fb2228dac9052de1b18b5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554446"
---
# <a name="copy-an-azure-sql-database"></a>Copy an Azure SQL database

Azure SQL Database provides several methods for creating a transactionally consistent copy of an existing Azure SQL database on either the same server or a different server. You can copy a SQL database using the Azure portal, PowerShell, or T-SQL. 

## <a name="overview"></a>Overview

A database copy is a snapshot of the source database as of the time of the copy request. You can select the same server or a different server, its service tier and performance level,  a different performance level within the same service tier (edition). After the copy is complete, the copy becomes a fully functional, independent database. At this point, you can upgrade or downgrade it to any edition. The logins, users, and permissions can be managed independently.  

## <a name="logins-in-the-database-copy"></a>Logins in the database copy

When you copy a database to the same logical server, the same logins can be used on both databases. The security principal you use to copy the database becomes the database owner (DBO) on the new database. All database users, their permissions, and their security identifiers (SIDs) are copied to the database copy.  

When you copy a database to a different logical server, the security principal on the new server becomes the database owner on the new database. If you use [contained database users](sql-database-manage-logins.md) for data access, ensure that both the primary and secondary databases always have the same user credentials, so after the copy completes you can immediately access it with the same credentials. 

If you use [Azure Active Directory](../active-directory/active-directory-whatis.md), you can completely eliminate the need for managing credentials in the copy. However, when you copy the database to a new server, the login-based access may not work because the logins do not exist on the new server. See [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md) to learn about managing logins when copying a database to a different logical server. 

After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner (DBO), can log on to the new database. To resolve logins after the copy operation completes, see [Resolve logins](sql-database-copy.md#resolve-logins.md)

## <a name="database-copy-using-the-azure-portal"></a>Database copy using the Azure portal

To copy a database using the Azure portal, open the page for your database and click **Copy** on the toolbar. 

   ![Database copy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-copy/database-copy.png)

## <a name="database-copy-using-powershell"></a>Database copy using PowerShell

To copy a database using PowerShell, use the [New-AzureRmSqlDatabaseCopy](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) cmdlet. 

```PowerShell
New-AzureRmSqlDatabaseCopy -ResourceGroupName "myResourceGroup" `
    -ServerName $sourceserver `
    -DatabaseName "MySampleDatabase" `
    -CopyResourceGroupName "myResourceGroup" `
    -CopyServerName $targetserver `
    -CopyDatabaseName "CopyOfMySampleDatabase"
```

For a complete sample script, see [Copy a database to a new server](scripts/sql-database-copy-database-to-new-server-powershell.md)

## <a name="database-copy-using-transact-sql"></a>Database copy using Transact-SQL

Log on to the master database using the server-level principal login or the login that created the database you want to copy. Logins that are not the server-level principal must be members of the dbmanager role to copy databases. For more information about logins and connecting to the server, see [Manage logins](sql-database-manage-logins.md).

Start copying the source database with the [CREATE DATABASE](https://msdn.microsoft.com/library/ms176061.aspx) statement. Executing this statement initiates the database copying process. Because copying a database is an asynchronous process, the CREATE DATABASE statement returns before the database completes copying.

### <a name="copy-a-sql-database-to-the-same-server"></a>Copy a SQL database to the same server
Log on to the master database using the server-level principal login or the login that created the database you want to copy. Logins that are not the server-level principal must be members of the dbmanager role to copy databases.

This command copies Database1 on to a new database named Database2 on the same server. Depending on the size of your database the copy operation may take some time to complete.

    -- Execute on the master database.
    -- Start copying.
    CREATE DATABASE Database1_copy AS COPY OF Database1;

### <a name="copy-a-sql-database-to-a-different-server"></a>Copy a SQL database to a different server

Log on to the master database of the destination server, the Azure SQL Database server where the new database is to be created. Use a login that has the same name and password as the database owner (DBO) of the source database on the source Azure SQL Database server. The login on the destination server must also be a member of the dbmanager role or be the server-level principal login.

This command copies Database1 on server1- to a new database named Database2 on server2. Depending on the size of your database the copy operation may take some time to complete.

    -- Execute on the master database of the target server (server2)
    -- Start copying from Server1 to Server2
    CREATE DATABASE Database1_copy AS COPY OF server1.Database1;


### <a name="monitor-the-progress-of-the-copy-operation"></a>Monitor the progress of the copy operation

Monitor the copying process by querying the sys.databases and sys.dm_database_copies views. While the copying is in progress, the state_desc column of the sys.databases view for the new database is set to COPYING.

* If the copying fails, the state_desc column of the sys.databases view for the new database is set to SUSPECT. In this case, execute the DROP statement on the new database and try again later.
* If the copying succeeds, the state_desc column of the sys.databases view for the new database is set to ONLINE. In this case, the copying is complete and the new database is a regular database, able to be changed independent of the source database.

> [!NOTE]
> * If you decide to cancel the copying while it is in progress, execute the [DROP DATABASE](https://msdn.microsoft.com/library/ms178613.aspx) statement on the new database. Alternatively, executing the DROP DATABASE statement on the source database also cancels the copying process.
> 

## <a name="resolve-logins"></a>Resolve logins

After the new database is online on the destination server, use the [ALTER USER](https://msdn.microsoft.com/library/ms176060.aspx) statement to remap the users from the new database to logins on the destination server. To resolve orphaned users, see [Troubleshoot Orphaned Users](https://msdn.microsoft.com/library/ms175475.aspx). See also [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).

All users in the new database maintain the permissions that they had in the source database. The user who initiated the database copy becomes the database owner of the new database and is assigned a new security identifier (SID). After the copying succeeds and before other users are remapped, only the login that initiated the copying, the database owner (DBO), can log on to the new database.

See also [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md) to learn about managing users and logins when copying a database to a different logical server.

## <a name="next-steps"></a>Next steps

* For information on logins, see [Manage logins](sql-database-manage-logins.md) and [How to manage Azure SQL database security after disaster recovery](sql-database-geo-replication-security-config.md).
* To export a database, see [Export the database to a BACPAC](sql-database-export.md)

