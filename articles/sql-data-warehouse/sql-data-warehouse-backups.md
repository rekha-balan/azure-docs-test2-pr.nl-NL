---
title: Azure SQL Data Warehouse backups - snapshots, geo-redundant | Microsoft Docs
description: Learn about SQL Data Warehouse built-in database backups that enable you to restore an Azure SQL Data Warehouse to a restore point or a different geographical region.
services: sql-data-warehouse
documentationcenter: ''
author: lakshmi1812
manager: jhubbard
editor: ''
ms.assetid: b5aff094-05b2-4578-acf3-ec456656febd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 3def0a1990217d0c67e5b5f52efc3523525fb344
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555307"
---
# <a name="sql-data-warehouse-backups"></a><span data-ttu-id="64c03-103">SQL Data Warehouse backups</span><span class="sxs-lookup"><span data-stu-id="64c03-103">SQL Data Warehouse backups</span></span>
<span data-ttu-id="64c03-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span><span class="sxs-lookup"><span data-stu-id="64c03-104">SQL Data Warehouse offers both local and geographical backups as part of its data warehouse backup capabilities.</span></span> <span data-ttu-id="64c03-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span><span class="sxs-lookup"><span data-stu-id="64c03-105">These include Azure Storage Blob snapshots and geo-redundant storage.</span></span> <span data-ttu-id="64c03-106">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or restore to a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="64c03-106">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or restore to a different geographical region.</span></span> <span data-ttu-id="64c03-107">This article explains the specifics of backups in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="64c03-107">This article explains the specifics of backups in SQL Data Warehouse.</span></span>

