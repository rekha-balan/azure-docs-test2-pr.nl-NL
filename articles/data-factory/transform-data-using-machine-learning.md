---
title: Create predictive data pipelines using Azure Data Factory | Microsoft Docs
description: Learn how to create a predictive pipeline by using Azure Machine Learning - Batch Execution Activity in Azure Data Factory.
services: data-factory
documentationcenter: ''
author: douglaslMS
manager: craigg
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: douglasl
ms.openlocfilehash: 87a71cff07d18dde25fa5c58b3718e7a57e3ce8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855738"
---
# <a name="create-predictive-pipelines-using-azure-machine-learning-and-azure-data-factory"></a><span data-ttu-id="d778c-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d778c-103">Create predictive pipelines using Azure Machine Learning and Azure Data Factory</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-azure-ml-batch-execution-activity.md)
> * [Current version](transform-data-using-machine-learning.md)

<span data-ttu-id="d778c-106">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span><span class="sxs-lookup"><span data-stu-id="d778c-106">[Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) enables you to build, test, and deploy predictive analytics solutions.</span></span> <span data-ttu-id="d778c-107">From a high-level point of view, it is done in three steps:</span><span class="sxs-lookup"><span data-stu-id="d778c-107">From a high-level point of view, it is done in three steps:</span></span>

1. <span data-ttu-id="d778c-108">**Create a training experiment**.</span><span class="sxs-lookup"><span data-stu-id="d778c-108">**Create a training experiment**.</span></span> <span data-ttu-id="d778c-109">You do this step by using the Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="d778c-109">You do this step by using the Azure ML Studio.</span></span> <span data-ttu-id="d778c-110">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span><span class="sxs-lookup"><span data-stu-id="d778c-110">The ML studio is a collaborative visual development environment that you use to train and test a predictive analytics model using training data.</span></span>
2. <span data-ttu-id="d778c-111">**Convert it to a predictive experiment**.</span><span class="sxs-lookup"><span data-stu-id="d778c-111">**Convert it to a predictive experiment**.</span></span> <span data-ttu-id="d778c-112">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span><span class="sxs-lookup"><span data-stu-id="d778c-112">Once your model has been trained with existing data and you are ready to use it to score new data, you prepare and streamline your experiment for scoring.</span></span>
3. <span data-ttu-id="d778c-113">**Deploy it as a web service**.</span><span class="sxs-lookup"><span data-stu-id="d778c-113">**Deploy it as a web service**.</span></span> <span data-ttu-id="d778c-114">You can publish your scoring experiment as an Azure web service.</span><span class="sxs-lookup"><span data-stu-id="d778c-114">You can publish your scoring experiment as an Azure web service.</span></span> <span data-ttu-id="d778c-115">You can send data to your model via this web service end point and receive result predictions from the model.</span><span class="sxs-lookup"><span data-stu-id="d778c-115">You can send data to your model via this web service end point and receive result predictions from the model.</span></span>  

### <a name="data-factory-and-machine-learning-together"></a><span data-ttu-id="d778c-116">Data Factory and Machine Learning together</span><span class="sxs-lookup"><span data-stu-id="d778c-116">Data Factory and Machine Learning together</span></span>
<span data-ttu-id="d778c-117">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span><span class="sxs-lookup"><span data-stu-id="d778c-117">Azure Data Factory enables you to easily create pipelines that use a published [Azure Machine Learning][azure-machine-learning] web service for predictive analytics.</span></span> <span data-ttu-id="d778c-118">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span><span class="sxs-lookup"><span data-stu-id="d778c-118">Using the **Batch Execution Activity** in an Azure Data Factory pipeline, you can invoke an Azure ML web service to make predictions on the data in batch.</span></span> 

<span data-ttu-id="d778c-119">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span><span class="sxs-lookup"><span data-stu-id="d778c-119">Over time, the predictive models in the Azure ML scoring experiments need to be retrained using new input datasets.</span></span> <span data-ttu-id="d778c-120">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span><span class="sxs-lookup"><span data-stu-id="d778c-120">You can retrain an Azure ML model from a Data Factory pipeline by doing the following steps:</span></span>

