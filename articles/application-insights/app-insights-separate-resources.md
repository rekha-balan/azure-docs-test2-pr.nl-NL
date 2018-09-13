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
# <a name="separating-application-insights-resources"></a>Separating Application Insights resources
Should the telemetry from different components and versions of your application be sent to different Application Insights resources, or combined into one? This article looks at best practices and the necessary techniques.

First, let's understand the question. The data received from your application is stored and processed by Application Insights in a Microsoft Azure *resource*. Each resource is identified by an *instrumentation key* (iKey). In your app, the key is provided to the Application Insights SDK so that it can send the data it collects to the right resource. The key can be provided either in code or in ApplicationInsights.config. By changing the key in the SDK, you can direct data to different resources. 

In a simple case, when you register an application with Application Insights, you create a new resource in Application Insights. In Visual Studio, the *Configure Application Insights* or *Add Application Insights* dialog does this for you.

If it's a high-volume website, it might be deployed on more than one server instance.

In more complex scenarios, you have a system that is made up of multiple components - for example, a web site and a back-end processor. 

## <a name="when-to-use-separate-ikeys"></a>When to use separate iKeys
Here are some general guidelines:

* Where you have an independently deployable application unit that runs on a set of server instances that can be scaled up/down independently of other components, then you would usually map that to a single resource - that is, it will have a single instrumentation key (iKey).
* By contrast, reasons for using separate iKeys include:
  * Easily read separate metrics from separate components.
  * Keep lower-volume telemetry separate from high-volume, so that throttling, quotas, and sampling on one stream don't affect the other.
  * Separate alerts, export, and work item configurations.
  * Spread [limits](app-insights-pricing.md#limits-summary) such as telemetry quota, throttling, and web test count.
  * Code under development and test should send to a separate iKey than the production stamp.  

A lot of Application Insights portal experiences are designed with these guidelines in mind. For example, the servers view segments on server instance, making the assumption that telemetry about one logical component can come from several server instances.

## <a name="single-ikey"></a>Single iKey
Where you send telemetry from multiple components to a single iKey:

* Add a property to all the telemetry that allows you to segment and filter on the component identity. The role ID is added automatically to telemetry from server role instances, but in other cases you can use a [telemetry initializer](app-insights-api-filtering-sampling.md#add-properties) to add the property.
* Update the Application Insights SDKs in the different components at the same time. Telemetry for one iKey should originate with the same version of the SDK.

## <a name="separate-ikeys"></a>Separate iKeys
Where you have multiple iKeys for different application components:

* Create a [dashboard](app-insights-dashboards.md) for a view of the key telemetry from your logical application, combined from the different application components. Dashboards can be shared, so a single logical system view can be used by different teams.
* Organize [resource groups](app-insights-resources-roles-access-control.md) at team level. Access permissions are assigned by resource group, and these include permissions to set up alerts. 
* Use [Azure Resource Manager templates and Powershell](app-insights-powershell.md) to help manage artifacts such as alert rules and web tests.

## <a name="separate-ikeys-for-devtest-and-production"></a>Separate iKeys for Dev/Test and Production
To make it easier to change the key automatically when your app is released, set the iKey in code, instead of in ApplicationInsights.config.

(If your system is an Azure Cloud Service, there's [another method of setting separate ikeys](app-insights-cloudservices.md).)

### <a name="dynamic-ikey"></a> Dynamic instrumentation key
Set the key in an initialization method, such as global.aspx.cs in an ASP.NET service:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

In this example, the ikeys for the different resources are placed in different versions of the web configuration file. Swapping the web configuration file - which you can do as part of the release script - will swap the target resource.

### <a name="web-pages"></a>Web pages
The iKey is also used in your app's web pages, in the [script that you got from the quick start blade](app-insights-javascript.md). Instead of coding it literally into the script, generate it from the server state. For example, in an ASP.NET app:

*JavaScript in Razor*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="creating-an-additional-application-insights-resource"></a>Creating an additional Application Insights resource
If you decide to separate telemetry for different application components, or for different stamps (dev/test/production) of the same component, then you'll have to create a new Application Insights resource.

In the [portal.azure.com](https://portal.azure.com), add an Application Insights resource:

![Click New, Application Insights](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-separate-resources/01-new.png)

* **Application type** affects what you see on the overview blade and the properties available in [metric explorer](app-insights-metrics-explorer.md). If you don't see your type of app, choose one of the web types for web pages.
* **Resource group** is a convenience for managing properties like [access control](app-insights-resources-roles-access-control.md). You could use separate resource groups for development, test, and production.
* **Subscription** is your payment account in Azure.
* **Location** is where we keep your data. Currently it can't be changed. 
* **Add to dashboard** puts a quick-access tile for your resource on your Azure Home page. 

Creating the resource takes a few seconds. You'll see an alert when it's done.

(You can write a [PowerShell script](app-insights-powershell-script-create-resource.md) to create a resource automatically.)

## <a name="getting-the-instrumentation-key"></a>Getting the instrumentation key
The instrumentation key identifies the resource that you created. 

![Click Essentials, click the Instrumentation Key, CTRL+C](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-separate-resources/02-props.png)

You need the instrumentation keys of all the resources to which your app will send data.



