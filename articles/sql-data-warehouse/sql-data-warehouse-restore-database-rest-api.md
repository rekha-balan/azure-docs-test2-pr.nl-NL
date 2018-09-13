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
# <a name="restore-an-azure-sql-data-warehouse-with-rest-apis"></a><span data-ttu-id="69615-103">Restore an Azure SQL Data Warehouse with REST APIs</span><span class="sxs-lookup"><span data-stu-id="69615-103">Restore an Azure SQL Data Warehouse with REST APIs</span></span>
<span data-ttu-id="69615-104">Restore an Azure SQL Data Warehouse using REST APIs.</span><span class="sxs-lookup"><span data-stu-id="69615-104">Restore an Azure SQL Data Warehouse using REST APIs.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="69615-105">Before you begin</span><span class="sxs-lookup"><span data-stu-id="69615-105">Before you begin</span></span>
<span data-ttu-id="69615-106">**Verify your DTU capacity.**</span><span class="sxs-lookup"><span data-stu-id="69615-106">**Verify your DTU capacity.**</span></span> <span data-ttu-id="69615-107">Each SQL Data Warehouse is hosted by a logical SQL server (e.g. myserver.database.windows.net) which has a default [DTU quota](../sql-database/sql-database-what-is-a-dtu.md).</span><span class="sxs-lookup"><span data-stu-id="69615-107">Each SQL Data Warehouse is hosted by a logical SQL server (e.g. myserver.database.windows.net) which has a default [DTU quota](../sql-database/sql-database-what-is-a-dtu.md).</span></span>  <span data-ttu-id="69615-108">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span><span class="sxs-lookup"><span data-stu-id="69615-108">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="69615-109">To request more DTU, you can [Create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="69615-109">To request more DTU, you can [Create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span>

## <a name="restore-an-active-or-paused-data-warehouse"></a><span data-ttu-id="69615-110">Restore an active or paused data warehouse</span><span class="sxs-lookup"><span data-stu-id="69615-110">Restore an active or paused data warehouse</span></span>
<span data-ttu-id="69615-111">To restore a data warehouse:</span><span class="sxs-lookup"><span data-stu-id="69615-111">To restore a data warehouse:</span></span>

1. <span data-ttu-id="69615-112">Get the list of database restore points using the Get Database Restore Points operation.</span><span class="sxs-lookup"><span data-stu-id="69615-112">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="69615-113">Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="69615-113">Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.</span></span>
3. <span data-ttu-id="69615-114">Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="69615-114">Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="69615-115">After the restore has completed, you can configure your recovered data warehouse by following [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).</span><span class="sxs-lookup"><span data-stu-id="69615-115">After the restore has completed, you can configure your recovered data warehouse by following [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).</span></span>
> 
> 

## <a name="restore-a-deleted-data-warehouse"></a><span data-ttu-id="69615-116">Restore a deleted data warehouse</span><span class="sxs-lookup"><span data-stu-id="69615-116">Restore a deleted data warehouse</span></span>
<span data-ttu-id="69615-117">To restore a deleted data warehouse:</span><span class="sxs-lookup"><span data-stu-id="69615-117">To restore a deleted data warehouse:</span></span>

1. <span data-ttu-id="69615-118">List all of your restorable deleted data warehouses by using the [List restorable dropped databases](https://msdn.microsoft.com/library/azure/dn509562.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="69615-118">List all of your restorable deleted data warehouses by using the [List restorable dropped databases](https://msdn.microsoft.com/library/azure/dn509562.aspx) operation.</span></span>
2. <span data-ttu-id="69615-119">Get the details for the deleted data warehouse you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span><span class="sxs-lookup"><span data-stu-id="69615-119">Get the details for the deleted data warehouse you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="69615-120">Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="69615-120">Begin your restore by using the [Create database restore request](https://msdn.microsoft.com/library/azure/dn509571.aspx) operation.</span></span>
4. <span data-ttu-id="69615-121">Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.</span><span class="sxs-lookup"><span data-stu-id="69615-121">Track the status of your restore by using the [Database operation status](https://msdn.microsoft.com/library/azure/dn720371.aspx) operation.</span></span>

> [!NOTE]
> <span data-ttu-id="69615-122">To configure your data warehouse after the restore has completed, see [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).</span><span class="sxs-lookup"><span data-stu-id="69615-122">To configure your data warehouse after the restore has completed, see [Configure your database after recovery](../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="69615-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="69615-123">Next steps</span></span>
<span data-ttu-id="69615-124">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview](../sql-database/sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="69615-124">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview](../sql-database/sql-database-business-continuity.md).</span></span>
