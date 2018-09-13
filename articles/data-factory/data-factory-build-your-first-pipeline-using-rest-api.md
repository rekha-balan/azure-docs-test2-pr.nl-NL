---
title: Build your first data factory (REST) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Data Factory REST API.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/25/2017
ms.author: spelluru
ms.openlocfilehash: 0982d5890ee8c3e865fd7777dbd275bc7fd6f47b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549268"
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="78978-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span><span class="sxs-lookup"><span data-stu-id="78978-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="78978-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-110">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="78978-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="78978-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

> [!NOTE]
> The data pipeline in this tutorial transforms input data to produce output data. It does not copy data from a source data store to a destination data store. For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
> 
> You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information. 

## <a name="prerequisites"></a><span data-ttu-id="78978-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="78978-117">Prerequisites</span></span>
* <span data-ttu-id="78978-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="78978-118">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="78978-119">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span><span class="sxs-lookup"><span data-stu-id="78978-119">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="78978-120">You use the CURL tool with REST commands to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-120">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="78978-121">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span><span class="sxs-lookup"><span data-stu-id="78978-121">Follow instructions from [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="78978-122">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="78978-122">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="78978-123">Get **client ID** and **secret key**.</span><span class="sxs-lookup"><span data-stu-id="78978-123">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="78978-124">Get **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="78978-124">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="78978-125">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="78978-125">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="78978-126">Install [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="78978-126">Install [Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>
* <span data-ttu-id="78978-127">Launch **PowerShell** and run the following command.</span><span class="sxs-lookup"><span data-stu-id="78978-127">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="78978-128">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="78978-128">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="78978-129">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="78978-129">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="78978-130">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="78978-130">Run **Login-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="78978-131">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="78978-131">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="78978-132">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="78978-132">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="78978-133">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="78978-133">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="78978-134">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span><span class="sxs-lookup"><span data-stu-id="78978-134">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="78978-135">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="78978-135">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="78978-136">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="78978-136">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="78978-137">Create JSON definitions</span><span class="sxs-lookup"><span data-stu-id="78978-137">Create JSON definitions</span></span>
<span data-ttu-id="78978-138">Create following JSON files in the folder where curl.exe is located.</span><span class="sxs-lookup"><span data-stu-id="78978-138">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="78978-139">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="78978-139">datafactory.json</span></span>
> [!IMPORTANT]
> Name must be globally unique, so you may want to prefix/suffix ADFCopyTutorialDF to make it a unique name.
>
>

```JSON
{
    "name": "FirstDataFactoryREST",
    "location": "WestUS"
}
```

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="78978-141">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="78978-141">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> Replace **accountname** and **accountkey** with name and key of your Azure storage account. To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/storage-create-storage-account.md#manage-your-storage-account).
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="78978-144">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="78978-144">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.2",
            "clusterSize": 1,
            "timeToLive": "00:30:00",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="78978-145">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="78978-145">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="78978-146">Property</span><span class="sxs-lookup"><span data-stu-id="78978-146">Property</span></span> | <span data-ttu-id="78978-147">Description</span><span class="sxs-lookup"><span data-stu-id="78978-147">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="78978-148">Version</span><span class="sxs-lookup"><span data-stu-id="78978-148">Version</span></span> |<span data-ttu-id="78978-149">Specifies that the version of the HDInsight created to be 3.2.</span><span class="sxs-lookup"><span data-stu-id="78978-149">Specifies that the version of the HDInsight created to be 3.2.</span></span> |
| <span data-ttu-id="78978-150">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="78978-150">ClusterSize</span></span> |<span data-ttu-id="78978-151">Size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-151">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="78978-152">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="78978-152">TimeToLive</span></span> |<span data-ttu-id="78978-153">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="78978-153">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="78978-154">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="78978-154">linkedServiceName</span></span> |<span data-ttu-id="78978-155">Specifies the storage account that is used to store the logs that are generated by HDInsight</span><span class="sxs-lookup"><span data-stu-id="78978-155">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="78978-156">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="78978-156">Note the following points:</span></span>

* <span data-ttu-id="78978-157">The Data Factory creates a **Windows-based** HDInsight cluster for you with the above JSON.</span><span class="sxs-lookup"><span data-stu-id="78978-157">The Data Factory creates a **Windows-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="78978-158">You could also have it create a **Linux-based** HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-158">You could also have it create a **Linux-based** HDInsight cluster.</span></span> <span data-ttu-id="78978-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="78978-159">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="78978-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-160">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="78978-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="78978-161">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="78978-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="78978-162">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="78978-163">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="78978-163">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="78978-164">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="78978-164">This behavior is by design.</span></span> <span data-ttu-id="78978-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="78978-165">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="78978-166">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="78978-166">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="78978-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="78978-167">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="78978-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="78978-168">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="78978-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="78978-169">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="78978-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="78978-170">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="78978-171">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="78978-171">inputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

<span data-ttu-id="78978-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-172">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="78978-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="78978-173">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="78978-174">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="78978-174">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="78978-175">Property</span><span class="sxs-lookup"><span data-stu-id="78978-175">Property</span></span> | <span data-ttu-id="78978-176">Description</span><span class="sxs-lookup"><span data-stu-id="78978-176">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="78978-177">type</span><span class="sxs-lookup"><span data-stu-id="78978-177">type</span></span> |<span data-ttu-id="78978-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="78978-178">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="78978-179">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="78978-179">linkedServiceName</span></span> |<span data-ttu-id="78978-180">refers to the StorageLinkedService you created earlier.</span><span class="sxs-lookup"><span data-stu-id="78978-180">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="78978-181">fileName</span><span class="sxs-lookup"><span data-stu-id="78978-181">fileName</span></span> |<span data-ttu-id="78978-182">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="78978-182">This property is optional.</span></span> <span data-ttu-id="78978-183">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="78978-183">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="78978-184">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="78978-184">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="78978-185">type</span><span class="sxs-lookup"><span data-stu-id="78978-185">type</span></span> |<span data-ttu-id="78978-186">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="78978-186">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="78978-187">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="78978-187">columnDelimiter</span></span> |<span data-ttu-id="78978-188">columns in the log files are delimited by a comma character (,)</span><span class="sxs-lookup"><span data-stu-id="78978-188">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="78978-189">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="78978-189">frequency/interval</span></span> |<span data-ttu-id="78978-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="78978-190">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="78978-191">external</span><span class="sxs-lookup"><span data-stu-id="78978-191">external</span></span> |<span data-ttu-id="78978-192">this property is set to true if the input data is not generated by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="78978-192">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="78978-193">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="78978-193">outputdataset.json</span></span>

```JSON
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="78978-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-194">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="78978-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="78978-195">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="78978-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="78978-196">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="78978-197">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="78978-197">pipeline.json</span></span>
> [!IMPORTANT]
> Replace **storageaccountname** with name of your Azure storage account.
>
>

```JSON
{
    "name": "MyFirstPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [{
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                "scriptLinkedService": "AzureStorageLinkedService",
                "defines": {
                    "inputtable": "wasb://adfgetstarted@<stroageaccountname>.blob.core.windows.net/inputdata",
                    "partitionedtable": "wasb://adfgetstarted@<stroageaccountname>t.blob.core.windows.net/partitioneddata"
                }
            },
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "policy": {
                "concurrency": 1,
                "retry": 3
            },
            "scheduler": {
                "frequency": "Month",
                "interval": 1
            },
            "name": "RunSampleHiveActivity",
            "linkedServiceName": "HDInsightOnDemandLinkedService"
        }],
        "start": "2016-07-10T00:00:00Z",
        "end": "2016-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="78978-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-199">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="78978-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="78978-200">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="78978-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="78978-201">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="78978-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-202">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="78978-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="78978-203">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.
>
>

## <a name="set-global-variables"></a><span data-ttu-id="78978-205">Set global variables</span><span class="sxs-lookup"><span data-stu-id="78978-205">Set global variables</span></span>
<span data-ttu-id="78978-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span><span class="sxs-lookup"><span data-stu-id="78978-206">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

> [!IMPORTANT]
> See [Prerequisites](#prerequisites) section for instructions on getting client ID, client secret, tenant ID, and subscription ID.
>
>

```PowerShell
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
$adf = "FirstDataFactoryREST"
```


## <a name="authenticate-with-aad"></a><span data-ttu-id="78978-208">Authenticate with AAD</span><span class="sxs-lookup"><span data-stu-id="78978-208">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="78978-209">Create data factory</span><span class="sxs-lookup"><span data-stu-id="78978-209">Create data factory</span></span>
<span data-ttu-id="78978-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="78978-210">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="78978-211">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="78978-211">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="78978-212">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="78978-212">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="78978-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform data.</span><span class="sxs-lookup"><span data-stu-id="78978-213">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run Hive script to transform data.</span></span> <span data-ttu-id="78978-214">Run the following commands to create the data factory:</span><span class="sxs-lookup"><span data-stu-id="78978-214">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="78978-215">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-215">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="78978-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="78978-216">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-217">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-217">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-218">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-218">View the results.</span></span> <span data-ttu-id="78978-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-219">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="78978-220">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="78978-220">Note the following points:</span></span>

* <span data-ttu-id="78978-221">The name of the Azure Data Factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="78978-221">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="78978-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="78978-222">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="78978-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="78978-223">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="78978-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="78978-224">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="78978-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span><span class="sxs-lookup"><span data-stu-id="78978-225">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="78978-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="78978-226">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="78978-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="78978-227">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="78978-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="78978-228">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="78978-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="78978-229">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="78978-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="78978-230">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="78978-231">You can run the following command to confirm that the Data Factory provider is registered:</span><span class="sxs-lookup"><span data-stu-id="78978-231">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="78978-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="78978-232">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="78978-233">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="78978-233">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="78978-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="78978-234">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="78978-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span><span class="sxs-lookup"><span data-stu-id="78978-235">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="78978-236">Create linked services</span><span class="sxs-lookup"><span data-stu-id="78978-236">Create linked services</span></span>
<span data-ttu-id="78978-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-237">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="78978-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="78978-238">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="78978-239">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="78978-239">The HDInsight linked service is used to run Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="78978-240">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="78978-240">Create Azure Storage linked service</span></span>
<span data-ttu-id="78978-241">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-241">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="78978-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span><span class="sxs-lookup"><span data-stu-id="78978-242">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="78978-243">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-243">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-244">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-244">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-245">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-245">View the results.</span></span> <span data-ttu-id="78978-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-246">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="78978-247">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="78978-247">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="78978-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-248">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="78978-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="78978-249">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="78978-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-250">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="78978-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="78978-251">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="78978-252">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-252">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-253">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-253">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-254">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-254">View the results.</span></span> <span data-ttu-id="78978-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-255">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="78978-256">Create datasets</span><span class="sxs-lookup"><span data-stu-id="78978-256">Create datasets</span></span>
<span data-ttu-id="78978-257">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="78978-257">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="78978-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="78978-258">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="78978-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="78978-259">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="78978-260">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="78978-260">Create input dataset</span></span>
<span data-ttu-id="78978-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="78978-261">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="78978-262">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-262">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-263">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-263">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-264">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-264">View the results.</span></span> <span data-ttu-id="78978-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-265">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="78978-266">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="78978-266">Create output dataset</span></span>
<span data-ttu-id="78978-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="78978-267">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="78978-268">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-268">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-269">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-269">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-270">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-270">View the results.</span></span> <span data-ttu-id="78978-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-271">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="78978-272">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="78978-272">Create pipeline</span></span>
<span data-ttu-id="78978-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="78978-273">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="78978-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span><span class="sxs-lookup"><span data-stu-id="78978-274">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="78978-275">The settings for the output dataset and the activity scheduler must match.</span><span class="sxs-lookup"><span data-stu-id="78978-275">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="78978-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="78978-276">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="78978-277">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="78978-277">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="78978-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-278">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="78978-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span><span class="sxs-lookup"><span data-stu-id="78978-279">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="78978-280">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="78978-280">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="78978-281">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="78978-281">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="78978-282">View the results.</span><span class="sxs-lookup"><span data-stu-id="78978-282">View the results.</span></span> <span data-ttu-id="78978-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="78978-283">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="78978-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="78978-284">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="78978-285">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="78978-285">Monitor pipeline</span></span>
<span data-ttu-id="78978-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-286">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

```PowerShell
$ds ="AzureBlobOutput"

$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=1970-01-01T00%3a00%3a00.0000000Z"&"end=2016-08-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};

$results2 = Invoke-Command -scriptblock $cmd;

IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

> [!IMPORTANT]
> Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes). Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.
>
>

<span data-ttu-id="78978-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="78978-289">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="78978-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="78978-290">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="78978-291">The creation of an on-demand HDInsight cluster usually takes some time.</span><span class="sxs-lookup"><span data-stu-id="78978-291">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![output data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.
>
>

<span data-ttu-id="78978-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span><span class="sxs-lookup"><span data-stu-id="78978-295">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="78978-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span><span class="sxs-lookup"><span data-stu-id="78978-296">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="78978-297">Summary</span><span class="sxs-lookup"><span data-stu-id="78978-297">Summary</span></span>
<span data-ttu-id="78978-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-298">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="78978-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="78978-299">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="78978-300">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="78978-300">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="78978-301">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="78978-301">Created two **linked services**:</span></span>
   1. <span data-ttu-id="78978-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-302">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="78978-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="78978-303">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="78978-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="78978-304">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="78978-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="78978-305">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="78978-306">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="78978-306">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78978-307">Next steps</span><span class="sxs-lookup"><span data-stu-id="78978-307">Next steps</span></span>
<span data-ttu-id="78978-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="78978-308">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="78978-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="78978-309">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="78978-310">See Also</span><span class="sxs-lookup"><span data-stu-id="78978-310">See Also</span></span>
| <span data-ttu-id="78978-311">Topic</span><span class="sxs-lookup"><span data-stu-id="78978-311">Topic</span></span> | <span data-ttu-id="78978-312">Description</span><span class="sxs-lookup"><span data-stu-id="78978-312">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="78978-313">Data Factory REST API Reference</span><span class="sxs-lookup"><span data-stu-id="78978-313">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="78978-314">See comprehensive documentation on Data Factory cmdlets</span><span class="sxs-lookup"><span data-stu-id="78978-314">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="78978-315">Pipelines</span><span class="sxs-lookup"><span data-stu-id="78978-315">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="78978-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="78978-316">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="78978-317">Datasets</span><span class="sxs-lookup"><span data-stu-id="78978-317">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="78978-318">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78978-318">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="78978-319">Scheduling and Execution</span><span class="sxs-lookup"><span data-stu-id="78978-319">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="78978-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="78978-320">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="78978-321">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="78978-321">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="78978-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="78978-322">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |

