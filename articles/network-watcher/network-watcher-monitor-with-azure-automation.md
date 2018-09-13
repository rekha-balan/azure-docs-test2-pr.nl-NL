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
# <a name="monitor-vpn-gateways-with-network-watcher-troubleshooting"></a>Monitor VPN gateways with Network Watcher troubleshooting

Gaining deep insights on your network performance is critical to provide reliable services to customers. It is therefore critical to detect network outage conditions quickly and take corrective action to mitigate the outage condition. Azure Automation enables you to implement and run a task in a programmatic fashion through runbooks. Using Azure Automation creates a perfect recipe for performing continuous and proactive network monitoring and alerting.

## <a name="scenario"></a>Scenario

The scenario in the following image is a multi-tiered application, with on premises connectivity established using a VPN Gateway and tunnel. Ensuring the VPN Gateway is up and running is critical to the applications performance.

A runbook is created with a script to check for connection status of the VPN tunnel, using the Resource Troubleshooting API to check for connection tunnel status. If the status is not healthy, an email trigger is sent to administrators.

![Scenario example][scenario]

This scenario will:

- Create a runbook calling the `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet to troubleshoot connection status
- Link a schedule to the runbook

## <a name="before-you-begin"></a>Before you begin

Before you start this scenario, you must have the following pre-requisites:

- An Azure automation account in Azure.
- You must have a set of credentials configure in Azure Automation. Learn more at [Azure Automation security](../automation/automation-security-overview.md)
- A valid SMTP server (Office 365, your on-premises email or another) and credentials defined in Azure Automation
- A configured Virtual Network Gateway in Azure.

> [!NOTE]
> The infrastructure depicted in the preceding image is for illustration purposes and are not created with the steps contained in this article.

### <a name="create-the-runbook"></a>Create the runbook

The first step to configuring the example is to create the runbook. This example uses a run-as account. To learn about run-as accounts, visit [Authenticate Runbooks with Azure Run As account](../automation/automation-sec-configure-azure-runas-account.md#create-an-automation-account-from-the-azure-portal)

### <a name="step-1"></a>Step 1

Navigate to Azure Automation in the [Azure portal](https://portal.azure.com) and click **Runbooks**

![automation account overview][1]

### <a name="step-2"></a>Step 2

Click **Add a runbook** to start the creation process of the runbook.

![runbooks blade][2]

### <a name="step-3"></a>Step 3

Under **Quick Create**, click **Create a new runbook** to create the runbook.

![add a runbook blade][3]

### <a name="step-4"></a>Step 4

In this step, we give the runbook a name, in the example it is called **Get-VPNGatewayStatus**. It is important to give the runbook a descriptive name, and recommended giving it a name that follows standard PowerShell naming standards. The runbook type for this example is **PowerShell**, the other options are Graphical, PowerShell workflow, and Graphical PowerShell workflow.

![runbook blade][4]

### <a name="step-5"></a>Step 5

In this step the runbook is created, the following code example provides all the code needed for the example. The items in the code that contain \<value\> need to be replaced with the values from your subscription.

Use the following code as click **Save**

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

### <a name="step-6"></a>Step 6

Once the runbook is saved, a schedule must be linked to it to automate the start of the runbook. To start the process, click **Schedule**.

![Step 6][6]

## <a name="link-a-schedule-to-the-runbook"></a>Link a schedule to the runbook

A new schedule must be created. Click **Link a schedule to your runbook**.

![Step 7][7]

### <a name="step-1"></a>Step 1

On the **Schedule** blade, click **Create a new schedule**

![Step 8][8]

### <a name="step-2"></a>Step 2

On the **New Schedule** blade fill out the schedule information. The values that can be set are in the following list:

- **Name** - The friendly name of the schedule.
- **Description** - A description of the schedule.
- **Starts** - This value is a combination of date, time, and time zone that make up the time the schedule triggers.
- **Recurrence** - This value determines the schedules repetition.  Valid values are **Once** or **Recurring**.
- **Recur every** - The recurrence interval of the schedule in hours, days, weeks, or months.
- **Set Expiration** - The value determines if the schedule should expire or not. Can be set to **Yes** or **No**. A valid date and time are to be provided if yes is chosen.

> [!NOTE]
> If you need to have a runbook run more often than every hour, multiple schedules must be created at different intervals (that is, 15, 30, 45 minutes after the hour)

![Step 9][9]

### <a name="step-3"></a>Step 3

Click Save to save the schedule to the runbook.

![Step 10][10]

## <a name="next-steps"></a>Next steps

Now that you have an understanding on how to integrate Network Watcher troubleshooting with Azure Automation, learn how to trigger packet captures on VM alerts by visiting [Create an alert triggered packet capture with Azure Network Watcher](network-watcher-alert-triggered-packet-capture.md).

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











