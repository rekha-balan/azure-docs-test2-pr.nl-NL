---
title: Use custom activities in an Azure Data Factory pipeline
description: Learn how to create custom activities and use them in an Azure Data Factory pipeline.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/29/2018
ms.author: douglasl
ms.openlocfilehash: f4a88c5495fc3297699110d8a12a22ff7d6c2bbb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871498"
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="6d006-103">Use custom activities in an Azure Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="6d006-103">Use custom activities in an Azure Data Factory pipeline</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-use-custom-activities.md)
> * [Current version](transform-data-using-dotnet-custom-activity.md)

<span data-ttu-id="6d006-106">There are two types of activities that you can use in an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="6d006-106">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="6d006-107">[Data movement activities](copy-activity-overview.md) to move data between [supported source and sink data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="6d006-107">[Data movement activities](copy-activity-overview.md) to move data between [supported source and sink data stores](copy-activity-overview.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="6d006-108">[Data transformation activities](transform-data.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="6d006-108">[Data transformation activities](transform-data.md) to transform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="6d006-109">To move data to/from a data store that Data Factory does not support, or to transform/process data in a way that isn't supported by Data Factory, you can create a **Custom activity** with your own data movement or transformation logic and use the activity in a pipeline.</span><span class="sxs-lookup"><span data-stu-id="6d006-109">To move data to/from a data store that Data Factory does not support, or to transform/process data in a way that isn't supported by Data Factory, you can create a **Custom activity** with your own data movement or transformation logic and use the activity in a pipeline.</span></span> <span data-ttu-id="6d006-110">The custom activity runs your customized code logic on an **Azure Batch** pool of virtual machines.</span><span class="sxs-lookup"><span data-stu-id="6d006-110">The custom activity runs your customized code logic on an **Azure Batch** pool of virtual machines.</span></span>

<span data-ttu-id="6d006-111">See following articles if you are new to Azure Batch service:</span><span class="sxs-lookup"><span data-stu-id="6d006-111">See following articles if you are new to Azure Batch service:</span></span>

* <span data-ttu-id="6d006-112">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of the Azure Batch service.</span><span class="sxs-lookup"><span data-stu-id="6d006-112">[Azure Batch basics](../batch/batch-technical-overview.md) for an overview of the Azure Batch service.</span></span>
* <span data-ttu-id="6d006-113">[New-AzureRmBatchAccount](/powershell/module/azurerm.batch/New-AzureRmBatchAccount?view=azurermps-4.3.1) cmdlet to create an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) to create the Azure Batch account using Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6d006-113">[New-AzureRmBatchAccount](/powershell/module/azurerm.batch/New-AzureRmBatchAccount?view=azurermps-4.3.1) cmdlet to create an Azure Batch account (or) [Azure portal](../batch/batch-account-create-portal.md) to create the Azure Batch account using Azure portal.</span></span> <span data-ttu-id="6d006-114">See [Using PowerShell to manage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) article for detailed instructions on using the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6d006-114">See [Using PowerShell to manage Azure Batch Account](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) article for detailed instructions on using the cmdlet.</span></span>
* <span data-ttu-id="6d006-115">[New-AzureBatchPool](/powershell/module/azurerm.batch/New-AzureBatchPool?view=azurermps-4.3.1) cmdlet to create an Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="6d006-115">[New-AzureBatchPool](/powershell/module/azurerm.batch/New-AzureBatchPool?view=azurermps-4.3.1) cmdlet to create an Azure Batch pool.</span></span>

## <a name="azure-batch-linked-service"></a><span data-ttu-id="6d006-116">Azure Batch linked service</span><span class="sxs-lookup"><span data-stu-id="6d006-116">Azure Batch linked service</span></span> 
<span data-ttu-id="6d006-117">The following JSON defines a sample Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="6d006-117">The following JSON defines a sample Azure Batch linked service.</span></span> <span data-ttu-id="6d006-118">For details, see [Compute environments supported by Azure Data Factory](compute-linked-services.md)</span><span class="sxs-lookup"><span data-stu-id="6d006-118">For details, see [Compute environments supported by Azure Data Factory](compute-linked-services.md)</span></span>

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "batchaccount",
            "accessKey": {
                "type": "SecureString",
                "value": "access key"
            },
            "batchUri": "https://batchaccount.region.batch.azure.com",
            "poolName": "poolname",
            "linkedServiceName": {
                "referenceName": "StorageLinkedService",
                "type": "LinkedServiceReference"
            }
        }
    }
}
```

 <span data-ttu-id="6d006-119">To learn more about Azure Batch linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d006-119">To learn more about Azure Batch linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> 

## <a name="custom-activity"></a><span data-ttu-id="6d006-120">Custom activity</span><span class="sxs-lookup"><span data-stu-id="6d006-120">Custom activity</span></span>

<span data-ttu-id="6d006-121">The following JSON snippet defines a pipeline with a simple Custom Activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-121">The following JSON snippet defines a pipeline with a simple Custom Activity.</span></span> <span data-ttu-id="6d006-122">The activity definition has a reference to the Azure Batch linked service.</span><span class="sxs-lookup"><span data-stu-id="6d006-122">The activity definition has a reference to the Azure Batch linked service.</span></span> 

```json
{
    "name": "MyCustomActivityPipeline",
    "properties": {
      "description": "Custom activity sample",
      "activities": [{
        "type": "Custom",
        "name": "MyCustomActivity",
        "linkedServiceName": {
          "referenceName": "AzureBatchLinkedService",
          "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "command": "helloworld.exe",
          "folderPath": "customactv2/helloworld",
          "resourceLinkedService": {
            "referenceName": "StorageLinkedService",
            "type": "LinkedServiceReference"
          }
        }
      }]
    }
  }
