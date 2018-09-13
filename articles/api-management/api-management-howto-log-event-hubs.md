---
title: How to log events to Azure Event Hubs in Azure API Management | Microsoft Docs
description: Learn how to log events to Azure Event Hubs in Azure API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: b7191c9f65c340443755752e4513fcb98985d67e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670559"
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="e0f74-103">How to log events to Azure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="e0f74-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="e0f74-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span><span class="sxs-lookup"><span data-stu-id="e0f74-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="e0f74-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span><span class="sxs-lookup"><span data-stu-id="e0f74-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="e0f74-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span><span class="sxs-lookup"><span data-stu-id="e0f74-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="e0f74-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="e0f74-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="e0f74-108">Create an Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="e0f74-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="e0f74-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="e0f74-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="e0f74-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span><span class="sxs-lookup"><span data-stu-id="e0f74-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="e0f74-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span><span class="sxs-lookup"><span data-stu-id="e0f74-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="e0f74-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Create event hub][create-event-hub]

<span data-ttu-id="e0f74-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="e0f74-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="e0f74-115">Name the first one **Sending** and give it **Send** permissions.</span><span class="sxs-lookup"><span data-stu-id="e0f74-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Sending policy][sending-policy]

<span data-ttu-id="e0f74-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e0f74-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Receiving policy][receiving-policy]

<span data-ttu-id="e0f74-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="e0f74-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span><span class="sxs-lookup"><span data-stu-id="e0f74-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Connection string][event-hub-dashboard]

<span data-ttu-id="e0f74-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Connection string][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="e0f74-124">Create an API Management logger</span><span class="sxs-lookup"><span data-stu-id="e0f74-124">Create an API Management logger</span></span>
<span data-ttu-id="e0f74-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx) in your API Management service so that it can log events to the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="e0f74-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="e0f74-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="e0f74-127">Before using the REST API for the first time, review the [prerequisites](https://msdn.microsoft.com/library/azure/dn776326.aspx#Prerequisites) and ensure that you have [enabled access to the REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="e0f74-127">Before using the REST API for the first time, review the [prerequisites](https://msdn.microsoft.com/library/azure/dn776326.aspx#Prerequisites) and ensure that you have [enabled access to the REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx#EnableRESTAPI).</span></span>

<span data-ttu-id="e0f74-128">To create a logger, make an HTTP PUT request using the following URL template.</span><span class="sxs-lookup"><span data-stu-id="e0f74-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="e0f74-129">Replace `{your service}` with the name of your API Management service instance.</span><span class="sxs-lookup"><span data-stu-id="e0f74-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="e0f74-130">Replace `{new logger name}` with the desired name for your new logger.</span><span class="sxs-lookup"><span data-stu-id="e0f74-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="e0f74-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span><span class="sxs-lookup"><span data-stu-id="e0f74-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="e0f74-132">Add the following headers to the request.</span><span class="sxs-lookup"><span data-stu-id="e0f74-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="e0f74-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="e0f74-133">Content-Type : application/json</span></span>
* <span data-ttu-id="e0f74-134">Authorization : SharedAccessSignature uid=...</span><span class="sxs-lookup"><span data-stu-id="e0f74-134">Authorization : SharedAccessSignature uid=...</span></span>
  * <span data-ttu-id="e0f74-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://msdn.microsoft.com/library/azure/dn798668.aspx).</span><span class="sxs-lookup"><span data-stu-id="e0f74-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://msdn.microsoft.com/library/azure/dn798668.aspx).</span></span>

<span data-ttu-id="e0f74-136">Specify the request body using the following template.</span><span class="sxs-lookup"><span data-stu-id="e0f74-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="e0f74-137">`type` must be set to `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="e0f74-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="e0f74-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span><span class="sxs-lookup"><span data-stu-id="e0f74-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="e0f74-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="e0f74-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span><span class="sxs-lookup"><span data-stu-id="e0f74-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="e0f74-141">For other possible return codes and their reasons, see [Create a Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#PUT).</span><span class="sxs-lookup"><span data-stu-id="e0f74-141">For other possible return codes and their reasons, see [Create a Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#PUT).</span></span> <span data-ttu-id="e0f74-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx) entity documentation.</span><span class="sxs-lookup"><span data-stu-id="e0f74-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="e0f74-143">Configure log-to-eventhubs policies</span><span class="sxs-lookup"><span data-stu-id="e0f74-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="e0f74-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span><span class="sxs-lookup"><span data-stu-id="e0f74-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="e0f74-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span><span class="sxs-lookup"><span data-stu-id="e0f74-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="e0f74-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="e0f74-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Publisher portal][publisher-portal]

<span data-ttu-id="e0f74-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span><span class="sxs-lookup"><span data-stu-id="e0f74-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="e0f74-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span><span class="sxs-lookup"><span data-stu-id="e0f74-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Add policy][add-policy]

<span data-ttu-id="e0f74-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span><span class="sxs-lookup"><span data-stu-id="e0f74-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Policy editor][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="e0f74-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span><span class="sxs-lookup"><span data-stu-id="e0f74-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="e0f74-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span><span class="sxs-lookup"><span data-stu-id="e0f74-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="e0f74-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span><span class="sxs-lookup"><span data-stu-id="e0f74-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="e0f74-156">Click **Save** to save the updated policy configuration.</span><span class="sxs-lookup"><span data-stu-id="e0f74-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="e0f74-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span><span class="sxs-lookup"><span data-stu-id="e0f74-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0f74-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0f74-158">Next steps</span></span>
* <span data-ttu-id="e0f74-159">Learn more about Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e0f74-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="e0f74-160">Get started with Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e0f74-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="e0f74-161">Receive messages with EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="e0f74-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="e0f74-162">Event Hubs programming guide</span><span class="sxs-lookup"><span data-stu-id="e0f74-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="e0f74-163">Learn more about API Management and Event Hubs integration</span><span class="sxs-lookup"><span data-stu-id="e0f74-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="e0f74-164">Logger entity reference</span><span class="sxs-lookup"><span data-stu-id="e0f74-164">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="e0f74-165">log-to-eventhub policy reference</span><span class="sxs-lookup"><span data-stu-id="e0f74-165">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
  * [<span data-ttu-id="e0f74-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span><span class="sxs-lookup"><span data-stu-id="e0f74-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="e0f74-167">Watch a video walkthrough</span><span class="sxs-lookup"><span data-stu-id="e0f74-167">Watch a video walkthrough</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-log-event-hubs/add-policy.png








