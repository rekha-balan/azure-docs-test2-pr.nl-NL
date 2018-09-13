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
# <a name="create-an-azure-network-watcher-instance"></a>Create an Azure Network Watcher instance

Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure. Scenario level monitoring enables you to diagnose problems at an end to end network level view. Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.

> [!NOTE]
> As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.

## <a name="create-a-network-watcher-in-the-portal"></a>Create a Network Watcher in the portal

Navigate to **More Services** > **Networking** > **Network Watcher**. You can select all the subscriptions you want to enable Network Watcher for. This action creates a Network Watcher in every region that is available.

![create a network watcher][1]

## <a name="create-a-network-watcher-with-powershell"></a>Create a Network Watcher with PowerShell

To create an instance of Network Watcher, run the following example:

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a>Create a Network Watcher with the REST API

ARMclient is used to call the REST API using PowerShell. ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)

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

Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-create/figure1.png












