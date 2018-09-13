---
title: Azure Application Insights Telemetry Data Model - Exception Telemetry | Microsoft Docs
description: Application Insights data model for exception telemetry
services: application-insights
documentationcenter: .net
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: conceptual
ms.date: 04/25/2017
ms.reviewer: sergkanz
ms.author: mbullwin
ms.openlocfilehash: dc5480b90ef6b5520f47c51f0c105202d7071089
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871051"
---
# <a name="exception-telemetry-application-insights-data-model"></a><span data-ttu-id="92ab5-103">Exception telemetry: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="92ab5-103">Exception telemetry: Application Insights data model</span></span>

<span data-ttu-id="92ab5-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span><span class="sxs-lookup"><span data-stu-id="92ab5-104">In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.</span></span>

## <a name="problem-id"></a><span data-ttu-id="92ab5-105">Problem Id</span><span class="sxs-lookup"><span data-stu-id="92ab5-105">Problem Id</span></span>

<span data-ttu-id="92ab5-106">Identifier of where the exception was thrown in code.</span><span class="sxs-lookup"><span data-stu-id="92ab5-106">Identifier of where the exception was thrown in code.</span></span> <span data-ttu-id="92ab5-107">Used for exceptions grouping.</span><span class="sxs-lookup"><span data-stu-id="92ab5-107">Used for exceptions grouping.</span></span> <span data-ttu-id="92ab5-108">Typically a combination of exception type and a function from the call stack.</span><span class="sxs-lookup"><span data-stu-id="92ab5-108">Typically a combination of exception type and a function from the call stack.</span></span>

<span data-ttu-id="92ab5-109">Max length: 1024 characters</span><span class="sxs-lookup"><span data-stu-id="92ab5-109">Max length: 1024 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="92ab5-110">Severity level</span><span class="sxs-lookup"><span data-stu-id="92ab5-110">Severity level</span></span>

<span data-ttu-id="92ab5-111">Trace severity level.</span><span class="sxs-lookup"><span data-stu-id="92ab5-111">Trace severity level.</span></span> <span data-ttu-id="92ab5-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="92ab5-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="exception-details"></a><span data-ttu-id="92ab5-113">Exception details</span><span class="sxs-lookup"><span data-stu-id="92ab5-113">Exception details</span></span>

<span data-ttu-id="92ab5-114">(To be extended)</span><span class="sxs-lookup"><span data-stu-id="92ab5-114">(To be extended)</span></span>

## <a name="custom-properties"></a><span data-ttu-id="92ab5-115">Custom properties</span><span class="sxs-lookup"><span data-stu-id="92ab5-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="92ab5-116">Custom measurements</span><span class="sxs-lookup"><span data-stu-id="92ab5-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="92ab5-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="92ab5-117">Next steps</span></span>

- <span data-ttu-id="92ab5-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="92ab5-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="92ab5-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span><span class="sxs-lookup"><span data-stu-id="92ab5-119">Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).</span></span>
- <span data-ttu-id="92ab5-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="92ab5-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
