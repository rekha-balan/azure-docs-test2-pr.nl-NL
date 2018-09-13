---
title: Use Azure Machine Learning endpoints in Stream Analytics | Microsoft Docs
description: Machine Language User defined functions in Stream Analytics
keywords: ''
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 406b258f-b8c2-4e55-953c-b7f84e8e5354
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 0a2f30569a51a0f31ad5187f84bba5321d4df38f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554777"
---
# <a name="machine-learning-integration-in-stream-analytics"></a><span data-ttu-id="6b380-103">Machine Learning integration in Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b380-103">Machine Learning integration in Stream Analytics</span></span>
<span data-ttu-id="6b380-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span><span class="sxs-lookup"><span data-stu-id="6b380-104">Stream Analytics supports user-defined functions that call out to Azure Machine Learning endpoints.</span></span> <span data-ttu-id="6b380-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span><span class="sxs-lookup"><span data-stu-id="6b380-105">REST API support for this feature is detailed in the [Stream Analytics REST API library](https://msdn.microsoft.com/library/azure/dn835031.aspx).</span></span> <span data-ttu-id="6b380-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="6b380-106">This article provides supplemental information needed for successful implementation of this capability in Stream Analytics.</span></span> <span data-ttu-id="6b380-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="6b380-107">A tutorial has also been posted and is available [here](stream-analytics-machine-learning-integration-tutorial.md).</span></span>

## <a name="overview-azure-machine-learning-terminology"></a><span data-ttu-id="6b380-108">Overview: Azure Machine Learning terminology</span><span class="sxs-lookup"><span data-stu-id="6b380-108">Overview: Azure Machine Learning terminology</span></span>
<span data-ttu-id="6b380-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span><span class="sxs-lookup"><span data-stu-id="6b380-109">Microsoft Azure Machine Learning provides a collaborative, drag-and-drop tool you can use to build, test, and deploy predictive analytics solutions on your data.</span></span> <span data-ttu-id="6b380-110">This tool is called the *Azure Machine Learning Studio*.</span><span class="sxs-lookup"><span data-stu-id="6b380-110">This tool is called the *Azure Machine Learning Studio*.</span></span> <span data-ttu-id="6b380-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span><span class="sxs-lookup"><span data-stu-id="6b380-111">The studio is used to interact with the Machine Learning resources and easily build, test, and iterate on your design.</span></span> <span data-ttu-id="6b380-112">These resources and their definitions are below.</span><span class="sxs-lookup"><span data-stu-id="6b380-112">These resources and their definitions are below.</span></span>

* <span data-ttu-id="6b380-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span><span class="sxs-lookup"><span data-stu-id="6b380-113">**Workspace**: The *workspace* is a container that holds all other Machine Learning resources together in a container for management and control.</span></span>
* <span data-ttu-id="6b380-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span><span class="sxs-lookup"><span data-stu-id="6b380-114">**Experiment**: *Experiments* are created by data scientists to utilize datasets and train a machine learning model.</span></span>
* <span data-ttu-id="6b380-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span><span class="sxs-lookup"><span data-stu-id="6b380-115">**Endpoint**: *Endpoints* are the Azure Machine Learning object used to take features as input, apply a specified machine learning model and return scored output.</span></span>
* <span data-ttu-id="6b380-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span><span class="sxs-lookup"><span data-stu-id="6b380-116">**Scoring Webservice**: A *scoring webservice* is a collection of endpoints as mentioned above.</span></span>

<span data-ttu-id="6b380-117">Each endpoint has apis for batch execution and synchronous execution.</span><span class="sxs-lookup"><span data-stu-id="6b380-117">Each endpoint has apis for batch execution and synchronous execution.</span></span> <span data-ttu-id="6b380-118">Stream Analytics uses synchronous execution.</span><span class="sxs-lookup"><span data-stu-id="6b380-118">Stream Analytics uses synchronous execution.</span></span> <span data-ttu-id="6b380-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md#request-response-service-rrs) in AzureML studio.</span><span class="sxs-lookup"><span data-stu-id="6b380-119">The specific service is named a [Request/Response Service](../machine-learning/machine-learning-consume-web-services.md#request-response-service-rrs) in AzureML studio.</span></span>

## <a name="machine-learning-resources-needed-for-stream-analytics-jobs"></a><span data-ttu-id="6b380-120">Machine Learning resources needed for Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6b380-120">Machine Learning resources needed for Stream Analytics jobs</span></span>
<span data-ttu-id="6b380-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md#get-an-azure-machine-learning-authorization-key), and a swagger definition are all necessary for successful execution.</span><span class="sxs-lookup"><span data-stu-id="6b380-121">For the purposes of Stream Analytics job processing, a Request/Response endpoint, an [apikey](../machine-learning/machine-learning-connect-to-azure-machine-learning-web-service.md#get-an-azure-machine-learning-authorization-key), and a swagger definition are all necessary for successful execution.</span></span> <span data-ttu-id="6b380-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span><span class="sxs-lookup"><span data-stu-id="6b380-122">Stream Analytics has an additional endpoint that constructs the url for swagger endpoint, looks up the interface and returns a default UDF definition to the user.</span></span>

## <a name="configure-a-stream-analytics-and-machine-learning-udf-via-rest-api"></a><span data-ttu-id="6b380-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span><span class="sxs-lookup"><span data-stu-id="6b380-123">Configure a Stream Analytics and Machine Learning UDF via REST API</span></span>
<span data-ttu-id="6b380-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span><span class="sxs-lookup"><span data-stu-id="6b380-124">By using REST APIs you may configure your job to call Azure Machine Language functions.</span></span> <span data-ttu-id="6b380-125">The steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="6b380-125">The steps are as follows:</span></span>

1. <span data-ttu-id="6b380-126">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="6b380-126">Create a Stream Analytics job</span></span>
2. <span data-ttu-id="6b380-127">Define an input</span><span class="sxs-lookup"><span data-stu-id="6b380-127">Define an input</span></span>
3. <span data-ttu-id="6b380-128">Define an output</span><span class="sxs-lookup"><span data-stu-id="6b380-128">Define an output</span></span>
4. <span data-ttu-id="6b380-129">Create a user-defined function (UDF)</span><span class="sxs-lookup"><span data-stu-id="6b380-129">Create a user-defined function (UDF)</span></span>
5. <span data-ttu-id="6b380-130">Write a Stream Analytics transformation that calls the UDF</span><span class="sxs-lookup"><span data-stu-id="6b380-130">Write a Stream Analytics transformation that calls the UDF</span></span>
6. <span data-ttu-id="6b380-131">Start the job</span><span class="sxs-lookup"><span data-stu-id="6b380-131">Start the job</span></span>

## <a name="creating-a-udf-with-basic-properties"></a><span data-ttu-id="6b380-132">Creating a UDF with basic properties</span><span class="sxs-lookup"><span data-stu-id="6b380-132">Creating a UDF with basic properties</span></span>
<span data-ttu-id="6b380-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span><span class="sxs-lookup"><span data-stu-id="6b380-133">As an example, the following sample code creates a scalar UDF named *newudf* that binds to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6b380-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span><span class="sxs-lookup"><span data-stu-id="6b380-134">Note that the *endpoint* (service URI) can be found on the API help page for the chosen service and the *apiKey* can be found on the Services main page.</span></span>

````
    PUT : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>  
````

<span data-ttu-id="6b380-135">Example request body:</span><span class="sxs-lookup"><span data-stu-id="6b380-135">Example request body:</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77fb4b46bf2a30c63c078dca/services/b7be5e40fd194258796fb402c1958eaf/execute ",
                        "apiKey": "replacekeyhere"
                    }
                }
            }
        }
    }
