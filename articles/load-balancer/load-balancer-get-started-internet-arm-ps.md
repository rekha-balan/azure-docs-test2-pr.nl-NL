---
title: Create an Azure Internet-facing load balancer - PowerShell | Microsoft Docs
description: Learn how to create an Internet-facing load balancer in Resource Manager by using PowerShell
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 8257f548-7019-417f-b15f-d004a1eec826
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: f610afbdfac7b5dd9a1a5eb6812c86d8ce0d63e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555288"
---
# <a name="get-started"></a><span data-ttu-id="9f81e-103">Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f81e-103">Creating an Internet-facing load balancer in Resource Manager by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="9f81e-108">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="9f81e-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="9f81e-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9f81e-109">You can also [learn how to create an Internet-facing load balancer by using the classic deployment model](load-balancer-get-started-internet-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-the-solution-by-using-azure-powershell"></a><span data-ttu-id="9f81e-110">Deploying the solution by using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9f81e-110">Deploying the solution by using Azure PowerShell</span></span>

<span data-ttu-id="9f81e-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f81e-111">The following procedures explain how to create an Internet-facing load balancer by using Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="9f81e-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span><span class="sxs-lookup"><span data-stu-id="9f81e-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a load balancer.</span></span>

<span data-ttu-id="9f81e-113">You must create and configure the following objects to deploy a load balancer:</span><span class="sxs-lookup"><span data-stu-id="9f81e-113">You must create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="9f81e-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span><span class="sxs-lookup"><span data-stu-id="9f81e-114">Front-end IP configuration: contains public IP (PIP) addresses for incoming network traffic.</span></span>
* <span data-ttu-id="9f81e-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="9f81e-115">Back-end address pool: contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="9f81e-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="9f81e-116">Load-balancing rules: contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="9f81e-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="9f81e-117">Inbound NAT rules: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="9f81e-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="9f81e-118">Probes: contains health probes used to check availability of virtual machine instances in the back-end address pool.</span></span>

<span data-ttu-id="9f81e-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9f81e-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-powershell-to-use-resource-manager"></a><span data-ttu-id="9f81e-120">Set up PowerShell to use Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9f81e-120">Set up PowerShell to use Resource Manager</span></span>

<span data-ttu-id="9f81e-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9f81e-121">Make sure you have the latest production version of the Azure Resource Manager module for PowerShell:</span></span>

1. <span data-ttu-id="9f81e-122">Sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="9f81e-122">Sign in to Azure.</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="9f81e-123">Enter your credentials when prompted.</span><span class="sxs-lookup"><span data-stu-id="9f81e-123">Enter your credentials when prompted.</span></span>

2. <span data-ttu-id="9f81e-124">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="9f81e-124">Check the subscriptions for the account.</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="9f81e-125">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="9f81e-125">Choose which of your Azure subscriptions to use.</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId 'GUID of subscription'
    ```

4. <span data-ttu-id="9f81e-126">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="9f81e-126">Create a resource group.</span></span> <span data-ttu-id="9f81e-127">(Skip this step if you're using an existing resource group.)</span><span class="sxs-lookup"><span data-stu-id="9f81e-127">(Skip this step if you're using an existing resource group.)</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name NRP-RG -location "West US"
    ```

## <a name="create-a-virtual-network-and-a-public-ip-address-for-the-front-end-ip-pool"></a><span data-ttu-id="9f81e-128">Create a virtual network and a public IP address for the front-end IP pool</span><span class="sxs-lookup"><span data-stu-id="9f81e-128">Create a virtual network and a public IP address for the front-end IP pool</span></span>

1. <span data-ttu-id="9f81e-129">Create a subnet and a virtual network.</span><span class="sxs-lookup"><span data-stu-id="9f81e-129">Create a subnet and a virtual network.</span></span>

    ```powershell
    $backendSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -AddressPrefix 10.0.2.0/24
    New-AzureRmvirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG -Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $backendSubnet
    ```

2. <span data-ttu-id="9f81e-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="9f81e-130">Create an Azure public IP address resource, named **PublicIP**, to be used by a front-end IP pool with the DNS name **loadbalancernrp.westus.cloudapp.azure.com**.</span></span> <span data-ttu-id="9f81e-131">The following command uses the static allocation type.</span><span class="sxs-lookup"><span data-stu-id="9f81e-131">The following command uses the static allocation type.</span></span>

    ```powershell
    $publicIP = New-AzureRmPublicIpAddress -Name PublicIp -ResourceGroupName NRP-RG -Location 'West US' -AllocationMethod Static -DomainNameLabel loadbalancernrp
    ```

   > [!IMPORTANT]
   > The load balancer uses the domain label of the public IP as a prefix for its FQDN. This is different from the classic deployment model, which uses the cloud service as the load balancer FQDN.
   > In this example, the FQDN is **loadbalancernrp.westus.cloudapp.azure.com**.

