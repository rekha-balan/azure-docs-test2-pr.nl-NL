---
title: Manage updates and patches for your Azure Windows VMs
description: This article provides an overview of how to use Azure Automation Update Management to manage updates and patches for your Azure Windows VMs.
services: automation
author: zjalexander
ms.service: automation
ms.component: update-management
ms.topic: tutorial
ms.date: 08/29/2018
ms.author: zachal
ms.custom: mvc
ms.openlocfilehash: 8458aaee9f8d328d959fb47fb3e32af176d545b1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870832"
---
# <a name="manage-windows-updates-by-using-azure-automation"></a><span data-ttu-id="39bdd-103">Manage Windows updates by using Azure Automation</span><span class="sxs-lookup"><span data-stu-id="39bdd-103">Manage Windows updates by using Azure Automation</span></span>

<span data-ttu-id="39bdd-104">You can use the Update Management solution to manage updates and patches for your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="39bdd-104">You can use the Update Management solution to manage updates and patches for your virtual machines.</span></span> <span data-ttu-id="39bdd-105">In this tutorial, you learn how to quickly assess the status of available updates, schedule installation of required updates, review deployment results, and create an alert to verify that updates apply successfully.</span><span class="sxs-lookup"><span data-stu-id="39bdd-105">In this tutorial, you learn how to quickly assess the status of available updates, schedule installation of required updates, review deployment results, and create an alert to verify that updates apply successfully.</span></span>

