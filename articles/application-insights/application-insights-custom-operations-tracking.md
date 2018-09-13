---
title: Track custom operations with Azure Application Insights .NET SDK | Microsoft Docs
description: Tracking custom operations with Azure Application Insights .NET SDK
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 06/30/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: 8295fb58bdf92ca8688f5f7b6270dc1b48632a73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965816"
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="e695c-103">Track custom operations with Application Insights .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e695c-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="e695c-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span><span class="sxs-lookup"><span data-stu-id="e695c-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="e695c-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span><span class="sxs-lookup"><span data-stu-id="e695c-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="e695c-106">There is a class of application patterns that can't be supported generically.</span><span class="sxs-lookup"><span data-stu-id="e695c-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="e695c-107">Proper monitoring of such patterns requires manual code instrumentation.</span><span class="sxs-lookup"><span data-stu-id="e695c-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="e695c-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span><span class="sxs-lookup"><span data-stu-id="e695c-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="e695c-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span><span class="sxs-lookup"><span data-stu-id="e695c-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="e695c-110">This documentation is relevant for:</span><span class="sxs-lookup"><span data-stu-id="e695c-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="e695c-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span><span class="sxs-lookup"><span data-stu-id="e695c-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="e695c-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span><span class="sxs-lookup"><span data-stu-id="e695c-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="e695c-113">Application Insights for ASP.NET Core version 2.1+.</span><span class="sxs-lookup"><span data-stu-id="e695c-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="e695c-114">Overview</span><span class="sxs-lookup"><span data-stu-id="e695c-114">Overview</span></span>
<span data-ttu-id="e695c-115">An operation is a logical piece of work run by an application.</span><span class="sxs-lookup"><span data-stu-id="e695c-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="e695c-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span><span class="sxs-lookup"><span data-stu-id="e695c-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="e695c-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span><span class="sxs-lookup"><span data-stu-id="e695c-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="e695c-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="e695c-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="e695c-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="e695c-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Microsoft.ApplicationInsights/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="e695c-120">Incoming operations tracking</span><span class="sxs-lookup"><span data-stu-id="e695c-120">Incoming operations tracking</span></span> 
<span data-ttu-id="e695c-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span><span class="sxs-lookup"><span data-stu-id="e695c-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="e695c-122">There are community-supported solutions for other platforms and frameworks.</span><span class="sxs-lookup"><span data-stu-id="e695c-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="e695c-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span><span class="sxs-lookup"><span data-stu-id="e695c-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="e695c-124">Another example that requires custom tracking is the worker that receives items from the queue.</span><span class="sxs-lookup"><span data-stu-id="e695c-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="e695c-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span><span class="sxs-lookup"><span data-stu-id="e695c-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="e695c-126">However, the high-level operation that describes message processing is not automatically collected.</span><span class="sxs-lookup"><span data-stu-id="e695c-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="e695c-127">Let's see how such operations could be tracked.</span><span class="sxs-lookup"><span data-stu-id="e695c-127">Let's see how such operations could be tracked.</span></span>

<span data-ttu-id="e695c-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span><span class="sxs-lookup"><span data-stu-id="e695c-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="e695c-129">After the operation is finished, you track the telemetry.</span><span class="sxs-lookup"><span data-stu-id="e695c-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="e695c-130">The following example demonstrates this task.</span><span class="sxs-lookup"><span data-stu-id="e695c-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="e695c-131">HTTP request in Owin self-hosted app</span><span class="sxs-lookup"><span data-stu-id="e695c-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="e695c-132">In this example, trace context is propagated according to the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="e695c-132">In this example, trace context is propagated according to the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="e695c-133">You should expect to receive headers that are described there.</span><span class="sxs-lookup"><span data-stu-id="e695c-133">You should expect to receive headers that are described there.</span></span>

