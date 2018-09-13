---
title: What is Azure SQL Data Warehouse? | Microsoft Docs
description: Enterprise-class distributed database capable of processing petabyte volumes of relational and non-relational data. It is the industry's first cloud data warehouse with grow, shrink, and pause in seconds.
services: sql-data-warehouse
author: igorstanko
manager: craigg
ms.service: sql-data-warehouse
ms.topic: overview
ms.component: design
ms.date: 04/17/2018
ms.author: igorstan
ms.reviewer: igorstan
ms.openlocfilehash: 7ba1cb75b7e7c5a93438ea4f17bb563477837099
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776522"
---
# <a name="what-is-azure-sql-data-warehouse"></a><span data-ttu-id="b29d0-105">What is Azure SQL Data Warehouse?</span><span class="sxs-lookup"><span data-stu-id="b29d0-105">What is Azure SQL Data Warehouse?</span></span>

<span data-ttu-id="b29d0-106">SQL Data Warehouse is a cloud-based Enterprise Data Warehouse (EDW) that leverages Massively Parallel Processing (MPP) to quickly run complex queries across petabytes of data.</span><span class="sxs-lookup"><span data-stu-id="b29d0-106">SQL Data Warehouse is a cloud-based Enterprise Data Warehouse (EDW) that leverages Massively Parallel Processing (MPP) to quickly run complex queries across petabytes of data.</span></span> <span data-ttu-id="b29d0-107">Use SQL Data Warehouse as a key component of a big data solution.</span><span class="sxs-lookup"><span data-stu-id="b29d0-107">Use SQL Data Warehouse as a key component of a big data solution.</span></span> <span data-ttu-id="b29d0-108">Import big data into SQL Data Warehouse with simple PolyBase T-SQL queries, and then use the power of MPP to run high-performance analytics.</span><span class="sxs-lookup"><span data-stu-id="b29d0-108">Import big data into SQL Data Warehouse with simple PolyBase T-SQL queries, and then use the power of MPP to run high-performance analytics.</span></span> <span data-ttu-id="b29d0-109">As you integrate and analyze, the data warehouse will become the single version of truth your business can count on for insights.</span><span class="sxs-lookup"><span data-stu-id="b29d0-109">As you integrate and analyze, the data warehouse will become the single version of truth your business can count on for insights.</span></span>  


## <a name="key-component-of-big-data-solution"></a><span data-ttu-id="b29d0-110">Key component of big data solution</span><span class="sxs-lookup"><span data-stu-id="b29d0-110">Key component of big data solution</span></span>
<span data-ttu-id="b29d0-111">SQL Data Warehouse is a key component of an end-to-end big data solution in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="b29d0-111">SQL Data Warehouse is a key component of an end-to-end big data solution in the Cloud.</span></span>

![Data warehouse solution](media/sql-data-warehouse-overview-what-is/data-warehouse-solution.png) 

<span data-ttu-id="b29d0-113">In a cloud data solution, data is ingested into big data stores from a variety of sources.</span><span class="sxs-lookup"><span data-stu-id="b29d0-113">In a cloud data solution, data is ingested into big data stores from a variety of sources.</span></span> <span data-ttu-id="b29d0-114">Once in a big data store, Hadoop, Spark, and machine learning algorithms prepare and train the data.</span><span class="sxs-lookup"><span data-stu-id="b29d0-114">Once in a big data store, Hadoop, Spark, and machine learning algorithms prepare and train the data.</span></span> <span data-ttu-id="b29d0-115">When the data is ready for complex analysis, SQL Data Warehouse uses PolyBase to query the big data stores.</span><span class="sxs-lookup"><span data-stu-id="b29d0-115">When the data is ready for complex analysis, SQL Data Warehouse uses PolyBase to query the big data stores.</span></span> <span data-ttu-id="b29d0-116">PolyBase uses standard T-SQL queries to bring the data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b29d0-116">PolyBase uses standard T-SQL queries to bring the data into SQL Data Warehouse.</span></span>
 
<span data-ttu-id="b29d0-117">SQL Data Warehouse stores data into relational tables with columnar storage.</span><span class="sxs-lookup"><span data-stu-id="b29d0-117">SQL Data Warehouse stores data into relational tables with columnar storage.</span></span> <span data-ttu-id="b29d0-118">This format significantly reduces the data storage costs, and improves query performance.</span><span class="sxs-lookup"><span data-stu-id="b29d0-118">This format significantly reduces the data storage costs, and improves query performance.</span></span> <span data-ttu-id="b29d0-119">Once data is stored in SQL Data Warehouse, you can run analytics at massive scale.</span><span class="sxs-lookup"><span data-stu-id="b29d0-119">Once data is stored in SQL Data Warehouse, you can run analytics at massive scale.</span></span> <span data-ttu-id="b29d0-120">Compared to traditional database systems, analysis queries finish in seconds instead of minutes, or hours instead of days.</span><span class="sxs-lookup"><span data-stu-id="b29d0-120">Compared to traditional database systems, analysis queries finish in seconds instead of minutes, or hours instead of days.</span></span> 

