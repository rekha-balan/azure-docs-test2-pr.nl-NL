---
title: Lookup activity in Azure Data Factory | Microsoft Docs
description: Learn how to use Lookup activity to look up a value from an external source. This output can be further referenced by succeeding activities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/15/2018
ms.author: shlo
ms.openlocfilehash: e437e7b7d5298af325ae2a5e2ba689b417bad022
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869912"
---
# <a name="lookup-activity-in-azure-data-factory"></a><span data-ttu-id="474a6-104">Lookup activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="474a6-104">Lookup activity in Azure Data Factory</span></span>

<span data-ttu-id="474a6-105">Lookup activity can retrieve a dataset from any of the Azure Data Factory-supported data sources.</span><span class="sxs-lookup"><span data-stu-id="474a6-105">Lookup activity can retrieve a dataset from any of the Azure Data Factory-supported data sources.</span></span> <span data-ttu-id="474a6-106">Use it in the following scenario:</span><span class="sxs-lookup"><span data-stu-id="474a6-106">Use it in the following scenario:</span></span>
- <span data-ttu-id="474a6-107">Dynamically determine which objects to operate on in a subsequent activity, instead of hard coding the object name.</span><span class="sxs-lookup"><span data-stu-id="474a6-107">Dynamically determine which objects to operate on in a subsequent activity, instead of hard coding the object name.</span></span> <span data-ttu-id="474a6-108">Some object examples are files and tables.</span><span class="sxs-lookup"><span data-stu-id="474a6-108">Some object examples are files and tables.</span></span>

<span data-ttu-id="474a6-109">Lookup activity reads and returns the content of a configuration file or table.</span><span class="sxs-lookup"><span data-stu-id="474a6-109">Lookup activity reads and returns the content of a configuration file or table.</span></span> <span data-ttu-id="474a6-110">It also returns the result of executing a query or stored procedure.</span><span class="sxs-lookup"><span data-stu-id="474a6-110">It also returns the result of executing a query or stored procedure.</span></span> <span data-ttu-id="474a6-111">The output from Lookup activity can be used in a subsequent copy or transformation activity if it's a singleton value.</span><span class="sxs-lookup"><span data-stu-id="474a6-111">The output from Lookup activity can be used in a subsequent copy or transformation activity if it's a singleton value.</span></span> <span data-ttu-id="474a6-112">The output can be used in a ForEach activity if it's an array of attributes.</span><span class="sxs-lookup"><span data-stu-id="474a6-112">The output can be used in a ForEach activity if it's an array of attributes.</span></span>

## <a name="supported-capabilities"></a><span data-ttu-id="474a6-113">Supported capabilities</span><span class="sxs-lookup"><span data-stu-id="474a6-113">Supported capabilities</span></span>

<span data-ttu-id="474a6-114">The following data sources are supported for Lookup activity.</span><span class="sxs-lookup"><span data-stu-id="474a6-114">The following data sources are supported for Lookup activity.</span></span> <span data-ttu-id="474a6-115">The largest number of rows that can be returned by Lookup activity is 5,000, up to 2 MB in size.</span><span class="sxs-lookup"><span data-stu-id="474a6-115">The largest number of rows that can be returned by Lookup activity is 5,000, up to 2 MB in size.</span></span> <span data-ttu-id="474a6-116">Currently, the longest duration for Lookup activity before timeout is one hour.</span><span class="sxs-lookup"><span data-stu-id="474a6-116">Currently, the longest duration for Lookup activity before timeout is one hour.</span></span>

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores-for-lookup-activity.md)]

## <a name="syntax"></a><span data-ttu-id="474a6-117">Syntax</span><span class="sxs-lookup"><span data-stu-id="474a6-117">Syntax</span></span>

```json
{
    "name": "LookupActivity",
    "type": "Lookup",
    "typeProperties": {
        "source": {
            "type": "<source type>"
            <additional source specific properties (optional)>
        },
        "dataset": { 
            "referenceName": "<source dataset name>",
            "type": "DatasetReference"
        },
        "firstRowOnly": false
    }
}
```

