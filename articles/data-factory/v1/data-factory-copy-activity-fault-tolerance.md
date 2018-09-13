---
title: Add fault tolerance in Azure Data Factory Copy Activity by skipping incompatible rows | Microsoft Docs
description: Learn how to add fault tolerance in Azure Data Factory Copy Activity by skipping incompatible rows during copy
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 03/27/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 5cfab02fc248139c76bd6123ac942832f8e1a21a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865162"
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a><span data-ttu-id="4d7ce-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span><span class="sxs-lookup"><span data-stu-id="4d7ce-103">Add fault tolerance in Copy Activity by skipping incompatible rows</span></span>

> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](data-factory-copy-activity-fault-tolerance.md)
> * [Version 2 (current version)](../copy-activity-fault-tolerance.md)

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [fault tolerance in copy activity of Data Factory](../copy-activity-fault-tolerance.md).

<span data-ttu-id="4d7ce-108">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span><span class="sxs-lookup"><span data-stu-id="4d7ce-108">Azure Data Factory [Copy Activity](data-factory-data-movement-activities.md) offers you two ways to handle incompatible rows when copying data between source and sink data stores:</span></span>

- <span data-ttu-id="4d7ce-109">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span><span class="sxs-lookup"><span data-stu-id="4d7ce-109">You can abort and fail the copy activity when incompatible data is encountered (default behavior).</span></span>
- <span data-ttu-id="4d7ce-110">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-110">You can continue to copy all of the data by adding fault tolerance and skipping incompatible data rows.</span></span> <span data-ttu-id="4d7ce-111">In addition, you can log the incompatible rows in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-111">In addition, you can log the incompatible rows in Azure Blob storage.</span></span> <span data-ttu-id="4d7ce-112">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-112">You can then examine the log to learn the cause for the failure, fix the data on the data source, and retry the copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4d7ce-113">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="4d7ce-113">Supported scenarios</span></span>
<span data-ttu-id="4d7ce-114">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span><span class="sxs-lookup"><span data-stu-id="4d7ce-114">Copy Activity supports three scenarios for detecting, skipping, and logging incompatible data:</span></span>

- <span data-ttu-id="4d7ce-115">**Incompatibility between the source data type and the sink native type**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-115">**Incompatibility between the source data type and the sink native type**</span></span>

    <span data-ttu-id="4d7ce-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-116">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains three **INT** type columns.</span></span> <span data-ttu-id="4d7ce-117">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-117">The CSV file rows that contain numeric data, such as `123,456,789` are copied successfully to the sink store.</span></span> <span data-ttu-id="4d7ce-118">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-118">However, the rows that contain non-numeric values, such as `123,456,abc` are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="4d7ce-119">**Mismatch in the number of columns between the source and the sink**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-119">**Mismatch in the number of columns between the source and the sink**</span></span>

    <span data-ttu-id="4d7ce-120">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-120">For example: Copy data from a CSV file in Blob storage to a SQL database with a schema definition that contains six columns.</span></span> <span data-ttu-id="4d7ce-121">The CSV file rows that contain six columns are copied successfully to the sink store.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-121">The CSV file rows that contain six columns are copied successfully to the sink store.</span></span> <span data-ttu-id="4d7ce-122">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-122">The CSV file rows that contain more or fewer than six columns are detected as incompatible and are skipped.</span></span>

- <span data-ttu-id="4d7ce-123">**Primary key violation when writing to SQL Server/Azure SQL Database/Azure Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-123">**Primary key violation when writing to SQL Server/Azure SQL Database/Azure Cosmos DB**</span></span>

    <span data-ttu-id="4d7ce-124">For example: Copy data from a SQL server to a SQL database.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-124">For example: Copy data from a SQL server to a SQL database.</span></span> <span data-ttu-id="4d7ce-125">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-125">A primary key is defined in the sink SQL database, but no such primary key is defined in the source SQL server.</span></span> <span data-ttu-id="4d7ce-126">The duplicated rows that exist in the source cannot be copied to the sink.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-126">The duplicated rows that exist in the source cannot be copied to the sink.</span></span> <span data-ttu-id="4d7ce-127">Copy Activity copies only the first row of the source data into the sink.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-127">Copy Activity copies only the first row of the source data into the sink.</span></span> <span data-ttu-id="4d7ce-128">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-128">The subsequent source rows that contain the duplicated primary key value are detected as incompatible and are skipped.</span></span>

>[!NOTE]
>This feature doesn't apply when copy activity is configured to invoke external data loading mechanism including [Azure SQL Data Warehouse PolyBase](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) or [Amazon Redshift Unload](data-factory-amazon-redshift-connector.md#use-unload-to-copy-data-from-amazon-redshift). For loading data into SQL Data Warehouse using PolyBase, use PolyBase's native fault tolerance support by specifying "[polyBaseSettings](data-factory-azure-sql-data-warehouse-connector.md#sqldwsink)" in copy activity.

