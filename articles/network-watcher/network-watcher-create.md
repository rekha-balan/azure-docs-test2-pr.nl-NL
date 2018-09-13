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
# <a name="create-an-azure-network-watcher-instance"></a>Create an Azure Network Watcher instance

Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure. Scenario level monitoring enables you to diagnose problems at an end to end network level view. Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.

## <a name="create-a-network-watcher-in-the-portal"></a>Create a Network Watcher in the portal

Navigate to **All Services** > **Networking** > **Network Watcher**. You can select all the subscriptions you want to enable Network Watcher for. This action creates a Network Watcher in every region that is available.

![create a network watcher](./media/network-watcher-create/figure1.png)

When you enable Network Watcher using the portal, the name of the Network Watcher instance is automatically set to *NetworkWatcher_region_name* where *region_name* corresponds to the Azure region where the instance is enabled. For example, a Network Watcher enabled in the West Central US region is named *NetworkWatcher_westcentralus*.

The Network Watcher instance is automatically created in a resource group named *NetworkWatcherRG*. The resource group is created if it does not already exist.

If you wish to customize the name of a Network Watcher instance and the resource group it's placed into, you can use Powershell, the Azure CLI, the REST API, or ARMClient methods described in the sections that follow. In each option, the resource group must exist before you create a Network Watcher in it.  

## <a name="create-a-network-watcher-with-powershell"></a>Create a Network Watcher with PowerShell

To create an instance of Network Watcher, run the following example:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-azure-cli"></a>Create a Network Watcher with the Azure CLI

To create an instance of Network Watcher, run the following example:

```azurecli
az network watcher configure --resource-group NetworkWatcherRG --locations westcentralus --enabled
```

## <a name="create-a-network-watcher-with-the-rest-api"></a>Create a Network Watcher with the REST API

The ARMclient is used to call the REST API using PowerShell. The ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)

### <a name="log-in-with-armclient"></a>Log in with ARMClient

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a>Create the network watcher

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

## <a name="next-steps"></a>Next steps

Now that you have an instance of Network Watcher, learn about the features available:

* [Topology](network-watcher-topology-overview.md)
* [Packet capture](network-watcher-packet-capture-overview.md)
* [IP flow verify](network-watcher-ip-flow-verify-overview.md)
* [Next hop](network-watcher-next-hop-overview.md)
* [Security group view](network-watcher-security-group-view-overview.md)
* [NSG flow logging](network-watcher-nsg-flow-logging-overview.md)
* [Virtual Network Gateway troubleshooting](network-watcher-troubleshoot-overview.md)

Once a Network Watcher instance is, you can enable packet capture within virtual machines. To learn how, see [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)
