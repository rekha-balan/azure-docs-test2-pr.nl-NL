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
# <a name="send-data-to-log-analytics-with-the-http-data-collector-api"></a>Send data to Log Analytics with the HTTP Data Collector API
This article shows you how to use the HTTP Data Collector API to send data to Log Analytics from a REST API client.  It describes how to format data collected by your script or application, include it in a request, and have that request authorized by Log Analytics.  Examples are provided for PowerShell, C#, and Python.

## <a name="concepts"></a>Concepts
You can use the HTTP Data Collector API to send data to Log Analytics from any client that can call a REST API.  This might be a runbook in Azure Automation that collects management data from Azure or another cloud, or it might be an alternate management system that uses Log Analytics to consolidate and analyze data.

All data in the Log Analytics repository is stored as a record with a particular record type.  You format your data to send to the HTTP Data Collector API as multiple records in JSON.  When you submit the data, an individual record is created in the repository for each record in the request payload.


![HTTP Data Collector overview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/overview.png)



## <a name="create-a-request"></a>Create a request
To use the HTTP Data Collector API, you create a POST request that includes the data to send in JavaScript Object Notation (JSON).  The next three tables list the attributes that are required for each request. We describe each attribute in more detail later in the article.

### <a name="request-uri"></a>Request URI
| Attribute | Property |
|:--- |:--- |
| Method |POST |
| URI |https://\<CustomerId\>.ods.opinsights.azure.com/api/logs?api-version=2016-04-01 |
| Content type |application/json |

### <a name="request-uri-parameters"></a>Request URI parameters
| Parameter | Description |
|:--- |:--- |
| CustomerID |The unique identifier for the Microsoft Operations Management Suite workspace. |
| Resource |The API resource name: /api/logs. |
| API Version |The version of the API to use with this request. Currently, it's 2016-04-01. |

### <a name="request-headers"></a>Request headers
| Header | Description |
|:--- |:--- |
| Authorization |The authorization signature. Later in the article, you can read about how to create an HMAC-SHA256 header. |
| Log-Type |Specify the record type of the data that is being submitted. Currently, the log type supports only alpha characters. It does not support numerics or special characters. |
| x-ms-date |The date that the request was processed, in RFC 1123 format. |
| time-generated-field |The name of a field in the data that contains the timestamp of the data item. If you specify a field then its contents are used for **TimeGenerated**. If this field isn’t specified, the default for **TimeGenerated** is the time that the message is ingested. The contents of the message field should follow the ISO 8601 format YYYY-MM-DDThh:mm:ssZ. |

## <a name="authorization"></a>Authorization
Any request to the Log Analytics HTTP Data Collector API must include an authorization header. To authenticate a request, you must sign the request with either the primary or the secondary key for the workspace that is making the request. Then, pass that signature as part of the request.   

Here's the format for the authorization header:

```
Authorization: SharedKey <WorkspaceID>:<Signature>
```

