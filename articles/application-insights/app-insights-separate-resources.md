---
title: Separating telemetry from development, test, and release in Azure Application Insights | Microsoft Docs
description: Direct telemetry to different resources for development, test, and production stamps.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/15/2017
ms.author: mbullwin
ms.openlocfilehash: 88626c3a4bfd4a1ff3a2e9cbc8c3f2b1c5553295
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825292"
---
# <a name="separating-telemetry-from-development-test-and-production"></a><span data-ttu-id="1fcc9-103">Separating telemetry from Development, Test, and Production</span><span class="sxs-lookup"><span data-stu-id="1fcc9-103">Separating telemetry from Development, Test, and Production</span></span>

<span data-ttu-id="1fcc9-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-104">When you are developing the next version of a web application, you don't want to mix up the [Application Insights](app-insights-overview.md) telemetry from the new version and the already released version.</span></span> <span data-ttu-id="1fcc9-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-105">To avoid confusion, send the telemetry from different development stages to separate Application Insights resources, with separate instrumentation keys (ikeys).</span></span> <span data-ttu-id="1fcc9-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-106">To make it easier to change the instrumentation key as a version moves from one stage to another, it can be useful to set the ikey in code instead of in the configuration file.</span></span> 

<span data-ttu-id="1fcc9-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="1fcc9-107">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

## <a name="about-resources-and-instrumentation-keys"></a><span data-ttu-id="1fcc9-108">About resources and instrumentation keys</span><span class="sxs-lookup"><span data-stu-id="1fcc9-108">About resources and instrumentation keys</span></span>

<span data-ttu-id="1fcc9-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-109">When you set up Application Insights monitoring for your web app, you create an Application Insights *resource* in Microsoft Azure.</span></span> <span data-ttu-id="1fcc9-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-110">You open this resource in the Azure portal in order to see and analyze the telemetry collected from your app.</span></span> <span data-ttu-id="1fcc9-111">The resource is identified by an *instrumentation key* (ikey).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-111">The resource is identified by an *instrumentation key* (ikey).</span></span> <span data-ttu-id="1fcc9-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-112">When you install the Application Insights package to monitor your app, you configure it with the instrumentation key, so that it knows where to send the telemetry.</span></span>

<span data-ttu-id="1fcc9-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-113">You typically choose to use separate resources or a single shared resource in different scenarios:</span></span>

* <span data-ttu-id="1fcc9-114">Different, independent applications - Use a separate resource and ikey for each app.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-114">Different, independent applications - Use a separate resource and ikey for each app.</span></span>
* <span data-ttu-id="1fcc9-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-115">Multiple components or roles of one business application - Use a [single shared resource](app-insights-monitor-multi-role-apps.md) for all the component apps.</span></span> <span data-ttu-id="1fcc9-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-116">Telemetry can be filtered or segmented by the cloud_RoleName property.</span></span>
* <span data-ttu-id="1fcc9-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-117">Development, Test, and Release - Use a separate resource and ikey for versions of the system in 'stamp' or stage of production.</span></span>
* <span data-ttu-id="1fcc9-118">A | B testing - Use a single resource.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-118">A | B testing - Use a single resource.</span></span> <span data-ttu-id="1fcc9-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-119">Create a TelemetryInitializer to add a property to the telemetry that identifies the variants.</span></span>


## <a name="dynamic-ikey"></a> <span data-ttu-id="1fcc9-120">Dynamic instrumentation key</span><span class="sxs-lookup"><span data-stu-id="1fcc9-120">Dynamic instrumentation key</span></span>

<span data-ttu-id="1fcc9-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-121">To make it easier to change the ikey as the code moves between stages of production, set it in code instead of in the configuration file.</span></span>

