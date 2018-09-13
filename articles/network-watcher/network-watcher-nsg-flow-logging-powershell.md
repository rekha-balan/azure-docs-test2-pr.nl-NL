---
title: Manage Network Security Group Flow logs with Azure Network Watcher - PowerShell | Microsoft Docs
description: This page explains how to manage Network Security Group Flow logs in Azure Network Watcher with PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 19f800dcd676a62c31ac5a79af99b5e0cae8a806
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562761"
---
# <a name="configuring-network-security-group-flow-logs-with-powershell"></a><span data-ttu-id="349ed-103">Configuring Network Security Group Flow logs with PowerShell</span><span class="sxs-lookup"><span data-stu-id="349ed-103">Configuring Network Security Group Flow logs with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="349ed-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="349ed-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="349ed-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="349ed-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="349ed-110">Enable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="349ed-110">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="349ed-111">The command to enable flow logs is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="349ed-111">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$NW = Get-AzurermNetworkWatcher -ResourceGroupName NetworkWatcherRg -Name NetworkWatcher_westcentralus
$nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName nsgRG-Name nsgName
$storageAccount = Get-AzureRmStorageAccount -ResourceGroupName StorageRG -Name contosostorage123
Get-AzureRmNetworkWatcherFlowLogStatus -NetworkWatcher $NW -TargetResourceId $nsg.Id
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="349ed-112">Disable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="349ed-112">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="349ed-113">Use the following example to disable flow logs:</span><span class="sxs-lookup"><span data-stu-id="349ed-113">Use the following example to disable flow logs:</span></span>

```powershell
Set-AzureRmNetworkWatcherConfigFlowLog -NetworkWatcher $NW -TargetResourceId $nsg.Id -StorageAccountId $storageAccount.Id -EnableFlowLog $false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="349ed-114">Download a Flow log</span><span class="sxs-lookup"><span data-stu-id="349ed-114">Download a Flow log</span></span>

<span data-ttu-id="349ed-115">The storage location of a flow log is defined at creation.</span><span class="sxs-lookup"><span data-stu-id="349ed-115">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="349ed-116">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="349ed-116">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="349ed-117">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="349ed-117">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="349ed-118">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="349ed-118">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="349ed-119">Next Steps</span><span class="sxs-lookup"><span data-stu-id="349ed-119">Next Steps</span></span>

<span data-ttu-id="349ed-120">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="349ed-120">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="349ed-121">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="349ed-121">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>