1. <span data-ttu-id="d778c-121">Publish the training experiment (not predictive experiment) as a web service.</span><span class="sxs-lookup"><span data-stu-id="d778c-121">Publish the training experiment (not predictive experiment) as a web service.</span></span> <span data-ttu-id="d778c-122">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span><span class="sxs-lookup"><span data-stu-id="d778c-122">You do this step in the Azure ML Studio as you did to expose predictive experiment as a web service in the previous scenario.</span></span>
2. <span data-ttu-id="d778c-123">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span><span class="sxs-lookup"><span data-stu-id="d778c-123">Use the Azure ML Batch Execution Activity to invoke the web service for the training experiment.</span></span> <span data-ttu-id="d778c-124">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span><span class="sxs-lookup"><span data-stu-id="d778c-124">Basically, you can use the Azure ML Batch Execution activity to invoke both training web service and scoring web service.</span></span>

<span data-ttu-id="d778c-125">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span><span class="sxs-lookup"><span data-stu-id="d778c-125">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="d778c-126">See [Updating models using Update Resource Activity](update-machine-learning-models.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="d778c-126">See [Updating models using Update Resource Activity](update-machine-learning-models.md) article for details.</span></span>

## <a name="azure-machine-learning-linked-service"></a><span data-ttu-id="d778c-127">Azure Machine Learning linked service</span><span class="sxs-lookup"><span data-stu-id="d778c-127">Azure Machine Learning linked service</span></span>

<span data-ttu-id="d778c-128">You create an **Azure Machine Learning** linked service to link an Azure Machine Learning Web Service to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="d778c-128">You create an **Azure Machine Learning** linked service to link an Azure Machine Learning Web Service to an Azure data factory.</span></span> <span data-ttu-id="d778c-129">The Linked Service is used by Azure Machine Learning Batch Execution Activity and  [Update Resource Activity](update-machine-learning-models.md).</span><span class="sxs-lookup"><span data-stu-id="d778c-129">The Linked Service is used by Azure Machine Learning Batch Execution Activity and  [Update Resource Activity](update-machine-learning-models.md).</span></span> 


```JSON
{
    "type" : "linkedServices",
    "name": "AzureMLLinkedService",
    "apiVersion" : "2017-09-01-preview",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "URL to Azure ML Predictive Web Service",
            "apiKey": {
                "type": "SecureString",
                "value": "api key"
            }
        }
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

<span data-ttu-id="d778c-130">See [Compute linked services](compute-linked-services.md) article for descriptions about properties in the JSON definition.</span><span class="sxs-lookup"><span data-stu-id="d778c-130">See [Compute linked services](compute-linked-services.md) article for descriptions about properties in the JSON definition.</span></span> 

<span data-ttu-id="d778c-131">Azure Machine Learning support both Classic Web Services and New Web Services for your predictive experiment.</span><span class="sxs-lookup"><span data-stu-id="d778c-131">Azure Machine Learning support both Classic Web Services and New Web Services for your predictive experiment.</span></span> <span data-ttu-id="d778c-132">You can choose the right one to use from Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d778c-132">You can choose the right one to use from Data Factory.</span></span> <span data-ttu-id="d778c-133">To get the information required to create the Azure Machine Learning Linked Service, go to https://services.azureml.net, where all your (new) Web Services and Classic Web Services are listed.</span><span class="sxs-lookup"><span data-stu-id="d778c-133">To get the information required to create the Azure Machine Learning Linked Service, go to https://services.azureml.net, where all your (new) Web Services and Classic Web Services are listed.</span></span> <span data-ttu-id="d778c-134">Click the Web Service you would like to access, and click **Consume** page.</span><span class="sxs-lookup"><span data-stu-id="d778c-134">Click the Web Service you would like to access, and click **Consume** page.</span></span> <span data-ttu-id="d778c-135">Copy **Primary Key** for **apiKey** property, and **Batch Requests** for **mlEndpoint** property.</span><span class="sxs-lookup"><span data-stu-id="d778c-135">Copy **Primary Key** for **apiKey** property, and **Batch Requests** for **mlEndpoint** property.</span></span> 

![Azure Machine Learning Web Services](./media/transform-data-using-machine-learning/web-services.png)

## <a name="azure-machine-learning-batch-execution-activity"></a><span data-ttu-id="d778c-137">Azure Machine Learning Batch Execution activity</span><span class="sxs-lookup"><span data-stu-id="d778c-137">Azure Machine Learning Batch Execution activity</span></span>

<span data-ttu-id="d778c-138">The following JSON snippet defines an Azure Machine Learning Batch Execution activity.</span><span class="sxs-lookup"><span data-stu-id="d778c-138">The following JSON snippet defines an Azure Machine Learning Batch Execution activity.</span></span> <span data-ttu-id="d778c-139">The activity definition has a reference to the Azure Machine Learning linked service you created earlier.</span><span class="sxs-lookup"><span data-stu-id="d778c-139">The activity definition has a reference to the Azure Machine Learning linked service you created earlier.</span></span> 

```JSON
{
    "name": "AzureMLExecutionActivityTemplate",
    "description": "description",
    "type": "AzureMLBatchExecution",
    "linkedServiceName": {
        "referenceName": "AzureMLLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "webServiceInputs": {
            "<web service input name 1>": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService1",
                    "type": "LinkedServiceReference"
                }, 
                "FilePath":"path1"
            }, 
            "<web service input name 2>": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService1",
                    "type": "LinkedServiceReference" 
                }, 
                "FilePath":"path2"
            }        
        },
        "webServiceOutputs": {
            "<web service output name 1>": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService2",
                    "type": "LinkedServiceReference"   
                }, 
                "FilePath":"path3"
            }, 
            "<web service output name 2>": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService2",
                    "type": "LinkedServiceReference"   
                }, 
                "FilePath":"path4"
            }         
        },
        "globalParameters": {
            "<Parameter 1 Name>": "<parameter value>",
            "<parameter 2 name>": "<parameter 2 value>"
        }
    }
}
```



| <span data-ttu-id="d778c-140">Property</span><span class="sxs-lookup"><span data-stu-id="d778c-140">Property</span></span>          | <span data-ttu-id="d778c-141">Description</span><span class="sxs-lookup"><span data-stu-id="d778c-141">Description</span></span>                              | <span data-ttu-id="d778c-142">Required</span><span class="sxs-lookup"><span data-stu-id="d778c-142">Required</span></span> |
| :---------------- | :--------------------------------------- | :------- |
| <span data-ttu-id="d778c-143">name</span><span class="sxs-lookup"><span data-stu-id="d778c-143">name</span></span>              | <span data-ttu-id="d778c-144">Name of the activity in the pipeline</span><span class="sxs-lookup"><span data-stu-id="d778c-144">Name of the activity in the pipeline</span></span>     | <span data-ttu-id="d778c-145">Yes</span><span class="sxs-lookup"><span data-stu-id="d778c-145">Yes</span></span>      |
| <span data-ttu-id="d778c-146">description</span><span class="sxs-lookup"><span data-stu-id="d778c-146">description</span></span>       | <span data-ttu-id="d778c-147">Text describing what the activity does.</span><span class="sxs-lookup"><span data-stu-id="d778c-147">Text describing what the activity does.</span></span>  | <span data-ttu-id="d778c-148">No</span><span class="sxs-lookup"><span data-stu-id="d778c-148">No</span></span>       |
| <span data-ttu-id="d778c-149">type</span><span class="sxs-lookup"><span data-stu-id="d778c-149">type</span></span>              | <span data-ttu-id="d778c-150">For Data Lake Analytics U-SQL activity, the activity type is  **AzureMLBatchExecution**.</span><span class="sxs-lookup"><span data-stu-id="d778c-150">For Data Lake Analytics U-SQL activity, the activity type is  **AzureMLBatchExecution**.</span></span> | <span data-ttu-id="d778c-151">Yes</span><span class="sxs-lookup"><span data-stu-id="d778c-151">Yes</span></span>      |
| <span data-ttu-id="d778c-152">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="d778c-152">linkedServiceName</span></span> | <span data-ttu-id="d778c-153">Linked Services to the Azure Machine Learning Linked Service.</span><span class="sxs-lookup"><span data-stu-id="d778c-153">Linked Services to the Azure Machine Learning Linked Service.</span></span> <span data-ttu-id="d778c-154">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span><span class="sxs-lookup"><span data-stu-id="d778c-154">To learn about this linked service, see [Compute linked services](compute-linked-services.md) article.</span></span> | <span data-ttu-id="d778c-155">Yes</span><span class="sxs-lookup"><span data-stu-id="d778c-155">Yes</span></span>      |
| <span data-ttu-id="d778c-156">webServiceInputs</span><span class="sxs-lookup"><span data-stu-id="d778c-156">webServiceInputs</span></span>  | <span data-ttu-id="d778c-157">Key, Value pairs, mapping the names of Azure Machine Learning Web Service Inputs.</span><span class="sxs-lookup"><span data-stu-id="d778c-157">Key, Value pairs, mapping the names of Azure Machine Learning Web Service Inputs.</span></span> <span data-ttu-id="d778c-158">Key must match the input parameters defined in the published Azure Machine Learning Web Service.</span><span class="sxs-lookup"><span data-stu-id="d778c-158">Key must match the input parameters defined in the published Azure Machine Learning Web Service.</span></span> <span data-ttu-id="d778c-159">Value is an Azure Storage Linked Services and FilePath properties pair specifying the input Blob locations.</span><span class="sxs-lookup"><span data-stu-id="d778c-159">Value is an Azure Storage Linked Services and FilePath properties pair specifying the input Blob locations.</span></span> | <span data-ttu-id="d778c-160">No</span><span class="sxs-lookup"><span data-stu-id="d778c-160">No</span></span>       |
| <span data-ttu-id="d778c-161">webServiceOutputs</span><span class="sxs-lookup"><span data-stu-id="d778c-161">webServiceOutputs</span></span> | <span data-ttu-id="d778c-162">Key, Value pairs, mapping the names of Azure Machine Learning Web Service Outputs.</span><span class="sxs-lookup"><span data-stu-id="d778c-162">Key, Value pairs, mapping the names of Azure Machine Learning Web Service Outputs.</span></span> <span data-ttu-id="d778c-163">Key must match the output parameters defined in the published Azure Machine Learning Web Service.</span><span class="sxs-lookup"><span data-stu-id="d778c-163">Key must match the output parameters defined in the published Azure Machine Learning Web Service.</span></span> <span data-ttu-id="d778c-164">Value is an Azure Storage Linked Services and FilePath properties pair specifying the output Blob locations.</span><span class="sxs-lookup"><span data-stu-id="d778c-164">Value is an Azure Storage Linked Services and FilePath properties pair specifying the output Blob locations.</span></span> | <span data-ttu-id="d778c-165">No</span><span class="sxs-lookup"><span data-stu-id="d778c-165">No</span></span>       |
| <span data-ttu-id="d778c-166">globalParameters</span><span class="sxs-lookup"><span data-stu-id="d778c-166">globalParameters</span></span>  | <span data-ttu-id="d778c-167">Key, Value pairs to be passed to the Azure ML Batch Execution Service endpoint.</span><span class="sxs-lookup"><span data-stu-id="d778c-167">Key, Value pairs to be passed to the Azure ML Batch Execution Service endpoint.</span></span> <span data-ttu-id="d778c-168">Keys must match the names of web service parameters defined in the published Azure ML web service.</span><span class="sxs-lookup"><span data-stu-id="d778c-168">Keys must match the names of web service parameters defined in the published Azure ML web service.</span></span> <span data-ttu-id="d778c-169">Values are passed in the GlobalParameters property of the Azure ML batch execution request</span><span class="sxs-lookup"><span data-stu-id="d778c-169">Values are passed in the GlobalParameters property of the Azure ML batch execution request</span></span> | <span data-ttu-id="d778c-170">No</span><span class="sxs-lookup"><span data-stu-id="d778c-170">No</span></span>       |

### <a name="scenario-1-experiments-using-web-service-inputsoutputs-that-refer-to-data-in-azure-blob-storage"></a><span data-ttu-id="d778c-171">Scenario 1: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="d778c-171">Scenario 1: Experiments using Web service inputs/outputs that refer to data in Azure Blob Storage</span></span>

<span data-ttu-id="d778c-172">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span><span class="sxs-lookup"><span data-stu-id="d778c-172">In this scenario, the Azure Machine Learning Web service makes predictions using data from a file in an Azure blob storage and stores the prediction results in the blob storage.</span></span> <span data-ttu-id="d778c-173">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span><span class="sxs-lookup"><span data-stu-id="d778c-173">The following JSON defines a Data Factory pipeline with an AzureMLBatchExecution activity.</span></span> <span data-ttu-id="d778c-174">The input and output data in Azure Blog Storage is referenced using a LinkedName and FilePath pair.</span><span class="sxs-lookup"><span data-stu-id="d778c-174">The input and output data in Azure Blog Storage is referenced using a LinkedName and FilePath pair.</span></span> <span data-ttu-id="d778c-175">In the sample Linked Service of inputs and outputs are different, you can use different Linked Services for each of your inputs/outputs for Data Factory to be able to pick up the right files and send to Azure ML Web Service.</span><span class="sxs-lookup"><span data-stu-id="d778c-175">In the sample Linked Service of inputs and outputs are different, you can use different Linked Services for each of your inputs/outputs for Data Factory to be able to pick up the right files and send to Azure ML Web Service.</span></span> 

> [!IMPORTANT]
> In your Azure ML experiment, web service input and output ports, and global parameters have default names ("input1", "input2") that you can customize. The names you use for webServiceInputs, webServiceOutputs, and globalParameters settings must exactly match the names in the experiments. You can view the sample request payload on the Batch Execution Help page for your Azure ML endpoint to verify the expected mapping.
>
> 

```JSON
{
    "name": "AzureMLExecutionActivityTemplate",
    "description": "description",
    "type": "AzureMLBatchExecution",
    "linkedServiceName": {
        "referenceName": "AzureMLLinkedService",
        "type": "LinkedServiceReference"
    },
    "typeProperties": {
        "webServiceInputs": {
            "input1": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService1",
                    "type": "LinkedServiceReference"
                }, 
                "FilePath":"amltest/input/in1.csv"
            }, 
            "input2": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService1",
                    "type": "LinkedServiceReference" 
                }, 
                "FilePath":"amltest/input/in2.csv"
            }        
        },
        "webServiceOutputs": {
            "outputName1": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService2",
                    "type": "LinkedServiceReference"   
                }, 
                "FilePath":"amltest2/output/out1.csv"
            }, 
            "outputName2": {
                "LinkedServiceName":{
                    "referenceName": "AzureStorageLinkedService2",
                    "type": "LinkedServiceReference"   
                }, 
                "FilePath":"amltest2/output/out2.csv"
            }         
        }
    }
}
```
### <a name="scenario-2-experiments-using-readerwriter-modules-to-refer-to-data-in-various-storages"></a><span data-ttu-id="d778c-179">Scenario 2: Experiments using Reader/Writer Modules to refer to data in various storages</span><span class="sxs-lookup"><span data-stu-id="d778c-179">Scenario 2: Experiments using Reader/Writer Modules to refer to data in various storages</span></span>
<span data-ttu-id="d778c-180">Another common scenario when creating Azure ML experiments is to use Import Data and Output Data modules.</span><span class="sxs-lookup"><span data-stu-id="d778c-180">Another common scenario when creating Azure ML experiments is to use Import Data and Output Data modules.</span></span> <span data-ttu-id="d778c-181">The Import Data module is used to load data into an experiment and the Output Data module is to save data from your experiments.</span><span class="sxs-lookup"><span data-stu-id="d778c-181">The Import Data module is used to load data into an experiment and the Output Data module is to save data from your experiments.</span></span> <span data-ttu-id="d778c-182">For details about Import Data and Output Data modules, see [Import Data](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Output Data](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span><span class="sxs-lookup"><span data-stu-id="d778c-182">For details about Import Data and Output Data modules, see [Import Data](https://msdn.microsoft.com/library/azure/dn905997.aspx) and [Output Data](https://msdn.microsoft.com/library/azure/dn905984.aspx) topics on MSDN Library.</span></span>     

<span data-ttu-id="d778c-183">When using the Import Data and Output Data modules, it is good practice to use a Web service parameter for each property of these modules.</span><span class="sxs-lookup"><span data-stu-id="d778c-183">When using the Import Data and Output Data modules, it is good practice to use a Web service parameter for each property of these modules.</span></span> <span data-ttu-id="d778c-184">These web parameters enable you to configure the values during runtime.</span><span class="sxs-lookup"><span data-stu-id="d778c-184">These web parameters enable you to configure the values during runtime.</span></span> <span data-ttu-id="d778c-185">For example, you could create an experiment with an Import Data module that uses an Azure SQL Database: XXX.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="d778c-185">For example, you could create an experiment with an Import Data module that uses an Azure SQL Database: XXX.database.windows.net.</span></span> <span data-ttu-id="d778c-186">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called `YYY.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="d778c-186">After the web service has been deployed, you want to enable the consumers of the web service to specify another Azure SQL Server called `YYY.database.windows.net`.</span></span> <span data-ttu-id="d778c-187">You can use a Web service parameter to allow this value to be configured.</span><span class="sxs-lookup"><span data-stu-id="d778c-187">You can use a Web service parameter to allow this value to be configured.</span></span>

