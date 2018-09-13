---
title: Web Activity in Azure Data Factory | Microsoft Docs
description: Learn how you can use Web Activity, one of the control flow activities supported by Data Factory, to invoke a REST endpoint from a pipeline.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
editor: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/14/2018
ms.author: shlo
ms.openlocfilehash: 71e89828645cadbbbf60527fca9968fd8ed568ff
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868503"
---
# <a name="web-activity-in-azure-data-factory"></a><span data-ttu-id="b8e32-103">Web activity in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b8e32-103">Web activity in Azure Data Factory</span></span>
<span data-ttu-id="b8e32-104">Web Activity can be used to call a custom REST endpoint from a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="b8e32-104">Web Activity can be used to call a custom REST endpoint from a Data Factory pipeline.</span></span> <span data-ttu-id="b8e32-105">You can pass datasets and linked services to be consumed and accessed by the activity.</span><span class="sxs-lookup"><span data-stu-id="b8e32-105">You can pass datasets and linked services to be consumed and accessed by the activity.</span></span> 

## <a name="syntax"></a><span data-ttu-id="b8e32-106">Syntax</span><span class="sxs-lookup"><span data-stu-id="b8e32-106">Syntax</span></span>

```json
{  
   "name":"MyWebActivity",
   "type":"WebActivity",
   "typeProperties":{  
      "method":"Post",
      "url":"<URLEndpoint>",
      "headers":{  
         "Content-Type":"application/json"
      },
      "authentication":{  
         "type":"ClientCertificate",  
         "pfx":"****",
         "password":"****"
      },
      "datasets":[  
         {  
            "referenceName":"<ConsumedDatasetName>",
            "type":"DatasetReference",
            "parameters":{  
               ...
            }
         }
      ],
      "linkedServices":[  
         {  
            "referenceName":"<ConsumedLinkedServiceName>",
            "type":"LinkedServiceReference"
         }
      ]
   }
}

```

## <a name="type-properties"></a><span data-ttu-id="b8e32-107">Type properties</span><span class="sxs-lookup"><span data-stu-id="b8e32-107">Type properties</span></span>

