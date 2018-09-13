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
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="54b16-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="54b16-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)

<span data-ttu-id="54b16-108">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="54b16-108">IP Flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="54b16-109">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span><span class="sxs-lookup"><span data-stu-id="54b16-109">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="54b16-110">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span><span class="sxs-lookup"><span data-stu-id="54b16-110">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="54b16-111">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span><span class="sxs-lookup"><span data-stu-id="54b16-111">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

<span data-ttu-id="54b16-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span><span class="sxs-lookup"><span data-stu-id="54b16-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="54b16-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span><span class="sxs-lookup"><span data-stu-id="54b16-113">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="54b16-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="54b16-114">Before you begin</span></span>

<span data-ttu-id="54b16-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="54b16-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="54b16-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="54b16-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="54b16-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="54b16-117">Scenario</span></span>

<span data-ttu-id="54b16-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span><span class="sxs-lookup"><span data-stu-id="54b16-118">This scenario uses IP Flow Verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="54b16-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span><span class="sxs-lookup"><span data-stu-id="54b16-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="54b16-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="54b16-120">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>


## <a name="get-a-vm"></a><span data-ttu-id="54b16-121">Get a VM</span><span class="sxs-lookup"><span data-stu-id="54b16-121">Get a VM</span></span>

<span data-ttu-id="54b16-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span><span class="sxs-lookup"><span data-stu-id="54b16-122">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="54b16-123">An Id of a virtual machine is required for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="54b16-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="54b16-124">If you already know the ID of the virtual machine to use, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="54b16-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```
azure vm show -g resourceGroupName -n virtualMachineName
```

## <a name="get-the-nics"></a><span data-ttu-id="54b16-125">Get the NICS</span><span class="sxs-lookup"><span data-stu-id="54b16-125">Get the NICS</span></span>

<span data-ttu-id="54b16-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="54b16-126">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="54b16-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="54b16-127">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```
azure network nic show -g resourceGroupName -n nicName
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="54b16-128">Run IP flow verify</span><span class="sxs-lookup"><span data-stu-id="54b16-128">Run IP flow verify</span></span>

<span data-ttu-id="54b16-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span><span class="sxs-lookup"><span data-stu-id="54b16-129">Now that we have the information needed to run the cmdlet, we run the `network watcher ip-flow-verify` cmdlet to test the traffic.</span></span> <span data-ttu-id="54b16-130">In this example, we are using the first IP address on the first NIC.</span><span class="sxs-lookup"><span data-stu-id="54b16-130">In this example, we are using the first IP address on the first NIC.</span></span>

```
azure network watcher ip-flow-verify -g resourceGroupName -n networkWatcherName -t targetResourceId -d directionInboundorOutbound -p protocolTCPorUDP -o localPort -m remotePort -l localIpAddr -r remoteIpAddr
```

> [!NOTE]
> IP Flow verify requires that the VM resource is allocated to run.

## <a name="review-results"></a><span data-ttu-id="54b16-132">Review Results</span><span class="sxs-lookup"><span data-stu-id="54b16-132">Review Results</span></span>

<span data-ttu-id="54b16-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span><span class="sxs-lookup"><span data-stu-id="54b16-133">After running `network watcher ip-flow-verify` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
data:    Access                          : Deny
data:    Rule Name                       : defaultSecurityRules/DefaultInboundDenyAll
info:    network watcher ip-flow-verify command OK
```

## <a name="next-steps"></a><span data-ttu-id="54b16-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="54b16-134">Next steps</span></span>

<span data-ttu-id="54b16-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span><span class="sxs-lookup"><span data-stu-id="54b16-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

<span data-ttu-id="54b16-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="54b16-136">Learn to audit your NSG settings by visiting [Auditing Network Security Groups (NSG) with Network Watcher](network-watcher-nsg-auditing-powershell.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure2.png


