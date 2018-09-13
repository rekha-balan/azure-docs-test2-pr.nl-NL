---
title: Monitor dev, test and production in Azure Application Insights | Microsoft Docs
description: Monitor the performance and usage of your application at different stages of development
services: application-insights
documentationcenter: ''
author: alancameronwills
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: 85df08df05203e67f3e6d8d31acf014e86368288
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555506"
---
# <a name="separating-application-insights-resources"></a><span data-ttu-id="8a24c-103">Separating Application Insights resources</span><span class="sxs-lookup"><span data-stu-id="8a24c-103">Separating Application Insights resources</span></span>
<span data-ttu-id="8a24c-104">Should the telemetry from different components and versions of your application be sent to different Application Insights resources, or combined into one?</span><span class="sxs-lookup"><span data-stu-id="8a24c-104">Should the telemetry from different components and versions of your application be sent to different Application Insights resources, or combined into one?</span></span> <span data-ttu-id="8a24c-105">This article looks at best practices and the necessary techniques.</span><span class="sxs-lookup"><span data-stu-id="8a24c-105">This article looks at best practices and the necessary techniques.</span></span>

<span data-ttu-id="8a24c-106">First, let's understand the question.</span><span class="sxs-lookup"><span data-stu-id="8a24c-106">First, let's understand the question.</span></span> <span data-ttu-id="8a24c-107">The data received from your application is stored and processed by Application Insights in a Microsoft Azure *resource*.</span><span class="sxs-lookup"><span data-stu-id="8a24c-107">The data received from your application is stored and processed by Application Insights in a Microsoft Azure *resource*.</span></span> <span data-ttu-id="8a24c-108">Each resource is identified by an *instrumentation key* (iKey).</span><span class="sxs-lookup"><span data-stu-id="8a24c-108">Each resource is identified by an *instrumentation key* (iKey).</span></span> <span data-ttu-id="8a24c-109">In your app, the key is provided to the Application Insights SDK so that it can send the data it collects to the right resource.</span><span class="sxs-lookup"><span data-stu-id="8a24c-109">In your app, the key is provided to the Application Insights SDK so that it can send the data it collects to the right resource.</span></span> <span data-ttu-id="8a24c-110">The key can be provided either in code or in ApplicationInsights.config. By changing the key in the SDK, you can direct data to different resources.</span><span class="sxs-lookup"><span data-stu-id="8a24c-110">The key can be provided either in code or in ApplicationInsights.config. By changing the key in the SDK, you can direct data to different resources.</span></span> 

<span data-ttu-id="8a24c-111">In a simple case, when you register an application with Application Insights, you create a new resource in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8a24c-111">In a simple case, when you register an application with Application Insights, you create a new resource in Application Insights.</span></span> <span data-ttu-id="8a24c-112">In Visual Studio, the *Configure Application Insights* or *Add Application Insights* dialog does this for you.</span><span class="sxs-lookup"><span data-stu-id="8a24c-112">In Visual Studio, the *Configure Application Insights* or *Add Application Insights* dialog does this for you.</span></span>

<span data-ttu-id="8a24c-113">If it's a high-volume website, it might be deployed on more than one server instance.</span><span class="sxs-lookup"><span data-stu-id="8a24c-113">If it's a high-volume website, it might be deployed on more than one server instance.</span></span>

<span data-ttu-id="8a24c-114">In more complex scenarios, you have a system that is made up of multiple components - for example, a web site and a back-end processor.</span><span class="sxs-lookup"><span data-stu-id="8a24c-114">In more complex scenarios, you have a system that is made up of multiple components - for example, a web site and a back-end processor.</span></span> 

## <a name="when-to-use-separate-ikeys"></a><span data-ttu-id="8a24c-115">When to use separate iKeys</span><span class="sxs-lookup"><span data-stu-id="8a24c-115">When to use separate iKeys</span></span>
<span data-ttu-id="8a24c-116">Here are some general guidelines:</span><span class="sxs-lookup"><span data-stu-id="8a24c-116">Here are some general guidelines:</span></span>

