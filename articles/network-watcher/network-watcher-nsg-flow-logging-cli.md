---
title: Manage Network Security Group Flow logs with Azure Network Watcher - Azure CLI | Microsoft Docs
description: This page explains how to manage Network Security Group Flow logs in Azure Network Watcher with Azure CLI
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
ms.openlocfilehash: 3880c1e476013c5569f4049df70069d7dd4a1942
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661935"
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="33ff9-103">Configuring Network Security Group Flow logs with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33ff9-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI](network-watcher-nsg-flow-logging-cli.md)
> - [REST API](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="33ff9-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="33ff9-108">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="33ff9-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="33ff9-109">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="33ff9-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="33ff9-110">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="33ff9-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="33ff9-111">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="33ff9-112">Enable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="33ff9-112">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="33ff9-113">The command to enable flow logs is shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="33ff9-113">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="33ff9-114">Disable Network Security Group Flow logs</span><span class="sxs-lookup"><span data-stu-id="33ff9-114">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="33ff9-115">Use the following example to disable flow logs:</span><span class="sxs-lookup"><span data-stu-id="33ff9-115">Use the following example to disable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="33ff9-116">Download a Flow log</span><span class="sxs-lookup"><span data-stu-id="33ff9-116">Download a Flow log</span></span>

<span data-ttu-id="33ff9-117">The storage location of a flow log is defined at creation.</span><span class="sxs-lookup"><span data-stu-id="33ff9-117">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="33ff9-118">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="33ff9-118">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="33ff9-119">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span><span class="sxs-lookup"><span data-stu-id="33ff9-119">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="33ff9-120">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="33ff9-120">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="33ff9-121">Next Steps</span><span class="sxs-lookup"><span data-stu-id="33ff9-121">Next Steps</span></span>

<span data-ttu-id="33ff9-122">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="33ff9-122">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="33ff9-123">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="33ff9-123">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
