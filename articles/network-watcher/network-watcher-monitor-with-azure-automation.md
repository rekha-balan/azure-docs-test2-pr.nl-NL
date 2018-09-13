---
title: Monitor VPN gateways with Azure Network Watcher troubleshooting | Microsoft Docs
description: This article describes how diagnose On-premises connectivity with Azure Automation and Network Watcher
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 01a240b075c1f2b6ad0528b932286ae115532d86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551221"
---
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a><span data-ttu-id="fa6aa-103">Monitor VPN gateways with Network Watcher troubleshooting</span><span class="sxs-lookup"><span data-stu-id="fa6aa-103">Monitor VPN gateways with Network Watcher troubleshooting</span></span>

<span data-ttu-id="fa6aa-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-104">Gaining deep insights on your network performance is critical to provide reliable services to customers.</span></span> <span data-ttu-id="fa6aa-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-105">It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition.</span></span> <span data-ttu-id="fa6aa-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-106">Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks.</span></span> <span data-ttu-id="fa6aa-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-107">Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.</span></span>

## <a name="scenario"></a><span data-ttu-id="fa6aa-108">Scenario</span><span class="sxs-lookup"><span data-stu-id="fa6aa-108">Scenario</span></span>

<span data-ttu-id="fa6aa-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-109">The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel.</span></span> <span data-ttu-id="fa6aa-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-110">Ensuring the VPN Gateway is up and running is critical to the applications performance.</span></span>

<span data-ttu-id="fa6aa-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-111">A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status.</span></span> <span data-ttu-id="fa6aa-112">If the status is not healthy, an email trigger is sent to administrators.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-112">If the status is not healthy, an email trigger is sent to administrators.</span></span>

![Scenario example][scenario]

<span data-ttu-id="fa6aa-114">This scenario will:</span><span class="sxs-lookup"><span data-stu-id="fa6aa-114">This scenario will:</span></span>

- <span data-ttu-id="fa6aa-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span><span class="sxs-lookup"><span data-stu-id="fa6aa-115">Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status</span></span>
- <span data-ttu-id="fa6aa-116">Link a schedule to the runbook</span><span class="sxs-lookup"><span data-stu-id="fa6aa-116">Link a schedule to the runbook</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fa6aa-117">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fa6aa-117">Before you begin</span></span>

<span data-ttu-id="fa6aa-118">Before you start this scenario, you must have the following pre-requisites:</span><span class="sxs-lookup"><span data-stu-id="fa6aa-118">Before you start this scenario, you must have the following pre-requisites:</span></span>

- <span data-ttu-id="fa6aa-119">An Azure automation account in Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-119">An Azure automation account in Azure.</span></span>
- <span data-ttu-id="fa6aa-120">You must have a set of credentials configure in Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-120">You must have a set of credentials configure in Azure Automation.</span></span> <span data-ttu-id="fa6aa-121">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fa6aa-121">Learn more at [Azure Automation security](../automation/automation-security-overview.md)</span></span>
- <span data-ttu-id="fa6aa-122">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span><span class="sxs-lookup"><span data-stu-id="fa6aa-122">A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation</span></span>
- <span data-ttu-id="fa6aa-123">A configured Virtual Network Gateway in Azure.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-123">A configured Virtual Network Gateway in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="fa6aa-124">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-124">The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.</span></span>

### <a name="create-the-runbook"></a><span data-ttu-id="fa6aa-125">Create the runbook</span><span class="sxs-lookup"><span data-stu-id="fa6aa-125">Create the runbook</span></span>

<span data-ttu-id="fa6aa-126">The first step to configuring the example is to create the runbook.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-126">The first step to configuring the example is to create the runbook.</span></span> <span data-ttu-id="fa6aa-127">This example uses a run-as account.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-127">This example uses a run-as account.</span></span> <span data-ttu-id="fa6aa-128">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md#create-an-automation-account-from-the-azure-portal)</span><span class="sxs-lookup"><span data-stu-id="fa6aa-128">To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md#create-an-automation-account-from-the-azure-portal)</span></span>

