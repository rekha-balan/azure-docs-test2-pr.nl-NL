---
title: Viewing diagnostic logs for Azure Data Lake Analytics | Microsoft Docs
description: 'Understand how to setup and access diagnostic logs for Azure Data Lake analytics '
services: data-lake-analytics
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf5633d4-bc43-444e-90fc-f90fbd0b7935
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/10/2017
ms.author: larryfr
ms.openlocfilehash: 3119a156304748c95619a175473c6acdcee67406
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555126"
---
# <a name="accessing-diagnostic-logs-for-azure-data-lake-analytics"></a>Accessing diagnostic logs for Azure Data Lake Analytics

Learn about how to enable diagnostic logging for your Data Lake Analytics account and how to view the logs collected for your account.

Organizations can enable diagnostic logging for their Azure Data Lake Analytics account to collect data access audit trails. These logs provide information such as:

* A list of users that accessed the data.
* How frequently the data is accessed.
* How much data is stored in the account.

## <a name="prerequisites"></a>Prerequisites

* **An Azure subscription**. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* **Enable your Azure subscription** for Data Lake Analytics Public Preview. See [instructions](data-lake-analytics-get-started-portal.md).

* **Azure Data Lake Analytics account**. Follow the instructions at [Get started with Azure Data Lake Analytics using the Azure portal](data-lake-analytics-get-started-portal.md).

## <a name="enable-logging"></a>Enable logging

