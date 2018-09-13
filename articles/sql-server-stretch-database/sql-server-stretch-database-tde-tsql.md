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
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure-transact-sql"></a><span data-ttu-id="db37d-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="db37d-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure (Transact-SQL)</span></span>
> [!div class="op_single_selector"]
> * [Azure portal](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="db37d-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span><span class="sxs-lookup"><span data-stu-id="db37d-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="db37d-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span><span class="sxs-lookup"><span data-stu-id="db37d-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="db37d-108">The database encryption key is protected by a built-in server certificate.</span><span class="sxs-lookup"><span data-stu-id="db37d-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="db37d-109">The built-in server certificate is unique for each Azure server.</span><span class="sxs-lookup"><span data-stu-id="db37d-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="db37d-110">Microsoft automatically rotates these certificates at least every 90 days.</span><span class="sxs-lookup"><span data-stu-id="db37d-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="db37d-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span><span class="sxs-lookup"><span data-stu-id="db37d-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="db37d-112">Enabling Encryption</span><span class="sxs-lookup"><span data-stu-id="db37d-112">Enabling Encryption</span></span>
<span data-ttu-id="db37d-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="db37d-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="db37d-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="db37d-114">Connect to the *master* database on the Azure server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="db37d-115">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="db37d-115">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="db37d-116">Disabling Encryption</span><span class="sxs-lookup"><span data-stu-id="db37d-116">Disabling Encryption</span></span>
<span data-ttu-id="db37d-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="db37d-117">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="db37d-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="db37d-118">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="db37d-119">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="db37d-119">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [database_name] SET ENCRYPTION OFF;
```

## <a name="verifying-encryption"></a><span data-ttu-id="db37d-120">Verifying Encryption</span><span class="sxs-lookup"><span data-stu-id="db37d-120">Verifying Encryption</span></span>
<span data-ttu-id="db37d-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span><span class="sxs-lookup"><span data-stu-id="db37d-121">To verify encryption status for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="db37d-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="db37d-122">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="db37d-123">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="db37d-123">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="db37d-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span><span class="sxs-lookup"><span data-stu-id="db37d-124">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->

<!--Link references-->
