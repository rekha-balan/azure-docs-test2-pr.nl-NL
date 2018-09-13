---
title: Create an Azure Network Watcher instance | Microsoft Docs
description: This page provides the steps to create an instance of Network Watcher using the portal and Azure REST API
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2cdc4f750af7f21bd0dab1caa7294b94621e2c4e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662398"
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="1d052-103">Create an Azure Network Watcher instance</span><span class="sxs-lookup"><span data-stu-id="1d052-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="1d052-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span><span class="sxs-lookup"><span data-stu-id="1d052-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="1d052-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span><span class="sxs-lookup"><span data-stu-id="1d052-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="1d052-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span><span class="sxs-lookup"><span data-stu-id="1d052-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="1d052-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="1d052-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="1d052-108">Create a Network Watcher in the portal</span><span class="sxs-lookup"><span data-stu-id="1d052-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="1d052-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="1d052-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="1d052-110">You can select all the subscriptions you want to enable Network Watcher for.</span><span class="sxs-lookup"><span data-stu-id="1d052-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="1d052-111">This action creates a Network Watcher in every region that is available.</span><span class="sxs-lookup"><span data-stu-id="1d052-111">This action creates a Network Watcher in every region that is available.</span></span>

![create a network watcher][1]

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="1d052-113">Create a Network Watcher with PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d052-113">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="1d052-114">To create an instance of Network Watcher, run the following example:</span><span class="sxs-lookup"><span data-stu-id="1d052-114">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="1d052-115">Create a Network Watcher with the REST API</span><span class="sxs-lookup"><span data-stu-id="1d052-115">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="1d052-116">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1d052-116">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="1d052-117">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="1d052-117">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="1d052-118">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="1d052-118">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="1d052-119">Create the network watcher</span><span class="sxs-lookup"><span data-stu-id="1d052-119">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="1d052-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d052-120">Next steps</span></span>

<span data-ttu-id="1d052-121">Now that you have an instance of Network Watcher, learn about the features available:</span><span class="sxs-lookup"><span data-stu-id="1d052-121">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="1d052-122">Topology</span><span class="sxs-lookup"><span data-stu-id="1d052-122">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="1d052-123">Packet capture</span><span class="sxs-lookup"><span data-stu-id="1d052-123">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="1d052-124">IP flow verify</span><span class="sxs-lookup"><span data-stu-id="1d052-124">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="1d052-125">Next hop</span><span class="sxs-lookup"><span data-stu-id="1d052-125">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="1d052-126">Security group view</span><span class="sxs-lookup"><span data-stu-id="1d052-126">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="1d052-127">NSG flow logging</span><span class="sxs-lookup"><span data-stu-id="1d052-127">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="1d052-128">Virtual Network Gateway troubleshooting</span><span class="sxs-lookup"><span data-stu-id="1d052-128">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="1d052-129">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1d052-129">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-create/figure1.png












