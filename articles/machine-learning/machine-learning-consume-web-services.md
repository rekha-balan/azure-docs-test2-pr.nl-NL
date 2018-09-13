---
title: Consume a Machine Learning Web service | Microsoft Docs
description: Once a machine learning service is deployed, the RESTFul Web service that is made available can be consumed either as request-response service or as a batch execution service.
services: machine-learning
documentationcenter: ''
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 804f8211-9437-4982-98e9-ca841b7edf56
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 01/05/2017
ms.author: garye
ms.openlocfilehash: f4f3caed8390ba3a80d6cf1282f4d2751c67ae6b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540776"
---
# <a name="how-to-consume-an-azure-machine-learning-web-service-that-has-been-deployed-from-a-machine-learning-experiment"></a><span data-ttu-id="d99a9-103">How to consume an Azure Machine Learning Web service that has been deployed from a Machine Learning experiment</span><span class="sxs-lookup"><span data-stu-id="d99a9-103">How to consume an Azure Machine Learning Web service that has been deployed from a Machine Learning experiment</span></span>
## <a name="introduction"></a><span data-ttu-id="d99a9-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="d99a9-104">Introduction</span></span>
<span data-ttu-id="d99a9-105">When deployed as a Web service, Azure Machine Learning experiments provide a REST API and JSON formatted messages that can be consumed by a wide range of devices and platforms.</span><span class="sxs-lookup"><span data-stu-id="d99a9-105">When deployed as a Web service, Azure Machine Learning experiments provide a REST API and JSON formatted messages that can be consumed by a wide range of devices and platforms.</span></span> <span data-ttu-id="d99a9-106">The Azure Machine Learning portal provides code that can be used to call the Web service in R, C#, and Python.</span><span class="sxs-lookup"><span data-stu-id="d99a9-106">The Azure Machine Learning portal provides code that can be used to call the Web service in R, C#, and Python.</span></span> 

<span data-ttu-id="d99a9-107">Services can be called with any programming language and from any device that satisfies three criteria:</span><span class="sxs-lookup"><span data-stu-id="d99a9-107">Services can be called with any programming language and from any device that satisfies three criteria:</span></span>

* <span data-ttu-id="d99a9-108">Has a network connection</span><span class="sxs-lookup"><span data-stu-id="d99a9-108">Has a network connection</span></span>
* <span data-ttu-id="d99a9-109">Has SSL capabilities to perform HTTPS requests</span><span class="sxs-lookup"><span data-stu-id="d99a9-109">Has SSL capabilities to perform HTTPS requests</span></span>
* <span data-ttu-id="d99a9-110">Can parse JSON (directly or with support libraries)</span><span class="sxs-lookup"><span data-stu-id="d99a9-110">Can parse JSON (directly or with support libraries)</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="d99a9-111">An Azure Machine Learning Web service can be consumed in two ways, either as a Request-Response Service or as a Batch Execution Service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-111">An Azure Machine Learning Web service can be consumed in two ways, either as a Request-Response Service or as a Batch Execution Service.</span></span> <span data-ttu-id="d99a9-112">In each scenario, the functionality is provided through the RESTFul Web service that is made available for consumption once you deploy the experiment.</span><span class="sxs-lookup"><span data-stu-id="d99a9-112">In each scenario, the functionality is provided through the RESTFul Web service that is made available for consumption once you deploy the experiment.</span></span>

> [!TIP]
> <span data-ttu-id="d99a9-113">For a simple way to create a web app to access your predictive Web service, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span><span class="sxs-lookup"><span data-stu-id="d99a9-113">For a simple way to create a web app to access your predictive Web service, see [Consume an Azure Machine Learning Web service with a web app template](machine-learning-consume-web-service-with-web-app-template.md).</span></span>
> 
> 
> <span data-ttu-id="d99a9-114">For information about how to create and deploy an Azure Machine Learning Web service, see [Deploy an Azure Machine Learning Web service][publish].</span><span class="sxs-lookup"><span data-stu-id="d99a9-114">For information about how to create and deploy an Azure Machine Learning Web service, see [Deploy an Azure Machine Learning Web service][publish].</span></span> <span data-ttu-id="d99a9-115">For a step-by-step walkthrough of creating a Machine Learning experiment and deploying it, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span><span class="sxs-lookup"><span data-stu-id="d99a9-115">For a step-by-step walkthrough of creating a Machine Learning experiment and deploying it, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

## <a name="request-response-service-rrs"></a><span data-ttu-id="d99a9-116">Request-Response Service (RRS)</span><span class="sxs-lookup"><span data-stu-id="d99a9-116">Request-Response Service (RRS)</span></span>
<span data-ttu-id="d99a9-117">A Request-Response Service (RRS) is a low-latency, highly scalable Web service used to provide an interface to the stateless models that have been created and deployed from an Azure Machine Learning Studio experiment.</span><span class="sxs-lookup"><span data-stu-id="d99a9-117">A Request-Response Service (RRS) is a low-latency, highly scalable Web service used to provide an interface to the stateless models that have been created and deployed from an Azure Machine Learning Studio experiment.</span></span> <span data-ttu-id="d99a9-118">It enables scenarios where the consuming application expects a response in real time.</span><span class="sxs-lookup"><span data-stu-id="d99a9-118">It enables scenarios where the consuming application expects a response in real time.</span></span>

<span data-ttu-id="d99a9-119">RRS accepts a single row, or multiple rows, of input parameters and can generate a single row, or multiple rows, as output.</span><span class="sxs-lookup"><span data-stu-id="d99a9-119">RRS accepts a single row, or multiple rows, of input parameters and can generate a single row, or multiple rows, as output.</span></span> <span data-ttu-id="d99a9-120">The output row(s) can contain multiple columns.</span><span class="sxs-lookup"><span data-stu-id="d99a9-120">The output row(s) can contain multiple columns.</span></span>

<span data-ttu-id="d99a9-121">An example for RRS is validating the authenticity of an application.</span><span class="sxs-lookup"><span data-stu-id="d99a9-121">An example for RRS is validating the authenticity of an application.</span></span> <span data-ttu-id="d99a9-122">Hundreds to millions of installations of an application can be expected in this case.</span><span class="sxs-lookup"><span data-stu-id="d99a9-122">Hundreds to millions of installations of an application can be expected in this case.</span></span> <span data-ttu-id="d99a9-123">When the application starts up, it calls the RRS service with the relevant input.</span><span class="sxs-lookup"><span data-stu-id="d99a9-123">When the application starts up, it calls the RRS service with the relevant input.</span></span> <span data-ttu-id="d99a9-124">The application then receives a validation response from the service that either allows or blocks the application from performing.</span><span class="sxs-lookup"><span data-stu-id="d99a9-124">The application then receives a validation response from the service that either allows or blocks the application from performing.</span></span>

