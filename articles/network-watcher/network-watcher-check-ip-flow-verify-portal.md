---
title: Verify traffic with Azure Network Watcher IP flow verify - Azure portal | Microsoft Docs
description: This article describes how to check if traffic to or from a virtual machine is allowed or denied
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 526431d13828e40318f907b7bcbc12ecbd666b11
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549096"
---
# <a name="check-if-traffic-is-allowed-or-denied-to-or-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="b0cd2-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="b0cd2-103">Check if traffic is allowed or denied to or from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [Azure portal](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [CLI](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)

<span data-ttu-id="b0cd2-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-108">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="b0cd2-109">The validation can be run for incoming or outgoing traffic.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-109">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="b0cd2-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-110">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or another resource.</span></span> <span data-ttu-id="b0cd2-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-111">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="b0cd2-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-112">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b0cd2-113">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b0cd2-113">Before you begin</span></span>

<span data-ttu-id="b0cd2-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="b0cd2-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="b0cd2-116">Scenario</span><span class="sxs-lookup"><span data-stu-id="b0cd2-116">Scenario</span></span>

<span data-ttu-id="b0cd2-117">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-117">This scenario uses IP Flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="b0cd2-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-118">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="b0cd2-119">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b0cd2-119">To learn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="b0cd2-120">Run IP flow verify</span><span class="sxs-lookup"><span data-stu-id="b0cd2-120">Run IP flow verify</span></span>

<span data-ttu-id="b0cd2-121">Navigate to your Network Watcher and click **IP flow verify**.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-121">Navigate to your Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="b0cd2-122">Select the virtual machine and network interface you want to verify traffic from.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-122">Select the virtual machine and network interface you want to verify traffic from.</span></span> <span data-ttu-id="b0cd2-123">Enter any additional filtering information and click **Check**.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-123">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="b0cd2-124">Once you click **Check**, the flow based on the criteria you provided is checked.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-124">Once you click **Check**, the flow based on the criteria you provided is checked.</span></span> <span data-ttu-id="b0cd2-125">The result is either **Access allowed** or **Access denied**.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-125">The result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="b0cd2-126">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-126">If access is denied, the Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="b0cd2-127">If the denial of traffic is expected behavior, then the rule was successful.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-127">If the denial of traffic is expected behavior, then the rule was successful.</span></span>

> [!NOTE]
> IP flow verify requires that the VM resource is allocated.

<span data-ttu-id="b0cd2-129">As you can see from the following image, the outbound HTTPS traffic was allowed.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-129">As you can see from the following image, the outbound HTTPS traffic was allowed.</span></span>

![ip flow verify overview][1]

<span data-ttu-id="b0cd2-131">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-131">As seen in the following image, traffic is changed to inbound and the inbound port changed to 123.</span></span> <span data-ttu-id="b0cd2-132">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-132">Traffic is now denied, the message "Access denied" is provided along with the network security group and security rule that deny the traffic.</span></span>

![ip flow results][2]

## <a name="next-steps"></a><span data-ttu-id="b0cd2-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="b0cd2-134">Next steps</span></span>

<span data-ttu-id="b0cd2-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span><span class="sxs-lookup"><span data-stu-id="b0cd2-135">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that are defined.</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/network-watcher/media/network-watcher-check-ip-flow-verify-portal/figure2.png















