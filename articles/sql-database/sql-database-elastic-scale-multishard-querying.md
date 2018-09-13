---
title: Query sharded Azure SQL databases | Microsoft Docs
description: Run queries across shards using the elastic database client library.
services: sql-database
documentationcenter: ''
manager: jhubbard
author: torsteng
editor: ''
ms.assetid: a4379c15-f213-4026-ab6f-a450ee9d5758
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2016
ms.author: torsteng
ms.openlocfilehash: aa54ec3d982ea4422422bd4e520d2211aad57159
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550427"
---
# <a name="multi-shard-querying"></a>Multi-shard querying
## <a name="overview"></a>Overview
With the [Elastic Database tools](sql-database-elastic-scale-introduction.md), you can create sharded database solutions. **Multi-shard querying** is used for tasks such as data collection/reporting that require running a query that stretches across several shards. (Contrast this to [data-dependent routing](sql-database-elastic-scale-data-dependent-routing.md), which performs all work on a single shard.) 

1. Get a [**RangeShardMap**](https://msdn.microsoft.com/library/azure/dn807318.aspx) or [**ListShardMap**](https://msdn.microsoft.com/library/azure/dn807370.aspx) using the [**TryGetRangeShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetrangeshardmap.aspx), the [**TryGetListShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.trygetlistshardmap.aspx), or the [**GetShardMap**](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.getshardmap.aspx) method. See [**Constructing a ShardMapManager**](sql-database-elastic-scale-shard-map-management.md#constructing-a-shardmapmanager) and [**Get a RangeShardMap or ListShardMap**](sql-database-elastic-scale-shard-map-management.md#get-a-rangeshardmap-or-listshardmap).
2. Create a **[MultiShardConnection](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardconnection.aspx)** object.
3. Create a **[MultiShardCommand](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.aspx)**. 
4. Set the **[CommandText property](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.commandtext.aspx#P:Microsoft.Azure.SqlDatabase.ElasticScale.Query.MultiShardCommand.CommandText)** to a T-SQL command.
5. Execute the command by calling the **[ExecuteReader method](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardcommand.executereader.aspx)**.
6. View the results using the **[MultiShardDataReader class](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multisharddatareader.aspx)**. 

## <a name="example"></a>Example
The following code illustrates the usage of multi-shard querying using a given **ShardMap** named *myShardMap*. 

    using (MultiShardConnection conn = new MultiShardConnection( 
                                        myShardMap.GetShards(), 
                                        myShardConnectionString) 
          ) 
    { 
    using (MultiShardCommand cmd = conn.CreateCommand())
           { 
            cmd.CommandText = "SELECT c1, c2, c3 FROM ShardedTable"; 
            cmd.CommandType = CommandType.Text; 
            cmd.ExecutionOptions = MultiShardExecutionOptions.IncludeShardNameColumn; 
            cmd.ExecutionPolicy = MultiShardExecutionPolicy.PartialResults; 

            using (MultiShardDataReader sdr = cmd.ExecuteReader()) 
                { 
                    while (sdr.Read())
                        { 
                            var c1Field = sdr.GetString(0); 
                            var c2Field = sdr.GetFieldValue<int>(1); 
                            var c3Field = sdr.GetFieldValue<Int64>(2);
                        } 
                 } 
           } 
    } 


A key difference is the construction of multi-shard connections. Where **SqlConnection** operates on a single database, the **MultiShardConnection** takes a ***collection of shards*** as its input. Populate the collection of shards from a shard map. The query is then executed on the collection of shards using **UNION ALL** semantics to assemble a single overall result. Optionally, the name of the shard where the row originates from can be added to the output using the **ExecutionOptions** property on command. 

Note the call to **myShardMap.GetShards()**. This method retrieves all shards from the shard map and provides an easy way to run a query across all relevant databases. The collection of shards for a multi-shard query can be refined further by performing a LINQ query over the collection returned from the call to **myShardMap.GetShards()**. In combination with the partial results policy, the current capability in multi-shard querying has been designed to work well for tens up to hundreds of shards.

A limitation with multi-shard querying is currently the lack of validation for shards and shardlets that are queried. While data-dependent routing verifies that a given shard is part of the shard map at the time of querying, multi-shard queries do not perform this check. This can lead to multi-shard queries running on databases that have  been removed from the shard map.

## <a name="multi-shard-queries-and-split-merge-operations"></a>Multi-shard queries and split-merge operations
Multi-shard queries do not verify whether shardlets on the queried database are participating in ongoing split-merge operations. (See [Scaling using the Elastic Database split-merge tool](sql-database-elastic-scale-overview-split-and-merge.md).) This can lead to inconsistencies where rows from the same shardlet show for multiple databases in the same multi-shard query. Be aware of these limitations and consider draining ongoing split-merge operations and changes to the shard map while performing multi-shard queries.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

## <a name="see-also"></a>See also
**[System.Data.SqlClient](http://msdn.microsoft.com/library/System.Data.SqlClient.aspx)** classes and methods.

Manage shards using the [Elastic Database client library](sql-database-elastic-database-client-library.md). Includes a  namespace called [Microsoft.Azure.SqlDatabase.ElasticScale.Query](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.aspx) that provides the ability to query multiple shards using a single query and result. It provides a querying abstraction over a collection of shards. It also provides alternative execution policies, in particular partial results, to deal with failures when querying over many shards.  
