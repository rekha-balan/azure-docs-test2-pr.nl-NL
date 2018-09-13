---
title: 'Tutorial: Create a pipeline with Copy Activity using Azure portal | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using the Data Factory Editor in the Azure portal.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: e4ce9363d862f71534899c429365de20c62f8b58
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564097"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-azure-portal"></a>Tutorial: Create a pipeline with Copy Activity using Azure portal
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Copy Wizard](data-factory-copy-data-wizard-tutorial.md)
> * [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Azure Resource Manager template](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [REST API](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [.NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

This tutorial shows you how to create and monitor an Azure data factory using the Azure portal. The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.

> [!NOTE]
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

Here are the steps you perform as part of this tutorial:

| Step | Description |
| --- | --- |
| [Create an Azure Data Factory](#create-data-factory) |In this step, you create an Azure data factory named **ADFTutorialDataFactory**. |
| [Create linked services](#create-linked-services) |In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**. <br/><br/>The AzureStorageLinkedService links the Azure storage and AzureSqlLinkedService links the Azure SQL database to the ADFTutorialDataFactory. The input data for the pipeline resides in a blob container in the Azure blob storage and output data be stored in a table in the Azure SQL database. Therefore, you add these two data stores as linked services to the data factory. |
| [Create input and output datasets](#create-datasets) |In the previous step, you created linked services that refer to data stores that contain input/output data. In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores. <br/><br/>For the InputDataset, you specify the blob container that contains a blob with the source data and for the OutputDataset, you specify the SQL table that stores the output data. You also specify other properties such as structure, availability, and policy. |
| [Create a pipeline](#create-pipeline) |In this step, you create a pipeline named **ADFTutorialPipeline** in the ADFTutorialDataFactory. <br/><br/>You add a **Copy Activity** to the pipeline that copies input data from the Azure blob to the output Azure SQL table. The Copy Activity performs the data movement in Azure Data Factory. It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way. See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity. |
| [Monitor pipeline](#monitor-pipeline) |In this step, you monitor slices of input and output tables by using Azure portal. |

## <a name="prerequisites"></a>Prerequisites
Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.

## <a name="create-data-factory"></a>Create data factory
In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.

1. After logging in to the [Azure portal](https://portal.azure.com/), click **New**, select **Intelligence + Analytics**, and click **Data Factory**. 
   
   ![New->DataFactory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. In the **New data factory** blade:
   
   1. Enter **ADFTutorialDataFactory** for the **name**. 
      
         ![New data factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       The name of the Azure data factory must be **globally unique**. If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again. See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory name not available](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. Select your Azure **subscription**.
   3. For the Resource Group, do one of the following steps:
      
      - Select **Use existing**, and select an existing resource group from the drop-down list. 
      - Select **Create new**, and enter the name of a resource group.   
         
          Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group. To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).  
   4. Select the **location** for the data factory. Only regions supported by the Data Factory service are shown in the drop-down list.
   5. Select **Pin to Startboard**.     
   6. Click **Create**.
      
      > [!IMPORTANT]
      > To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.
      > 
      > The name of the data factory may be registered as a DNS name in the future and hence become publically visible.                
      > 
      > 
3. To see the status/notification messages, click the bell icon on the toolbar. 
   
   ![Notification messages](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/Notifications.png) 
4. After the creation is complete, you see the **Data Factory** blade as shown in the image.
   
   ![Data factory home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a>Create linked services
Linked services link data stores or compute services to an Azure data factory. See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity. See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory. In this tutorial, you do not use any compute service. 

In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**. AzureStorageLinkedService linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the **ADFTutorialDataFactory**. You create a pipeline later in this tutorial that copies data from a blob container in AzureStorageLinkedService to a SQL table in AzureSqlLinkedService.

### <a name="create-a-linked-service-for-the-azure-storage-account"></a>Create a linked service for the Azure storage account
1. In the **Data Factory** blade, click **Author and deploy** tile to launch the **Editor** for the data factory.
   
   ![Author and Deploy Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. In the **Editor**, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu. You should see the JSON template for creating an Azure storage linked service in the right pane. 
   
    ![Editor New data store button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account. 
   
    ![Editor Blob Storage JSON](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. Click **Deploy** on the toolbar. You should see the deployed **AzureStorageLinkedService** in the tree view now. 
   
    ![Editor Blob Storage Deploy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

> [!NOTE]
> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties.
> 
> 

### <a name="create-a-linked-service-for-the-azure-sql-database"></a>Create a linked service for the Azure SQL Database
1. In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu. You should see the JSON template for creating the Azure SQL linked service in the right pane.
2. Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password. 
3. Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.
4. Confirm that you see **AzureSqlLinkedService** in the tree view. 

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-datasets"></a>Create datasets
In the previous step, you created linked services **AzureStorageLinkedService** and **AzureSqlLinkedService** to link an Azure Storage account and Azure SQL database to the data factory: **ADFTutorialDataFactory**. In this step, you define two datasets -- **InputDataset** and **OutputDataset** -- that represent the input/output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively. For InputDataset, you specify the blob container that contains a blob with the source data and for OutputDataset, you specify the SQL table that stores the output data. 

### <a name="create-input-dataset"></a>Create input dataset
In this step, you create a dataset named **InputDataset** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService** linked service.

1. In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu. 
   
    ![New dataset menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. Replace JSON in the right pane with the following JSON snippet: 
   
    ```JSON
    {
      "name": "InputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```   
    Note the following points: 
   
    - dataset **type** is set to **AzureBlob**.
    - **linkedServiceName** is set to **AzureStorageLinkedService**. You created this linked service in Step 2.
    - **folderPath** is set to the **adftutorial** container. You can also specify the name of a blob within the folder using the **fileName** property. Since you are not specifying the name of the blob, data from all blobs in the container is considered as an input data.
    - format **type** is set to **TextFormat**
    - There are two fields in the text file – **FirstName** and **LastName** separated by a comma character (**columnDelimiter**)
    - The **availability** is set to **hourly** (**frequency** is set to **hour** and **interval** is set to **1**). Therefore, Data Factory looks for input data every hour in the root folder of blob container (**adftutorial**) you specified. 
     
     if you don't specify a **fileName** for an **input** dataset, all files/blobs from the input folder (**folderPath**) are considered as inputs. If you specify a fileName in the JSON, only the specified file/blob is considered asn input.
     
     If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).
     
     To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property. In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart. For example, if a slice is being produced for 2016-09-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2016/09/20 and the fileName is set to 08.csv. 

    ```JSON     
    "folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
    "fileName": "{Hour}.csv",
    "partitionedBy": 
    [
       { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
       { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } }, 
       { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }, 
       { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } } 
    ],
    ```
3. Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset. Confirm that you see the **InputDataset** in the tree view.

> [!NOTE]
> See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties.
> 
> 

### <a name="create-output-dataset"></a>Create output dataset
In this part of the step, you create an output dataset named **OutputDataset**. This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**. 

1. In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu. 
2. Replace JSON in the right pane with the following JSON snippet:

    ```JSON   
    {
      "name": "OutputDataset",
      "properties": {
        "structure": [
          {
            "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
          }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
          "tableName": "emp"
        },
        "availability": {
          "frequency": "Hour",
          "interval": 1
        }
      }
    }
    ```     
    Note the following points: 
   
    - dataset **type** is set to **AzureSQLTable**.
    - **linkedServiceName** is set to **AzureSqlLinkedService** (you created this linked service in Step 2).
    - **tablename** is set to **emp**.
    - There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database. ID is an identity column, so you need to specify only **FirstName** and **LastName** here.
    - The **availability** is set to **hourly** (**frequency** set to **hour** and **interval** set to **1**).  The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.
3. Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset. Confirm that you see the **OutputDataset** in the tree view. 

> [!NOTE]
> See [Move data from/to Azure SQL Database](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties.
> 
> 

## <a name="create-pipeline"></a>Create pipeline
In this step, you create a pipeline with a **Copy Activity** that uses **InputDataset** as input and **OutputDataset** as output.

1. In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**. Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.
2. Replace JSON in the right pane with the following JSON snippet: 

    ```JSON   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
        "activities": [
          {
            "name": "CopyFromBlobToSQL",
            "type": "Copy",
            "inputs": [
              {
                "name": "InputDataset"
              }
            ],
            "outputs": [
              {
                "name": "OutputDataset"
              }
            ],
            "typeProperties": {
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "SqlSink",
                "writeBatchSize": 10000,
                "writeBatchTimeout": "60:00:00"
              }
            },
            "Policy": {
              "concurrency": 1,
              "executionPriorityOrder": "NewestFirst",
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2016-07-12T00:00:00Z",
        "end": "2016-07-13T00:00:00Z"
      }
    } 
    ```   
    
    Note the following points:
   
    - In the activities section, there is only one activity whose **type** is set to **Copy**.
    - Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.
    - In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.
     
    Replace the value of the **start** property with the current day and **end** value with the next day. You can specify only the date part and skip the time part of the date time. For example, "2016-02-03", which is equivalent to "2016-02-03T00:00:00Z"
     
    Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601). For example: 2016-10-14T16:32:41Z. The **end** time is optional, but we use it in this tutorial. 
     
    If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**". To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.
     
    In the preceding example, there are 24 data slices as each data slice is produced hourly.
3. Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**. Confirm that you see the pipeline in the tree view. 
4. Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.

**Congratulations!** You have successfully created an Azure data factory, linked services, tables, and a pipeline and scheduled the pipeline.   

### <a name="view-the-data-factory-in-a-diagram-view"></a>View the data factory in a Diagram View
1. In the **Data Factory** blade, click **Diagram**.
   
    ![Data Factory Blade - Diagram Tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. You should see the diagram similar to the following image: 
   
    ![Diagram view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)
   
    You can zoom in, zoom out, zoom to 100%, zoom to fit, automatically position pipelines and tables, and show lineage information (highlights upstream and downstream items of selected items).  You can double-click an object (input/output table or pipeline) to see properties for it. 
3. Right-click **ADFTutorialPipeline** in the Diagram View and click **Open pipeline**. 
   
    ![Open Pipeline](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DiagramView-OpenPipeline.png)
4. You should see the activities in the pipeline along with input and output datasets for the activities. In this tutorial, you have only one activity in the pipeline (Copy Activity) with InputDataset as input dataset and OutputDataset as output dataset.   
   
    ![Opened pipeline view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DiagramView-OpenedPipeline.png)
5. Click **Data factory** in the breadcrumb in the top-left corner to get back to the diagram view. The diagram view displays all the pipelines. In this example, you have only created one pipeline.   

## <a name="monitor-pipeline"></a>Monitor pipeline
In this step, you use the Azure portal to monitor what’s going on in an Azure data factory. 

### <a name="monitor-pipeline-using-diagram-view"></a>Monitor pipeline using Diagram View
1. Click **X** to close the **Diagram** view to see the Data Factory home page for the data factory. If you have closed the web browser, do the following steps: 
   1. Navigate to [Azure portal](https://portal.azure.com/). 
   2. Double-click **ADFTutorialDataFactory** on the **Startboard** (or) click **Data factories** on the left menu, and search for ADFTutorialDataFactory. 
2. You should see the count and names of tables and pipeline you created on this blade.
   
    ![home page with names](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactory-home-page-pipeline-tables.png)
3. Now, click **Datasets** tile.
4. In the **Datasets** blade, click **InputDataset**. This dataset is the input dataset for **ADFTutorialPipeline**.
   
    ![Datasets with InputDataset selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. Click **... (ellipsis)** to see all the data slices.
   
    ![All input data slices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    Notice that all the data slices up to the current time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**. Confirm that no slices show up in the **Recently failed slices** section at the bottom.
   
    Both **Recently updated slices** and **Recently failed slices** lists are sorted by the **LAST UPDATE TIME**. 
   
    Click **Filter** on the toolbar to filter the slices.  
   
    ![Filter input slices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/filter-input-slices.png)
6. Close the blades until you see the **Datasets** blade. Click the **OutputDataset**. This dataset is the output dataset for **ADFTutorialPipeline**.
   
    ![data sets blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datasets-blade.png)
7. You should see the **OutputDataset** blade as shown in the following image:
   
    ![table blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-table-blade.png) 
8. Notice that the data slices up to the current time have already been produced and they are **Ready**. No slices show up in the **Problem slices** section at the bottom.
9. Click **… (Ellipsis)** to see all the slices.
   
    ![data slices blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png)
10. Click any data slice from the list and you should see the **Data slice** blade.
    
     ![data slice blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.
11. In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom. Click an **activity run** to see the **Activity run details** blade. 
    
    ![Activity Run Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)
12. Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.
13. (optional) Click **Pipelines** on the home page for **ADFTutorialDataFactory**, click **ADFTutorialPipeline** in the **Pipelines** blade, and drill through input tables (**Consumed**) or output tables (**Produced**).
14. Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.
    
    ![sql query results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

### <a name="monitor-pipeline-using-monitor--manage-app"></a>Monitor pipeline using Monitor & Manage App
You can also use Monitor & Manage application to monitor your pipelines. For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).

1. Click **Monitor & Manage** tile on the home page for your data factory.
   
    ![Monitor & Manage tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. You should see **Monitor & Manage application**. Change the **Start time** and **End time** to include start (2016-07-12) and end times (2016-07-13) of your pipeline, and click **Apply**. 
   
    ![Monitor & Manage App](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png) 
3. Select an activity window in the **Activity Windows** list to see details about it. 
    ![Activity window details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)

## <a name="summary"></a>Summary
In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database. You used the Azure portal to create the data factory, linked services, datasets, and a pipeline. Here are the high-level steps you performed in this tutorial:  

1. Created an Azure **data factory**.
2. Created **linked services**:
   1. An **Azure Storage** linked service to link your Azure Storage account that holds input data.     
   2. An **Azure SQL** linked service to link your Azure SQL database that holds the output data. 
3. Created **datasets** that describe input data and output data for pipelines.
4. Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.  

## <a name="see-also"></a>See Also
| Topic | Description |
|:--- |:--- |
| [Pipelines](data-factory-create-pipelines.md) |This article helps you understand pipelines and activities in Azure Data Factory. |
| [Datasets](data-factory-create-datasets.md) |This article helps you understand datasets in Azure Data Factory. |
| [Scheduling and execution](data-factory-scheduling-and-execution.md) |This article explains the scheduling and execution aspects of Azure Data Factory application model. |



























