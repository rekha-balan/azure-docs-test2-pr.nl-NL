---
title: System variables in Azure Data Factory | Microsoft Docs
description: This article describes system variables supported by Azure Data Factory. You can use these variables in expressions when defining Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 06/12/2018
ms.author: shlo
ms.openlocfilehash: 43ea8703bdbfc23511c831a5f91c9461948cc254
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856407"
---
# <a name="system-variables-supported-by-azure-data-factory"></a><span data-ttu-id="884fa-104">System variables supported by Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="884fa-104">System variables supported by Azure Data Factory</span></span>
<span data-ttu-id="884fa-105">This article describes system variables supported by Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="884fa-105">This article describes system variables supported by Azure Data Factory.</span></span> <span data-ttu-id="884fa-106">You can use these variables in expressions when defining Data Factory entities.</span><span class="sxs-lookup"><span data-stu-id="884fa-106">You can use these variables in expressions when defining Data Factory entities.</span></span>

## <a name="pipeline-scope"></a><span data-ttu-id="884fa-107">Pipeline scope</span><span class="sxs-lookup"><span data-stu-id="884fa-107">Pipeline scope</span></span>
<span data-ttu-id="884fa-108">These system variables can be referenced anywhere in the pipeline JSON.</span><span class="sxs-lookup"><span data-stu-id="884fa-108">These system variables can be referenced anywhere in the pipeline JSON.</span></span>

| <span data-ttu-id="884fa-109">Variable Name</span><span class="sxs-lookup"><span data-stu-id="884fa-109">Variable Name</span></span> | <span data-ttu-id="884fa-110">Description</span><span class="sxs-lookup"><span data-stu-id="884fa-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="884fa-111">@pipeline().DataFactory</span><span class="sxs-lookup"><span data-stu-id="884fa-111">@pipeline().DataFactory</span></span> |<span data-ttu-id="884fa-112">Name of the data factory the pipeline run is running within</span><span class="sxs-lookup"><span data-stu-id="884fa-112">Name of the data factory the pipeline run is running within</span></span> |
| <span data-ttu-id="884fa-113">@pipeline().Pipeline</span><span class="sxs-lookup"><span data-stu-id="884fa-113">@pipeline().Pipeline</span></span> |<span data-ttu-id="884fa-114">Name of the pipeline</span><span class="sxs-lookup"><span data-stu-id="884fa-114">Name of the pipeline</span></span> |
| <span data-ttu-id="884fa-115">@pipeline().RunId</span><span class="sxs-lookup"><span data-stu-id="884fa-115">@pipeline().RunId</span></span> | <span data-ttu-id="884fa-116">ID of the specific pipeline run</span><span class="sxs-lookup"><span data-stu-id="884fa-116">ID of the specific pipeline run</span></span> |
| <span data-ttu-id="884fa-117">@pipeline().TriggerType</span><span class="sxs-lookup"><span data-stu-id="884fa-117">@pipeline().TriggerType</span></span> | <span data-ttu-id="884fa-118">Type of the trigger that invoked the pipeline (Manual, Scheduler)</span><span class="sxs-lookup"><span data-stu-id="884fa-118">Type of the trigger that invoked the pipeline (Manual, Scheduler)</span></span> |
| <span data-ttu-id="884fa-119">@pipeline().TriggerId</span><span class="sxs-lookup"><span data-stu-id="884fa-119">@pipeline().TriggerId</span></span>| <span data-ttu-id="884fa-120">ID of the trigger that invokes the pipeline</span><span class="sxs-lookup"><span data-stu-id="884fa-120">ID of the trigger that invokes the pipeline</span></span> |
| <span data-ttu-id="884fa-121">@pipeline().TriggerName</span><span class="sxs-lookup"><span data-stu-id="884fa-121">@pipeline().TriggerName</span></span>| <span data-ttu-id="884fa-122">Name of the trigger that invokes the pipeline</span><span class="sxs-lookup"><span data-stu-id="884fa-122">Name of the trigger that invokes the pipeline</span></span> |
| <span data-ttu-id="884fa-123">@pipeline().TriggerTime</span><span class="sxs-lookup"><span data-stu-id="884fa-123">@pipeline().TriggerTime</span></span>| <span data-ttu-id="884fa-124">Time when the trigger that invoked the pipeline.</span><span class="sxs-lookup"><span data-stu-id="884fa-124">Time when the trigger that invoked the pipeline.</span></span> <span data-ttu-id="884fa-125">The trigger time is the actual fired time, not the scheduled time.</span><span class="sxs-lookup"><span data-stu-id="884fa-125">The trigger time is the actual fired time, not the scheduled time.</span></span> <span data-ttu-id="884fa-126">For example, `13:20:08.0149599Z` is returned instead of `13:20:00.00Z`</span><span class="sxs-lookup"><span data-stu-id="884fa-126">For example, `13:20:08.0149599Z` is returned instead of `13:20:00.00Z`</span></span> |

