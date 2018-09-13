---
title: Load balancing on multiple IP configurations in Azure| Microsoft Docs
description: Load balancing across primary and secondary IP configurations.
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: annahar
ms.openlocfilehash: e535043a12e0701101a9731b2ab6b0f3d8b19c74
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555962"
---
# <a name="load-balancing-on-multiple-ip-configurations-using-powershell"></a><span data-ttu-id="08157-103">Load balancing on multiple IP configurations using PowerShell</span><span class="sxs-lookup"><span data-stu-id="08157-103">Load balancing on multiple IP configurations using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [CLI](load-balancer-multiple-ip-cli.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)

<span data-ttu-id="08157-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span><span class="sxs-lookup"><span data-stu-id="08157-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).</span></span> <span data-ttu-id="08157-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span><span class="sxs-lookup"><span data-stu-id="08157-108">For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="08157-109">Each of the secondary NICs have two IP configurations.</span><span class="sxs-lookup"><span data-stu-id="08157-109">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="08157-110">Each VM hosts both websites contoso.com and fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="08157-110">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="08157-111">Each website is bound to one of the IP configurations on the secondary NIC.</span><span class="sxs-lookup"><span data-stu-id="08157-111">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="08157-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span><span class="sxs-lookup"><span data-stu-id="08157-112">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="08157-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span><span class="sxs-lookup"><span data-stu-id="08157-113">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB scenario image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-multiple-ip/lb-multi-ip.PNG)

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="08157-115">Steps to load balance on multiple IP configurations</span><span class="sxs-lookup"><span data-stu-id="08157-115">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="08157-116">Follow the steps below to achieve the scenario outlined in this article:</span><span class="sxs-lookup"><span data-stu-id="08157-116">Follow the steps below to achieve the scenario outlined in this article:</span></span>

1. <span data-ttu-id="08157-117">Install Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08157-117">Install Azure PowerShell.</span></span> <span data-ttu-id="08157-118">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span><span class="sxs-lookup"><span data-stu-id="08157-118">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>
2. <span data-ttu-id="08157-119">Create a resource group using the following settings:</span><span class="sxs-lookup"><span data-stu-id="08157-119">Create a resource group using the following settings:</span></span>

    ```powershell
    $location = "westcentralus".
    $myResourceGroup = "contosofabrikam"
    ```

    <span data-ttu-id="08157-120">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08157-120">For more information, see Step 2 of [Create a Resource Group](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

