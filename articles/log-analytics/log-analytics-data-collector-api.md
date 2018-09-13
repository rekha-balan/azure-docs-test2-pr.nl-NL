---
title: Log Analytics HTTP Data Collector API | Microsoft Docs
description: You can use the Log Analytics HTTP Data Collector API to add POST JSON data to the Log Analytics repository from any client that can call the REST API. This article describes how to use the API, and has examples of how to publish data by using different programming languages.
services: log-analytics
documentationcenter: ''
author: bwren
manager: jwhit
editor: ''
ms.assetid: a831fd90-3f55-423b-8b20-ccbaaac2ca75
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bwren
ms.openlocfilehash: 2e9c211352f1a548ba8db7bcf19a44eb3158903c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554234"
---
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a><span data-ttu-id="0cb30-104">Send data to Log Analytics with the HTTP Data Collector API</span><span class="sxs-lookup"><span data-stu-id="0cb30-104">Send data to Log Analytics with the HTTP Data Collector API</span></span>
<span data-ttu-id="0cb30-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span><span class="sxs-lookup"><span data-stu-id="0cb30-105">This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.</span></span>  <span data-ttu-id="0cb30-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="0cb30-106">It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.</span></span>  <span data-ttu-id="0cb30-107">Examples are provided for PowerShell, C#, and Python.</span><span class="sxs-lookup"><span data-stu-id="0cb30-107">Examples are provided for PowerShell, C#, and Python.</span></span>

## <a name="concepts"></a><span data-ttu-id="0cb30-108">Concepts</span><span class="sxs-lookup"><span data-stu-id="0cb30-108">Concepts</span></span>
<span data-ttu-id="0cb30-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span><span class="sxs-lookup"><span data-stu-id="0cb30-109">You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.</span></span>  <span data-ttu-id="0cb30-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span><span class="sxs-lookup"><span data-stu-id="0cb30-110">This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.</span></span>

<span data-ttu-id="0cb30-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span><span class="sxs-lookup"><span data-stu-id="0cb30-111">All data in the Log Analytics repository is stored as a record with a particular record type.</span></span>  <span data-ttu-id="0cb30-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span><span class="sxs-lookup"><span data-stu-id="0cb30-112">You format your data to send to the HTTP Data Collector API as multiple records in JSON.</span></span>  <span data-ttu-id="0cb30-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span><span class="sxs-lookup"><span data-stu-id="0cb30-113">When you submit the data, an individual record is created in the repository for each record in the request payload.</span></span>


