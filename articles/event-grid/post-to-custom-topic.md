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
# <a name="post-to-custom-topic-for-azure-event-grid"></a><span data-ttu-id="5b954-103">Post to custom topic for Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="5b954-103">Post to custom topic for Azure Event Grid</span></span>

<span data-ttu-id="5b954-104">This article describes how to post an event to a custom topic.</span><span class="sxs-lookup"><span data-stu-id="5b954-104">This article describes how to post an event to a custom topic.</span></span> <span data-ttu-id="5b954-105">It shows the format of the post and event data.</span><span class="sxs-lookup"><span data-stu-id="5b954-105">It shows the format of the post and event data.</span></span> <span data-ttu-id="5b954-106">The [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/event-grid/v1_0/) only applies to posts that match the expected format.</span><span class="sxs-lookup"><span data-stu-id="5b954-106">The [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/event-grid/v1_0/) only applies to posts that match the expected format.</span></span>

## <a name="endpoint"></a><span data-ttu-id="5b954-107">Endpoint</span><span class="sxs-lookup"><span data-stu-id="5b954-107">Endpoint</span></span>

<span data-ttu-id="5b954-108">When sending the HTTP POST to a custom topic, use the URI format: `https://<topic-endpoint>?api-version=2018-01-01`.</span><span class="sxs-lookup"><span data-stu-id="5b954-108">When sending the HTTP POST to a custom topic, use the URI format: `https://<topic-endpoint>?api-version=2018-01-01`.</span></span>

<span data-ttu-id="5b954-109">For example, a valid URI is: `https://exampletopic.westus2-1.eventgrid.azure.net/api/events?api-version=2018-01-01`.</span><span class="sxs-lookup"><span data-stu-id="5b954-109">For example, a valid URI is: `https://exampletopic.westus2-1.eventgrid.azure.net/api/events?api-version=2018-01-01`.</span></span>

<span data-ttu-id="5b954-110">To get the endpoint for a custom topic with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="5b954-110">To get the endpoint for a custom topic with Azure CLI, use:</span></span>

```azurecli-interactive
az eventgrid topic show --name <topic-name> -g <topic-resource-group> --query "endpoint"
```

<span data-ttu-id="5b954-111">To get the endpoint for a custom topic with Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="5b954-111">To get the endpoint for a custom topic with Azure PowerShell, use:</span></span>

```powershell
(Get-AzureRmEventGridTopic -ResourceGroupName <topic-resource-group> -Name <topic-name>).Endpoint
```

## <a name="header"></a><span data-ttu-id="5b954-112">Header</span><span class="sxs-lookup"><span data-stu-id="5b954-112">Header</span></span>

<span data-ttu-id="5b954-113">In the request, include a header value named `aeg-sas-key` that contains a key for authentication.</span><span class="sxs-lookup"><span data-stu-id="5b954-113">In the request, include a header value named `aeg-sas-key` that contains a key for authentication.</span></span>

<span data-ttu-id="5b954-114">For example, a valid header value is `aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==`.</span><span class="sxs-lookup"><span data-stu-id="5b954-114">For example, a valid header value is `aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==`.</span></span>

<span data-ttu-id="5b954-115">To get the key for a custom topic with Azure CLI, use:</span><span class="sxs-lookup"><span data-stu-id="5b954-115">To get the key for a custom topic with Azure CLI, use:</span></span>

```azurecli
az eventgrid topic key list --name <topic-name> -g <topic-resource-group> --query "key1"
```

<span data-ttu-id="5b954-116">To get the key for a custom topic with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="5b954-116">To get the key for a custom topic with PowerShell, use:</span></span>

```powershell
(Get-AzureRmEventGridTopicKey -ResourceGroupName <topic-resource-group> -Name <topic-name>).Key1
```

## <a name="event-data"></a><span data-ttu-id="5b954-117">Event data</span><span class="sxs-lookup"><span data-stu-id="5b954-117">Event data</span></span>

<span data-ttu-id="5b954-118">For custom topics, the top-level data contains the same fields as standard resource-defined events.</span><span class="sxs-lookup"><span data-stu-id="5b954-118">For custom topics, the top-level data contains the same fields as standard resource-defined events.</span></span> <span data-ttu-id="5b954-119">One of those properties is a data property that contains properties unique to the custom topic.</span><span class="sxs-lookup"><span data-stu-id="5b954-119">One of those properties is a data property that contains properties unique to the custom topic.</span></span> <span data-ttu-id="5b954-120">As event publisher, you determine the properties for that data object.</span><span class="sxs-lookup"><span data-stu-id="5b954-120">As event publisher, you determine the properties for that data object.</span></span> <span data-ttu-id="5b954-121">Use the following schema:</span><span class="sxs-lookup"><span data-stu-id="5b954-121">Use the following schema:</span></span>

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

