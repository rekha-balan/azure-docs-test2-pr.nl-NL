---
title: Add extended metrics for Azure virtual machines | Microsoft Docs
description: This article helps you enable and configure extended diagnostics metrics for your Azure VMs.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/12/2018
ms.topic: conceptual
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: 439692decaedcced68a7f754759dbb4c3878806a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865544"
---
# <a name="add-extended-metrics-for-azure-virtual-machines"></a><span data-ttu-id="e2b5f-103">Add extended metrics for Azure virtual machines</span><span class="sxs-lookup"><span data-stu-id="e2b5f-103">Add extended metrics for Azure virtual machines</span></span>

<span data-ttu-id="e2b5f-104">Cost Management uses Azure metric data from your Azure VMs to show you detailed information about their resources.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-104">Cost Management uses Azure metric data from your Azure VMs to show you detailed information about their resources.</span></span> <span data-ttu-id="e2b5f-105">Metric data, also called performance counters, is used by Cost Management to generate reports.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-105">Metric data, also called performance counters, is used by Cost Management to generate reports.</span></span> <span data-ttu-id="e2b5f-106">However, Cost Management does not automatically gather all Azure metric data from guest VMs — you must enable metric collection.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-106">However, Cost Management does not automatically gather all Azure metric data from guest VMs — you must enable metric collection.</span></span> <span data-ttu-id="e2b5f-107">This article helps you enable and configure additional diagnostics metrics for your Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-107">This article helps you enable and configure additional diagnostics metrics for your Azure VMs.</span></span>

<span data-ttu-id="e2b5f-108">After you enable metric collection, you can:</span><span class="sxs-lookup"><span data-stu-id="e2b5f-108">After you enable metric collection, you can:</span></span>

- <span data-ttu-id="e2b5f-109">Know when your VMs are reaching their memory, disk, and CPU limits.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-109">Know when your VMs are reaching their memory, disk, and CPU limits.</span></span>
- <span data-ttu-id="e2b5f-110">Detect usage trends and anomalies.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-110">Detect usage trends and anomalies.</span></span>
- <span data-ttu-id="e2b5f-111">Control your costs by sizing according to usage.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-111">Control your costs by sizing according to usage.</span></span>
- <span data-ttu-id="e2b5f-112">Get cost effective sizing optimization recommendations from Cost Management.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-112">Get cost effective sizing optimization recommendations from Cost Management.</span></span>

<span data-ttu-id="e2b5f-113">For example, you might want to monitor the CPU % and Memory % of your Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-113">For example, you might want to monitor the CPU % and Memory % of your Azure VMs.</span></span> <span data-ttu-id="e2b5f-114">The Azure VM metrics correspond to _[Host] Percentage CPU_ and _[Guest] Memory percentage_.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-114">The Azure VM metrics correspond to _[Host] Percentage CPU_ and _[Guest] Memory percentage_.</span></span>

> [!NOTE]
> <span data-ttu-id="e2b5f-115">Extended metric data collection is only supported with Azure guest-level monitoring.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-115">Extended metric data collection is only supported with Azure guest-level monitoring.</span></span> <span data-ttu-id="e2b5f-116">Cost Management is not compatible with the Log Analytics VM extension.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-116">Cost Management is not compatible with the Log Analytics VM extension.</span></span>

## <a name="verify-that-metrics-are-enabled-on-vms"></a><span data-ttu-id="e2b5f-117">Verify that metrics are enabled on VMs</span><span class="sxs-lookup"><span data-stu-id="e2b5f-117">Verify that metrics are enabled on VMs</span></span>

1. <span data-ttu-id="e2b5f-118">Sign in to the Azure portal at http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-118">Sign in to the Azure portal at http://portal.azure.com.</span></span>
2. <span data-ttu-id="e2b5f-119">Under **Virtual machines**, select a VM and then under **Monitoring**, select **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-119">Under **Virtual machines**, select a VM and then under **Monitoring**, select **Metrics**.</span></span> <span data-ttu-id="e2b5f-120">A list of available metrics is shown.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-120">A list of available metrics is shown.</span></span>
3. <span data-ttu-id="e2b5f-121">Select some metrics and a graph displays data for them.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-121">Select some metrics and a graph displays data for them.</span></span>  
    ![Example metric – host percentage CPU](./media/azure-vm-extended-metrics/metric01.png)

