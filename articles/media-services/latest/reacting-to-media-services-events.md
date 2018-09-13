---
title: Reacting to Azure Media Services events | Microsoft Docs
description: Use Azure Event Grid to subscribe to Media Services events.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 03/19/2018
ms.author: juliako
ms.openlocfilehash: 969957d53824bd70440e5529b83bc830bb5d9cc4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965509"
---
# <a name="reacting-to-media-services-events"></a><span data-ttu-id="844e5-103">Reacting to Media Services events</span><span class="sxs-lookup"><span data-stu-id="844e5-103">Reacting to Media Services events</span></span>

<span data-ttu-id="844e5-104">Media Services events allow applications to react to different events (for example, the job state change event) using modern serverless architectures.</span><span class="sxs-lookup"><span data-stu-id="844e5-104">Media Services events allow applications to react to different events (for example, the job state change event) using modern serverless architectures.</span></span> <span data-ttu-id="844e5-105">It does so without the need for complicated code or expensive and inefficient polling services.</span><span class="sxs-lookup"><span data-stu-id="844e5-105">It does so without the need for complicated code or expensive and inefficient polling services.</span></span> <span data-ttu-id="844e5-106">Instead, events are pushed through [Azure Event Grid](https://azure.microsoft.com/services/event-grid/) to event handlers such as [Azure Functions](https://azure.microsoft.com/services/functions/), [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/), or even to your own Webhook, and you only pay for what you use.</span><span class="sxs-lookup"><span data-stu-id="844e5-106">Instead, events are pushed through [Azure Event Grid](https://azure.microsoft.com/services/event-grid/) to event handlers such as [Azure Functions](https://azure.microsoft.com/services/functions/), [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/), or even to your own Webhook, and you only pay for what you use.</span></span> <span data-ttu-id="844e5-107">For information about pricing, see [Event Grid pricing](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="844e5-107">For information about pricing, see [Event Grid pricing](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

<span data-ttu-id="844e5-108">Availability for Media Services events is tied to Event Grid [availability](../../event-grid/overview.md) and will become available in other regions as Event Grid does.</span><span class="sxs-lookup"><span data-stu-id="844e5-108">Availability for Media Services events is tied to Event Grid [availability](../../event-grid/overview.md) and will become available in other regions as Event Grid does.</span></span>  

## <a name="available-media-services-events"></a><span data-ttu-id="844e5-109">Available Media Services events</span><span class="sxs-lookup"><span data-stu-id="844e5-109">Available Media Services events</span></span>

<span data-ttu-id="844e5-110">Event grid uses [event subscriptions](../../event-grid/concepts.md#event-subscriptions) to route event messages to subscribers.</span><span class="sxs-lookup"><span data-stu-id="844e5-110">Event grid uses [event subscriptions](../../event-grid/concepts.md#event-subscriptions) to route event messages to subscribers.</span></span>  <span data-ttu-id="844e5-111">Currently, Media Services event subscriptions can include the following event type:</span><span class="sxs-lookup"><span data-stu-id="844e5-111">Currently, Media Services event subscriptions can include the following event type:</span></span>  

|<span data-ttu-id="844e5-112">Event Name</span><span class="sxs-lookup"><span data-stu-id="844e5-112">Event Name</span></span>|<span data-ttu-id="844e5-113">Description</span><span class="sxs-lookup"><span data-stu-id="844e5-113">Description</span></span>|
|----------|-----------|
| <span data-ttu-id="844e5-114">Microsoft.Media.JobStateChange</span><span class="sxs-lookup"><span data-stu-id="844e5-114">Microsoft.Media.JobStateChange</span></span>| <span data-ttu-id="844e5-115">Raised when a state of the job changes.</span><span class="sxs-lookup"><span data-stu-id="844e5-115">Raised when a state of the job changes.</span></span> |

## <a name="event-schema"></a><span data-ttu-id="844e5-116">Event Schema</span><span class="sxs-lookup"><span data-stu-id="844e5-116">Event Schema</span></span>

<span data-ttu-id="844e5-117">Media Services events contain all the information you need to respond to changes in your data.</span><span class="sxs-lookup"><span data-stu-id="844e5-117">Media Services events contain all the information you need to respond to changes in your data.</span></span>  <span data-ttu-id="844e5-118">You can identify a  Media Services event because the eventType property starts with "Microsoft.Media.".</span><span class="sxs-lookup"><span data-stu-id="844e5-118">You can identify a  Media Services event because the eventType property starts with "Microsoft.Media.".</span></span>

<span data-ttu-id="844e5-119">For more information, see [Media Services event schemas](media-services-event-schemas.md).</span><span class="sxs-lookup"><span data-stu-id="844e5-119">For more information, see [Media Services event schemas](media-services-event-schemas.md).</span></span>

## <a name="practices-for-consuming-events"></a><span data-ttu-id="844e5-120">Practices for consuming events</span><span class="sxs-lookup"><span data-stu-id="844e5-120">Practices for consuming events</span></span>

<span data-ttu-id="844e5-121">Applications that handle Media Services events should follow a few recommended practices:</span><span class="sxs-lookup"><span data-stu-id="844e5-121">Applications that handle Media Services events should follow a few recommended practices:</span></span>

* <span data-ttu-id="844e5-122">As multiple subscriptions can be configured to route events to the same event handler, it is important not to assume events are from a particular source, but to check the topic of the message to ensure that it comes from the storage account you are expecting.</span><span class="sxs-lookup"><span data-stu-id="844e5-122">As multiple subscriptions can be configured to route events to the same event handler, it is important not to assume events are from a particular source, but to check the topic of the message to ensure that it comes from the storage account you are expecting.</span></span>
* <span data-ttu-id="844e5-123">Similarly, check that the eventType is one you are prepared to process, and do not assume that all events you receive will be the types you expect.</span><span class="sxs-lookup"><span data-stu-id="844e5-123">Similarly, check that the eventType is one you are prepared to process, and do not assume that all events you receive will be the types you expect.</span></span>
* <span data-ttu-id="844e5-124">Ignore fields you don’t understand.</span><span class="sxs-lookup"><span data-stu-id="844e5-124">Ignore fields you don’t understand.</span></span>  <span data-ttu-id="844e5-125">This practice will help keep you resilient to new features that might be added in the future.</span><span class="sxs-lookup"><span data-stu-id="844e5-125">This practice will help keep you resilient to new features that might be added in the future.</span></span>
* <span data-ttu-id="844e5-126">Use the "subject" prefix and suffix matches to limit events to a particular event.</span><span class="sxs-lookup"><span data-stu-id="844e5-126">Use the "subject" prefix and suffix matches to limit events to a particular event.</span></span>

## <a name="next-steps"></a><span data-ttu-id="844e5-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="844e5-127">Next steps</span></span>

[<span data-ttu-id="844e5-128">Get job state events</span><span class="sxs-lookup"><span data-stu-id="844e5-128">Get job state events</span></span>](job-state-events-cli-how-to.md)