![HTTP Data Collector overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a><span data-ttu-id="0cb30-115">Create a request</span><span class="sxs-lookup"><span data-stu-id="0cb30-115">Create a request</span></span>
<span data-ttu-id="0cb30-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="0cb30-116">To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).</span></span>  <span data-ttu-id="0cb30-117">The next three tables list the attributes that are required for each request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-117">The next three tables list the attributes that are required for each request.</span></span> <span data-ttu-id="0cb30-118">We describe each attribute in more detail later in the article.</span><span class="sxs-lookup"><span data-stu-id="0cb30-118">We describe each attribute in more detail later in the article.</span></span>

### <a name="request-uri"></a><span data-ttu-id="0cb30-119">Request URI</span><span class="sxs-lookup"><span data-stu-id="0cb30-119">Request URI</span></span>
| <span data-ttu-id="0cb30-120">Attribute</span><span class="sxs-lookup"><span data-stu-id="0cb30-120">Attribute</span></span> | <span data-ttu-id="0cb30-121">Property</span><span class="sxs-lookup"><span data-stu-id="0cb30-121">Property</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cb30-122">Method</span><span class="sxs-lookup"><span data-stu-id="0cb30-122">Method</span></span> |<span data-ttu-id="0cb30-123">POST</span><span class="sxs-lookup"><span data-stu-id="0cb30-123">POST</span></span> |
| <span data-ttu-id="0cb30-124">URI</span><span class="sxs-lookup"><span data-stu-id="0cb30-124">URI</span></span> |<span data-ttu-id="0cb30-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span><span class="sxs-lookup"><span data-stu-id="0cb30-125">https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01</span></span> |
| <span data-ttu-id="0cb30-126">Content type</span><span class="sxs-lookup"><span data-stu-id="0cb30-126">Content type</span></span> |<span data-ttu-id="0cb30-127">application/json</span><span class="sxs-lookup"><span data-stu-id="0cb30-127">application/json</span></span> |

### <a name="request-uri-parameters"></a><span data-ttu-id="0cb30-128">Request URI parameters</span><span class="sxs-lookup"><span data-stu-id="0cb30-128">Request URI parameters</span></span>
| <span data-ttu-id="0cb30-129">Parameter</span><span class="sxs-lookup"><span data-stu-id="0cb30-129">Parameter</span></span> | <span data-ttu-id="0cb30-130">Description</span><span class="sxs-lookup"><span data-stu-id="0cb30-130">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cb30-131">CustomerID</span><span class="sxs-lookup"><span data-stu-id="0cb30-131">CustomerID</span></span> |<span data-ttu-id="0cb30-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span><span class="sxs-lookup"><span data-stu-id="0cb30-132">The unique identifier for the Microsoft Operations Management Suite workspace.</span></span> |
| <span data-ttu-id="0cb30-133">Resource</span><span class="sxs-lookup"><span data-stu-id="0cb30-133">Resource</span></span> |<span data-ttu-id="0cb30-134">The API resource name: /api/logs.</span><span class="sxs-lookup"><span data-stu-id="0cb30-134">The API resource name: /api/logs.</span></span> |
| <span data-ttu-id="0cb30-135">API Version</span><span class="sxs-lookup"><span data-stu-id="0cb30-135">API Version</span></span> |<span data-ttu-id="0cb30-136">The version of the API to use with this request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-136">The version of the API to use with this request.</span></span> <span data-ttu-id="0cb30-137">Currently, it's 2016-04-01.</span><span class="sxs-lookup"><span data-stu-id="0cb30-137">Currently, it's 2016-04-01.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0cb30-138">Request headers</span><span class="sxs-lookup"><span data-stu-id="0cb30-138">Request headers</span></span>
| <span data-ttu-id="0cb30-139">Header</span><span class="sxs-lookup"><span data-stu-id="0cb30-139">Header</span></span> | <span data-ttu-id="0cb30-140">Description</span><span class="sxs-lookup"><span data-stu-id="0cb30-140">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cb30-141">Authorization</span><span class="sxs-lookup"><span data-stu-id="0cb30-141">Authorization</span></span> |<span data-ttu-id="0cb30-142">The authorization signature.</span><span class="sxs-lookup"><span data-stu-id="0cb30-142">The authorization signature.</span></span> <span data-ttu-id="0cb30-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span><span class="sxs-lookup"><span data-stu-id="0cb30-143">Later in the article, you can read about how to create an HMAC-SHA256 header.</span></span> |
| <span data-ttu-id="0cb30-144">Log-Type</span><span class="sxs-lookup"><span data-stu-id="0cb30-144">Log-Type</span></span> |<span data-ttu-id="0cb30-145">Specify the record type of the data that is being submitted.</span><span class="sxs-lookup"><span data-stu-id="0cb30-145">Specify the record type of the data that is being submitted.</span></span> <span data-ttu-id="0cb30-146">Currently, the log type supports only alpha characters.</span><span class="sxs-lookup"><span data-stu-id="0cb30-146">Currently, the log type supports only alpha characters.</span></span> <span data-ttu-id="0cb30-147">It does not support numerics or special characters.</span><span class="sxs-lookup"><span data-stu-id="0cb30-147">It does not support numerics or special characters.</span></span> |
| <span data-ttu-id="0cb30-148">x-ms-date</span><span class="sxs-lookup"><span data-stu-id="0cb30-148">x-ms-date</span></span> |<span data-ttu-id="0cb30-149">The date that the request was processed, in RFC 1123 format.</span><span class="sxs-lookup"><span data-stu-id="0cb30-149">The date that the request was processed, in RFC 1123 format.</span></span> |
| <span data-ttu-id="0cb30-150">time-generated-field</span><span class="sxs-lookup"><span data-stu-id="0cb30-150">time-generated-field</span></span> |<span data-ttu-id="0cb30-151">The name of a field in the data that contains the timestamp of the data item.</span><span class="sxs-lookup"><span data-stu-id="0cb30-151">The name of a field in the data that contains the timestamp of the data item.</span></span> <span data-ttu-id="0cb30-152">If you specify a field then its contents are used for **TimeGenerated**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-152">If you specify a field then its contents are used for **TimeGenerated**.</span></span> <span data-ttu-id="0cb30-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span><span class="sxs-lookup"><span data-stu-id="0cb30-153">If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested.</span></span> <span data-ttu-id="0cb30-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span><span class="sxs-lookup"><span data-stu-id="0cb30-154">The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ.</span></span> |

## <a name="authorization"></a><span data-ttu-id="0cb30-155">Authorization</span><span class="sxs-lookup"><span data-stu-id="0cb30-155">Authorization</span></span>
<span data-ttu-id="0cb30-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span><span class="sxs-lookup"><span data-stu-id="0cb30-156">Any request to the Log Analytics HTTP Data Collector API must include an authorization header.</span></span> <span data-ttu-id="0cb30-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-157">To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request.</span></span> <span data-ttu-id="0cb30-158">Then, pass that signature as part of the request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-158">Then, pass that signature as part of the request.</span></span>   

<span data-ttu-id="0cb30-159">Here's the format for the authorization header:</span><span class="sxs-lookup"><span data-stu-id="0cb30-159">Here's the format for the authorization header:</span></span>

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

<span data-ttu-id="0cb30-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span><span class="sxs-lookup"><span data-stu-id="0cb30-160">*WorkspaceID* is the unique identifier for the Operations Management Suite workspace.</span></span> <span data-ttu-id="0cb30-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span><span class="sxs-lookup"><span data-stu-id="0cb30-161">*Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx).</span></span> <span data-ttu-id="0cb30-162">Then, you encode it by using Base64 encoding.</span><span class="sxs-lookup"><span data-stu-id="0cb30-162">Then, you encode it by using Base64 encoding.</span></span>

