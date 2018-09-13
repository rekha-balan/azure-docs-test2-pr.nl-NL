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
# <a name="sql-server-stored-procedure-activity"></a>SQL Server Stored Procedure Activity
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

You use data transformation activities in a Data Factory [pipeline](data-factory-create-pipelines.md) to transform and process raw data into predictions and insights. The Stored Procedure Activity is one of the transformation activities that Data Factory supports. This article builds on the [data transformation activities](data-factory-data-transformation-activities.md) article, which presents a general overview of data transformation and the supported transformation activities.

You can use the Stored Procedure Activity to invoke a stored procedure in one of the following data stores: Azure SQL Database, Azure SQL Data Warehouse, SQL Server Database in your enterprise or on an Azure virtual machine (VM).  If you are using SQL Server, install Data Management Gateway on the same machine that hosts the database or on a separate machine that has access to the database. Data Management Gateway is a component that connects data sources on-premises/on Azure VM with cloud services in a secure and managed way. See [Data Management Gateway](data-factory-data-management-gateway.md) article for details.

The following walkthrough uses the Stored Procedure Activity in a pipeline to invoke a stored procedure in an Azure SQL database. 

## <a name="walkthrough"></a>Walkthrough
### <a name="sample-table-and-stored-procedure"></a>Sample table and stored procedure
1. Create the following **table** in your Azure SQL Database using SQL Server Management Studio or any other tool you are comfortable with. The datetimestamp column is the date and time when the corresponding ID is generated.

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
    Id is the unique identified and the datetimestamp column is the date and time when the corresponding ID is generated.
    
    ![Sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/sample-data.png)

    In this sample, the stored procedure is in an Azure SQL Database. If the stored procedure is in an Azure SQL Data Warehouse and SQL Server Database, the approach is similar. For a SQL Server database, you must install a [Data Management Gateway](data-factory-data-management-gateway.md).
2. Create the following **stored procedure** that inserts data in to the **sampletable**.

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

### <a name="create-a-data-factory"></a>Create a data factory
1. Log in to [Azure portal](https://portal.azure.com/).
2. Click **NEW** on the left menu, click **Intelligence + Analytics**, and click **Data Factory**.

    ![New data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-factory.png)    
3. In the **New data factory** blade, enter **SProcDF** for the Name. Azure Data Factory names are **globally unique**. You need to prefix the name of the data factory with your name, to enable the successful creation of the factory.

   ![New data factory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-factory-blade.png)         
4. Select your **Azure subscription**.
5. For **Resource Group**, do one of the following steps:
   1. Click **Create new** and enter a name for the resource group.
   2. Click **Use existing** and select an existing resource group.  
6. Select the **location** for the data factory.
7. Select **Pin to dashboard** so that you can see the data factory on the dashboard next time you log in.
8. Click **Create** on the **New data factory** blade.
9. You see the data factory being created in the **dashboard** of the Azure portal. After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.

   ![Data Factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-home-page.png)

### <a name="create-an-azure-sql-linked-service"></a>Create an Azure SQL linked service
After creating the data factory, you create an Azure SQL linked service that links your Azure SQL Database to the data factory. This database contains the sampletable table and sp_sample stored procedure.

1. Click **Author and deploy** on the **Data Factory** blade for **SProcDF** to launch the Data Factory Editor.
2. Click **New data store** on the command bar and choose **Azure SQL Database**. You should see the JSON script for creating an Azure SQL linked service in the editor.

   ![New data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-data-store.png)
3. In the JSON script, make the following changes:

   1. Replace `<servername>` with the name of your Azure SQL Database server.
   2. Replace `<databasename>` with the database in which you created the table and the stored procedure.
   3. Replace `<username@servername>` with the user account that has access to the database.
   4. Replace `<password>` with the password for the user account.

      ![New data store](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/azure-sql-linked-service.png)
4. To deploy the linked service, click **Deploy** on the command bar. Confirm that you see the AzureSqlLinkedService in the tree view on the left.

    ![tree view with linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/tree-view.png)

### <a name="create-an-output-dataset"></a>Create an output dataset
1. Click **... More** on the toolbar, click **New dataset**, and click **Azure SQL**. **New dataset** on the command bar and select **Azure SQL**.

    ![tree view with linked service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/new-dataset.png)
2. Copy/paste the following JSON script in to the JSON editor.

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
3. To deploy the dataset, click **Deploy** on the command bar. Confirm that you see the dataset in the tree view.

    ![tree view with linked services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/tree-view-2.png)

### <a name="create-a-pipeline-with-sqlserverstoredprocedure-activity"></a>Create a pipeline with SqlServerStoredProcedure activity
Now, let's create a pipeline with a SqlServerStoredProcedure activity.

1. Click **... More** on the command bar and click **New pipeline**.
2. Copy/paste the following JSON snippet:   

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

    The **storedProcedureName** set to **sp_sample**. Name and casing of the parameter **DateTime** must match the name and casing of the parameter in the stored procedure definition.

    If you need pass null for a parameter, use the syntax: "param1": null (all lowercase).
3. To deploy the pipeline, click **Deploy** on the toolbar.  

### <a name="monitor-the-pipeline"></a>Monitor the pipeline
1. Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-diagram-tile.png)
2. In the **Diagram View**, you see an overview of the pipelines, and datasets used in this tutorial.

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-diagram-view.png)
3. In the Diagram View, double-click the dataset `sprocsampleout`. You see the slices in Ready state. There should be five slices because a slice is produced for each hour between the start time and end time from the JSON.

    ![diagram tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/data-factory-slices.png)
