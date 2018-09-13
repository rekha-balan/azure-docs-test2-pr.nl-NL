---
title: Article about known issues/migration limitations with online migrations to Azure SQL Database | Microsoft Docs
description: Learn about known issues/migration limitations with online migrations to Azure SQL Database.
services: database-migration
author: HJToland3
ms.author: jtoland
manager: ''
ms.reviewer: ''
ms.service: database-migration
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 09/11/2018
ms.openlocfilehash: e61e975a07dd643652ca4847025499e3e77f42be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870759"
---
# <a name="known-issuesmigration-limitations-with-online-migrations-to-azure-sql-db"></a><span data-ttu-id="102ff-103">Known issues/migration limitations with online migrations to Azure SQL DB</span><span class="sxs-lookup"><span data-stu-id="102ff-103">Known issues/migration limitations with online migrations to Azure SQL DB</span></span>

<span data-ttu-id="102ff-104">Known issues and limitations associated with online migrations from SQL Server to Azure SQL Database are described below.</span><span class="sxs-lookup"><span data-stu-id="102ff-104">Known issues and limitations associated with online migrations from SQL Server to Azure SQL Database are described below.</span></span>

### <a name="migration-of-temporal-tables-not-supported"></a><span data-ttu-id="102ff-105">Migration of temporal tables not supported</span><span class="sxs-lookup"><span data-stu-id="102ff-105">Migration of temporal tables not supported</span></span>

<span data-ttu-id="102ff-106">**Symptom**</span><span class="sxs-lookup"><span data-stu-id="102ff-106">**Symptom**</span></span>

<span data-ttu-id="102ff-107">If your source database consists of one or more temporal tables, your database migration fails during the “Full data load” operation and you may see the following message:</span><span class="sxs-lookup"><span data-stu-id="102ff-107">If your source database consists of one or more temporal tables, your database migration fails during the “Full data load” operation and you may see the following message:</span></span>