*WorkspaceID* is the unique identifier for the Operations Management Suite workspace. *Signature* is a [Hash-based Message Authentication Code (HMAC)](https://msdn.microsoft.com/library/system.security.cryptography.hmacsha256.aspx) that is constructed from the request and then computed by using the [SHA256 algorithm](https://msdn.microsoft.com/library/system.security.cryptography.sha256.aspx). Then, you encode it by using Base64 encoding.

Use this format to encode the **SharedKey** signature string:

```
StringToSign = VERB + "\n" +
                  Content-Length + "\n" +
               Content-Type + "\n" +
                  x-ms-date + "\n" +
                  "/api/logs";
```

Here's an example of a signature string:

```
POST\n1024\napplication/json\nx-ms-date:Mon, 04 Apr 2016 08:00:00 GMT\n/api/logs
```

When you have the signature string, encode it by using the HMAC-SHA256 algorithm on the UTF-8-encoded string, and then encode the result as Base64. Use this format:

```
Signature=Base64(HMAC-SHA256(UTF8(StringToSign)))
```

The samples in the next sections have sample code to help you create an authorization header.

## <a name="request-body"></a>Request body
The body of the message must be in JSON. It must include one or more records with the property name and value pairs in this format:

```
{
"property1": "value1",
" property 2": "value2"
" property 3": "value3",
" property 4": "value4"
}
```

You can batch multiple records together in a single request by using the following format. All the records must be the same record type.

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

## <a name="record-type-and-properties"></a>Record type and properties
You define a custom record type when you submit data through the Log Analytics HTTP Data Collector API. Currently, you can't write data to existing record types that were created by other data types and solutions. Log Analytics reads the incoming data and then creates properties that match the data types of the values that you enter.

Each request to the Log Analytics API must include a **Log-Type** header with the name for the record type. The suffix **_CL** is automatically appended to the name you enter to distinguish it from other log types as a custom log. For example, if you enter the name **MyNewRecordType**, Log Analytics creates a record with the type **MyNewRecordType_CL**. This helps ensure that there are no conflicts between user-created type names and those shipped in current or future Microsoft solutions.

To identify a property's data type, Log Analytics adds a suffix to the property name. If a property contains a null value, the property is not included in that record. This table lists the property data type and corresponding suffix:

| Property data type | Suffix |
|:--- |:--- |
| String |_s |
| Boolean |_b |
| Double |_d |
| Date/time |_t |
| GUID |_g |

The data type that Log Analytics uses for each property depends on whether the record type for the new record already exists.

* If the record type does not exist, Log Analytics creates a new one. Log Analytics uses the JSON type inference to determine the data type for each property for the new record.
* If the record type does exist, Log Analytics attempts to create a new record based on existing properties. If the data type for a property in the new record doesn’t match and can’t be converted to the existing type, or if the record includes a property that doesn’t exist, Log Analytics creates a new property that has the relevant suffix.

For example, this submission entry would create a record with three properties, **number_d**, **boolean_b**, and **string_s**:

![Sample record 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-01.png)

If you then submitted this next entry, with all values formatted as strings, the properties would not change. These values can be converted to existing data types:

![Sample record 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-02.png)

But, if you then made this next submission, Log Analytics would create the new properties **boolean_d** and **string_d**. These values can't be converted:

![Sample record 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-03.png)

If you then submitted the following entry, before the record type was created, Log Analytics would create a record with three properties, **number_s**, **boolean_s**, and **string_s**. In this entry, each of the initial values is formatted as a string:

![Sample record 4](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-data-collector-api/record-04.png)

## <a name="data-limits"></a>Data limits
There are some constraints around the data posted to the Log Analytics Data collection API.

* Maximum of 30 MB per post to Log Analytics Data Collector API. This is a size limit for a single post. If the data from a single post that exceeds 30 MB, you should split the data up to smaller sized chunks and send them concurrently. 
* Maximum of 32 KB limit for field values. If the field value is greater than 32 KB, the data will be truncated. 
* Recommended maximum number of fields for a given type is 50. This is a practical limit from a usability and search experience perspective.  

## <a name="return-codes"></a>Return codes
The HTTP status code 200 means that the request has been received for processing. This indicates that the operation completed successfully.

This table lists the complete set of status codes that the service might return:

| Code | Status | Error code | Description |
|:--- |:--- |:--- |:--- |
| 200 |OK | |The request was successfully accepted. |
| 400 |Bad request |InactiveCustomer |The workspace has been closed. |
| 400 |Bad request |InvalidApiVersion |The API version that you specified was not recognized by the service. |
| 400 |Bad request |InvalidCustomerId |The workspace ID specified is invalid. |
| 400 |Bad request |InvalidDataFormat |Invalid JSON was submitted. The response body might contain more information about how to resolve the error. |
| 400 |Bad request |InvalidLogType |The log type specified contained special characters or numerics. |
| 400 |Bad request |MissingApiVersion |The API version wasn’t specified. |
| 400 |Bad request |MissingContentType |The content type wasn’t specified. |
| 400 |Bad request |MissingLogType |The required value log type wasn’t specified. |
| 400 |Bad request |UnsupportedContentType |The content type was not set to **application/json**. |
| 403 |Forbidden |InvalidAuthorization |The service failed to authenticate the request. Verify that the workspace ID and connection key are valid. |
| 404 |Not Found | | Either the URL provided is incorrect, or the request is too large. |
| 429 |Too Many Requests | | The service is experiencing a high volume of data from your account. Please retry the request later. |
| 500 |Internal Server Error |UnspecifiedError |The service encountered an internal error. Please retry the request. |
| 503 |Service Unavailable |ServiceUnavailable |The service currently is unavailable to receive requests. Please retry your request. |

## <a name="query-data"></a>Query data
To query data submitted by the Log Analytics HTTP Data Collector API, search for records with **Type** that is equal to the **LogType** value that you specified, appended with **_CL**. For example, if you used **MyCustomLog**, then you'd return all records with **Type=MyCustomLog_CL**.

## <a name="sample-requests"></a>Sample requests
In the next sections, you'll find samples of how to submit data to the Log Analytics HTTP Data Collector API by using different programming languages.

For each sample, do these steps to set the variables for the authorization header:

1. In the Operations Management Suite portal, select the **Settings** tile, and then select the **Connected Sources** tab.
2. To the right of **Workspace ID**, select the copy icon, and then paste the ID as the value of the **Customer ID** variable.
3. To the right of **Primary Key**, select the copy icon, and then paste the ID as the value of the **Shared Key** variable.

Alternatively, you can change the variables for the log type and JSON data.

### <a name="powershell-sample"></a>PowerShell sample
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

### <a name="c-sample"></a>C# sample
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

### <a name="python-sample"></a>Python sample
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

## <a name="next-steps"></a>Next steps
- Use the [Log Search API](log-analytics-log-search-api.md) to retrieve data from the Log Analytics repository.




