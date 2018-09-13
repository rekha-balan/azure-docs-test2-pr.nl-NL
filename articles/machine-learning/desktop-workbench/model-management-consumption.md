---
title: Azure Machine Learning Model Management web service consumption | Microsoft Docs
description: This document describes the steps and concepts involved in consuming web services deployed using model management in Azure Machine Learning.
services: machine-learning
author: raymondlaghaeian
ms.author: raymondl
manager: hjerez
ms.reviewer: jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 09/06/2017
ms.openlocfilehash: 4a49ccff68003cf7b81a7d945176992a2893d1ac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966644"
---
# <a name="consuming-web-services"></a><span data-ttu-id="e7a49-103">Consuming web services</span><span class="sxs-lookup"><span data-stu-id="e7a49-103">Consuming web services</span></span>
<span data-ttu-id="e7a49-104">Once you deploy a model as a realtime web service, you can send it data and get predictions from a variety of platforms and applications.</span><span class="sxs-lookup"><span data-stu-id="e7a49-104">Once you deploy a model as a realtime web service, you can send it data and get predictions from a variety of platforms and applications.</span></span> <span data-ttu-id="e7a49-105">The realtime web service exposes a REST API for getting predictions.</span><span class="sxs-lookup"><span data-stu-id="e7a49-105">The realtime web service exposes a REST API for getting predictions.</span></span> <span data-ttu-id="e7a49-106">You can send data to the web service in the single or multi-row format to get one or more predictions at a time.</span><span class="sxs-lookup"><span data-stu-id="e7a49-106">You can send data to the web service in the single or multi-row format to get one or more predictions at a time.</span></span>

<span data-ttu-id="e7a49-107">With the [Azure Machine Learning Web service](model-management-service-deploy.md), an external application synchronously communicates with a predictive model by making HTTP POST call to the service URL.</span><span class="sxs-lookup"><span data-stu-id="e7a49-107">With the [Azure Machine Learning Web service](model-management-service-deploy.md), an external application synchronously communicates with a predictive model by making HTTP POST call to the service URL.</span></span> <span data-ttu-id="e7a49-108">To make a web service call, the client application needs to specify the API key that is created when you deploy a prediction, and put the request data into the POST request body.</span><span class="sxs-lookup"><span data-stu-id="e7a49-108">To make a web service call, the client application needs to specify the API key that is created when you deploy a prediction, and put the request data into the POST request body.</span></span>

> [!NOTE]
> <span data-ttu-id="e7a49-109">Note that API keys are only available in the cluster deployment mode.</span><span class="sxs-lookup"><span data-stu-id="e7a49-109">Note that API keys are only available in the cluster deployment mode.</span></span> <span data-ttu-id="e7a49-110">Local web services do not have keys.</span><span class="sxs-lookup"><span data-stu-id="e7a49-110">Local web services do not have keys.</span></span>

## <a name="service-deployment-options"></a><span data-ttu-id="e7a49-111">Service deployment options</span><span class="sxs-lookup"><span data-stu-id="e7a49-111">Service deployment options</span></span>
<span data-ttu-id="e7a49-112">Azure Machine Learning Web services can be deployed to the cloud-based clusters for both production and test scenarios, and to local workstations using docker engine.</span><span class="sxs-lookup"><span data-stu-id="e7a49-112">Azure Machine Learning Web services can be deployed to the cloud-based clusters for both production and test scenarios, and to local workstations using docker engine.</span></span> <span data-ttu-id="e7a49-113">The functionality of the predictive model in both cases remains the same.</span><span class="sxs-lookup"><span data-stu-id="e7a49-113">The functionality of the predictive model in both cases remains the same.</span></span> <span data-ttu-id="e7a49-114">Cluster-based deployment provides scalable and performant solution based on Azure Container Services, while the local deployment can be used for debugging.</span><span class="sxs-lookup"><span data-stu-id="e7a49-114">Cluster-based deployment provides scalable and performant solution based on Azure Container Services, while the local deployment can be used for debugging.</span></span> 

<span data-ttu-id="e7a49-115">The Azure Machine Learning CLI and API provides convenient commands for creating and managing compute environments for service deployments using the ```az ml env``` option.</span><span class="sxs-lookup"><span data-stu-id="e7a49-115">The Azure Machine Learning CLI and API provides convenient commands for creating and managing compute environments for service deployments using the ```az ml env``` option.</span></span> 

