---
title: Monitor XTP in-memory storage | Microsoft Docs
description: Estimate and monitor XTP in-memory storage use, capacity; resolve capacity error 41823
services: sql-database
documentationcenter: ''
author: jodebrui
manager: jhubbard
editor: ''
ms.assetid: b617308e-692c-4938-8fa2-070034a3ecef
ms.service: sql-database
ms.custom: monitor and tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/19/2016
ms.author: jodebrui
ms.openlocfilehash: f53fa3763edb1d9164278d1e3c418e200d7ada89
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555077"
---
# <a name="monitor-in-memory-oltp-storage"></a>Monitor In-Memory OLTP Storage
When using [In-Memory OLTP](sql-database-in-memory.md), data in memory-optimized tables and table variables resides in In-Memory OLTP storage. Each Premium service tier has a maximum In-Memory OLTP storage size, which is documented in the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels). Once this limit is exceeded, insert and update operations may start failing (with error 41823). At that point you will need to either delete data to reclaim memory, or upgrade the performance tier of your database.

## <a name="determine-whether-data-will-fit-within-the-in-memory-storage-cap"></a>Determine whether data will fit within the in-memory storage cap
Determine the storage cap: consult the [SQL Database Service Tiers article](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) for the storage caps of the different Premium service tiers.

Estimating memory requirements for a memory-optimized table works the same way for SQL Server as it does in Azure SQL Database. Take a few minutes to review that topic on [MSDN](https://msdn.microsoft.com/library/dn282389.aspx).

Note that the table and table variable rows, as well as indexes, count toward the max user data size. In addition, ALTER TABLE needs enough room to create a new version of the entire table and its indexes.

## <a name="monitoring-and-alerting"></a>Monitoring and alerting
You can monitor in-memory storage use as a percentage of the [storage cap for your performance tier](sql-database-service-tiers.md#single-database-service-tiers-and-performance-levels) in the Azure [portal](https://portal.azure.com/): 

* On the Database blade, locate the Resource utilization box and click on Edit.
* Then select the metric `In-Memory OLTP Storage percentage`.
* To add an alert, click on the Resource Utilization box to open the Metric blade, then click on Add alert.

Or use the following query to show the in-memory storage utilization:

    SELECT xtp_storage_percent FROM sys.dm_db_resource_stats


## <a name="correct-out-of-memory-situations---error-41823"></a>Correct out-of-memory situations - Error 41823
Running out-of-memory results in INSERT, UPDATE, and CREATE operations failing with error message 41823.

Error message 41823 indicates that the memory-optimized tables and table variables have exceeded the maximum size.

To resolve this error, either:

* Delete data from the memory-optimized tables, potentially offloading the data to traditional, disk-based tables; or,
* Upgrade the service tier to one with enough in-memory storage for the data you need to keep in memory-optimized tables.

## <a name="next-steps"></a>Next steps
For monitoring guidance, see [Monitoring Azure SQL Database using dynamic management views](sql-database-monitoring-with-dmvs.md).
