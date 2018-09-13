---
title: Using user-defined schemas in SQL Data Warehouse | Microsoft Docs
description: Tips for using T-SQL user-defined schemas in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: d46f41e75538fae230219068d3530b7181564ac0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774351"
---
# <a name="using-user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="ab677-103">Using user-defined schemas in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ab677-103">Using user-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="ab677-104">Tips for using T-SQL user-defined schemas in Azure SQL Data Warehouse for developing solutions.</span><span class="sxs-lookup"><span data-stu-id="ab677-104">Tips for using T-SQL user-defined schemas in Azure SQL Data Warehouse for developing solutions.</span></span>

## <a name="schemas-for-application-boundaries"></a><span data-ttu-id="ab677-105">Schemas for application boundaries</span><span class="sxs-lookup"><span data-stu-id="ab677-105">Schemas for application boundaries</span></span>

<span data-ttu-id="ab677-106">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span><span class="sxs-lookup"><span data-stu-id="ab677-106">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="ab677-107">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span><span class="sxs-lookup"><span data-stu-id="ab677-107">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="ab677-108">In this topology each database operates as a workload and security boundary in the architecture.</span><span class="sxs-lookup"><span data-stu-id="ab677-108">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="ab677-109">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span><span class="sxs-lookup"><span data-stu-id="ab677-109">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="ab677-110">Cross database joins are not permitted.</span><span class="sxs-lookup"><span data-stu-id="ab677-110">Cross database joins are not permitted.</span></span> <span data-ttu-id="ab677-111">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span><span class="sxs-lookup"><span data-stu-id="ab677-111">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="ab677-112">SQL Data Warehouse does not support cross database queries of any kind.</span><span class="sxs-lookup"><span data-stu-id="ab677-112">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="ab677-113">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span><span class="sxs-lookup"><span data-stu-id="ab677-113">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="ab677-114">Recommendations</span><span class="sxs-lookup"><span data-stu-id="ab677-114">Recommendations</span></span>
<span data-ttu-id="ab677-115">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span><span class="sxs-lookup"><span data-stu-id="ab677-115">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="ab677-116">Use one SQL Data Warehouse database to run your entire data warehouse workload</span><span class="sxs-lookup"><span data-stu-id="ab677-116">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="ab677-117">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="ab677-117">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="ab677-118">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span><span class="sxs-lookup"><span data-stu-id="ab677-118">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="ab677-119">If user-defined schemas have not been used previously then you have a clean slate.</span><span class="sxs-lookup"><span data-stu-id="ab677-119">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="ab677-120">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="ab677-120">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="ab677-121">If schemas have already been used then you have a few options:</span><span class="sxs-lookup"><span data-stu-id="ab677-121">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="ab677-122">Remove the legacy schema names and start fresh</span><span class="sxs-lookup"><span data-stu-id="ab677-122">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="ab677-123">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span><span class="sxs-lookup"><span data-stu-id="ab677-123">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="ab677-124">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span><span class="sxs-lookup"><span data-stu-id="ab677-124">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="ab677-125">On first inspection option 3 may seem like the most appealing option.</span><span class="sxs-lookup"><span data-stu-id="ab677-125">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="ab677-126">However, the devil is in the detail.</span><span class="sxs-lookup"><span data-stu-id="ab677-126">However, the devil is in the detail.</span></span> <span data-ttu-id="ab677-127">Views are read only in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ab677-127">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="ab677-128">Any data or table modification would need to be performed against the base table.</span><span class="sxs-lookup"><span data-stu-id="ab677-128">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="ab677-129">Option 3 also introduces a layer of views into your system.</span><span class="sxs-lookup"><span data-stu-id="ab677-129">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="ab677-130">You might want to give this some additional thought if you are using views in your architecture already.</span><span class="sxs-lookup"><span data-stu-id="ab677-130">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="ab677-131">Examples:</span><span class="sxs-lookup"><span data-stu-id="ab677-131">Examples:</span></span>
<span data-ttu-id="ab677-132">Implement user-defined schemas based on database names</span><span class="sxs-lookup"><span data-stu-id="ab677-132">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for the data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in the stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in the edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="ab677-133">Retain legacy schema names by pre-pending them to the table name.</span><span class="sxs-lookup"><span data-stu-id="ab677-133">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="ab677-134">Use schemas for the workload boundary.</span><span class="sxs-lookup"><span data-stu-id="ab677-134">Use schemas for the workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines the data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend the old schema name to the table and create in the staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend the old schema name to the table and create in the data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="ab677-135">Retain legacy schema names using views</span><span class="sxs-lookup"><span data-stu-id="ab677-135">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines the staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines the data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines the legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create the base staging tables in the staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create the base data warehouse tables in the data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in the legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="ab677-136">Any change in schema strategy needs a review of the security model for the database.</span><span class="sxs-lookup"><span data-stu-id="ab677-136">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="ab677-137">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span><span class="sxs-lookup"><span data-stu-id="ab677-137">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="ab677-138">If more granular permissions are required then you can use database roles.</span><span class="sxs-lookup"><span data-stu-id="ab677-138">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ab677-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="ab677-139">Next steps</span></span>
<span data-ttu-id="ab677-140">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="ab677-140">For more development tips, see [development overview](sql-data-warehouse-overview-develop.md).</span></span>