## <a name="type-properties"></a><span data-ttu-id="474a6-118">Type properties</span><span class="sxs-lookup"><span data-stu-id="474a6-118">Type properties</span></span>
<span data-ttu-id="474a6-119">Name</span><span class="sxs-lookup"><span data-stu-id="474a6-119">Name</span></span> | <span data-ttu-id="474a6-120">Description</span><span class="sxs-lookup"><span data-stu-id="474a6-120">Description</span></span> | <span data-ttu-id="474a6-121">Type</span><span class="sxs-lookup"><span data-stu-id="474a6-121">Type</span></span> | <span data-ttu-id="474a6-122">Required?</span><span class="sxs-lookup"><span data-stu-id="474a6-122">Required?</span></span>
---- | ----------- | ---- | --------
<span data-ttu-id="474a6-123">dataset</span><span class="sxs-lookup"><span data-stu-id="474a6-123">dataset</span></span> | <span data-ttu-id="474a6-124">Provides the dataset reference for the lookup.</span><span class="sxs-lookup"><span data-stu-id="474a6-124">Provides the dataset reference for the lookup.</span></span> <span data-ttu-id="474a6-125">Get details from the **Dataset properties** section in each corresponding connector article.</span><span class="sxs-lookup"><span data-stu-id="474a6-125">Get details from the **Dataset properties** section in each corresponding connector article.</span></span> | <span data-ttu-id="474a6-126">Key/value pair</span><span class="sxs-lookup"><span data-stu-id="474a6-126">Key/value pair</span></span> | <span data-ttu-id="474a6-127">Yes</span><span class="sxs-lookup"><span data-stu-id="474a6-127">Yes</span></span>
<span data-ttu-id="474a6-128">source</span><span class="sxs-lookup"><span data-stu-id="474a6-128">source</span></span> | <span data-ttu-id="474a6-129">Contains dataset-specific source properties, the same as the Copy Activity source.</span><span class="sxs-lookup"><span data-stu-id="474a6-129">Contains dataset-specific source properties, the same as the Copy Activity source.</span></span> <span data-ttu-id="474a6-130">Get details from the **Copy Activity properties** section in each corresponding connector article.</span><span class="sxs-lookup"><span data-stu-id="474a6-130">Get details from the **Copy Activity properties** section in each corresponding connector article.</span></span> | <span data-ttu-id="474a6-131">Key/value pair</span><span class="sxs-lookup"><span data-stu-id="474a6-131">Key/value pair</span></span> | <span data-ttu-id="474a6-132">Yes</span><span class="sxs-lookup"><span data-stu-id="474a6-132">Yes</span></span>
<span data-ttu-id="474a6-133">firstRowOnly</span><span class="sxs-lookup"><span data-stu-id="474a6-133">firstRowOnly</span></span> | <span data-ttu-id="474a6-134">Indicates whether to return only the first row or all rows.</span><span class="sxs-lookup"><span data-stu-id="474a6-134">Indicates whether to return only the first row or all rows.</span></span> | <span data-ttu-id="474a6-135">Boolean</span><span class="sxs-lookup"><span data-stu-id="474a6-135">Boolean</span></span> | <span data-ttu-id="474a6-136">No.</span><span class="sxs-lookup"><span data-stu-id="474a6-136">No.</span></span> <span data-ttu-id="474a6-137">The default is `true`.</span><span class="sxs-lookup"><span data-stu-id="474a6-137">The default is `true`.</span></span>

> [!NOTE]

