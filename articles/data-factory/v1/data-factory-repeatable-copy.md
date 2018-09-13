---
title: Repeatable copy in Azure Data Factory| Microsoft Docs
description: Learn how to avoid duplicates even though a slice that copies data is run more than once.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 8b1d1cf62dad94ca6141ce33783c0b16b50c931c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967396"
---
# <a name="repeatable-copy-in-azure-data-factory"></a><span data-ttu-id="8c5ac-103">Repeatable copy in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8c5ac-103">Repeatable copy in Azure Data Factory</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="8c5ac-104">Repeatable read from relational sources</span><span class="sxs-lookup"><span data-stu-id="8c5ac-104">Repeatable read from relational sources</span></span>
<span data-ttu-id="8c5ac-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-105">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="8c5ac-106">In Azure Data Factory, you can rerun a slice manually.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-106">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="8c5ac-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-107">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="8c5ac-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-108">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span>  
 
> [!NOTE]
> <span data-ttu-id="8c5ac-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-109">The following samples are for Azure SQL but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="8c5ac-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-110">You may have to adjust the **type** of source and the **query** property (for example: query instead of sqlReaderQuery) for the data store.</span></span>   

<span data-ttu-id="8c5ac-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-111">Usually, when reading from relational stores, you want to read only the data corresponding to that slice.</span></span> <span data-ttu-id="8c5ac-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-112">A way to do so would be by using the WindowStart and WindowEnd system variables available in Azure Data Factory.</span></span> <span data-ttu-id="8c5ac-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-113">Read about the variables and functions in Azure Data Factory here in the [Azure Data Factory - Functions and System Variables](data-factory-functions-variables.md) article.</span></span> <span data-ttu-id="8c5ac-114">Example:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-114">Example:</span></span> 

```json
"source": {
    "type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm\\'', WindowStart, WindowEnd)"
},
```
<span data-ttu-id="8c5ac-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-115">This query reads data that falls in the slice duration range (WindowStart -> WindowEnd) from the table MyTable.</span></span> <span data-ttu-id="8c5ac-116">Rerun of this slice would also always ensure that the same data is read.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-116">Rerun of this slice would also always ensure that the same data is read.</span></span> 

<span data-ttu-id="8c5ac-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-117">In other cases, you may wish to read the entire table and may define the sqlReaderQuery as follows:</span></span>

```json
"source": 
{            
    "type": "SqlSource",
    "sqlReaderQuery": "select * from MyTable"
},
```

## <a name="repeatable-write-to-sqlsink"></a><span data-ttu-id="8c5ac-118">Repeatable write to SqlSink</span><span class="sxs-lookup"><span data-stu-id="8c5ac-118">Repeatable write to SqlSink</span></span>
<span data-ttu-id="8c5ac-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-119">When copying data to **Azure SQL/SQL Server** from other data stores, you need to keep repeatability in mind to avoid unintended outcomes.</span></span> 

<span data-ttu-id="8c5ac-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-120">When copying data to Azure SQL/SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="8c5ac-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-121">Say, you are copying data from a CSV (comma-separated values) file containing two records to the following table in an Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="8c5ac-122">When a slice runs, the two records are copied to the SQL table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-122">When a slice runs, the two records are copied to the SQL table.</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

<span data-ttu-id="8c5ac-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-123">Suppose you found errors in source file and updated the quantity of Down Tube from 2 to 4.</span></span> <span data-ttu-id="8c5ac-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-124">If you rerun the data slice for that period manually, you’ll find two new records appended to Azure SQL/SQL Server Database.</span></span> <span data-ttu-id="8c5ac-125">This example assumes that none of the columns in the table has the primary key constraint.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-125">This example assumes that none of the columns in the table has the primary key constraint.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8c5ac-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-126">To avoid this behavior, you need to specify UPSERT semantics by using one of the following two mechanisms:</span></span>

### <a name="mechanism-1-using-sqlwritercleanupscript"></a><span data-ttu-id="8c5ac-127">Mechanism 1: using sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="8c5ac-127">Mechanism 1: using sqlWriterCleanupScript</span></span>
<span data-ttu-id="8c5ac-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-128">You can use the **sqlWriterCleanupScript** property to clean up data from the sink table before inserting the data when a slice is run.</span></span> 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

