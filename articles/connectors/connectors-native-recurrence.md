---
title: Add the recurrence trigger in logic apps | Microsoft Docs
description: Overview of the recurrence trigger, and how to use it with an Azure logic app.
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: 9e76a51832b4e10691987a666d166891ca6e7b78
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550764"
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="43c19-103">Get started with the recurrence trigger</span><span class="sxs-lookup"><span data-stu-id="43c19-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="43c19-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span><span class="sxs-lookup"><span data-stu-id="43c19-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="43c19-105">For example, you can:</span><span class="sxs-lookup"><span data-stu-id="43c19-105">For example, you can:</span></span>

* <span data-ttu-id="43c19-106">Schedule a workflow to run a SQL stored procedure every day.</span><span class="sxs-lookup"><span data-stu-id="43c19-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="43c19-107">Email a summary of all tweets within the last week about a certain hashtag.</span><span class="sxs-lookup"><span data-stu-id="43c19-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="43c19-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="43c19-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="43c19-109">Use a recurrence trigger</span><span class="sxs-lookup"><span data-stu-id="43c19-109">Use a recurrence trigger</span></span>
<span data-ttu-id="43c19-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span><span class="sxs-lookup"><span data-stu-id="43c19-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="43c19-111">[Learn more about triggers](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43c19-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="43c19-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span><span class="sxs-lookup"><span data-stu-id="43c19-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="43c19-113">Add the **Recurrence** trigger as the first step in a logic app.</span><span class="sxs-lookup"><span data-stu-id="43c19-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="43c19-114">Fill in the parameters for the recurrence interval.</span><span class="sxs-lookup"><span data-stu-id="43c19-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="43c19-115">The logic app now starts a run after each interval of time.</span><span class="sxs-lookup"><span data-stu-id="43c19-115">The logic app now starts a run after each interval of time.</span></span>

![HTTP trigger](https://docstestmedia1.blob.core.windows.net/azure-media/articles/connectors/media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="43c19-117">Trigger details</span><span class="sxs-lookup"><span data-stu-id="43c19-117">Trigger details</span></span>
<span data-ttu-id="43c19-118">The recurrence trigger has the following properties that you can configure.</span><span class="sxs-lookup"><span data-stu-id="43c19-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="43c19-119">It fires a logic app after a specified time interval.</span><span class="sxs-lookup"><span data-stu-id="43c19-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="43c19-120">A \* means that it is a required field.</span><span class="sxs-lookup"><span data-stu-id="43c19-120">A \* means that it is a required field.</span></span>

| <span data-ttu-id="43c19-121">Display name</span><span class="sxs-lookup"><span data-stu-id="43c19-121">Display name</span></span> | <span data-ttu-id="43c19-122">Property name</span><span class="sxs-lookup"><span data-stu-id="43c19-122">Property name</span></span> | <span data-ttu-id="43c19-123">Description</span><span class="sxs-lookup"><span data-stu-id="43c19-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43c19-124">Frequency\*</span><span class="sxs-lookup"><span data-stu-id="43c19-124">Frequency\*</span></span> |<span data-ttu-id="43c19-125">frequency</span><span class="sxs-lookup"><span data-stu-id="43c19-125">frequency</span></span> |<span data-ttu-id="43c19-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span><span class="sxs-lookup"><span data-stu-id="43c19-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="43c19-127">Interval\*</span><span class="sxs-lookup"><span data-stu-id="43c19-127">Interval\*</span></span> |<span data-ttu-id="43c19-128">interval</span><span class="sxs-lookup"><span data-stu-id="43c19-128">interval</span></span> |<span data-ttu-id="43c19-129">The interval of the given frequency for the recurrence.</span><span class="sxs-lookup"><span data-stu-id="43c19-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="43c19-130">Time Zone</span><span class="sxs-lookup"><span data-stu-id="43c19-130">Time Zone</span></span> |<span data-ttu-id="43c19-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="43c19-131">timeZone</span></span> |<span data-ttu-id="43c19-132">If a start time is provided without a UTC offset, this time zone will be used.</span><span class="sxs-lookup"><span data-stu-id="43c19-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="43c19-133">Start time</span><span class="sxs-lookup"><span data-stu-id="43c19-133">Start time</span></span> |<span data-ttu-id="43c19-134">startTime</span><span class="sxs-lookup"><span data-stu-id="43c19-134">startTime</span></span> |<span data-ttu-id="43c19-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="43c19-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="43c19-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="43c19-136">Next steps</span></span>
<span data-ttu-id="43c19-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="43c19-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="43c19-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="43c19-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>


