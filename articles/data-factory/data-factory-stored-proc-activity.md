---
title: SQL Server Stored Procedure Activity
description: Learn how you can use the SQL Server Stored Procedure Activity to invoke a stored procedure in an Azure SQL Database or Azure SQL Data Warehouse from a Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: spelluru
ms.openlocfilehash: c769de5272ba22b8f0227088ab0ddf8274e0d4f6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660559"
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="c367c-103">SQL Server Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="c367c-103">SQL Server Stored Procedure Activity</span></span>
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Hive Activity](data-factory-hive-activity.md) 
> * [Pig Activity](data-factory-pig-activity.md)
> * [MapReduce Activity](data-factory-map-reduce.md)
> * [Hadoop Streaming Activity](data-factory-hadoop-streaming-activity.md)
> * [Spark Activity](data-factory-spark.md)
> * [Machine Learning Batch Execution Activity](data-factory-azure-ml-batch-execution-activity.md)
> * [Machine Learning Update Resource Activity](data-factory-azure-ml-update-resource-activity.md)
> * [Stored Procedure Activity](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL Activity](data-factory-usql-activity.md)
> * [.NET Custom Activity](data-factory-use-custom-activities.md)

<span data-ttu-id="c367c-114">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span><span class="sxs-lookup"><span data-stu-id="c367c-114">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="c367c-115">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="c367c-115">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="c367c-116">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="c367c-116">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.</span></span>

<span data-ttu-id="c367c-117">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or on an Azure virtual machine (VM).</span><span class="sxs-lookup"><span data-stu-id="c367c-117">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or on an Azure virtual machine (VM).</span></span>  <span data-ttu-id="c367c-118">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span><span class="sxs-lookup"><span data-stu-id="c367c-118">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="c367c-119">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="c367c-119">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="c367c-120">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="c367c-120">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

<span data-ttu-id="c367c-121">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c367c-121">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="c367c-122">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="c367c-122">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="c367c-123">Sample table and stored procedure</span><span class="sxs-lookup"><span data-stu-id="c367c-123">Sample table and stored procedure</span></span>
1. <span data-ttu-id="c367c-124">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span><span class="sxs-lookup"><span data-stu-id="c367c-124">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="c367c-125">The datetimestamp column is the date and time when the corresponding ID is generated.</span><span class="sxs-lookup"><span data-stu-id="c367c-125">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

    ```SQL
    CREATE TABLE dbo.sampletable
    (
        Id uniqueidentifier,
        datetimestamp nvarchar(127)
    )
    GO

    CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable(Id);
    GO
    ```
    <span data-ttu-id="c367c-126">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span><span class="sxs-lookup"><span data-stu-id="c367c-126">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="c367c-128">In this sample, the stored procedure is in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c367c-128">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="c367c-129">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span><span class="sxs-lookup"><span data-stu-id="c367c-129">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="c367c-130">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="c367c-130">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="c367c-131">Create the following **stored procedure** that inserts data in to the **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="c367c-131">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

    ```SQL
    CREATE PROCEDURE sp_sample @DateTime nvarchar(127)
    AS

    BEGIN
        INSERT INTO [sampletable]
        VALUES (newid(), @DateTime)
    END
    ```

   > [!IMPORTANT]
   > **Name** and **casing** of the parameter (DateTime in this example) must match that of parameter specified in the pipeline/activity JSON. In the stored procedure definition, ensure that **@** is used as a prefix for the parameter.

