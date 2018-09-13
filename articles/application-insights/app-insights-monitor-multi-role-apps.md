---
title: Azure Application Insights support for multiple components, microservices, and containers | Microsoft Docs
description: Monitoring apps that consist of multiple components or roles for performance and usage.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 05/17/2017
ms.author: mbullwin
ms.openlocfilehash: c9982cb5dbf8d281d9abe0f33a21d57a9174befd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865122"
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a><span data-ttu-id="23505-103">Monitor multi-component applications with Application Insights (preview)</span><span class="sxs-lookup"><span data-stu-id="23505-103">Monitor multi-component applications with Application Insights (preview)</span></span>

<span data-ttu-id="23505-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="23505-104">You can monitor apps that consist of multiple server components, roles, or services with [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="23505-105">The health of the components and the relationships between them are displayed on a single Application Map.</span><span class="sxs-lookup"><span data-stu-id="23505-105">The health of the components and the relationships between them are displayed on a single Application Map.</span></span> <span data-ttu-id="23505-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span><span class="sxs-lookup"><span data-stu-id="23505-106">You can trace individual operations through multiple components with automatic HTTP correlation.</span></span> <span data-ttu-id="23505-107">Container diagnostics can be integrated and correlated with application telemetry.</span><span class="sxs-lookup"><span data-stu-id="23505-107">Container diagnostics can be integrated and correlated with application telemetry.</span></span> <span data-ttu-id="23505-108">Use a single Application Insights resource for all the components of your application.</span><span class="sxs-lookup"><span data-stu-id="23505-108">Use a single Application Insights resource for all the components of your application.</span></span> 

![Multi-component application map](./media/app-insights-monitor-multi-role-apps/app-map.png)

<span data-ttu-id="23505-110">We use 'component' here to mean any functioning part of a large application.</span><span class="sxs-lookup"><span data-stu-id="23505-110">We use 'component' here to mean any functioning part of a large application.</span></span> <span data-ttu-id="23505-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span><span class="sxs-lookup"><span data-stu-id="23505-111">For example, a typical business application may consist of client code running in web browsers, talking to one or more web app services, which in turn use back end services.</span></span> <span data-ttu-id="23505-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="23505-112">Server components may be hosted on-premises on in the cloud, or may be Azure web and worker roles, or may run in containers such as Docker or Service Fabric.</span></span> 

### <a name="sharing-a-single-application-insights-resource"></a><span data-ttu-id="23505-113">Sharing a single Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="23505-113">Sharing a single Application Insights resource</span></span> 

<span data-ttu-id="23505-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span><span class="sxs-lookup"><span data-stu-id="23505-114">The key technique here is to send telemetry from every component in your application to the same Application Insights resource, but use the `cloud_RoleName` property to distinguish components when necessary.</span></span> <span data-ttu-id="23505-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span><span class="sxs-lookup"><span data-stu-id="23505-115">The Application Insights SDK adds the `cloud_RoleName` property to the telemetry components emit.</span></span> <span data-ttu-id="23505-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span><span class="sxs-lookup"><span data-stu-id="23505-116">For example, the SDK will add a web site name, or service role name to the `cloud_RoleName` property.</span></span> <span data-ttu-id="23505-117">You can override this value with a telemetryinitializer.</span><span class="sxs-lookup"><span data-stu-id="23505-117">You can override this value with a telemetryinitializer.</span></span> <span data-ttu-id="23505-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span><span class="sxs-lookup"><span data-stu-id="23505-118">The Application Map uses the `cloud_RoleName` property to identify the components on the map.</span></span>

<span data-ttu-id="23505-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span><span class="sxs-lookup"><span data-stu-id="23505-119">For more information about how do override the `cloud_RoleName` property see [Add properties: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).</span></span>  

<span data-ttu-id="23505-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span><span class="sxs-lookup"><span data-stu-id="23505-120">In some cases, this may not be appropriate, and you may prefer to use separate resources for different groups of components.</span></span> <span data-ttu-id="23505-121">For example, you might need to use different resources for management or billing purposes.</span><span class="sxs-lookup"><span data-stu-id="23505-121">For example, you might need to use different resources for management or billing purposes.</span></span> <span data-ttu-id="23505-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="23505-122">Using separate resources means that you don't see all the components displayed on a single Application Map; and that you can't query across components in [Analytics](app-insights-analytics.md).</span></span> <span data-ttu-id="23505-123">You also have to set up the separate resources.</span><span class="sxs-lookup"><span data-stu-id="23505-123">You also have to set up the separate resources.</span></span>

<span data-ttu-id="23505-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="23505-124">With that caveat, we'll assume in the rest of this document that you want to send data from multiple components to one Application Insights resource.</span></span>

