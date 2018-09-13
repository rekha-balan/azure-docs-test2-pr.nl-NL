---
title: Troubleshoot and diagnose failures - Azure Logic Apps | Microsoft Docs
description: Learn how to troubleshoot and diagnose workflow failures in Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: ecfan
ms.author: estfan
ms.reviewer: klam, jehollan, LADocs
ms.topic: article
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.date: 10/15/2017
ms.openlocfilehash: 994e7945a7107815029bd415f4cc0d45bb68e335
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818160"
---
# <a name="troubleshoot-and-diagnose-workflow-failures-in-azure-logic-apps"></a><span data-ttu-id="881a8-103">Troubleshoot and diagnose workflow failures in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="881a8-103">Troubleshoot and diagnose workflow failures in Azure Logic Apps</span></span>

<span data-ttu-id="881a8-104">Your logic app generates information that can help you diagnose and debug problems in your app.</span><span class="sxs-lookup"><span data-stu-id="881a8-104">Your logic app generates information that can help you diagnose and debug problems in your app.</span></span> <span data-ttu-id="881a8-105">You can diagnose a logic app by reviewing each step in the workflow through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="881a8-105">You can diagnose a logic app by reviewing each step in the workflow through the Azure portal.</span></span> <span data-ttu-id="881a8-106">Or you can add some steps to a workflow for runtime debugging.</span><span class="sxs-lookup"><span data-stu-id="881a8-106">Or you can add some steps to a workflow for runtime debugging.</span></span>

## <a name="review-trigger-history"></a><span data-ttu-id="881a8-107">Review trigger history</span><span class="sxs-lookup"><span data-stu-id="881a8-107">Review trigger history</span></span>

<span data-ttu-id="881a8-108">Each logic app starts with trigger.</span><span class="sxs-lookup"><span data-stu-id="881a8-108">Each logic app starts with trigger.</span></span> <span data-ttu-id="881a8-109">If the trigger doesn't fire, first check the trigger history.</span><span class="sxs-lookup"><span data-stu-id="881a8-109">If the trigger doesn't fire, first check the trigger history.</span></span> <span data-ttu-id="881a8-110">This history lists all the trigger attempts that your logic app made and details about inputs and outputs for each trigger attempt.</span><span class="sxs-lookup"><span data-stu-id="881a8-110">This history lists all the trigger attempts that your logic app made and details about inputs and outputs for each trigger attempt.</span></span>