```

<span data-ttu-id="6d006-123">In this sample, the helloworld.exe is a custom application stored in the customactv2/helloworld folder of the Azure Storage account used in the resourceLinkedService.</span><span class="sxs-lookup"><span data-stu-id="6d006-123">In this sample, the helloworld.exe is a custom application stored in the customactv2/helloworld folder of the Azure Storage account used in the resourceLinkedService.</span></span> <span data-ttu-id="6d006-124">The Custom activity submits this custom application to be executed on Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="6d006-124">The Custom activity submits this custom application to be executed on Azure Batch.</span></span> <span data-ttu-id="6d006-125">You can replace the command to any preferred application that can be executed on the target Operation System of the Azure Batch Pool nodes.</span><span class="sxs-lookup"><span data-stu-id="6d006-125">You can replace the command to any preferred application that can be executed on the target Operation System of the Azure Batch Pool nodes.</span></span> 

<span data-ttu-id="6d006-126">The following table describes names and descriptions of properties that are specific to this activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-126">The following table describes names and descriptions of properties that are specific to this activity.</span></span> 

| <span data-ttu-id="6d006-127">Property</span><span class="sxs-lookup"><span data-stu-id="6d006-127">Property</span></span>              | <span data-ttu-id="6d006-128">Description</span><span class="sxs-lookup"><span data-stu-id="6d006-128">Description</span></span>                              | <span data-ttu-id="6d006-129">Required</span><span class="sxs-lookup"><span data-stu-id="6d006-129">Required</span></span> |
| :-------------------- | :--------------------------------------- | :------- |
| <span data-ttu-id="6d006-130">name</span><span class="sxs-lookup"><span data-stu-id="6d006-130">name</span></span>                  | <span data-ttu-id="6d006-131">Name of the activity in the pipeline</span><span class="sxs-lookup"><span data-stu-id="6d006-131">Name of the activity in the pipeline</span></span>     | <span data-ttu-id="6d006-132">Yes</span><span class="sxs-lookup"><span data-stu-id="6d006-132">Yes</span></span>      |
| <span data-ttu-id="6d006-133">description</span><span class="sxs-lookup"><span data-stu-id="6d006-133">description</span></span>           | <span data-ttu-id="6d006-134">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="6d006-134">Text describing what the activity does.</span></span>  | <span data-ttu-id="6d006-135">No</span><span class="sxs-lookup"><span data-stu-id="6d006-135">No</span></span>       |
| <span data-ttu-id="6d006-136">type</span><span class="sxs-lookup"><span data-stu-id="6d006-136">type</span></span>                  | <span data-ttu-id="6d006-137">For Custom activity, the activity type is **Custom**.</span><span class="sxs-lookup"><span data-stu-id="6d006-137">For Custom activity, the activity type is **Custom**.</span></span> | <span data-ttu-id="6d006-138">Yes</span><span class="sxs-lookup"><span data-stu-id="6d006-138">Yes</span></span>      |
| <span data-ttu-id="6d006-139">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="6d006-139">linkedServiceName</span></span>     | <span data-ttu-id="6d006-140">Linked Service to Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="6d006-140">Linked Service to Azure Batch.</span></span> <span data-ttu-id="6d006-141">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="6d006-141">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span>  | <span data-ttu-id="6d006-142">Yes</span><span class="sxs-lookup"><span data-stu-id="6d006-142">Yes</span></span>      |
| <span data-ttu-id="6d006-143">command</span><span class="sxs-lookup"><span data-stu-id="6d006-143">command</span></span>               | <span data-ttu-id="6d006-144">Command of the custom application to be executed.</span><span class="sxs-lookup"><span data-stu-id="6d006-144">Command of the custom application to be executed.</span></span> <span data-ttu-id="6d006-145">If the application is already available on the Azure Batch Pool Node, the resourceLinkedService and folderPath can be skipped.</span><span class="sxs-lookup"><span data-stu-id="6d006-145">If the application is already available on the Azure Batch Pool Node, the resourceLinkedService and folderPath can be skipped.</span></span> <span data-ttu-id="6d006-146">For example, you can specify the command to be `cmd /c dir`, which is natively supported by the Windows Batch Pool node.</span><span class="sxs-lookup"><span data-stu-id="6d006-146">For example, you can specify the command to be `cmd /c dir`, which is natively supported by the Windows Batch Pool node.</span></span> | <span data-ttu-id="6d006-147">Yes</span><span class="sxs-lookup"><span data-stu-id="6d006-147">Yes</span></span>      |
| <span data-ttu-id="6d006-148">resourceLinkedService</span><span class="sxs-lookup"><span data-stu-id="6d006-148">resourceLinkedService</span></span> | <span data-ttu-id="6d006-149">Azure Storage Linked Service to the Storage account where the custom application is stored</span><span class="sxs-lookup"><span data-stu-id="6d006-149">Azure Storage Linked Service to the Storage account where the custom application is stored</span></span> | <span data-ttu-id="6d006-150">No</span><span class="sxs-lookup"><span data-stu-id="6d006-150">No</span></span>       |
| <span data-ttu-id="6d006-151">folderPath</span><span class="sxs-lookup"><span data-stu-id="6d006-151">folderPath</span></span>            | <span data-ttu-id="6d006-152">Path to the folder of the custom application and all its dependencies</span><span class="sxs-lookup"><span data-stu-id="6d006-152">Path to the folder of the custom application and all its dependencies</span></span> | <span data-ttu-id="6d006-153">No</span><span class="sxs-lookup"><span data-stu-id="6d006-153">No</span></span>       |
| <span data-ttu-id="6d006-154">referenceObjects</span><span class="sxs-lookup"><span data-stu-id="6d006-154">referenceObjects</span></span>      | <span data-ttu-id="6d006-155">An array of existing Linked Services and Datasets.</span><span class="sxs-lookup"><span data-stu-id="6d006-155">An array of existing Linked Services and Datasets.</span></span> <span data-ttu-id="6d006-156">The referenced Linked Services and Datasets are passed to the custom application in JSON format so your custom code can reference resources of the Data Factory</span><span class="sxs-lookup"><span data-stu-id="6d006-156">The referenced Linked Services and Datasets are passed to the custom application in JSON format so your custom code can reference resources of the Data Factory</span></span> | <span data-ttu-id="6d006-157">No</span><span class="sxs-lookup"><span data-stu-id="6d006-157">No</span></span>       |
| <span data-ttu-id="6d006-158">extendedProperties</span><span class="sxs-lookup"><span data-stu-id="6d006-158">extendedProperties</span></span>    | <span data-ttu-id="6d006-159">User-defined properties that can be passed to the custom application in JSON format so your custom code can reference additional properties</span><span class="sxs-lookup"><span data-stu-id="6d006-159">User-defined properties that can be passed to the custom application in JSON format so your custom code can reference additional properties</span></span> | <span data-ttu-id="6d006-160">No</span><span class="sxs-lookup"><span data-stu-id="6d006-160">No</span></span>       |

## <a name="custom-activity-permissions"></a><span data-ttu-id="6d006-161">Custom activity permissions</span><span class="sxs-lookup"><span data-stu-id="6d006-161">Custom activity permissions</span></span>

<span data-ttu-id="6d006-162">The custom activity sets the Azure Batch auto-user account to *Non-admin access with task scope* (the default auto-user specification).</span><span class="sxs-lookup"><span data-stu-id="6d006-162">The custom activity sets the Azure Batch auto-user account to *Non-admin access with task scope* (the default auto-user specification).</span></span> <span data-ttu-id="6d006-163">You can't change the permission level of the auto-user account.</span><span class="sxs-lookup"><span data-stu-id="6d006-163">You can't change the permission level of the auto-user account.</span></span> <span data-ttu-id="6d006-164">For more info, see [Run tasks under user accounts in Batch | Auto-user accounts](../batch/batch-user-accounts.md#auto-user-accounts).</span><span class="sxs-lookup"><span data-stu-id="6d006-164">For more info, see [Run tasks under user accounts in Batch | Auto-user accounts](../batch/batch-user-accounts.md#auto-user-accounts).</span></span>

## <a name="executing-commands"></a><span data-ttu-id="6d006-165">Executing commands</span><span class="sxs-lookup"><span data-stu-id="6d006-165">Executing commands</span></span>

<span data-ttu-id="6d006-166">You can directly execute a command using Custom Activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-166">You can directly execute a command using Custom Activity.</span></span> <span data-ttu-id="6d006-167">The following example runs the "echo hello world" command on the target Azure Batch Pool nodes and prints the output to stdout.</span><span class="sxs-lookup"><span data-stu-id="6d006-167">The following example runs the "echo hello world" command on the target Azure Batch Pool nodes and prints the output to stdout.</span></span> 

  ```json
  {
    "name": "MyCustomActivity",
    "properties": {
      "description": "Custom activity sample",
      "activities": [{
        "type": "Custom",
        "name": "MyCustomActivity",
        "linkedServiceName": {
          "referenceName": "AzureBatchLinkedService",
          "type": "LinkedServiceReference"
        },
        "typeProperties": {
          "command": "cmd /c echo hello world"
        }
      }]
    }
  } 
  ```

## <a name="passing-objects-and-properties"></a><span data-ttu-id="6d006-168">Passing objects and properties</span><span class="sxs-lookup"><span data-stu-id="6d006-168">Passing objects and properties</span></span>

<span data-ttu-id="6d006-169">This sample shows how you can use the referenceObjects and extendedProperties to pass Data Factory objects and user-defined properties to your custom application.</span><span class="sxs-lookup"><span data-stu-id="6d006-169">This sample shows how you can use the referenceObjects and extendedProperties to pass Data Factory objects and user-defined properties to your custom application.</span></span> 


```json
{
  "name": "MyCustomActivityPipeline",
  "properties": {
    "description": "Custom activity sample",
    "activities": [{
      "type": "Custom",
      "name": "MyCustomActivity",
      "linkedServiceName": {
        "referenceName": "AzureBatchLinkedService",
        "type": "LinkedServiceReference"
      },
      "typeProperties": {
        "command": "SampleApp.exe",
        "folderPath": "customactv2/SampleApp",
        "resourceLinkedService": {
          "referenceName": "StorageLinkedService",
          "type": "LinkedServiceReference"
        },
        "referenceObjects": {
          "linkedServices": [{
            "referenceName": "AzureBatchLinkedService",
            "type": "LinkedServiceReference"
          }]
        },
        "extendedProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "aSampleSecureString"
            },
            "PropertyBagPropertyName1": "PropertyBagValue1",
            "propertyBagPropertyName2": "PropertyBagValue2",
            "dateTime1": "2015-04-12T12:13:14Z"              
        }
      }
    }]
  }
}
```

<span data-ttu-id="6d006-170">When the activity is executed, referenceObjects and extendedProperties are stored in following files that are deployed to the same execution folder of the SampleApp.exe:</span><span class="sxs-lookup"><span data-stu-id="6d006-170">When the activity is executed, referenceObjects and extendedProperties are stored in following files that are deployed to the same execution folder of the SampleApp.exe:</span></span> 

- <span data-ttu-id="6d006-171">activity.json</span><span class="sxs-lookup"><span data-stu-id="6d006-171">activity.json</span></span>

  <span data-ttu-id="6d006-172">Stores extendedProperties and properties of the custom activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-172">Stores extendedProperties and properties of the custom activity.</span></span> 

- <span data-ttu-id="6d006-173">linkedServices.json</span><span class="sxs-lookup"><span data-stu-id="6d006-173">linkedServices.json</span></span>

  <span data-ttu-id="6d006-174">Stores an array of Linked Services defined in the referenceObjects property.</span><span class="sxs-lookup"><span data-stu-id="6d006-174">Stores an array of Linked Services defined in the referenceObjects property.</span></span> 

- <span data-ttu-id="6d006-175">datasets.json</span><span class="sxs-lookup"><span data-stu-id="6d006-175">datasets.json</span></span>

  <span data-ttu-id="6d006-176">Stores an array of Datasets defined in the referenceObjects property.</span><span class="sxs-lookup"><span data-stu-id="6d006-176">Stores an array of Datasets defined in the referenceObjects property.</span></span> 

<span data-ttu-id="6d006-177">Following sample code demonstrate how the SampleApp.exe can access the required information from JSON files:</span><span class="sxs-lookup"><span data-stu-id="6d006-177">Following sample code demonstrate how the SampleApp.exe can access the required information from JSON files:</span></span> 

```csharp
using Newtonsoft.Json;
using System;
using System.IO;

