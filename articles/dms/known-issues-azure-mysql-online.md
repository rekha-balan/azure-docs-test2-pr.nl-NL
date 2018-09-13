---
title: Article about known issues/migration limitations with online migrations to Azure Database for MySQL | Microsoft Docs
description: Learn about known issues/migration limitations with online migrations to Azure Database for MySQL.
services: database-migration
author: HJToland3
ms.author: jtoland
manager: ''
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 08/24/2018
ms.openlocfilehash: d1d1483edd31702b1b9f14eaf4aba1a3f38ed142
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865704"
---
# <a name="known-issuesmigration-limitations-with-online-migrations-to-azure-db-for-mysql"></a><span data-ttu-id="27280-103">Known issues/migration limitations with online migrations to Azure DB for MySQL</span><span class="sxs-lookup"><span data-stu-id="27280-103">Known issues/migration limitations with online migrations to Azure DB for MySQL</span></span>

<span data-ttu-id="27280-104">Known issues and limitations associated with online migrations from MySQL to Azure Database for MySQL are described in the following sections.</span><span class="sxs-lookup"><span data-stu-id="27280-104">Known issues and limitations associated with online migrations from MySQL to Azure Database for MySQL are described in the following sections.</span></span> 

## <a name="online-migration-configuration"></a><span data-ttu-id="27280-105">Online migration configuration</span><span class="sxs-lookup"><span data-stu-id="27280-105">Online migration configuration</span></span>
- <span data-ttu-id="27280-106">The source MySQL Server version must be version 5.6.35, 5.7.18 or later</span><span class="sxs-lookup"><span data-stu-id="27280-106">The source MySQL Server version must be version 5.6.35, 5.7.18 or later</span></span>
- <span data-ttu-id="27280-107">Azure Database for MySQL supports:</span><span class="sxs-lookup"><span data-stu-id="27280-107">Azure Database for MySQL supports:</span></span>
    - <span data-ttu-id="27280-108">MySQL community edition</span><span class="sxs-lookup"><span data-stu-id="27280-108">MySQL community edition</span></span>
    - <span data-ttu-id="27280-109">InnoDB engine</span><span class="sxs-lookup"><span data-stu-id="27280-109">InnoDB engine</span></span>
- <span data-ttu-id="27280-110">Same version migration.</span><span class="sxs-lookup"><span data-stu-id="27280-110">Same version migration.</span></span> <span data-ttu-id="27280-111">Migrating MySQL 5.6 to Azure Database for MySQL 5.7 isn't supported.</span><span class="sxs-lookup"><span data-stu-id="27280-111">Migrating MySQL 5.6 to Azure Database for MySQL 5.7 isn't supported.</span></span>
- <span data-ttu-id="27280-112">Enable binary logging in my.ini (Windows) or my.cnf (Unix)</span><span class="sxs-lookup"><span data-stu-id="27280-112">Enable binary logging in my.ini (Windows) or my.cnf (Unix)</span></span>
    - <span data-ttu-id="27280-113">Set Server_id to any number larger or equals to 1, for example, Server_id=1 (only for MySQL 5.6)</span><span class="sxs-lookup"><span data-stu-id="27280-113">Set Server_id to any number larger or equals to 1, for example, Server_id=1 (only for MySQL 5.6)</span></span>
    - <span data-ttu-id="27280-114">Set log-bin = <path> (only for MySQL 5.6)</span><span class="sxs-lookup"><span data-stu-id="27280-114">Set log-bin = <path> (only for MySQL 5.6)</span></span>
    - <span data-ttu-id="27280-115">Set binlog_format = row</span><span class="sxs-lookup"><span data-stu-id="27280-115">Set binlog_format = row</span></span>
    - <span data-ttu-id="27280-116">Expire_logs_days = 5 (recommended - only for MySQL 5.6)</span><span class="sxs-lookup"><span data-stu-id="27280-116">Expire_logs_days = 5 (recommended - only for MySQL 5.6)</span></span>
