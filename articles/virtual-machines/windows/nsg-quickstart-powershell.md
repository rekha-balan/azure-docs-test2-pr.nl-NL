---
title: Open ports to a VM using Azure PowerShell | Microsoft Docs
description: Learn how to open a port / create an endpoint to your Windows VM using the Azure resource manager deployment mode and Azure PowerShell
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: cf45f7d8-451a-48ab-8419-730366d54f1e
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 90dfe30050edc02180b6f3512876208e44b24f40
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555882"
---
# <a name="opening-ports-and-endpoints-to-a-vm-in-azure-using-powershell"></a><span data-ttu-id="5d6bd-103">Opening ports and endpoints to a VM in Azure using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d6bd-103">Opening ports and endpoints to a VM in Azure using PowerShell</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="5d6bd-104">Quick commands</span><span class="sxs-lookup"><span data-stu-id="5d6bd-104">Quick commands</span></span>
<span data-ttu-id="5d6bd-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="5d6bd-105">To create a Network Security Group and ACL rules you need [the latest version of Azure PowerShell installed](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="5d6bd-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5d6bd-106">You can also [perform these steps using the Azure portal](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5d6bd-107">Log in to your Azure account:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-107">Log in to your Azure account:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="5d6bd-108">In the following examples, replace example parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-108">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="5d6bd-109">Example parameter names included `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-109">Example parameter names included `myResourceGroup`, `myNetworkSecurityGroup`, and `myVnet`.</span></span>

<span data-ttu-id="5d6bd-110">Create a rule.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-110">Create a rule.</span></span> <span data-ttu-id="5d6bd-111">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-111">The following example creates a rule named `myNetworkSecurityGroupRule` to allow TCP traffic on port 80:</span></span>

```powershell
$httprule = New-AzureRmNetworkSecurityRuleConfig -Name "myNetworkSecurityGroupRule" `
    -Description "Allow HTTP" -Access "Allow" -Protocol "Tcp" -Direction "Inbound" `
    -Priority "100" -SourceAddressPrefix "Internet" -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 80
```

<span data-ttu-id="5d6bd-112">Next, create your Network Security group and assign the HTTP rule you just created as follows.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-112">Next, create your Network Security group and assign the HTTP rule you just created as follows.</span></span> <span data-ttu-id="5d6bd-113">The following example creates a Network Security Group named `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-113">The following example creates a Network Security Group named `myNetworkSecurityGroup`:</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" `
    -Location "WestUS" -Name "myNetworkSecurityGroup" -SecurityRules $httprule
```

<span data-ttu-id="5d6bd-114">Now let's assign your Network Security Group to a subnet.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-114">Now let's assign your Network Security Group to a subnet.</span></span> <span data-ttu-id="5d6bd-115">The following example assigns an existing virtual network named `myVnet` to the variable `$vnet`:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-115">The following example assigns an existing virtual network named `myVnet` to the variable `$vnet`:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
    -Name "myVnet"
```

<span data-ttu-id="5d6bd-116">Associate your Network Security Group with your subnet.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-116">Associate your Network Security Group with your subnet.</span></span> <span data-ttu-id="5d6bd-117">The following example associates the subnet named `mySubnet` with your Network Security Group:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-117">The following example associates the subnet named `mySubnet` with your Network Security Group:</span></span>

```powershell
$subnetPrefix = $vnet.Subnets|?{$_.Name -eq 'mySubnet'}

Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "mySubnet" `
    -AddressPrefix $subnetPrefix.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

<span data-ttu-id="5d6bd-118">Finally, update your virtual network in order for your changes to take effect:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-118">Finally, update your virtual network in order for your changes to take effect:</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```


## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="5d6bd-119">More information on Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="5d6bd-119">More information on Network Security Groups</span></span>
<span data-ttu-id="5d6bd-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-120">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="5d6bd-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-121">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="5d6bd-122">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5d6bd-122">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="5d6bd-123">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-123">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="5d6bd-124">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="5d6bd-124">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="5d6bd-125">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-125">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="5d6bd-126">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-126">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="5d6bd-127">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5d6bd-127">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-ps.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d6bd-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="5d6bd-128">Next steps</span></span>
<span data-ttu-id="5d6bd-129">In this example, you created a simple rule to allow HTTP traffic.</span><span class="sxs-lookup"><span data-stu-id="5d6bd-129">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="5d6bd-130">You can find information on creating more detailed environments in the following articles:</span><span class="sxs-lookup"><span data-stu-id="5d6bd-130">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="5d6bd-131">Azure Resource Manager overview</span><span class="sxs-lookup"><span data-stu-id="5d6bd-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="5d6bd-132">What is a Network Security Group (NSG)?</span><span class="sxs-lookup"><span data-stu-id="5d6bd-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="5d6bd-133">Azure Resource Manager Overview for Load Balancers</span><span class="sxs-lookup"><span data-stu-id="5d6bd-133">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