````

## <a name="call-retrievedefaultdefinition-endpoint-for-default-udf"></a><span data-ttu-id="6b380-136">Call RetrieveDefaultDefinition endpoint for default UDF</span><span class="sxs-lookup"><span data-stu-id="6b380-136">Call RetrieveDefaultDefinition endpoint for default UDF</span></span>
<span data-ttu-id="6b380-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span><span class="sxs-lookup"><span data-stu-id="6b380-137">Once the skeleton UDF is created the complete definition of the UDF is needed.</span></span> <span data-ttu-id="6b380-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span><span class="sxs-lookup"><span data-stu-id="6b380-138">The RetreiveDefaultDefinition endpoint helps you get the default definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6b380-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span><span class="sxs-lookup"><span data-stu-id="6b380-139">The payload below requires you to get the default UDF definition for a scalar function that is bound to an Azure Machine Learning endpoint.</span></span> <span data-ttu-id="6b380-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span><span class="sxs-lookup"><span data-stu-id="6b380-140">It doesn’t specify the actual endpoint as it has already been provided during PUT request.</span></span> <span data-ttu-id="6b380-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span><span class="sxs-lookup"><span data-stu-id="6b380-141">Stream Analytics calls the endpoint provided in the request if it is provided explicitly.</span></span> <span data-ttu-id="6b380-142">Otherwise it uses the one originally referenced.</span><span class="sxs-lookup"><span data-stu-id="6b380-142">Otherwise it uses the one originally referenced.</span></span> <span data-ttu-id="6b380-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span><span class="sxs-lookup"><span data-stu-id="6b380-143">Here the UDF takes a single string parameter (a sentence) and returns a single output of type string which indicates the “sentiment” label for that sentence.</span></span>

