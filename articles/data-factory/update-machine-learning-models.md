---
title: Update machine learning models using Azure Data Factory | Microsoft Docs
description: Describes how to create create predictive pipelines using Azure Data Factory and machine learning
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: shlo
ms.openlocfilehash: 4eed11b312bce27dc0cd98daa3e2599a28fcabbd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967568"
---
# <a name="update-azure-machine-learning-models-by-using-update-resource-activity"></a><span data-ttu-id="a0695-103">Update Azure Machine Learning models by using Update Resource activity</span><span class="sxs-lookup"><span data-stu-id="a0695-103">Update Azure Machine Learning models by using Update Resource activity</span></span>
<span data-ttu-id="a0695-104">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](transform-data-using-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-104">This article complements the main Azure Data Factory - Azure Machine Learning integration article: [Create predictive pipelines using Azure Machine Learning and Azure Data Factory](transform-data-using-machine-learning.md).</span></span> <span data-ttu-id="a0695-105">If you haven't already done so, review the main article before reading through this article.</span><span class="sxs-lookup"><span data-stu-id="a0695-105">If you haven't already done so, review the main article before reading through this article.</span></span> 

## <a name="overview"></a><span data-ttu-id="a0695-106">Overview</span><span class="sxs-lookup"><span data-stu-id="a0695-106">Overview</span></span>
<span data-ttu-id="a0695-107">As part of the process of operationalizing Azure Machine Learning models, your model is trained and saved.</span><span class="sxs-lookup"><span data-stu-id="a0695-107">As part of the process of operationalizing Azure Machine Learning models, your model is trained and saved.</span></span> <span data-ttu-id="a0695-108">You then use it to create a predictive Web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-108">You then use it to create a predictive Web service.</span></span> <span data-ttu-id="a0695-109">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span><span class="sxs-lookup"><span data-stu-id="a0695-109">The Web service can then be consumed in web sites, dashboards, and mobile apps.</span></span>

<span data-ttu-id="a0695-110">Models you create using Machine Learning are typically not static.</span><span class="sxs-lookup"><span data-stu-id="a0695-110">Models you create using Machine Learning are typically not static.</span></span> <span data-ttu-id="a0695-111">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span><span class="sxs-lookup"><span data-stu-id="a0695-111">As new data becomes available or when the consumer of the API has their own data the model needs to be retrained.</span></span> <span data-ttu-id="a0695-112">Refer to [Retrain a Machine Learning Model](../machine-learning/machine-learning-retrain-machine-learning-model.md) for details about how you can retrain a model in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a0695-112">Refer to [Retrain a Machine Learning Model](../machine-learning/machine-learning-retrain-machine-learning-model.md) for details about how you can retrain a model in Azure Machine Learning.</span></span> 

<span data-ttu-id="a0695-113">Retraining may occur frequently.</span><span class="sxs-lookup"><span data-stu-id="a0695-113">Retraining may occur frequently.</span></span> <span data-ttu-id="a0695-114">With Batch Execution activity and Update Resource activity, you can operationalize the Azure Machine Learning model retraining and updating the predictive Web Service using Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0695-114">With Batch Execution activity and Update Resource activity, you can operationalize the Azure Machine Learning model retraining and updating the predictive Web Service using Data Factory.</span></span> 

<span data-ttu-id="a0695-115">The following picture depicts the relationship between training and predictive Web Services.</span><span class="sxs-lookup"><span data-stu-id="a0695-115">The following picture depicts the relationship between training and predictive Web Services.</span></span> 

![Web services](./media/update-machine-learning-models/web-services.png)

## <a name="azure-machine-learning-update-resource-activity"></a><span data-ttu-id="a0695-117">Azure Machine Learning update resource activity</span><span class="sxs-lookup"><span data-stu-id="a0695-117">Azure Machine Learning update resource activity</span></span> 

<span data-ttu-id="a0695-118">The following JSON snippet defines an Azure Machine Learning Batch Execution activity.</span><span class="sxs-lookup"><span data-stu-id="a0695-118">The following JSON snippet defines an Azure Machine Learning Batch Execution activity.</span></span>

```json
{
    "name": "amlUpdateResource",
    "type": "AzureMLUpdateResource",
    "description": "description",
    "linkedServiceName": {
        "type": "LinkedServiceReference",
        "referenceName": "updatableScoringEndpoint2"
    },
    "typeProperties": {
        "trainedModelName": "ModelName",
        "trainedModelLinkedServiceName": {
                    "type": "LinkedServiceReference",
                    "referenceName": "StorageLinkedService"
                },
        "trainedModelFilePath": "ilearner file path"
    }
}
```




| <span data-ttu-id="a0695-119">Property</span><span class="sxs-lookup"><span data-stu-id="a0695-119">Property</span></span>                      | <span data-ttu-id="a0695-120">Description</span><span class="sxs-lookup"><span data-stu-id="a0695-120">Description</span></span>                              | <span data-ttu-id="a0695-121">Required</span><span class="sxs-lookup"><span data-stu-id="a0695-121">Required</span></span> |
| :---------------------------- | :--------------------------------------- | :------- |
| <span data-ttu-id="a0695-122">name</span><span class="sxs-lookup"><span data-stu-id="a0695-122">name</span></span>                          | <span data-ttu-id="a0695-123">Name of the activity in the pipeline</span><span class="sxs-lookup"><span data-stu-id="a0695-123">Name of the activity in the pipeline</span></span>     | <span data-ttu-id="a0695-124">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-124">Yes</span></span>      |
| <span data-ttu-id="a0695-125">description</span><span class="sxs-lookup"><span data-stu-id="a0695-125">description</span></span>                   | <span data-ttu-id="a0695-126">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="a0695-126">Text describing what the activity does.</span></span>  | <span data-ttu-id="a0695-127">No</span><span class="sxs-lookup"><span data-stu-id="a0695-127">No</span></span>       |
| <span data-ttu-id="a0695-128">type</span><span class="sxs-lookup"><span data-stu-id="a0695-128">type</span></span>                          | <span data-ttu-id="a0695-129">For Azure Machine Learning Update Resource activity, the activity type is  **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="a0695-129">For Azure Machine Learning Update Resource activity, the activity type is  **AzureMLUpdateResource**.</span></span> | <span data-ttu-id="a0695-130">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-130">Yes</span></span>      |
| <span data-ttu-id="a0695-131">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="a0695-131">linkedServiceName</span></span>             | <span data-ttu-id="a0695-132">Azure Machine Learning linked service that contains updateResourceEndpoint property.</span><span class="sxs-lookup"><span data-stu-id="a0695-132">Azure Machine Learning linked service that contains updateResourceEndpoint property.</span></span> | <span data-ttu-id="a0695-133">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-133">Yes</span></span>      |
| <span data-ttu-id="a0695-134">trainedModelName</span><span class="sxs-lookup"><span data-stu-id="a0695-134">trainedModelName</span></span>              | <span data-ttu-id="a0695-135">Name of the Trained Model module in the Web Service experiment to be updated</span><span class="sxs-lookup"><span data-stu-id="a0695-135">Name of the Trained Model module in the Web Service experiment to be updated</span></span> | <span data-ttu-id="a0695-136">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-136">Yes</span></span>      |
| <span data-ttu-id="a0695-137">trainedModelLinkedServiceName</span><span class="sxs-lookup"><span data-stu-id="a0695-137">trainedModelLinkedServiceName</span></span> | <span data-ttu-id="a0695-138">Name of Azure Storage linked service holding the ilearner file that is uploaded by the update operation</span><span class="sxs-lookup"><span data-stu-id="a0695-138">Name of Azure Storage linked service holding the ilearner file that is uploaded by the update operation</span></span> | <span data-ttu-id="a0695-139">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-139">Yes</span></span>      |
| <span data-ttu-id="a0695-140">trainedModelFilePath</span><span class="sxs-lookup"><span data-stu-id="a0695-140">trainedModelFilePath</span></span>          | <span data-ttu-id="a0695-141">The relative file path in trainedModelLinkedService to represent the ilearner file that is uploaded by the update operation</span><span class="sxs-lookup"><span data-stu-id="a0695-141">The relative file path in trainedModelLinkedService to represent the ilearner file that is uploaded by the update operation</span></span> | <span data-ttu-id="a0695-142">Yes</span><span class="sxs-lookup"><span data-stu-id="a0695-142">Yes</span></span>      |


## <a name="end-to-end-workflow"></a><span data-ttu-id="a0695-143">End-to-end workflow</span><span class="sxs-lookup"><span data-stu-id="a0695-143">End-to-end workflow</span></span>

<span data-ttu-id="a0695-144">The entire process of operationalizing retraining a model and update the predictive Web Services involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="a0695-144">The entire process of operationalizing retraining a model and update the predictive Web Services involves the following steps:</span></span> 

- <span data-ttu-id="a0695-145">Invoke the **training Web Service** by using the **Batch Execution activity**.</span><span class="sxs-lookup"><span data-stu-id="a0695-145">Invoke the **training Web Service** by using the **Batch Execution activity**.</span></span> <span data-ttu-id="a0695-146">Invoking a training Web Service is the same as invoking a predictive Web Service described in [Create predictive pipelines using Azure Machine Learning and Data Factory Batch Execution activity](transform-data-using-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-146">Invoking a training Web Service is the same as invoking a predictive Web Service described in [Create predictive pipelines using Azure Machine Learning and Data Factory Batch Execution activity](transform-data-using-machine-learning.md).</span></span> <span data-ttu-id="a0695-147">The output of the training Web Service is a iLearner file that you can use to update the predictive Web Service.</span><span class="sxs-lookup"><span data-stu-id="a0695-147">The output of the training Web Service is a iLearner file that you can use to update the predictive Web Service.</span></span> 
- <span data-ttu-id="a0695-148">Invoke the **update resource endpoint** of the **predictive Web Service** by using the **Update Resource activity** to update the Web Service with the newly trained model.</span><span class="sxs-lookup"><span data-stu-id="a0695-148">Invoke the **update resource endpoint** of the **predictive Web Service** by using the **Update Resource activity** to update the Web Service with the newly trained model.</span></span> 

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="a0695-149">Azure Machine Learning linked service</span><span class="sxs-lookup"><span data-stu-id="a0695-149">Azure Machine Learning linked service</span></span>

<span data-ttu-id="a0695-150">For the above mentioned end-to-end workflow to work, you need to create two Azure Machine Learning linked services:</span><span class="sxs-lookup"><span data-stu-id="a0695-150">For the above mentioned end-to-end workflow to work, you need to create two Azure Machine Learning linked services:</span></span> 

1. <span data-ttu-id="a0695-151">An Azure Machine Learning linked service to the training web service, this linked service is used by Batch Execution activity in the same way as what's mentioned in [Create predictive pipelines using Azure Machine Learning and Data Factory Batch Execution activity](transform-data-using-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-151">An Azure Machine Learning linked service to the training web service, this linked service is used by Batch Execution activity in the same way as what's mentioned in [Create predictive pipelines using Azure Machine Learning and Data Factory Batch Execution activity](transform-data-using-machine-learning.md).</span></span> <span data-ttu-id="a0695-152">Difference is the output of the training web service is an iLearner file which is then used by Update Resource activity to update the predictive web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-152">Difference is the output of the training web service is an iLearner file which is then used by Update Resource activity to update the predictive web service.</span></span> 
2. <span data-ttu-id="a0695-153">An Azure Machine Learning linked service to the update resource endpoint of the predictive web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-153">An Azure Machine Learning linked service to the update resource endpoint of the predictive web service.</span></span> <span data-ttu-id="a0695-154">This linked service is used by Update Resource activity to update the predictive web service using the iLearner file returned from above step.</span><span class="sxs-lookup"><span data-stu-id="a0695-154">This linked service is used by Update Resource activity to update the predictive web service using the iLearner file returned from above step.</span></span> 

<span data-ttu-id="a0695-155">For the second Azure Machine Learning linked service, the configuration is different when your Azure Machine Learning Web Service is a classic Web Service or a new Web Service.</span><span class="sxs-lookup"><span data-stu-id="a0695-155">For the second Azure Machine Learning linked service, the configuration is different when your Azure Machine Learning Web Service is a classic Web Service or a new Web Service.</span></span> <span data-ttu-id="a0695-156">The differences are discussed separately in the following sections.</span><span class="sxs-lookup"><span data-stu-id="a0695-156">The differences are discussed separately in the following sections.</span></span> 

## <a name="web-service-is-new-azure-resource-manager-web-service"></a><span data-ttu-id="a0695-157">Web service is new Azure Resource Manager web service</span><span class="sxs-lookup"><span data-stu-id="a0695-157">Web service is new Azure Resource Manager web service</span></span> 

<span data-ttu-id="a0695-158">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span><span class="sxs-lookup"><span data-stu-id="a0695-158">If the web service is the new type of web service that exposes an Azure Resource Manager endpoint, you do not need to add the second **non-default** endpoint.</span></span> <span data-ttu-id="a0695-159">The **updateResourceEndpoint** in the linked service is of the format:</span><span class="sxs-lookup"><span data-stu-id="a0695-159">The **updateResourceEndpoint** in the linked service is of the format:</span></span> 

```
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. 
```

<span data-ttu-id="a0695-160">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="a0695-160">You can get values for place holders in the URL when querying the web service on the [Azure Machine Learning Web Services Portal](https://services.azureml.net/).</span></span> 

<span data-ttu-id="a0695-161">The new type of update resource endpoint requires service principal authentication.</span><span class="sxs-lookup"><span data-stu-id="a0695-161">The new type of update resource endpoint requires service principal authentication.</span></span> <span data-ttu-id="a0695-162">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the **Contributor** or **Owner** role of the subscription or the resource group where the web service belongs to.</span><span class="sxs-lookup"><span data-stu-id="a0695-162">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the **Contributor** or **Owner** role of the subscription or the resource group where the web service belongs to.</span></span> <span data-ttu-id="a0695-163">The See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a0695-163">The See [how to create service principal and assign permissions to manage Azure resource](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="a0695-164">Make note of the following values, which you use to define the linked service:</span><span class="sxs-lookup"><span data-stu-id="a0695-164">Make note of the following values, which you use to define the linked service:</span></span>

- <span data-ttu-id="a0695-165">Application ID</span><span class="sxs-lookup"><span data-stu-id="a0695-165">Application ID</span></span>
- <span data-ttu-id="a0695-166">Application key</span><span class="sxs-lookup"><span data-stu-id="a0695-166">Application key</span></span> 
- <span data-ttu-id="a0695-167">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="a0695-167">Tenant ID</span></span>

<span data-ttu-id="a0695-168">Here is a sample linked service definition:</span><span class="sxs-lookup"><span data-stu-id="a0695-168">Here is a sample linked service definition:</span></span> 

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "description": "The linked service for AML web service.",
        "typeProperties": {
            "mlEndpoint": "https://ussouthcentral.services.azureml.net/workspaces/0000000000000000  000000000000000000000/services/0000000000000000000000000000000000000/jobs?api-version=2.0",
            "apiKey": {
            "type": "SecureString",
            "value": "APIKeyOfEndpoint1"
            },
            "updateResourceEndpoint": "https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resource-group-name}/providers/Microsoft.MachineLearning/webServices/{web-service-name}?api-version=2016-05-01-preview. ",
            "servicePrincipalId": "000000000-0000-0000-0000-0000000000000",
            "servicePrincipalKey": {
            "type": "SecureString",
            "value": "servicePrincipalKey"
            },
            "tenant": "mycompany.com"
        }
    }
}
```

<span data-ttu-id="a0695-169">The following scenario provides more details.</span><span class="sxs-lookup"><span data-stu-id="a0695-169">The following scenario provides more details.</span></span> <span data-ttu-id="a0695-170">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="a0695-170">It has an example for retraining and updating Azure ML models from an Azure Data Factory pipeline.</span></span>


## <a name="sample-retraining-and-updating-an-azure-machine-learning-model"></a><span data-ttu-id="a0695-171">Sample: Retraining and updating an Azure Machine Learning model</span><span class="sxs-lookup"><span data-stu-id="a0695-171">Sample: Retraining and updating an Azure Machine Learning model</span></span>

<span data-ttu-id="a0695-172">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span><span class="sxs-lookup"><span data-stu-id="a0695-172">This section provides a sample pipeline that uses the **Azure ML Batch Execution activity** to retrain a model.</span></span> <span data-ttu-id="a0695-173">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-173">The pipeline also uses the **Azure ML Update Resource activity** to update the model in the scoring web service.</span></span> <span data-ttu-id="a0695-174">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span><span class="sxs-lookup"><span data-stu-id="a0695-174">The section also provides JSON snippets for all the linked services, datasets, and pipeline in the example.</span></span>

### <a name="azure-blob-storage-linked-service"></a><span data-ttu-id="a0695-175">Azure Blob storage linked service:</span><span class="sxs-lookup"><span data-stu-id="a0695-175">Azure Blob storage linked service:</span></span>
<span data-ttu-id="a0695-176">The Azure Storage holds the following data:</span><span class="sxs-lookup"><span data-stu-id="a0695-176">The Azure Storage holds the following data:</span></span>

* <span data-ttu-id="a0695-177">training data.</span><span class="sxs-lookup"><span data-stu-id="a0695-177">training data.</span></span> <span data-ttu-id="a0695-178">The input data for the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-178">The input data for the Azure ML training web service.</span></span>  
* <span data-ttu-id="a0695-179">iLearner file.</span><span class="sxs-lookup"><span data-stu-id="a0695-179">iLearner file.</span></span> <span data-ttu-id="a0695-180">The output from the Azure ML training web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-180">The output from the Azure ML training web service.</span></span> <span data-ttu-id="a0695-181">This file is also the input to the Update Resource activity.</span><span class="sxs-lookup"><span data-stu-id="a0695-181">This file is also the input to the Update Resource activity.</span></span>  

<span data-ttu-id="a0695-182">Here is the sample JSON definition of the linked service:</span><span class="sxs-lookup"><span data-stu-id="a0695-182">Here is the sample JSON definition of the linked service:</span></span>

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

### <a name="linked-service-for-azure-ml-training-endpoint"></a><span data-ttu-id="a0695-183">Linked service for Azure ML training endpoint</span><span class="sxs-lookup"><span data-stu-id="a0695-183">Linked service for Azure ML training endpoint</span></span>
<span data-ttu-id="a0695-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-184">The following JSON snippet defines an Azure Machine Learning linked service that points to the default endpoint of the training web service.</span></span>

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

<span data-ttu-id="a0695-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span><span class="sxs-lookup"><span data-stu-id="a0695-185">In **Azure ML Studio**, do the following to get values for **mlEndpoint** and **apiKey**:</span></span>

1. <span data-ttu-id="a0695-186">Click **WEB SERVICES** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="a0695-186">Click **WEB SERVICES** on the left menu.</span></span>
2. <span data-ttu-id="a0695-187">Click the **training web service** in the list of web services.</span><span class="sxs-lookup"><span data-stu-id="a0695-187">Click the **training web service** in the list of web services.</span></span>
3. <span data-ttu-id="a0695-188">Click copy next to **API key** text box.</span><span class="sxs-lookup"><span data-stu-id="a0695-188">Click copy next to **API key** text box.</span></span> <span data-ttu-id="a0695-189">Paste the key in the clipboard into the Data Factory JSON editor.</span><span class="sxs-lookup"><span data-stu-id="a0695-189">Paste the key in the clipboard into the Data Factory JSON editor.</span></span>
4. <span data-ttu-id="a0695-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span><span class="sxs-lookup"><span data-stu-id="a0695-190">In the **Azure ML studio**, click **BATCH EXECUTION** link.</span></span>
5. <span data-ttu-id="a0695-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span><span class="sxs-lookup"><span data-stu-id="a0695-191">Copy the **Request URI** from the **Request** section and paste it into the Data Factory JSON editor.</span></span>   

### <a name="linked-service-for-azure-ml-updatable-scoring-endpoint"></a><span data-ttu-id="a0695-192">Linked service for Azure ML updatable scoring endpoint:</span><span class="sxs-lookup"><span data-stu-id="a0695-192">Linked service for Azure ML updatable scoring endpoint:</span></span>
<span data-ttu-id="a0695-193">The following JSON snippet defines an Azure Machine Learning linked service that points to updatable endpoint of the scoring web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-193">The following JSON snippet defines an Azure Machine Learning linked service that points to updatable endpoint of the scoring web service.</span></span>  

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

### <a name="pipeline"></a><span data-ttu-id="a0695-194">Pipeline</span><span class="sxs-lookup"><span data-stu-id="a0695-194">Pipeline</span></span>
<span data-ttu-id="a0695-195">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span><span class="sxs-lookup"><span data-stu-id="a0695-195">The pipeline has two activities: **AzureMLBatchExecution** and **AzureMLUpdateResource**.</span></span> <span data-ttu-id="a0695-196">The Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span><span class="sxs-lookup"><span data-stu-id="a0695-196">The Batch Execution activity takes the training data as input and produces an iLearner file as an output.</span></span> <span data-ttu-id="a0695-197">The Update Resource activity then takes this iLearner file and use it to update the predictive web service.</span><span class="sxs-lookup"><span data-stu-id="a0695-197">The Update Resource activity then takes this iLearner file and use it to update the predictive web service.</span></span> 

```JSON
{
    "name": "LookupPipelineDemo",
    "properties": {
        "activities": [
            {
                "name": "amlBEGetilearner",
                "description": "Use AML BES to get the ileaner file from training web service",
                "type": "AzureMLBatchExecution",
                "linkedServiceName": {
                    "referenceName": "trainingEndpoint",
                    "type": "LinkedServiceReference"
                },
                "typeProperties": {
                    "webServiceInputs": {
                        "input1": {
                            "LinkedServiceName":{
                                "referenceName": "StorageLinkedService",
                                "type": "LinkedServiceReference"
                            }, 
                            "FilePath":"azuremltesting/input"
                        }, 
                        "input2": {
                            "LinkedServiceName":{
                                "referenceName": "StorageLinkedService",
                                "type": "LinkedServiceReference" 
                            }, 
                            "FilePath":"azuremltesting/input"
                        }        
                    },
                    "webServiceOutputs": {
                        "output1": {
                            "LinkedServiceName":{
                                "referenceName": "StorageLinkedService",
                                "type": "LinkedServiceReference"   
                            }, 
                            "FilePath":"azuremltesting/output"
                        }        
                    }
                }
            },
            {
                "name": "amlUpdateResource",
                "type": "AzureMLUpdateResource",
                "description": "Use AML Update Resource to update the predict web service",
                "linkedServiceName": {
                    "type": "LinkedServiceReference",
                    "referenceName": "updatableScoringEndpoint2"
                },
                "typeProperties": {
                    "trainedModelName": "ADFV2Sample Model [trained model]",
                    "trainedModelLinkedServiceName": {
                                "type": "LinkedServiceReference",
                                "referenceName": "StorageLinkedService"
                            },
                    "trainedModelFilePath": "azuremltesting/output/newModelForArm.ilearner"
                },
                "dependsOn": [ 
                    { 
                        "activity": "amlbeGetilearner", 
                        "dependencyConditions": [ "Succeeded" ] 
                    }
                 ]

            }
        ]
    }
}
```
## <a name="next-steps"></a><span data-ttu-id="a0695-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="a0695-198">Next steps</span></span>
<span data-ttu-id="a0695-199">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="a0695-199">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="a0695-200">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="a0695-200">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="a0695-201">Hive activity</span><span class="sxs-lookup"><span data-stu-id="a0695-201">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="a0695-202">Pig activity</span><span class="sxs-lookup"><span data-stu-id="a0695-202">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="a0695-203">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="a0695-203">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="a0695-204">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="a0695-204">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="a0695-205">Spark activity</span><span class="sxs-lookup"><span data-stu-id="a0695-205">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="a0695-206">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="a0695-206">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="a0695-207">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="a0695-207">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