<span data-ttu-id="e2b5f-123">In the preceding example, a limited set of standard metrics are available for your hosts, but memory metrics are not.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-123">In the preceding example, a limited set of standard metrics are available for your hosts, but memory metrics are not.</span></span> <span data-ttu-id="e2b5f-124">Memory metrics are part of extended metrics.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-124">Memory metrics are part of extended metrics.</span></span> <span data-ttu-id="e2b5f-125">You must perform some additional steps to enable extended metrics.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-125">You must perform some additional steps to enable extended metrics.</span></span> <span data-ttu-id="e2b5f-126">The following information guides you through enabling them.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-126">The following information guides you through enabling them.</span></span>

## <a name="enable-extended-metrics-in-the-azure-portal"></a><span data-ttu-id="e2b5f-127">Enable extended metrics in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e2b5f-127">Enable extended metrics in the Azure portal</span></span>

<span data-ttu-id="e2b5f-128">Standard metrics are host computer metrics.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-128">Standard metrics are host computer metrics.</span></span> <span data-ttu-id="e2b5f-129">The _[Host] Percentage CPU_ metric is one example.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-129">The _[Host] Percentage CPU_ metric is one example.</span></span> <span data-ttu-id="e2b5f-130">There are also basic metrics for guest VMs and they're also called extended metrics.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-130">There are also basic metrics for guest VMs and they're also called extended metrics.</span></span> <span data-ttu-id="e2b5f-131">Examples of extended metrics include _[Guest] Memory percentage_ and _[Guest] Memory available_.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-131">Examples of extended metrics include _[Guest] Memory percentage_ and _[Guest] Memory available_.</span></span>

<span data-ttu-id="e2b5f-132">Enabling extended metrics is straightforward.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-132">Enabling extended metrics is straightforward.</span></span> <span data-ttu-id="e2b5f-133">For each VM, enable guest-level monitoring.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-133">For each VM, enable guest-level monitoring.</span></span> <span data-ttu-id="e2b5f-134">When you enable guest-level monitoring, the Azure diagnostics agent is installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-134">When you enable guest-level monitoring, the Azure diagnostics agent is installed on the VM.</span></span> <span data-ttu-id="e2b5f-135">The following process is the same for classic and regular VMs and the same for Windows and Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-135">The following process is the same for classic and regular VMs and the same for Windows and Linux VMs.</span></span>

<span data-ttu-id="e2b5f-136">Keep in mind that both Azure and Linux guest-level monitoring require a storage account.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-136">Keep in mind that both Azure and Linux guest-level monitoring require a storage account.</span></span> <span data-ttu-id="e2b5f-137">When you enable guest-level monitoring, if you don't choose an existing storage account, then one is created for you.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-137">When you enable guest-level monitoring, if you don't choose an existing storage account, then one is created for you.</span></span>

### <a name="enable-guest-level-monitoring-on-existing-vms"></a><span data-ttu-id="e2b5f-138">Enable guest-level monitoring on existing VMs</span><span class="sxs-lookup"><span data-stu-id="e2b5f-138">Enable guest-level monitoring on existing VMs</span></span>

1. <span data-ttu-id="e2b5f-139">In **Virtual Machines**, view your list of your VMs and then select a VM.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-139">In **Virtual Machines**, view your list of your VMs and then select a VM.</span></span>
2. <span data-ttu-id="e2b5f-140">Under **Monitoring**, select **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-140">Under **Monitoring**, select **Metrics**.</span></span>
3. <span data-ttu-id="e2b5f-141">Click **Diagnostic settings**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-141">Click **Diagnostic settings**.</span></span>
4. <span data-ttu-id="e2b5f-142">On the Diagnostics settings page, click **Enable guest-level monitoring**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-142">On the Diagnostics settings page, click **Enable guest-level monitoring**.</span></span>  
    <span data-ttu-id="e2b5f-143">![Enable guest level monitoring](./media/azure-vm-extended-metrics/enable-guest-monitoring.png)</span><span class="sxs-lookup"><span data-stu-id="e2b5f-143">![Enable guest level monitoring](./media/azure-vm-extended-metrics/enable-guest-monitoring.png)</span></span>