````
POST : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>/RetrieveDefaultDefinition?api-version=<apiVersion>
````

<span data-ttu-id="6b380-144">Example request body:</span><span class="sxs-lookup"><span data-stu-id="6b380-144">Example request body:</span></span>  

````
    {
        "bindingType": "Microsoft.MachineLearning/WebService",
        "bindingRetrievalProperties": {
            "executeEndpoint": null,
            "udfType": "Scalar"
        }
    }
````

<span data-ttu-id="6b380-145">A sample output of this would look something like below.</span><span class="sxs-lookup"><span data-stu-id="6b380-145">A sample output of this would look something like below.</span></span>  

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="patch-udf-with-the-response"></a><span data-ttu-id="6b380-146">Patch UDF with the response</span><span class="sxs-lookup"><span data-stu-id="6b380-146">Patch UDF with the response</span></span>
<span data-ttu-id="6b380-147">Now the UDF must be patched with the previous response, as shown below.</span><span class="sxs-lookup"><span data-stu-id="6b380-147">Now the UDF must be patched with the previous response, as shown below.</span></span>

````
PATCH : /subscriptions/<subscriptionId>/resourceGroups/<resourceGroup>/providers/Microsoft.StreamAnalytics/streamingjobs/<streamingjobName>/functions/<udfName>?api-version=<apiVersion>
````

<span data-ttu-id="6b380-148">Request Body (Output from RetrieveDefaultDefinition):</span><span class="sxs-lookup"><span data-stu-id="6b380-148">Request Body (Output from RetrieveDefaultDefinition):</span></span>

````
    {
        "name": "newudf",
        "properties": {
            "type": "Scalar",
            "properties": {
                "inputs": [{
                    "dataType": "nvarchar(max)",
                    "isConfigurationParameter": null
                }],
                "output": {
                    "dataType": "nvarchar(max)"
                },
                "binding": {
                    "type": "Microsoft.MachineLearning/WebService",
                    "properties": {
                        "endpoint": "https://ussouthcentral.services.azureml.net/workspaces/f80d5d7a77ga4a4bbf2a30c63c078dca/services/b7be5e40fd194258896fb602c1858eaf/execute",
                        "apiKey": null,
                        "inputs": {
                            "name": "input1",
                            "columnNames": [{
                                "name": "tweet",
                                "dataType": "string",
                                "mapTo": 0
                            }]
                        },
                        "outputs": [{
                            "name": "Sentiment",
                            "dataType": "string"
                        }],
                        "batchSize": 10
                    }
                }
            }
        }
    }
````

## <a name="implement-stream-analytics-transformation-to-call-the-udf"></a><span data-ttu-id="6b380-149">Implement Stream Analytics transformation to call the UDF</span><span class="sxs-lookup"><span data-stu-id="6b380-149">Implement Stream Analytics transformation to call the UDF</span></span>
<span data-ttu-id="6b380-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span><span class="sxs-lookup"><span data-stu-id="6b380-150">Now query the UDF (here named scoreTweet) for every input event and write a response for that event to an output.</span></span>  

````
    {
        "name": "transformation",
        "properties": {
            "streamingUnits": null,
            "query": "select *,scoreTweet(Tweet) TweetSentiment into blobOutput from blobInput"
        }
    }
````


## <a name="get-help"></a><span data-ttu-id="6b380-151">Get help</span><span class="sxs-lookup"><span data-stu-id="6b380-151">Get help</span></span>
<span data-ttu-id="6b380-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6b380-152">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b380-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="6b380-153">Next steps</span></span>
* [<span data-ttu-id="6b380-154">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b380-154">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6b380-155">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b380-155">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="6b380-156">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="6b380-156">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6b380-157">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="6b380-157">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6b380-158">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="6b380-158">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

