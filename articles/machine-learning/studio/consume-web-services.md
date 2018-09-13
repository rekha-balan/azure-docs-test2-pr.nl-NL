---
title: How to consume an Azure Machine Learning Web service | Microsoft Docs
description: Once a machine learning service is deployed, the RESTFul Web service that is made available can be consumed either as real-time request-response service or as a batch execution service.
services: machine-learning
documentationcenter: ''
author: YasinMSFT
ms.author: yahajiza
manager: hjerez
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.component: studio
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 06/02/2017
ms.openlocfilehash: b89fb0fbb499fa06c9e56f02937b1c586efde9b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966653"
---
# <a name="how-to-consume-an-azure-machine-learning-web-service"></a><span data-ttu-id="88058-103">How to consume an Azure Machine Learning Web service</span><span class="sxs-lookup"><span data-stu-id="88058-103">How to consume an Azure Machine Learning Web service</span></span>

<span data-ttu-id="88058-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API to send it data and get predictions.</span><span class="sxs-lookup"><span data-stu-id="88058-104">Once you deploy an Azure Machine Learning predictive model as a Web service, you can use a REST API to send it data and get predictions.</span></span> <span data-ttu-id="88058-105">You can send the data in real-time or in batch mode.</span><span class="sxs-lookup"><span data-stu-id="88058-105">You can send the data in real-time or in batch mode.</span></span>

<span data-ttu-id="88058-106">You can find more information about how to create and deploy a Machine Learning Web service using Machine Learning Studio here:</span><span class="sxs-lookup"><span data-stu-id="88058-106">You can find more information about how to create and deploy a Machine Learning Web service using Machine Learning Studio here:</span></span>

* <span data-ttu-id="88058-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](create-experiment.md).</span><span class="sxs-lookup"><span data-stu-id="88058-107">For a tutorial on how to create an experiment in Machine Learning Studio, see [Create your first experiment](create-experiment.md).</span></span>
* <span data-ttu-id="88058-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="88058-108">For details on how to deploy a Web service, see [Deploy a Machine Learning Web service](publish-a-machine-learning-web-service.md).</span></span>
* <span data-ttu-id="88058-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="88058-109">For more information about Machine Learning in general, visit the [Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="overview"></a><span data-ttu-id="88058-110">Overview</span><span class="sxs-lookup"><span data-stu-id="88058-110">Overview</span></span>
<span data-ttu-id="88058-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span><span class="sxs-lookup"><span data-stu-id="88058-111">With the Azure Machine Learning Web service, an external application communicates with a Machine Learning workflow scoring model in real time.</span></span> <span data-ttu-id="88058-112">A Machine Learning Web service call returns prediction results to an external application.</span><span class="sxs-lookup"><span data-stu-id="88058-112">A Machine Learning Web service call returns prediction results to an external application.</span></span> <span data-ttu-id="88058-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span><span class="sxs-lookup"><span data-stu-id="88058-113">To make a Machine Learning Web service call, you pass an API key that is created when you deploy a prediction.</span></span> <span data-ttu-id="88058-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span><span class="sxs-lookup"><span data-stu-id="88058-114">The Machine Learning Web service is based on REST, a popular architecture choice for web programming projects.</span></span>

<span data-ttu-id="88058-115">Azure Machine Learning has two types of services:</span><span class="sxs-lookup"><span data-stu-id="88058-115">Azure Machine Learning has two types of services:</span></span>

* <span data-ttu-id="88058-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="88058-116">Request-Response Service (RRS) – A low latency, highly scalable service that provides an interface to the stateless models created and deployed from the Machine Learning Studio.</span></span>
* <span data-ttu-id="88058-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span><span class="sxs-lookup"><span data-stu-id="88058-117">Batch Execution Service (BES) – An asynchronous service that scores a batch for data records.</span></span>

