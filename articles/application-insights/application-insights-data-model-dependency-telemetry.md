---
title: Azure Application Insights Telemetry Data Model - Dependency Telemetry | Microsoft Docs
description: Application Insights data model for dependency telemetry
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/17/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: 5765be9fc88cbe38841078b5c298d3ee12269e6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857730"
---
# <a name="dependency-telemetry-application-insights-data-model"></a><span data-ttu-id="2c1cb-103">Dependency telemetry: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="2c1cb-103">Dependency telemetry: Application Insights data model</span></span>

<span data-ttu-id="2c1cb-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-104">Dependency Telemetry (in [Application Insights](app-insights-overview.md)) represents an interaction of the monitored component with a remote component such as SQL or an HTTP endpoint.</span></span>

## <a name="name"></a><span data-ttu-id="2c1cb-105">Name</span><span class="sxs-lookup"><span data-stu-id="2c1cb-105">Name</span></span>

<span data-ttu-id="2c1cb-106">Name of the command initiated with this dependency call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-106">Name of the command initiated with this dependency call.</span></span> <span data-ttu-id="2c1cb-107">Low cardinality value.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-107">Low cardinality value.</span></span> <span data-ttu-id="2c1cb-108">Examples are stored procedure name and URL path template.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-108">Examples are stored procedure name and URL path template.</span></span>

## <a name="id"></a><span data-ttu-id="2c1cb-109">ID</span><span class="sxs-lookup"><span data-stu-id="2c1cb-109">ID</span></span>

<span data-ttu-id="2c1cb-110">Identifier of a dependency call instance.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-110">Identifier of a dependency call instance.</span></span> <span data-ttu-id="2c1cb-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-111">Used for correlation with the request telemetry item corresponding to this dependency call.</span></span> <span data-ttu-id="2c1cb-112">For more information, see [correlation](application-insights-correlation.md) page.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-112">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="data"></a><span data-ttu-id="2c1cb-113">Data</span><span class="sxs-lookup"><span data-stu-id="2c1cb-113">Data</span></span>

<span data-ttu-id="2c1cb-114">Command initiated by this dependency call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-114">Command initiated by this dependency call.</span></span> <span data-ttu-id="2c1cb-115">Examples are SQL statement and HTTP URL with all query parameters.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-115">Examples are SQL statement and HTTP URL with all query parameters.</span></span>

## <a name="type"></a><span data-ttu-id="2c1cb-116">Type</span><span class="sxs-lookup"><span data-stu-id="2c1cb-116">Type</span></span>

<span data-ttu-id="2c1cb-117">Dependency type name.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-117">Dependency type name.</span></span> <span data-ttu-id="2c1cb-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-118">Low cardinality value for logical grouping of dependencies and interpretation of other fields like commandName and resultCode.</span></span> <span data-ttu-id="2c1cb-119">Examples are SQL, Azure table, and HTTP.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-119">Examples are SQL, Azure table, and HTTP.</span></span>

## <a name="target"></a><span data-ttu-id="2c1cb-120">Target</span><span class="sxs-lookup"><span data-stu-id="2c1cb-120">Target</span></span>

<span data-ttu-id="2c1cb-121">Target site of a dependency call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-121">Target site of a dependency call.</span></span> <span data-ttu-id="2c1cb-122">Examples are server name, host address.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-122">Examples are server name, host address.</span></span> <span data-ttu-id="2c1cb-123">For more information, see [correlation](application-insights-correlation.md) page.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-123">For more information, see [correlation](application-insights-correlation.md) page.</span></span>

## <a name="duration"></a><span data-ttu-id="2c1cb-124">Duration</span><span class="sxs-lookup"><span data-stu-id="2c1cb-124">Duration</span></span>

<span data-ttu-id="2c1cb-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-125">Request duration in format: `DD.HH:MM:SS.MMMMMM`.</span></span> <span data-ttu-id="2c1cb-126">Must be less than `1000` days.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-126">Must be less than `1000` days.</span></span>

## <a name="result-code"></a><span data-ttu-id="2c1cb-127">Result code</span><span class="sxs-lookup"><span data-stu-id="2c1cb-127">Result code</span></span>

<span data-ttu-id="2c1cb-128">Result code of a dependency call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-128">Result code of a dependency call.</span></span> <span data-ttu-id="2c1cb-129">Examples are SQL error code and HTTP status code.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-129">Examples are SQL error code and HTTP status code.</span></span>

## <a name="success"></a><span data-ttu-id="2c1cb-130">Success</span><span class="sxs-lookup"><span data-stu-id="2c1cb-130">Success</span></span>

<span data-ttu-id="2c1cb-131">Indication of successful or unsuccessful call.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-131">Indication of successful or unsuccessful call.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="2c1cb-132">Custom properties</span><span class="sxs-lookup"><span data-stu-id="2c1cb-132">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="2c1cb-133">Custom measurements</span><span class="sxs-lookup"><span data-stu-id="2c1cb-133">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]


## <a name="next-steps"></a><span data-ttu-id="2c1cb-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="2c1cb-134">Next steps</span></span>

- <span data-ttu-id="2c1cb-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span><span class="sxs-lookup"><span data-stu-id="2c1cb-135">Set up dependency tracking for [.NET](app-insights-asp-net-dependencies.md).</span></span>
- <span data-ttu-id="2c1cb-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="2c1cb-136">Set up dependency tracking for [Java](app-insights-java-agent.md).</span></span>
- [<span data-ttu-id="2c1cb-137">Write custom dependency telemetry</span><span class="sxs-lookup"><span data-stu-id="2c1cb-137">Write custom dependency telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackdependency)
- <span data-ttu-id="2c1cb-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-138">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="2c1cb-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2c1cb-139">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
