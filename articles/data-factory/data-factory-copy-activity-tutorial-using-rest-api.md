---
title: 'Tutorial: Create a pipeline with Copy Activity using REST API | Microsoft Docs'
description: In this tutorial, you create an Azure Data Factory pipeline with a Copy Activity by using REST API.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: spelluru
ms.openlocfilehash: 1bd21ca8e2e5b9565a1fc9ce6bb6163ef768f455
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540689"
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-rest-api"></a><span data-ttu-id="16716-103">Tutorial: Create a pipeline with Copy Activity using REST API</span><span class="sxs-lookup"><span data-stu-id="16716-103">Tutorial: Create a pipeline with Copy Activity using REST API</span></span>
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

<span data-ttu-id="16716-112">This tutorial shows you how to create and monitor an Azure data factory using the REST API.</span><span class="sxs-lookup"><span data-stu-id="16716-112">This tutorial shows you how to create and monitor an Azure data factory using the REST API.</span></span> <span data-ttu-id="16716-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="16716-113">The pipeline in the data factory uses a Copy Activity to copy data from Azure Blob Storage to Azure SQL Database.</span></span>

> [!NOTE]
> This article does not cover all the Data Factory REST API. See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.
> 
> The data pipeline in this tutorial copies data from a source data store to a destination data store. It does not transform input data to produce output data. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="16716-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="16716-119">Prerequisites</span></span>
* <span data-ttu-id="16716-120">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="16716-120">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="16716-121">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span><span class="sxs-lookup"><span data-stu-id="16716-121">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="16716-122">You use the Curl tool with REST commands to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="16716-122">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="16716-123">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span><span class="sxs-lookup"><span data-stu-id="16716-123">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="16716-124">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16716-124">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="16716-125">Get **client ID** and **secret key**.</span><span class="sxs-lookup"><span data-stu-id="16716-125">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="16716-126">Get **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="16716-126">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="16716-127">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="16716-127">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="16716-128">Install [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="16716-128">Install [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>  
* <span data-ttu-id="16716-129">Launch **PowerShell** and do the following steps.</span><span class="sxs-lookup"><span data-stu-id="16716-129">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="16716-130">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="16716-130">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="16716-131">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="16716-131">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="16716-132">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="16716-132">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. <span data-ttu-id="16716-133">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="16716-133">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="16716-134">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="16716-134">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="16716-135">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="16716-135">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="16716-136">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span><span class="sxs-lookup"><span data-stu-id="16716-136">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="16716-137">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span><span class="sxs-lookup"><span data-stu-id="16716-137">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="16716-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="16716-138">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="16716-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="16716-139">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="16716-140">Create JSON definitions</span><span class="sxs-lookup"><span data-stu-id="16716-140">Create JSON definitions</span></span>
<span data-ttu-id="16716-141">Create following JSON files in the folder where curl.exe is located.</span><span class="sxs-lookup"><span data-stu-id="16716-141">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="16716-142">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="16716-142">datafactory.json</span></span>
> [!IMPORTANT]
> Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="16716-144">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="16716-144">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> Replace **accountname** and **accountkey** with name and key of your Azure storage account. To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-access-keys).
> 
> 

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="16716-147">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="16716-147">azuersqllinkedservice.json</span></span>
> [!IMPORTANT]
> Replace **servername**, **databasename**, **username**, and **password** with name of your Azure SQL server, name of SQL database, user account, and password for the account.  
> 
> 

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

### <a name="inputdatasetjson"></a><span data-ttu-id="16716-149">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="16716-149">inputdataset.json</span></span>

