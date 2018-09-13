---
title: Pause, resume, scale with T-SQL in Azure SQL Data Warehouse | Microsoft Docs
description: Transact-SQL (T-SQL) tasks to scale-out performance by adjusting DWUs. Save costs by scaling back during non-peak times.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: a970d939-2adf-4856-8a78-d4fe8ab2cceb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: e37a943c775261a6817169c95a931f1b268305d9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552533"
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-t-sql"></a><span data-ttu-id="4e3f7-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="4e3f7-104">Manage compute power in Azure SQL Data Warehouse (T-SQL)</span></span>
> [!div class="op_single_selector"]
> * [Overview](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="current-dwu-bk"></a>

## <a name="view-current-dwu-settings"></a><span data-ttu-id="4e3f7-110">View current DWU settings</span><span class="sxs-lookup"><span data-stu-id="4e3f7-110">View current DWU settings</span></span>
<span data-ttu-id="4e3f7-111">To view the current DWU settings for your databases:</span><span class="sxs-lookup"><span data-stu-id="4e3f7-111">To view the current DWU settings for your databases:</span></span>

1. <span data-ttu-id="4e3f7-112">Open SQL Server Object Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-112">Open SQL Server Object Explorer in Visual Studio.</span></span>
2. <span data-ttu-id="4e3f7-113">Connect to the master database associated with the logical SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-113">Connect to the master database associated with the logical SQL Database server.</span></span>
3. <span data-ttu-id="4e3f7-114">Select from the sys.database_service_objectives dynamic management view.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-114">Select from the sys.database_service_objectives dynamic management view.</span></span> <span data-ttu-id="4e3f7-115">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="4e3f7-115">Here is an example:</span></span> 

```sql
SELECT
    db.name [Database]
,   ds.edition [Edition]
,   ds.service_objective [Service Objective]
FROM
    sys.database_service_objectives ds
JOIN
    sys.databases db ON ds.database_id = db.database_id
```

<a name="scale-dwu-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute"></a><span data-ttu-id="4e3f7-116">Scale compute</span><span class="sxs-lookup"><span data-stu-id="4e3f7-116">Scale compute</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="4e3f7-117">To change the DWUs:</span><span class="sxs-lookup"><span data-stu-id="4e3f7-117">To change the DWUs:</span></span>

1. <span data-ttu-id="4e3f7-118">Connect to the master database associated with your logical SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-118">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="4e3f7-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-119">Use the [ALTER DATABASE][ALTER DATABASE] TSQL statement.</span></span> <span data-ttu-id="4e3f7-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-120">The following example sets the service level objective to DW1000 for the database MySQLDW.</span></span> 

```Sql
ALTER DATABASE MySQLDW
MODIFY (SERVICE_OBJECTIVE = 'DW1000')
;
```

<a name="check-database-state-bk"></a>

## <a name="check-database-state-and-operation-progress"></a><span data-ttu-id="4e3f7-121">Check database state and operation progress</span><span class="sxs-lookup"><span data-stu-id="4e3f7-121">Check database state and operation progress</span></span>

1. <span data-ttu-id="4e3f7-122">Connect to the master database associated with your logical SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-122">Connect to the master database associated with your logical SQL Database server.</span></span>
2. <span data-ttu-id="4e3f7-123">Submit query to check database state</span><span class="sxs-lookup"><span data-stu-id="4e3f7-123">Submit query to check database state</span></span>

```sql
SELECT *
FROM
sys.databases
```

3. <span data-ttu-id="4e3f7-124">Submit query to check status of operation</span><span class="sxs-lookup"><span data-stu-id="4e3f7-124">Submit query to check status of operation</span></span>

```sql
SELECT *
FROM
    sys.dm_operation_status
WHERE
    resource_type_desc = 'Database'
AND 
    major_resource_id = 'MySQLDW'
```

<span data-ttu-id="4e3f7-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span><span class="sxs-lookup"><span data-stu-id="4e3f7-125">This DMV will return information about various management operations on your SQL Data Warehouse such as the operation and the state of the operation, which will either be IN_PROGRESS or COMPLETED.</span></span>



<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="4e3f7-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="4e3f7-126">Next steps</span></span>
<span data-ttu-id="4e3f7-127">For other management tasks, see [Management overview][Management overview].</span><span class="sxs-lookup"><span data-stu-id="4e3f7-127">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Service capacity limits]: ./sql-data-warehouse-service-capacity-limits.md
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute power overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->

[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
