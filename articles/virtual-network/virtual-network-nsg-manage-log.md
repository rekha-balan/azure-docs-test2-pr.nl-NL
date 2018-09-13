---
title: Monitor operations, events, and counters for NSGs | Microsoft Docs
description: Learn how to enable counters, events, and operational logging for NSGs
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2e699078-043f-48bd-8aa8-b011a32d98ca
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/31/2017
ms.author: jdial
ms.openlocfilehash: 10581234a4475d0d3b32c7891fcf97eed55f7a1d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555243"
---
# <a name="log-analytics-for-network-security-groups-nsgs"></a><span data-ttu-id="f7436-103">Log analytics for network security groups (NSGs)</span><span class="sxs-lookup"><span data-stu-id="f7436-103">Log analytics for network security groups (NSGs)</span></span>

<span data-ttu-id="f7436-104">You can enable the following diagnostic log categories for NSGs:</span><span class="sxs-lookup"><span data-stu-id="f7436-104">You can enable the following diagnostic log categories for NSGs:</span></span>

* <span data-ttu-id="f7436-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span><span class="sxs-lookup"><span data-stu-id="f7436-105">**Event:** Contains entries for which NSG rules are applied to VMs and instance roles based on MAC address.</span></span> <span data-ttu-id="f7436-106">The status for these rules is collected every 60 seconds.</span><span class="sxs-lookup"><span data-stu-id="f7436-106">The status for these rules is collected every 60 seconds.</span></span>
* <span data-ttu-id="f7436-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span><span class="sxs-lookup"><span data-stu-id="f7436-107">**Rule counter:** Contains entries for how many times each NSG rule is applied to deny or allow traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="f7436-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="f7436-108">Diagnostic logs are only available for NSGs deployed through the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="f7436-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="f7436-109">You cannot enable diagnostic logging for NSGs deployed through the classic deployment model.</span></span> <span data-ttu-id="f7436-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-110">For a better understanding of the two models, reference the [Understanding Azure deployment models](../resource-manager-deployment-model.md) article.</span></span>

<span data-ttu-id="f7436-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span><span class="sxs-lookup"><span data-stu-id="f7436-111">Activity logging (previously known as audit or operational logs) is enabled by default for NSGs created through either Azure deployment model.</span></span> <span data-ttu-id="f7436-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span><span class="sxs-lookup"><span data-stu-id="f7436-112">To determine which operations were completed on NSGs in the activity log, look for entries that contain the following resource types:</span></span> 

- <span data-ttu-id="f7436-113">Microsoft.ClassicNetwork/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="f7436-113">Microsoft.ClassicNetwork/networkSecurityGroups</span></span> 
- <span data-ttu-id="f7436-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="f7436-114">Microsoft.ClassicNetwork/networkSecurityGroups/securityRules</span></span>
- <span data-ttu-id="f7436-115">Microsoft.Network/networkSecurityGroups</span><span class="sxs-lookup"><span data-stu-id="f7436-115">Microsoft.Network/networkSecurityGroups</span></span>
- <span data-ttu-id="f7436-116">Microsoft.Network/networkSecurityGroups/securityRules</span><span class="sxs-lookup"><span data-stu-id="f7436-116">Microsoft.Network/networkSecurityGroups/securityRules</span></span> 

<span data-ttu-id="f7436-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span><span class="sxs-lookup"><span data-stu-id="f7436-117">Read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) article to learn more about activity logs.</span></span> 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="f7436-118">Enable diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="f7436-118">Enable diagnostic logging</span></span>

