---
title: Create a public load balancer with IPv6 - Azure CLI | Microsoft Docs
description: Learn how to create a public load balancer with IPv6 using Azure CLI.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
tags: azure-resource-manager
keywords: ipv6, azure load balancer, dual stack, public ip, native ipv6, mobile, iot
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/25/2018
ms.author: kumud
ms.openlocfilehash: 39a3f1a400abae4a9a30c07b7352518b55d0daf1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773064"
---
# <a name="create-a-public-load-balancer-with-ipv6-using-azure-cli"></a><span data-ttu-id="56c86-104">Create a public load balancer with IPv6 using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56c86-104">Create a public load balancer with IPv6 using Azure CLI</span></span>


<span data-ttu-id="56c86-105">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span><span class="sxs-lookup"><span data-stu-id="56c86-105">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="56c86-106">Load balancers provide high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span><span class="sxs-lookup"><span data-stu-id="56c86-106">Load balancers provide high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="56c86-107">Load balancers can also present these services on multiple ports or multiple IP addresses or both.</span><span class="sxs-lookup"><span data-stu-id="56c86-107">Load balancers can also present these services on multiple ports or multiple IP addresses or both.</span></span>

## <a name="example-deployment-scenario"></a><span data-ttu-id="56c86-108">Example deployment scenario</span><span class="sxs-lookup"><span data-stu-id="56c86-108">Example deployment scenario</span></span>

<span data-ttu-id="56c86-109">The following diagram illustrates the load balancing solution that's deployed by using the example template described in this article.</span><span class="sxs-lookup"><span data-stu-id="56c86-109">The following diagram illustrates the load balancing solution that's deployed by using the example template described in this article.</span></span>

