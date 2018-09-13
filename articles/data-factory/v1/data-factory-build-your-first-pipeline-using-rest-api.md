---
title: Build your first data factory (REST) | Microsoft Docs
description: In this tutorial, you create a sample Azure Data Factory pipeline using Data Factory REST API.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 7e0a2465-2d85-4143-a4bb-42e03c273097
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 11/01/2017
ms.author: shlo
robots: noindex
ms.openlocfilehash: d0bb951e7392eb0f818ed0e9b5c17e203f94e753
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870834"
---
# <a name="tutorial-build-your-first-azure-data-factory-using-data-factory-rest-api"></a><span data-ttu-id="af1ff-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span><span class="sxs-lookup"><span data-stu-id="af1ff-103">Tutorial: Build your first Azure data factory using Data Factory REST API</span></span>
> [!div class="op_single_selector"]
> * [Overview and prerequisites](data-factory-build-your-first-pipeline.md)
> * [Azure portal](data-factory-build-your-first-pipeline-using-editor.md)
> * [Visual Studio](data-factory-build-your-first-pipeline-using-vs.md)
> * [PowerShell](data-factory-build-your-first-pipeline-using-powershell.md)
> * [Resource Manager Template](data-factory-build-your-first-pipeline-using-arm.md)
> * [REST API](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>


> [!NOTE]
> This article applies to version 1 of Data Factory. If you are using the current version of the Data Factory service, see [Quickstart: Create a data factory using Azure Data Factory](../quickstart-create-data-factory-rest-api.md).

<span data-ttu-id="af1ff-112">In this article, you use Data Factory REST API to create your first Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-112">In this article, you use Data Factory REST API to create your first Azure data factory.</span></span> <span data-ttu-id="af1ff-113">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="af1ff-113">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="af1ff-114">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-114">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="af1ff-115">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span><span class="sxs-lookup"><span data-stu-id="af1ff-115">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="af1ff-116">The pipeline is scheduled to run once a month between the specified start and end times.</span><span class="sxs-lookup"><span data-stu-id="af1ff-116">The pipeline is scheduled to run once a month between the specified start and end times.</span></span>

> [!NOTE]
> This article does not cover all the REST API. For comprehensive documentation on REST API, see [Data Factory REST API Reference](/rest/api/datafactory/).
> 
> A pipeline can have more than one activity. And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity. For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).


