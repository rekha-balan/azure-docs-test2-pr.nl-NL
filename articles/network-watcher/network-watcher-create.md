---
title: Create an Azure Network Watcher instance | Microsoft Docs
description: Learn how to enable Network Watcher in an Azure region.
services: network-watcher
documentationcenter: na
author: jimdial
manager: timlt
editor: ''
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: jdial
ms.openlocfilehash: 5e9fa204b698b2541c4d2df233a529d3274c8738
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812304"
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="fd2cd-103">Create an Azure Network Watcher instance</span><span class="sxs-lookup"><span data-stu-id="fd2cd-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="fd2cd-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="fd2cd-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="fd2cd-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="fd2cd-107">Create a Network Watcher in the portal</span><span class="sxs-lookup"><span data-stu-id="fd2cd-107">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="fd2cd-108">Navigate to **All Services** > **Networking** > **Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-108">Navigate to **All Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="fd2cd-109">You can select all the subscriptions you want to enable Network Watcher for.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-109">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="fd2cd-110">This action creates a Network Watcher in every region that is available.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-110">This action creates a Network Watcher in every region that is available.</span></span>

![create a network watcher](./media/network-watcher-create/figure1.png)

<span data-ttu-id="fd2cd-112">When you enable Network Watcher using the portal, the name of the Network Watcher instance is automatically set to *NetworkWatcher_region_name* where *region_name* corresponds to the Azure region where the instance is enabled.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-112">When you enable Network Watcher using the portal, the name of the Network Watcher instance is automatically set to *NetworkWatcher_region_name* where *region_name* corresponds to the Azure region where the instance is enabled.</span></span> <span data-ttu-id="fd2cd-113">For example, a Network Watcher enabled in the West Central US region is named *NetworkWatcher_westcentralus*.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-113">For example, a Network Watcher enabled in the West Central US region is named *NetworkWatcher_westcentralus*.</span></span>

<span data-ttu-id="fd2cd-114">The Network Watcher instance is automatically created in a resource group named *NetworkWatcherRG*.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-114">The Network Watcher instance is automatically created in a resource group named *NetworkWatcherRG*.</span></span> <span data-ttu-id="fd2cd-115">The resource group is created if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-115">The resource group is created if it does not already exist.</span></span>

<span data-ttu-id="fd2cd-116">If you wish to customize the name of a Network Watcher instance and the resource group it's placed into, you can use Powershell, the Azure CLI, the REST API, or ARMClient methods described in the sections that follow.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-116">If you wish to customize the name of a Network Watcher instance and the resource group it's placed into, you can use Powershell, the Azure CLI, the REST API, or ARMClient methods described in the sections that follow.</span></span> <span data-ttu-id="fd2cd-117">In each option, the resource group must exist before you create a Network Watcher in it.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-117">In each option, the resource group must exist before you create a Network Watcher in it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="fd2cd-118">Create a Network Watcher with PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd2cd-118">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="fd2cd-119">To create an instance of Network Watcher, run the following example:</span><span class="sxs-lookup"><span data-stu-id="fd2cd-119">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-azure-cli"></a><span data-ttu-id="fd2cd-120">Create a Network Watcher with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fd2cd-120">Create a Network Watcher with the Azure CLI</span></span>

<span data-ttu-id="fd2cd-121">To create an instance of Network Watcher, run the following example:</span><span class="sxs-lookup"><span data-stu-id="fd2cd-121">To create an instance of Network Watcher, run the following example:</span></span>

```azurecli
az network watcher configure --resource-group NetworkWatcherRG --locations westcentralus --enabled
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="fd2cd-122">Create a Network Watcher with the REST API</span><span class="sxs-lookup"><span data-stu-id="fd2cd-122">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="fd2cd-123">The ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-123">The ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="fd2cd-124">The ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="fd2cd-124">The ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="fd2cd-125">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="fd2cd-125">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="fd2cd-126">Create the network watcher</span><span class="sxs-lookup"><span data-stu-id="fd2cd-126">Create the network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fd2cd-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd2cd-127">Next steps</span></span>

<span data-ttu-id="fd2cd-128">Now that you have an instance of Network Watcher, learn about the features available:</span><span class="sxs-lookup"><span data-stu-id="fd2cd-128">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="fd2cd-129">Topology</span><span class="sxs-lookup"><span data-stu-id="fd2cd-129">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="fd2cd-130">Packet capture</span><span class="sxs-lookup"><span data-stu-id="fd2cd-130">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="fd2cd-131">IP flow verify</span><span class="sxs-lookup"><span data-stu-id="fd2cd-131">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="fd2cd-132">Next hop</span><span class="sxs-lookup"><span data-stu-id="fd2cd-132">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="fd2cd-133">Security group view</span><span class="sxs-lookup"><span data-stu-id="fd2cd-133">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="fd2cd-134">NSG flow logging</span><span class="sxs-lookup"><span data-stu-id="fd2cd-134">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="fd2cd-135">Virtual Network Gateway troubleshooting</span><span class="sxs-lookup"><span data-stu-id="fd2cd-135">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="fd2cd-136">Once a Network Watcher instance is, you can enable packet capture within virtual machines.</span><span class="sxs-lookup"><span data-stu-id="fd2cd-136">Once a Network Watcher instance is, you can enable packet capture within virtual machines.</span></span> <span data-ttu-id="fd2cd-137">To learn how, see [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="fd2cd-137">To learn how, see [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>
