---
title: 'T-SQL: Manage an Azure SQL Database elastic pool | Microsoft Docs'
description: Use T-SQL to manage an Azure SQL Database elastic pool.
services: sql-database
documentationcenter: ''
author: srinia
manager: jhubbard
editor: ''
ms.assetid: 4e288e17-bc3e-4255-9fbe-0a2ac0dbd7dd
ms.service: sql-database
ms.custom: multiple databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-management
ms.date: 05/27/2016
ms.author: srinia
ms.openlocfilehash: a3acd5f4ec63061254b550737ae9fb4d39b343c6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551325"
---
# <a name="monitor-and-manage-an-elastic-pool-with-transact-sql"></a><span data-ttu-id="ce206-103">Monitor and manage an elastic pool with Transact-SQL</span><span class="sxs-lookup"><span data-stu-id="ce206-103">Monitor and manage an elastic pool with Transact-SQL</span></span>
<span data-ttu-id="ce206-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="ce206-104">This topic shows you how to manage scalable [elastic pools](sql-database-elastic-pool.md) with Transact-SQL.</span></span>  <span data-ttu-id="ce206-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="ce206-105">You can also create and manage an Azure elastic pool the [Azure portal](https://portal.azure.com/), [PowerShell](sql-database-elastic-pool-manage-powershell.md), the REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="ce206-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="ce206-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>


<span data-ttu-id="ce206-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span><span class="sxs-lookup"><span data-stu-id="ce206-107">Use the [Create Database (Azure SQL Database)](https://msdn.microsoft.com/library/dn268335.aspx) and [Alter Database(Azure SQL Database)](https://msdn.microsoft.com/library/mt574871.aspx) commands to create and move databases into and out of elastic pools.</span></span> <span data-ttu-id="ce206-108">The elastic pool must exist before you can use these commands.</span><span class="sxs-lookup"><span data-stu-id="ce206-108">The elastic pool must exist before you can use these commands.</span></span> <span data-ttu-id="ce206-109">These commands affect only databases.</span><span class="sxs-lookup"><span data-stu-id="ce206-109">These commands affect only databases.</span></span> <span data-ttu-id="ce206-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span><span class="sxs-lookup"><span data-stu-id="ce206-110">Creation of new pools and the setting of pool properties (such as min and max eDTUs) cannot be changed with T-SQL commands.</span></span>

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="ce206-111">Create a pooled database in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="ce206-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="ce206-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span><span class="sxs-lookup"><span data-stu-id="ce206-112">Use the CREATE DATABASE command with the SERVICE_OBJECTIVE option.</span></span>   

    CREATE DATABASE db1 ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3M100] ));
    -- Create a database named db1 in an elastic named S3M100.

<span data-ttu-id="ce206-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span><span class="sxs-lookup"><span data-stu-id="ce206-113">All databases in an elastic pool inherit the service tier of the elastic pool (Basic, Standard, Premium).</span></span> 

## <a name="move-a-database-between-elastic-pools"></a><span data-ttu-id="ce206-114">Move a database between elastic pools</span><span class="sxs-lookup"><span data-stu-id="ce206-114">Move a database between elastic pools</span></span>
<span data-ttu-id="ce206-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span><span class="sxs-lookup"><span data-stu-id="ce206-115">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC\_POOL.</span></span> <span data-ttu-id="ce206-116">Set the name to the name of the target pool.</span><span class="sxs-lookup"><span data-stu-id="ce206-116">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [PM125] ));
    -- Move the database named db1 to an elastic named P1M125  

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="ce206-117">Move a database into an elastic pool</span><span class="sxs-lookup"><span data-stu-id="ce206-117">Move a database into an elastic pool</span></span>
<span data-ttu-id="ce206-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span><span class="sxs-lookup"><span data-stu-id="ce206-118">Use the ALTER DATABASE command with the MODIFY and set SERVICE\_OBJECTIVE option as ELASTIC_POOL.</span></span> <span data-ttu-id="ce206-119">Set the name to the name of the target pool.</span><span class="sxs-lookup"><span data-stu-id="ce206-119">Set the name to the name of the target pool.</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = ELASTIC_POOL (name = [S3100] ));
    -- Move the database named db1 to an elastic named S3100.

