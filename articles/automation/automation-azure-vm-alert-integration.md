---
title: " Remediate Azure VM Alerts with Automation Runbooks | Microsoft Docs"
description: This article demonstrates how to integrate Azure Virtual Machine alerts with Azure Automation runbooks and auto-remediate issues
services: automation
documentationcenter: ''
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1f7baa7f-7283-4a4f-9385-3f5cd1062c7f
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/14/2016
ms.author: csand;magoedte
ms.openlocfilehash: bc9a10022de7bc49986a3c5ddeae6c79cc26d1ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563096"
---
# <a name="azure-automation-scenario---remediate-azure-vm-alerts"></a><span data-ttu-id="37fd4-103">Azure Automation scenario - remediate Azure VM alerts</span><span class="sxs-lookup"><span data-stu-id="37fd4-103">Azure Automation scenario - remediate Azure VM alerts</span></span>
<span data-ttu-id="37fd4-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span><span class="sxs-lookup"><span data-stu-id="37fd4-104">Azure Automation and Azure Virtual Machines have released a new feature allowing you to configure Virtual Machine (VM) alerts to run Automation runbooks.</span></span> <span data-ttu-id="37fd4-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span><span class="sxs-lookup"><span data-stu-id="37fd4-105">This new capability allows you to automatically perform standard remediation in response to VM alerts, like restarting or stopping the VM.</span></span>

<span data-ttu-id="37fd4-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span><span class="sxs-lookup"><span data-stu-id="37fd4-106">Previously, during VM alert rule creation you were able to [specify an Automation webhook](https://azure.microsoft.com/blog/using-azure-automation-to-take-actions-on-azure-alerts/) to a runbook in order to run the runbook whenever the alert triggered.</span></span> <span data-ttu-id="37fd4-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span><span class="sxs-lookup"><span data-stu-id="37fd4-107">However, this required you to do the work of creating the runbook, creating the webhook for the runbook, and then copying and pasting the webhook during alert rule creation.</span></span> <span data-ttu-id="37fd4-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span><span class="sxs-lookup"><span data-stu-id="37fd4-108">With this new release, the process is much easier because you can directly choose a runbook from a list during alert rule creation, and you can choose an Automation account which will run the runbook or easily create an account.</span></span>

<span data-ttu-id="37fd4-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="37fd4-109">In this article, we will show you how easy it is to set up an Azure VM alert and configure an Automation runbook to run whenever the alert triggers.</span></span> <span data-ttu-id="37fd4-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span><span class="sxs-lookup"><span data-stu-id="37fd4-110">Example scenarios include restarting a VM when the memory usage exceeds some threshold due to an application on the VM with a memory leak, or stopping a VM when the CPU user time has been below 1% for past hour and is not in use.</span></span> <span data-ttu-id="37fd4-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span><span class="sxs-lookup"><span data-stu-id="37fd4-111">We’ll also explain how the automated creation of a service principal in your Automation account simplifies the use of runbooks in Azure alert remediation.</span></span>

## <a name="create-an-alert-on-a-vm"></a><span data-ttu-id="37fd4-112">Create an alert on a VM</span><span class="sxs-lookup"><span data-stu-id="37fd4-112">Create an alert on a VM</span></span>
<span data-ttu-id="37fd4-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span><span class="sxs-lookup"><span data-stu-id="37fd4-113">Perform the following steps to configure an alert to launch a runbook when its threshold has been met.</span></span>

> [!NOTE]
> <span data-ttu-id="37fd4-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span><span class="sxs-lookup"><span data-stu-id="37fd4-114">With this release, we only support V2 virtual machines and support for classic VMs will be added soon.</span></span>  
> 
> 

1. <span data-ttu-id="37fd4-115">Log in to the Azure portal and click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="37fd4-115">Log in to the Azure portal and click **Virtual Machines**.</span></span>  
2. <span data-ttu-id="37fd4-116">Select one of your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="37fd4-116">Select one of your virtual machines.</span></span>  <span data-ttu-id="37fd4-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span><span class="sxs-lookup"><span data-stu-id="37fd4-117">The virtual machine dashboard blade will appear and the **Settings** blade to its right.</span></span>  
3. <span data-ttu-id="37fd4-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span><span class="sxs-lookup"><span data-stu-id="37fd4-118">From the **Settings** blade, under the Monitoring section select **Alert rules**.</span></span>
4. <span data-ttu-id="37fd4-119">On the **Alert rules** blade, click **Add alert**.</span><span class="sxs-lookup"><span data-stu-id="37fd4-119">On the **Alert rules** blade, click **Add alert**.</span></span>

