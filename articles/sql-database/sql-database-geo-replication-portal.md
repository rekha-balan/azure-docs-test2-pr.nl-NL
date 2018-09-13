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
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a>Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover

This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.

To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).

> [!NOTE]
> Active geo-replication (readable secondaries) is now available for all databases in all service tiers. In April 2017, the non-readable secondary type will be retired, and existing non-readable databases will automatically be upgraded to readable secondaries.
> 
> 

To configure active geo-replication by using the Azure portal, you need the following resource:

* An Azure SQL database: The primary database that you want to replicate to a different geographical region.

> [!Note]
Active geo-replication must be between databases in the same subscription.

## <a name="add-a-secondary-database"></a>Add a secondary database
The following steps create a new secondary database in a geo-replication partnership.  

To add a secondary database, you must be the subscription owner or co-owner.

The secondary database has the same name as the primary database and has, by default, the same service level. The secondary database can be a single database or a database in an elastic pool. For more information, see [Service tiers](sql-database-service-tiers.md).
After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.

> [!NOTE]
> If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.
> 

1. In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.
2. On the SQL database page, select **Geo-Replication**, and then select the region to create the secondary database. You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).
   
    ![Configure geo-replication](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. Select or configure the server and pricing tier for the secondary database.
   
    ![Configure secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/create-secondary.png)
4. Optionally, you can add a secondary database to an elastic pool. To create the secondary database in a pool, click **elastic pool** and select a pool on the target server. A pool must already exist on the target server. This workflow does not create a pool.
5. Click **Create** to add the secondary.
6. The secondary database is created and the seeding process begins.
   
    ![Configure secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/seeding0.png)
7. When the seeding process is complete, the secondary database displays its status.
   
    ![Seeding complete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a>Initiate a failover

The secondary database can be switched to become the primary.  

1. In the [Azure portal](http://portal.azure.com), browse to the primary database in the Geo-Replication partnership.
2. On the SQL Database blade, select **All settings** > **Geo-Replication**.
3. In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.
   
    ![failover](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-failover-portal/secondaries.png)
4. Click **Yes** to begin the failover.

The command immediately switches the secondary database into the primary role. 

There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched. If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary. The entire operation should take less than a minute to complete under normal circumstances. 

> [!NOTE]
> If the primary is online and committing transactions when the command is issued some data loss may occur.
> 
> 

## <a name="remove-secondary-database"></a>Remove secondary database
This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database. If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.  

1. In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.
2. On the SQL database page, select **Geo-Replication**.
3. In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.
4. Click **Stop Replication**.
   
    ![Remove secondary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-geo-replication-portal/remove-secondary.png)
5. A confirmation window opens. Click **Yes** to remove the database from the geo-replication partnership. (Set it to a read-write database not part of any replication.)

## <a name="next-steps"></a>Next steps
* To learn more about active geo-replication, see [Active geo-replication](sql-database-geo-replication-overview.md).
* For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).