```csharp
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="e695c-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span><span class="sxs-lookup"><span data-stu-id="e695c-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="e695c-135">However, it's omitted here for simplicity.</span><span class="sxs-lookup"><span data-stu-id="e695c-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="e695c-136">Queue instrumentation</span><span class="sxs-lookup"><span data-stu-id="e695c-136">Queue instrumentation</span></span>
<span data-ttu-id="e695c-137">While there is [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md) to pass correlation details with HTTP request, every queue protocol has to define how the same details are passed along the queue message.</span><span class="sxs-lookup"><span data-stu-id="e695c-137">While there is [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md) to pass correlation details with HTTP request, every queue protocol has to define how the same details are passed along the queue message.</span></span> <span data-ttu-id="e695c-138">Some queue protocols (such as AMQP) allow passing additional metadata and some others (such Azure Storage Queue) require the context to be encoded into the message payload.</span><span class="sxs-lookup"><span data-stu-id="e695c-138">Some queue protocols (such as AMQP) allow passing additional metadata and some others (such Azure Storage Queue) require the context to be encoded into the message payload.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="e695c-139">Service Bus Queue</span><span class="sxs-lookup"><span data-stu-id="e695c-139">Service Bus Queue</span></span>
<span data-ttu-id="e695c-140">Application Insights tracks Service Bus Messaging calls with the new [Microsoft Azure ServiceBus Client for .NET](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus/) version 3.0.0 and higher.</span><span class="sxs-lookup"><span data-stu-id="e695c-140">Application Insights tracks Service Bus Messaging calls with the new [Microsoft Azure ServiceBus Client for .NET](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus/) version 3.0.0 and higher.</span></span>
<span data-ttu-id="e695c-141">If you use [message handler pattern](/dotnet/api/microsoft.azure.servicebus.queueclient.registermessagehandler) to process messages, you are done: all Service Bus calls done by your service are automatically tracked and correlated with other telemetry items.</span><span class="sxs-lookup"><span data-stu-id="e695c-141">If you use [message handler pattern](/dotnet/api/microsoft.azure.servicebus.queueclient.registermessagehandler) to process messages, you are done: all Service Bus calls done by your service are automatically tracked and correlated with other telemetry items.</span></span> <span data-ttu-id="e695c-142">Refer to the [Service Bus client tracing with Microsoft Application Insights](../service-bus-messaging/service-bus-end-to-end-tracing.md) if you manually process messages.</span><span class="sxs-lookup"><span data-stu-id="e695c-142">Refer to the [Service Bus client tracing with Microsoft Application Insights](../service-bus-messaging/service-bus-end-to-end-tracing.md) if you manually process messages.</span></span>

<span data-ttu-id="e695c-143">If you use [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) package, read further - following examples demonstrate how to track (and correlate) calls to the Service Bus as Service Bus queue uses AMQP protocol and Application Insights doesn't automatically track queue operations.</span><span class="sxs-lookup"><span data-stu-id="e695c-143">If you use [WindowsAzure.ServiceBus](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) package, read further - following examples demonstrate how to track (and correlate) calls to the Service Bus as Service Bus queue uses AMQP protocol and Application Insights doesn't automatically track queue operations.</span></span>
<span data-ttu-id="e695c-144">Correlation identifiers are passed in the message properties.</span><span class="sxs-lookup"><span data-stu-id="e695c-144">Correlation identifiers are passed in the message properties.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="e695c-145">Enqueue</span><span class="sxs-lookup"><span data-stu-id="e695c-145">Enqueue</span></span>

```csharp
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="e695c-146">Process</span><span class="sxs-lookup"><span data-stu-id="e695c-146">Process</span></span>
```csharp
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="e695c-147">Azure Storage queue</span><span class="sxs-lookup"><span data-stu-id="e695c-147">Azure Storage queue</span></span>
<span data-ttu-id="e695c-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e695c-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="e695c-149">The Storage queue has an HTTP API.</span><span class="sxs-lookup"><span data-stu-id="e695c-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="e695c-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="e695c-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="e695c-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="e695c-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="e695c-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="e695c-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="e695c-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span><span class="sxs-lookup"><span data-stu-id="e695c-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
```csharp
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="e695c-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span><span class="sxs-lookup"><span data-stu-id="e695c-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="e695c-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="e695c-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="e695c-156">Enqueue</span><span class="sxs-lookup"><span data-stu-id="e695c-156">Enqueue</span></span>
<span data-ttu-id="e695c-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e695c-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="e695c-158">In many cases, this instrumentation should be enough.</span><span class="sxs-lookup"><span data-stu-id="e695c-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="e695c-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span><span class="sxs-lookup"><span data-stu-id="e695c-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="e695c-160">This example shows how to track the `Enqueue` operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-160">This example shows how to track the `Enqueue` operation.</span></span> <span data-ttu-id="e695c-161">You can:</span><span class="sxs-lookup"><span data-stu-id="e695c-161">You can:</span></span>

 - <span data-ttu-id="e695c-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="e695c-163">Otherwise, they're tracked as children of the incoming request.</span><span class="sxs-lookup"><span data-stu-id="e695c-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="e695c-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span><span class="sxs-lookup"><span data-stu-id="e695c-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="e695c-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span><span class="sxs-lookup"><span data-stu-id="e695c-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="e695c-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span><span class="sxs-lookup"><span data-stu-id="e695c-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="e695c-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span><span class="sxs-lookup"><span data-stu-id="e695c-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```csharp
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="e695c-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span><span class="sxs-lookup"><span data-stu-id="e695c-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="e695c-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="e695c-170">You do *not* need to assign any properties on it except the operation name.</span><span class="sxs-lookup"><span data-stu-id="e695c-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="e695c-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="e695c-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="e695c-172">You can also use `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="e695c-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="e695c-173">Dequeue</span><span class="sxs-lookup"><span data-stu-id="e695c-173">Dequeue</span></span>
<span data-ttu-id="e695c-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e695c-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="e695c-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span><span class="sxs-lookup"><span data-stu-id="e695c-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="e695c-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span><span class="sxs-lookup"><span data-stu-id="e695c-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="e695c-177">The `Dequeue` operation is tricky.</span><span class="sxs-lookup"><span data-stu-id="e695c-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="e695c-178">The Application Insights SDK automatically tracks HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="e695c-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="e695c-179">However, it doesn't know the correlation context until the message is parsed.</span><span class="sxs-lookup"><span data-stu-id="e695c-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="e695c-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span><span class="sxs-lookup"><span data-stu-id="e695c-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="e695c-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span><span class="sxs-lookup"><span data-stu-id="e695c-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="e695c-182">The following example demonstrates how to do it:</span><span class="sxs-lookup"><span data-stu-id="e695c-182">The following example demonstrates how to do it:</span></span>

