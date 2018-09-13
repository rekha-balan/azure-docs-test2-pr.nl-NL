---
title: Open ports to a VM using the Azure portal | Microsoft Docs
description: Learn how to open a port / create an endpoint to your Windows VM using the resource manager deployment model in the Azure Portal
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 4a71ba7d440f848b5af06a96055929c7cacaeb4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553362"
---
# <a name="opening-ports-to-a-vm-in-azure-using-the-azure-portal"></a><span data-ttu-id="9925f-103">Opening ports to a VM in Azure using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9925f-103">Opening ports to a VM in Azure using the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="9925f-104">Quick commands</span><span class="sxs-lookup"><span data-stu-id="9925f-104">Quick commands</span></span>
<span data-ttu-id="9925f-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9925f-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="9925f-106">First, create your Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="9925f-106">First, create your Network Security Group.</span></span> <span data-ttu-id="9925f-107">Select a resource group in the portal, click **Add**, then search for and select 'Network security group':</span><span class="sxs-lookup"><span data-stu-id="9925f-107">Select a resource group in the portal, click **Add**, then search for and select 'Network security group':</span></span>

![Add a Network Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="9925f-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span><span class="sxs-lookup"><span data-stu-id="9925f-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="9925f-110">Click **Create** when finished:</span><span class="sxs-lookup"><span data-stu-id="9925f-110">Click **Create** when finished:</span></span>

![Create a Network Security Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="9925f-112">Select your new Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="9925f-112">Select your new Network Security Group.</span></span> <span data-ttu-id="9925f-113">Select 'Inbound security rules', then click the **Add** button to create a rule:</span><span class="sxs-lookup"><span data-stu-id="9925f-113">Select 'Inbound security rules', then click the **Add** button to create a rule:</span></span>

![Add an inbound rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="9925f-115">Provide a name for your new rule.</span><span class="sxs-lookup"><span data-stu-id="9925f-115">Provide a name for your new rule.</span></span> <span data-ttu-id="9925f-116">Port 80 is already entered by default.</span><span class="sxs-lookup"><span data-stu-id="9925f-116">Port 80 is already entered by default.</span></span> <span data-ttu-id="9925f-117">This blade is where you would change the source, protocol, and destination when adding additional rules to your Network Security Group.</span><span class="sxs-lookup"><span data-stu-id="9925f-117">This blade is where you would change the source, protocol, and destination when adding additional rules to your Network Security Group.</span></span> <span data-ttu-id="9925f-118">Click **OK** to create the rule:</span><span class="sxs-lookup"><span data-stu-id="9925f-118">Click **OK** to create the rule:</span></span>

![Create an inbound rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="9925f-120">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span><span class="sxs-lookup"><span data-stu-id="9925f-120">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="9925f-121">Let's associate the Network Security Group with a subnet.</span><span class="sxs-lookup"><span data-stu-id="9925f-121">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="9925f-122">Select 'Subnets', then click **Associate**:</span><span class="sxs-lookup"><span data-stu-id="9925f-122">Select 'Subnets', then click **Associate**:</span></span>

![Associate a Network Security Group with a subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="9925f-124">Select your virtual network, and then select the appropriate subnet:</span><span class="sxs-lookup"><span data-stu-id="9925f-124">Select your virtual network, and then select the appropriate subnet:</span></span>

![Associating a Network Security Group with virtual networking](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="9925f-126">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span><span class="sxs-lookup"><span data-stu-id="9925f-126">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="9925f-127">Any VMs you connect to that subnet are reachable on port 80.</span><span class="sxs-lookup"><span data-stu-id="9925f-127">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="9925f-128">More information on Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="9925f-128">More information on Network Security Groups</span></span>
<span data-ttu-id="9925f-129">The quick commands here allow you to get up and running with traffic flowing to your VM.</span><span class="sxs-lookup"><span data-stu-id="9925f-129">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="9925f-130">Network Security Groups provide many great features and granularity for controlling access to your resources.</span><span class="sxs-lookup"><span data-stu-id="9925f-130">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="9925f-131">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9925f-131">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="9925f-132">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="9925f-132">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="9925f-133">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="9925f-133">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="9925f-134">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span><span class="sxs-lookup"><span data-stu-id="9925f-134">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="9925f-135">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span><span class="sxs-lookup"><span data-stu-id="9925f-135">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="9925f-136">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9925f-136">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9925f-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="9925f-137">Next steps</span></span>
<span data-ttu-id="9925f-138">In this example, you created a simple rule to allow HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="9925f-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="9925f-139">You can find information on creating more detailed environments in the following articles:</span><span class="sxs-lookup"><span data-stu-id="9925f-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="9925f-140">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="9925f-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="9925f-141">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="9925f-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="9925f-142">Azure Resource Manager Overview for Load Balancers</span><span class="sxs-lookup"><span data-stu-id="9925f-142">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)







