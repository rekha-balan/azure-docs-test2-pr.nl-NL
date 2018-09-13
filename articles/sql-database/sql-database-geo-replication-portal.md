---
title: 'Azure portal: SQL Database geo-replication | Microsoft Docs'
description: Configure geo-replication for Azure SQL Database in the Azure portal and initiate failover
services: sql-database
author: CarlRabeler
manager: craigg
ms.service: sql-database
ms.custom: business continuity
ms.topic: conceptual
ms.date: 07/16/2018
ms.author: carlrab
ms.openlocfilehash: 27fb8f369ad23592902c05fe5275fc54bc6cf148
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774715"
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="4b1a5-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span><span class="sxs-lookup"><span data-stu-id="4b1a5-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="4b1a5-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="4b1a5-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="4b1a5-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span><span class="sxs-lookup"><span data-stu-id="4b1a5-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="4b1a5-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="4b1a5-108">Active geo-replication must be between databases in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="4b1a5-109">Add a secondary database</span><span class="sxs-lookup"><span data-stu-id="4b1a5-109">Add a secondary database</span></span>
<span data-ttu-id="4b1a5-110">The following steps create a new secondary database in a geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="4b1a5-111">To add a secondary database, you must be the subscription owner or co-owner.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="4b1a5-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="4b1a5-113">The secondary database can be a single database or a database in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="4b1a5-114">For more information, see [DTU-based purchasing model](sql-database-service-tiers-dtu.md) and [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-114">For more information, see [DTU-based purchasing model](sql-database-service-tiers-dtu.md) and [vCore-based purchasing model](sql-database-service-tiers-vcore.md).</span></span>
<span data-ttu-id="4b1a5-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="4b1a5-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="4b1a5-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="4b1a5-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="4b1a5-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configure geo-replication](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="4b1a5-121">Select or configure the server and pricing tier for the secondary database.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configure secondary](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="4b1a5-123">Optionally, you can add a secondary database to an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="4b1a5-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="4b1a5-125">A pool must already exist on the target server.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="4b1a5-126">This workflow does not create a pool.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="4b1a5-127">Click **Create** to add the secondary.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="4b1a5-128">The secondary database is created and the seeding process begins.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configure secondary](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="4b1a5-130">When the seeding process is complete, the secondary database displays its status.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Seeding complete](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="4b1a5-132">Initiate a failover</span><span class="sxs-lookup"><span data-stu-id="4b1a5-132">Initiate a failover</span></span>

<span data-ttu-id="4b1a5-133">The secondary database can be switched to become the primary.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="4b1a5-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="4b1a5-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="4b1a5-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="4b1a5-138">Click **Yes** to begin the failover.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="4b1a5-139">The command immediately switches the secondary database into the primary role.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="4b1a5-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="4b1a5-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="4b1a5-142">The entire operation should take less than a minute to complete under normal circumstances.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="4b1a5-143">This command is designed for quick recovery of the database in case of an outage.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="4b1a5-144">It triggers failover without data synchronization (forced failover).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="4b1a5-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="4b1a5-146">Remove secondary database</span><span class="sxs-lookup"><span data-stu-id="4b1a5-146">Remove secondary database</span></span>
<span data-ttu-id="4b1a5-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="4b1a5-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="4b1a5-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="4b1a5-150">On the SQL database page, select **geo-replication**.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="4b1a5-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="4b1a5-152">Click **Stop Replication**.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-152">Click **Stop Replication**.</span></span>
   
    ![Remove secondary](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="4b1a5-154">A confirmation window opens.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-154">A confirmation window opens.</span></span> <span data-ttu-id="4b1a5-155">Click **Yes** to remove the database from the geo-replication partnership.</span><span class="sxs-lookup"><span data-stu-id="4b1a5-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="4b1a5-156">(Set it to a read-write database not part of any replication.)</span><span class="sxs-lookup"><span data-stu-id="4b1a5-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b1a5-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b1a5-157">Next steps</span></span>
* <span data-ttu-id="4b1a5-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="4b1a5-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a5-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