```JSON
{
  "name": "AzureBlobInput",
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

<span data-ttu-id="16716-150">The JSON definition defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="16716-150">The JSON definition defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="16716-151">In addition, it specifies that the input data is located in the file **emp.txt** that is in blob container **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="16716-151">In addition, it specifies that the input data is located in the file **emp.txt** that is in blob container **adftutorial**.</span></span> 

 <span data-ttu-id="16716-152">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="16716-152">Note the following points:</span></span> 

* <span data-ttu-id="16716-153">dataset **type** is set to **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="16716-153">dataset **type** is set to **AzureBlob**.</span></span>
* <span data-ttu-id="16716-154">**linkedServiceName** is set to **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16716-154">**linkedServiceName** is set to **AzureStorageLinkedService**.</span></span> 
* <span data-ttu-id="16716-155">**folderPath** is set to the **adftutorial** container and **fileName** is set to **emp.txt**.</span><span class="sxs-lookup"><span data-stu-id="16716-155">**folderPath** is set to the **adftutorial** container and **fileName** is set to **emp.txt**.</span></span>  
* <span data-ttu-id="16716-156">format **type** is set to **TextFormat**</span><span class="sxs-lookup"><span data-stu-id="16716-156">format **type** is set to **TextFormat**</span></span>
* <span data-ttu-id="16716-157">There are two fields in the text file – **FirstName** and **LastName** – separated by a comma character (columnDelimiter)</span><span class="sxs-lookup"><span data-stu-id="16716-157">There are two fields in the text file – **FirstName** and **LastName** – separated by a comma character (columnDelimiter)</span></span>    
* <span data-ttu-id="16716-158">The **availability** is set to **hourly** (frequency is set to hour and interval is set to 1).</span><span class="sxs-lookup"><span data-stu-id="16716-158">The **availability** is set to **hourly** (frequency is set to hour and interval is set to 1).</span></span> <span data-ttu-id="16716-159">Therefore, Data Factory looks for input data every hour in the root folder of the specified blob container (adftutorial).</span><span class="sxs-lookup"><span data-stu-id="16716-159">Therefore, Data Factory looks for input data every hour in the root folder of the specified blob container (adftutorial).</span></span> 

<span data-ttu-id="16716-160">if you don't specify a **fileName** for an input dataset, all files/blobs from the input folder (folderPath) are considered as inputs.</span><span class="sxs-lookup"><span data-stu-id="16716-160">if you don't specify a **fileName** for an input dataset, all files/blobs from the input folder (folderPath) are considered as inputs.</span></span> <span data-ttu-id="16716-161">If you specify a fileName in the JSON, only the specified file/blob is considered as an input.</span><span class="sxs-lookup"><span data-stu-id="16716-161">If you specify a fileName in the JSON, only the specified file/blob is considered as an input.</span></span>

<span data-ttu-id="16716-162">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span><span class="sxs-lookup"><span data-stu-id="16716-162">If you do not specify a **fileName** for an **output table**, the generated files in the **folderPath** are named in the following format: Data.&lt;Guid&gt;.txt (example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.).</span></span>

<span data-ttu-id="16716-163">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span><span class="sxs-lookup"><span data-stu-id="16716-163">To set **folderPath** and **fileName** dynamically based on the **SliceStart** time, use the **partitionedBy** property.</span></span> <span data-ttu-id="16716-164">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span><span class="sxs-lookup"><span data-stu-id="16716-164">In the following example, folderPath uses Year, Month, and Day from the SliceStart (start time of the slice being processed) and fileName uses Hour from the SliceStart.</span></span> <span data-ttu-id="16716-165">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span><span class="sxs-lookup"><span data-stu-id="16716-165">For example, if a slice is being produced for 2014-10-20T08:00:00, the folderName is set to wikidatagateway/wikisampledataout/2014/10/20 and the fileName is set to 08.csv.</span></span> 

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

### <a name="outputdatasetjson"></a><span data-ttu-id="16716-166">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="16716-166">outputdataset.json</span></span>

```JSON
{
  "name": "AzureSqlOutput",
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

<span data-ttu-id="16716-167">The JSON definition defines a dataset named **AzureSqlOutput**, which represents output data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="16716-167">The JSON definition defines a dataset named **AzureSqlOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="16716-168">In addition, it specifies that the results are stored in the table: **emp** in the database represented by the AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="16716-168">In addition, it specifies that the results are stored in the table: **emp** in the database represented by the AzureSqlLinkedService.</span></span> <span data-ttu-id="16716-169">The **availability** section specifies that the output dataset is produced on an hourly (frequency: hour and interval: 1) basis.</span><span class="sxs-lookup"><span data-stu-id="16716-169">The **availability** section specifies that the output dataset is produced on an hourly (frequency: hour and interval: 1) basis.</span></span>

<span data-ttu-id="16716-170">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="16716-170">Note the following points:</span></span> 

* <span data-ttu-id="16716-171">dataset **type** is set to **AzureSQLTable**.</span><span class="sxs-lookup"><span data-stu-id="16716-171">dataset **type** is set to **AzureSQLTable**.</span></span>
* <span data-ttu-id="16716-172">**linkedServiceName** is set to **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16716-172">**linkedServiceName** is set to **AzureSqlLinkedService**.</span></span>
* <span data-ttu-id="16716-173">**tablename** is set to **emp**.</span><span class="sxs-lookup"><span data-stu-id="16716-173">**tablename** is set to **emp**.</span></span>
* <span data-ttu-id="16716-174">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="16716-174">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="16716-175">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="16716-175">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>
* <span data-ttu-id="16716-176">The **availability** is set to **hourly** (frequency set to hour and interval set to 1).</span><span class="sxs-lookup"><span data-stu-id="16716-176">The **availability** is set to **hourly** (frequency set to hour and interval set to 1).</span></span>  <span data-ttu-id="16716-177">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="16716-177">The Data Factory service generates an output data slice every hour in the **emp** table in the Azure SQL database.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="16716-178">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="16716-178">pipeline.json</span></span>

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob to Azure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data to Azure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
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
    "start": "2016-08-12T00:00:00Z",
    "end": "2016-08-13T00:00:00Z"
  }
}
```

<span data-ttu-id="16716-179">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="16716-179">Note the following points:</span></span>

* <span data-ttu-id="16716-180">In the activities section, there is only one activity whose **type** is set to **CopyActivity**.</span><span class="sxs-lookup"><span data-stu-id="16716-180">In the activities section, there is only one activity whose **type** is set to **CopyActivity**.</span></span>
* <span data-ttu-id="16716-181">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="16716-181">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span>
* <span data-ttu-id="16716-182">In the **transformation** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="16716-182">In the **transformation** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span>

<span data-ttu-id="16716-183">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="16716-183">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="16716-184">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="16716-184">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="16716-185">For example, "2015-02-03", which is equivalent to "2015-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="16716-185">For example, "2015-02-03", which is equivalent to "2015-02-03T00:00:00Z"</span></span>

<span data-ttu-id="16716-186">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="16716-186">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="16716-187">For example: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="16716-187">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="16716-188">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="16716-188">The **end** time is optional, but we use it in this tutorial.</span></span> 

<span data-ttu-id="16716-189">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="16716-189">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="16716-190">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="16716-190">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>

<span data-ttu-id="16716-191">In the example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="16716-191">In the example, there are 24 data slices as each data slice is produced hourly.</span></span>

> [!NOTE]
> See [Anatomy of a Pipeline](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.
> 
> 

## <a name="set-global-variables"></a><span data-ttu-id="16716-193">Set global variables</span><span class="sxs-lookup"><span data-stu-id="16716-193">Set global variables</span></span>
<span data-ttu-id="16716-194">In Azure PowerShell, execute the following commands after replacing the values with your own:</span><span class="sxs-lookup"><span data-stu-id="16716-194">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="16716-196">Authenticate with AAD</span><span class="sxs-lookup"><span data-stu-id="16716-196">Authenticate with AAD</span></span>
<span data-ttu-id="16716-197">Run the following command to authenticate with Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="16716-197">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="16716-198">Create data factory</span><span class="sxs-lookup"><span data-stu-id="16716-198">Create data factory</span></span>
<span data-ttu-id="16716-199">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="16716-199">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="16716-200">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="16716-200">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="16716-201">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="16716-201">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="16716-202">For example, a Copy Activity to copy data from a source to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="16716-202">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="16716-203">A HDInsight Hive activity to run Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="16716-203">A HDInsight Hive activity to run Hive script to transform input data to product output data.</span></span> <span data-ttu-id="16716-204">Run the following commands to create the data factory:</span><span class="sxs-lookup"><span data-stu-id="16716-204">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="16716-205">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-205">Assign the command to variable named **cmd**.</span></span> 
   
    <span data-ttu-id="16716-206">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="16716-206">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-207">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-207">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-208">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-208">View the results.</span></span> <span data-ttu-id="16716-209">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-209">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="16716-210">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="16716-210">Note the following points:</span></span>

* <span data-ttu-id="16716-211">The name of the Azure Data Factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="16716-211">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="16716-212">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="16716-212">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="16716-213">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="16716-213">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="16716-214">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span><span class="sxs-lookup"><span data-stu-id="16716-214">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="16716-215">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="16716-215">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="16716-216">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="16716-216">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="16716-217">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="16716-217">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="16716-218">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="16716-218">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="16716-219">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="16716-219">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="16716-220">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="16716-220">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="16716-221">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="16716-221">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="16716-222">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="16716-222">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="16716-223">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="16716-223">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="16716-224">Before creating a pipeline, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="16716-224">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="16716-225">You first create linked services to link source and destination data stores to your data store.</span><span class="sxs-lookup"><span data-stu-id="16716-225">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="16716-226">Then, define input and output datasets to represent data in linked data stores.</span><span class="sxs-lookup"><span data-stu-id="16716-226">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="16716-227">Finally, create the pipeline with an activity that uses these datasets.</span><span class="sxs-lookup"><span data-stu-id="16716-227">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="16716-228">Create linked services</span><span class="sxs-lookup"><span data-stu-id="16716-228">Create linked services</span></span>
<span data-ttu-id="16716-229">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="16716-229">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="16716-230">A data store can be an Azure Storage, Azure SQL Database, or an on-premises SQL Server database that contains input data or stores output data for a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="16716-230">A data store can be an Azure Storage, Azure SQL Database, or an on-premises SQL Server database that contains input data or stores output data for a Data Factory pipeline.</span></span> <span data-ttu-id="16716-231">A compute service is the service that processes input data and produces output data.</span><span class="sxs-lookup"><span data-stu-id="16716-231">A compute service is the service that processes input data and produces output data.</span></span> 

<span data-ttu-id="16716-232">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16716-232">In this step, you create two linked services: **AzureStorageLinkedService** and **AzureSqlLinkedService**.</span></span> <span data-ttu-id="16716-233">AzureStorageLinkedService linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the data factory: **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="16716-233">AzureStorageLinkedService linked service links an Azure Storage Account and AzureSqlLinkedService links an Azure SQL database to the data factory: **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="16716-234">You create a pipeline later in this tutorial that copies data from a blob container in AzuretStorageLinkedService to a SQL table in AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="16716-234">You create a pipeline later in this tutorial that copies data from a blob container in AzuretStorageLinkedService to a SQL table in AzureSqlLinkedService.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="16716-235">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="16716-235">Create Azure Storage linked service</span></span>
<span data-ttu-id="16716-236">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="16716-236">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="16716-237">With this tutorial, you use the Azure Storage account to store input data.</span><span class="sxs-lookup"><span data-stu-id="16716-237">With this tutorial, you use the Azure Storage account to store input data.</span></span> 

1. <span data-ttu-id="16716-238">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-238">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-239">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-239">Run the command by using **Invoke-Command**.</span></span>
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-240">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-240">View the results.</span></span> <span data-ttu-id="16716-241">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-241">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="16716-242">Create Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="16716-242">Create Azure SQL linked service</span></span>
<span data-ttu-id="16716-243">In this step, you link your Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="16716-243">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="16716-244">With this tutorial, you use the same Azure SQL database to store the output data.</span><span class="sxs-lookup"><span data-stu-id="16716-244">With this tutorial, you use the same Azure SQL database to store the output data.</span></span>

1. <span data-ttu-id="16716-245">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-245">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-246">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-246">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-247">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-247">View the results.</span></span> <span data-ttu-id="16716-248">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-248">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="16716-249">Create datasets</span><span class="sxs-lookup"><span data-stu-id="16716-249">Create datasets</span></span>
<span data-ttu-id="16716-250">In the previous step, you created linked services **AzureStorageLinkedService** and **AzureSqlLinkedService** to link an Azure Storage account and Azure SQL database to the data factory: **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="16716-250">In the previous step, you created linked services **AzureStorageLinkedService** and **AzureSqlLinkedService** to link an Azure Storage account and Azure SQL database to the data factory: **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="16716-251">In this step, you create datasets that represent the input and output data for the Copy Activity in the pipeline you create in the next step.</span><span class="sxs-lookup"><span data-stu-id="16716-251">In this step, you create datasets that represent the input and output data for the Copy Activity in the pipeline you create in the next step.</span></span> 

<span data-ttu-id="16716-252">The input dataset in this tutorial refers to a blob container in the Azure Storage that AzureStorageLinkedService points to.</span><span class="sxs-lookup"><span data-stu-id="16716-252">The input dataset in this tutorial refers to a blob container in the Azure Storage that AzureStorageLinkedService points to.</span></span> <span data-ttu-id="16716-253">The output dataset refers to a SQL table in the Azure SQL database that AzureSqlLinkedService points to.</span><span class="sxs-lookup"><span data-stu-id="16716-253">The output dataset refers to a SQL table in the Azure SQL database that AzureSqlLinkedService points to.</span></span>  

### <a name="prepare-azure-blob-storage-and-azure-sql-database-for-the-tutorial"></a><span data-ttu-id="16716-254">Prepare Azure Blob Storage and Azure SQL Database for the tutorial</span><span class="sxs-lookup"><span data-stu-id="16716-254">Prepare Azure Blob Storage and Azure SQL Database for the tutorial</span></span>
<span data-ttu-id="16716-255">Perform the following steps to prepare the Azure blob storage and Azure SQL database for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="16716-255">Perform the following steps to prepare the Azure blob storage and Azure SQL database for this tutorial.</span></span> 

* <span data-ttu-id="16716-256">Create a blob container named **adftutorial** in the Azure blob storage that **AzureStorageLinkedService** points to.</span><span class="sxs-lookup"><span data-stu-id="16716-256">Create a blob container named **adftutorial** in the Azure blob storage that **AzureStorageLinkedService** points to.</span></span> 
* <span data-ttu-id="16716-257">Create and upload a text file, **emp.txt**, as a blob to the **adftutorial** container.</span><span class="sxs-lookup"><span data-stu-id="16716-257">Create and upload a text file, **emp.txt**, as a blob to the **adftutorial** container.</span></span> 
* <span data-ttu-id="16716-258">Create a table named **emp** in the Azure SQL Database in the Azure SQL database that **AzureSqlLinkedService** points to.</span><span class="sxs-lookup"><span data-stu-id="16716-258">Create a table named **emp** in the Azure SQL Database in the Azure SQL database that **AzureSqlLinkedService** points to.</span></span>

1. <span data-ttu-id="16716-259">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="16716-259">Launch Notepad.</span></span> <span data-ttu-id="16716-260">Copy the following text and save it as **emp.txt** to **C:\ADFGetStartedPSH** folder on your hard drive.</span><span class="sxs-lookup"><span data-stu-id="16716-260">Copy the following text and save it as **emp.txt** to **C:\ADFGetStartedPSH** folder on your hard drive.</span></span> 

    ```   
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="16716-261">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="16716-261">Use tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/) to create the **adftutorial** container and to upload the **emp.txt** file to the container.</span></span>
   
    ![Azure Storage Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-powershell/getstarted-storage-explorer.png)
