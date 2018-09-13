---
title: Azure Application Insights Snapshot Debugger for .NET apps | Microsoft Docs
description: Debug snapshots are automatically collected when exceptions are thrown in production .NET apps
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/08/2018
ms.reviewer: pharring
ms.author: mbullwin
ms.openlocfilehash: d4c27c8297fb5a2ad13a245279a206d00fc4f8b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870499"
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a><span data-ttu-id="ea865-103">Debug snapshots on exceptions in .NET apps</span><span class="sxs-lookup"><span data-stu-id="ea865-103">Debug snapshots on exceptions in .NET apps</span></span>

<span data-ttu-id="ea865-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span><span class="sxs-lookup"><span data-stu-id="ea865-104">When an exception occurs, you can automatically collect a debug snapshot from your live web application.</span></span> <span data-ttu-id="ea865-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span><span class="sxs-lookup"><span data-stu-id="ea865-105">The snapshot shows the state of source code and variables at the moment the exception was thrown.</span></span> <span data-ttu-id="ea865-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span><span class="sxs-lookup"><span data-stu-id="ea865-106">The Snapshot Debugger (preview) in [Azure Application Insights](app-insights-overview.md) monitors exception telemetry from your web app.</span></span> <span data-ttu-id="ea865-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span><span class="sxs-lookup"><span data-stu-id="ea865-107">It collects snapshots on your top-throwing exceptions so that you have the information you need to diagnose issues in production.</span></span> <span data-ttu-id="ea865-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-108">Include the [Snapshot collector NuGet package](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) in your application, and optionally configure collection parameters in [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md). Snapshots appear on [exceptions](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

<span data-ttu-id="ea865-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span><span class="sxs-lookup"><span data-stu-id="ea865-109">You can view debug snapshots in the portal to see the call stack and inspect variables at each call stack frame.</span></span> <span data-ttu-id="ea865-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="ea865-110">To get a more powerful debugging experience with source code, open snapshots with Visual Studio 2017 Enterprise by [downloading the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span> <span data-ttu-id="ea865-111">In Visual Studio, you can also [set Snappoints to interactively take snapshots](https://aka.ms/snappoint) without waiting for an exception.</span><span class="sxs-lookup"><span data-stu-id="ea865-111">In Visual Studio, you can also [set Snappoints to interactively take snapshots](https://aka.ms/snappoint) without waiting for an exception.</span></span>

<span data-ttu-id="ea865-112">Snapshot collection is available for:</span><span class="sxs-lookup"><span data-stu-id="ea865-112">Snapshot collection is available for:</span></span>
* <span data-ttu-id="ea865-113">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span><span class="sxs-lookup"><span data-stu-id="ea865-113">.NET Framework and ASP.NET applications running .NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="ea865-114">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span><span class="sxs-lookup"><span data-stu-id="ea865-114">.NET Core 2.0 and ASP.NET Core 2.0 applications running on Windows.</span></span>

<span data-ttu-id="ea865-115">The following environments are supported:</span><span class="sxs-lookup"><span data-stu-id="ea865-115">The following environments are supported:</span></span>
* <span data-ttu-id="ea865-116">Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ea865-116">Azure App Service.</span></span>
* <span data-ttu-id="ea865-117">Azure Cloud Service running OS family 4 or later.</span><span class="sxs-lookup"><span data-stu-id="ea865-117">Azure Cloud Service running OS family 4 or later.</span></span>
* <span data-ttu-id="ea865-118">Azure Service Fabric services running on Windows Server 2012 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="ea865-118">Azure Service Fabric services running on Windows Server 2012 R2 or later.</span></span>
* <span data-ttu-id="ea865-119">Azure Virtual Machines running Windows Server 2012 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="ea865-119">Azure Virtual Machines running Windows Server 2012 R2 or later.</span></span>
* <span data-ttu-id="ea865-120">On-premises virtual or physical machines running Windows Server 2012 R2 or later.</span><span class="sxs-lookup"><span data-stu-id="ea865-120">On-premises virtual or physical machines running Windows Server 2012 R2 or later.</span></span>

> [!NOTE]
> <span data-ttu-id="ea865-121">Client applications (for example, WPF, Windows Forms or UWP) are not supported.</span><span class="sxs-lookup"><span data-stu-id="ea865-121">Client applications (for example, WPF, Windows Forms or UWP) are not supported.</span></span>

### <a name="configure-snapshot-collection-for-aspnet-applications"></a><span data-ttu-id="ea865-122">Configure snapshot collection for ASP.NET applications</span><span class="sxs-lookup"><span data-stu-id="ea865-122">Configure snapshot collection for ASP.NET applications</span></span>

1. <span data-ttu-id="ea865-123">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span><span class="sxs-lookup"><span data-stu-id="ea865-123">[Enable Application Insights in your web app](app-insights-asp-net.md), if you haven't done it yet.</span></span>

2. <span data-ttu-id="ea865-124">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span><span class="sxs-lookup"><span data-stu-id="ea865-124">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="ea865-125">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="ea865-125">Review the default options that the package added to [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span>

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- The default is true, but you can disable Snapshot Debugging by setting it to false -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this to true. -->
        <!-- DeveloperMode is a property on the active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need to see an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>1</ThresholdForSnapshotting>
        <!-- The maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- The maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often we reconnect to the stamp. The default value is 15 minutes.-->
        <ReconnectInterval>00:15:00</ReconnectInterval>
        <!-- How often to reset problem counters. -->
        <ProblemCounterResetInterval>1.00:00:00</ProblemCounterResetInterval>
        <!-- The maximum number of snapshots allowed in ten minutes.The default value is 1. -->
        <SnapshotsPerTenMinutesLimit>1</SnapshotsPerTenMinutesLimit>
        <!-- The maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>30</SnapshotsPerDayLimit>
        <!-- Whether or not to collect snapshot in low IO priority thread. The default value is true. -->
        <SnapshotInLowPriorityThread>true</SnapshotInLowPriorityThread>
        <!-- Agree to send anonymous data to Microsoft to make this product better. -->
        <ProvideAnonymousTelemetry>true</ProvideAnonymousTelemetry>
        <!-- The limit on the number of failed requests to request snapshots before the telemetry processor is disabled. -->
        <FailedRequestLimit>3</FailedRequestLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. <span data-ttu-id="ea865-126">Snapshots are collected only on exceptions that are reported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-126">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="ea865-127">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-127">In some cases (for example, older versions of the .NET platform), you might need to [configure exception collection](app-insights-asp-net-exceptions.md#exceptions) to see exceptions with snapshots in the portal.</span></span>


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a><span data-ttu-id="ea865-128">Configure snapshot collection for ASP.NET Core 2.0 applications</span><span class="sxs-lookup"><span data-stu-id="ea865-128">Configure snapshot collection for ASP.NET Core 2.0 applications</span></span>

1. <span data-ttu-id="ea865-129">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span><span class="sxs-lookup"><span data-stu-id="ea865-129">[Enable Application Insights in your ASP.NET Core web app](app-insights-asp-net-core.md), if you haven't done it yet.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ea865-130">Be sure that your application references version 2.1.1, or newer, of the Microsoft.ApplicationInsights.AspNetCore package.</span><span class="sxs-lookup"><span data-stu-id="ea865-130">Be sure that your application references version 2.1.1, or newer, of the Microsoft.ApplicationInsights.AspNetCore package.</span></span>

2. <span data-ttu-id="ea865-131">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span><span class="sxs-lookup"><span data-stu-id="ea865-131">Include the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="ea865-132">Modify your application's `Startup` class to add and configure the Snapshot Collector's telemetry processor.</span><span class="sxs-lookup"><span data-stu-id="ea865-132">Modify your application's `Startup` class to add and configure the Snapshot Collector's telemetry processor.</span></span>

    <span data-ttu-id="ea865-133">Add the following using statements to `Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="ea865-133">Add the following using statements to `Startup.cs`</span></span>

   ```csharp
   using Microsoft.ApplicationInsights.SnapshotCollector;
   using Microsoft.Extensions.Options;
   using Microsoft.ApplicationInsights.AspNetCore;
   using Microsoft.ApplicationInsights.Extensibility;
   ```

   <span data-ttu-id="ea865-134">Add the following `SnapshotCollectorTelemetryProcessorFactory` class to `Startup` class.</span><span class="sxs-lookup"><span data-stu-id="ea865-134">Add the following `SnapshotCollectorTelemetryProcessorFactory` class to `Startup` class.</span></span>

   ```csharp
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           private readonly IServiceProvider _serviceProvider;

           public SnapshotCollectorTelemetryProcessorFactory(IServiceProvider serviceProvider) =>
               _serviceProvider = serviceProvider;

           public ITelemetryProcessor Create(ITelemetryProcessor next)
           {
               var snapshotConfigurationOptions = _serviceProvider.GetService<IOptions<SnapshotCollectorConfiguration>>();
               return new SnapshotCollectorTelemetryProcessor(next, configuration: snapshotConfigurationOptions.Value);
           }
       }
       ...
    ```
    <span data-ttu-id="ea865-135">Add the `SnapshotCollectorConfiguration` and `SnapshotCollectorTelemetryProcessorFactory` services to the startup pipeline:</span><span class="sxs-lookup"><span data-stu-id="ea865-135">Add the `SnapshotCollectorConfiguration` and `SnapshotCollectorTelemetryProcessorFactory` services to the startup pipeline:</span></span>

    ```csharp
       // This method gets called by the runtime. Use this method to add services to the container.
       public void ConfigureServices(IServiceCollection services)
       {
           // Configure SnapshotCollector from application settings
           services.Configure<SnapshotCollectorConfiguration>(Configuration.GetSection(nameof(SnapshotCollectorConfiguration)));

           // Add SnapshotCollector telemetry processor.
           services.AddSingleton<ITelemetryProcessorFactory>(sp => new SnapshotCollectorTelemetryProcessorFactory(sp));

           // TODO: Add other services your application needs here.
       }
   }
   ```

4. <span data-ttu-id="ea865-136">Configure the Snapshot Collector by adding a SnapshotCollectorConfiguration section to appsettings.json.</span><span class="sxs-lookup"><span data-stu-id="ea865-136">Configure the Snapshot Collector by adding a SnapshotCollectorConfiguration section to appsettings.json.</span></span> <span data-ttu-id="ea865-137">For example:</span><span class="sxs-lookup"><span data-stu-id="ea865-137">For example:</span></span>

   ```json
   {
     "ApplicationInsights": {
       "InstrumentationKey": "<your instrumentation key>"
     },
     "SnapshotCollectorConfiguration": {
       "IsEnabledInDeveloperMode": false,
       "ThresholdForSnapshotting": 1,
       "MaximumSnapshotsRequired": 3,
       "MaximumCollectionPlanSize": 50,
       "ReconnectInterval": "00:15:00",
       "ProblemCounterResetInterval":"1.00:00:00",
       "SnapshotsPerTenMinutesLimit": 1,
       "SnapshotsPerDayLimit": 30,
       "SnapshotInLowPriorityThread": true,
       "ProvideAnonymousTelemetry": true,
       "FailedRequestLimit": 3
     }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a><span data-ttu-id="ea865-138">Configure snapshot collection for other .NET applications</span><span class="sxs-lookup"><span data-stu-id="ea865-138">Configure snapshot collection for other .NET applications</span></span>

1. <span data-ttu-id="ea865-139">If your application isn't already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="ea865-139">If your application isn't already instrumented with Application Insights, get started by [enabling Application Insights and setting the instrumentation key](app-insights-windows-desktop.md).</span></span>

2. <span data-ttu-id="ea865-140">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span><span class="sxs-lookup"><span data-stu-id="ea865-140">Add the [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) NuGet package in your app.</span></span>

3. <span data-ttu-id="ea865-141">Snapshots are collected only on exceptions that are reported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-141">Snapshots are collected only on exceptions that are reported to Application Insights.</span></span> <span data-ttu-id="ea865-142">You may need to modify your code to report them.</span><span class="sxs-lookup"><span data-stu-id="ea865-142">You may need to modify your code to report them.</span></span> <span data-ttu-id="ea865-143">The exception handling code depends on the structure of your application, but an example is below:</span><span class="sxs-lookup"><span data-stu-id="ea865-143">The exception handling code depends on the structure of your application, but an example is below:</span></span>
    ```csharp
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle the request.
        }
        catch (Exception ex)
        {
            // Report the exception to Application Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow the exception if desired.
        }
   }
    ```

## <a name="grant-permissions"></a><span data-ttu-id="ea865-144">Grant permissions</span><span class="sxs-lookup"><span data-stu-id="ea865-144">Grant permissions</span></span>

<span data-ttu-id="ea865-145">Owners of the Azure subscription can inspect snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-145">Owners of the Azure subscription can inspect snapshots.</span></span> <span data-ttu-id="ea865-146">Other users must be granted permission by an owner.</span><span class="sxs-lookup"><span data-stu-id="ea865-146">Other users must be granted permission by an owner.</span></span>

<span data-ttu-id="ea865-147">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-147">To grant permission, assign the `Application Insights Snapshot Debugger` role to users who will inspect snapshots.</span></span> <span data-ttu-id="ea865-148">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span><span class="sxs-lookup"><span data-stu-id="ea865-148">This role can be assigned to individual users or groups by subscription owners for the target Application Insights resource or its resource group or subscription.</span></span>

1. <span data-ttu-id="ea865-149">Navigate to the Application Insights resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-149">Navigate to the Application Insights resource in the Azure portal.</span></span>
1. <span data-ttu-id="ea865-150">Click **Access Control (IAM)**.</span><span class="sxs-lookup"><span data-stu-id="ea865-150">Click **Access Control (IAM)**.</span></span>
1. <span data-ttu-id="ea865-151">Click the **+Add** button.</span><span class="sxs-lookup"><span data-stu-id="ea865-151">Click the **+Add** button.</span></span>
1. <span data-ttu-id="ea865-152">Select **Application Insights Snapshot Debugger** from the **Roles** drop-down list.</span><span class="sxs-lookup"><span data-stu-id="ea865-152">Select **Application Insights Snapshot Debugger** from the **Roles** drop-down list.</span></span>
1. <span data-ttu-id="ea865-153">Search for and enter a name for the user to add.</span><span class="sxs-lookup"><span data-stu-id="ea865-153">Search for and enter a name for the user to add.</span></span>
1. <span data-ttu-id="ea865-154">Click the **Save** button to add the user to the role.</span><span class="sxs-lookup"><span data-stu-id="ea865-154">Click the **Save** button to add the user to the role.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="ea865-155">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span><span class="sxs-lookup"><span data-stu-id="ea865-155">Snapshots can potentially contain personal and other sensitive information in variable and parameter values.</span></span>

## <a name="debug-snapshots-in-the-application-insights-portal"></a><span data-ttu-id="ea865-156">Debug snapshots in the Application Insights portal</span><span class="sxs-lookup"><span data-stu-id="ea865-156">Debug snapshots in the Application Insights portal</span></span>

<span data-ttu-id="ea865-157">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-157">If a snapshot is available for a given exception or a problem ID, an **Open Debug Snapshot** button appears on the [exception](app-insights-asp-net-exceptions.md) in the Application Insights portal.</span></span>

![Open Debug Snapshot button on exception](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

<span data-ttu-id="ea865-159">In the Debug Snapshot view, you see a call stack and a variables pane.</span><span class="sxs-lookup"><span data-stu-id="ea865-159">In the Debug Snapshot view, you see a call stack and a variables pane.</span></span> <span data-ttu-id="ea865-160">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span><span class="sxs-lookup"><span data-stu-id="ea865-160">When you select frames of the call stack in the call stack pane, you can view local variables and parameters for that function call in the variables pane.</span></span>

![View Debug Snapshot in the portal](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

<span data-ttu-id="ea865-162">Snapshots might include sensitive information, and by default they aren't viewable.</span><span class="sxs-lookup"><span data-stu-id="ea865-162">Snapshots might include sensitive information, and by default they aren't viewable.</span></span> <span data-ttu-id="ea865-163">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span><span class="sxs-lookup"><span data-stu-id="ea865-163">To view snapshots, you must have the `Application Insights Snapshot Debugger` role assigned to you.</span></span>

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a><span data-ttu-id="ea865-164">Debug snapshots with Visual Studio 2017 Enterprise</span><span class="sxs-lookup"><span data-stu-id="ea865-164">Debug snapshots with Visual Studio 2017 Enterprise</span></span>
1. <span data-ttu-id="ea865-165">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="ea865-165">Click the **Download Snapshot** button to download a `.diagsession` file, which can be opened by Visual Studio 2017 Enterprise.</span></span>

2. <span data-ttu-id="ea865-166">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span><span class="sxs-lookup"><span data-stu-id="ea865-166">To open the `.diagsession` file, you must first [download and install the Snapshot Debugger extension for Visual Studio](https://aka.ms/snapshotdebugger).</span></span>

3. <span data-ttu-id="ea865-167">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span><span class="sxs-lookup"><span data-stu-id="ea865-167">After you open the snapshot file, the Minidump Debugging page in Visual Studio appears.</span></span> <span data-ttu-id="ea865-168">Click **Debug Managed Code** to start debugging the snapshot.</span><span class="sxs-lookup"><span data-stu-id="ea865-168">Click **Debug Managed Code** to start debugging the snapshot.</span></span> <span data-ttu-id="ea865-169">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span><span class="sxs-lookup"><span data-stu-id="ea865-169">The snapshot opens to the line of code where the exception was thrown so that you can debug the current state of the process.</span></span>

    ![View debug snapshot in Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

<span data-ttu-id="ea865-171">The downloaded snapshot includes any symbol files that were found on your web application server.</span><span class="sxs-lookup"><span data-stu-id="ea865-171">The downloaded snapshot includes any symbol files that were found on your web application server.</span></span> <span data-ttu-id="ea865-172">These symbol files are required to associate snapshot data with source code.</span><span class="sxs-lookup"><span data-stu-id="ea865-172">These symbol files are required to associate snapshot data with source code.</span></span> <span data-ttu-id="ea865-173">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span><span class="sxs-lookup"><span data-stu-id="ea865-173">For App Service apps, make sure to enable symbol deployment when you publish your web apps.</span></span>

## <a name="how-snapshots-work"></a><span data-ttu-id="ea865-174">How snapshots work</span><span class="sxs-lookup"><span data-stu-id="ea865-174">How snapshots work</span></span>

<span data-ttu-id="ea865-175">The Snapshot Collector is implemented as an [Application Insights Telemetry Processor](app-insights-configuration-with-applicationinsights-config.md#telemetry-processors-aspnet).</span><span class="sxs-lookup"><span data-stu-id="ea865-175">The Snapshot Collector is implemented as an [Application Insights Telemetry Processor](app-insights-configuration-with-applicationinsights-config.md#telemetry-processors-aspnet).</span></span> <span data-ttu-id="ea865-176">When your application runs, the Snapshot Collector Telemetry Processor is added to your application's telemetry pipeline.</span><span class="sxs-lookup"><span data-stu-id="ea865-176">When your application runs, the Snapshot Collector Telemetry Processor is added to your application's telemetry pipeline.</span></span>
<span data-ttu-id="ea865-177">Each time your application calls [TrackException](app-insights-asp-net-exceptions.md#exceptions), the Snapshot Collector computes a Problem ID from the type of exception being thrown and the throwing method.</span><span class="sxs-lookup"><span data-stu-id="ea865-177">Each time your application calls [TrackException](app-insights-asp-net-exceptions.md#exceptions), the Snapshot Collector computes a Problem ID from the type of exception being thrown and the throwing method.</span></span>
<span data-ttu-id="ea865-178">Each time your application calls TrackException, a counter is incremented for the appropriate Problem ID.</span><span class="sxs-lookup"><span data-stu-id="ea865-178">Each time your application calls TrackException, a counter is incremented for the appropriate Problem ID.</span></span> <span data-ttu-id="ea865-179">When the counter reaches the `ThresholdForSnapshotting` value, the Problem ID is added to a Collection Plan.</span><span class="sxs-lookup"><span data-stu-id="ea865-179">When the counter reaches the `ThresholdForSnapshotting` value, the Problem ID is added to a Collection Plan.</span></span>

<span data-ttu-id="ea865-180">The Snapshot Collector also monitors exceptions as they're thrown by subscribing to the [AppDomain.CurrentDomain.FirstChanceException](https://docs.microsoft.com/dotnet/api/system.appdomain.firstchanceexception) event.</span><span class="sxs-lookup"><span data-stu-id="ea865-180">The Snapshot Collector also monitors exceptions as they're thrown by subscribing to the [AppDomain.CurrentDomain.FirstChanceException](https://docs.microsoft.com/dotnet/api/system.appdomain.firstchanceexception) event.</span></span> <span data-ttu-id="ea865-181">When that event fires, the Problem ID of the exception is computed and compared against the Problem IDs in the Collection Plan.</span><span class="sxs-lookup"><span data-stu-id="ea865-181">When that event fires, the Problem ID of the exception is computed and compared against the Problem IDs in the Collection Plan.</span></span>
<span data-ttu-id="ea865-182">If there's a match, then a snapshot of the running process is created.</span><span class="sxs-lookup"><span data-stu-id="ea865-182">If there's a match, then a snapshot of the running process is created.</span></span> <span data-ttu-id="ea865-183">The snapshot is assigned a unique identifier and the exception is stamped with that identifier.</span><span class="sxs-lookup"><span data-stu-id="ea865-183">The snapshot is assigned a unique identifier and the exception is stamped with that identifier.</span></span> <span data-ttu-id="ea865-184">After the FirstChanceException handler returns, the thrown exception is processed as normal.</span><span class="sxs-lookup"><span data-stu-id="ea865-184">After the FirstChanceException handler returns, the thrown exception is processed as normal.</span></span> <span data-ttu-id="ea865-185">Eventually, the exception reaches the TrackException method again where it, along with the snapshot identifier, is reported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-185">Eventually, the exception reaches the TrackException method again where it, along with the snapshot identifier, is reported to Application Insights.</span></span>

<span data-ttu-id="ea865-186">The main process continues to run and serve traffic to users with little interruption.</span><span class="sxs-lookup"><span data-stu-id="ea865-186">The main process continues to run and serve traffic to users with little interruption.</span></span> <span data-ttu-id="ea865-187">Meanwhile, the snapshot is handed off to the Snapshot Uploader process.</span><span class="sxs-lookup"><span data-stu-id="ea865-187">Meanwhile, the snapshot is handed off to the Snapshot Uploader process.</span></span> <span data-ttu-id="ea865-188">The Snapshot Uploader creates a minidump and uploads it to Application Insights along with any relevant symbol (.pdb) files.</span><span class="sxs-lookup"><span data-stu-id="ea865-188">The Snapshot Uploader creates a minidump and uploads it to Application Insights along with any relevant symbol (.pdb) files.</span></span>

> [!TIP]
> - <span data-ttu-id="ea865-189">A process snapshot is a suspended clone of the running process.</span><span class="sxs-lookup"><span data-stu-id="ea865-189">A process snapshot is a suspended clone of the running process.</span></span>
> - <span data-ttu-id="ea865-190">Creating the snapshot takes about 10 to 20 milliseconds.</span><span class="sxs-lookup"><span data-stu-id="ea865-190">Creating the snapshot takes about 10 to 20 milliseconds.</span></span>
> - <span data-ttu-id="ea865-191">The default value for `ThresholdForSnapshotting` is 1.</span><span class="sxs-lookup"><span data-stu-id="ea865-191">The default value for `ThresholdForSnapshotting` is 1.</span></span> <span data-ttu-id="ea865-192">This is also the minimum value.</span><span class="sxs-lookup"><span data-stu-id="ea865-192">This is also the minimum value.</span></span> <span data-ttu-id="ea865-193">Therefore, your app has to trigger the same exception **twice** before a snapshot is created.</span><span class="sxs-lookup"><span data-stu-id="ea865-193">Therefore, your app has to trigger the same exception **twice** before a snapshot is created.</span></span>
> - <span data-ttu-id="ea865-194">Set `IsEnabledInDeveloperMode` to true if you want to generate snapshots while debugging in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea865-194">Set `IsEnabledInDeveloperMode` to true if you want to generate snapshots while debugging in Visual Studio.</span></span>
> - <span data-ttu-id="ea865-195">The snapshot creation rate is limited by the `SnapshotsPerTenMinutesLimit` setting.</span><span class="sxs-lookup"><span data-stu-id="ea865-195">The snapshot creation rate is limited by the `SnapshotsPerTenMinutesLimit` setting.</span></span> <span data-ttu-id="ea865-196">By default, the limit is one snapshot every ten minutes.</span><span class="sxs-lookup"><span data-stu-id="ea865-196">By default, the limit is one snapshot every ten minutes.</span></span>
> - <span data-ttu-id="ea865-197">No more than 50 snapshots per day may be uploaded.</span><span class="sxs-lookup"><span data-stu-id="ea865-197">No more than 50 snapshots per day may be uploaded.</span></span>

## <a name="current-limitations"></a><span data-ttu-id="ea865-198">Current limitations</span><span class="sxs-lookup"><span data-stu-id="ea865-198">Current limitations</span></span>

### <a name="publish-symbols"></a><span data-ttu-id="ea865-199">Publish symbols</span><span class="sxs-lookup"><span data-stu-id="ea865-199">Publish symbols</span></span>
<span data-ttu-id="ea865-200">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea865-200">The Snapshot Debugger requires symbol files on the production server to decode variables and to provide a debugging experience in Visual Studio.</span></span>
<span data-ttu-id="ea865-201">Version 15.2 (or above) of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span><span class="sxs-lookup"><span data-stu-id="ea865-201">Version 15.2 (or above) of Visual Studio 2017 publishes symbols for release builds by default when it publishes to App Service.</span></span> <span data-ttu-id="ea865-202">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span><span class="sxs-lookup"><span data-stu-id="ea865-202">In prior versions, you need to add the following line to your publish profile `.pubxml` file so that symbols are published in release mode:</span></span>

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

<span data-ttu-id="ea865-203">For Azure Compute and other types, make sure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span><span class="sxs-lookup"><span data-stu-id="ea865-203">For Azure Compute and other types, make sure that the symbol files are in the same folder of the main application .dll (typically, `wwwroot/bin`) or are available on the current path.</span></span>

### <a name="optimized-builds"></a><span data-ttu-id="ea865-204">Optimized builds</span><span class="sxs-lookup"><span data-stu-id="ea865-204">Optimized builds</span></span>
<span data-ttu-id="ea865-205">In some cases, local variables can't be viewed in release builds because of optimizations that are applied by the JIT compiler.</span><span class="sxs-lookup"><span data-stu-id="ea865-205">In some cases, local variables can't be viewed in release builds because of optimizations that are applied by the JIT compiler.</span></span>
<span data-ttu-id="ea865-206">However, in Azure App Services, the Snapshot Collector can deoptimize throwing methods that are part of its Collection Plan.</span><span class="sxs-lookup"><span data-stu-id="ea865-206">However, in Azure App Services, the Snapshot Collector can deoptimize throwing methods that are part of its Collection Plan.</span></span>

> [!TIP]
> <span data-ttu-id="ea865-207">Install the Application Insights Site Extension in your App Service to get deoptimization support.</span><span class="sxs-lookup"><span data-stu-id="ea865-207">Install the Application Insights Site Extension in your App Service to get deoptimization support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ea865-208">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="ea865-208">Troubleshooting</span></span>

<span data-ttu-id="ea865-209">These tips help you troubleshoot problems with the Snapshot Debugger.</span><span class="sxs-lookup"><span data-stu-id="ea865-209">These tips help you troubleshoot problems with the Snapshot Debugger.</span></span>

### <a name="use-the-snapshot-health-check"></a><span data-ttu-id="ea865-210">Use the snapshot health check</span><span class="sxs-lookup"><span data-stu-id="ea865-210">Use the snapshot health check</span></span>
<span data-ttu-id="ea865-211">Several common problems result in the Open Debug Snapshot not showing up.</span><span class="sxs-lookup"><span data-stu-id="ea865-211">Several common problems result in the Open Debug Snapshot not showing up.</span></span> <span data-ttu-id="ea865-212">Using an outdated Snapshot Collector, for example; reaching the daily upload limit; or perhaps the snapshot is just taking a long time to upload.</span><span class="sxs-lookup"><span data-stu-id="ea865-212">Using an outdated Snapshot Collector, for example; reaching the daily upload limit; or perhaps the snapshot is just taking a long time to upload.</span></span> <span data-ttu-id="ea865-213">Use the Snapshot Health Check to troubleshoot common problems.</span><span class="sxs-lookup"><span data-stu-id="ea865-213">Use the Snapshot Health Check to troubleshoot common problems.</span></span>

<span data-ttu-id="ea865-214">There's a link in the exception pane of the end-to-end trace view that takes you to the Snapshot Health Check.</span><span class="sxs-lookup"><span data-stu-id="ea865-214">There's a link in the exception pane of the end-to-end trace view that takes you to the Snapshot Health Check.</span></span>

![Enter snapshot health check](./media/app-insights-snapshot-debugger/enter-snapshot-health-check.png)

<span data-ttu-id="ea865-216">The interactive, chat-like interface looks for common problems and guides you to fix them.</span><span class="sxs-lookup"><span data-stu-id="ea865-216">The interactive, chat-like interface looks for common problems and guides you to fix them.</span></span>

![Health Check](./media/app-insights-snapshot-debugger/healthcheck.png)

<span data-ttu-id="ea865-218">If that doesn't solve the problem, then refer to the following manual troubleshooting steps.</span><span class="sxs-lookup"><span data-stu-id="ea865-218">If that doesn't solve the problem, then refer to the following manual troubleshooting steps.</span></span>

### <a name="verify-the-instrumentation-key"></a><span data-ttu-id="ea865-219">Verify the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="ea865-219">Verify the instrumentation key</span></span>

<span data-ttu-id="ea865-220">Make sure you're using the correct instrumentation key in your published application.</span><span class="sxs-lookup"><span data-stu-id="ea865-220">Make sure you're using the correct instrumentation key in your published application.</span></span> <span data-ttu-id="ea865-221">Usually, the instrumentation key is read from the ApplicationInsights.config file.</span><span class="sxs-lookup"><span data-stu-id="ea865-221">Usually, the instrumentation key is read from the ApplicationInsights.config file.</span></span> <span data-ttu-id="ea865-222">Verify the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-222">Verify the value is the same as the instrumentation key for the Application Insights resource that you see in the portal.</span></span>

### <a name="upgrade-to-the-latest-version-of-the-nuget-package"></a><span data-ttu-id="ea865-223">Upgrade to the latest version of the NuGet package</span><span class="sxs-lookup"><span data-stu-id="ea865-223">Upgrade to the latest version of the NuGet package</span></span>

<span data-ttu-id="ea865-224">Use Visual Studio's NuGet Package Manager to make sure you're using the latest version of Microsoft.ApplicationInsights.SnapshotCollector.</span><span class="sxs-lookup"><span data-stu-id="ea865-224">Use Visual Studio's NuGet Package Manager to make sure you're using the latest version of Microsoft.ApplicationInsights.SnapshotCollector.</span></span> <span data-ttu-id="ea865-225">Release notes can be found at https://github.com/Microsoft/ApplicationInsights-Home/issues/167</span><span class="sxs-lookup"><span data-stu-id="ea865-225">Release notes can be found at https://github.com/Microsoft/ApplicationInsights-Home/issues/167</span></span>

### <a name="check-the-uploader-logs"></a><span data-ttu-id="ea865-226">Check the uploader logs</span><span class="sxs-lookup"><span data-stu-id="ea865-226">Check the uploader logs</span></span>

<span data-ttu-id="ea865-227">After a snapshot is created, a minidump file (.dmp) is created on disk.</span><span class="sxs-lookup"><span data-stu-id="ea865-227">After a snapshot is created, a minidump file (.dmp) is created on disk.</span></span> <span data-ttu-id="ea865-228">A separate uploader process creates that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span><span class="sxs-lookup"><span data-stu-id="ea865-228">A separate uploader process creates that minidump file and uploads it, along with any associated PDBs, to Application Insights Snapshot Debugger storage.</span></span> <span data-ttu-id="ea865-229">After the minidump has uploaded successfully, it's deleted from disk.</span><span class="sxs-lookup"><span data-stu-id="ea865-229">After the minidump has uploaded successfully, it's deleted from disk.</span></span> <span data-ttu-id="ea865-230">The log files for the uploader process are kept on disk.</span><span class="sxs-lookup"><span data-stu-id="ea865-230">The log files for the uploader process are kept on disk.</span></span> <span data-ttu-id="ea865-231">In an App Service environment, you can find these logs in `D:\Home\LogFiles`.</span><span class="sxs-lookup"><span data-stu-id="ea865-231">In an App Service environment, you can find these logs in `D:\Home\LogFiles`.</span></span> <span data-ttu-id="ea865-232">Use the Kudu management site for App Service to find these log files.</span><span class="sxs-lookup"><span data-stu-id="ea865-232">Use the Kudu management site for App Service to find these log files.</span></span>

1. <span data-ttu-id="ea865-233">Open your App Service application in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-233">Open your App Service application in the Azure portal.</span></span>
2. <span data-ttu-id="ea865-234">Click **Advanced Tools**, or search for **Kudu**.</span><span class="sxs-lookup"><span data-stu-id="ea865-234">Click **Advanced Tools**, or search for **Kudu**.</span></span>
3. <span data-ttu-id="ea865-235">Click **Go**.</span><span class="sxs-lookup"><span data-stu-id="ea865-235">Click **Go**.</span></span>
4. <span data-ttu-id="ea865-236">In the **Debug console** drop-down list box, select **CMD**.</span><span class="sxs-lookup"><span data-stu-id="ea865-236">In the **Debug console** drop-down list box, select **CMD**.</span></span>
5. <span data-ttu-id="ea865-237">Click **LogFiles**.</span><span class="sxs-lookup"><span data-stu-id="ea865-237">Click **LogFiles**.</span></span>

<span data-ttu-id="ea865-238">You should see at least one file with a name that begins with `Uploader_` or `SnapshotUploader_` and a `.log` extension.</span><span class="sxs-lookup"><span data-stu-id="ea865-238">You should see at least one file with a name that begins with `Uploader_` or `SnapshotUploader_` and a `.log` extension.</span></span> <span data-ttu-id="ea865-239">Click the appropriate icon to download any log files or open them in a browser.</span><span class="sxs-lookup"><span data-stu-id="ea865-239">Click the appropriate icon to download any log files or open them in a browser.</span></span>
<span data-ttu-id="ea865-240">The file name includes a unique suffix that identifies the App Service instance.</span><span class="sxs-lookup"><span data-stu-id="ea865-240">The file name includes a unique suffix that identifies the App Service instance.</span></span> <span data-ttu-id="ea865-241">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span><span class="sxs-lookup"><span data-stu-id="ea865-241">If your App Service instance is hosted on more than one machine, there are separate log files for each machine.</span></span> <span data-ttu-id="ea865-242">When the uploader detects a new minidump file, it's recorded in the log file.</span><span class="sxs-lookup"><span data-stu-id="ea865-242">When the uploader detects a new minidump file, it's recorded in the log file.</span></span> <span data-ttu-id="ea865-243">Here's an example of a successful snapshot and upload:</span><span class="sxs-lookup"><span data-stu-id="ea865-243">Here's an example of a successful snapshot and upload:</span></span>

```
SnapshotUploader.exe Information: 0 : Received Fork request ID 139e411a23934dc0b9ea08a626db16c5 from process 6368 (Low pri)
    DateTime=2018-03-09T01:42:41.8571711Z
SnapshotUploader.exe Information: 0 : Creating minidump from Fork request ID 139e411a23934dc0b9ea08a626db16c5 from process 6368 (Low pri)
    DateTime=2018-03-09T01:42:41.8571711Z
SnapshotUploader.exe Information: 0 : Dump placeholder file created: 139e411a23934dc0b9ea08a626db16c5.dm_
    DateTime=2018-03-09T01:42:41.8728496Z
SnapshotUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2018-03-09T01:42:45.7525022Z
SnapshotUploader.exe Information: 0 : Successfully wrote minidump to D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2018-03-09T01:42:45.7681360Z
SnapshotUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 214.42 MB (uncompressed)
    DateTime=2018-03-09T01:42:45.7681360Z
SnapshotUploader.exe Information: 0 : Upload successful. Compressed size 86.56 MB
    DateTime=2018-03-09T01:42:59.6184651Z
SnapshotUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2018-03-09T01:42:59.6184651Z
SnapshotUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2018-03-09T01:42:59.6809606Z
SnapshotUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2018-03-09T01:42:59.8059929Z
SnapshotUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2018-03-09T01:42:59.8530649Z
```

> [!NOTE]
> <span data-ttu-id="ea865-244">The example above is from version 1.2.0 of the Microsoft.ApplicationInsights.SnapshotCollector NuGet package.</span><span class="sxs-lookup"><span data-stu-id="ea865-244">The example above is from version 1.2.0 of the Microsoft.ApplicationInsights.SnapshotCollector NuGet package.</span></span> <span data-ttu-id="ea865-245">In earlier versions, the uploader process is called `MinidumpUploader.exe` and the log is less detailed.</span><span class="sxs-lookup"><span data-stu-id="ea865-245">In earlier versions, the uploader process is called `MinidumpUploader.exe` and the log is less detailed.</span></span>

<span data-ttu-id="ea865-246">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span><span class="sxs-lookup"><span data-stu-id="ea865-246">In the previous example, the instrumentation key is `c12a605e73c44346a984e00000000000`.</span></span> <span data-ttu-id="ea865-247">This value should match the instrumentation key for your application.</span><span class="sxs-lookup"><span data-stu-id="ea865-247">This value should match the instrumentation key for your application.</span></span>
<span data-ttu-id="ea865-248">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span><span class="sxs-lookup"><span data-stu-id="ea865-248">The minidump is associated with a snapshot with the ID `139e411a23934dc0b9ea08a626db16c5`.</span></span> <span data-ttu-id="ea865-249">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span><span class="sxs-lookup"><span data-stu-id="ea865-249">You can use this ID later to locate the associated exception telemetry in Application Insights Analytics.</span></span>

<span data-ttu-id="ea865-250">The uploader scans for new PDBs about once every 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="ea865-250">The uploader scans for new PDBs about once every 15 minutes.</span></span> <span data-ttu-id="ea865-251">Here's an example:</span><span class="sxs-lookup"><span data-stu-id="ea865-251">Here's an example:</span></span>

```
SnapshotUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2018-03-09T01:47:19.4457768Z
SnapshotUploader.exe Information: 0 : Scanning D:\home\site\wwwroot for local PDBs.
    DateTime=2018-03-09T01:47:19.4457768Z
SnapshotUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2018-03-09T01:47:19.4614027Z
SnapshotUploader.exe Information: 0 : Deleted PDB scan marker : D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\6368.pdbscan
    DateTime=2018-03-09T01:47:19.4614027Z
```

<span data-ttu-id="ea865-252">For applications that _aren't_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span><span class="sxs-lookup"><span data-stu-id="ea865-252">For applications that _aren't_ hosted in App Service, the uploader logs are in the same folder as the minidumps: `%TEMP%\Dumps\<ikey>` (where `<ikey>` is your instrumentation key).</span></span>

### <a name="troubleshooting-cloud-services"></a><span data-ttu-id="ea865-253">Troubleshooting Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ea865-253">Troubleshooting Cloud Services</span></span>
<span data-ttu-id="ea865-254">For roles in Cloud Services, the default temporary folder may be too small to hold the minidump files, leading to lost snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-254">For roles in Cloud Services, the default temporary folder may be too small to hold the minidump files, leading to lost snapshots.</span></span>
<span data-ttu-id="ea865-255">The space needed depends on the total working set of your application and the number of concurrent snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-255">The space needed depends on the total working set of your application and the number of concurrent snapshots.</span></span>
<span data-ttu-id="ea865-256">The working set of a 32-bit ASP.NET web role is typically between 200 MB and 500 MB.</span><span class="sxs-lookup"><span data-stu-id="ea865-256">The working set of a 32-bit ASP.NET web role is typically between 200 MB and 500 MB.</span></span>
<span data-ttu-id="ea865-257">Allow for at least two concurrent snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-257">Allow for at least two concurrent snapshots.</span></span>
<span data-ttu-id="ea865-258">For example, if your application uses 1 GB of total working set, you should make sure that there is at least 2 GB of disk space to store snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-258">For example, if your application uses 1 GB of total working set, you should make sure that there is at least 2 GB of disk space to store snapshots.</span></span>
<span data-ttu-id="ea865-259">Follow these steps to configure your Cloud Service role with a dedicated local resource for snapshots.</span><span class="sxs-lookup"><span data-stu-id="ea865-259">Follow these steps to configure your Cloud Service role with a dedicated local resource for snapshots.</span></span>

1. <span data-ttu-id="ea865-260">Add a new local resource to your Cloud Service by editing the Cloud Service definition (.csdef) file.</span><span class="sxs-lookup"><span data-stu-id="ea865-260">Add a new local resource to your Cloud Service by editing the Cloud Service definition (.csdef) file.</span></span> <span data-ttu-id="ea865-261">The following example defines a resource called `SnapshotStore` with a size of 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ea865-261">The following example defines a resource called `SnapshotStore` with a size of 5 GB.</span></span>
   ```xml
   <LocalResources>
     <LocalStorage name="SnapshotStore" cleanOnRoleRecycle="false" sizeInMB="5120" />
   </LocalResources>
   ```

2. <span data-ttu-id="ea865-262">Modify your role's startup code to add an environment variable that points to the `SnapshotStore` local resource.</span><span class="sxs-lookup"><span data-stu-id="ea865-262">Modify your role's startup code to add an environment variable that points to the `SnapshotStore` local resource.</span></span> <span data-ttu-id="ea865-263">For Worker Roles, the code should be added to your role's `OnStart` method:</span><span class="sxs-lookup"><span data-stu-id="ea865-263">For Worker Roles, the code should be added to your role's `OnStart` method:</span></span>
   ```csharp
   public override bool OnStart()
   {
       Environment.SetEnvironmentVariable("SNAPSHOTSTORE", RoleEnvironment.GetLocalResource("SnapshotStore").RootPath);
       return base.OnStart();
   }
   ```
   <span data-ttu-id="ea865-264">For Web Roles (ASP.NET), the code should be added to your web application's `Application_Start` method:</span><span class="sxs-lookup"><span data-stu-id="ea865-264">For Web Roles (ASP.NET), the code should be added to your web application's `Application_Start` method:</span></span>
   ```csharp
   using Microsoft.WindowsAzure.ServiceRuntime;
   using System;

   namespace MyWebRoleApp
   {
       public class MyMvcApplication : System.Web.HttpApplication
       {
          protected void Application_Start()
          {
             Environment.SetEnvironmentVariable("SNAPSHOTSTORE", RoleEnvironment.GetLocalResource("SnapshotStore").RootPath);
             // TODO: The rest of your application startup code
          }
       }
   }
   ```

3. <span data-ttu-id="ea865-265">Update your role's ApplicationInsights.config file to override the temporary folder location used by `SnapshotCollector`</span><span class="sxs-lookup"><span data-stu-id="ea865-265">Update your role's ApplicationInsights.config file to override the temporary folder location used by `SnapshotCollector`</span></span>
   ```xml
   <TelemetryProcessors>
    <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
      <!-- Use the SnapshotStore local resource for snapshots -->
      <TempFolder>%SNAPSHOTSTORE%</TempFolder>
      <!-- Other SnapshotCollector configuration options -->
    </Add>
   </TelemetryProcessors>
   ```

### <a name="overriding-the-shadow-copy-folder"></a><span data-ttu-id="ea865-266">Overriding the Shadow Copy folder</span><span class="sxs-lookup"><span data-stu-id="ea865-266">Overriding the Shadow Copy folder</span></span>

<span data-ttu-id="ea865-267">When the Snapshot Collector starts up, it tries to find a folder on disk that is suitable for running the Snapshot Uploader process.</span><span class="sxs-lookup"><span data-stu-id="ea865-267">When the Snapshot Collector starts up, it tries to find a folder on disk that is suitable for running the Snapshot Uploader process.</span></span> <span data-ttu-id="ea865-268">The chosen folder is known as the Shadow Copy folder.</span><span class="sxs-lookup"><span data-stu-id="ea865-268">The chosen folder is known as the Shadow Copy folder.</span></span>

<span data-ttu-id="ea865-269">The Snapshot Collector checks a few well-known locations, making sure it has permissions to copy the Snapshot Uploader binaries.</span><span class="sxs-lookup"><span data-stu-id="ea865-269">The Snapshot Collector checks a few well-known locations, making sure it has permissions to copy the Snapshot Uploader binaries.</span></span> <span data-ttu-id="ea865-270">The following environment variables are used:</span><span class="sxs-lookup"><span data-stu-id="ea865-270">The following environment variables are used:</span></span>
- <span data-ttu-id="ea865-271">Fabric_Folder_App_Temp</span><span class="sxs-lookup"><span data-stu-id="ea865-271">Fabric_Folder_App_Temp</span></span>
- <span data-ttu-id="ea865-272">LOCALAPPDATA</span><span class="sxs-lookup"><span data-stu-id="ea865-272">LOCALAPPDATA</span></span>
- <span data-ttu-id="ea865-273">APPDATA</span><span class="sxs-lookup"><span data-stu-id="ea865-273">APPDATA</span></span>
- <span data-ttu-id="ea865-274">TEMP</span><span class="sxs-lookup"><span data-stu-id="ea865-274">TEMP</span></span>

<span data-ttu-id="ea865-275">If a suitable folder can't be found, Snapshot Collector reports an error saying _"Could not find a suitable shadow copy folder."_</span><span class="sxs-lookup"><span data-stu-id="ea865-275">If a suitable folder can't be found, Snapshot Collector reports an error saying _"Could not find a suitable shadow copy folder."_</span></span>

<span data-ttu-id="ea865-276">If the copy fails, Snapshot Collector reports a `ShadowCopyFailed` error.</span><span class="sxs-lookup"><span data-stu-id="ea865-276">If the copy fails, Snapshot Collector reports a `ShadowCopyFailed` error.</span></span>

<span data-ttu-id="ea865-277">If the uploader can't be launched, Snapshot Collector reports an `UploaderCannotStartFromShadowCopy` error.</span><span class="sxs-lookup"><span data-stu-id="ea865-277">If the uploader can't be launched, Snapshot Collector reports an `UploaderCannotStartFromShadowCopy` error.</span></span> <span data-ttu-id="ea865-278">The body of the message often contains `System.UnauthorizedAccessException`.</span><span class="sxs-lookup"><span data-stu-id="ea865-278">The body of the message often contains `System.UnauthorizedAccessException`.</span></span> <span data-ttu-id="ea865-279">This error usually occurs because the application is running under an account with reduced permissions.</span><span class="sxs-lookup"><span data-stu-id="ea865-279">This error usually occurs because the application is running under an account with reduced permissions.</span></span> <span data-ttu-id="ea865-280">The account has permission to write to the shadow copy folder, but it doesn't have permission to execute code.</span><span class="sxs-lookup"><span data-stu-id="ea865-280">The account has permission to write to the shadow copy folder, but it doesn't have permission to execute code.</span></span>

<span data-ttu-id="ea865-281">Since these errors usually happen during startup, they'll usually be followed by an `ExceptionDuringConnect` error saying _"Uploader failed to start."_</span><span class="sxs-lookup"><span data-stu-id="ea865-281">Since these errors usually happen during startup, they'll usually be followed by an `ExceptionDuringConnect` error saying _"Uploader failed to start."_</span></span>

<span data-ttu-id="ea865-282">To work around these errors, you can specify the shadow copy folder manually via the `ShadowCopyFolder` configuration option.</span><span class="sxs-lookup"><span data-stu-id="ea865-282">To work around these errors, you can specify the shadow copy folder manually via the `ShadowCopyFolder` configuration option.</span></span> <span data-ttu-id="ea865-283">For example, using ApplicationInsights.config:</span><span class="sxs-lookup"><span data-stu-id="ea865-283">For example, using ApplicationInsights.config:</span></span>

   ```xml
   <TelemetryProcessors>
    <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
      <!-- Override the default shadow copy folder. -->
      <ShadowCopyFolder>D:\SnapshotUploader</ShadowCopyFolder>
      <!-- Other SnapshotCollector configuration options -->
    </Add>
   </TelemetryProcessors>
   ```

<span data-ttu-id="ea865-284">Or, if you're using appsettings.json with a .NET Core application:</span><span class="sxs-lookup"><span data-stu-id="ea865-284">Or, if you're using appsettings.json with a .NET Core application:</span></span>

   ```json
   {
     "ApplicationInsights": {
       "InstrumentationKey": "<your instrumentation key>"
     },
     "SnapshotCollectorConfiguration": {
       "ShadowCopyFolder": "D:\\SnapshotUploader"
     }
   }
   ```

### <a name="use-application-insights-search-to-find-exceptions-with-snapshots"></a><span data-ttu-id="ea865-285">Use Application Insights search to find exceptions with snapshots</span><span class="sxs-lookup"><span data-stu-id="ea865-285">Use Application Insights search to find exceptions with snapshots</span></span>

<span data-ttu-id="ea865-286">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span><span class="sxs-lookup"><span data-stu-id="ea865-286">When a snapshot is created, the throwing exception is tagged with a snapshot ID.</span></span> <span data-ttu-id="ea865-287">That snapshot ID is included as a custom property when the exception telemetry is reported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-287">That snapshot ID is included as a custom property when the exception telemetry is reported to Application Insights.</span></span> <span data-ttu-id="ea865-288">Using **Search** in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span><span class="sxs-lookup"><span data-stu-id="ea865-288">Using **Search** in Application Insights, you can find all telemetry with the `ai.snapshot.id` custom property.</span></span>

1. <span data-ttu-id="ea865-289">Browse to your Application Insights resource in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ea865-289">Browse to your Application Insights resource in the Azure portal.</span></span>
2. <span data-ttu-id="ea865-290">Click **Search**.</span><span class="sxs-lookup"><span data-stu-id="ea865-290">Click **Search**.</span></span>
3. <span data-ttu-id="ea865-291">Type `ai.snapshot.id` in the Search text box and press Enter.</span><span class="sxs-lookup"><span data-stu-id="ea865-291">Type `ai.snapshot.id` in the Search text box and press Enter.</span></span>

![Search for telemetry with a snapshot ID in the portal](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

<span data-ttu-id="ea865-293">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span><span class="sxs-lookup"><span data-stu-id="ea865-293">If this search returns no results, then no snapshots were reported to Application Insights for your application in the selected time range.</span></span>

<span data-ttu-id="ea865-294">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span><span class="sxs-lookup"><span data-stu-id="ea865-294">To search for a specific snapshot ID from the Uploader logs, type that ID in the Search box.</span></span> <span data-ttu-id="ea865-295">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="ea865-295">If you can't find telemetry for a snapshot that you know was uploaded, follow these steps:</span></span>

1. <span data-ttu-id="ea865-296">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span><span class="sxs-lookup"><span data-stu-id="ea865-296">Double-check that you're looking at the right Application Insights resource by verifying the instrumentation key.</span></span>

2. <span data-ttu-id="ea865-297">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span><span class="sxs-lookup"><span data-stu-id="ea865-297">Using the timestamp from the Uploader log, adjust the Time Range filter of the search to cover that time range.</span></span>

<span data-ttu-id="ea865-298">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-298">If you still don't see an exception with that snapshot ID, then the exception telemetry wasn't reported to Application Insights.</span></span> <span data-ttu-id="ea865-299">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span><span class="sxs-lookup"><span data-stu-id="ea865-299">This situation can happen if your application crashed after it took the snapshot but before it reported the exception telemetry.</span></span> <span data-ttu-id="ea865-300">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span><span class="sxs-lookup"><span data-stu-id="ea865-300">In this case, check the App Service logs under `Diagnose and solve problems` to see if there were unexpected restarts or unhandled exceptions.</span></span>

### <a name="edit-network-proxy-or-firewall-rules"></a><span data-ttu-id="ea865-301">Edit network proxy or firewall rules</span><span class="sxs-lookup"><span data-stu-id="ea865-301">Edit network proxy or firewall rules</span></span>

<span data-ttu-id="ea865-302">If your application connects to the Internet via a proxy or a firewall, you may need to edit the rules to allow your application to communicate with the Snapshot Debugger service.</span><span class="sxs-lookup"><span data-stu-id="ea865-302">If your application connects to the Internet via a proxy or a firewall, you may need to edit the rules to allow your application to communicate with the Snapshot Debugger service.</span></span> <span data-ttu-id="ea865-303">Here is [a list of IP addresses and ports used by the Snapshot Debugger](app-insights-ip-addresses.md#snapshot-debugger).</span><span class="sxs-lookup"><span data-stu-id="ea865-303">Here is [a list of IP addresses and ports used by the Snapshot Debugger](app-insights-ip-addresses.md#snapshot-debugger).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea865-304">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea865-304">Next steps</span></span>

* <span data-ttu-id="ea865-305">[Set snappoints in your code](https://docs.microsoft.com/visualstudio/debugger/debug-live-azure-applications) to get snapshots without waiting for an exception.</span><span class="sxs-lookup"><span data-stu-id="ea865-305">[Set snappoints in your code](https://docs.microsoft.com/visualstudio/debugger/debug-live-azure-applications) to get snapshots without waiting for an exception.</span></span>
* <span data-ttu-id="ea865-306">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="ea865-306">[Diagnose exceptions in your web apps](app-insights-asp-net-exceptions.md) explains how to make more exceptions visible to Application Insights.</span></span>
* <span data-ttu-id="ea865-307">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span><span class="sxs-lookup"><span data-stu-id="ea865-307">[Smart Detection](app-insights-proactive-diagnostics.md) automatically discovers performance anomalies.</span></span>
