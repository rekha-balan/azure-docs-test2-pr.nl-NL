---
title: Filtering and preprocessing in the Azure Application Insights SDK | Microsoft Docs
description: Write Telemetry Processors and Telemetry Initializers for the SDK to filter or add properties to the data before the telemetry is sent to the Application Insights portal.
services: application-insights
documentationcenter: ''
author: beckylino
manager: carmonm
ms.assetid: 38a9e454-43d5-4dba-a0f0-bd7cd75fb97b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 11/23/2016
ms.author: awills
ms.openlocfilehash: f961cde4aa8de5bdd0f8f220d355f2c93af580a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554647"
---
# <a name="filtering-and-preprocessing-telemetry-in-the-application-insights-sdk"></a><span data-ttu-id="9446e-103">Filtering and preprocessing telemetry in the Application Insights SDK</span><span class="sxs-lookup"><span data-stu-id="9446e-103">Filtering and preprocessing telemetry in the Application Insights SDK</span></span>


<span data-ttu-id="9446e-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="9446e-104">You can write and configure plug-ins for the Application Insights SDK to customize how telemetry is captured and processed before it is sent to the Application Insights service.</span></span>

* <span data-ttu-id="9446e-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span><span class="sxs-lookup"><span data-stu-id="9446e-105">[Sampling](app-insights-sampling.md) reduces the volume of telemetry without affecting your statistics.</span></span> <span data-ttu-id="9446e-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span><span class="sxs-lookup"><span data-stu-id="9446e-106">It keeps together related data points so that you can navigate between them when diagnosing a problem.</span></span> <span data-ttu-id="9446e-107">In the portal, the total counts are multiplied to compensate for the sampling.</span><span class="sxs-lookup"><span data-stu-id="9446e-107">In the portal, the total counts are multiplied to compensate for the sampling.</span></span>
* <span data-ttu-id="9446e-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span><span class="sxs-lookup"><span data-stu-id="9446e-108">Filtering with Telemetry Processors [for ASP.NET](#filtering) or [Java](app-insights-java-filter-telemetry.md) lets you select or modify telemetry in the SDK before it is sent to the server.</span></span> <span data-ttu-id="9446e-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span><span class="sxs-lookup"><span data-stu-id="9446e-109">For example, you could reduce the volume of telemetry by excluding requests from robots.</span></span> <span data-ttu-id="9446e-110">But filtering is a more basic approach to reducing traffic than sampling.</span><span class="sxs-lookup"><span data-stu-id="9446e-110">But filtering is a more basic approach to reducing traffic than sampling.</span></span> <span data-ttu-id="9446e-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span><span class="sxs-lookup"><span data-stu-id="9446e-111">It allows you more control over what is transmitted, but you have to be aware that it affects your statistics - for example, if you filter out all successful requests.</span></span>
* <span data-ttu-id="9446e-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span><span class="sxs-lookup"><span data-stu-id="9446e-112">[Telemetry Initializers add properties](#add-properties) to any telemetry sent from your app, including telemetry from the standard modules.</span></span> <span data-ttu-id="9446e-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span><span class="sxs-lookup"><span data-stu-id="9446e-113">For example, you could add calculated values; or version numbers by which to filter the data in the portal.</span></span>
* <span data-ttu-id="9446e-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span><span class="sxs-lookup"><span data-stu-id="9446e-114">[The SDK API](app-insights-api-custom-events-metrics.md) is used to send custom events and metrics.</span></span>

<span data-ttu-id="9446e-115">Before you start:</span><span class="sxs-lookup"><span data-stu-id="9446e-115">Before you start:</span></span>

* <span data-ttu-id="9446e-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span><span class="sxs-lookup"><span data-stu-id="9446e-116">Install the Application Insights [SDK for ASP.NET](app-insights-asp-net.md) or [SDK for Java](app-insights-java-get-started.md) in your app.</span></span>

<a name="filtering"></a>