## <a name="prerequisites"></a><span data-ttu-id="af1ff-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af1ff-122">Prerequisites</span></span>
* <span data-ttu-id="af1ff-123">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span><span class="sxs-lookup"><span data-stu-id="af1ff-123">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="af1ff-124">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span><span class="sxs-lookup"><span data-stu-id="af1ff-124">Install [Curl](https://curl.haxx.se/dlwiz/) on your machine.</span></span> <span data-ttu-id="af1ff-125">You use the CURL tool with REST commands to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-125">You use the CURL tool with REST commands to create a data factory.</span></span>
* <span data-ttu-id="af1ff-126">Follow instructions from [this article](../../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span><span class="sxs-lookup"><span data-stu-id="af1ff-126">Follow instructions from [this article](../../azure-resource-manager/resource-group-create-service-principal-portal.md) to:</span></span>
  1. <span data-ttu-id="af1ff-127">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-127">Create a Web application named **ADFGetStartedApp** in Azure Active Directory.</span></span>
  2. <span data-ttu-id="af1ff-128">Get **client ID** and **secret key**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-128">Get **client ID** and **secret key**.</span></span>
  3. <span data-ttu-id="af1ff-129">Get **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-129">Get **tenant ID**.</span></span>
  4. <span data-ttu-id="af1ff-130">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="af1ff-130">Assign the **ADFGetStartedApp** application to the **Data Factory Contributor** role.</span></span>
* <span data-ttu-id="af1ff-131">Install [Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="af1ff-131">Install [Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="af1ff-132">Launch **PowerShell** and run the following command.</span><span class="sxs-lookup"><span data-stu-id="af1ff-132">Launch **PowerShell** and run the following command.</span></span> <span data-ttu-id="af1ff-133">Keep Azure PowerShell open until the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="af1ff-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="af1ff-134">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="af1ff-134">If you close and reopen, you need to run the commands again.</span></span>
  1. <span data-ttu-id="af1ff-135">Run **Connect-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="af1ff-135">Run **Connect-AzureRmAccount** and enter the user name and password that you use to sign in to the Azure portal.</span></span>
  2. <span data-ttu-id="af1ff-136">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span><span class="sxs-lookup"><span data-stu-id="af1ff-136">Run **Get-AzureRmSubscription** to view all the subscriptions for this account.</span></span>
  3. <span data-ttu-id="af1ff-137">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="af1ff-137">Run **Get-AzureRmSubscription -SubscriptionName NameOfAzureSubscription | Set-AzureRmContext** to select the subscription that you want to work with.</span></span> <span data-ttu-id="af1ff-138">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="af1ff-138">Replace **NameOfAzureSubscription** with the name of your Azure subscription.</span></span>
* <span data-ttu-id="af1ff-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span><span class="sxs-lookup"><span data-stu-id="af1ff-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

   <span data-ttu-id="af1ff-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="af1ff-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="af1ff-141">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="af1ff-141">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>

## <a name="create-json-definitions"></a><span data-ttu-id="af1ff-142">Create JSON definitions</span><span class="sxs-lookup"><span data-stu-id="af1ff-142">Create JSON definitions</span></span>
<span data-ttu-id="af1ff-143">Create following JSON files in the folder where curl.exe is located.</span><span class="sxs-lookup"><span data-stu-id="af1ff-143">Create following JSON files in the folder where curl.exe is located.</span></span>

### <a name="datafactoryjson"></a><span data-ttu-id="af1ff-144">datafactory.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-144">datafactory.json</span></span>
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

### <a name="azurestoragelinkedservicejson"></a><span data-ttu-id="af1ff-146">azurestoragelinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-146">azurestoragelinkedservice.json</span></span>
> [!IMPORTANT]
> Replace **accountname** and **accountkey** with name and key of your Azure storage account. To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).
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

### <a name="hdinsightondemandlinkedservicejson"></a><span data-ttu-id="af1ff-149">hdinsightondemandlinkedservice.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-149">hdinsightondemandlinkedservice.json</span></span>

```JSON
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

<span data-ttu-id="af1ff-150">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="af1ff-150">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="af1ff-151">Property</span><span class="sxs-lookup"><span data-stu-id="af1ff-151">Property</span></span> | <span data-ttu-id="af1ff-152">Description</span><span class="sxs-lookup"><span data-stu-id="af1ff-152">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af1ff-153">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="af1ff-153">ClusterSize</span></span> |<span data-ttu-id="af1ff-154">Size of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-154">Size of the HDInsight cluster.</span></span> |
| <span data-ttu-id="af1ff-155">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="af1ff-155">TimeToLive</span></span> |<span data-ttu-id="af1ff-156">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span><span class="sxs-lookup"><span data-stu-id="af1ff-156">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
| <span data-ttu-id="af1ff-157">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="af1ff-157">linkedServiceName</span></span> |<span data-ttu-id="af1ff-158">Specifies the storage account that is used to store the logs that are generated by HDInsight</span><span class="sxs-lookup"><span data-stu-id="af1ff-158">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

<span data-ttu-id="af1ff-159">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="af1ff-159">Note the following points:</span></span>

* <span data-ttu-id="af1ff-160">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span><span class="sxs-lookup"><span data-stu-id="af1ff-160">The Data Factory creates a **Linux-based** HDInsight cluster for you with the above JSON.</span></span> <span data-ttu-id="af1ff-161">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="af1ff-161">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
* <span data-ttu-id="af1ff-162">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-162">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="af1ff-163">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="af1ff-163">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
* <span data-ttu-id="af1ff-164">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="af1ff-164">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="af1ff-165">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="af1ff-165">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="af1ff-166">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="af1ff-166">This behavior is by design.</span></span> <span data-ttu-id="af1ff-167">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="af1ff-167">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

    <span data-ttu-id="af1ff-168">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="af1ff-168">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="af1ff-169">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="af1ff-169">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="af1ff-170">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="af1ff-170">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="af1ff-171">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="af1ff-171">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

<span data-ttu-id="af1ff-172">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="af1ff-172">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

### <a name="inputdatasetjson"></a><span data-ttu-id="af1ff-173">inputdataset.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-173">inputdataset.json</span></span>

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

<span data-ttu-id="af1ff-174">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-174">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="af1ff-175">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-175">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

<span data-ttu-id="af1ff-176">The following table provides descriptions for the JSON properties used in the snippet:</span><span class="sxs-lookup"><span data-stu-id="af1ff-176">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

| <span data-ttu-id="af1ff-177">Property</span><span class="sxs-lookup"><span data-stu-id="af1ff-177">Property</span></span> | <span data-ttu-id="af1ff-178">Description</span><span class="sxs-lookup"><span data-stu-id="af1ff-178">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="af1ff-179">type</span><span class="sxs-lookup"><span data-stu-id="af1ff-179">type</span></span> |<span data-ttu-id="af1ff-180">The type property is set to AzureBlob because data resides in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="af1ff-180">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
| <span data-ttu-id="af1ff-181">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="af1ff-181">linkedServiceName</span></span> |<span data-ttu-id="af1ff-182">refers to the StorageLinkedService you created earlier.</span><span class="sxs-lookup"><span data-stu-id="af1ff-182">refers to the StorageLinkedService you created earlier.</span></span> |
| <span data-ttu-id="af1ff-183">fileName</span><span class="sxs-lookup"><span data-stu-id="af1ff-183">fileName</span></span> |<span data-ttu-id="af1ff-184">This property is optional.</span><span class="sxs-lookup"><span data-stu-id="af1ff-184">This property is optional.</span></span> <span data-ttu-id="af1ff-185">If you omit this property, all the files from the folderPath are picked.</span><span class="sxs-lookup"><span data-stu-id="af1ff-185">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="af1ff-186">In this case, only the input.log is processed.</span><span class="sxs-lookup"><span data-stu-id="af1ff-186">In this case, only the input.log is processed.</span></span> |
| <span data-ttu-id="af1ff-187">type</span><span class="sxs-lookup"><span data-stu-id="af1ff-187">type</span></span> |<span data-ttu-id="af1ff-188">The log files are in text format, so we use TextFormat.</span><span class="sxs-lookup"><span data-stu-id="af1ff-188">The log files are in text format, so we use TextFormat.</span></span> |
| <span data-ttu-id="af1ff-189">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="af1ff-189">columnDelimiter</span></span> |<span data-ttu-id="af1ff-190">columns in the log files are delimited by a comma character (,)</span><span class="sxs-lookup"><span data-stu-id="af1ff-190">columns in the log files are delimited by a comma character (,)</span></span> |
| <span data-ttu-id="af1ff-191">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="af1ff-191">frequency/interval</span></span> |<span data-ttu-id="af1ff-192">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span><span class="sxs-lookup"><span data-stu-id="af1ff-192">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
| <span data-ttu-id="af1ff-193">external</span><span class="sxs-lookup"><span data-stu-id="af1ff-193">external</span></span> |<span data-ttu-id="af1ff-194">this property is set to true if the input data is not generated by the Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="af1ff-194">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |

### <a name="outputdatasetjson"></a><span data-ttu-id="af1ff-195">outputdataset.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-195">outputdataset.json</span></span>

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

<span data-ttu-id="af1ff-196">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-196">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="af1ff-197">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-197">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="af1ff-198">The **availability** section specifies that the output dataset is produced on a monthly basis.</span><span class="sxs-lookup"><span data-stu-id="af1ff-198">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

### <a name="pipelinejson"></a><span data-ttu-id="af1ff-199">pipeline.json</span><span class="sxs-lookup"><span data-stu-id="af1ff-199">pipeline.json</span></span>
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
        "start": "2017-07-10T00:00:00Z",
        "end": "2017-07-11T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="af1ff-201">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-201">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process data on a HDInsight cluster.</span></span>

<span data-ttu-id="af1ff-202">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-202">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

<span data-ttu-id="af1ff-203">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span><span class="sxs-lookup"><span data-stu-id="af1ff-203">The **defines** section specifies runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

<span data-ttu-id="af1ff-204">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-204">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

<span data-ttu-id="af1ff-205">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-205">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

> [!NOTE]
> See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the preceding example.
>
>

## <a name="set-global-variables"></a><span data-ttu-id="af1ff-207">Set global variables</span><span class="sxs-lookup"><span data-stu-id="af1ff-207">Set global variables</span></span>
<span data-ttu-id="af1ff-208">In Azure PowerShell, execute the following commands after replacing the values with your own:</span><span class="sxs-lookup"><span data-stu-id="af1ff-208">In Azure PowerShell, execute the following commands after replacing the values with your own:</span></span>

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


## <a name="authenticate-with-aad"></a><span data-ttu-id="af1ff-210">Authenticate with AAD</span><span class="sxs-lookup"><span data-stu-id="af1ff-210">Authenticate with AAD</span></span>

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken)
```


## <a name="create-data-factory"></a><span data-ttu-id="af1ff-211">Create data factory</span><span class="sxs-lookup"><span data-stu-id="af1ff-211">Create data factory</span></span>
<span data-ttu-id="af1ff-212">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-212">In this step, you create an Azure Data Factory named **FirstDataFactoryREST**.</span></span> <span data-ttu-id="af1ff-213">A data factory can have one or more pipelines.</span><span class="sxs-lookup"><span data-stu-id="af1ff-213">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="af1ff-214">A pipeline can have one or more activities in it.</span><span class="sxs-lookup"><span data-stu-id="af1ff-214">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="af1ff-215">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span><span class="sxs-lookup"><span data-stu-id="af1ff-215">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform data.</span></span> <span data-ttu-id="af1ff-216">Run the following commands to create the data factory:</span><span class="sxs-lookup"><span data-stu-id="af1ff-216">Run the following commands to create the data factory:</span></span>

1. <span data-ttu-id="af1ff-217">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-217">Assign the command to variable named **cmd**.</span></span>

    <span data-ttu-id="af1ff-218">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-218">Confirm that the name of the data factory you specify here (ADFCopyTutorialDF) matches the name specified in the **datafactory.json**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/FirstDataFactoryREST?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-219">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-219">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-220">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-220">View the results.</span></span> <span data-ttu-id="af1ff-221">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-221">If the data factory has been successfully created, you see the JSON for the data factory in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

<span data-ttu-id="af1ff-222">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="af1ff-222">Note the following points:</span></span>

* <span data-ttu-id="af1ff-223">The name of the Azure Data Factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="af1ff-223">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="af1ff-224">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="af1ff-224">If you see the error in results: **Data factory name “FirstDataFactoryREST” is not available**, do the following steps:</span></span>
  1. <span data-ttu-id="af1ff-225">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span><span class="sxs-lookup"><span data-stu-id="af1ff-225">Change the name (for example, yournameFirstDataFactoryREST) in the **datafactory.json** file.</span></span> <span data-ttu-id="af1ff-226">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="af1ff-226">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
  2. <span data-ttu-id="af1ff-227">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span><span class="sxs-lookup"><span data-stu-id="af1ff-227">In the first command where the **$cmd** variable is assigned a value, replace FirstDataFactoryREST with the new name and run the command.</span></span>
  3. <span data-ttu-id="af1ff-228">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="af1ff-228">Run the next two commands to invoke the REST API to create the data factory and print the results of the operation.</span></span>
* <span data-ttu-id="af1ff-229">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span><span class="sxs-lookup"><span data-stu-id="af1ff-229">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="af1ff-230">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span><span class="sxs-lookup"><span data-stu-id="af1ff-230">The name of the data factory may be registered as a DNS name in the future and hence become publicly visible.</span></span>
* <span data-ttu-id="af1ff-231">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span><span class="sxs-lookup"><span data-stu-id="af1ff-231">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="af1ff-232">In Azure PowerShell, run the following command to register the Data Factory provider:</span><span class="sxs-lookup"><span data-stu-id="af1ff-232">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

      <span data-ttu-id="af1ff-233">You can run the following command to confirm that the Data Factory provider is registered:</span><span class="sxs-lookup"><span data-stu-id="af1ff-233">You can run the following command to confirm that the Data Factory provider is registered:</span></span>
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="af1ff-234">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="af1ff-234">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="af1ff-235">This action automatically registers the provider for you.</span><span class="sxs-lookup"><span data-stu-id="af1ff-235">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="af1ff-236">Before creating a pipeline, you need to create a few Data Factory entities first.</span><span class="sxs-lookup"><span data-stu-id="af1ff-236">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="af1ff-237">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span><span class="sxs-lookup"><span data-stu-id="af1ff-237">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent data in linked data stores.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="af1ff-238">Create linked services</span><span class="sxs-lookup"><span data-stu-id="af1ff-238">Create linked services</span></span>
<span data-ttu-id="af1ff-239">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-239">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="af1ff-240">The Azure Storage account holds the input and output data for the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="af1ff-240">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="af1ff-241">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span><span class="sxs-lookup"><span data-stu-id="af1ff-241">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="af1ff-242">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="af1ff-242">Create Azure Storage linked service</span></span>
<span data-ttu-id="af1ff-243">In this step, you link your Azure Storage account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-243">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="af1ff-244">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span><span class="sxs-lookup"><span data-stu-id="af1ff-244">With this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="af1ff-245">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-245">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azurestoragelinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-246">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-246">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-247">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-247">View the results.</span></span> <span data-ttu-id="af1ff-248">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-248">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="af1ff-249">Create Azure HDInsight linked service</span><span class="sxs-lookup"><span data-stu-id="af1ff-249">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="af1ff-250">In this step, you link an on-demand HDInsight cluster to your data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-250">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="af1ff-251">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span><span class="sxs-lookup"><span data-stu-id="af1ff-251">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="af1ff-252">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-252">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="af1ff-253">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span><span class="sxs-lookup"><span data-stu-id="af1ff-253">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="af1ff-254">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-254">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@hdinsightondemandlinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/hdinsightondemandlinkedservice?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-255">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-255">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-256">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-256">View the results.</span></span> <span data-ttu-id="af1ff-257">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-257">If the linked service has been successfully created, you see the JSON for the linked service in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a><span data-ttu-id="af1ff-258">Create datasets</span><span class="sxs-lookup"><span data-stu-id="af1ff-258">Create datasets</span></span>
<span data-ttu-id="af1ff-259">In this step, you create datasets to represent the input and output data for Hive processing.</span><span class="sxs-lookup"><span data-stu-id="af1ff-259">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="af1ff-260">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="af1ff-260">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="af1ff-261">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span><span class="sxs-lookup"><span data-stu-id="af1ff-261">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="af1ff-262">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="af1ff-262">Create input dataset</span></span>
<span data-ttu-id="af1ff-263">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="af1ff-263">In this step, you create the input dataset to represent input data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="af1ff-264">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-264">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-265">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-265">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-266">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-266">View the results.</span></span> <span data-ttu-id="af1ff-267">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-267">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="af1ff-268">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="af1ff-268">Create output dataset</span></span>
<span data-ttu-id="af1ff-269">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="af1ff-269">In this step, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="af1ff-270">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-270">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobOutput?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-271">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-271">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-272">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-272">View the results.</span></span> <span data-ttu-id="af1ff-273">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-273">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```

## <a name="create-pipeline"></a><span data-ttu-id="af1ff-274">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="af1ff-274">Create pipeline</span></span>
<span data-ttu-id="af1ff-275">In this step, you create your first pipeline with a **HDInsightHive** activity.</span><span class="sxs-lookup"><span data-stu-id="af1ff-275">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="af1ff-276">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span><span class="sxs-lookup"><span data-stu-id="af1ff-276">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="af1ff-277">The settings for the output dataset and the activity scheduler must match.</span><span class="sxs-lookup"><span data-stu-id="af1ff-277">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="af1ff-278">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="af1ff-278">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="af1ff-279">If the activity doesn't take any input, you can skip creating the input dataset.</span><span class="sxs-lookup"><span data-stu-id="af1ff-279">If the activity doesn't take any input, you can skip creating the input dataset.</span></span>

<span data-ttu-id="af1ff-280">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-280">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="af1ff-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span><span class="sxs-lookup"><span data-stu-id="af1ff-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

1. <span data-ttu-id="af1ff-282">Assign the command to variable named **cmd**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-282">Assign the command to variable named **cmd**.</span></span>

    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. <span data-ttu-id="af1ff-283">Run the command by using **Invoke-Command**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-283">Run the command by using **Invoke-Command**.</span></span>

    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. <span data-ttu-id="af1ff-284">View the results.</span><span class="sxs-lookup"><span data-stu-id="af1ff-284">View the results.</span></span> <span data-ttu-id="af1ff-285">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span><span class="sxs-lookup"><span data-stu-id="af1ff-285">If the dataset has been successfully created, you see the JSON for the dataset in the **results**; otherwise, you see an error message.</span></span>

    ```PowerShell
    Write-Host $results
    ```
4. <span data-ttu-id="af1ff-286">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span><span class="sxs-lookup"><span data-stu-id="af1ff-286">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="af1ff-287">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="af1ff-287">Monitor pipeline</span></span>
<span data-ttu-id="af1ff-288">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-288">In this step, you use Data Factory REST API to monitor slices being produced by the pipeline.</span></span>

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

<span data-ttu-id="af1ff-291">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span><span class="sxs-lookup"><span data-stu-id="af1ff-291">Run the Invoke-Command and the next one until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="af1ff-292">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span><span class="sxs-lookup"><span data-stu-id="af1ff-292">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="af1ff-293">The creation of an on-demand HDInsight cluster usually takes some time.</span><span class="sxs-lookup"><span data-stu-id="af1ff-293">The creation of an on-demand HDInsight cluster usually takes some time.</span></span>

![output data](./media/data-factory-build-your-first-pipeline-using-rest-api/three-ouptut-files.png)

> [!IMPORTANT]
> The input file gets deleted when the slice is processed successfully. Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.
>
>

<span data-ttu-id="af1ff-297">You can also use Azure portal to monitor slices and troubleshoot any issues.</span><span class="sxs-lookup"><span data-stu-id="af1ff-297">You can also use Azure portal to monitor slices and troubleshoot any issues.</span></span> <span data-ttu-id="af1ff-298">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-a-pipeline) details.</span><span class="sxs-lookup"><span data-stu-id="af1ff-298">See [Monitor pipelines using Azure portal](data-factory-build-your-first-pipeline-using-editor.md#monitor-a-pipeline) details.</span></span>

## <a name="summary"></a><span data-ttu-id="af1ff-299">Summary</span><span class="sxs-lookup"><span data-stu-id="af1ff-299">Summary</span></span>
<span data-ttu-id="af1ff-300">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-300">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="af1ff-301">You used the Data Factory Editor in the Azure portal to do the following steps:</span><span class="sxs-lookup"><span data-stu-id="af1ff-301">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="af1ff-302">Created an Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="af1ff-302">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="af1ff-303">Created two **linked services**:</span><span class="sxs-lookup"><span data-stu-id="af1ff-303">Created two **linked services**:</span></span>
   1. <span data-ttu-id="af1ff-304">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-304">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="af1ff-305">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-305">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="af1ff-306">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span><span class="sxs-lookup"><span data-stu-id="af1ff-306">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="af1ff-307">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="af1ff-307">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="af1ff-308">Created a **pipeline** with a **HDInsight Hive** activity.</span><span class="sxs-lookup"><span data-stu-id="af1ff-308">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af1ff-309">Next steps</span><span class="sxs-lookup"><span data-stu-id="af1ff-309">Next steps</span></span>
<span data-ttu-id="af1ff-310">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af1ff-310">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="af1ff-311">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="af1ff-311">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="af1ff-312">See Also</span><span class="sxs-lookup"><span data-stu-id="af1ff-312">See Also</span></span>
| <span data-ttu-id="af1ff-313">Topic</span><span class="sxs-lookup"><span data-stu-id="af1ff-313">Topic</span></span> | <span data-ttu-id="af1ff-314">Description</span><span class="sxs-lookup"><span data-stu-id="af1ff-314">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="af1ff-315">Data Factory REST API Reference</span><span class="sxs-lookup"><span data-stu-id="af1ff-315">Data Factory REST API Reference</span></span>](/rest/api/datafactory/) |<span data-ttu-id="af1ff-316">See comprehensive documentation on Data Factory cmdlets</span><span class="sxs-lookup"><span data-stu-id="af1ff-316">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="af1ff-317">Pipelines</span><span class="sxs-lookup"><span data-stu-id="af1ff-317">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="af1ff-318">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span><span class="sxs-lookup"><span data-stu-id="af1ff-318">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="af1ff-319">Datasets</span><span class="sxs-lookup"><span data-stu-id="af1ff-319">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="af1ff-320">This article helps you understand datasets in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="af1ff-320">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="af1ff-321">Scheduling and Execution</span><span class="sxs-lookup"><span data-stu-id="af1ff-321">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="af1ff-322">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span><span class="sxs-lookup"><span data-stu-id="af1ff-322">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="af1ff-323">Monitor and manage pipelines using Monitoring App</span><span class="sxs-lookup"><span data-stu-id="af1ff-323">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="af1ff-324">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span><span class="sxs-lookup"><span data-stu-id="af1ff-324">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
