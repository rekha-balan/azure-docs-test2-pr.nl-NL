---
title: SQL Server Stored Procedure Activity
description: Learn how you can use the SQL Server Stored Procedure Activity to invoke a stored procedure in an Azure SQL Database or Azure SQL Data Warehouse from a Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.assetid: 1c46ed69-4049-44ec-9b46-e90e964a4a8e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: douglasl
robots: noindex
ms.openlocfilehash: b10fbd953eb9ca904043973ebc1f7c6adb9f9abc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865860"
---
# <a name="sql-server-stored-procedure-activity"></a><span data-ttu-id="f692c-103">SQL Server Stored Procedure Activity</span><span class="sxs-lookup"><span data-stu-id="f692c-103">SQL Server Stored Procedure Activity</span></span>
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

> [!NOTE]
> This article applies to version 1 of Azure Data Factory. If you are using the current version of the Data Factory service, see [transform data using stored procedure activity in Data Factory](../transform-data-using-stored-procedure.md).

## <a name="overview"></a><span data-ttu-id="f692c-116">Overview</span><span class="sxs-lookup"><span data-stu-id="f692c-116">Overview</span></span>
<span data-ttu-id="f692c-117">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span><span class="sxs-lookup"><span data-stu-id="f692c-117">You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights.</span></span> <span data-ttu-id="f692c-118">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span><span class="sxs-lookup"><span data-stu-id="f692c-118">The Stored Procedure Activity is one of the transformation activities that Data Factory supports.</span></span> <span data-ttu-id="f692c-119">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f692c-119">This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities in Data Factory.</span></span>

<span data-ttu-id="f692c-120">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span><span class="sxs-lookup"><span data-stu-id="f692c-120">You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores in your enterprise or on an Azure virtual machine (VM):</span></span> 

- <span data-ttu-id="f692c-121">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="f692c-121">Azure SQL Database</span></span>
- <span data-ttu-id="f692c-122">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f692c-122">Azure SQL Data Warehouse</span></span>
- <span data-ttu-id="f692c-123">SQL Server Database.</span><span class="sxs-lookup"><span data-stu-id="f692c-123">SQL Server Database.</span></span>  <span data-ttu-id="f692c-124">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span><span class="sxs-lookup"><span data-stu-id="f692c-124">If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database.</span></span> <span data-ttu-id="f692c-125">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span><span class="sxs-lookup"><span data-stu-id="f692c-125">Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way.</span></span> <span data-ttu-id="f692c-126">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="f692c-126">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.</span></span>

> [!IMPORTANT]
> When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property. For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md). For details about the property, see following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). Invoking a stored procedure while copying data into an Azure SQL Data Warehouse by using a copy activity is not supported. But, you can use the stored procedure activity to invoke a stored procedure in a SQL Data Warehouse. 
>  
> When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property. For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          


<span data-ttu-id="f692c-134">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="f692c-134">The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database.</span></span> 

## <a name="walkthrough"></a><span data-ttu-id="f692c-135">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="f692c-135">Walkthrough</span></span>
### <a name="sample-table-and-stored-procedure"></a><span data-ttu-id="f692c-136">Sample table and stored procedure</span><span class="sxs-lookup"><span data-stu-id="f692c-136">Sample table and stored procedure</span></span>
1. <span data-ttu-id="f692c-137">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span><span class="sxs-lookup"><span data-stu-id="f692c-137">Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with.</span></span> <span data-ttu-id="f692c-138">The datetimestamp column is the date and time when the corresponding ID is generated.</span><span class="sxs-lookup"><span data-stu-id="f692c-138">The datetimestamp column is the date and time when the corresponding ID is generated.</span></span>

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
    <span data-ttu-id="f692c-139">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span><span class="sxs-lookup"><span data-stu-id="f692c-139">Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.</span></span>
    
    ![Sample data](./media/data-factory-stored-proc-activity/sample-data.png)

    <span data-ttu-id="f692c-141">In this sample, the stored procedure is in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="f692c-141">In this sample, the stored procedure is in an Azure SQL Database.</span></span> <span data-ttu-id="f692c-142">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span><span class="sxs-lookup"><span data-stu-id="f692c-142">If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar.</span></span> <span data-ttu-id="f692c-143">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f692c-143">For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).</span></span>
