---
title: Performance monitoring for Java web apps in Azure Application Insights | Microsoft Docs
description: Extended performance and usage monitoring of your Java website with Application Insights.
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 08/24/2016
ms.author: mbullwin
ms.openlocfilehash: 30983e283f47761d103829f02b02bc281bd785ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797763"
---
# <a name="monitor-dependencies-caught-exceptions-and-method-execution-times-in-java-web-apps"></a><span data-ttu-id="797a1-103">Monitor dependencies, caught exceptions and method execution times in Java web apps</span><span class="sxs-lookup"><span data-stu-id="797a1-103">Monitor dependencies, caught exceptions and method execution times in Java web apps</span></span>


<span data-ttu-id="797a1-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span><span class="sxs-lookup"><span data-stu-id="797a1-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="797a1-105">**Dependencies:** Data about calls that your application makes to other components, including:</span><span class="sxs-lookup"><span data-stu-id="797a1-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="797a1-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring) are captured.</span><span class="sxs-lookup"><span data-stu-id="797a1-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring) are captured.</span></span>
  * <span data-ttu-id="797a1-107">**Redis** calls made via the Jedis client are captured.</span><span class="sxs-lookup"><span data-stu-id="797a1-107">**Redis** calls made via the Jedis client are captured.</span></span>
  * <span data-ttu-id="797a1-108">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server and Oracle DB commands are automatically captured.</span><span class="sxs-lookup"><span data-stu-id="797a1-108">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server and Oracle DB commands are automatically captured.</span></span> <span data-ttu-id="797a1-109">For MySQL, if the call takes longer than 10s, the agent reports the query plan.</span><span class="sxs-lookup"><span data-stu-id="797a1-109">For MySQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="797a1-110">**Caught exceptions:** Information about exceptions that are handled by your code.</span><span class="sxs-lookup"><span data-stu-id="797a1-110">**Caught exceptions:** Information about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="797a1-111">**Method execution time:** Information about the time it takes to execute specific methods.</span><span class="sxs-lookup"><span data-stu-id="797a1-111">**Method execution time:** Information about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="797a1-112">To use the Java agent, you install it on your server.</span><span class="sxs-lookup"><span data-stu-id="797a1-112">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="797a1-113">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span><span class="sxs-lookup"><span data-stu-id="797a1-113">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="797a1-114">Install the Application Insights agent for Java</span><span class="sxs-lookup"><span data-stu-id="797a1-114">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="797a1-115">On the machine running your Java server, [download the agent](https://github.com/Microsoft/ApplicationInsights-Java/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="797a1-115">On the machine running your Java server, [download the agent](https://github.com/Microsoft/ApplicationInsights-Java/releases/latest).</span></span> <span data-ttu-id="797a1-116">Please ensure to download the same verson of Java Agent as Application Insights Java SDK core and web packages.</span><span class="sxs-lookup"><span data-stu-id="797a1-116">Please ensure to download the same verson of Java Agent as Application Insights Java SDK core and web packages.</span></span>
2. <span data-ttu-id="797a1-117">Edit the application server startup script, and add the following JVM:</span><span class="sxs-lookup"><span data-stu-id="797a1-117">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="797a1-118">`javaagent:`*full path to the agent JAR file*</span><span class="sxs-lookup"><span data-stu-id="797a1-118">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="797a1-119">For example, in Tomcat on a Linux machine:</span><span class="sxs-lookup"><span data-stu-id="797a1-119">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="797a1-120">Restart your application server.</span><span class="sxs-lookup"><span data-stu-id="797a1-120">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="797a1-121">Configure the agent</span><span class="sxs-lookup"><span data-stu-id="797a1-121">Configure the agent</span></span>
<span data-ttu-id="797a1-122">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span><span class="sxs-lookup"><span data-stu-id="797a1-122">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="797a1-123">Set the content of the xml file.</span><span class="sxs-lookup"><span data-stu-id="797a1-123">Set the content of the xml file.</span></span> <span data-ttu-id="797a1-124">Edit the following example to include or omit the features you want.</span><span class="sxs-lookup"><span data-stu-id="797a1-124">Edit the following example to include or omit the features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="797a1-125">You have to enable reports exception and method timing for individual methods.</span><span class="sxs-lookup"><span data-stu-id="797a1-125">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="797a1-126">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span><span class="sxs-lookup"><span data-stu-id="797a1-126">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="797a1-127">View the data</span><span class="sxs-lookup"><span data-stu-id="797a1-127">View the data</span></span>
<span data-ttu-id="797a1-128">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span><span class="sxs-lookup"><span data-stu-id="797a1-128">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="797a1-129">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="797a1-129">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="797a1-130">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="797a1-130">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="797a1-131">Questions?</span><span class="sxs-lookup"><span data-stu-id="797a1-131">Questions?</span></span> <span data-ttu-id="797a1-132">Problems?</span><span class="sxs-lookup"><span data-stu-id="797a1-132">Problems?</span></span>
* <span data-ttu-id="797a1-133">No data?</span><span class="sxs-lookup"><span data-stu-id="797a1-133">No data?</span></span> [<span data-ttu-id="797a1-134">Set firewall exceptions</span><span class="sxs-lookup"><span data-stu-id="797a1-134">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="797a1-135">Troubleshooting Java</span><span class="sxs-lookup"><span data-stu-id="797a1-135">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