```csharp
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="e695c-183">Process</span><span class="sxs-lookup"><span data-stu-id="e695c-183">Process</span></span>

<span data-ttu-id="e695c-184">In the following example, an incoming message is tracked in a manner similarly to incoming HTTP request:</span><span class="sxs-lookup"><span data-stu-id="e695c-184">In the following example, an incoming message is tracked in a manner similarly to incoming HTTP request:</span></span>

```csharp
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="e695c-185">Similarly, other queue operations can be instrumented.</span><span class="sxs-lookup"><span data-stu-id="e695c-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="e695c-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="e695c-187">Instrumenting queue management operations isn't necessary.</span><span class="sxs-lookup"><span data-stu-id="e695c-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="e695c-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span><span class="sxs-lookup"><span data-stu-id="e695c-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="e695c-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span><span class="sxs-lookup"><span data-stu-id="e695c-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="e695c-190">Alternatively, you can use the `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="e695c-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="e695c-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights SDK does it for you:</span><span class="sxs-lookup"><span data-stu-id="e695c-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights SDK does it for you:</span></span>

- <span data-ttu-id="e695c-192">Create a new `Activity` after you've got an item from the queue.</span><span class="sxs-lookup"><span data-stu-id="e695c-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="e695c-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span><span class="sxs-lookup"><span data-stu-id="e695c-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="e695c-194">Start the `Activity`.</span><span class="sxs-lookup"><span data-stu-id="e695c-194">Start the `Activity`.</span></span>
- <span data-ttu-id="e695c-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span><span class="sxs-lookup"><span data-stu-id="e695c-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="e695c-196">Do it from the same asynchronous control flow (execution context).</span><span class="sxs-lookup"><span data-stu-id="e695c-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="e695c-197">In this way, they're correlated properly.</span><span class="sxs-lookup"><span data-stu-id="e695c-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="e695c-198">Stop the `Activity`.</span><span class="sxs-lookup"><span data-stu-id="e695c-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="e695c-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span><span class="sxs-lookup"><span data-stu-id="e695c-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="e695c-200">Batch processing</span><span class="sxs-lookup"><span data-stu-id="e695c-200">Batch processing</span></span>
<span data-ttu-id="e695c-201">With some queues, you can dequeue multiple messages with one request.</span><span class="sxs-lookup"><span data-stu-id="e695c-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="e695c-202">Processing such messages is presumably independent and belongs to the different logical operations.</span><span class="sxs-lookup"><span data-stu-id="e695c-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="e695c-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span><span class="sxs-lookup"><span data-stu-id="e695c-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="e695c-204">Each message should be processed in its own asynchronous control flow.</span><span class="sxs-lookup"><span data-stu-id="e695c-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="e695c-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span><span class="sxs-lookup"><span data-stu-id="e695c-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="e695c-206">Long-running background tasks</span><span class="sxs-lookup"><span data-stu-id="e695c-206">Long-running background tasks</span></span>
<span data-ttu-id="e695c-207">Some applications start long-running operations that might be caused by user requests.</span><span class="sxs-lookup"><span data-stu-id="e695c-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="e695c-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span><span class="sxs-lookup"><span data-stu-id="e695c-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

