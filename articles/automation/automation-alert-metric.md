---
title: Monitor Azure Automation runbooks with metric alerts
description: This article walks you through monitoring Azure Automation runbooks based off of metrics
services: automation
ms.service: automation
author: georgewallace
ms.author: gwallace
ms.date: 05/17/2018
ms.topic: article
manager: carmonm
ms.openlocfilehash: a8a4b24e6b2503f64cc3fd7f4fd8c7400c547d4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965581"
---
# <a name="monitoring-runbooks-with-metric-alerts"></a><span data-ttu-id="b1476-103">Monitoring runbooks with metric alerts</span><span class="sxs-lookup"><span data-stu-id="b1476-103">Monitoring runbooks with metric alerts</span></span>

<span data-ttu-id="b1476-104">In this article, you learn how to create alerts based on the completion status of runbooks.</span><span class="sxs-lookup"><span data-stu-id="b1476-104">In this article, you learn how to create alerts based on the completion status of runbooks.</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="b1476-105">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="b1476-105">Log in to Azure</span></span>

<span data-ttu-id="b1476-106">Log in to Azure at https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b1476-106">Log in to Azure at https://portal.azure.com</span></span>

## <a name="create-alert"></a><span data-ttu-id="b1476-107">Create alert</span><span class="sxs-lookup"><span data-stu-id="b1476-107">Create alert</span></span>

<span data-ttu-id="b1476-108">Alerts allow you to define a condition to monitor for and an action to take when that condition is met.</span><span class="sxs-lookup"><span data-stu-id="b1476-108">Alerts allow you to define a condition to monitor for and an action to take when that condition is met.</span></span>

<span data-ttu-id="b1476-109">In the Azure portal, navigate to **All services** and select **Monitor**.</span><span class="sxs-lookup"><span data-stu-id="b1476-109">In the Azure portal, navigate to **All services** and select **Monitor**.</span></span> <span data-ttu-id="b1476-110">On the Monitor page, select **Alerts** and click **+ New Alert Rule**.</span><span class="sxs-lookup"><span data-stu-id="b1476-110">On the Monitor page, select **Alerts** and click **+ New Alert Rule**.</span></span>

### <a name="define-the-alert-condition"></a><span data-ttu-id="b1476-111">Define the alert condition</span><span class="sxs-lookup"><span data-stu-id="b1476-111">Define the alert condition</span></span>

1. <span data-ttu-id="b1476-112">Under **1. Define alert condition**, click **+  Select target**.</span><span class="sxs-lookup"><span data-stu-id="b1476-112">Under **1. Define alert condition**, click **+  Select target**.</span></span> <span data-ttu-id="b1476-113">Choose your subscription, and under **Filter by resource type**, select **Automation Accounts**.</span><span class="sxs-lookup"><span data-stu-id="b1476-113">Choose your subscription, and under **Filter by resource type**, select **Automation Accounts**.</span></span> <span data-ttu-id="b1476-114">Choose your Automation Account and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b1476-114">Choose your Automation Account and click **Done**.</span></span>

   ![Select a resource for the alert](./media/automation-alert-activity-log/select-resource.png)

### <a name="configure-alert-criteria"></a><span data-ttu-id="b1476-116">Configure alert criteria</span><span class="sxs-lookup"><span data-stu-id="b1476-116">Configure alert criteria</span></span>

1. <span data-ttu-id="b1476-117">Click **+ Add criteria**.</span><span class="sxs-lookup"><span data-stu-id="b1476-117">Click **+ Add criteria**.</span></span> <span data-ttu-id="b1476-118">Select **Metrics** for the **Signal type**, and choose **Total Jobs** from the table.</span><span class="sxs-lookup"><span data-stu-id="b1476-118">Select **Metrics** for the **Signal type**, and choose **Total Jobs** from the table.</span></span>