<span data-ttu-id="37fd4-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span><span class="sxs-lookup"><span data-stu-id="37fd4-120">This opens up the **Add an alert rule** blade, where you can configure the conditions for the alert and choose among one or all of these options: send email to someone, use a webhook to forward the alert to another system, and/or run an Automation runbook in response attempt to remediate the issue.</span></span>

## <a name="configure-a-runbook"></a><span data-ttu-id="37fd4-121">Configure a runbook</span><span class="sxs-lookup"><span data-stu-id="37fd4-121">Configure a runbook</span></span>
<span data-ttu-id="37fd4-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span><span class="sxs-lookup"><span data-stu-id="37fd4-122">To configure a runbook to run when the VM alert threshold is met, select **Automation Runbook**.</span></span> <span data-ttu-id="37fd4-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span><span class="sxs-lookup"><span data-stu-id="37fd4-123">In the **Configure runbook** blade, you can select the runbook to run and the Automation account to run the runbook in.</span></span>

![Configure an Automation runbook and create a new Automation Account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-azure-vm-alert-integration/ConfigureRunbookNewAccount.png)

> [!NOTE]
> <span data-ttu-id="37fd4-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span><span class="sxs-lookup"><span data-stu-id="37fd4-125">For this release you can choose from three runbooks that the service provides – Restart VM, Stop VM, or Remove VM (delete it).</span></span>  <span data-ttu-id="37fd4-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span><span class="sxs-lookup"><span data-stu-id="37fd4-126">The ability to select other runbooks or one of your own runbooks will be available in a future release.</span></span>
> 
> 

![Runbooks to choose from](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-azure-vm-alert-integration/RunbooksToChoose.png)

<span data-ttu-id="37fd4-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span><span class="sxs-lookup"><span data-stu-id="37fd4-128">After you select one of the three available runbooks, the **Automation account** drop-down list appears and you can select an automation account the runbook will run as.</span></span> <span data-ttu-id="37fd4-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="37fd4-129">Runbooks need to run in the context of an [Automation account](automation-security-overview.md) that is in your Azure subscription.</span></span> <span data-ttu-id="37fd4-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span><span class="sxs-lookup"><span data-stu-id="37fd4-130">You can select an Automation account that you already created, or you can have a new Automation account created for you.</span></span>

<span data-ttu-id="37fd4-131">The runbooks that are provided authenticate to Azure using a service principal.</span><span class="sxs-lookup"><span data-stu-id="37fd4-131">The runbooks that are provided authenticate to Azure using a service principal.</span></span> <span data-ttu-id="37fd4-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span><span class="sxs-lookup"><span data-stu-id="37fd4-132">If you choose to run the runbook in one of your existing Automation accounts, we will automatically create the service principal for you.</span></span> <span data-ttu-id="37fd4-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span><span class="sxs-lookup"><span data-stu-id="37fd4-133">If you choose to create a new Automation account, then we will automatically create the account and the service principal.</span></span> <span data-ttu-id="37fd4-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span><span class="sxs-lookup"><span data-stu-id="37fd4-134">In both cases, two assets will also be created in the Automation account – a certificate asset named **AzureRunAsCertificate** and a connection asset named **AzureRunAsConnection**.</span></span> <span data-ttu-id="37fd4-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span><span class="sxs-lookup"><span data-stu-id="37fd4-135">The runbooks will use **AzureRunAsConnection** to authenticate with Azure in order to perform the management action against the VM.</span></span>

> [!NOTE]
> <span data-ttu-id="37fd4-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span><span class="sxs-lookup"><span data-stu-id="37fd4-136">The service principal is created in the subscription scope and is assigned the Contributor role.</span></span> <span data-ttu-id="37fd4-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="37fd4-137">This role is required in order for the account to have permission to run Automation runbooks to manage Azure VMs.</span></span>  <span data-ttu-id="37fd4-138">The creation of an Automaton account and/or service principal is a one-time event.</span><span class="sxs-lookup"><span data-stu-id="37fd4-138">The creation of an Automaton account and/or service principal is a one-time event.</span></span> <span data-ttu-id="37fd4-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span><span class="sxs-lookup"><span data-stu-id="37fd4-139">Once they are created, you can use that account to run runbooks for other Azure VM alerts.</span></span>
> 
> 