> * <span data-ttu-id="474a6-138">Source columns with **ByteArray** type aren't supported.</span><span class="sxs-lookup"><span data-stu-id="474a6-138">Source columns with **ByteArray** type aren't supported.</span></span>
> * <span data-ttu-id="474a6-139">**Structure** isn't supported in dataset definitions.</span><span class="sxs-lookup"><span data-stu-id="474a6-139">**Structure** isn't supported in dataset definitions.</span></span> <span data-ttu-id="474a6-140">For text-format files, use the header row to provide the column name.</span><span class="sxs-lookup"><span data-stu-id="474a6-140">For text-format files, use the header row to provide the column name.</span></span>
> * <span data-ttu-id="474a6-141">If your lookup source is a JSON file, the `jsonPathDefinition` setting for reshaping the JSON object isn't supported.</span><span class="sxs-lookup"><span data-stu-id="474a6-141">If your lookup source is a JSON file, the `jsonPathDefinition` setting for reshaping the JSON object isn't supported.</span></span> <span data-ttu-id="474a6-142">The entire objects will be retrieved.</span><span class="sxs-lookup"><span data-stu-id="474a6-142">The entire objects will be retrieved.</span></span>

## <a name="use-the-lookup-activity-result-in-a-subsequent-activity"></a><span data-ttu-id="474a6-143">Use the Lookup activity result in a subsequent activity</span><span class="sxs-lookup"><span data-stu-id="474a6-143">Use the Lookup activity result in a subsequent activity</span></span>

<span data-ttu-id="474a6-144">The lookup result is returned in the `output` section of the activity run result.</span><span class="sxs-lookup"><span data-stu-id="474a6-144">The lookup result is returned in the `output` section of the activity run result.</span></span>

* <span data-ttu-id="474a6-145">**When `firstRowOnly` is set to `true` (default)**, the output format is as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="474a6-145">**When `firstRowOnly` is set to `true` (default)**, the output format is as shown in the following code.</span></span> <span data-ttu-id="474a6-146">The lookup result is under a fixed `firstRow` key.</span><span class="sxs-lookup"><span data-stu-id="474a6-146">The lookup result is under a fixed `firstRow` key.</span></span> <span data-ttu-id="474a6-147">To use the result in subsequent activity, use the pattern of `@{activity('MyLookupActivity').output.firstRow.TableName}`.</span><span class="sxs-lookup"><span data-stu-id="474a6-147">To use the result in subsequent activity, use the pattern of `@{activity('MyLookupActivity').output.firstRow.TableName}`.</span></span>

    ```json
    {
        "firstRow":
        {
            "Id": "1",
            "TableName" : "Table1"
        }
    }
    ```

* <span data-ttu-id="474a6-148">**When `firstRowOnly` is set to `false`**, the output format is as shown in the following code.</span><span class="sxs-lookup"><span data-stu-id="474a6-148">**When `firstRowOnly` is set to `false`**, the output format is as shown in the following code.</span></span> <span data-ttu-id="474a6-149">A `count` field indicates how many records are returned.</span><span class="sxs-lookup"><span data-stu-id="474a6-149">A `count` field indicates how many records are returned.</span></span> <span data-ttu-id="474a6-150">Detailed values are displayed under a fixed `value` array.</span><span class="sxs-lookup"><span data-stu-id="474a6-150">Detailed values are displayed under a fixed `value` array.</span></span> <span data-ttu-id="474a6-151">In such a case, the Lookup activity is followed by a [Foreach activity](control-flow-for-each-activity.md).</span><span class="sxs-lookup"><span data-stu-id="474a6-151">In such a case, the Lookup activity is followed by a [Foreach activity](control-flow-for-each-activity.md).</span></span> <span data-ttu-id="474a6-152">You pass the `value` array to the ForEach activity `items` field by using the pattern of `@activity('MyLookupActivity').output.value`.</span><span class="sxs-lookup"><span data-stu-id="474a6-152">You pass the `value` array to the ForEach activity `items` field by using the pattern of `@activity('MyLookupActivity').output.value`.</span></span> <span data-ttu-id="474a6-153">To access elements in the `value` array, use the following syntax: `@{activity('lookupActivity').output.value[zero based index].propertyname}`.</span><span class="sxs-lookup"><span data-stu-id="474a6-153">To access elements in the `value` array, use the following syntax: `@{activity('lookupActivity').output.value[zero based index].propertyname}`.</span></span> <span data-ttu-id="474a6-154">An example is `@{activity('lookupActivity').output.value[0].tablename}`.</span><span class="sxs-lookup"><span data-stu-id="474a6-154">An example is `@{activity('lookupActivity').output.value[0].tablename}`.</span></span>

    ```json
    {
        "count": "2",
        "value": [
            {
                "Id": "1",
                "TableName" : "Table1"
            },
            {
                "Id": "2",
                "TableName" : "Table2"
            }
        ]
    } 
    ```