> [!NOTE]
> Web service input and output are different from Web service parameters. In the first scenario, you have seen how an input and output can be specified for an Azure ML Web service. In this scenario, you pass parameters for a Web service that correspond to properties of Import Data/Output Data modules.
>
> 

<span data-ttu-id="d778c-191">Let's look at a scenario for using Web service parameters.</span><span class="sxs-lookup"><span data-stu-id="d778c-191">Let's look at a scenario for using Web service parameters.</span></span> <span data-ttu-id="d778c-192">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="d778c-192">You have a deployed Azure Machine Learning web service that uses a reader module to read data from one of the data sources supported by Azure Machine Learning (for example: Azure SQL Database).</span></span> <span data-ttu-id="d778c-193">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="d778c-193">After the batch execution is performed, the results are written using a Writer module (Azure SQL Database).</span></span>  <span data-ttu-id="d778c-194">No web service inputs and outputs are defined in the experiments.</span><span class="sxs-lookup"><span data-stu-id="d778c-194">No web service inputs and outputs are defined in the experiments.</span></span> <span data-ttu-id="d778c-195">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span><span class="sxs-lookup"><span data-stu-id="d778c-195">In this case, we recommend that you configure relevant web service parameters for the reader and writer modules.</span></span> <span data-ttu-id="d778c-196">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span><span class="sxs-lookup"><span data-stu-id="d778c-196">This configuration allows the reader/writer modules to be configured when using the AzureMLBatchExecution activity.</span></span> <span data-ttu-id="d778c-197">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span><span class="sxs-lookup"><span data-stu-id="d778c-197">You specify Web service parameters in the **globalParameters** section in the activity JSON as follows.</span></span>