- <span data-ttu-id="27280-117">User must have the ReplicationAdmin role.</span><span class="sxs-lookup"><span data-stu-id="27280-117">User must have the ReplicationAdmin role.</span></span>
- <span data-ttu-id="27280-118">Collations defined for the source MySQL database are the same as the ones defined in target Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="27280-118">Collations defined for the source MySQL database are the same as the ones defined in target Azure Database for MySQL.</span></span>
- <span data-ttu-id="27280-119">Schema must match between source MySQL database and target database in Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="27280-119">Schema must match between source MySQL database and target database in Azure Database for MySQL.</span></span>
- <span data-ttu-id="27280-120">Schema in target Azure Database for MySQL must not have foreign keys.</span><span class="sxs-lookup"><span data-stu-id="27280-120">Schema in target Azure Database for MySQL must not have foreign keys.</span></span> <span data-ttu-id="27280-121">Use the following query to drop foreign keys:</span><span class="sxs-lookup"><span data-stu-id="27280-121">Use the following query to drop foreign keys:</span></span>
    ```
    SET group_concat_max_len = 8192;
    SELECT SchemaName, GROUP_CONCAT(DropQuery SEPARATOR ';\n') as DropQuery, GROUP_CONCAT(AddQuery SEPARATOR ';\n') as AddQuery
    FROM
    (SELECT 
    KCU.REFERENCED_TABLE_SCHEMA as SchemaName, KCU.TABLE_NAME, KCU.COLUMN_NAME,
        CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' DROP FOREIGN KEY ', KCU.CONSTRAINT_NAME) AS DropQuery,
        CONCAT('ALTER TABLE ', KCU.TABLE_NAME, ' ADD CONSTRAINT ', KCU.CONSTRAINT_NAME, ' FOREIGN KEY (`', KCU.COLUMN_NAME, '`) REFERENCES `', KCU.REFERENCED_TABLE_NAME, '` (`', KCU.REFERENCED_COLUMN_NAME, '`) ON UPDATE ',RC.UPDATE_RULE, ' ON DELETE ',RC.DELETE_RULE) AS AddQuery
        FROM INFORMATION_SCHEMA.KEY_COLUMN_USAGE KCU, information_schema.REFERENTIAL_CONSTRAINTS RC
        WHERE
          KCU.CONSTRAINT_NAME = RC.CONSTRAINT_NAME
          AND KCU.REFERENCED_TABLE_SCHEMA = RC.UNIQUE_CONSTRAINT_SCHEMA
      AND KCU.REFERENCED_TABLE_SCHEMA = ['schema_name']) Queries
      GROUP BY SchemaName;
    ```

    <span data-ttu-id="27280-122">Run the drop foreign key (which is the second column) in the query result.</span><span class="sxs-lookup"><span data-stu-id="27280-122">Run the drop foreign key (which is the second column) in the query result.</span></span>
- <span data-ttu-id="27280-123">Schema in target Azure Database for MySQL must not have any triggers.</span><span class="sxs-lookup"><span data-stu-id="27280-123">Schema in target Azure Database for MySQL must not have any triggers.</span></span> <span data-ttu-id="27280-124">To drop triggers in target database:</span><span class="sxs-lookup"><span data-stu-id="27280-124">To drop triggers in target database:</span></span>
    ```
    SELECT Concat('DROP TRIGGER ', Trigger_Name, ';') FROM  information_schema.TRIGGERS WHERE TRIGGER_SCHEMA = 'your_schema';
    ```

## <a name="datatype-limitations"></a><span data-ttu-id="27280-125">Datatype limitations</span><span class="sxs-lookup"><span data-stu-id="27280-125">Datatype limitations</span></span>
- <span data-ttu-id="27280-126">**Limitation**: If there's a JSON datatype in the source MySQL database, migration will fail during continuous sync.</span><span class="sxs-lookup"><span data-stu-id="27280-126">**Limitation**: If there's a JSON datatype in the source MySQL database, migration will fail during continuous sync.</span></span>

    <span data-ttu-id="27280-127">**Workaround**: Modify JSON datatype to medium text or longtext in source MySQL database.</span><span class="sxs-lookup"><span data-stu-id="27280-127">**Workaround**: Modify JSON datatype to medium text or longtext in source MySQL database.</span></span>

- <span data-ttu-id="27280-128">**Limitation**: If there's no primary key on tables, continuous sync will fail.</span><span class="sxs-lookup"><span data-stu-id="27280-128">**Limitation**: If there's no primary key on tables, continuous sync will fail.</span></span>
 
    <span data-ttu-id="27280-129">**Workaround**: Temporarily set a primary key for the table for migration to continue.</span><span class="sxs-lookup"><span data-stu-id="27280-129">**Workaround**: Temporarily set a primary key for the table for migration to continue.</span></span> <span data-ttu-id="27280-130">You can remove the primary key after data migration is complete.</span><span class="sxs-lookup"><span data-stu-id="27280-130">You can remove the primary key after data migration is complete.</span></span>