## <a name="filtering-itelemetryprocessor"></a><span data-ttu-id="9446e-117">Filtering: ITelemetryProcessor</span><span class="sxs-lookup"><span data-stu-id="9446e-117">Filtering: ITelemetryProcessor</span></span>
<span data-ttu-id="9446e-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span><span class="sxs-lookup"><span data-stu-id="9446e-118">This technique gives you more direct control over what is included or excluded from the telemetry stream.</span></span> <span data-ttu-id="9446e-119">You can use it in conjunction with Sampling, or separately.</span><span class="sxs-lookup"><span data-stu-id="9446e-119">You can use it in conjunction with Sampling, or separately.</span></span>

<span data-ttu-id="9446e-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span><span class="sxs-lookup"><span data-stu-id="9446e-120">To filter telemetry, you write a telemetry processor and register it with the SDK.</span></span> <span data-ttu-id="9446e-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span><span class="sxs-lookup"><span data-stu-id="9446e-121">All telemetry goes through your processor, and you can choose to drop it from the stream, or add properties.</span></span> <span data-ttu-id="9446e-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span><span class="sxs-lookup"><span data-stu-id="9446e-122">This includes telemetry from the standard modules such as the HTTP request collector and the dependency collector, as well as telemetry you have written yourself.</span></span> <span data-ttu-id="9446e-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span><span class="sxs-lookup"><span data-stu-id="9446e-123">You can, for example, filter out telemetry about requests from robots, or successful dependency calls.</span></span>