## <a name="list-deployed-services-and-images"></a><span data-ttu-id="e7a49-116">List deployed services and images</span><span class="sxs-lookup"><span data-stu-id="e7a49-116">List deployed services and images</span></span>
<span data-ttu-id="e7a49-117">You can list the currently deployed services and Docker images using CLI command ```az ml service list realtime -o table```.</span><span class="sxs-lookup"><span data-stu-id="e7a49-117">You can list the currently deployed services and Docker images using CLI command ```az ml service list realtime -o table```.</span></span> <span data-ttu-id="e7a49-118">Note that this command always works in the context of the current compute environment.</span><span class="sxs-lookup"><span data-stu-id="e7a49-118">Note that this command always works in the context of the current compute environment.</span></span> <span data-ttu-id="e7a49-119">It would not show services that are deployed in an environment that is not set to be the current.</span><span class="sxs-lookup"><span data-stu-id="e7a49-119">It would not show services that are deployed in an environment that is not set to be the current.</span></span> <span data-ttu-id="e7a49-120">To set the environment use ```az ml env set```.</span><span class="sxs-lookup"><span data-stu-id="e7a49-120">To set the environment use ```az ml env set```.</span></span> 

## <a name="get-service-information"></a><span data-ttu-id="e7a49-121">Get service information</span><span class="sxs-lookup"><span data-stu-id="e7a49-121">Get service information</span></span>
<span data-ttu-id="e7a49-122">After the web service has been successfully deployed, use the following command to get the service URL and other details for calling the service endpoint.</span><span class="sxs-lookup"><span data-stu-id="e7a49-122">After the web service has been successfully deployed, use the following command to get the service URL and other details for calling the service endpoint.</span></span> 

```
az ml service usage realtime -i <web service id>
```

<span data-ttu-id="e7a49-123">This command prints out the service URL, required request headers, swagger URL, and sample data for calling the service if the service API schema was provided at the deployment time.</span><span class="sxs-lookup"><span data-stu-id="e7a49-123">This command prints out the service URL, required request headers, swagger URL, and sample data for calling the service if the service API schema was provided at the deployment time.</span></span>

<span data-ttu-id="e7a49-124">You can test the service directly from the CLI without composing an HTTP request, by entering the sample CLI command with the input data:</span><span class="sxs-lookup"><span data-stu-id="e7a49-124">You can test the service directly from the CLI without composing an HTTP request, by entering the sample CLI command with the input data:</span></span>

```
az ml service run realtime -i <web service id> -d "Your input data"
```

## <a name="get-the-service-api-key"></a><span data-ttu-id="e7a49-125">Get the service API key</span><span class="sxs-lookup"><span data-stu-id="e7a49-125">Get the service API key</span></span>
<span data-ttu-id="e7a49-126">To get the web service key, use the following command:</span><span class="sxs-lookup"><span data-stu-id="e7a49-126">To get the web service key, use the following command:</span></span>

```
az ml service keys realtime -i <web service id>
```
<span data-ttu-id="e7a49-127">When creating HTTP request, use the key in the authorization header: "Authorization": "Bearer <key>"</span><span class="sxs-lookup"><span data-stu-id="e7a49-127">When creating HTTP request, use the key in the authorization header: "Authorization": "Bearer <key>"</span></span>

## <a name="get-the-service-swagger-description"></a><span data-ttu-id="e7a49-128">Get the service Swagger description</span><span class="sxs-lookup"><span data-stu-id="e7a49-128">Get the service Swagger description</span></span>
<span data-ttu-id="e7a49-129">If the service API schema was supplied, the service endpoint would expose a Swagger document at ```http://<ip>/api/v1/service/<service name>/swagger.json```.</span><span class="sxs-lookup"><span data-stu-id="e7a49-129">If the service API schema was supplied, the service endpoint would expose a Swagger document at ```http://<ip>/api/v1/service/<service name>/swagger.json```.</span></span> <span data-ttu-id="e7a49-130">The Swagger document can be used to automatically generate the service client and explore the expected input data and other details about the service.</span><span class="sxs-lookup"><span data-stu-id="e7a49-130">The Swagger document can be used to automatically generate the service client and explore the expected input data and other details about the service.</span></span>