![Load balancer scenario](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

<span data-ttu-id="56c86-111">In this scenario, you create the following Azure resources:</span><span class="sxs-lookup"><span data-stu-id="56c86-111">In this scenario, you create the following Azure resources:</span></span>

* <span data-ttu-id="56c86-112">Two virtual machines (VMs)</span><span class="sxs-lookup"><span data-stu-id="56c86-112">Two virtual machines (VMs)</span></span>
* <span data-ttu-id="56c86-113">A virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span><span class="sxs-lookup"><span data-stu-id="56c86-113">A virtual network interface for each VM with both IPv4 and IPv6 addresses assigned</span></span>
* <span data-ttu-id="56c86-114">A public load balancer with an IPv4 and an IPv6 public IP address</span><span class="sxs-lookup"><span data-stu-id="56c86-114">A public load balancer with an IPv4 and an IPv6 public IP address</span></span>
* <span data-ttu-id="56c86-115">An availability set that contains the two VMs</span><span class="sxs-lookup"><span data-stu-id="56c86-115">An availability set that contains the two VMs</span></span>
* <span data-ttu-id="56c86-116">Two load balancing rules to map the public VIPs to the private endpoints</span><span class="sxs-lookup"><span data-stu-id="56c86-116">Two load balancing rules to map the public VIPs to the private endpoints</span></span>

## <a name="deploy-the-solution-by-using-azure-cli"></a><span data-ttu-id="56c86-117">Deploy the solution by using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56c86-117">Deploy the solution by using Azure CLI</span></span>

<span data-ttu-id="56c86-118">The following steps show how to create a public load balancer by using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="56c86-118">The following steps show how to create a public load balancer by using Azure CLI.</span></span> <span data-ttu-id="56c86-119">Using CLI, you create and configure each object individually, and then put them together to create a resource.</span><span class="sxs-lookup"><span data-stu-id="56c86-119">Using CLI, you create and configure each object individually, and then put them together to create a resource.</span></span>

<span data-ttu-id="56c86-120">To deploy a load balancer, create and configure the following objects:</span><span class="sxs-lookup"><span data-stu-id="56c86-120">To deploy a load balancer, create and configure the following objects:</span></span>

* <span data-ttu-id="56c86-121">**Front-end IP configuration**: Contains public IP addresses for incoming network traffic.</span><span class="sxs-lookup"><span data-stu-id="56c86-121">**Front-end IP configuration**: Contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="56c86-122">**Back-end address pool**: Contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="56c86-122">**Back-end address pool**: Contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="56c86-123">**Load balancing rules**: Contains rules that map a public port on the load balancer to a port in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="56c86-123">**Load balancing rules**: Contains rules that map a public port on the load balancer to a port in the back-end address pool.</span></span>
* <span data-ttu-id="56c86-124">**Inbound NAT rules**: Contains network address translation (NAT) rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="56c86-124">**Inbound NAT rules**: Contains network address translation (NAT) rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="56c86-125">**Probes**: Contains health probes that are used to check the availability of virtual machine instances in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="56c86-125">**Probes**: Contains health probes that are used to check the availability of virtual machine instances in the back-end address pool.</span></span>

## <a name="set-up-azure-cli"></a><span data-ttu-id="56c86-126">Set up Azure CLI</span><span class="sxs-lookup"><span data-stu-id="56c86-126">Set up Azure CLI</span></span>

<span data-ttu-id="56c86-127">In this example, you run the Azure CLI tools in a PowerShell command window.</span><span class="sxs-lookup"><span data-stu-id="56c86-127">In this example, you run the Azure CLI tools in a PowerShell command window.</span></span> <span data-ttu-id="56c86-128">To improve readability and reuse, you use PowerShell's scripting capabilities, not the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="56c86-128">To improve readability and reuse, you use PowerShell's scripting capabilities, not the Azure PowerShell cmdlets.</span></span>

1. <span data-ttu-id="56c86-129">[Install and Configure the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) by following the steps in the linked article and sign in to your Azure account.</span><span class="sxs-lookup"><span data-stu-id="56c86-129">[Install and Configure the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) by following the steps in the linked article and sign in to your Azure account.</span></span>

2. <span data-ttu-id="56c86-130">Set up PowerShell variables for use with the Azure CLI commands:</span><span class="sxs-lookup"><span data-stu-id="56c86-130">Set up PowerShell variables for use with the Azure CLI commands:</span></span>

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a><span data-ttu-id="56c86-131">Create a resource group, a load balancer, a virtual network, and subnets</span><span class="sxs-lookup"><span data-stu-id="56c86-131">Create a resource group, a load balancer, a virtual network, and subnets</span></span>

1. <span data-ttu-id="56c86-132">Create a resource group:</span><span class="sxs-lookup"><span data-stu-id="56c86-132">Create a resource group:</span></span>

    ```azurecli
    az group create --name $rgName --location $location
    ```

2. <span data-ttu-id="56c86-133">Create a load balancer:</span><span class="sxs-lookup"><span data-stu-id="56c86-133">Create a load balancer:</span></span>

    ```azurecli
    $lb = az network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. <span data-ttu-id="56c86-134">Create a virtual network:</span><span class="sxs-lookup"><span data-stu-id="56c86-134">Create a virtual network:</span></span>

    ```azurecli
    $vnet = az network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

4. <span data-ttu-id="56c86-135">In this virtual network, create two subnets:</span><span class="sxs-lookup"><span data-stu-id="56c86-135">In this virtual network, create two subnets:</span></span>

    ```azurecli
    $subnet1 = az network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = az network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a><span data-ttu-id="56c86-136">Create public IP addresses for the front-end pool</span><span class="sxs-lookup"><span data-stu-id="56c86-136">Create public IP addresses for the front-end pool</span></span>

1. <span data-ttu-id="56c86-137">Set up the PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="56c86-137">Set up the PowerShell variables:</span></span>

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. <span data-ttu-id="56c86-138">Create a public IP address for the front-end IP pool:</span><span class="sxs-lookup"><span data-stu-id="56c86-138">Create a public IP address for the front-end IP pool:</span></span>

    ```azurecli
    $publicipV4 = az network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --version IPv4 --allocation-method Dynamic --dns-name $dnsLabel
    $publicipV6 = az network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --version IPv6 --allocation-method Dynamic --dns-name $dnsLabel
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="56c86-139">The load balancer uses the domain label of the public IP as its fully qualified domain name (FQDN).</span><span class="sxs-lookup"><span data-stu-id="56c86-139">The load balancer uses the domain label of the public IP as its fully qualified domain name (FQDN).</span></span> <span data-ttu-id="56c86-140">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span><span class="sxs-lookup"><span data-stu-id="56c86-140">This a change from classic deployment, which uses the cloud service name as the load balancer FQDN.</span></span>
    >
    > <span data-ttu-id="56c86-141">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="56c86-141">In this example, the FQDN is *contoso09152016.southcentralus.cloudapp.azure.com*.</span></span>

## <a name="create-front-end-and-back-end-pools"></a><span data-ttu-id="56c86-142">Create front-end and back-end pools</span><span class="sxs-lookup"><span data-stu-id="56c86-142">Create front-end and back-end pools</span></span>

<span data-ttu-id="56c86-143">In this section, you create the following IP pools:</span><span class="sxs-lookup"><span data-stu-id="56c86-143">In this section, you create the following IP pools:</span></span>
* <span data-ttu-id="56c86-144">The front-end IP pool that receives the incoming network traffic on the load balancer.</span><span class="sxs-lookup"><span data-stu-id="56c86-144">The front-end IP pool that receives the incoming network traffic on the load balancer.</span></span>
* <span data-ttu-id="56c86-145">The back-end IP pool where the front-end pool sends the load-balanced network traffic.</span><span class="sxs-lookup"><span data-stu-id="56c86-145">The back-end IP pool where the front-end pool sends the load-balanced network traffic.</span></span>

1. <span data-ttu-id="56c86-146">Set up the PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="56c86-146">Set up the PowerShell variables:</span></span>

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. <span data-ttu-id="56c86-147">Create a front-end IP pool, and associate it with the public IP that you created in the previous step and the load balancer.</span><span class="sxs-lookup"><span data-stu-id="56c86-147">Create a front-end IP pool, and associate it with the public IP that you created in the previous step and the load balancer.</span></span>

    ```azurecli
    $frontendV4 = az network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-address $publicIpv4Name --lb-name $lbName
    $frontendV6 = az network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-address $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = az network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = az network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-load-balancer-rules"></a><span data-ttu-id="56c86-148">Create the probe, NAT rules, and load balancer rules</span><span class="sxs-lookup"><span data-stu-id="56c86-148">Create the probe, NAT rules, and load balancer rules</span></span>

<span data-ttu-id="56c86-149">This example creates the following items:</span><span class="sxs-lookup"><span data-stu-id="56c86-149">This example creates the following items:</span></span>

* <span data-ttu-id="56c86-150">A probe rule to check for connectivity to TCP port 80.</span><span class="sxs-lookup"><span data-stu-id="56c86-150">A probe rule to check for connectivity to TCP port 80.</span></span>
* <span data-ttu-id="56c86-151">A NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP.\*</span><span class="sxs-lookup"><span data-stu-id="56c86-151">A NAT rule to translate all incoming traffic on port 3389 to port 3389 for RDP.\*</span></span>
* <span data-ttu-id="56c86-152">A NAT rule to translate all incoming traffic on port 3391 to port 3389 for remote desktop protocol (RDP).\*</span><span class="sxs-lookup"><span data-stu-id="56c86-152">A NAT rule to translate all incoming traffic on port 3391 to port 3389 for remote desktop protocol (RDP).\*</span></span>
* <span data-ttu-id="56c86-153">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="56c86-153">A load balancer rule to balance all incoming traffic on port 80 to port 80 on the addresses in the back-end pool.</span></span>

<span data-ttu-id="56c86-154">\* NAT rules are associated with a specific virtual-machine instance behind the load balancer.</span><span class="sxs-lookup"><span data-stu-id="56c86-154">\* NAT rules are associated with a specific virtual-machine instance behind the load balancer.</span></span> <span data-ttu-id="56c86-155">The network traffic that arrives on port 3389 is sent to the specific virtual machine and port that's associated with the NAT rule.</span><span class="sxs-lookup"><span data-stu-id="56c86-155">The network traffic that arrives on port 3389 is sent to the specific virtual machine and port that's associated with the NAT rule.</span></span> <span data-ttu-id="56c86-156">You must specify a protocol (UDP or TCP) for a NAT rule.</span><span class="sxs-lookup"><span data-stu-id="56c86-156">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="56c86-157">You cannot assign both protocols to the same port.</span><span class="sxs-lookup"><span data-stu-id="56c86-157">You cannot assign both protocols to the same port.</span></span>

1. <span data-ttu-id="56c86-158">Set up the PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="56c86-158">Set up the PowerShell variables:</span></span>

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. <span data-ttu-id="56c86-159">Create the probe.</span><span class="sxs-lookup"><span data-stu-id="56c86-159">Create the probe.</span></span>

    <span data-ttu-id="56c86-160">The following example creates a TCP probe that checks for connectivity to the back-end TCP port 80 every 15 seconds.</span><span class="sxs-lookup"><span data-stu-id="56c86-160">The following example creates a TCP probe that checks for connectivity to the back-end TCP port 80 every 15 seconds.</span></span> <span data-ttu-id="56c86-161">After two consecutive failures, it marks the back-end resource as unavailable.</span><span class="sxs-lookup"><span data-stu-id="56c86-161">After two consecutive failures, it marks the back-end resource as unavailable.</span></span>

    ```azurecli
    $probeV4V6 = az network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --threshold 2 --lb-name $lbName
    ```

3. <span data-ttu-id="56c86-162">Create inbound NAT rules that allow RDP connections to the back-end resources:</span><span class="sxs-lookup"><span data-stu-id="56c86-162">Create inbound NAT rules that allow RDP connections to the back-end resources:</span></span>

    ```azurecli
    $inboundNatRuleRdp1 = az network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = az network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. <span data-ttu-id="56c86-163">Create load balancer rules that send traffic to different back-end ports, depending on the front end that received the request.</span><span class="sxs-lookup"><span data-stu-id="56c86-163">Create load balancer rules that send traffic to different back-end ports, depending on the front end that received the request.</span></span>

    ```azurecli
    $lbruleIPv4 = az network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = az network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. <span data-ttu-id="56c86-164">Check your settings:</span><span class="sxs-lookup"><span data-stu-id="56c86-164">Check your settings:</span></span>

    ```azurecli
    az network lb show --resource-group $rgName --name $lbName
    ```

    <span data-ttu-id="56c86-165">Expected output:</span><span class="sxs-lookup"><span data-stu-id="56c86-165">Expected output:</span></span>

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a><span data-ttu-id="56c86-166">Create NICs</span><span class="sxs-lookup"><span data-stu-id="56c86-166">Create NICs</span></span>

<span data-ttu-id="56c86-167">Create NICs and associate them with NAT rules, load balancer rules, and probes.</span><span class="sxs-lookup"><span data-stu-id="56c86-167">Create NICs and associate them with NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="56c86-168">Set up the PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="56c86-168">Set up the PowerShell variables:</span></span>

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. <span data-ttu-id="56c86-169">Create a NIC for each back end, and add an IPv6 configuration:</span><span class="sxs-lookup"><span data-stu-id="56c86-169">Create a NIC for each back end, and add an IPv6 configuration:</span></span>

    ```azurecli
    $nic1 = az network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-address-version "IPv4" --subnet $subnet1Id --lb-address-pools $backendAddressPoolV4Id --lb-inbound-nat-rules $natRule1V4Id
    $nic1IPv6 = az network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-address-version "IPv6" --lb-address-pools $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = az network nic create --name $nic2Name --resource-group $rgname --location $location --private-ip-address-version "IPv4" --subnet $subnet2Id --lb-address-pools $backendAddressPoolV4Id --lb-inbound-nat-rules $natRule2V4Id
    $nic2IPv6 = az network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-address-version "IPv6" --lb-address-pools $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a><span data-ttu-id="56c86-170">Create the back-end VM resources, and attach each NIC</span><span class="sxs-lookup"><span data-stu-id="56c86-170">Create the back-end VM resources, and attach each NIC</span></span>

<span data-ttu-id="56c86-171">To create VMs, you must have a storage account.</span><span class="sxs-lookup"><span data-stu-id="56c86-171">To create VMs, you must have a storage account.</span></span> <span data-ttu-id="56c86-172">For load balancing, the VMs need to be members of an availability set.</span><span class="sxs-lookup"><span data-stu-id="56c86-172">For load balancing, the VMs need to be members of an availability set.</span></span> <span data-ttu-id="56c86-173">For more information about creating VMs, see [Create an Azure VM by using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="56c86-173">For more information about creating VMs, see [Create an Azure VM by using PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).</span></span>

1. <span data-ttu-id="56c86-174">Set up the PowerShell variables:</span><span class="sxs-lookup"><span data-stu-id="56c86-174">Set up the PowerShell variables:</span></span>

    ```powershell
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $imageurn = "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > <span data-ttu-id="56c86-175">This example uses the username and password for the VMs in cleartext.</span><span class="sxs-lookup"><span data-stu-id="56c86-175">This example uses the username and password for the VMs in cleartext.</span></span> <span data-ttu-id="56c86-176">Take appropriate care when you use these credentials in cleartext.</span><span class="sxs-lookup"><span data-stu-id="56c86-176">Take appropriate care when you use these credentials in cleartext.</span></span> <span data-ttu-id="56c86-177">For a more secure method of handling credentials in PowerShell, see the [`Get-Credential`](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="56c86-177">For a more secure method of handling credentials in PowerShell, see the [`Get-Credential`](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

2. <span data-ttu-id="56c86-178">Create the availability set:</span><span class="sxs-lookup"><span data-stu-id="56c86-178">Create the availability set:</span></span>

    ```azurecli
    $availabilitySet = az vm availability-set create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. <span data-ttu-id="56c86-179">Create the virtual machines with the associated NICs:</span><span class="sxs-lookup"><span data-stu-id="56c86-179">Create the virtual machines with the associated NICs:</span></span>

    ```azurecli
    az vm create --resource-group $rgname --name $vm1Name --image $imageurn --admin-username $vmUserName --admin-password $mySecurePassword --nics $nic1Id --location $location --availability-set $availabilitySetName --size "Standard_A1" 

    az vm create --resource-group $rgname --name $vm2Name --image $imageurn --admin-username $vmUserName --admin-password $mySecurePassword --nics $nic2Id --location $location --availability-set $availabilitySetName --size "Standard_A1" 
    ```

## <a name="next-steps"></a><span data-ttu-id="56c86-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="56c86-180">Next steps</span></span>

[<span data-ttu-id="56c86-181">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="56c86-181">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)  
[<span data-ttu-id="56c86-182">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="56c86-182">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)  
[<span data-ttu-id="56c86-183">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="56c86-183">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
