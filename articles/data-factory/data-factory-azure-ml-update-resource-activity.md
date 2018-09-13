---
title: Update Machine Learning models using Azure Data Factory | Microsoft Docs
description: Describes how to create create predictive pipelines using Azure Data Factory and Azure Machine Learning
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: shlo
ms.openlocfilehash: e3e1377688c624c541d5d241732361e775e362de
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553448"
---
# <a name="updating-azure-machine-learning-models-using-update-resource-activity"></a><span data-ttu-id="c9621-103">Updating Azure Machine Learning models using Update Resource Activity</span><span class="sxs-lookup"><span data-stu-id="c9621-103">Updating Azure Machine Learning models using Update Resource Activity</span></span>

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

<span data-ttu-id="c9621-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span><span class="sxs-lookup"><span data-stu-id="c9621-114">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](data-factory-azure-ml-batch-execution-activity.md).</span></span> <span data-ttu-id="c9621-115">If you haven't already done so, review the main article before reading through this article.</span><span class="sxs-lookup"><span data-stu-id="c9621-115">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="c9621-116">Overview</span><span class="sxs-lookup"><span data-stu-id="c9621-116">Overview</span></span>
<span data-ttu-id="c9621-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span><span class="sxs-lookup"><span data-stu-id="c9621-117">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="c9621-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span><span class="sxs-lookup"><span data-stu-id="c9621-118">After you are done with retraining, you want to update the scoring web service with the retrained ML model.</span></span> <span data-ttu-id="c9621-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span><span class="sxs-lookup"><span data-stu-id="c9621-119">The typical steps to enable retraining and updating Azure ML models via web services are:</span></span>

1. <span data-ttu-id="c9621-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="c9621-120">Create an experiment in [Azure ML Studio](https://studio.azureml.net).</span></span>
2. <span data-ttu-id="c9621-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span><span class="sxs-lookup"><span data-stu-id="c9621-121">When you are satisfied with the model, use Azure ML Studio to publish web services for both the **training experiment** and scoring/**predictive experiment**.</span></span>

<span data-ttu-id="c9621-122">The following table describes the web services used in this example.</span><span class="sxs-lookup"><span data-stu-id="c9621-122">The following table describes the web services used in this example.</span></span>  <span data-ttu-id="c9621-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span><span class="sxs-lookup"><span data-stu-id="c9621-123">See [Retrain Machine Learning models programmatically](../machine-learning/machine-learning-retrain-models-programmatically.md) for details.</span></span>

- <span data-ttu-id="c9621-124">**Training web service** - Receives training data and produces trained models.</span><span class="sxs-lookup"><span data-stu-id="c9621-124">**Training web service** - Receives training data and produces trained models.</span></span> <span data-ttu-id="c9621-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c9621-125">The output of the retraining is an .ilearner file in an Azure Blob storage.</span></span> <span data-ttu-id="c9621-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-126">The **default endpoint** is automatically created for you when you publish the training experiment as a web service.</span></span> <span data-ttu-id="c9621-127">You can create more endpoints but the example uses only the default endpoint.</span><span class="sxs-lookup"><span data-stu-id="c9621-127">You can create more endpoints but the example uses only the default endpoint.</span></span>
- <span data-ttu-id="c9621-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span><span class="sxs-lookup"><span data-stu-id="c9621-128">**Scoring web service** - Receives unlabeled data examples and makes predictions.</span></span> <span data-ttu-id="c9621-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span><span class="sxs-lookup"><span data-stu-id="c9621-129">The output of prediction could have various forms, such as a .csv file or rows in an Azure SQL database, depending on the configuration of the experiment.</span></span> <span data-ttu-id="c9621-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-130">The default endpoint is automatically created for you when you publish the predictive experiment as a web service.</span></span> 

<span data-ttu-id="c9621-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="c9621-131">The following picture depicts the relationship between training and scoring endpoints in Azure ML.</span></span>

![Web services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/web-services.png)

<span data-ttu-id="c9621-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span><span class="sxs-lookup"><span data-stu-id="c9621-133">You can invoke the **training web service** by using the **Azure ML Batch Execution Activity**.</span></span> <span data-ttu-id="c9621-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span><span class="sxs-lookup"><span data-stu-id="c9621-134">Invoking a training web service is same as invoking an Azure ML web service (scoring web service) for scoring data.</span></span> <span data-ttu-id="c9621-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span><span class="sxs-lookup"><span data-stu-id="c9621-135">The preceding sections cover how to invoke an Azure ML web service from an Azure Data Factory pipeline in detail.</span></span> 

