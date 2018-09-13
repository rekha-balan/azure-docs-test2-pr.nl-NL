---
title: Viewing diagnostic logs for Azure Data Lake Store | Microsoft Docs
description: 'Understand how to setup and access diagnostic logs for Azure Data Lake Store '
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: f6e75eb1-d0ae-47cf-bdb8-06684b7c0a94
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: nitinme
ms.openlocfilehash: 23bf7c7a2a62cb1b3847c6c04c4d051236132eaa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556638"
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-store"></a>Accessing diagnostic logs for Azure Data Lake Store
Learn about how to enable diagnostic logging for your Data Lake Store account and how to view the logs collected for your account.

Organizations can enable diagnostic logging for their Azure Data Lake Store account to collect data access audit trails that provides information such as list of users accessing the data, how frequently the data is accessed, how much data is stored in the account, etc.

## <a name="prerequisites"></a>Prerequisites
* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).
* **Azure Data Lake Store account**. Follow the instructions at [Get started with Azure Data Lake Store using the Azure Portal](data-lake-store-get-started-portal.md).

## <a name="enable-diagnostic-logging-for-your-data-lake-store-account"></a>Enable diagnostic logging for your Data Lake Store account
1. Sign on to the new [Azure Portal](https://portal.azure.com).
2. Open your Data Lake Store account, and from your Data Lake Store account blade, click **Settings**, and then click **Diagnostic logs**.
3. In the **Diagnostics logs** blade, click **Turn on diagnostics**.

    ![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/turn-on-diagnostics.png "Enable diagnostic logs")

3. In the **Diagnostic** blade, make the following changes to configure diagnostic logging.
   
    ![Enable diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")
   
   * Set **Status** to **On** to enable diagnostic logging.
   * You can choose to store/process the data in different ways.
     
        * Select the option to **Archive to a storage account** to store logs to an Azure Storage account. You use this option if you want to archive the data that will be batch-processed at a later date. If you select this option you must provide an Azure Storage account to save the logs to.
        
        * Select the option to **Stream to an event hub** to stream log data to an Azure Event Hub. Most likely you will use this option if you have a downstream processing pipeline to analyze incoming logs at real time. If you select this option, you must provide the details for the Azure Event Hub you want to use.

        * Select the option to **Send to Log Analytics** to use the Azure Log Analytics service to analyze the generated log data. If you select this option, you must provide the details for the Operations Management Suite workspace that you would use the perform log analysis.
     
   * Specify whether you want to get audit logs or request logs or both.
   * Specify the number of days for which the data must be retained. Retention is only applicable if you are using Azure storage account to archive log data.
   * Click **Save**.

Once you have enabled diagnostic settings, you can watch the logs in the **Diagnostic Logs** tab.

## <a name="view-diagnostic-logs-for-your-data-lake-store-account"></a>View diagnostic logs for your Data Lake Store account
There are two ways to view the log data for your Data Lake Store account.

* From the Data Lake Store account settings view
* From the Azure Storage account where the data is stored

### <a name="using-the-data-lake-store-settings-view"></a>Using the Data Lake Store Settings view
1. From your Data Lake Store account **Settings** blade, click **Diagnostic Logs**.
   
    ![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs") 
2. In the **Diagnostic Logs** blade, you should see the logs categorized by **Audit Logs** and **Request Logs**.
   
   * Request logs capture every API request made on the Data Lake Store account.
   * Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Store account. For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.
3. Click the **Download** link against each log entry to download the logs.

### <a name="from-the-azure-storage-account-that-contains-log-data"></a>From the Azure Storage account that contains log data
1. Open the Azure Storage account blade associated with Data Lake Store for logging, and then click Blobs. The **Blob service** blade lists two containers.
   
    ![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")
   
   * The container **insights-logs-audit** contains the audit logs.
   * The container **insights-logs-requests** contains the request logs.
2. Within these containers, the logs are stored under the following structure.
   
    ![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-diagnostic-logs/view-diagnostic-logs-storage-account-structure.png "View diagnostic logs")
   
    As an example, the complete path to an audit log could be `https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=04/m=00/PT1H.json`
   
    Similary, the complete path to a request log could be `https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/mydatalakestore/y=2016/m=07/d=18/h=14/m=00/PT1H.json`

## <a name="understand-the-structure-of-the-log-data"></a>Understand the structure of the log data
The audit and request logs are in a JSON format. In this section, we look at the structure of JSON for request and audit logs.

### <a name="request-logs"></a>Request logs
Here's a sample entry in the JSON-formatted request log. Each blob has one root object called **records** that contains an array of log objects.

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-07T21:02:53.456Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Requests",
             "operationName": "GETCustomerIngressEgress",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {"HttpMethod":"GET","Path":"/webhdfs/v1/Samples/Outputs/Drivers.csv","RequestContentLength":0,"ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8","StartTime":"2016-07-07T21:02:52.472Z","EndTime":"2016-07-07T21:02:53.456Z"}
        }
        ,
        . . . .
      ]
    }

#### <a name="request-log-schema"></a>Request log schema
| Name | Type | Description |
| --- | --- | --- |
| time |String |The timestamp (in UTC) of the log |
| resourceId |String |The ID of the resource that operation took place on |
| category |String |The log category. For example, **Requests**. |
| operationName |String |Name of the operation that is logged. For example, getfilestatus. |
| resultType |String |The status of the operation, For example, 200. |
| callerIpAddress |String |The IP address of the client making the request |
| correlationId |String |The id of the log that can used to group together a set of related log entries |
| identity |Object |The identity that generated the log |
| properties |JSON |See below for details |

#### <a name="request-log-properties-schema"></a>Request log properties schema
| Name | Type | Description |
| --- | --- | --- |
| HttpMethod |String |The HTTP Method used for the operation. For example, GET. |
| Path |String |The path the operation was performed on |
| RequestContentLength |int |The content length of the HTTP request |
| ClientRequestId |String |The Id that uniquely identifies this request |
| StartTime |String |The time at which the server received the request |
| EndTime |String |The time at which the server sent a response |

### <a name="audit-logs"></a>Audit logs
Here's a sample entry in the JSON-formatted audit log. Each blob has one root object called **records** that contains an array of log objects

    {
    "records": 
      [        
        . . . .
        ,
        {
             "time": "2016-07-08T19:08:59.359Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKESTORE/ACCOUNTS/<data_lake_store_account_name>",
             "category": "Audit",
             "operationName": "SeOpenStream",
             "resultType": "0",
             "correlationId": "381110fc03534e1cb99ec52376ceebdf;Append_BrEKAmg;25.66.9.145",
             "identity": "A9DAFFAF-FFEE-4BB5-A4A0-1B6CBBF24355",
             "properties": {"StreamName":"adl://<data_lake_store_account_name>.azuredatalakestore.net/logs.csv"}
        }
        ,
        . . . .
      ]
    }

#### <a name="audit-log-schema"></a>Audit log schema
| Name | Type | Description |
| --- | --- | --- |
| time |String |The timestamp (in UTC) of the log |
| resourceId |String |The ID of the resource that operation took place on |
| category |String |The log category. For example, **Audit**. |
| operationName |String |Name of the operation that is logged. For example, getfilestatus. |
| resultType |String |The status of the operation, For example, 200. |
| correlationId |String |The id of the log that can used to group together a set of related log entries |
| identity |Object |The identity that generated the log |
| properties |JSON |See below for details |

#### <a name="audit-log-properties-schema"></a>Audit log properties schema
| Name | Type | Description |
| --- | --- | --- |
| StreamName |String |The path the operation was performed on |

## <a name="samples-to-process-the-log-data"></a>Samples to process the log data
Azure Data Lake Store provides a sample on how to process and analyze the log data. You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample). 

## <a name="see-also"></a>See also
* [Overview of Azure Data Lake Store](data-lake-store-overview.md)
* [Secure data in Data Lake Store](data-lake-store-secure-data.md)