1. <span data-ttu-id="881a8-111">To check whether the trigger fired, on your logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="881a8-111">To check whether the trigger fired, on your logic app menu, choose **Overview**.</span></span> <span data-ttu-id="881a8-112">Under **Trigger History**, review the trigger's status.</span><span class="sxs-lookup"><span data-stu-id="881a8-112">Under **Trigger History**, review the trigger's status.</span></span>

   > [!TIP]
   > <span data-ttu-id="881a8-113">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span><span class="sxs-lookup"><span data-stu-id="881a8-113">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span></span>

   ![Review trigger history](./media/logic-apps-diagnosing-failures/logic-app-trigger-history-overview.png)

   > [!TIP]
   > * <span data-ttu-id="881a8-115">If you don't find the data that you expect, try selecting **Refresh** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="881a8-115">If you don't find the data that you expect, try selecting **Refresh** on the toolbar.</span></span>
   > * <span data-ttu-id="881a8-116">If the list shows many trigger attempts, and you can't find the entry you want, try filtering the list.</span><span class="sxs-lookup"><span data-stu-id="881a8-116">If the list shows many trigger attempts, and you can't find the entry you want, try filtering the list.</span></span>

   <span data-ttu-id="881a8-117">Here are the possible statuses for a trigger attempt:</span><span class="sxs-lookup"><span data-stu-id="881a8-117">Here are the possible statuses for a trigger attempt:</span></span>

   | <span data-ttu-id="881a8-118">Status</span><span class="sxs-lookup"><span data-stu-id="881a8-118">Status</span></span> | <span data-ttu-id="881a8-119">Description</span><span class="sxs-lookup"><span data-stu-id="881a8-119">Description</span></span> | 
   | ------ | ----------- | 
   | <span data-ttu-id="881a8-120">**Succeeded**</span><span class="sxs-lookup"><span data-stu-id="881a8-120">**Succeeded**</span></span> | <span data-ttu-id="881a8-121">The trigger checked the endpoint and found available data.</span><span class="sxs-lookup"><span data-stu-id="881a8-121">The trigger checked the endpoint and found available data.</span></span> <span data-ttu-id="881a8-122">Usually, a "Fired" status also appears alongside this status.</span><span class="sxs-lookup"><span data-stu-id="881a8-122">Usually, a "Fired" status also appears alongside this status.</span></span> <span data-ttu-id="881a8-123">If not, the trigger definition might have a condition or `SplitOn` command that wasn't met.</span><span class="sxs-lookup"><span data-stu-id="881a8-123">If not, the trigger definition might have a condition or `SplitOn` command that wasn't met.</span></span> <p><span data-ttu-id="881a8-124">This status can apply to a manual trigger, recurrence trigger, or polling trigger.</span><span class="sxs-lookup"><span data-stu-id="881a8-124">This status can apply to a manual trigger, recurrence trigger, or polling trigger.</span></span> <span data-ttu-id="881a8-125">A trigger can run successfully, but the run itself might still fail when the actions generate unhandled errors.</span><span class="sxs-lookup"><span data-stu-id="881a8-125">A trigger can run successfully, but the run itself might still fail when the actions generate unhandled errors.</span></span> | 
   | <span data-ttu-id="881a8-126">**Skipped**</span><span class="sxs-lookup"><span data-stu-id="881a8-126">**Skipped**</span></span> | <span data-ttu-id="881a8-127">The trigger checked the endpoint but found no data.</span><span class="sxs-lookup"><span data-stu-id="881a8-127">The trigger checked the endpoint but found no data.</span></span> | 
   | <span data-ttu-id="881a8-128">**Failed**</span><span class="sxs-lookup"><span data-stu-id="881a8-128">**Failed**</span></span> | <span data-ttu-id="881a8-129">An error occurred.</span><span class="sxs-lookup"><span data-stu-id="881a8-129">An error occurred.</span></span> <span data-ttu-id="881a8-130">To review any generated error messages for a failed trigger, select that trigger attempt and choose **Outputs**.</span><span class="sxs-lookup"><span data-stu-id="881a8-130">To review any generated error messages for a failed trigger, select that trigger attempt and choose **Outputs**.</span></span> <span data-ttu-id="881a8-131">For example, you might find inputs that aren't valid.</span><span class="sxs-lookup"><span data-stu-id="881a8-131">For example, you might find inputs that aren't valid.</span></span> | 
   ||| 

   <span data-ttu-id="881a8-132">You might have multiple trigger entries with the same date and time, which happens when your logic app finds multiple items.</span><span class="sxs-lookup"><span data-stu-id="881a8-132">You might have multiple trigger entries with the same date and time, which happens when your logic app finds multiple items.</span></span> 
   <span data-ttu-id="881a8-133">Each time the trigger fires, the Logic Apps engine creates a logic app instance to run your workflow.</span><span class="sxs-lookup"><span data-stu-id="881a8-133">Each time the trigger fires, the Logic Apps engine creates a logic app instance to run your workflow.</span></span> <span data-ttu-id="881a8-134">By default, each instance runs in parallel so that no workflow has to wait before starting a run.</span><span class="sxs-lookup"><span data-stu-id="881a8-134">By default, each instance runs in parallel so that no workflow has to wait before starting a run.</span></span>

   > [!TIP]
   > <span data-ttu-id="881a8-135">You can recheck the trigger without waiting for the next recurrence.</span><span class="sxs-lookup"><span data-stu-id="881a8-135">You can recheck the trigger without waiting for the next recurrence.</span></span> <span data-ttu-id="881a8-136">On the overview toolbar, choose **Run trigger**, and select the trigger, which forces a check.</span><span class="sxs-lookup"><span data-stu-id="881a8-136">On the overview toolbar, choose **Run trigger**, and select the trigger, which forces a check.</span></span> <span data-ttu-id="881a8-137">Or, select **Run** on Logic Apps Designer toolbar.</span><span class="sxs-lookup"><span data-stu-id="881a8-137">Or, select **Run** on Logic Apps Designer toolbar.</span></span>

3. <span data-ttu-id="881a8-138">To examine the details for a trigger attempt, under **Trigger History**, select that trigger attempt.</span><span class="sxs-lookup"><span data-stu-id="881a8-138">To examine the details for a trigger attempt, under **Trigger History**, select that trigger attempt.</span></span> 

   ![Select a trigger attempt](./media/logic-apps-diagnosing-failures/logic-app-trigger-history.png)

4. <span data-ttu-id="881a8-140">Review the inputs and any outputs that the trigger generated.</span><span class="sxs-lookup"><span data-stu-id="881a8-140">Review the inputs and any outputs that the trigger generated.</span></span> <span data-ttu-id="881a8-141">Trigger outputs show the data that came from the trigger.</span><span class="sxs-lookup"><span data-stu-id="881a8-141">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="881a8-142">These outputs can help you determine whether all properties returned as expected.</span><span class="sxs-lookup"><span data-stu-id="881a8-142">These outputs can help you determine whether all properties returned as expected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="881a8-143">If you find any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="881a8-143">If you find any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>

   ![Trigger outputs](./media/logic-apps-diagnosing-failures/trigger-outputs.png)