<span data-ttu-id="b8e32-108">Property</span><span class="sxs-lookup"><span data-stu-id="b8e32-108">Property</span></span> | <span data-ttu-id="b8e32-109">Description</span><span class="sxs-lookup"><span data-stu-id="b8e32-109">Description</span></span> | <span data-ttu-id="b8e32-110">Allowed values</span><span class="sxs-lookup"><span data-stu-id="b8e32-110">Allowed values</span></span> | <span data-ttu-id="b8e32-111">Required</span><span class="sxs-lookup"><span data-stu-id="b8e32-111">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="b8e32-112">name</span><span class="sxs-lookup"><span data-stu-id="b8e32-112">name</span></span> | <span data-ttu-id="b8e32-113">Name of the web activity</span><span class="sxs-lookup"><span data-stu-id="b8e32-113">Name of the web activity</span></span> | <span data-ttu-id="b8e32-114">String</span><span class="sxs-lookup"><span data-stu-id="b8e32-114">String</span></span> | <span data-ttu-id="b8e32-115">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-115">Yes</span></span>
<span data-ttu-id="b8e32-116">type</span><span class="sxs-lookup"><span data-stu-id="b8e32-116">type</span></span> | <span data-ttu-id="b8e32-117">Must be set to **WebActivity**.</span><span class="sxs-lookup"><span data-stu-id="b8e32-117">Must be set to **WebActivity**.</span></span> | <span data-ttu-id="b8e32-118">String</span><span class="sxs-lookup"><span data-stu-id="b8e32-118">String</span></span> | <span data-ttu-id="b8e32-119">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-119">Yes</span></span>
<span data-ttu-id="b8e32-120">method</span><span class="sxs-lookup"><span data-stu-id="b8e32-120">method</span></span> | <span data-ttu-id="b8e32-121">Rest API method for the target endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-121">Rest API method for the target endpoint.</span></span> | <span data-ttu-id="b8e32-122">String.</span><span class="sxs-lookup"><span data-stu-id="b8e32-122">String.</span></span> <br/><br/><span data-ttu-id="b8e32-123">Supported Types: "GET", "POST", "PUT"</span><span class="sxs-lookup"><span data-stu-id="b8e32-123">Supported Types: "GET", "POST", "PUT"</span></span> | <span data-ttu-id="b8e32-124">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-124">Yes</span></span>
<span data-ttu-id="b8e32-125">url</span><span class="sxs-lookup"><span data-stu-id="b8e32-125">url</span></span> | <span data-ttu-id="b8e32-126">Target endpoint and path</span><span class="sxs-lookup"><span data-stu-id="b8e32-126">Target endpoint and path</span></span> | <span data-ttu-id="b8e32-127">String (or expression with resultType of string).</span><span class="sxs-lookup"><span data-stu-id="b8e32-127">String (or expression with resultType of string).</span></span> <span data-ttu-id="b8e32-128">The activity will timeout at 1 minute with an error if it does not receive a response from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-128">The activity will timeout at 1 minute with an error if it does not receive a response from the endpoint.</span></span> | <span data-ttu-id="b8e32-129">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-129">Yes</span></span>
<span data-ttu-id="b8e32-130">headers</span><span class="sxs-lookup"><span data-stu-id="b8e32-130">headers</span></span> | <span data-ttu-id="b8e32-131">Headers that are sent to the request.</span><span class="sxs-lookup"><span data-stu-id="b8e32-131">Headers that are sent to the request.</span></span> <span data-ttu-id="b8e32-132">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us", "Content-Type": "application/json" }`.</span><span class="sxs-lookup"><span data-stu-id="b8e32-132">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us", "Content-Type": "application/json" }`.</span></span> | <span data-ttu-id="b8e32-133">String (or expression with resultType of string)</span><span class="sxs-lookup"><span data-stu-id="b8e32-133">String (or expression with resultType of string)</span></span> | <span data-ttu-id="b8e32-134">Yes, Content-type header is required.</span><span class="sxs-lookup"><span data-stu-id="b8e32-134">Yes, Content-type header is required.</span></span> `"headers":{ "Content-Type":"application/json"}`
<span data-ttu-id="b8e32-135">body</span><span class="sxs-lookup"><span data-stu-id="b8e32-135">body</span></span> | <span data-ttu-id="b8e32-136">Represents the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-136">Represents the payload that is sent to the endpoint.</span></span>  | <span data-ttu-id="b8e32-137">String (or expression with resultType of string).</span><span class="sxs-lookup"><span data-stu-id="b8e32-137">String (or expression with resultType of string).</span></span> <br/><br/><span data-ttu-id="b8e32-138">See the schema of the request payload in [Request payload schema](#request-payload-schema) section.</span><span class="sxs-lookup"><span data-stu-id="b8e32-138">See the schema of the request payload in [Request payload schema](#request-payload-schema) section.</span></span> | <span data-ttu-id="b8e32-139">Required for POST/PUT methods.</span><span class="sxs-lookup"><span data-stu-id="b8e32-139">Required for POST/PUT methods.</span></span>
<span data-ttu-id="b8e32-140">authentication</span><span class="sxs-lookup"><span data-stu-id="b8e32-140">authentication</span></span> | <span data-ttu-id="b8e32-141">Authentication method used for calling the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-141">Authentication method used for calling the endpoint.</span></span> <span data-ttu-id="b8e32-142">Supported Types are "Basic, or ClientCertificate."</span><span class="sxs-lookup"><span data-stu-id="b8e32-142">Supported Types are "Basic, or ClientCertificate."</span></span> <span data-ttu-id="b8e32-143">For more information, see [Authentication](#authentication) section.</span><span class="sxs-lookup"><span data-stu-id="b8e32-143">For more information, see [Authentication](#authentication) section.</span></span> <span data-ttu-id="b8e32-144">If authentication is not required, exclude this property.</span><span class="sxs-lookup"><span data-stu-id="b8e32-144">If authentication is not required, exclude this property.</span></span> | <span data-ttu-id="b8e32-145">String (or expression with resultType of string)</span><span class="sxs-lookup"><span data-stu-id="b8e32-145">String (or expression with resultType of string)</span></span> | <span data-ttu-id="b8e32-146">No</span><span class="sxs-lookup"><span data-stu-id="b8e32-146">No</span></span>
<span data-ttu-id="b8e32-147">datasets</span><span class="sxs-lookup"><span data-stu-id="b8e32-147">datasets</span></span> | <span data-ttu-id="b8e32-148">List of datasets passed to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-148">List of datasets passed to the endpoint.</span></span> | <span data-ttu-id="b8e32-149">Array of dataset references.</span><span class="sxs-lookup"><span data-stu-id="b8e32-149">Array of dataset references.</span></span> <span data-ttu-id="b8e32-150">Can be an empty array.</span><span class="sxs-lookup"><span data-stu-id="b8e32-150">Can be an empty array.</span></span> | <span data-ttu-id="b8e32-151">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-151">Yes</span></span>
<span data-ttu-id="b8e32-152">linkedServices</span><span class="sxs-lookup"><span data-stu-id="b8e32-152">linkedServices</span></span> | <span data-ttu-id="b8e32-153">List of linked services passed to endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-153">List of linked services passed to endpoint.</span></span> | <span data-ttu-id="b8e32-154">Array of linked service references.</span><span class="sxs-lookup"><span data-stu-id="b8e32-154">Array of linked service references.</span></span> <span data-ttu-id="b8e32-155">Can be an empty array.</span><span class="sxs-lookup"><span data-stu-id="b8e32-155">Can be an empty array.</span></span> | <span data-ttu-id="b8e32-156">Yes</span><span class="sxs-lookup"><span data-stu-id="b8e32-156">Yes</span></span>

> [!NOTE]
> <span data-ttu-id="b8e32-157">REST endpoints that the web activity invokes must return a response of type JSON.</span><span class="sxs-lookup"><span data-stu-id="b8e32-157">REST endpoints that the web activity invokes must return a response of type JSON.</span></span> <span data-ttu-id="b8e32-158">The activity will timeout at 1 minute with an error if it does not receive a response from the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-158">The activity will timeout at 1 minute with an error if it does not receive a response from the endpoint.</span></span>

<span data-ttu-id="b8e32-159">The following table shows the requirements for JSON content:</span><span class="sxs-lookup"><span data-stu-id="b8e32-159">The following table shows the requirements for JSON content:</span></span>

| <span data-ttu-id="b8e32-160">Value type</span><span class="sxs-lookup"><span data-stu-id="b8e32-160">Value type</span></span> | <span data-ttu-id="b8e32-161">Request body</span><span class="sxs-lookup"><span data-stu-id="b8e32-161">Request body</span></span> | <span data-ttu-id="b8e32-162">Response body</span><span class="sxs-lookup"><span data-stu-id="b8e32-162">Response body</span></span> |
|---|---|---|
|<span data-ttu-id="b8e32-163">JSON object</span><span class="sxs-lookup"><span data-stu-id="b8e32-163">JSON object</span></span> | <span data-ttu-id="b8e32-164">Supported</span><span class="sxs-lookup"><span data-stu-id="b8e32-164">Supported</span></span> | <span data-ttu-id="b8e32-165">Supported</span><span class="sxs-lookup"><span data-stu-id="b8e32-165">Supported</span></span> |
|<span data-ttu-id="b8e32-166">JSON array</span><span class="sxs-lookup"><span data-stu-id="b8e32-166">JSON array</span></span> | <span data-ttu-id="b8e32-167">Supported</span><span class="sxs-lookup"><span data-stu-id="b8e32-167">Supported</span></span> <br/><span data-ttu-id="b8e32-168">(At present, JSON arrays don't work as a result of a bug.</span><span class="sxs-lookup"><span data-stu-id="b8e32-168">(At present, JSON arrays don't work as a result of a bug.</span></span> <span data-ttu-id="b8e32-169">A fix is in progress.)</span><span class="sxs-lookup"><span data-stu-id="b8e32-169">A fix is in progress.)</span></span> | <span data-ttu-id="b8e32-170">Unsupported</span><span class="sxs-lookup"><span data-stu-id="b8e32-170">Unsupported</span></span> |
| <span data-ttu-id="b8e32-171">JSON value</span><span class="sxs-lookup"><span data-stu-id="b8e32-171">JSON value</span></span> | <span data-ttu-id="b8e32-172">Supported</span><span class="sxs-lookup"><span data-stu-id="b8e32-172">Supported</span></span> | <span data-ttu-id="b8e32-173">Unsupported</span><span class="sxs-lookup"><span data-stu-id="b8e32-173">Unsupported</span></span> |
| <span data-ttu-id="b8e32-174">Non-JSON type</span><span class="sxs-lookup"><span data-stu-id="b8e32-174">Non-JSON type</span></span> | <span data-ttu-id="b8e32-175">Unsupported</span><span class="sxs-lookup"><span data-stu-id="b8e32-175">Unsupported</span></span> | <span data-ttu-id="b8e32-176">Unsupported</span><span class="sxs-lookup"><span data-stu-id="b8e32-176">Unsupported</span></span> |
||||

## <a name="authentication"></a><span data-ttu-id="b8e32-177">Authentication</span><span class="sxs-lookup"><span data-stu-id="b8e32-177">Authentication</span></span>

### <a name="none"></a><span data-ttu-id="b8e32-178">None</span><span class="sxs-lookup"><span data-stu-id="b8e32-178">None</span></span>
<span data-ttu-id="b8e32-179">If authentication is not required, do not include the "authentication" property.</span><span class="sxs-lookup"><span data-stu-id="b8e32-179">If authentication is not required, do not include the "authentication" property.</span></span>

### <a name="basic"></a><span data-ttu-id="b8e32-180">Basic</span><span class="sxs-lookup"><span data-stu-id="b8e32-180">Basic</span></span>
<span data-ttu-id="b8e32-181">Specify user name and password to use with the basic authentication.</span><span class="sxs-lookup"><span data-stu-id="b8e32-181">Specify user name and password to use with the basic authentication.</span></span> 

```json
"authentication":{  
   "type":"Basic,
   "username":"****",
   "password":"****"
}
```

### <a name="client-certificate"></a><span data-ttu-id="b8e32-182">Client certificate</span><span class="sxs-lookup"><span data-stu-id="b8e32-182">Client certificate</span></span>
<span data-ttu-id="b8e32-183">Specify base64-encoded contents of a PFX file and the password.</span><span class="sxs-lookup"><span data-stu-id="b8e32-183">Specify base64-encoded contents of a PFX file and the password.</span></span> 

```json
"authentication":{  
   "type":"ClientCertificate",
   "pfx":"****",   
   "password":"****"
}
```
## <a name="request-payload-schema"></a><span data-ttu-id="b8e32-184">Request payload schema</span><span class="sxs-lookup"><span data-stu-id="b8e32-184">Request payload schema</span></span>
<span data-ttu-id="b8e32-185">When you use the POST/PUT method, the body property represents the payload that is sent to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-185">When you use the POST/PUT method, the body property represents the payload that is sent to the endpoint.</span></span> <span data-ttu-id="b8e32-186">You can pass linked services and datasets as part of the payload.</span><span class="sxs-lookup"><span data-stu-id="b8e32-186">You can pass linked services and datasets as part of the payload.</span></span> <span data-ttu-id="b8e32-187">Here is the schema for the payload:</span><span class="sxs-lookup"><span data-stu-id="b8e32-187">Here is the schema for the payload:</span></span> 

```json
{
    "body": {
        "myMessage": "Sample",
        "datasets": [{
            "name": "MyDataset1",
            "properties": {
                ...
            }
        }],
        "linkedServices": [{
            "name": "MyStorageLinkedService1",
            "properties": {
                ...
            }
        }]
    }
} 
```

## <a name="example"></a><span data-ttu-id="b8e32-188">Example</span><span class="sxs-lookup"><span data-stu-id="b8e32-188">Example</span></span>
<span data-ttu-id="b8e32-189">In this example, the web activity in the pipeline calls a REST end point.</span><span class="sxs-lookup"><span data-stu-id="b8e32-189">In this example, the web activity in the pipeline calls a REST end point.</span></span> <span data-ttu-id="b8e32-190">It passes an Azure SQL linked service and an Azure SQL dataset to the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b8e32-190">It passes an Azure SQL linked service and an Azure SQL dataset to the endpoint.</span></span> <span data-ttu-id="b8e32-191">The REST end point uses the Azure SQL connection string to connect to the Azure SQL server and returns the name of the instance of SQL server.</span><span class="sxs-lookup"><span data-stu-id="b8e32-191">The REST end point uses the Azure SQL connection string to connect to the Azure SQL server and returns the name of the instance of SQL server.</span></span> 

### <a name="pipeline-definition"></a><span data-ttu-id="b8e32-192">Pipeline definition</span><span class="sxs-lookup"><span data-stu-id="b8e32-192">Pipeline definition</span></span>

```json
{
    "name": "<MyWebActivityPipeline>",
    "properties": {
        "activities": [
            {
                "name": "<MyWebActivity>",
                "type": "WebActivity",
                "typeProperties": {
                    "method": "Post",
                    "url": "@pipeline().parameters.url",
                    "headers": {
                        "Content-Type": "application/json"
                    },
                    "authentication": {
                        "type": "ClientCertificate",
                        "pfx": "*****",
                        "password": "*****"
                    },
                    "datasets": [
                        {
                            "referenceName": "MySQLDataset",
                            "type": "DatasetReference",
                            "parameters": {
                                "SqlTableName": "@pipeline().parameters.sqlTableName"
                            }
                        }
                    ],
                    "linkedServices": [
                        {
                            "referenceName": "SqlLinkedService",
                            "type": "LinkedServiceReference"
                        }
                    ]
                }
            }
        ],
        "parameters": {
            "sqlTableName": {
                "type": "String"
            },
            "url": {
                "type": "String"
            }
        }
    }
}