<span data-ttu-id="88058-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="88058-118">For more information about Machine Learning Web services, see [Deploy a Machine Learning Web service](publish-a-machine-learning-web-service.md).</span></span>

## <a name="get-an-azure-machine-learning-authorization-key"></a><span data-ttu-id="88058-119">Get an Azure Machine Learning authorization key</span><span class="sxs-lookup"><span data-stu-id="88058-119">Get an Azure Machine Learning authorization key</span></span>
<span data-ttu-id="88058-120">When you deploy your experiment, API keys are generated for the Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-120">When you deploy your experiment, API keys are generated for the Web service.</span></span> <span data-ttu-id="88058-121">You can retrieve the keys from several locations.</span><span class="sxs-lookup"><span data-stu-id="88058-121">You can retrieve the keys from several locations.</span></span>

### <a name="from-the-microsoft-azure-machine-learning-web-services-portal"></a><span data-ttu-id="88058-122">From the Microsoft Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="88058-122">From the Microsoft Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="88058-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span><span class="sxs-lookup"><span data-stu-id="88058-123">Sign in to the [Microsoft Azure Machine Learning Web Services](https://services.azureml.net) portal.</span></span>

<span data-ttu-id="88058-124">To retrieve the API key for a New Machine Learning Web service:</span><span class="sxs-lookup"><span data-stu-id="88058-124">To retrieve the API key for a New Machine Learning Web service:</span></span>

1. <span data-ttu-id="88058-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span><span class="sxs-lookup"><span data-stu-id="88058-125">In the Azure Machine Learning Web Services portal, click **Web Services** the top menu.</span></span>
2. <span data-ttu-id="88058-126">Click the Web service for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="88058-126">Click the Web service for which you want to retrieve the key.</span></span>
3. <span data-ttu-id="88058-127">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="88058-127">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="88058-128">Copy and save the **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="88058-128">Copy and save the **Primary Key**.</span></span>

<span data-ttu-id="88058-129">To retrieve the API key for a Classic Machine Learning Web service:</span><span class="sxs-lookup"><span data-stu-id="88058-129">To retrieve the API key for a Classic Machine Learning Web service:</span></span>

1. <span data-ttu-id="88058-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span><span class="sxs-lookup"><span data-stu-id="88058-130">In the Azure Machine Learning Web Services portal, click **Classic Web Services** the top menu.</span></span>
2. <span data-ttu-id="88058-131">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="88058-131">Click the Web service with which you are working.</span></span>
3. <span data-ttu-id="88058-132">Click the endpoint for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="88058-132">Click the endpoint for which you want to retrieve the key.</span></span>
4. <span data-ttu-id="88058-133">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="88058-133">On the top menu, click **Consume**.</span></span>
5. <span data-ttu-id="88058-134">Copy and save the **Primary Key**.</span><span class="sxs-lookup"><span data-stu-id="88058-134">Copy and save the **Primary Key**.</span></span>

### <a name="classic-web-service"></a><span data-ttu-id="88058-135">Classic Web service</span><span class="sxs-lookup"><span data-stu-id="88058-135">Classic Web service</span></span>
 <span data-ttu-id="88058-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="88058-136">You can also retrieve a key for a Classic Web service from Machine Learning Studio.</span></span>

#### <a name="machine-learning-studio"></a><span data-ttu-id="88058-137">Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="88058-137">Machine Learning Studio</span></span>
1. <span data-ttu-id="88058-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span><span class="sxs-lookup"><span data-stu-id="88058-138">In Machine Learning Studio, click **WEB SERVICES** on the left.</span></span>
2. <span data-ttu-id="88058-139">Click a Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-139">Click a Web service.</span></span> <span data-ttu-id="88058-140">The **API key** is on the **DASHBOARD** tab.</span><span class="sxs-lookup"><span data-stu-id="88058-140">The **API key** is on the **DASHBOARD** tab.</span></span>

