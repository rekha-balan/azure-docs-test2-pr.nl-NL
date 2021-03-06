---
title: Find next hop with Azure Network Watcher Next Hop - Azure portal | Microsoft Docs
description: This article will describe how you can find what the next hop type is and ip address using Next Hop using the Azure portal
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 73369b7477fe651ee7b99ce270bc4866b52d7b32
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44548779"
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a>Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [CLI](network-watcher-check-next-hop-cli.md)
> - [Azure REST API](network-watcher-check-next-hop-rest.md)

Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine. This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.

## <a name="before-you-begin"></a>Before you begin

This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher. The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.

## <a name="scenario"></a>Scenario

The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource. To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).

In this scenario, you will:

* Retrieve the next hop from a virtual machine.

## <a name="get-next-hop"></a>Get Next Hop

### <a name="step-1"></a>Step 1

Navigate to your Network Watcher resource in the Azure portal.

### <a name="step-2"></a>Step 2

Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.

> [!NOTE]
> Next hop requires that the VM resource is allocated to run.

![get next hop overview][1]

### <a name="step-3"></a>Step 3

Once the task is complete, the results are provided. The IP address and type of device the next hop is, is displayed. The following table shows the available returned values in the portal.

**Next Hop Type**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* None

If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.

![get next hop results][2]

## <a name="next-steps"></a>Next steps

Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-next-hop-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-next-hop-portal/figure2.png
