namespace SampleApp
{
    class Program
    {
        static void Main(string[] args)
        {
            //From Extend Properties
            dynamic activity = JsonConvert.DeserializeObject(File.ReadAllText("activity.json"));
            Console.WriteLine(activity.typeProperties.extendedProperties.connectionString.value);

            // From LinkedServices
            dynamic linkedServices = JsonConvert.DeserializeObject(File.ReadAllText("linkedServices.json"));
            Console.WriteLine(linkedServices[0].properties.typeProperties.accountName);
        }
    }
}
```

## <a name="retrieve-execution-outputs"></a><span data-ttu-id="6d006-178">Retrieve execution outputs</span><span class="sxs-lookup"><span data-stu-id="6d006-178">Retrieve execution outputs</span></span>

  <span data-ttu-id="6d006-179">You can start a pipeline run using the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="6d006-179">You can start a pipeline run using the following PowerShell command:</span></span> 

  ```.powershell
  $runId = Invoke-AzureRmDataFactoryV2Pipeline -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineName $pipelineName
  ```
  <span data-ttu-id="6d006-180">When the pipeline is running, you can check the execution output using the following commands:</span><span class="sxs-lookup"><span data-stu-id="6d006-180">When the pipeline is running, you can check the execution output using the following commands:</span></span> 

  ```.powershell
  while ($True) {
      $result = Get-AzureRmDataFactoryV2ActivityRun -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName -PipelineRunId $runId -RunStartedAfter (Get-Date).AddMinutes(-30) -RunStartedBefore (Get-Date).AddMinutes(30)

      if(!$result) {
          Write-Host "Waiting for pipeline to start..." -foregroundcolor "Yellow"
      }
      elseif (($result | Where-Object { $_.Status -eq "InProgress" } | Measure-Object).count -ne 0) {
          Write-Host "Pipeline run status: In Progress" -foregroundcolor "Yellow"
      }
      else {
          Write-Host "Pipeline '"$pipelineName"' run finished. Result:" -foregroundcolor "Yellow"
          $result
          break
      }
      ($result | Format-List | Out-String)
      Start-Sleep -Seconds 15
  }

  Write-Host "Activity `Output` section:" -foregroundcolor "Yellow"
  $result.Output -join "`r`n"

  Write-Host "Activity `Error` section:" -foregroundcolor "Yellow"
  $result.Error -join "`r`n"
  ```

  <span data-ttu-id="6d006-181">The **stdout** and **stderr** of your custom application are saved to the **adfjobs** container in the Azure Storage Linked Service you defined when creating Azure Batch Linked Service with a GUID of the task.</span><span class="sxs-lookup"><span data-stu-id="6d006-181">The **stdout** and **stderr** of your custom application are saved to the **adfjobs** container in the Azure Storage Linked Service you defined when creating Azure Batch Linked Service with a GUID of the task.</span></span> <span data-ttu-id="6d006-182">You can get the detailed path from Activity Run output as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="6d006-182">You can get the detailed path from Activity Run output as shown in the following snippet:</span></span> 

  ```shell
  Pipeline ' MyCustomActivity' run finished. Result:

  ResourceGroupName : resourcegroupname
  DataFactoryName   : datafactoryname
  ActivityName      : MyCustomActivity
  PipelineRunId     : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
  PipelineName      : MyCustomActivity
  Input             : {command}
  Output            : {exitcode, outputs, effectiveIntegrationRuntime}
  LinkedServiceName : 
  ActivityRunStart  : 10/5/2017 3:33:06 PM
  ActivityRunEnd    : 10/5/2017 3:33:28 PM
  DurationInMs      : 21203
  Status            : Succeeded
  Error             : {errorCode, message, failureType, target}

  Activity Output section:
  "exitcode": 0
  "outputs": [
    "https://shengcstorbatch.blob.core.windows.net/adfjobs/<GUID>/output/stdout.txt",
    "https://shengcstorbatch.blob.core.windows.net/adfjobs/<GUID>/output/stderr.txt"
  ]
  "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)"
  Activity Error section:
  "errorCode": ""
  "message": ""
  "failureType": ""
  "target": "MyCustomActivity"
  ```
<span data-ttu-id="6d006-183">If you would like to consume the content of stdout.txt in downstream activities, you can get the path to the stdout.txt file in expression "\@activity('MyCustomActivity').output.outputs[0]".</span><span class="sxs-lookup"><span data-stu-id="6d006-183">If you would like to consume the content of stdout.txt in downstream activities, you can get the path to the stdout.txt file in expression "\@activity('MyCustomActivity').output.outputs[0]".</span></span> 

  > [!IMPORTANT]
  > - The activity.json, linkedServices.json, and datasets.json are stored in the runtime folder of the Batch task. For this example, the activity.json, linkedServices.json, and datasets.json are stored in "https://adfv2storage.blob.core.windows.net/adfjobs/<GUID>/runtime/" path. If needed, you need to clean them up separately. 
  > - For Linked Services uses Self-Hosted Integration Runtime, the sensitive information like keys or passwords are encrypted by the Self-Hosted Integration Runtime to ensure credential stays in customer defined private network environment. Some sensitive fields could be missing when referenced by your custom application code in this way. Use SecureString in extendedProperties instead of using Linked Service reference if needed. 

## <a name="compare-v2-v1"></a> <span data-ttu-id="6d006-190">Compare v2 Custom Activity and version 1 (Custom) DotNet Activity</span><span class="sxs-lookup"><span data-stu-id="6d006-190">Compare v2 Custom Activity and version 1 (Custom) DotNet Activity</span></span>

  <span data-ttu-id="6d006-191">In Azure Data Factory version 1, you implement a (Custom) DotNet Activity by creating a .Net Class Library project with a class that implements the `Execute` method of the `IDotNetActivity` interface.</span><span class="sxs-lookup"><span data-stu-id="6d006-191">In Azure Data Factory version 1, you implement a (Custom) DotNet Activity by creating a .Net Class Library project with a class that implements the `Execute` method of the `IDotNetActivity` interface.</span></span> <span data-ttu-id="6d006-192">The Linked Services, Datasets, and Extended Properties in the JSON payload of a (Custom) DotNet Activity are passed to the execution method as strongly-typed objects.</span><span class="sxs-lookup"><span data-stu-id="6d006-192">The Linked Services, Datasets, and Extended Properties in the JSON payload of a (Custom) DotNet Activity are passed to the execution method as strongly-typed objects.</span></span> <span data-ttu-id="6d006-193">For details about the version 1 behavior, see [(Custom) DotNet in version 1](v1/data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="6d006-193">For details about the version 1 behavior, see [(Custom) DotNet in version 1](v1/data-factory-use-custom-activities.md).</span></span> <span data-ttu-id="6d006-194">Because of this implementation, your version 1 DotNet Activity code has to target .Net Framework 4.5.2.</span><span class="sxs-lookup"><span data-stu-id="6d006-194">Because of this implementation, your version 1 DotNet Activity code has to target .Net Framework 4.5.2.</span></span> <span data-ttu-id="6d006-195">The version 1 DotNet Activity also has to be executed on Windows-based Azure Batch Pool nodes.</span><span class="sxs-lookup"><span data-stu-id="6d006-195">The version 1 DotNet Activity also has to be executed on Windows-based Azure Batch Pool nodes.</span></span> 

  <span data-ttu-id="6d006-196">In the Azure Data Factory V2 Custom Activity, you are not required to implement a .Net interface.</span><span class="sxs-lookup"><span data-stu-id="6d006-196">In the Azure Data Factory V2 Custom Activity, you are not required to implement a .Net interface.</span></span> <span data-ttu-id="6d006-197">You can now directly run commands, scripts, and your own custom code, compiled as an executable.</span><span class="sxs-lookup"><span data-stu-id="6d006-197">You can now directly run commands, scripts, and your own custom code, compiled as an executable.</span></span> <span data-ttu-id="6d006-198">To configure this implementation, you specify the `Command` property together with the `folderPath` property.</span><span class="sxs-lookup"><span data-stu-id="6d006-198">To configure this implementation, you specify the `Command` property together with the `folderPath` property.</span></span> <span data-ttu-id="6d006-199">The Custom Activity uploads the executable and its dependencies to `folderpath` and executes the command for you.</span><span class="sxs-lookup"><span data-stu-id="6d006-199">The Custom Activity uploads the executable and its dependencies to `folderpath` and executes the command for you.</span></span> 

  <span data-ttu-id="6d006-200">The Linked Services, Datasets (defined in referenceObjects), and Extended Properties defined in the JSON payload of a Data Factory v2 Custom Activity can be accessed by your executable as JSON files.</span><span class="sxs-lookup"><span data-stu-id="6d006-200">The Linked Services, Datasets (defined in referenceObjects), and Extended Properties defined in the JSON payload of a Data Factory v2 Custom Activity can be accessed by your executable as JSON files.</span></span> <span data-ttu-id="6d006-201">You can access the required properties using a JSON serializer as shown in the preceding SampleApp.exe code sample.</span><span class="sxs-lookup"><span data-stu-id="6d006-201">You can access the required properties using a JSON serializer as shown in the preceding SampleApp.exe code sample.</span></span> 

  <span data-ttu-id="6d006-202">With the changes introduced in the Data Factory V2 Custom Activity, you can write your custom code logic in your preferred language and execute it on Windows and Linux Operation Systems supported by Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="6d006-202">With the changes introduced in the Data Factory V2 Custom Activity, you can write your custom code logic in your preferred language and execute it on Windows and Linux Operation Systems supported by Azure Batch.</span></span> 

  <span data-ttu-id="6d006-203">The following table describes the differences between the Data Factory V2 Custom Activity and the Data Factory version 1 (Custom) DotNet Activity:</span><span class="sxs-lookup"><span data-stu-id="6d006-203">The following table describes the differences between the Data Factory V2 Custom Activity and the Data Factory version 1 (Custom) DotNet Activity:</span></span> 


|<span data-ttu-id="6d006-204">Differences</span><span class="sxs-lookup"><span data-stu-id="6d006-204">Differences</span></span>      | <span data-ttu-id="6d006-205">Custom Activity</span><span class="sxs-lookup"><span data-stu-id="6d006-205">Custom Activity</span></span>      | <span data-ttu-id="6d006-206">version 1 (Custom) DotNet Activity</span><span class="sxs-lookup"><span data-stu-id="6d006-206">version 1 (Custom) DotNet Activity</span></span>      |
| ---- | ---- | ---- |
|<span data-ttu-id="6d006-207">How custom logic is defined</span><span class="sxs-lookup"><span data-stu-id="6d006-207">How custom logic is defined</span></span>      |<span data-ttu-id="6d006-208">By providing an executable</span><span class="sxs-lookup"><span data-stu-id="6d006-208">By providing an executable</span></span>      |<span data-ttu-id="6d006-209">By implementing a .Net DLL</span><span class="sxs-lookup"><span data-stu-id="6d006-209">By implementing a .Net DLL</span></span>      |
|<span data-ttu-id="6d006-210">Execution environment of the custom logic</span><span class="sxs-lookup"><span data-stu-id="6d006-210">Execution environment of the custom logic</span></span>      |<span data-ttu-id="6d006-211">Windows or Linux</span><span class="sxs-lookup"><span data-stu-id="6d006-211">Windows or Linux</span></span>      |<span data-ttu-id="6d006-212">Windows (.Net Framework 4.5.2)</span><span class="sxs-lookup"><span data-stu-id="6d006-212">Windows (.Net Framework 4.5.2)</span></span>      |
|<span data-ttu-id="6d006-213">Executing scripts</span><span class="sxs-lookup"><span data-stu-id="6d006-213">Executing scripts</span></span>      |<span data-ttu-id="6d006-214">Supports executing scripts directly (for example "cmd /c echo hello world" on Windows VM)</span><span class="sxs-lookup"><span data-stu-id="6d006-214">Supports executing scripts directly (for example "cmd /c echo hello world" on Windows VM)</span></span>      |<span data-ttu-id="6d006-215">Requires implementation in the .Net DLL</span><span class="sxs-lookup"><span data-stu-id="6d006-215">Requires implementation in the .Net DLL</span></span>      |
|<span data-ttu-id="6d006-216">Dataset required</span><span class="sxs-lookup"><span data-stu-id="6d006-216">Dataset required</span></span>      |<span data-ttu-id="6d006-217">Optional</span><span class="sxs-lookup"><span data-stu-id="6d006-217">Optional</span></span>      |<span data-ttu-id="6d006-218">Required to chain activities and pass information</span><span class="sxs-lookup"><span data-stu-id="6d006-218">Required to chain activities and pass information</span></span>      |
|<span data-ttu-id="6d006-219">Pass information from activity to custom logic</span><span class="sxs-lookup"><span data-stu-id="6d006-219">Pass information from activity to custom logic</span></span>      |<span data-ttu-id="6d006-220">Through ReferenceObjects (LinkedServices and Datasets) and ExtendedProperties (custom properties)</span><span class="sxs-lookup"><span data-stu-id="6d006-220">Through ReferenceObjects (LinkedServices and Datasets) and ExtendedProperties (custom properties)</span></span>      |<span data-ttu-id="6d006-221">Through ExtendedProperties (custom properties), Input, and Output Datasets</span><span class="sxs-lookup"><span data-stu-id="6d006-221">Through ExtendedProperties (custom properties), Input, and Output Datasets</span></span>      |
|<span data-ttu-id="6d006-222">Retrieve information in custom logic</span><span class="sxs-lookup"><span data-stu-id="6d006-222">Retrieve information in custom logic</span></span>      |<span data-ttu-id="6d006-223">Parses activity.json, linkedServices.json, and datasets.json stored in the same folder of the executable</span><span class="sxs-lookup"><span data-stu-id="6d006-223">Parses activity.json, linkedServices.json, and datasets.json stored in the same folder of the executable</span></span>      |<span data-ttu-id="6d006-224">Through .Net SDK (.Net Frame 4.5.2)</span><span class="sxs-lookup"><span data-stu-id="6d006-224">Through .Net SDK (.Net Frame 4.5.2)</span></span>      |
|<span data-ttu-id="6d006-225">Logging</span><span class="sxs-lookup"><span data-stu-id="6d006-225">Logging</span></span>      |<span data-ttu-id="6d006-226">Writes directly to STDOUT</span><span class="sxs-lookup"><span data-stu-id="6d006-226">Writes directly to STDOUT</span></span>      |<span data-ttu-id="6d006-227">Implementing Logger in .Net DLL</span><span class="sxs-lookup"><span data-stu-id="6d006-227">Implementing Logger in .Net DLL</span></span>      |


  <span data-ttu-id="6d006-228">If you have existing .Net code written for a version 1 (Custom) DotNet Activity, you need to modify your code for it to work with the current version of the Custom Activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-228">If you have existing .Net code written for a version 1 (Custom) DotNet Activity, you need to modify your code for it to work with the current version of the Custom Activity.</span></span> <span data-ttu-id="6d006-229">Update your code by following these high-level guidelines:</span><span class="sxs-lookup"><span data-stu-id="6d006-229">Update your code by following these high-level guidelines:</span></span>  

   - <span data-ttu-id="6d006-230">Change the project from a .Net Class Library to a Console App.</span><span class="sxs-lookup"><span data-stu-id="6d006-230">Change the project from a .Net Class Library to a Console App.</span></span> 
   - <span data-ttu-id="6d006-231">Start your application with the `Main` method.</span><span class="sxs-lookup"><span data-stu-id="6d006-231">Start your application with the `Main` method.</span></span> <span data-ttu-id="6d006-232">The `Execute` method of the `IDotNetActivity` interface is no longer required.</span><span class="sxs-lookup"><span data-stu-id="6d006-232">The `Execute` method of the `IDotNetActivity` interface is no longer required.</span></span> 
   - <span data-ttu-id="6d006-233">Read and parse the Linked Services, Datasets and Activity with a JSON serializer, and not as strongly-typed objects.</span><span class="sxs-lookup"><span data-stu-id="6d006-233">Read and parse the Linked Services, Datasets and Activity with a JSON serializer, and not as strongly-typed objects.</span></span> <span data-ttu-id="6d006-234">Pass the values of required properties to your main custom code logic.</span><span class="sxs-lookup"><span data-stu-id="6d006-234">Pass the values of required properties to your main custom code logic.</span></span> <span data-ttu-id="6d006-235">Refer to the preceding SampleApp.exe code as an example.</span><span class="sxs-lookup"><span data-stu-id="6d006-235">Refer to the preceding SampleApp.exe code as an example.</span></span> 
   - <span data-ttu-id="6d006-236">The Logger object is no longer supported.</span><span class="sxs-lookup"><span data-stu-id="6d006-236">The Logger object is no longer supported.</span></span> <span data-ttu-id="6d006-237">Output from your executable can be printed to the console and is saved to stdout.txt.</span><span class="sxs-lookup"><span data-stu-id="6d006-237">Output from your executable can be printed to the console and is saved to stdout.txt.</span></span> 
   - <span data-ttu-id="6d006-238">The Microsoft.Azure.Management.DataFactories NuGet package is no longer required.</span><span class="sxs-lookup"><span data-stu-id="6d006-238">The Microsoft.Azure.Management.DataFactories NuGet package is no longer required.</span></span> 
   - <span data-ttu-id="6d006-239">Compile your code, upload the executable and its dependencies to Azure Storage, and define the path in the `folderPath` property.</span><span class="sxs-lookup"><span data-stu-id="6d006-239">Compile your code, upload the executable and its dependencies to Azure Storage, and define the path in the `folderPath` property.</span></span> 

<span data-ttu-id="6d006-240">For a complete sample of how the end-to-end DLL and pipeline sample described in the Data Factory version 1 article [Use custom activities in an Azure Data Factory pipeline](https://docs.microsoft.com/azure/data-factory/v1/data-factory-use-custom-activities) can be rewritten as a Data Factory Custom Activity, see [Data Factory Custom Activity sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFv2CustomActivitySample).</span><span class="sxs-lookup"><span data-stu-id="6d006-240">For a complete sample of how the end-to-end DLL and pipeline sample described in the Data Factory version 1 article [Use custom activities in an Azure Data Factory pipeline](https://docs.microsoft.com/azure/data-factory/v1/data-factory-use-custom-activities) can be rewritten as a Data Factory Custom Activity, see [Data Factory Custom Activity sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFv2CustomActivitySample).</span></span> 

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="6d006-241">Auto-scaling of Azure Batch</span><span class="sxs-lookup"><span data-stu-id="6d006-241">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="6d006-242">You can also create an Azure Batch pool with **autoscale** feature.</span><span class="sxs-lookup"><span data-stu-id="6d006-242">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="6d006-243">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span><span class="sxs-lookup"><span data-stu-id="6d006-243">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on the number of pending tasks.</span></span> 

<span data-ttu-id="6d006-244">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span><span class="sxs-lookup"><span data-stu-id="6d006-244">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="6d006-245">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span><span class="sxs-lookup"><span data-stu-id="6d006-245">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="6d006-246">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span><span class="sxs-lookup"><span data-stu-id="6d006-246">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="6d006-247">It ensures that TargetDedicated never goes beyond 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="6d006-247">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="6d006-248">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span><span class="sxs-lookup"><span data-stu-id="6d006-248">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="6d006-249">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span><span class="sxs-lookup"><span data-stu-id="6d006-249">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>

<span data-ttu-id="6d006-250">Autoscale formula:</span><span class="sxs-lookup"><span data-stu-id="6d006-250">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="6d006-251">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span><span class="sxs-lookup"><span data-stu-id="6d006-251">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="6d006-252">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span><span class="sxs-lookup"><span data-stu-id="6d006-252">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="6d006-253">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="6d006-253">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d006-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="6d006-254">Next steps</span></span>
<span data-ttu-id="6d006-255">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="6d006-255">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="6d006-256">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="6d006-256">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="6d006-257">Hive activity</span><span class="sxs-lookup"><span data-stu-id="6d006-257">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="6d006-258">Pig activity</span><span class="sxs-lookup"><span data-stu-id="6d006-258">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="6d006-259">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="6d006-259">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="6d006-260">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="6d006-260">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="6d006-261">Spark activity</span><span class="sxs-lookup"><span data-stu-id="6d006-261">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="6d006-262">Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="6d006-262">Machine Learning Batch Execution activity</span></span>](transform-data-using-machine-learning.md)
* [<span data-ttu-id="6d006-263">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="6d006-263">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
