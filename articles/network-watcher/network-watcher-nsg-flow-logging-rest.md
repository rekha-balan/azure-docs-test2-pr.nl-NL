---
title: Manage Network Security Group flow logs with Azure Network Watcher - REST API | Microsoft Docs
description: This page explains how to manage Network Security Group flow logs in Azure Network Watcher with REST API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6cf2a84edb21f5ec6aaefe867a2d7c6d78db2f69
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555324"
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="9e977-103">Configuring Network Security Group flow logs using REST API</span><span class="sxs-lookup"><span data-stu-id="9e977-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="9e977-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="9e977-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="9e977-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="9e977-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9e977-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9e977-110">Before you begin</span></span>

<span data-ttu-id="9e977-111">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e977-111">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="9e977-112">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="9e977-112">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="9e977-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="9e977-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.

## <a name="scenario"></a><span data-ttu-id="9e977-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="9e977-115">Scenario</span></span>

<span data-ttu-id="9e977-116">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span><span class="sxs-lookup"><span data-stu-id="9e977-116">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="9e977-117">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e977-117">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="9e977-118">In this scenario, you will:</span><span class="sxs-lookup"><span data-stu-id="9e977-118">In this scenario, you will:</span></span>

* <span data-ttu-id="9e977-119">Enable flow logs</span><span class="sxs-lookup"><span data-stu-id="9e977-119">Enable flow logs</span></span>
* <span data-ttu-id="9e977-120">Disable flow logs</span><span class="sxs-lookup"><span data-stu-id="9e977-120">Disable flow logs</span></span>
* <span data-ttu-id="9e977-121">Query flow logs status</span><span class="sxs-lookup"><span data-stu-id="9e977-121">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="9e977-122">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="9e977-122">Log in with ARMClient</span></span>

<span data-ttu-id="9e977-123">Log in to armclient with your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="9e977-123">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="9e977-124">Enable Network Security Group flow logs</span><span class="sxs-lookup"><span data-stu-id="9e977-124">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="9e977-125">The command to enable flow logs is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="9e977-125">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="9e977-126">The response returned from the preceding example is as follows:</span><span class="sxs-lookup"><span data-stu-id="9e977-126">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="9e977-127">Disable Network Security Group flow logs</span><span class="sxs-lookup"><span data-stu-id="9e977-127">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="9e977-128">Use the following example to disable flow logs.</span><span class="sxs-lookup"><span data-stu-id="9e977-128">Use the following example to disable flow logs.</span></span> <span data-ttu-id="9e977-129">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span><span class="sxs-lookup"><span data-stu-id="9e977-129">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="9e977-130">The response returned from the preceding example is as follows:</span><span class="sxs-lookup"><span data-stu-id="9e977-130">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="9e977-131">Query flow logs</span><span class="sxs-lookup"><span data-stu-id="9e977-131">Query flow logs</span></span>

<span data-ttu-id="9e977-132">The following REST call queries the status of flow logs on a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="9e977-132">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="9e977-133">The following is an example of the response returned:</span><span class="sxs-lookup"><span data-stu-id="9e977-133">The following is an example of the response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="9e977-134">Download a flow log</span><span class="sxs-lookup"><span data-stu-id="9e977-134">Download a flow log</span></span>

<span data-ttu-id="9e977-135">The storage location of a flow log is defined at creation.</span><span class="sxs-lookup"><span data-stu-id="9e977-135">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="9e977-136">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="9e977-136">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="9e977-137">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="9e977-137">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="9e977-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e977-138">Next steps</span></span>

<span data-ttu-id="9e977-139">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="9e977-139">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="9e977-140">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="9e977-140">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