3. <span data-ttu-id="08157-121">[Create an Availability Set](../virtual-machines/windows/create-availability-set.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span><span class="sxs-lookup"><span data-stu-id="08157-121">[Create an Availability Set](../virtual-machines/windows/create-availability-set.md?toc=%2fazure%2fload-balancer%2ftoc.json) to contain your VMs.</span></span> <span data-ttu-id="08157-122">For this scenario, use the following command:</span><span class="sxs-lookup"><span data-stu-id="08157-122">For this scenario, use the following command:</span></span>

    ```powershell
    New-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset" -Location "West Central US"
    ```

4. <span data-ttu-id="08157-123">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span><span class="sxs-lookup"><span data-stu-id="08157-123">Follow instructions steps 3 through 5 in [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) article to prepare the creation of a VM with a single NIC.</span></span> <span data-ttu-id="08157-124">Execute step 6.1, and use the following instead of step 6.2:</span><span class="sxs-lookup"><span data-stu-id="08157-124">Execute step 6.1, and use the following instead of step 6.2:</span></span>

    ```powershell
    $availset = Get-AzureRmAvailabilitySet -ResourceGroupName "contosofabrikam" -Name "myAvailset"
    New-AzureRmVMConfig -VMName "VM1" -VMSize "Standard_DS1_v2" -AvailabilitySetId $availset.Id
    ```

    <span data-ttu-id="08157-125">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span><span class="sxs-lookup"><span data-stu-id="08157-125">Then complete [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json) steps 6.3 through 6.8.</span></span>

5. <span data-ttu-id="08157-126">Add a second IP configuration to each of the VMs.</span><span class="sxs-lookup"><span data-stu-id="08157-126">Add a second IP configuration to each of the VMs.</span></span> <span data-ttu-id="08157-127">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span><span class="sxs-lookup"><span data-stu-id="08157-127">Follow the instructions in [Assign multiple IP addresses to virtual machines](../virtual-network/virtual-network-multiple-ip-addresses-powershell.md#add) article.</span></span> <span data-ttu-id="08157-128">Use the following configuration settings:</span><span class="sxs-lookup"><span data-stu-id="08157-128">Use the following configuration settings:</span></span>

    ```powershell
    $NicName = "VM1-NIC2"
    $RgName = "contosofabrikam"
    $NicLocation = "West Central US"
    $IPConfigName4 = "VM1-ipconfig2"
    $Subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -VirtualNetwork $myVnet
    ```

    <span data-ttu-id="08157-129">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="08157-129">You do not need to associate the secondary IP configurations with public IPs for the purpose of this tutorial.</span></span> <span data-ttu-id="08157-130">Edit the command to remove the public IP association part.</span><span class="sxs-lookup"><span data-stu-id="08157-130">Edit the command to remove the public IP association part.</span></span>

6. <span data-ttu-id="08157-131">Complete steps 4 through 6 of this article again for VM2.</span><span class="sxs-lookup"><span data-stu-id="08157-131">Complete steps 4 through 6 of this article again for VM2.</span></span> <span data-ttu-id="08157-132">Be sure to replace the VM name to VM2 when doing this.</span><span class="sxs-lookup"><span data-stu-id="08157-132">Be sure to replace the VM name to VM2 when doing this.</span></span> <span data-ttu-id="08157-133">Note that you do not need to create a virtual network for the second VM.</span><span class="sxs-lookup"><span data-stu-id="08157-133">Note that you do not need to create a virtual network for the second VM.</span></span> <span data-ttu-id="08157-134">You may or may not create a new subnet based on your use case.</span><span class="sxs-lookup"><span data-stu-id="08157-134">You may or may not create a new subnet based on your use case.</span></span>

7. <span data-ttu-id="08157-135">Create two public IP addresses and store them in the appropriate variables as shown:</span><span class="sxs-lookup"><span data-stu-id="08157-135">Create two public IP addresses and store them in the appropriate variables as shown:</span></span>

    ```powershell
    $publicIP1 = New-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel contoso
    $publicIP2 = New-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam -Location 'West Central US' -AllocationMethod Dynamic -DomainNameLabel fabrikam

    $publicIP1 = Get-AzureRmPublicIpAddress -Name PublicIp1 -ResourceGroupName contosofabrikam
    $publicIP2 = Get-AzureRmPublicIpAddress -Name PublicIp2 -ResourceGroupName contosofabrikam
    ```

8. <span data-ttu-id="08157-136">Create two frontend IP configurations:</span><span class="sxs-lookup"><span data-stu-id="08157-136">Create two frontend IP configurations:</span></span>

    ```powershell
    $frontendIP1 = New-AzureRmLoadBalancerFrontendIpConfig -Name contosofe -PublicIpAddress $publicIP1
    $frontendIP2 = New-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2
    ```

9. <span data-ttu-id="08157-137">Create your backend address pools, a probe, and your load balancing rules:</span><span class="sxs-lookup"><span data-stu-id="08157-137">Create your backend address pools, a probe, and your load balancing rules:</span></span>

    ```powershell
    $beaddresspool1 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name contosopool
    $beaddresspool2 = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool

    $healthProbe = New-AzureRmLoadBalancerProbeConfig -Name HTTP -RequestPath 'index.html' -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2

    $lbrule1 = New-AzureRmLoadBalancerRuleConfig -Name HTTPc -FrontendIpConfiguration $frontendIP1 -BackendAddressPool $beaddresspool1 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    $lbrule2 = New-AzureRmLoadBalancerRuleConfig -Name HTTPf -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthprobe -Protocol Tcp -FrontendPort 80 -BackendPort 80
    ```

10. <span data-ttu-id="08157-138">Once you have these resources created, create your load balancer:</span><span class="sxs-lookup"><span data-stu-id="08157-138">Once you have these resources created, create your load balancer:</span></span>

    ```powershell
    $mylb = New-AzureRmLoadBalancer -ResourceGroupName contosofabrikam -Name mylb -Location 'West Central US' -FrontendIpConfiguration $frontendIP1 -LoadBalancingRule $lbrule -BackendAddressPool $beAddressPool -Probe $healthProbe
    ```

11. <span data-ttu-id="08157-139">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span><span class="sxs-lookup"><span data-stu-id="08157-139">Add the second backend address pool and frontend IP configuration to your newly created load balancer:</span></span>

    ```powershell
    $mylb = Get-AzureRmLoadBalancer -Name "mylb" -ResourceGroupName $myResourceGroup | Add-AzureRmLoadBalancerBackendAddressPoolConfig -Name fabrikampool | Set-AzureRmLoadBalancer

    $mylb | Add-AzureRmLoadBalancerFrontendIpConfig -Name fabrikamfe -PublicIpAddress $publicIP2 | Set-AzureRmLoadBalancer
    
    Add-AzureRmLoadBalancerRuleConfig -Name HTTP -LoadBalancer $mylb -FrontendIpConfiguration $frontendIP2 -BackendAddressPool $beaddresspool2 -Probe $healthProbe -Protocol Tcp -FrontendPort 80 -BackendPort 80 | Set-AzureRmLoadBalancer
    ```

12. <span data-ttu-id="08157-140">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span><span class="sxs-lookup"><span data-stu-id="08157-140">The commands below get the NICs and then add both IP configurations of each secondary NIC to the backend address pool of the load balancer:</span></span>

    ```powershell
    $nic1 = Get-AzureRmNetworkInterface -Name "VM1-NIC2" -ResourceGroupName "MyResourcegroup";
    $nic2 = Get-AzureRmNetworkInterface -Name "VM2-NIC2" -ResourceGroupName "MyResourcegroup";

    $nic1.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic1.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);
    $nic2.IpConfigurations[0].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[0]);
    $nic2.IpConfigurations[1].LoadBalancerBackendAddressPools.Add($mylb.BackendAddressPools[1]);

    $mylb = $mylb | Set-AzureRmLoadBalancer

    $nic1 | Set-AzureRmNetworkInterface
    $nic2 | Set-AzureRmNetworkInterface
    ```

13. <span data-ttu-id="08157-141">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="08157-141">Finally, you must configure DNS resource records to point to the respective frontend IP address of the Load Balancer.</span></span> <span data-ttu-id="08157-142">You may host your domains in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="08157-142">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="08157-143">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="08157-143">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="08157-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="08157-144">Next steps</span></span>
- <span data-ttu-id="08157-145">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="08157-145">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="08157-146">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="08157-146">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>

