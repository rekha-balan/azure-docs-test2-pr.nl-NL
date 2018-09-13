---
title: Create predictive data pipelines using Azure Data Factory | Microsoft Docs
description: Describes how to create create predictive pipelines using Azure Data Factory and Azure Machine Learning
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 4fad8445-4e96-4ce0-aa23-9b88e5ec1965
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: shlo
ms.openlocfilehash: ad7ef9307b61ad3bd2f9ea3d25575c68d9bf77b6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556223"
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="823ce-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="823ce-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>

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

## <a name="introduction"></a><span data-ttu-id="823ce-114">Introduction</span><span class="sxs-lookup"><span data-stu-id="823ce-114">Introduction</span></span>

### <a name="azure-machine-learning"></a><span data-ttu-id="823ce-115">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="823ce-115">Azure Machine Learning</span></span>
<span data-ttu-id="823ce-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="823ce-116">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="823ce-117">From a high-level point of view, it is done in three steps:</span><span class="sxs-lookup"><span data-stu-id="823ce-117">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="823ce-118">**Create a training experiment**.</span><span class="sxs-lookup"><span data-stu-id="823ce-118">**Create a training experiment**.</span></span> <span data-ttu-id="823ce-119">You do this step by using the Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="823ce-119">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="823ce-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span><span class="sxs-lookup"><span data-stu-id="823ce-120">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="823ce-121">**Convert it to a predictive experiment**.</span><span class="sxs-lookup"><span data-stu-id="823ce-121">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="823ce-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span><span class="sxs-lookup"><span data-stu-id="823ce-122">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="823ce-123">**Deploy it as a web service**.</span><span class="sxs-lookup"><span data-stu-id="823ce-123">**Deploy it as a web service**.</span></span> <span data-ttu-id="823ce-124">You can publish your scoring experiment as an Azure web service.</span><span class="sxs-lookup"><span data-stu-id="823ce-124">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="823ce-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span><span class="sxs-lookup"><span data-stu-id="823ce-125">You can send data to your model via this web service end point and receive result predictions fro the model.</span></span>  

### <a name="azure-data-factory"></a><span data-ttu-id="823ce-126">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="823ce-126">Azure Data Factory</span></span>
<span data-ttu-id="823ce-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span><span class="sxs-lookup"><span data-stu-id="823ce-127">Data Factory is a cloud-based data integration service that orchestrates and automates the **movement** and **transformation** of data.</span></span> <span data-ttu-id="823ce-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span><span class="sxs-lookup"><span data-stu-id="823ce-128">You can create data integration solutions using Azure Data Factory that can ingest data from various data stores, transform/process the data, and publish the result data to the data stores.</span></span>

<span data-ttu-id="823ce-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span><span class="sxs-lookup"><span data-stu-id="823ce-129">Data Factory service allows you to create data pipelines that move and transform data, and then run the pipelines on a specified schedule (hourly, daily, weekly, etc.).</span></span> <span data-ttu-id="823ce-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span><span class="sxs-lookup"><span data-stu-id="823ce-130">It also provides rich visualizations to display the lineage and dependencies between your data pipelines, and monitor all your data pipelines from a single unified view to easily pinpoint issues and setup monitoring alerts.</span></span>

<span data-ttu-id="823ce-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span><span class="sxs-lookup"><span data-stu-id="823ce-131">See [Introduction to Azure Data Factory](data-factory-introduction.md) and [Build your first pipeline](data-factory-build-your-first-pipeline.md) articles to quickly get started with the Azure Data Factory service.</span></span>

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="823ce-132">Data Factory and Machine Learning together</span><span class="sxs-lookup"><span data-stu-id="823ce-132">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="823ce-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="823ce-133">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="823ce-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span><span class="sxs-lookup"><span data-stu-id="823ce-134">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> <span data-ttu-id="823ce-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span><span class="sxs-lookup"><span data-stu-id="823ce-135">See [Invoking an Azure ML web service using the Batch Execution Activity](#invoking-an-azure-ml-web-service-using-the-batch-execution-activity) section for details.</span></span>

<span data-ttu-id="823ce-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span><span class="sxs-lookup"><span data-stu-id="823ce-136">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="823ce-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span><span class="sxs-lookup"><span data-stu-id="823ce-137">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="823ce-138">Publish the training experiment (not predictive experiment) as a web service.</span><span class="sxs-lookup"><span data-stu-id="823ce-138">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="823ce-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span><span class="sxs-lookup"><span data-stu-id="823ce-139">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="823ce-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span><span class="sxs-lookup"><span data-stu-id="823ce-140">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="823ce-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span><span class="sxs-lookup"><span data-stu-id="823ce-141">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="823ce-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span><span class="sxs-lookup"><span data-stu-id="823ce-142">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="823ce-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="823ce-143">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