```

### <a name="pipeline-parameter-values"></a><span data-ttu-id="b8e32-193">Pipeline parameter values</span><span class="sxs-lookup"><span data-stu-id="b8e32-193">Pipeline parameter values</span></span>

```json
{
    "sqlTableName": "department",
    "url": "https://adftes.azurewebsites.net/api/execute/running"
}

```

### <a name="web-service-endpoint-code"></a><span data-ttu-id="b8e32-194">Web service endpoint code</span><span class="sxs-lookup"><span data-stu-id="b8e32-194">Web service endpoint code</span></span>

```csharp

[HttpPost]
public HttpResponseMessage Execute(JObject payload)
{
    Trace.TraceInformation("Start Execute");

    JObject result = new JObject();
    result.Add("status", "complete");

    JArray datasets = payload.GetValue("datasets") as JArray;
    result.Add("sinktable", datasets[0]["properties"]["typeProperties"]["tableName"].ToString());

    JArray linkedServices = payload.GetValue("linkedServices") as JArray;
    string connString = linkedServices[0]["properties"]["typeProperties"]["connectionString"].ToString();

    System.Data.SqlClient.SqlConnection sqlConn = new System.Data.SqlClient.SqlConnection(connString);

    result.Add("sinkServer", sqlConn.DataSource);

    Trace.TraceInformation("Stop Execute");

    return this.Request.CreateResponse(HttpStatusCode.OK, result);
}

