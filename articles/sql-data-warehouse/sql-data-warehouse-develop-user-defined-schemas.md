---
title: User-defined schemas in SQL Data Warehouse | Microsoft Docs
description: Tips for using Transact-SQL schemas in Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: dfb58956ad6637cf0f50b4c052ab98fb7c26139d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550957"
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="05c36-103">User-defined schemas in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="05c36-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="05c36-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span><span class="sxs-lookup"><span data-stu-id="05c36-104">Traditional data warehouses often use separate databases to create application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="05c36-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span><span class="sxs-lookup"><span data-stu-id="05c36-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="05c36-106">In this topology each database operates as a workload and security boundary in the architecture.</span><span class="sxs-lookup"><span data-stu-id="05c36-106">In this topology each database operates as a workload and security boundary in the architecture.</span></span>

<span data-ttu-id="05c36-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span><span class="sxs-lookup"><span data-stu-id="05c36-107">By contrast, SQL Data Warehouse runs the entire data warehouse workload within one database.</span></span> <span data-ttu-id="05c36-108">Cross database joins are not permitted.</span><span class="sxs-lookup"><span data-stu-id="05c36-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="05c36-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span><span class="sxs-lookup"><span data-stu-id="05c36-109">Therefore SQL Data Warehouse expects all tables used by the warehouse to be stored within the one database.</span></span>

> [!NOTE]
> <span data-ttu-id="05c36-110">SQL Data Warehouse does not support cross database queries of any kind.</span><span class="sxs-lookup"><span data-stu-id="05c36-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="05c36-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span><span class="sxs-lookup"><span data-stu-id="05c36-111">Consequently, data warehouse implementations that leverage this pattern will need to be revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="05c36-112">Recommendations</span><span class="sxs-lookup"><span data-stu-id="05c36-112">Recommendations</span></span>
<span data-ttu-id="05c36-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span><span class="sxs-lookup"><span data-stu-id="05c36-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="05c36-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span><span class="sxs-lookup"><span data-stu-id="05c36-114">Use one SQL Data Warehouse database to run your entire data warehouse workload</span></span>
2. <span data-ttu-id="05c36-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span><span class="sxs-lookup"><span data-stu-id="05c36-115">Consolidate your existing data warehouse environment to use one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="05c36-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span><span class="sxs-lookup"><span data-stu-id="05c36-116">Leverage **user-defined schemas** to provide the boundary previously implemented using databases.</span></span>

<span data-ttu-id="05c36-117">If user-defined schemas have not been used previously then you have a clean slate.</span><span class="sxs-lookup"><span data-stu-id="05c36-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="05c36-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span><span class="sxs-lookup"><span data-stu-id="05c36-118">Simply use the old database name as the basis for your user-defined schemas in the SQL Data Warehouse database.</span></span>

<span data-ttu-id="05c36-119">If schemas have already been used then you have a few options:</span><span class="sxs-lookup"><span data-stu-id="05c36-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="05c36-120">Remove the legacy schema names and start fresh</span><span class="sxs-lookup"><span data-stu-id="05c36-120">Remove the legacy schema names and start fresh</span></span>
2. <span data-ttu-id="05c36-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span><span class="sxs-lookup"><span data-stu-id="05c36-121">Retain the legacy schema names by pre-pending the legacy schema name to the table name</span></span>
3. <span data-ttu-id="05c36-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span><span class="sxs-lookup"><span data-stu-id="05c36-122">Retain the legacy schema names by implementing views over the table in an extra schema to re-create the old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="05c36-123">On first inspection option 3 may seem like the most appealing option.</span><span class="sxs-lookup"><span data-stu-id="05c36-123">On first inspection option 3 may seem like the most appealing option.</span></span> <span data-ttu-id="05c36-124">However, the devil is in the detail.</span><span class="sxs-lookup"><span data-stu-id="05c36-124">However, the devil is in the detail.</span></span> <span data-ttu-id="05c36-125">Views are read only in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="05c36-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="05c36-126">Any data or table modification would need to be performed against the base table.</span><span class="sxs-lookup"><span data-stu-id="05c36-126">Any data or table modification would need to be performed against the base table.</span></span> <span data-ttu-id="05c36-127">Option 3 also introduces a layer of views into your system.</span><span class="sxs-lookup"><span data-stu-id="05c36-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="05c36-128">You might want to give this some additional thought if you are using views in your architecture already.</span><span class="sxs-lookup"><span data-stu-id="05c36-128">You might want to give this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="05c36-129">Examples:</span><span class="sxs-lookup"><span data-stu-id="05c36-129">Examples:</span></span>
<span data-ttu-id="05c36-130">Implement user-defined schemas based on database names</span><span class="sxs-lookup"><span data-stu-id="05c36-130">Implement user-defined schemas based on database names</span></span>

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

<span data-ttu-id="05c36-131">Retain legacy schema names by pre-pending them to the table name.</span><span class="sxs-lookup"><span data-stu-id="05c36-131">Retain legacy schema names by pre-pending them to the table name.</span></span> <span data-ttu-id="05c36-132">Use schemas for the workload boundary.</span><span class="sxs-lookup"><span data-stu-id="05c36-132">Use schemas for the workload boundary.</span></span>

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

<span data-ttu-id="05c36-133">Retain legacy schema names using views</span><span class="sxs-lookup"><span data-stu-id="05c36-133">Retain legacy schema names using views</span></span>

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
> <span data-ttu-id="05c36-134">Any change in schema strategy needs a review of the security model for the database.</span><span class="sxs-lookup"><span data-stu-id="05c36-134">Any change in schema strategy needs a review of the security model for the database.</span></span> <span data-ttu-id="05c36-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span><span class="sxs-lookup"><span data-stu-id="05c36-135">In many cases you might be able to simplify the security model by assigning permissions at the schema level.</span></span> <span data-ttu-id="05c36-136">If more granular permissions are required then you can use database roles.</span><span class="sxs-lookup"><span data-stu-id="05c36-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="05c36-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="05c36-137">Next steps</span></span>
<span data-ttu-id="05c36-138">For more development tips, see [development overview][development overview].</span><span class="sxs-lookup"><span data-stu-id="05c36-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