<span data-ttu-id="102ff-108">{ "resourceId":"/subscriptions/<subscription id>/resourceGroups/migrateready/providers/Microsoft.DataMigration/services/<DMS Service name>", "errorType":"Database migration error", "errorEvents":"["Capture functionalities could not be set.</span><span class="sxs-lookup"><span data-stu-id="102ff-108">{ "resourceId":"/subscriptions/<subscription id>/resourceGroups/migrateready/providers/Microsoft.DataMigration/services/<DMS Service name>", "errorType":"Database migration error", "errorEvents":"["Capture functionalities could not be set.</span></span> <span data-ttu-id="102ff-109">RetCode: SQL_ERROR SqlState: 42000 NativeError: 13570 Message: [Microsoft][SQL Server Native Client 11.0][SQL Server]The use of replication is not supported with system-versioned temporal table '[Application.</span><span class="sxs-lookup"><span data-stu-id="102ff-109">RetCode: SQL_ERROR SqlState: 42000 NativeError: 13570 Message: [Microsoft][SQL Server Native Client 11.0][SQL Server]The use of replication is not supported with system-versioned temporal table '[Application.</span></span> <span data-ttu-id="102ff-110">Cities]' Line: 1 Column: -1 "]" }</span><span class="sxs-lookup"><span data-stu-id="102ff-110">Cities]' Line: 1 Column: -1 "]" }</span></span>
 
 ![Temporal table errors example](media\known-issues-azure-sql-online\dms-temporal-tables-errors.png)

<span data-ttu-id="102ff-112">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-112">**Workaround**</span></span>

1. <span data-ttu-id="102ff-113">Find the temporal tables in your source schema using the query below.</span><span class="sxs-lookup"><span data-stu-id="102ff-113">Find the temporal tables in your source schema using the query below.</span></span>
     ``` 
     select name,temporal_type,temporal_type_desc,* from sys.tables where temporal_type <>0
     ```
2. <span data-ttu-id="102ff-114">Exclude these tables from the **Configure migration settings** blade, on which you specify tables for migration.</span><span class="sxs-lookup"><span data-stu-id="102ff-114">Exclude these tables from the **Configure migration settings** blade, on which you specify tables for migration.</span></span>

3. <span data-ttu-id="102ff-115">Rerun the migration activity.</span><span class="sxs-lookup"><span data-stu-id="102ff-115">Rerun the migration activity.</span></span>

<span data-ttu-id="102ff-116">**Resources**</span><span class="sxs-lookup"><span data-stu-id="102ff-116">**Resources**</span></span>

<span data-ttu-id="102ff-117">For more information, see the article [Temporal Tables](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="102ff-117">For more information, see the article [Temporal Tables](https://docs.microsoft.com/sql/relational-databases/tables/temporal-tables?view=sql-server-2017).</span></span>
 
### <a name="migration-of-tables-includes-one-or-more-columns-with-the-hierarchyid-data-type"></a><span data-ttu-id="102ff-118">Migration of tables includes one or more columns with the hierarchyid data type</span><span class="sxs-lookup"><span data-stu-id="102ff-118">Migration of tables includes one or more columns with the hierarchyid data type</span></span>

<span data-ttu-id="102ff-119">**Symptom**</span><span class="sxs-lookup"><span data-stu-id="102ff-119">**Symptom**</span></span>

<span data-ttu-id="102ff-120">You may see a SQL Exception suggesting “ntext is incompatible with hierarchyid” during the “Full data load” operation:</span><span class="sxs-lookup"><span data-stu-id="102ff-120">You may see a SQL Exception suggesting “ntext is incompatible with hierarchyid” during the “Full data load” operation:</span></span>
     
![hierarchyid errors example](media\known-issues-azure-sql-online\dms-hierarchyid-errors.png)

<span data-ttu-id="102ff-122">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-122">**Workaround**</span></span>

1. <span data-ttu-id="102ff-123">Find the user tables that include columns with the hierarchyid data type using the query below.</span><span class="sxs-lookup"><span data-stu-id="102ff-123">Find the user tables that include columns with the hierarchyid data type using the query below.</span></span>

      ``` 
      select object_name(object_id) 'Table name' from sys.columns where system_type_id =240 and object_id in (select object_id from sys.objects where type='U')
      ``` 

 2. <span data-ttu-id="102ff-124">Exclude these tables from the **Configure migration settings** blade, on which you specify tables for migration.</span><span class="sxs-lookup"><span data-stu-id="102ff-124">Exclude these tables from the **Configure migration settings** blade, on which you specify tables for migration.</span></span>

 3. <span data-ttu-id="102ff-125">Rerun the migration activity.</span><span class="sxs-lookup"><span data-stu-id="102ff-125">Rerun the migration activity.</span></span>

### <a name="migration-failures-with-various-integrity-violations-with-active-triggers-in-the-schema-during-full-data-load-or-incremental-data-sync"></a><span data-ttu-id="102ff-126">Migration failures with various integrity violations with active triggers in the schema during “Full data load” or “Incremental data sync”</span><span class="sxs-lookup"><span data-stu-id="102ff-126">Migration failures with various integrity violations with active triggers in the schema during “Full data load” or “Incremental data sync”</span></span>

<span data-ttu-id="102ff-127">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-127">**Workaround**</span></span>
1. <span data-ttu-id="102ff-128">Find the triggers that are currently active in the source database using the query below:</span><span class="sxs-lookup"><span data-stu-id="102ff-128">Find the triggers that are currently active in the source database using the query below:</span></span>
     ```
     select * from sys.triggers where is_disabled =0
     ```
2. <span data-ttu-id="102ff-129">Disable the triggers on your source database using the steps provided in the article [DISABLE TRIGGER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/disable-trigger-transact-sql?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="102ff-129">Disable the triggers on your source database using the steps provided in the article [DISABLE TRIGGER (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/disable-trigger-transact-sql?view=sql-server-2017).</span></span>

3. <span data-ttu-id="102ff-130">Re-Run the migration activity.</span><span class="sxs-lookup"><span data-stu-id="102ff-130">Re-Run the migration activity.</span></span>

### <a name="support-for-lob-data-types"></a><span data-ttu-id="102ff-131">Support for LOB data types</span><span class="sxs-lookup"><span data-stu-id="102ff-131">Support for LOB data types</span></span>

<span data-ttu-id="102ff-132">**Symptom**</span><span class="sxs-lookup"><span data-stu-id="102ff-132">**Symptom**</span></span>

<span data-ttu-id="102ff-133">If the length of Large Object (LOB) column is bigger than 32 KB, data might get truncated at the target.</span><span class="sxs-lookup"><span data-stu-id="102ff-133">If the length of Large Object (LOB) column is bigger than 32 KB, data might get truncated at the target.</span></span> <span data-ttu-id="102ff-134">You can check the length of LOB column using the query below:</span><span class="sxs-lookup"><span data-stu-id="102ff-134">You can check the length of LOB column using the query below:</span></span> 

``` 
SELECT max(len(ColumnName)) as LEN from TableName
```

<span data-ttu-id="102ff-135">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-135">**Workaround**</span></span>

<span data-ttu-id="102ff-136">If you have an LOB column that is bigger than 32 KB, contact the engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="102ff-136">If you have an LOB column that is bigger than 32 KB, contact the engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span></span>

### <a name="issues-with-timestamp-columns"></a><span data-ttu-id="102ff-137">Issues with timestamp columns</span><span class="sxs-lookup"><span data-stu-id="102ff-137">Issues with timestamp columns</span></span>

<span data-ttu-id="102ff-138">**Symptom**</span><span class="sxs-lookup"><span data-stu-id="102ff-138">**Symptom**</span></span>

<span data-ttu-id="102ff-139">DMS doesn't migrate the source timestamp value; instead, DMS generates a new timestamp value in the target table.</span><span class="sxs-lookup"><span data-stu-id="102ff-139">DMS doesn't migrate the source timestamp value; instead, DMS generates a new timestamp value in the target table.</span></span>

<span data-ttu-id="102ff-140">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-140">**Workaround**</span></span>

<span data-ttu-id="102ff-141">If you need DMS to migrate the exact timestamp value stored in the source table, contact the engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="102ff-141">If you need DMS to migrate the exact timestamp value stored in the source table, contact the engineering team at [dmsfeedback@microsoft.com](mailto:dmsfeedback@microsoft.com).</span></span>

### <a name="data-migration-errors-do-not-provide-additional-details-on-the-database-detailed-status-blade"></a><span data-ttu-id="102ff-142">Data migration errors do not provide additional details on the Database detailed status blade.</span><span class="sxs-lookup"><span data-stu-id="102ff-142">Data migration errors do not provide additional details on the Database detailed status blade.</span></span>

<span data-ttu-id="102ff-143">**Symptom**</span><span class="sxs-lookup"><span data-stu-id="102ff-143">**Symptom**</span></span>

<span data-ttu-id="102ff-144">When you encounter the migration failures in the Databases details status view, selecting the **Data migration errors** link on the top ribbon may not provide  additional details specific to the migration failures.</span><span class="sxs-lookup"><span data-stu-id="102ff-144">When you encounter the migration failures in the Databases details status view, selecting the **Data migration errors** link on the top ribbon may not provide  additional details specific to the migration failures.</span></span>

![data migration errors no details example](media\known-issues-azure-sql-online\dms-data-migration-errors-no-details.png)

<span data-ttu-id="102ff-146">**Workaround**</span><span class="sxs-lookup"><span data-stu-id="102ff-146">**Workaround**</span></span>

<span data-ttu-id="102ff-147">To get to specific failure details, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="102ff-147">To get to specific failure details, follow the steps below.</span></span>

1. <span data-ttu-id="102ff-148">Close the Database detailed status blade to display the Migration activity screen.</span><span class="sxs-lookup"><span data-stu-id="102ff-148">Close the Database detailed status blade to display the Migration activity screen.</span></span>

     ![migration activity screen](media\known-issues-azure-sql-online\dms-migration-activity-screen.png)

2. <span data-ttu-id="102ff-150">Select **See error details** to view specific error messages that help you to troubleshoot migration errors.</span><span class="sxs-lookup"><span data-stu-id="102ff-150">Select **See error details** to view specific error messages that help you to troubleshoot migration errors.</span></span>
