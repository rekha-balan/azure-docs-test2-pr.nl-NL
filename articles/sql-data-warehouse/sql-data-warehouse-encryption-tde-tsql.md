---
title: Transparent Data Encryption in SQL Data Warehouse (T-SQL)| Microsoft Docs
description: Transparent Data Encryption (TDE) in SQL Data Warehouse (T-SQL)
services: sql-data-warehouse
documentationcenter: ''
author: ronortloff
manager: barbkess
editor: ''
ms.assetid: 8ccefef3-1308-41ee-b336-5e491d1098ae
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 74c9032aababdce91ed617cd7a4c628915b42504
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555317"
---
# <a name="get-started-with-transparent-data-encryption-tde"></a><span data-ttu-id="d3357-103">Get started with Transparent Data Encryption (TDE)</span><span class="sxs-lookup"><span data-stu-id="d3357-103">Get started with Transparent Data Encryption (TDE)</span></span>
> [!div class="op_single_selector"]
> * [Security Overview](sql-data-warehouse-overview-manage-security.md)
> * [Authentication](sql-data-warehouse-authentication.md)
> * [Encryption (Portal)](sql-data-warehouse-encryption-tde.md)
> * [Encryption (T-SQL)](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

## <a name="required-permssions"></a><span data-ttu-id="d3357-108">Required Permssions</span><span class="sxs-lookup"><span data-stu-id="d3357-108">Required Permssions</span></span>
<span data-ttu-id="d3357-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span><span class="sxs-lookup"><span data-stu-id="d3357-109">To enable Transparent Data Encryption (TDE), you must be an administrator or a member of the dbmanager role.</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="d3357-110">Enabling Encryption</span><span class="sxs-lookup"><span data-stu-id="d3357-110">Enabling Encryption</span></span>
<span data-ttu-id="d3357-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d3357-111">Follow these steps to enable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="d3357-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="d3357-112">Connect to the *master* database on the server hosting the database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="d3357-113">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="d3357-113">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION ON;
```

## <a name="disabling-encryption"></a><span data-ttu-id="d3357-114">Disabling Encryption</span><span class="sxs-lookup"><span data-stu-id="d3357-114">Disabling Encryption</span></span>
<span data-ttu-id="d3357-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="d3357-115">Follow these steps to disable TDE for a SQL Data Warehouse:</span></span>

1. <span data-ttu-id="d3357-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="d3357-116">Connect to the *master* database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="d3357-117">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="d3357-117">Execute the following statement to encrypt the database.</span></span>

```sql
ALTER DATABASE [AdventureWorks] SET ENCRYPTION OFF;
```

> [!NOTE]
> A paused SQL Data Warehouse must be resumed before making changes to the TDE settings.
> 
> 

## <a name="verifying-encryption"></a><span data-ttu-id="d3357-119">Verifying Encryption</span><span class="sxs-lookup"><span data-stu-id="d3357-119">Verifying Encryption</span></span>
<span data-ttu-id="d3357-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="d3357-120">To verify encryption status for a SQL Data Warehouse, follow the steps below:</span></span>

1. <span data-ttu-id="d3357-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span><span class="sxs-lookup"><span data-stu-id="d3357-121">Connect to the *master* or instance database using a login that is an administrator or a member of the **dbmanager** role in the master database</span></span>
2. <span data-ttu-id="d3357-122">Execute the following statement to encrypt the database.</span><span class="sxs-lookup"><span data-stu-id="d3357-122">Execute the following statement to encrypt the database.</span></span>

```sql
SELECT
    [name],
    [is_encrypted]
FROM
    sys.databases;
```

<span data-ttu-id="d3357-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span><span class="sxs-lookup"><span data-stu-id="d3357-123">A result of ```1``` indicates an encrypted database, ```0``` indicates a non-encrypted database.</span></span>

## <a name="encryption-dmvs"></a><span data-ttu-id="d3357-124">Encryption DMVs</span><span class="sxs-lookup"><span data-stu-id="d3357-124">Encryption DMVs</span></span>
* <span data-ttu-id="d3357-125">[sys.databases][sys.databases]</span><span class="sxs-lookup"><span data-stu-id="d3357-125">[sys.databases][sys.databases]</span></span> 
* <span data-ttu-id="d3357-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span><span class="sxs-lookup"><span data-stu-id="d3357-126">[sys.dm_pdw_nodes_database_encryption_keys][sys.dm_pdw_nodes_database_encryption_keys]</span></span>

<!--Anchors-->
[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx
[sys.databases]: http://msdn.microsoft.com/library/ms178534.aspx  
[sys.dm_pdw_nodes_database_encryption_keys]: https://msdn.microsoft.com/library/mt203922.aspx  

<!--Image references-->

<!--Link references-->
