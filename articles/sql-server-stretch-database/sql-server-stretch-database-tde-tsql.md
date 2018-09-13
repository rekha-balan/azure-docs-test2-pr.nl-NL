---
title: Enable Transparent Data Encryption for Stretch Database TSQL - Azure | Microsoft Docs
description: Enable Transparent Data Encryption (TDE) for SQL Server Stretch Database on Azure TSQL
services: sql-server-stretch-database
documentationcenter: ''
author: douglaslMS
manager: jhubbard
editor: ''
ms.assetid: 27753d91-9ca2-4d47-b34d-b5e2c2f029bb
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: anvang
ms.openlocfilehash: ed26c2b386e08b76f78b4a05e12c46d2b97c20f2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551829"
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a>Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.

TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key. The database encryption key is protected by a built-in server certificate. The built-in server certificate is unique for each Azure server. Microsoft automatically rotates these certificates at least every 90 days. For a general description of TDE, see [Transparent Data Encryption (TDE)].

## <a name="enabling-encryption"></a>Enabling Encryption
To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:

1. Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database
2. Execute the following statement to encrypt the database.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a>Disabling Encryption
To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:

1. Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database
2. Execute the following statement to encrypt the database.

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a>Verifying Encryption
To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:

1. Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database
2. Execute the following statement to encrypt the database.

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