<span data-ttu-id="8c5ac-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-129">When a slice runs, the cleanup script is run first to delete data that corresponds to the slice from the SQL table.</span></span> <span data-ttu-id="8c5ac-130">The copy activity then inserts data into the SQL Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-130">The copy activity then inserts data into the SQL Table.</span></span> <span data-ttu-id="8c5ac-131">If the slice is rerun, the quantity is updated as desired.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-131">If the slice is rerun, the quantity is updated as desired.</span></span>

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8c5ac-132">Suppose the Flat Washer record is removed from the original csv.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-132">Suppose the Flat Washer record is removed from the original csv.</span></span> <span data-ttu-id="8c5ac-133">Then rerunning the slice would produce the following result:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-133">Then rerunning the slice would produce the following result:</span></span> 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```

<span data-ttu-id="8c5ac-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-134">The copy activity ran the cleanup script to delete the corresponding data for that slice.</span></span> <span data-ttu-id="8c5ac-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-135">Then it read the input from the csv (which then contained only one record) and inserted it into the Table.</span></span> 

### <a name="mechanism-2-using-sliceidentifiercolumnname"></a><span data-ttu-id="8c5ac-136">Mechanism 2: using sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="8c5ac-136">Mechanism 2: using sliceIdentifierColumnName</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8c5ac-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-137">Currently, sliceIdentifierColumnName is not supported for Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="8c5ac-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-138">The second mechanism to achieve repeatability is by having a dedicated column (sliceIdentifierColumnName) in the target Table.</span></span> <span data-ttu-id="8c5ac-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-139">This column would be used by Azure Data Factory to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="8c5ac-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-140">This approach works when there is flexibility in changing or defining the destination SQL Table schema.</span></span> 

<span data-ttu-id="8c5ac-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-141">This column is used by Azure Data Factory for repeatability purposes and in the process Azure Data Factory does not make any schema changes to the Table.</span></span> <span data-ttu-id="8c5ac-142">Way to use this approach:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-142">Way to use this approach:</span></span>

1. <span data-ttu-id="8c5ac-143">Define a column of type **binary (32)** in the destination SQL Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-143">Define a column of type **binary (32)** in the destination SQL Table.</span></span> <span data-ttu-id="8c5ac-144">There should be no constraints on this column.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-144">There should be no constraints on this column.</span></span> <span data-ttu-id="8c5ac-145">Let's name this column as AdfSliceIdentifier for this example.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-145">Let's name this column as AdfSliceIdentifier for this example.</span></span>


    <span data-ttu-id="8c5ac-146">Source table:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-146">Source table:</span></span>

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL
    )
    ```

    <span data-ttu-id="8c5ac-147">Destination table:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-147">Destination table:</span></span> 

    ```sql
    CREATE TABLE [dbo].[Student](
       [Id] [varchar](32) NOT NULL,
       [Name] [nvarchar](256) NOT NULL,
       [AdfSliceIdentifier] [binary](32) NULL
    )
    ```

2. <span data-ttu-id="8c5ac-148">Use it in the copy activity as follows:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-148">Use it in the copy activity as follows:</span></span>
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "AdfSliceIdentifier"
    }
    ```

<span data-ttu-id="8c5ac-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-149">Azure Data Factory populates this column as per its need to ensure the source and destination stay synchronized.</span></span> <span data-ttu-id="8c5ac-150">The values of this column should not be used outside of this context.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-150">The values of this column should not be used outside of this context.</span></span> 

<span data-ttu-id="8c5ac-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-151">Similar to mechanism 1, Copy Activity automatically cleans up the data for the given slice from the destination SQL Table.</span></span> <span data-ttu-id="8c5ac-152">It then inserts data from source in to the destination table.</span><span class="sxs-lookup"><span data-stu-id="8c5ac-152">It then inserts data from source in to the destination table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c5ac-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c5ac-153">Next steps</span></span>
<span data-ttu-id="8c5ac-154">Review the following connector articles that for complete JSON examples:</span><span class="sxs-lookup"><span data-stu-id="8c5ac-154">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="8c5ac-155">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="8c5ac-155">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="8c5ac-156">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8c5ac-156">Azure SQL Data Warehouse</span></span>](data-factory-azure-sql-data-warehouse-connector.md)
- [<span data-ttu-id="8c5ac-157">SQL Server</span><span class="sxs-lookup"><span data-stu-id="8c5ac-157">SQL Server</span></span>](data-factory-sqlserver-connector.md)