3. <span data-ttu-id="16716-263">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="16716-263">Use the following SQL script to create the **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp 
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID); 
    ```

    <span data-ttu-id="16716-264">If you have SQL Server 2014 installed on your computer: follow instructions from [Step 2: Connect to SQL Database of the Managing Azure SQL Database using SQL Server Management Studio][sql-management-studio] article to connect to your Azure SQL server and run the SQL script.</span><span class="sxs-lookup"><span data-stu-id="16716-264">If you have SQL Server 2014 installed on your computer: follow instructions from [Step 2: Connect to SQL Database of the Managing Azure SQL Database using SQL Server Management Studio][sql-management-studio] article to connect to your Azure SQL server and run the SQL script.</span></span>

    <span data-ttu-id="16716-265">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span><span class="sxs-lookup"><span data-stu-id="16716-265">If your client is not allowed to access the Azure SQL server, you need to configure firewall for your Azure SQL server to allow access from your machine (IP Address).</span></span> <span data-ttu-id="16716-266">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="16716-266">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps to configure the firewall for your Azure SQL server.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="16716-267">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="16716-267">Create input dataset</span></span>
<span data-ttu-id="16716-268">In this step, you create a dataset named **AzureBlobInput** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService** linked service.</span><span class="sxs-lookup"><span data-stu-id="16716-268">In this step, you create a dataset named **AzureBlobInput** that points to a blob container in the Azure Storage represented by the **AzureStorageLinkedService** linked service.</span></span> <span data-ttu-id="16716-269">This blob container (adftutorial) contains the input data in the file: **emp.txt**.</span><span class="sxs-lookup"><span data-stu-id="16716-269">This blob container (adftutorial) contains the input data in the file: **emp.txt**.</span></span> 

1. <span data-ttu-id="16716-270">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-270">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-271">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-271">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-272">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-272">View the results.</span></span> <span data-ttu-id="16716-273">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-273">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="16716-274">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="16716-274">Create output dataset</span></span>
<span data-ttu-id="16716-275">In this step, you create an output table named **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="16716-275">In this step, you create an output table named **AzureSqlOutput**.</span></span> <span data-ttu-id="16716-276">This dataset points to a SQL table (emp) in the Azure SQL database represented by **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="16716-276">This dataset points to a SQL table (emp) in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span> <span data-ttu-id="16716-277">The pipeline copies data from the input blob to the **emp** table.</span><span class="sxs-lookup"><span data-stu-id="16716-277">The pipeline copies data from the input blob to the **emp** table.</span></span> 

1. <span data-ttu-id="16716-278">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-278">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-279">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-279">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-280">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-280">View the results.</span></span> <span data-ttu-id="16716-281">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-281">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="16716-282">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="16716-282">Create pipeline</span></span>
<span data-ttu-id="16716-283">In this step, you create a pipeline with a **Copy Activity** that uses **AzureBlobInput** as input and **AzureSqlOutput** as output.</span><span class="sxs-lookup"><span data-stu-id="16716-283">In this step, you create a pipeline with a **Copy Activity** that uses **AzureBlobInput** as input and **AzureSqlOutput** as output.</span></span>

1. <span data-ttu-id="16716-284">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="16716-284">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="16716-285">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="16716-285">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="16716-286">View the results.</span><span class="sxs-lookup"><span data-stu-id="16716-286">View the results.</span></span> <span data-ttu-id="16716-287">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="16716-287">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="16716-288">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="16716-288">**Congratulations!**</span></span> <span data-ttu-id="16716-289">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="16716-289">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="16716-290">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="16716-290">Monitor pipeline</span></span>
<span data-ttu-id="16716-291">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="16716-291">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

<span data-ttu-id="16716-292">Run these commands until you see a slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="16716-292">Run these commands until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="16716-293">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span><span class="sxs-lookup"><span data-stu-id="16716-293">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="16716-294">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="16716-294">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="16716-295">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="16716-295">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="16716-296">Summary</span><span class="sxs-lookup"><span data-stu-id="16716-296">Summary</span></span>
<span data-ttu-id="16716-297">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="16716-297">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="16716-298">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="16716-298">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="16716-299">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="16716-299">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="16716-300">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="16716-300">Created **linked services**:</span></span>
   1. <span data-ttu-id="16716-301">An Azure Storage linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="16716-301">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="16716-302">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="16716-302">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="16716-303">Created **datasets**, which describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="16716-303">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="16716-304">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span><span class="sxs-lookup"><span data-stu-id="16716-304">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="see-also"></a><span data-ttu-id="16716-305">See Also</span><span class="sxs-lookup"><span data-stu-id="16716-305">See Also</span></span>
| <span data-ttu-id="16716-306">Topic</span><span class="sxs-lookup"><span data-stu-id="16716-306">Topic</span></span> | <span data-ttu-id="16716-307">Description</span><span class="sxs-lookup"><span data-stu-id="16716-307">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="16716-308">Data Movement Activities</span><span class="sxs-lookup"><span data-stu-id="16716-308">Data Movement Activities</span></span>](data-factory-data-movement-activities.md) |<span data-ttu-id="16716-309">This article provides detailed information about the Copy Activity you used in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="16716-309">This article provides detailed information about the Copy Activity you used in the tutorial.</span></span> |
| [<span data-ttu-id="16716-310">Scheduling and execution</span><span class="sxs-lookup"><span data-stu-id="16716-310">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="16716-311">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="16716-311">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="16716-312">Pipelines</span><span class="sxs-lookup"><span data-stu-id="16716-312">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="16716-313">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="16716-313">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="16716-314">Datasets</span><span class="sxs-lookup"><span data-stu-id="16716-314">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="16716-315">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="16716-315">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="16716-316">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="16716-316">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="16716-317">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="16716-317">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908

[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[azure-portal]: http://portal.azure.com
[download-azure-powershell]: /powershell/azureps-cmdlets-docs
[data-factory-introduction]: data-factory-introduction.md

[image-data-factory-get-started-storage-explorer]: ./https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-copy-activity-tutorial-using-powershell/getstarted-storage-explorer.png

[sql-management-studio]: ../sql-database/sql-database-manage-azure-ssms.md