### <a name="create-a-data-factory"></a><span data-ttu-id="c367c-134">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="c367c-134">Create a data factory</span></span>
1. <span data-ttu-id="c367c-135">Log in to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c367c-135">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c367c-136">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c367c-136">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![New data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="c367c-138">In the **New data factory** blade, enter **SProcDF** for the Name.</span><span class="sxs-lookup"><span data-stu-id="c367c-138">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="c367c-139">Azure Data Factory names are **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="c367c-139">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="c367c-140">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span><span class="sxs-lookup"><span data-stu-id="c367c-140">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![New data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="c367c-142">Select your **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="c367c-142">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="c367c-143">For **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="c367c-143">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="c367c-144">Click **Create new** and enter a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="c367c-144">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="c367c-145">Click **Use existing** and select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="c367c-145">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="c367c-146">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="c367c-146">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="c367c-147">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span><span class="sxs-lookup"><span data-stu-id="c367c-147">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="c367c-148">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="c367c-148">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="c367c-149">You see the data factory being created in the **dashboard** of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c367c-149">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="c367c-150">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="c367c-150">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="c367c-152">Create an Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="c367c-152">Create an Azure SQL linked service</span></span>
<span data-ttu-id="c367c-153">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL Database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="c367c-153">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL Database to the data factory.</span></span> <span data-ttu-id="c367c-154">This database contains the sampletable table and sp_sample stored procedure.</span><span class="sxs-lookup"><span data-stu-id="c367c-154">This database contains the sampletable table and sp_sample stored procedure.</span></span>