## <a name="configure-multi-component-applications"></a><span data-ttu-id="23505-125">Configure multi-component applications</span><span class="sxs-lookup"><span data-stu-id="23505-125">Configure multi-component applications</span></span>

<span data-ttu-id="23505-126">To get a multi-component application map, you need to achieve these goals:</span><span class="sxs-lookup"><span data-stu-id="23505-126">To get a multi-component application map, you need to achieve these goals:</span></span>

* <span data-ttu-id="23505-127">**Install the latest pre-release** Application Insights package in each component of the application.</span><span class="sxs-lookup"><span data-stu-id="23505-127">**Install the latest pre-release** Application Insights package in each component of the application.</span></span> 
* <span data-ttu-id="23505-128">**Share a single Application Insights resource** for all the components of your application.</span><span class="sxs-lookup"><span data-stu-id="23505-128">**Share a single Application Insights resource** for all the components of your application.</span></span>
* <span data-ttu-id="23505-129">**Enable Composite Application Map** in the Previews blade.</span><span class="sxs-lookup"><span data-stu-id="23505-129">**Enable Composite Application Map** in the Previews blade.</span></span>

<span data-ttu-id="23505-130">Configure each component of your application using the appropriate method for its type.</span><span class="sxs-lookup"><span data-stu-id="23505-130">Configure each component of your application using the appropriate method for its type.</span></span> <span data-ttu-id="23505-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span><span class="sxs-lookup"><span data-stu-id="23505-131">([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)</span></span>

### <a name="1-install-the-latest-pre-release-package"></a><span data-ttu-id="23505-132">1. Install the latest pre-release package</span><span class="sxs-lookup"><span data-stu-id="23505-132">1. Install the latest pre-release package</span></span>

<span data-ttu-id="23505-133">Update or install the Application Insights packages in the project for each server component.</span><span class="sxs-lookup"><span data-stu-id="23505-133">Update or install the Application Insights packages in the project for each server component.</span></span> <span data-ttu-id="23505-134">If you're using Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="23505-134">If you're using Visual Studio:</span></span>

1. <span data-ttu-id="23505-135">Right-click a project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="23505-135">Right-click a project and select **Manage NuGet Packages**.</span></span> 
2. <span data-ttu-id="23505-136">Select **Include prerelease**.</span><span class="sxs-lookup"><span data-stu-id="23505-136">Select **Include prerelease**.</span></span>
3. <span data-ttu-id="23505-137">If Application Insights packages appear in Updates, select them.</span><span class="sxs-lookup"><span data-stu-id="23505-137">If Application Insights packages appear in Updates, select them.</span></span> 

    <span data-ttu-id="23505-138">Otherwise, browse for and install the appropriate package:</span><span class="sxs-lookup"><span data-stu-id="23505-138">Otherwise, browse for and install the appropriate package:</span></span>
    
    * <span data-ttu-id="23505-139">Microsoft.ApplicationInsights.WindowsServer</span><span class="sxs-lookup"><span data-stu-id="23505-139">Microsoft.ApplicationInsights.WindowsServer</span></span>
    * <span data-ttu-id="23505-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="23505-140">Microsoft.ApplicationInsights.ServiceFabric - for components running as guest executables and Docker containers running a in Service Fabric application</span></span>
    * <span data-ttu-id="23505-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span><span class="sxs-lookup"><span data-stu-id="23505-141">Microsoft.ApplicationInsights.ServiceFabric.Native - for reliable services in ServiceFabric applications</span></span>
    * <span data-ttu-id="23505-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span><span class="sxs-lookup"><span data-stu-id="23505-142">Microsoft.ApplicationInsights.Kubernetes for components running in Docker on Kubernetes</span></span>

### <a name="2-share-a-single-application-insights-resource"></a><span data-ttu-id="23505-143">2. Share a single Application Insights resource</span><span class="sxs-lookup"><span data-stu-id="23505-143">2. Share a single Application Insights resource</span></span>

* <span data-ttu-id="23505-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span><span class="sxs-lookup"><span data-stu-id="23505-144">In Visual Studio, right-click a project and select **Configure Application Insights**, or **Application Insights > Configure**.</span></span> <span data-ttu-id="23505-145">For the first project, use the wizard to create an Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="23505-145">For the first project, use the wizard to create an Application Insights resource.</span></span> <span data-ttu-id="23505-146">For subsequent projects, select the same resource.</span><span class="sxs-lookup"><span data-stu-id="23505-146">For subsequent projects, select the same resource.</span></span>
* <span data-ttu-id="23505-147">If there is no Application Insights menu, configure manually:</span><span class="sxs-lookup"><span data-stu-id="23505-147">If there is no Application Insights menu, configure manually:</span></span>

   1. <span data-ttu-id="23505-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span><span class="sxs-lookup"><span data-stu-id="23505-148">In [Azure portal](https://portal,azure.com), open the Application Insights resource you already created for another component.</span></span>
   2. <span data-ttu-id="23505-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span><span class="sxs-lookup"><span data-stu-id="23505-149">In the Overview blade, open the Essentials drop-down tab, and copy the **Instrumentation Key.**</span></span>
   3. <span data-ttu-id="23505-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="23505-150">In your project, open ApplicationInsights.config and insert: `<InstrumentationKey>your copied key</InstrumentationKey>`</span></span>

