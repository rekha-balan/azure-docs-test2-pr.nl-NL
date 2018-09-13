---
title: Restore Azure SQL Data Warehouse (Azure portal) | Microsoft Docs
description: Azure portal tasks for restoring Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: ''
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess;sonyama
ms.openlocfilehash: 0e8dad6cb51e1c136875ce5e9b2bcc367f0eb874
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551130"
---
# <a name="restore-azure-sql-data-warehouse-portal"></a>Restore Azure SQL Data Warehouse (portal)
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.

## <a name="before-you-begin"></a>Before you begin
**Verify your DTU capacity.** Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota. Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring. To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Restore an active or paused database
To restore a database:

1. Sign in to the [Azure portal][Azure portal].
2. In the left pane, select **Browse**, and then select **SQL servers**.

    ![Select Browse > SQL servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Find your server, and then select it.

    ![Select your server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Find the instance of SQL Data Warehouse that you want to restore from, and then select it.

    ![Select the instance of SQL Data Warehouse to restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. At the top of the Data Warehouse blade, select **Restore**.

    ![Select Restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Specify a new **Database name**.
7. Select the latest **Restore point**.

   Make sure you choose the latest restore point. Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.

      ![Select a restore point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Select **OK**.
9. The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.

> [!NOTE]
> After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Restore a deleted database
To restore a deleted database:

1. Sign in to the [Azure portal][Azure portal].
2. In the left pane, select **Browse**, and then select **SQL servers**.

    ![Select Browse > SQL servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Find your server, and then select it.

    ![Select your server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Scroll down to the **Operations** section on your server's blade.
5. Select the **Deleted databases** tile.

    ![Select the Deleted databases tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Select the deleted database that you want to restore.

    ![Select a database to restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Specify a new **Database name**.

    ![Add a name for the database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Select **OK**.
9. The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.

> [!NOTE]
> To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Next steps
To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/