## <a name="schedule-trigger-scope"></a><span data-ttu-id="884fa-127">Schedule Trigger scope</span><span class="sxs-lookup"><span data-stu-id="884fa-127">Schedule Trigger scope</span></span>
<span data-ttu-id="884fa-128">These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "ScheduleTrigger."</span><span class="sxs-lookup"><span data-stu-id="884fa-128">These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "ScheduleTrigger."</span></span>

| <span data-ttu-id="884fa-129">Variable Name</span><span class="sxs-lookup"><span data-stu-id="884fa-129">Variable Name</span></span> | <span data-ttu-id="884fa-130">Description</span><span class="sxs-lookup"><span data-stu-id="884fa-130">Description</span></span> |
| --- | --- |
| <span data-ttu-id="884fa-131">@trigger().scheduledTime</span><span class="sxs-lookup"><span data-stu-id="884fa-131">@trigger().scheduledTime</span></span> |<span data-ttu-id="884fa-132">Time when the trigger was scheduled to invoke the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="884fa-132">Time when the trigger was scheduled to invoke the pipeline run.</span></span> <span data-ttu-id="884fa-133">For example, for a trigger that fires every 5 min, this variable would return `2017-06-01T22:20:00Z`, `2017-06-01T22:25:00Z`, `2017-06-01T22:29:00Z` respectively.</span><span class="sxs-lookup"><span data-stu-id="884fa-133">For example, for a trigger that fires every 5 min, this variable would return `2017-06-01T22:20:00Z`, `2017-06-01T22:25:00Z`, `2017-06-01T22:29:00Z` respectively.</span></span>|
| <span data-ttu-id="884fa-134">@trigger().startTime</span><span class="sxs-lookup"><span data-stu-id="884fa-134">@trigger().startTime</span></span> |<span data-ttu-id="884fa-135">Time when the trigger **actually** fired to invoke the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="884fa-135">Time when the trigger **actually** fired to invoke the pipeline run.</span></span> <span data-ttu-id="884fa-136">For example, for a trigger that fires every 5 min, this variable might return something like this `2017-06-01T22:20:00.4061448Z`, `2017-06-01T22:25:00.7958577Z`, `2017-06-01T22:29:00.9935483Z` respectively.</span><span class="sxs-lookup"><span data-stu-id="884fa-136">For example, for a trigger that fires every 5 min, this variable might return something like this `2017-06-01T22:20:00.4061448Z`, `2017-06-01T22:25:00.7958577Z`, `2017-06-01T22:29:00.9935483Z` respectively.</span></span>|

## <a name="tumbling-window-trigger-scope"></a><span data-ttu-id="884fa-137">Tumbling Window Trigger scope</span><span class="sxs-lookup"><span data-stu-id="884fa-137">Tumbling Window Trigger scope</span></span>
<span data-ttu-id="884fa-138">These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "TumblingWindowTrigger."</span><span class="sxs-lookup"><span data-stu-id="884fa-138">These system variables can be referenced anywhere in the trigger JSON if the trigger is of type: "TumblingWindowTrigger."</span></span>

| <span data-ttu-id="884fa-139">Variable Name</span><span class="sxs-lookup"><span data-stu-id="884fa-139">Variable Name</span></span> | <span data-ttu-id="884fa-140">Description</span><span class="sxs-lookup"><span data-stu-id="884fa-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="884fa-141">@trigger().outputs.windowStartTime</span><span class="sxs-lookup"><span data-stu-id="884fa-141">@trigger().outputs.windowStartTime</span></span> |<span data-ttu-id="884fa-142">Start of the window when the trigger was scheduled to invoke the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="884fa-142">Start of the window when the trigger was scheduled to invoke the pipeline run.</span></span> <span data-ttu-id="884fa-143">If the tumbling window trigger has a frequency of "hourly" this would be the time at the beginning of the hour.</span><span class="sxs-lookup"><span data-stu-id="884fa-143">If the tumbling window trigger has a frequency of "hourly" this would be the time at the beginning of the hour.</span></span>|
| <span data-ttu-id="884fa-144">@trigger().outputs.windowEndTime</span><span class="sxs-lookup"><span data-stu-id="884fa-144">@trigger().outputs.windowEndTime</span></span> |<span data-ttu-id="884fa-145">End of the window when the trigger was scheduled to invoke the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="884fa-145">End of the window when the trigger was scheduled to invoke the pipeline run.</span></span> <span data-ttu-id="884fa-146">If the tumbling window trigger has a frequency of "hourly" this would be the time at the end of the hour.</span><span class="sxs-lookup"><span data-stu-id="884fa-146">If the tumbling window trigger has a frequency of "hourly" this would be the time at the end of the hour.</span></span>|
## <a name="next-steps"></a><span data-ttu-id="884fa-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="884fa-147">Next steps</span></span>
<span data-ttu-id="884fa-148">For information about how these variables are used in expressions, see [Expression language & functions](control-flow-expression-language-functions.md).</span><span class="sxs-lookup"><span data-stu-id="884fa-148">For information about how these variables are used in expressions, see [Expression language & functions](control-flow-expression-language-functions.md).</span></span>