## <a name="invoking-a-web-service-using-batch-execution-activity"></a><span data-ttu-id="823ce-144">Invoking a web service using Batch Execution Activity</span><span class="sxs-lookup"><span data-stu-id="823ce-144">Invoking a web service using Batch Execution Activity</span></span>
<span data-ttu-id="823ce-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="823ce-145">You use Azure Data Factory to orchestrate data movement and processing, and then perform batch execution using Azure Machine Learning.</span></span> <span data-ttu-id="823ce-146">Here are the top-level steps:</span><span class="sxs-lookup"><span data-stu-id="823ce-146">Here are the top-level steps:</span></span>

1. <span data-ttu-id="823ce-147">Create an Azure Machine Learning linked service.</span><span class="sxs-lookup"><span data-stu-id="823ce-147">Create an Azure Machine Learning linked service.</span></span> <span data-ttu-id="823ce-148">You need the following values:</span><span class="sxs-lookup"><span data-stu-id="823ce-148">You need the following values:</span></span>

   1. <span data-ttu-id="823ce-149">**Request URI** for the Batch Execution API.</span><span class="sxs-lookup"><span data-stu-id="823ce-149">**Request URI** for the Batch Execution API.</span></span> <span data-ttu-id="823ce-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span><span class="sxs-lookup"><span data-stu-id="823ce-150">You can find the Request URI by clicking the **BATCH EXECUTION** link in the web services page.</span></span>
   2. <span data-ttu-id="823ce-151">**API key** for the published Azure Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="823ce-151">**API key** for the published Azure Machine Learning web service.</span></span> <span data-ttu-id="823ce-152">You can find the API key by clicking the web service that you have published.</span><span class="sxs-lookup"><span data-stu-id="823ce-152">You can find the API key by clicking the web service that you have published.</span></span>
   3. <span data-ttu-id="823ce-153">Use the **AzureMLBatchExecution** activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-153">Use the **AzureMLBatchExecution** activity.</span></span>

      ![Machine Learning Dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/AzureMLDashboard.png)

      ![Batch URI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/batch-uri.png)

### <a name="scenario-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="823ce-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="823ce-156">Scenario: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>
<span data-ttu-id="823ce-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="823ce-157">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="823ce-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-158">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="823ce-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span><span class="sxs-lookup"><span data-stu-id="823ce-159">The activity has the dataset **DecisionTreeInputBlob** as input and **DecisionTreeResultBlob** as the output.</span></span> <span data-ttu-id="823ce-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span><span class="sxs-lookup"><span data-stu-id="823ce-160">The **DecisionTreeInputBlob** is passed as an input to the web service by using the **webServiceInput** JSON property.</span></span> <span data-ttu-id="823ce-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span><span class="sxs-lookup"><span data-stu-id="823ce-161">The **DecisionTreeResultBlob** is passed as an output to the Web service by using the **webServiceOutputs** JSON property.</span></span>  

