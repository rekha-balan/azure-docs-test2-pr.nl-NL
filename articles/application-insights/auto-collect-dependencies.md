---
title: Azure Application Insights - Dependency Auto-Collection | Microsoft Docs
description: Application Insights automatically collect and visualize dependencies
services: application-insights
documentationcenter: .net
author: nikmd23
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: reference
ms.date: 08/13/2018
ms.reviewer: mbullwin
ms.author: nimolnar
ms.openlocfilehash: f20963f030c9040b696f7d6a33b25bcee2dc517f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856437"
---
# <a name="dependency-auto-collection"></a><span data-ttu-id="3702f-103">Dependency auto-collection</span><span class="sxs-lookup"><span data-stu-id="3702f-103">Dependency auto-collection</span></span>

<span data-ttu-id="3702f-104">Below is the currently supported list of dependency calls that are automatically detected as dependencies without requiring any additional modification to your application's code.</span><span class="sxs-lookup"><span data-stu-id="3702f-104">Below is the currently supported list of dependency calls that are automatically detected as dependencies without requiring any additional modification to your application's code.</span></span> <span data-ttu-id="3702f-105">This consists of outgoing calls to communication libraries, storage clients, logging & metrics libraries, as well as incoming calls into application frameworks and servers.</span><span class="sxs-lookup"><span data-stu-id="3702f-105">This consists of outgoing calls to communication libraries, storage clients, logging & metrics libraries, as well as incoming calls into application frameworks and servers.</span></span> <span data-ttu-id="3702f-106">These dependencies are visualized in the Application Insights [Application map](https://docs.microsoft.com/azure/application-insights/app-insights-app-map) and [Transaction diagnostics](https://docs.microsoft.com/azure/application-insights/app-insights-transaction-diagnostics) views.</span><span class="sxs-lookup"><span data-stu-id="3702f-106">These dependencies are visualized in the Application Insights [Application map](https://docs.microsoft.com/azure/application-insights/app-insights-app-map) and [Transaction diagnostics](https://docs.microsoft.com/azure/application-insights/app-insights-transaction-diagnostics) views.</span></span> <span data-ttu-id="3702f-107">If your dependency isn't on the list below, you can still track it manually with a [track dependency call](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackdependency).</span><span class="sxs-lookup"><span data-stu-id="3702f-107">If your dependency isn't on the list below, you can still track it manually with a [track dependency call](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#trackdependency).</span></span>

## <a name="net"></a><span data-ttu-id="3702f-108">.NET</span><span class="sxs-lookup"><span data-stu-id="3702f-108">.NET</span></span>

| <span data-ttu-id="3702f-109">App frameworks</span><span class="sxs-lookup"><span data-stu-id="3702f-109">App frameworks</span></span>| <span data-ttu-id="3702f-110">Versions</span><span class="sxs-lookup"><span data-stu-id="3702f-110">Versions</span></span> |
| ------------------------|----------|
| <span data-ttu-id="3702f-111">ASP.NET Webforms</span><span class="sxs-lookup"><span data-stu-id="3702f-111">ASP.NET Webforms</span></span> | <span data-ttu-id="3702f-112">4.5+</span><span class="sxs-lookup"><span data-stu-id="3702f-112">4.5+</span></span> |
| <span data-ttu-id="3702f-113">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="3702f-113">ASP.NET MVC</span></span> | <span data-ttu-id="3702f-114">4+</span><span class="sxs-lookup"><span data-stu-id="3702f-114">4+</span></span> |
| <span data-ttu-id="3702f-115">ASP.NET WebAPI</span><span class="sxs-lookup"><span data-stu-id="3702f-115">ASP.NET WebAPI</span></span> | <span data-ttu-id="3702f-116">4.5+</span><span class="sxs-lookup"><span data-stu-id="3702f-116">4.5+</span></span> |
| <span data-ttu-id="3702f-117">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="3702f-117">ASP.NET Core</span></span> | <span data-ttu-id="3702f-118">1.1+</span><span class="sxs-lookup"><span data-stu-id="3702f-118">1.1+</span></span> |
| <span data-ttu-id="3702f-119"><b> Communication libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-119"><b> Communication libraries</b></span></span> |
| [<span data-ttu-id="3702f-120">HttpClient</span><span class="sxs-lookup"><span data-stu-id="3702f-120">HttpClient</span></span>](https://www.microsoft.com/net/) | <span data-ttu-id="3702f-121">4.5+, .NET Core 1.1+</span><span class="sxs-lookup"><span data-stu-id="3702f-121">4.5+, .NET Core 1.1+</span></span> |
| [<span data-ttu-id="3702f-122">SqlClient</span><span class="sxs-lookup"><span data-stu-id="3702f-122">SqlClient</span></span>](https://www.nuget.org/packages/System.Data.SqlClient) | <span data-ttu-id="3702f-123">.NET Core 1.0+, NuGet 4.3.0</span><span class="sxs-lookup"><span data-stu-id="3702f-123">.NET Core 1.0+, NuGet 4.3.0</span></span> |
| [<span data-ttu-id="3702f-124">EventHubs Client SDK</span><span class="sxs-lookup"><span data-stu-id="3702f-124">EventHubs Client SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.EventHubs) | <span data-ttu-id="3702f-125">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3702f-125">1.1.0</span></span> |
| [<span data-ttu-id="3702f-126">ServiceBus Client SDK</span><span class="sxs-lookup"><span data-stu-id="3702f-126">ServiceBus Client SDK</span></span>](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus) | <span data-ttu-id="3702f-127">3.0.0</span><span class="sxs-lookup"><span data-stu-id="3702f-127">3.0.0</span></span> |
| <span data-ttu-id="3702f-128"><b>Storage clients</b></span><span class="sxs-lookup"><span data-stu-id="3702f-128"><b>Storage clients</b></span></span>|  |
| <span data-ttu-id="3702f-129">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="3702f-129">ADO.NET</span></span> | <span data-ttu-id="3702f-130">4.5+</span><span class="sxs-lookup"><span data-stu-id="3702f-130">4.5+</span></span> |
| <span data-ttu-id="3702f-131"><b>Logging libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-131"><b>Logging libraries</b></span></span> |  |
| <span data-ttu-id="3702f-132">ILogger</span><span class="sxs-lookup"><span data-stu-id="3702f-132">ILogger</span></span> | <span data-ttu-id="3702f-133">1.1+</span><span class="sxs-lookup"><span data-stu-id="3702f-133">1.1+</span></span> |
| <span data-ttu-id="3702f-134">System.Diagnostics.Trace</span><span class="sxs-lookup"><span data-stu-id="3702f-134">System.Diagnostics.Trace</span></span> | <span data-ttu-id="3702f-135">4.5+</span><span class="sxs-lookup"><span data-stu-id="3702f-135">4.5+</span></span> |
| [<span data-ttu-id="3702f-136">nLog</span><span class="sxs-lookup"><span data-stu-id="3702f-136">nLog</span></span>](https://www.nuget.org/packages/NLog/) | <span data-ttu-id="3702f-137">4.4.12+</span><span class="sxs-lookup"><span data-stu-id="3702f-137">4.4.12+</span></span> |
| [<span data-ttu-id="3702f-138">log4net</span><span class="sxs-lookup"><span data-stu-id="3702f-138">log4net</span></span>](https://www.nuget.org/packages/log4net/) | <span data-ttu-id="3702f-139">2.0.8+ on NetStandard  1.3, 2.0.6+ on .NET 4.5+</span><span class="sxs-lookup"><span data-stu-id="3702f-139">2.0.8+ on NetStandard  1.3, 2.0.6+ on .NET 4.5+</span></span> |

## <a name="java"></a><span data-ttu-id="3702f-140">Java</span><span class="sxs-lookup"><span data-stu-id="3702f-140">Java</span></span>
| <span data-ttu-id="3702f-141">App servers</span><span class="sxs-lookup"><span data-stu-id="3702f-141">App servers</span></span> | <span data-ttu-id="3702f-142">Versions</span><span class="sxs-lookup"><span data-stu-id="3702f-142">Versions</span></span> |
|-------------|----------|
| [<span data-ttu-id="3702f-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="3702f-143">Tomcat</span></span>](https://tomcat.apache.org/) | <span data-ttu-id="3702f-144">7, 8</span><span class="sxs-lookup"><span data-stu-id="3702f-144">7, 8</span></span> | 
| [<span data-ttu-id="3702f-145">JBoss EAP</span><span class="sxs-lookup"><span data-stu-id="3702f-145">JBoss EAP</span></span>](https://developers.redhat.com/products/eap/download/) | <span data-ttu-id="3702f-146">6, 7</span><span class="sxs-lookup"><span data-stu-id="3702f-146">6, 7</span></span> |
| [<span data-ttu-id="3702f-147">Jetty</span><span class="sxs-lookup"><span data-stu-id="3702f-147">Jetty</span></span>](http://www.eclipse.org/jetty/) | <span data-ttu-id="3702f-148">9</span><span class="sxs-lookup"><span data-stu-id="3702f-148">9</span></span> |
| <span data-ttu-id="3702f-149"><b>App frameworks </b></span><span class="sxs-lookup"><span data-stu-id="3702f-149"><b>App frameworks </b></span></span> |  |
| [<span data-ttu-id="3702f-150">Spring</span><span class="sxs-lookup"><span data-stu-id="3702f-150">Spring</span></span>](https://spring.io/) | <span data-ttu-id="3702f-151">3.0</span><span class="sxs-lookup"><span data-stu-id="3702f-151">3.0</span></span> |
| [<span data-ttu-id="3702f-152">Spring Boot</span><span class="sxs-lookup"><span data-stu-id="3702f-152">Spring Boot</span></span>](https://spring.io/projects/spring-boot) | <span data-ttu-id="3702f-153">1.5.9+<sup>\*</sup></span><span class="sxs-lookup"><span data-stu-id="3702f-153">1.5.9+<sup>\*</sup></span></span> |
| <span data-ttu-id="3702f-154">Java Servlet</span><span class="sxs-lookup"><span data-stu-id="3702f-154">Java Servlet</span></span> | <span data-ttu-id="3702f-155">3.1+</span><span class="sxs-lookup"><span data-stu-id="3702f-155">3.1+</span></span> |
| <span data-ttu-id="3702f-156"><b>Communication libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-156"><b>Communication libraries</b></span></span> |  |
| [<span data-ttu-id="3702f-157">Apache Http Client</span><span class="sxs-lookup"><span data-stu-id="3702f-157">Apache Http Client</span></span>](https://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient) | <span data-ttu-id="3702f-158">4.3+<sup>†</sup></span><span class="sxs-lookup"><span data-stu-id="3702f-158">4.3+<sup>†</sup></span></span> |
| <span data-ttu-id="3702f-159"><b>Storage clients</b></span><span class="sxs-lookup"><span data-stu-id="3702f-159"><b>Storage clients</b></span></span> | |
| [<span data-ttu-id="3702f-160">SQL Server</span><span class="sxs-lookup"><span data-stu-id="3702f-160">SQL Server</span></span>]( https://mvnrepository.com/artifact/com.microsoft.sqlserver/mssql-jdbc) | <span data-ttu-id="3702f-161">1+<sup>†</sup></span><span class="sxs-lookup"><span data-stu-id="3702f-161">1+<sup>†</sup></span></span> |
| [<span data-ttu-id="3702f-162">Oracle</span><span class="sxs-lookup"><span data-stu-id="3702f-162">Oracle</span></span>]( http://www.oracle.com/technetwork/database/application-development/jdbc/downloads/index.html) | <span data-ttu-id="3702f-163">1+<sup>†</sup></span><span class="sxs-lookup"><span data-stu-id="3702f-163">1+<sup>†</sup></span></span> |
| [<span data-ttu-id="3702f-164">MySql</span><span class="sxs-lookup"><span data-stu-id="3702f-164">MySql</span></span>]( https://mvnrepository.com/artifact/mysql/mysql-connector-java) | <span data-ttu-id="3702f-165">1+<sup>†</sup></span><span class="sxs-lookup"><span data-stu-id="3702f-165">1+<sup>†</sup></span></span> |
| <span data-ttu-id="3702f-166"><b>Logging libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-166"><b>Logging libraries</b></span></span> | |
| [<span data-ttu-id="3702f-167">Logback</span><span class="sxs-lookup"><span data-stu-id="3702f-167">Logback</span></span>](https://logback.qos.ch/) | <span data-ttu-id="3702f-168">1+</span><span class="sxs-lookup"><span data-stu-id="3702f-168">1+</span></span> |
| [<span data-ttu-id="3702f-169">Log4j</span><span class="sxs-lookup"><span data-stu-id="3702f-169">Log4j</span></span>](https://logging.apache.org/log4j/) | <span data-ttu-id="3702f-170">1.2+</span><span class="sxs-lookup"><span data-stu-id="3702f-170">1.2+</span></span> |
| <span data-ttu-id="3702f-171"><b>Metrics libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-171"><b>Metrics libraries</b></span></span> |  |
| <span data-ttu-id="3702f-172">JMX</span><span class="sxs-lookup"><span data-stu-id="3702f-172">JMX</span></span> | <span data-ttu-id="3702f-173">1.0+</span><span class="sxs-lookup"><span data-stu-id="3702f-173">1.0+</span></span> |

> [!NOTE]
> <span data-ttu-id="3702f-174">\*Except reactive programing support.</span><span class="sxs-lookup"><span data-stu-id="3702f-174">\*Except reactive programing support.</span></span>
> <br><span data-ttu-id="3702f-175">†Requires installation of [JVM Agent](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent#install-the-application-insights-agent-for-java).</span><span class="sxs-lookup"><span data-stu-id="3702f-175">†Requires installation of [JVM Agent](https://docs.microsoft.com/azure/application-insights/app-insights-java-agent#install-the-application-insights-agent-for-java).</span></span>

## <a name="nodejs"></a><span data-ttu-id="3702f-176">Node.js</span><span class="sxs-lookup"><span data-stu-id="3702f-176">Node.js</span></span>

| <span data-ttu-id="3702f-177">Communication libraries</span><span class="sxs-lookup"><span data-stu-id="3702f-177">Communication libraries</span></span> | <span data-ttu-id="3702f-178">Versions</span><span class="sxs-lookup"><span data-stu-id="3702f-178">Versions</span></span> |
| ------------------------|----------|
| <span data-ttu-id="3702f-179">[HTTP](https://nodejs.org/api/http.html), [HTTPS](https://nodejs.org/api/https.html)</span><span class="sxs-lookup"><span data-stu-id="3702f-179">[HTTP](https://nodejs.org/api/http.html), [HTTPS](https://nodejs.org/api/https.html)</span></span> | <span data-ttu-id="3702f-180">0.10+</span><span class="sxs-lookup"><span data-stu-id="3702f-180">0.10+</span></span> |
| <span data-ttu-id="3702f-181"><b>Storage clients</b></span><span class="sxs-lookup"><span data-stu-id="3702f-181"><b>Storage clients</b></span></span> | |
| [<span data-ttu-id="3702f-182">Redis</span><span class="sxs-lookup"><span data-stu-id="3702f-182">Redis</span></span>](https://www.npmjs.com/package/redis) | <span data-ttu-id="3702f-183">2.x</span><span class="sxs-lookup"><span data-stu-id="3702f-183">2.x</span></span> |
| <span data-ttu-id="3702f-184">[MongoDb](https://www.npmjs.com/package/mongodb); [MongoDb Core](https://www.npmjs.com/package/mongodb-core)</span><span class="sxs-lookup"><span data-stu-id="3702f-184">[MongoDb](https://www.npmjs.com/package/mongodb); [MongoDb Core](https://www.npmjs.com/package/mongodb-core)</span></span> | <span data-ttu-id="3702f-185">2.0.0 - 2.3.0</span><span class="sxs-lookup"><span data-stu-id="3702f-185">2.0.0 - 2.3.0</span></span> |
| [<span data-ttu-id="3702f-186">MySQL</span><span class="sxs-lookup"><span data-stu-id="3702f-186">MySQL</span></span>](https://www.npmjs.com/package/mysql) | <span data-ttu-id="3702f-187">2.0.0 - 2.14.x</span><span class="sxs-lookup"><span data-stu-id="3702f-187">2.0.0 - 2.14.x</span></span> |
| <span data-ttu-id="3702f-188">[PostgreSql](https://www.npmjs.com/package/pg);</span><span class="sxs-lookup"><span data-stu-id="3702f-188">[PostgreSql](https://www.npmjs.com/package/pg);</span></span> | <span data-ttu-id="3702f-189">6.x</span><span class="sxs-lookup"><span data-stu-id="3702f-189">6.x</span></span> |
| [<span data-ttu-id="3702f-190">pg-pool</span><span class="sxs-lookup"><span data-stu-id="3702f-190">pg-pool</span></span>](https://www.npmjs.com/package/pg-pool) | <span data-ttu-id="3702f-191">1.x</span><span class="sxs-lookup"><span data-stu-id="3702f-191">1.x</span></span> |
| <span data-ttu-id="3702f-192"><b>Logging libraries</b></span><span class="sxs-lookup"><span data-stu-id="3702f-192"><b>Logging libraries</b></span></span> | |
| [<span data-ttu-id="3702f-193">console</span><span class="sxs-lookup"><span data-stu-id="3702f-193">console</span></span>](https://nodejs.org/api/console.html) | <span data-ttu-id="3702f-194">0.10+</span><span class="sxs-lookup"><span data-stu-id="3702f-194">0.10+</span></span> |
| [<span data-ttu-id="3702f-195">Bunyan</span><span class="sxs-lookup"><span data-stu-id="3702f-195">Bunyan</span></span>](https://www.npmjs.com/package/bunyan) | <span data-ttu-id="3702f-196">1.x</span><span class="sxs-lookup"><span data-stu-id="3702f-196">1.x</span></span> |
| [<span data-ttu-id="3702f-197">Winston</span><span class="sxs-lookup"><span data-stu-id="3702f-197">Winston</span></span>](https://www.npmjs.com/package/winston) | <span data-ttu-id="3702f-198">2.x</span><span class="sxs-lookup"><span data-stu-id="3702f-198">2.x</span></span> |

## <a name="javascript"></a><span data-ttu-id="3702f-199">JavaScript</span><span class="sxs-lookup"><span data-stu-id="3702f-199">JavaScript</span></span>

| <span data-ttu-id="3702f-200">Communication libraries</span><span class="sxs-lookup"><span data-stu-id="3702f-200">Communication libraries</span></span> | <span data-ttu-id="3702f-201">Versions</span><span class="sxs-lookup"><span data-stu-id="3702f-201">Versions</span></span> |
| ------------------------|----------|
| [<span data-ttu-id="3702f-202">XMLHttpRequest</span><span class="sxs-lookup"><span data-stu-id="3702f-202">XMLHttpRequest</span></span>](https://developer.mozilla.org/docs/Web/API/XMLHttpRequest) | <span data-ttu-id="3702f-203">All</span><span class="sxs-lookup"><span data-stu-id="3702f-203">All</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3702f-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="3702f-204">Next steps</span></span>

- <span data-ttu-id="3702f-205">Set up custom dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="3702f-205">Set up custom dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="3702f-206">Set up custom dependency tracking for [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="3702f-206">Set up custom dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="3702f-207">Write custom dependency telemetry</span><span class="sxs-lookup"><span data-stu-id="3702f-207">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="3702f-208">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="3702f-208">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="3702f-209">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="3702f-209">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
