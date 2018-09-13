---
title: Azure Application Insights Telemetry Data Model - Event Telemetry | Microsoft Docs
description: Application Insights data model for event telemetry
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
ms.openlocfilehash: 062478783465edc2d3afa4b80a22f119e68da049
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868102"
---
# <a name="event-telemetry-application-insights-data-model"></a><span data-ttu-id="d614e-103">Event telemetry: Application Insights data model</span><span class="sxs-lookup"><span data-stu-id="d614e-103">Event telemetry: Application Insights data model</span></span>

<span data-ttu-id="d614e-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span><span class="sxs-lookup"><span data-stu-id="d614e-104">You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application.</span></span> <span data-ttu-id="d614e-105">Typically it is a user interaction such as button click or order checkout.</span><span class="sxs-lookup"><span data-stu-id="d614e-105">Typically it is a user interaction such as button click or order checkout.</span></span> <span data-ttu-id="d614e-106">It can also be an application life cycle event like initialization or configuration update.</span><span class="sxs-lookup"><span data-stu-id="d614e-106">It can also be an application life cycle event like initialization or configuration update.</span></span> 

<span data-ttu-id="d614e-107">Semantically, events may or may not be correlated to requests.</span><span class="sxs-lookup"><span data-stu-id="d614e-107">Semantically, events may or may not be correlated to requests.</span></span> <span data-ttu-id="d614e-108">However, if used properly, event telemetry is more important than requests or traces.</span><span class="sxs-lookup"><span data-stu-id="d614e-108">However, if used properly, event telemetry is more important than requests or traces.</span></span> <span data-ttu-id="d614e-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="d614e-109">Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).</span></span>

## <a name="name"></a><span data-ttu-id="d614e-110">Name</span><span class="sxs-lookup"><span data-stu-id="d614e-110">Name</span></span>

<span data-ttu-id="d614e-111">Event name.</span><span class="sxs-lookup"><span data-stu-id="d614e-111">Event name.</span></span> <span data-ttu-id="d614e-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span><span class="sxs-lookup"><span data-stu-id="d614e-112">To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names.</span></span> <span data-ttu-id="d614e-113">For example, don't use a separate name for each generated instance of an event.</span><span class="sxs-lookup"><span data-stu-id="d614e-113">For example, don't use a separate name for each generated instance of an event.</span></span>

<span data-ttu-id="d614e-114">Max length: 512 characters</span><span class="sxs-lookup"><span data-stu-id="d614e-114">Max length: 512 characters</span></span>

## <a name="custom-properties"></a><span data-ttu-id="d614e-115">Custom properties</span><span class="sxs-lookup"><span data-stu-id="d614e-115">Custom properties</span></span>

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a><span data-ttu-id="d614e-116">Custom measurements</span><span class="sxs-lookup"><span data-stu-id="d614e-116">Custom measurements</span></span>

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a><span data-ttu-id="d614e-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="d614e-117">Next steps</span></span>

- <span data-ttu-id="d614e-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span><span class="sxs-lookup"><span data-stu-id="d614e-118">See [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- [<span data-ttu-id="d614e-119">Write custom event telemetry</span><span class="sxs-lookup"><span data-stu-id="d614e-119">Write custom event telemetry</span></span>](app-insights-api-custom-events-metrics.md#trackevent)
- <span data-ttu-id="d614e-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span><span class="sxs-lookup"><span data-stu-id="d614e-120">Check out [platforms](app-insights-platforms.md) supported by Application Insights.</span></span>
