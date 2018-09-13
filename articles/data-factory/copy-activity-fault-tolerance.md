---
title: Fault tolerance of copy activity in Azure Data Factory | Microsoft Docs
description: Learn about how to add fault tolerance to copy activity in Azure Data Factory by skipping the incompatible rows.
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
ms.date: 03/27/2018
ms.author: jingwang
ms.openlocfilehash: 6c76820b39f31d92362295d54984069393fa0dec
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857908"
---
#  <a name="fault-tolerance-of-copy-activity-in-azure-data-factory"></a><span data-ttu-id="37ee5-103">Fault tolerance of copy activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="37ee5-103">Fault tolerance of copy activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-activity-fault-tolerance.md)
> * [Current version](copy-activity-fault-tolerance.md)

<span data-ttu-id="37ee5-106">The copy activity in Azure Data Factory offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span><span class="sxs-lookup"><span data-stu-id="37ee5-106">The copy activity in Azure Data Factory offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="37ee5-107">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span><span class="sxs-lookup"><span data-stu-id="37ee5-107">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="37ee5-108">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span><span class="sxs-lookup"><span data-stu-id="37ee5-108">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="37ee5-109">In addition, you can log the incompatible rows in Azure Blob storage or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="37ee5-109">In addition, you can log the incompatible rows in Azure Blob storage or Azure Data Lake Store.</span></span> <span data-ttu-id="37ee5-110">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span><span class="sxs-lookup"><span data-stu-id="37ee5-110">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="37ee5-111">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="37ee5-111">Supported scenarios</span></span>
<span data-ttu-id="37ee5-112">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span><span class="sxs-lookup"><span data-stu-id="37ee5-112">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="37ee5-113">**Incompatibility between the source data type and the sink native type**.</span><span class="sxs-lookup"><span data-stu-id="37ee5-113">**Incompatibility between the source data type and the sink native type**.</span></span> 

    <span data-ttu-id="37ee5-114">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three INT type columns.</span><span class="sxs-lookup"><span data-stu-id="37ee5-114">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three INT type columns.</span></span> <span data-ttu-id="37ee5-115">The CSV file rows that contain numeric data, such as 123,456,789 are copied successfully to the sink store.</span><span class="sxs-lookup"><span data-stu-id="37ee5-115">The CSV file rows that contain numeric data, such as 123,456,789 are copied successfully to the sink store.</span></span> <span data-ttu-id="37ee5-116">However, the rows that contain non-numeric values, such as 123,456, abc are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="37ee5-116">However, the rows that contain non-numeric values, such as 123,456, abc are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="37ee5-117">**Mismatch in the number of columns between the source and the sink**.</span><span class="sxs-lookup"><span data-stu-id="37ee5-117">**Mismatch in the number of columns between the source and the sink**.</span></span>

    <span data-ttu-id="37ee5-118">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span><span class="sxs-lookup"><span data-stu-id="37ee5-118">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="37ee5-119">The CSV file rows that contain six columns are copied successfully to the sink store.</span><span class="sxs-lookup"><span data-stu-id="37ee5-119">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="37ee5-120">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="37ee5-120">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="37ee5-121">**Primary key violation when writing to SQL Server/Azure SQL Database/Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="37ee5-121">**Primary key violation when writing to SQL Server/Azure SQL Database/Azure Cosmos DB**.</span></span>

    <span data-ttu-id="37ee5-122">For example: Copy data from a SQL server to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="37ee5-122">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="37ee5-123">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span><span class="sxs-lookup"><span data-stu-id="37ee5-123">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="37ee5-124">The duplicated rows that exist in the source cannot be copied to the sink.</span><span class="sxs-lookup"><span data-stu-id="37ee5-124">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="37ee5-125">Copy Activity copies only the first row of the source data into the sink.</span><span class="sxs-lookup"><span data-stu-id="37ee5-125">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="37ee5-126">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="37ee5-126">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

