---
title: Replicate data into Azure Database for MySQL.
description: This article describes data-in replication for Azure Database for MySQL.
services: mysql
author: ajlam
ms.author: andrela
manager: kfile
editor: jasonwhowell
ms.service: mysql
ms.topic: article
ms.date: 08/31/2018
ms.openlocfilehash: 6135e4a0182f3af7db54eab974e4c307402185ab
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856602"
---
# <a name="replicate-data-into-azure-database-for-mysql"></a>Replicate data into Azure Database for MySQL

Data-in Replication allows you to synchronize data from a MySQL server running on-premises, in virtual machines, or database services hosted by other cloud providers into the Azure Database for MySQL service. Data-in Replication is based on the binary log (binlog) file position-based replication native to MySQL. To learn more about binlog replication, see the [MySQL binlog replication overview](https://dev.mysql.com/doc/refman/5.7/en/binlog-replication-configuration-overview.html). 

## <a name="when-to-use-data-in-replication"></a>When to use Data-in Replication
The main scenarios to consider using Data-in Replication are:

- **Hybrid Data Synchronization:** With Data-in Replication, you can keep data synchronized between your on-premises servers and Azure Database for MySQL. This synchronization is useful for creating hybrid applications. This method is appealing when you have an existing local database server, but want to move the data to a region closer to end users.
- **Multi-Cloud Synchronization:** For complex cloud solutions, use Data-in Replication to synchronize data between Azure Database for MySQL and different cloud providers, including virtual machines and database services hosted in those clouds.

## <a name="limitations-and-considerations"></a>Limitations and considerations

### <a name="data-not-replicated"></a>Data not replicated
The [*mysql system database*](https://dev.mysql.com/doc/refman/5.7/en/system-database.html) on the master server is not replicated. Changes to accounts and permissions on the master server are not replicated. If you create an account on the master server and this account needs to access the replica server, then manually create the same account on the replica server side. To understand what tables are contained in the system database, see the [MySQL manual](https://dev.mysql.com/doc/refman/5.7/en/system-database.html).

### <a name="requirements"></a>Requirements
- The master server version must be at least MySQL version 5.6. 
- The master and replica server versions must be the same. For example, both must be MySQL version 5.6 or both must be MySQL version 5.7.
- Each table must have a primary key.
- Master server should use the MySQL InnoDB engine.
- User must have permissions to configure binary logging and create new users on the master server.

### <a name="other"></a>Other
- Data-in replication is only supported in General Purpose and Memory Optimized pricing tiers
- Global transaction identifiers (GTID) are not supported.

## <a name="next-steps"></a>Next steps
- Learn how to [set up data-in replication](howto-data-in-replication.md)
