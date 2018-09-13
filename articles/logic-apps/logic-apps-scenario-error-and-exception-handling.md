---
title: Exception handling & error logging scenario - Azure Logic Apps | Microsoft Docs
description: Describes a real use case about advanced exception handling and error logging for Azure Logic Apps
keywords: ''
services: logic-apps
author: hedidin
manager: anneta
editor: ''
documentationcenter: ''
ms.assetid: 63b0b843-f6b0-4d9a-98d0-17500be17385
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/29/2016
ms.author: b-hoedid
ms.openlocfilehash: 8b6b1e379245cc93ef5a9d17b8a55d6ab54d0cc3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662158"
---
# <a name="scenario-exception-handling-and-error-logging-for-logic-apps"></a><span data-ttu-id="2750e-103">Scenario: Exception handling and error logging for logic apps</span><span class="sxs-lookup"><span data-stu-id="2750e-103">Scenario: Exception handling and error logging for logic apps</span></span>

<span data-ttu-id="2750e-104">This scenario describes how you can extend a logic app to better support exception handling.</span><span class="sxs-lookup"><span data-stu-id="2750e-104">This scenario describes how you can extend a logic app to better support exception handling.</span></span> <span data-ttu-id="2750e-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span><span class="sxs-lookup"><span data-stu-id="2750e-105">We've used a real-life use case to answer the question: "Does Azure Logic Apps support exception and error handling?"</span></span>

> [!NOTE]
> <span data-ttu-id="2750e-106">The current Azure Logic Apps schema provides a standard template for action responses.</span><span class="sxs-lookup"><span data-stu-id="2750e-106">The current Azure Logic Apps schema provides a standard template for action responses.</span></span> <span data-ttu-id="2750e-107">This template includes both internal validation and error responses returned from an API app.</span><span class="sxs-lookup"><span data-stu-id="2750e-107">This template includes both internal validation and error responses returned from an API app.</span></span>

## <a name="scenario-and-use-case-overview"></a><span data-ttu-id="2750e-108">Scenario and use case overview</span><span class="sxs-lookup"><span data-stu-id="2750e-108">Scenario and use case overview</span></span>

<span data-ttu-id="2750e-109">Here's the story as the use case for this scenario:</span><span class="sxs-lookup"><span data-stu-id="2750e-109">Here's the story as the use case for this scenario:</span></span> 

