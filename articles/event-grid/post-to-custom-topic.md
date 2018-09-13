---
title: Post event to custom Azure Event Grid topic
description: Describes how to post an event to a custom topic for Azure Event Grid
services: event-grid
author: tfitzmac
manager: timlt
ms.service: event-grid
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: tomfitz
ms.openlocfilehash: e4256de1d9112d785b6d1cd52067fc99144a0a04
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965789"
---
# <a name="post-to-custom-topic-for-azure-event-grid"></a>Post to custom topic for Azure Event Grid

This article describes how to post an event to a custom topic. It shows the format of the post and event data. The [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/event-grid/v1_0/) only applies to posts that match the expected format.

## <a name="endpoint"></a>Endpoint

When sending the HTTP POST to a custom topic, use the URI format: `https://<topic-endpoint>?api-version=2018-01-01`.

For example, a valid URI is: `https://exampletopic.westus2-1.eventgrid.azure.net/api/events?api-version=2018-01-01`.

To get the endpoint for a custom topic with Azure CLI, use:

```azurecli-interactive
az eventgrid topic show --name <topic-name> -g <topic-resource-group> --query "endpoint"
```

To get the endpoint for a custom topic with Azure PowerShell, use:

```powershell
(Get-AzureRmEventGridTopic -ResourceGroupName <topic-resource-group> -Name <topic-name>).Endpoint
```

## <a name="header"></a>Header

In the request, include a header value named `aeg-sas-key` that contains a key for authentication.

For example, a valid header value is `aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==`.

To get the key for a custom topic with Azure CLI, use:

```azurecli
az eventgrid topic key list --name <topic-name> -g <topic-resource-group> --query "key1"
```

To get the key for a custom topic with PowerShell, use:

```powershell
(Get-AzureRmEventGridTopicKey -ResourceGroupName <topic-resource-group> -Name <topic-name>).Key1
```

## <a name="event-data"></a>Event data

For custom topics, the top-level data contains the same fields as standard resource-defined events. One of those properties is a data property that contains properties unique to the custom topic. As event publisher, you determine the properties for that data object. Use the following schema:

```json
[
  {
    "id": string,    
    "eventType": string,
    "subject": string,
    "eventTime": string-in-date-time-format,
    "data":{
      object-unique-to-each-publisher
    },
    "dataVersion": string
  }
]
```

For a description of these properties, see [Azure Event Grid event schema](event-schema.md). When posting events to an event grid topic, the array can have a total size of up to 1 MB. Each event in the array is limited to 64 KB.

For example, a valid event data schema is:

```json
[{
  "id": "1807",
  "eventType": "recordInserted",
  "subject": "myapp/vehicles/motorcycles",
  "eventTime": "2017-08-10T21:03:07+00:00",
  "data": {
    "make": "Ducati",
    "model": "Monster"
  },
  "dataVersion": "1.0"
}]
```

## <a name="response"></a>Response

After posting to the topic endpoint, you receive a response. The response is a standard HTTP response code. Some common responses are:

|Result  |Response  |
|---------|---------|
|Success  | 200 OK  |
|Event data has incorrect format | 400 Bad Request |
|Invalid access key | 401 Unauthorized |
|Incorrect endpoint | 404 Not Found |
|Array or event exceeds size limits | 413 Payload Too Large |

For errors, the message body has the following format:

```json
{
    "error": {
        "code": "<HTTP status code>",
        "message": "<description>",
        "details": [{
            "code": "<HTTP status code>",
            "message": "<description>"
    }]
  }
}
```

## <a name="next-steps"></a>Next steps

* For information about monitoring event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).
* For more information about the authentication key, see [Event Grid security and authentication](security-authentication.md).
* For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).