* <span data-ttu-id="8a24c-117">Where you have an independently deployable application unit that runs on a set of server instances that can be scaled up/down independently of other components, then you would usually map that to a single resource - that is, it will have a single instrumentation key (iKey).</span><span class="sxs-lookup"><span data-stu-id="8a24c-117">Where you have an independently deployable application unit that runs on a set of server instances that can be scaled up/down independently of other components, then you would usually map that to a single resource - that is, it will have a single instrumentation key (iKey).</span></span>
* <span data-ttu-id="8a24c-118">By contrast, reasons for using separate iKeys include:</span><span class="sxs-lookup"><span data-stu-id="8a24c-118">By contrast, reasons for using separate iKeys include:</span></span>
  * <span data-ttu-id="8a24c-119">Easily read separate metrics from separate components.</span><span class="sxs-lookup"><span data-stu-id="8a24c-119">Easily read separate metrics from separate components.</span></span>
  * <span data-ttu-id="8a24c-120">Keep lower-volume telemetry separate from high-volume, so that throttling, quotas, and sampling on one stream don't affect the other.</span><span class="sxs-lookup"><span data-stu-id="8a24c-120">Keep lower-volume telemetry separate from high-volume, so that throttling, quotas, and sampling on one stream don't affect the other.</span></span>
  * <span data-ttu-id="8a24c-121">Separate alerts, export, and work item configurations.</span><span class="sxs-lookup"><span data-stu-id="8a24c-121">Separate alerts, export, and work item configurations.</span></span>
  * <span data-ttu-id="8a24c-122">Spread [limits](app-insights-pricing.md#limits-summary) such as telemetry quota, throttling, and web test count.</span><span class="sxs-lookup"><span data-stu-id="8a24c-122">Spread [limits](app-insights-pricing.md#limits-summary) such as telemetry quota, throttling, and web test count.</span></span>
  * <span data-ttu-id="8a24c-123">Code under development and test should send to a separate iKey than the production stamp.</span><span class="sxs-lookup"><span data-stu-id="8a24c-123">Code under development and test should send to a separate iKey than the production stamp.</span></span>  

<span data-ttu-id="8a24c-124">A lot of Application Insights portal experiences are designed with these guidelines in mind.</span><span class="sxs-lookup"><span data-stu-id="8a24c-124">A lot of Application Insights portal experiences are designed with these guidelines in mind.</span></span> <span data-ttu-id="8a24c-125">For example, the servers view segments on server instance, making the assumption that telemetry about one logical component can come from several server instances.</span><span class="sxs-lookup"><span data-stu-id="8a24c-125">For example, the servers view segments on server instance, making the assumption that telemetry about one logical component can come from several server instances.</span></span>

## <a name="single-ikey"></a><span data-ttu-id="8a24c-126">Single iKey</span><span class="sxs-lookup"><span data-stu-id="8a24c-126">Single iKey</span></span>
<span data-ttu-id="8a24c-127">Where you send telemetry from multiple components to a single iKey:</span><span class="sxs-lookup"><span data-stu-id="8a24c-127">Where you send telemetry from multiple components to a single iKey:</span></span>

* <span data-ttu-id="8a24c-128">Add a property to all the telemetry that allows you to segment and filter on the component identity.</span><span class="sxs-lookup"><span data-stu-id="8a24c-128">Add a property to all the telemetry that allows you to segment and filter on the component identity.</span></span> <span data-ttu-id="8a24c-129">The role ID is added automatically to telemetry from server role instances, but in other cases you can use a [telemetry initializer](app-insights-api-filtering-sampling.md#add-properties) to add the property.</span><span class="sxs-lookup"><span data-stu-id="8a24c-129">The role ID is added automatically to telemetry from server role instances, but in other cases you can use a [telemetry initializer](app-insights-api-filtering-sampling.md#add-properties) to add the property.</span></span>
* <span data-ttu-id="8a24c-130">Update the Application Insights SDKs in the different components at the same time.</span><span class="sxs-lookup"><span data-stu-id="8a24c-130">Update the Application Insights SDKs in the different components at the same time.</span></span> <span data-ttu-id="8a24c-131">Telemetry for one iKey should originate with the same version of the SDK.</span><span class="sxs-lookup"><span data-stu-id="8a24c-131">Telemetry for one iKey should originate with the same version of the SDK.</span></span>

## <a name="separate-ikeys"></a><span data-ttu-id="8a24c-132">Separate iKeys</span><span class="sxs-lookup"><span data-stu-id="8a24c-132">Separate iKeys</span></span>
<span data-ttu-id="8a24c-133">Where you have multiple iKeys for different application components:</span><span class="sxs-lookup"><span data-stu-id="8a24c-133">Where you have multiple iKeys for different application components:</span></span>

* <span data-ttu-id="8a24c-134">Create a [dashboard](app-insights-dashboards.md) for a view of the key telemetry from your logical application, combined from the different application components.</span><span class="sxs-lookup"><span data-stu-id="8a24c-134">Create a [dashboard](app-insights-dashboards.md) for a view of the key telemetry from your logical application, combined from the different application components.</span></span> <span data-ttu-id="8a24c-135">Dashboards can be shared, so a single logical system view can be used by different teams.</span><span class="sxs-lookup"><span data-stu-id="8a24c-135">Dashboards can be shared, so a single logical system view can be used by different teams.</span></span>
* <span data-ttu-id="8a24c-136">Organize [resource groups](app-insights-resources-roles-access-control.md) at team level.</span><span class="sxs-lookup"><span data-stu-id="8a24c-136">Organize [resource groups](app-insights-resources-roles-access-control.md) at team level.</span></span> <span data-ttu-id="8a24c-137">Access permissions are assigned by resource group, and these include permissions to set up alerts.</span><span class="sxs-lookup"><span data-stu-id="8a24c-137">Access permissions are assigned by resource group, and these include permissions to set up alerts.</span></span> 
* <span data-ttu-id="8a24c-138">Use [Azure Resource Manager templates and Powershell](app-insights-powershell.md) to help manage artifacts such as alert rules and web tests.</span><span class="sxs-lookup"><span data-stu-id="8a24c-138">Use [Azure Resource Manager templates and Powershell](app-insights-powershell.md) to help manage artifacts such as alert rules and web tests.</span></span>

## <a name="separate-ikeys-for-devtest-and-production"></a><span data-ttu-id="8a24c-139">Separate iKeys for Dev/Test and Production</span><span class="sxs-lookup"><span data-stu-id="8a24c-139">Separate iKeys for Dev/Test and Production</span></span>
<span data-ttu-id="8a24c-140">To make it easier to change the key automatically when your app is released, set the iKey in code, instead of in ApplicationInsights.config.</span><span class="sxs-lookup"><span data-stu-id="8a24c-140">To make it easier to change the key automatically when your app is released, set the iKey in code, instead of in ApplicationInsights.config.</span></span>

<span data-ttu-id="8a24c-141">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span><span class="sxs-lookup"><span data-stu-id="8a24c-141">(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)</span></span>

### <a name="dynamic-ikey"></a> <span data-ttu-id="8a24c-142">Dynamic instrumentation key</span><span class="sxs-lookup"><span data-stu-id="8a24c-142">Dynamic instrumentation key</span></span>
<span data-ttu-id="8a24c-143">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span><span class="sxs-lookup"><span data-stu-id="8a24c-143">Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:</span></span>

<span data-ttu-id="8a24c-144">*C#*</span><span class="sxs-lookup"><span data-stu-id="8a24c-144">*C#*</span></span>

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

<span data-ttu-id="8a24c-145">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span><span class="sxs-lookup"><span data-stu-id="8a24c-145">In this example, the ikeys for the different resources are placed in different versions of the web configuration file.</span></span> <span data-ttu-id="8a24c-146">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span><span class="sxs-lookup"><span data-stu-id="8a24c-146">Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.</span></span>

### <a name="web-pages"></a><span data-ttu-id="8a24c-147">Web pages</span><span class="sxs-lookup"><span data-stu-id="8a24c-147">Web pages</span></span>
<span data-ttu-id="8a24c-148">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8a24c-148">The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md).</span></span> <span data-ttu-id="8a24c-149">Instead of coding it literally into the script, generate it from the server state.</span><span class="sxs-lookup"><span data-stu-id="8a24c-149">Instead of coding it literally into the script, generate it from the server state.</span></span> <span data-ttu-id="8a24c-150">For example, in an ASP.NET app:</span><span class="sxs-lookup"><span data-stu-id="8a24c-150">For example, in an ASP.NET app:</span></span>

<span data-ttu-id="8a24c-151">*JavaScript in Razor*</span><span class="sxs-lookup"><span data-stu-id="8a24c-151">*JavaScript in Razor*</span></span>

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="creating-an-additional-application-insights-resource"></a><span data-ttu-id="8a24c-152">Creating an additional Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="8a24c-152">Creating an additional Application Insights resource</span></span>
<span data-ttu-id="8a24c-153">If you decide to separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="8a24c-153">If you decide to separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.</span></span>

<span data-ttu-id="8a24c-154">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span><span class="sxs-lookup"><span data-stu-id="8a24c-154">In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:</span></span>

![Click New, Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-separate-resources/01-new.png)

* <span data-ttu-id="8a24c-156">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8a24c-156">**Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md).</span></span> <span data-ttu-id="8a24c-157">If you don't see your type of app, choose one of the web types for web pages.</span><span class="sxs-lookup"><span data-stu-id="8a24c-157">If you don't see your type of app, choose one of the web types for web pages.</span></span>
* <span data-ttu-id="8a24c-158">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="8a24c-158">**Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md).</span></span> <span data-ttu-id="8a24c-159">You could use separate resource groups for development, test, and production.</span><span class="sxs-lookup"><span data-stu-id="8a24c-159">You could use separate resource groups for development, test, and production.</span></span>
* <span data-ttu-id="8a24c-160">**Subscription** is your payment account in Azure.</span><span class="sxs-lookup"><span data-stu-id="8a24c-160">**Subscription** is your payment account in Azure.</span></span>
* <span data-ttu-id="8a24c-161">**Location** is where we keep your data.</span><span class="sxs-lookup"><span data-stu-id="8a24c-161">**Location** is where we keep your data.</span></span> <span data-ttu-id="8a24c-162">Currently it can't be changed.</span><span class="sxs-lookup"><span data-stu-id="8a24c-162">Currently it can't be changed.</span></span> 
* <span data-ttu-id="8a24c-163">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span><span class="sxs-lookup"><span data-stu-id="8a24c-163">**Add to dashboard** puts a quick-access tile for your resource on your Azure Home page.</span></span> 

<span data-ttu-id="8a24c-164">Creating the resource takes a few seconds.</span><span class="sxs-lookup"><span data-stu-id="8a24c-164">Creating the resource takes a few seconds.</span></span> <span data-ttu-id="8a24c-165">You'll see an alert when it's done.</span><span class="sxs-lookup"><span data-stu-id="8a24c-165">You'll see an alert when it's done.</span></span>

<span data-ttu-id="8a24c-166">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span><span class="sxs-lookup"><span data-stu-id="8a24c-166">(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)</span></span>

## <a name="getting-the-instrumentation-key"></a><span data-ttu-id="8a24c-167">Getting the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="8a24c-167">Getting the instrumentation key</span></span>
<span data-ttu-id="8a24c-168">The instrumentation key identifies the resource that you created.</span><span class="sxs-lookup"><span data-stu-id="8a24c-168">The instrumentation key identifies the resource that you created.</span></span> 

![Click Essentials, click the Instrumentation Key, CTRL+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-separate-resources/02-props.png)

<span data-ttu-id="8a24c-170">You need the instrumentation keys of all the resources to which your app will send data.</span><span class="sxs-lookup"><span data-stu-id="8a24c-170">You need the instrumentation keys of all the resources to which your app will send data.</span></span>