## <a id="connect"></a><span data-ttu-id="88058-141">Connect to a Machine Learning Web service</span><span class="sxs-lookup"><span data-stu-id="88058-141">Connect to a Machine Learning Web service</span></span>
<span data-ttu-id="88058-142">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span><span class="sxs-lookup"><span data-stu-id="88058-142">You can connect to a Machine Learning Web service using any programming language that supports HTTP request and response.</span></span> <span data-ttu-id="88058-143">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span><span class="sxs-lookup"><span data-stu-id="88058-143">You can view examples in C#, Python, and R from a Machine Learning Web service help page.</span></span>

<span data-ttu-id="88058-144">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-144">**Machine Learning API help** Machine Learning API help is created when you deploy a Web service.</span></span> <span data-ttu-id="88058-145">See [Azure Machine Learning Walkthrough- Deploy Web Service](walkthrough-5-publish-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="88058-145">See [Azure Machine Learning Walkthrough- Deploy Web Service](walkthrough-5-publish-web-service.md).</span></span>
<span data-ttu-id="88058-146">The Machine Learning API help contains details about a prediction Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-146">The Machine Learning API help contains details about a prediction Web service.</span></span>

1. <span data-ttu-id="88058-147">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="88058-147">Click the Web service with which you are working.</span></span>
2. <span data-ttu-id="88058-148">Click the endpoint for which you want to view the API Help Page.</span><span class="sxs-lookup"><span data-stu-id="88058-148">Click the endpoint for which you want to view the API Help Page.</span></span>
3. <span data-ttu-id="88058-149">On the top menu, click **Consume**.</span><span class="sxs-lookup"><span data-stu-id="88058-149">On the top menu, click **Consume**.</span></span>
4. <span data-ttu-id="88058-150">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span><span class="sxs-lookup"><span data-stu-id="88058-150">Click **API help page** under either the Request-Response or Batch Execution endpoints.</span></span>

<span data-ttu-id="88058-151">**To view Machine Learning API help for a New Web service**</span><span class="sxs-lookup"><span data-stu-id="88058-151">**To view Machine Learning API help for a New Web service**</span></span>