1. <span data-ttu-id="b1476-119">The **Configure signal logic** page is where you define the logic that triggers the alert.</span><span class="sxs-lookup"><span data-stu-id="b1476-119">The **Configure signal logic** page is where you define the logic that triggers the alert.</span></span> <span data-ttu-id="b1476-120">Under the historical graph you are presented with two dimensions, **Runbook Name** and **Status**.</span><span class="sxs-lookup"><span data-stu-id="b1476-120">Under the historical graph you are presented with two dimensions, **Runbook Name** and **Status**.</span></span> <span data-ttu-id="b1476-121">Dimensions are different properties for a metric that can be used to filter results.</span><span class="sxs-lookup"><span data-stu-id="b1476-121">Dimensions are different properties for a metric that can be used to filter results.</span></span> <span data-ttu-id="b1476-122">For **Runbook Name**, select the runbook you want to alert on or leave blank to alert on all runbooks.</span><span class="sxs-lookup"><span data-stu-id="b1476-122">For **Runbook Name**, select the runbook you want to alert on or leave blank to alert on all runbooks.</span></span> <span data-ttu-id="b1476-123">For **Status**, select a status from the drop-down you want to monitor for.</span><span class="sxs-lookup"><span data-stu-id="b1476-123">For **Status**, select a status from the drop-down you want to monitor for.</span></span> <span data-ttu-id="b1476-124">The runbook name and status values that appear in the dropdown are only for jobs that have ran in the past week.</span><span class="sxs-lookup"><span data-stu-id="b1476-124">The runbook name and status values that appear in the dropdown are only for jobs that have ran in the past week.</span></span>

   <span data-ttu-id="b1476-125">If you want to alert on a status or runbook that is not shown in the dropdown, click the **\+** next to the dimension.</span><span class="sxs-lookup"><span data-stu-id="b1476-125">If you want to alert on a status or runbook that is not shown in the dropdown, click the **\+** next to the dimension.</span></span> <span data-ttu-id="b1476-126">This opens a dialog that allows you to enter in a custom value, which has not emitted for that dimension recently.</span><span class="sxs-lookup"><span data-stu-id="b1476-126">This opens a dialog that allows you to enter in a custom value, which has not emitted for that dimension recently.</span></span> <span data-ttu-id="b1476-127">If you enter a value that doesn't exist for a property your alert will not be triggered.</span><span class="sxs-lookup"><span data-stu-id="b1476-127">If you enter a value that doesn't exist for a property your alert will not be triggered.</span></span>

1. <span data-ttu-id="b1476-128">Under **Alert logic**, define the condition and threshold for your alert.</span><span class="sxs-lookup"><span data-stu-id="b1476-128">Under **Alert logic**, define the condition and threshold for your alert.</span></span> <span data-ttu-id="b1476-129">A preview of your condition defined is shown underneath.</span><span class="sxs-lookup"><span data-stu-id="b1476-129">A preview of your condition defined is shown underneath.</span></span>

1. <span data-ttu-id="b1476-130">Under **Evaluated based on** select the timespan for the query and how often you want that query ran.</span><span class="sxs-lookup"><span data-stu-id="b1476-130">Under **Evaluated based on** select the timespan for the query and how often you want that query ran.</span></span> <span data-ttu-id="b1476-131">For example, if you choose **Over the last 5 minutes** for **Period** and **Every 1 Minute** for **Frequency**, the alert looks for the number of runbooks that met your criteria over the past 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="b1476-131">For example, if you choose **Over the last 5 minutes** for **Period** and **Every 1 Minute** for **Frequency**, the alert looks for the number of runbooks that met your criteria over the past 5 minutes.</span></span> <span data-ttu-id="b1476-132">This query is ran every minute, and once the alert criteria you defined is no longer found in a 5-minute window, the alert resolves itself.</span><span class="sxs-lookup"><span data-stu-id="b1476-132">This query is ran every minute, and once the alert criteria you defined is no longer found in a 5-minute window, the alert resolves itself.</span></span> <span data-ttu-id="b1476-133">When finished, click **Done**.</span><span class="sxs-lookup"><span data-stu-id="b1476-133">When finished, click **Done**.</span></span>

   ![Select a resource for the alert](./media/automation-alert-activity-log/configure-signal-logic.png)