## <a name="configuration"></a><span data-ttu-id="4d7ce-131">Configuration</span><span class="sxs-lookup"><span data-stu-id="4d7ce-131">Configuration</span></span>
<span data-ttu-id="4d7ce-132">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span><span class="sxs-lookup"><span data-stu-id="4d7ce-132">The following example provides a JSON definition to configure skipping the incompatible rows in Copy Activity:</span></span>

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
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| <span data-ttu-id="4d7ce-133">Property</span><span class="sxs-lookup"><span data-stu-id="4d7ce-133">Property</span></span> | <span data-ttu-id="4d7ce-134">Description</span><span class="sxs-lookup"><span data-stu-id="4d7ce-134">Description</span></span> | <span data-ttu-id="4d7ce-135">Allowed values</span><span class="sxs-lookup"><span data-stu-id="4d7ce-135">Allowed values</span></span> | <span data-ttu-id="4d7ce-136">Required</span><span class="sxs-lookup"><span data-stu-id="4d7ce-136">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4d7ce-137">**enableSkipIncompatibleRow**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-137">**enableSkipIncompatibleRow**</span></span> | <span data-ttu-id="4d7ce-138">Enable skipping incompatible rows during copy or not.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-138">Enable skipping incompatible rows during copy or not.</span></span> | <span data-ttu-id="4d7ce-139">True</span><span class="sxs-lookup"><span data-stu-id="4d7ce-139">True</span></span><br/><span data-ttu-id="4d7ce-140">False (default)</span><span class="sxs-lookup"><span data-stu-id="4d7ce-140">False (default)</span></span> | <span data-ttu-id="4d7ce-141">No</span><span class="sxs-lookup"><span data-stu-id="4d7ce-141">No</span></span> |
| <span data-ttu-id="4d7ce-142">**redirectIncompatibleRowSettings**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-142">**redirectIncompatibleRowSettings**</span></span> | <span data-ttu-id="4d7ce-143">A group of properties that can be specified when you want to log the incompatible rows.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-143">A group of properties that can be specified when you want to log the incompatible rows.</span></span> | &nbsp; | <span data-ttu-id="4d7ce-144">No</span><span class="sxs-lookup"><span data-stu-id="4d7ce-144">No</span></span> |
| <span data-ttu-id="4d7ce-145">**linkedServiceName**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-145">**linkedServiceName**</span></span> | <span data-ttu-id="4d7ce-146">The linked service of Azure Storage to store the log that contains the skipped rows.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-146">The linked service of Azure Storage to store the log that contains the skipped rows.</span></span> | <span data-ttu-id="4d7ce-147">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-147">The name of an [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) or [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) linked service, which refers to the storage instance that you want to use to store the log file.</span></span> | <span data-ttu-id="4d7ce-148">No</span><span class="sxs-lookup"><span data-stu-id="4d7ce-148">No</span></span> |
| <span data-ttu-id="4d7ce-149">**path**</span><span class="sxs-lookup"><span data-stu-id="4d7ce-149">**path**</span></span> | <span data-ttu-id="4d7ce-150">The path of the log file that contains the skipped rows.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-150">The path of the log file that contains the skipped rows.</span></span> | <span data-ttu-id="4d7ce-151">Specify the Blob storage path that you want to use to log the incompatible data.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-151">Specify the Blob storage path that you want to use to log the incompatible data.</span></span> <span data-ttu-id="4d7ce-152">If you do not provide a path, the service creates a container for you.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-152">If you do not provide a path, the service creates a container for you.</span></span> | <span data-ttu-id="4d7ce-153">No</span><span class="sxs-lookup"><span data-stu-id="4d7ce-153">No</span></span> |

## <a name="monitoring"></a><span data-ttu-id="4d7ce-154">Monitoring</span><span class="sxs-lookup"><span data-stu-id="4d7ce-154">Monitoring</span></span>
<span data-ttu-id="4d7ce-155">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span><span class="sxs-lookup"><span data-stu-id="4d7ce-155">After the copy activity run completes, you can see the number of skipped rows in the monitoring section:</span></span>

![Monitor skipped incompatible rows](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

<span data-ttu-id="4d7ce-157">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-157">If you configure to log the incompatible rows, you can find the log file at this path: `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` In the log file, you can see the rows that were skipped and the root cause of the incompatibility.</span></span>

<span data-ttu-id="4d7ce-158">Both the original data and the corresponding error are logged in the file.</span><span class="sxs-lookup"><span data-stu-id="4d7ce-158">Both the original data and the corresponding error are logged in the file.</span></span> <span data-ttu-id="4d7ce-159">An example of the log file content is as follows:</span><span class="sxs-lookup"><span data-stu-id="4d7ce-159">An example of the log file content is as follows:</span></span>
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a><span data-ttu-id="4d7ce-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d7ce-160">Next steps</span></span>
<span data-ttu-id="4d7ce-161">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4d7ce-161">To learn more about Azure Data Factory Copy Activity, see [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>
