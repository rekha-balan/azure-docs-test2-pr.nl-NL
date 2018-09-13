---
title: 'Tutorial: Use REST API to create an Azure Data Factory pipeline | Microsoft Docs'
description: In this tutorial, you use REST API to create an Azure Data Factory pipeline with a Copy Activity to copy data from an Azure blob storage an Azure SQL database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: ''
editor: ''
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: d5256b2053d75569f9fce71d002aaede9b9e4aa6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856169"
---
# <a name="tutorial-use-rest-api-to-create-an-azure-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="0cae8-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span><span class="sxs-lookup"><span data-stu-id="0cae8-103">Tutorial: Use REST API to create an Azure Data Factory pipeline to copy data</span></span> 
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

> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [copy activity tutorial](../quickstart-create-data-factory-rest-api.md). 

<span data-ttu-id="0cae8-114">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-114">In this article, you learn how to use REST API to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="0cae8-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0cae8-115">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="0cae8-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span><span class="sxs-lookup"><span data-stu-id="0cae8-116">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="0cae8-117">The copy activity copies data from a supported data store to a supported sink data store.</span><span class="sxs-lookup"><span data-stu-id="0cae8-117">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="0cae8-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0cae8-118">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0cae8-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span><span class="sxs-lookup"><span data-stu-id="0cae8-119">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="0cae8-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-120">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="0cae8-121">A pipeline can have more than one activity.</span><span class="sxs-lookup"><span data-stu-id="0cae8-121">A pipeline can have more than one activity.</span></span> <span data-ttu-id="0cae8-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span><span class="sxs-lookup"><span data-stu-id="0cae8-122">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="0cae8-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="0cae8-123">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> This article does not cover all the Data Factory REST API. See [Data Factory REST API Reference](/rest/api/datafactory/) for comprehensive documentation on Data Factory cmdlets.
>  
> The data pipeline in this tutorial copies data from a source data store to a destination data store. For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a><span data-ttu-id="0cae8-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0cae8-128">Prerequisites</span></span>
* <span data-ttu-id="0cae8-129">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="0cae8-129">Go through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="0cae8-130">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span><span class="sxs-lookup"><span data-stu-id="0cae8-130">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="0cae8-131">You use the Curl tool with REST commands to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-131">You use the Curl tool with REST commands to create a data factory.</span></span> 
* <span data-ttu-id="0cae8-132">Follow instructions from [this article](../../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span><span class="sxs-lookup"><span data-stu-id="0cae8-132">Follow instructions from [this article](../../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span> 
  1. <span data-ttu-id="0cae8-133">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-133">Create a Web application named **ADFCopyTutorialApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="0cae8-134">Get **client ID** and **secret key**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-134">Get **client ID** and **secret key**.</span></span> 
  3. <span data-ttu-id="0cae8-135">Get **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-135">Get **tenant ID**.</span></span> 
  4. <span data-ttu-id="0cae8-136">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="0cae8-136">Assign the **ADFCopyTutorialApp** application to the **Data Factory Contributor** role.</span></span>  
* <span data-ttu-id="0cae8-137">Install [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0cae8-137">Install [Azure PowerShell](/powershell/azure/overview).</span></span>  
* <span data-ttu-id="0cae8-138">Launch **PowerShell** and do the following steps.</span><span class="sxs-lookup"><span data-stu-id="0cae8-138">Launch **PowerShell** and do the following steps.</span></span> <span data-ttu-id="0cae8-139">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0cae8-139">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="0cae8-140">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="0cae8-140">If you close and reopen, you need to run the commands again.</span></span>
  
  1. <span data-ttu-id="0cae8-141">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="0cae8-141">Run the following command and enter the user name and password that you use to sign in to the Azure portal:</span></span>
    
    ```PowerShell 
    Connect-AzureRmAccount
    ```   
  2. <span data-ttu-id="0cae8-142">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="0cae8-142">Run the following command to view all the subscriptions for this account:</span></span>

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. <span data-ttu-id="0cae8-143">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="0cae8-143">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="0cae8-144">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0cae8-144">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span> 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. <span data-ttu-id="0cae8-145">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0cae8-145">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      <span data-ttu-id="0cae8-146">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span><span class="sxs-lookup"><span data-stu-id="0cae8-146">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span> 
     
      <span data-ttu-id="0cae8-147">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="0cae8-147">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="0cae8-148">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0cae8-148">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="0cae8-149">Create JSON definitions</span><span class="sxs-lookup"><span data-stu-id="0cae8-149">Create JSON definitions</span></span>
<span data-ttu-id="0cae8-150">Create following JSON files in the folder where curl.exe is located.</span><span class="sxs-lookup"><span data-stu-id="0cae8-150">Create following JSON files in the folder where curl.exe is located.</span></span> 

### <a name="datafactoryjson"></a><span data-ttu-id="0cae8-151">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-151">datafactory.json</span></span>
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

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="0cae8-153">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-153">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> Replace **accountname** and **accountkey** with name and key of your Azure storage account. To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

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

<span data-ttu-id="0cae8-156">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="0cae8-156">For details about JSON properties, see [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span></span>

### <a name="azuersqllinkedservicejson"></a><span data-ttu-id="0cae8-157">azuersqllinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-157">azuersqllinkedservice.json</span></span>
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

<span data-ttu-id="0cae8-159">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0cae8-159">For details about JSON properties, see [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="0cae8-160">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-160">inputdataset.json</span></span>

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

<span data-ttu-id="0cae8-161">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="0cae8-161">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="0cae8-162">Property</span><span class="sxs-lookup"><span data-stu-id="0cae8-162">Property</span></span> | <span data-ttu-id="0cae8-163">Description</span><span class="sxs-lookup"><span data-stu-id="0cae8-163">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cae8-164">type</span><span class="sxs-lookup"><span data-stu-id="0cae8-164">type</span></span> | <span data-ttu-id="0cae8-165">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="0cae8-165">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
| <span data-ttu-id="0cae8-166">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0cae8-166">linkedServiceName</span></span> | <span data-ttu-id="0cae8-167">Refers to the **AzureStorageLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="0cae8-167">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="0cae8-168">folderPath</span><span class="sxs-lookup"><span data-stu-id="0cae8-168">folderPath</span></span> | <span data-ttu-id="0cae8-169">Specifies the blob **container** and the **folder** that contains input blobs.</span><span class="sxs-lookup"><span data-stu-id="0cae8-169">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="0cae8-170">In this tutorial, adftutorial is the blob container and folder is the root folder.</span><span class="sxs-lookup"><span data-stu-id="0cae8-170">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
| <span data-ttu-id="0cae8-171">fileName</span><span class="sxs-lookup"><span data-stu-id="0cae8-171">fileName</span></span> | <span data-ttu-id="0cae8-172">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="0cae8-172">This property is optional.</span></span> <span data-ttu-id="0cae8-173">If you omit this property, all files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="0cae8-173">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="0cae8-174">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span><span class="sxs-lookup"><span data-stu-id="0cae8-174">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
| <span data-ttu-id="0cae8-175">format -> type</span><span class="sxs-lookup"><span data-stu-id="0cae8-175">format -> type</span></span> |<span data-ttu-id="0cae8-176">The input file is in the text format, so we use **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-176">The input file is in the text format, so we use **TextFormat**.</span></span> |
| <span data-ttu-id="0cae8-177">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="0cae8-177">columnDelimiter</span></span> | <span data-ttu-id="0cae8-178">The columns in the input file are delimited by **comma character (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-178">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
| <span data-ttu-id="0cae8-179">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="0cae8-179">frequency/interval</span></span> | <span data-ttu-id="0cae8-180">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-180">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="0cae8-181">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span><span class="sxs-lookup"><span data-stu-id="0cae8-181">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="0cae8-182">It looks for the data within the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="0cae8-182">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
| <span data-ttu-id="0cae8-183">external</span><span class="sxs-lookup"><span data-stu-id="0cae8-183">external</span></span> | <span data-ttu-id="0cae8-184">This property is set to **true** if the data is not generated by this pipeline.</span><span class="sxs-lookup"><span data-stu-id="0cae8-184">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="0cae8-185">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span><span class="sxs-lookup"><span data-stu-id="0cae8-185">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

<span data-ttu-id="0cae8-186">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cae8-186">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>

### <a name="outputdatasetjson"></a><span data-ttu-id="0cae8-187">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-187">outputdataset.json</span></span>

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
<span data-ttu-id="0cae8-188">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="0cae8-188">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="0cae8-189">Property</span><span class="sxs-lookup"><span data-stu-id="0cae8-189">Property</span></span> | <span data-ttu-id="0cae8-190">Description</span><span class="sxs-lookup"><span data-stu-id="0cae8-190">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cae8-191">type</span><span class="sxs-lookup"><span data-stu-id="0cae8-191">type</span></span> | <span data-ttu-id="0cae8-192">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-192">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
| <span data-ttu-id="0cae8-193">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="0cae8-193">linkedServiceName</span></span> | <span data-ttu-id="0cae8-194">Refers to the **AzureSqlLinkedService** that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="0cae8-194">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
| <span data-ttu-id="0cae8-195">tableName</span><span class="sxs-lookup"><span data-stu-id="0cae8-195">tableName</span></span> | <span data-ttu-id="0cae8-196">Specified the **table** to which the data is copied.</span><span class="sxs-lookup"><span data-stu-id="0cae8-196">Specified the **table** to which the data is copied.</span></span> | 
| <span data-ttu-id="0cae8-197">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="0cae8-197">frequency/interval</span></span> | <span data-ttu-id="0cae8-198">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span><span class="sxs-lookup"><span data-stu-id="0cae8-198">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

<span data-ttu-id="0cae8-199">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-199">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="0cae8-200">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span><span class="sxs-lookup"><span data-stu-id="0cae8-200">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

<span data-ttu-id="0cae8-201">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0cae8-201">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="0cae8-202">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="0cae8-202">pipeline.json</span></span>

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
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

<span data-ttu-id="0cae8-203">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="0cae8-203">Note the following points:</span></span>

- <span data-ttu-id="0cae8-204">In the activities section, there is only one activity whose **type** is set to **Copy**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-204">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="0cae8-205">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-205">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="0cae8-206">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-206">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
- <span data-ttu-id="0cae8-207">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-207">Input for the activity is set to **AzureBlobInput** and output for the activity is set to **AzureSqlOutput**.</span></span> 
- <span data-ttu-id="0cae8-208">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span><span class="sxs-lookup"><span data-stu-id="0cae8-208">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="0cae8-209">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0cae8-209">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0cae8-210">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span><span class="sxs-lookup"><span data-stu-id="0cae8-210">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
 
<span data-ttu-id="0cae8-211">Replace the value of the **start** property with the current day and **end** value with the next day.</span><span class="sxs-lookup"><span data-stu-id="0cae8-211">Replace the value of the **start** property with the current day and **end** value with the next day.</span></span> <span data-ttu-id="0cae8-212">You can specify only the date part and skip the time part of the date time.</span><span class="sxs-lookup"><span data-stu-id="0cae8-212">You can specify only the date part and skip the time part of the date time.</span></span> <span data-ttu-id="0cae8-213">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="0cae8-213">For example, "2017-02-03", which is equivalent to "2017-02-03T00:00:00Z"</span></span>
 
<span data-ttu-id="0cae8-214">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="0cae8-214">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="0cae8-215">For example: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="0cae8-215">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="0cae8-216">The **end** time is optional, but we use it in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="0cae8-216">The **end** time is optional, but we use it in this tutorial.</span></span> 
 
<span data-ttu-id="0cae8-217">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span><span class="sxs-lookup"><span data-stu-id="0cae8-217">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="0cae8-218">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="0cae8-218">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
 
<span data-ttu-id="0cae8-219">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span><span class="sxs-lookup"><span data-stu-id="0cae8-219">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

<span data-ttu-id="0cae8-220">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span><span class="sxs-lookup"><span data-stu-id="0cae8-220">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0cae8-221">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-221">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="0cae8-222">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-222">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="0cae8-223">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-223">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="0cae8-224">Set global variables</span><span class="sxs-lookup"><span data-stu-id="0cae8-224">Set global variables</span></span>
<span data-ttu-id="0cae8-225">In Azure PowerShell, execute the following commands after replacing the values with your own:</span><span class="sxs-lookup"><span data-stu-id="0cae8-225">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

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
```

<span data-ttu-id="0cae8-227">Run the following command after updating the name of the data factory you are using:</span><span class="sxs-lookup"><span data-stu-id="0cae8-227">Run the following command after updating the name of the data factory you are using:</span></span> 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a><span data-ttu-id="0cae8-228">Authenticate with AAD</span><span class="sxs-lookup"><span data-stu-id="0cae8-228">Authenticate with AAD</span></span>
<span data-ttu-id="0cae8-229">Run the following command to authenticate with Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="0cae8-229">Run the following command to authenticate with Azure Active Directory (AAD):</span></span> 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a><span data-ttu-id="0cae8-230">Create data factory</span><span class="sxs-lookup"><span data-stu-id="0cae8-230">Create data factory</span></span>
<span data-ttu-id="0cae8-231">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-231">In this step, you create an Azure Data Factory named **ADFCopyTutorialDF**.</span></span> <span data-ttu-id="0cae8-232">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="0cae8-232">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="0cae8-233">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="0cae8-233">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="0cae8-234">For example, a Copy Activity to copy data from a source to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="0cae8-234">For example, a Copy Activity to copy data from a source to a destination data store.</span></span> <span data-ttu-id="0cae8-235">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span><span class="sxs-lookup"><span data-stu-id="0cae8-235">A HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="0cae8-236">Run the following commands to create the data factory:</span><span class="sxs-lookup"><span data-stu-id="0cae8-236">Run the following commands to create the data factory:</span></span> 

1. <span data-ttu-id="0cae8-237">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-237">Assign the command to variable named **cmd**.</span></span> 
   
    > [!IMPORTANT]
    > Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-239">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-239">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-240">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-240">View the results.</span></span> <span data-ttu-id="0cae8-241">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-241">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>  
   
    ```
    Write-Host $results
    ```

<span data-ttu-id="0cae8-242">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="0cae8-242">Note the following points:</span></span>

* <span data-ttu-id="0cae8-243">The name of the Azure Data Factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="0cae8-243">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="0cae8-244">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="0cae8-244">If you see the error in results: **Data factory name “ADFCopyTutorialDF” is not available**, do the following steps:</span></span>  
  
  1. <span data-ttu-id="0cae8-245">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="0cae8-245">Change the name (for example, yournameADFCopyTutorialDF) in the **datafactory.json** file.</span></span>
  2. <span data-ttu-id="0cae8-246">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span><span class="sxs-lookup"><span data-stu-id="0cae8-246">In the first command where the **$cmd** variable is assigned a value, replace ADFCopyTutorialDF with the new name and run the command.</span></span> 
  3. <span data-ttu-id="0cae8-247">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="0cae8-247">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span> 
     
     <span data-ttu-id="0cae8-248">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="0cae8-248">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="0cae8-249">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="0cae8-249">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="0cae8-250">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="0cae8-250">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="0cae8-251">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="0cae8-251">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span> 
  
  * <span data-ttu-id="0cae8-252">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="0cae8-252">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="0cae8-253">You can run the following command to confirm that the Data Factory provider is registered.</span><span class="sxs-lookup"><span data-stu-id="0cae8-253">You can run the following command to confirm that the Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="0cae8-254">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cae8-254">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="0cae8-255">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="0cae8-255">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="0cae8-256">Before creating a pipeline, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="0cae8-256">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="0cae8-257">You first create linked services to link source and destination data stores to your data store.</span><span class="sxs-lookup"><span data-stu-id="0cae8-257">You first create linked services to link source and destination data stores to your data store.</span></span> <span data-ttu-id="0cae8-258">Then, define input and output datasets to represent data in linked data stores.</span><span class="sxs-lookup"><span data-stu-id="0cae8-258">Then, define input and output datasets to represent data in linked data stores.</span></span> <span data-ttu-id="0cae8-259">Finally, create the pipeline with an activity that uses these datasets.</span><span class="sxs-lookup"><span data-stu-id="0cae8-259">Finally, create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="0cae8-260">Create linked services</span><span class="sxs-lookup"><span data-stu-id="0cae8-260">Create linked services</span></span>
<span data-ttu-id="0cae8-261">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-261">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="0cae8-262">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0cae8-262">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="0cae8-263">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span><span class="sxs-lookup"><span data-stu-id="0cae8-263">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> <span data-ttu-id="0cae8-264">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="0cae8-264">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="0cae8-265">The AzureStorageLinkedService links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-265">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="0cae8-266">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-266">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="0cae8-267">AzureSqlLinkedService links your Azure SQL database to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-267">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="0cae8-268">The data that is copied from the blob storage is stored in this database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-268">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="0cae8-269">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="0cae8-269">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="0cae8-270">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="0cae8-270">Create Azure Storage linked service</span></span>
<span data-ttu-id="0cae8-271">In this step, you link your Azure storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-271">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="0cae8-272">You specify the name and key of your Azure storage account in this section.</span><span class="sxs-lookup"><span data-stu-id="0cae8-272">You specify the name and key of your Azure storage account in this section.</span></span> <span data-ttu-id="0cae8-273">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="0cae8-273">See [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span>  

1. <span data-ttu-id="0cae8-274">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-274">Assign the command to variable named **cmd**.</span></span> 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-275">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-275">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-276">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-276">View the results.</span></span> <span data-ttu-id="0cae8-277">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-277">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a><span data-ttu-id="0cae8-278">Create Azure SQL linked service</span><span class="sxs-lookup"><span data-stu-id="0cae8-278">Create Azure SQL linked service</span></span>
<span data-ttu-id="0cae8-279">In this step, you link your Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-279">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="0cae8-280">You specify the Azure SQL server name, database name, user name, and user password in this section.</span><span class="sxs-lookup"><span data-stu-id="0cae8-280">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> <span data-ttu-id="0cae8-281">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span><span class="sxs-lookup"><span data-stu-id="0cae8-281">See [Azure SQL linked service](data-factory-azure-sql-connector.md#linked-service-properties) for details about JSON properties used to define an Azure SQL linked service.</span></span>

1. <span data-ttu-id="0cae8-282">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-282">Assign the command to variable named **cmd**.</span></span> 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-283">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-283">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-284">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-284">View the results.</span></span> <span data-ttu-id="0cae8-285">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-285">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="0cae8-286">Create datasets</span><span class="sxs-lookup"><span data-stu-id="0cae8-286">Create datasets</span></span>
<span data-ttu-id="0cae8-287">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span><span class="sxs-lookup"><span data-stu-id="0cae8-287">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="0cae8-288">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span><span class="sxs-lookup"><span data-stu-id="0cae8-288">In this step, you define two datasets named AzureBlobInput and AzureSqlOutput that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="0cae8-289">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="0cae8-289">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="0cae8-290">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="0cae8-290">And, the input blob dataset (AzureBlobInput) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="0cae8-291">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-291">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="0cae8-292">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="0cae8-292">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="0cae8-293">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="0cae8-293">Create input dataset</span></span>
<span data-ttu-id="0cae8-294">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span><span class="sxs-lookup"><span data-stu-id="0cae8-294">In this step, you create a dataset named AzureBlobInput that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="0cae8-295">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span><span class="sxs-lookup"><span data-stu-id="0cae8-295">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="0cae8-296">In this tutorial, you specify a value for the fileName.</span><span class="sxs-lookup"><span data-stu-id="0cae8-296">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="0cae8-297">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-297">Assign the command to variable named **cmd**.</span></span> 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-298">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-298">Run the command by using **Invoke-Command**.</span></span>
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-299">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-299">View the results.</span></span> <span data-ttu-id="0cae8-300">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-300">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="0cae8-301">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="0cae8-301">Create output dataset</span></span>
<span data-ttu-id="0cae8-302">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-302">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="0cae8-303">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span><span class="sxs-lookup"><span data-stu-id="0cae8-303">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="0cae8-304">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-304">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-305">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-305">Run the command by using **Invoke-Command**.</span></span>
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-306">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-306">View the results.</span></span> <span data-ttu-id="0cae8-307">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-307">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a><span data-ttu-id="0cae8-308">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="0cae8-308">Create pipeline</span></span>
<span data-ttu-id="0cae8-309">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span><span class="sxs-lookup"><span data-stu-id="0cae8-309">In this step, you create a pipeline with a **copy activity** that uses **AzureBlobInput** as an input and **AzureSqlOutput** as an output.</span></span>

<span data-ttu-id="0cae8-310">Currently, output dataset is what drives the schedule.</span><span class="sxs-lookup"><span data-stu-id="0cae8-310">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="0cae8-311">In this tutorial, output dataset is configured to produce a slice once an hour.</span><span class="sxs-lookup"><span data-stu-id="0cae8-311">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="0cae8-312">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span><span class="sxs-lookup"><span data-stu-id="0cae8-312">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="0cae8-313">Therefore, 24 slices of output dataset are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0cae8-313">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="0cae8-314">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-314">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="0cae8-315">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-315">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="0cae8-316">View the results.</span><span class="sxs-lookup"><span data-stu-id="0cae8-316">View the results.</span></span> <span data-ttu-id="0cae8-317">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="0cae8-317">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>  

    ```PowerShell   
    Write-Host $results
    ```

<span data-ttu-id="0cae8-318">**Congratulations!**</span><span class="sxs-lookup"><span data-stu-id="0cae8-318">**Congratulations!**</span></span> <span data-ttu-id="0cae8-319">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-319">You have successfully created an Azure data factory, with a pipeline that copies data from Azure Blob Storage to Azure SQL database.</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="0cae8-320">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="0cae8-320">Monitor pipeline</span></span>
<span data-ttu-id="0cae8-321">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="0cae8-321">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Make sure that the start and end times specified in the following command match the start and end times of the pipeline. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
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

<span data-ttu-id="0cae8-323">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="0cae8-323">Run the Invoke-Command and the next one until you see a slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="0cae8-324">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span><span class="sxs-lookup"><span data-stu-id="0cae8-324">When the slice is in Ready state, check the **emp** table in your Azure SQL database for the output data.</span></span> 

<span data-ttu-id="0cae8-325">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-325">For each slice, two rows of data from the source file are copied to the emp table in the Azure SQL database.</span></span> <span data-ttu-id="0cae8-326">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span><span class="sxs-lookup"><span data-stu-id="0cae8-326">Therefore, you see 24 new records in the emp table when all the slices are successfully processed (in Ready state).</span></span> 

## <a name="summary"></a><span data-ttu-id="0cae8-327">Summary</span><span class="sxs-lookup"><span data-stu-id="0cae8-327">Summary</span></span>
<span data-ttu-id="0cae8-328">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="0cae8-328">In this tutorial, you used REST API to create an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="0cae8-329">Here are the high-level steps you performed in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="0cae8-329">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="0cae8-330">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="0cae8-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="0cae8-331">Created **linked services**:</span><span class="sxs-lookup"><span data-stu-id="0cae8-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="0cae8-332">An Azure Storage linked service to link your Azure Storage account that holds input data.</span><span class="sxs-lookup"><span data-stu-id="0cae8-332">An Azure Storage linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="0cae8-333">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="0cae8-333">An Azure SQL linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="0cae8-334">Created **datasets**, which describe input data and output data for pipelines.</span><span class="sxs-lookup"><span data-stu-id="0cae8-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="0cae8-335">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span><span class="sxs-lookup"><span data-stu-id="0cae8-335">Created a **pipeline** with a Copy Activity with BlobSource as source and SqlSink as sink.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0cae8-336">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cae8-336">Next steps</span></span>
<span data-ttu-id="0cae8-337">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span><span class="sxs-lookup"><span data-stu-id="0cae8-337">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="0cae8-338">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span><span class="sxs-lookup"><span data-stu-id="0cae8-338">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="0cae8-339">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span><span class="sxs-lookup"><span data-stu-id="0cae8-339">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>
