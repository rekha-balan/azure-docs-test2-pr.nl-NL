---
title: Azure Service Bus diagnostic logs | Microsoft Docs
description: Learn how to set up diagnostic logs for Service Bus in Azure.
keywords: ''
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: ''
ms.assetid: ''
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/23/2017
ms.author: babanisa;sethm
ms.openlocfilehash: 80b7d3cc16914a4c8b264d93922a82d61dd0ac78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663019"
---
# <a name="service-bus-diagnostic-logs"></a>Service Bus diagnostic logs

You can view two types of logs for Azure Service Bus:
* **[Activity logs](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. These logs contain information about operations performed on a job. The logs are always enabled.
* **[Diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. You can configure diagnostic logs for richer information about everything that happens within a job. Diagnostic logs cover activities from the time the job is created until the job is deleted, including updates and activities that occur while the job is running.

## <a name="turn-on-diagnostic-logs"></a>Turn on diagnostic logs
Diagnostics logs are disabled by default. To enable diagnostic logs, do the following:

1.  In the [Azure portal](https://portal.azure.com), go to the streaming job blade.

2.  Under **Monitoring**, go to the **Diagnostics logs** blade.

    ![blade navigation to diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image1.png)  

3.  Click **Turn on diagnostics**.

    ![turn on diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image2.png)

4.  For **Status**, click **On**.

    ![change status diagnostic logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-bus-messaging/media/service-bus-diagnostic-logs/image3.png)

5.  Set the archival target that you want; for example, a storage account, an Event Hub, or Azure Log Analytics.

6.  Select the categories of logs that you want to collect; for example, **Execution** or **Authoring**.

7.  Save the new diagnostics settings.

New settings take effect in about 10 minutes. After that, logs appear in the configured archival target, on the **Diagnostics logs** blade.

For more information about configuring diagnostics, see the [overview of Azure diagnostic logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Diagnostic logs schema

All logs are stored in JavaScript Object Notation (JSON) format. Each entry has string fields that use the format described in the following example.

## <a name="operation-logs-example"></a>Operation logs example

Logs in the **OperationalLogs** category capture what happens during Service Bus operations. Specifically, these logs capture the operation type, including queue creation, resources used, and the status of the operation.

Operation log JSON strings include elements listed in the following table:

Name | Description
------- | -------
ActivityId | Internal ID, used for tracking
EventName | Operation name           
resourceId | Azure Resource Manager resource ID
SubscriptionId | Subscription ID
EventTimeString | Operation time
EventProperties | Operation properties
Status | Operation status
Caller | Caller of operation (Azure portal or management client)
category | OperationalLogs

Here's an example of an operation log JSON string:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create Queue",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Next steps
* [Introduction to Service Bus](service-bus-messaging-overview.md)
* [Get started with Service Bus](service-bus-dotnet-get-started-with-queues.md)