## <a name="what-is-a-data-warehouse-backup"></a><span data-ttu-id="64c03-108">What is a data warehouse backup?</span><span class="sxs-lookup"><span data-stu-id="64c03-108">What is a data warehouse backup?</span></span>
<span data-ttu-id="64c03-109">A data warehouse backup is the data that you can use to restore a data warehouse to a specific time.</span><span class="sxs-lookup"><span data-stu-id="64c03-109">A data warehouse backup is the data that you can use to restore a data warehouse to a specific time.</span></span>  <span data-ttu-id="64c03-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="64c03-110">Since SQL Data Warehouse is a distributed system, a data warehouse backup consists of many files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="64c03-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span><span class="sxs-lookup"><span data-stu-id="64c03-111">Database backups are an essential part of any business continuity and disaster recovery strategy because they protect your data from accidental corruption or deletion.</span></span> <span data-ttu-id="64c03-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-112">For more information, see [Business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>

## <a name="data-redundancy"></a><span data-ttu-id="64c03-113">Data redundancy</span><span class="sxs-lookup"><span data-stu-id="64c03-113">Data redundancy</span></span>
<span data-ttu-id="64c03-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="64c03-114">SQL Data Warehouse protects your data by storing your data in locally redundant (LRS) Azure Premium Storage.</span></span> <span data-ttu-id="64c03-115">This Azure Storage feature stores multiple synchronous copies of the data in the local data center to guarantee transparent data protection if there are localized failures.</span><span class="sxs-lookup"><span data-stu-id="64c03-115">This Azure Storage feature stores multiple synchronous copies of the data in the local data center to guarantee transparent data protection if there are localized failures.</span></span> <span data-ttu-id="64c03-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span><span class="sxs-lookup"><span data-stu-id="64c03-116">Data redundancy ensures that your data can survive infrastructure issues such as disk failures.</span></span> <span data-ttu-id="64c03-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span><span class="sxs-lookup"><span data-stu-id="64c03-117">Data redundancy ensures business continuity with a fault tolerant and highly available infrastructure.</span></span>

<span data-ttu-id="64c03-118">To learn more about:</span><span class="sxs-lookup"><span data-stu-id="64c03-118">To learn more about:</span></span>

* <span data-ttu-id="64c03-119">Azure Premium storage, see [Introduction to Azure Premium Storage](../storage/storage-premium-storage.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-119">Azure Premium storage, see [Introduction to Azure Premium Storage](../storage/storage-premium-storage.md).</span></span>
* <span data-ttu-id="64c03-120">Locally Redundant storage, see [Azure Storage replication](../storage/storage-redundancy.md#locally-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="64c03-120">Locally Redundant storage, see [Azure Storage replication](../storage/storage-redundancy.md#locally-redundant-storage).</span></span>

## <a name="azure-storage-blob-snapshots"></a><span data-ttu-id="64c03-121">Azure Storage Blob snapshots</span><span class="sxs-lookup"><span data-stu-id="64c03-121">Azure Storage Blob snapshots</span></span>
<span data-ttu-id="64c03-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the data warehouse locally.</span><span class="sxs-lookup"><span data-stu-id="64c03-122">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the data warehouse locally.</span></span> <span data-ttu-id="64c03-123">You can restore a data warehouse to a snapshot restore point.</span><span class="sxs-lookup"><span data-stu-id="64c03-123">You can restore a data warehouse to a snapshot restore point.</span></span> <span data-ttu-id="64c03-124">Snapshots start a minimum of every eight hours and are available for seven days.</span><span class="sxs-lookup"><span data-stu-id="64c03-124">Snapshots start a minimum of every eight hours and are available for seven days.</span></span>  

<span data-ttu-id="64c03-125">To learn more about:</span><span class="sxs-lookup"><span data-stu-id="64c03-125">To learn more about:</span></span>

* <span data-ttu-id="64c03-126">Azure blob snapshots, see [Create a blob snapshot](../storage/storage-blob-snapshots.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-126">Azure blob snapshots, see [Create a blob snapshot](../storage/storage-blob-snapshots.md).</span></span>

## <a name="geo-redundant-backups"></a><span data-ttu-id="64c03-127">Geo-redundant backups</span><span class="sxs-lookup"><span data-stu-id="64c03-127">Geo-redundant backups</span></span>
<span data-ttu-id="64c03-128">Every 24 hours, SQL Data Warehouse stores the full data warehouse in Standard storage.</span><span class="sxs-lookup"><span data-stu-id="64c03-128">Every 24 hours, SQL Data Warehouse stores the full data warehouse in Standard storage.</span></span> <span data-ttu-id="64c03-129">The full data warehouse is created to match the time of the last snapshot.</span><span class="sxs-lookup"><span data-stu-id="64c03-129">The full data warehouse is created to match the time of the last snapshot.</span></span> <span data-ttu-id="64c03-130">The standard storage belongs to a geo-redundant storage account with read access (RA-GRS).</span><span class="sxs-lookup"><span data-stu-id="64c03-130">The standard storage belongs to a geo-redundant storage account with read access (RA-GRS).</span></span> <span data-ttu-id="64c03-131">The Azure Storage RA-GRS feature replicates the backup files to a [paired data center](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-131">The Azure Storage RA-GRS feature replicates the backup files to a [paired data center](../best-practices-availability-paired-regions.md).</span></span> <span data-ttu-id="64c03-132">This geo-replication ensures you can restore data warehouse in case you cannot access the snapshots in your primary region.</span><span class="sxs-lookup"><span data-stu-id="64c03-132">This geo-replication ensures you can restore data warehouse in case you cannot access the snapshots in your primary region.</span></span> 

<span data-ttu-id="64c03-133">This feature is on by default.</span><span class="sxs-lookup"><span data-stu-id="64c03-133">This feature is on by default.</span></span> <span data-ttu-id="64c03-134">If you don't want to use geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span><span class="sxs-lookup"><span data-stu-id="64c03-134">If you don't want to use geo-redundant backups, you can [opt out] (https://docs.microsoft.com/powershell/resourcemanager/Azurerm.sql/v2.1.0/Set-AzureRmSqlDatabaseGeoBackupPolicy?redirectedfrom=msdn).</span></span> 

> [!NOTE]
> <span data-ttu-id="64c03-135">In Azure storage, the term *replication* refers to copying files from one location to another.</span><span class="sxs-lookup"><span data-stu-id="64c03-135">In Azure storage, the term *replication* refers to copying files from one location to another.</span></span> <span data-ttu-id="64c03-136">SQL's *database replication* refers to keeping to multiple secondary databases synchronized with a primary database.</span><span class="sxs-lookup"><span data-stu-id="64c03-136">SQL's *database replication* refers to keeping to multiple secondary databases synchronized with a primary database.</span></span> 
> 
> 

<span data-ttu-id="64c03-137">To learn more about:</span><span class="sxs-lookup"><span data-stu-id="64c03-137">To learn more about:</span></span>

* <span data-ttu-id="64c03-138">Geo-redundant storage, see [Azure Storage replication](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-138">Geo-redundant storage, see [Azure Storage replication](../storage/storage-redundancy.md).</span></span>
* <span data-ttu-id="64c03-139">RA-GRS storage, see [Read-access geo-redundant storage](../storage/storage-redundancy.md#read-access-geo-redundant-storage).</span><span class="sxs-lookup"><span data-stu-id="64c03-139">RA-GRS storage, see [Read-access geo-redundant storage](../storage/storage-redundancy.md#read-access-geo-redundant-storage).</span></span>

## <a name="data-warehouse-backup-schedule-and-retention-period"></a><span data-ttu-id="64c03-140">Data warehouse backup schedule and retention period</span><span class="sxs-lookup"><span data-stu-id="64c03-140">Data warehouse backup schedule and retention period</span></span>
<span data-ttu-id="64c03-141">SQL Data Warehouse creates snapshots on your online data warehouses every four to eight hours and keeps each snapshot for seven days.</span><span class="sxs-lookup"><span data-stu-id="64c03-141">SQL Data Warehouse creates snapshots on your online data warehouses every four to eight hours and keeps each snapshot for seven days.</span></span> <span data-ttu-id="64c03-142">You can restore your online database to one of the restore points in the past seven days.</span><span class="sxs-lookup"><span data-stu-id="64c03-142">You can restore your online database to one of the restore points in the past seven days.</span></span> 

<span data-ttu-id="64c03-143">To see when the last snapshot started, run this query on your online SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="64c03-143">To see when the last snapshot started, run this query on your online SQL Data Warehouse.</span></span> 

```sql
select top 1 *
from sys.pdw_loader_backup_runs 
order by run_id desc;
```

<span data-ttu-id="64c03-144">If you need to retain a snapshot for longer than seven days, you can restore a restore point to a new data warehouse.</span><span class="sxs-lookup"><span data-stu-id="64c03-144">If you need to retain a snapshot for longer than seven days, you can restore a restore point to a new data warehouse.</span></span> <span data-ttu-id="64c03-145">After the restore is finished, SQL Data Warehouse starts creating snapshots on the new data warehouse.</span><span class="sxs-lookup"><span data-stu-id="64c03-145">After the restore is finished, SQL Data Warehouse starts creating snapshots on the new data warehouse.</span></span> <span data-ttu-id="64c03-146">If you don't make changes to the new data warehouse, the snapshots stay empty and therefore the snapshot cost is minimal.</span><span class="sxs-lookup"><span data-stu-id="64c03-146">If you don't make changes to the new data warehouse, the snapshots stay empty and therefore the snapshot cost is minimal.</span></span> <span data-ttu-id="64c03-147">You could also pause the database to keep SQL Data Warehouse from creating snapshots.</span><span class="sxs-lookup"><span data-stu-id="64c03-147">You could also pause the database to keep SQL Data Warehouse from creating snapshots.</span></span>

### <a name="what-happens-to-my-backup-retention-while-my-data-warehouse-is-paused"></a><span data-ttu-id="64c03-148">What happens to my backup retention while my data warehouse is paused?</span><span class="sxs-lookup"><span data-stu-id="64c03-148">What happens to my backup retention while my data warehouse is paused?</span></span>
<span data-ttu-id="64c03-149">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span><span class="sxs-lookup"><span data-stu-id="64c03-149">SQL Data Warehouse does not create snapshots and does not expire snapshots while a data warehouse is paused.</span></span> <span data-ttu-id="64c03-150">The snapshot age does not change while the data warehouse is paused.</span><span class="sxs-lookup"><span data-stu-id="64c03-150">The snapshot age does not change while the data warehouse is paused.</span></span> <span data-ttu-id="64c03-151">Snapshot retention is based on the number of days the data warehouse is online, not calendar days.</span><span class="sxs-lookup"><span data-stu-id="64c03-151">Snapshot retention is based on the number of days the data warehouse is online, not calendar days.</span></span>

<span data-ttu-id="64c03-152">For example, if a snapshot starts October 1 at 4 pm and the data warehouse is paused October 3 at 4 pm, the snapshot is two days old.</span><span class="sxs-lookup"><span data-stu-id="64c03-152">For example, if a snapshot starts October 1 at 4 pm and the data warehouse is paused October 3 at 4 pm, the snapshot is two days old.</span></span> <span data-ttu-id="64c03-153">Whenever the data warehouse comes back online the snapshot is two days old.</span><span class="sxs-lookup"><span data-stu-id="64c03-153">Whenever the data warehouse comes back online the snapshot is two days old.</span></span> <span data-ttu-id="64c03-154">If the data warehouse comes online October 5 at 4 pm, the snapshot is two days old and remains for five more days.</span><span class="sxs-lookup"><span data-stu-id="64c03-154">If the data warehouse comes online October 5 at 4 pm, the snapshot is two days old and remains for five more days.</span></span>

<span data-ttu-id="64c03-155">When the data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span><span class="sxs-lookup"><span data-stu-id="64c03-155">When the data warehouse comes back online, SQL Data Warehouse resumes new snapshots and expires snapshots when they have more than seven days of data.</span></span>

### <a name="how-long-is-the-retention-period-for-a-dropped-data-warehouse"></a><span data-ttu-id="64c03-156">How long is the retention period for a dropped data warehouse?</span><span class="sxs-lookup"><span data-stu-id="64c03-156">How long is the retention period for a dropped data warehouse?</span></span>
<span data-ttu-id="64c03-157">When a data warehouse is dropped, the data warehouse and the snapshots are saved for seven days and then removed.</span><span class="sxs-lookup"><span data-stu-id="64c03-157">When a data warehouse is dropped, the data warehouse and the snapshots are saved for seven days and then removed.</span></span> <span data-ttu-id="64c03-158">You can restore the data warehouse to any of the saved restore points.</span><span class="sxs-lookup"><span data-stu-id="64c03-158">You can restore the data warehouse to any of the saved restore points.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64c03-159">If you delete a logical SQL server instance, all databases that belong to the instance are also deleted and cannot be recovered.</span><span class="sxs-lookup"><span data-stu-id="64c03-159">If you delete a logical SQL server instance, all databases that belong to the instance are also deleted and cannot be recovered.</span></span> <span data-ttu-id="64c03-160">You cannot restore a deleted server.</span><span class="sxs-lookup"><span data-stu-id="64c03-160">You cannot restore a deleted server.</span></span>
> 
> 

## <a name="data-warehouse-backup-costs"></a><span data-ttu-id="64c03-161">Data warehouse backup costs</span><span class="sxs-lookup"><span data-stu-id="64c03-161">Data warehouse backup costs</span></span>
<span data-ttu-id="64c03-162">The total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded to the nearest TB.</span><span class="sxs-lookup"><span data-stu-id="64c03-162">The total cost for your primary data warehouse and seven days of Azure Blob snapshots is rounded to the nearest TB.</span></span> <span data-ttu-id="64c03-163">For example, if your data warehouse is 1.5 TB and the snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span><span class="sxs-lookup"><span data-stu-id="64c03-163">For example, if your data warehouse is 1.5 TB and the snapshots use 100 GB, you are billed for 2 TB of data at Azure Premium Storage rates.</span></span> 

> [!NOTE]
> <span data-ttu-id="64c03-164">Each snapshot is empty initially and grows as you make changes to the primary data warehouse.</span><span class="sxs-lookup"><span data-stu-id="64c03-164">Each snapshot is empty initially and grows as you make changes to the primary data warehouse.</span></span> <span data-ttu-id="64c03-165">All snapshots increase in size as the data warehouse changes.</span><span class="sxs-lookup"><span data-stu-id="64c03-165">All snapshots increase in size as the data warehouse changes.</span></span> <span data-ttu-id="64c03-166">Therefore, the storage costs for snapshots grow according to the rate of change.</span><span class="sxs-lookup"><span data-stu-id="64c03-166">Therefore, the storage costs for snapshots grow according to the rate of change.</span></span>
> 
> 

<span data-ttu-id="64c03-167">If you are using geo-redundant storage, you receive a separate storage charge.</span><span class="sxs-lookup"><span data-stu-id="64c03-167">If you are using geo-redundant storage, you receive a separate storage charge.</span></span> <span data-ttu-id="64c03-168">The geo-redundant storage is billed at the standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span><span class="sxs-lookup"><span data-stu-id="64c03-168">The geo-redundant storage is billed at the standard Read-Access Geographically Redundant Storage (RA-GRS) rate.</span></span>

<span data-ttu-id="64c03-169">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="64c03-169">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="using-database-backups"></a><span data-ttu-id="64c03-170">Using database backups</span><span class="sxs-lookup"><span data-stu-id="64c03-170">Using database backups</span></span>
<span data-ttu-id="64c03-171">The primary use for SQL data warehouse backups is to restore the data warehouse to one of the restore points within the retention period.</span><span class="sxs-lookup"><span data-stu-id="64c03-171">The primary use for SQL data warehouse backups is to restore the data warehouse to one of the restore points within the retention period.</span></span>  

* <span data-ttu-id="64c03-172">To restore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64c03-172">To restore a SQL data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="64c03-173">Related topics</span><span class="sxs-lookup"><span data-stu-id="64c03-173">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="64c03-174">Scenarios</span><span class="sxs-lookup"><span data-stu-id="64c03-174">Scenarios</span></span>
* <span data-ttu-id="64c03-175">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="64c03-175">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

* <span data-ttu-id="64c03-176">To restore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span><span class="sxs-lookup"><span data-stu-id="64c03-176">To restore a data warehouse, see [Restore a SQL data warehouse](sql-data-warehouse-restore-database-overview.md)</span></span>

<!-- ### Tutorials -->