## <a name="create-a-front-end-ip-pool-and-a-back-end-address-pool"></a><span data-ttu-id="9f81e-135">Create a front-end IP pool and a back-end address pool</span><span class="sxs-lookup"><span data-stu-id="9f81e-135">Create a front-end IP pool and a back-end address pool</span></span>

1. <span data-ttu-id="9f81e-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span><span class="sxs-lookup"><span data-stu-id="9f81e-136">Create a front-end IP pool named **LB-Frontend** that uses the **PublicIp** resource.</span></span>

    ```powershell
    $frontendIP = New-AzureRmLoadBalancerFrontendIpConfig -Name LB-Frontend -PublicIpAddress $publicIP
    ```

2. <span data-ttu-id="9f81e-137">Create a back-end address pool named **LB-backend**.</span><span class="sxs-lookup"><span data-stu-id="9f81e-137">Create a back-end address pool named **LB-backend**.</span></span>

    ```powershell
    $beaddresspool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name LB-backend
    ```

## <a name="create-nat-rules-a-load-balancer-rule-a-probe-and-a-load-balancer"></a><span data-ttu-id="9f81e-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-138">Create NAT rules, a load balancer rule, a probe, and a load balancer</span></span>

<span data-ttu-id="9f81e-139">This example creates the following items:</span><span class="sxs-lookup"><span data-stu-id="9f81e-139">This example creates the following items:</span></span>

* <span data-ttu-id="9f81e-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span><span class="sxs-lookup"><span data-stu-id="9f81e-140">A NAT rule to translate all incoming traffic on port 3441 to port 3389</span></span>
* <span data-ttu-id="9f81e-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span><span class="sxs-lookup"><span data-stu-id="9f81e-141">A NAT rule to translate all incoming traffic on port 3442 to port 3389</span></span>
* <span data-ttu-id="9f81e-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span><span class="sxs-lookup"><span data-stu-id="9f81e-142">A probe rule to check the health status on a page named **HealthProbe.aspx**</span></span>
* <span data-ttu-id="9f81e-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span><span class="sxs-lookup"><span data-stu-id="9f81e-143">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool</span></span>
* <span data-ttu-id="9f81e-144">A load balancer that uses all these objects</span><span class="sxs-lookup"><span data-stu-id="9f81e-144">A load balancer that uses all these objects</span></span>

<span data-ttu-id="9f81e-145">Use these steps:</span><span class="sxs-lookup"><span data-stu-id="9f81e-145">Use these steps:</span></span>

1. <span data-ttu-id="9f81e-146">Create the NAT rules.</span><span class="sxs-lookup"><span data-stu-id="9f81e-146">Create the NAT rules.</span></span>

    ```powershell
    $inboundNATRule1= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP1 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3441 -BackendPort 3389

    $inboundNATRule2= New-AzureRmLoadBalancerInboundNatRuleConfig -Name RDP2 -FrontendIpConfiguration $frontendIP -Protocol TCP -FrontendPort 3442 -BackendPort 3389
    ```

2. <span data-ttu-id="9f81e-147">Create a health probe.</span><span class="sxs-lookup"><span data-stu-id="9f81e-147">Create a health probe.</span></span> <span data-ttu-id="9f81e-148">There are two ways to configure a probe:</span><span class="sxs-lookup"><span data-stu-id="9f81e-148">There are two ways to configure a probe:</span></span>

    <span data-ttu-id="9f81e-149">HTTP probe</span><span class="sxs-lookup"><span data-stu-id="9f81e-149">HTTP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -RequestPath 'HealthProbe.aspx' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

    <span data-ttu-id="9f81e-150">TCP probe</span><span class="sxs-lookup"><span data-stu-id="9f81e-150">TCP probe</span></span>

    ```powershell
    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HealthProbe -Protocol Tcp -Port 80 -IntervalInSeconds 15 -ProbeCount 2
    ```

3. <span data-ttu-id="9f81e-151">Create a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="9f81e-151">Create a load balancer rule.</span></span>

    ```powershell
    $lbrule = New-AzureRmLoadBalancerRuleConfig -Name HTTP -FrontendIpConfiguration $frontendIP -BackendAddressPool  $beAddressPool -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

4. <span data-ttu-id="9f81e-152">Create the load balancer by using the previously created objects.</span><span class="sxs-lookup"><span data-stu-id="9f81e-152">Create the load balancer by using the previously created objects.</span></span>

    ```powershell
    $NRPLB = New-AzureRmLoadBalancer -ResourceGroupName NRP-RG -Name NRP-LB -Location 'West US' -FrontendIpConfiguration $frontendIP -InboundNatRule $inboundNATRule1,$inboundNatRule2 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