<span data-ttu-id="b29d0-121">The analysis results can go to worldwide reporting databases or applications.</span><span class="sxs-lookup"><span data-stu-id="b29d0-121">The analysis results can go to worldwide reporting databases or applications.</span></span> <span data-ttu-id="b29d0-122">Business analysts can then gain insights to make well-informed business decisions.</span><span class="sxs-lookup"><span data-stu-id="b29d0-122">Business analysts can then gain insights to make well-informed business decisions.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b29d0-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="b29d0-123">Next steps</span></span>
<span data-ttu-id="b29d0-124">Now that you know a bit about SQL Data Warehouse, learn how to quickly [create a SQL Data Warehouse][create a SQL Data Warehouse] and [load sample data][load sample data].</span><span class="sxs-lookup"><span data-stu-id="b29d0-124">Now that you know a bit about SQL Data Warehouse, learn how to quickly [create a SQL Data Warehouse][create a SQL Data Warehouse] and [load sample data][load sample data].</span></span> <span data-ttu-id="b29d0-125">If you are new to Azure, you may find the [Azure glossary][Azure glossary] helpful as you encounter new terminology.</span><span class="sxs-lookup"><span data-stu-id="b29d0-125">If you are new to Azure, you may find the [Azure glossary][Azure glossary] helpful as you encounter new terminology.</span></span> <span data-ttu-id="b29d0-126">Or look at some of these other SQL Data Warehouse Resources.</span><span class="sxs-lookup"><span data-stu-id="b29d0-126">Or look at some of these other SQL Data Warehouse Resources.</span></span>  

* <span data-ttu-id="b29d0-127">[Customer success stories]</span><span class="sxs-lookup"><span data-stu-id="b29d0-127">[Customer success stories]</span></span>
* <span data-ttu-id="b29d0-128">[Blogs]</span><span class="sxs-lookup"><span data-stu-id="b29d0-128">[Blogs]</span></span>
* <span data-ttu-id="b29d0-129">[Feature requests]</span><span class="sxs-lookup"><span data-stu-id="b29d0-129">[Feature requests]</span></span>
* <span data-ttu-id="b29d0-130">[Videos]</span><span class="sxs-lookup"><span data-stu-id="b29d0-130">[Videos]</span></span>
* <span data-ttu-id="b29d0-131">[Customer Advisory Team blogs]</span><span class="sxs-lookup"><span data-stu-id="b29d0-131">[Customer Advisory Team blogs]</span></span>
* <span data-ttu-id="b29d0-132">[Create support ticket]</span><span class="sxs-lookup"><span data-stu-id="b29d0-132">[Create support ticket]</span></span>
* <span data-ttu-id="b29d0-133">[MSDN forum]</span><span class="sxs-lookup"><span data-stu-id="b29d0-133">[MSDN forum]</span></span>
* <span data-ttu-id="b29d0-134">[Stack Overflow forum]</span><span class="sxs-lookup"><span data-stu-id="b29d0-134">[Stack Overflow forum]</span></span>
* <span data-ttu-id="b29d0-135">[Twitter]</span><span class="sxs-lookup"><span data-stu-id="b29d0-135">[Twitter]</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-overview-what-is/dwarchitecture.png

<!--Article references-->
[Create support ticket]: ./sql-data-warehouse-get-started-create-support-ticket.md
[load sample data]: ./sql-data-warehouse-load-sample-databases.md
[create a SQL Data Warehouse]: ./sql-data-warehouse-get-started-provision.md
[Migration documentation]: ./sql-data-warehouse-overview-migrate.md
[SQL Data Warehouse solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[Integrated tools overview]: ./sql-data-warehouse-overview-integrate.md
[Backup and restore overview]: ./sql-data-warehouse-restore-database-overview.md
[Azure glossary]: ../azure-glossary-cloud-terminology.md

<!--MSDN references-->

<!--Other Web references-->
[Customer success stories]: https://azure.microsoft.com/case-studies/?service=sql-data-warehouse
[Blogs]: https://azure.microsoft.com/blog/tag/azure-sql-data-warehouse/
[Customer Advisory Team blogs]: https://blogs.msdn.microsoft.com/sqlcat/tag/sql-dw/
[Feature requests]: https://feedback.azure.com/forums/307516-sql-data-warehouse
[MSDN forum]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureSQLDataWarehouse
[Stack Overflow forum]: http://stackoverflow.com/questions/tagged/azure-sqldw
[Twitter]: https://twitter.com/hashtag/SQLDW
[Videos]: https://azure.microsoft.com/documentation/videos/index/?services=sql-data-warehouse
[SLA for SQL Data Warehouse]: https://azure.microsoft.com/support/legal/sla/sql-data-warehouse/v1_0/
[Volume Licensing]: http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=37
[Service Level Agreements]: https://azure.microsoft.com/support/legal/sla/
