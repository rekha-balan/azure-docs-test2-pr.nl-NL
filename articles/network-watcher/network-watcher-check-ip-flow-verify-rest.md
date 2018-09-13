---
title: Verify traffic with Azure Network Watcher IP flow verify - REST | Microsoft Docs
description: This article describes how to check if traffic to or from a virtual machine is allowed or denied
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: deb1ad8b541a9d56dbe92f099d626974956a6039
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550012"
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d7ee7-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d7ee7-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)

<span data-ttu-id="d7ee7-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="d7ee7-109">The validation can be run for incoming or outgoing traffic.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-109">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="d7ee7-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="d7ee7-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d7ee7-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d7ee7-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="d7ee7-113">Before you begin</span></span>

<span data-ttu-id="d7ee7-114">ARMclient is used to call the REST API using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-114">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="d7ee7-115">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span><span class="sxs-lookup"><span data-stu-id="d7ee7-115">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="d7ee7-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-116">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d7ee7-117">Scenario</span><span class="sxs-lookup"><span data-stu-id="d7ee7-117">Scenario</span></span>

<span data-ttu-id="d7ee7-118">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-118">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="d7ee7-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-119">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="d7ee7-120">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d7ee7-120">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="d7ee7-121">In this scenario, you:</span><span class="sxs-lookup"><span data-stu-id="d7ee7-121">In this scenario, you:</span></span>

* <span data-ttu-id="d7ee7-122">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="d7ee7-122">Retrieve a virtual machine</span></span>
* <span data-ttu-id="d7ee7-123">Call IP flow verify</span><span class="sxs-lookup"><span data-stu-id="d7ee7-123">Call IP flow verify</span></span>
* <span data-ttu-id="d7ee7-124">Verify results</span><span class="sxs-lookup"><span data-stu-id="d7ee7-124">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="d7ee7-125">Log in with ARMClient</span><span class="sxs-lookup"><span data-stu-id="d7ee7-125">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="d7ee7-126">Retrieve a virtual machine</span><span class="sxs-lookup"><span data-stu-id="d7ee7-126">Retrieve a virtual machine</span></span>

<span data-ttu-id="d7ee7-127">Run the following script to return a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-127">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="d7ee7-128">The following code needs values for the variables:</span><span class="sxs-lookup"><span data-stu-id="d7ee7-128">The following code needs values for the variables:</span></span>

* <span data-ttu-id="d7ee7-129">**subscriptionId** - The subscription Id to use.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-129">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="d7ee7-130">**resourceGroupName** - The name of a resource group that contains virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-130">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="d7ee7-131">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-131">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="d7ee7-132">The results should be similar to the following code sample:</span><span class="sxs-lookup"><span data-stu-id="d7ee7-132">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="d7ee7-133">Call IP flow Verify</span><span class="sxs-lookup"><span data-stu-id="d7ee7-133">Call IP flow Verify</span></span>

<span data-ttu-id="d7ee7-134">The following example creates a request to verify the traffic for a specified virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-134">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="d7ee7-135">The response returns if the traffic is allowed or if the traffic is denied.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-135">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="d7ee7-136">If traffic is denied it also returns what rule blocks the traffic.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-136">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> IP flow verify requires that the VM resource is allocated.

<span data-ttu-id="d7ee7-138">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-138">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="d7ee7-139">These values are provided by the preceding output.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-139">These values are provided by the preceding output.</span></span>

> [!Important]
> For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="d7ee7-141">Understanding the results</span><span class="sxs-lookup"><span data-stu-id="d7ee7-141">Understanding the results</span></span>

<span data-ttu-id="d7ee7-142">The response you get back tells you whether the traffic is allowed or denied.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-142">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="d7ee7-143">The response looks like one of the following examples:</span><span class="sxs-lookup"><span data-stu-id="d7ee7-143">The response looks like one of the following examples:</span></span>

<span data-ttu-id="d7ee7-144">**Allowed**</span><span class="sxs-lookup"><span data-stu-id="d7ee7-144">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="d7ee7-145">**Denied**</span><span class="sxs-lookup"><span data-stu-id="d7ee7-145">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="d7ee7-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7ee7-146">Next steps</span></span>

<span data-ttu-id="d7ee7-147">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="d7ee7-147">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