<span data-ttu-id="2750e-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2750e-110">A well-known healthcare organization engaged us to develop an Azure solution that would create a patient portal by using Microsoft Dynamics CRM Online.</span></span> <span data-ttu-id="2750e-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span><span class="sxs-lookup"><span data-stu-id="2750e-111">They needed to send appointment records between the Dynamics CRM Online patient portal and Salesforce.</span></span> <span data-ttu-id="2750e-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span><span class="sxs-lookup"><span data-stu-id="2750e-112">We were asked to use the [HL7 FHIR](http://www.hl7.org/implement/standards/fhir/) standard for all patient records.</span></span>

<span data-ttu-id="2750e-113">The project had two major requirements:</span><span class="sxs-lookup"><span data-stu-id="2750e-113">The project had two major requirements:</span></span>  

* <span data-ttu-id="2750e-114">A method to log records sent from the Dynamics CRM Online portal</span><span class="sxs-lookup"><span data-stu-id="2750e-114">A method to log records sent from the Dynamics CRM Online portal</span></span>
* <span data-ttu-id="2750e-115">A way to view any errors that occurred within the workflow</span><span class="sxs-lookup"><span data-stu-id="2750e-115">A way to view any errors that occurred within the workflow</span></span>

> [!TIP]
> <span data-ttu-id="2750e-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span><span class="sxs-lookup"><span data-stu-id="2750e-116">For a high-level video about this project, see [Integration User Group](http://www.integrationusergroup.com/logic-apps-support-error-handling/ "Integration User Group").</span></span>

## <a name="how-we-solved-the-problem"></a><span data-ttu-id="2750e-117">How we solved the problem</span><span class="sxs-lookup"><span data-stu-id="2750e-117">How we solved the problem</span></span>

<span data-ttu-id="2750e-118">We chose [Azure DocumentDB](https://azure.microsoft.com/services/documentdb/ "Azure DocumentDB") as a repository for the log and error records (DocumentDB refers to records as documents).</span><span class="sxs-lookup"><span data-stu-id="2750e-118">We chose [Azure DocumentDB](https://azure.microsoft.com/services/documentdb/ "Azure DocumentDB") as a repository for the log and error records (DocumentDB refers to records as documents).</span></span> <span data-ttu-id="2750e-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span><span class="sxs-lookup"><span data-stu-id="2750e-119">Because Azure Logic Apps has a standard template for all responses, we would not have to create a custom schema.</span></span> <span data-ttu-id="2750e-120">We could create an API app to **Insert** and **Query** for both error and log records.</span><span class="sxs-lookup"><span data-stu-id="2750e-120">We could create an API app to **Insert** and **Query** for both error and log records.</span></span> <span data-ttu-id="2750e-121">We could also define a schema for each within the API app.</span><span class="sxs-lookup"><span data-stu-id="2750e-121">We could also define a schema for each within the API app.</span></span>  

<span data-ttu-id="2750e-122">Another requirement was to purge records after a certain date.</span><span class="sxs-lookup"><span data-stu-id="2750e-122">Another requirement was to purge records after a certain date.</span></span> <span data-ttu-id="2750e-123">DocumentDB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span><span class="sxs-lookup"><span data-stu-id="2750e-123">DocumentDB has a property called [Time to Live](https://azure.microsoft.com/blog/documentdb-now-supports-time-to-live-ttl/ "Time to Live") (TTL), which allowed us to set a **Time to Live** value for each record or collection.</span></span> <span data-ttu-id="2750e-124">This capability eliminated the need to manually delete records in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2750e-124">This capability eliminated the need to manually delete records in DocumentDB.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2750e-125">To complete this tutorial, you need to create a DocumentDB database and two collections (Logging and Errors).</span><span class="sxs-lookup"><span data-stu-id="2750e-125">To complete this tutorial, you need to create a DocumentDB database and two collections (Logging and Errors).</span></span>

## <a name="create-the-logic-app"></a><span data-ttu-id="2750e-126">Create the logic app</span><span class="sxs-lookup"><span data-stu-id="2750e-126">Create the logic app</span></span>

<span data-ttu-id="2750e-127">The first step is to create the logic app and open the app in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="2750e-127">The first step is to create the logic app and open the app in Logic App Designer.</span></span> <span data-ttu-id="2750e-128">In this example, we are using parent-child logic apps.</span><span class="sxs-lookup"><span data-stu-id="2750e-128">In this example, we are using parent-child logic apps.</span></span> <span data-ttu-id="2750e-129">Let's assume that we have already created the parent and are going to create one child logic app.</span><span class="sxs-lookup"><span data-stu-id="2750e-129">Let's assume that we have already created the parent and are going to create one child logic app.</span></span>

<span data-ttu-id="2750e-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span><span class="sxs-lookup"><span data-stu-id="2750e-130">Because we are going to log the record coming out of Dynamics CRM Online, let's start at the top.</span></span> <span data-ttu-id="2750e-131">We must use a **Request** trigger because the parent logic app triggers this child.</span><span class="sxs-lookup"><span data-stu-id="2750e-131">We must use a **Request** trigger because the parent logic app triggers this child.</span></span>

### <a name="logic-app-trigger"></a><span data-ttu-id="2750e-132">Logic app trigger</span><span class="sxs-lookup"><span data-stu-id="2750e-132">Logic app trigger</span></span>

<span data-ttu-id="2750e-133">We are using a **Request** trigger as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="2750e-133">We are using a **Request** trigger as shown in the following example:</span></span>

```` json
"triggers": {
        "request": {
          "type": "request",
          "kind": "http",
          "inputs": {
            "schema": {
              "properties": {
                "CRMid": {
                  "type": "string"
                },
                "recordType": {
                  "type": "string"
                },
                "salesforceID": {
                  "type": "string"
                },
                "update": {
                  "type": "boolean"
                }
              },
              "required": [
                "CRMid",
                "recordType",
                "salesforceID",
                "update"
              ],
              "type": "object"
            }
          }
        }
      },

````


## <a name="steps"></a><span data-ttu-id="2750e-134">Steps</span><span class="sxs-lookup"><span data-stu-id="2750e-134">Steps</span></span>

<span data-ttu-id="2750e-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span><span class="sxs-lookup"><span data-stu-id="2750e-135">We must log the source (request) of the patient record from the Dynamics CRM Online portal.</span></span>

1. <span data-ttu-id="2750e-136">We must get a new appointment record from Dynamics CRM Online.</span><span class="sxs-lookup"><span data-stu-id="2750e-136">We must get a new appointment record from Dynamics CRM Online.</span></span>

   <span data-ttu-id="2750e-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span><span class="sxs-lookup"><span data-stu-id="2750e-137">The trigger coming from CRM provides us with the **CRM PatentId**, **record type**, **New or Updated Record** (new or update Boolean value), and **SalesforceId**.</span></span> <span data-ttu-id="2750e-138">The **SalesforceId** can be null because it's only used for an update.</span><span class="sxs-lookup"><span data-stu-id="2750e-138">The **SalesforceId** can be null because it's only used for an update.</span></span>
   <span data-ttu-id="2750e-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span><span class="sxs-lookup"><span data-stu-id="2750e-139">We get the CRM record by using the CRM **PatientID** and the **Record Type**.</span></span>

2. <span data-ttu-id="2750e-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span><span class="sxs-lookup"><span data-stu-id="2750e-140">Next, we need to add our DocumentDB API app **InsertLogEntry** operation as shown here in Logic App Designer.</span></span>

   <span data-ttu-id="2750e-141">**Insert log entry**</span><span class="sxs-lookup"><span data-stu-id="2750e-141">**Insert log entry**</span></span>

   ![Insert Log Entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/lognewpatient.png)

   <span data-ttu-id="2750e-143">**Insert error entry**</span><span class="sxs-lookup"><span data-stu-id="2750e-143">**Insert error entry**</span></span>

   ![Insert Log Entry](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/insertlogentry.png)

   <span data-ttu-id="2750e-145">**Check for create record failure**</span><span class="sxs-lookup"><span data-stu-id="2750e-145">**Check for create record failure**</span></span>

   ![Condition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/condition.png)

## <a name="logic-app-source-code"></a><span data-ttu-id="2750e-147">Logic app source code</span><span class="sxs-lookup"><span data-stu-id="2750e-147">Logic app source code</span></span>

> [!NOTE]
> <span data-ttu-id="2750e-148">The following examples are samples only.</span><span class="sxs-lookup"><span data-stu-id="2750e-148">The following examples are samples only.</span></span> <span data-ttu-id="2750e-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span><span class="sxs-lookup"><span data-stu-id="2750e-149">Because this tutorial is based on an implementation now in production, the value of a **Source Node** might not display properties that are related to scheduling an appointment.></span></span> 

### <a name="logging"></a><span data-ttu-id="2750e-150">Logging</span><span class="sxs-lookup"><span data-stu-id="2750e-150">Logging</span></span>

<span data-ttu-id="2750e-151">The following logic app code sample shows how to handle logging.</span><span class="sxs-lookup"><span data-stu-id="2750e-151">The following logic app code sample shows how to handle logging.</span></span>

#### <a name="log-entry"></a><span data-ttu-id="2750e-152">Log entry</span><span class="sxs-lookup"><span data-stu-id="2750e-152">Log entry</span></span>

<span data-ttu-id="2750e-153">Here is the logic app source code for inserting a log entry.</span><span class="sxs-lookup"><span data-stu-id="2750e-153">Here is the logic app source code for inserting a log entry.</span></span>

``` json
"InsertLogEntry": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "date": "@{outputs('Gets_NewPatientRecord')['headers']['Date']}",
            "operation": "New Patient",
            "patientId": "@{triggerBody()['CRMid']}",
            "providerId": "@{triggerBody()['providerID']}",
            "source": "@{outputs('Gets_NewPatientRecord')['headers']}"
        },
        "method": "post",
        "uri": "https://.../api/Log"
        },
        "runAfter":    {
            "Gets_NewPatientecord": ["Succeeded"]
        }
}
```

#### <a name="log-request"></a><span data-ttu-id="2750e-154">Log request</span><span class="sxs-lookup"><span data-stu-id="2750e-154">Log request</span></span>

<span data-ttu-id="2750e-155">Here is the log request message posted to the API app.</span><span class="sxs-lookup"><span data-stu-id="2750e-155">Here is the log request message posted to the API app.</span></span>

``` json
    {
    "uri": "https://.../api/Log",
    "method": "post",
    "body": {
        "date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "operation": "New Patient",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "providerId": "",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}"
        }
    }

```


#### <a name="log-response"></a><span data-ttu-id="2750e-156">Log response</span><span class="sxs-lookup"><span data-stu-id="2750e-156">Log response</span></span>

<span data-ttu-id="2750e-157">Here is the log response message from the API app.</span><span class="sxs-lookup"><span data-stu-id="2750e-157">Here is the log response message from the API app.</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:32:17 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "964",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "ttl": 2592000,
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0_1465597937",
        "_rid": "XngRAOT6IQEHAAAAAAAAAA==",
        "_self": "dbs/XngRAA==/colls/XngRAOT6IQE=/docs/XngRAOT6IQEHAAAAAAAAAA==/",
        "_ts": 1465597936,
        "_etag": "/"0400fc2f-0000-0000-0000-575b3ff00000/"",
        "patientID": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:56Z",
        "source": "{/"Pragma/":/"no-cache/",/"x-ms-request-id/":/"e750c9a9-bd48-44c4-bbba-1688b6f8a132/",/"OData-Version/":/"4.0/",/"Cache-Control/":/"no-cache/",/"Date/":/"Fri, 10 Jun 2016 22:31:56 GMT/",/"Set-Cookie/":/"ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1/",/"Server/":/"Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0/",/"X-AspNet-Version/":/"4.0.30319/",/"X-Powered-By/":/"ASP.NET/",/"Content-Length/":/"1935/",/"Content-Type/":/"application/json; odata.metadata=minimal; odata.streaming=true/",/"Expires/":/"-1/"}",
        "operation": "New Patient",
        "salesforceId": "",
        "expired": false
    }
}

```

<span data-ttu-id="2750e-158">Now let's look at the error handling steps.</span><span class="sxs-lookup"><span data-stu-id="2750e-158">Now let's look at the error handling steps.</span></span>

### <a name="error-handling"></a><span data-ttu-id="2750e-159">Error handling</span><span class="sxs-lookup"><span data-stu-id="2750e-159">Error handling</span></span>

<span data-ttu-id="2750e-160">The following logic app code sample shows how you can implement error handling.</span><span class="sxs-lookup"><span data-stu-id="2750e-160">The following logic app code sample shows how you can implement error handling.</span></span>

#### <a name="create-error-record"></a><span data-ttu-id="2750e-161">Create error record</span><span class="sxs-lookup"><span data-stu-id="2750e-161">Create error record</span></span>

<span data-ttu-id="2750e-162">Here is the logic app source code for creating an error record.</span><span class="sxs-lookup"><span data-stu-id="2750e-162">Here is the logic app source code for creating an error record.</span></span>

``` json
"actions": {
    "CreateErrorRecord": {
        "metadata": {
        "apiDefinitionUrl": "https://.../swagger/docs/v1",
        "swaggerSource": "website"
        },
        "type": "Http",
        "inputs": {
        "body": {
            "action": "New_Patient",
            "isError": true,
            "crmId": "@{triggerBody()['CRMid']}",
            "patientID": "@{triggerBody()['CRMid']}",
            "message": "@{body('Create_NewPatientRecord')['message']}",
            "providerId": "@{triggerBody()['providerId']}",
            "severity": 4,
            "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
            "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
            "salesforceId": "",
            "update": false
        },
        "method": "post",
        "uri": "https://.../api/CrMtoSfError"
        },
        "runAfter":
        {
            "Create_NewPatientRecord": ["Failed" ]
        }
    }
}             
```

#### <a name="insert-error-into-documentdb--request"></a><span data-ttu-id="2750e-163">Insert error into DocumentDB--request</span><span class="sxs-lookup"><span data-stu-id="2750e-163">Insert error into DocumentDB--request</span></span>

``` json

{
    "uri": "https://.../api/CrMtoSfError",
    "method": "post",
    "body": {
        "action": "New_Patient",
        "isError": true,
        "crmId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "patientId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "providerId": "",
        "severity": 4,
        "salesforceId": "",
        "update": false,
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MasterID_mp__c/":/"/",/"C_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"ONY_ID__c/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "statusCode": "400"
    }
}
```

#### <a name="insert-error-into-documentdb--response"></a><span data-ttu-id="2750e-164">Insert error into DocumentDB--response</span><span class="sxs-lookup"><span data-stu-id="2750e-164">Insert error into DocumentDB--response</span></span>

``` json
{
    "statusCode": 200,
    "headers": {
        "Pragma": "no-cache",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:57 GMT",
        "Server": "Microsoft-IIS/8.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "1561",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "id": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0-1465597917",
        "_rid": "sQx2APhVzAA8AAAAAAAAAA==",
        "_self": "dbs/sQx2AA==/colls/sQx2APhVzAA=/docs/sQx2APhVzAA8AAAAAAAAAA==/",
        "_ts": 1465597912,
        "_etag": "/"0c00eaac-0000-0000-0000-575b3fdc0000/"",
        "prescriberId": "6b115f6d-a7ee-e511-80f5-3863bb2eb2d0",
        "timestamp": "2016-06-10T22:31:57.3651027Z",
        "action": "New_Patient",
        "salesforceId": "",
        "update": false,
        "body": "CRM failed to complete task: Message: duplicate value found: CRM_HUB_ID__c duplicates value on record with id: 001U000001c83gK",
        "source": "{/"Account_Class_vod__c/":/"PRAC/",/"Account_Status_MED__c/":/"I/",/"CRM_HUB_ID__c/":/"6b115f6d-a7ee-e511-80f5-3863bb2eb2d0/",/"Credentials_vod__c/":/"DO - Degree level is DO/",/"DTC_ID_MED__c/":/"/",/"Fax/":/"/",/"FirstName/":/"A/",/"Gender_vod__c/":/"/",/"IMS_ID__c/":/"/",/"LastName/":/"BAILEY/",/"MterID_mp__c/":/"/",/"Medicis_ID_MED__c/":/"851588/",/"Middle_vod__c/":/"/",/"NPI_vod__c/":/"/",/"PDRP_MED__c/":false,/"PersonDoNotCall/":false,/"PersonEmail/":/"/",/"PersonHasOptedOutOfEmail/":false,/"PersonHasOptedOutOfFax/":false,/"PersonMobilePhone/":/"/",/"Phone/":/"/",/"Practicing_Specialty__c/":/"FM - FAMILY MEDICINE/",/"Primary_City__c/":/"/",/"Primary_State__c/":/"/",/"Primary_Street_Line2__c/":/"/",/"Primary_Street__c/":/"/",/"Primary_Zip__c/":/"/",/"RecordTypeId/":/"012U0000000JaPWIA0/",/"Request_Date__c/":/"2016-06-10T22:31:55.9647467Z/",/"XXXXXXX/":/"/",/"Specialty_1_vod__c/":/"/",/"Suffix_vod__c/":/"/",/"Website/":/"/"}",
        "code": 400,
        "errors": null,
        "isError": true,
        "severity": 4,
        "notes": null,
        "resolved": 0
        }
}
```

#### <a name="salesforce-error-response"></a><span data-ttu-id="2750e-165">Salesforce error response</span><span class="sxs-lookup"><span data-stu-id="2750e-165">Salesforce error response</span></span>

``` json
{
    "statusCode": 400,
    "headers": {
        "Pragma": "no-cache",
        "x-ms-request-id": "3e8e4884-288e-4633-972c-8271b2cc912c",
        "X-Content-Type-Options": "nosniff",
        "Cache-Control": "no-cache",
        "Date": "Fri, 10 Jun 2016 22:31:56 GMT",
        "Set-Cookie": "ARRAffinity=785f4334b5e64d2db0b84edcc1b84f1bf37319679aefce206b51510e56fd9770;Path=/;Domain=127.0.0.1",
        "Server": "Microsoft-IIS/8.0,Microsoft-HTTPAPI/2.0",
        "X-AspNet-Version": "4.0.30319",
        "X-Powered-By": "ASP.NET",
        "Content-Length": "205",
        "Content-Type": "application/json; charset=utf-8",
        "Expires": "-1"
    },
    "body": {
        "status": 400,
        "message": "Salesforce failed to complete task: Message: duplicate value found: Account_ID_MED__c duplicates value on record with id: 001U000001c83gK",
        "source": "Salesforce.Common",
        "errors": []
    }
}

```

### <a name="return-the-response-back-to-parent-logic-app"></a><span data-ttu-id="2750e-166">Return the response back to parent logic app</span><span class="sxs-lookup"><span data-stu-id="2750e-166">Return the response back to parent logic app</span></span>

<span data-ttu-id="2750e-167">After you get the response, you can pass the response back to the parent logic app.</span><span class="sxs-lookup"><span data-stu-id="2750e-167">After you get the response, you can pass the response back to the parent logic app.</span></span>

#### <a name="return-success-response-to-parent-logic-app"></a><span data-ttu-id="2750e-168">Return success response to parent logic app</span><span class="sxs-lookup"><span data-stu-id="2750e-168">Return success response to parent logic app</span></span>

``` json
"SuccessResponse": {
    "runAfter":
        {
            "UpdateNew_CRMPatientResponse": ["Succeeded"]
        },
    "inputs": {
        "body": {
            "status": "Success"
    },
    "headers": {
    "    Content-type": "application/json",
        "x-ms-date": "@utcnow()"
    },
    "statusCode": 200
    },
    "type": "Response"
}
```

#### <a name="return-error-response-to-parent-logic-app"></a><span data-ttu-id="2750e-169">Return error response to parent logic app</span><span class="sxs-lookup"><span data-stu-id="2750e-169">Return error response to parent logic app</span></span>

``` json
"ErrorResponse": {
    "runAfter":
        {
            "Create_NewPatientRecord": ["Failed"]
        },
    "inputs": {
        "body": {
            "status": "BadRequest"
        },
        "headers": {
            "Content-type": "application/json",
            "x-ms-date": "@utcnow()"
        },
        "statusCode": 400
    },
    "type": "Response"
}

```


## <a name="documentdb-repository-and-portal"></a><span data-ttu-id="2750e-170">DocumentDB repository and portal</span><span class="sxs-lookup"><span data-stu-id="2750e-170">DocumentDB repository and portal</span></span>

<span data-ttu-id="2750e-171">Our solution added capabilities with [DocumentDB](https://azure.microsoft.com/services/documentdb).</span><span class="sxs-lookup"><span data-stu-id="2750e-171">Our solution added capabilities with [DocumentDB](https://azure.microsoft.com/services/documentdb).</span></span>

### <a name="error-management-portal"></a><span data-ttu-id="2750e-172">Error management portal</span><span class="sxs-lookup"><span data-stu-id="2750e-172">Error management portal</span></span>

<span data-ttu-id="2750e-173">To view the errors, you can create an MVC web app to display the error records from DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2750e-173">To view the errors, you can create an MVC web app to display the error records from DocumentDB.</span></span> <span data-ttu-id="2750e-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span><span class="sxs-lookup"><span data-stu-id="2750e-174">The **List**, **Details**, **Edit**, and **Delete** operations are included in the current version.</span></span>

> [!NOTE]
> <span data-ttu-id="2750e-175">Edit operation: DocumentDB replaces the entire document.</span><span class="sxs-lookup"><span data-stu-id="2750e-175">Edit operation: DocumentDB replaces the entire document.</span></span> <span data-ttu-id="2750e-176">The records shown in the **List** and **Detail** views are samples only.</span><span class="sxs-lookup"><span data-stu-id="2750e-176">The records shown in the **List** and **Detail** views are samples only.</span></span> <span data-ttu-id="2750e-177">They are not actual patient appointment records.</span><span class="sxs-lookup"><span data-stu-id="2750e-177">They are not actual patient appointment records.</span></span>

<span data-ttu-id="2750e-178">Here are examples of our MVC app details created with the previously described approach.</span><span class="sxs-lookup"><span data-stu-id="2750e-178">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="error-management-list"></a><span data-ttu-id="2750e-179">Error management list</span><span class="sxs-lookup"><span data-stu-id="2750e-179">Error management list</span></span>
![Error List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/errorlist.png)

#### <a name="error-management-detail-view"></a><span data-ttu-id="2750e-181">Error management detail view</span><span class="sxs-lookup"><span data-stu-id="2750e-181">Error management detail view</span></span>
![Error Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/errordetails.png)

### <a name="log-management-portal"></a><span data-ttu-id="2750e-183">Log management portal</span><span class="sxs-lookup"><span data-stu-id="2750e-183">Log management portal</span></span>

<span data-ttu-id="2750e-184">To view the logs, we also created an MVC web app.</span><span class="sxs-lookup"><span data-stu-id="2750e-184">To view the logs, we also created an MVC web app.</span></span> <span data-ttu-id="2750e-185">Here are examples of our MVC app details created with the previously described approach.</span><span class="sxs-lookup"><span data-stu-id="2750e-185">Here are examples of our MVC app details created with the previously described approach.</span></span>

#### <a name="sample-log-detail-view"></a><span data-ttu-id="2750e-186">Sample log detail view</span><span class="sxs-lookup"><span data-stu-id="2750e-186">Sample log detail view</span></span>
![Log Detail View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-scenario-error-and-exception-handling/samplelogdetail.png)

### <a name="api-app-details"></a><span data-ttu-id="2750e-188">API app details</span><span class="sxs-lookup"><span data-stu-id="2750e-188">API app details</span></span>

#### <a name="logic-apps-exception-management-api"></a><span data-ttu-id="2750e-189">Logic Apps exception management API</span><span class="sxs-lookup"><span data-stu-id="2750e-189">Logic Apps exception management API</span></span>

<span data-ttu-id="2750e-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span><span class="sxs-lookup"><span data-stu-id="2750e-190">Our open-source Azure Logic Apps exception management API app provides functionality as described here - there are two controllers:</span></span>

* <span data-ttu-id="2750e-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="2750e-191">**ErrorController** inserts an error record (document) in a DocumentDB collection.</span></span>
* <span data-ttu-id="2750e-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="2750e-192">**LogController** Inserts a log record (document) in a DocumentDB collection.</span></span>

> [!TIP]
> <span data-ttu-id="2750e-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span><span class="sxs-lookup"><span data-stu-id="2750e-193">Both controllers use `async Task<dynamic>` operations, allowing operations to resolve at runtime, so we can create the DocumentDB schema in the body of the operation.</span></span> 
> 

<span data-ttu-id="2750e-194">Every document in DocumentDB must have a unique ID.</span><span class="sxs-lookup"><span data-stu-id="2750e-194">Every document in DocumentDB must have a unique ID.</span></span> <span data-ttu-id="2750e-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span><span class="sxs-lookup"><span data-stu-id="2750e-195">We are using `PatientId` and adding a timestamp that is converted to a Unix timestamp value (double).</span></span> <span data-ttu-id="2750e-196">We truncate the value to remove the fractional value.</span><span class="sxs-lookup"><span data-stu-id="2750e-196">We truncate the value to remove the fractional value.</span></span>

<span data-ttu-id="2750e-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span><span class="sxs-lookup"><span data-stu-id="2750e-197">You can view the source code of our error controller API [from GitHub](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi/blob/master/Logic App Exception Management API/Controllers/ErrorController.cs).</span></span>

<span data-ttu-id="2750e-198">We call the API from a logic app by using the following syntax:</span><span class="sxs-lookup"><span data-stu-id="2750e-198">We call the API from a logic app by using the following syntax:</span></span>

``` json
 "actions": {
        "CreateErrorRecord": {
          "metadata": {
            "apiDefinitionUrl": "https://.../swagger/docs/v1",
            "swaggerSource": "website"
          },
          "type": "Http",
          "inputs": {
            "body": {
              "action": "New_Patient",
              "isError": true,
              "crmId": "@{triggerBody()['CRMid']}",
              "prescriberId": "@{triggerBody()['CRMid']}",
              "message": "@{body('Create_NewPatientRecord')['message']}",
              "salesforceId": "@{triggerBody()['salesforceID']}",
              "severity": 4,
              "source": "@{actions('Create_NewPatientRecord')['inputs']['body']}",
              "statusCode": "@{int(outputs('Create_NewPatientRecord')['statusCode'])}",
              "update": false
            },
            "method": "post",
            "uri": "https://.../api/CrMtoSfError"
          },
          "runAfter": {
              "Create_NewPatientRecord": ["Failed"]
            }
        }
 }
```

<span data-ttu-id="2750e-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span><span class="sxs-lookup"><span data-stu-id="2750e-199">The expression in the preceding code sample checks for the *Create_NewPatientRecord* status of **Failed**.</span></span>

## <a name="summary"></a><span data-ttu-id="2750e-200">Summary</span><span class="sxs-lookup"><span data-stu-id="2750e-200">Summary</span></span>

* <span data-ttu-id="2750e-201">You can easily implement logging and error handling in a logic app.</span><span class="sxs-lookup"><span data-stu-id="2750e-201">You can easily implement logging and error handling in a logic app.</span></span>
* <span data-ttu-id="2750e-202">You can use DocumentDB as the repository for log and error records (documents).</span><span class="sxs-lookup"><span data-stu-id="2750e-202">You can use DocumentDB as the repository for log and error records (documents).</span></span>
* <span data-ttu-id="2750e-203">You can use MVC to create a portal to display log and error records.</span><span class="sxs-lookup"><span data-stu-id="2750e-203">You can use MVC to create a portal to display log and error records.</span></span>

### <a name="source-code"></a><span data-ttu-id="2750e-204">Source code</span><span class="sxs-lookup"><span data-stu-id="2750e-204">Source code</span></span>

<span data-ttu-id="2750e-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span><span class="sxs-lookup"><span data-stu-id="2750e-205">The source code for the Logic Apps exception management API application is available in this [GitHub repository](https://github.com/HEDIDIN/LogicAppsExceptionManagementApi "Logic App Exception Management API").</span></span>

## <a name="next-steps"></a><span data-ttu-id="2750e-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="2750e-206">Next steps</span></span>

* [<span data-ttu-id="2750e-207">View more logic app examples and scenarios</span><span class="sxs-lookup"><span data-stu-id="2750e-207">View more logic app examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="2750e-208">Learn about monitoring logic apps</span><span class="sxs-lookup"><span data-stu-id="2750e-208">Learn about monitoring logic apps</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
* [<span data-ttu-id="2750e-209">Create automated deployment templates for logic apps</span><span class="sxs-lookup"><span data-stu-id="2750e-209">Create automated deployment templates for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)