## <a name="batch-execution-service-bes"></a><span data-ttu-id="d99a9-125">Batch Execution Service (BES)</span><span class="sxs-lookup"><span data-stu-id="d99a9-125">Batch Execution Service (BES)</span></span>
<span data-ttu-id="d99a9-126">A Batch Execution Service (BES) is a service that handles high volume, asynchronous, scoring of a batch of data records.</span><span class="sxs-lookup"><span data-stu-id="d99a9-126">A Batch Execution Service (BES) is a service that handles high volume, asynchronous, scoring of a batch of data records.</span></span> <span data-ttu-id="d99a9-127">The input for the BES contains a batch of records from various sources, such as blobs, tables in Azure, SQL Azure, HDInsight (results of a Hive Query, for example), and HTTP sources.</span><span class="sxs-lookup"><span data-stu-id="d99a9-127">The input for the BES contains a batch of records from various sources, such as blobs, tables in Azure, SQL Azure, HDInsight (results of a Hive Query, for example), and HTTP sources.</span></span> <span data-ttu-id="d99a9-128">The output for the BES contains the results of the scoring.</span><span class="sxs-lookup"><span data-stu-id="d99a9-128">The output for the BES contains the results of the scoring.</span></span> <span data-ttu-id="d99a9-129">Results are output to a file in Azure blob storage and data from the storage endpoint is returned in the response.</span><span class="sxs-lookup"><span data-stu-id="d99a9-129">Results are output to a file in Azure blob storage and data from the storage endpoint is returned in the response.</span></span>

<span data-ttu-id="d99a9-130">A BES would be useful when responses are not needed immediately, such as for regularly scheduled scoring for individuals or internet of things (IOT) devices.</span><span class="sxs-lookup"><span data-stu-id="d99a9-130">A BES would be useful when responses are not needed immediately, such as for regularly scheduled scoring for individuals or internet of things (IOT) devices.</span></span>

## <a name="examples"></a><span data-ttu-id="d99a9-131">Examples</span><span class="sxs-lookup"><span data-stu-id="d99a9-131">Examples</span></span>
<span data-ttu-id="d99a9-132">To show how both RRS and BES work, we use an example Azure Web service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-132">To show how both RRS and BES work, we use an example Azure Web service.</span></span> <span data-ttu-id="d99a9-133">This service would be used in an IOT (Internet Of Things) scenario.</span><span class="sxs-lookup"><span data-stu-id="d99a9-133">This service would be used in an IOT (Internet Of Things) scenario.</span></span> <span data-ttu-id="d99a9-134">To keep it simple, our device only sends up one value, `cog_speed`, and gets a single answer back.</span><span class="sxs-lookup"><span data-stu-id="d99a9-134">To keep it simple, our device only sends up one value, `cog_speed`, and gets a single answer back.</span></span>

<span data-ttu-id="d99a9-135">Once the experiment has been deployed, there are four pieces of information that we need to call either the RRS or BES service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-135">Once the experiment has been deployed, there are four pieces of information that we need to call either the RRS or BES service.</span></span>

* <span data-ttu-id="d99a9-136">The service **API key** or **Primary key**</span><span class="sxs-lookup"><span data-stu-id="d99a9-136">The service **API key** or **Primary key**</span></span>
* <span data-ttu-id="d99a9-137">The service **request URI**</span><span class="sxs-lookup"><span data-stu-id="d99a9-137">The service **request URI**</span></span>
* <span data-ttu-id="d99a9-138">The expected API **request headers** and **body**</span><span class="sxs-lookup"><span data-stu-id="d99a9-138">The expected API **request headers** and **body**</span></span>
* <span data-ttu-id="d99a9-139">The expected API **response headers** and **body**</span><span class="sxs-lookup"><span data-stu-id="d99a9-139">The expected API **response headers** and **body**</span></span>

<span data-ttu-id="d99a9-140">The manner in which you find this information depends on what type of service you deployed: A New Web service or a Classic Web Service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-140">The manner in which you find this information depends on what type of service you deployed: A New Web service or a Classic Web Service.</span></span>

### <a name="information-location-in-the-azure-machine-learning-web-services-portal"></a><span data-ttu-id="d99a9-141">Information location in the Azure Machine Learning Web Services portal</span><span class="sxs-lookup"><span data-stu-id="d99a9-141">Information location in the Azure Machine Learning Web Services portal</span></span>
<span data-ttu-id="d99a9-142">To find the needed information:</span><span class="sxs-lookup"><span data-stu-id="d99a9-142">To find the needed information:</span></span>

1. <span data-ttu-id="d99a9-143">Sign in to the [Azure Machine Learning Web Services][webservicesportal] portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-143">Sign in to the [Azure Machine Learning Web Services][webservicesportal] portal.</span></span>
2. <span data-ttu-id="d99a9-144">Click **Web Services** or **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="d99a9-144">Click **Web Services** or **Classic Web Services**.</span></span>
3. <span data-ttu-id="d99a9-145">Click the Web service with which you working.</span><span class="sxs-lookup"><span data-stu-id="d99a9-145">Click the Web service with which you working.</span></span> 
4. <span data-ttu-id="d99a9-146">If you are working with a Classic Web Service, click the endpoint you are working with.</span><span class="sxs-lookup"><span data-stu-id="d99a9-146">If you are working with a Classic Web Service, click the endpoint you are working with.</span></span>

<span data-ttu-id="d99a9-147">The information is located on these pages:</span><span class="sxs-lookup"><span data-stu-id="d99a9-147">The information is located on these pages:</span></span>

* <span data-ttu-id="d99a9-148">The **Primary key** is available on the **Consume** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-148">The **Primary key** is available on the **Consume** page</span></span>
* <span data-ttu-id="d99a9-149">The **request URI** is available on the **Consume** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-149">The **request URI** is available on the **Consume** page</span></span> 
* <span data-ttu-id="d99a9-150">The expected API **request headers**, **response headers**, and **body** are available on the **Swagger API** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-150">The expected API **request headers**, **response headers**, and **body** are available on the **Swagger API** page</span></span>

### <a name="information-locations-in-machine-learning-studio-classic-web-service-only"></a><span data-ttu-id="d99a9-151">Information locations in Machine Learning Studio (Classic Web service only)</span><span class="sxs-lookup"><span data-stu-id="d99a9-151">Information locations in Machine Learning Studio (Classic Web service only)</span></span>
<span data-ttu-id="d99a9-152">You can find the needed information from two locations: Machine Learning Studio or the Azure Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-152">You can find the needed information from two locations: Machine Learning Studio or the Azure Machine Learning Web Services portal.</span></span>

<span data-ttu-id="d99a9-153">To find the needed information in Machine Learning studio:</span><span class="sxs-lookup"><span data-stu-id="d99a9-153">To find the needed information in Machine Learning studio:</span></span>

1. <span data-ttu-id="d99a9-154">Sign in to [Machine Learning Studio][mlstudio].</span><span class="sxs-lookup"><span data-stu-id="d99a9-154">Sign in to [Machine Learning Studio][mlstudio].</span></span>
2. <span data-ttu-id="d99a9-155">On the left of the screen, click **WEB SERVICES**.</span><span class="sxs-lookup"><span data-stu-id="d99a9-155">On the left of the screen, click **WEB SERVICES**.</span></span>
3. <span data-ttu-id="d99a9-156">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="d99a9-156">Click the Web service with which you are working.</span></span> 

<span data-ttu-id="d99a9-157">The information is located on these pages:</span><span class="sxs-lookup"><span data-stu-id="d99a9-157">The information is located on these pages:</span></span>

* <span data-ttu-id="d99a9-158">The **API key** is available on the service **Dashboard**</span><span class="sxs-lookup"><span data-stu-id="d99a9-158">The **API key** is available on the service **Dashboard**</span></span> 
* <span data-ttu-id="d99a9-159">The **request URI** is available on the API help page</span><span class="sxs-lookup"><span data-stu-id="d99a9-159">The **request URI** is available on the API help page</span></span>
* <span data-ttu-id="d99a9-160">The expected API **request headers**, **response headers**, and **body** are available on the API help page</span><span class="sxs-lookup"><span data-stu-id="d99a9-160">The expected API **request headers**, **response headers**, and **body** are available on the API help page</span></span>

