---
title: Restore an Azure SQL Data Warehouse (REST API) | Microsoft Docs
description: REST API tasks for restoring an Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: ''
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555241"
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="cec18-103">Restore an Azure SQL Data Warehouse (REST API)</span><span class="sxs-lookup"><span data-stu-id="cec18-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * [Overview][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

<span data-ttu-id="cec18-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span><span class="sxs-lookup"><span data-stu-id="cec18-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cec18-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="cec18-109">Before you begin</span></span>
<span data-ttu-id="cec18-110">**Verify your DTU capacity.**</span><span class="sxs-lookup"><span data-stu-id="cec18-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="cec18-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span><span class="sxs-lookup"><span data-stu-id="cec18-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="cec18-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span><span class="sxs-lookup"><span data-stu-id="cec18-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="cec18-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="cec18-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="cec18-114">Restore an active or paused database</span><span class="sxs-lookup"><span data-stu-id="cec18-114">Restore an active or paused database</span></span>
<span data-ttu-id="cec18-115">To restore a database:</span><span class="sxs-lookup"><span data-stu-id="cec18-115">To restore a database:</span></span>

1. <span data-ttu-id="cec18-116">Get the list of database restore points using the Get Database Restore Points operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="cec18-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="cec18-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="cec18-120">Restore a deleted database</span><span class="sxs-lookup"><span data-stu-id="cec18-120">Restore a deleted database</span></span>
<span data-ttu-id="cec18-121">To restore a deleted database:</span><span class="sxs-lookup"><span data-stu-id="cec18-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="cec18-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="cec18-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="cec18-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="cec18-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span><span class="sxs-lookup"><span data-stu-id="cec18-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cec18-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="cec18-127">Next steps</span></span>
<span data-ttu-id="cec18-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="cec18-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