<span data-ttu-id="0cb30-163">Use this format to encode the **SharedKey** signature string:</span><span class="sxs-lookup"><span data-stu-id="0cb30-163">Use this format to encode the **SharedKey** signature string:</span></span>

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

<span data-ttu-id="0cb30-164">Here's an example of a signature string:</span><span class="sxs-lookup"><span data-stu-id="0cb30-164">Here's an example of a signature string:</span></span>

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

<span data-ttu-id="0cb30-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span><span class="sxs-lookup"><span data-stu-id="0cb30-165">When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64.</span></span> <span data-ttu-id="0cb30-166">Use this format:</span><span class="sxs-lookup"><span data-stu-id="0cb30-166">Use this format:</span></span>

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

<span data-ttu-id="0cb30-167">The samples in the next sections have sample code to help you create an authorization header.</span><span class="sxs-lookup"><span data-stu-id="0cb30-167">The samples in the next sections have sample code to help you create an authorization header.</span></span>

## <a name="request-body"></a><span data-ttu-id="0cb30-168">Request body</span><span class="sxs-lookup"><span data-stu-id="0cb30-168">Request body</span></span>
<span data-ttu-id="0cb30-169">The body of the message must be in JSON.</span><span class="sxs-lookup"><span data-stu-id="0cb30-169">The body of the message must be in JSON.</span></span> <span data-ttu-id="0cb30-170">It must include one or more records with the property name and value pairs in this format:</span><span class="sxs-lookup"><span data-stu-id="0cb30-170">It must include one or more records with the property name and value pairs in this format:</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

<span data-ttu-id="0cb30-171">You can batch multiple records together in a single request by using the following format.</span><span class="sxs-lookup"><span data-stu-id="0cb30-171">You can batch multiple records together in a single request by using the following format.</span></span> <span data-ttu-id="0cb30-172">All the records must be the same record type.</span><span class="sxs-lookup"><span data-stu-id="0cb30-172">All the records must be the same record type.</span></span>

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
},
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

## <a name="record-type-and-properties"></a><span data-ttu-id="0cb30-173">Record type and properties</span><span class="sxs-lookup"><span data-stu-id="0cb30-173">Record type and properties</span></span>
<span data-ttu-id="0cb30-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span><span class="sxs-lookup"><span data-stu-id="0cb30-174">You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API.</span></span> <span data-ttu-id="0cb30-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span><span class="sxs-lookup"><span data-stu-id="0cb30-175">Currently, you can't write data to existing record types that were created by other data types and solutions.</span></span> <span data-ttu-id="0cb30-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span><span class="sxs-lookup"><span data-stu-id="0cb30-176">Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.</span></span>

<span data-ttu-id="0cb30-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span><span class="sxs-lookup"><span data-stu-id="0cb30-177">Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type.</span></span> <span data-ttu-id="0cb30-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span><span class="sxs-lookup"><span data-stu-id="0cb30-178">The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log.</span></span> <span data-ttu-id="0cb30-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-179">For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**.</span></span> <span data-ttu-id="0cb30-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span><span class="sxs-lookup"><span data-stu-id="0cb30-180">This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.</span></span>

<span data-ttu-id="0cb30-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span><span class="sxs-lookup"><span data-stu-id="0cb30-181">To identify a property's data type, Log Analytics adds a suffix to the property name.</span></span> <span data-ttu-id="0cb30-182">If a property contains a null value, the property is not included in that record.</span><span class="sxs-lookup"><span data-stu-id="0cb30-182">If a property contains a null value, the property is not included in that record.</span></span> <span data-ttu-id="0cb30-183">This table lists the property data type and corresponding suffix:</span><span class="sxs-lookup"><span data-stu-id="0cb30-183">This table lists the property data type and corresponding suffix:</span></span>

| <span data-ttu-id="0cb30-184">Property data type</span><span class="sxs-lookup"><span data-stu-id="0cb30-184">Property data type</span></span> | <span data-ttu-id="0cb30-185">Suffix</span><span class="sxs-lookup"><span data-stu-id="0cb30-185">Suffix</span></span> |
|:--- |:--- |
| <span data-ttu-id="0cb30-186">String</span><span class="sxs-lookup"><span data-stu-id="0cb30-186">String</span></span> |<span data-ttu-id="0cb30-187">_s</span><span class="sxs-lookup"><span data-stu-id="0cb30-187">_s</span></span> |
| <span data-ttu-id="0cb30-188">Boolean</span><span class="sxs-lookup"><span data-stu-id="0cb30-188">Boolean</span></span> |<span data-ttu-id="0cb30-189">_b</span><span class="sxs-lookup"><span data-stu-id="0cb30-189">_b</span></span> |
| <span data-ttu-id="0cb30-190">Double</span><span class="sxs-lookup"><span data-stu-id="0cb30-190">Double</span></span> |<span data-ttu-id="0cb30-191">_d</span><span class="sxs-lookup"><span data-stu-id="0cb30-191">_d</span></span> |
| <span data-ttu-id="0cb30-192">Date/time</span><span class="sxs-lookup"><span data-stu-id="0cb30-192">Date/time</span></span> |<span data-ttu-id="0cb30-193">_t</span><span class="sxs-lookup"><span data-stu-id="0cb30-193">_t</span></span> |
| <span data-ttu-id="0cb30-194">GUID</span><span class="sxs-lookup"><span data-stu-id="0cb30-194">GUID</span></span> |<span data-ttu-id="0cb30-195">_g</span><span class="sxs-lookup"><span data-stu-id="0cb30-195">_g</span></span> |