>[!NOTE]
>This feature doesn't apply when copy activity is configured to invoke external data loading mechanism including [Azure SQL Data Warehouse PolyBase](connector-azure-sql-data-warehouse.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) or [Amazon Redshift Unload](connector-amazon-redshift.md#use-unload-to-copy-data-from-amazon-redshift). For loading data into SQL Data Warehouse using PolyBase, use PolyBase's native fault tolerance support by specifying "[polyBaseSettings](connector-azure-sql-data-warehouse.md#azure-sql-data-warehouse-as-sink)" in copy activity.

## <a name="configuration"></a><span data-ttu-id="37ee5-129">Configuration</span><span class="sxs-lookup"><span data-stu-id="37ee5-129">Configuration</span></span>
<span data-ttu-id="37ee5-130">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span><span class="sxs-lookup"><span data-stu-id="37ee5-130">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },
    "enableSkipIncompatibleRow": true,
    "redirectIncompatibleRowSettings": {
         "linkedServiceName": {
              "referenceName": "<Azure Storage or Data Lake Store linked service>",
              "type": "LinkedServiceReference"
            },
            "path": "redirectcontainer/erroroutput"
     }
}
```

<span data-ttu-id="37ee5-131">Property</span><span class="sxs-lookup"><span data-stu-id="37ee5-131">Property</span></span> | <span data-ttu-id="37ee5-132">Description</span><span class="sxs-lookup"><span data-stu-id="37ee5-132">Description</span></span> | <span data-ttu-id="37ee5-133">Allowed values</span><span class="sxs-lookup"><span data-stu-id="37ee5-133">Allowed values</span></span> | <span data-ttu-id="37ee5-134">Required</span><span class="sxs-lookup"><span data-stu-id="37ee5-134">Required</span></span>
-------- | ----------- | -------------- | -------- 
<span data-ttu-id="37ee5-135">enableSkipIncompatibleRow</span><span class="sxs-lookup"><span data-stu-id="37ee5-135">enableSkipIncompatibleRow</span></span> | <span data-ttu-id="37ee5-136">Specifies whether to skip incompatible rows during copy or not.</span><span class="sxs-lookup"><span data-stu-id="37ee5-136">Specifies whether to skip incompatible rows during copy or not.</span></span> | <span data-ttu-id="37ee5-137">True</span><span class="sxs-lookup"><span data-stu-id="37ee5-137">True</span></span><br/><span data-ttu-id="37ee5-138">False (default)</span><span class="sxs-lookup"><span data-stu-id="37ee5-138">False (default)</span></span> | <span data-ttu-id="37ee5-139">No</span><span class="sxs-lookup"><span data-stu-id="37ee5-139">No</span></span>
<span data-ttu-id="37ee5-140">redirectIncompatibleRowSettings</span><span class="sxs-lookup"><span data-stu-id="37ee5-140">redirectIncompatibleRowSettings</span></span> | <span data-ttu-id="37ee5-141">A group of properties that can be specified when you want to log the incompatible rows.</span><span class="sxs-lookup"><span data-stu-id="37ee5-141">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="37ee5-142">No</span><span class="sxs-lookup"><span data-stu-id="37ee5-142">No</span></span>
<span data-ttu-id="37ee5-143">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="37ee5-143">linkedServiceName</span></span> | <span data-ttu-id="37ee5-144">The linked service of [Azure Storage](connector-azure-blob-storage.md#linked-service-properties) or [Azure Data Lake Store](connector-azure-data-lake-store.md#linked-service-properties) to store the log that contains the skipped rows.</span><span class="sxs-lookup"><span data-stu-id="37ee5-144">The linked service of [Azure Storage](connector-azure-blob-storage.md#linked-service-properties) or [Azure Data Lake Store](connector-azure-data-lake-store.md#linked-service-properties) to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="37ee5-145">The name of an `AzureStorage` or `AzureDataLakeStore` type linked service, which refers to the instance that you want to use to store the log file.</span><span class="sxs-lookup"><span data-stu-id="37ee5-145">The name of an `AzureStorage` or `AzureDataLakeStore` type linked service, which refers to the instance that you want to use to store the log file.</span></span> | <span data-ttu-id="37ee5-146">No</span><span class="sxs-lookup"><span data-stu-id="37ee5-146">No</span></span>
<span data-ttu-id="37ee5-147">path</span><span class="sxs-lookup"><span data-stu-id="37ee5-147">path</span></span> | <span data-ttu-id="37ee5-148">The path of the log file that contains the skipped rows.</span><span class="sxs-lookup"><span data-stu-id="37ee5-148">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="37ee5-149">Specify the path that you want to use to log the incompatible data.</span><span class="sxs-lookup"><span data-stu-id="37ee5-149">Specify the path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="37ee5-150">If you do not provide a path, the service creates a container for you.</span><span class="sxs-lookup"><span data-stu-id="37ee5-150">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="37ee5-151">No</span><span class="sxs-lookup"><span data-stu-id="37ee5-151">No</span></span>

## <a name="monitor-skipped-rows"></a><span data-ttu-id="37ee5-152">Monitor skipped rows</span><span class="sxs-lookup"><span data-stu-id="37ee5-152">Monitor skipped rows</span></span>
<span data-ttu-id="37ee5-153">After the copy activity run completes, you can see the number of skipped rows in the output of the copy activity:</span><span class="sxs-lookup"><span data-stu-id="37ee5-153">After the copy activity run completes, you can see the number of skipped rows in the output of the copy activity:</span></span>

```json
"output": {
            "dataRead": 95,
            "dataWritten": 186,
            "rowsCopied": 9,
            "rowsSkipped": 2,
            "copyDuration": 16,
            "throughput": 0.01,
            "redirectRowPath": "https://myblobstorage.blob.core.windows.net//myfolder/a84bf8d4-233f-4216-8cb5-45962831cd1b/",
            "errors": []
        },

