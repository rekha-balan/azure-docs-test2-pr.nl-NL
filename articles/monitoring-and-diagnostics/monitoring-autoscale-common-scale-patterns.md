---
title: Overview of common autoscale patterns
description: Learn some of the common patterns to auto scale your resource in Azure.
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 05/07/2017
ms.author: ancav
ms.component: autoscale
ms.openlocfilehash: 84727ec3694f64d40ad002a248a255df9074d7f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966444"
---
# <a name="overview-of-common-autoscale-patterns"></a>Overview of common autoscale patterns
This article describes some of the common patterns to scale your resource in Azure.

Azure Monitor auto scale applies only to Virtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments. 

# <a name="lets-get-started"></a>Lets get started

This article assumes that you are familiar with auto scale. You can [get started here to scale your resource][1]. The following are some of the common scale patterns.

## <a name="scale-based-on-cpu"></a>Scale based on CPU

You have a web app (/VMSS/cloud service role) and 

- You want to scale out/scale in based on CPU.
- Additionally, you want to ensure there is a minimum number of instances. 
- Also, you want to ensure that you set a maximum limit to the number of instances you can scale to.

![Scale based on CPU][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Scale differently on weekdays vs weekends

You have a web app (/VMSS/cloud service role) and

- You want 3 instances by default (on weekdays)
- You don't expect traffic on weekends and hence you want to scale down to 1 instance on weekends.

![Scale differently on weekdays vs weekends][3]

## <a name="scale-differently-during-holidays"></a>Scale differently during holidays

You have a web app (/VMSS/cloud service role) and 

- You want to scale up/down based on CPU usage by default
- However, during holiday season (or specific days that are important for your business) you want to override the defaults and have more capacity at your disposal.

![Scale differently on holidays][4]

## <a name="scale-based-on-custom-metric"></a>Scale based on custom metric

You have a web front end and a API tier that communicates with the backend. 

- You want to scale the API tier based on custom events in the front end (example: You want to scale your checkout process based on the number of items in the shopping cart)

![Scale based on custom metric][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png