1. <span data-ttu-id="c367c-155">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="c367c-155">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="c367c-156">Click **New data store** on the command bar and choose **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="c367c-156">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="c367c-157">You should see the JSON script for creating an Azure SQL linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="c367c-157">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![New data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="c367c-159">In the JSON script, make the following changes:</span><span class="sxs-lookup"><span data-stu-id="c367c-159">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="c367c-160">Replace `<servername>` with the name of your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="c367c-160">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="c367c-161">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="c367c-161">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="c367c-162">Replace `<username@servername>` with the user account that has access to the database.</span><span class="sxs-lookup"><span data-stu-id="c367c-162">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="c367c-163">Replace `<password>` with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="c367c-163">Replace `<password>` with the password for the user account.</span></span>

      ![New data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="c367c-165">To deploy the linked service, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="c367c-165">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="c367c-166">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="c367c-166">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![tree view with linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="c367c-168">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="c367c-168">Create an output dataset</span></span>
1. <span data-ttu-id="c367c-169">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="c367c-169">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="c367c-170">**New dataset** on the command bar and select **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="c367c-170">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![tree view with linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="c367c-172">Copy/paste the following JSON script in to the JSON editor.</span><span class="sxs-lookup"><span data-stu-id="c367c-172">Copy/paste the following JSON script in to the JSON editor.</span></span>

    ```JSON
    {                
        "name": "sprocsampleout",
        "properties": {
            "type": "AzureSqlTable",
            "linkedServiceName": "AzureSqlLinkedService",
            "typeProperties": {
                "tableName": "sampletable"
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="c367c-173">To deploy the dataset, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="c367c-173">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="c367c-174">Confirm that you see the dataset in the tree view.</span><span class="sxs-lookup"><span data-stu-id="c367c-174">Confirm that you see the dataset in the tree view.</span></span>

    ![tree view with linked services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="c367c-176">Create a pipeline with SqlServerStoredProcedure activity</span><span class="sxs-lookup"><span data-stu-id="c367c-176">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="c367c-177">Now, let's create a pipeline with a SqlServerStoredProcedure activity.</span><span class="sxs-lookup"><span data-stu-id="c367c-177">Now, let's create a pipeline with a SqlServerStoredProcedure activity.</span></span>

1. <span data-ttu-id="c367c-178">Click **... More** on the command bar and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c367c-178">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="c367c-179">Copy/paste the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="c367c-179">Copy/paste the following JSON snippet:</span></span>   

    ```JSON
    {
        "name": "SprocActivitySamplePipeline",
        "properties": {
            "activities": [
                {
                    "type": "SqlServerStoredProcedure",
                    "typeProperties": {
                        "storedProcedureName": "sp_sample",
                        "storedProcedureParameters": {
                            "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                        }
                    },
                    "outputs": [
                        {
                            "name": "sprocsampleout"
                        }
                    ],
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                    },
                    "name": "SprocActivitySample"
                }
            ],
             "start": "2016-08-02T00:00:00Z",
             "end": "2016-08-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="c367c-180">The **storedProcedureName** set to **sp_sample**.</span><span class="sxs-lookup"><span data-stu-id="c367c-180">The **storedProcedureName** set to **sp_sample**.</span></span> <span data-ttu-id="c367c-181">Name and casing of the parameter **DateTime** must match the name and casing of the parameter in the stored procedure definition.</span><span class="sxs-lookup"><span data-stu-id="c367c-181">Name and casing of the parameter **DateTime** must match the name and casing of the parameter in the stored procedure definition.</span></span>

    <span data-ttu-id="c367c-182">If you need pass null for a parameter, use the syntax: "param1": null (all lowercase).</span><span class="sxs-lookup"><span data-stu-id="c367c-182">If you need pass null for a parameter, use the syntax: "param1": null (all lowercase).</span></span>
3. <span data-ttu-id="c367c-183">To deploy the pipeline, click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="c367c-183">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="c367c-184">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="c367c-184">Monitor the pipeline</span></span>
1. <span data-ttu-id="c367c-185">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="c367c-185">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="c367c-187">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="c367c-187">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="c367c-189">In the Diagram View, double-click the dataset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="c367c-189">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="c367c-190">You see the slices in Ready state.</span><span class="sxs-lookup"><span data-stu-id="c367c-190">You see the slices in Ready state.</span></span> <span data-ttu-id="c367c-191">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span><span class="sxs-lookup"><span data-stu-id="c367c-191">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="c367c-193">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="c367c-193">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="c367c-195">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="c367c-195">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  

> [!NOTE]
> In this example, the SprocActivitySample has no inputs. If you want to chain this activity with an activity upstream (that is, prior processing), the outputs of the upstream activity can be used as inputs in this activity. In such a case, this activity does not execute until the upstream activity is completed and the outputs of the upstream activities are available (in Ready status). The inputs cannot be used directly as a parameter to the stored procedure activity
>
>

## <a name="json-format"></a><span data-ttu-id="c367c-200">JSON format</span><span class="sxs-lookup"><span data-stu-id="c367c-200">JSON format</span></span>
<span data-ttu-id="c367c-201">Here is the JSON format for defining a Stored Procedure Activity:</span><span class="sxs-lookup"><span data-stu-id="c367c-201">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

```JSON
{
    "name": "SQLSPROCActivity",
    "description": "description",
    "type": "SqlServerStoredProcedure",
    "inputs":  [ { "name": "inputtable"  } ],
    "outputs":  [ { "name": "outputtable" } ],
    "typeProperties":
    {
        "storedProcedureName": "<name of the stored procedure>",
        "storedProcedureParameters":  
        {
            "param1": "param1Value"
            …
        }
    }
}
```

## <a name="json-properties"></a><span data-ttu-id="c367c-202">JSON properties</span><span class="sxs-lookup"><span data-stu-id="c367c-202">JSON properties</span></span>
| <span data-ttu-id="c367c-203">Property</span><span class="sxs-lookup"><span data-stu-id="c367c-203">Property</span></span> | <span data-ttu-id="c367c-204">Description</span><span class="sxs-lookup"><span data-stu-id="c367c-204">Description</span></span> | <span data-ttu-id="c367c-205">Required</span><span class="sxs-lookup"><span data-stu-id="c367c-205">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c367c-206">name</span><span class="sxs-lookup"><span data-stu-id="c367c-206">name</span></span> | <span data-ttu-id="c367c-207">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="c367c-207">Name of the activity</span></span> |<span data-ttu-id="c367c-208">Yes</span><span class="sxs-lookup"><span data-stu-id="c367c-208">Yes</span></span> |
| <span data-ttu-id="c367c-209">description</span><span class="sxs-lookup"><span data-stu-id="c367c-209">description</span></span> |<span data-ttu-id="c367c-210">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="c367c-210">Text describing what the activity is used for</span></span> |<span data-ttu-id="c367c-211">No</span><span class="sxs-lookup"><span data-stu-id="c367c-211">No</span></span> |
| <span data-ttu-id="c367c-212">type</span><span class="sxs-lookup"><span data-stu-id="c367c-212">type</span></span> | <span data-ttu-id="c367c-213">Must be set to: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="c367c-213">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="c367c-214">Yes</span><span class="sxs-lookup"><span data-stu-id="c367c-214">Yes</span></span> |
| <span data-ttu-id="c367c-215">inputs</span><span class="sxs-lookup"><span data-stu-id="c367c-215">inputs</span></span> | <span data-ttu-id="c367c-216">Optional.</span><span class="sxs-lookup"><span data-stu-id="c367c-216">Optional.</span></span> <span data-ttu-id="c367c-217">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span><span class="sxs-lookup"><span data-stu-id="c367c-217">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="c367c-218">The input dataset cannot be consumed in the stored procedure as a parameter.</span><span class="sxs-lookup"><span data-stu-id="c367c-218">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="c367c-219">It is only used to check the dependency before starting the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="c367c-219">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="c367c-220">No</span><span class="sxs-lookup"><span data-stu-id="c367c-220">No</span></span> |
| <span data-ttu-id="c367c-221">outputs</span><span class="sxs-lookup"><span data-stu-id="c367c-221">outputs</span></span> | <span data-ttu-id="c367c-222">You must specify an output dataset for a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="c367c-222">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="c367c-223">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span><span class="sxs-lookup"><span data-stu-id="c367c-223">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="c367c-224">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span><span class="sxs-lookup"><span data-stu-id="c367c-224">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="c367c-225">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#run-activities-in-a-sequence)) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c367c-225">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#run-activities-in-a-sequence)) in the pipeline.</span></span> <span data-ttu-id="c367c-226">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span><span class="sxs-lookup"><span data-stu-id="c367c-226">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="c367c-227">It is the stored procedure that writes to a SQL table that the output dataset points to.</span><span class="sxs-lookup"><span data-stu-id="c367c-227">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="c367c-228">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="c367c-228">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="c367c-229">Yes</span><span class="sxs-lookup"><span data-stu-id="c367c-229">Yes</span></span> |
| <span data-ttu-id="c367c-230">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="c367c-230">storedProcedureName</span></span> |<span data-ttu-id="c367c-231">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span><span class="sxs-lookup"><span data-stu-id="c367c-231">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="c367c-232">Yes</span><span class="sxs-lookup"><span data-stu-id="c367c-232">Yes</span></span> |
| <span data-ttu-id="c367c-233">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="c367c-233">storedProcedureParameters</span></span> |<span data-ttu-id="c367c-234">Specify values for stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="c367c-234">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="c367c-235">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span><span class="sxs-lookup"><span data-stu-id="c367c-235">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="c367c-236">See the following sample to learn about using this property.</span><span class="sxs-lookup"><span data-stu-id="c367c-236">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="c367c-237">No</span><span class="sxs-lookup"><span data-stu-id="c367c-237">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="c367c-238">Passing a static value</span><span class="sxs-lookup"><span data-stu-id="c367c-238">Passing a static value</span></span>
<span data-ttu-id="c367c-239">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span><span class="sxs-lookup"><span data-stu-id="c367c-239">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Sample data 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="c367c-241">**Table:**</span><span class="sxs-lookup"><span data-stu-id="c367c-241">**Table:**</span></span>

```SQL
CREATE TABLE dbo.sampletable2
(
    Id uniqueidentifier,
    datetimestamp nvarchar(127),
    scenario nvarchar(127)
)
GO

CREATE CLUSTERED INDEX ClusteredID ON dbo.sampletable2(Id);
```

<span data-ttu-id="c367c-242">**Stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="c367c-242">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="c367c-243">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="c367c-243">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="c367c-244">The **typeProperties** section in the preceding sample looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="c367c-244">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

```JSON
"typeProperties":
{
    "storedProcedureName": "sp_sample",
    "storedProcedureParameters":
    {
        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
        "Scenario": "Document sample"
    }
}
```

<span data-ttu-id="c367c-245">**Data Factory dataset:**</span><span class="sxs-lookup"><span data-stu-id="c367c-245">**Data Factory dataset:**</span></span>

```JSON
{
    "name": "sprocsampleout2",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "sampletable2"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="c367c-246">**Data Factory pipeline**</span><span class="sxs-lookup"><span data-stu-id="c367c-246">**Data Factory pipeline**</span></span>

```JSON
{
    "name": "SprocActivitySamplePipeline2",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample2",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)",
                        "Scenario": "Document sample"
                    }
                },
                "outputs": [
                    {
                        "name": "sprocsampleout2"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
        "start": "2016-10-02T00:00:00Z",
        "end": "2016-10-02T05:00:00Z"
    }
}
```













