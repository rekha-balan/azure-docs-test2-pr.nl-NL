---
title: Transform data by using the Stored Procedure activity in Azure Data Factory | Microsoft Docs
description: Explains how to use SQL Server Stored Procedure Activity to invoke a stored procedure in an Azure SQL Database/Data Warehouse from a Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: douglasl
ms.openlocfilehash: e8e0f8352404892ea8af6a0fa176c336dd2c1659
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968546"
---
# <a name="transform-data-by-using-the-sql-server-stored-procedure-activity-in-azure-data-factory"></a><span data-ttu-id="68168-103">Transform data by using the SQL Server Stored Procedure activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="68168-103">Transform data by using the SQL Server Stored Procedure activity in Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-stored-proc-activity.md)
> * [Current version](transform-data-using-stored-procedure.md)

<span data-ttu-id="68168-106">You use data transformation activities in a Data Factory [pipeline](concepts-pipelines-activities.md) to transform and process raw data into predictions and insights.</span><span class="sxs-lookup"><span data-stu-id="68168-106">You use data transformation activities in a Data Factory [pipeline](concepts-pipelines-activities.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="68168-107">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="68168-107">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="68168-108">This article builds on the [transform data](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="68168-108">This article builds on the [transform data](transform-data.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

> [!NOTE]
> If you are new to Azure Data Factory, read through [Introduction to Azure Data Factory](introduction.md) and do the tutorial: [Tutorial: transform data](tutorial-transform-data-spark-powershell.md) before reading this article. 

<span data-ttu-id="68168-110">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span><span class="sxs-lookup"><span data-stu-id="68168-110">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="68168-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="68168-111">Azure SQL Database</span></span>
- <span data-ttu-id="68168-112">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="68168-112">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="68168-113">SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="68168-113">SQL Server Database.</span></span>  <span data-ttu-id="68168-114">If you are using SQL Server, install Self-hosted integration runtime on the same machine that hosts the database or on a separate machine that has access to the database.</span><span class="sxs-lookup"><span data-stu-id="68168-114">If you are using SQL Server, install Self-hosted integration runtime on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="68168-115">Self-Hosted integration runtime is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="68168-115">Self-Hosted integration runtime is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="68168-116">See [Self-hosted integration runtime](create-self-hosted-integration-runtime.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="68168-116">See [Self-hosted integration runtime](create-self-hosted-integration-runtime.md) article for details.</span></span>

> [!IMPORTANT]
> When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property. For details about the property, see following connector articles: [Azure SQL Database](connector-azure-sql-database.md), [SQL Server](connector-sql-server.md). Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported. But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse. 
>
> When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property. For more information, see the following connector articles: [Azure SQL Database](connector-azure-sql-database.md), [SQL Server](connector-sql-server.md), [Azure SQL Data Warehouse](connector-azure-sql-data-warehouse.md)          

 

## <a name="syntax-details"></a><span data-ttu-id="68168-123">Syntax details</span><span class="sxs-lookup"><span data-stu-id="68168-123">Syntax details</span></span>
<span data-ttu-id="68168-124">Here is the JSON format for defining a Stored Procedure Activity:</span><span class="sxs-lookup"><span data-stu-id="68168-124">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```json
{
    "name": "Stored Procedure Activity",
    "description":"Description",
    "type": "SqlServerStoredProcedure",
    "linkedServiceName": {
        "referenceName": "AzureSqlLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "storedProcedureName": "sp_sample",
        "storedProcedureParameters": {
            "identifier": { "value": "1", "type": "Int" },
            "stringData": { "value": "str1" }

        }
    }
}
```

<span data-ttu-id="68168-125">The following table describes these JSON properties:</span><span class="sxs-lookup"><span data-stu-id="68168-125">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="68168-126">Property</span><span class="sxs-lookup"><span data-stu-id="68168-126">Property</span></span>                  | <span data-ttu-id="68168-127">Description</span><span class="sxs-lookup"><span data-stu-id="68168-127">Description</span></span>                              | <span data-ttu-id="68168-128">Required</span><span class="sxs-lookup"><span data-stu-id="68168-128">Required</span></span> |
| ------------------------- | ---------------------------------------- | -------- |
| <span data-ttu-id="68168-129">name</span><span class="sxs-lookup"><span data-stu-id="68168-129">name</span></span>                      | <span data-ttu-id="68168-130">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="68168-130">Name of the activity</span></span>                     | <span data-ttu-id="68168-131">Yes</span><span class="sxs-lookup"><span data-stu-id="68168-131">Yes</span></span>      |
| <span data-ttu-id="68168-132">description</span><span class="sxs-lookup"><span data-stu-id="68168-132">description</span></span>               | <span data-ttu-id="68168-133">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="68168-133">Text describing what the activity is used for</span></span> | <span data-ttu-id="68168-134">No</span><span class="sxs-lookup"><span data-stu-id="68168-134">No</span></span>       |
| <span data-ttu-id="68168-135">type</span><span class="sxs-lookup"><span data-stu-id="68168-135">type</span></span>                      | <span data-ttu-id="68168-136">For Stored Procedure Activity, the activity type is **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="68168-136">For Stored Procedure Activity, the activity type is **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="68168-137">Yes</span><span class="sxs-lookup"><span data-stu-id="68168-137">Yes</span></span>      |
| <span data-ttu-id="68168-138">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="68168-138">linkedServiceName</span></span>         | <span data-ttu-id="68168-139">Reference to the **Azure SQL Database** or **Azure SQL Data Warehouse** or **SQL Server** registered as a linked service in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="68168-139">Reference to the **Azure SQL Database** or **Azure SQL Data Warehouse** or **SQL Server** registered as a linked service in Data Factory.</span></span> <span data-ttu-id="68168-140">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="68168-140">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="68168-141">Yes</span><span class="sxs-lookup"><span data-stu-id="68168-141">Yes</span></span>      |
| <span data-ttu-id="68168-142">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="68168-142">storedProcedureName</span></span>       | <span data-ttu-id="68168-143">Specify the name of the stored procedure to invoke.</span><span class="sxs-lookup"><span data-stu-id="68168-143">Specify the name of the stored procedure to invoke.</span></span> | <span data-ttu-id="68168-144">Yes</span><span class="sxs-lookup"><span data-stu-id="68168-144">Yes</span></span>      |
| <span data-ttu-id="68168-145">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="68168-145">storedProcedureParameters</span></span> | <span data-ttu-id="68168-146">Specify the values for stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="68168-146">Specify the values for stored procedure parameters.</span></span> <span data-ttu-id="68168-147">Use `"param1": { "value": "param1Value","type":"param1Type" }` to pass parameter values and their type supported by the data source.</span><span class="sxs-lookup"><span data-stu-id="68168-147">Use `"param1": { "value": "param1Value","type":"param1Type" }` to pass parameter values and their type supported by the data source.</span></span> <span data-ttu-id="68168-148">If you need to pass null for a parameter, use `"param1": { "value": null }` (all lower case).</span><span class="sxs-lookup"><span data-stu-id="68168-148">If you need to pass null for a parameter, use `"param1": { "value": null }` (all lower case).</span></span> | <span data-ttu-id="68168-149">No</span><span class="sxs-lookup"><span data-stu-id="68168-149">No</span></span>       |

## <a name="next-steps"></a><span data-ttu-id="68168-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="68168-150">Next steps</span></span>
<span data-ttu-id="68168-151">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="68168-151">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="68168-152">U-SQL Activity</span><span class="sxs-lookup"><span data-stu-id="68168-152">U-SQL Activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="68168-153">Hive Activity</span><span class="sxs-lookup"><span data-stu-id="68168-153">Hive Activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="68168-154">Pig Activity</span><span class="sxs-lookup"><span data-stu-id="68168-154">Pig Activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="68168-155">MapReduce Activity</span><span class="sxs-lookup"><span data-stu-id="68168-155">MapReduce Activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="68168-156">Hadoop Streaming Activity</span><span class="sxs-lookup"><span data-stu-id="68168-156">Hadoop Streaming Activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="68168-157">Spark Activity</span><span class="sxs-lookup"><span data-stu-id="68168-157">Spark Activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="68168-158">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="68168-158">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="68168-159">Machine Learning Bach Execution Activity</span><span class="sxs-lookup"><span data-stu-id="68168-159">Machine Learning Bach Execution Activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="68168-160">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="68168-160">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