## <a name="move-a-database-out-of-an-elastic-pool"></a><span data-ttu-id="ce206-120">Move a database out of an elastic pool</span><span class="sxs-lookup"><span data-stu-id="ce206-120">Move a database out of an elastic pool</span></span>
<span data-ttu-id="ce206-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span><span class="sxs-lookup"><span data-stu-id="ce206-121">Use the ALTER DATABASE command and set the SERVICE_OBJECTIVE to one of the performance levels (such as S0 or S1).</span></span>

    ALTER DATABASE db1 MODIFY ( SERVICE_OBJECTIVE = 'S1');
    -- Changes the database into a stand-alone database with the service objective S1.

## <a name="list-databases-in-an-elastic-pool"></a><span data-ttu-id="ce206-122">List databases in an elastic pool</span><span class="sxs-lookup"><span data-stu-id="ce206-122">List databases in an elastic pool</span></span>
<span data-ttu-id="ce206-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="ce206-123">Use the [sys.database\_service \_objectives view](https://msdn.microsoft.com/library/mt712619) to list all the databases in an elastic pool.</span></span> <span data-ttu-id="ce206-124">Log in to the master database to query the view.</span><span class="sxs-lookup"><span data-stu-id="ce206-124">Log in to the master database to query the view.</span></span>

    SELECT d.name, slo.*  
    FROM sys.databases d 
    JOIN sys.database_service_objectives slo  
    ON d.database_id = slo.database_id
    WHERE elastic_pool_name = 'MyElasticPool'; 

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="ce206-125">Get resource usage data for an elastic pool</span><span class="sxs-lookup"><span data-stu-id="ce206-125">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="ce206-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span><span class="sxs-lookup"><span data-stu-id="ce206-126">Use the [sys.elastic\_pool \_resource \_stats view](https://msdn.microsoft.com/library/mt280062.aspx) to examine the resource usage statistics of an elastic pool on a logical server.</span></span> <span data-ttu-id="ce206-127">Log in to the master database to query the view.</span><span class="sxs-lookup"><span data-stu-id="ce206-127">Log in to the master database to query the view.</span></span>

    SELECT * FROM sys.elastic_pool_resource_stats 
    WHERE elastic_pool_name = 'MyElasticPool'
    ORDER BY end_time DESC;

## <a name="get-resource-usage-for-a-pooled-database"></a><span data-ttu-id="ce206-128">Get resource usage for a pooled database</span><span class="sxs-lookup"><span data-stu-id="ce206-128">Get resource usage for a pooled database</span></span>
<span data-ttu-id="ce206-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span><span class="sxs-lookup"><span data-stu-id="ce206-129">Use the [sys.dm\_ db\_ resource\_stats view](https://msdn.microsoft.com/library/dn800981.aspx) or [sys.resource \_stats view](https://msdn.microsoft.com/library/dn269979.aspx) to examine the resource usage statistics of a database in an elastic pool.</span></span> <span data-ttu-id="ce206-130">This process is similar to querying resource usage for a single database.</span><span class="sxs-lookup"><span data-stu-id="ce206-130">This process is similar to querying resource usage for a single database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce206-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="ce206-131">Next steps</span></span>
<span data-ttu-id="ce206-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span><span class="sxs-lookup"><span data-stu-id="ce206-132">After creating an elastic pool, you can manage elastic databases in the pool by creating elastic jobs.</span></span> <span data-ttu-id="ce206-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span><span class="sxs-lookup"><span data-stu-id="ce206-133">Elastic jobs facilitate running T-SQL scripts against any number of databases in the pool.</span></span> <span data-ttu-id="ce206-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce206-134">For more information, see [Elastic database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

<span data-ttu-id="ce206-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span><span class="sxs-lookup"><span data-stu-id="ce206-135">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic database tools to scale out, move data, query, or create transactions.</span></span>