```JSON
"typeProperties": {
    "globalParameters": {
        "Database server name": "<myserver>.database.windows.net",
        "Database name": "<database>",
        "Server user account name": "<user name>",
        "Server user account password": "<password>"
    }
}
```


> [!NOTE]
> The Web service parameters are case-sensitive, so ensure that the names you specify in the activity JSON match the ones exposed by the Web service.
>

<span data-ttu-id="d778c-199">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span><span class="sxs-lookup"><span data-stu-id="d778c-199">After you are done with retraining, update the scoring web service (predictive experiment exposed as a web service) with the newly trained model by using the **Azure ML Update Resource Activity**.</span></span> <span data-ttu-id="d778c-200">See [Updating models using Update Resource Activity](update-machine-learning-models.md) article for details.</span><span class="sxs-lookup"><span data-stu-id="d778c-200">See [Updating models using Update Resource Activity](update-machine-learning-models.md) article for details.</span></span>



## <a name="next-steps"></a><span data-ttu-id="d778c-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="d778c-201">Next steps</span></span>
<span data-ttu-id="d778c-202">See the following articles that explain how to transform data in other ways:</span><span class="sxs-lookup"><span data-stu-id="d778c-202">See the following articles that explain how to transform data in other ways:</span></span> 

* [<span data-ttu-id="d778c-203">U-SQL activity</span><span class="sxs-lookup"><span data-stu-id="d778c-203">U-SQL activity</span></span>](transform-data-using-data-lake-analytics.md)
* [<span data-ttu-id="d778c-204">Hive activity</span><span class="sxs-lookup"><span data-stu-id="d778c-204">Hive activity</span></span>](transform-data-using-hadoop-hive.md)
* [<span data-ttu-id="d778c-205">Pig activity</span><span class="sxs-lookup"><span data-stu-id="d778c-205">Pig activity</span></span>](transform-data-using-hadoop-pig.md)
* [<span data-ttu-id="d778c-206">MapReduce activity</span><span class="sxs-lookup"><span data-stu-id="d778c-206">MapReduce activity</span></span>](transform-data-using-hadoop-map-reduce.md)
* [<span data-ttu-id="d778c-207">Hadoop Streaming activity</span><span class="sxs-lookup"><span data-stu-id="d778c-207">Hadoop Streaming activity</span></span>](transform-data-using-hadoop-streaming.md)
* [<span data-ttu-id="d778c-208">Spark activity</span><span class="sxs-lookup"><span data-stu-id="d778c-208">Spark activity</span></span>](transform-data-using-spark.md)
* [<span data-ttu-id="d778c-209">.NET custom activity</span><span class="sxs-lookup"><span data-stu-id="d778c-209">.NET custom activity</span></span>](transform-data-using-dotnet-custom-activity.md)
* [<span data-ttu-id="d778c-210">Stored procedure activity</span><span class="sxs-lookup"><span data-stu-id="d778c-210">Stored procedure activity</span></span>](transform-data-using-stored-procedure.md)