![Copy the instrumentation key to the .config file](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-composite-application-map"></a><span data-ttu-id="23505-152">3. Enable Composite Application Map</span><span class="sxs-lookup"><span data-stu-id="23505-152">3. Enable Composite Application Map</span></span>

<span data-ttu-id="23505-153">In the Azure portal, open the resource for your application.</span><span class="sxs-lookup"><span data-stu-id="23505-153">In the Azure portal, open the resource for your application.</span></span> <span data-ttu-id="23505-154">Under the CONFIGURE sub-heading, click Previews to open the Previews blade.</span><span class="sxs-lookup"><span data-stu-id="23505-154">Under the CONFIGURE sub-heading, click Previews to open the Previews blade.</span></span> <span data-ttu-id="23505-155">In the Previews blade, enable *Composite Application Map*.</span><span class="sxs-lookup"><span data-stu-id="23505-155">In the Previews blade, enable *Composite Application Map*.</span></span>

### <a name="4-enable-docker-metrics-optional"></a><span data-ttu-id="23505-156">4. Enable Docker metrics (Optional)</span><span class="sxs-lookup"><span data-stu-id="23505-156">4. Enable Docker metrics (Optional)</span></span> 

<span data-ttu-id="23505-157">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span><span class="sxs-lookup"><span data-stu-id="23505-157">If a component runs in a Docker hosted on an Azure Windows VM, you can collect additional metrics from the container.</span></span> <span data-ttu-id="23505-158">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span><span class="sxs-lookup"><span data-stu-id="23505-158">Insert this in your [Azure diagnostics](../monitoring-and-diagnostics/azure-diagnostics.md) configuration file:</span></span>

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-to-separate-components"></a><span data-ttu-id="23505-159">Use cloud_RoleName to separate components</span><span class="sxs-lookup"><span data-stu-id="23505-159">Use cloud_RoleName to separate components</span></span>

<span data-ttu-id="23505-160">The `cloud_RoleName` property is attached to all telemetry.</span><span class="sxs-lookup"><span data-stu-id="23505-160">The `cloud_RoleName` property is attached to all telemetry.</span></span> <span data-ttu-id="23505-161">It identifies the component - the role or service - that originates the telemetry.</span><span class="sxs-lookup"><span data-stu-id="23505-161">It identifies the component - the role or service - that originates the telemetry.</span></span> <span data-ttu-id="23505-162">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span><span class="sxs-lookup"><span data-stu-id="23505-162">(It is not the same as cloud_RoleInstance, which separates identical roles that are running in parallel on multiple server processes or machines.)</span></span>

<span data-ttu-id="23505-163">In the portal, you can filter or segment your telemetry using this property.</span><span class="sxs-lookup"><span data-stu-id="23505-163">In the portal, you can filter or segment your telemetry using this property.</span></span> <span data-ttu-id="23505-164">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span><span class="sxs-lookup"><span data-stu-id="23505-164">In this example, the Failures blade is filtered to show just information from the front-end web service, filtering out failures from the CRM API backend:</span></span>

![Metric chart segmented by Cloud Role Name](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a><span data-ttu-id="23505-166">Trace operations between components</span><span class="sxs-lookup"><span data-stu-id="23505-166">Trace operations between components</span></span>

<span data-ttu-id="23505-167">You can trace from one component to another, the calls made while processing an individual operation.</span><span class="sxs-lookup"><span data-stu-id="23505-167">You can trace from one component to another, the calls made while processing an individual operation.</span></span>


![Show telemetry for operation](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

<span data-ttu-id="23505-169">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span><span class="sxs-lookup"><span data-stu-id="23505-169">Click through to a correlated list of telemetry for this operation across the front-end web server and the back-end API:</span></span>

![Search across components](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a><span data-ttu-id="23505-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="23505-171">Next steps</span></span>

* [<span data-ttu-id="23505-172">Separate telemetry from Development, Test, and Production</span><span class="sxs-lookup"><span data-stu-id="23505-172">Separate telemetry from Development, Test, and Production</span></span>](app-insights-separate-resources.md)