4. When a slice is in **Ready** state, run a `select * from sampletable` query against the Azure SQL database to verify that the data was inserted in to the table by the stored procedure.

   ![Output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/output.png)

   See [Monitor the pipeline](data-factory-monitor-manage-pipelines.md) for detailed information about monitoring Azure Data Factory pipelines.  

> [!NOTE]
> In this example, the SprocActivitySample has no inputs. If you want to chain this activity with an activity upstream (that is, prior processing), the outputs of the upstream activity can be used as inputs in this activity. In such a case, this activity does not execute until the upstream activity is completed and the outputs of the upstream activities are available (in Ready status). The inputs cannot be used directly as a parameter to the stored procedure activity
>
>

## <a name="json-format"></a>JSON format
Here is the JSON format for defining a Stored Procedure Activity:

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

## <a name="json-properties"></a>JSON properties
| Property | Description | Required |
| --- | --- | --- |
| name | Name of the activity |Yes |
| description |Text describing what the activity is used for |No |
| type | Must be set to: **SqlServerStoredProcedure** | Yes |
| inputs | Optional. If you do specify an input dataset, it must be available (in ‘Ready’ status) for the stored procedure activity to run. The input dataset cannot be consumed in the stored procedure as a parameter. It is only used to check the dependency before starting the stored procedure activity. |No |
| outputs | You must specify an output dataset for a stored procedure activity. Output dataset specifies the **schedule** for the stored procedure activity (hourly, weekly, monthly, etc.). <br/><br/>The output dataset must use a **linked service** that refers to an Azure SQL Database or an Azure SQL Data Warehouse or a SQL Server Database in which you want the stored procedure to run. <br/><br/>The output dataset can serve as a way to pass the result of the stored procedure for subsequent processing by another activity ([chaining activities](data-factory-scheduling-and-execution.md#run-activities-in-a-sequence)) in the pipeline. However, Data Factory does not automatically write the output of a stored procedure to this dataset. It is the stored procedure that writes to a SQL table that the output dataset points to. <br/><br/>In some cases, the output dataset can be a **dummy dataset**, which is used only to specify the schedule for running the stored procedure activity. |Yes |
| storedProcedureName |Specify the name of the stored procedure in the Azure SQL database or Azure SQL Data Warehouse that is represented by the linked service that the output table uses. |Yes |
| storedProcedureParameters |Specify values for stored procedure parameters. If you need to pass null for a parameter, use the syntax: "param1": null (all lower case). See the following sample to learn about using this property. |No |

## <a name="passing-a-static-value"></a>Passing a static value
Now, let’s consider adding another column named ‘Scenario’ in the table containing a static value called ‘Document sample’.

![Sample data 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-stored-proc-activity/sample-data-2.png)

**Table:**

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

**Stored procedure:**

```SQL
CREATE PROCEDURE sp_sample2 @DateTime nvarchar(127) , @Scenario nvarchar(127)

AS

BEGIN
    INSERT INTO [sampletable2]
    VALUES (newid(), @DateTime, @Scenario)
END
```

Now, pass the **Scenario** parameter and the value from the stored procedure activity. The **typeProperties** section in the preceding sample looks like the following snippet:

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

**Data Factory dataset:**

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

**Data Factory pipeline**

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













