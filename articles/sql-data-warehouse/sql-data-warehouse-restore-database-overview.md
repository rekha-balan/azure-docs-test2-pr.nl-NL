---
title: Restore an Azure data warehouse - local and geo-redundant | Microsoft Docs
description: Overview of the database restore options for recovering a database in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: ''
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: bb311a7747d3f2761d9e295421135a040b2359ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556441"
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="19364-103">SQL Data Warehouse restore</span><span class="sxs-lookup"><span data-stu-id="19364-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

<span data-ttu-id="19364-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span><span class="sxs-lookup"><span data-stu-id="19364-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="19364-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="19364-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="19364-110">This article explains the specifics of restoring a data warehouse.</span><span class="sxs-lookup"><span data-stu-id="19364-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="19364-111">What is a data warehouse restore?</span><span class="sxs-lookup"><span data-stu-id="19364-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="19364-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span><span class="sxs-lookup"><span data-stu-id="19364-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="19364-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span><span class="sxs-lookup"><span data-stu-id="19364-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="19364-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="19364-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="19364-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span><span class="sxs-lookup"><span data-stu-id="19364-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="19364-116">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="19364-116">For more information, see:</span></span>

* [<span data-ttu-id="19364-117">SQL Data Warehouse backups</span><span class="sxs-lookup"><span data-stu-id="19364-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="19364-118">Business continuity overview</span><span class="sxs-lookup"><span data-stu-id="19364-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="19364-119">Data warehouse restore points</span><span class="sxs-lookup"><span data-stu-id="19364-119">Data warehouse restore points</span></span>
<span data-ttu-id="19364-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span><span class="sxs-lookup"><span data-stu-id="19364-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="19364-121">Each snapshot has a restore point that represents the time the snapshot started.</span><span class="sxs-lookup"><span data-stu-id="19364-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="19364-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span><span class="sxs-lookup"><span data-stu-id="19364-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="19364-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span><span class="sxs-lookup"><span data-stu-id="19364-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="19364-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span><span class="sxs-lookup"><span data-stu-id="19364-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="19364-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span><span class="sxs-lookup"><span data-stu-id="19364-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="19364-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="19364-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="19364-127">Geo-redundant restore</span><span class="sxs-lookup"><span data-stu-id="19364-127">Geo-redundant restore</span></span>
<span data-ttu-id="19364-128">If you are using the geo-redundant storage, you can restore the data warehouse to your [paired data center](../best-practices-availability-paired-regions.md) in a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="19364-128">If you are using the geo-redundant storage, you can restore the data warehouse to your [paired data center](../best-practices-availability-paired-regions.md) in a different geographical region.</span></span> <span data-ttu-id="19364-129">The data warehouse is restored from the last daily backup.</span><span class="sxs-lookup"><span data-stu-id="19364-129">The data warehouse is restored from the last daily backup.</span></span> 

## <a name="restore-timeline"></a><span data-ttu-id="19364-130">Restore timeline</span><span class="sxs-lookup"><span data-stu-id="19364-130">Restore timeline</span></span>
<span data-ttu-id="19364-131">You can restore a database to any available restore point within the last seven days.</span><span class="sxs-lookup"><span data-stu-id="19364-131">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="19364-132">Snapshots start every four to eight hours and are available for seven days.</span><span class="sxs-lookup"><span data-stu-id="19364-132">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="19364-133">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span><span class="sxs-lookup"><span data-stu-id="19364-133">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="19364-134">Restore costs</span><span class="sxs-lookup"><span data-stu-id="19364-134">Restore costs</span></span>
<span data-ttu-id="19364-135">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span><span class="sxs-lookup"><span data-stu-id="19364-135">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="19364-136">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span><span class="sxs-lookup"><span data-stu-id="19364-136">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="19364-137">The advantage of pausing is you are not charged for the DWU computing resources.</span><span class="sxs-lookup"><span data-stu-id="19364-137">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="19364-138">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="19364-138">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="19364-139">Uses for restore</span><span class="sxs-lookup"><span data-stu-id="19364-139">Uses for restore</span></span>
<span data-ttu-id="19364-140">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span><span class="sxs-lookup"><span data-stu-id="19364-140">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="19364-141">You can also use data warehouse restore to retain a backup for longer than seven days.</span><span class="sxs-lookup"><span data-stu-id="19364-141">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="19364-142">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span><span class="sxs-lookup"><span data-stu-id="19364-142">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="19364-143">The paused database incurs storage charges at the Azure Premium Storage rate.</span><span class="sxs-lookup"><span data-stu-id="19364-143">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="19364-144">Related topics</span><span class="sxs-lookup"><span data-stu-id="19364-144">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="19364-145">Scenarios</span><span class="sxs-lookup"><span data-stu-id="19364-145">Scenarios</span></span>
* <span data-ttu-id="19364-146">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="19364-146">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="19364-147">To perform a data warehouse restore, restore using:</span><span class="sxs-lookup"><span data-stu-id="19364-147">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="19364-148">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="19364-148">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="19364-149">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="19364-149">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="19364-150">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="19364-150">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