<span data-ttu-id="0cb30-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span><span class="sxs-lookup"><span data-stu-id="0cb30-196">The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.</span></span>

* <span data-ttu-id="0cb30-197">If the record type does not exist, Log Analytics creates a new one.</span><span class="sxs-lookup"><span data-stu-id="0cb30-197">If the record type does not exist, Log Analytics creates a new one.</span></span> <span data-ttu-id="0cb30-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span><span class="sxs-lookup"><span data-stu-id="0cb30-198">Log Analytics uses the JSON type inference to determine the data type for each property for the new record.</span></span>
* <span data-ttu-id="0cb30-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span><span class="sxs-lookup"><span data-stu-id="0cb30-199">If the record type does exist, Log Analytics attempts to create a new record based on existing properties.</span></span> <span data-ttu-id="0cb30-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span><span class="sxs-lookup"><span data-stu-id="0cb30-200">If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.</span></span>

<span data-ttu-id="0cb30-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span><span class="sxs-lookup"><span data-stu-id="0cb30-201">For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:</span></span>

![Sample record 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-01.png)

<span data-ttu-id="0cb30-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span><span class="sxs-lookup"><span data-stu-id="0cb30-203">If you then submitted this next entry, with all values formatted as strings, the properties would not change.</span></span> <span data-ttu-id="0cb30-204">These values can be converted to existing data types:</span><span class="sxs-lookup"><span data-stu-id="0cb30-204">These values can be converted to existing data types:</span></span>

![Sample record 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-02.png)

<span data-ttu-id="0cb30-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-206">But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**.</span></span> <span data-ttu-id="0cb30-207">These values can't be converted:</span><span class="sxs-lookup"><span data-stu-id="0cb30-207">These values can't be converted:</span></span>

![Sample record 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-03.png)

<span data-ttu-id="0cb30-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-209">If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**.</span></span> <span data-ttu-id="0cb30-210">In this entry, each of the initial values is formatted as a string:</span><span class="sxs-lookup"><span data-stu-id="0cb30-210">In this entry, each of the initial values is formatted as a string:</span></span>