> [!IMPORTANT]
> If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**. See the [Web service requires multiple inputs](#web-service-requires-multiple-inputs) section for an example of using the webServiceInputs property.
>
> Datasets that are referenced by the **webServiceInput**/**webServiceInputs** and **webServiceOutputs** properties (in **typeProperties**) must also be included in the Activity **inputs** and **outputs**.
>
> In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize. The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments. You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.
>
>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchExecution",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "DecisionTreeInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "DecisionTreeResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "typeProperties":
        {
            "webServiceInput": "DecisionTreeInputBlob",
            "webServiceOutputs": {
                "output1": "DecisionTreeResultBlob"
            }                
        },
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```
> [!NOTE]
> Only inputs and outputs of the AzureMLBatchExecution activity can be passed as parameters to the Web service. For example, in the above JSON snippet, DecisionTreeInputBlob is an input to the AzureMLBatchExecution activity, which is passed as an input to the Web service via webServiceInput parameter.   
>
>

### <a name="example"></a><span data-ttu-id="823ce-170">Example</span><span class="sxs-lookup"><span data-stu-id="823ce-170">Example</span></span>
<span data-ttu-id="823ce-171">This example uses Azure Storage to hold both the input and output data.</span><span class="sxs-lookup"><span data-stu-id="823ce-171">This example uses Azure Storage to hold both the input and output data.</span></span>

<span data-ttu-id="823ce-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span><span class="sxs-lookup"><span data-stu-id="823ce-172">We recommend that you go through the [Build your first pipeline with Data Factory][adf-build-1st-pipeline] tutorial before going through this example.</span></span> <span data-ttu-id="823ce-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span><span class="sxs-lookup"><span data-stu-id="823ce-173">Use the Data Factory Editor to create Data Factory artifacts (linked services, datasets, pipeline) in this example.</span></span>   

1. <span data-ttu-id="823ce-174">Create a **linked service** for your **Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="823ce-174">Create a **linked service** for your **Azure Storage**.</span></span> <span data-ttu-id="823ce-175">If the input and output files are in different storage accounts, you need two linked services.</span><span class="sxs-lookup"><span data-stu-id="823ce-175">If the input and output files are in different storage accounts, you need two linked services.</span></span> <span data-ttu-id="823ce-176">Here is a JSON example:</span><span class="sxs-lookup"><span data-stu-id="823ce-176">Here is a JSON example:</span></span>

    ```JSON
    {
      "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
          "connectionString": "DefaultEndpointsProtocol=https;AccountName=[acctName];AccountKey=[acctKey]"
        }
      }
    }
    ```
2. <span data-ttu-id="823ce-177">Create the **input** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="823ce-177">Create the **input** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="823ce-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span><span class="sxs-lookup"><span data-stu-id="823ce-178">Unlike some other Data Factory datasets, these datasets must contain both **folderPath** and **fileName** values.</span></span> <span data-ttu-id="823ce-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span><span class="sxs-lookup"><span data-stu-id="823ce-179">You can use partitioning to cause each batch execution (each data slice) to process or produce unique input and output files.</span></span> <span data-ttu-id="823ce-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span><span class="sxs-lookup"><span data-stu-id="823ce-180">You may need to include some upstream activity to transform the input into the CSV file format and place it in the storage account for each slice.</span></span> <span data-ttu-id="823ce-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-181">In that case, you would not include the **external** and **externalData** settings shown in the following example, and your DecisionTreeInputBlob would be the output dataset of a different Activity.</span></span>

    ```JSON
    {
      "name": "DecisionTreeInputBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/input",
          "fileName": "in.csv",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "external": true,
        "availability": {
          "frequency": "Day",
          "interval": 1
        },
        "policy": {
          "externalData": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
          }
        }
      }
    }
    ```

    <span data-ttu-id="823ce-182">Your input csv file must have the column header row.</span><span class="sxs-lookup"><span data-stu-id="823ce-182">Your input csv file must have the column header row.</span></span> <span data-ttu-id="823ce-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span><span class="sxs-lookup"><span data-stu-id="823ce-183">If you are using the **Copy Activity** to create/move the csv into the blob storage, you should set the sink property **blobWriterAddHeader** to **true**.</span></span> <span data-ttu-id="823ce-184">For example:</span><span class="sxs-lookup"><span data-stu-id="823ce-184">For example:</span></span>

    ```JSON
    sink:
    {
        "type": "BlobSink",     
        "blobWriterAddHeader": true
    }
    ```

    <span data-ttu-id="823ce-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span><span class="sxs-lookup"><span data-stu-id="823ce-185">If the csv file does not have the header row, you may see the following error: **Error in Activity: Error reading string. Unexpected token: StartObject. Path '', line 1, position 1**.</span></span>
3. <span data-ttu-id="823ce-186">Create the **output** Azure Data Factory **dataset**.</span><span class="sxs-lookup"><span data-stu-id="823ce-186">Create the **output** Azure Data Factory **dataset**.</span></span> <span data-ttu-id="823ce-187">This example uses partitioning to create a unique output path for each slice execution.</span><span class="sxs-lookup"><span data-stu-id="823ce-187">This example uses partitioning to create a unique output path for each slice execution.</span></span> <span data-ttu-id="823ce-188">Without the partitioning, the activity would overwrite the file.</span><span class="sxs-lookup"><span data-stu-id="823ce-188">Without the partitioning, the activity would overwrite the file.</span></span>

    ```JSON
    {
      "name": "DecisionTreeResultBlob",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
          "folderPath": "azuremltesting/scored/{folderpart}/",
          "fileName": "{filepart}result.csv",
          "partitionedBy": [
            {
              "name": "folderpart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "yyyyMMdd"
              }
            },
            {
              "name": "filepart",
              "value": {
                "type": "DateTime",
                "date": "SliceStart",
                "format": "HHmmss"
              }
            }
          ],
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Day",
          "interval": 15
        }
      }
    }
    ```
4. <span data-ttu-id="823ce-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span><span class="sxs-lookup"><span data-stu-id="823ce-189">Create a **linked service** of type: **AzureMLLinkedService**, providing the API key and model batch execution URL.</span></span>

    ```JSON
    {
      "name": "MyAzureMLLinkedService",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
          "mlEndpoint": "https://[batch execution endpoint]/jobs",
          "apiKey": "[apikey]"
        }
      }
    }
    ```
5. <span data-ttu-id="823ce-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-190">Finally, author a pipeline containing an **AzureMLBatchExecution** Activity.</span></span> <span data-ttu-id="823ce-191">At runtime, pipeline performs the following steps:</span><span class="sxs-lookup"><span data-stu-id="823ce-191">At runtime, pipeline performs the following steps:</span></span>

   1. <span data-ttu-id="823ce-192">Gets the location of the input file from your input datasets.</span><span class="sxs-lookup"><span data-stu-id="823ce-192">Gets the location of the input file from your input datasets.</span></span>
   2. <span data-ttu-id="823ce-193">Invokes the Azure Machine Learning batch execution API</span><span class="sxs-lookup"><span data-stu-id="823ce-193">Invokes the Azure Machine Learning batch execution API</span></span>
   3. <span data-ttu-id="823ce-194">Copies the batch execution output to the blob given in your output dataset.</span><span class="sxs-lookup"><span data-stu-id="823ce-194">Copies the batch execution output to the blob given in your output dataset.</span></span>

      > [!NOTE]
      > AzureMLBatchExecution activity can have zero or more inputs and one or more outputs.
      >
      >

    ```JSON
    {
        "name": "PredictivePipeline",
        "properties": {
            "description": "use AzureML model",
            "activities": [
            {
                "name": "MLActivity",
                "type": "AzureMLBatchExecution",
                "description": "prediction analysis on batch input",
                "inputs": [
                {
                    "name": "DecisionTreeInputBlob"
                }
                ],
                "outputs": [
                {
                    "name": "DecisionTreeResultBlob"
                }
                ],
                "linkedServiceName": "MyAzureMLLinkedService",
                "typeProperties":
                {
                    "webServiceInput": "DecisionTreeInputBlob",
                    "webServiceOutputs": {
                        "output1": "DecisionTreeResultBlob"
                    }                
                },
                "policy": {
                    "concurrency": 3,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            }
            ],
            "start": "2016-02-13T00:00:00Z",
            "end": "2016-02-14T00:00:00Z"
        }
    }
    ```

      <span data-ttu-id="823ce-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="823ce-196">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="823ce-197">For example: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="823ce-197">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="823ce-198">The **end** time is optional.</span><span class="sxs-lookup"><span data-stu-id="823ce-198">The **end** time is optional.</span></span> <span data-ttu-id="823ce-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="823ce-199">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="823ce-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="823ce-200">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="823ce-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span><span class="sxs-lookup"><span data-stu-id="823ce-201">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

      > [!NOTE]
      > Specifying input for the AzureMLBatchExecution activity is optional.
      >
      >

### <a name="scenario-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="823ce-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span><span class="sxs-lookup"><span data-stu-id="823ce-203">Scenario: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="823ce-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span><span class="sxs-lookup"><span data-stu-id="823ce-204">Another common scenario when creating Azure ML experiments is to use Reader and Writer modules.</span></span> <span data-ttu-id="823ce-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span><span class="sxs-lookup"><span data-stu-id="823ce-205">The reader module is used to load data into an experiment and the writer module is to save data from your experiments.</span></span> <span data-ttu-id="823ce-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="823ce-206">For details about reader and writer modules, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="823ce-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span><span class="sxs-lookup"><span data-stu-id="823ce-207">When using the reader and writer modules, it is good practice to use a Web service parameter for each property of these reader/writer modules.</span></span> <span data-ttu-id="823ce-208">These web parameters enable you to configure the values during runtime.</span><span class="sxs-lookup"><span data-stu-id="823ce-208">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="823ce-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="823ce-209">For example, you could create an experiment with a reader module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="823ce-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="823ce-210">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called YYY.database.windows.net.</span></span> <span data-ttu-id="823ce-211">You can use a Web service parameter to allow this value to be configured.</span><span class="sxs-lookup"><span data-stu-id="823ce-211">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> Web service input and output are different from Web service parameters. In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service. In this scenario, you pass parameters for a Web service that correspond to properties of reader/writer modules.
>
>

<span data-ttu-id="823ce-215">Let's look at a scenario for using Web service parameters.</span><span class="sxs-lookup"><span data-stu-id="823ce-215">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="823ce-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="823ce-216">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="823ce-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="823ce-217">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="823ce-218">No web service inputs and outputs are defined in the experiments.</span><span class="sxs-lookup"><span data-stu-id="823ce-218">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="823ce-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span><span class="sxs-lookup"><span data-stu-id="823ce-219">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="823ce-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-220">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="823ce-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span><span class="sxs-lookup"><span data-stu-id="823ce-221">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```

<span data-ttu-id="823ce-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="823ce-222">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.
>
>

### <a name="using-a-reader-module-to-read-data-from-multiple-files-in-azure-blob"></a><span data-ttu-id="823ce-224">Using a Reader module to read data from multiple files in Azure Blob</span><span class="sxs-lookup"><span data-stu-id="823ce-224">Using a Reader module to read data from multiple files in Azure Blob</span></span>
<span data-ttu-id="823ce-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span><span class="sxs-lookup"><span data-stu-id="823ce-225">Big data pipelines with activities such as Pig and Hive can produce one or more output files with no extensions.</span></span> <span data-ttu-id="823ce-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span><span class="sxs-lookup"><span data-stu-id="823ce-226">For example, when you specify an external Hive table, the data for the external Hive table can be stored in Azure blob storage with the following name 000000_0.</span></span> <span data-ttu-id="823ce-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span><span class="sxs-lookup"><span data-stu-id="823ce-227">You can use the reader module in an experiment to read multiple files, and use them for predictions.</span></span>

<span data-ttu-id="823ce-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span><span class="sxs-lookup"><span data-stu-id="823ce-228">When using the reader module in an Azure Machine Learning experiment, you can specify Azure Blob as an input.</span></span> <span data-ttu-id="823ce-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="823ce-229">The files in the Azure blob storage can be the output files (Example: 000000_0) that are produced by a Pig and Hive script running on HDInsight.</span></span> <span data-ttu-id="823ce-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span><span class="sxs-lookup"><span data-stu-id="823ce-230">The reader module allows you to read files (with no extensions) by configuring the **Path to container, directory/blob**.</span></span> <span data-ttu-id="823ce-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="823ce-231">The **Path to container** points to the container and **directory/blob** points to folder that contains the files as shown in the following image.</span></span> <span data-ttu-id="823ce-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span><span class="sxs-lookup"><span data-stu-id="823ce-232">The asterisk that is, \*) **specifies that all the files in the container/folder (that is, data/aggregateddata/year=2014/month-6/\*)** are read as part of the experiment.</span></span>

![Azure Blob properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-create-predictive-pipelines/azure-blob-properties.png)

### <a name="example"></a><span data-ttu-id="823ce-234">Example</span><span class="sxs-lookup"><span data-stu-id="823ce-234">Example</span></span>
#### <a name="pipeline-with-azuremlbatchexecution-activity-with-web-service-parameters"></a><span data-ttu-id="823ce-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span><span class="sxs-lookup"><span data-stu-id="823ce-235">Pipeline with AzureMLBatchExecution activity with Web Service Parameters</span></span>

```JSON
{
  "name": "MLWithSqlReaderSqlWriter",
  "properties": {
    "description": "Azure ML model with sql azure reader/writer",
    "activities": [
      {
        "name": "MLSqlReaderSqlWriterActivity",
        "type": "AzureMLBatchExecution",
        "description": "test",
        "inputs": [
          {
            "name": "MLSqlInput"
          }
        ],
        "outputs": [
          {
            "name": "MLSqlOutput"
          }
        ],
        "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
        "typeProperties":
        {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
                "output1": "MLSqlOutput"
            }
              "globalParameters": {
                "Database server name": "<myserver>.database.windows.net",
                "Database name": "<database>",
                "Server user account name": "<user name>",
                "Server user account password": "<password>"
              }              
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        },
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

<span data-ttu-id="823ce-236">In the above JSON example:</span><span class="sxs-lookup"><span data-stu-id="823ce-236">In the above JSON example:</span></span>

* <span data-ttu-id="823ce-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="823ce-237">The deployed Azure Machine Learning Web service uses a reader and a writer module to read/write data from/to an Azure SQL Database.</span></span> <span data-ttu-id="823ce-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span><span class="sxs-lookup"><span data-stu-id="823ce-238">This Web service exposes the following four parameters:  Database server name, Database name, Server user account name, and Server user account password.</span></span>  
* <span data-ttu-id="823ce-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span><span class="sxs-lookup"><span data-stu-id="823ce-239">Both **start** and **end** datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="823ce-240">For example: 2014-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="823ce-240">For example: 2014-10-14T16:32:41Z.</span></span> <span data-ttu-id="823ce-241">The **end** time is optional.</span><span class="sxs-lookup"><span data-stu-id="823ce-241">The **end** time is optional.</span></span> <span data-ttu-id="823ce-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span><span class="sxs-lookup"><span data-stu-id="823ce-242">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours.**"</span></span> <span data-ttu-id="823ce-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span><span class="sxs-lookup"><span data-stu-id="823ce-243">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span> <span data-ttu-id="823ce-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span><span class="sxs-lookup"><span data-stu-id="823ce-244">See [JSON Scripting Reference](https://msdn.microsoft.com/library/dn835050.aspx) for details about JSON properties.</span></span>

### <a name="other-scenarios"></a><span data-ttu-id="823ce-245">Other scenarios</span><span class="sxs-lookup"><span data-stu-id="823ce-245">Other scenarios</span></span>
#### <a name="web-service-requires-multiple-inputs"></a><span data-ttu-id="823ce-246">Web service requires multiple inputs</span><span class="sxs-lookup"><span data-stu-id="823ce-246">Web service requires multiple inputs</span></span>
<span data-ttu-id="823ce-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span><span class="sxs-lookup"><span data-stu-id="823ce-247">If the web service takes multiple inputs, use the **webServiceInputs** property instead of using **webServiceInput**.</span></span> <span data-ttu-id="823ce-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span><span class="sxs-lookup"><span data-stu-id="823ce-248">Datasets that are referenced by the **webServiceInputs** must also be included in the Activity **inputs**.</span></span>

<span data-ttu-id="823ce-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span><span class="sxs-lookup"><span data-stu-id="823ce-249">In your Azure ML experiment, web service input and output ports and global parameters have default names ("input1", "input2") that you can customize.</span></span> <span data-ttu-id="823ce-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span><span class="sxs-lookup"><span data-stu-id="823ce-250">The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments.</span></span> <span data-ttu-id="823ce-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span><span class="sxs-lookup"><span data-stu-id="823ce-251">You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.</span></span>

```JSON
{
    "name": "PredictivePipeline",
    "properties": {
        "description": "use AzureML model",
        "activities": [{
            "name": "MLActivity",
            "type": "AzureMLBatchExecution",
            "description": "prediction analysis on batch input",
            "inputs": [{
                "name": "inputDataset1"
            }, {
                "name": "inputDataset2"
            }],
            "outputs": [{
                "name": "outputDataset"
            }],
            "linkedServiceName": "MyAzureMLLinkedService",
            "typeProperties": {
                "webServiceInputs": {
                    "input1": "inputDataset1",
                    "input2": "inputDataset2"
                },
                "webServiceOutputs": {
                    "output1": "outputDataset"
                }
            },
            "policy": {
                "concurrency": 3,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "02:00:00"
            }
        }],
        "start": "2016-02-13T00:00:00Z",
        "end": "2016-02-14T00:00:00Z"
    }
}
```

#### <a name="web-service-does-not-require-an-input"></a><span data-ttu-id="823ce-252">Web Service does not require an input</span><span class="sxs-lookup"><span data-stu-id="823ce-252">Web Service does not require an input</span></span>
<span data-ttu-id="823ce-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span><span class="sxs-lookup"><span data-stu-id="823ce-253">Azure ML batch execution web services can be used to run any workflows, for example R or Python scripts, that may not require any inputs.</span></span> <span data-ttu-id="823ce-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="823ce-254">Or, the experiment might be configured with a Reader module that does not expose any GlobalParameters.</span></span> <span data-ttu-id="823ce-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span><span class="sxs-lookup"><span data-stu-id="823ce-255">In that case, the AzureMLBatchExecution Activity would be configured as follows:</span></span>

```JSON
{
    "name": "scoring service",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "myBlob"
        }
    ],
    "typeProperties": {
        "webServiceOutputs": {
            "output1": "myBlob"
        }              
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-does-not-require-an-inputoutput"></a><span data-ttu-id="823ce-256">Web Service does not require an input/output</span><span class="sxs-lookup"><span data-stu-id="823ce-256">Web Service does not require an input/output</span></span>
<span data-ttu-id="823ce-257">The Azure ML batch execution web service might not have any Web Service output configured.</span><span class="sxs-lookup"><span data-stu-id="823ce-257">The Azure ML batch execution web service might not have any Web Service output configured.</span></span> <span data-ttu-id="823ce-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span><span class="sxs-lookup"><span data-stu-id="823ce-258">In this example, there is no Web Service input or output, nor are any GlobalParameters configured.</span></span> <span data-ttu-id="823ce-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span><span class="sxs-lookup"><span data-stu-id="823ce-259">There is still an output configured on the activity itself, but it is not given as a webServiceOutput.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "outputs": [
        {
            "name": "placeholderOutputDataset"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

#### <a name="web-service-uses-readers-and-writers-and-the-activity-runs-only-when-other-activities-have-succeeded"></a><span data-ttu-id="823ce-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span><span class="sxs-lookup"><span data-stu-id="823ce-260">Web Service uses readers and writers, and the activity runs only when other activities have succeeded</span></span>
<span data-ttu-id="823ce-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span><span class="sxs-lookup"><span data-stu-id="823ce-261">The Azure ML web service reader and writer modules might be configured to run with or without any GlobalParameters.</span></span> <span data-ttu-id="823ce-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span><span class="sxs-lookup"><span data-stu-id="823ce-262">However, you may want to embed service calls in a pipeline that uses dataset dependencies to invoke the service only when some upstream processing has completed.</span></span> <span data-ttu-id="823ce-263">You can also trigger some other action after the batch execution has completed using this approach.</span><span class="sxs-lookup"><span data-stu-id="823ce-263">You can also trigger some other action after the batch execution has completed using this approach.</span></span> <span data-ttu-id="823ce-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span><span class="sxs-lookup"><span data-stu-id="823ce-264">In that case, you can express the dependencies using activity inputs and outputs, without naming any of them as Web Service inputs or outputs.</span></span>

```JSON
{
    "name": "retraining",
    "type": "AzureMLBatchExecution",
    "inputs": [
        {
            "name": "upstreamData1"
        },
        {
            "name": "upstreamData2"
        }
    ],
    "outputs": [
        {
            "name": "downstreamData"
        }
    ],
    "typeProperties": {
     },
    "linkedServiceName": "mlEndpoint",
    "policy": {
        "concurrency": 1,
        "executionPriorityOrder": "NewestFirst",
        "retry": 1,
        "timeout": "02:00:00"
    }
},
```

<span data-ttu-id="823ce-265">The **takeaways** are:</span><span class="sxs-lookup"><span data-stu-id="823ce-265">The **takeaways** are:</span></span>

* <span data-ttu-id="823ce-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span><span class="sxs-lookup"><span data-stu-id="823ce-266">If your experiment endpoint uses a webServiceInput: it is represented by a blob dataset and is included in the activity inputs and the webServiceInput property.</span></span> <span data-ttu-id="823ce-267">Otherwise, the webServiceInput property is omitted.</span><span class="sxs-lookup"><span data-stu-id="823ce-267">Otherwise, the webServiceInput property is omitted.</span></span>
* <span data-ttu-id="823ce-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span><span class="sxs-lookup"><span data-stu-id="823ce-268">If your experiment endpoint uses webServiceOutput(s): they are represented by blob datasets and are included in the activity outputs and in the webServiceOutputs property.</span></span> <span data-ttu-id="823ce-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span><span class="sxs-lookup"><span data-stu-id="823ce-269">The activity outputs and webServiceOutputs are mapped by the name of each output in the experiment.</span></span> <span data-ttu-id="823ce-270">Otherwise, the webServiceOutputs property is omitted.</span><span class="sxs-lookup"><span data-stu-id="823ce-270">Otherwise, the webServiceOutputs property is omitted.</span></span>
* <span data-ttu-id="823ce-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span><span class="sxs-lookup"><span data-stu-id="823ce-271">If your experiment endpoint exposes globalParameter(s), they are given in the activity globalParameters property as key, value pairs.</span></span> <span data-ttu-id="823ce-272">Otherwise, the globalParameters property is omitted.</span><span class="sxs-lookup"><span data-stu-id="823ce-272">Otherwise, the globalParameters property is omitted.</span></span> <span data-ttu-id="823ce-273">The keys are case-sensitive.</span><span class="sxs-lookup"><span data-stu-id="823ce-273">The keys are case-sensitive.</span></span> <span data-ttu-id="823ce-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span><span class="sxs-lookup"><span data-stu-id="823ce-274">[Azure Data Factory functions](data-factory-functions-variables.md) may be used in the values.</span></span>
* <span data-ttu-id="823ce-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span><span class="sxs-lookup"><span data-stu-id="823ce-275">Additional datasets may be included in the Activity inputs and outputs properties, without being referenced in the Activity typeProperties.</span></span> <span data-ttu-id="823ce-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-276">These datasets govern execution using slice dependencies but are otherwise ignored by the AzureMLBatchExecution Activity.</span></span>


## <a name="updating-models-using-update-resource-activity"></a><span data-ttu-id="823ce-277">Updating models using Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="823ce-277">Updating models using Update Resource Activity</span></span>
<span data-ttu-id="823ce-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span><span class="sxs-lookup"><span data-stu-id="823ce-278">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="823ce-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="823ce-279">See [Updating models using Update Resource Activity](data-factory-azure-ml-update-resource-activity.md) article for details.</span></span>

### <a name="reader-and-writer-modules"></a><span data-ttu-id="823ce-280">Reader and Writer Modules</span><span class="sxs-lookup"><span data-stu-id="823ce-280">Reader and Writer Modules</span></span>
<span data-ttu-id="823ce-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span><span class="sxs-lookup"><span data-stu-id="823ce-281">A common scenario for using Web service parameters is the use of Azure SQL Readers and Writers.</span></span> <span data-ttu-id="823ce-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="823ce-282">The reader module is used to load data into an experiment from data management services outside Azure Machine Learning Studio.</span></span> <span data-ttu-id="823ce-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="823ce-283">The writer module is to save data from your experiments into data management services outside Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="823ce-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="823ce-284">For details about Azure Blob/Azure SQL reader/writer, see [Reader](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Writer](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span> <span data-ttu-id="823ce-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span><span class="sxs-lookup"><span data-stu-id="823ce-285">The example in the previous section used the Azure Blob reader and Azure Blob writer.</span></span> <span data-ttu-id="823ce-286">This section discusses using Azure SQL reader and Azure SQL writer.</span><span class="sxs-lookup"><span data-stu-id="823ce-286">This section discusses using Azure SQL reader and Azure SQL writer.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="823ce-287">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="823ce-287">Frequently asked questions</span></span>
<span data-ttu-id="823ce-288">**Q:** I have multiple files that are generated by my big data pipelines.</span><span class="sxs-lookup"><span data-stu-id="823ce-288">**Q:** I have multiple files that are generated by my big data pipelines.</span></span> <span data-ttu-id="823ce-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span><span class="sxs-lookup"><span data-stu-id="823ce-289">Can I use the AzureMLBatchExecution Activity to work on all the files?</span></span>

<span data-ttu-id="823ce-290">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="823ce-290">**A:** Yes.</span></span> <span data-ttu-id="823ce-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span><span class="sxs-lookup"><span data-stu-id="823ce-291">See the **Using a Reader module to read data from multiple files in Azure Blob** section for details.</span></span>

## <a name="azure-ml-batch-scoring-activity"></a><span data-ttu-id="823ce-292">Azure ML Batch Scoring Activity</span><span class="sxs-lookup"><span data-stu-id="823ce-292">Azure ML Batch Scoring Activity</span></span>
<span data-ttu-id="823ce-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span><span class="sxs-lookup"><span data-stu-id="823ce-293">If you are using the **AzureMLBatchScoring** activity to integrate with Azure Machine Learning, we recommend that you use the latest **AzureMLBatchExecution** activity.</span></span>

<span data-ttu-id="823ce-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="823ce-294">The AzureMLBatchExecution activity is introduced in the August 2015 release of Azure SDK and Azure PowerShell.</span></span>

<span data-ttu-id="823ce-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span><span class="sxs-lookup"><span data-stu-id="823ce-295">If you want to continue using the AzureMLBatchScoring activity, continue reading through this section.</span></span>  

### <a name="azure-ml-batch-scoring-activity-using-azure-storage-for-inputoutput"></a><span data-ttu-id="823ce-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span><span class="sxs-lookup"><span data-stu-id="823ce-296">Azure ML Batch Scoring activity using Azure Storage for input/output</span></span>

```JSON
{
  "name": "PredictivePipeline",
  "properties": {
    "description": "use AzureML model",
    "activities": [
      {
        "name": "MLActivity",
        "type": "AzureMLBatchScoring",
        "description": "prediction analysis on batch input",
        "inputs": [
          {
            "name": "ScoringInputBlob"
          }
        ],
        "outputs": [
          {
            "name": "ScoringResultBlob"
          }
        ],
        "linkedServiceName": "MyAzureMLLinkedService",
        "policy": {
          "concurrency": 3,
          "executionPriorityOrder": "NewestFirst",
          "retry": 1,
          "timeout": "02:00:00"
        }
      }
    ],
    "start": "2016-02-13T00:00:00Z",
    "end": "2016-02-14T00:00:00Z"
  }
}
```

### <a name="web-service-parameters"></a><span data-ttu-id="823ce-297">Web Service Parameters</span><span class="sxs-lookup"><span data-stu-id="823ce-297">Web Service Parameters</span></span>
<span data-ttu-id="823ce-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="823ce-298">To specify values for Web service parameters, add a **typeProperties** section to the **AzureMLBatchScoringActivty** section in the pipeline JSON as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
        "Param 1": "Value 1",
        "Param 2": "Value 2"
    }
}
```
<span data-ttu-id="823ce-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="823ce-299">You can also use [Data Factory Functions](data-factory-functions-variables.md) in passing values for the Web service parameters as shown in the following example:</span></span>

```JSON
"typeProperties": {
    "webServiceParameters": {
       "Database query": "$$Text.Format('SELECT * FROM myTable WHERE timeColumn = \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(WindowStart, 0))"
    }
}
```

> [!NOTE]
> The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.
>
>

## <a name="see-also"></a><span data-ttu-id="823ce-301">See Also</span><span class="sxs-lookup"><span data-stu-id="823ce-301">See Also</span></span>
* [<span data-ttu-id="823ce-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="823ce-302">Azure blog post: Getting started with Azure Data Factory and Azure Machine Learning</span></span>](https://azure.microsoft.com/blog/getting-started-with-azure-data-factory-and-azure-machine-learning-4/)

[adf-build-1st-pipeline]: data-factory-build-your-first-pipeline.md

[azure-machine-learning]: http://azure.microsoft.com/services/machine-learning/



