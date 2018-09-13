---
title: Pause, resume, scale with REST in Azure SQL Data Warehouse | Microsoft Docs
description: PowerShell tasks to manage compute power. Scale compute resources by adjusting DWUs. Or, pause and resume compute resources to save costs.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: barbkess
editor: ''
ms.assetid: 21de7337-9356-49bb-a6eb-06c1beeba2c4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 482b7b2cbd770c6ceaf335309b26c32e6116a3c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564409"
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-rest"></a><span data-ttu-id="03ef8-105">Manage compute power in Azure SQL Data Warehouse (REST)</span><span class="sxs-lookup"><span data-stu-id="03ef8-105">Manage compute power in Azure SQL Data Warehouse (REST)</span></span>
> [!div class="op_single_selector"]
> * [Overview](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>

<a name="scale-performance-bk"></a>
<a name="scale-compute-bk"></a>

## <a name="scale-compute-power"></a><span data-ttu-id="03ef8-111">Scale compute power</span><span class="sxs-lookup"><span data-stu-id="03ef8-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="03ef8-112">To change the DWUs, use the [Create or Update Database][Create or Update Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="03ef8-112">To change the DWUs, use the [Create or Update Database][Create or Update Database] REST API.</span></span> <span data-ttu-id="03ef8-113">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span><span class="sxs-lookup"><span data-stu-id="03ef8-113">The following example sets the service level objective to DW1000 for the database MySQLDW which is hosted on server MyServer.</span></span> <span data-ttu-id="03ef8-114">The server is in an Azure resource group named ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="03ef8-114">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
PUT https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/ResourceGroup1/providers/Microsoft.Sql/servers/MyServer/databases/MySQLDW?api-version=2014-04-01-preview HTTP/1.1
Content-Type: application/json; charset=UTF-8

{
    "properties": {
        "requestedServiceObjectiveName": DW1000
    }
}
```

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="03ef8-115">Pause compute</span><span class="sxs-lookup"><span data-stu-id="03ef8-115">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="03ef8-116">To pause a database, use the [Pause Database][Pause Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="03ef8-116">To pause a database, use the [Pause Database][Pause Database] REST API.</span></span> <span data-ttu-id="03ef8-117">The following example pauses a database named Database02 hosted on a server named Server01.</span><span class="sxs-lookup"><span data-stu-id="03ef8-117">The following example pauses a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="03ef8-118">The server is in an Azure resource group named ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="03ef8-118">The server is in an Azure resource group named ResourceGroup1.</span></span>

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/ResourceGroup1/providers/Microsoft.Sql/servers/Server01/databases/Database02/pause?api-version=2014-04-01-preview HTTP/1.1
```

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="03ef8-119">Resume compute</span><span class="sxs-lookup"><span data-stu-id="03ef8-119">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="03ef8-120">To start a database, use the [Resume Database][Resume Database] REST API.</span><span class="sxs-lookup"><span data-stu-id="03ef8-120">To start a database, use the [Resume Database][Resume Database] REST API.</span></span> <span data-ttu-id="03ef8-121">The following example starts a database named Database02 hosted on a server named Server01.</span><span class="sxs-lookup"><span data-stu-id="03ef8-121">The following example starts a database named Database02 hosted on a server named Server01.</span></span> <span data-ttu-id="03ef8-122">The server is in an Azure resource group named ResourceGroup1.</span><span class="sxs-lookup"><span data-stu-id="03ef8-122">The server is in an Azure resource group named ResourceGroup1.</span></span> 

```
POST https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/ResourceGroup1/providers/Microsoft.Sql/servers/Server01/databases/Database02/resume?api-version=2014-04-01-preview HTTP/1.1
```

## <a name="check-database-state"></a><span data-ttu-id="03ef8-123">Check database state</span><span class="sxs-lookup"><span data-stu-id="03ef8-123">Check database state</span></span>

```json
GET https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Sql/servers/{serverName}/databases/{databaseName}?api-version=2014-04-01 HTTP/1.1
```

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="03ef8-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="03ef8-124">Next steps</span></span>
<span data-ttu-id="03ef8-125">For other management tasks, see [Management overview][Management overview].</span><span class="sxs-lookup"><span data-stu-id="03ef8-125">For other management tasks, see [Management overview][Management overview].</span></span>

<!--Image references-->

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->
[Pause Database]: https://msdn.microsoft.com/library/azure/mt718817.aspx
[Resume Database]: https://msdn.microsoft.com/library/azure/mt718820.aspx
[Create or Update Database]: https://msdn.microsoft.com/library/azure/mt163685.aspx

<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