## <a name="get-service-logs"></a><span data-ttu-id="e7a49-131">Get service logs</span><span class="sxs-lookup"><span data-stu-id="e7a49-131">Get service logs</span></span>
<span data-ttu-id="e7a49-132">To understand the service behavior and diagnose problems, there are several ways to retrieve the service logs:</span><span class="sxs-lookup"><span data-stu-id="e7a49-132">To understand the service behavior and diagnose problems, there are several ways to retrieve the service logs:</span></span>
- <span data-ttu-id="e7a49-133">CLI command ```az ml service logs realtime -i <service id>```.</span><span class="sxs-lookup"><span data-stu-id="e7a49-133">CLI command ```az ml service logs realtime -i <service id>```.</span></span> <span data-ttu-id="e7a49-134">This command works in both cluster and local modes.</span><span class="sxs-lookup"><span data-stu-id="e7a49-134">This command works in both cluster and local modes.</span></span>
- <span data-ttu-id="e7a49-135">If the service logging was enabled at deployment, the service logs will also be sent to AppInsight.</span><span class="sxs-lookup"><span data-stu-id="e7a49-135">If the service logging was enabled at deployment, the service logs will also be sent to AppInsight.</span></span> <span data-ttu-id="e7a49-136">The CLI command ```az ml service usage realtime -i <service id>``` shows the AppInsight URL.</span><span class="sxs-lookup"><span data-stu-id="e7a49-136">The CLI command ```az ml service usage realtime -i <service id>``` shows the AppInsight URL.</span></span> <span data-ttu-id="e7a49-137">Note that the AppInsight logs may be delayed by 2-5 mins.</span><span class="sxs-lookup"><span data-stu-id="e7a49-137">Note that the AppInsight logs may be delayed by 2-5 mins.</span></span>
- <span data-ttu-id="e7a49-138">Cluster logs can be viewed through Kubernetes console that is connected when you set the current cluster environment with ```az ml env set```</span><span class="sxs-lookup"><span data-stu-id="e7a49-138">Cluster logs can be viewed through Kubernetes console that is connected when you set the current cluster environment with ```az ml env set```</span></span>
- <span data-ttu-id="e7a49-139">Local docker logs are available through the docker engine logs when the service is running locally.</span><span class="sxs-lookup"><span data-stu-id="e7a49-139">Local docker logs are available through the docker engine logs when the service is running locally.</span></span>

## <a name="call-the-service-using-c"></a><span data-ttu-id="e7a49-140">Call the service using C#</span><span class="sxs-lookup"><span data-stu-id="e7a49-140">Call the service using C#</span></span>
<span data-ttu-id="e7a49-141">Use the service URL to send a request from a C# Console App.</span><span class="sxs-lookup"><span data-stu-id="e7a49-141">Use the service URL to send a request from a C# Console App.</span></span> 

1. <span data-ttu-id="e7a49-142">In Visual Studio, create a new Console App:</span><span class="sxs-lookup"><span data-stu-id="e7a49-142">In Visual Studio, create a new Console App:</span></span> 
    * <span data-ttu-id="e7a49-143">In the menu, click, File -> New -> Project</span><span class="sxs-lookup"><span data-stu-id="e7a49-143">In the menu, click, File -> New -> Project</span></span>
    * <span data-ttu-id="e7a49-144">Under Visual Studio C#, click Windows Class Desktop, then select Console App.</span><span class="sxs-lookup"><span data-stu-id="e7a49-144">Under Visual Studio C#, click Windows Class Desktop, then select Console App.</span></span>
