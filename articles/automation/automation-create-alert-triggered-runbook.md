---
title: Use an alert to trigger an Azure Automation runbook
description: Learn how to trigger a runbook to run when an Azure alert is raised.
services: automation
ms.service: automation
ms.component: process-automation
author: georgewallace
ms.author: gwallace
ms.date: 03/15/2018
ms.topic: conceptual
manager: carmonm
ms.openlocfilehash: e791cddb07d3204f807dbeff98b7fc69419ae23c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868066"
---
# <a name="use-an-alert-to-trigger-an-azure-automation-runbook"></a><span data-ttu-id="b5d6a-103">Use an alert to trigger an Azure Automation runbook</span><span class="sxs-lookup"><span data-stu-id="b5d6a-103">Use an alert to trigger an Azure Automation runbook</span></span>

<span data-ttu-id="b5d6a-104">You can use [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md?toc=%2fazure%2fautomation%2ftoc.json) to monitor base-level metrics and logs for most services in Azure.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-104">You can use [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview-azure-monitor.md?toc=%2fazure%2fautomation%2ftoc.json) to monitor base-level metrics and logs for most services in Azure.</span></span> <span data-ttu-id="b5d6a-105">You can call Azure Automation runbooks by using [action groups](../monitoring-and-diagnostics/monitoring-action-groups.md?toc=%2fazure%2fautomation%2ftoc.json) or by using classic alerts to automate tasks based on alerts.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-105">You can call Azure Automation runbooks by using [action groups](../monitoring-and-diagnostics/monitoring-action-groups.md?toc=%2fazure%2fautomation%2ftoc.json) or by using classic alerts to automate tasks based on alerts.</span></span> <span data-ttu-id="b5d6a-106">This article shows you how to configure and run a runbook by using alerts.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-106">This article shows you how to configure and run a runbook by using alerts.</span></span>

## <a name="alert-types"></a><span data-ttu-id="b5d6a-107">Alert types</span><span class="sxs-lookup"><span data-stu-id="b5d6a-107">Alert types</span></span>

<span data-ttu-id="b5d6a-108">You can use automation runbooks with three alert types:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-108">You can use automation runbooks with three alert types:</span></span>
* <span data-ttu-id="b5d6a-109">Classic metric alerts</span><span class="sxs-lookup"><span data-stu-id="b5d6a-109">Classic metric alerts</span></span>
* <span data-ttu-id="b5d6a-110">Activity log alerts</span><span class="sxs-lookup"><span data-stu-id="b5d6a-110">Activity log alerts</span></span>
* <span data-ttu-id="b5d6a-111">Near real-time metric alerts</span><span class="sxs-lookup"><span data-stu-id="b5d6a-111">Near real-time metric alerts</span></span>

<span data-ttu-id="b5d6a-112">When an alert calls a runbook, the actual call is an HTTP POST request to the webhook.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-112">When an alert calls a runbook, the actual call is an HTTP POST request to the webhook.</span></span> <span data-ttu-id="b5d6a-113">The body of the POST request contains a JSON-formated object that has useful properties that are related to the alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-113">The body of the POST request contains a JSON-formated object that has useful properties that are related to the alert.</span></span> <span data-ttu-id="b5d6a-114">The following table lists links to the payload schema for each alert type:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-114">The following table lists links to the payload schema for each alert type:</span></span>

