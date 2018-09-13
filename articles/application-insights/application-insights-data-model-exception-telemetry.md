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
# <a name="exception-telemetry-application-insights-data-model"></a>Exception telemetry: Application Insights data model

In [Application Insights](app-insights-overview.md), an instance of Exception represents a handled or unhandled exception that occurred during execution of the monitored application.

## <a name="problem-id"></a>Problem Id

Identifier of where the exception was thrown in code. Used for exceptions grouping. Typically a combination of exception type and a function from the call stack.

Max length: 1024 characters

## <a name="severity-level"></a>Severity level

Trace severity level. Value can be `Verbose`, `Information`, `Warning`, `Error`, `Critical`.

## <a name="exception-details"></a>Exception details

(To be extended)

## <a name="custom-properties"></a>Custom properties

[!INCLUDE [application-insights-data-model-properties](../../includes/application-insights-data-model-properties.md)]

## <a name="custom-measurements"></a>Custom measurements

[!INCLUDE [application-insights-data-model-measurements](../../includes/application-insights-data-model-measurements.md)]

## <a name="next-steps"></a>Next steps

- See [data model](application-insights-data-model.md) for Application Insights types and data model.
- Learn how to [diagnose exceptions in your web apps with Application Insights](app-insights-asp-net-exceptions.md).
- Check out [platforms](app-insights-platforms.md) supported by Application Insights.
