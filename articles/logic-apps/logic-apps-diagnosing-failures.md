---
title: Diagnose failures - Azure Logic Apps | Microsoft Docs
description: Common ways to understand where logic apps are failing
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: ''
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: jehollan
ms.openlocfilehash: 2fe8501c8a3b996c5a509e09bc7b30ac90fd2cc0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555736"
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="634b0-103">Diagnose logic app failures</span><span class="sxs-lookup"><span data-stu-id="634b0-103">Diagnose logic app failures</span></span>
<span data-ttu-id="634b0-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span><span class="sxs-lookup"><span data-stu-id="634b0-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="634b0-105">Azure portal tools</span><span class="sxs-lookup"><span data-stu-id="634b0-105">Azure portal tools</span></span>
<span data-ttu-id="634b0-106">The Azure portal provides many tools to diagnose each logic app at each step.</span><span class="sxs-lookup"><span data-stu-id="634b0-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="634b0-107">Trigger history</span><span class="sxs-lookup"><span data-stu-id="634b0-107">Trigger history</span></span>

<span data-ttu-id="634b0-108">Each logic app has at least one trigger.</span><span class="sxs-lookup"><span data-stu-id="634b0-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="634b0-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span><span class="sxs-lookup"><span data-stu-id="634b0-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="634b0-110">You can access the trigger history on the logic app'ss main blade.</span><span class="sxs-lookup"><span data-stu-id="634b0-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Locating the trigger history][1]

<span data-ttu-id="634b0-112">The trigger history lists all trigger attempts that your logic app made.</span><span class="sxs-lookup"><span data-stu-id="634b0-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="634b0-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span><span class="sxs-lookup"><span data-stu-id="634b0-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="634b0-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span><span class="sxs-lookup"><span data-stu-id="634b0-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="634b0-115">The different statuses you might see are:</span><span class="sxs-lookup"><span data-stu-id="634b0-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="634b0-116">**Skipped**.</span><span class="sxs-lookup"><span data-stu-id="634b0-116">**Skipped**.</span></span> <span data-ttu-id="634b0-117">The endpoint was polled to check for data and received a response that no data was available.</span><span class="sxs-lookup"><span data-stu-id="634b0-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="634b0-118">**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="634b0-118">**Succeeded**.</span></span> <span data-ttu-id="634b0-119">The trigger received a response that data was available.</span><span class="sxs-lookup"><span data-stu-id="634b0-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="634b0-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span><span class="sxs-lookup"><span data-stu-id="634b0-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="634b0-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span><span class="sxs-lookup"><span data-stu-id="634b0-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="634b0-122">**Failed**.</span><span class="sxs-lookup"><span data-stu-id="634b0-122">**Failed**.</span></span> <span data-ttu-id="634b0-123">An error was generated.</span><span class="sxs-lookup"><span data-stu-id="634b0-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="634b0-124">Start a trigger manually</span><span class="sxs-lookup"><span data-stu-id="634b0-124">Start a trigger manually</span></span>

<span data-ttu-id="634b0-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span><span class="sxs-lookup"><span data-stu-id="634b0-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="634b0-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span><span class="sxs-lookup"><span data-stu-id="634b0-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="634b0-127">Run history</span><span class="sxs-lookup"><span data-stu-id="634b0-127">Run history</span></span>

<span data-ttu-id="634b0-128">Every fired trigger results in a run.</span><span class="sxs-lookup"><span data-stu-id="634b0-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="634b0-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span><span class="sxs-lookup"><span data-stu-id="634b0-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Locating the run history][2]

<span data-ttu-id="634b0-131">A run displays one of the following statuses:</span><span class="sxs-lookup"><span data-stu-id="634b0-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="634b0-132">**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="634b0-132">**Succeeded**.</span></span> <span data-ttu-id="634b0-133">All actions succeeded.</span><span class="sxs-lookup"><span data-stu-id="634b0-133">All actions succeeded.</span></span> <span data-ttu-id="634b0-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span><span class="sxs-lookup"><span data-stu-id="634b0-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="634b0-135">That is, the failure was handled by an action that was set to run after a failed action.</span><span class="sxs-lookup"><span data-stu-id="634b0-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="634b0-136">**Failed**.</span><span class="sxs-lookup"><span data-stu-id="634b0-136">**Failed**.</span></span> <span data-ttu-id="634b0-137">At least one action had a failure that was not handled by an action later in the workflow.</span><span class="sxs-lookup"><span data-stu-id="634b0-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="634b0-138">**Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="634b0-138">**Cancelled**.</span></span> <span data-ttu-id="634b0-139">The workflow was running but received a cancel request.</span><span class="sxs-lookup"><span data-stu-id="634b0-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="634b0-140">**Running**.</span><span class="sxs-lookup"><span data-stu-id="634b0-140">**Running**.</span></span> <span data-ttu-id="634b0-141">The workflow is currently running.</span><span class="sxs-lookup"><span data-stu-id="634b0-141">The workflow is currently running.</span></span> <span data-ttu-id="634b0-142">This status might occur for throttled workflows, or because of the current pricing plan.</span><span class="sxs-lookup"><span data-stu-id="634b0-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="634b0-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="634b0-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="634b0-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span><span class="sxs-lookup"><span data-stu-id="634b0-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="634b0-145">When you are looking at a run history, you can drill in for more details.</span><span class="sxs-lookup"><span data-stu-id="634b0-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="634b0-146">Trigger outputs</span><span class="sxs-lookup"><span data-stu-id="634b0-146">Trigger outputs</span></span>

<span data-ttu-id="634b0-147">Trigger outputs show the data that came from the trigger.</span><span class="sxs-lookup"><span data-stu-id="634b0-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="634b0-148">These outputs can help you determine whether all properties returned as expected.</span><span class="sxs-lookup"><span data-stu-id="634b0-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="634b0-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="634b0-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Trigger output examples][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="634b0-151">Action inputs and outputs</span><span class="sxs-lookup"><span data-stu-id="634b0-151">Action inputs and outputs</span></span>

<span data-ttu-id="634b0-152">You can drill into the inputs and outputs that an action received.</span><span class="sxs-lookup"><span data-stu-id="634b0-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="634b0-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span><span class="sxs-lookup"><span data-stu-id="634b0-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Action inputs and outputs][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="634b0-155">Debug workflow runtime</span><span class="sxs-lookup"><span data-stu-id="634b0-155">Debug workflow runtime</span></span>

<span data-ttu-id="634b0-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span><span class="sxs-lookup"><span data-stu-id="634b0-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="634b0-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span><span class="sxs-lookup"><span data-stu-id="634b0-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="634b0-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="634b0-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="634b0-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span><span class="sxs-lookup"><span data-stu-id="634b0-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="634b0-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span><span class="sxs-lookup"><span data-stu-id="634b0-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-diagnosing-failures/runhistory.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-diagnosing-failures/actionoutputs.png




