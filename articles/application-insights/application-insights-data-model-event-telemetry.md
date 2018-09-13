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
# <a name="event-telemetry-application-insights-data-model"></a>Event telemetry: Application Insights data model

You can create event telemetry items (in [Application Insights](app-insights-overview.md)) to represent an event that occurred in your application. Typically it is a user interaction such as button click or order checkout. It can also be an application life cycle event like initialization or configuration update. 

Semantically, events may or may not be correlated to requests. However, if used properly, event telemetry is more important than requests or traces. Events represent business telemetry and should be a subject to separate, less aggressive [sampling](app-insights-api-filtering-sampling.md).

## <a name="name"></a>Name

Event name. To allow proper grouping and useful metrics, restrict your application so that it generates a small number of separate event names. For example, don't use a separate name for each generated instance of an event.

Max length: 512 characters

## <a name="custom-properties"></a>Custom properties

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Custom measurements

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Next steps

- See [data model](application-insights-data-model.md) for Application Insights types and data model.
- [Write custom event telemetry](app-insights-api-custom-events-metrics.md#trackevent)
- Check out [platforms](app-insights-platforms.md) supported by Application Insights.