<span data-ttu-id="1fcc9-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-122">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="1fcc9-123">*C#*</span><span class="sxs-lookup"><span data-stu-id="1fcc9-123">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="1fcc9-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-124">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="1fcc9-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-125">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="1fcc9-126">Web pages</span><span class="sxs-lookup"><span data-stu-id="1fcc9-126">Web pages</span></span>
<span data-ttu-id="1fcc9-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-127">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="1fcc9-128">Instead of coding it literally into the script, generate it from the server state.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-128">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="1fcc9-129">For example, in an ASP.NET app:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-129">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="1fcc9-130">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="1fcc9-130">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a><span data-ttu-id="1fcc9-131">Create additional Application Insights resources</span><span class="sxs-lookup"><span data-stu-id="1fcc9-131">Create additional Application Insights resources</span></span>
<span data-ttu-id="1fcc9-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-132">To separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="1fcc9-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-133">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Click New, Application Insights](./media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="1fcc9-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-135">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="1fcc9-136">If you don't see your type of app, choose one of the web types for web pages.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-136">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="1fcc9-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-137">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="1fcc9-138">You could use separate resource groups for development, test, and production.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-138">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="1fcc9-139">**Subscription** is your payment account in Azure.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-139">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="1fcc9-140">**Location** is where we keep your data.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-140">**Location** is where we keep your data.</span></span> <span data-ttu-id="1fcc9-141">Currently it can't be changed.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-141">Currently it can't be changed.</span></span> 
* <span data-ttu-id="1fcc9-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-142">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="1fcc9-143">Creating the resource takes a few seconds.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-143">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="1fcc9-144">You'll see an alert when it's done.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-144">You'll see an alert when it's done.</span></span>

<span data-ttu-id="1fcc9-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span><span class="sxs-lookup"><span data-stu-id="1fcc9-145">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

### <a name="getting-the-instrumentation-key"></a><span data-ttu-id="1fcc9-146">Getting the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="1fcc9-146">Getting the instrumentation key</span></span>
<span data-ttu-id="1fcc9-147">The instrumentation key identifies the resource that you created.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-147">The instrumentation key identifies the resource that you created.</span></span> 

![Click Essentials, click the Instrumentation Key, CTRL+C](./media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="1fcc9-149">You need the instrumentation keys of all the resources to which your app will send data.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-149">You need the instrumentation keys of all the resources to which your app will send data.</span></span>

## <a name="filter-on-build-number"></a><span data-ttu-id="1fcc9-150">Filter on build number</span><span class="sxs-lookup"><span data-stu-id="1fcc9-150">Filter on build number</span></span>
<span data-ttu-id="1fcc9-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-151">When you publish a new version of your app, you'll want to be able to separate the telemetry from different builds.</span></span>

<span data-ttu-id="1fcc9-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-152">You can set the Application Version property so that you can filter [search](app-insights-diagnostic-search.md) and [metric explorer](app-insights-metrics-explorer.md) results.</span></span>

![Filtering on a property](./media/app-insights-separate-resources/050-filter.png)

<span data-ttu-id="1fcc9-154">There are several different methods of setting the Application Version property.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-154">There are several different methods of setting the Application Version property.</span></span>

* <span data-ttu-id="1fcc9-155">Set directly:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-155">Set directly:</span></span>

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* <span data-ttu-id="1fcc9-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-156">Wrap that line in a [telemetry initializer](app-insights-api-custom-events-metrics.md#defaults) to ensure that all TelemetryClient instances are set consistently.</span></span>
* <span data-ttu-id="1fcc9-157">[ASP.NET] Set the version in `BuildInfo.config`.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-157">[ASP.NET] Set the version in `BuildInfo.config`.</span></span> <span data-ttu-id="1fcc9-158">The web module will pick up the version from the BuildLabel node.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-158">The web module will pick up the version from the BuildLabel node.</span></span> <span data-ttu-id="1fcc9-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-159">Include this file in your project and remember to set the Copy Always property in Solution Explorer.</span></span>

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* <span data-ttu-id="1fcc9-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-160">[ASP.NET] Generate BuildInfo.config automatically in MSBuild.</span></span> <span data-ttu-id="1fcc9-161">To do this, add a few lines to your `.csproj` file:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-161">To do this, add a few lines to your `.csproj` file:</span></span>

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    <span data-ttu-id="1fcc9-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-162">This generates a file called *yourProjectName*.BuildInfo.config. The Publish process renames it to BuildInfo.config.</span></span>

    <span data-ttu-id="1fcc9-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-163">The build label contains a placeholder (AutoGen_...) when you build with Visual Studio.</span></span> <span data-ttu-id="1fcc9-164">But when built with MSBuild, it is populated with the correct version number.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-164">But when built with MSBuild, it is populated with the correct version number.</span></span>

    <span data-ttu-id="1fcc9-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span><span class="sxs-lookup"><span data-stu-id="1fcc9-165">To allow MSBuild to generate version numbers, set the version like `1.0.*` in AssemblyReference.cs</span></span>

## <a name="version-and-release-tracking"></a><span data-ttu-id="1fcc9-166">Version and release tracking</span><span class="sxs-lookup"><span data-stu-id="1fcc9-166">Version and release tracking</span></span>
<span data-ttu-id="1fcc9-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-167">To track the application version, make sure `buildinfo.config` is generated by your Microsoft Build Engine process.</span></span> <span data-ttu-id="1fcc9-168">In your .csproj file, add:</span><span class="sxs-lookup"><span data-stu-id="1fcc9-168">In your .csproj file, add:</span></span>  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

<span data-ttu-id="1fcc9-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-169">When it has the build info, the Application Insights web module automatically adds **Application version** as a property to every item of telemetry.</span></span> <span data-ttu-id="1fcc9-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="1fcc9-170">That allows you to filter by version when you perform [diagnostic searches](app-insights-diagnostic-search.md), or when you [explore metrics](app-insights-metrics-explorer.md).</span></span>

<span data-ttu-id="1fcc9-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-171">However, notice that the build version number is generated only by the Microsoft Build Engine, not by the developer build in Visual Studio.</span></span>

### <a name="release-annotations"></a><span data-ttu-id="1fcc9-172">Release annotations</span><span class="sxs-lookup"><span data-stu-id="1fcc9-172">Release annotations</span></span>
<span data-ttu-id="1fcc9-173">If you use Azure DevOps, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-173">If you use Azure DevOps, you can [get an annotation marker](app-insights-annotations.md) added to your charts whenever you release a new version.</span></span> <span data-ttu-id="1fcc9-174">The following image shows how this marker appears.</span><span class="sxs-lookup"><span data-stu-id="1fcc9-174">The following image shows how this marker appears.</span></span>

![Screenshot of sample release annotation on a chart](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a><span data-ttu-id="1fcc9-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="1fcc9-176">Next steps</span></span>

* [<span data-ttu-id="1fcc9-177">Shared resources for multiple roles</span><span class="sxs-lookup"><span data-stu-id="1fcc9-177">Shared resources for multiple roles</span></span>](app-insights-monitor-multi-role-apps.md)
* [<span data-ttu-id="1fcc9-178">Create a Telemetry Initializer to distinguish A|B variants</span><span class="sxs-lookup"><span data-stu-id="1fcc9-178">Create a Telemetry Initializer to distinguish A|B variants</span></span>](app-insights-api-filtering-sampling.md#add-properties)
