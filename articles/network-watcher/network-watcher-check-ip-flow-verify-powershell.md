---
title: verify traffic with Azure Network Watcher IP flow verify - PowerShell | Microsoft Docs
description: This article describes how to check if traffic to or from a virtual machine is allowed or denied using PowerShell
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: e1dad757-8c5d-467f-812e-7cc751143207
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 42c842e3beefefb00d1d8826b0d110467a2fc802
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556001"
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="fc1f8-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="fc1f8-103">Check if traffic is allowed or denied to or from a VM with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)

<span data-ttu-id="fc1f8-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="fc1f8-109">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-109">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="fc1f8-110">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-110">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="fc1f8-111">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-111">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fc1f8-112">Before you begin</span><span class="sxs-lookup"><span data-stu-id="fc1f8-112">Before you begin</span></span>

<span data-ttu-id="fc1f8-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="fc1f8-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="fc1f8-115">Scenario</span><span class="sxs-lookup"><span data-stu-id="fc1f8-115">Scenario</span></span>

<span data-ttu-id="fc1f8-116">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-116">This scenario uses IP flow verify to verify if a virtual machine can talk to a known Bing IP address.</span></span> <span data-ttu-id="fc1f8-117">If the traffic is denied, it returns the security rule that is denying that traffic.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-117">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="fc1f8-118">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="fc1f8-118">To learn more about IP flow verify, visit [IP flow verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="fc1f8-119">Retrieve Network Watcher</span><span class="sxs-lookup"><span data-stu-id="fc1f8-119">Retrieve Network Watcher</span></span>

<span data-ttu-id="fc1f8-120">The first step is to retrieve the Network Watcher instance.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-120">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="fc1f8-121">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-121">The `$networkWatcher` variable is passed to the IP flow verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-vm"></a><span data-ttu-id="fc1f8-122">Get a VM</span><span class="sxs-lookup"><span data-stu-id="fc1f8-122">Get a VM</span></span>

<span data-ttu-id="fc1f8-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-123">IP flow verify tests traffic to or from an IP address on a virtual machine to or from a remote destination.</span></span> <span data-ttu-id="fc1f8-124">An Id of a virtual machine is required for the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-124">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="fc1f8-125">If you already know the ID of the virtual machine to use, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-125">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

## <a name="get-the-nics"></a><span data-ttu-id="fc1f8-126">Get the NICS</span><span class="sxs-lookup"><span data-stu-id="fc1f8-126">Get the NICS</span></span>

<span data-ttu-id="fc1f8-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="fc1f8-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkInterfaceIDs.ForEach({$_})}
```

## <a name="run-ip-flow-verify"></a><span data-ttu-id="fc1f8-129">Run IP flow verify</span><span class="sxs-lookup"><span data-stu-id="fc1f8-129">Run IP flow verify</span></span>

<span data-ttu-id="fc1f8-130">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-130">Now that we have the information needed to run the cmdlet, we run the `Test-AzureRmNetworkWatcherIPFlow` cmdlet to test the traffic.</span></span> <span data-ttu-id="fc1f8-131">In this example, we are using the first IP address on the first NIC.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-131">In this example, we are using the first IP address on the first NIC.</span></span>

```powershell
Test-AzureRmNetworkWatcherIPFlow -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id `
-Direction Outbound -Protocol TCP `
-LocalIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress -LocalPort 6895 -RemoteIPAddress 204.79.197.200 -RemotePort 80
```

> [!NOTE]
> IP flow verify requires that the VM resource is allocated to run.

## <a name="review-results"></a><span data-ttu-id="fc1f8-133">Review Results</span><span class="sxs-lookup"><span data-stu-id="fc1f8-133">Review Results</span></span>

<span data-ttu-id="fc1f8-134">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-134">After running `Test-AzureRmNetworkWatcherIPFlow` the results are returned, the following example is the results returned from the preceding step.</span></span>

```
Access RuleName                                  
------ --------                                  
Allow  defaultSecurityRules/AllowInternetOutBound
```

## <a name="next-steps"></a><span data-ttu-id="fc1f8-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc1f8-135">Next steps</span></span>

<span data-ttu-id="fc1f8-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span><span class="sxs-lookup"><span data-stu-id="fc1f8-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure2.png