```

## <a name="next-steps"></a><span data-ttu-id="b8e32-195">Next steps</span><span class="sxs-lookup"><span data-stu-id="b8e32-195">Next steps</span></span>
<span data-ttu-id="b8e32-196">See other control flow activities supported by Data Factory:</span><span class="sxs-lookup"><span data-stu-id="b8e32-196">See other control flow activities supported by Data Factory:</span></span> 

- [<span data-ttu-id="b8e32-197">Execute Pipeline Activity</span><span class="sxs-lookup"><span data-stu-id="b8e32-197">Execute Pipeline Activity</span></span>](control-flow-execute-pipeline-activity.md)
- [<span data-ttu-id="b8e32-198">For Each Activity</span><span class="sxs-lookup"><span data-stu-id="b8e32-198">For Each Activity</span></span>](control-flow-for-each-activity.md)
- [<span data-ttu-id="b8e32-199">Get Metadata Activity</span><span class="sxs-lookup"><span data-stu-id="b8e32-199">Get Metadata Activity</span></span>](control-flow-get-metadata-activity.md)
- [<span data-ttu-id="b8e32-200">Lookup Activity</span><span class="sxs-lookup"><span data-stu-id="b8e32-200">Lookup Activity</span></span>](control-flow-lookup-activity.md)