1. Sign on to the new [Azure portal](https://portal.azure.com).

2. Open your Data Lake Analytics account and select **Diagnostic logs** from the __Monitoring section__. Next, select __Turn on diagnostics__.

    ![Turn on diagnostics to collect audit and request logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/turn-on-logging.png)

3. From __Diagnostics settings__, set the status to __On__ and select logging options.

    ![Turn on diagnostics to collect audit and request logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/enable-diagnostic-logs.png "Enable diagnostic logs")

   * Set **Status** to **On** to enable diagnostic logging.

   * You can choose to store/process the data in two different ways.

     * Select __Archive to a storage account__ to store logs in an Azure storage account. Use this option if you want to archive the data. If you select this option, you must provide an Azure storage account to save the logs to.

     * Select **Stream to an Event Hub** to stream log data to an Azure Event Hub. Use this option if you have a downstream processing pipeline to analyze incoming logs in real time. If you select this option, you must provide the details for the Azure Event Hub you want to use.

     * Select __Send to Log Analytics__ to send the data to the Log Analytics service. Use this if you want to use Log Analytics to gather and analyze logs.
   * Specify whether you want to get audit logs or request logs or both.

   * Specify the number of days for which the data must be retained.

   * Click **Save**.

        > [!NOTE]
        > You must select either __Archive to a storage account__, __Stream to an Event Hub__ or __Send to Log Analytics__ before using the __Save__ button.

Once you have enabled diagnostic settings, you can return to the __Diagnostics logs__ blade to view logs.

## <a name="view-logs"></a>View logs

There are two ways to view the log data for your Data Lake Analytics account.

* From the Data Lake Analytics account settings
* From the Azure Storage account where the data is stored

### <a name="using-the-data-lake-analytics-settings-view"></a>Using the Data Lake Analytics Settings view

1. From your Data Lake Analytics account blade, select **Diagnostic Logs** and then select the entry to display logs for.

    ![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs.png "View diagnostic logs")

2. The logs are categorized by **Audit Logs** and **Request Logs**.

    ![log entries](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/diagnostic-log-entries.png)

   * Request logs capture every API request made on the Data Lake Analytics account.
   * Audit Logs are similar to request Logs but provide a much more detailed breakdown of the operations being performed on the Data Lake Analytics account. For example, a single upload API call in request logs might result in multiple "Append" operations in the audit logs.

3. Click the **Download** link for a log entry to download the logs.

### <a name="from-the-azure-storage-account-that-contains-log-data"></a>From the Azure Storage account that contains log data

1. Open the Azure Storage account blade associated with Data Lake Analytics for logging, and then click Blobs. The **Blob service** blade lists two containers.

    ![View diagnostic logging](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-diagnostic-logs/view-diagnostic-logs-storage-account.png "View diagnostic logs")

   * The container **insights-logs-audit** contains the audit logs.
   * The container **insights-logs-requests** contains the request logs.
2. Within these containers, the logs are stored under the following structure.

        resourceId=/
          SUBSCRIPTIONS/
            <<SUBSCRIPTION_ID>>/
              RESOURCEGROUPS/
                <<RESOURCE_GRP_NAME>>/
                  PROVIDERS/
                    MICROSOFT.DATALAKEANALYTICS/
                      ACCOUNTS/
                        <DATA_LAKE_ANALYTICS_NAME>>/
                          y=####/
                            m=##/
                              d=##/
                                h=##/
                                  m=00/
                                    PT1H.json

   > [!NOTE]
   > The `##` entries in the path contain the year, month, day, and hour in which the log was created. Data Lake Analytics creates one file every hour, so `m=` always contains a value of `00`.

    As an example, the complete path to an audit log could be:

        https://adllogs.blob.core.windows.net/insights-logs-audit/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=04/m=00/PT1H.json

    Similarly, the complete path to a request log could be:

        https://adllogs.blob.core.windows.net/insights-logs-requests/resourceId=/SUBSCRIPTIONS/<sub-id>/RESOURCEGROUPS/myresourcegroup/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/mydatalakeanalytics/y=2016/m=07/d=18/h=14/m=00/PT1H.json

## <a name="log-structure"></a>Log structure

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
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_analytics_account_name>",
             "category": "Requests",
             "operationName": "GetAggregatedJobHistory",
             "resultType": "200",
             "callerIpAddress": "::ffff:1.1.1.1",
             "correlationId": "4a11c709-05f5-417c-a98d-6e81b3e29c58",
             "identity": "1808bd5f-62af-45f4-89d8-03c5e81bac30",
             "properties": {
                 "HttpMethod":"POST",
                 "Path":"/JobAggregatedHistory",
                 "RequestContentLength":122,
                 "ClientRequestId":"3b7adbd9-3519-4f28-a61c-bd89506163b8",
                 "StartTime":"2016-07-07T21:02:52.472Z",
                 "EndTime":"2016-07-07T21:02:53.456Z"
                 }
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
| operationName |String |Name of the operation that is logged. For example, GetAggregatedJobHistory. |
| resultType |String |The status of the operation, For example, 200. |
| callerIpAddress |String |The IP address of the client making the request |
| correlationId |String |The id of the log. This value can be used to group a set of related log entries |
| identity |Object |The identity that generated the log |
| properties |JSON |See the next section (Request log properties schema) for details |

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
             "time": "2016-07-28T19:15:16.245Z",
             "resourceId": "/SUBSCRIPTIONS/<subscription_id>/RESOURCEGROUPS/<resource_group_name>/PROVIDERS/MICROSOFT.DATALAKEANALYTICS/ACCOUNTS/<data_lake_ANALYTICS_account_name>",
             "category": "Audit",
             "operationName": "JobSubmitted",
             "identity": "user@somewhere.com",
             "properties": {
                 "JobId":"D74B928F-5194-4E6C-971F-C27026C290E6",
                 "JobName": "New Job",
                 "JobRuntimeName": "default",
                 "SubmitTime": "7/28/2016 7:14:57 PM"
                 }
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
| operationName |String |Name of the operation that is logged. For example, JobSubmitted. |
| resultType |String |A substatus for the job status (operationName). |
| resultSignature |String |Additional details on the job status (operationName). |
| identity |String |The user that requested the operation. For example, susan@contoso.com. |
| properties |JSON |See the next section (Audit log properties schema) for details |

> [!NOTE]
> **resultType** and **resultSignature** provide information on the result of an operation, and only contain a value if an operation has completed. For example, they contain a value when **operationName** contains a value of **JobStarted** or **JobEnded**.
>
>

#### <a name="audit-log-properties-schema"></a>Audit log properties schema

| Name | Type | Description |
| --- | --- | --- |
| JobId |String |The ID assigned to the job |
| JobName |String |The name that was provided for the job |
| JobRunTime |String |The runtime used to process the job |
| SubmitTime |String |The time (in UTC) that the job was submitted |
| StartTime |String |The time the job started running after submission (in UTC). |
| EndTime |String |The time the job ended. |
| Parallelism |String |The number of Data Lake Analytics units requested for this job during submission. |

> [!NOTE]
> **SubmitTime**, **StartTime**, **EndTime** and **Parallelism** provide information on an operation, and only contain a value if an operation has started or completed. For example, **SubmitTime** contains a value after **operationName** indicates **JobSubmitted**.

## <a name="process-the-log-data"></a>Process the log data

Azure Data Lake Analytics provides a sample on how to process and analyze the log data. You can find the sample at [https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample](https://github.com/Azure/AzureDataLake/tree/master/Samples/AzureDiagnosticsSample).

## <a name="next-steps"></a>Next steps
* [Overview of Azure Data Lake Analytics](data-lake-analytics-overview.md)





