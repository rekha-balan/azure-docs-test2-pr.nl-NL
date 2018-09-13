---
title: Schema mapping in copy activity | Microsoft Docs
description: Learn about how copy activity in Azure Data Factory maps schemas and data types from source data to sink data when copying data.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/22/2018
ms.author: jingwang
ms.openlocfilehash: 16275ddc4d4ad85bdac54244ceeec568603fdfef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867363"
---
# <a name="schema-mapping-in-copy-activity"></a><span data-ttu-id="130dc-103">Schema mapping in copy activity</span><span class="sxs-lookup"><span data-stu-id="130dc-103">Schema mapping in copy activity</span></span>
<span data-ttu-id="130dc-104">This article describes how Azure Data Factory copy activity does schema mapping and data type mapping from source data to sink data when perform the data copy.</span><span class="sxs-lookup"><span data-stu-id="130dc-104">This article describes how Azure Data Factory copy activity does schema mapping and data type mapping from source data to sink data when perform the data copy.</span></span>

## <a name="column-mapping"></a><span data-ttu-id="130dc-105">Column mapping</span><span class="sxs-lookup"><span data-stu-id="130dc-105">Column mapping</span></span>

<span data-ttu-id="130dc-106">By default, copy activity **map source data to sink by column names**, unless [explicit column mapping](#explicit-column-mapping) is configured.</span><span class="sxs-lookup"><span data-stu-id="130dc-106">By default, copy activity **map source data to sink by column names**, unless [explicit column mapping](#explicit-column-mapping) is configured.</span></span> <span data-ttu-id="130dc-107">More specifically, copy activity:</span><span class="sxs-lookup"><span data-stu-id="130dc-107">More specifically, copy activity:</span></span>

1. <span data-ttu-id="130dc-108">Read the data from source and determine the source schema</span><span class="sxs-lookup"><span data-stu-id="130dc-108">Read the data from source and determine the source schema</span></span>

    * <span data-ttu-id="130dc-109">For data sources with pre-defined schema in the data store/file format, for example, databases/files with metadata (Avro/ORC/Parquet/Text with header), source schema is extracted from the query result or file metadata.</span><span class="sxs-lookup"><span data-stu-id="130dc-109">For data sources with pre-defined schema in the data store/file format, for example, databases/files with metadata (Avro/ORC/Parquet/Text with header), source schema is extracted from the query result or file metadata.</span></span>
    * <span data-ttu-id="130dc-110">For data sources with flexible schema, for example,  Azure Table/Cosmos DB, source schema is inferred from the query result.</span><span class="sxs-lookup"><span data-stu-id="130dc-110">For data sources with flexible schema, for example,  Azure Table/Cosmos DB, source schema is inferred from the query result.</span></span> <span data-ttu-id="130dc-111">You can overwrite it by providing the "structure" in dataset.</span><span class="sxs-lookup"><span data-stu-id="130dc-111">You can overwrite it by providing the "structure" in dataset.</span></span>
    * <span data-ttu-id="130dc-112">For Text file without header, default column names are generated with pattern "Prop_0", "Prop_1", ...You can overwrite it by providing the "structure" in dataset.</span><span class="sxs-lookup"><span data-stu-id="130dc-112">For Text file without header, default column names are generated with pattern "Prop_0", "Prop_1", ...You can overwrite it by providing the "structure" in dataset.</span></span>
    * <span data-ttu-id="130dc-113">For Dynamics source, you have to provide the schema information in the dataset "structure" section.</span><span class="sxs-lookup"><span data-stu-id="130dc-113">For Dynamics source, you have to provide the schema information in the dataset "structure" section.</span></span>

2. <span data-ttu-id="130dc-114">Apply explicit column mapping if specified.</span><span class="sxs-lookup"><span data-stu-id="130dc-114">Apply explicit column mapping if specified.</span></span>

3. <span data-ttu-id="130dc-115">Write the data to sink</span><span class="sxs-lookup"><span data-stu-id="130dc-115">Write the data to sink</span></span>

    * <span data-ttu-id="130dc-116">For data stores with pre-defined schema, the data is written to the columns with the same name.</span><span class="sxs-lookup"><span data-stu-id="130dc-116">For data stores with pre-defined schema, the data is written to the columns with the same name.</span></span>
    * <span data-ttu-id="130dc-117">For data stores without fixed schema and for file formats, the column names/metadata will be generated based on the source schema.</span><span class="sxs-lookup"><span data-stu-id="130dc-117">For data stores without fixed schema and for file formats, the column names/metadata will be generated based on the source schema.</span></span>

### <a name="explicit-column-mapping"></a><span data-ttu-id="130dc-118">Explicit column mapping</span><span class="sxs-lookup"><span data-stu-id="130dc-118">Explicit column mapping</span></span>

<span data-ttu-id="130dc-119">You can specify **columnMappings** in the **typeProperties** section of the Copy activity to do explicit column mapping.</span><span class="sxs-lookup"><span data-stu-id="130dc-119">You can specify **columnMappings** in the **typeProperties** section of the Copy activity to do explicit column mapping.</span></span> <span data-ttu-id="130dc-120">In this scenario, "structure" section is required for both input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="130dc-120">In this scenario, "structure" section is required for both input and output datasets.</span></span> <span data-ttu-id="130dc-121">Column mapping supports **mapping all or subset of columns in the source dataset "structure" to all columns in the sink dataset "structure"**.</span><span class="sxs-lookup"><span data-stu-id="130dc-121">Column mapping supports **mapping all or subset of columns in the source dataset "structure" to all columns in the sink dataset "structure"**.</span></span> <span data-ttu-id="130dc-122">The following are error conditions that result in an exception:</span><span class="sxs-lookup"><span data-stu-id="130dc-122">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="130dc-123">Source data store query result does not have a column name that is specified in the input dataset "structure" section.</span><span class="sxs-lookup"><span data-stu-id="130dc-123">Source data store query result does not have a column name that is specified in the input dataset "structure" section.</span></span>
* <span data-ttu-id="130dc-124">Sink data store (if with pre-defined schema) does not have a column name that is specified in the output dataset "structure" section.</span><span class="sxs-lookup"><span data-stu-id="130dc-124">Sink data store (if with pre-defined schema) does not have a column name that is specified in the output dataset "structure" section.</span></span>
* <span data-ttu-id="130dc-125">Either fewer columns or more columns in the "structure" of sink dataset than specified in the mapping.</span><span class="sxs-lookup"><span data-stu-id="130dc-125">Either fewer columns or more columns in the "structure" of sink dataset than specified in the mapping.</span></span>
* <span data-ttu-id="130dc-126">Duplicate mapping.</span><span class="sxs-lookup"><span data-stu-id="130dc-126">Duplicate mapping.</span></span>

#### <a name="explicit-column-mapping-example"></a><span data-ttu-id="130dc-127">Explicit column mapping example</span><span class="sxs-lookup"><span data-stu-id="130dc-127">Explicit column mapping example</span></span>

<span data-ttu-id="130dc-128">In this sample, the input table has a structure and it points to a table in an on-premises SQL database.</span><span class="sxs-lookup"><span data-stu-id="130dc-128">In this sample, the input table has a structure and it points to a table in an on-premises SQL database.</span></span>

```json
{
    "name": "SqlServerInput",
    "properties": {
        "structure":
         [
            { "name": "UserId"},
            { "name": "Name"},
            { "name": "Group"}
         ],
        "type": "SqlServerTable",
        "linkedServiceName": {
            "referenceName": "SqlServerLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "SourceTable"
        }
    }
}
```

<span data-ttu-id="130dc-129">In this sample, the output table has a structure and it points to a table in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="130dc-129">In this sample, the output table has a structure and it points to a table in an Azure SQL Database.</span></span>

```json
{
    "name": "AzureSqlOutput",
    "properties": {
        "structure":
        [
            { "name": "MyUserId"},
            { "name": "MyName" },
            { "name": "MyGroup"}
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": {
            "referenceName": "AzureSqlLinkedService",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "SinkTable"
        }
    }
}
```

<span data-ttu-id="130dc-130">The following JSON defines a copy activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="130dc-130">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="130dc-131">The columns from source mapped to columns in sink (**columnMappings**) by using the **translator** property.</span><span class="sxs-lookup"><span data-stu-id="130dc-131">The columns from source mapped to columns in sink (**columnMappings**) by using the **translator** property.</span></span>

```json
{
    "name": "CopyActivity",
    "type": "Copy",
    "inputs": [
        {
            "referenceName": "SqlServerInput",
            "type": "DatasetReference"
        }
    ],
    "outputs": [
        {
            "referenceName": "AzureSqlOutput",
            "type": "DatasetReference"
        }
    ],
    "typeProperties":    {
        "source": { "type": "SqlSource" },
        "sink": { "type": "SqlSink" },
        "translator":
        {
            "type": "TabularTranslator",
            "columnMappings": 
            {
                "UserId": "MyUserId",
                "Group": "MyGroup",
                "Name": "MyName"
            }
        }
    }
}
```

<span data-ttu-id="130dc-132">If you were using the syntax of `"columnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"` to specify column mapping, it is still supported as-is.</span><span class="sxs-lookup"><span data-stu-id="130dc-132">If you were using the syntax of `"columnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"` to specify column mapping, it is still supported as-is.</span></span>

<span data-ttu-id="130dc-133">**Column mapping flow:**</span><span class="sxs-lookup"><span data-stu-id="130dc-133">**Column mapping flow:**</span></span>

![Column mapping flow](./media/copy-activity-schema-and-type-mapping/column-mapping-sample.png)

## <a name="data-type-mapping"></a><span data-ttu-id="130dc-135">Data type mapping</span><span class="sxs-lookup"><span data-stu-id="130dc-135">Data type mapping</span></span>

<span data-ttu-id="130dc-136">Copy activity performs source types to sink types mapping with the following 2-step approach:</span><span class="sxs-lookup"><span data-stu-id="130dc-136">Copy activity performs source types to sink types mapping with the following 2-step approach:</span></span>

1. <span data-ttu-id="130dc-137">Convert from native source types to Azure Data Factory interim data types</span><span class="sxs-lookup"><span data-stu-id="130dc-137">Convert from native source types to Azure Data Factory interim data types</span></span>
2. <span data-ttu-id="130dc-138">Convert from Azure Data Factory interim data types to native sink type</span><span class="sxs-lookup"><span data-stu-id="130dc-138">Convert from Azure Data Factory interim data types to native sink type</span></span>

<span data-ttu-id="130dc-139">You can find the mapping between native type to interim type in the "Data type mapping" section in each connector topic.</span><span class="sxs-lookup"><span data-stu-id="130dc-139">You can find the mapping between native type to interim type in the "Data type mapping" section in each connector topic.</span></span>

### <a name="supported-data-types"></a><span data-ttu-id="130dc-140">Supported data types</span><span class="sxs-lookup"><span data-stu-id="130dc-140">Supported data types</span></span>

<span data-ttu-id="130dc-141">Data Factory supports the following interim data types: You can specify below values when providing type information in [dataset structure](concepts-datasets-linked-services.md#dataset-structure) configuration:</span><span class="sxs-lookup"><span data-stu-id="130dc-141">Data Factory supports the following interim data types: You can specify below values when providing type information in [dataset structure](concepts-datasets-linked-services.md#dataset-structure) configuration:</span></span>

* <span data-ttu-id="130dc-142">Byte[]</span><span class="sxs-lookup"><span data-stu-id="130dc-142">Byte[]</span></span>
* <span data-ttu-id="130dc-143">Boolean</span><span class="sxs-lookup"><span data-stu-id="130dc-143">Boolean</span></span>
* <span data-ttu-id="130dc-144">Datetime</span><span class="sxs-lookup"><span data-stu-id="130dc-144">Datetime</span></span>
* <span data-ttu-id="130dc-145">Datetimeoffset</span><span class="sxs-lookup"><span data-stu-id="130dc-145">Datetimeoffset</span></span>
* <span data-ttu-id="130dc-146">Decimal</span><span class="sxs-lookup"><span data-stu-id="130dc-146">Decimal</span></span>
* <span data-ttu-id="130dc-147">Double</span><span class="sxs-lookup"><span data-stu-id="130dc-147">Double</span></span>
* <span data-ttu-id="130dc-148">Guid</span><span class="sxs-lookup"><span data-stu-id="130dc-148">Guid</span></span>
* <span data-ttu-id="130dc-149">Int16</span><span class="sxs-lookup"><span data-stu-id="130dc-149">Int16</span></span>
* <span data-ttu-id="130dc-150">Int32</span><span class="sxs-lookup"><span data-stu-id="130dc-150">Int32</span></span>
* <span data-ttu-id="130dc-151">Int64</span><span class="sxs-lookup"><span data-stu-id="130dc-151">Int64</span></span>
* <span data-ttu-id="130dc-152">Single</span><span class="sxs-lookup"><span data-stu-id="130dc-152">Single</span></span>
* <span data-ttu-id="130dc-153">String</span><span class="sxs-lookup"><span data-stu-id="130dc-153">String</span></span>
* <span data-ttu-id="130dc-154">Timespan</span><span class="sxs-lookup"><span data-stu-id="130dc-154">Timespan</span></span>

### <a name="explicit-data-type-conversion"></a><span data-ttu-id="130dc-155">Explicit data type conversion</span><span class="sxs-lookup"><span data-stu-id="130dc-155">Explicit data type conversion</span></span>

<span data-ttu-id="130dc-156">When copying data into data stores with fixed schema, for example,  SQL Server/Oracle, when source and sink has different type on the same column，the explicit type conversion should be declared in the source side:</span><span class="sxs-lookup"><span data-stu-id="130dc-156">When copying data into data stores with fixed schema, for example,  SQL Server/Oracle, when source and sink has different type on the same column，the explicit type conversion should be declared in the source side:</span></span>

* <span data-ttu-id="130dc-157">For file source, for example, CSV/Avro, the type conversion shall be declared via source structure with full column list (source side column name and sink side type)</span><span class="sxs-lookup"><span data-stu-id="130dc-157">For file source, for example, CSV/Avro, the type conversion shall be declared via source structure with full column list (source side column name and sink side type)</span></span>
* <span data-ttu-id="130dc-158">For relational source (for example, SQL/Oracle), the type conversion should be achieved by explicit type casting in the query statement.</span><span class="sxs-lookup"><span data-stu-id="130dc-158">For relational source (for example, SQL/Oracle), the type conversion should be achieved by explicit type casting in the query statement.</span></span>

## <a name="when-to-specify-dataset-structure"></a><span data-ttu-id="130dc-159">When to specify dataset "structure"</span><span class="sxs-lookup"><span data-stu-id="130dc-159">When to specify dataset "structure"</span></span>

<span data-ttu-id="130dc-160">In below scenarios, "structure" in dataset is required:</span><span class="sxs-lookup"><span data-stu-id="130dc-160">In below scenarios, "structure" in dataset is required:</span></span>

* <span data-ttu-id="130dc-161">Applying [explicit data type conversion](#explicit-data-type-conversion) for file sources during copy (input dataset)</span><span class="sxs-lookup"><span data-stu-id="130dc-161">Applying [explicit data type conversion](#explicit-data-type-conversion) for file sources during copy (input dataset)</span></span>
* <span data-ttu-id="130dc-162">Applying [explicit column mapping](#explicit-column-mapping) during copy (both input and output dataset)</span><span class="sxs-lookup"><span data-stu-id="130dc-162">Applying [explicit column mapping](#explicit-column-mapping) during copy (both input and output dataset)</span></span>
* <span data-ttu-id="130dc-163">Copying from Dynamics 365/CRM source (input dataset)</span><span class="sxs-lookup"><span data-stu-id="130dc-163">Copying from Dynamics 365/CRM source (input dataset)</span></span>
* <span data-ttu-id="130dc-164">Copying to Cosmos DB as nested object when source is not JSON files (output dataset)</span><span class="sxs-lookup"><span data-stu-id="130dc-164">Copying to Cosmos DB as nested object when source is not JSON files (output dataset)</span></span>

<span data-ttu-id="130dc-165">In below scenarios, "structure" in dataset is suggested:</span><span class="sxs-lookup"><span data-stu-id="130dc-165">In below scenarios, "structure" in dataset is suggested:</span></span>

* <span data-ttu-id="130dc-166">Copying from Text file without header (input dataset).</span><span class="sxs-lookup"><span data-stu-id="130dc-166">Copying from Text file without header (input dataset).</span></span> <span data-ttu-id="130dc-167">You can specify the column names for Text file aligning with the corresponding sink columns, to save from providing explicit column mapping.</span><span class="sxs-lookup"><span data-stu-id="130dc-167">You can specify the column names for Text file aligning with the corresponding sink columns, to save from providing explicit column mapping.</span></span>
* <span data-ttu-id="130dc-168">Copying from data stores with flexible schema, for example,  Azure Table/Cosmos DB (input dataset), to guarantee the expected data (columns) being copied over instead of let copy activity infer schema based on top row(s) during each activity run.</span><span class="sxs-lookup"><span data-stu-id="130dc-168">Copying from data stores with flexible schema, for example,  Azure Table/Cosmos DB (input dataset), to guarantee the expected data (columns) being copied over instead of let copy activity infer schema based on top row(s) during each activity run.</span></span>


## <a name="next-steps"></a><span data-ttu-id="130dc-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="130dc-169">Next steps</span></span>
<span data-ttu-id="130dc-170">See the other Copy Activity articles:</span><span class="sxs-lookup"><span data-stu-id="130dc-170">See the other Copy Activity articles:</span></span>

- [<span data-ttu-id="130dc-171">Copy activity overview</span><span class="sxs-lookup"><span data-stu-id="130dc-171">Copy activity overview</span></span>](copy-activity-overview.md)
- [<span data-ttu-id="130dc-172">Copy activity fault tolerance</span><span class="sxs-lookup"><span data-stu-id="130dc-172">Copy activity fault tolerance</span></span>](copy-activity-fault-tolerance.md)
- [<span data-ttu-id="130dc-173">Copy activity performance</span><span class="sxs-lookup"><span data-stu-id="130dc-173">Copy activity performance</span></span>](copy-activity-performance.md)
