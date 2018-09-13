---
title: Azure SQL Elastic Scale FAQ | Microsoft Docs
description: Frequently Asked Questions about Azure SQL Database Elastic Scale.
services: sql-database
documentationcenter: ''
manager: jhubbard
author: ddove
editor: ''
ms.assetid: e60dde9c-bb7b-4f2f-b52c-bdb506d49fcb
ms.service: sql-database
ms.custom: multiple databases
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: c86b9c42becc7906d431cd2cec797daab38346d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548804"
---
# <a name="elastic-database-tools-faq"></a>Elastic database tools FAQ
#### <a name="if-i-have-a-single-tenant-per-shard-and-no-sharding-key-how-do-i-populate-the-sharding-key-for-the-schema-info"></a>If I have a single-tenant per shard and no sharding key, how do I populate the sharding key for the schema info?
The schema info object is only used to split merge scenarios. If an application is inherently single-tenant, then it does not require the Split Merge tool and thus there is no need to populate the schema info object.

#### <a name="ive-provisioned-a-database-and-i-already-have-a-shard-map-manager-how-do-i-register-this-new-database-as-a-shard"></a>I’ve provisioned a database and I already have a Shard Map Manager, how do I register this new database as a shard?
Please see **[Adding a shard to an application using the elastic database client library](sql-database-elastic-scale-add-a-shard.md)**. 

#### <a name="how-much-do-elastic-database-tools-cost"></a>How much do elastic database tools cost?
Using the elastic database client library does not incur any costs. Costs accrue only for the Azure SQL databases that you use for shards and the Shard Map Manager, as well as the web/worker roles you provision for the Split Merge tool.

#### <a name="why-are-my-credentials-not-working-when-i-add-a-shard-from-a-different-server"></a>Why are my credentials not working when I add a shard from a different server?
Do not use credentials in the form of “User ID=username@servername”, instead simply use “User ID = username”.  Also, be sure that the “username” login has permissions on the shard.

#### <a name="do-i-need-to-create-a-shard-map-manager-and-populate-shards-every-time-i-start-my-applications"></a>Do I need to create a Shard Map Manager and populate shards every time I start my applications?
No—the creation of the Shard Map Manager (for example, **[ShardMapManagerFactory.CreateSqlShardMapManager](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.createsqlshardmapmanager.aspx)**) is a one-time operation.  Your application should use the call **[ShardMapManagerFactory.TryGetSqlShardMapManager()](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager.aspx)** at application start-up time.  There should only one such call per application domain.

#### <a name="i-have-questions-about-using-elastic-database-tools-how-do-i-get-them-answered"></a>I have questions about using elastic database tools, how do I get them answered?
Please reach out to us on the [Azure SQL Database forum](https://social.msdn.microsoft.com/forums/azure/home?forum=ssdsgetstarted).

#### <a name="when-i-get-a-database-connection-using-a-sharding-key-i-can-still-query-data-for-other-sharding-keys-on-the-same-shard--is-this-by-design"></a>When I get a database connection using a sharding key, I can still query data for other sharding keys on the same shard.  Is this by design?
The Elastic Scale APIs give you a connection to the correct database for your sharding key, but do not provide sharding key filtering.  Add **WHERE** clauses to your query to restrict the scope to the provided sharding key, if necessary.

#### <a name="can-i-use-a-different-azure-database-edition-for-each-shard-in-my-shard-set"></a>Can I use a different Azure Database edition for each shard in my shard set?
Yes, a shard is an individual database, and thus one shard could be a Premium edition while another be a Standard edition. Further, the edition of a shard can scale up or down multiple times during the lifetime of the shard.

#### <a name="does-the-split-merge-tool-provision-or-delete-a-database-during-a-split-or-merge-operation"></a>Does the Split Merge tool provision (or delete) a database during a split or merge operation?
No. For **split** operations, the target database must exist with the appropriate schema and be registered with the Shard Map Manager.  For **merge** operations, you must delete the shard from the shard map manager and then delete the database.

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