<span data-ttu-id="d99a9-161">To access the API help page, click either the **REQUEST/RESPONSE** or **BATCH EXECUTION** link as appropriate to your task.</span><span class="sxs-lookup"><span data-stu-id="d99a9-161">To access the API help page, click either the **REQUEST/RESPONSE** or **BATCH EXECUTION** link as appropriate to your task.</span></span>

<span data-ttu-id="d99a9-162">To find the needed information on the Azure Machine Learning Web Services portal:</span><span class="sxs-lookup"><span data-stu-id="d99a9-162">To find the needed information on the Azure Machine Learning Web Services portal:</span></span>

1. <span data-ttu-id="d99a9-163">Sign in to the [Azure Machine Learning Web Services][webservicesportal] portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-163">Sign in to the [Azure Machine Learning Web Services][webservicesportal] portal.</span></span>
2. <span data-ttu-id="d99a9-164">Click **Classic Web Services**.</span><span class="sxs-lookup"><span data-stu-id="d99a9-164">Click **Classic Web Services**.</span></span>
3. <span data-ttu-id="d99a9-165">Click the Web service with which you are working.</span><span class="sxs-lookup"><span data-stu-id="d99a9-165">Click the Web service with which you are working.</span></span> 
4. <span data-ttu-id="d99a9-166">Click the endpoint with which you are working.</span><span class="sxs-lookup"><span data-stu-id="d99a9-166">Click the endpoint with which you are working.</span></span>

<span data-ttu-id="d99a9-167">The information is located on these pages:</span><span class="sxs-lookup"><span data-stu-id="d99a9-167">The information is located on these pages:</span></span>

* <span data-ttu-id="d99a9-168">The **Primary key** is available on the **Consume** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-168">The **Primary key** is available on the **Consume** page</span></span>
* <span data-ttu-id="d99a9-169">The **request URI** is available on the **Consume** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-169">The **request URI** is available on the **Consume** page</span></span> 
* <span data-ttu-id="d99a9-170">The expected API **request headers**, **response headers**, and **body** are available on the **Swagger API** page</span><span class="sxs-lookup"><span data-stu-id="d99a9-170">The expected API **request headers**, **response headers**, and **body** are available on the **Swagger API** page</span></span>

<span data-ttu-id="d99a9-171">In the two examples below, the C# language is used to illustrate the code needed.</span><span class="sxs-lookup"><span data-stu-id="d99a9-171">In the two examples below, the C# language is used to illustrate the code needed.</span></span>

### <a name="rrs-example"></a><span data-ttu-id="d99a9-172">RRS Example</span><span class="sxs-lookup"><span data-stu-id="d99a9-172">RRS Example</span></span>
<span data-ttu-id="d99a9-173">The following sample request shows the API input the payload for the API call of our sample service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-173">The following sample request shows the API input the payload for the API call of our sample service.</span></span> <span data-ttu-id="d99a9-174">For a Classic Web service, you can find payload samples on the **API help page** or on the **Swagger API** page of the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-174">For a Classic Web service, you can find payload samples on the **API help page** or on the **Swagger API** page of the Machine Learning Web Services portal.</span></span> <span data-ttu-id="d99a9-175">For a New Web service, you can find payload samples on the **Swagger API** page of the Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-175">For a New Web service, you can find payload samples on the **Swagger API** page of the Machine Learning Web Services portal.</span></span>

<span data-ttu-id="d99a9-176">**Sample Request**</span><span class="sxs-lookup"><span data-stu-id="d99a9-176">**Sample Request**</span></span>

    {
      "Inputs": {
        "input1": {
          "ColumnNames": [
            "cog_speed"
          ],
          "Values": [
            [
              "0"
            ],
            [
              "1"
            ]
          ]
        }
      },
      "GlobalParameters": {}
    }


<span data-ttu-id="d99a9-177">Similarly, the following sample shows the API response for the service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-177">Similarly, the following sample shows the API response for the service.</span></span>

<span data-ttu-id="d99a9-178">**Sample Response**</span><span class="sxs-lookup"><span data-stu-id="d99a9-178">**Sample Response**</span></span>

    {
      "Results": {
        "output1": {
          "type": "DataTable",
          "value": {
            "ColumnNames": [
              "cog_speed"
            ],
            "ColumnTypes": [
              "Numeric"
            ].
          "Values": [
            [
              "0"
            ],
            [
              "1"
            ]
          ]
        }
      },
      "GlobalParameters": {}
    }

<span data-ttu-id="d99a9-179">The following is the code sample for the C# implementation.</span><span class="sxs-lookup"><span data-stu-id="d99a9-179">The following is the code sample for the C# implementation.</span></span> <span data-ttu-id="d99a9-180">For a Classic Web service, you can find code samples at the bottom of the **API help page** or at the bottom of the **Consume** page.</span><span class="sxs-lookup"><span data-stu-id="d99a9-180">For a Classic Web service, you can find code samples at the bottom of the **API help page** or at the bottom of the **Consume** page.</span></span> <span data-ttu-id="d99a9-181">For a New Web service, you can find code samples at the bottom of the **Consume** page.</span><span class="sxs-lookup"><span data-stu-id="d99a9-181">For a New Web service, you can find code samples at the bottom of the **Consume** page.</span></span>

<span data-ttu-id="d99a9-182">**Sample Code in C#**</span><span class="sxs-lookup"><span data-stu-id="d99a9-182">**Sample Code in C#**</span></span>

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
        public class StringTable
        {
            public string[] ColumnNames { get; set; }
            public string[,] Values { get; set; }
        }

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
                        Inputs = new Dictionary<string, StringTable> () {
                            {
                                "input1",
                                new StringTable()
                                {
                                    ColumnNames = new string[] {"cog_speed"},
                                    Values = new string[,] {  { "0"},  { "1"}  }
                                }
                            },
                        GlobalParameters = new Dictionary<string, string>() { }
                    };

                    const string apiKey = "abc123"; // Replace this with the API key for the Web service
                    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue( "Bearer", apiKey);

                    client.BaseAddress = new Uri("https://ussouthcentral.services.azureml.net/workspaces/<workspace id>/services/<service id>/execute?api-version=2.0&details=true");

                    // WARNING: The 'await' statement below can result in a deadlock if you are calling this code from the UI thread of an ASP.Net application.
                    // One way to address this would be to call ConfigureAwait(false) so that the execution does not attempt to resume on the original context.
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
                        Console.WriteLine("Failed with status code: {0}", response.StatusCode);
                    }
                }
            }
        }
    }

<span data-ttu-id="d99a9-183">**Sample Code in Java**</span><span class="sxs-lookup"><span data-stu-id="d99a9-183">**Sample Code in Java**</span></span>

