---
title: Monitor APIs with Azure API Management, Event Hubs, and Runscope | Microsoft Docs
description: Sample application demonstrating the log-to-eventhub policy by connecting Azure API Management, Azure Event Hubs and Runscope for HTTP  logging and monitoring
services: api-management
documentationcenter: ''
author: darrelmiller
manager: erikre
editor: ''
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 950265d8d09f86f4ae9da3c0503713a9ffa3829f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563912"
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="0313c-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span><span class="sxs-lookup"><span data-stu-id="0313c-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="0313c-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span><span class="sxs-lookup"><span data-stu-id="0313c-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="0313c-105">However, the existence of the requests and responses are transient.</span><span class="sxs-lookup"><span data-stu-id="0313c-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="0313c-106">The request is made and it flows through the API Management service to your backend API.</span><span class="sxs-lookup"><span data-stu-id="0313c-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="0313c-107">Your API processes the request and a response flows back through to the API consumer.</span><span class="sxs-lookup"><span data-stu-id="0313c-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="0313c-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span><span class="sxs-lookup"><span data-stu-id="0313c-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="0313c-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0313c-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="0313c-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span><span class="sxs-lookup"><span data-stu-id="0313c-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="0313c-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span><span class="sxs-lookup"><span data-stu-id="0313c-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="0313c-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span><span class="sxs-lookup"><span data-stu-id="0313c-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="0313c-113">Why Send From API Management Service?</span><span class="sxs-lookup"><span data-stu-id="0313c-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="0313c-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span><span class="sxs-lookup"><span data-stu-id="0313c-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="0313c-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span><span class="sxs-lookup"><span data-stu-id="0313c-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="0313c-116">If there are multiple APIs then each one must deploy the middleware.</span><span class="sxs-lookup"><span data-stu-id="0313c-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="0313c-117">Often there are reasons why backend APIs cannot be updated.</span><span class="sxs-lookup"><span data-stu-id="0313c-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="0313c-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span><span class="sxs-lookup"><span data-stu-id="0313c-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="0313c-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="0313c-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="0313c-120">Why send to an Azure Event Hub?</span><span class="sxs-lookup"><span data-stu-id="0313c-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="0313c-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="0313c-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="0313c-122">There are many different places where I might want to log my requests.</span><span class="sxs-lookup"><span data-stu-id="0313c-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="0313c-123">Why not just send the requests directly to the final destination?</span><span class="sxs-lookup"><span data-stu-id="0313c-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="0313c-124">That is an option.</span><span class="sxs-lookup"><span data-stu-id="0313c-124">That is an option.</span></span> <span data-ttu-id="0313c-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span><span class="sxs-lookup"><span data-stu-id="0313c-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="0313c-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span><span class="sxs-lookup"><span data-stu-id="0313c-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="0313c-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span><span class="sxs-lookup"><span data-stu-id="0313c-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="0313c-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span><span class="sxs-lookup"><span data-stu-id="0313c-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="0313c-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span><span class="sxs-lookup"><span data-stu-id="0313c-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="0313c-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span><span class="sxs-lookup"><span data-stu-id="0313c-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="0313c-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span><span class="sxs-lookup"><span data-stu-id="0313c-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="0313c-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span><span class="sxs-lookup"><span data-stu-id="0313c-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="0313c-133">Event Hubs have the ability to stream events to multiple consumer groups.</span><span class="sxs-lookup"><span data-stu-id="0313c-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="0313c-134">This allows events to be processed by completely different systems.</span><span class="sxs-lookup"><span data-stu-id="0313c-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="0313c-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span><span class="sxs-lookup"><span data-stu-id="0313c-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="0313c-136">A policy to send application/http messages</span><span class="sxs-lookup"><span data-stu-id="0313c-136">A policy to send application/http messages</span></span>
<span data-ttu-id="0313c-137">An Event Hub accepts event data as a simple string.</span><span class="sxs-lookup"><span data-stu-id="0313c-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="0313c-138">The contents of that string are completely up to you.</span><span class="sxs-lookup"><span data-stu-id="0313c-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="0313c-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span><span class="sxs-lookup"><span data-stu-id="0313c-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="0313c-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span><span class="sxs-lookup"><span data-stu-id="0313c-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="0313c-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span><span class="sxs-lookup"><span data-stu-id="0313c-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="0313c-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span><span class="sxs-lookup"><span data-stu-id="0313c-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="0313c-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span><span class="sxs-lookup"><span data-stu-id="0313c-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="0313c-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="0313c-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="0313c-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span><span class="sxs-lookup"><span data-stu-id="0313c-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="0313c-146">In our case we are just going to use the body as our message to send to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0313c-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="0313c-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span><span class="sxs-lookup"><span data-stu-id="0313c-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="0313c-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span><span class="sxs-lookup"><span data-stu-id="0313c-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="0313c-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="0313c-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="0313c-150">Policy declaration</span><span class="sxs-lookup"><span data-stu-id="0313c-150">Policy declaration</span></span>
<span data-ttu-id="0313c-151">There a few particular things worth mentioning about this policy expression.</span><span class="sxs-lookup"><span data-stu-id="0313c-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="0313c-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span><span class="sxs-lookup"><span data-stu-id="0313c-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="0313c-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="0313c-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="0313c-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span><span class="sxs-lookup"><span data-stu-id="0313c-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="0313c-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span><span class="sxs-lookup"><span data-stu-id="0313c-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="0313c-156">The ordered delivery of messages is only guaranteed within a partition.</span><span class="sxs-lookup"><span data-stu-id="0313c-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="0313c-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span><span class="sxs-lookup"><span data-stu-id="0313c-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="0313c-158">However, that may cause some of our messages to be processed out of order.</span><span class="sxs-lookup"><span data-stu-id="0313c-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="0313c-159">Partitions</span><span class="sxs-lookup"><span data-stu-id="0313c-159">Partitions</span></span>
<span data-ttu-id="0313c-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span><span class="sxs-lookup"><span data-stu-id="0313c-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="0313c-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span><span class="sxs-lookup"><span data-stu-id="0313c-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="0313c-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span><span class="sxs-lookup"><span data-stu-id="0313c-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="0313c-163">HTTP payloads</span><span class="sxs-lookup"><span data-stu-id="0313c-163">HTTP payloads</span></span>
<span data-ttu-id="0313c-164">After building the `requestLine` we check to see if the request body should be truncated.</span><span class="sxs-lookup"><span data-stu-id="0313c-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="0313c-165">The request body is truncated to only 1024.</span><span class="sxs-lookup"><span data-stu-id="0313c-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="0313c-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span><span class="sxs-lookup"><span data-stu-id="0313c-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="0313c-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span><span class="sxs-lookup"><span data-stu-id="0313c-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="0313c-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span><span class="sxs-lookup"><span data-stu-id="0313c-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="0313c-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span><span class="sxs-lookup"><span data-stu-id="0313c-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="0313c-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span><span class="sxs-lookup"><span data-stu-id="0313c-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="0313c-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span><span class="sxs-lookup"><span data-stu-id="0313c-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="0313c-172">In these cases it would be best to avoid reading the body at all.</span><span class="sxs-lookup"><span data-stu-id="0313c-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="0313c-173">HTTP headers</span><span class="sxs-lookup"><span data-stu-id="0313c-173">HTTP headers</span></span>
<span data-ttu-id="0313c-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span><span class="sxs-lookup"><span data-stu-id="0313c-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="0313c-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span><span class="sxs-lookup"><span data-stu-id="0313c-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="0313c-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span><span class="sxs-lookup"><span data-stu-id="0313c-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="0313c-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span><span class="sxs-lookup"><span data-stu-id="0313c-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="0313c-178">Message Metadata</span><span class="sxs-lookup"><span data-stu-id="0313c-178">Message Metadata</span></span>
<span data-ttu-id="0313c-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span><span class="sxs-lookup"><span data-stu-id="0313c-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="0313c-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span><span class="sxs-lookup"><span data-stu-id="0313c-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="0313c-181">The message id is created by using another policy that looks like this:</span><span class="sxs-lookup"><span data-stu-id="0313c-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="0313c-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span><span class="sxs-lookup"><span data-stu-id="0313c-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="0313c-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span><span class="sxs-lookup"><span data-stu-id="0313c-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="0313c-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span><span class="sxs-lookup"><span data-stu-id="0313c-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="0313c-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span><span class="sxs-lookup"><span data-stu-id="0313c-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="0313c-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span><span class="sxs-lookup"><span data-stu-id="0313c-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="0313c-187">Receiving events from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0313c-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="0313c-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="0313c-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="0313c-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span><span class="sxs-lookup"><span data-stu-id="0313c-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="0313c-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span><span class="sxs-lookup"><span data-stu-id="0313c-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="0313c-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0313c-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="0313c-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span><span class="sxs-lookup"><span data-stu-id="0313c-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="0313c-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="0313c-193">EventProcessorHost</span></span>
<span data-ttu-id="0313c-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span><span class="sxs-lookup"><span data-stu-id="0313c-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="0313c-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span><span class="sxs-lookup"><span data-stu-id="0313c-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="0313c-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span><span class="sxs-lookup"><span data-stu-id="0313c-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="0313c-197">There is no need for updating shared state and therefore no risk of threading issues.</span><span class="sxs-lookup"><span data-stu-id="0313c-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="0313c-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span><span class="sxs-lookup"><span data-stu-id="0313c-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="0313c-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="0313c-199">IEventProcessor</span></span>
<span data-ttu-id="0313c-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="0313c-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="0313c-201">The essence of that method is shown here:</span><span class="sxs-lookup"><span data-stu-id="0313c-201">The essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="0313c-202">A list of EventData objects are passed into the method and we iterate over that list.</span><span class="sxs-lookup"><span data-stu-id="0313c-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="0313c-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="0313c-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="0313c-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="0313c-204">HttpMessage</span></span>
<span data-ttu-id="0313c-205">The `HttpMessage` instance contains three pieces of data:</span><span class="sxs-lookup"><span data-stu-id="0313c-205">The `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="0313c-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="0313c-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="0313c-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="0313c-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="0313c-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="0313c-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="0313c-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span><span class="sxs-lookup"><span data-stu-id="0313c-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="0313c-210">Forwarding the HTTP message</span><span class="sxs-lookup"><span data-stu-id="0313c-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="0313c-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="0313c-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="0313c-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span><span class="sxs-lookup"><span data-stu-id="0313c-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="0313c-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span><span class="sxs-lookup"><span data-stu-id="0313c-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="0313c-214">The `IHttpMessageProcessor` implementation looks like this,</span><span class="sxs-lookup"><span data-stu-id="0313c-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="0313c-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span><span class="sxs-lookup"><span data-stu-id="0313c-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="0313c-216">In order to access the Runscope API you will need an account and an API Key.</span><span class="sxs-lookup"><span data-stu-id="0313c-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="0313c-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="0313c-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="0313c-218">Complete sample</span><span class="sxs-lookup"><span data-stu-id="0313c-218">Complete sample</span></span>
<span data-ttu-id="0313c-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span><span class="sxs-lookup"><span data-stu-id="0313c-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="0313c-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/storage-create-storage-account.md) to run the sample for yourself.</span><span class="sxs-lookup"><span data-stu-id="0313c-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="0313c-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span><span class="sxs-lookup"><span data-stu-id="0313c-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="0313c-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span><span class="sxs-lookup"><span data-stu-id="0313c-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Demonstration of request being forwarded to Runscope](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="0313c-224">Summary</span><span class="sxs-lookup"><span data-stu-id="0313c-224">Summary</span></span>
<span data-ttu-id="0313c-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span><span class="sxs-lookup"><span data-stu-id="0313c-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="0313c-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span><span class="sxs-lookup"><span data-stu-id="0313c-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="0313c-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span><span class="sxs-lookup"><span data-stu-id="0313c-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0313c-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="0313c-228">Next steps</span></span>
* <span data-ttu-id="0313c-229">Learn more about Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0313c-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="0313c-230">Get started with Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="0313c-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="0313c-231">Receive messages with EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="0313c-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="0313c-232">Event Hubs programming guide</span><span class="sxs-lookup"><span data-stu-id="0313c-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="0313c-233">Learn more about API Management and Event Hubs integration</span><span class="sxs-lookup"><span data-stu-id="0313c-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="0313c-234">How to log events to Azure Event Hubs in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="0313c-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="0313c-235">Logger entity reference</span><span class="sxs-lookup"><span data-stu-id="0313c-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="0313c-236">log-to-eventhub policy reference</span><span class="sxs-lookup"><span data-stu-id="0313c-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)

