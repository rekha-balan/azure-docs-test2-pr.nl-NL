---
title: Restore an Azure SQL Data Warehouse - REST API | Microsoft Docs
description: Restore an Azure SQL Data Warehouse using REST APIs.
services: sql-data-warehouse
author: kevinvngo
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: manage
ms.date: 04/17/2018
ms.author: kevin
ms.reviewer: igorstan
ms.openlocfilehash: 71236afd3f72497887f42667f971539ed294bef1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784581"
---
# <a name="restore-an-azure-sql-data-warehouse-with-rest-apis"></a>Restore an Azure SQL Data Warehouse with REST APIs
Restore an Azure SQL Data Warehouse using REST APIs.

## <a name="before-you-begin"></a>Before you begin
**Verify your DTU capacity.** Each SQL Data Warehouse is hosted by a logical SQL server (e.g. myserver.database.windows.net) which has a default [DTU quota](../sql-database/sql-database-what-is-a-dtu.md).  Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored. To request more DTU, you can [Create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).

## <a name="restore-an-active-or-paused-data-warehouse"></a>Restore an active or paused data warehouse
To restore a data warehouse:

1. Get the list of database restore points using the Get Database Restore Points operation.
2. Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.
3. Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.

> [!NOTE]
> After the restore has completed, you can configure your recovered data warehouse by following [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).
> 
> 

## <a name="restore-a-deleted-data-warehouse"></a>Restore a deleted data warehouse
To restore a deleted data warehouse:

1. List all of your restorable deleted data warehouses by using the [List restorable dropped databases](https://msdn.microsoft.com/library/azure/dn509562.aspx) operation.
2. Get the details for the deleted data warehouse you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.
3. Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.
4. Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.

> [!NOTE]
> To configure your data warehouse after the restore has completed, see [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).
> 
> 

## <a name="next-steps"></a>Next steps
To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview](../sql-database/sql-database-business-continuity.md).
