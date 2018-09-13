---
title: Invoke stored procedure from Azure Data Factory Copy Activity | Microsoft Docs
description: Learn how to invoke a stored procedure in Azure SQL Database, or SQL Server from an Azure Data Factory copy activity.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: jingwang
ms.openlocfilehash: 8824990ca10f8a0f83162768557bcb2f4008b514
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553538"
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="84bbf-103">Invoke stored procedure from copy activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="84bbf-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="84bbf-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span><span class="sxs-lookup"><span data-stu-id="84bbf-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="84bbf-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span><span class="sxs-lookup"><span data-stu-id="84bbf-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="84bbf-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="84bbf-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="84bbf-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span><span class="sxs-lookup"><span data-stu-id="84bbf-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="84bbf-108">Output dataset JSON</span><span class="sxs-lookup"><span data-stu-id="84bbf-108">Output dataset JSON</span></span>
<span data-ttu-id="84bbf-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="84bbf-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="84bbf-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="84bbf-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="84bbf-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="84bbf-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="84bbf-112">SqlSink section in copy activity JSON</span><span class="sxs-lookup"><span data-stu-id="84bbf-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="84bbf-113">Define the **SqlSink** section in the copy activity JSON as follows.</span><span class="sxs-lookup"><span data-stu-id="84bbf-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="84bbf-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span><span class="sxs-lookup"><span data-stu-id="84bbf-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="84bbf-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="84bbf-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="84bbf-116">Stored procedure definition</span><span class="sxs-lookup"><span data-stu-id="84bbf-116">Stored procedure definition</span></span> 
<span data-ttu-id="84bbf-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="84bbf-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="84bbf-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span><span class="sxs-lookup"><span data-stu-id="84bbf-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="84bbf-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="84bbf-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="84bbf-120">Table type definition</span><span class="sxs-lookup"><span data-stu-id="84bbf-120">Table type definition</span></span>
<span data-ttu-id="84bbf-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="84bbf-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="84bbf-122">The schema of the table type must match the schema of the input dataset.</span><span class="sxs-lookup"><span data-stu-id="84bbf-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="84bbf-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="84bbf-123">Next steps</span></span>
<span data-ttu-id="84bbf-124">Review the following connector articles that for complete JSON examples:</span><span class="sxs-lookup"><span data-stu-id="84bbf-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="84bbf-125">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="84bbf-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="84bbf-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="84bbf-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