## <a name="review-run-history"></a><span data-ttu-id="881a8-145">Review run history</span><span class="sxs-lookup"><span data-stu-id="881a8-145">Review run history</span></span>

<span data-ttu-id="881a8-146">Each fired trigger starts a workflow run.</span><span class="sxs-lookup"><span data-stu-id="881a8-146">Each fired trigger starts a workflow run.</span></span> <span data-ttu-id="881a8-147">You can review what happened during that run, including the status for each step in the workflow, plus the inputs and outputs for each step.</span><span class="sxs-lookup"><span data-stu-id="881a8-147">You can review what happened during that run, including the status for each step in the workflow, plus the inputs and outputs for each step.</span></span>

1. <span data-ttu-id="881a8-148">On the logic app menu, choose **Overview**.</span><span class="sxs-lookup"><span data-stu-id="881a8-148">On the logic app menu, choose **Overview**.</span></span> <span data-ttu-id="881a8-149">Under **Runs history**, review the run for the fired trigger.</span><span class="sxs-lookup"><span data-stu-id="881a8-149">Under **Runs history**, review the run for the fired trigger.</span></span>

   > [!TIP]
   > <span data-ttu-id="881a8-150">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span><span class="sxs-lookup"><span data-stu-id="881a8-150">If you don't see the logic app menu, try returning to the Azure dashboard, and reopen your logic app.</span></span>

   ![Review runs history](./media/logic-apps-diagnosing-failures/logic-app-runs-history-overview.png)

   > [!TIP]
   > * <span data-ttu-id="881a8-152">If you don't find the data that you expect, try selecting **Refresh** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="881a8-152">If you don't find the data that you expect, try selecting **Refresh** on the toolbar.</span></span>
   > * <span data-ttu-id="881a8-153">If the list shows many runs, and you can't find the entry you want, try filtering the list.</span><span class="sxs-lookup"><span data-stu-id="881a8-153">If the list shows many runs, and you can't find the entry you want, try filtering the list.</span></span>

   <span data-ttu-id="881a8-154">Here are the possible statuses for a run:</span><span class="sxs-lookup"><span data-stu-id="881a8-154">Here are the possible statuses for a run:</span></span>

   | <span data-ttu-id="881a8-155">Status</span><span class="sxs-lookup"><span data-stu-id="881a8-155">Status</span></span> | <span data-ttu-id="881a8-156">Description</span><span class="sxs-lookup"><span data-stu-id="881a8-156">Description</span></span> | 
   | ------ | ----------- | 
   | <span data-ttu-id="881a8-157">**Succeeded**</span><span class="sxs-lookup"><span data-stu-id="881a8-157">**Succeeded**</span></span> | <span data-ttu-id="881a8-158">All actions succeeded.</span><span class="sxs-lookup"><span data-stu-id="881a8-158">All actions succeeded.</span></span> <p><span data-ttu-id="881a8-159">If any failures happened in a specific action, a following action in the workflow handled that failure.</span><span class="sxs-lookup"><span data-stu-id="881a8-159">If any failures happened in a specific action, a following action in the workflow handled that failure.</span></span> | 
   | <span data-ttu-id="881a8-160">**Failed**</span><span class="sxs-lookup"><span data-stu-id="881a8-160">**Failed**</span></span> | <span data-ttu-id="881a8-161">At least one action failed, and no later actions in the workflow were set up to handle the failure.</span><span class="sxs-lookup"><span data-stu-id="881a8-161">At least one action failed, and no later actions in the workflow were set up to handle the failure.</span></span> | 
   | <span data-ttu-id="881a8-162">**Cancelled**</span><span class="sxs-lookup"><span data-stu-id="881a8-162">**Cancelled**</span></span> | <span data-ttu-id="881a8-163">The workflow was running but received a cancel request.</span><span class="sxs-lookup"><span data-stu-id="881a8-163">The workflow was running but received a cancel request.</span></span> | 
   | <span data-ttu-id="881a8-164">**Running**</span><span class="sxs-lookup"><span data-stu-id="881a8-164">**Running**</span></span> | <span data-ttu-id="881a8-165">The workflow is currently running.</span><span class="sxs-lookup"><span data-stu-id="881a8-165">The workflow is currently running.</span></span> <p><span data-ttu-id="881a8-166">This status might happen for throttled workflows, or due to the current pricing plan.</span><span class="sxs-lookup"><span data-stu-id="881a8-166">This status might happen for throttled workflows, or due to the current pricing plan.</span></span> <span data-ttu-id="881a8-167">For more information, see the [action limits on the pricing page](https://azure.microsoft.com/pricing/details/logic-apps/).</span><span class="sxs-lookup"><span data-stu-id="881a8-167">For more information, see the [action limits on the pricing page](https://azure.microsoft.com/pricing/details/logic-apps/).</span></span> <span data-ttu-id="881a8-168">If you set up [diagnostics logging](../logic-apps/logic-apps-monitor-your-logic-apps.md), you can also get information about any throttle events that happen.</span><span class="sxs-lookup"><span data-stu-id="881a8-168">If you set up [diagnostics logging](../logic-apps/logic-apps-monitor-your-logic-apps.md), you can also get information about any throttle events that happen.</span></span> | 
   ||| 

2. <span data-ttu-id="881a8-169">Review the details for each step in a specific run.</span><span class="sxs-lookup"><span data-stu-id="881a8-169">Review the details for each step in a specific run.</span></span> <span data-ttu-id="881a8-170">Under **Runs history**, select the run that you want to examine.</span><span class="sxs-lookup"><span data-stu-id="881a8-170">Under **Runs history**, select the run that you want to examine.</span></span>

   ![Review runs history](./media/logic-apps-diagnosing-failures/logic-app-run-history.png)

   <span data-ttu-id="881a8-172">Whether the run itself succeeded or failed, the Run Details view shows each step and whether they succeeded or failed.</span><span class="sxs-lookup"><span data-stu-id="881a8-172">Whether the run itself succeeded or failed, the Run Details view shows each step and whether they succeeded or failed.</span></span>

   ![View details for a logic app run](./media/logic-apps-diagnosing-failures/logic-app-run-details.png)

3. <span data-ttu-id="881a8-174">To examine the inputs, outputs, and any error messages for a specific step, choose that step so that the shape expands and shows the details.</span><span class="sxs-lookup"><span data-stu-id="881a8-174">To examine the inputs, outputs, and any error messages for a specific step, choose that step so that the shape expands and shows the details.</span></span> <span data-ttu-id="881a8-175">For example:</span><span class="sxs-lookup"><span data-stu-id="881a8-175">For example:</span></span>

   ![View step details](./media/logic-apps-diagnosing-failures/logic-app-run-details-expanded.png)

## <a name="perform-runtime-debugging"></a><span data-ttu-id="881a8-177">Perform runtime debugging</span><span class="sxs-lookup"><span data-stu-id="881a8-177">Perform runtime debugging</span></span>

<span data-ttu-id="881a8-178">To help with debugging, you can add diagnostic steps to a workflow, along with reviewing the trigger and runs history.</span><span class="sxs-lookup"><span data-stu-id="881a8-178">To help with debugging, you can add diagnostic steps to a workflow, along with reviewing the trigger and runs history.</span></span> <span data-ttu-id="881a8-179">For example, you can add steps that use the [Webhook Tester](https://webhook.site/) service so that you can inspect HTTP requests and determine their exact size, shape, and format.</span><span class="sxs-lookup"><span data-stu-id="881a8-179">For example, you can add steps that use the [Webhook Tester](https://webhook.site/) service so that you can inspect HTTP requests and determine their exact size, shape, and format.</span></span>

1. <span data-ttu-id="881a8-180">Visit [Webhook Tester](https://webhook.site/) and copy the unique URL created</span><span class="sxs-lookup"><span data-stu-id="881a8-180">Visit [Webhook Tester](https://webhook.site/) and copy the unique URL created</span></span>

2. <span data-ttu-id="881a8-181">In your logic app, add an HTTP POST action with the body content that you want to test, for example, an expression or another step output.</span><span class="sxs-lookup"><span data-stu-id="881a8-181">In your logic app, add an HTTP POST action with the body content that you want to test, for example, an expression or another step output.</span></span>

3. <span data-ttu-id="881a8-182">Paste the URL for your Webhook Tester into the HTTP POST action.</span><span class="sxs-lookup"><span data-stu-id="881a8-182">Paste the URL for your Webhook Tester into the HTTP POST action.</span></span>

4. <span data-ttu-id="881a8-183">To review how a request is formed when generated from the Logic Apps engine, run the logic app, and see Webhook Tester for details.</span><span class="sxs-lookup"><span data-stu-id="881a8-183">To review how a request is formed when generated from the Logic Apps engine, run the logic app, and see Webhook Tester for details.</span></span>

## <a name="next-steps"></a><span data-ttu-id="881a8-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="881a8-184">Next steps</span></span>

[<span data-ttu-id="881a8-185">Monitor your logic app</span><span class="sxs-lookup"><span data-stu-id="881a8-185">Monitor your logic app</span></span>](../logic-apps/logic-apps-monitor-your-logic-apps.md)
