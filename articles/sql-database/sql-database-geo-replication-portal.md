---
title: 'Azure portal: SQL Database geo-replication | Microsoft Docs'
description: Configure geo-replication for Azure SQL Database in the Azure portal and initiate failover
services: sql-database
documentationcenter: ''
author: CarlRabeler
manager: jhubbard
editor: ''
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/062/2016
ms.author: carlrab
ms.openlocfilehash: b642981e9f9bf2b05483efefd47e72e99fa9e7e8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553289"
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="85f89-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span><span class="sxs-lookup"><span data-stu-id="85f89-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="85f89-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span><span class="sxs-lookup"><span data-stu-id="85f89-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="85f89-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="85f89-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="85f89-106">Active geo-replication (readable secondaries) is now available for all databases in all service tiers.</span><span class="sxs-lookup"><span data-stu-id="85f89-106">Active geo-replication (readable secondaries) is now available for all databases in all service tiers.</span></span> <span data-ttu-id="85f89-107">In April 2017, the non-readable secondary type will be retired, and existing non-readable databases will automatically be upgraded to readable secondaries.</span><span class="sxs-lookup"><span data-stu-id="85f89-107">In April 2017, the non-readable secondary type will be retired, and existing non-readable databases will automatically be upgraded to readable secondaries.</span></span>
> 
> 

<span data-ttu-id="85f89-108">To configure active geo-replication by using the Azure portal, you need the following resource:</span><span class="sxs-lookup"><span data-stu-id="85f89-108">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="85f89-109">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="85f89-109">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="85f89-110">Active geo-replication must be between databases in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="85f89-110">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="85f89-111">Add a secondary database</span><span class="sxs-lookup"><span data-stu-id="85f89-111">Add a secondary database</span></span>
<span data-ttu-id="85f89-112">The following steps create a new secondary database in a geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="85f89-112">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="85f89-113">To add a secondary database, you must be the subscription owner or co-owner.</span><span class="sxs-lookup"><span data-stu-id="85f89-113">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="85f89-114">The secondary database has the same name as the primary database and has, by default, the same service level.</span><span class="sxs-lookup"><span data-stu-id="85f89-114">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="85f89-115">The secondary database can be a single database or a database in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="85f89-115">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="85f89-116">For more information, see [Service tiers](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="85f89-116">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="85f89-117">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span><span class="sxs-lookup"><span data-stu-id="85f89-117">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="85f89-118">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span><span class="sxs-lookup"><span data-stu-id="85f89-118">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="85f89-119">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="85f89-119">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="85f89-120">On the SQL database page, select **Geo-Replication**, and then select the region to create the secondary database.</span><span class="sxs-lookup"><span data-stu-id="85f89-120">On the SQL database page, select **Geo-Replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="85f89-121">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="85f89-121">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configure geo-replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="85f89-123">Select or configure the server and pricing tier for the secondary database.</span><span class="sxs-lookup"><span data-stu-id="85f89-123">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configure secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="85f89-125">Optionally, you can add a secondary database to an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="85f89-125">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="85f89-126">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span><span class="sxs-lookup"><span data-stu-id="85f89-126">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="85f89-127">A pool must already exist on the target server.</span><span class="sxs-lookup"><span data-stu-id="85f89-127">A pool must already exist on the target server.</span></span> <span data-ttu-id="85f89-128">This workflow does not create a pool.</span><span class="sxs-lookup"><span data-stu-id="85f89-128">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="85f89-129">Click **Create** to add the secondary.</span><span class="sxs-lookup"><span data-stu-id="85f89-129">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="85f89-130">The secondary database is created and the seeding process begins.</span><span class="sxs-lookup"><span data-stu-id="85f89-130">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configure secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="85f89-132">When the seeding process is complete, the secondary database displays its status.</span><span class="sxs-lookup"><span data-stu-id="85f89-132">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Seeding complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="85f89-134">Initiate a failover</span><span class="sxs-lookup"><span data-stu-id="85f89-134">Initiate a failover</span></span>

<span data-ttu-id="85f89-135">The secondary database can be switched to become the primary.</span><span class="sxs-lookup"><span data-stu-id="85f89-135">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="85f89-136">In the [Azure portal](http://portal.azure.com), browse to the primary database in the Geo-Replication partnership.</span><span class="sxs-lookup"><span data-stu-id="85f89-136">In the [Azure portal](http://portal.azure.com), browse to the primary database in the Geo-Replication partnership.</span></span>
2. <span data-ttu-id="85f89-137">On the SQL Database blade, select **All settings** > **Geo-Replication**.</span><span class="sxs-lookup"><span data-stu-id="85f89-137">On the SQL Database blade, select **All settings** > **Geo-Replication**.</span></span>
3. <span data-ttu-id="85f89-138">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span><span class="sxs-lookup"><span data-stu-id="85f89-138">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![failover](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="85f89-140">Click **Yes** to begin the failover.</span><span class="sxs-lookup"><span data-stu-id="85f89-140">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="85f89-141">The command immediately switches the secondary database into the primary role.</span><span class="sxs-lookup"><span data-stu-id="85f89-141">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="85f89-142">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span><span class="sxs-lookup"><span data-stu-id="85f89-142">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="85f89-143">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span><span class="sxs-lookup"><span data-stu-id="85f89-143">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="85f89-144">The entire operation should take less than a minute to complete under normal circumstances.</span><span class="sxs-lookup"><span data-stu-id="85f89-144">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="85f89-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span><span class="sxs-lookup"><span data-stu-id="85f89-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span>
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="85f89-146">Remove secondary database</span><span class="sxs-lookup"><span data-stu-id="85f89-146">Remove secondary database</span></span>
<span data-ttu-id="85f89-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span><span class="sxs-lookup"><span data-stu-id="85f89-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="85f89-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span><span class="sxs-lookup"><span data-stu-id="85f89-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="85f89-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="85f89-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="85f89-150">On the SQL database page, select **Geo-Replication**.</span><span class="sxs-lookup"><span data-stu-id="85f89-150">On the SQL database page, select **Geo-Replication**.</span></span>
3. <span data-ttu-id="85f89-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="85f89-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="85f89-152">Click **Stop Replication**.</span><span class="sxs-lookup"><span data-stu-id="85f89-152">Click **Stop Replication**.</span></span>
   
    ![Remove secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="85f89-154">A confirmation window opens.</span><span class="sxs-lookup"><span data-stu-id="85f89-154">A confirmation window opens.</span></span> <span data-ttu-id="85f89-155">Click **Yes** to remove the database from the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="85f89-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="85f89-156">(Set it to a read-write database not part of any replication.)</span><span class="sxs-lookup"><span data-stu-id="85f89-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="85f89-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="85f89-157">Next steps</span></span>
* <span data-ttu-id="85f89-158">To learn more about active geo-replication, see [Active geo-replication](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85f89-158">To learn more about active geo-replication, see [Active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="85f89-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="85f89-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>







