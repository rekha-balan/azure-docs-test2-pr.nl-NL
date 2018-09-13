---
title: Java web app analytics with Azure Application Insights | Microsoft Docs
description: 'Application Performance Monitoring for Java web apps with Application Insights. '
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: awills
ms.openlocfilehash: cefddc8aaf2d468d5a83fd457ae83801a6133eca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550381"
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="9d160-103">Get started with Application Insights in a Java web project</span><span class="sxs-lookup"><span data-stu-id="9d160-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="9d160-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span><span class="sxs-lookup"><span data-stu-id="9d160-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="9d160-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span><span class="sxs-lookup"><span data-stu-id="9d160-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="9d160-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span><span class="sxs-lookup"><span data-stu-id="9d160-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="9d160-108">You need:</span><span class="sxs-lookup"><span data-stu-id="9d160-108">You need:</span></span>

* <span data-ttu-id="9d160-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span><span class="sxs-lookup"><span data-stu-id="9d160-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="9d160-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="9d160-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="9d160-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span><span class="sxs-lookup"><span data-stu-id="9d160-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="9d160-112">1. Get an Application Insights instrumentation key</span><span class="sxs-lookup"><span data-stu-id="9d160-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="9d160-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d160-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9d160-114">Create an Application Insights resource.</span><span class="sxs-lookup"><span data-stu-id="9d160-114">Create an Application Insights resource.</span></span> <span data-ttu-id="9d160-115">Set the application type to Java web application.</span><span class="sxs-lookup"><span data-stu-id="9d160-115">Set the application type to Java web application.</span></span>

    ![Fill a name, choose Java web app, and click Create](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="9d160-117">Find the instrumentation key of the new resource.</span><span class="sxs-lookup"><span data-stu-id="9d160-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="9d160-118">You'll need to paste this key into your code project shortly.</span><span class="sxs-lookup"><span data-stu-id="9d160-118">You'll need to paste this key into your code project shortly.</span></span>

    ![In the new resource overview, click Properties and copy the Instrumentation Key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="9d160-120">2. Add the Application Insights SDK for Java to your project</span><span class="sxs-lookup"><span data-stu-id="9d160-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="9d160-121">*Choose the appropriate way for your project.*</span><span class="sxs-lookup"><span data-stu-id="9d160-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="9d160-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span><span class="sxs-lookup"><span data-stu-id="9d160-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="9d160-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span><span class="sxs-lookup"><span data-stu-id="9d160-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="9d160-124">If you're using Maven...</span><span class="sxs-lookup"><span data-stu-id="9d160-124">If you're using Maven...</span></span>
<span data-ttu-id="9d160-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="9d160-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="9d160-126">Then, refresh the project dependencies to get the binaries downloaded.</span><span class="sxs-lookup"><span data-stu-id="9d160-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="9d160-127">*Build or checksum validation errors?*</span><span class="sxs-lookup"><span data-stu-id="9d160-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="9d160-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span><span class="sxs-lookup"><span data-stu-id="9d160-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="9d160-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="9d160-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="9d160-130">*Need to update to a new SDK?*</span><span class="sxs-lookup"><span data-stu-id="9d160-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="9d160-131">Refresh your project's dependencies.</span><span class="sxs-lookup"><span data-stu-id="9d160-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="9d160-132">If you're using Gradle...</span><span class="sxs-lookup"><span data-stu-id="9d160-132">If you're using Gradle...</span></span>
<span data-ttu-id="9d160-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span><span class="sxs-lookup"><span data-stu-id="9d160-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="9d160-134">Then refresh the project dependencies to get the binaries downloaded.</span><span class="sxs-lookup"><span data-stu-id="9d160-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="9d160-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span><span class="sxs-lookup"><span data-stu-id="9d160-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="9d160-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="9d160-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="9d160-137">*To update to a new SDK*</span><span class="sxs-lookup"><span data-stu-id="9d160-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="9d160-138">Refresh your project's dependencies.</span><span class="sxs-lookup"><span data-stu-id="9d160-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="9d160-139">Otherwise ...</span><span class="sxs-lookup"><span data-stu-id="9d160-139">Otherwise ...</span></span>
<span data-ttu-id="9d160-140">Manually add the SDK:</span><span class="sxs-lookup"><span data-stu-id="9d160-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="9d160-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="9d160-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="9d160-142">Extract the binaries from the zip file and add them to your project.</span><span class="sxs-lookup"><span data-stu-id="9d160-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="9d160-143">Questions...</span><span class="sxs-lookup"><span data-stu-id="9d160-143">Questions...</span></span>
* <span data-ttu-id="9d160-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span><span class="sxs-lookup"><span data-stu-id="9d160-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="9d160-145">`applicationinsights-core` gives you the bare API.</span><span class="sxs-lookup"><span data-stu-id="9d160-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="9d160-146">You always need this component.</span><span class="sxs-lookup"><span data-stu-id="9d160-146">You always need this component.</span></span>
  * <span data-ttu-id="9d160-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span><span class="sxs-lookup"><span data-stu-id="9d160-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="9d160-148">You can omit this component if you don't want this telemetry automatically collected.</span><span class="sxs-lookup"><span data-stu-id="9d160-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="9d160-149">For example, if you want to write your own.</span><span class="sxs-lookup"><span data-stu-id="9d160-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="9d160-150">*To update the SDK when we publish changes*</span><span class="sxs-lookup"><span data-stu-id="9d160-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="9d160-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span><span class="sxs-lookup"><span data-stu-id="9d160-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="9d160-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="9d160-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="9d160-153">3. Add an Application Insights .xml file</span><span class="sxs-lookup"><span data-stu-id="9d160-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="9d160-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span><span class="sxs-lookup"><span data-stu-id="9d160-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="9d160-155">Copy the following XML into it.</span><span class="sxs-lookup"><span data-stu-id="9d160-155">Copy the following XML into it.</span></span>

<span data-ttu-id="9d160-156">Substitute the instrumentation key that you got from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9d160-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```


* <span data-ttu-id="9d160-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span><span class="sxs-lookup"><span data-stu-id="9d160-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="9d160-158">The HTTP Request component is optional.</span><span class="sxs-lookup"><span data-stu-id="9d160-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="9d160-159">It automatically sends telemetry about requests and response times to the portal.</span><span class="sxs-lookup"><span data-stu-id="9d160-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="9d160-160">Events correlation is an addition to the HTTP request component.</span><span class="sxs-lookup"><span data-stu-id="9d160-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="9d160-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span><span class="sxs-lookup"><span data-stu-id="9d160-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="9d160-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="9d160-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="9d160-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span><span class="sxs-lookup"><span data-stu-id="9d160-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="9d160-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span><span class="sxs-lookup"><span data-stu-id="9d160-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="9d160-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span><span class="sxs-lookup"><span data-stu-id="9d160-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="9d160-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span><span class="sxs-lookup"><span data-stu-id="9d160-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="9d160-167">Alternative ways to set the instrumentation key</span><span class="sxs-lookup"><span data-stu-id="9d160-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="9d160-168">Application Insights SDK looks for the key in this order:</span><span class="sxs-lookup"><span data-stu-id="9d160-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="9d160-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="9d160-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="9d160-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="9d160-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="9d160-171">Configuration file: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="9d160-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="9d160-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="9d160-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="9d160-173">4. Add an HTTP filter</span><span class="sxs-lookup"><span data-stu-id="9d160-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="9d160-174">The last configuration step allows the HTTP request component to log each web request.</span><span class="sxs-lookup"><span data-stu-id="9d160-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="9d160-175">(Not required if you just want the bare API.)</span><span class="sxs-lookup"><span data-stu-id="9d160-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="9d160-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span><span class="sxs-lookup"><span data-stu-id="9d160-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="9d160-177">To get the most accurate results, the filter should be mapped before all other filters.</span><span class="sxs-lookup"><span data-stu-id="9d160-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="9d160-178">If you're using Spring Web MVC 3.1 or later</span><span class="sxs-lookup"><span data-stu-id="9d160-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="9d160-179">Edit these elements in \*-servlet.xml to include the Application Insights package:</span><span class="sxs-lookup"><span data-stu-id="9d160-179">Edit these elements in \*-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="9d160-180">If you're using Struts 2</span><span class="sxs-lookup"><span data-stu-id="9d160-180">If you're using Struts 2</span></span>
<span data-ttu-id="9d160-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span><span class="sxs-lookup"><span data-stu-id="9d160-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="9d160-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span><span class="sxs-lookup"><span data-stu-id="9d160-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="9d160-183">5. Run your application</span><span class="sxs-lookup"><span data-stu-id="9d160-183">5. Run your application</span></span>
<span data-ttu-id="9d160-184">Either run it in debug mode on your development machine, or publish to your server.</span><span class="sxs-lookup"><span data-stu-id="9d160-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="9d160-185">6. View your telemetry in Application Insights</span><span class="sxs-lookup"><span data-stu-id="9d160-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="9d160-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d160-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="9d160-187">HTTP requests data appears on the overview blade.</span><span class="sxs-lookup"><span data-stu-id="9d160-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="9d160-188">(If it isn't there, wait a few seconds and then click Refresh.)</span><span class="sxs-lookup"><span data-stu-id="9d160-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![sample data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="9d160-190">[Learn more about metrics.][metrics]</span><span class="sxs-lookup"><span data-stu-id="9d160-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="9d160-191">Click through any chart to see more detailed aggregated metrics.</span><span class="sxs-lookup"><span data-stu-id="9d160-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="9d160-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="9d160-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="9d160-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span><span class="sxs-lookup"><span data-stu-id="9d160-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="9d160-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span><span class="sxs-lookup"><span data-stu-id="9d160-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="9d160-195">Instance data</span><span class="sxs-lookup"><span data-stu-id="9d160-195">Instance data</span></span>
<span data-ttu-id="9d160-196">Click through a specific request type to see individual instances.</span><span class="sxs-lookup"><span data-stu-id="9d160-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="9d160-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span><span class="sxs-lookup"><span data-stu-id="9d160-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="9d160-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span><span class="sxs-lookup"><span data-stu-id="9d160-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="9d160-199">Analytics: Powerful query language</span><span class="sxs-lookup"><span data-stu-id="9d160-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="9d160-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span><span class="sxs-lookup"><span data-stu-id="9d160-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="9d160-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span><span class="sxs-lookup"><span data-stu-id="9d160-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Example of Analytics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="9d160-203">7. Install your app on the server</span><span class="sxs-lookup"><span data-stu-id="9d160-203">7. Install your app on the server</span></span>
<span data-ttu-id="9d160-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span><span class="sxs-lookup"><span data-stu-id="9d160-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="9d160-205">Make sure your firewall allows your application to send telemetry to these ports:</span><span class="sxs-lookup"><span data-stu-id="9d160-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="9d160-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="9d160-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="9d160-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="9d160-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="9d160-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span><span class="sxs-lookup"><span data-stu-id="9d160-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="9d160-209">On Windows servers, install:</span><span class="sxs-lookup"><span data-stu-id="9d160-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="9d160-210">Microsoft Visual C++ Redistributable</span><span class="sxs-lookup"><span data-stu-id="9d160-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="9d160-211">(This component enables performance counters.)</span><span class="sxs-lookup"><span data-stu-id="9d160-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="9d160-212">Exceptions and request failures</span><span class="sxs-lookup"><span data-stu-id="9d160-212">Exceptions and request failures</span></span>
<span data-ttu-id="9d160-213">Unhandled exceptions are automatically collected:</span><span class="sxs-lookup"><span data-stu-id="9d160-213">Unhandled exceptions are automatically collected:</span></span>

![Open Settings, Failures](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="9d160-215">To collect data on other exceptions, you have two options:</span><span class="sxs-lookup"><span data-stu-id="9d160-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="9d160-216">[Insert calls to trackException() in your code][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="9d160-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="9d160-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="9d160-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="9d160-218">You specify the methods you want to watch.</span><span class="sxs-lookup"><span data-stu-id="9d160-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="9d160-219">Monitor method calls and external dependencies</span><span class="sxs-lookup"><span data-stu-id="9d160-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="9d160-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span><span class="sxs-lookup"><span data-stu-id="9d160-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="9d160-221">Performance counters</span><span class="sxs-lookup"><span data-stu-id="9d160-221">Performance counters</span></span>
<span data-ttu-id="9d160-222">Open **Settings**, **Servers**, to see a range of performance counters.</span><span class="sxs-lookup"><span data-stu-id="9d160-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="9d160-223">Customize performance counter collection</span><span class="sxs-lookup"><span data-stu-id="9d160-223">Customize performance counter collection</span></span>
<span data-ttu-id="9d160-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span><span class="sxs-lookup"><span data-stu-id="9d160-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="9d160-225">Collect additional performance counters</span><span class="sxs-lookup"><span data-stu-id="9d160-225">Collect additional performance counters</span></span>
<span data-ttu-id="9d160-226">You can specify additional performance counters to be collected.</span><span class="sxs-lookup"><span data-stu-id="9d160-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="9d160-227">JMX counters (exposed by the Java Virtual Machine)</span><span class="sxs-lookup"><span data-stu-id="9d160-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="9d160-228">`displayName` – The name displayed in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="9d160-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="9d160-229">`objectName` – The JMX object name.</span><span class="sxs-lookup"><span data-stu-id="9d160-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="9d160-230">`attribute` – The attribute of the JMX object name to fetch</span><span class="sxs-lookup"><span data-stu-id="9d160-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="9d160-231">`type` (optional) - The type of JMX object’s attribute:</span><span class="sxs-lookup"><span data-stu-id="9d160-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="9d160-232">Default: a simple type such as int or long.</span><span class="sxs-lookup"><span data-stu-id="9d160-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="9d160-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span><span class="sxs-lookup"><span data-stu-id="9d160-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="9d160-234">`tabular`: the perf counter data is in the format of a table row</span><span class="sxs-lookup"><span data-stu-id="9d160-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="9d160-235">Windows performance counters</span><span class="sxs-lookup"><span data-stu-id="9d160-235">Windows performance counters</span></span>
<span data-ttu-id="9d160-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span><span class="sxs-lookup"><span data-stu-id="9d160-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="9d160-237">Categories can either be global, or can have numbered or named instances.</span><span class="sxs-lookup"><span data-stu-id="9d160-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="9d160-238">displayName – The name displayed in the Application Insights portal.</span><span class="sxs-lookup"><span data-stu-id="9d160-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="9d160-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span><span class="sxs-lookup"><span data-stu-id="9d160-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="9d160-240">counterName – The name of the performance counter.</span><span class="sxs-lookup"><span data-stu-id="9d160-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="9d160-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span><span class="sxs-lookup"><span data-stu-id="9d160-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="9d160-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="9d160-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="9d160-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span><span class="sxs-lookup"><span data-stu-id="9d160-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="9d160-244">Unix performance counters</span><span class="sxs-lookup"><span data-stu-id="9d160-244">Unix performance counters</span></span>
* <span data-ttu-id="9d160-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span><span class="sxs-lookup"><span data-stu-id="9d160-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="9d160-246">Get user and session data</span><span class="sxs-lookup"><span data-stu-id="9d160-246">Get user and session data</span></span>
<span data-ttu-id="9d160-247">OK, you're sending telemetry from your web server.</span><span class="sxs-lookup"><span data-stu-id="9d160-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="9d160-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span><span class="sxs-lookup"><span data-stu-id="9d160-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="9d160-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span><span class="sxs-lookup"><span data-stu-id="9d160-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="9d160-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span><span class="sxs-lookup"><span data-stu-id="9d160-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="9d160-251">Capture log traces</span><span class="sxs-lookup"><span data-stu-id="9d160-251">Capture log traces</span></span>
<span data-ttu-id="9d160-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span><span class="sxs-lookup"><span data-stu-id="9d160-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="9d160-253">You can correlate the logs with HTTP requests and other telemetry.</span><span class="sxs-lookup"><span data-stu-id="9d160-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="9d160-254">[Learn how][javalogs].</span><span class="sxs-lookup"><span data-stu-id="9d160-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="9d160-255">Send your own telemetry</span><span class="sxs-lookup"><span data-stu-id="9d160-255">Send your own telemetry</span></span>
<span data-ttu-id="9d160-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span><span class="sxs-lookup"><span data-stu-id="9d160-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="9d160-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span><span class="sxs-lookup"><span data-stu-id="9d160-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="9d160-258">[Search events and logs][diagnostic] to help diagnose problems.</span><span class="sxs-lookup"><span data-stu-id="9d160-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="9d160-259">Availability web tests</span><span class="sxs-lookup"><span data-stu-id="9d160-259">Availability web tests</span></span>
<span data-ttu-id="9d160-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span><span class="sxs-lookup"><span data-stu-id="9d160-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="9d160-261">[To set up][availability], click Web tests.</span><span class="sxs-lookup"><span data-stu-id="9d160-261">[To set up][availability], click Web tests.</span></span>

![Click Web tests, then Add Web test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="9d160-263">You'll get charts of response times, plus email notifications if your site goes down.</span><span class="sxs-lookup"><span data-stu-id="9d160-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web test example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="9d160-265">[Learn more about availability web tests.][availability]</span><span class="sxs-lookup"><span data-stu-id="9d160-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="9d160-266">Questions?</span><span class="sxs-lookup"><span data-stu-id="9d160-266">Questions?</span></span> <span data-ttu-id="9d160-267">Problems?</span><span class="sxs-lookup"><span data-stu-id="9d160-267">Problems?</span></span>
[<span data-ttu-id="9d160-268">Troubleshooting Java</span><span class="sxs-lookup"><span data-stu-id="9d160-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="9d160-269">Video</span><span class="sxs-lookup"><span data-stu-id="9d160-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="9d160-270">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d160-270">Next steps</span></span>
* [<span data-ttu-id="9d160-271">Monitor dependency calls</span><span class="sxs-lookup"><span data-stu-id="9d160-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="9d160-272">Monitor Unix performance counters</span><span class="sxs-lookup"><span data-stu-id="9d160-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="9d160-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span><span class="sxs-lookup"><span data-stu-id="9d160-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="9d160-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span><span class="sxs-lookup"><span data-stu-id="9d160-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="9d160-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span><span class="sxs-lookup"><span data-stu-id="9d160-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="9d160-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span><span class="sxs-lookup"><span data-stu-id="9d160-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="9d160-277">For more information, see the [Java Developer Center](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="9d160-277">For more information, see the [Java Developer Center](/develop/java/).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md












