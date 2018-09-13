---
title: Review Azure subscription billing data with REST API | Microsoft Docs
description: Learn how to use Azure REST APIs to review subscription billing details.
services: billing
documentationcenter: na
author: lleonard-msft
manager: MBaldwin
editor: ''
ms.assetid: 82D50B98-40F2-44B1-A445-4391EA9EBBAA
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2018
ms.author: alleonar
ms.openlocfilehash: cc29d1f613af67604d50654be794cc90080098bb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968679"
---
# <a name="review-subscription-billing-using-rest-apis"></a>Review subscription billing using REST APIs

Azure Reporting APIs help you review and manage your Azure costs.  

Filters help customize results to meet your needs.

Here, you learn to use a REST API to return subscription billing details for a given date range.

``` http
GET https://management.azure.com/subscriptions/${subscriptionID}/providers/Microsoft.Billing/billingPeriods/${billingPeriod}/providers/Microsoft.Consumption/usageDetails?$filter=properties/usageEnd ge '${startDate}' AND properties/usageEnd le '${endDate}'
Content-Type: application/json   
Authorization: Bearer
```

## <a name="build-the-request"></a>Build the request  

The `{subscriptionID}` parameter is required and identifies the target subscription.

The `{billingPeriod}` parameter is required and specifies a current [billing period](https://docs.microsoft.com/rest/api/billing/billingperiods/get#billingperiod).

The `${startDate}` and `${endDate}` parameters are required for this example, but optional for the endpoint.  They specify the date range as strings in the form of YYYY-MM-DD (examples: `'20180501'` and `'20180615'`). 

The following headers are required: 

|Request header|Description|  
|--------------------|-----------------|  
|*Content-Type:*|Required. Set to `application/json`.|  
|*Authorization:*|Required. Set to a valid `Bearer` [access token](https://docs.microsoft.com/rest/api/azure/#authorization-code-grant-interactive-clients). |  

## <a name="response"></a>Response  

Status code 200 (OK) is returned for a successful response, which contains a list of detailed costs for your account.

``` json
{
  "value": [
    {
      "id": "/subscriptions/{$subscriptionID}/providers/Microsoft.Billing/billingPeriods/201702/providers/Microsoft.Consumption/usageDetails/{$detailsID}",
      "name": "{$detailsID}",
      "type": "Microsoft.Consumption/usageDetails",
      "properties": {
        "billingPeriodId": "/subscriptions/${subscriptionID}/providers/Microsoft.Billing/billingPeriods/${billingPeriod}",
        "invoiceId": "/subscriptions/${subscriptionID}/providers/Microsoft.Billing/invoices/${invoiceID}",
        "usageStart": "${startDate}}",
        "usageEnd": "${endDate}",
        "currency": "USD",
        "usageQuantity": ${usageQuantity},
        "billableQuantity": ${billableQuantity},
        "pretaxCost": ${cost},
        "meterId": "${meterID}",
        "meterDetails": ${meterDetails}
      }
    }
    ],
    "nextLink": "${nextLinkURL}"
} 
```  

Each item in **value** represents a details regarding the use of a service:

|Response property|Description|
|----------------|----------|
|**subscriptionGuid** | Globally unique ID for the subscription. | 
|**startDate** | Date the use started. |
|**endDate** | Date the use ended. |
|**useageQuantity** | Quantity used. | 
|**billableQuantity** | Quantity actually billed. |
|**pretaxCost** | Cost invoiced, before applicable taxes. | 
|**meterDetails** | Detailed information about the use. |
|**nextLink**| When set, specifies a URL for the next "page" of details. Blank when the page is the last one. |  
||
  
This example is abbreviated; see [List usage details](https://docs.microsoft.com/rest/api/consumption/usagedetails/listbybillingperiod#usagedetailslistresult) for a complete description of each response field. 

Other status codes indicate error conditions. In these cases, the response object explains why the request failed.

``` json
{  
  "error": [  
    { "code": "Error type." 
      "message": "Error response describing why the operation failed."  
    }  
  ]  
}  
```  

## <a name="next-steps"></a>Next steps 
- Review [Enterprise reporting overview](https://docs.microsoft.com/azure/billing/billing-enterprise-api)
- Investigate [Enterprise Billing REST API](https://docs.microsoft.com/rest/api/billing/)   
- [Get started with Azure REST API](https://docs.microsoft.com/rest/api/azure/)   