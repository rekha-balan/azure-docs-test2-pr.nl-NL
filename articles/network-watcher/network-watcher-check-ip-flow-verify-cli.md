---
title: Verify traffic with Azure Network Watcher IP Flow Verify - Azure CLI | Microsoft Docs
description: This article describes how to check if traffic to or from a virtual machine is allowed or denied using Azure CLI
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 92b857ed-c834-4c1b-8ee9-538e7ae7391d
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 1dde21cc40df292c565092404cc8c9be72143662
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554430"
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)

IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine. This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend. IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules. Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.

This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux. Network Watcher currently uses Azure CLI 1.0 for CLI support.

## <a name="before-you-begin"></a>Before you begin

This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher. The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.

## <a name="scenario"></a>Scenario

This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address. If the traffic is denied, it returns the security rule that is denying that traffic. To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)


## <a name="get-a-vm"></a>Get a VM

IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination. An Id of a virtual machine is required for the cmdlet. If you already know the ID of the virtual machine to use, you can skip this step.

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a>Get the NICS

The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine. If you already know the IP address that you want to test on the virtual machine, you can skip this step.

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a>Run IP flow verify

Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic. In this example, we are using the first IP address on the first NIC.

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> IP Flow verify requires that the VM resource is allocated to run.

## <a name="review-results"></a>Review Results

After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a>Next steps

If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.

Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure2.png