```csharp
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process the task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="e695c-209">In this example, `telemetryClient.StartOperation` creates `RequestTelemetry` and fills the correlation context.</span><span class="sxs-lookup"><span data-stu-id="e695c-209">In this example, `telemetryClient.StartOperation` creates `RequestTelemetry` and fills the correlation context.</span></span> <span data-ttu-id="e695c-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="e695c-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span><span class="sxs-lookup"><span data-stu-id="e695c-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="e695c-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span><span class="sxs-lookup"><span data-stu-id="e695c-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="e695c-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span><span class="sxs-lookup"><span data-stu-id="e695c-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="e695c-214">However, it can have nested operations.</span><span class="sxs-lookup"><span data-stu-id="e695c-214">However, it can have nested operations.</span></span> <span data-ttu-id="e695c-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="e695c-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="e695c-216">Outgoing dependencies tracking</span><span class="sxs-lookup"><span data-stu-id="e695c-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="e695c-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e695c-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="e695c-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span><span class="sxs-lookup"><span data-stu-id="e695c-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="e695c-219">The general approach for custom dependency tracking is to:</span><span class="sxs-lookup"><span data-stu-id="e695c-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="e695c-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span><span class="sxs-lookup"><span data-stu-id="e695c-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="e695c-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span><span class="sxs-lookup"><span data-stu-id="e695c-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="e695c-222">Make a dependency call and wait for it.</span><span class="sxs-lookup"><span data-stu-id="e695c-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="e695c-223">Stop the operation with `StopOperation` when it's finished.</span><span class="sxs-lookup"><span data-stu-id="e695c-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="e695c-224">Handle exceptions.</span><span class="sxs-lookup"><span data-stu-id="e695c-224">Handle exceptions.</span></span>

```csharp
public async Task RunMyTaskAsync()
{
    using (var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1"))
    {
        try 
        {
            var myTask = await StartMyTaskAsync();
            // Update status code and success as appropriate.
        }
        catch(...) 
        {
            // Update status code and success as appropriate.
        }
    }
}
```

<span data-ttu-id="e695c-225">Disposing operation causes operation to be stopped, so you may do it instead of calling `StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="e695c-225">Disposing operation causes operation to be stopped, so you may do it instead of calling `StopOperation`.</span></span>

<span data-ttu-id="e695c-226">*Warning*: in some cases unhanded exception may [prevent](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/try-finally) `finally` to be called so operations may not be tracked.</span><span class="sxs-lookup"><span data-stu-id="e695c-226">*Warning*: in some cases unhanded exception may [prevent](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/try-finally) `finally` to be called so operations may not be tracked.</span></span>

### <a name="parallel-operations-processing-and-tracking"></a><span data-ttu-id="e695c-227">Parallel operations processing and tracking</span><span class="sxs-lookup"><span data-stu-id="e695c-227">Parallel operations processing and tracking</span></span>

<span data-ttu-id="e695c-228">`StopOperation` only stops the operation that was started.</span><span class="sxs-lookup"><span data-stu-id="e695c-228">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="e695c-229">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span><span class="sxs-lookup"><span data-stu-id="e695c-229">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="e695c-230">This situation might happen if you start multiple operations in parallel in the same execution context:</span><span class="sxs-lookup"><span data-stu-id="e695c-230">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```csharp
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// FAILURE!!! This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="e695c-231">Make sure you always call `StartOperation` and process operation in the same **async** method to isolate operations running in parallel.</span><span class="sxs-lookup"><span data-stu-id="e695c-231">Make sure you always call `StartOperation` and process operation in the same **async** method to isolate operations running in parallel.</span></span> <span data-ttu-id="e695c-232">If operation is synchronous (or not async), wrap process and track with `Task.Run`:</span><span class="sxs-lookup"><span data-stu-id="e695c-232">If operation is synchronous (or not async), wrap process and track with `Task.Run`:</span></span>

```csharp
public void RunMyTask(string name)
{
    using (var operation = telemetryClient.StartOperation<DependencyTelemetry>(name))
    {
        Process();
        // Update status code and success as appropriate.
    }
}

public async Task RunAllTasks()
{
    var task1 = Task.Run(() => RunMyTask("task 1"));
    var task2 = Task.Run(() => RunMyTask("task 2"));
    
    await Task.WhenAll(task1, task2);
}
```

## <a name="next-steps"></a><span data-ttu-id="e695c-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="e695c-233">Next steps</span></span>

- <span data-ttu-id="e695c-234">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e695c-234">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="e695c-235">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="e695c-235">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="e695c-236">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e695c-236">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="e695c-237">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span><span class="sxs-lookup"><span data-stu-id="e695c-237">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="e695c-238">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span><span class="sxs-lookup"><span data-stu-id="e695c-238">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
