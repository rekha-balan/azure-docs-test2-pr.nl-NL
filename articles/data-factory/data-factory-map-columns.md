---
title: Mapping dataset columns in Azure Data Factory | Microsoft Docs
description: Learn how to map source columns to destination columns.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: jingwang
ms.openlocfilehash: d0dd51b91a04702e98c7cb4caad5a73d88433934
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549187"
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="84b33-103">Map source dataset columns to destination dataset columns</span><span class="sxs-lookup"><span data-stu-id="84b33-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="84b33-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span><span class="sxs-lookup"><span data-stu-id="84b33-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="84b33-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span><span class="sxs-lookup"><span data-stu-id="84b33-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="84b33-106">Column mapping supports the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="84b33-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="84b33-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span><span class="sxs-lookup"><span data-stu-id="84b33-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="84b33-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span><span class="sxs-lookup"><span data-stu-id="84b33-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="84b33-109">The following are error conditions that result in an exception:</span><span class="sxs-lookup"><span data-stu-id="84b33-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="84b33-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span><span class="sxs-lookup"><span data-stu-id="84b33-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="84b33-111">Duplicate mapping.</span><span class="sxs-lookup"><span data-stu-id="84b33-111">Duplicate mapping.</span></span>
* <span data-ttu-id="84b33-112">SQL query result does not have a column name that is specified in the mapping.</span><span class="sxs-lookup"><span data-stu-id="84b33-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="84b33-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span><span class="sxs-lookup"><span data-stu-id="84b33-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="84b33-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span><span class="sxs-lookup"><span data-stu-id="84b33-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="84b33-115">Sample 1 – column mapping from Azure SQL to Azure blob</span><span class="sxs-lookup"><span data-stu-id="84b33-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="84b33-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="84b33-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

<span data-ttu-id="84b33-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="84b33-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="84b33-118">The following JSON defines a copy activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="84b33-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="84b33-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span><span class="sxs-lookup"><span data-stu-id="84b33-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="84b33-120">**Column mapping flow:**</span><span class="sxs-lookup"><span data-stu-id="84b33-120">**Column mapping flow:**</span></span>

![Column mapping flow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="84b33-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span><span class="sxs-lookup"><span data-stu-id="84b33-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="84b33-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span><span class="sxs-lookup"><span data-stu-id="84b33-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
<span data-ttu-id="84b33-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span><span class="sxs-lookup"><span data-stu-id="84b33-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="84b33-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span><span class="sxs-lookup"><span data-stu-id="84b33-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="84b33-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span><span class="sxs-lookup"><span data-stu-id="84b33-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="84b33-127">**Column mapping flow**</span><span class="sxs-lookup"><span data-stu-id="84b33-127">**Column mapping flow**</span></span>

![Column mapping flow-2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="84b33-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="84b33-129">Next steps</span></span>
<span data-ttu-id="84b33-130">See the article for a tutorial on using Copy Activity:</span><span class="sxs-lookup"><span data-stu-id="84b33-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="84b33-131">Copy data from Blob Storage to SQL Database</span><span class="sxs-lookup"><span data-stu-id="84b33-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)


