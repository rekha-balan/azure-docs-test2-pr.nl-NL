---
title: Explore Java trace logs in Azure Application Insights | Microsoft Docs
description: Search Log4J or Logback traces in Application Insights
services: application-insights
documentationcenter: java
author: alancameronwills
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: awills
ms.openlocfilehash: 9eb836b6b49030e41a68e45ac4d69b2a1702b74e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563089"
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="dd799-103">Explore Java trace logs in Application Insights</span><span class="sxs-lookup"><span data-stu-id="dd799-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="dd799-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span><span class="sxs-lookup"><span data-stu-id="dd799-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically to Application Insights where you can explore and search on them.</span></span>

## <a name="install-the-java-sdk"></a><span data-ttu-id="dd799-105">Install the Java SDK</span><span class="sxs-lookup"><span data-stu-id="dd799-105">Install the Java SDK</span></span>

<span data-ttu-id="dd799-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span><span class="sxs-lookup"><span data-stu-id="dd799-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="dd799-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span><span class="sxs-lookup"><span data-stu-id="dd799-107">(If you don't want to track HTTP requests, you can omit most of the .xml configuration file, but you must at least include the `InstrumentationKey` element.</span></span> <span data-ttu-id="dd799-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span><span class="sxs-lookup"><span data-stu-id="dd799-108">You should also call `new TelemetryClient()` to initialize the SDK.)</span></span>


## <a name="add-logging-libraries-to-your-project"></a><span data-ttu-id="dd799-109">Add logging libraries to your project</span><span class="sxs-lookup"><span data-stu-id="dd799-109">Add logging libraries to your project</span></span>
<span data-ttu-id="dd799-110">*Choose the appropriate way for your project.*</span><span class="sxs-lookup"><span data-stu-id="dd799-110">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="dd799-111">If you're using Maven...</span><span class="sxs-lookup"><span data-stu-id="dd799-111">If you're using Maven...</span></span>
<span data-ttu-id="dd799-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span><span class="sxs-lookup"><span data-stu-id="dd799-112">If your project is already set up to use Maven for build, merge one of the following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="dd799-113">Then refresh the project dependencies, to get the binaries downloaded.</span><span class="sxs-lookup"><span data-stu-id="dd799-113">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="dd799-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="dd799-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="dd799-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="dd799-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="dd799-116">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="dd799-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="dd799-117">If you're using Gradle...</span><span class="sxs-lookup"><span data-stu-id="dd799-117">If you're using Gradle...</span></span>
<span data-ttu-id="dd799-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span><span class="sxs-lookup"><span data-stu-id="dd799-118">If your project is already set up to use Gradle for build, add one of the following lines to the `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="dd799-119">Then refresh the project dependencies, to get the binaries downloaded.</span><span class="sxs-lookup"><span data-stu-id="dd799-119">Then refresh the project dependencies, to get the binaries downloaded.</span></span>

<span data-ttu-id="dd799-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="dd799-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="dd799-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="dd799-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="dd799-122">**Log4J v1.2**</span><span class="sxs-lookup"><span data-stu-id="dd799-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="dd799-123">Otherwise ...</span><span class="sxs-lookup"><span data-stu-id="dd799-123">Otherwise ...</span></span>
<span data-ttu-id="dd799-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span><span class="sxs-lookup"><span data-stu-id="dd799-124">Download and extract the appropriate appender, then add the appropriate library to your project:</span></span>

| <span data-ttu-id="dd799-125">Logger</span><span class="sxs-lookup"><span data-stu-id="dd799-125">Logger</span></span> | <span data-ttu-id="dd799-126">Download</span><span class="sxs-lookup"><span data-stu-id="dd799-126">Download</span></span> | <span data-ttu-id="dd799-127">Library</span><span class="sxs-lookup"><span data-stu-id="dd799-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd799-128">Logback</span><span class="sxs-lookup"><span data-stu-id="dd799-128">Logback</span></span> |[<span data-ttu-id="dd799-129">SDK with Logback appender</span><span class="sxs-lookup"><span data-stu-id="dd799-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="dd799-130">applicationinsights-logging-logback</span><span class="sxs-lookup"><span data-stu-id="dd799-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="dd799-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="dd799-131">Log4J v2.0</span></span> |[<span data-ttu-id="dd799-132">SDK with Log4J v2 appender</span><span class="sxs-lookup"><span data-stu-id="dd799-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="dd799-133">applicationinsights-logging-log4j2</span><span class="sxs-lookup"><span data-stu-id="dd799-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="dd799-134">Log4j v1.2</span><span class="sxs-lookup"><span data-stu-id="dd799-134">Log4j v1.2</span></span> |[<span data-ttu-id="dd799-135">SDK with Log4J v1.2 appender</span><span class="sxs-lookup"><span data-stu-id="dd799-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="dd799-136">applicationinsights-logging-log4j1_2</span><span class="sxs-lookup"><span data-stu-id="dd799-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-the-appender-to-your-logging-framework"></a><span data-ttu-id="dd799-137">Add the appender to your logging framework</span><span class="sxs-lookup"><span data-stu-id="dd799-137">Add the appender to your logging framework</span></span>
<span data-ttu-id="dd799-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span><span class="sxs-lookup"><span data-stu-id="dd799-138">To start getting traces, merge the relevant snippet of code to the Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="dd799-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="dd799-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="dd799-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="dd799-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="dd799-141">*Log4J v1.2*</span><span class="sxs-lookup"><span data-stu-id="dd799-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="dd799-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span><span class="sxs-lookup"><span data-stu-id="dd799-142">The Application Insights appenders can be referenced by any configured logger, and not necessarily by the root logger (as shown in the code samples above).</span></span>

## <a name="explore-your-traces-in-the-application-insights-portal"></a><span data-ttu-id="dd799-143">Explore your traces in the Application Insights portal</span><span class="sxs-lookup"><span data-stu-id="dd799-143">Explore your traces in the Application Insights portal</span></span>
<span data-ttu-id="dd799-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span><span class="sxs-lookup"><span data-stu-id="dd799-144">Now that you've configured your project to send traces to Application Insights, you can view and search these traces in the Application Insights portal, in the [Search][diagnostic] blade.</span></span>

![In the Application Insights portal, open Search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-insights/media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="dd799-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="dd799-146">Next steps</span></span>
<span data-ttu-id="dd799-147">[Diagnostic search][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="dd799-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md