### <a name="step-1"></a><span data-ttu-id="fa6aa-129">Step 1</span><span class="sxs-lookup"><span data-stu-id="fa6aa-129">Step 1</span></span>

<span data-ttu-id="fa6aa-130">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span><span class="sxs-lookup"><span data-stu-id="fa6aa-130">Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**</span></span>

![automation account overview][1]

### <a name="step-2"></a><span data-ttu-id="fa6aa-132">Step 2</span><span class="sxs-lookup"><span data-stu-id="fa6aa-132">Step 2</span></span>

<span data-ttu-id="fa6aa-133">Click **Add a runbook** to start the creation process of the runbook.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-133">Click **Add a runbook** to start the creation process of the runbook.</span></span>

![runbooks blade][2]

### <a name="step-3"></a><span data-ttu-id="fa6aa-135">Step 3</span><span class="sxs-lookup"><span data-stu-id="fa6aa-135">Step 3</span></span>

<span data-ttu-id="fa6aa-136">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-136">Under **Quick Create**, click **Create a new runbook** to create the runbook.</span></span>

![add a runbook blade][3]

### <a name="step-4"></a><span data-ttu-id="fa6aa-138">Step 4</span><span class="sxs-lookup"><span data-stu-id="fa6aa-138">Step 4</span></span>

<span data-ttu-id="fa6aa-139">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-139">In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**.</span></span> <span data-ttu-id="fa6aa-140">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-140">It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards.</span></span> <span data-ttu-id="fa6aa-141">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-141">The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.</span></span>

![runbook blade][4]

### <a name="step-5"></a><span data-ttu-id="fa6aa-143">Step 5</span><span class="sxs-lookup"><span data-stu-id="fa6aa-143">Step 5</span></span>

<span data-ttu-id="fa6aa-144">In this step the runbook is created, the following code example provides all the code needed for the example.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-144">In this step the runbook is created, the following code example provides all the code needed for the example.</span></span> <span data-ttu-id="fa6aa-145">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-145">The items in the code that contain \<value\> need to be replaced with the values from your subscription.</span></span>

<span data-ttu-id="fa6aa-146">Use the following code as click **Save**</span><span class="sxs-lookup"><span data-stu-id="fa6aa-146">Use the following code as click **Save**</span></span>

```PowerShell
# Get credentials for Office 365 account
$MyCredential = "Office 365 account"
$Cred = Get-AutomationPSCredential -Name $MyCredential

# Get the connection "AzureRunAsConnection "
$connectionName = "AzureRunAsConnection"
$servicePrincipalConnection=Get-AutomationConnection -Name $connectionName
$subscriptionId = "<subscription id>"
"Logging in to Azure..."
Add-AzureRmAccount `
    -ServicePrincipal `
    -TenantId $servicePrincipalConnection.TenantId `
    -ApplicationId $servicePrincipalConnection.ApplicationId `
    -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
"Setting context to a specific subscription"
Set-AzureRmContext -SubscriptionId $subscriptionId

$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
$result = Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)logs"


if($result.code -ne "Healthy")
    {
        $Body = "Connection for ${vpnconnectionName} is: $($result.code). View the logs at $($sa.PrimaryEndpoints.Blob)logs to learn more."
        $subject = "${connectionname} Status"
        Send-MailMessage `
        -To 'admin@contoso.com' `
        -Subject $subject `
        -Body $Body `
        -UseSsl `
        -Port 587 `
        -SmtpServer 'smtp.office365.com' `
        -From "${$username}" `
        -BodyAsHtml `
        -Credential $Cred
    }
else
    {
    Write-Output ("Connection Status is: $($result.connectionStatus)")
    }