### <a name="copy-activity-example"></a><span data-ttu-id="474a6-155">Copy Activity example</span><span class="sxs-lookup"><span data-stu-id="474a6-155">Copy Activity example</span></span>
<span data-ttu-id="474a6-156">In this example, Copy Activity copies data from a SQL table in your Azure SQL Database instance to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-156">In this example, Copy Activity copies data from a SQL table in your Azure SQL Database instance to Azure Blob storage.</span></span> <span data-ttu-id="474a6-157">The name of the SQL table is stored in a JSON file in Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-157">The name of the SQL table is stored in a JSON file in Blob storage.</span></span> <span data-ttu-id="474a6-158">The Lookup activity looks up the table name at runtime.</span><span class="sxs-lookup"><span data-stu-id="474a6-158">The Lookup activity looks up the table name at runtime.</span></span> <span data-ttu-id="474a6-159">JSON is modified dynamically by using this approach.</span><span class="sxs-lookup"><span data-stu-id="474a6-159">JSON is modified dynamically by using this approach.</span></span> <span data-ttu-id="474a6-160">You don't need to redeploy pipelines or datasets.</span><span class="sxs-lookup"><span data-stu-id="474a6-160">You don't need to redeploy pipelines or datasets.</span></span> 

<span data-ttu-id="474a6-161">This example demonstrates lookup for the first row only.</span><span class="sxs-lookup"><span data-stu-id="474a6-161">This example demonstrates lookup for the first row only.</span></span> <span data-ttu-id="474a6-162">For lookup for all rows and to chain the results with ForEach activity, see the samples in [Copy multiple tables in bulk by using Azure Data Factory](tutorial-bulk-copy.md).</span><span class="sxs-lookup"><span data-stu-id="474a6-162">For lookup for all rows and to chain the results with ForEach activity, see the samples in [Copy multiple tables in bulk by using Azure Data Factory](tutorial-bulk-copy.md).</span></span>

### <a name="pipeline"></a><span data-ttu-id="474a6-163">Pipeline</span><span class="sxs-lookup"><span data-stu-id="474a6-163">Pipeline</span></span>
<span data-ttu-id="474a6-164">This pipeline contains two activities: Lookup and Copy.</span><span class="sxs-lookup"><span data-stu-id="474a6-164">This pipeline contains two activities: Lookup and Copy.</span></span> 

- <span data-ttu-id="474a6-165">The Lookup activity is configured to use **LookupDataset**, which refers to a location in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-165">The Lookup activity is configured to use **LookupDataset**, which refers to a location in Azure Blob storage.</span></span> <span data-ttu-id="474a6-166">The Lookup activity reads the name of the SQL table from a JSON file in this location.</span><span class="sxs-lookup"><span data-stu-id="474a6-166">The Lookup activity reads the name of the SQL table from a JSON file in this location.</span></span> 
- <span data-ttu-id="474a6-167">Copy Activity uses the output of the Lookup activity, which is the name of the SQL table.</span><span class="sxs-lookup"><span data-stu-id="474a6-167">Copy Activity uses the output of the Lookup activity, which is the name of the SQL table.</span></span> <span data-ttu-id="474a6-168">The **tableName** property in the **SourceDataset** is configured to use the output from the Lookup activity.</span><span class="sxs-lookup"><span data-stu-id="474a6-168">The **tableName** property in the **SourceDataset** is configured to use the output from the Lookup activity.</span></span> <span data-ttu-id="474a6-169">Copy Activity copies data from the SQL table to a location in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-169">Copy Activity copies data from the SQL table to a location in Azure Blob storage.</span></span> <span data-ttu-id="474a6-170">The location is specified by the **SinkDataset** property.</span><span class="sxs-lookup"><span data-stu-id="474a6-170">The location is specified by the **SinkDataset** property.</span></span> 