```
<span data-ttu-id="37ee5-154">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv`.</span><span class="sxs-lookup"><span data-stu-id="37ee5-154">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv`.</span></span> 

<span data-ttu-id="37ee5-155">The log files can only be the csv files.</span><span class="sxs-lookup"><span data-stu-id="37ee5-155">The log files can only be the csv files.</span></span> <span data-ttu-id="37ee5-156">The original data being skipped will be logged with comma as column delimiter if needed.</span><span class="sxs-lookup"><span data-stu-id="37ee5-156">The original data being skipped will be logged with comma as column delimiter if needed.</span></span> <span data-ttu-id="37ee5-157">We add two more columns "ErrorCode" and "ErrorMessage" in additional to the original source data in log file, where you can see the root cause of the incompatibility.</span><span class="sxs-lookup"><span data-stu-id="37ee5-157">We add two more columns "ErrorCode" and "ErrorMessage" in additional to the original source data in log file, where you can see the root cause of the incompatibility.</span></span> <span data-ttu-id="37ee5-158">The ErrorCode and ErrorMessage will be quoted by double quotes.</span><span class="sxs-lookup"><span data-stu-id="37ee5-158">The ErrorCode and ErrorMessage will be quoted by double quotes.</span></span> 

<span data-ttu-id="37ee5-159">An example of the log file content is as follows:</span><span class="sxs-lookup"><span data-stu-id="37ee5-159">An example of the log file content is as follows:</span></span>

```
data1, data2, data3, "UserErrorInvalidDataValue", "Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'."
data4, data5, data6, "2627", "Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4)."
```

## <a name="next-steps"></a><span data-ttu-id="37ee5-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="37ee5-160">Next steps</span></span>
<span data-ttu-id="37ee5-161">See the other Copy Activity articles:</span><span class="sxs-lookup"><span data-stu-id="37ee5-161">See the other Copy Activity articles:</span></span>

- [<span data-ttu-id="37ee5-162">Copy activity overview</span><span class="sxs-lookup"><span data-stu-id="37ee5-162">Copy activity overview</span></span>](copy-activity-overview.md)
- [<span data-ttu-id="37ee5-163">Copy activity performance</span><span class="sxs-lookup"><span data-stu-id="37ee5-163">Copy activity performance</span></span>](copy-activity-performance.md)


