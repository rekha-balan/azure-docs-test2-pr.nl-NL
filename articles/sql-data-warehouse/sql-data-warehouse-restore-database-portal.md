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
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="28aeb-103">Restore Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="28aeb-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
<span data-ttu-id="28aeb-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="28aeb-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28aeb-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="28aeb-109">Before you begin</span></span>
<span data-ttu-id="28aeb-110">**Verify your DTU capacity.**</span><span class="sxs-lookup"><span data-stu-id="28aeb-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="28aeb-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span><span class="sxs-lookup"><span data-stu-id="28aeb-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="28aeb-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span><span class="sxs-lookup"><span data-stu-id="28aeb-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="28aeb-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="28aeb-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="28aeb-114">Restore an active or paused database</span><span class="sxs-lookup"><span data-stu-id="28aeb-114">Restore an active or paused database</span></span>
<span data-ttu-id="28aeb-115">To restore a database:</span><span class="sxs-lookup"><span data-stu-id="28aeb-115">To restore a database:</span></span>

1. <span data-ttu-id="28aeb-116">Sign in to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="28aeb-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="28aeb-117">In the left pane, select **Browse**, and then select **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Select Browse > SQL servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="28aeb-119">Find your server, and then select it.</span><span class="sxs-lookup"><span data-stu-id="28aeb-119">Find your server, and then select it.</span></span>

    ![Select your server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="28aeb-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span><span class="sxs-lookup"><span data-stu-id="28aeb-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Select the instance of SQL Data Warehouse to restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="28aeb-123">At the top of the Data Warehouse blade, select **Restore**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Select Restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="28aeb-125">Specify a new **Database name**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="28aeb-126">Select the latest **Restore point**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="28aeb-127">Make sure you choose the latest restore point.</span><span class="sxs-lookup"><span data-stu-id="28aeb-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="28aeb-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span><span class="sxs-lookup"><span data-stu-id="28aeb-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Select a restore point](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="28aeb-130">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-130">Select **OK**.</span></span>
9. <span data-ttu-id="28aeb-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span><span class="sxs-lookup"><span data-stu-id="28aeb-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="28aeb-133">Restore a deleted database</span><span class="sxs-lookup"><span data-stu-id="28aeb-133">Restore a deleted database</span></span>
<span data-ttu-id="28aeb-134">To restore a deleted database:</span><span class="sxs-lookup"><span data-stu-id="28aeb-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="28aeb-135">Sign in to the [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="28aeb-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="28aeb-136">In the left pane, select **Browse**, and then select **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Select Browse > SQL servers](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="28aeb-138">Find your server, and then select it.</span><span class="sxs-lookup"><span data-stu-id="28aeb-138">Find your server, and then select it.</span></span>

    ![Select your server](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="28aeb-140">Scroll down to the **Operations** section on your server's blade.</span><span class="sxs-lookup"><span data-stu-id="28aeb-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="28aeb-141">Select the **Deleted databases** tile.</span><span class="sxs-lookup"><span data-stu-id="28aeb-141">Select the **Deleted databases** tile.</span></span>

    ![Select the Deleted databases tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="28aeb-143">Select the deleted database that you want to restore.</span><span class="sxs-lookup"><span data-stu-id="28aeb-143">Select the deleted database that you want to restore.</span></span>

    ![Select a database to restore](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="28aeb-145">Specify a new **Database name**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-145">Specify a new **Database name**.</span></span>

    ![Add a name for the database](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-data-warehouse/media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="28aeb-147">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="28aeb-147">Select **OK**.</span></span>
9. <span data-ttu-id="28aeb-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span><span class="sxs-lookup"><span data-stu-id="28aeb-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].
>
>

## <a name="next-steps"></a><span data-ttu-id="28aeb-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="28aeb-150">Next steps</span></span>
<span data-ttu-id="28aeb-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="28aeb-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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