```json
{
    "name": "LookupPipelineDemo",
    "properties": {
        "activities": [
            {
                "name": "LookupActivity",
                "type": "Lookup",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "dataset": { 
                        "referenceName": "LookupDataset", 
                        "type": "DatasetReference" 
                    }
                }
            },
            {
                "name": "CopyActivity",
                "type": "Copy",
                "typeProperties": {
                    "source": { 
                        "type": "SqlSource", 
                        "sqlReaderQuery": "select * from @{activity('LookupActivity').output.firstRow.tableName}" 
                    },
                    "sink": { 
                        "type": "BlobSink" 
                    }
                },                
                "dependsOn": [ 
                    { 
                        "activity": "LookupActivity", 
                        "dependencyConditions": [ "Succeeded" ] 
                    }
                 ],
                "inputs": [ 
                    { 
                        "referenceName": "SourceDataset", 
                        "type": "DatasetReference" 
                    } 
                ],
                "outputs": [ 
                    { 
                        "referenceName": "SinkDataset", 
                        "type": "DatasetReference" 
                    } 
                ]
            }
        ]
    }
}
```

### <a name="lookup-dataset"></a><span data-ttu-id="474a6-171">Lookup dataset</span><span class="sxs-lookup"><span data-stu-id="474a6-171">Lookup dataset</span></span>
<span data-ttu-id="474a6-172">The **lookup** dataset is the **sourcetable.json** file in the Azure Storage lookup folder specified by the **AzureStorageLinkedService** type.</span><span class="sxs-lookup"><span data-stu-id="474a6-172">The **lookup** dataset is the **sourcetable.json** file in the Azure Storage lookup folder specified by the **AzureStorageLinkedService** type.</span></span> 

```json
{
    "name": "LookupDataset",
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": "lookup",
            "fileName": "sourcetable.json",
            "format": {
                "type": "JsonFormat",
                "filePattern": "SetOfObjects"
            }
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        }
    }
}
```

### <a name="source-dataset-for-copy-activity"></a><span data-ttu-id="474a6-173">**Source** dataset for Copy Activity</span><span class="sxs-lookup"><span data-stu-id="474a6-173">**Source** dataset for Copy Activity</span></span>
<span data-ttu-id="474a6-174">The **source** dataset uses the output of the Lookup activity, which is the name of the SQL table.</span><span class="sxs-lookup"><span data-stu-id="474a6-174">The **source** dataset uses the output of the Lookup activity, which is the name of the SQL table.</span></span> <span data-ttu-id="474a6-175">Copy Activity copies data from this SQL table to a location in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-175">Copy Activity copies data from this SQL table to a location in Azure Blob storage.</span></span> <span data-ttu-id="474a6-176">The location is specified by the **sink** dataset.</span><span class="sxs-lookup"><span data-stu-id="474a6-176">The location is specified by the **sink** dataset.</span></span> 

```json
{
    "name": "SourceDataset",
    "properties": {
        "type": "AzureSqlTable",
        "typeProperties":{
            "tableName": "@{activity('LookupActivity').output.firstRow.tableName}"
        },
        "linkedServiceName": {
            "referenceName": "AzureSqlLinkedService",
            "type": "LinkedServiceReference"
        }
    }
}
```