### <a name="define-alert-details"></a><span data-ttu-id="b1476-135">Define alert details</span><span class="sxs-lookup"><span data-stu-id="b1476-135">Define alert details</span></span>

1. <span data-ttu-id="b1476-136">Under **2. Define alert details**, give the alert a friendly name and description.</span><span class="sxs-lookup"><span data-stu-id="b1476-136">Under **2. Define alert details**, give the alert a friendly name and description.</span></span> <span data-ttu-id="b1476-137">Set the **Severity** to match your alert condition.</span><span class="sxs-lookup"><span data-stu-id="b1476-137">Set the **Severity** to match your alert condition.</span></span> <span data-ttu-id="b1476-138">There are five severities ranging from 0 to 5.</span><span class="sxs-lookup"><span data-stu-id="b1476-138">There are five severities ranging from 0 to 5.</span></span> <span data-ttu-id="b1476-139">The alerts are treated the same independent of the severity, you can match the severity to match your business logic.</span><span class="sxs-lookup"><span data-stu-id="b1476-139">The alerts are treated the same independent of the severity, you can match the severity to match your business logic.</span></span>

1. <span data-ttu-id="b1476-140">At the bottom of the section is a button that allows you to enable the rule upon completion.</span><span class="sxs-lookup"><span data-stu-id="b1476-140">At the bottom of the section is a button that allows you to enable the rule upon completion.</span></span> <span data-ttu-id="b1476-141">By default rules are enabled at creation.</span><span class="sxs-lookup"><span data-stu-id="b1476-141">By default rules are enabled at creation.</span></span> <span data-ttu-id="b1476-142">If you select No, you can create the alert and it is created in a **Disabled** state.</span><span class="sxs-lookup"><span data-stu-id="b1476-142">If you select No, you can create the alert and it is created in a **Disabled** state.</span></span> <span data-ttu-id="b1476-143">From the **Rules** page in Azure Monitor, you can select it and click **Enable** to enable the alert when you are ready.</span><span class="sxs-lookup"><span data-stu-id="b1476-143">From the **Rules** page in Azure Monitor, you can select it and click **Enable** to enable the alert when you are ready.</span></span>

### <a name="define-the-action-to-take"></a><span data-ttu-id="b1476-144">Define the action to take</span><span class="sxs-lookup"><span data-stu-id="b1476-144">Define the action to take</span></span>

