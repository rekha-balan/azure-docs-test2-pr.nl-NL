---
title: Add a delay in logic apps | Microsoft Docs
description: Overview of the delay and delay-until actions, and how to use them with an Azure logic app.
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: f90d1e3e3898b6e073606cb31f462a18b0db3656
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555045"
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="efc02-103">Get started with the delay and delay-until actions</span><span class="sxs-lookup"><span data-stu-id="efc02-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="efc02-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span><span class="sxs-lookup"><span data-stu-id="efc02-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="efc02-105">For example, you can:</span><span class="sxs-lookup"><span data-stu-id="efc02-105">For example, you can:</span></span>

* <span data-ttu-id="efc02-106">Wait until a weekday to send a status update over email.</span><span class="sxs-lookup"><span data-stu-id="efc02-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="efc02-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span><span class="sxs-lookup"><span data-stu-id="efc02-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="efc02-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="efc02-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="efc02-109">Use the delay actions</span><span class="sxs-lookup"><span data-stu-id="efc02-109">Use the delay actions</span></span>
<span data-ttu-id="efc02-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="efc02-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="efc02-111">[Learn more about actions](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="efc02-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="efc02-112">Here’s an example sequence of how to use a delay step in a logic app:</span><span class="sxs-lookup"><span data-stu-id="efc02-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="efc02-113">After adding a trigger, click **New Step** to add an action.</span><span class="sxs-lookup"><span data-stu-id="efc02-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="efc02-114">Search for **delay** to bring up the delay actions.</span><span class="sxs-lookup"><span data-stu-id="efc02-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="efc02-115">In this example, we will select **Delay**.</span><span class="sxs-lookup"><span data-stu-id="efc02-115">In this example, we will select **Delay**.</span></span>
   
    ![Delay actions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="efc02-117">Complete any of the action properties to configure the delay.</span><span class="sxs-lookup"><span data-stu-id="efc02-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Delay config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="efc02-119">Click **Save** to publish and activate the logic app.</span><span class="sxs-lookup"><span data-stu-id="efc02-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="efc02-120">Action details</span><span class="sxs-lookup"><span data-stu-id="efc02-120">Action details</span></span>
<span data-ttu-id="efc02-121">The recurrence trigger has the following properties that can be configured.</span><span class="sxs-lookup"><span data-stu-id="efc02-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="efc02-122">Delay action</span><span class="sxs-lookup"><span data-stu-id="efc02-122">Delay action</span></span>
<span data-ttu-id="efc02-123">This action delays the run for a certain time interval.</span><span class="sxs-lookup"><span data-stu-id="efc02-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="efc02-124">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="efc02-124">A \* means that it is a required field.</span></span>

| <span data-ttu-id="efc02-125">Display name</span><span class="sxs-lookup"><span data-stu-id="efc02-125">Display name</span></span> | <span data-ttu-id="efc02-126">Property name</span><span class="sxs-lookup"><span data-stu-id="efc02-126">Property name</span></span> | <span data-ttu-id="efc02-127">Description</span><span class="sxs-lookup"><span data-stu-id="efc02-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc02-128">Count\*</span><span class="sxs-lookup"><span data-stu-id="efc02-128">Count\*</span></span> |<span data-ttu-id="efc02-129">count</span><span class="sxs-lookup"><span data-stu-id="efc02-129">count</span></span> |<span data-ttu-id="efc02-130">The number of time units to delay</span><span class="sxs-lookup"><span data-stu-id="efc02-130">The number of time units to delay</span></span> |
| <span data-ttu-id="efc02-131">Unit\*</span><span class="sxs-lookup"><span data-stu-id="efc02-131">Unit\*</span></span> |<span data-ttu-id="efc02-132">unit</span><span class="sxs-lookup"><span data-stu-id="efc02-132">unit</span></span> |<span data-ttu-id="efc02-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span><span class="sxs-lookup"><span data-stu-id="efc02-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="efc02-134">Delay-until action</span><span class="sxs-lookup"><span data-stu-id="efc02-134">Delay-until action</span></span>
<span data-ttu-id="efc02-135">This action delays the run until a specified date/time.</span><span class="sxs-lookup"><span data-stu-id="efc02-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="efc02-136">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="efc02-136">A \* means that it is a required field.</span></span>

| <span data-ttu-id="efc02-137">Display name</span><span class="sxs-lookup"><span data-stu-id="efc02-137">Display name</span></span> | <span data-ttu-id="efc02-138">Property name</span><span class="sxs-lookup"><span data-stu-id="efc02-138">Property name</span></span> | <span data-ttu-id="efc02-139">Description</span><span class="sxs-lookup"><span data-stu-id="efc02-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="efc02-140">Year\*</span><span class="sxs-lookup"><span data-stu-id="efc02-140">Year\*</span></span> |<span data-ttu-id="efc02-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="efc02-141">timestamp</span></span> |<span data-ttu-id="efc02-142">The year to delay until (GMT)</span><span class="sxs-lookup"><span data-stu-id="efc02-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="efc02-143">Month\*</span><span class="sxs-lookup"><span data-stu-id="efc02-143">Month\*</span></span> |<span data-ttu-id="efc02-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="efc02-144">timestamp</span></span> |<span data-ttu-id="efc02-145">The month to delay until (GMT)</span><span class="sxs-lookup"><span data-stu-id="efc02-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="efc02-146">Day\*</span><span class="sxs-lookup"><span data-stu-id="efc02-146">Day\*</span></span> |<span data-ttu-id="efc02-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="efc02-147">timestamp</span></span> |<span data-ttu-id="efc02-148">The day to delay until (GMT)</span><span class="sxs-lookup"><span data-stu-id="efc02-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="efc02-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="efc02-149">Next steps</span></span>
<span data-ttu-id="efc02-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="efc02-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="efc02-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="efc02-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>