### <a name="sink-dataset-for-copy-activity"></a><span data-ttu-id="474a6-177">**Sink** dataset for Copy Activity</span><span class="sxs-lookup"><span data-stu-id="474a6-177">**Sink** dataset for Copy Activity</span></span>
<span data-ttu-id="474a6-178">Copy Activity copies data from the SQL table to the **filebylookup.csv** file in the **csv** folder in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-178">Copy Activity copies data from the SQL table to the **filebylookup.csv** file in the **csv** folder in Azure Storage.</span></span> <span data-ttu-id="474a6-179">The file is specified by the **AzureStorageLinkedService** property.</span><span class="sxs-lookup"><span data-stu-id="474a6-179">The file is specified by the **AzureStorageLinkedService** property.</span></span> 

```json
{
    "name": "SinkDataset",
    "properties": {
        "type": "AzureBlob",
        "typeProperties": {
            "folderPath": "csv",
            "fileName": "filebylookup.csv",
            "format": {
                "type": "TextFormat"                                                                    
            }
        },
        "linkedServiceName": {
            "referenceName": "AzureStorageLinkedService",
            "type": "LinkedServiceReference"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="474a6-180">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="474a6-180">Azure Storage linked service</span></span>
<span data-ttu-id="474a6-181">This storage account contains the JSON file with the names of the SQL tables.</span><span class="sxs-lookup"><span data-stu-id="474a6-181">This storage account contains the JSON file with the names of the SQL tables.</span></span> 

```json
{
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "value": "DefaultEndpointsProtocol=https;AccountName=<StorageAccountName>;AccountKey=<StorageAccountKey>",
                "type": "SecureString"
            }
        }
    },
        "name": "AzureStorageLinkedService"
}
```

### <a name="azure-sql-database-linked-service"></a><span data-ttu-id="474a6-182">Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="474a6-182">Azure SQL Database linked service</span></span>
<span data-ttu-id="474a6-183">This Azure SQL Database instance contains the data to be copied to Blob storage.</span><span class="sxs-lookup"><span data-stu-id="474a6-183">This Azure SQL Database instance contains the data to be copied to Blob storage.</span></span> 

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": {
                "value": "Server=<server>;Initial Catalog=<database>;User ID=<user>;Password=<password>;",
                "type": "SecureString"
            }
        }
    }
}
```

### <a name="sourcetablejson"></a><span data-ttu-id="474a6-184">sourcetable.json</span><span class="sxs-lookup"><span data-stu-id="474a6-184">sourcetable.json</span></span>

#### <a name="set-of-objects"></a><span data-ttu-id="474a6-185">Set of objects</span><span class="sxs-lookup"><span data-stu-id="474a6-185">Set of objects</span></span>

```json
{
  "Id": "1",
  "tableName": "Table1"
}
{
   "Id": "2",
  "tableName": "Table2"
}
```

#### <a name="array-of-objects"></a><span data-ttu-id="474a6-186">Array of objects</span><span class="sxs-lookup"><span data-stu-id="474a6-186">Array of objects</span></span>

```json
[ 
    {
        "Id": "1",
        "tableName": "Table1"
    },
    {
        "Id": "2",
        "tableName": "Table2"
    }
]
```

## <a name="next-steps"></a><span data-ttu-id="474a6-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="474a6-187">Next steps</span></span>
<span data-ttu-id="474a6-188">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="474a6-188">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="474a6-189">Execute Pipeline activity</span><span class="sxs-lookup"><span data-stu-id="474a6-189">Execute Pipeline activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="474a6-190">ForEach activity</span><span class="sxs-lookup"><span data-stu-id="474a6-190">ForEach activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="474a6-191">GetMetadata activity</span><span class="sxs-lookup"><span data-stu-id="474a6-191">GetMetadata activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="474a6-192">Web activity</span><span class="sxs-lookup"><span data-stu-id="474a6-192">Web activity</span></span>](control-flow-web-activity.md)