1. <span data-ttu-id="b1476-145">Under **3. Define action group**, click **+ New action group**.</span><span class="sxs-lookup"><span data-stu-id="b1476-145">Under **3. Define action group**, click **+ New action group**.</span></span> <span data-ttu-id="b1476-146">An action group is a group of actions that you can use across multiple alerts.</span><span class="sxs-lookup"><span data-stu-id="b1476-146">An action group is a group of actions that you can use across multiple alerts.</span></span> <span data-ttu-id="b1476-147">These can include but are not limited to, email notifications, runbooks, webhooks, and many more.</span><span class="sxs-lookup"><span data-stu-id="b1476-147">These can include but are not limited to, email notifications, runbooks, webhooks, and many more.</span></span> <span data-ttu-id="b1476-148">To learn more about action groups, see [Create and manage action groups](../monitoring-and-diagnostics/monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="b1476-148">To learn more about action groups, see [Create and manage action groups](../monitoring-and-diagnostics/monitoring-action-groups.md)</span></span>

1. <span data-ttu-id="b1476-149">In the **Action group name** box, give it a friendly name and short name.</span><span class="sxs-lookup"><span data-stu-id="b1476-149">In the **Action group name** box, give it a friendly name and short name.</span></span> <span data-ttu-id="b1476-150">The short name is used in place of a full action group name when notifications are sent using this group.</span><span class="sxs-lookup"><span data-stu-id="b1476-150">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

1. <span data-ttu-id="b1476-151">In the **Actions** section under **ACTION TYPE**, select **Email/SMS/Push/Voice**.</span><span class="sxs-lookup"><span data-stu-id="b1476-151">In the **Actions** section under **ACTION TYPE**, select **Email/SMS/Push/Voice**.</span></span>

1. <span data-ttu-id="b1476-152">On the **Email/SMS/Push/Voice** page, give it a name.</span><span class="sxs-lookup"><span data-stu-id="b1476-152">On the **Email/SMS/Push/Voice** page, give it a name.</span></span> <span data-ttu-id="b1476-153">Check the **Email** checkbox and enter in a valid email address to be used.</span><span class="sxs-lookup"><span data-stu-id="b1476-153">Check the **Email** checkbox and enter in a valid email address to be used.</span></span>

   ![Configure email action group](./media/automation-alert-activity-log/add-action-group.png)

1. <span data-ttu-id="b1476-155">Click **OK** on the **Email/SMS/Push/Voice** page to close it and click **OK** to close the **Add action group** page.</span><span class="sxs-lookup"><span data-stu-id="b1476-155">Click **OK** on the **Email/SMS/Push/Voice** page to close it and click **OK** to close the **Add action group** page.</span></span> <span data-ttu-id="b1476-156">The Name specified in this page is saved as the **ACTION NAME**.</span><span class="sxs-lookup"><span data-stu-id="b1476-156">The Name specified in this page is saved as the **ACTION NAME**.</span></span>

1. <span data-ttu-id="b1476-157">When complete, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b1476-157">When complete, click **Save**.</span></span> <span data-ttu-id="b1476-158">This creates the rule that alerts you when a runbook completed with a certain status.</span><span class="sxs-lookup"><span data-stu-id="b1476-158">This creates the rule that alerts you when a runbook completed with a certain status.</span></span>

> [!NOTE]
> <span data-ttu-id="b1476-159">When adding an email address to an Action Group, a notification email is sent stating the address has been added to an Action Group.</span><span class="sxs-lookup"><span data-stu-id="b1476-159">When adding an email address to an Action Group, a notification email is sent stating the address has been added to an Action Group.</span></span>

## <a name="notification"></a><span data-ttu-id="b1476-160">Notification</span><span class="sxs-lookup"><span data-stu-id="b1476-160">Notification</span></span>

<span data-ttu-id="b1476-161">When the alert criteria is met, the action group runs the action defined.</span><span class="sxs-lookup"><span data-stu-id="b1476-161">When the alert criteria is met, the action group runs the action defined.</span></span> <span data-ttu-id="b1476-162">In this article's example, an email is sent.</span><span class="sxs-lookup"><span data-stu-id="b1476-162">In this article's example, an email is sent.</span></span> <span data-ttu-id="b1476-163">The following image is an example of an email you receive after the alert is triggered:</span><span class="sxs-lookup"><span data-stu-id="b1476-163">The following image is an example of an email you receive after the alert is triggered:</span></span>

![Email alert](./media/automation-alert-activity-log/alert-email.png)

<span data-ttu-id="b1476-165">Once the metric is no longer outside of the threshold defined, the alert is deactivated and the action group runs the action defined.</span><span class="sxs-lookup"><span data-stu-id="b1476-165">Once the metric is no longer outside of the threshold defined, the alert is deactivated and the action group runs the action defined.</span></span> <span data-ttu-id="b1476-166">If an email action type is selected, a resolution email is sent stating it has been resolved.</span><span class="sxs-lookup"><span data-stu-id="b1476-166">If an email action type is selected, a resolution email is sent stating it has been resolved.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1476-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1476-167">Next steps</span></span>

<span data-ttu-id="b1476-168">Continue to the following article to learn about other ways that you can integrate alertings into your Automation Account.</span><span class="sxs-lookup"><span data-stu-id="b1476-168">Continue to the following article to learn about other ways that you can integrate alertings into your Automation Account.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1476-169">Use an alert to trigger an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="b1476-169">Use an alert to trigger an Azure Automation runbook</span></span>](automation-create-alert-triggered-runbook.md)