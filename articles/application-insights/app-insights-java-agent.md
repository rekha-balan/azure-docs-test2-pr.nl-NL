---
title: Performance monitoring for Java web apps in Azure Application Insights | Microsoft Docs
description: Extended performance and usage monitoring of your Java website with Application Insights.
services: application-insights
documentationcenter: java
author: harelbr
manager: douge
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: awills
ms.openlocfilehash: ad15cb60e8ffb9de9f038d8cc08d3c84e1b6bc73
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563087"
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="0e6ff-103">Monitor dependencies, exceptions and execution times in Java web apps</span><span class="sxs-lookup"><span data-stu-id="0e6ff-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="0e6ff-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span><span class="sxs-lookup"><span data-stu-id="0e6ff-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="0e6ff-105">**Dependencies:** Data about calls that your application makes to other components, including:</span><span class="sxs-lookup"><span data-stu-id="0e6ff-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="0e6ff-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span><span class="sxs-lookup"><span data-stu-id="0e6ff-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="0e6ff-107">**Redis** calls made via the Jedis client.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="0e6ff-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="0e6ff-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="0e6ff-110">"executeBatch" calls are supported.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="0e6ff-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="0e6ff-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="0e6ff-113">**Method execution time:** Data about the time it takes to execute specific methods.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="0e6ff-114">To use the Java agent, you install it on your server.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="0e6ff-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span><span class="sxs-lookup"><span data-stu-id="0e6ff-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="0e6ff-116">Install the Application Insights agent for Java</span><span class="sxs-lookup"><span data-stu-id="0e6ff-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="0e6ff-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="0e6ff-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="0e6ff-118">Edit the application server startup script, and add the following JVM:</span><span class="sxs-lookup"><span data-stu-id="0e6ff-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="0e6ff-119">`javaagent:`*full path to the agent JAR file*</span><span class="sxs-lookup"><span data-stu-id="0e6ff-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="0e6ff-120">For example, in Tomcat on a Linux machine:</span><span class="sxs-lookup"><span data-stu-id="0e6ff-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="0e6ff-121">Restart your application server.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="0e6ff-122">Configure the agent</span><span class="sxs-lookup"><span data-stu-id="0e6ff-122">Configure the agent</span></span>
<span data-ttu-id="0e6ff-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="0e6ff-124">Set the content of the xml file.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-124">Set the content of the xml file.</span></span> <span data-ttu-id="0e6ff-125">Edit the following example to include or omit the features you want.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-125">Edit the following example to include or omit the features you want.</span></span>

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

<span data-ttu-id="0e6ff-126">You have to enable reports exception and method timing for individual methods.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="0e6ff-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span><span class="sxs-lookup"><span data-stu-id="0e6ff-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="0e6ff-128">View the data</span><span class="sxs-lookup"><span data-stu-id="0e6ff-128">View the data</span></span>
<span data-ttu-id="0e6ff-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span><span class="sxs-lookup"><span data-stu-id="0e6ff-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="0e6ff-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="0e6ff-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="0e6ff-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="0e6ff-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="0e6ff-132">Questions?</span><span class="sxs-lookup"><span data-stu-id="0e6ff-132">Questions?</span></span> <span data-ttu-id="0e6ff-133">Problems?</span><span class="sxs-lookup"><span data-stu-id="0e6ff-133">Problems?</span></span>
* <span data-ttu-id="0e6ff-134">No data?</span><span class="sxs-lookup"><span data-stu-id="0e6ff-134">No data?</span></span> [<span data-ttu-id="0e6ff-135">Set firewall exceptions</span><span class="sxs-lookup"><span data-stu-id="0e6ff-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="0e6ff-136">Troubleshooting Java</span><span class="sxs-lookup"><span data-stu-id="0e6ff-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