2. <span data-ttu-id="e7a49-145">Enter `MyFirstService` as the Name of the project, then click OK.</span><span class="sxs-lookup"><span data-stu-id="e7a49-145">Enter `MyFirstService` as the Name of the project, then click OK.</span></span>
3. <span data-ttu-id="e7a49-146">In Project References, set references to `System.Net`, and `System.Net.Http`.</span><span class="sxs-lookup"><span data-stu-id="e7a49-146">In Project References, set references to `System.Net`, and `System.Net.Http`.</span></span>
4. <span data-ttu-id="e7a49-147">Click Tools -> NuGet Package Manager -> Package Manager Console, then install the **Microsoft.AspNet.WebApi.Client** package.</span><span class="sxs-lookup"><span data-stu-id="e7a49-147">Click Tools -> NuGet Package Manager -> Package Manager Console, then install the **Microsoft.AspNet.WebApi.Client** package.</span></span>
5. <span data-ttu-id="e7a49-148">Open **Program.cs** file, and replace the code with the following code:</span><span class="sxs-lookup"><span data-stu-id="e7a49-148">Open **Program.cs** file, and replace the code with the following code:</span></span>
6. <span data-ttu-id="e7a49-149">Update the `SERVICE_URL` and `API_KEY` parameters with the information from your web service.</span><span class="sxs-lookup"><span data-stu-id="e7a49-149">Update the `SERVICE_URL` and `API_KEY` parameters with the information from your web service.</span></span>
7. <span data-ttu-id="e7a49-150">Run the project.</span><span class="sxs-lookup"><span data-stu-id="e7a49-150">Run the project.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Net.Http;
using System.Net.Http.Headers;
using Newtonsoft.Json;

namespace MyFirstService
{
    class Program
    {
        // Web Service URL (update it with your service url)
        private const string SERVICE_URL = "http://<service ip address>:80/api/v1/service/<service name>/score";
        private const string API_KEY = "your service key";

        static void Main(string[] args)
        {
            Program.PostRequest();
            Console.ReadLine();
        }

        private static void PostRequest()
        {
            HttpClient client = new HttpClient();
            client.BaseAddress = new Uri(SERVICE_URL);
            //For local web service, comment out this line.
            client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", API_KEY);

            var inputJson = new List<RequestPayload>();
            RequestPayload payload = new RequestPayload();
            List<InputDf> inputDf = new List<InputDf>();
            inputDf.Add(new InputDf()
            {
                feature1 = value1,
                feature2 = value2,
            });
            payload.Input_df_list = inputDf;
            inputJson.Add(payload);

            try
            {
                var request = new HttpRequestMessage(HttpMethod.Post, string.Empty);
                request.Content = new StringContent(JsonConvert.SerializeObject(payload));
                request.Content.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                var response = client.SendAsync(request).Result;

                Console.Write(response.Content.ReadAsStringAsync().Result);
            }
            catch (Exception e)
            {
                Console.Out.WriteLine(e.Message);
            }
        }
        public class InputDf
        {
            public double feature1 { get; set; }
            public double feature2 { get; set; }
        }
        public class RequestPayload
        {
            [JsonProperty("input_df")]
            public List<InputDf> Input_df_list { get; set; }
        }
    }
}
```

## <a name="call-the-web-service-using-python"></a><span data-ttu-id="e7a49-151">Call the web service using Python</span><span class="sxs-lookup"><span data-stu-id="e7a49-151">Call the web service using Python</span></span>
<span data-ttu-id="e7a49-152">Use Python to send a request to your real-time web service.</span><span class="sxs-lookup"><span data-stu-id="e7a49-152">Use Python to send a request to your real-time web service.</span></span> 

1. <span data-ttu-id="e7a49-153">Copy the following code sample to a new Python file.</span><span class="sxs-lookup"><span data-stu-id="e7a49-153">Copy the following code sample to a new Python file.</span></span>
2. <span data-ttu-id="e7a49-154">Update the data, url, and api_key parameters.</span><span class="sxs-lookup"><span data-stu-id="e7a49-154">Update the data, url, and api_key parameters.</span></span> <span data-ttu-id="e7a49-155">For local web services, remove the 'Authorization' header.</span><span class="sxs-lookup"><span data-stu-id="e7a49-155">For local web services, remove the 'Authorization' header.</span></span>
3. <span data-ttu-id="e7a49-156">Run the code.</span><span class="sxs-lookup"><span data-stu-id="e7a49-156">Run the code.</span></span> 

```python
import requests
import json

data = "{\"input_df\": [{\"feature1\": value1, \"feature2\": value2}]}"
body = str.encode(json.dumps(data))

url = 'http://<service ip address>:80/api/v1/service/<service name>/score'
api_key = 'your service key' 
headers = {'Content-Type':'application/json', 'Authorization':('Bearer '+ api_key)}

resp = requests.post(url, body, headers=headers)
resp.text
```
