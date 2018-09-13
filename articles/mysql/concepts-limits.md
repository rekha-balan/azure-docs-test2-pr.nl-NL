---
title: Limitations in Azure Database for MySQL
description: This article describes limitations in Azure Database for MySQL, such as number of connection and storage engine options.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 06/30/2018
ms.openlocfilehash: 1fd5905b8ea3f87fe6cfc2a830b73b8120a717dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871588"
---
# <a name="limitations-in-azure-database-for-mysql"></a>Limitations in Azure Database for MySQL
The following sections describe capacity, storage engine support, privilege support, data manipulation statement support, and functional limits in the database service. Also see [general limitations](https://dev.mysql.com/doc/mysql-reslimits-excerpt/5.6/en/limits.html) applicable to the MySQL database engine.

## <a name="maximum-connections"></a>Maximum connections
The maximum number of connections per pricing tier and vCores are as follows: 

|**Pricing Tier**|**vCore(s)**| **Max Connections**|
|---|---|---|
|Basic| 1| 50|
|Basic| 2| 100|
|General Purpose| 2| 300|
|General Purpose| 4| 625|
|General Purpose| 8| 1250|
|General Purpose| 16| 2500|
|General Purpose| 32| 5000|
|Memory Optimized| 2| 600|
|Memory Optimized| 4| 1250|
|Memory Optimized| 8| 2500|
|Memory Optimized| 16| 5000|

When connections exceed the limit, you may receive the following error:
> ERROR 1040 (08004): Too many connections

## <a name="storage-engine-support"></a>Storage engine support

### <a name="supported"></a>Supported
- [InnoDB](https://dev.mysql.com/doc/refman/5.7/en/innodb-introduction.html)
- [MEMORY](https://dev.mysql.com/doc/refman/5.7/en/memory-storage-engine.html)

### <a name="unsupported"></a>Unsupported
- [MyISAM](https://dev.mysql.com/doc/refman/5.7/en/myisam-storage-engine.html)
- [BLACKHOLE](https://dev.mysql.com/doc/refman/5.7/en/blackhole-storage-engine.html)
- [ARCHIVE](https://dev.mysql.com/doc/refman/5.7/en/archive-storage-engine.html)
- [FEDERATED](https://dev.mysql.com/doc/refman/5.7/en/federated-storage-engine.html)

## <a name="privilege-support"></a>Privilege support

### <a name="unsupported"></a>Unsupported
- DBA role: Many server parameters and settings can inadvertently degrade server performance or negate ACID properties of the DBMS. As such, to maintain the service integrity and SLA at a product level, this service does not expose the DBA role. The default user account, which is constructed when a new database instance is created, allows that user to perform most of DDL and DML statements in the managed database instance. 
- SUPER privilege: Similarly [SUPER privilege](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html#priv_super) is also restricted.

## <a name="data-manipulation-statement-support"></a>Data manipulation statement support

### <a name="supported"></a>Supported
- `LOAD DATA INFILE` is supported, but the `[LOCAL]` parameter must be specified and directed to a UNC path (Azure storage mounted through SMB).

### <a name="unsupported"></a>Unsupported
- `SELECT ... INTO OUTFILE`

## <a name="functional-limitations"></a>Functional limitations

### <a name="scale-operations"></a>Scale operations
- Dynamic scaling to and from the Basic pricing tiers is currently not supported.
- Decreasing server storage size is not supported.

### <a name="server-version-upgrades"></a>Server version upgrades
- Automated migration between major database engine versions is currently not supported.

### <a name="point-in-time-restore"></a>Point-in-time-restore
- When using the PITR feature, the new server is created with the same configurations as the server it is based on.
- Restoring a deleted server is not supported.

### <a name="vnet-service-endpoints"></a>VNet service endpoints
- Support for VNet service endpoints is only for General Purpose and Memory Optimized servers.

### <a name="subscription-management"></a>Subscription management
- Dynamically moving pre-created servers across subscription and resource group is currently not supported.

## <a name="current-known-issues"></a>Current known issues
- MySQL server instance displays the wrong server version after connection is established. To get the correct server instance engine version, use the `select version();` command.

## <a name="next-steps"></a>Next steps
- [What’s available in each service tier](concepts-pricing-tiers.md)
- [Supported MySQL database versions](concepts-supported-versions.md)
