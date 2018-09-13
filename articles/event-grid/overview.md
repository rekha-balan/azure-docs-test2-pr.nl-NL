---
title: Azure Event Grid overview
description: Describes Azure Event Grid and its concepts.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: overview
ms.date: 08/17/2018
ms.author: babanisa
ms.openlocfilehash: 90e8d6a3ef093046c5ee6324f6e6590e59124da7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866682"
---
# <a name="an-introduction-to-azure-event-grid"></a><span data-ttu-id="e5125-103">An introduction to Azure Event Grid</span><span class="sxs-lookup"><span data-stu-id="e5125-103">An introduction to Azure Event Grid</span></span>

<span data-ttu-id="e5125-104">Azure Event Grid allows you to easily build applications with event-based architectures.</span><span class="sxs-lookup"><span data-stu-id="e5125-104">Azure Event Grid allows you to easily build applications with event-based architectures.</span></span> <span data-ttu-id="e5125-105">First select the Azure resource you would like to subscribe to, and then give the event handler or WebHook endpoint to send the event to.</span><span class="sxs-lookup"><span data-stu-id="e5125-105">First select the Azure resource you would like to subscribe to, and then give the event handler or WebHook endpoint to send the event to.</span></span> <span data-ttu-id="e5125-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span><span class="sxs-lookup"><span data-stu-id="e5125-106">Event Grid has built-in support for events coming from Azure services, like storage blobs and resource groups.</span></span> <span data-ttu-id="e5125-107">Event Grid also has support for your own events, using custom topics.</span><span class="sxs-lookup"><span data-stu-id="e5125-107">Event Grid also has support for your own events, using custom topics.</span></span> 

<span data-ttu-id="e5125-108">You can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure your events are reliably delivered.</span><span class="sxs-lookup"><span data-stu-id="e5125-108">You can use filters to route specific events to different endpoints, multicast to multiple endpoints, and make sure your events are reliably delivered.</span></span>

<span data-ttu-id="e5125-109">Currently, Azure Event Grid is available in all public regions.</span><span class="sxs-lookup"><span data-stu-id="e5125-109">Currently, Azure Event Grid is available in all public regions.</span></span> <span data-ttu-id="e5125-110">It is not yet available in the Azure Germany, Azure China, or Azure Government clouds.</span><span class="sxs-lookup"><span data-stu-id="e5125-110">It is not yet available in the Azure Germany, Azure China, or Azure Government clouds.</span></span>

<span data-ttu-id="e5125-111">This article provides an overview of Azure Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e5125-111">This article provides an overview of Azure Event Grid.</span></span> <span data-ttu-id="e5125-112">If you want to get started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="e5125-112">If you want to get started with Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span> 

![Event Grid functional model](./media/overview/functional-model.png)

<span data-ttu-id="e5125-114">Please note: this image shows how Event Grid connects sources and handlers, and is not a comprehensive list of supported integrations.</span><span class="sxs-lookup"><span data-stu-id="e5125-114">Please note: this image shows how Event Grid connects sources and handlers, and is not a comprehensive list of supported integrations.</span></span>

## <a name="event-sources"></a><span data-ttu-id="e5125-115">Event sources</span><span class="sxs-lookup"><span data-stu-id="e5125-115">Event sources</span></span>

<span data-ttu-id="e5125-116">For full details on the capabilities of each source as well as related articles, see [event sources](event-sources.md).</span><span class="sxs-lookup"><span data-stu-id="e5125-116">For full details on the capabilities of each source as well as related articles, see [event sources](event-sources.md).</span></span> <span data-ttu-id="e5125-117">Currently, the following Azure services support sending events to Event Grid:</span><span class="sxs-lookup"><span data-stu-id="e5125-117">Currently, the following Azure services support sending events to Event Grid:</span></span>

* <span data-ttu-id="e5125-118">Azure Subscriptions (management operations)</span><span class="sxs-lookup"><span data-stu-id="e5125-118">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="e5125-119">Container Registry</span><span class="sxs-lookup"><span data-stu-id="e5125-119">Container Registry</span></span>
* <span data-ttu-id="e5125-120">Custom Topics</span><span class="sxs-lookup"><span data-stu-id="e5125-120">Custom Topics</span></span>
* <span data-ttu-id="e5125-121">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e5125-121">Event Hubs</span></span>
* <span data-ttu-id="e5125-122">IoT Hub</span><span class="sxs-lookup"><span data-stu-id="e5125-122">IoT Hub</span></span>
* <span data-ttu-id="e5125-123">Media Services</span><span class="sxs-lookup"><span data-stu-id="e5125-123">Media Services</span></span>
* <span data-ttu-id="e5125-124">Resource Groups (management operations)</span><span class="sxs-lookup"><span data-stu-id="e5125-124">Resource Groups (management operations)</span></span>
* <span data-ttu-id="e5125-125">Service Bus</span><span class="sxs-lookup"><span data-stu-id="e5125-125">Service Bus</span></span>
* <span data-ttu-id="e5125-126">Storage Blob</span><span class="sxs-lookup"><span data-stu-id="e5125-126">Storage Blob</span></span>
* <span data-ttu-id="e5125-127">Storage General-purpose v2 (GPv2)</span><span class="sxs-lookup"><span data-stu-id="e5125-127">Storage General-purpose v2 (GPv2)</span></span>