<span data-ttu-id="39bdd-106">For pricing information, see [Automation pricing for Update Management](https://azure.microsoft.com/pricing/details/automation/).</span><span class="sxs-lookup"><span data-stu-id="39bdd-106">For pricing information, see [Automation pricing for Update Management](https://azure.microsoft.com/pricing/details/automation/).</span></span>

<span data-ttu-id="39bdd-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="39bdd-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39bdd-108">Onboard a VM for Update Management</span><span class="sxs-lookup"><span data-stu-id="39bdd-108">Onboard a VM for Update Management</span></span>
> * <span data-ttu-id="39bdd-109">View an update assessment</span><span class="sxs-lookup"><span data-stu-id="39bdd-109">View an update assessment</span></span>
> * <span data-ttu-id="39bdd-110">Configure alerting</span><span class="sxs-lookup"><span data-stu-id="39bdd-110">Configure alerting</span></span>
> * <span data-ttu-id="39bdd-111">Schedule an update deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-111">Schedule an update deployment</span></span>
> * <span data-ttu-id="39bdd-112">View the results of a deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-112">View the results of a deployment</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39bdd-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39bdd-113">Prerequisites</span></span>

<span data-ttu-id="39bdd-114">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="39bdd-114">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="39bdd-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="39bdd-115">An Azure subscription.</span></span> <span data-ttu-id="39bdd-116">If you don't have one yet, you can [activate your monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="39bdd-116">If you don't have one yet, you can [activate your monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="39bdd-117">An [Azure Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span><span class="sxs-lookup"><span data-stu-id="39bdd-117">An [Azure Automation account](automation-offering-get-started.md) to hold the watcher and action runbooks and the Watcher Task.</span></span>
* <span data-ttu-id="39bdd-118">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span><span class="sxs-lookup"><span data-stu-id="39bdd-118">A [virtual machine](../virtual-machines/windows/quick-create-portal.md) to onboard.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="39bdd-119">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="39bdd-119">Sign in to Azure</span></span>

<span data-ttu-id="39bdd-120">Sign in to the Azure portal at https://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="39bdd-120">Sign in to the Azure portal at https://portal.azure.com.</span></span>

## <a name="enable-update-management"></a><span data-ttu-id="39bdd-121">Enable Update Management</span><span class="sxs-lookup"><span data-stu-id="39bdd-121">Enable Update Management</span></span>

<span data-ttu-id="39bdd-122">First, enable Update Management on your VM for this tutorial:</span><span class="sxs-lookup"><span data-stu-id="39bdd-122">First, enable Update Management on your VM for this tutorial:</span></span>

1. <span data-ttu-id="39bdd-123">In the Azure portal, in the left menu, select **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-123">In the Azure portal, in the left menu, select **Virtual machines**.</span></span> <span data-ttu-id="39bdd-124">Select a VM from the list.</span><span class="sxs-lookup"><span data-stu-id="39bdd-124">Select a VM from the list.</span></span>
2. <span data-ttu-id="39bdd-125">On the VM page, under **OPERATIONS**, select **Update management**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-125">On the VM page, under **OPERATIONS**, select **Update management**.</span></span> <span data-ttu-id="39bdd-126">The **Enable Update Management** pane opens.</span><span class="sxs-lookup"><span data-stu-id="39bdd-126">The **Enable Update Management** pane opens.</span></span>

<span data-ttu-id="39bdd-127">Validation is performed to determine whether Update Management is enabled for this VM.</span><span class="sxs-lookup"><span data-stu-id="39bdd-127">Validation is performed to determine whether Update Management is enabled for this VM.</span></span> <span data-ttu-id="39bdd-128">This validation includes checks for an Azure Log Analytics workspace and linked Automation account, and whether the Update Management solution is in the workspace.</span><span class="sxs-lookup"><span data-stu-id="39bdd-128">This validation includes checks for an Azure Log Analytics workspace and linked Automation account, and whether the Update Management solution is in the workspace.</span></span>

<span data-ttu-id="39bdd-129">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that's generated by features and services like Update Management.</span><span class="sxs-lookup"><span data-stu-id="39bdd-129">A [Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace is used to collect data that's generated by features and services like Update Management.</span></span> <span data-ttu-id="39bdd-130">The workspace provides a single location to review and analyze data from multiple sources.</span><span class="sxs-lookup"><span data-stu-id="39bdd-130">The workspace provides a single location to review and analyze data from multiple sources.</span></span>

<span data-ttu-id="39bdd-131">The validation process also checks to see whether the VM is provisioned with the Microsoft Monitoring Agent (MMA) and Automation Hybrid Runbook Worker.</span><span class="sxs-lookup"><span data-stu-id="39bdd-131">The validation process also checks to see whether the VM is provisioned with the Microsoft Monitoring Agent (MMA) and Automation Hybrid Runbook Worker.</span></span> <span data-ttu-id="39bdd-132">This agent is used to communicate with Azure Automation and to obtain information about the update status.</span><span class="sxs-lookup"><span data-stu-id="39bdd-132">This agent is used to communicate with Azure Automation and to obtain information about the update status.</span></span> <span data-ttu-id="39bdd-133">The agent requires port 443 to be open to communicate with the Azure Automation service and to download updates.</span><span class="sxs-lookup"><span data-stu-id="39bdd-133">The agent requires port 443 to be open to communicate with the Azure Automation service and to download updates.</span></span>

<span data-ttu-id="39bdd-134">If any of the following prerequisites were found to be missing during onboarding, they're automatically added:</span><span class="sxs-lookup"><span data-stu-id="39bdd-134">If any of the following prerequisites were found to be missing during onboarding, they're automatically added:</span></span>

* <span data-ttu-id="39bdd-135">[Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace</span><span class="sxs-lookup"><span data-stu-id="39bdd-135">[Log Analytics](../log-analytics/log-analytics-overview.md?toc=%2fazure%2fautomation%2ftoc.json) workspace</span></span>
* <span data-ttu-id="39bdd-136">An [Automation account](./automation-offering-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="39bdd-136">An [Automation account](./automation-offering-get-started.md)</span></span>
* <span data-ttu-id="39bdd-137">A [Hybrid Runbook Worker](./automation-hybrid-runbook-worker.md) (enabled on the VM)</span><span class="sxs-lookup"><span data-stu-id="39bdd-137">A [Hybrid Runbook Worker](./automation-hybrid-runbook-worker.md) (enabled on the VM)</span></span>

<span data-ttu-id="39bdd-138">Under **Update Management**, set the location, Log Analytics workspace, and Automation account to use.</span><span class="sxs-lookup"><span data-stu-id="39bdd-138">Under **Update Management**, set the location, Log Analytics workspace, and Automation account to use.</span></span> <span data-ttu-id="39bdd-139">Then, select **Enable**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-139">Then, select **Enable**.</span></span> <span data-ttu-id="39bdd-140">If these options aren't available, it means that another automation solution is enabled for the VM.</span><span class="sxs-lookup"><span data-stu-id="39bdd-140">If these options aren't available, it means that another automation solution is enabled for the VM.</span></span> <span data-ttu-id="39bdd-141">In that case, the same workspace and Automation account must be used.</span><span class="sxs-lookup"><span data-stu-id="39bdd-141">In that case, the same workspace and Automation account must be used.</span></span>

![Enable the Update Management solution window](./media/automation-tutorial-update-management/manageupdates-update-enable.png)

<span data-ttu-id="39bdd-143">Enabling the solution can take up to a few minutes.</span><span class="sxs-lookup"><span data-stu-id="39bdd-143">Enabling the solution can take up to a few minutes.</span></span> <span data-ttu-id="39bdd-144">During this time, don't close the browser window.</span><span class="sxs-lookup"><span data-stu-id="39bdd-144">During this time, don't close the browser window.</span></span> <span data-ttu-id="39bdd-145">After the solution is enabled, information about missing updates on the VM flows to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="39bdd-145">After the solution is enabled, information about missing updates on the VM flows to Log Analytics.</span></span> <span data-ttu-id="39bdd-146">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span><span class="sxs-lookup"><span data-stu-id="39bdd-146">It can take between 30 minutes and 6 hours for the data to be available for analysis.</span></span>

## <a name="view-update-assessment"></a><span data-ttu-id="39bdd-147">View update assessment</span><span class="sxs-lookup"><span data-stu-id="39bdd-147">View update assessment</span></span>

<span data-ttu-id="39bdd-148">After Update Management is enabled, the **Update management** pane opens.</span><span class="sxs-lookup"><span data-stu-id="39bdd-148">After Update Management is enabled, the **Update management** pane opens.</span></span> <span data-ttu-id="39bdd-149">If any updates are missing, a list of missing updates is shown on the **Missing updates** tab.</span><span class="sxs-lookup"><span data-stu-id="39bdd-149">If any updates are missing, a list of missing updates is shown on the **Missing updates** tab.</span></span>

<span data-ttu-id="39bdd-150">Under **INFORMATION LINK**, select the update link to open the support article for the update in a new window.</span><span class="sxs-lookup"><span data-stu-id="39bdd-150">Under **INFORMATION LINK**, select the update link to open the support article for the update in a new window.</span></span> <span data-ttu-id="39bdd-151">You can learn important information about the update in this window.</span><span class="sxs-lookup"><span data-stu-id="39bdd-151">You can learn important information about the update in this window.</span></span>

![View update status](./media/automation-tutorial-update-management/manageupdates-view-status-win.png)

<span data-ttu-id="39bdd-153">Click anywhere else on the update to open the **Log Search** pane for the selected update.</span><span class="sxs-lookup"><span data-stu-id="39bdd-153">Click anywhere else on the update to open the **Log Search** pane for the selected update.</span></span> <span data-ttu-id="39bdd-154">The query for the log search is predefined for that specific update.</span><span class="sxs-lookup"><span data-stu-id="39bdd-154">The query for the log search is predefined for that specific update.</span></span> <span data-ttu-id="39bdd-155">You can modify this query or create your own query to view detailed information about the updates that are deployed or missing in your environment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-155">You can modify this query or create your own query to view detailed information about the updates that are deployed or missing in your environment.</span></span>

![View update status](./media/automation-tutorial-update-management/logsearch.png)

## <a name="configure-alerts"></a><span data-ttu-id="39bdd-157">Configure alerts</span><span class="sxs-lookup"><span data-stu-id="39bdd-157">Configure alerts</span></span>

<span data-ttu-id="39bdd-158">In this step, you learn to set up an alert to let you know when updates have been successfully deployed through a Log Analytics query or by tracking the master runbook for Update Management for deployments that failed.</span><span class="sxs-lookup"><span data-stu-id="39bdd-158">In this step, you learn to set up an alert to let you know when updates have been successfully deployed through a Log Analytics query or by tracking the master runbook for Update Management for deployments that failed.</span></span>

### <a name="alert-conditions"></a><span data-ttu-id="39bdd-159">Alert conditions</span><span class="sxs-lookup"><span data-stu-id="39bdd-159">Alert conditions</span></span>

<span data-ttu-id="39bdd-160">For each type of alert, there are different alert conditions that need to be defined.</span><span class="sxs-lookup"><span data-stu-id="39bdd-160">For each type of alert, there are different alert conditions that need to be defined.</span></span>

#### <a name="log-analytics-query-alert"></a><span data-ttu-id="39bdd-161">Log Analytics query alert</span><span class="sxs-lookup"><span data-stu-id="39bdd-161">Log Analytics query alert</span></span>

<span data-ttu-id="39bdd-162">For successful deployments, you can create an alert based on a Log Analytics query.</span><span class="sxs-lookup"><span data-stu-id="39bdd-162">For successful deployments, you can create an alert based on a Log Analytics query.</span></span> <span data-ttu-id="39bdd-163">For failed deployments, you can use the [Runbook alert](#runbook-alert) steps to alert when the master runbook that orchestrators update deployments fails.</span><span class="sxs-lookup"><span data-stu-id="39bdd-163">For failed deployments, you can use the [Runbook alert](#runbook-alert) steps to alert when the master runbook that orchestrators update deployments fails.</span></span> <span data-ttu-id="39bdd-164">You can write a custom query for additional alerts to cover many different scenarios.</span><span class="sxs-lookup"><span data-stu-id="39bdd-164">You can write a custom query for additional alerts to cover many different scenarios.</span></span>

<span data-ttu-id="39bdd-165">In the Azure portal, go to **Monitor**, and then select **Create Alert**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-165">In the Azure portal, go to **Monitor**, and then select **Create Alert**.</span></span>

<span data-ttu-id="39bdd-166">Under **1. Define alert condition**, click **Select target**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-166">Under **1. Define alert condition**, click **Select target**.</span></span> <span data-ttu-id="39bdd-167">Under **Filter by resource type**, select **Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-167">Under **Filter by resource type**, select **Log Analytics**.</span></span> <span data-ttu-id="39bdd-168">Select your Log Analytics workspace, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-168">Select your Log Analytics workspace, and then select **Done**.</span></span>

![Create alert](./media/automation-tutorial-update-management/create-alert.png)

<span data-ttu-id="39bdd-170">Select **Add criteria**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-170">Select **Add criteria**.</span></span>

<span data-ttu-id="39bdd-171">Under **Configure signal logic**, in the table, select **Custom log search**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-171">Under **Configure signal logic**, in the table, select **Custom log search**.</span></span> <span data-ttu-id="39bdd-172">Enter the following query in the **Search query** text box:</span><span class="sxs-lookup"><span data-stu-id="39bdd-172">Enter the following query in the **Search query** text box:</span></span>

```loganalytics
UpdateRunProgress
| where InstallationStatus == 'Succeeded'
| where TimeGenerated > now(-10m)
| summarize by UpdateRunName, Computer
```
<span data-ttu-id="39bdd-173">This query returns the computers and the update run name that completed in the specified timeframe.</span><span class="sxs-lookup"><span data-stu-id="39bdd-173">This query returns the computers and the update run name that completed in the specified timeframe.</span></span>

<span data-ttu-id="39bdd-174">Under **Alert logic**, for **Threshold**, enter **1**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-174">Under **Alert logic**, for **Threshold**, enter **1**.</span></span> <span data-ttu-id="39bdd-175">When you're finished, select **Done**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-175">When you're finished, select **Done**.</span></span>

![Configure signal logic](./media/automation-tutorial-update-management/signal-logic.png)

#### <a name="runbook-alert"></a><span data-ttu-id="39bdd-177">Runbook alert</span><span class="sxs-lookup"><span data-stu-id="39bdd-177">Runbook alert</span></span>

<span data-ttu-id="39bdd-178">For failed deployments you must alert of the failure of the master run In the Azure portal, go to **Monitor**, and then select **Create Alert**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-178">For failed deployments you must alert of the failure of the master run In the Azure portal, go to **Monitor**, and then select **Create Alert**.</span></span>

<span data-ttu-id="39bdd-179">Under **1. Define alert condition**, click **Select target**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-179">Under **1. Define alert condition**, click **Select target**.</span></span> <span data-ttu-id="39bdd-180">Under **Filter by resource type**, select **Automation Accounts**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-180">Under **Filter by resource type**, select **Automation Accounts**.</span></span> <span data-ttu-id="39bdd-181">Select your Automation Account, and then select **Done**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-181">Select your Automation Account, and then select **Done**.</span></span>

<span data-ttu-id="39bdd-182">For **Runbook Name**, click the **\+** sign and enter **Patch-MicrosoftOMSComputers** as a custom name.</span><span class="sxs-lookup"><span data-stu-id="39bdd-182">For **Runbook Name**, click the **\+** sign and enter **Patch-MicrosoftOMSComputers** as a custom name.</span></span> <span data-ttu-id="39bdd-183">For **Status**, choose **Failed** or click the **\+** sign to enter **Failed**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-183">For **Status**, choose **Failed** or click the **\+** sign to enter **Failed**.</span></span>

![Configure signal logic for runbooks](./media/automation-tutorial-update-management/signal-logic-runbook.png)

<span data-ttu-id="39bdd-185">Under **Alert logic**, for **Threshold**, enter **1**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-185">Under **Alert logic**, for **Threshold**, enter **1**.</span></span> <span data-ttu-id="39bdd-186">When you're finished, select **Done**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-186">When you're finished, select **Done**.</span></span>

### <a name="alert-details"></a><span data-ttu-id="39bdd-187">Alert details</span><span class="sxs-lookup"><span data-stu-id="39bdd-187">Alert details</span></span>

<span data-ttu-id="39bdd-188">Under **2. Define alert details**, enter a name and description for the alert.</span><span class="sxs-lookup"><span data-stu-id="39bdd-188">Under **2. Define alert details**, enter a name and description for the alert.</span></span> <span data-ttu-id="39bdd-189">Set **Severity** to **Informational(Sev 2)** for a successful run, or **Informational(Sev 1)** for a failed run.</span><span class="sxs-lookup"><span data-stu-id="39bdd-189">Set **Severity** to **Informational(Sev 2)** for a successful run, or **Informational(Sev 1)** for a failed run.</span></span>

![Configure signal logic](./media/automation-tutorial-update-management/define-alert-details.png)

<span data-ttu-id="39bdd-191">Under **3. Define action group**, select **New action group**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-191">Under **3. Define action group**, select **New action group**.</span></span> <span data-ttu-id="39bdd-192">An action group is a group of actions that you can use across multiple alerts.</span><span class="sxs-lookup"><span data-stu-id="39bdd-192">An action group is a group of actions that you can use across multiple alerts.</span></span> <span data-ttu-id="39bdd-193">The actions can include but are not limited to email notifications, runbooks, webhooks, and many more.</span><span class="sxs-lookup"><span data-stu-id="39bdd-193">The actions can include but are not limited to email notifications, runbooks, webhooks, and many more.</span></span> <span data-ttu-id="39bdd-194">To learn more about action groups, see [Create and manage action groups](../monitoring-and-diagnostics/monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="39bdd-194">To learn more about action groups, see [Create and manage action groups](../monitoring-and-diagnostics/monitoring-action-groups.md).</span></span>

<span data-ttu-id="39bdd-195">In the **Action group name** box, enter a name for the alert and a short name.</span><span class="sxs-lookup"><span data-stu-id="39bdd-195">In the **Action group name** box, enter a name for the alert and a short name.</span></span> <span data-ttu-id="39bdd-196">The short name is used in place of a full action group name when notifications are sent by using this group.</span><span class="sxs-lookup"><span data-stu-id="39bdd-196">The short name is used in place of a full action group name when notifications are sent by using this group.</span></span>

<span data-ttu-id="39bdd-197">Under **Actions**, enter a name for the action, like **Email Notifications**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-197">Under **Actions**, enter a name for the action, like **Email Notifications**.</span></span> <span data-ttu-id="39bdd-198">Under **ACTION TYPE**, select **Email/SMS/Push/Voice**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-198">Under **ACTION TYPE**, select **Email/SMS/Push/Voice**.</span></span> <span data-ttu-id="39bdd-199">Under **DETAILS**, select **Edit details**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-199">Under **DETAILS**, select **Edit details**.</span></span>

<span data-ttu-id="39bdd-200">In the **Email/SMS/Push/Voice** pane, enter a name.</span><span class="sxs-lookup"><span data-stu-id="39bdd-200">In the **Email/SMS/Push/Voice** pane, enter a name.</span></span> <span data-ttu-id="39bdd-201">Select the **Email** check box, and then enter a valid email address.</span><span class="sxs-lookup"><span data-stu-id="39bdd-201">Select the **Email** check box, and then enter a valid email address.</span></span>

![Configure an email action group](./media/automation-tutorial-update-management/configure-email-action-group.png)

<span data-ttu-id="39bdd-203">In the **Email/SMS/Push/Voice** pane, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-203">In the **Email/SMS/Push/Voice** pane, select **OK**.</span></span> <span data-ttu-id="39bdd-204">In the **Add action group** pane, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-204">In the **Add action group** pane, select **OK**.</span></span>

<span data-ttu-id="39bdd-205">To customize the subject of the alert email,  under **Create rule**, under **Customize Actions**, select **Email subject**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-205">To customize the subject of the alert email,  under **Create rule**, under **Customize Actions**, select **Email subject**.</span></span> <span data-ttu-id="39bdd-206">When you're finished, select **Create alert rule**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-206">When you're finished, select **Create alert rule**.</span></span> <span data-ttu-id="39bdd-207">The alert tells you when an update deployment succeeds, and which machines were part of that update deployment run.</span><span class="sxs-lookup"><span data-stu-id="39bdd-207">The alert tells you when an update deployment succeeds, and which machines were part of that update deployment run.</span></span>

## <a name="schedule-an-update-deployment"></a><span data-ttu-id="39bdd-208">Schedule an update deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-208">Schedule an update deployment</span></span>

<span data-ttu-id="39bdd-209">Next, schedule a deployment that follows your release schedule and service window to install updates.</span><span class="sxs-lookup"><span data-stu-id="39bdd-209">Next, schedule a deployment that follows your release schedule and service window to install updates.</span></span> <span data-ttu-id="39bdd-210">You can choose which update types to include in the deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-210">You can choose which update types to include in the deployment.</span></span> <span data-ttu-id="39bdd-211">For example, you can include critical or security updates and exclude update rollups.</span><span class="sxs-lookup"><span data-stu-id="39bdd-211">For example, you can include critical or security updates and exclude update rollups.</span></span>

<span data-ttu-id="39bdd-212">To schedule a new update deployment for the VM, go to **Update management**, and then select **Schedule update deployment**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-212">To schedule a new update deployment for the VM, go to **Update management**, and then select **Schedule update deployment**.</span></span>

<span data-ttu-id="39bdd-213">Under **New update deployment**, specify the following information:</span><span class="sxs-lookup"><span data-stu-id="39bdd-213">Under **New update deployment**, specify the following information:</span></span>

* <span data-ttu-id="39bdd-214">**Name**: Enter a unique name for the update deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-214">**Name**: Enter a unique name for the update deployment.</span></span>

* <span data-ttu-id="39bdd-215">**Operating system**: Select the OS to target for the update deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-215">**Operating system**: Select the OS to target for the update deployment.</span></span>

* <span data-ttu-id="39bdd-216">**Machines to update**: Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span><span class="sxs-lookup"><span data-stu-id="39bdd-216">**Machines to update**: Select a Saved search, Imported group, or pick Machine from the drop-down and select individual machines.</span></span> <span data-ttu-id="39bdd-217">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span><span class="sxs-lookup"><span data-stu-id="39bdd-217">If you choose **Machines**, the readiness of the machine is shown in the **UPDATE AGENT READINESS** column.</span></span> <span data-ttu-id="39bdd-218">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span><span class="sxs-lookup"><span data-stu-id="39bdd-218">To learn about the different methods of creating computer groups in Log Analytics, see [Computer groups in Log Analytics](../log-analytics/log-analytics-computer-groups.md)</span></span>

* <span data-ttu-id="39bdd-219">**Update classification**: Select the types of software that the update deployment included in the deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-219">**Update classification**: Select the types of software that the update deployment included in the deployment.</span></span> <span data-ttu-id="39bdd-220">For this tutorial, leave all types selected.</span><span class="sxs-lookup"><span data-stu-id="39bdd-220">For this tutorial, leave all types selected.</span></span>

  <span data-ttu-id="39bdd-221">The classification types are:</span><span class="sxs-lookup"><span data-stu-id="39bdd-221">The classification types are:</span></span>

   |<span data-ttu-id="39bdd-222">OS</span><span class="sxs-lookup"><span data-stu-id="39bdd-222">OS</span></span>  |<span data-ttu-id="39bdd-223">Type</span><span class="sxs-lookup"><span data-stu-id="39bdd-223">Type</span></span>  |
   |---------|---------|
   |<span data-ttu-id="39bdd-224">Windows</span><span class="sxs-lookup"><span data-stu-id="39bdd-224">Windows</span></span>     | <span data-ttu-id="39bdd-225">Critical updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-225">Critical updates</span></span></br><span data-ttu-id="39bdd-226">Security updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-226">Security updates</span></span></br><span data-ttu-id="39bdd-227">Update rollups</span><span class="sxs-lookup"><span data-stu-id="39bdd-227">Update rollups</span></span></br><span data-ttu-id="39bdd-228">Feature packs</span><span class="sxs-lookup"><span data-stu-id="39bdd-228">Feature packs</span></span></br><span data-ttu-id="39bdd-229">Service packs</span><span class="sxs-lookup"><span data-stu-id="39bdd-229">Service packs</span></span></br><span data-ttu-id="39bdd-230">Definition updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-230">Definition updates</span></span></br><span data-ttu-id="39bdd-231">Tools</span><span class="sxs-lookup"><span data-stu-id="39bdd-231">Tools</span></span></br><span data-ttu-id="39bdd-232">Updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-232">Updates</span></span>        |
   |<span data-ttu-id="39bdd-233">Linux</span><span class="sxs-lookup"><span data-stu-id="39bdd-233">Linux</span></span>     | <span data-ttu-id="39bdd-234">Critical and security updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-234">Critical and security updates</span></span></br><span data-ttu-id="39bdd-235">Other updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-235">Other updates</span></span>       |

   <span data-ttu-id="39bdd-236">For a description of the classification types, see [update classifications](automation-update-management.md#update-classifications).</span><span class="sxs-lookup"><span data-stu-id="39bdd-236">For a description of the classification types, see [update classifications](automation-update-management.md#update-classifications).</span></span>

* <span data-ttu-id="39bdd-237">**Schedule settings**: The **Schedule Settings** pane opens.</span><span class="sxs-lookup"><span data-stu-id="39bdd-237">**Schedule settings**: The **Schedule Settings** pane opens.</span></span> <span data-ttu-id="39bdd-238">The default start time is 30 minutes after the current time.</span><span class="sxs-lookup"><span data-stu-id="39bdd-238">The default start time is 30 minutes after the current time.</span></span> <span data-ttu-id="39bdd-239">You can set the start time to any time from 10 minutes in the future.</span><span class="sxs-lookup"><span data-stu-id="39bdd-239">You can set the start time to any time from 10 minutes in the future.</span></span>

   <span data-ttu-id="39bdd-240">You can also specify whether the deployment occurs once, or set up a recurring schedule.</span><span class="sxs-lookup"><span data-stu-id="39bdd-240">You can also specify whether the deployment occurs once, or set up a recurring schedule.</span></span> <span data-ttu-id="39bdd-241">Under **Recurrence**, select **Once**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-241">Under **Recurrence**, select **Once**.</span></span> <span data-ttu-id="39bdd-242">Leave the default as 1 day and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-242">Leave the default as 1 day and select **OK**.</span></span> <span data-ttu-id="39bdd-243">This sets up a recurring schedule.</span><span class="sxs-lookup"><span data-stu-id="39bdd-243">This sets up a recurring schedule.</span></span>

* <span data-ttu-id="39bdd-244">**Maintenance window (minutes)**: Leave the default value.</span><span class="sxs-lookup"><span data-stu-id="39bdd-244">**Maintenance window (minutes)**: Leave the default value.</span></span> <span data-ttu-id="39bdd-245">You can set the window of time that you want the update deployment to occur within.</span><span class="sxs-lookup"><span data-stu-id="39bdd-245">You can set the window of time that you want the update deployment to occur within.</span></span> <span data-ttu-id="39bdd-246">This setting helps ensure that changes are performed within your defined service windows.</span><span class="sxs-lookup"><span data-stu-id="39bdd-246">This setting helps ensure that changes are performed within your defined service windows.</span></span>

* <span data-ttu-id="39bdd-247">**Reboot options**: This setting determines how reboots should be handled.</span><span class="sxs-lookup"><span data-stu-id="39bdd-247">**Reboot options**: This setting determines how reboots should be handled.</span></span> <span data-ttu-id="39bdd-248">Available options are:</span><span class="sxs-lookup"><span data-stu-id="39bdd-248">Available options are:</span></span>
  * <span data-ttu-id="39bdd-249">Reboot if required (Default)</span><span class="sxs-lookup"><span data-stu-id="39bdd-249">Reboot if required (Default)</span></span>
  * <span data-ttu-id="39bdd-250">Always reboot</span><span class="sxs-lookup"><span data-stu-id="39bdd-250">Always reboot</span></span>
  * <span data-ttu-id="39bdd-251">Never reboot</span><span class="sxs-lookup"><span data-stu-id="39bdd-251">Never reboot</span></span>
  * <span data-ttu-id="39bdd-252">Only reboot - will not install updates</span><span class="sxs-lookup"><span data-stu-id="39bdd-252">Only reboot - will not install updates</span></span>

<span data-ttu-id="39bdd-253">When you're finished configuring the schedule, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-253">When you're finished configuring the schedule, select **Create**.</span></span>

![Update Schedule Settings pane](./media/automation-tutorial-update-management/manageupdates-schedule-win.png)

<span data-ttu-id="39bdd-255">You're returned to the status dashboard.</span><span class="sxs-lookup"><span data-stu-id="39bdd-255">You're returned to the status dashboard.</span></span> <span data-ttu-id="39bdd-256">Select **Scheduled Update deployments** to show the deployment schedule you created.</span><span class="sxs-lookup"><span data-stu-id="39bdd-256">Select **Scheduled Update deployments** to show the deployment schedule you created.</span></span>

## <a name="view-results-of-an-update-deployment"></a><span data-ttu-id="39bdd-257">View results of an update deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-257">View results of an update deployment</span></span>

<span data-ttu-id="39bdd-258">After the scheduled deployment starts, you can see the status for that deployment on the **Update deployments** tab under **Update management**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-258">After the scheduled deployment starts, you can see the status for that deployment on the **Update deployments** tab under **Update management**.</span></span> <span data-ttu-id="39bdd-259">The status is **In progress** when the deployment is currently running.</span><span class="sxs-lookup"><span data-stu-id="39bdd-259">The status is **In progress** when the deployment is currently running.</span></span> <span data-ttu-id="39bdd-260">When the deployment finishes, if it's successful, the status changes to **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-260">When the deployment finishes, if it's successful, the status changes to **Succeeded**.</span></span> <span data-ttu-id="39bdd-261">When there are failures with one or more updates in the deployment, the status is **Partially failed**.</span><span class="sxs-lookup"><span data-stu-id="39bdd-261">When there are failures with one or more updates in the deployment, the status is **Partially failed**.</span></span>

<span data-ttu-id="39bdd-262">Select the completed update deployment to see the dashboard for that update deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-262">Select the completed update deployment to see the dashboard for that update deployment.</span></span>

![Update deployment status dashboard for a specific deployment](./media/automation-tutorial-update-management/manageupdates-view-results.png)

<span data-ttu-id="39bdd-264">Under **Update results**, a summary provides the total number of updates and deployment results on the VM.</span><span class="sxs-lookup"><span data-stu-id="39bdd-264">Under **Update results**, a summary provides the total number of updates and deployment results on the VM.</span></span> <span data-ttu-id="39bdd-265">The table on the right shows a detailed breakdown of each update and the installation results.</span><span class="sxs-lookup"><span data-stu-id="39bdd-265">The table on the right shows a detailed breakdown of each update and the installation results.</span></span>

<span data-ttu-id="39bdd-266">The following list shows the available values:</span><span class="sxs-lookup"><span data-stu-id="39bdd-266">The following list shows the available values:</span></span>

* <span data-ttu-id="39bdd-267">**Not attempted**: The update wasn't installed because there was insufficient time available based on the maintenance window duration defined.</span><span class="sxs-lookup"><span data-stu-id="39bdd-267">**Not attempted**: The update wasn't installed because there was insufficient time available based on the maintenance window duration defined.</span></span>
* <span data-ttu-id="39bdd-268">**Succeeded**: The update succeeded.</span><span class="sxs-lookup"><span data-stu-id="39bdd-268">**Succeeded**: The update succeeded.</span></span>
* <span data-ttu-id="39bdd-269">**Failed**: The update failed.</span><span class="sxs-lookup"><span data-stu-id="39bdd-269">**Failed**: The update failed.</span></span>

<span data-ttu-id="39bdd-270">Select **All logs** to see all log entries that the deployment created.</span><span class="sxs-lookup"><span data-stu-id="39bdd-270">Select **All logs** to see all log entries that the deployment created.</span></span>

<span data-ttu-id="39bdd-271">Select **Output** to see the job stream of the runbook responsible for managing the update deployment on the target VM.</span><span class="sxs-lookup"><span data-stu-id="39bdd-271">Select **Output** to see the job stream of the runbook responsible for managing the update deployment on the target VM.</span></span>

<span data-ttu-id="39bdd-272">Select **Errors** to see detailed information about any errors from the deployment.</span><span class="sxs-lookup"><span data-stu-id="39bdd-272">Select **Errors** to see detailed information about any errors from the deployment.</span></span>

<span data-ttu-id="39bdd-273">When your update deployment is successful, an email that's similar to the following example is sent to show success of the deployment:</span><span class="sxs-lookup"><span data-stu-id="39bdd-273">When your update deployment is successful, an email that's similar to the following example is sent to show success of the deployment:</span></span>

![Configure email action group](./media/automation-tutorial-update-management/email-notification.png)

## <a name="next-steps"></a><span data-ttu-id="39bdd-275">Next steps</span><span class="sxs-lookup"><span data-stu-id="39bdd-275">Next steps</span></span>

<span data-ttu-id="39bdd-276">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="39bdd-276">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39bdd-277">Onboard a VM for Update Management</span><span class="sxs-lookup"><span data-stu-id="39bdd-277">Onboard a VM for Update Management</span></span>
> * <span data-ttu-id="39bdd-278">View an update assessment</span><span class="sxs-lookup"><span data-stu-id="39bdd-278">View an update assessment</span></span>
> * <span data-ttu-id="39bdd-279">Configure alerting</span><span class="sxs-lookup"><span data-stu-id="39bdd-279">Configure alerting</span></span>
> * <span data-ttu-id="39bdd-280">Schedule an update deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-280">Schedule an update deployment</span></span>
> * <span data-ttu-id="39bdd-281">View the results of a deployment</span><span class="sxs-lookup"><span data-stu-id="39bdd-281">View the results of a deployment</span></span>

<span data-ttu-id="39bdd-282">Continue to the overview for the Update Management solution.</span><span class="sxs-lookup"><span data-stu-id="39bdd-282">Continue to the overview for the Update Management solution.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39bdd-283">Update Management solution</span><span class="sxs-lookup"><span data-stu-id="39bdd-283">Update Management solution</span></span>](../operations-management-suite/oms-solution-update-management.md?toc=%2fazure%2fautomation%2ftoc.json)