<span data-ttu-id="37fd4-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span><span class="sxs-lookup"><span data-stu-id="37fd4-140">When you click **OK** the alert is configured and if you selected the option to create a new Automation account, it is created along with the service principal.</span></span>  <span data-ttu-id="37fd4-141">This can take a few seconds to complete.</span><span class="sxs-lookup"><span data-stu-id="37fd4-141">This can take a few seconds to complete.</span></span>  

![Runbook being configured](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-azure-vm-alert-integration/RunbookBeingConfigured.png)

<span data-ttu-id="37fd4-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span><span class="sxs-lookup"><span data-stu-id="37fd4-143">After the configuration is completed you will see the name of the runbook appear in the **Add an alert rule** blade.</span></span>

![Runbook configured](https://docstestmedia1.blob.core.windows.net/azure-media/articles/automation/media/automation-azure-vm-alert-integration/RunbookConfigured.png)

<span data-ttu-id="37fd4-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span><span class="sxs-lookup"><span data-stu-id="37fd4-145">Click **OK** in the **Add an alert rule** blade and the alert rule will be created and activate if the virtual machine is in a running state.</span></span>

### <a name="enable-or-disable-a-runbook"></a><span data-ttu-id="37fd4-146">Enable or disable a runbook</span><span class="sxs-lookup"><span data-stu-id="37fd4-146">Enable or disable a runbook</span></span>
<span data-ttu-id="37fd4-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span><span class="sxs-lookup"><span data-stu-id="37fd4-147">If you have a runbook configured for an alert, you can disable it without removing the runbook configuration.</span></span> <span data-ttu-id="37fd4-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span><span class="sxs-lookup"><span data-stu-id="37fd4-148">This allows you to keep the alert running and perhaps test some of the alert rules and then later re-enable the runbook.</span></span>

## <a name="create-a-runbook-that-works-with-an-azure-alert"></a><span data-ttu-id="37fd4-149">Create a runbook that works with an Azure alert</span><span class="sxs-lookup"><span data-stu-id="37fd4-149">Create a runbook that works with an Azure alert</span></span>
<span data-ttu-id="37fd4-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span><span class="sxs-lookup"><span data-stu-id="37fd4-150">When you choose a runbook as part of an Azure alert rule, the runbook needs to have logic in it to manage the alert data that is passed to it.</span></span>  <span data-ttu-id="37fd4-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="37fd4-151">When a runbook is configured in an alert rule, a webhook is created for the runbook; that webhook is then used to start the runbook each time the alert triggers.</span></span>  <span data-ttu-id="37fd4-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span><span class="sxs-lookup"><span data-stu-id="37fd4-152">The actual call to start the runbook is an HTTP POST request to the webhook URL.</span></span> <span data-ttu-id="37fd4-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span><span class="sxs-lookup"><span data-stu-id="37fd4-153">The body of the POST request contains a JSON-formated object that contains useful properties related to the alert.</span></span>  <span data-ttu-id="37fd4-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span><span class="sxs-lookup"><span data-stu-id="37fd4-154">As you can see below, the alert data contains details like subscriptionID, resourceGroupName, resourceName, and resourceType.</span></span>

### <a name="example-of-alert-data"></a><span data-ttu-id="37fd4-155">Example of Alert data</span><span class="sxs-lookup"><span data-stu-id="37fd4-155">Example of Alert data</span></span>
```
{
    "WebhookName": "AzureAlertTest",
    "RequestBody": "{
    \"status\":\"Activated\",
    \"context\": {
        \"id\":\"/subscriptions/<subscriptionId>/resourceGroups/MyResourceGroup/providers/microsoft.insights/alertrules/AlertTest\",
        \"name\":\"AlertTest\",
        \"description\":\"\",
        \"condition\": {
            \"metricName\":\"CPU percentage guest OS\",
            \"metricUnit\":\"Percent\",
            \"metricValue\":\"4.26337916666667\",
            \"threshold\":\"1\",
            \"windowSize\":\"60\",
            \"timeAggregation\":\"Average\",
            \"operator\":\"GreaterThan\"},
        \"subscriptionId\":\<subscriptionID> \",
        \"resourceGroupName\":\"TestResourceGroup\",
        \"timestamp\":\"2016-04-24T23:19:50.1440170Z\",
        \"resourceName\":\"TestVM\",
        \"resourceType\":\"microsoft.compute/virtualmachines\",
        \"resourceRegion\":\"westus\",
        \"resourceId\":\"/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\",
        \"portalLink\":\"https://portal.azure.com/#resource/subscriptions/<subscriptionId>/resourceGroups/TestResourceGroup/providers/Microsoft.Compute/virtualMachines/TestVM\"
        },
    \"properties\":{}
    }",
    "RequestHeader": {
        "Connection": "Keep-Alive",
        "Host": "<webhookURL>"
    }
}
```

<span data-ttu-id="37fd4-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span><span class="sxs-lookup"><span data-stu-id="37fd4-156">When the Automation webhook service receives the HTTP POST it extracts the alert data and passes it to the runbook in the WebhookData runbook input parameter.</span></span>  <span data-ttu-id="37fd4-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span><span class="sxs-lookup"><span data-stu-id="37fd4-157">Below is a sample runbook that shows how to use the WebhookData parameter and extract the alert data and use it to manage the Azure resource that triggered the alert.</span></span>

### <a name="example-runbook"></a><span data-ttu-id="37fd4-158">Example runbook</span><span class="sxs-lookup"><span data-stu-id="37fd4-158">Example runbook</span></span>
```
#  This runbook will restart an ARM (V2) VM in response to an Azure VM alert.

[OutputType("PSAzureOperationResponse")]

param ( [object] $WebhookData )

if ($WebhookData)
{
    # Get the data object from WebhookData
    $WebhookBody = (ConvertFrom-Json -InputObject $WebhookData.RequestBody)

    # Assure that the alert status is 'Activated' (alert condition went from false to true)
    # and not 'Resolved' (alert condition went from true to false)
    if ($WebhookBody.status -eq "Activated")
    {
        # Get the info needed to identify the VM
        $AlertContext = [object] $WebhookBody.context
        $ResourceName = $AlertContext.resourceName
        $ResourceType = $AlertContext.resourceType
        $ResourceGroupName = $AlertContext.resourceGroupName
        $SubId = $AlertContext.subscriptionId

        # Assure that this is the expected resource type
        Write-Verbose "ResourceType: $ResourceType"
        if ($ResourceType -eq "microsoft.compute/virtualmachines")
        {
            # This is an ARM (V2) VM

            # Authenticate to Azure with service principal and certificate
            $ConnectionAssetName = "AzureRunAsConnection"
            $Conn = Get-AutomationConnection -Name $ConnectionAssetName
            if ($Conn -eq $null) {
                throw "Could not retrieve connection asset: $ConnectionAssetName. Check that this asset exists in the Automation account."
            }
            Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint | Write-Verbose
            Set-AzureRmContext -SubscriptionId $SubId -ErrorAction Stop | Write-Verbose

            # Restart the VM
            Restart-AzureRmVM -Name $ResourceName -ResourceGroupName $ResourceGroupName
        } else {
            Write-Error "$ResourceType is not a supported resource type for this runbook."
        }
    } else {
        # The alert status was not 'Activated' so no action taken
        Write-Verbose ("No action taken. Alert status: " + $WebhookBody.status)
    }
} else {
    Write-Error "This runbook is meant to be started from an Azure alert only."
}
```

## <a name="summary"></a><span data-ttu-id="37fd4-159">Summary</span><span class="sxs-lookup"><span data-stu-id="37fd4-159">Summary</span></span>
<span data-ttu-id="37fd4-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="37fd4-160">When you configure an alert on an Azure VM, you now have the ability to easily configure an Automation runbook to automatically perform remediation action when the alert triggers.</span></span> <span data-ttu-id="37fd4-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span><span class="sxs-lookup"><span data-stu-id="37fd4-161">For this release, you can choose from runbooks to restart, stop, or delete a VM depending on your alert scenario.</span></span> <span data-ttu-id="37fd4-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span><span class="sxs-lookup"><span data-stu-id="37fd4-162">This is just the beginning of enabling scenarios where you control the actions (notification, troubleshooting, remediation) that will be taken automatically when an alert triggers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37fd4-163">Next Steps</span><span class="sxs-lookup"><span data-stu-id="37fd4-163">Next Steps</span></span>
* <span data-ttu-id="37fd4-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span><span class="sxs-lookup"><span data-stu-id="37fd4-164">To get started with Graphical runbooks, see [My first graphical runbook](automation-first-runbook-graphical.md)</span></span>
* <span data-ttu-id="37fd4-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span><span class="sxs-lookup"><span data-stu-id="37fd4-165">To get started with PowerShell workflow runbooks, see [My first PowerShell workflow runbook](automation-first-runbook-textual.md)</span></span>
* <span data-ttu-id="37fd4-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span><span class="sxs-lookup"><span data-stu-id="37fd4-166">To learn more about runbook types, their advantages and limitations, see [Azure Automation runbook types](automation-runbook-types.md)</span></span>