## <a name="create-nics"></a><span data-ttu-id="9f81e-153">Create NICs</span><span class="sxs-lookup"><span data-stu-id="9f81e-153">Create NICs</span></span>

<span data-ttu-id="9f81e-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span><span class="sxs-lookup"><span data-stu-id="9f81e-154">Create network interfaces (or modify existing ones) and then associate them to NAT rules, load balancer rules, and probes:</span></span>

1. <span data-ttu-id="9f81e-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span><span class="sxs-lookup"><span data-stu-id="9f81e-155">Get the virtual network and a virtual network subnet, where the NICs need to be created.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name NRPVNet -ResourceGroupName NRP-RG
    $backendSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name LB-Subnet-BE -VirtualNetwork $vnet
    ```

2. <span data-ttu-id="9f81e-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="9f81e-156">Create a NIC named **lb-nic1-be**, and associate it with the first NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic1= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic1-be -Location 'West US' -PrivateIpAddress 10.0.2.6 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[0]
    ```

3. <span data-ttu-id="9f81e-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="9f81e-157">Create a NIC named **lb-nic2-be**, and associate it with the second NAT rule and the first (and only) back-end address pool.</span></span>

    ```powershell
    $backendnic2= New-AzureRmNetworkInterface -ResourceGroupName NRP-RG -Name lb-nic2-be -Location 'West US' -PrivateIpAddress 10.0.2.7 -Subnet $backendSubnet -LoadBalancerBackendAddressPool $nrplb.BackendAddressPools[0] -LoadBalancerInboundNatRule $nrplb.InboundNatRules[1]
    ```

4. <span data-ttu-id="9f81e-158">Check the NICs.</span><span class="sxs-lookup"><span data-stu-id="9f81e-158">Check the NICs.</span></span>

        $backendnic1

    <span data-ttu-id="9f81e-159">Expected output:</span><span class="sxs-lookup"><span data-stu-id="9f81e-159">Expected output:</span></span>

        Name                 : lb-nic1-be
        ResourceGroupName    : NRP-RG
        Location             : westus
        Id                   : /subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        Etag                 : W/"d448256a-e1df-413a-9103-a137e07276d1"
        ResourceGuid         : 896cac4f-152a-40b9-b079-3e2201a5906e
        ProvisioningState    : Succeeded
        Tags                 :
        VirtualMachine       : null
        IpConfigurations     : [
                            {
                            "Name": "ipconfig1",
                            "Etag": "W/\"d448256a-e1df-413a-9103-a137e07276d1\"",
                            "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/ipconfig1",
                            "PrivateIpAddress": "10.0.2.6",
                            "PrivateIpAllocationMethod": "Static",
                            "Subnet": {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/virtualNetworks/NRPVNet/subnets/LB-Subnet-BE"
                            },
                            "ProvisioningState": "Succeeded",
                            "PrivateIpAddressVersion": "IPv4",
                            "PublicIpAddress": {
                                "Id": null
                            },
                            "LoadBalancerBackendAddressPools": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/backendAddressPools/LB-backend"
                                }
                            ],
                            "LoadBalancerInboundNatRules": [
                                {
                                "Id": "/subscriptions/f50504a2-1865-4541-823a-b32842e3e0ee/resourceGroups/NRP-RG/providers/Microsoft.Network/loadBalancers/NRPlb/inboundNatRules/RDP1"
                                }
                            ],
                            "Primary": true,
                            "ApplicationGatewayBackendAddressPools": []
                            }
                        ]
        DnsSettings          : {
                            "DnsServers": [],
                            "AppliedDnsServers": [],
                            "InternalDomainNameSuffix": "prcwibzcuvie5hnxav0yjks2cd.dx.internal.cloudapp.net"
                        }
        EnableIPForwarding   : False
        NetworkSecurityGroup : null
        Primary              :

5. <span data-ttu-id="9f81e-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span><span class="sxs-lookup"><span data-stu-id="9f81e-160">Use the `Add-AzureRmVMNetworkInterface` cmdlet to assign the NICs to different VMs.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="9f81e-161">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="9f81e-161">Create a virtual machine</span></span>