> [!WARNING]
> <span data-ttu-id="9446e-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span><span class="sxs-lookup"><span data-stu-id="9446e-124">Filtering the telemetry sent from the SDK using processors can skew the statistics that you see in the portal, and make it difficult to follow related items.</span></span>
>
> <span data-ttu-id="9446e-125">Instead, consider using [sampling](app-insights-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="9446e-125">Instead, consider using [sampling](app-insights-sampling.md).</span></span>
>
>

### <a name="create-a-telemetry-processor-c"></a><span data-ttu-id="9446e-126">Create a telemetry processor (C#)</span><span class="sxs-lookup"><span data-stu-id="9446e-126">Create a telemetry processor (C#)</span></span>
1. <span data-ttu-id="9446e-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span><span class="sxs-lookup"><span data-stu-id="9446e-127">Verify that the Application Insights SDK in your project is  version 2.0.0 or later.</span></span> <span data-ttu-id="9446e-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span><span class="sxs-lookup"><span data-stu-id="9446e-128">Right-click your project in Visual Studio Solution Explorer and choose Manage NuGet Packages.</span></span> <span data-ttu-id="9446e-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span><span class="sxs-lookup"><span data-stu-id="9446e-129">In NuGet package manager, check Microsoft.ApplicationInsights.Web.</span></span>
2. <span data-ttu-id="9446e-130">To create a filter, implement ITelemetryProcessor.</span><span class="sxs-lookup"><span data-stu-id="9446e-130">To create a filter, implement ITelemetryProcessor.</span></span> <span data-ttu-id="9446e-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span><span class="sxs-lookup"><span data-stu-id="9446e-131">This is another extensibility point like telemetry module, telemetry initializer, and telemetry channel.</span></span>

    <span data-ttu-id="9446e-132">Notice that Telemetry Processors construct a chain of processing.</span><span class="sxs-lookup"><span data-stu-id="9446e-132">Notice that Telemetry Processors construct a chain of processing.</span></span> <span data-ttu-id="9446e-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span><span class="sxs-lookup"><span data-stu-id="9446e-133">When you instantiate a telemetry processor, you pass a link to the next processor in the chain.</span></span> <span data-ttu-id="9446e-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span><span class="sxs-lookup"><span data-stu-id="9446e-134">When a telemetry data point is passed to the Process method, it does its work and then calls the next Telemetry Processor in the chain.</span></span>

    ``` C#

    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    public class SuccessfulDependencyFilter : ITelemetryProcessor
      {

        private ITelemetryProcessor Next { get; set; }

        // You can pass values from .config
        public string MyParamFromConfigFile { get; set; }

        // Link processors to each other in a chain.
        public SuccessfulDependencyFilter(ITelemetryProcessor next)
        {
            this.Next = next;
        }
        public void Process(ITelemetry item)
        {
            // To filter out an item, just return
            if (!OKtoSend(item)) { return; }
            // Modify the item if required
            ModifyItem(item);

            this.Next.Process(item);
        }

        // Example: replace with your own criteria.
        private bool OKtoSend (ITelemetry item)
        {
            var dependency = item as DependencyTelemetry;
            if (dependency == null) return true;

            return dependency.Success != true;
        }

        // Example: replace with your own modifiers.
        private void ModifyItem (ITelemetry item)
        {
            item.Context.Properties.Add("app-version", "1." + MyParamFromConfigFile);
        }
    }

    ```
1. <span data-ttu-id="9446e-135">Insert this in ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="9446e-135">Insert this in ApplicationInsights.config:</span></span>

```XML

    <TelemetryProcessors>
      <Add Type="WebApplication9.SuccessfulDependencyFilter, WebApplication9">
         <!-- Set public property -->
         <MyParamFromConfigFile>2-beta</MyParamFromConfigFile>
      </Add>
    </TelemetryProcessors>

```

<span data-ttu-id="9446e-136">(This is the same section where you initialize a sampling filter.)</span><span class="sxs-lookup"><span data-stu-id="9446e-136">(This is the same section where you initialize a sampling filter.)</span></span>

<span data-ttu-id="9446e-137">You can pass string values from the .config file by providing public named properties in your class.</span><span class="sxs-lookup"><span data-stu-id="9446e-137">You can pass string values from the .config file by providing public named properties in your class.</span></span>

> [!WARNING]
> <span data-ttu-id="9446e-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span><span class="sxs-lookup"><span data-stu-id="9446e-138">Take care to match the type name and any property names in the .config file to the class and property names in the code.</span></span> <span data-ttu-id="9446e-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span><span class="sxs-lookup"><span data-stu-id="9446e-139">If the .config file references a non-existent type or property, the SDK may silently fail to send any telemetry.</span></span>
>
>

<span data-ttu-id="9446e-140">**Alternatively,** you can initialize the filter in code.</span><span class="sxs-lookup"><span data-stu-id="9446e-140">**Alternatively,** you can initialize the filter in code.</span></span> <span data-ttu-id="9446e-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span><span class="sxs-lookup"><span data-stu-id="9446e-141">In a suitable initialization class - for example AppStart in Global.asax.cs - insert your processor into the chain:</span></span>

```C#

    var builder = TelemetryConfiguration.Active.TelemetryProcessorChainBuilder;
    builder.Use((next) => new SuccessfulDependencyFilter(next));

    // If you have more processors:
    builder.Use((next) => new AnotherProcessor(next));

    builder.Build();

```

<span data-ttu-id="9446e-142">TelemetryClients created after this point will use your processors.</span><span class="sxs-lookup"><span data-stu-id="9446e-142">TelemetryClients created after this point will use your processors.</span></span>

### <a name="example-filters"></a><span data-ttu-id="9446e-143">Example filters</span><span class="sxs-lookup"><span data-stu-id="9446e-143">Example filters</span></span>
#### <a name="synthetic-requests"></a><span data-ttu-id="9446e-144">Synthetic requests</span><span class="sxs-lookup"><span data-stu-id="9446e-144">Synthetic requests</span></span>
<span data-ttu-id="9446e-145">Filter out bots and web tests.</span><span class="sxs-lookup"><span data-stu-id="9446e-145">Filter out bots and web tests.</span></span> <span data-ttu-id="9446e-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span><span class="sxs-lookup"><span data-stu-id="9446e-146">Although Metrics Explorer gives you the option to filter out synthetic sources, this option reduces traffic by filtering them at the SDK.</span></span>

``` C#

    public void Process(ITelemetry item)
    {
      if (!string.IsNullOrEmpty(item.Context.Operation.SyntheticSource)) {return;}

      // Send everything else:
      this.Next.Process(item);
    }

```

#### <a name="failed-authentication"></a><span data-ttu-id="9446e-147">Failed authentication</span><span class="sxs-lookup"><span data-stu-id="9446e-147">Failed authentication</span></span>
<span data-ttu-id="9446e-148">Filter out requests with a "401" response.</span><span class="sxs-lookup"><span data-stu-id="9446e-148">Filter out requests with a "401" response.</span></span>

```C#

public void Process(ITelemetry item)
{
    var request = item as RequestTelemetry;

    if (request != null &&
    request.ResponseCode.Equals("401", StringComparison.OrdinalIgnoreCase))
    {
        // To filter out an item, just terminate the chain:
        return;
    }
    // Send everything else:
    this.Next.Process(item);
}

```

#### <a name="filter-out-fast-remote-dependency-calls"></a><span data-ttu-id="9446e-149">Filter out fast remote dependency calls</span><span class="sxs-lookup"><span data-stu-id="9446e-149">Filter out fast remote dependency calls</span></span>
<span data-ttu-id="9446e-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span><span class="sxs-lookup"><span data-stu-id="9446e-150">If you only want to diagnose calls that are slow, filter out the fast ones.</span></span>

> [!NOTE]
> <span data-ttu-id="9446e-151">This will skew the statistics you see on the portal.</span><span class="sxs-lookup"><span data-stu-id="9446e-151">This will skew the statistics you see on the portal.</span></span> <span data-ttu-id="9446e-152">The dependency chart will look as if the dependency calls are all failures.</span><span class="sxs-lookup"><span data-stu-id="9446e-152">The dependency chart will look as if the dependency calls are all failures.</span></span>
>
>

``` C#

public void Process(ITelemetry item)
{
    var request = item as DependencyTelemetry;

    if (request != null && request.Duration.TotalMilliseconds < 100)
    {
        return;
    }
    this.Next.Process(item);
}

```

#### <a name="diagnose-dependency-issues"></a><span data-ttu-id="9446e-153">Diagnose dependency issues</span><span class="sxs-lookup"><span data-stu-id="9446e-153">Diagnose dependency issues</span></span>
<span data-ttu-id="9446e-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span><span class="sxs-lookup"><span data-stu-id="9446e-154">[This blog](https://azure.microsoft.com/blog/implement-an-application-insights-telemetry-processor/) describes a project to diagnose dependency issues by automatically sending regular pings to dependencies.</span></span>


<a name="add-properties"></a>

## <a name="add-properties-itelemetryinitializer"></a><span data-ttu-id="9446e-155">Add properties: ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="9446e-155">Add properties: ITelemetryInitializer</span></span>
<span data-ttu-id="9446e-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span><span class="sxs-lookup"><span data-stu-id="9446e-156">Use telemetry initializers to define global properties that are sent with all telemetry; and to override selected behavior of the standard telemetry modules.</span></span>

<span data-ttu-id="9446e-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="9446e-157">For example, the Application Insights for Web package collects telemetry about HTTP requests.</span></span> <span data-ttu-id="9446e-158">By default, it flags as failed any request with a response code >= 400.</span><span class="sxs-lookup"><span data-stu-id="9446e-158">By default, it flags as failed any request with a response code >= 400.</span></span> <span data-ttu-id="9446e-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span><span class="sxs-lookup"><span data-stu-id="9446e-159">But if you want to treat 400 as a success, you can provide a telemetry initializer that sets the Success property.</span></span>

<span data-ttu-id="9446e-160">If you provide a telemetry initializer, it is called whenever any of the Track\*() methods is called.</span><span class="sxs-lookup"><span data-stu-id="9446e-160">If you provide a telemetry initializer, it is called whenever any of the Track\*() methods is called.</span></span> <span data-ttu-id="9446e-161">This includes methods called by the standard telemetry modules.</span><span class="sxs-lookup"><span data-stu-id="9446e-161">This includes methods called by the standard telemetry modules.</span></span> <span data-ttu-id="9446e-162">By convention, these modules do not set any property that has already been set by an initializer.</span><span class="sxs-lookup"><span data-stu-id="9446e-162">By convention, these modules do not set any property that has already been set by an initializer.</span></span>

<span data-ttu-id="9446e-163">**Define your initializer**</span><span class="sxs-lookup"><span data-stu-id="9446e-163">**Define your initializer**</span></span>

<span data-ttu-id="9446e-164">*C#*</span><span class="sxs-lookup"><span data-stu-id="9446e-164">*C#*</span></span>

```C#

    using System;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.DataContracts;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that overrides the default SDK
       * behavior of treating response codes >= 400 as failed requests
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            var requestTelemetry = telemetry as RequestTelemetry;
            // Is this a TrackRequest() ?
            if (requestTelemetry == null) return;
            int code;
            bool parsed = Int32.TryParse(requestTelemetry.ResponseCode, out code);
            if (!parsed) return;
            if (code >= 400 && code < 500)
            {
                // If we set the Success property, the SDK won't change it:
                requestTelemetry.Success = true;
                // Allow us to filter these requests in the portal:
                requestTelemetry.Context.Properties["Overridden400s"] = "true";
            }
            // else leave the SDK to set the Success property      
        }
      }
    }
```

<span data-ttu-id="9446e-165">**Load your initializer**</span><span class="sxs-lookup"><span data-stu-id="9446e-165">**Load your initializer**</span></span>

<span data-ttu-id="9446e-166">In ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="9446e-166">In ApplicationInsights.config:</span></span>

    <ApplicationInsights>
      <TelemetryInitializers>
        <!-- Fully qualified type name, assembly name: -->
        <Add Type="MvcWebRole.Telemetry.MyTelemetryInitializer, MvcWebRole"/>
        ...
      </TelemetryInitializers>
    </ApplicationInsights>

<span data-ttu-id="9446e-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span><span class="sxs-lookup"><span data-stu-id="9446e-167">*Alternatively,* you can instantiate the initializer in code, for example in Global.aspx.cs:</span></span>

```C#
    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```


[<span data-ttu-id="9446e-168">See more of this sample.</span><span class="sxs-lookup"><span data-stu-id="9446e-168">See more of this sample.</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/tree/master/Samples/AzureEmailService/MvcWebRole)

<a name="js-initializer"></a>

### <a name="javascript-telemetry-initializers"></a><span data-ttu-id="9446e-169">JavaScript telemetry initializers</span><span class="sxs-lookup"><span data-stu-id="9446e-169">JavaScript telemetry initializers</span></span>
<span data-ttu-id="9446e-170">*JavaScript*</span><span class="sxs-lookup"><span data-stu-id="9446e-170">*JavaScript*</span></span>

<span data-ttu-id="9446e-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span><span class="sxs-lookup"><span data-stu-id="9446e-171">Insert a telemetry initializer immediately after the initialization code that you got from the portal:</span></span>

```JS

    <script type="text/javascript">
        // ... initialization code
        ...({
            instrumentationKey: "your instrumentation key"
        });
        window.appInsights = appInsights;


        // Adding telemetry initializer.
        // This is called whenever a new telemetry item
        // is created.

        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;

                // To check the telemetry item’s type - for example PageView:
                if (envelope.name == Microsoft.ApplicationInsights.Telemetry.PageView.envelopeType) {
                    // this statement removes url from all page view documents
                    telemetryItem.url = "URL CENSORED";
                }

                // To set custom properties:
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["globalProperty"] = "boo";

                // To set custom metrics:
                telemetryItem.measurements = telemetryItem.measurements || {};
                telemetryItem.measurements["globalMetric"] = 100;
            });
        });

        // End of inserted code.

        appInsights.trackPageView();
    </script>
```

<span data-ttu-id="9446e-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span><span class="sxs-lookup"><span data-stu-id="9446e-172">For a summary of the non-custom properties available on the telemetryItem, see [Application Insights Export Data Model](app-insights-export-data-model.md).</span></span>

<span data-ttu-id="9446e-173">You can add as many initializers as you like.</span><span class="sxs-lookup"><span data-stu-id="9446e-173">You can add as many initializers as you like.</span></span>

## <a name="itelemetryprocessor-and-itelemetryinitializer"></a><span data-ttu-id="9446e-174">ITelemetryProcessor and ITelemetryInitializer</span><span class="sxs-lookup"><span data-stu-id="9446e-174">ITelemetryProcessor and ITelemetryInitializer</span></span>
<span data-ttu-id="9446e-175">What's the difference between telemetry processors and telemetry initializers?</span><span class="sxs-lookup"><span data-stu-id="9446e-175">What's the difference between telemetry processors and telemetry initializers?</span></span>

* <span data-ttu-id="9446e-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span><span class="sxs-lookup"><span data-stu-id="9446e-176">There are some overlaps in what you can do with them: both can be used to add properties to telemetry.</span></span>
* <span data-ttu-id="9446e-177">TelemetryInitializers always run before TelemetryProcessors.</span><span class="sxs-lookup"><span data-stu-id="9446e-177">TelemetryInitializers always run before TelemetryProcessors.</span></span>
* <span data-ttu-id="9446e-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span><span class="sxs-lookup"><span data-stu-id="9446e-178">TelemetryProcessors allow you to completely replace or discard a telemetry item.</span></span>
* <span data-ttu-id="9446e-179">TelemetryProcessors don't process performance counter telemetry.</span><span class="sxs-lookup"><span data-stu-id="9446e-179">TelemetryProcessors don't process performance counter telemetry.</span></span>


## <a name="reference-docs"></a><span data-ttu-id="9446e-180">Reference docs</span><span class="sxs-lookup"><span data-stu-id="9446e-180">Reference docs</span></span>
* [<span data-ttu-id="9446e-181">API Overview</span><span class="sxs-lookup"><span data-stu-id="9446e-181">API Overview</span></span>](app-insights-api-custom-events-metrics.md)
* [<span data-ttu-id="9446e-182">ASP.NET reference</span><span class="sxs-lookup"><span data-stu-id="9446e-182">ASP.NET reference</span></span>](https://msdn.microsoft.com/library/dn817570.aspx)

## <a name="sdk-code"></a><span data-ttu-id="9446e-183">SDK Code</span><span class="sxs-lookup"><span data-stu-id="9446e-183">SDK Code</span></span>
* [<span data-ttu-id="9446e-184">ASP.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="9446e-184">ASP.NET Core SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [<span data-ttu-id="9446e-185">ASP.NET 5</span><span class="sxs-lookup"><span data-stu-id="9446e-185">ASP.NET 5</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [<span data-ttu-id="9446e-186">JavaScript SDK</span><span class="sxs-lookup"><span data-stu-id="9446e-186">JavaScript SDK</span></span>](https://github.com/Microsoft/ApplicationInsights-JS)

## <a name="next"></a><span data-ttu-id="9446e-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="9446e-187">Next steps</span></span>
* [<span data-ttu-id="9446e-188">Search events and logs</span><span class="sxs-lookup"><span data-stu-id="9446e-188">Search events and logs</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="9446e-189">Sampling</span><span class="sxs-lookup"><span data-stu-id="9446e-189">Sampling</span></span>](app-insights-sampling.md)
* [<span data-ttu-id="9446e-190">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="9446e-190">Troubleshooting</span></span>](app-insights-troubleshoot-faq.md)