<span data-ttu-id="88058-152">In the [Azure Machine Learning Web Services Portal](https://services.azureml.net/):</span><span class="sxs-lookup"><span data-stu-id="88058-152">In the [Azure Machine Learning Web Services Portal](https://services.azureml.net/):</span></span>

1. <span data-ttu-id="88058-153">Click **WEB SERVICES** on the top menu.</span><span class="sxs-lookup"><span data-stu-id="88058-153">Click **WEB SERVICES** on the top menu.</span></span>
2. <span data-ttu-id="88058-154">Click the Web service for which you want to retrieve the key.</span><span class="sxs-lookup"><span data-stu-id="88058-154">Click the Web service for which you want to retrieve the key.</span></span>

<span data-ttu-id="88058-155">Click **Use Web Service** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span><span class="sxs-lookup"><span data-stu-id="88058-155">Click **Use Web Service** to get the URIs for the Request-Reposonse and Batch Execution Services and Sample code in C#, R, and Python.</span></span>

<span data-ttu-id="88058-156">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span><span class="sxs-lookup"><span data-stu-id="88058-156">Click **Swagger API** to get Swagger based documentation for the APIs called from the supplied URIs.</span></span>

### <a name="c-sample"></a><span data-ttu-id="88058-157">C# Sample</span><span class="sxs-lookup"><span data-stu-id="88058-157">C# Sample</span></span>
<span data-ttu-id="88058-158">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span><span class="sxs-lookup"><span data-stu-id="88058-158">To connect to a Machine Learning Web service, use an **HttpClient** passing ScoreData.</span></span> <span data-ttu-id="88058-159">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span><span class="sxs-lookup"><span data-stu-id="88058-159">ScoreData contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="88058-160">You authenticate to the Machine Learning service with an API key.</span><span class="sxs-lookup"><span data-stu-id="88058-160">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="88058-161">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span><span class="sxs-lookup"><span data-stu-id="88058-161">To connect to a Machine Learning Web service, the **Microsoft.AspNet.WebApi.Client** NuGet package must be installed.</span></span>

<span data-ttu-id="88058-162">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span><span class="sxs-lookup"><span data-stu-id="88058-162">**Install Microsoft.AspNet.WebApi.Client NuGet in Visual Studio**</span></span>

1. <span data-ttu-id="88058-163">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span><span class="sxs-lookup"><span data-stu-id="88058-163">Publish the Download dataset from UCI: Adult 2 class dataset Web Service.</span></span>
2. <span data-ttu-id="88058-164">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="88058-164">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="88058-165">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span><span class="sxs-lookup"><span data-stu-id="88058-165">Choose **Install-Package Microsoft.AspNet.WebApi.Client**.</span></span>

<span data-ttu-id="88058-166">**To run the code sample**</span><span class="sxs-lookup"><span data-stu-id="88058-166">**To run the code sample**</span></span>

1. <span data-ttu-id="88058-167">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span><span class="sxs-lookup"><span data-stu-id="88058-167">Publish "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="88058-168">Assign apiKey with the key from a Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-168">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="88058-169">See **Get an Azure Machine Learning authorization key** above.</span><span class="sxs-lookup"><span data-stu-id="88058-169">See **Get an Azure Machine Learning authorization key** above.</span></span>
3. <span data-ttu-id="88058-170">Assign serviceUri with the Request URI.</span><span class="sxs-lookup"><span data-stu-id="88058-170">Assign serviceUri with the Request URI.</span></span>

<span data-ttu-id="88058-171">**Here is what a complete request will look like.**</span><span class="sxs-lookup"><span data-stu-id="88058-171">**Here is what a complete request will look like.**</span></span>
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Net.Http;
using System.Net.Http.Formatting;
using System.Net.Http.Headers;
using System.Text;
using System.Threading.Tasks;

namespace CallRequestResponseService
{
    class Program
    {
        static void Main(string[] args)
        {
            InvokeRequestResponseService().Wait();
        }

        static async Task InvokeRequestResponseService()
        {
            using (var client = new HttpClient())
            {
                var scoreRequest = new
                {
                    Inputs = new Dictionary<string, List<Dictionary<string, string>>> () {
                        {
                            "input1",
                            // Replace columns labels with those used in your dataset
                            new List<Dictionary<string, string>>(){new Dictionary<string, string>(){
                                    {
                                        "column1", "value1"
                                    },
                                    {
                                        "column2", "value2"
                                    },
                                    {
                                        "column3", "value3"
                                    }
                                }
                            }
                        },
                    },
                    GlobalParameters = new Dictionary<string, string>() {}
                };

                // Replace these values with your API key and URI found on https://services.azureml.net/
                const string apiKey = "<your-api-key>"; 
                const string apiUri = "<your-api-uri>";
                
                client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue( "Bearer", apiKey);
                client.BaseAddress = new Uri(apiUri);

                // WARNING: The 'await' statement below can result in a deadlock
                // if you are calling this code from the UI thread of an ASP.Net application.
                // One way to address this would be to call ConfigureAwait(false)
                // so that the execution does not attempt to resume on the original context.
                // For instance, replace code such as:
                //      result = await DoSomeTask()
                // with the following:
                //      result = await DoSomeTask().ConfigureAwait(false)

                HttpResponseMessage response = await client.PostAsJsonAsync("", scoreRequest);

                if (response.IsSuccessStatusCode)
                {
                    string result = await response.Content.ReadAsStringAsync();
                    Console.WriteLine("Result: {0}", result);
                }
                else
                {
                    Console.WriteLine(string.Format("The request failed with status code: {0}", response.StatusCode));

                    // Print the headers - they include the requert ID and the timestamp,
                    // which are useful for debugging the failure
                    Console.WriteLine(response.Headers.ToString());

                    string responseContent = await response.Content.ReadAsStringAsync();
                    Console.WriteLine(responseContent);
                }
            }
        }
    }
}
```

### <a name="python-sample"></a><span data-ttu-id="88058-172">Python Sample</span><span class="sxs-lookup"><span data-stu-id="88058-172">Python Sample</span></span>
<span data-ttu-id="88058-173">To connect to a Machine Learning Web service, use the **urllib2** library for Python 2.X and **urllib.request** library for Python 3.X.</span><span class="sxs-lookup"><span data-stu-id="88058-173">To connect to a Machine Learning Web service, use the **urllib2** library for Python 2.X and **urllib.request** library for Python 3.X.</span></span> <span data-ttu-id="88058-174">You will pass ScoreData, which contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span><span class="sxs-lookup"><span data-stu-id="88058-174">You will pass ScoreData, which contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="88058-175">You authenticate to the Machine Learning service with an API key.</span><span class="sxs-lookup"><span data-stu-id="88058-175">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="88058-176">**To run the code sample**</span><span class="sxs-lookup"><span data-stu-id="88058-176">**To run the code sample**</span></span>

1. <span data-ttu-id="88058-177">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span><span class="sxs-lookup"><span data-stu-id="88058-177">Deploy "Sample 1: Download dataset from UCI: Adult 2 class dataset" experiment, part of the Machine Learning sample collection.</span></span>
2. <span data-ttu-id="88058-178">Assign apiKey with the key from a Web service.</span><span class="sxs-lookup"><span data-stu-id="88058-178">Assign apiKey with the key from a Web service.</span></span> <span data-ttu-id="88058-179">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span><span class="sxs-lookup"><span data-stu-id="88058-179">See the **Get an Azure Machine Learning authorization key** section near the beginning of this article.</span></span>
3. <span data-ttu-id="88058-180">Assign serviceUri with the Request URI.</span><span class="sxs-lookup"><span data-stu-id="88058-180">Assign serviceUri with the Request URI.</span></span>

<span data-ttu-id="88058-181">**Here is what a complete request will look like.**</span><span class="sxs-lookup"><span data-stu-id="88058-181">**Here is what a complete request will look like.**</span></span>
```python
import urllib2 # urllib.request for Python 3.X
import json

data = {
    "Inputs": {
        "input1":
        [
            {
                'column1': "value1",   
                'column2': "value2",   
                'column3': "value3"
            }
        ],
    },
    "GlobalParameters":  {}
}

body = str.encode(json.dumps(data))

# Replace this with the URI and API Key for your web service
url = '<your-api-uri>'
api_key = '<your-api-key>'
headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

# "urllib.request.Request(uri, body, headers)" for Python 3.X
req = urllib2.Request(url, body, headers)

try:
    # "urllib.request.urlopen(req)" for Python 3.X
    response = urllib2.urlopen(req)

    result = response.read()
    print(result)
# "urllib.error.HTTPError as error" for Python 3.X
except urllib2.HTTPError, error: 
    print("The request failed with status code: " + str(error.code))

    # Print the headers - they include the requert ID and the timestamp, which are useful for debugging the failure
    print(error.info())
    print(json.loads(error.read())) 
```

### <a name="r-sample"></a><span data-ttu-id="88058-182">R Sample</span><span class="sxs-lookup"><span data-stu-id="88058-182">R Sample</span></span>

<span data-ttu-id="88058-183">To connect to a Machine Learning Web Service, use the **RCurl** and **rjson** libraries to make the request and process the returned JSON response.</span><span class="sxs-lookup"><span data-stu-id="88058-183">To connect to a Machine Learning Web Service, use the **RCurl** and **rjson** libraries to make the request and process the returned JSON response.</span></span> <span data-ttu-id="88058-184">You will pass ScoreData, which contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span><span class="sxs-lookup"><span data-stu-id="88058-184">You will pass ScoreData, which contains a FeatureVector, an n-dimensional vector of numerical features that represents the ScoreData.</span></span> <span data-ttu-id="88058-185">You authenticate to the Machine Learning service with an API key.</span><span class="sxs-lookup"><span data-stu-id="88058-185">You authenticate to the Machine Learning service with an API key.</span></span>

<span data-ttu-id="88058-186">**Here is what a complete request will look like.**</span><span class="sxs-lookup"><span data-stu-id="88058-186">**Here is what a complete request will look like.**</span></span>
```r
library("RCurl")
library("rjson")

# Accept SSL certificates issued by public Certificate Authorities
options(RCurlOptions = list(cainfo = system.file("CurlSSL", "cacert.pem", package = "RCurl")))

h = basicTextGatherer()
hdr = basicHeaderGatherer()

req = list(
    Inputs = list(
            "input1" = list(
                list(
                        'column1' = "value1",
                        'column2' = "value2",
                        'column3' = "value3"
                    )
            )
        ),
        GlobalParameters = setNames(fromJSON('{}'), character(0))
)

body = enc2utf8(toJSON(req))
api_key = "<your-api-key>" # Replace this with the API key for the web service
authz_hdr = paste('Bearer', api_key, sep=' ')

h$reset()
curlPerform(url = "<your-api-uri>",
httpheader=c('Content-Type' = "application/json", 'Authorization' = authz_hdr),
postfields=body,
writefunction = h$update,
headerfunction = hdr$update,
verbose = TRUE
)

headers = hdr$value()
httpStatus = headers["status"]
if (httpStatus >= 400)
{
print(paste("The request failed with status code:", httpStatus, sep=" "))

# Print the headers - they include the requert ID and the timestamp, which are useful for debugging the failure
print(headers)
}

print("Result:")
result = h$value()
print(fromJSON(result))
```

### <a name="javascript-sample"></a><span data-ttu-id="88058-187">JavaScript Sample</span><span class="sxs-lookup"><span data-stu-id="88058-187">JavaScript Sample</span></span>

<span data-ttu-id="88058-188">To connect to a Machine Learning Web Service, use the **request** npm package in your project.</span><span class="sxs-lookup"><span data-stu-id="88058-188">To connect to a Machine Learning Web Service, use the **request** npm package in your project.</span></span> <span data-ttu-id="88058-189">You will also use the `JSON` object to format your input and parse the result.</span><span class="sxs-lookup"><span data-stu-id="88058-189">You will also use the `JSON` object to format your input and parse the result.</span></span> <span data-ttu-id="88058-190">Install using `npm install request --save`, or add `"request": "*"` to your package.json under `dependencies` and run `npm install`.</span><span class="sxs-lookup"><span data-stu-id="88058-190">Install using `npm install request --save`, or add `"request": "*"` to your package.json under `dependencies` and run `npm install`.</span></span>

<span data-ttu-id="88058-191">**Here is what a complete request will look like.**</span><span class="sxs-lookup"><span data-stu-id="88058-191">**Here is what a complete request will look like.**</span></span>
```js
let req = require("request");

const uri = "<your-api-uri>";
const apiKey = "<your-api-key>";

let data = {
    "Inputs": {
        "input1":
        [
            {
                'column1': "value1",
                'column2': "value2",
                'column3': "value3"
            }
        ],
    },
    "GlobalParameters": {}
}

const options = {
    uri: uri,
    method: "POST",
    headers: {
        "Content-Type": "application/json",
        "Authorization": "Bearer " + apiKey,
    },
    body: JSON.stringify(data)
}

req(options, (err, res, body) => {
    if (!err && res.statusCode == 200) {
        console.log(body);
    } else {
        console.log("The request failed with status code: " + res.statusCode);
    }
});
```