<span data-ttu-id="9f81e-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9f81e-162">For guidance on creating a virtual machine and assigning a NIC, see [Create an Azure VM using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

## <a name="add-the-network-interface-to-the-load-balancer"></a><span data-ttu-id="9f81e-163">Add the network interface to the load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-163">Add the network interface to the load balancer</span></span>

1. <span data-ttu-id="9f81e-164">Retrieve the load balancer from Azure.</span><span class="sxs-lookup"><span data-stu-id="9f81e-164">Retrieve the load balancer from Azure.</span></span>

    <span data-ttu-id="9f81e-165">Load the load balancer resource into a variable (if you haven't done that yet).</span><span class="sxs-lookup"><span data-stu-id="9f81e-165">Load the load balancer resource into a variable (if you haven't done that yet).</span></span> <span data-ttu-id="9f81e-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="9f81e-166">The variable is called **$lb**. Use the same names from the load balancer resource that you created earlier.</span></span>

    ```powershell
    $lb= get-azurermloadbalancer -name NRP-LB -resourcegroupname NRP-RG
    ```

2. <span data-ttu-id="9f81e-167">Load the back-end configuration to a variable.</span><span class="sxs-lookup"><span data-stu-id="9f81e-167">Load the back-end configuration to a variable.</span></span>

    ```powershell
    $backend=Get-AzureRmLoadBalancerBackendAddressPoolConfig -name LB-backend -LoadBalancer $lb
    ```

3. <span data-ttu-id="9f81e-168">Load the already created network interface into a variable.</span><span class="sxs-lookup"><span data-stu-id="9f81e-168">Load the already created network interface into a variable.</span></span> <span data-ttu-id="9f81e-169">The variable name is **$nic**.</span><span class="sxs-lookup"><span data-stu-id="9f81e-169">The variable name is **$nic**.</span></span> <span data-ttu-id="9f81e-170">The network interface name is the same one from the earlier example.</span><span class="sxs-lookup"><span data-stu-id="9f81e-170">The network interface name is the same one from the earlier example.</span></span>

    ```powershell
    $nic =get-azurermnetworkinterface -name lb-nic1-be -resourcegroupname NRP-RG
    ```

4. <span data-ttu-id="9f81e-171">Change the back-end configuration on the network interface.</span><span class="sxs-lookup"><span data-stu-id="9f81e-171">Change the back-end configuration on the network interface.</span></span>

    ```powershell
    $nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$backend
    ```

5. <span data-ttu-id="9f81e-172">Save the network interface object.</span><span class="sxs-lookup"><span data-stu-id="9f81e-172">Save the network interface object.</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```

    <span data-ttu-id="9f81e-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span><span class="sxs-lookup"><span data-stu-id="9f81e-173">After a network interface is added to the load balancer back-end pool, it starts receiving network traffic based on the load-balancing rules for that load balancer resource.</span></span>

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="9f81e-174">Update an existing load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-174">Update an existing load balancer</span></span>

1. <span data-ttu-id="9f81e-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="9f81e-175">By using the load balancer from the earlier example, assign a load balancer object to the variable **$slb** by using `Get-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb = get-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
    ```

2. <span data-ttu-id="9f81e-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span><span class="sxs-lookup"><span data-stu-id="9f81e-176">In the following example, you add an inbound NAT rule--by using port 81 in the front-end pool and port 8181 for the back-end pool--to an existing load balancer.</span></span>

    ```powershell
    $slb | Add-AzureRmLoadBalancerInboundNatRuleConfig -Name NewRule -FrontendIpConfiguration $slb.FrontendIpConfigurations[0] -FrontendPort 81  -BackendPort 8181 -Protocol TCP
    ```

3. <span data-ttu-id="9f81e-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="9f81e-177">Save the new configuration by using `Set-AzureLoadBalancer`.</span></span>

    ```powershell
    $slb | Set-AzureRmLoadBalancer
    ```

## <a name="remove-a-load-balancer"></a><span data-ttu-id="9f81e-178">Remove a load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-178">Remove a load balancer</span></span>

<span data-ttu-id="9f81e-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span><span class="sxs-lookup"><span data-stu-id="9f81e-179">Use the command `Remove-AzureLoadBalancer` to delete a previously created load balancer named **NRP-LB** in a resource group called **NRP-RG**.</span></span>

```powershell
Remove-AzureRmLoadBalancer -Name NRP-LB -ResourceGroupName NRP-RG
```

> [!NOTE]
> You can use the optional switch **-Force** to avoid the prompt for deletion.

## <a name="next-steps"></a><span data-ttu-id="9f81e-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="9f81e-181">Next steps</span></span>

[<span data-ttu-id="9f81e-182">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-182">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="9f81e-183">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="9f81e-183">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="9f81e-184">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="9f81e-184">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