2. <span data-ttu-id="f692c-144">Create the following **stored procedure** that inserts data in to the **sampletable**.</span><span class="sxs-lookup"><span data-stu-id="f692c-144">Create the following **stored procedure** that inserts data in to the **sampletable**.</span></span>

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

### <a name="create-a-data-factory"></a><span data-ttu-id="f692c-147">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f692c-147">Create a data factory</span></span>
1. <span data-ttu-id="f692c-148">Log in to [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f692c-148">Log in to [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f692c-149">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="f692c-149">Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.</span></span>

    ![New data factory](media/data-factory-stored-proc-activity/new-data-factory.png)    
3. <span data-ttu-id="f692c-151">In the **New data factory** blade, enter **SProcDF** for the Name.</span><span class="sxs-lookup"><span data-stu-id="f692c-151">In the **New data factory** blade, enter **SProcDF** for the Name.</span></span> <span data-ttu-id="f692c-152">Azure Data Factory names are **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="f692c-152">Azure Data Factory names are **globally unique**.</span></span> <span data-ttu-id="f692c-153">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span><span class="sxs-lookup"><span data-stu-id="f692c-153">You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.</span></span>

   ![New data factory](media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. <span data-ttu-id="f692c-155">Select your **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f692c-155">Select your **Azure subscription**.</span></span>
5. <span data-ttu-id="f692c-156">For **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="f692c-156">For **Resource Group**, do one of the following steps:</span></span>
   1. <span data-ttu-id="f692c-157">Click **Create new** and enter a name for the resource group.</span><span class="sxs-lookup"><span data-stu-id="f692c-157">Click **Create new** and enter a name for the resource group.</span></span>
   2. <span data-ttu-id="f692c-158">Click **Use existing** and select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="f692c-158">Click **Use existing** and select an existing resource group.</span></span>  
6. <span data-ttu-id="f692c-159">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="f692c-159">Select the **location** for the data factory.</span></span>
7. <span data-ttu-id="f692c-160">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span><span class="sxs-lookup"><span data-stu-id="f692c-160">Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.</span></span>
8. <span data-ttu-id="f692c-161">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="f692c-161">Click **Create** on the **New data factory** blade.</span></span>
9. <span data-ttu-id="f692c-162">You see the data factory being created in the **dashboard** of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f692c-162">You see the data factory being created in the **dashboard** of the Azure portal.</span></span> <span data-ttu-id="f692c-163">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="f692c-163">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![Data Factory home page](media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a><span data-ttu-id="f692c-165">Create an Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="f692c-165">Create an Azure SQL linked service</span></span>
<span data-ttu-id="f692c-166">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span><span class="sxs-lookup"><span data-stu-id="f692c-166">After creating the data factory, you create an Azure SQL linked service that links your Azure SQL database, which contains the sampletable table and sp_sample stored procedure, to your data factory.</span></span>

1. <span data-ttu-id="f692c-167">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="f692c-167">Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.</span></span>
2. <span data-ttu-id="f692c-168">Click **New data store** on the command bar and choose **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="f692c-168">Click **New data store** on the command bar and choose **Azure SQL Database**.</span></span> <span data-ttu-id="f692c-169">You should see the JSON script for creating an Azure SQL linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="f692c-169">You should see the JSON script for creating an Azure SQL linked service in the editor.</span></span>

   ![New data store](media/data-factory-stored-proc-activity/new-data-store.png)
3. <span data-ttu-id="f692c-171">In the JSON script, make the following changes:</span><span class="sxs-lookup"><span data-stu-id="f692c-171">In the JSON script, make the following changes:</span></span>

   1. <span data-ttu-id="f692c-172">Replace `<servername>` with the name of your Azure SQL Database server.</span><span class="sxs-lookup"><span data-stu-id="f692c-172">Replace `<servername>` with the name of your Azure SQL Database server.</span></span>
   2. <span data-ttu-id="f692c-173">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f692c-173">Replace `<databasename>` with the database in which you created the table and the stored procedure.</span></span>
   3. <span data-ttu-id="f692c-174">Replace `<username@servername>` with the user account that has access to the database.</span><span class="sxs-lookup"><span data-stu-id="f692c-174">Replace `<username@servername>` with the user account that has access to the database.</span></span>
   4. <span data-ttu-id="f692c-175">Replace `<password>` with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="f692c-175">Replace `<password>` with the password for the user account.</span></span>

      ![New data store](media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. <span data-ttu-id="f692c-177">To deploy the linked service, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f692c-177">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="f692c-178">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span><span class="sxs-lookup"><span data-stu-id="f692c-178">Confirm that you see the AzureSqlLinkedService in the tree view on the left.</span></span>

    ![tree view with linked service](media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a><span data-ttu-id="f692c-180">Create an output dataset</span><span class="sxs-lookup"><span data-stu-id="f692c-180">Create an output dataset</span></span>
<span data-ttu-id="f692c-181">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span><span class="sxs-lookup"><span data-stu-id="f692c-181">You must specify an output dataset for a stored procedure activity even if the stored procedure does not produce any data.</span></span> <span data-ttu-id="f692c-182">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span><span class="sxs-lookup"><span data-stu-id="f692c-182">That's because it's the output dataset that drives the schedule of the activity (how often the activity is run - hourly, daily, etc.).</span></span> <span data-ttu-id="f692c-183">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span><span class="sxs-lookup"><span data-stu-id="f692c-183">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <span data-ttu-id="f692c-184">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f692c-184">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="f692c-185">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span><span class="sxs-lookup"><span data-stu-id="f692c-185">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="f692c-186">It is the stored procedure that writes to a SQL table that the output dataset points to.</span><span class="sxs-lookup"><span data-stu-id="f692c-186">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <span data-ttu-id="f692c-187">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span><span class="sxs-lookup"><span data-stu-id="f692c-187">In some cases, the output dataset can be a **dummy dataset** (a dataset that points to a table that does not really hold output of the stored procedure).</span></span> <span data-ttu-id="f692c-188">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-188">This dummy dataset is used only to specify the schedule for running the stored procedure activity.</span></span> 

1. <span data-ttu-id="f692c-189">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="f692c-189">Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**.</span></span> <span data-ttu-id="f692c-190">**New dataset** on the command bar and select **Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="f692c-190">**New dataset** on the command bar and select **Azure SQL**.</span></span>

    ![tree view with linked service](media/data-factory-stored-proc-activity/new-dataset.png)
2. <span data-ttu-id="f692c-192">Copy/paste the following JSON script in to the JSON editor.</span><span class="sxs-lookup"><span data-stu-id="f692c-192">Copy/paste the following JSON script in to the JSON editor.</span></span>

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
3. <span data-ttu-id="f692c-193">To deploy the dataset, click **Deploy** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="f692c-193">To deploy the dataset, click **Deploy** on the command bar.</span></span> <span data-ttu-id="f692c-194">Confirm that you see the dataset in the tree view.</span><span class="sxs-lookup"><span data-stu-id="f692c-194">Confirm that you see the dataset in the tree view.</span></span>

    ![tree view with linked services](media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a><span data-ttu-id="f692c-196">Create a pipeline with SqlServerStoredProcedure activity</span><span class="sxs-lookup"><span data-stu-id="f692c-196">Create a pipeline with SqlServerStoredProcedure activity</span></span>
<span data-ttu-id="f692c-197">Now, let's create a pipeline with a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-197">Now, let's create a pipeline with a stored procedure activity.</span></span> 

<span data-ttu-id="f692c-198">Notice the following properties:</span><span class="sxs-lookup"><span data-stu-id="f692c-198">Notice the following properties:</span></span> 

- <span data-ttu-id="f692c-199">The **type** property is set to **SqlServerStoredProcedure**.</span><span class="sxs-lookup"><span data-stu-id="f692c-199">The **type** property is set to **SqlServerStoredProcedure**.</span></span> 
- <span data-ttu-id="f692c-200">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span><span class="sxs-lookup"><span data-stu-id="f692c-200">The **storedProcedureName** in type properties is set to **sp_sample** (name of the stored procedure).</span></span>
- <span data-ttu-id="f692c-201">The **storedProcedureParameters** section contains one parameter named **DateTime**.</span><span class="sxs-lookup"><span data-stu-id="f692c-201">The **storedProcedureParameters** section contains one parameter named **DateTime**.</span></span> <span data-ttu-id="f692c-202">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span><span class="sxs-lookup"><span data-stu-id="f692c-202">Name and casing of the parameter in JSON must match the name and casing of the parameter in the stored procedure definition.</span></span> <span data-ttu-id="f692c-203">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span><span class="sxs-lookup"><span data-stu-id="f692c-203">If you need pass null for a parameter, use the syntax: `"param1": null` (all lowercase).</span></span>
 
1. <span data-ttu-id="f692c-204">Click **... More** on the command bar and click **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="f692c-204">Click **... More** on the command bar and click **New pipeline**.</span></span>
2. <span data-ttu-id="f692c-205">Copy/paste the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="f692c-205">Copy/paste the following JSON snippet:</span></span>   

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
             "start": "2017-04-02T00:00:00Z",
             "end": "2017-04-02T05:00:00Z",
            "isPaused": false
        }
    }
    ```
3. <span data-ttu-id="f692c-206">To deploy the pipeline, click **Deploy** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="f692c-206">To deploy the pipeline, click **Deploy** on the toolbar.</span></span>  

### <a name="monitor-the-pipeline"></a><span data-ttu-id="f692c-207">Monitor the pipeline</span><span class="sxs-lookup"><span data-stu-id="f692c-207">Monitor the pipeline</span></span>
1. <span data-ttu-id="f692c-208">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="f692c-208">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![diagram tile](media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. <span data-ttu-id="f692c-210">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f692c-210">In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![diagram tile](media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. <span data-ttu-id="f692c-212">In the Diagram View, double-click the dataset `sprocsampleout`.</span><span class="sxs-lookup"><span data-stu-id="f692c-212">In the Diagram View, double-click the dataset `sprocsampleout`.</span></span> <span data-ttu-id="f692c-213">You see the slices in Ready state.</span><span class="sxs-lookup"><span data-stu-id="f692c-213">You see the slices in Ready state.</span></span> <span data-ttu-id="f692c-214">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span><span class="sxs-lookup"><span data-stu-id="f692c-214">There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.</span></span>

    ![diagram tile](media/data-factory-stored-proc-activity/data-factory-slices.png)
4. <span data-ttu-id="f692c-216">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span><span class="sxs-lookup"><span data-stu-id="f692c-216">When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.</span></span>

   ![Output data](./media/data-factory-stored-proc-activity/output.png)

   <span data-ttu-id="f692c-218">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="f692c-218">See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.</span></span>  


## <a name="specify-an-input-dataset"></a><span data-ttu-id="f692c-219">Specify an input dataset</span><span class="sxs-lookup"><span data-stu-id="f692c-219">Specify an input dataset</span></span>
<span data-ttu-id="f692c-220">In the walkthrough, stored procedure activity does not have any input datasets.</span><span class="sxs-lookup"><span data-stu-id="f692c-220">In the walkthrough, stored procedure activity does not have any input datasets.</span></span> <span data-ttu-id="f692c-221">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="f692c-221">If you specify an input dataset, the stored procedure activity does not run until the slice of input dataset is available (in Ready state).</span></span> <span data-ttu-id="f692c-222">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span><span class="sxs-lookup"><span data-stu-id="f692c-222">The dataset can be an external dataset (that is not produced by another activity in the same pipeline) or an internal dataset that is produced by an upstream activity (the activity that runs before this activity).</span></span> <span data-ttu-id="f692c-223">You can specify multiple input datasets for the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-223">You can specify multiple input datasets for the stored procedure activity.</span></span> <span data-ttu-id="f692c-224">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="f692c-224">If you do so, the stored procedure activity runs only when all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="f692c-225">The input dataset cannot be consumed in the stored procedure as a parameter.</span><span class="sxs-lookup"><span data-stu-id="f692c-225">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="f692c-226">It is only used to check the dependency before starting the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-226">It is only used to check the dependency before starting the stored procedure activity.</span></span>

## <a name="chaining-with-other-activities"></a><span data-ttu-id="f692c-227">Chaining with other activities</span><span class="sxs-lookup"><span data-stu-id="f692c-227">Chaining with other activities</span></span>
<span data-ttu-id="f692c-228">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-228">If you want to chain an upstream activity with this activity, specify the output of the upstream activity as an input of this activity.</span></span> <span data-ttu-id="f692c-229">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span><span class="sxs-lookup"><span data-stu-id="f692c-229">When you do so, the stored procedure activity does not run until the upstream activity completes and the output dataset of the upstream activity is available (in Ready status).</span></span> <span data-ttu-id="f692c-230">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-230">You can specify output datasets of multiple upstream activities as input datasets of the stored procedure activity.</span></span> <span data-ttu-id="f692c-231">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span><span class="sxs-lookup"><span data-stu-id="f692c-231">When you do so, the stored procedure activity runs only when all the input dataset slices are available.</span></span>  

<span data-ttu-id="f692c-232">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-232">In the following example, the output of the copy activity is: OutputDataset, which is an input of the stored procedure activity.</span></span> <span data-ttu-id="f692c-233">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="f692c-233">Therefore, the stored procedure activity does not run until the copy activity completes and the OutputDataset slice is available (in Ready state).</span></span> <span data-ttu-id="f692c-234">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="f692c-234">If you specify multiple input datasets, the stored procedure activity does not run until all the input dataset slices are available (in Ready state).</span></span> <span data-ttu-id="f692c-235">The input datasets cannot be used directly as parameters to the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-235">The input datasets cannot be used directly as parameters to the stored procedure activity.</span></span> 

<span data-ttu-id="f692c-236">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span><span class="sxs-lookup"><span data-stu-id="f692c-236">For more information on chaining activities, see [multiple activities in a pipeline](data-factory-create-pipelines.md#multiple-activities-in-a-pipeline)</span></span>

```json
{

    "name": "ADFTutorialPipeline",
    "properties": {
        "description": "Copy data from a blob to blob",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [ { "name": "InputDataset" } ],
                "outputs": [ { "name": "OutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst"
                },
                "name": "CopyFromBlobToSQL"
            },
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "SPSproc"
                },
                "inputs": [ { "name": "OutputDataset" } ],
                "outputs": [ { "name": "SQLOutputDataset" } ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunStoredProcedure"
            }

        ],
        "start": "2017-04-12T00:00:00Z",
        "end": "2017-04-13T00:00:00Z",
        "isPaused": false,
    }
}
```

<span data-ttu-id="f692c-237">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f692c-237">Similarly, to link the store procedure activity with **downstream activities** (the activities that run after the stored procedure activity completes), specify the output dataset of the stored procedure activity as an input of the downstream activity in the pipeline.</span></span>

> [!IMPORTANT]
> When copying data into Azure SQL Database or SQL Server, you can configure the **SqlSink** in copy activity to invoke a stored procedure by using the **sqlWriterStoredProcedureName** property. For more information, see [Invoke stored procedure from copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md). For details about the property, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties).
>  
> When copying data from Azure SQL Database or SQL Server or Azure SQL Data Warehouse, you can configure **SqlSource** in copy activity to invoke a stored procedure to read data from the source database by using the **sqlReaderStoredProcedureName** property. For more information, see the following connector articles: [Azure SQL Database](data-factory-azure-sql-connector.md#copy-activity-properties), [SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties), [Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties)          

## <a name="json-format"></a><span data-ttu-id="f692c-243">JSON format</span><span class="sxs-lookup"><span data-stu-id="f692c-243">JSON format</span></span>
<span data-ttu-id="f692c-244">Here is the JSON format for defining a Stored Procedure Activity:</span><span class="sxs-lookup"><span data-stu-id="f692c-244">Here is the JSON format for defining a Stored Procedure Activity:</span></span>

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

<span data-ttu-id="f692c-245">The following table describes these JSON properties:</span><span class="sxs-lookup"><span data-stu-id="f692c-245">The following table describes these JSON properties:</span></span>

| <span data-ttu-id="f692c-246">Property</span><span class="sxs-lookup"><span data-stu-id="f692c-246">Property</span></span> | <span data-ttu-id="f692c-247">Description</span><span class="sxs-lookup"><span data-stu-id="f692c-247">Description</span></span> | <span data-ttu-id="f692c-248">Required</span><span class="sxs-lookup"><span data-stu-id="f692c-248">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f692c-249">name</span><span class="sxs-lookup"><span data-stu-id="f692c-249">name</span></span> | <span data-ttu-id="f692c-250">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="f692c-250">Name of the activity</span></span> |<span data-ttu-id="f692c-251">Yes</span><span class="sxs-lookup"><span data-stu-id="f692c-251">Yes</span></span> |
| <span data-ttu-id="f692c-252">description</span><span class="sxs-lookup"><span data-stu-id="f692c-252">description</span></span> |<span data-ttu-id="f692c-253">Text describing what the activity is used for</span><span class="sxs-lookup"><span data-stu-id="f692c-253">Text describing what the activity is used for</span></span> |<span data-ttu-id="f692c-254">No</span><span class="sxs-lookup"><span data-stu-id="f692c-254">No</span></span> |
| <span data-ttu-id="f692c-255">type</span><span class="sxs-lookup"><span data-stu-id="f692c-255">type</span></span> | <span data-ttu-id="f692c-256">Must be set to: **SqlServerStoredProcedure**</span><span class="sxs-lookup"><span data-stu-id="f692c-256">Must be set to: **SqlServerStoredProcedure**</span></span> | <span data-ttu-id="f692c-257">Yes</span><span class="sxs-lookup"><span data-stu-id="f692c-257">Yes</span></span> |
| <span data-ttu-id="f692c-258">inputs</span><span class="sxs-lookup"><span data-stu-id="f692c-258">inputs</span></span> | <span data-ttu-id="f692c-259">Optional.</span><span class="sxs-lookup"><span data-stu-id="f692c-259">Optional.</span></span> <span data-ttu-id="f692c-260">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span><span class="sxs-lookup"><span data-stu-id="f692c-260">If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run.</span></span> <span data-ttu-id="f692c-261">The input dataset cannot be consumed in the stored procedure as a parameter.</span><span class="sxs-lookup"><span data-stu-id="f692c-261">The input dataset cannot be consumed in the stored procedure as a parameter.</span></span> <span data-ttu-id="f692c-262">It is only used to check the dependency before starting the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-262">It is only used to check the dependency before starting the stored procedure activity.</span></span> |<span data-ttu-id="f692c-263">No</span><span class="sxs-lookup"><span data-stu-id="f692c-263">No</span></span> |
| <span data-ttu-id="f692c-264">outputs</span><span class="sxs-lookup"><span data-stu-id="f692c-264">outputs</span></span> | <span data-ttu-id="f692c-265">You must specify an output dataset for a stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-265">You must specify an output dataset for a stored procedure activity.</span></span> <span data-ttu-id="f692c-266">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span><span class="sxs-lookup"><span data-stu-id="f692c-266">Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.).</span></span> <br/><br/><span data-ttu-id="f692c-267">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span><span class="sxs-lookup"><span data-stu-id="f692c-267">The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run.</span></span> <br/><br/><span data-ttu-id="f692c-268">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="f692c-268">The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) in the pipeline.</span></span> <span data-ttu-id="f692c-269">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span><span class="sxs-lookup"><span data-stu-id="f692c-269">However, Data Factory does not automatically write the output of a stored procedure to this dataset.</span></span> <span data-ttu-id="f692c-270">It is the stored procedure that writes to a SQL table that the output dataset points to.</span><span class="sxs-lookup"><span data-stu-id="f692c-270">It is the stored procedure that writes to a SQL table that the output dataset points to.</span></span> <br/><br/><span data-ttu-id="f692c-271">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-271">In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity.</span></span> |<span data-ttu-id="f692c-272">Yes</span><span class="sxs-lookup"><span data-stu-id="f692c-272">Yes</span></span> |
| <span data-ttu-id="f692c-273">storedProcedureName</span><span class="sxs-lookup"><span data-stu-id="f692c-273">storedProcedureName</span></span> |<span data-ttu-id="f692c-274">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span><span class="sxs-lookup"><span data-stu-id="f692c-274">Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse or SQL Server database that is represented by the linked service that the output table uses.</span></span> |<span data-ttu-id="f692c-275">Yes</span><span class="sxs-lookup"><span data-stu-id="f692c-275">Yes</span></span> |
| <span data-ttu-id="f692c-276">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f692c-276">storedProcedureParameters</span></span> |<span data-ttu-id="f692c-277">Specify values for stored procedure parameters.</span><span class="sxs-lookup"><span data-stu-id="f692c-277">Specify values for stored procedure parameters.</span></span> <span data-ttu-id="f692c-278">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span><span class="sxs-lookup"><span data-stu-id="f692c-278">If you need to pass null for a parameter, use the syntax: "param1": null (all lower case).</span></span> <span data-ttu-id="f692c-279">See the following sample to learn about using this property.</span><span class="sxs-lookup"><span data-stu-id="f692c-279">See the following sample to learn about using this property.</span></span> |<span data-ttu-id="f692c-280">No</span><span class="sxs-lookup"><span data-stu-id="f692c-280">No</span></span> |

## <a name="passing-a-static-value"></a><span data-ttu-id="f692c-281">Passing a static value</span><span class="sxs-lookup"><span data-stu-id="f692c-281">Passing a static value</span></span>
<span data-ttu-id="f692c-282">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span><span class="sxs-lookup"><span data-stu-id="f692c-282">Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.</span></span>

![Sample data 2](./media/data-factory-stored-proc-activity/sample-data-2.png)

<span data-ttu-id="f692c-284">**Table:**</span><span class="sxs-lookup"><span data-stu-id="f692c-284">**Table:**</span></span>

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

<span data-ttu-id="f692c-285">**Stored procedure:**</span><span class="sxs-lookup"><span data-stu-id="f692c-285">**Stored procedure:**</span></span>

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

<span data-ttu-id="f692c-286">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span><span class="sxs-lookup"><span data-stu-id="f692c-286">Now, pass the **Scenario** parameter and the value from the stored procedure activity.</span></span> <span data-ttu-id="f692c-287">The **typeProperties** section in the preceding sample looks like the following snippet:</span><span class="sxs-lookup"><span data-stu-id="f692c-287">The **typeProperties** section in the preceding sample looks like the following snippet:</span></span>

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

<span data-ttu-id="f692c-288">**Data Factory dataset:**</span><span class="sxs-lookup"><span data-stu-id="f692c-288">**Data Factory dataset:**</span></span>

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

<span data-ttu-id="f692c-289">**Data Factory pipeline**</span><span class="sxs-lookup"><span data-stu-id="f692c-289">**Data Factory pipeline**</span></span>

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