## <a name="lob-limitations"></a><span data-ttu-id="27280-131">LOB limitations</span><span class="sxs-lookup"><span data-stu-id="27280-131">LOB limitations</span></span>
<span data-ttu-id="27280-132">Large Object (LOB) columns are columns that could grow large in size.</span><span class="sxs-lookup"><span data-stu-id="27280-132">Large Object (LOB) columns are columns that could grow large in size.</span></span> <span data-ttu-id="27280-133">For MySQL, Medium text, Longtext, Blob, Mediumblob, Longblob, etc. are some of the datatypes of LOB.</span><span class="sxs-lookup"><span data-stu-id="27280-133">For MySQL, Medium text, Longtext, Blob, Mediumblob, Longblob, etc. are some of the datatypes of LOB.</span></span>

- <span data-ttu-id="27280-134">**Limitation**: If LOB data types are used as primary keys, migration will fail.</span><span class="sxs-lookup"><span data-stu-id="27280-134">**Limitation**: If LOB data types are used as primary keys, migration will fail.</span></span>

    <span data-ttu-id="27280-135">**Workaround**: Replace primary key with other datatypes or columns that aren't LOB.</span><span class="sxs-lookup"><span data-stu-id="27280-135">**Workaround**: Replace primary key with other datatypes or columns that aren't LOB.</span></span>

- <span data-ttu-id="27280-136">**Limitation**: If the length of Large Object (LOB) column is bigger than 32 KB, data might be truncated at the target.</span><span class="sxs-lookup"><span data-stu-id="27280-136">**Limitation**: If the length of Large Object (LOB) column is bigger than 32 KB, data might be truncated at the target.</span></span> <span data-ttu-id="27280-137">You can check the length of LOB column using this query:</span><span class="sxs-lookup"><span data-stu-id="27280-137">You can check the length of LOB column using this query:</span></span>
    ```
    SELECT max(length(description)) as LEN from catalog;
    ```

    <span data-ttu-id="27280-138">**Workaround**: If you have LOB object that is bigger than 32 KB, contact engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="27280-138">**Workaround**: If you have LOB object that is bigger than 32 KB, contact engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span></span> 

## <a name="other-limitations"></a><span data-ttu-id="27280-139">Other limitations</span><span class="sxs-lookup"><span data-stu-id="27280-139">Other limitations</span></span>
- <span data-ttu-id="27280-140">A password string that has opening and closing curly brackets {  } at the beginning and end of the password string isn't supported.</span><span class="sxs-lookup"><span data-stu-id="27280-140">A password string that has opening and closing curly brackets {  } at the beginning and end of the password string isn't supported.</span></span> <span data-ttu-id="27280-141">This limitation applies to both connecting to source MySQL and target Azure Database for MySQL.</span><span class="sxs-lookup"><span data-stu-id="27280-141">This limitation applies to both connecting to source MySQL and target Azure Database for MySQL.</span></span>
- <span data-ttu-id="27280-142">The following DDLs aren't supported:</span><span class="sxs-lookup"><span data-stu-id="27280-142">The following DDLs aren't supported:</span></span>
    - <span data-ttu-id="27280-143">All partition DDLs</span><span class="sxs-lookup"><span data-stu-id="27280-143">All partition DDLs</span></span>
    - <span data-ttu-id="27280-144">Drop table</span><span class="sxs-lookup"><span data-stu-id="27280-144">Drop table</span></span>
    - <span data-ttu-id="27280-145">Rename table</span><span class="sxs-lookup"><span data-stu-id="27280-145">Rename table</span></span>
- <span data-ttu-id="27280-146">Using the *alter table <table_name> add column <column_name>* statement to add columns to the beginning or to the middle of a table isn't supported.</span><span class="sxs-lookup"><span data-stu-id="27280-146">Using the *alter table <table_name> add column <column_name>* statement to add columns to the beginning or to the middle of a table isn't supported.</span></span> <span data-ttu-id="27280-147">THe *alter table <table_name> add column <column_name>* adds the column at the end of the table.</span><span class="sxs-lookup"><span data-stu-id="27280-147">THe *alter table <table_name> add column <column_name>* adds the column at the end of the table.</span></span>
- <span data-ttu-id="27280-148">Indexes created on only part of the column data aren't supported.</span><span class="sxs-lookup"><span data-stu-id="27280-148">Indexes created on only part of the column data aren't supported.</span></span> <span data-ttu-id="27280-149">The following statement is an example that creates an index using only part of the column data:</span><span class="sxs-lookup"><span data-stu-id="27280-149">The following statement is an example that creates an index using only part of the column data:</span></span>
    ``` 
    CREATE INDEX partial_name ON customer (name(10));
    ```

- <span data-ttu-id="27280-150">In DMS, the limit of databases to migrate in one single migration activity is four.</span><span class="sxs-lookup"><span data-stu-id="27280-150">In DMS, the limit of databases to migrate in one single migration activity is four.</span></span>