## <a name="event-handlers"></a><span data-ttu-id="e5125-128">Event handlers</span><span class="sxs-lookup"><span data-stu-id="e5125-128">Event handlers</span></span>

<span data-ttu-id="e5125-129">For full details on the capabilities of each handler as well as related articles, see [event handlers](event-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="e5125-129">For full details on the capabilities of each handler as well as related articles, see [event handlers](event-handlers.md).</span></span> <span data-ttu-id="e5125-130">Currently, the following Azure services support handling events from Event Grid:</span><span class="sxs-lookup"><span data-stu-id="e5125-130">Currently, the following Azure services support handling events from Event Grid:</span></span> 

* <span data-ttu-id="e5125-131">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e5125-131">Azure Automation</span></span>
* <span data-ttu-id="e5125-132">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e5125-132">Azure Functions</span></span>
* <span data-ttu-id="e5125-133">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e5125-133">Event Hubs</span></span>
* <span data-ttu-id="e5125-134">Hybrid Connections</span><span class="sxs-lookup"><span data-stu-id="e5125-134">Hybrid Connections</span></span>
* <span data-ttu-id="e5125-135">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="e5125-135">Logic Apps</span></span>
* <span data-ttu-id="e5125-136">Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="e5125-136">Microsoft Flow</span></span>
* <span data-ttu-id="e5125-137">Queue Storage</span><span class="sxs-lookup"><span data-stu-id="e5125-137">Queue Storage</span></span>
* <span data-ttu-id="e5125-138">WebHooks</span><span class="sxs-lookup"><span data-stu-id="e5125-138">WebHooks</span></span>

## <a name="concepts"></a><span data-ttu-id="e5125-139">Concepts</span><span class="sxs-lookup"><span data-stu-id="e5125-139">Concepts</span></span>

<span data-ttu-id="e5125-140">There are five concepts in Azure Event Grid that let you get going:</span><span class="sxs-lookup"><span data-stu-id="e5125-140">There are five concepts in Azure Event Grid that let you get going:</span></span>

* <span data-ttu-id="e5125-141">**Events** - What happened.</span><span class="sxs-lookup"><span data-stu-id="e5125-141">**Events** - What happened.</span></span>
* <span data-ttu-id="e5125-142">**Event sources** - Where the event took place.</span><span class="sxs-lookup"><span data-stu-id="e5125-142">**Event sources** - Where the event took place.</span></span>
* <span data-ttu-id="e5125-143">**Topics** - The endpoint where publishers send events.</span><span class="sxs-lookup"><span data-stu-id="e5125-143">**Topics** - The endpoint where publishers send events.</span></span>
* <span data-ttu-id="e5125-144">**Event subscriptions** - The endpoint or built-in mechanism to route events, sometimes to multiple handlers.</span><span class="sxs-lookup"><span data-stu-id="e5125-144">**Event subscriptions** - The endpoint or built-in mechanism to route events, sometimes to multiple handlers.</span></span> <span data-ttu-id="e5125-145">Subscriptions are also used by handlers to intelligently filter incoming events.</span><span class="sxs-lookup"><span data-stu-id="e5125-145">Subscriptions are also used by handlers to intelligently filter incoming events.</span></span>
* <span data-ttu-id="e5125-146">**Event handlers** - The app or service reacting to the event.</span><span class="sxs-lookup"><span data-stu-id="e5125-146">**Event handlers** - The app or service reacting to the event.</span></span>

<span data-ttu-id="e5125-147">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span><span class="sxs-lookup"><span data-stu-id="e5125-147">For more information about these concepts, see [Concepts in Azure Event Grid](concepts.md).</span></span>

## <a name="capabilities"></a><span data-ttu-id="e5125-148">Capabilities</span><span class="sxs-lookup"><span data-stu-id="e5125-148">Capabilities</span></span>

<span data-ttu-id="e5125-149">Here are some of the key features of Azure Event Grid:</span><span class="sxs-lookup"><span data-stu-id="e5125-149">Here are some of the key features of Azure Event Grid:</span></span>

* <span data-ttu-id="e5125-150">**Simplicity** - Point and click to aim events from your Azure resource to any event handler or endpoint.</span><span class="sxs-lookup"><span data-stu-id="e5125-150">**Simplicity** - Point and click to aim events from your Azure resource to any event handler or endpoint.</span></span>
* <span data-ttu-id="e5125-151">**Advanced filtering** - Filter on event type or event publish path to ensure event handlers only receive relevant events.</span><span class="sxs-lookup"><span data-stu-id="e5125-151">**Advanced filtering** - Filter on event type or event publish path to ensure event handlers only receive relevant events.</span></span>
* <span data-ttu-id="e5125-152">**Fan-out** - Subscribe multiple endpoints to the same event to send copies of the event to as many places as needed.</span><span class="sxs-lookup"><span data-stu-id="e5125-152">**Fan-out** - Subscribe multiple endpoints to the same event to send copies of the event to as many places as needed.</span></span>
* <span data-ttu-id="e5125-153">**Reliability** - Utilize 24-hour retry with exponential backoff to ensure events are delivered.</span><span class="sxs-lookup"><span data-stu-id="e5125-153">**Reliability** - Utilize 24-hour retry with exponential backoff to ensure events are delivered.</span></span>
* <span data-ttu-id="e5125-154">**Pay-per-event** - Pay only for the amount you use Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e5125-154">**Pay-per-event** - Pay only for the amount you use Event Grid.</span></span>
* <span data-ttu-id="e5125-155">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span><span class="sxs-lookup"><span data-stu-id="e5125-155">**High throughput** - Build high-volume workloads on Event Grid with support for millions of events per second.</span></span>
* <span data-ttu-id="e5125-156">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span><span class="sxs-lookup"><span data-stu-id="e5125-156">**Built-in Events** - Get up and running quickly with resource-defined built-in events.</span></span>
* <span data-ttu-id="e5125-157">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span><span class="sxs-lookup"><span data-stu-id="e5125-157">**Custom Events** - use Event Grid route, filter, and reliably deliver custom events in your app.</span></span>

<span data-ttu-id="e5125-158">For a comparison of Event Grid, Event Hubs, and Service Bus, see [Choose between Azure services that deliver messages](compare-messaging-services.md).</span><span class="sxs-lookup"><span data-stu-id="e5125-158">For a comparison of Event Grid, Event Hubs, and Service Bus, see [Choose between Azure services that deliver messages](compare-messaging-services.md).</span></span>

## <a name="what-can-i-do-with-event-grid"></a><span data-ttu-id="e5125-159">What can I do with Event Grid?</span><span class="sxs-lookup"><span data-stu-id="e5125-159">What can I do with Event Grid?</span></span>

<span data-ttu-id="e5125-160">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span><span class="sxs-lookup"><span data-stu-id="e5125-160">Azure Event Grid provides several capabilities that vastly improve serverless, ops automation, and integration work:</span></span> 

### <a name="serverless-application-architectures"></a><span data-ttu-id="e5125-161">Serverless application architectures</span><span class="sxs-lookup"><span data-stu-id="e5125-161">Serverless application architectures</span></span>

![Serverless application](./media/overview/serverless_web_app.png)

<span data-ttu-id="e5125-163">Event Grid connects data sources and event handlers.</span><span class="sxs-lookup"><span data-stu-id="e5125-163">Event Grid connects data sources and event handlers.</span></span> <span data-ttu-id="e5125-164">For example, use Event Grid to instantly trigger a serverless function to run image analysis each time a new photo is added to a blob storage container.</span><span class="sxs-lookup"><span data-stu-id="e5125-164">For example, use Event Grid to instantly trigger a serverless function to run image analysis each time a new photo is added to a blob storage container.</span></span> 

### <a name="ops-automation"></a><span data-ttu-id="e5125-165">Ops Automation</span><span class="sxs-lookup"><span data-stu-id="e5125-165">Ops Automation</span></span>

![Ops automation](./media/overview/Ops_automation.png)

<span data-ttu-id="e5125-167">Event Grid allows you to speed automation and simplify policy enforcement.</span><span class="sxs-lookup"><span data-stu-id="e5125-167">Event Grid allows you to speed automation and simplify policy enforcement.</span></span> <span data-ttu-id="e5125-168">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span><span class="sxs-lookup"><span data-stu-id="e5125-168">For example, Event Grid can notify Azure Automation when a virtual machine is created, or a SQL Database is spun up.</span></span> <span data-ttu-id="e5125-169">These events can be used to automatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span><span class="sxs-lookup"><span data-stu-id="e5125-169">These events can be used to automatically check that service configurations are compliant, put metadata into operations tools, tag virtual machines, or file work items.</span></span>

### <a name="application-integration"></a><span data-ttu-id="e5125-170">Application integration</span><span class="sxs-lookup"><span data-stu-id="e5125-170">Application integration</span></span>

![Application integration](./media/overview/app_integration.png)

<span data-ttu-id="e5125-172">Event Grid connects your app with other services.</span><span class="sxs-lookup"><span data-stu-id="e5125-172">Event Grid connects your app with other services.</span></span> <span data-ttu-id="e5125-173">For example, create a custom topic to send your app's event data to Event Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span><span class="sxs-lookup"><span data-stu-id="e5125-173">For example, create a custom topic to send your app's event data to Event Grid, and take advantage of its reliable delivery, advanced routing, and direct integration with Azure.</span></span> <span data-ttu-id="e5125-174">Alternatively, you can use Event Grid with Logic Apps to process data anywhere, without writing code.</span><span class="sxs-lookup"><span data-stu-id="e5125-174">Alternatively, you can use Event Grid with Logic Apps to process data anywhere, without writing code.</span></span> 

## <a name="how-much-does-event-grid-cost"></a><span data-ttu-id="e5125-175">How much does Event Grid cost?</span><span class="sxs-lookup"><span data-stu-id="e5125-175">How much does Event Grid cost?</span></span>

<span data-ttu-id="e5125-176">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span><span class="sxs-lookup"><span data-stu-id="e5125-176">Azure Event Grid uses a pay-per-event pricing model, so you only pay for what you use.</span></span> <span data-ttu-id="e5125-177">The first 100,000 operations per month are free.</span><span class="sxs-lookup"><span data-stu-id="e5125-177">The first 100,000 operations per month are free.</span></span> <span data-ttu-id="e5125-178">Operations are defined as event ingress, subscription delivery attempts, management calls, and filtering by subject suffix.</span><span class="sxs-lookup"><span data-stu-id="e5125-178">Operations are defined as event ingress, subscription delivery attempts, management calls, and filtering by subject suffix.</span></span> <span data-ttu-id="e5125-179">For details, see the [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span><span class="sxs-lookup"><span data-stu-id="e5125-179">For details, see the [pricing page](https://azure.microsoft.com/pricing/details/event-grid/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5125-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5125-180">Next steps</span></span>

* [<span data-ttu-id="e5125-181">Route Storage Blob events</span><span class="sxs-lookup"><span data-stu-id="e5125-181">Route Storage Blob events</span></span>](../storage/blobs/storage-blob-event-quickstart.md?toc=%2fazure%2fevent-grid%2ftoc.json)  
  <span data-ttu-id="e5125-182">Respond to storage blob events by using Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e5125-182">Respond to storage blob events by using Event Grid.</span></span>
* [<span data-ttu-id="e5125-183">Create and subscribe to custom events</span><span class="sxs-lookup"><span data-stu-id="e5125-183">Create and subscribe to custom events</span></span>](custom-event-quickstart.md)  
  <span data-ttu-id="e5125-184">Jump right in and start sending your own custom events to any endpoint using the Azure Event Grid quickstart.</span><span class="sxs-lookup"><span data-stu-id="e5125-184">Jump right in and start sending your own custom events to any endpoint using the Azure Event Grid quickstart.</span></span>
* [<span data-ttu-id="e5125-185">Using Logic Apps as an Event Handler</span><span class="sxs-lookup"><span data-stu-id="e5125-185">Using Logic Apps as an Event Handler</span></span>](monitor-virtual-machine-changes-event-grid-logic-app.md)  
  <span data-ttu-id="e5125-186">A tutorial on building an app using Logic Apps to react to events pushed by Event Grid.</span><span class="sxs-lookup"><span data-stu-id="e5125-186">A tutorial on building an app using Logic Apps to react to events pushed by Event Grid.</span></span>
* [<span data-ttu-id="e5125-187">Stream big data into a data warehouse</span><span class="sxs-lookup"><span data-stu-id="e5125-187">Stream big data into a data warehouse</span></span>](event-grid-event-hubs-integration.md)  
  <span data-ttu-id="e5125-188">A tutorial that uses Azure Functions to stream data from Event Hubs to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e5125-188">A tutorial that uses Azure Functions to stream data from Event Hubs to SQL Data Warehouse.</span></span>
* [<span data-ttu-id="e5125-189">Event Grid REST API reference</span><span class="sxs-lookup"><span data-stu-id="e5125-189">Event Grid REST API reference</span></span>](/rest/api/eventgrid)  
  <span data-ttu-id="e5125-190">Provides more technical information about the Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span><span class="sxs-lookup"><span data-stu-id="e5125-190">Provides more technical information about the Azure Event Grid, and a reference for managing Event Subscriptions, routing, and filtering.</span></span>