---
title: Temporary tables in SQL Data Warehouse | Microsoft Docs
description: Essential guidance for using temporary tables and highlights the principles of session level temporary tables.
services: sql-data-warehouse
author: ronortloff
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: implement
ms.date: 04/17/2018
ms.author: rortloff
ms.reviewer: igorstan
ms.openlocfilehash: f8eb401d8bc4f348be3c84390d3422571bebe444
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44813929"
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="18b63-103">Temporary tables in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="18b63-103">Temporary tables in SQL Data Warehouse</span></span>
<span data-ttu-id="18b63-104">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span><span class="sxs-lookup"><span data-stu-id="18b63-104">This article contains essential guidance for using temporary tables and highlights the principles of session level temporary tables.</span></span> <span data-ttu-id="18b63-105">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span><span class="sxs-lookup"><span data-stu-id="18b63-105">Using the information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="what-are-temporary-tables"></a><span data-ttu-id="18b63-106">What are temporary tables?</span><span class="sxs-lookup"><span data-stu-id="18b63-106">What are temporary tables?</span></span>
<span data-ttu-id="18b63-107">Temporary tables are useful when processing data - especially during transformation where the intermediate results are transient.</span><span class="sxs-lookup"><span data-stu-id="18b63-107">Temporary tables are useful when processing data - especially during transformation where the intermediate results are transient.</span></span> <span data-ttu-id="18b63-108">In SQL Data Warehouse, temporary tables exist at the session level.</span><span class="sxs-lookup"><span data-stu-id="18b63-108">In SQL Data Warehouse, temporary tables exist at the session level.</span></span>  <span data-ttu-id="18b63-109">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span><span class="sxs-lookup"><span data-stu-id="18b63-109">They are only visible to the session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="18b63-110">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span><span class="sxs-lookup"><span data-stu-id="18b63-110">Temporary tables offer a performance benefit because their results are written to local rather than remote storage.</span></span>  <span data-ttu-id="18b63-111">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="18b63-111">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside the session, including both inside and outside of a stored procedure.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="18b63-112">Create a temporary table</span><span class="sxs-lookup"><span data-stu-id="18b63-112">Create a temporary table</span></span>
<span data-ttu-id="18b63-113">Temporary tables are created by prefixing your table name with a `#`.</span><span class="sxs-lookup"><span data-stu-id="18b63-113">Temporary tables are created by prefixing your table name with a `#`.</span></span>  <span data-ttu-id="18b63-114">For example:</span><span class="sxs-lookup"><span data-stu-id="18b63-114">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="18b63-115">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span><span class="sxs-lookup"><span data-stu-id="18b63-115">Temporary tables can also be created with a `CTAS` using exactly the same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="18b63-116">`CTAS` is a powerful command and has the added advantage of being efficient in its use of transaction log space.</span><span class="sxs-lookup"><span data-stu-id="18b63-116">`CTAS` is a powerful command and has the added advantage of being efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="18b63-117">Dropping temporary tables</span><span class="sxs-lookup"><span data-stu-id="18b63-117">Dropping temporary tables</span></span>
<span data-ttu-id="18b63-118">When a new session is created, no temporary tables should exist.</span><span class="sxs-lookup"><span data-stu-id="18b63-118">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="18b63-119">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the following example:</span><span class="sxs-lookup"><span data-stu-id="18b63-119">However, if you are calling the same stored procedure, which creates a temporary with the same name, to ensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in the following example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="18b63-120">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span><span class="sxs-lookup"><span data-stu-id="18b63-120">For coding consistency, it is a good practice to use this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="18b63-121">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span><span class="sxs-lookup"><span data-stu-id="18b63-121">It is also a good idea to use `DROP TABLE` to remove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="18b63-122">In stored procedure development, it is common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span><span class="sxs-lookup"><span data-stu-id="18b63-122">In stored procedure development, it is common to see the drop commands bundled together at the end of a procedure to ensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="18b63-123">Modularizing code</span><span class="sxs-lookup"><span data-stu-id="18b63-123">Modularizing code</span></span>
<span data-ttu-id="18b63-124">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span><span class="sxs-lookup"><span data-stu-id="18b63-124">Since temporary tables can be seen anywhere in a user session, this can be exploited to help you modularize your application code.</span></span>  <span data-ttu-id="18b63-125">For example, the following stored procedure generates DDL to update all statistics in the database by statistic name.</span><span class="sxs-lookup"><span data-stu-id="18b63-125">For example, the following stored procedure generates DDL to update all statistics in the database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="18b63-126">At this stage, the only action that has occurred is the creation of a stored procedure that generatess a temporary table, #stats_ddl, with DDL statements.</span><span class="sxs-lookup"><span data-stu-id="18b63-126">At this stage, the only action that has occurred is the creation of a stored procedure that generatess a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="18b63-127">This stored procedure drops #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span><span class="sxs-lookup"><span data-stu-id="18b63-127">This stored procedure drops #stats_ddl if it already exists to ensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="18b63-128">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it leaves the created table so that it can be read outside of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="18b63-128">However, since there is no `DROP TABLE` at the end of the stored procedure, when the stored procedure completes, it leaves the created table so that it can be read outside of the stored procedure.</span></span>  <span data-ttu-id="18b63-129">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span><span class="sxs-lookup"><span data-stu-id="18b63-129">In SQL Data Warehouse, unlike other SQL Server databases, it is possible to use the temporary table outside of the procedure that created it.</span></span>  <span data-ttu-id="18b63-130">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span><span class="sxs-lookup"><span data-stu-id="18b63-130">SQL Data Warehouse temporary tables can be used **anywhere** inside the session.</span></span> <span data-ttu-id="18b63-131">This can lead to more modular and manageable code as in the following example:</span><span class="sxs-lookup"><span data-stu-id="18b63-131">This can lead to more modular and manageable code as in the following example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="18b63-132">Temporary table limitations</span><span class="sxs-lookup"><span data-stu-id="18b63-132">Temporary table limitations</span></span>
<span data-ttu-id="18b63-133">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span><span class="sxs-lookup"><span data-stu-id="18b63-133">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="18b63-134">Currently, only session scoped temporary tables are supported.</span><span class="sxs-lookup"><span data-stu-id="18b63-134">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="18b63-135">Global Temporary Tables are not supported.</span><span class="sxs-lookup"><span data-stu-id="18b63-135">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="18b63-136">In addition, views cannot be created on temporary tables.</span><span class="sxs-lookup"><span data-stu-id="18b63-136">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18b63-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="18b63-137">Next steps</span></span>
<span data-ttu-id="18b63-138">To learn more about developing tables, see the [Table Overview](sql-data-warehouse-tables-overview.md).</span><span class="sxs-lookup"><span data-stu-id="18b63-138">To learn more about developing tables, see the [Table Overview](sql-data-warehouse-tables-overview.md).</span></span>