5. <span data-ttu-id="e2b5f-144">After a few minutes, the Azure diagnostics agent is installed on the VM.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-144">After a few minutes, the Azure diagnostics agent is installed on the VM.</span></span> <span data-ttu-id="e2b5f-145">Refresh the page and the list of available metrics is updated with guest metrics.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-145">Refresh the page and the list of available metrics is updated with guest metrics.</span></span>  
    ![Extended metrics](./media/azure-vm-extended-metrics/extended-metrics.png)

### <a name="enable-guest-level-monitoring-on-new-vms"></a><span data-ttu-id="e2b5f-147">Enable guest-level monitoring on new VMs</span><span class="sxs-lookup"><span data-stu-id="e2b5f-147">Enable guest-level monitoring on new VMs</span></span>

<span data-ttu-id="e2b5f-148">When you create new VMs, ensure that you select **Guest OS diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-148">When you create new VMs, ensure that you select **Guest OS diagnostics**.</span></span>

![Enable Guest OS diagnostics](./media/azure-vm-extended-metrics/new-enable-diag.png)

## <a name="resource-manager-credentials"></a><span data-ttu-id="e2b5f-150">Resource Manager credentials</span><span class="sxs-lookup"><span data-stu-id="e2b5f-150">Resource Manager credentials</span></span>

<span data-ttu-id="e2b5f-151">After you enable extended metrics, ensure that Cost Management has access to your [Resource Manager credentials](activate-subs-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="e2b5f-151">After you enable extended metrics, ensure that Cost Management has access to your [Resource Manager credentials](activate-subs-accounts.md).</span></span> <span data-ttu-id="e2b5f-152">Your credentials are required for Cost Management to collect and display performance data for your VMs.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-152">Your credentials are required for Cost Management to collect and display performance data for your VMs.</span></span> <span data-ttu-id="e2b5f-153">They're also used to create cost optimization recommendations.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-153">They're also used to create cost optimization recommendations.</span></span> <span data-ttu-id="e2b5f-154">Cost Management needs at least three days of performance data from an instance to determine if it is a candidate for a downsizing recommendation.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-154">Cost Management needs at least three days of performance data from an instance to determine if it is a candidate for a downsizing recommendation.</span></span>

## <a name="enable-vm-metrics-with-a-script"></a><span data-ttu-id="e2b5f-155">Enable VM metrics with a script</span><span class="sxs-lookup"><span data-stu-id="e2b5f-155">Enable VM metrics with a script</span></span>

<span data-ttu-id="e2b5f-156">You can enable VM metrics with Azure PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-156">You can enable VM metrics with Azure PowerShell scripts.</span></span> <span data-ttu-id="e2b5f-157">When you have many VMs that you want to enable metrics on, you can use a script to automate the process.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-157">When you have many VMs that you want to enable metrics on, you can use a script to automate the process.</span></span> <span data-ttu-id="e2b5f-158">Example scripts are on GitHub at [Azure Enable Diagnostics](https://github.com/Cloudyn/azure-enable-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="e2b5f-158">Example scripts are on GitHub at [Azure Enable Diagnostics](https://github.com/Cloudyn/azure-enable-diagnostics).</span></span>

## <a name="view-azure-performance-metrics"></a><span data-ttu-id="e2b5f-159">View Azure performance metrics</span><span class="sxs-lookup"><span data-stu-id="e2b5f-159">View Azure performance metrics</span></span>

<span data-ttu-id="e2b5f-160">To view performance metrics on your Azure Instances in the Cloudyn portal, navigate to **Assets** > **Compute** > **Instance Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-160">To view performance metrics on your Azure Instances in the Cloudyn portal, navigate to **Assets** > **Compute** > **Instance Explorer**.</span></span> <span data-ttu-id="e2b5f-161">In the list of VM instances, expand an instance and then expand a resource to view details.</span><span class="sxs-lookup"><span data-stu-id="e2b5f-161">In the list of VM instances, expand an instance and then expand a resource to view details.</span></span>

![Instance Explorer](./media/azure-vm-extended-metrics/instance-explorer.png)

## <a name="next-steps"></a><span data-ttu-id="e2b5f-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2b5f-163">Next steps</span></span>

- <span data-ttu-id="e2b5f-164">If you haven't already enabled Azure Resource Manager API access for your accounts, proceed to [Activate Azure subscriptions and accounts](activate-subs-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="e2b5f-164">If you haven't already enabled Azure Resource Manager API access for your accounts, proceed to [Activate Azure subscriptions and accounts](activate-subs-accounts.md).</span></span>