![Sample record 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a><span data-ttu-id="0cb30-212">Data limits</span><span class="sxs-lookup"><span data-stu-id="0cb30-212">Data limits</span></span>
<span data-ttu-id="0cb30-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span><span class="sxs-lookup"><span data-stu-id="0cb30-213">There are some constraints around the data posted to the Log Analytics Data collection API.</span></span>

* <span data-ttu-id="0cb30-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span><span class="sxs-lookup"><span data-stu-id="0cb30-214">Maximum of 30 MB per post to Log Analytics Data Collector API.</span></span> <span data-ttu-id="0cb30-215">This is a size limit for a single post.</span><span class="sxs-lookup"><span data-stu-id="0cb30-215">This is a size limit for a single post.</span></span> <span data-ttu-id="0cb30-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span><span class="sxs-lookup"><span data-stu-id="0cb30-216">If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently.</span></span> 
* <span data-ttu-id="0cb30-217">Maximum of 32 KB limit for field values.</span><span class="sxs-lookup"><span data-stu-id="0cb30-217">Maximum of 32 KB limit for field values.</span></span> <span data-ttu-id="0cb30-218">If the field value is greater than 32 KB, the data will be truncated.</span><span class="sxs-lookup"><span data-stu-id="0cb30-218">If the field value is greater than 32 KB, the data will be truncated.</span></span> 
* <span data-ttu-id="0cb30-219">Recommended maximum number of fields for a given type is 50.</span><span class="sxs-lookup"><span data-stu-id="0cb30-219">Recommended maximum number of fields for a given type is 50.</span></span> <span data-ttu-id="0cb30-220">This is a practical limit from a usability and search experience perspective.</span><span class="sxs-lookup"><span data-stu-id="0cb30-220">This is a practical limit from a usability and search experience perspective.</span></span>  

## <a name="return-codes"></a><span data-ttu-id="0cb30-221">Return codes</span><span class="sxs-lookup"><span data-stu-id="0cb30-221">Return codes</span></span>
<span data-ttu-id="0cb30-222">The HTTP status code 200 means that the request has been received for processing.</span><span class="sxs-lookup"><span data-stu-id="0cb30-222">The HTTP status code 200 means that the request has been received for processing.</span></span> <span data-ttu-id="0cb30-223">This indicates that the operation completed successfully.</span><span class="sxs-lookup"><span data-stu-id="0cb30-223">This indicates that the operation completed successfully.</span></span>

<span data-ttu-id="0cb30-224">This table lists the complete set of status codes that the service might return:</span><span class="sxs-lookup"><span data-stu-id="0cb30-224">This table lists the complete set of status codes that the service might return:</span></span>

| <span data-ttu-id="0cb30-225">Code</span><span class="sxs-lookup"><span data-stu-id="0cb30-225">Code</span></span> | <span data-ttu-id="0cb30-226">Status</span><span class="sxs-lookup"><span data-stu-id="0cb30-226">Status</span></span> | <span data-ttu-id="0cb30-227">Error code</span><span class="sxs-lookup"><span data-stu-id="0cb30-227">Error code</span></span> | <span data-ttu-id="0cb30-228">Description</span><span class="sxs-lookup"><span data-stu-id="0cb30-228">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="0cb30-229">200</span><span class="sxs-lookup"><span data-stu-id="0cb30-229">200</span></span> |<span data-ttu-id="0cb30-230">OK</span><span class="sxs-lookup"><span data-stu-id="0cb30-230">OK</span></span> | |<span data-ttu-id="0cb30-231">The request was successfully accepted.</span><span class="sxs-lookup"><span data-stu-id="0cb30-231">The request was successfully accepted.</span></span> |
| <span data-ttu-id="0cb30-232">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-232">400</span></span> |<span data-ttu-id="0cb30-233">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-233">Bad request</span></span> |<span data-ttu-id="0cb30-234">InactiveCustomer</span><span class="sxs-lookup"><span data-stu-id="0cb30-234">InactiveCustomer</span></span> |<span data-ttu-id="0cb30-235">The workspace has been closed.</span><span class="sxs-lookup"><span data-stu-id="0cb30-235">The workspace has been closed.</span></span> |
| <span data-ttu-id="0cb30-236">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-236">400</span></span> |<span data-ttu-id="0cb30-237">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-237">Bad request</span></span> |<span data-ttu-id="0cb30-238">InvalidApiVersion</span><span class="sxs-lookup"><span data-stu-id="0cb30-238">InvalidApiVersion</span></span> |<span data-ttu-id="0cb30-239">The API version that you specified was not recognized by the service.</span><span class="sxs-lookup"><span data-stu-id="0cb30-239">The API version that you specified was not recognized by the service.</span></span> |
| <span data-ttu-id="0cb30-240">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-240">400</span></span> |<span data-ttu-id="0cb30-241">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-241">Bad request</span></span> |<span data-ttu-id="0cb30-242">InvalidCustomerId</span><span class="sxs-lookup"><span data-stu-id="0cb30-242">InvalidCustomerId</span></span> |<span data-ttu-id="0cb30-243">The workspace ID specified is invalid.</span><span class="sxs-lookup"><span data-stu-id="0cb30-243">The workspace ID specified is invalid.</span></span> |
| <span data-ttu-id="0cb30-244">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-244">400</span></span> |<span data-ttu-id="0cb30-245">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-245">Bad request</span></span> |<span data-ttu-id="0cb30-246">InvalidDataFormat</span><span class="sxs-lookup"><span data-stu-id="0cb30-246">InvalidDataFormat</span></span> |<span data-ttu-id="0cb30-247">Invalid JSON was submitted.</span><span class="sxs-lookup"><span data-stu-id="0cb30-247">Invalid JSON was submitted.</span></span> <span data-ttu-id="0cb30-248">The response body might contain more information about how to resolve the error.</span><span class="sxs-lookup"><span data-stu-id="0cb30-248">The response body might contain more information about how to resolve the error.</span></span> |
| <span data-ttu-id="0cb30-249">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-249">400</span></span> |<span data-ttu-id="0cb30-250">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-250">Bad request</span></span> |<span data-ttu-id="0cb30-251">InvalidLogType</span><span class="sxs-lookup"><span data-stu-id="0cb30-251">InvalidLogType</span></span> |<span data-ttu-id="0cb30-252">The log type specified contained special characters or numerics.</span><span class="sxs-lookup"><span data-stu-id="0cb30-252">The log type specified contained special characters or numerics.</span></span> |
| <span data-ttu-id="0cb30-253">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-253">400</span></span> |<span data-ttu-id="0cb30-254">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-254">Bad request</span></span> |<span data-ttu-id="0cb30-255">MissingApiVersion</span><span class="sxs-lookup"><span data-stu-id="0cb30-255">MissingApiVersion</span></span> |<span data-ttu-id="0cb30-256">The API version wasn’t specified.</span><span class="sxs-lookup"><span data-stu-id="0cb30-256">The API version wasn’t specified.</span></span> |
| <span data-ttu-id="0cb30-257">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-257">400</span></span> |<span data-ttu-id="0cb30-258">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-258">Bad request</span></span> |<span data-ttu-id="0cb30-259">MissingContentType</span><span class="sxs-lookup"><span data-stu-id="0cb30-259">MissingContentType</span></span> |<span data-ttu-id="0cb30-260">The content type wasn’t specified.</span><span class="sxs-lookup"><span data-stu-id="0cb30-260">The content type wasn’t specified.</span></span> |
| <span data-ttu-id="0cb30-261">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-261">400</span></span> |<span data-ttu-id="0cb30-262">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-262">Bad request</span></span> |<span data-ttu-id="0cb30-263">MissingLogType</span><span class="sxs-lookup"><span data-stu-id="0cb30-263">MissingLogType</span></span> |<span data-ttu-id="0cb30-264">The required value log type wasn’t specified.</span><span class="sxs-lookup"><span data-stu-id="0cb30-264">The required value log type wasn’t specified.</span></span> |
| <span data-ttu-id="0cb30-265">400</span><span class="sxs-lookup"><span data-stu-id="0cb30-265">400</span></span> |<span data-ttu-id="0cb30-266">Bad request</span><span class="sxs-lookup"><span data-stu-id="0cb30-266">Bad request</span></span> |<span data-ttu-id="0cb30-267">UnsupportedContentType</span><span class="sxs-lookup"><span data-stu-id="0cb30-267">UnsupportedContentType</span></span> |<span data-ttu-id="0cb30-268">The content type was not set to **application/json**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-268">The content type was not set to **application/json**.</span></span> |
| <span data-ttu-id="0cb30-269">403</span><span class="sxs-lookup"><span data-stu-id="0cb30-269">403</span></span> |<span data-ttu-id="0cb30-270">Forbidden</span><span class="sxs-lookup"><span data-stu-id="0cb30-270">Forbidden</span></span> |<span data-ttu-id="0cb30-271">InvalidAuthorization</span><span class="sxs-lookup"><span data-stu-id="0cb30-271">InvalidAuthorization</span></span> |<span data-ttu-id="0cb30-272">The service failed to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-272">The service failed to authenticate the request.</span></span> <span data-ttu-id="0cb30-273">Verify that the workspace ID and connection key are valid.</span><span class="sxs-lookup"><span data-stu-id="0cb30-273">Verify that the workspace ID and connection key are valid.</span></span> |
| <span data-ttu-id="0cb30-274">404</span><span class="sxs-lookup"><span data-stu-id="0cb30-274">404</span></span> |<span data-ttu-id="0cb30-275">Not Found</span><span class="sxs-lookup"><span data-stu-id="0cb30-275">Not Found</span></span> | | <span data-ttu-id="0cb30-276">Either the URL provided is incorrect, or the request is too large.</span><span class="sxs-lookup"><span data-stu-id="0cb30-276">Either the URL provided is incorrect, or the request is too large.</span></span> |
| <span data-ttu-id="0cb30-277">429</span><span class="sxs-lookup"><span data-stu-id="0cb30-277">429</span></span> |<span data-ttu-id="0cb30-278">Too Many Requests</span><span class="sxs-lookup"><span data-stu-id="0cb30-278">Too Many Requests</span></span> | | <span data-ttu-id="0cb30-279">The service is experiencing a high volume of data from your account.</span><span class="sxs-lookup"><span data-stu-id="0cb30-279">The service is experiencing a high volume of data from your account.</span></span> <span data-ttu-id="0cb30-280">Please retry the request later.</span><span class="sxs-lookup"><span data-stu-id="0cb30-280">Please retry the request later.</span></span> |
| <span data-ttu-id="0cb30-281">500</span><span class="sxs-lookup"><span data-stu-id="0cb30-281">500</span></span> |<span data-ttu-id="0cb30-282">Internal Server Error</span><span class="sxs-lookup"><span data-stu-id="0cb30-282">Internal Server Error</span></span> |<span data-ttu-id="0cb30-283">UnspecifiedError</span><span class="sxs-lookup"><span data-stu-id="0cb30-283">UnspecifiedError</span></span> |<span data-ttu-id="0cb30-284">The service encountered an internal error.</span><span class="sxs-lookup"><span data-stu-id="0cb30-284">The service encountered an internal error.</span></span> <span data-ttu-id="0cb30-285">Please retry the request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-285">Please retry the request.</span></span> |
| <span data-ttu-id="0cb30-286">503</span><span class="sxs-lookup"><span data-stu-id="0cb30-286">503</span></span> |<span data-ttu-id="0cb30-287">Service Unavailable</span><span class="sxs-lookup"><span data-stu-id="0cb30-287">Service Unavailable</span></span> |<span data-ttu-id="0cb30-288">ServiceUnavailable</span><span class="sxs-lookup"><span data-stu-id="0cb30-288">ServiceUnavailable</span></span> |<span data-ttu-id="0cb30-289">The service currently is unavailable to receive requests.</span><span class="sxs-lookup"><span data-stu-id="0cb30-289">The service currently is unavailable to receive requests.</span></span> <span data-ttu-id="0cb30-290">Please retry your request.</span><span class="sxs-lookup"><span data-stu-id="0cb30-290">Please retry your request.</span></span> |

## <a name="query-data"></a><span data-ttu-id="0cb30-291">Query data</span><span class="sxs-lookup"><span data-stu-id="0cb30-291">Query data</span></span>
<span data-ttu-id="0cb30-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-292">To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**.</span></span> <span data-ttu-id="0cb30-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span><span class="sxs-lookup"><span data-stu-id="0cb30-293">For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.</span></span>

## <a name="sample-requests"></a><span data-ttu-id="0cb30-294">Sample requests</span><span class="sxs-lookup"><span data-stu-id="0cb30-294">Sample requests</span></span>
<span data-ttu-id="0cb30-295">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span><span class="sxs-lookup"><span data-stu-id="0cb30-295">In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.</span></span>

<span data-ttu-id="0cb30-296">For each sample, do these steps to set the variables for the authorization header:</span><span class="sxs-lookup"><span data-stu-id="0cb30-296">For each sample, do these steps to set the variables for the authorization header:</span></span>

1. <span data-ttu-id="0cb30-297">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span><span class="sxs-lookup"><span data-stu-id="0cb30-297">In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.</span></span>
2. <span data-ttu-id="0cb30-298">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span><span class="sxs-lookup"><span data-stu-id="0cb30-298">To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.</span></span>
3. <span data-ttu-id="0cb30-299">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span><span class="sxs-lookup"><span data-stu-id="0cb30-299">To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.</span></span>

<span data-ttu-id="0cb30-300">Alternatively, you can change the variables for the log type and JSON data.</span><span class="sxs-lookup"><span data-stu-id="0cb30-300">Alternatively, you can change the variables for the log type and JSON data.</span></span>

### <a name="powershell-sample"></a><span data-ttu-id="0cb30-301">PowerShell sample</span><span class="sxs-lookup"><span data-stu-id="0cb30-301">PowerShell sample</span></span>
```
# Replace with your Workspace ID
$CustomerId = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"  

# Replace with your Primary Key
$SharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# Specify the name of the record type that you'll be creating
$LogType = "MyRecordType"

# Specify a field with the created time for the records
$TimeStampField = "DateValue"


# Create two records with the same set of properties to create
$json = @"
[{  "StringValue": "MyString1",
    "NumberValue": 42,
    "BooleanValue": true,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "9909ED01-A74C-4874-8ABF-D2678E3AE23D"
},
{   "StringValue": "MyString2",
    "NumberValue": 43,
    "BooleanValue": false,
    "DateValue": "2016-05-12T20:00:00.625Z",
    "GUIDValue": "8809ED01-A74C-4874-8ABF-D2678E3AE23D"
}]
"@

# Create the function to create the authorization signature
Function Build-Signature ($customerId, $sharedKey, $date, $contentLength, $method, $contentType, $resource)
{
    $xHeaders = "x-ms-date:" + $date
    $stringToHash = $method + "`n" + $contentLength + "`n" + $contentType + "`n" + $xHeaders + "`n" + $resource

    $bytesToHash = [Text.Encoding]::UTF8.GetBytes($stringToHash)
    $keyBytes = [Convert]::FromBase64String($sharedKey)

    $sha256 = New-Object System.Security.Cryptography.HMACSHA256
    $sha256.Key = $keyBytes
    $calculatedHash = $sha256.ComputeHash($bytesToHash)
    $encodedHash = [Convert]::ToBase64String($calculatedHash)
    $authorization = 'SharedKey {0}:{1}' -f $customerId,$encodedHash
    return $authorization
}


# Create the function to create and post the request
Function Post-OMSData($customerId, $sharedKey, $body, $logType)
{
    $method = "POST"
    $contentType = "application/json"
    $resource = "/api/logs"
    $rfc1123date = [DateTime]::UtcNow.ToString("r")
    $contentLength = $body.Length
    $signature = Build-Signature `
        -customerId $customerId `
        -sharedKey $sharedKey `
        -date $rfc1123date `
        -contentLength $contentLength `
        -fileName $fileName `
        -method $method `
        -contentType $contentType `
        -resource $resource
    $uri = "https://" + $customerId + ".ods.opinsights.azure.com" + $resource + "?api-version=2016-04-01"

    $headers = @{
        "Authorization" = $signature;
        "Log-Type" = $logType;
        "x-ms-date" = $rfc1123date;
        "time-generated-field" = $TimeStampField;
    }

    $response = Invoke-WebRequest -Uri $uri -Method $method -ContentType $contentType -Headers $headers -Body $body -UseBasicParsing
    return $response.StatusCode

}

# Submit the data to the API endpoint
Post-OMSData -customerId $customerId -sharedKey $sharedKey -body ([System.Text.Encoding]::UTF8.GetBytes($json)) -logType $logType  
```

### <a name="c-sample"></a><span data-ttu-id="0cb30-302">C# sample</span><span class="sxs-lookup"><span data-stu-id="0cb30-302">C# sample</span></span>
```
using System;
using System.Net;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Security.Cryptography;
using System.Text;
using System.Threading.Tasks;

namespace OIAPIExample
{
    class ApiExample
    {
        // An example JSON object, with key/value pairs
        static string json = @"[{""DemoField1"":""DemoValue1"",""DemoField2"":""DemoValue2""},{""DemoField3"":""DemoValue3"",""DemoField4"":""DemoValue4""}]";

        // Update customerId to your Operations Management Suite workspace ID
        static string customerId = "xxxxxxxx-xxx-xxx-xxx-xxxxxxxxxxxx";

        // For sharedKey, use either the primary or the secondary Connected Sources client authentication key   
        static string sharedKey = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx";

        // LogName is name of the event type that is being submitted to Log Analytics
        static string LogName = "DemoExample";

        // You can use an optional field to specify the timestamp from the data. If the time field is not specified, Log Analytics assumes the time is the message ingestion time
        static string TimeStampField = "";

        static void Main()
        {
            // Create a hash for the API signature
            var datestring = DateTime.UtcNow.ToString("r");
            string stringToHash = "POST\n" + json.Length + "\napplication/json\n" + "x-ms-date:" + datestring + "\n/api/logs";
            string hashedString = BuildSignature(stringToHash, sharedKey);
            string signature = "SharedKey " + customerId + ":" + hashedString;
    
            PostData(signature, datestring, json);
        }

        // Build the API signature
        public static string BuildSignature(string message, string secret)
        {
            var encoding = new System.Text.ASCIIEncoding();
            byte[] keyByte = Convert.FromBase64String(secret);
            byte[] messageBytes = encoding.GetBytes(message);
            using (var hmacsha256 = new HMACSHA256(keyByte))
            {
                byte[] hash = hmacsha256.ComputeHash(messageBytes);
                return Convert.ToBase64String(hash);
            }
        }

        // Send a request to the POST API endpoint
        public static void PostData(string signature, string date, string json)
        {
            try
            { 
                string url = "https://" + customerId + ".ods.opinsights.azure.com/api/logs?api-version=2016-04-01";
    
                System.Net.Http.HttpClient client = new System.Net.Http.HttpClient();
                client.DefaultRequestHeaders.Add("Accept", "application/json");
                client.DefaultRequestHeaders.Add("Log-Type", LogName);
                client.DefaultRequestHeaders.Add("Authorization", signature);
                client.DefaultRequestHeaders.Add("x-ms-date", date);
                client.DefaultRequestHeaders.Add("time-generated-field", TimeStampField);
    
                System.Net.Http.HttpContent httpContent = new StringContent(json, Encoding.UTF8);
                httpContent.Headers.ContentType = new MediaTypeHeaderValue("application/json");
                Task<System.Net.Http.HttpResponseMessage> response = client.PostAsync(new Uri(url), httpContent);
    
                System.Net.Http.HttpContent responseContent = response.Result.Content;
                string result = responseContent.ReadAsStringAsync().Result;
                Console.WriteLine("Return Result: " + result);
            }
            catch (Exception excep)
            {
                Console.WriteLine("API Post Exception: " + excep.Message);
            }
        }
    }
}

```

### <a name="python-sample"></a><span data-ttu-id="0cb30-303">Python sample</span><span class="sxs-lookup"><span data-stu-id="0cb30-303">Python sample</span></span>
```
import json
import requests
import datetime
import hashlib
import hmac
import base64

# Update the customer ID to your Operations Management Suite workspace ID
customer_id = 'xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'

# For the shared key, use either the primary or the secondary Connected Sources client authentication key   
shared_key = "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"

# The log type is the name of the event that is being submitted
log_type = 'WebMonitorTest'

# An example JSON web monitor object
json_data = [{
   "slot_ID": 12345,
    "ID": "5cdad72f-c848-4df0-8aaa-ffe033e75d57",
    "availability_Value": 100,
    "performance_Value": 6.954,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "true"
},
{   
    "slot_ID": 67890,
    "ID": "b6bee458-fb65-492e-996d-61c4d7fbb942",
    "availability_Value": 100,
    "performance_Value": 3.379,
    "measurement_Name": "last_one_hour",
    "duration": 3600,
    "warning_Threshold": 0,
    "critical_Threshold": 0,
    "IsActive": "false"
}]
body = json.dumps(json_data)

#####################
######Functions######  
#####################

# Build the API signature
def build_signature(customer_id, shared_key, date, content_length, method, content_type, resource):
    x_headers = 'x-ms-date:' + date
    string_to_hash = method + "\n" + str(content_length) + "\n" + content_type + "\n" + x_headers + "\n" + resource
    bytes_to_hash = bytes(string_to_hash).encode('utf-8')  
    decoded_key = base64.b64decode(shared_key)
    encoded_hash = base64.b64encode(hmac.new(decoded_key, bytes_to_hash, digestmod=hashlib.sha256).digest())
    authorization = "SharedKey {}:{}".format(customer_id,encoded_hash)
    return authorization

# Build and send a request to the POST API
def post_data(customer_id, shared_key, body, log_type):
    method = 'POST'
    content_type = 'application/json'
    resource = '/api/logs'
    rfc1123date = datetime.datetime.utcnow().strftime('%a, %d %b %Y %H:%M:%S GMT')
    content_length = len(body)
    signature = build_signature(customer_id, shared_key, rfc1123date, content_length, method, content_type, resource)
    uri = 'https://' + customer_id + '.ods.opinsights.azure.com' + resource + '?api-version=2016-04-01'

    headers = {
        'content-type': content_type,
        'Authorization': signature,
        'Log-Type': log_type,
        'x-ms-date': rfc1123date
    }

    response = requests.post(uri,data=body, headers=headers)
    if (response.status_code >= 200 and response.status_code <= 299):
        print 'Accepted'
    else:
        print "Response code: {}".format(response.status_code)

post_data(customer_id, shared_key, body, log_type)
```

## <a name="next-steps"></a><span data-ttu-id="0cb30-304">Next steps</span><span class="sxs-lookup"><span data-stu-id="0cb30-304">Next steps</span></span>
- <span data-ttu-id="0cb30-305">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span><span class="sxs-lookup"><span data-stu-id="0cb30-305">Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.</span></span>