<span data-ttu-id="d99a9-184">The following sample code shows how to construct a REST API request in Java.</span><span class="sxs-lookup"><span data-stu-id="d99a9-184">The following sample code shows how to construct a REST API request in Java.</span></span> <span data-ttu-id="d99a9-185">It assumes that the variables (apikey and apiurl) have the necessary API details and the variable jsonBody has a correct JSON object as expected by the REST API.</span><span class="sxs-lookup"><span data-stu-id="d99a9-185">It assumes that the variables (apikey and apiurl) have the necessary API details and the variable jsonBody has a correct JSON object as expected by the REST API.</span></span> <span data-ttu-id="d99a9-186">You can download the full code from github - [https://github.com/nk773/AzureML_RRSApp](https://github.com/nk773/AzureML_RRSApp).</span><span class="sxs-lookup"><span data-stu-id="d99a9-186">You can download the full code from github - [https://github.com/nk773/AzureML_RRSApp](https://github.com/nk773/AzureML_RRSApp).</span></span> <span data-ttu-id="d99a9-187">This Java sample requires [apache http client library](https://hc.apache.org/downloads.cgi).</span><span class="sxs-lookup"><span data-stu-id="d99a9-187">This Java sample requires [apache http client library](https://hc.apache.org/downloads.cgi).</span></span>

    /**
     * Download full code from github - [https://github.com/nk773/AzureML_RRSApp](https://github.com/nk773/AzureML_RRSApp)
      */
        /**
           * Call REST API for retrieving prediction from Azure ML 
           * @return response from the REST API
           */    
        public static String rrsHttpPost() {

            HttpPost post;
            HttpClient client;
            StringEntity entity;

            try {
                    // create HttpPost and HttpClient object
                    post = new HttpPost(apiurl);
                    client = HttpClientBuilder.create().build();

                    // setup output message by copying JSON body into 
                    // apache StringEntity object along with content type
                    entity = new StringEntity(jsonBody, HTTP.UTF_8);
                    entity.setContentEncoding(HTTP.UTF_8);
                    entity.setContentType("text/json");

                    // add HTTP headers
                    post.setHeader("Accept", "text/json");
                    post.setHeader("Accept-Charset", "UTF-8");

                    // set Authorization header based on the API key
                    post.setHeader("Authorization", ("Bearer "+apikey));
                    post.setEntity(entity);

                    // Call REST API and retrieve response content
                    HttpResponse authResponse = client.execute(post);

                    return EntityUtils.toString(authResponse.getEntity());

            }
            catch (Exception e) {

                    return e.toString();
            }

        }




### <a name="bes-example"></a><span data-ttu-id="d99a9-188">BES Example</span><span class="sxs-lookup"><span data-stu-id="d99a9-188">BES Example</span></span>
<span data-ttu-id="d99a9-189">Unlike the RRS service, the BES service is asynchronous.</span><span class="sxs-lookup"><span data-stu-id="d99a9-189">Unlike the RRS service, the BES service is asynchronous.</span></span> <span data-ttu-id="d99a9-190">This means that the BES API is simply queuing up a job to be executed, and the caller polls the job's status to see when it has completed.</span><span class="sxs-lookup"><span data-stu-id="d99a9-190">This means that the BES API is simply queuing up a job to be executed, and the caller polls the job's status to see when it has completed.</span></span> <span data-ttu-id="d99a9-191">Here are the operations currently supported for batch jobs:</span><span class="sxs-lookup"><span data-stu-id="d99a9-191">Here are the operations currently supported for batch jobs:</span></span>

1. <span data-ttu-id="d99a9-192">Create (submit) a batch job</span><span class="sxs-lookup"><span data-stu-id="d99a9-192">Create (submit) a batch job</span></span>
2. <span data-ttu-id="d99a9-193">Start this batch job</span><span class="sxs-lookup"><span data-stu-id="d99a9-193">Start this batch job</span></span>
3. <span data-ttu-id="d99a9-194">Get the status or result of the batch job</span><span class="sxs-lookup"><span data-stu-id="d99a9-194">Get the status or result of the batch job</span></span>
4. <span data-ttu-id="d99a9-195">Cancel a running batch job</span><span class="sxs-lookup"><span data-stu-id="d99a9-195">Cancel a running batch job</span></span>

<span data-ttu-id="d99a9-196">**1. Create a Batch Execution Job**</span><span class="sxs-lookup"><span data-stu-id="d99a9-196">**1. Create a Batch Execution Job**</span></span>

<span data-ttu-id="d99a9-197">When you create a batch job for your Azure Machine Learning service, you can specify several parameters that define the batch execution:</span><span class="sxs-lookup"><span data-stu-id="d99a9-197">When you create a batch job for your Azure Machine Learning service, you can specify several parameters that define the batch execution:</span></span>

* <span data-ttu-id="d99a9-198">**Input**: Represents a blob reference where the batch job's input is stored.</span><span class="sxs-lookup"><span data-stu-id="d99a9-198">**Input**: Represents a blob reference where the batch job's input is stored.</span></span>
* <span data-ttu-id="d99a9-199">**GlobalParameters**: Represents the set of global parameters that you can define for their experiment.</span><span class="sxs-lookup"><span data-stu-id="d99a9-199">**GlobalParameters**: Represents the set of global parameters that you can define for their experiment.</span></span> <span data-ttu-id="d99a9-200">An Azure Machine Learning experiment can have both required and optional parameters that customize the service's execution, and the caller is expected to provide all required parameters, if applicable.</span><span class="sxs-lookup"><span data-stu-id="d99a9-200">An Azure Machine Learning experiment can have both required and optional parameters that customize the service's execution, and the caller is expected to provide all required parameters, if applicable.</span></span> <span data-ttu-id="d99a9-201">These parameters are specified as a collection of key-value pairs.</span><span class="sxs-lookup"><span data-stu-id="d99a9-201">These parameters are specified as a collection of key-value pairs.</span></span>
* <span data-ttu-id="d99a9-202">**Outputs**: If the service has defined one or more outputs, the caller can redirect any of them to an Azure blob location.</span><span class="sxs-lookup"><span data-stu-id="d99a9-202">**Outputs**: If the service has defined one or more outputs, the caller can redirect any of them to an Azure blob location.</span></span> <span data-ttu-id="d99a9-203">By setting this parameter, you can save the output of the service in a preferred location and under a predictable name, otherwise the output blob name is randomly generated.</span><span class="sxs-lookup"><span data-stu-id="d99a9-203">By setting this parameter, you can save the output of the service in a preferred location and under a predictable name, otherwise the output blob name is randomly generated.</span></span> 
  
    <span data-ttu-id="d99a9-204">The service expects the output content, based on its type, to be saved as supported formats:</span><span class="sxs-lookup"><span data-stu-id="d99a9-204">The service expects the output content, based on its type, to be saved as supported formats:</span></span>
  
  * <span data-ttu-id="d99a9-205">dataset outputs: can be saved as **.csv, .tsv, .arff**</span><span class="sxs-lookup"><span data-stu-id="d99a9-205">dataset outputs: can be saved as **.csv, .tsv, .arff**</span></span>
  * <span data-ttu-id="d99a9-206">trained model outputs: Must be saved as **.ilearner**</span><span class="sxs-lookup"><span data-stu-id="d99a9-206">trained model outputs: Must be saved as **.ilearner**</span></span>
    
    <span data-ttu-id="d99a9-207">You specify the Output location overrides as a collection of output name, or blob reference pairs.</span><span class="sxs-lookup"><span data-stu-id="d99a9-207">You specify the Output location overrides as a collection of output name, or blob reference pairs.</span></span> <span data-ttu-id="d99a9-208">The *output name* is the user-defined name for a specific output node, and *blob reference* is a reference to an Azure blob location to which the output is redirected.</span><span class="sxs-lookup"><span data-stu-id="d99a9-208">The *output name* is the user-defined name for a specific output node, and *blob reference* is a reference to an Azure blob location to which the output is redirected.</span></span> <span data-ttu-id="d99a9-209">The *output name* is shown on the service's API help page.</span><span class="sxs-lookup"><span data-stu-id="d99a9-209">The *output name* is shown on the service's API help page.</span></span>

<span data-ttu-id="d99a9-210">All the job creation parameters are optional depending on the nature of your service.</span><span class="sxs-lookup"><span data-stu-id="d99a9-210">All the job creation parameters are optional depending on the nature of your service.</span></span> <span data-ttu-id="d99a9-211">For example, services with no input node defined do not require passing in an *Input* parameter.</span><span class="sxs-lookup"><span data-stu-id="d99a9-211">For example, services with no input node defined do not require passing in an *Input* parameter.</span></span> <span data-ttu-id="d99a9-212">Likewise, the output location override feature is optional, as outputs are otherwise stored in the default storage account that was set up for your Azure Machine Learning workspace.</span><span class="sxs-lookup"><span data-stu-id="d99a9-212">Likewise, the output location override feature is optional, as outputs are otherwise stored in the default storage account that was set up for your Azure Machine Learning workspace.</span></span> <span data-ttu-id="d99a9-213">The following sample request payloads for a service where only the input information is provided:</span><span class="sxs-lookup"><span data-stu-id="d99a9-213">The following sample request payloads for a service where only the input information is provided:</span></span>

<span data-ttu-id="d99a9-214">**Sample Request**</span><span class="sxs-lookup"><span data-stu-id="d99a9-214">**Sample Request**</span></span>

    {
      "Input": {
        "ConnectionString":     
        "DefaultEndpointsProtocol=https;AccountName=mystorageacct;AccountKey=mystorageacctKey",
        "RelativeLocation": "/mycontainer/mydatablob.csv",
        "BaseLocation": null,
        "SasBlobToken": null
      },
      "Outputs": null,
      "GlobalParameters": null
    }

<span data-ttu-id="d99a9-215">The response to the batch job creation API is the unique job ID that is associated with your job.</span><span class="sxs-lookup"><span data-stu-id="d99a9-215">The response to the batch job creation API is the unique job ID that is associated with your job.</span></span> <span data-ttu-id="d99a9-216">This ID is important since it provides the only means for you to reference this job in the system for other operations.</span><span class="sxs-lookup"><span data-stu-id="d99a9-216">This ID is important since it provides the only means for you to reference this job in the system for other operations.</span></span>  

<span data-ttu-id="d99a9-217">**Sample Response**</span><span class="sxs-lookup"><span data-stu-id="d99a9-217">**Sample Response**</span></span>

    "539d0bc2fde945b6ac986b851d0000f0" // The JOB_ID

<span data-ttu-id="d99a9-218">**2. Start a Batch Execution Job**</span><span class="sxs-lookup"><span data-stu-id="d99a9-218">**2. Start a Batch Execution Job**</span></span>

<span data-ttu-id="d99a9-219">When you Create a batch job it is registered in the system and places it in a *Not started* state.</span><span class="sxs-lookup"><span data-stu-id="d99a9-219">When you Create a batch job it is registered in the system and places it in a *Not started* state.</span></span> <span data-ttu-id="d99a9-220">To actually schedule the job for execution, you call the **start** API described on the service endpoint's API help page or the Web service's Swagger API page, and provide the job ID obtained when the job was created.</span><span class="sxs-lookup"><span data-stu-id="d99a9-220">To actually schedule the job for execution, you call the **start** API described on the service endpoint's API help page or the Web service's Swagger API page, and provide the job ID obtained when the job was created.</span></span>

<span data-ttu-id="d99a9-221">**3. Get the Status of a Batch Execution Job**</span><span class="sxs-lookup"><span data-stu-id="d99a9-221">**3. Get the Status of a Batch Execution Job**</span></span>

<span data-ttu-id="d99a9-222">You can poll the status of your asynchronous batch job at any time by passing the job's ID to the *GetJobStatus* API.</span><span class="sxs-lookup"><span data-stu-id="d99a9-222">You can poll the status of your asynchronous batch job at any time by passing the job's ID to the *GetJobStatus* API.</span></span> <span data-ttu-id="d99a9-223">The API response contains an indicator of the job's current state and the results of the batch job indicating whether it has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="d99a9-223">The API response contains an indicator of the job's current state and the results of the batch job indicating whether it has completed successfully.</span></span> <span data-ttu-id="d99a9-224">If there is an error, more information about the actual reason behind the failure is returned in the *Details* property, as shown here:</span><span class="sxs-lookup"><span data-stu-id="d99a9-224">If there is an error, more information about the actual reason behind the failure is returned in the *Details* property, as shown here:</span></span>

<span data-ttu-id="d99a9-225">**Response Payload**</span><span class="sxs-lookup"><span data-stu-id="d99a9-225">**Response Payload**</span></span>

    {
        "StatusCode": STATUS_CODE,
        "Results": RESULTS,
        "Details": DETAILS
    }

<span data-ttu-id="d99a9-226">*StatusCode* can be one of the following:</span><span class="sxs-lookup"><span data-stu-id="d99a9-226">*StatusCode* can be one of the following:</span></span>

* <span data-ttu-id="d99a9-227">Not started</span><span class="sxs-lookup"><span data-stu-id="d99a9-227">Not started</span></span>
* <span data-ttu-id="d99a9-228">Running</span><span class="sxs-lookup"><span data-stu-id="d99a9-228">Running</span></span>
* <span data-ttu-id="d99a9-229">Failed</span><span class="sxs-lookup"><span data-stu-id="d99a9-229">Failed</span></span>
* <span data-ttu-id="d99a9-230">Canceled</span><span class="sxs-lookup"><span data-stu-id="d99a9-230">Canceled</span></span>
* <span data-ttu-id="d99a9-231">Finished</span><span class="sxs-lookup"><span data-stu-id="d99a9-231">Finished</span></span>

<span data-ttu-id="d99a9-232">The *Results* property is populated when the job has successfully completed (it is **null** otherwise.) Once the job has completed, and if the service has at least one output node defined, the results are returned as a collection of *[output name, blob reference]* pairs, where the blob reference is a SAS read-only reference to the blob containing the result.</span><span class="sxs-lookup"><span data-stu-id="d99a9-232">The *Results* property is populated when the job has successfully completed (it is **null** otherwise.) Once the job has completed, and if the service has at least one output node defined, the results are returned as a collection of *[output name, blob reference]* pairs, where the blob reference is a SAS read-only reference to the blob containing the result.</span></span>

<span data-ttu-id="d99a9-233">**Sample Response**</span><span class="sxs-lookup"><span data-stu-id="d99a9-233">**Sample Response**</span></span>

    {
        "Status Code": "Finished",
        "Results":
        {
            "dataOutput":
            {              
                "ConnectionString": null,
                "RelativeLocation": "outputs/dataOutput.csv",
                "BaseLocation": "https://mystorageaccount.blob.core.windows.net/",
                "SasBlobToken": "?sv=2013-08-15&sr=b&sig=ABCD&st=2015-04-04T05%3A39%3A55Z&se=2015-04-05T05%3A44%3A55Z&sp=r"              
            },
            "trainedModelOutput":
            {              
                "ConnectionString": null,
                "RelativeLocation": "models/trainedModel.ilearner",
                "BaseLocation": "https://mystorageaccount.blob.core.windows.net/",
                "SasBlobToken": "?sv=2013-08-15&sr=b&sig=EFGH%3D&st=2015-04-04T05%3A39%3A55Z&se=2015-04-05T05%3A44%3A55Z&sp=r"              
            },           
        },
        "Details": null
    }

<span data-ttu-id="d99a9-234">**4. Cancel a Batch Execution Job**</span><span class="sxs-lookup"><span data-stu-id="d99a9-234">**4. Cancel a Batch Execution Job**</span></span>

<span data-ttu-id="d99a9-235">You can cancel a running batch job at any time by calling the designated *CancelJob* API and passing in the job's id. You might cancel for various reasons such as the job is taking too long to complete.</span><span class="sxs-lookup"><span data-stu-id="d99a9-235">You can cancel a running batch job at any time by calling the designated *CancelJob* API and passing in the job's id. You might cancel for various reasons such as the job is taking too long to complete.</span></span>

#### <a name="using-the-bes-sdk"></a><span data-ttu-id="d99a9-236">Using the BES SDK</span><span class="sxs-lookup"><span data-stu-id="d99a9-236">Using the BES SDK</span></span>
<span data-ttu-id="d99a9-237">The [BES SDK Nuget package](http://www.nuget.org/packages/Microsoft.Azure.MachineLearning/) provides functions that simplify calling BES to score in batch mode.</span><span class="sxs-lookup"><span data-stu-id="d99a9-237">The [BES SDK Nuget package](http://www.nuget.org/packages/Microsoft.Azure.MachineLearning/) provides functions that simplify calling BES to score in batch mode.</span></span> <span data-ttu-id="d99a9-238">To install the Nuget package, in Visual Studio in the **Tools** menu, select **Nuget Package Manager** and click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d99a9-238">To install the Nuget package, in Visual Studio in the **Tools** menu, select **Nuget Package Manager** and click **Package Manager Console**.</span></span>

<span data-ttu-id="d99a9-239">Azure Machine Learning experiments that are deployed as Web services can include Web service input modules.</span><span class="sxs-lookup"><span data-stu-id="d99a9-239">Azure Machine Learning experiments that are deployed as Web services can include Web service input modules.</span></span> <span data-ttu-id="d99a9-240">This means that input to the Web service is provided through a Web service call in the form of a reference to a blob location.</span><span class="sxs-lookup"><span data-stu-id="d99a9-240">This means that input to the Web service is provided through a Web service call in the form of a reference to a blob location.</span></span> <span data-ttu-id="d99a9-241">There is also the option of not using a Web service input module and using an **Import Data** module instead.</span><span class="sxs-lookup"><span data-stu-id="d99a9-241">There is also the option of not using a Web service input module and using an **Import Data** module instead.</span></span> <span data-ttu-id="d99a9-242">In this case, the **Import Data** module reads from a data source, such as a SQL DB using a query at run time.</span><span class="sxs-lookup"><span data-stu-id="d99a9-242">In this case, the **Import Data** module reads from a data source, such as a SQL DB using a query at run time.</span></span> <span data-ttu-id="d99a9-243">Web service parameters can be used to dynamically point to other servers or tables, etc. The SDK supports both of these patterns.</span><span class="sxs-lookup"><span data-stu-id="d99a9-243">Web service parameters can be used to dynamically point to other servers or tables, etc. The SDK supports both of these patterns.</span></span>

<span data-ttu-id="d99a9-244">The following code sample demonstrates how to submit and monitor a batch job against an Azure Machine Learning service using the BES SDK.</span><span class="sxs-lookup"><span data-stu-id="d99a9-244">The following code sample demonstrates how to submit and monitor a batch job against an Azure Machine Learning service using the BES SDK.</span></span> <span data-ttu-id="d99a9-245">The comments contain details on the settings and calls.</span><span class="sxs-lookup"><span data-stu-id="d99a9-245">The comments contain details on the settings and calls.</span></span>

#### <a name="sample-code"></a><span data-ttu-id="d99a9-246">**Sample Code**</span><span class="sxs-lookup"><span data-stu-id="d99a9-246">**Sample Code**</span></span>
    // This code requires the Nuget package Microsoft.Azure.MachineLearning to be installed.
    // Instructions for doing this in Visual Studio:
    // Tools -> Nuget Package Manager -> Package Manager Console
    // Install-Package Microsoft.Azure.MachineLearning

      using System;
      using System.Collections.Generic;
      using System.Threading.Tasks;

      using Microsoft.Azure.MachineLearning;
      using Microsoft.Azure.MachineLearning.Contracts;
      using Microsoft.Azure.MachineLearning.Exceptions;

    namespace CallBatchExecutionService
    {
        class Program
        {
            static void Main(string[] args)
            {                
                InvokeBatchExecutionService().Wait();
            }

            static async Task InvokeBatchExecutionService()
            {
                // First collect and fill in the URI and access key for your Web service endpoint.
                // These are available on your service's API help page.
                var endpointUri = "https://ussouthcentral.services.azureml.net/workspaces/YOUR_WORKSPACE_ID/services/YOUR_SERVICE_ENDPOINT_ID/";
                string accessKey = "YOUR_SERVICE_ENDPOINT_ACCESS_KEY";

                // Create an Azure Machine Learning runtime client for this endpoint
                var runtimeClient = new RuntimeClient(endpointUri, accessKey);

                // Define the request information for your batch job. This information can contain:
                // -- A reference to the AzureBlob containing the input for your job run
                // -- A set of values for global parameters defined as part of your experiment and service
                // -- A set of output blob locations that allow you to redirect the job's results

                // NOTE: This sample is applicable, as is, for a service with explicit input port and
                // potential global parameters. Also, we choose to also demo how you could override the
                // location of one of the output blobs that could be generated by your service. You might
                // need to tweak these features to adjust the sample to your service.
                //
                // All of these properties of a BatchJobRequest shown below can be optional, depending on
                // your service, so it is not required to specify all with any request.  If you do not want to
                // use any of the parameters, a null value should be passed in its place.

                // Define the reference to the blob containing your input data. You can refer to this blob by its
                    // connection string / container / blob name values; alternatively, we also support references
                    // based on a blob SAS URI

                    BlobReference inputBlob = BlobReference.CreateFromConnectionStringData(connectionString:                                         "DefaultEndpointsProtocol=https;AccountName=YOUR_ACCOUNT_NAME;AccountKey=YOUR_ACCOUNT_KEY",
                        containerName: "YOUR_CONTAINER_NAME",
                        blobName: "YOUR_INPUT_BLOB_NAME");

                    // If desired, one can override the location where the job outputs are to be stored, by passing in
                    // the storage account details and name of the blob where we want the output to be redirected to.

                    var outputLocations = new Dictionary<string, BlobReference>
                        {
                          {
                           "YOUR_OUTPUT_NODE_NAME",
                           BlobReference.CreateFromConnectionStringData(                                     connectionString: "DefaultEndpointsProtocol=https;AccountName=YOUR_ACCOUNT_NAME;AccountKey=YOUR_ACCOUNT_KEY",
                                containerName: "YOUR_CONTAINER_NAME",
                                blobName: "YOUR_DESIRED_OUTPUT_BLOB_NAME")
                           }
                        };

                // If applicable, you can also set the global parameters for your service
                var globalParameters = new Dictionary<string, string>
                {
                    { "YOUR_GLOBAL_PARAMETER", "PARAMETER_VALUE" }
                };

                var jobRequest = new BatchJobRequest
                {
                    Input = inputBlob,
                    GlobalParameters = globalParameters,
                    Outputs = outputLocations
                };

                try
                {
                    // Register the batch job with the system, which will grant you access to a job object
                    BatchJob job = await runtimeClient.RegisterBatchJobAsync(jobRequest);

                    // Start the job to allow it to be scheduled in the running queue
                    await job.StartAsync();

                    // Wait for the job's completion and handle the output
                    BatchJobStatus jobStatus = await job.WaitForCompletionAsync();
                    if (jobStatus.JobState == JobState.Finished)
                    {
                        // Process job outputs
                        Console.WriteLine(@"Job {0} has completed successfully and returned {1} outputs", job.Id, jobStatus.Results.Count);
                        foreach (var output in jobStatus.Results)
                        {
                            Console.WriteLine(@"\t{0}: {1}", output.Key, output.Value.AbsoluteUri);
                        }
                    }
                    else if (jobStatus.JobState == JobState.Failed)
                    {
                        // Handle job failure
                        Console.WriteLine(@"Job {0} has failed with this error: {1}", job.Id, jobStatus.Details);
                    }
                }
                catch (ArgumentException aex)
                {
                    Console.WriteLine("Argument {0} is invalid: {1}", aex.ParamName, aex.Message);
                }
                catch (RuntimeException runtimeError)
                {
                    Console.WriteLine("Runtime error occurred: {0} - {1}", runtimeError.ErrorCode, runtimeError.Message);
                    Console.WriteLine("Error details:");
                    foreach (var errorDetails in runtimeError.Details)
                    {
                        Console.WriteLine("\t{0} - {1}", errorDetails.Code, errorDetails.Message);
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine("Unexpected error occurred: {0} - {1}", ex.GetType().Name, ex.Message);
                }
            }
        }
    }

#### <a name="sample-code-in-java-for-bes"></a><span data-ttu-id="d99a9-247">Sample code in Java for BES</span><span class="sxs-lookup"><span data-stu-id="d99a9-247">Sample code in Java for BES</span></span>
<span data-ttu-id="d99a9-248">The Batch execution service REST API takes the JSON consisting of a reference to an input sample csv and an output sample csv, as shown in the following sample, and creates a job in the Azure ML to do the batch predictions.</span><span class="sxs-lookup"><span data-stu-id="d99a9-248">The Batch execution service REST API takes the JSON consisting of a reference to an input sample csv and an output sample csv, as shown in the following sample, and creates a job in the Azure ML to do the batch predictions.</span></span> <span data-ttu-id="d99a9-249">You can view the full code in [GitHub](https://github.com/nk773/AzureML_BESApp/tree/master/src/azureml_besapp).</span><span class="sxs-lookup"><span data-stu-id="d99a9-249">You can view the full code in [GitHub](https://github.com/nk773/AzureML_BESApp/tree/master/src/azureml_besapp).</span></span> <span data-ttu-id="d99a9-250">This Java sample requires [apache http client library](https://hc.apache.org/downloads.cgi).</span><span class="sxs-lookup"><span data-stu-id="d99a9-250">This Java sample requires [apache http client library](https://hc.apache.org/downloads.cgi).</span></span> 

    { "GlobalParameters": {}, 
        "Inputs": { "input1": { "ConnectionString":     "DefaultEndpointsProtocol=https;
            AccountName=myAcctName; AccountKey=Q8kkieg==", 
            "RelativeLocation": "myContainer/sampleinput.csv" } }, 
        "Outputs": { "output1": { "ConnectionString":     "DefaultEndpointsProtocol=https;
            AccountName=myAcctName; AccountKey=kjC12xQ8kkieg==", 
            "RelativeLocation": "myContainer/sampleoutput.csv" } } 
    } 


##### <a name="create-a-bes-job"></a><span data-ttu-id="d99a9-251">Create a BES job</span><span class="sxs-lookup"><span data-stu-id="d99a9-251">Create a BES job</span></span>
        /**
         * Call REST API to create a job to Azure ML 
         * for batch predictions
         * @return response from the REST API
         */    
        public static String besCreateJob() {

            HttpPost post;
            HttpClient client;
            StringEntity entity;

            try {
                // create HttpPost and HttpClient object
                post = new HttpPost(apiurl);
                client = HttpClientBuilder.create().build();

                // setup output message by copying JSON body into 
                // apache StringEntity object along with content type
                entity = new StringEntity(jsonBody, HTTP.UTF_8);
                entity.setContentEncoding(HTTP.UTF_8);
                entity.setContentType("text/json");

                // add HTTP headers
                post.setHeader("Accept", "text/json");
                post.setHeader("Accept-Charset", "UTF-8");

                // set Authorization header based on the API key
                // note a space after the word "Bearer " - don't miss that
                post.setHeader("Authorization", ("Bearer "+apikey));
                post.setEntity(entity);

                // Call REST API and retrieve response content
                HttpResponse authResponse = client.execute(post);

                jobId = EntityUtils.toString(authResponse.getEntity()).replaceAll("\"", "");


                return jobId;

            }
            catch (Exception e) {

                return e.toString();
            }

        }

##### <a name="start-a-previously-created-bes-job"></a><span data-ttu-id="d99a9-252">Start a previously created BES job</span><span class="sxs-lookup"><span data-stu-id="d99a9-252">Start a previously created BES job</span></span>
        /**
         * Call REST API for starting prediction job previously submitted 
         * 
         * @param job job to be started 
         * @return response from the REST API
         */    
        public static String besStartJob(String job){
            HttpPost post;
            HttpClient client;
            StringEntity entity;

            try {
                // create HttpPost and HttpClient object
                post = new HttpPost(startJobUrl+"/"+job+"/start?api-version=2.0");
                client = HttpClientBuilder.create().build();

                // add HTTP headers
                post.setHeader("Accept", "text/json");
                post.setHeader("Accept-Charset", "UTF-8");

                // set Authorization header based on the API key
                post.setHeader("Authorization", ("Bearer "+apikey));

                // Call REST API and retrieve response content
                HttpResponse authResponse = client.execute(post);

                if (authResponse.getEntity()==null)
                {
                    return authResponse.getStatusLine().toString();
                }

                return EntityUtils.toString(authResponse.getEntity());

            }
            catch (Exception e) {

                return e.toString();
            }
        }
##### <a name="cancel-a-previously-created-bes-job"></a><span data-ttu-id="d99a9-253">Cancel a previously created BES job</span><span class="sxs-lookup"><span data-stu-id="d99a9-253">Cancel a previously created BES job</span></span>
        /**
         * Call REST API for canceling the batch job 
         * 
         * @param job job to be started 
         * @return response from the REST API
         */    
        public static String besCancelJob(String job) {
            HttpDelete post;
            HttpClient client;
            StringEntity entity;

            try {
                // create HttpPost and HttpClient object
                post = new HttpDelete(startJobUrl+job);
                client = HttpClientBuilder.create().build();

                // add HTTP headers
                post.setHeader("Accept", "text/json");
                post.setHeader("Accept-Charset", "UTF-8");

                // set Authorization header based on the API key
                post.setHeader("Authorization", ("Bearer "+apikey));

                // Call REST API and retrieve response content
                HttpResponse authResponse = client.execute(post);

                if (authResponse.getEntity()==null)
                {
                    return authResponse.getStatusLine().toString();
                }
                return EntityUtils.toString(authResponse.getEntity());

            }
            catch (Exception e) {

                return e.toString();
            }
        }

### <a name="other-programming-environments"></a><span data-ttu-id="d99a9-254">Other programming environments</span><span class="sxs-lookup"><span data-stu-id="d99a9-254">Other programming environments</span></span>
<span data-ttu-id="d99a9-255">You can also generate the code in many other languages following the directions provided at [swagger.io](http://swagger.io/) site.</span><span class="sxs-lookup"><span data-stu-id="d99a9-255">You can also generate the code in many other languages following the directions provided at [swagger.io](http://swagger.io/) site.</span></span> <span data-ttu-id="d99a9-256">For a Classic Web service you can get the swagger document:</span><span class="sxs-lookup"><span data-stu-id="d99a9-256">For a Classic Web service you can get the swagger document:</span></span>

* <span data-ttu-id="d99a9-257">From the API help page</span><span class="sxs-lookup"><span data-stu-id="d99a9-257">From the API help page</span></span> 
* <span data-ttu-id="d99a9-258">By calling Get API Document for Endpoint, found on the Swagger API page of Machine Learning Web Services portal.</span><span class="sxs-lookup"><span data-stu-id="d99a9-258">By calling Get API Document for Endpoint, found on the Swagger API page of Machine Learning Web Services portal.</span></span> 

<span data-ttu-id="d99a9-259">Go to the [swagger.io](http://swagger.io/swagger-codegen/) and follow the instructions to download swagger code, java, and apache mvn.</span><span class="sxs-lookup"><span data-stu-id="d99a9-259">Go to the [swagger.io](http://swagger.io/swagger-codegen/) and follow the instructions to download swagger code, java, and apache mvn.</span></span> 

<span data-ttu-id="d99a9-260">The following list is the summary of instructions on setting up swagger for other programming environments.</span><span class="sxs-lookup"><span data-stu-id="d99a9-260">The following list is the summary of instructions on setting up swagger for other programming environments.</span></span>

* <span data-ttu-id="d99a9-261">Make sure Java 7 or higher is installed</span><span class="sxs-lookup"><span data-stu-id="d99a9-261">Make sure Java 7 or higher is installed</span></span>
* <span data-ttu-id="d99a9-262">Install apache mvn (On ubuntu, you can use *apt-get install mvn*)</span><span class="sxs-lookup"><span data-stu-id="d99a9-262">Install apache mvn (On ubuntu, you can use *apt-get install mvn*)</span></span>
* <span data-ttu-id="d99a9-263">Goto github for swagger and download the swagger project as a zip file</span><span class="sxs-lookup"><span data-stu-id="d99a9-263">Goto github for swagger and download the swagger project as a zip file</span></span>
* <span data-ttu-id="d99a9-264">Unzip swagger</span><span class="sxs-lookup"><span data-stu-id="d99a9-264">Unzip swagger</span></span>
* <span data-ttu-id="d99a9-265">Build swagger tools by running *mvn package* from the swagger's source directory</span><span class="sxs-lookup"><span data-stu-id="d99a9-265">Build swagger tools by running *mvn package* from the swagger's source directory</span></span>

<span data-ttu-id="d99a9-266">Now you can use any of the swagger tools.</span><span class="sxs-lookup"><span data-stu-id="d99a9-266">Now you can use any of the swagger tools.</span></span> <span data-ttu-id="d99a9-267">Here are the instructions to generate Java client code.</span><span class="sxs-lookup"><span data-stu-id="d99a9-267">Here are the instructions to generate Java client code.</span></span> 

* <span data-ttu-id="d99a9-268">Go to the Azure ML API Help page (example [here](https://studio.azureml.net/apihelp/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/jobs))</span><span class="sxs-lookup"><span data-stu-id="d99a9-268">Go to the Azure ML API Help page (example [here](https://studio.azureml.net/apihelp/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/jobs))</span></span>
* <span data-ttu-id="d99a9-269">Find the URL for swagger.json for Azure ML REST APIs (second last bullet on top of API help page)</span><span class="sxs-lookup"><span data-stu-id="d99a9-269">Find the URL for swagger.json for Azure ML REST APIs (second last bullet on top of API help page)</span></span>
* <span data-ttu-id="d99a9-270">Click the swagger document link (example [here](https://management.azureml.net/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/apidocument))</span><span class="sxs-lookup"><span data-stu-id="d99a9-270">Click the swagger document link (example [here](https://management.azureml.net/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/apidocument))</span></span>
* <span data-ttu-id="d99a9-271">Use the following command as shown in the [Read Me file of swagger](https://github.com/swagger-api/swagger-codegen/blob/master/README.md) to generate the client code</span><span class="sxs-lookup"><span data-stu-id="d99a9-271">Use the following command as shown in the [Read Me file of swagger](https://github.com/swagger-api/swagger-codegen/blob/master/README.md) to generate the client code</span></span>

<span data-ttu-id="d99a9-272">**Sample Command Line to generate client code**</span><span class="sxs-lookup"><span data-stu-id="d99a9-272">**Sample Command Line to generate client code**</span></span>

    java -jar swagger-codegen-cli.jar generate\
     -i https://ussouthcentral.services.azureml.net:443/workspaces/\
    fb62b56f29fc4ba4b8a8f900c9b89584/services/26a3afce1767461ab6e73d5a206fbd62/swagger.json\
     -l java -o /home/username/sample

* <span data-ttu-id="d99a9-273">Combine values in the fields host, basePath and "/swagger.json" in the sample of a swagger [API help page](https://management.azureml.net/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/apidocument) shown below to construct swagger URL used in the preceding command line.</span><span class="sxs-lookup"><span data-stu-id="d99a9-273">Combine values in the fields host, basePath and "/swagger.json" in the sample of a swagger [API help page](https://management.azureml.net/workspaces/afbd553b9bac4c95be3d040998943a4f/webservices/4dfadc62adcc485eb0cf162397fb5682/endpoints/26a3afce1767461ab6e73d5a206fbd62/apidocument) shown below to construct swagger URL used in the preceding command line.</span></span>

<span data-ttu-id="d99a9-274">**Sample API Help Page**</span><span class="sxs-lookup"><span data-stu-id="d99a9-274">**Sample API Help Page**</span></span>

    {
      "swagger": "2.0",
      "info": {
        "version": "2.0",
        "title": "Sample 5: Binary Classification with Web service: Adult Dataset [Predictive Exp.]",
        "description": "No description provided for this Web service.",
        "x-endpoint-name": "default"
      },
      "host": "ussouthcentral.services.azureml.net:443",
      "basePath": "/workspaces/afbd553b9bac4c95be3d040998943a4f/services/26a3afce1767461ab6e73d5a206fbd62",
      "schemes": [
        "https"
      ],
      "consumes": [
        "application/json"
      ],
      "produces": [
        "application/json"
      ],
      "paths": {
        "/swagger.json": {
          "get": {
            "summary": "Get swagger API document for the Web service",
            "operationId": "getSwaggerDocument",

<!-- Relative Links -->

[publish]: machine-learning-publish-a-machine-learning-web-service.md
[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- External Links -->
[webservicesportal]: https://services.azureml.net/
[mlstudio]: https://studio.azureml.net
