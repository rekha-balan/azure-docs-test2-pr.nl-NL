---
title: Azure SQL Database purchasing models | Microsoft Docs
description: Learn about purchasing model for Azure SQL Database.
services: sql-database
author: CarlRabeler
ms.service: sql-database
ms.custom: DBs & servers
ms.topic: conceptual
ms.date: 08/17/2018
manager: craigg
ms.author: carlrab
ms.openlocfilehash: 5fcdf02fe75905fb3e492671ba44adb65dfd0da7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810196"
---
# <a name="azure-sql-database-purchasing-models-and-resources"></a>Azure SQL Database purchasing models and resources 

Azure SQL Database enables you to easily purchase fully managed PaaS database engine that fits your performance and cost needs. Depending on the deployment model of Azure SQL Database, you can select the purchasing model that fits your needs: 
 - [Logical servers](sql-database-logical-servers.md) in [Azure SQL Database](sql-database-technical-overview.md) offers two purchasing models for compute, storage, and IO resources: a DTU-based purchasing model and a [vCore-based purchasing model](sql-database-service-tiers-vcore.md). 
 - [Managed Instances](sql-database-managed-instance.md) in Azure SQL Database only offer the [vCore-based purchasing model](sql-database-service-tiers-vcore.md).

The following table and chart compare and contrast these two purchasing models.