```

![Step 5][5]

### <a name="step-6"></a><span data-ttu-id="fa6aa-148">Step 6</span><span class="sxs-lookup"><span data-stu-id="fa6aa-148">Step 6</span></span>

<span data-ttu-id="fa6aa-149">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-149">Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook.</span></span> <span data-ttu-id="fa6aa-150">To start the process, click **Schedule**.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-150">To start the process, click **Schedule**.</span></span>

![Step 6][6]

## <a name="link-a-schedule-to-the-runbook"></a><span data-ttu-id="fa6aa-152">Link a schedule to the runbook</span><span class="sxs-lookup"><span data-stu-id="fa6aa-152">Link a schedule to the runbook</span></span>

<span data-ttu-id="fa6aa-153">A new schedule must be created.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-153">A new schedule must be created.</span></span> <span data-ttu-id="fa6aa-154">Click **Link a schedule to your runbook**.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-154">Click **Link a schedule to your runbook**.</span></span>

![Step 7][7]

### <a name="step-1"></a><span data-ttu-id="fa6aa-156">Step 1</span><span class="sxs-lookup"><span data-stu-id="fa6aa-156">Step 1</span></span>

<span data-ttu-id="fa6aa-157">On the **Schedule** blade, click **Create a new schedule**</span><span class="sxs-lookup"><span data-stu-id="fa6aa-157">On the **Schedule** blade, click **Create a new schedule**</span></span>

![Step 8][8]

### <a name="step-2"></a><span data-ttu-id="fa6aa-159">Step 2</span><span class="sxs-lookup"><span data-stu-id="fa6aa-159">Step 2</span></span>

<span data-ttu-id="fa6aa-160">On the **New Schedule** blade fill out the schedule information.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-160">On the **New Schedule** blade fill out the schedule information.</span></span> <span data-ttu-id="fa6aa-161">The values that can be set are in the following list:</span><span class="sxs-lookup"><span data-stu-id="fa6aa-161">The values that can be set are in the following list:</span></span>

- <span data-ttu-id="fa6aa-162">**Name** - The friendly name of the schedule.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-162">**Name** - The friendly name of the schedule.</span></span>
- <span data-ttu-id="fa6aa-163">**Description** - A description of the schedule.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-163">**Description** - A description of the schedule.</span></span>
- <span data-ttu-id="fa6aa-164">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-164">**Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.</span></span>
- <span data-ttu-id="fa6aa-165">**Recurrence** - This value determines the schedules repetition.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-165">**Recurrence** - This value determines the schedules repetition.</span></span>  <span data-ttu-id="fa6aa-166">Valid values are **Once** or **Recurring**.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-166">Valid values are **Once** or **Recurring**.</span></span>
- <span data-ttu-id="fa6aa-167">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-167">**Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.</span></span>
- <span data-ttu-id="fa6aa-168">**Set Expiration** - The value determines if the schedule should expire or not.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-168">**Set Expiration** - The value determines if the schedule should expire or not.</span></span> <span data-ttu-id="fa6aa-169">Can be set to **Yes** or **No**.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-169">Can be set to **Yes** or **No**.</span></span> <span data-ttu-id="fa6aa-170">A valid date and time are to be provided if yes is chosen.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-170">A valid date and time are to be provided if yes is chosen.</span></span>

> [!NOTE]
> <span data-ttu-id="fa6aa-171">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span><span class="sxs-lookup"><span data-stu-id="fa6aa-171">If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)</span></span>

![Step 9][9]

### <a name="step-3"></a><span data-ttu-id="fa6aa-173">Step 3</span><span class="sxs-lookup"><span data-stu-id="fa6aa-173">Step 3</span></span>

<span data-ttu-id="fa6aa-174">Click Save to save the schedule to the runbook.</span><span class="sxs-lookup"><span data-stu-id="fa6aa-174">Click Save to save the schedule to the runbook.</span></span>

![Step 10][10]

## <a name="next-steps"></a><span data-ttu-id="fa6aa-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="fa6aa-176">Next steps</span></span>

<span data-ttu-id="fa6aa-177">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span><span class="sxs-lookup"><span data-stu-id="fa6aa-177">Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).</span></span>

<!-- images -->
[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/scenario.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure2.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure3.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure4.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure5.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure6.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure7.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure8.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure9.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-monitor-with-azure-automation/figure10.png