|<span data-ttu-id="b5d6a-115">Alert</span><span class="sxs-lookup"><span data-stu-id="b5d6a-115">Alert</span></span>  |<span data-ttu-id="b5d6a-116">Description</span><span class="sxs-lookup"><span data-stu-id="b5d6a-116">Description</span></span>|<span data-ttu-id="b5d6a-117">Payload schema</span><span class="sxs-lookup"><span data-stu-id="b5d6a-117">Payload schema</span></span>  |
|---------|---------|---------|
|[<span data-ttu-id="b5d6a-118">Classic metric alert</span><span class="sxs-lookup"><span data-stu-id="b5d6a-118">Classic metric alert</span></span>](../monitoring-and-diagnostics/insights-alerts-portal.md?toc=%2fazure%2fautomation%2ftoc.json)    |<span data-ttu-id="b5d6a-119">Sends a notification when any platform-level metric meets a specific condition.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-119">Sends a notification when any platform-level metric meets a specific condition.</span></span> <span data-ttu-id="b5d6a-120">For example, when the value for **CPU %** on a VM is greater than **90** for the past 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-120">For example, when the value for **CPU %** on a VM is greater than **90** for the past 5 minutes.</span></span>| [<span data-ttu-id="b5d6a-121">Class metric alert payload schema</span><span class="sxs-lookup"><span data-stu-id="b5d6a-121">Class metric alert payload schema</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md?toc=%2fazure%2fautomation%2ftoc.json#payload-schema)         |
|[<span data-ttu-id="b5d6a-122">Activity log alert</span><span class="sxs-lookup"><span data-stu-id="b5d6a-122">Activity log alert</span></span>](../monitoring-and-diagnostics/monitoring-activity-log-alerts.md?toc=%2fazure%2fautomation%2ftoc.json)    |<span data-ttu-id="b5d6a-123">Sends a notification when any new event in the Azure activity log matches specific conditions.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-123">Sends a notification when any new event in the Azure activity log matches specific conditions.</span></span> <span data-ttu-id="b5d6a-124">For example, when a `Delete VM` operation occurs in **myProductionResourceGroup** or when a new Azure Service Health event with an **Active** status appears.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-124">For example, when a `Delete VM` operation occurs in **myProductionResourceGroup** or when a new Azure Service Health event with an **Active** status appears.</span></span>| [<span data-ttu-id="b5d6a-125">Activity log alert payload schema</span><span class="sxs-lookup"><span data-stu-id="b5d6a-125">Activity log alert payload schema</span></span>](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md?toc=%2fazure%2fautomation%2ftoc.json#payload-schema)        |
|[<span data-ttu-id="b5d6a-126">Near real-time metric alert</span><span class="sxs-lookup"><span data-stu-id="b5d6a-126">Near real-time metric alert</span></span>](../monitoring-and-diagnostics/monitoring-near-real-time-metric-alerts.md?toc=%2fazure%2fautomation%2ftoc.json)    |<span data-ttu-id="b5d6a-127">Sends a notification faster than metric alerts when one or more platform-level metrics meet specified conditions.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-127">Sends a notification faster than metric alerts when one or more platform-level metrics meet specified conditions.</span></span> <span data-ttu-id="b5d6a-128">For example, when the value for **CPU %** on a VM is greater than **90**, and the value for **Network In** is greater than **500 MB** for the past 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-128">For example, when the value for **CPU %** on a VM is greater than **90**, and the value for **Network In** is greater than **500 MB** for the past 5 minutes.</span></span>| [<span data-ttu-id="b5d6a-129">Near real-time metric alert payload schema</span><span class="sxs-lookup"><span data-stu-id="b5d6a-129">Near real-time metric alert payload schema</span></span>](../monitoring-and-diagnostics/monitoring-near-real-time-metric-alerts.md?toc=%2fazure%2fautomation%2ftoc.json#payload-schema)          |

<span data-ttu-id="b5d6a-130">Because the data that's provided by each type of alert is different, each alert type is handled differently.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-130">Because the data that's provided by each type of alert is different, each alert type is handled differently.</span></span> <span data-ttu-id="b5d6a-131">In the next section, you learn how to create a runbook to handle different types of alerts.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-131">In the next section, you learn how to create a runbook to handle different types of alerts.</span></span>

## <a name="create-a-runbook-to-handle-alerts"></a><span data-ttu-id="b5d6a-132">Create a runbook to handle alerts</span><span class="sxs-lookup"><span data-stu-id="b5d6a-132">Create a runbook to handle alerts</span></span>

<span data-ttu-id="b5d6a-133">To use Automation with alerts, you need a runbook that has logic that manages the alert JSON payload that's passed to the runbook.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-133">To use Automation with alerts, you need a runbook that has logic that manages the alert JSON payload that's passed to the runbook.</span></span> <span data-ttu-id="b5d6a-134">The following example runbook must be called from an Azure alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-134">The following example runbook must be called from an Azure alert.</span></span> 

<span data-ttu-id="b5d6a-135">As described in the preceding section, each type of alert has a different schema.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-135">As described in the preceding section, each type of alert has a different schema.</span></span> <span data-ttu-id="b5d6a-136">The script takes in the webhook data in the `WebhookData` runbook input parameter from an alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-136">The script takes in the webhook data in the `WebhookData` runbook input parameter from an alert.</span></span> <span data-ttu-id="b5d6a-137">Then, the script evaluates the JSON payload to determine which alert type was used.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-137">Then, the script evaluates the JSON payload to determine which alert type was used.</span></span> 

<span data-ttu-id="b5d6a-138">This example uses an alert from a VM.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-138">This example uses an alert from a VM.</span></span> <span data-ttu-id="b5d6a-139">It retrieves the VM data from the payload, and then uses that information to stop the VM.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-139">It retrieves the VM data from the payload, and then uses that information to stop the VM.</span></span> <span data-ttu-id="b5d6a-140">The connection must be set up in the Automation account where the runbook is run.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-140">The connection must be set up in the Automation account where the runbook is run.</span></span>

<span data-ttu-id="b5d6a-141">The runbook uses the **AzureRunAsConnection** [Run As account](automation-create-runas-account.md) to authenticate with Azure to perform the management action against the VM.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-141">The runbook uses the **AzureRunAsConnection** [Run As account](automation-create-runas-account.md) to authenticate with Azure to perform the management action against the VM.</span></span>

<span data-ttu-id="b5d6a-142">Use this example to create a runbook called **Stop-AzureVmInResponsetoVMAlert**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-142">Use this example to create a runbook called **Stop-AzureVmInResponsetoVMAlert**.</span></span> <span data-ttu-id="b5d6a-143">You can modify the PowerShell script, and use it with many different resources.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-143">You can modify the PowerShell script, and use it with many different resources.</span></span>

1. <span data-ttu-id="b5d6a-144">Go to your Azure Automation account.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-144">Go to your Azure Automation account.</span></span>
1. <span data-ttu-id="b5d6a-145">Under **PROCESS AUTOMATION**, select **Runbooks**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-145">Under **PROCESS AUTOMATION**, select **Runbooks**.</span></span>
1. <span data-ttu-id="b5d6a-146">At the top of the list of runbooks, select **Add a runbook**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-146">At the top of the list of runbooks, select **Add a runbook**.</span></span> 
1. <span data-ttu-id="b5d6a-147">On the **Add Runbook** page, select **Quick Create**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-147">On the **Add Runbook** page, select **Quick Create**.</span></span>
1. <span data-ttu-id="b5d6a-148">For the runbook name, enter **Stop-AzureVmInResponsetoVMAlert**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-148">For the runbook name, enter **Stop-AzureVmInResponsetoVMAlert**.</span></span> <span data-ttu-id="b5d6a-149">For the runbook type, select **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-149">For the runbook type, select **PowerShell**.</span></span> <span data-ttu-id="b5d6a-150">Then, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-150">Then, select **Create**.</span></span>  
1. <span data-ttu-id="b5d6a-151">Copy the following PowerShell example into the **Edit** pane.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-151">Copy the following PowerShell example into the **Edit** pane.</span></span> 

    ```powershell-interactive
    <#
    .SYNOPSIS
    This runbook stops a resource management VM in response to an Azure alert trigger.

    .DESCRIPTION
    This runbook stops a resource management VM in response to an Azure alert trigger.
    The input is alert data that has the information required to identify which VM to stop.
    
    DEPENDENCIES
    - The runbook must be called from an Azure alert via a webhook.
    
    REQUIRED AUTOMATION ASSETS
    - An Automation connection asset called "AzureRunAsConnection" that is of type AzureRunAsConnection.
    - An Automation certificate asset called "AzureRunAsCertificate".

    .PARAMETER WebhookData
    Optional. (The user doesn't need to enter anything, but the service always passes an object.)
    This is the data that's sent in the webhook that's triggered from the alert.

    .NOTES
    AUTHOR: Azure Automation Team
    LASTEDIT: 2017-11-22
    #>

    [OutputType("PSAzureOperationResponse")]

    param
    (
        [Parameter (Mandatory=$false)]
        [object] $WebhookData
    )

    $ErrorActionPreference = "stop"

    if ($WebhookData)
    {
        # Get the data object from WebhookData.
        $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

        # Get the info needed to identify the VM (depends on the payload schema).
        $schemaId = $WebhookBody.schemaId
        Write-Verbose "schemaId: $schemaId" -Verbose
        if ($schemaId -eq "AzureMonitorMetricAlert") {
            # This is the near-real-time Metric Alert schema
            $AlertContext = [object] ($WebhookBody.data).context
            $ResourceName = $AlertContext.resourceName
            $status = ($WebhookBody.data).status
        }
        elseif ($schemaId -eq "Microsoft.Insights/activityLogs") {
            # This is the Activity Log Alert schema
            $AlertContext = [object] (($WebhookBody.data).context).activityLog
            $ResourceName = (($AlertContext.resourceId).Split("/"))[-1]
            $status = ($WebhookBody.data).status
        }
        elseif ($schemaId -eq $null) {
            # This is the original Metric Alert schema
            $AlertContext = [object] $WebhookBody.context
            $ResourceName = $AlertContext.resourceName
            $status = $WebhookBody.status
        }
        else {
            # The schema isn't supported.
            Write-Error "The alert data schema - $schemaId - is not supported."
        }

        Write-Verbose "status: $status" -Verbose
        if ($status -eq "Activated")
        {
            $ResourceType = $AlertContext.resourceType
            $ResourceGroupName = $AlertContext.resourceGroupName
            $SubId = $AlertContext.subscriptionId
            Write-Verbose "resourceType: $ResourceType" -Verbose
            Write-Verbose "resourceName: $ResourceName" -Verbose
            Write-Verbose "resourceGroupName: $ResourceGroupName" -Verbose
            Write-Verbose "subscriptionId: $SubId" -Verbose

            # Use this only if this is a resource management VM.
            if ($ResourceType -eq "Microsoft.Compute/virtualMachines")
            {
                # This is the VM.
                Write-Verbose "This is a resource management VM." -Verbose

                # Authenticate to Azure by using the service principal and certificate. Then, set the subscription.
                Write-Verbose "Authenticating to Azure with service principal and certificate" -Verbose
                $ConnectionAssetName = "AzureRunAsConnection"
                Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
                $Conn = Get-AutomationConnection -Name $ConnectionAssetName
                if ($Conn -eq $null)
                {
                    throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
                }
                Write-Verbose "Authenticating to Azure with service principal." -Verbose
                Connect-AzureRmAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
                Write-Verbose "Setting subscription to work against: $SubId" -Verbose
                Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

                # Stop the VM.
                Write-Verbose "Stopping the VM - $ResourceName - in resource group - $ResourceGroupName -" -Verbose
                Stop-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName -Force
                # [OutputType(PSAzureOperationResponse")]
            }
            else {
                # ResourceType isn't supported.
                Write-Error "$ResourceType is not a supported resource type for this runbook."
            }
        }
        else {
            # The alert status was not 'Activated', so no action taken.
            Write-Verbose ("No action taken. Alert status: " + $status) -Verbose
        }
    }
    else {
        # Error
        Write-Error "This runbook is meant to be started from an Azure alert webhook only."
    }
    ```
1. <span data-ttu-id="b5d6a-152">Select **Publish** to save and publish the runbook.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-152">Select **Publish** to save and publish the runbook.</span></span>

## <a name="create-an-action-group"></a><span data-ttu-id="b5d6a-153">Create an action group</span><span class="sxs-lookup"><span data-stu-id="b5d6a-153">Create an action group</span></span>

<span data-ttu-id="b5d6a-154">An action group is a collection of actions that are triggered by an alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-154">An action group is a collection of actions that are triggered by an alert.</span></span> <span data-ttu-id="b5d6a-155">Runbooks are just one of the many actions that you can use with action groups.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-155">Runbooks are just one of the many actions that you can use with action groups.</span></span>

1. <span data-ttu-id="b5d6a-156">In the Azure portal, select **Monitor** > **SETTINGS** > **Action groups**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-156">In the Azure portal, select **Monitor** > **SETTINGS** > **Action groups**.</span></span>
1. <span data-ttu-id="b5d6a-157">Select **Add action group**, and then enter the required information:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-157">Select **Add action group**, and then enter the required information:</span></span>  
    1. <span data-ttu-id="b5d6a-158">In the **Action group name** box, enter a name.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-158">In the **Action group name** box, enter a name.</span></span>
    1. <span data-ttu-id="b5d6a-159">In the **Short name** box, enter a name.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-159">In the **Short name** box, enter a name.</span></span> <span data-ttu-id="b5d6a-160">The short name is used in place of a full action group name when notifications are sent by using this action group.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-160">The short name is used in place of a full action group name when notifications are sent by using this action group.</span></span>
    1. <span data-ttu-id="b5d6a-161">The **Subscription** box is automatically filled with your current subscription.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-161">The **Subscription** box is automatically filled with your current subscription.</span></span> <span data-ttu-id="b5d6a-162">This is the subscription in which the action group is saved.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-162">This is the subscription in which the action group is saved.</span></span>
    1. <span data-ttu-id="b5d6a-163">Select the resource group in which the action group is saved.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-163">Select the resource group in which the action group is saved.</span></span>

<span data-ttu-id="b5d6a-164">For this example, you create two actions: a runbook action and a notification action.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-164">For this example, you create two actions: a runbook action and a notification action.</span></span>

### <a name="runbook-action"></a><span data-ttu-id="b5d6a-165">Runbook action</span><span class="sxs-lookup"><span data-stu-id="b5d6a-165">Runbook action</span></span>

<span data-ttu-id="b5d6a-166">To create a runbook action in the action group:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-166">To create a runbook action in the action group:</span></span>

1. <span data-ttu-id="b5d6a-167">Under **Actions**, for **ACTION NAME**, enter a name for the action.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-167">Under **Actions**, for **ACTION NAME**, enter a name for the action.</span></span> <span data-ttu-id="b5d6a-168">For **ACTION TYPE**, select **Automation Runbook**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-168">For **ACTION TYPE**, select **Automation Runbook**.</span></span>
1. <span data-ttu-id="b5d6a-169">Under **DETAILS**, select **Edit Details**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-169">Under **DETAILS**, select **Edit Details**.</span></span>  
1. <span data-ttu-id="b5d6a-170">On the **Configure Runbook** page, under **Runbook source**, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-170">On the **Configure Runbook** page, under **Runbook source**, select **User**.</span></span>  
1. <span data-ttu-id="b5d6a-171">Select your **Subscription** and **Automation account**, and then select the **Stop-AzureVmInResponsetoVMAlert** runbook.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-171">Select your **Subscription** and **Automation account**, and then select the **Stop-AzureVmInResponsetoVMAlert** runbook.</span></span>  
1. <span data-ttu-id="b5d6a-172">When you are finished, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-172">When you are finished, select **OK**.</span></span>

### <a name="notification-action"></a><span data-ttu-id="b5d6a-173">Notification action</span><span class="sxs-lookup"><span data-stu-id="b5d6a-173">Notification action</span></span>

<span data-ttu-id="b5d6a-174">To create a notification action in the action group:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-174">To create a notification action in the action group:</span></span>

1. <span data-ttu-id="b5d6a-175">Under **Actions**, for **ACTION NAME**, enter a name for the action.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-175">Under **Actions**, for **ACTION NAME**, enter a name for the action.</span></span> <span data-ttu-id="b5d6a-176">For **ACTION TYPE**, select **Email**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-176">For **ACTION TYPE**, select **Email**.</span></span>  
1. <span data-ttu-id="b5d6a-177">Under **DETAILS** select, **Edit Details**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-177">Under **DETAILS** select, **Edit Details**.</span></span>  
1. <span data-ttu-id="b5d6a-178">On the **Email** page, enter the email address to use for notification, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-178">On the **Email** page, enter the email address to use for notification, and then select **OK**.</span></span> <span data-ttu-id="b5d6a-179">Adding an email address in addition to the runbook as an action is helpful.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-179">Adding an email address in addition to the runbook as an action is helpful.</span></span> <span data-ttu-id="b5d6a-180">You are notified when the runbook is started.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-180">You are notified when the runbook is started.</span></span>  

    <span data-ttu-id="b5d6a-181">Your action group should look like the following image:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-181">Your action group should look like the following image:</span></span>

   ![Add action group page](./media/automation-create-alert-triggered-runbook/add-action-group.png)
1. <span data-ttu-id="b5d6a-183">To create the action group, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-183">To create the action group, select **OK**.</span></span>

<span data-ttu-id="b5d6a-184">You can use this action group in the [activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts.md?toc=%2fazure%2fautomation%2ftoc.json) and [near real-time alerts](../monitoring-and-diagnostics/monitor-alerts-unified-usage.md?toc=%2fazure%2fautomation%2ftoc.json#create-an-alert-rule-with-the-azure-portal) that you create.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-184">You can use this action group in the [activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts.md?toc=%2fazure%2fautomation%2ftoc.json) and [near real-time alerts](../monitoring-and-diagnostics/monitor-alerts-unified-usage.md?toc=%2fazure%2fautomation%2ftoc.json#create-an-alert-rule-with-the-azure-portal) that you create.</span></span>

## <a name="classic-alert"></a><span data-ttu-id="b5d6a-185">Classic alert</span><span class="sxs-lookup"><span data-stu-id="b5d6a-185">Classic alert</span></span>

<span data-ttu-id="b5d6a-186">Classic alerts are based on metrics, and do not use action groups.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-186">Classic alerts are based on metrics, and do not use action groups.</span></span> <span data-ttu-id="b5d6a-187">However, you can set up a runbook action based on a classic alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-187">However, you can set up a runbook action based on a classic alert.</span></span> 

<span data-ttu-id="b5d6a-188">To create a classic alert:</span><span class="sxs-lookup"><span data-stu-id="b5d6a-188">To create a classic alert:</span></span>

1. <span data-ttu-id="b5d6a-189">Select **Add metric alert**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-189">Select **Add metric alert**.</span></span>
1. <span data-ttu-id="b5d6a-190">Name your metric alert **myVMCPUAlert**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-190">Name your metric alert **myVMCPUAlert**.</span></span> <span data-ttu-id="b5d6a-191">Enter a brief description for the alert.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-191">Enter a brief description for the alert.</span></span>
1. <span data-ttu-id="b5d6a-192">For the metric alert condition, select **Greater than**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-192">For the metric alert condition, select **Greater than**.</span></span> <span data-ttu-id="b5d6a-193">For the **Threshold** value, select **10**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-193">For the **Threshold** value, select **10**.</span></span> <span data-ttu-id="b5d6a-194">For the **Period** value, select **Over the last five minutes**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-194">For the **Period** value, select **Over the last five minutes**.</span></span>
1. <span data-ttu-id="b5d6a-195">Under **Take action**, select **Run a runbook from this alert**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-195">Under **Take action**, select **Run a runbook from this alert**.</span></span>
1. <span data-ttu-id="b5d6a-196">On the **Configure Runbook** page, for **Runbook source**, select **User**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-196">On the **Configure Runbook** page, for **Runbook source**, select **User**.</span></span> <span data-ttu-id="b5d6a-197">Choose your automation account, and then select the **Stop-AzureVmInResponsetoVMAlert** runbook.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-197">Choose your automation account, and then select the **Stop-AzureVmInResponsetoVMAlert** runbook.</span></span> <span data-ttu-id="b5d6a-198">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-198">Select **OK**.</span></span>
1. <span data-ttu-id="b5d6a-199">To save the alert rule, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5d6a-199">To save the alert rule, select **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5d6a-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5d6a-200">Next steps</span></span>

* <span data-ttu-id="b5d6a-201">For more information about starting an Automation runbook by using a webhook, see [Start a runbook from a webhook](automation-webhooks.md).</span><span class="sxs-lookup"><span data-stu-id="b5d6a-201">For more information about starting an Automation runbook by using a webhook, see [Start a runbook from a webhook](automation-webhooks.md).</span></span>
* <span data-ttu-id="b5d6a-202">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="b5d6a-202">For details about different ways to start a runbook, see [Starting a runbook](automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="b5d6a-203">To learn how to create an activity log alert, see [Create activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts.md?toc=%2fazure%2fautomation%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b5d6a-203">To learn how to create an activity log alert, see [Create activity log alerts](../monitoring-and-diagnostics/monitoring-activity-log-alerts.md?toc=%2fazure%2fautomation%2ftoc.json).</span></span>
* <span data-ttu-id="b5d6a-204">To learn how to create a near real-time alert, see [Create an alert rule in the Azure portal](../monitoring-and-diagnostics/monitor-alerts-unified-usage.md?toc=%2fazure%2fautomation%2ftoc.json#create-an-alert-rule-with-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="b5d6a-204">To learn how to create a near real-time alert, see [Create an alert rule in the Azure portal](../monitoring-and-diagnostics/monitor-alerts-unified-usage.md?toc=%2fazure%2fautomation%2ftoc.json#create-an-alert-rule-with-the-azure-portal).</span></span>