<span data-ttu-id="c9621-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="c9621-136">You can invoke the **scoring web service** by using the **Azure ML Update Resource Activity** to update the web service with the newly trained model.</span></span> <span data-ttu-id="c9621-137">The following examples provide linked service definitions:</span><span class="sxs-lookup"><span data-stu-id="c9621-137">The following examples provide linked service definitions:</span></span> 

## <a name="scoring-web-service-is-a-classic-web-service"></a><span data-ttu-id="c9621-138">Scoring web service is a classic web service</span><span class="sxs-lookup"><span data-stu-id="c9621-138">Scoring web service is a classic web service</span></span>
<span data-ttu-id="c9621-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c9621-139">If the scoring web service is a **classic web service**, create the second **non-default and updatable endpoint** by using the [Azure portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="c9621-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span><span class="sxs-lookup"><span data-stu-id="c9621-140">See [Create Endpoints](../machine-learning/machine-learning-create-endpoint.md) article for steps.</span></span> <span data-ttu-id="c9621-141">After you create the non-default updatable endpoint, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="c9621-141">After you create the non-default updatable endpoint, do the following steps:</span></span>

* <span data-ttu-id="c9621-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span><span class="sxs-lookup"><span data-stu-id="c9621-142">Click **BATCH EXECUTION** to get the URI value for the **mlEndpoint** JSON property.</span></span>
* <span data-ttu-id="c9621-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span><span class="sxs-lookup"><span data-stu-id="c9621-143">Click **UPDATE RESOURCE** link to get the URI value for the **updateResourceEndpoint** JSON property.</span></span> <span data-ttu-id="c9621-144">The API key is on the endpoint page itself (in the bottom-right corner).</span><span class="sxs-lookup"><span data-stu-id="c9621-144">The API key is on the endpoint page itself (in the bottom-right corner).</span></span>

![updatable endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/updatable-endpoint.png)

<span data-ttu-id="c9621-146">The following example provides a sample JSON definition for the AzureML linked service.</span><span class="sxs-lookup"><span data-stu-id="c9621-146">The following example provides a sample JSON definition for the AzureML linked service.</span></span> <span data-ttu-id="c9621-147">The linked service uses the apiKey for authentication.</span><span class="sxs-lookup"><span data-stu-id="c9621-147">The linked service uses the apiKey for authentication.</span></span>  

```json
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--scoring experiment--/jobs",
            "apiKey": "endpoint2Key",
            "updateResourceEndpoint": "https://management.azureml.net/workspaces/xxx/webservices/--scoring experiment--/endpoints/endpoint2"
        }
    }
}
```

## <a name="scoring-web-service-is-azure-resource-manager-web-service"></a><span data-ttu-id="c9621-148">Scoring web service is Azure Resource Manager web service</span><span class="sxs-lookup"><span data-stu-id="c9621-148">Scoring web service is Azure Resource Manager web service</span></span> 
<span data-ttu-id="c9621-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span><span class="sxs-lookup"><span data-stu-id="c9621-149">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="c9621-150">The **updateResourceEndpoint** in the linked service is of the format:</span><span class="sxs-lookup"><span data-stu-id="c9621-150">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="c9621-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="c9621-151">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> <span data-ttu-id="c9621-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span><span class="sxs-lookup"><span data-stu-id="c9621-152">The new type of update resource endpoint requires an AAD (Azure Active Directory) token.</span></span> <span data-ttu-id="c9621-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span><span class="sxs-lookup"><span data-stu-id="c9621-153">Specify **servicePrincipalId** and **servicePrincipalKey**in AzureML linked service.</span></span> <span data-ttu-id="c9621-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c9621-154">See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="c9621-155">Here is a sample AzureML linked service definition:</span><span class="sxs-lookup"><span data-stu-id="c9621-155">Here is a sample AzureML linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": "xxxxxxxxxxxx",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myRG/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": "xxxxx",
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="c9621-156">The following scenario provides more details.</span><span class="sxs-lookup"><span data-stu-id="c9621-156">The following scenario provides more details.</span></span> <span data-ttu-id="c9621-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="c9621-157">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>

## <a name="scenario-retraining-and-updating-an-azure-ml-model"></a><span data-ttu-id="c9621-158">Scenario: retraining and updating an Azure ML model</span><span class="sxs-lookup"><span data-stu-id="c9621-158">Scenario: retraining and updating an Azure ML model</span></span>
<span data-ttu-id="c9621-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span><span class="sxs-lookup"><span data-stu-id="c9621-159">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="c9621-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-160">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="c9621-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span><span class="sxs-lookup"><span data-stu-id="c9621-161">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

<span data-ttu-id="c9621-162">Here is the diagram view of the sample pipeline.</span><span class="sxs-lookup"><span data-stu-id="c9621-162">Here is the diagram view of the sample pipeline.</span></span> <span data-ttu-id="c9621-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span><span class="sxs-lookup"><span data-stu-id="c9621-163">As you can see, the Azure ML Batch Execution Activity takes the training input and produces a training output (iLearner file).</span></span> <span data-ttu-id="c9621-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span><span class="sxs-lookup"><span data-stu-id="c9621-164">The Azure ML Update Resource Activity takes this training output and updates the model in the scoring web service endpoint.</span></span> <span data-ttu-id="c9621-165">The Update Resource Activity does not produce any output.</span><span class="sxs-lookup"><span data-stu-id="c9621-165">The Update Resource Activity does not produce any output.</span></span> <span data-ttu-id="c9621-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c9621-166">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![pipeline diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="c9621-168">Azure Blob storage linked service:</span><span class="sxs-lookup"><span data-stu-id="c9621-168">Azure Blob storage linked service:</span></span>
<span data-ttu-id="c9621-169">The Azure Storage holds the following data:</span><span class="sxs-lookup"><span data-stu-id="c9621-169">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="c9621-170">training data.</span><span class="sxs-lookup"><span data-stu-id="c9621-170">training data.</span></span> <span data-ttu-id="c9621-171">The input data for the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-171">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="c9621-172">iLearner file.</span><span class="sxs-lookup"><span data-stu-id="c9621-172">iLearner file.</span></span> <span data-ttu-id="c9621-173">The output from the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-173">The output from the Azure ML training web service.</span></span> <span data-ttu-id="c9621-174">This file is also the input to the Update Resource activity.</span><span class="sxs-lookup"><span data-stu-id="c9621-174">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="c9621-175">Here is the sample JSON definition of the linked service:</span><span class="sxs-lookup"><span data-stu-id="c9621-175">Here is the sample JSON definition of the linked service:</span></span>

```JSON
{
    "name": "StorageLinkedService",
      "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=name;AccountKey=key"
        }
    }
}
```

### <a name="training-input-dataset"></a><span data-ttu-id="c9621-176">Training input dataset:</span><span class="sxs-lookup"><span data-stu-id="c9621-176">Training input dataset:</span></span>
<span data-ttu-id="c9621-177">The following dataset represents the input training data for the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-177">The following dataset represents the input training data for the Azure ML training web service.</span></span> <span data-ttu-id="c9621-178">The Azure ML Batch Execution activity takes this dataset as an input.</span><span class="sxs-lookup"><span data-stu-id="c9621-178">The Azure ML Batch Execution activity takes this dataset as an input.</span></span>

```JSON
{
    "name": "trainingData",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "labeledexamples",
            "fileName": "labeledexamples.arff",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
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

### <a name="training-output-dataset"></a><span data-ttu-id="c9621-179">Training output dataset:</span><span class="sxs-lookup"><span data-stu-id="c9621-179">Training output dataset:</span></span>
<span data-ttu-id="c9621-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-180">The following dataset represents the output iLearner file from the Azure ML training web service.</span></span> <span data-ttu-id="c9621-181">The Azure ML Batch Execution Activity produces this dataset.</span><span class="sxs-lookup"><span data-stu-id="c9621-181">The Azure ML Batch Execution Activity produces this dataset.</span></span> <span data-ttu-id="c9621-182">This dataset is also the input to the Azure ML Update Resource activity.</span><span class="sxs-lookup"><span data-stu-id="c9621-182">This dataset is also the input to the Azure ML Update Resource activity.</span></span>

```JSON
{
    "name": "trainedModelBlob",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "trainingoutput",
            "fileName": "model.ilearner",
            "format": {
                "type": "TextFormat"
            }
        },
        "availability": {
            "frequency": "Week",
            "interval": 1
        }
    }
}
```

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="c9621-183">Linked service for Azure ML training endpoint</span><span class="sxs-lookup"><span data-stu-id="c9621-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="c9621-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

```JSON
{    
    "name": "trainingEndpoint",
      "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/xxx/services/--training experiment--/jobs",
              "apiKey": "myKey"
        }
      }
}
```

<span data-ttu-id="c9621-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="c9621-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="c9621-186">Click **WEB SERVICES** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="c9621-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="c9621-187">Click the **training web service** in the list of web services.</span><span class="sxs-lookup"><span data-stu-id="c9621-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="c9621-188">Click copy next to **API key** text box.</span><span class="sxs-lookup"><span data-stu-id="c9621-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="c9621-189">Paste the key in the clipboard into the Data Factory JSON editor.</span><span class="sxs-lookup"><span data-stu-id="c9621-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="c9621-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span><span class="sxs-lookup"><span data-stu-id="c9621-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="c9621-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span><span class="sxs-lookup"><span data-stu-id="c9621-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="c9621-192">Linked Service for Azure ML updatable scoring endpoint:</span><span class="sxs-lookup"><span data-stu-id="c9621-192">Linked Service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="c9621-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="c9621-193">The following JSON snippet defines an Azure Machine Learning linked service that points to the non-default updatable endpoint of the scoring web service.</span></span>  

```JSON
{
    "name": "updatableScoringEndpoint2",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/00000000eb0abe4d6bbb1d7886062747d7/services/00000000026734a5889e02fbb1f65cefd/jobs?api-version=2.0",
            "apiKey": "sooooooooooh3WvG1hBfKS2BNNcfwSO7hhY6dY98noLfOdqQydYDIXyf2KoIaN3JpALu/AKtflHWMOCuicm/Q==",
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Default-MachineLearning-SouthCentralUS/providers/Microsoft.MachineLearning/webServices/myWebService?api-version=2016-05-01-preview",
            "servicePrincipalId": "fe200044-c008-4008-a005-94000000731",
            "servicePrincipalKey": "zWa0000000000Tp6FjtZOspK/WMA2tQ08c8U+gZRBlw=",
            "tenant": "mycompany.com"
        }
    }
}
```

### <a name="placeholder-output-dataset"></a><span data-ttu-id="c9621-194">Placeholder output dataset:</span><span class="sxs-lookup"><span data-stu-id="c9621-194">Placeholder output dataset:</span></span>
<span data-ttu-id="c9621-195">The Azure ML Update Resource activity does not generate any output.</span><span class="sxs-lookup"><span data-stu-id="c9621-195">The Azure ML Update Resource activity does not generate any output.</span></span> <span data-ttu-id="c9621-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span><span class="sxs-lookup"><span data-stu-id="c9621-196">However, Azure Data Factory requires an output dataset to drive the schedule of a pipeline.</span></span> <span data-ttu-id="c9621-197">Therefore, we use a dummy/placeholder dataset in this example.</span><span class="sxs-lookup"><span data-stu-id="c9621-197">Therefore, we use a dummy/placeholder dataset in this example.</span></span>  

```JSON
{
    "name": "placeholderBlob",
    "properties": {
        "availability": {
            "frequency": "Week",
            "interval": 1
        },
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "any",
            "format": {
                "type": "TextFormat"
            }
        }
    }
}
```

### <a name="pipeline"></a><span data-ttu-id="c9621-198">Pipeline</span><span class="sxs-lookup"><span data-stu-id="c9621-198">Pipeline</span></span>
<span data-ttu-id="c9621-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="c9621-199">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="c9621-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span><span class="sxs-lookup"><span data-stu-id="c9621-200">The Azure ML Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="c9621-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span><span class="sxs-lookup"><span data-stu-id="c9621-201">The activity invokes the training web service (training experiment exposed as a web service) with the input training data and receives the ilearner file from the webservice.</span></span> <span data-ttu-id="c9621-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c9621-202">The placeholderBlob is just a dummy output dataset that is required by the Azure Data Factory service to run the pipeline.</span></span>

![pipeline diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-azure-ml-batch-execution-activity/update-activity-pipeline-diagram.png)

```JSON
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "Training Exp for ADF ML [trained model]",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "outputs": [
                    {
                        "name": "placeholderBlob"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00Z",
           "end": "2016-02-14T00:00:00Z"
    }
}
```



