---
title: Vertically scale Azure virtual machine scale sets | Microsoft Docs
description: How to vertically scale a Virtual Machine in response to monitoring alerts with Azure Automation
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 16b17421-6b8f-483e-8a84-26327c44e9d3
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: negat
ms.openlocfilehash: 6e4733e023d1dc27fb099216f9afea07fe07446c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808150"
---
# <a name="vertical-autoscale-with-virtual-machine-scale-sets"></a><span data-ttu-id="5492e-103">Vertical autoscale with virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="5492e-103">Vertical autoscale with virtual machine scale sets</span></span>
<span data-ttu-id="5492e-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span><span class="sxs-lookup"><span data-stu-id="5492e-104">This article describes how to vertically scale Azure [Virtual Machine Scale Sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/) with or without reprovisioning.</span></span> <span data-ttu-id="5492e-105">For vertical scaling of VMs that are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5492e-105">For vertical scaling of VMs that are not in scale sets, refer to [Vertically scale Azure virtual machine with Azure Automation](../virtual-machines/windows/vertical-scaling-automation.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5492e-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span><span class="sxs-lookup"><span data-stu-id="5492e-106">Vertical scaling, also known as *scale up* and *scale down*, means increasing or decreasing virtual machine (VM) sizes in response to a workload.</span></span> <span data-ttu-id="5492e-107">Compare this behavior with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span><span class="sxs-lookup"><span data-stu-id="5492e-107">Compare this behavior with [horizontal scaling](virtual-machine-scale-sets-autoscale-overview.md), also referred to as *scale out* and *scale in*, where the number of VMs is altered depending on the workload.</span></span>

<span data-ttu-id="5492e-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span><span class="sxs-lookup"><span data-stu-id="5492e-108">Reprovisioning means removing an existing VM and replacing it with a new one.</span></span> <span data-ttu-id="5492e-109">When you increase or decrease the size of VMs in a virtual machine scale set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span><span class="sxs-lookup"><span data-stu-id="5492e-109">When you increase or decrease the size of VMs in a virtual machine scale set, in some cases you want to resize existing VMs and retain your data, while in other cases you need to deploy new VMs of the new size.</span></span> <span data-ttu-id="5492e-110">This document covers both cases.</span><span class="sxs-lookup"><span data-stu-id="5492e-110">This document covers both cases.</span></span>

<span data-ttu-id="5492e-111">Vertical scaling can be useful when:</span><span class="sxs-lookup"><span data-stu-id="5492e-111">Vertical scaling can be useful when:</span></span>

* <span data-ttu-id="5492e-112">A service built on virtual machines is under-utilized (for example at weekends).</span><span class="sxs-lookup"><span data-stu-id="5492e-112">A service built on virtual machines is under-utilized (for example at weekends).</span></span> <span data-ttu-id="5492e-113">Reducing the VM size can reduce monthly costs.</span><span class="sxs-lookup"><span data-stu-id="5492e-113">Reducing the VM size can reduce monthly costs.</span></span>
* <span data-ttu-id="5492e-114">Increasing VM size to cope with larger demand without creating additional VMs.</span><span class="sxs-lookup"><span data-stu-id="5492e-114">Increasing VM size to cope with larger demand without creating additional VMs.</span></span>

<span data-ttu-id="5492e-115">You can set up vertical scaling to be triggered based on metric based alerts from your virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="5492e-115">You can set up vertical scaling to be triggered based on metric based alerts from your virtual machine scale set.</span></span> <span data-ttu-id="5492e-116">When the alert is activated, it fires a webhook that triggers a runbook that can scale your scale set up or down.</span><span class="sxs-lookup"><span data-stu-id="5492e-116">When the alert is activated, it fires a webhook that triggers a runbook that can scale your scale set up or down.</span></span> <span data-ttu-id="5492e-117">Vertical scaling can be configured by following these steps:</span><span class="sxs-lookup"><span data-stu-id="5492e-117">Vertical scaling can be configured by following these steps:</span></span>

1. <span data-ttu-id="5492e-118">Create an Azure Automation account with run-as capability.</span><span class="sxs-lookup"><span data-stu-id="5492e-118">Create an Azure Automation account with run-as capability.</span></span>
2. <span data-ttu-id="5492e-119">Import Azure Automation Vertical Scale runbooks for virtual machine scale sets into your subscription.</span><span class="sxs-lookup"><span data-stu-id="5492e-119">Import Azure Automation Vertical Scale runbooks for virtual machine scale sets into your subscription.</span></span>
3. <span data-ttu-id="5492e-120">Add a webhook to your runbook.</span><span class="sxs-lookup"><span data-stu-id="5492e-120">Add a webhook to your runbook.</span></span>
4. <span data-ttu-id="5492e-121">Add an alert to your virtual machine scale set using a webhook notification.</span><span class="sxs-lookup"><span data-stu-id="5492e-121">Add an alert to your virtual machine scale set using a webhook notification.</span></span>

> [!NOTE]
> <span data-ttu-id="5492e-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span><span class="sxs-lookup"><span data-stu-id="5492e-122">Vertical autoscaling can only take place within certain ranges of VM sizes.</span></span> <span data-ttu-id="5492e-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span><span class="sxs-lookup"><span data-stu-id="5492e-123">Compare the specifications of each size before deciding to scale from one to another (higher number does not always indicate bigger VM size).</span></span> <span data-ttu-id="5492e-124">You can choose to scale between the following pairs of sizes:</span><span class="sxs-lookup"><span data-stu-id="5492e-124">You can choose to scale between the following pairs of sizes:</span></span>
> 
> | <span data-ttu-id="5492e-125">VM sizes scaling pair</span><span class="sxs-lookup"><span data-stu-id="5492e-125">VM sizes scaling pair</span></span> |  |
> | --- | --- |
> | <span data-ttu-id="5492e-126">Standard_A0</span><span class="sxs-lookup"><span data-stu-id="5492e-126">Standard_A0</span></span> |<span data-ttu-id="5492e-127">Standard_A11</span><span class="sxs-lookup"><span data-stu-id="5492e-127">Standard_A11</span></span> |
> | <span data-ttu-id="5492e-128">Standard_D1</span><span class="sxs-lookup"><span data-stu-id="5492e-128">Standard_D1</span></span> |<span data-ttu-id="5492e-129">Standard_D14</span><span class="sxs-lookup"><span data-stu-id="5492e-129">Standard_D14</span></span> |
> | <span data-ttu-id="5492e-130">Standard_DS1</span><span class="sxs-lookup"><span data-stu-id="5492e-130">Standard_DS1</span></span> |<span data-ttu-id="5492e-131">Standard_DS14</span><span class="sxs-lookup"><span data-stu-id="5492e-131">Standard_DS14</span></span> |
> | <span data-ttu-id="5492e-132">Standard_D1v2</span><span class="sxs-lookup"><span data-stu-id="5492e-132">Standard_D1v2</span></span> |<span data-ttu-id="5492e-133">Standard_D15v2</span><span class="sxs-lookup"><span data-stu-id="5492e-133">Standard_D15v2</span></span> |
> | <span data-ttu-id="5492e-134">Standard_G1</span><span class="sxs-lookup"><span data-stu-id="5492e-134">Standard_G1</span></span> |<span data-ttu-id="5492e-135">Standard_G5</span><span class="sxs-lookup"><span data-stu-id="5492e-135">Standard_G5</span></span> |
> | <span data-ttu-id="5492e-136">Standard_GS1</span><span class="sxs-lookup"><span data-stu-id="5492e-136">Standard_GS1</span></span> |<span data-ttu-id="5492e-137">Standard_GS5</span><span class="sxs-lookup"><span data-stu-id="5492e-137">Standard_GS5</span></span> |
> 
> 

## <a name="create-an-azure-automation-account-with-run-as-capability"></a><span data-ttu-id="5492e-138">Create an Azure Automation Account with run-as capability</span><span class="sxs-lookup"><span data-stu-id="5492e-138">Create an Azure Automation Account with run-as capability</span></span>
<span data-ttu-id="5492e-139">The first thing you need to do is create an Azure Automation account that hosts the runbooks used to scale the virtual machine scale set instances.</span><span class="sxs-lookup"><span data-stu-id="5492e-139">The first thing you need to do is create an Azure Automation account that hosts the runbooks used to scale the virtual machine scale set instances.</span></span> <span data-ttu-id="5492e-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature that makes setting up the Service Principal for automatically running the runbooks on a user's behalf.</span><span class="sxs-lookup"><span data-stu-id="5492e-140">Recently [Azure Automation](https://azure.microsoft.com/services/automation/) introduced the "Run As account" feature that makes setting up the Service Principal for automatically running the runbooks on a user's behalf.</span></span> <span data-ttu-id="5492e-141">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="5492e-141">For more information, see:</span></span>

* [<span data-ttu-id="5492e-142">Authenticate Runbooks with Azure Run As account</span><span class="sxs-lookup"><span data-stu-id="5492e-142">Authenticate Runbooks with Azure Run As account</span></span>](../automation/automation-sec-configure-azure-runas-account.md)

## <a name="import-azure-automation-vertical-scale-runbooks-into-your-subscription"></a><span data-ttu-id="5492e-143">Import Azure Automation Vertical Scale runbooks into your subscription</span><span class="sxs-lookup"><span data-stu-id="5492e-143">Import Azure Automation Vertical Scale runbooks into your subscription</span></span>
<span data-ttu-id="5492e-144">The runbooks needed to vertically scale your virtual machine scale sets are already published in the Azure Automation Runbook Gallery.</span><span class="sxs-lookup"><span data-stu-id="5492e-144">The runbooks needed to vertically scale your virtual machine scale sets are already published in the Azure Automation Runbook Gallery.</span></span> <span data-ttu-id="5492e-145">To import them into your subscription follow the steps in this article:</span><span class="sxs-lookup"><span data-stu-id="5492e-145">To import them into your subscription follow the steps in this article:</span></span>

* [<span data-ttu-id="5492e-146">Runbook and module galleries for Azure Automation</span><span class="sxs-lookup"><span data-stu-id="5492e-146">Runbook and module galleries for Azure Automation</span></span>](../automation/automation-runbook-gallery.md)

<span data-ttu-id="5492e-147">Choose the Browse Gallery option from the Runbooks menu:</span><span class="sxs-lookup"><span data-stu-id="5492e-147">Choose the Browse Gallery option from the Runbooks menu:</span></span>

![Runbooks to be imported][runbooks]

<span data-ttu-id="5492e-149">The runbooks that need to be imported are shown.</span><span class="sxs-lookup"><span data-stu-id="5492e-149">The runbooks that need to be imported are shown.</span></span> <span data-ttu-id="5492e-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span><span class="sxs-lookup"><span data-stu-id="5492e-150">Select the runbook based on whether you want vertical scaling with or without reprovisioning:</span></span>

![Runbooks gallery][gallery]

## <a name="add-a-webhook-to-your-runbook"></a><span data-ttu-id="5492e-152">Add a webhook to your runbook</span><span class="sxs-lookup"><span data-stu-id="5492e-152">Add a webhook to your runbook</span></span>
<span data-ttu-id="5492e-153">Once you've imported the runbooks, add a webhook to the runbook so it can be triggered by an alert from a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="5492e-153">Once you've imported the runbooks, add a webhook to the runbook so it can be triggered by an alert from a virtual machine scale set.</span></span> <span data-ttu-id="5492e-154">The details of creating a webhook for your Runbook are described in this article:</span><span class="sxs-lookup"><span data-stu-id="5492e-154">The details of creating a webhook for your Runbook are described in this article:</span></span>

* [<span data-ttu-id="5492e-155">Azure Automation webhooks</span><span class="sxs-lookup"><span data-stu-id="5492e-155">Azure Automation webhooks</span></span>](../automation/automation-webhooks.md)

> [!NOTE]
> <span data-ttu-id="5492e-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this address in the next section.</span><span class="sxs-lookup"><span data-stu-id="5492e-156">Make sure you copy the webhook URI before closing the webhook dialog as you will need this address in the next section.</span></span>
> 
> 

## <a name="add-an-alert-to-your-virtual-machine-scale-set"></a><span data-ttu-id="5492e-157">Add an alert to your virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="5492e-157">Add an alert to your virtual machine scale set</span></span>
<span data-ttu-id="5492e-158">Below is a PowerShell script that shows how to add an alert to a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="5492e-158">Below is a PowerShell script that shows how to add an alert to a virtual machine scale set.</span></span> <span data-ttu-id="5492e-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5492e-159">Refer to the following article to get the name of the metric to fire the alert on: [Azure Monitor autoscaling common metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md).</span></span>

```
$actionEmail = New-AzureRmAlertRuleEmail -CustomEmail user@contoso.com
$actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri <uri-of-the-webhook>
$threshold = <value-of-the-threshold>
$rg = <resource-group-name>
$id = <resource-id-to-add-the-alert-to>
$location = <location-of-the-resource>
$alertName = <name-of-the-resource>
$metricName = <metric-to-fire-the-alert-on>
$timeWindow = <time-window-in-hh:mm:ss-format>
$condition = <condition-for-the-threshold> # Other valid values are LessThanOrEqual, GreaterThan, GreaterThanOrEqual
$description = <description-for-the-alert>

Add-AzureRmMetricAlertRule  -Name  $alertName `
                            -Location  $location `
                            -ResourceGroup $rg `
                            -TargetResourceId $id `
                            -MetricName $metricName `
                            -Operator  $condition `
                            -Threshold $threshold `
                            -WindowSize  $timeWindow `
                            -TimeAggregationOperator Average `
                            -Actions $actionEmail, $actionWebhook `
                            -Description $description
```

> [!NOTE]
> <span data-ttu-id="5492e-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span><span class="sxs-lookup"><span data-stu-id="5492e-160">It is recommended to configure a reasonable time window for the alert in order to avoid triggering vertical scaling, and any associated service interruption, too often.</span></span> <span data-ttu-id="5492e-161">Consider a window of least 20-30 minutes or more.</span><span class="sxs-lookup"><span data-stu-id="5492e-161">Consider a window of least 20-30 minutes or more.</span></span> <span data-ttu-id="5492e-162">Consider horizontal scaling if you need to avoid any interruption.</span><span class="sxs-lookup"><span data-stu-id="5492e-162">Consider horizontal scaling if you need to avoid any interruption.</span></span>
> 
> 

<span data-ttu-id="5492e-163">For more information on how to create alerts, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="5492e-163">For more information on how to create alerts, see the following articles:</span></span>

* [<span data-ttu-id="5492e-164">Azure Monitor PowerShell quickstart samples</span><span class="sxs-lookup"><span data-stu-id="5492e-164">Azure Monitor PowerShell quickstart samples</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md)
* [<span data-ttu-id="5492e-165">Azure Monitor Cross-platform CLI quickstart samples</span><span class="sxs-lookup"><span data-stu-id="5492e-165">Azure Monitor Cross-platform CLI quickstart samples</span></span>](../monitoring-and-diagnostics/insights-cli-samples.md)

## <a name="summary"></a><span data-ttu-id="5492e-166">Summary</span><span class="sxs-lookup"><span data-stu-id="5492e-166">Summary</span></span>
<span data-ttu-id="5492e-167">This article showed simple vertical scaling examples.</span><span class="sxs-lookup"><span data-stu-id="5492e-167">This article showed simple vertical scaling examples.</span></span> <span data-ttu-id="5492e-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span><span class="sxs-lookup"><span data-stu-id="5492e-168">With these building blocks - Automation account, runbooks, webhooks, alerts - you can connect a rich variety of events with a customized set of actions.</span></span>

[runbooks]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks.png
[gallery]: ./media/virtual-machine-scale-sets-vertical-scale-reprovision/runbooks-gallery.png
