---
title: Elastic Database tools glossary | Microsoft Docs
description: Explanation of terms used for elastic database tools
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: a23a4e81-6706-452d-afc1-a550e5e47af9
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f74108922e241a7f81973f9a5c9ae3530efdbc16
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564662"
---
# <a name="elastic-database-tools-glossary"></a><span data-ttu-id="5bdc9-103">Elastic Database tools glossary</span><span class="sxs-lookup"><span data-stu-id="5bdc9-103">Elastic Database tools glossary</span></span>
<span data-ttu-id="5bdc9-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-104">The following terms are defined for the [Elastic Database tools](sql-database-elastic-scale-introduction.md), a feature of Azure SQL Database.</span></span> <span data-ttu-id="5bdc9-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bdc9-105">The tools are used to manage [shard maps](sql-database-elastic-scale-shard-map-management.md), and include the [client library](sql-database-elastic-database-client-library.md), the [split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md), [elastic pools](sql-database-elastic-pool.md), and [queries](sql-database-elastic-query-overview.md).</span></span> 

<span data-ttu-id="5bdc9-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span><span class="sxs-lookup"><span data-stu-id="5bdc9-106">These terms are used in [Adding a shard using Elastic Database tools](sql-database-elastic-scale-add-a-shard.md) and [Using the RecoveryManager class to fix shard map problems](sql-database-elastic-database-recovery-manager.md).</span></span>

![Elastic Scale terms][1]

<span data-ttu-id="5bdc9-108">**Database**: An Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-108">**Database**: An Azure SQL database.</span></span> 

<span data-ttu-id="5bdc9-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-109">**Data dependent routing**: The functionality that enables an application to connect to a shard given a specific sharding key.</span></span> <span data-ttu-id="5bdc9-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span><span class="sxs-lookup"><span data-stu-id="5bdc9-110">See [Data dependent routing](sql-database-elastic-scale-data-dependent-routing.md).</span></span> <span data-ttu-id="5bdc9-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-111">Compare to **[Multi-Shard Query](sql-database-elastic-scale-multishard-querying.md)**.</span></span>

<span data-ttu-id="5bdc9-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-112">**Global shard map**: The map between sharding keys and their respective shards within a **shard set**.</span></span> <span data-ttu-id="5bdc9-113">The global shard map is stored in the **shard map manager**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-113">The global shard map is stored in the **shard map manager**.</span></span> <span data-ttu-id="5bdc9-114">Compare to **local shard map**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-114">Compare to **local shard map**.</span></span>

<span data-ttu-id="5bdc9-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-115">**List shard map**: A shard map in which sharding keys are mapped individually.</span></span> <span data-ttu-id="5bdc9-116">Compare to **Range Shard Map**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-116">Compare to **Range Shard Map**.</span></span>   

<span data-ttu-id="5bdc9-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-117">**Local shard map**: Stored on a shard, the local shard map contains mappings for the shardlets that reside on the shard.</span></span>

<span data-ttu-id="5bdc9-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span><span class="sxs-lookup"><span data-stu-id="5bdc9-118">**Multi-shard query**: The ability to issue a query against multiple shards; results sets are returned using UNION ALL semantics (also known as “fan-out query”).</span></span> <span data-ttu-id="5bdc9-119">Compare to **data dependent routing**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-119">Compare to **data dependent routing**.</span></span>

<span data-ttu-id="5bdc9-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span><span class="sxs-lookup"><span data-stu-id="5bdc9-120">**Multi-tenant** and **Single-tenant**: This shows a single-tenant database and a multi-tenant database:</span></span>

![Single and multi-tenant databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-glossary/multi-single-simple.png)

<span data-ttu-id="5bdc9-122">Here is a representation of **sharded** single and multi-tenant databases.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-122">Here is a representation of **sharded** single and multi-tenant databases.</span></span> 

![Single and multi-tenant databases](https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-glossary/shards-single-multi.png)

<span data-ttu-id="5bdc9-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-124">**Range shard map**: A shard map in which the shard distribution strategy is based on multiple ranges of contiguous values.</span></span> 

<span data-ttu-id="5bdc9-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-125">**Reference tables**: Tables that are not sharded but are replicated across shards.</span></span> <span data-ttu-id="5bdc9-126">For example, zip codes can be stored in a reference table.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-126">For example, zip codes can be stored in a reference table.</span></span> 

<span data-ttu-id="5bdc9-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-127">**Shard**: An Azure SQL database that stores data from a sharded data set.</span></span> 

<span data-ttu-id="5bdc9-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-128">**Shard elasticity**: The ability to perform both **horizontal scaling** and **vertical scaling**.</span></span>

<span data-ttu-id="5bdc9-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-129">**Sharded tables**: Tables that are sharded, i.e., whose data is distributed across shards based on their sharding key values.</span></span> 

<span data-ttu-id="5bdc9-130">**Sharding key**: A column value that determines how data is distributed across shards.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-130">**Sharding key**: A column value that determines how data is distributed across shards.</span></span> <span data-ttu-id="5bdc9-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-131">The value type can be one of the following: **int**, **bigint**, **varbinary**, or **uniqueidentifier**.</span></span> 

<span data-ttu-id="5bdc9-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-132">**Shard set**: The collection of shards that are attributed to the same shard map in the shard map manager.</span></span>  

<span data-ttu-id="5bdc9-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-133">**Shardlet**: All of the data associated with a single value of a sharding key on a shard.</span></span> <span data-ttu-id="5bdc9-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-134">A shardlet is the smallest unit of data movement possible when redistributing sharded tables.</span></span> 

<span data-ttu-id="5bdc9-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-135">**Shard map**: The set of mappings between sharding keys and their respective shards.</span></span>

<span data-ttu-id="5bdc9-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-136">**Shard map manager**: A management object and data store that contains the shard map(s), shard locations, and mappings for one or more shard sets.</span></span>

![Mappings][2]

## <a name="verbs"></a><span data-ttu-id="5bdc9-138">Verbs</span><span class="sxs-lookup"><span data-stu-id="5bdc9-138">Verbs</span></span>
<span data-ttu-id="5bdc9-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-139">**Horizontal scaling**: The act of scaling out (or in) a collection of shards by adding or removing shards to a shard map, as shown below.</span></span>

![Horizontal and vertical scaling][3]

<span data-ttu-id="5bdc9-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-141">**Merge**: The act of moving shardlets from two shards to one shard and updating the shard map accordingly.</span></span>

<span data-ttu-id="5bdc9-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-142">**Shardlet move**: The act of moving a single shardlet to a different shard.</span></span> 

<span data-ttu-id="5bdc9-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-143">**Shard**: The act of horizontally partitioning identically structured data across multiple databases based on a sharding key.</span></span>

<span data-ttu-id="5bdc9-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-144">**Split**: The act of moving several shardlets from one shard to another (typically new) shard.</span></span> <span data-ttu-id="5bdc9-145">A sharding key is provided by the user as the split point.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-145">A sharding key is provided by the user as the split point.</span></span>

<span data-ttu-id="5bdc9-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span><span class="sxs-lookup"><span data-stu-id="5bdc9-146">**Vertical Scaling**: The act of scaling up (or down) the performance level of an individual shard.</span></span> <span data-ttu-id="5bdc9-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span><span class="sxs-lookup"><span data-stu-id="5bdc9-147">For example, changing a shard from Standard to Premium (which results in more computing resources).</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-glossary/glossary.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-glossary/mappings.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/sql-database/media/sql-database-elastic-scale-glossary/h_versus_vert.png






