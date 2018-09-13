---
title: Migrate your schema to SQL Data Warehouse | Microsoft Docs
description: Tips for migrating your schema to Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: ''
ms.assetid: 538b60c9-a07f-49bf-9ea3-1082ed6699fb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 0630f43642a0be98c470032d32b74ca14ee144e5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555545"
---
# <a name="migrate-your-schema-to-sql-data-warehouse"></a><span data-ttu-id="5c391-103">Migrate your schema to SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="5c391-103">Migrate your schema to SQL Data Warehouse</span></span>
<span data-ttu-id="5c391-104">The following summaries help you understand the differences between SQL Server and SQL Data Warehouse to help you migrate your database.</span><span class="sxs-lookup"><span data-stu-id="5c391-104">The following summaries help you understand the differences between SQL Server and SQL Data Warehouse to help you migrate your database.</span></span>

## <a name="table-migration"></a><span data-ttu-id="5c391-105">Table Migration</span><span class="sxs-lookup"><span data-stu-id="5c391-105">Table Migration</span></span>
<span data-ttu-id="5c391-106">When migrating your tables, you'll want to become familiar with the table features of SQL Data Warehouse tables.</span><span class="sxs-lookup"><span data-stu-id="5c391-106">When migrating your tables, you'll want to become familiar with the table features of SQL Data Warehouse tables.</span></span>  <span data-ttu-id="5c391-107">The [table overview][table overview] is a great place to start.</span><span class="sxs-lookup"><span data-stu-id="5c391-107">The [table overview][table overview] is a great place to start.</span></span>  <span data-ttu-id="5c391-108">This article introduces you to the most important considerations when creating a table such as table statistics, distribution, partitioning, and indexing.</span><span class="sxs-lookup"><span data-stu-id="5c391-108">This article introduces you to the most important considerations when creating a table such as table statistics, distribution, partitioning, and indexing.</span></span>  <span data-ttu-id="5c391-109">It also covers some [unsupported table features][unsupported table features] and workarounds.</span><span class="sxs-lookup"><span data-stu-id="5c391-109">It also covers some [unsupported table features][unsupported table features] and workarounds.</span></span>

<span data-ttu-id="5c391-110">SQL Data Warehouse supports the common business data types.</span><span class="sxs-lookup"><span data-stu-id="5c391-110">SQL Data Warehouse supports the common business data types.</span></span>  <span data-ttu-id="5c391-111">See the [data types][data types] article for a list of supported and [unsupported data types][unsupported data types].</span><span class="sxs-lookup"><span data-stu-id="5c391-111">See the [data types][data types] article for a list of supported and [unsupported data types][unsupported data types].</span></span>  <span data-ttu-id="5c391-112">The [data types][data types] article also contains a query to identify [unsupported data types][unsupported data types].</span><span class="sxs-lookup"><span data-stu-id="5c391-112">The [data types][data types] article also contains a query to identify [unsupported data types][unsupported data types].</span></span>  <span data-ttu-id="5c391-113">When converting your data types, be sure to look at the [data type best practices][data type best practices].</span><span class="sxs-lookup"><span data-stu-id="5c391-113">When converting your data types, be sure to look at the [data type best practices][data type best practices].</span></span>

## <a name="next-steps"></a><span data-ttu-id="5c391-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="5c391-114">Next steps</span></span>
<span data-ttu-id="5c391-115">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span><span class="sxs-lookup"><span data-stu-id="5c391-115">Once you have successfully migrated your database schema to SQL Data Warehouse, proceed to one of the following articles:</span></span>

* <span data-ttu-id="5c391-116">[Migrate your data][Migrate your data]</span><span class="sxs-lookup"><span data-stu-id="5c391-116">[Migrate your data][Migrate your data]</span></span>
* <span data-ttu-id="5c391-117">[Migrate your code][Migrate your code]</span><span class="sxs-lookup"><span data-stu-id="5c391-117">[Migrate your code][Migrate your code]</span></span>

<span data-ttu-id="5c391-118">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span><span class="sxs-lookup"><span data-stu-id="5c391-118">For more about SQL Data Warehouse best practices, see the [best practices][best practices] article.</span></span>

<!--Image references-->

<!--Article references-->
[Migrate your code]: ./sql-data-warehouse-migrate-code.md
[Migrate your data]: ./sql-data-warehouse-migrate-data.md
[best practices]: ./sql-data-warehouse-best-practices.md
[table overview]: ./sql-data-warehouse-tables-overview.md
[unsupported table features]: ./sql-data-warehouse-tables-overview.md#unsupported-table-features
[data types]: ./sql-data-warehouse-tables-data-types.md
[unsupported data types]: ./sql-data-warehouse-tables-data-types.md#unsupported-data-types
[data type best practices]: ./sql-data-warehouse-tables-data-types.md#data-type-best-practices

<!--MSDN references-->


<!--Other Web references-->
