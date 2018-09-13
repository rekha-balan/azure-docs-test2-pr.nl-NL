---
title: Azure Application Insights Telemetry Data Model - Trace Telemetry | Microsoft Docs
description: Application Insights data model for trace telemetry
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
ms.openlocfilehash: 79d012ddb454842e53fe296d9b618438ee7b3e91
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868097"
---
# <a name="trace-telemetry-application-insights-data-model"></a><span data-ttu-id="4d581-103">Trace telemetry: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="4d581-103">Trace telemetry: Application Insights data model</span></span>

<span data-ttu-id="4d581-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span><span class="sxs-lookup"><span data-stu-id="4d581-104">Trace telemetry (in [Application Insights](app-insights-overview.md)) represents `printf` style trace statements that are text-searched.</span></span> <span data-ttu-id="4d581-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span><span class="sxs-lookup"><span data-stu-id="4d581-105">`Log4Net`, `NLog`, and other text-based log file entries are translated into instances of this type.</span></span> <span data-ttu-id="4d581-106">The trace does not have measurements as an extensibility.</span><span class="sxs-lookup"><span data-stu-id="4d581-106">The trace does not have measurements as an extensibility.</span></span>

## <a name="message"></a><span data-ttu-id="4d581-107">Message</span><span class="sxs-lookup"><span data-stu-id="4d581-107">Message</span></span>

<span data-ttu-id="4d581-108">Trace message.</span><span class="sxs-lookup"><span data-stu-id="4d581-108">Trace message.</span></span>

<span data-ttu-id="4d581-109">Max length: 32768 characters</span><span class="sxs-lookup"><span data-stu-id="4d581-109">Max length: 32768 characters</span></span>

## <a name="severity-level"></a><span data-ttu-id="4d581-110">Severity level</span><span class="sxs-lookup"><span data-stu-id="4d581-110">Severity level</span></span>

<span data-ttu-id="4d581-111">Trace severity level.</span><span class="sxs-lookup"><span data-stu-id="4d581-111">Trace severity level.</span></span> <span data-ttu-id="4d581-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span><span class="sxs-lookup"><span data-stu-id="4d581-112">Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.</span></span>

## <a name="custom-properties"></a><span data-ttu-id="4d581-113">Custom properties</span><span class="sxs-lookup"><span data-stu-id="4d581-113">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="next-steps"></a><span data-ttu-id="4d581-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="4d581-114">Next steps</span></span>

- <span data-ttu-id="4d581-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4d581-115">[Explore .NET trace logs in Application Insights](app-insights-asp-net-trace-logs.md).</span></span>
- <span data-ttu-id="4d581-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span><span class="sxs-lookup"><span data-stu-id="4d581-116">[Explore Java trace logs in Application Insights](app-insights-java-trace-logs.md).</span></span>
- <span data-ttu-id="4d581-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="4d581-117">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="4d581-118">Write custom trace telemetry</span><span class="sxs-lookup"><span data-stu-id="4d581-118">Write custom trace telemetry</span></span>](app-insights-api-custom-events-metrics.md#tracktrace)
- <span data-ttu-id="4d581-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="4d581-119">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