<span data-ttu-id="5b954-122">For a description of these properties, see [Azure Event Grid event schema](event-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5b954-122">For a description of these properties, see [Azure Event Grid event schema](event-schema.md).</span></span> <span data-ttu-id="5b954-123">When posting events to an event grid topic, the array can have a total size of up to 1 MB.</span><span class="sxs-lookup"><span data-stu-id="5b954-123">When posting events to an event grid topic, the array can have a total size of up to 1 MB.</span></span> <span data-ttu-id="5b954-124">Each event in the array is limited to 64 KB.</span><span class="sxs-lookup"><span data-stu-id="5b954-124">Each event in the array is limited to 64 KB.</span></span>

<span data-ttu-id="5b954-125">For example, a valid event data schema is:</span><span class="sxs-lookup"><span data-stu-id="5b954-125">For example, a valid event data schema is:</span></span>

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

## <a name="response"></a><span data-ttu-id="5b954-126">Response</span><span class="sxs-lookup"><span data-stu-id="5b954-126">Response</span></span>

<span data-ttu-id="5b954-127">After posting to the topic endpoint, you receive a response.</span><span class="sxs-lookup"><span data-stu-id="5b954-127">After posting to the topic endpoint, you receive a response.</span></span> <span data-ttu-id="5b954-128">The response is a standard HTTP response code.</span><span class="sxs-lookup"><span data-stu-id="5b954-128">The response is a standard HTTP response code.</span></span> <span data-ttu-id="5b954-129">Some common responses are:</span><span class="sxs-lookup"><span data-stu-id="5b954-129">Some common responses are:</span></span>

|<span data-ttu-id="5b954-130">Result</span><span class="sxs-lookup"><span data-stu-id="5b954-130">Result</span></span>  |<span data-ttu-id="5b954-131">Response</span><span class="sxs-lookup"><span data-stu-id="5b954-131">Response</span></span>  |
|---------|---------|
|<span data-ttu-id="5b954-132">Success</span><span class="sxs-lookup"><span data-stu-id="5b954-132">Success</span></span>  | <span data-ttu-id="5b954-133">200 OK</span><span class="sxs-lookup"><span data-stu-id="5b954-133">200 OK</span></span>  |
|<span data-ttu-id="5b954-134">Event data has incorrect format</span><span class="sxs-lookup"><span data-stu-id="5b954-134">Event data has incorrect format</span></span> | <span data-ttu-id="5b954-135">400 Bad Request</span><span class="sxs-lookup"><span data-stu-id="5b954-135">400 Bad Request</span></span> |
|<span data-ttu-id="5b954-136">Invalid access key</span><span class="sxs-lookup"><span data-stu-id="5b954-136">Invalid access key</span></span> | <span data-ttu-id="5b954-137">401 Unauthorized</span><span class="sxs-lookup"><span data-stu-id="5b954-137">401 Unauthorized</span></span> |
|<span data-ttu-id="5b954-138">Incorrect endpoint</span><span class="sxs-lookup"><span data-stu-id="5b954-138">Incorrect endpoint</span></span> | <span data-ttu-id="5b954-139">404 Not Found</span><span class="sxs-lookup"><span data-stu-id="5b954-139">404 Not Found</span></span> |
|<span data-ttu-id="5b954-140">Array or event exceeds size limits</span><span class="sxs-lookup"><span data-stu-id="5b954-140">Array or event exceeds size limits</span></span> | <span data-ttu-id="5b954-141">413 Payload Too Large</span><span class="sxs-lookup"><span data-stu-id="5b954-141">413 Payload Too Large</span></span> |

<span data-ttu-id="5b954-142">For errors, the message body has the following format:</span><span class="sxs-lookup"><span data-stu-id="5b954-142">For errors, the message body has the following format:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="5b954-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="5b954-143">Next steps</span></span>

* <span data-ttu-id="5b954-144">For information about monitoring event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span><span class="sxs-lookup"><span data-stu-id="5b954-144">For information about monitoring event deliveries, see [Monitor Event Grid message delivery](monitor-event-delivery.md).</span></span>
* <span data-ttu-id="5b954-145">For more information about the authentication key, see [Event Grid security and authentication](security-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="5b954-145">For more information about the authentication key, see [Event Grid security and authentication](security-authentication.md).</span></span>
* <span data-ttu-id="5b954-146">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="5b954-146">For more information about creating an Azure Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