<span data-ttu-id="f7436-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span><span class="sxs-lookup"><span data-stu-id="f7436-119">Diagnostic logging must be enabled for *each* NSG you want to collect data for.</span></span> <span data-ttu-id="f7436-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span><span class="sxs-lookup"><span data-stu-id="f7436-120">The [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article explains where diagnostic logs can be sent.</span></span> <span data-ttu-id="f7436-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span><span class="sxs-lookup"><span data-stu-id="f7436-121">If you don't have an existing NSG, complete the steps in the [Create a network security group](virtual-networks-create-nsg-arm-pportal.md) article to create one.</span></span> <span data-ttu-id="f7436-122">You can enable NSG diagnostic logging using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="f7436-122">You can enable NSG diagnostic logging using any of the following methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="f7436-123">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f7436-123">Azure portal</span></span>

<span data-ttu-id="f7436-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f7436-124">To use the portal to enable logging, login to the [portal](https://portal.azure.com).</span></span> <span data-ttu-id="f7436-125">Click **More services**, then type *network security groups*.</span><span class="sxs-lookup"><span data-stu-id="f7436-125">Click **More services**, then type *network security groups*.</span></span> <span data-ttu-id="f7436-126">Select the NSG you want to enable logging for.</span><span class="sxs-lookup"><span data-stu-id="f7436-126">Select the NSG you want to enable logging for.</span></span> <span data-ttu-id="f7436-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-in-the-portal) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-127">Follow the instructions for non-compute resources in the [Enable diagnostic logs in the portal](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-in-the-portal) article.</span></span> <span data-ttu-id="f7436-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span><span class="sxs-lookup"><span data-stu-id="f7436-128">Select **NetworkSecurityGroupEvent**, **NetworkSecurityGroupRuleCounter**, or both categories of logs.</span></span>

### <a name="powershell"></a><span data-ttu-id="f7436-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f7436-129">PowerShell</span></span>

<span data-ttu-id="f7436-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-via-powershell) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-130">To use PowerShell to enable logging, follow the instructions in the [Enable diagnostic logs via PowerShell](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-via-powershell) article.</span></span> <span data-ttu-id="f7436-131">Evaluate the following information before entering a command from the article:</span><span class="sxs-lookup"><span data-stu-id="f7436-131">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="f7436-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span><span class="sxs-lookup"><span data-stu-id="f7436-132">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `Get-AzureRmNetworkSecurityGroup -Name [nsg-name] -ResourceGroupName [resource-group-name]`.</span></span> <span data-ttu-id="f7436-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span><span class="sxs-lookup"><span data-stu-id="f7436-133">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="f7436-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="f7436-134">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="f7436-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span><span class="sxs-lookup"><span data-stu-id="f7436-135">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

### <a name="azure-command-line-interface-cli"></a><span data-ttu-id="f7436-136">Azure command-line interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="f7436-136">Azure command-line interface (CLI)</span></span>

<span data-ttu-id="f7436-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-via-cli) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-137">To use the CLI to enable logging, follow the instructions in the [Enable diagnostic logs via CLI](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#enable-diagnostic-logs-via-cli) article.</span></span> <span data-ttu-id="f7436-138">Evaluate the following information before entering a command from the article:</span><span class="sxs-lookup"><span data-stu-id="f7436-138">Evaluate the following information before entering a command from the article:</span></span>

- <span data-ttu-id="f7436-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span><span class="sxs-lookup"><span data-stu-id="f7436-139">You can determine the value to use for the `-ResourceId` parameter by replacing the following [text], as appropriate, then entering the command `azure network nsg show [resource-group-name] [nsg-name]`.</span></span> <span data-ttu-id="f7436-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span><span class="sxs-lookup"><span data-stu-id="f7436-140">The ID output from the command looks similar to */subscriptions/[Subscription Id]/resourceGroups/[resource-group]/providers/Microsoft.Network/networkSecurityGroups/[NSG name]*.</span></span>
- <span data-ttu-id="f7436-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span><span class="sxs-lookup"><span data-stu-id="f7436-141">If you only want to collect data from log category add `-Categories [category]` to the end of the command in the article, where category is either *NetworkSecurityGroupEvent* or *NetworkSecurityGroupRuleCounter*.</span></span> <span data-ttu-id="f7436-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span><span class="sxs-lookup"><span data-stu-id="f7436-142">If you don't use the `-Categories` parameter, data collection is enabled for both log categories.</span></span>

## <a name="logged-data"></a><span data-ttu-id="f7436-143">Logged data</span><span class="sxs-lookup"><span data-stu-id="f7436-143">Logged data</span></span>

<span data-ttu-id="f7436-144">JSON-formatted data is written for both logs.</span><span class="sxs-lookup"><span data-stu-id="f7436-144">JSON-formatted data is written for both logs.</span></span> <span data-ttu-id="f7436-145">The specific data written for each log type is listed in the following sections:</span><span class="sxs-lookup"><span data-stu-id="f7436-145">The specific data written for each log type is listed in the following sections:</span></span>

### <a name="event-log"></a><span data-ttu-id="f7436-146">Event log</span><span class="sxs-lookup"><span data-stu-id="f7436-146">Event log</span></span>
<span data-ttu-id="f7436-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span><span class="sxs-lookup"><span data-stu-id="f7436-147">This log contains information about which NSG rules are applied to VMs and cloud service role instances, based on MAC address.</span></span> <span data-ttu-id="f7436-148">The following example data is logged for each event:</span><span class="sxs-lookup"><span data-stu-id="f7436-148">The following example data is logged for each event:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupEvent",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION-ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupEvents",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-B791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "priority":1000,
        "type":"allow",
        "conditions":{
            "protocols":"6",
            "destinationPortRange":"3389-3389",
            "sourcePortRange":"0-65535",
            "sourceIP":"0.0.0.0/0",
            "destinationIP":"0.0.0.0/0"
            }
        }
}
```

### <a name="rule-counter-log"></a><span data-ttu-id="f7436-149">Rule counter log</span><span class="sxs-lookup"><span data-stu-id="f7436-149">Rule counter log</span></span>

<span data-ttu-id="f7436-150">This log contains information about each rule applied to resources.</span><span class="sxs-lookup"><span data-stu-id="f7436-150">This log contains information about each rule applied to resources.</span></span> <span data-ttu-id="f7436-151">The following example data is logged each time a rule is applied:</span><span class="sxs-lookup"><span data-stu-id="f7436-151">The following example data is logged each time a rule is applied:</span></span>

```json
{
    "time": "[DATE-TIME]",
    "systemId": "007d0441-5d6b-41f6-8bfd-930db640ec03",
    "category": "NetworkSecurityGroupRuleCounter",
    "resourceId": "/SUBSCRIPTIONS/[SUBSCRIPTION ID]/RESOURCEGROUPS/[RESOURCE-GROUP-NAME]TESTRG/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/[NSG-NAME]",
    "operationName": "NetworkSecurityGroupCounters",
    "properties": {
        "vnetResourceGuid":"{5E8AEC16-C728-441F-B0CA-791E1DBC2F4}",
        "subnetPrefix":"192.168.1.0/24",
        "macAddress":"00-0D-3A-92-6A-7C",
        "primaryIPv4Address":"192.168.1.4",
        "ruleName":"UserRule_default-allow-rdp",
        "direction":"In",
        "type":"allow",
        "matchedConnections":125
        }
}
```

## <a name="view-and-analyze-logs"></a><span data-ttu-id="f7436-152">View and analyze logs</span><span class="sxs-lookup"><span data-stu-id="f7436-152">View and analyze logs</span></span>

<span data-ttu-id="f7436-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-153">To learn how to view activity log data, read the [Overview of the Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="f7436-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span><span class="sxs-lookup"><span data-stu-id="f7436-154">To learn how to view diagnostic log data, read the [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article.</span></span> <span data-ttu-id="f7436-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span><span class="sxs-lookup"><span data-stu-id="f7436-155">If you send diagnostics data to Log Analytics, you can use the [Azure Network Security Group analytics](../log-analytics/log-analytics-azure-networking-analytics.md) (preview) management solution for enhanced insights.</span></span> 