|**Purchasing model**|**Description**|**Best for**|
|---|---|---|
|DTU-based model|This model is based on a bundled measure of compute, storage, and IO resources. Performance levels are expressed in terms of Database Transaction Units (DTUs) for single databases and elastic Database Transaction Units (eDTUs) for elastic pools. For more on DTUs and eDTUs, see [What are DTUs and eDTUs](sql-database-service-tiers.md#what-are-database-transaction-units-dtus)?|Best for customers who want simple, pre-configured resource options.| 
|vCore-based model|This model allows you to independently choose compute and storage resources. It also allows you to use Azure Hybrid Benefit for SQL Server to gain cost savings.|Best for customers who value flexibility, control, and transparency.|
||||  

![pricing model](./media/sql-database-service-tiers/pricing-model.png)

## <a name="vcore-based-purchasing-model"></a>vCore-based purchasing model 

A virtual core represents the logical CPU offered with an option to choose between generations of hardware and physical characteristics of hardware (for example, number of cores, memory, storage size). The vCore-based purchasing model gives your flexibility, control, transparency of individual resource consumption and a straightforward way to translate on-premises workload requirements to the cloud. This model allows you to choose compute, memory, and storage based upon their workload needs. In the vCore-based purchasing model, customers can choose between [General Purpose](sql-database-high-availability.md#standardgeneral-purpose-availability) and [Business critical](sql-database-high-availability.md#premiumbusiness-critical-availability) service tiers for both [single databases](sql-database-single-database-scale.md), [managed instances](sql-database-managed-instance.md), and [elastic pools](sql-database-elastic-pool.md). 

The vCore-based purchasing model enables you to independently choose compute and storage resources, match on-premises performance, and optimize price. In the vCore-based purchasing model, customers pay for:
- Compute (service tier + number of vCores and amount of memory + generation of hardware)*
- Type and amount of data and log storage 
- Number of IOs** - applicable to [Logical servers](sql-database-logical-servers.md) only
- Backup storage (RA-GRS)** 

\* In the initial public preview, the Gen 4 Logical CPUs are based on Intel E5-2673 v3 (Haswell) 2.4-GHz processors.

\*\* During preview, seven days of backups and IOs are free.

> [!IMPORTANT]
> Compute, IOs, data and log storage are charged per database or elastic pool. Backups storage is charged per each database. For details of Managed Instance charges, refer to [Azure SQL Database Managed Instance](sql-database-managed-instance.md).
> **Region limitations:** The vCore-based purchasing model is not yet available in the following regions: West Europe, France Central, UK South, UK West and Australia Southeast.

If your database or elastic pool consumes more than 300 DTU conversion to vCore may reduce your cost. You can convert using your API of choice or using the Azure portal, with no downtime. However, conversion is not required. If the DTU purchasing model meets your performance and business requirements, you should continue using it. If you decide to convert from the DTU-model to vCore-model, you should select the performance level using the following rule of thumb: each 100 DTU in Standard tier requires at least 1 vCore in General Purpose tier; each 125 DTU in Premium tier requires at least 1 vCore in Business Critical tier.

## <a name="dtu-based-purchasing-model"></a>DTU-based purchasing model

The Database Transaction Unit (DTU) represents a blended measure of CPU, memory, reads, and writes. The DTU-based purchasing model offers a set of preconfigured bundles of compute resources and included storage to drive different levels of application performance. Customers who prefer the simplicity of a preconfigured bundle and fixed payments each month, may find the DTU-based model more suitable for their needs. In the DTU-based purchasing model, customers can choose between **Basic**, **Standard**, and **Premium** service tiers for both [single databases](sql-database-single-database-scale.md) and [elastic pools](sql-database-elastic-pool.md). This purchase model is not available in [managed instances](sql-database-managed-instance.md).

### <a name="what-are-database-transaction-units-dtus"></a>What are Database Transaction Units (DTUs)?
For a single Azure SQL database at a specific performance level within a [service tier](sql-database-single-database-scale.md), Microsoft guarantees a certain level of resources for that database (independent of any other database in the Azure cloud), providing a predictable level of performance. The amount of resources is calculated as a number of Database Transaction Units or DTUs and is a bundled measure of compute, storage, and IO resources. The ratio amongst these resources was originally determined by an [OLTP benchmark workload](sql-database-benchmark-overview.md), designed to be typical of real-world OLTP workloads. When your workload exceeds the amount of any of these resources, your throughput is throttled - resulting in slower performance and timeouts. The resources used by your workload do not impact the resources available to other SQL databases in the Azure cloud, and the resources used by other workloads do not impact the resources available to your SQL database.

![bounding box](./media/sql-database-what-is-a-dtu/bounding-box.png)

DTUs are most useful for understanding the relative amount of resources between Azure SQL Databases at different performance levels and service tiers. For example, doubling the DTUs by increasing the performance level of a database equates to doubling the set of resources available to that database. For example, a Premium P11 database with 1750 DTUs provides 350x more DTU compute power than a Basic database with 5 DTUs.  

To gain deeper insight into the resource (DTU) consumption of your workload, use [Azure SQL Database Query Performance Insight](sql-database-query-performance.md) to:

- Identify the top queries by CPU/Duration/Execution count that can potentially be tuned for improved performance. For example, an IO intensive query might benefit from the use of [in-memory optimization techniques](sql-database-in-memory.md) to make better use of the available memory at a certain service tier and performance level.
- Drill down into the details of a query, view its text and history of resource utilization.
- Access performance tuning recommendations that show actions performed by [SQL Database Advisor](sql-database-advisor.md).

### <a name="what-are-elastic-database-transaction-units-edtus"></a>What are elastic Database Transaction Units (eDTUs)?
Rather than provide a dedicated set of resources (DTUs) that may not always be needed for a SQL Database that is always available, you can place databases into an [elastic pool](sql-database-elastic-pool.md) on a SQL Database server that shares a pool of resources among those databases. The shared resources in an elastic pool are measured by elastic Database Transaction Units or eDTUs. Elastic pools provide a simple cost effective solution to manage the performance goals for multiple databases having widely varying and unpredictable usage patterns. An elastic pool guarantees resources cannot be consumed by one database in the pool, while ensuring each database in the pool always has a minimum amount of necessary resources available. 

![Intro to SQL Database: eDTUs by tier and level](./media/sql-database-what-is-a-dtu/sqldb_elastic_pools.png)

A pool is given a set number of eDTUs for a set price. Within the elastic pool, individual databases are given the flexibility to auto-scale within the configured boundaries. A database under heavier load will consume more eDTUs to meet demand. Databases under lighter loads will consume less eDTUs. Databases with no load will consume no eDTUs. By provisioning resources for the entire pool, rather than per database, management tasks are simplified, providing a predictable budget for the pool.

Additional eDTUs can be added to an existing pool with no database downtime and with no impact on the databases in the pool. Similarly, if extra eDTUs are no longer needed, they can be removed from an existing pool at any point in time. You can add or subtract databases to the pool or limit the amount of eDTUs a database can use under heavy load to reserve eDTUs for other databases. If a database is predictably under-utilizing resources, you can move it out of the pool and configure it as a single database with a predictable amount of required resources.

### <a name="how-can-i-determine-the-number-of-dtus-needed-by-my-workload"></a>How can I determine the number of DTUs needed by my workload?
If you are looking to migrate an existing on-premises or SQL Server virtual machine workload to Azure SQL Database, you can use the [DTU Calculator](http://dtucalculator.azurewebsites.net/) to approximate the number of DTUs needed. For an existing Azure SQL Database workload, you can use [SQL Database Query Performance Insight](sql-database-query-performance.md) to understand your database resource consumption (DTUs) to gain deeper insight for optimizing your workload. You can also use the [sys.dm_db_ resource_stats](https://msdn.microsoft.com/library/dn800981.aspx) DMV to view resource consumption for the last hour. Alternatively, the catalog view [sys.resource_stats](http://msdn.microsoft.com/library/dn269979.aspx) displays resource consumption for the last 14 days, but at a lower fidelity of five-minute averages.

### <a name="how-do-i-know-if-i-could-benefit-from-an-elastic-pool-of-resources"></a>How do I know if I could benefit from an elastic pool of resources?
Pools are suited for a large number of databases with specific utilization patterns. For a given database, this pattern is characterized by a low utilization average with relatively infrequent utilization spikes. SQL Database automatically evaluates the historical resource usage of databases in an existing SQL Database server and recommends the appropriate pool configuration in the Azure portal. For more information, see [when should an elastic pool be used?](sql-database-elastic-pool.md)


## <a name="next-steps"></a>Next steps

- For vCore-based purchasing model, see [vCore-based purchasing model](sql-database-service-tiers-vcore.md)
- For the DTU-based purchasing model, see [DTU-based purchasing model](sql-database-service-tiers-dtu.md).
