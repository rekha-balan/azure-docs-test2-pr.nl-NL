---
title: Tutorial:Configure port forwarding in Load Balancer - Azure portal | Microsoft Docs
description: This tutorial shows how to configure port forwarding using Azure Load Balancer to create connection to VMs in an Azure virtual network.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: As an IT administrator, I want to configure port forwarding in Azure Load Balancer to remotely connect to VMs in an Azure virtual network.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/31/18
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: eac0636af1b46912897a4c93f86477c46299bc0f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865302"
---
# <a name="tutorial-configure-port-fowarding-in-load-balancer-using-the-azure-portal"></a><span data-ttu-id="35cee-103">Tutorial: Configure port fowarding in Load Balancer using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="35cee-103">Tutorial: Configure port fowarding in Load Balancer using the Azure portal</span></span>

<span data-ttu-id="35cee-104">Port forwarding using Azure Load Balancer enables you to remotely connect to VMs in the Azure virtual network using the Load Balancer's public IP address through port number.</span><span class="sxs-lookup"><span data-stu-id="35cee-104">Port forwarding using Azure Load Balancer enables you to remotely connect to VMs in the Azure virtual network using the Load Balancer's public IP address through port number.</span></span> <span data-ttu-id="35cee-105">In this tutorial, you learn to configure port forwarding in Azure Load Balancer and learn how to:</span><span class="sxs-lookup"><span data-stu-id="35cee-105">In this tutorial, you learn to configure port forwarding in Azure Load Balancer and learn how to:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="35cee-106">Create an Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="35cee-106">Create an Azure load balancer</span></span>
> * <span data-ttu-id="35cee-107">Create a load balancer health probe</span><span class="sxs-lookup"><span data-stu-id="35cee-107">Create a load balancer health probe</span></span>
> * <span data-ttu-id="35cee-108">Create load balancer traffic rules</span><span class="sxs-lookup"><span data-stu-id="35cee-108">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="35cee-109">Create virtual machines and install IIS server</span><span class="sxs-lookup"><span data-stu-id="35cee-109">Create virtual machines and install IIS server</span></span>
> * <span data-ttu-id="35cee-110">Attach virtual machines to a load balancer</span><span class="sxs-lookup"><span data-stu-id="35cee-110">Attach virtual machines to a load balancer</span></span>
> * <span data-ttu-id="35cee-111">Create load balancer inbound NAT rules</span><span class="sxs-lookup"><span data-stu-id="35cee-111">Create load balancer inbound NAT rules</span></span>
> * <span data-ttu-id="35cee-112">View port forwarding in action</span><span class="sxs-lookup"><span data-stu-id="35cee-112">View port forwarding in action</span></span>


<span data-ttu-id="35cee-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="35cee-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="log-in-to-azure"></a><span data-ttu-id="35cee-114">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="35cee-114">Log in to Azure</span></span>

<span data-ttu-id="35cee-115">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="35cee-115">Log in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

## <a name="create-a-standard-load-balancer"></a><span data-ttu-id="35cee-116">Create a Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="35cee-116">Create a Standard Load Balancer</span></span>

<span data-ttu-id="35cee-117">In this section, you create a public load balancer that helps load balance virtual machines.</span><span class="sxs-lookup"><span data-stu-id="35cee-117">In this section, you create a public load balancer that helps load balance virtual machines.</span></span> <span data-ttu-id="35cee-118">Standard Load Balancer only supports a Standard Public IP address.</span><span class="sxs-lookup"><span data-stu-id="35cee-118">Standard Load Balancer only supports a Standard Public IP address.</span></span> <span data-ttu-id="35cee-119">When you create a Standard Load Balancer, you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-119">When you create a Standard Load Balancer, you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span></span> 

1. <span data-ttu-id="35cee-120">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="35cee-120">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="35cee-121">In the **Create a load balancer** page enter these values for the load balancer:</span><span class="sxs-lookup"><span data-stu-id="35cee-121">In the **Create a load balancer** page enter these values for the load balancer:</span></span>
    - <span data-ttu-id="35cee-122">*myLoadBalancer* - for the name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-122">*myLoadBalancer* - for the name of the load balancer.</span></span>
    - <span data-ttu-id="35cee-123">**Standard** - for the SKU version of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-123">**Standard** - for the SKU version of the load balancer.</span></span>
    - <span data-ttu-id="35cee-124">**Public** - for the type of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-124">**Public** - for the type of the load balancer.</span></span>
    - <span data-ttu-id="35cee-125">*myPublicIP* - for the **New** Public IP that you create.</span><span class="sxs-lookup"><span data-stu-id="35cee-125">*myPublicIP* - for the **New** Public IP that you create.</span></span>
    - <span data-ttu-id="35cee-126">*myResourceGroupSLB* -  for the name of the **New** resource group that you select to create.</span><span class="sxs-lookup"><span data-stu-id="35cee-126">*myResourceGroupSLB* -  for the name of the **New** resource group that you select to create.</span></span>
    - <span data-ttu-id="35cee-127">**westeurope** - for the location.</span><span class="sxs-lookup"><span data-stu-id="35cee-127">**westeurope** - for the location.</span></span>
3. <span data-ttu-id="35cee-128">Click **Create** to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-128">Click **Create** to create the load balancer.</span></span>

![Create a load balancer](./media/load-balancer-standard-public-portal/1a-load-balancer.png)
   
## <a name="create-load-balancer-resources"></a><span data-ttu-id="35cee-130">Create load balancer resources</span><span class="sxs-lookup"><span data-stu-id="35cee-130">Create load balancer resources</span></span>

<span data-ttu-id="35cee-131">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify load balancer rules.</span><span class="sxs-lookup"><span data-stu-id="35cee-131">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify load balancer rules.</span></span>

### <a name="create-a-backend-address-pool"></a><span data-ttu-id="35cee-132">Create a backend address pool</span><span class="sxs-lookup"><span data-stu-id="35cee-132">Create a backend address pool</span></span>

<span data-ttu-id="35cee-133">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-133">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span> <span data-ttu-id="35cee-134">Create the backend address pool *myBackendPool* to inlcude *VM1* and *VM2*.</span><span class="sxs-lookup"><span data-stu-id="35cee-134">Create the backend address pool *myBackendPool* to inlcude *VM1* and *VM2*.</span></span>

1. <span data-ttu-id="35cee-135">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="35cee-135">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="35cee-136">Under **Settings**, click **Backend pools**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35cee-136">Under **Settings**, click **Backend pools**, then click **Add**.</span></span>
3. <span data-ttu-id="35cee-137">On the **Add a backend pool** page, for name, type *myBackEndPool*, as the name for your backend pool, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-137">On the **Add a backend pool** page, for name, type *myBackEndPool*, as the name for your backend pool, and then click **OK**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="35cee-138">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="35cee-138">Create a health probe</span></span>

<span data-ttu-id="35cee-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="35cee-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="35cee-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="35cee-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="35cee-141">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="35cee-141">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="35cee-142">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="35cee-142">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="35cee-143">Under **Settings**, click **Health probes**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35cee-143">Under **Settings**, click **Health probes**, then click **Add**.</span></span>
3. <span data-ttu-id="35cee-144">Use these values to create the health probe:</span><span class="sxs-lookup"><span data-stu-id="35cee-144">Use these values to create the health probe:</span></span>
    - <span data-ttu-id="35cee-145">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="35cee-145">*myHealthProbe* - for the name of the health probe.</span></span>
    - <span data-ttu-id="35cee-146">**HTTP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="35cee-146">**HTTP** - for the protocol type.</span></span>
    - <span data-ttu-id="35cee-147">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="35cee-147">*80* - for the port number.</span></span>
    - <span data-ttu-id="35cee-148">*15* - for number of **Interval** in seconds between probe attempts.</span><span class="sxs-lookup"><span data-stu-id="35cee-148">*15* - for number of **Interval** in seconds between probe attempts.</span></span>
    - <span data-ttu-id="35cee-149">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="35cee-149">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span></span>
4. <span data-ttu-id="35cee-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-150">Click **OK**.</span></span>

   ![Adding a probe](./media/load-balancer-standard-public-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="35cee-152">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="35cee-152">Create a load balancer rule</span></span>

<span data-ttu-id="35cee-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="35cee-153">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="35cee-154">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="35cee-154">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="35cee-155">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="35cee-155">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

1. <span data-ttu-id="35cee-156">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="35cee-156">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="35cee-157">Under **Settings**, click **Load balancing rules**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35cee-157">Under **Settings**, click **Load balancing rules**, then click **Add**.</span></span>
3. <span data-ttu-id="35cee-158">Use these values to configure the load balancing rule:</span><span class="sxs-lookup"><span data-stu-id="35cee-158">Use these values to configure the load balancing rule:</span></span>
    - <span data-ttu-id="35cee-159">*myHTTPRule* - for the name of the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="35cee-159">*myHTTPRule* - for the name of the load balancing rule.</span></span>
    - <span data-ttu-id="35cee-160">**TCP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="35cee-160">**TCP** - for the protocol type.</span></span>
    - <span data-ttu-id="35cee-161">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="35cee-161">*80* - for the port number.</span></span>
    - <span data-ttu-id="35cee-162">*80* - for the backend port.</span><span class="sxs-lookup"><span data-stu-id="35cee-162">*80* - for the backend port.</span></span>
    - <span data-ttu-id="35cee-163">*myBackendPool* - for the name of the backend pool.</span><span class="sxs-lookup"><span data-stu-id="35cee-163">*myBackendPool* - for the name of the backend pool.</span></span>
    - <span data-ttu-id="35cee-164">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="35cee-164">*myHealthProbe* - for the name of the health probe.</span></span>
4. <span data-ttu-id="35cee-165">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-165">Click **OK**.</span></span>
    
## <a name="create-backend-servers"></a><span data-ttu-id="35cee-166">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="35cee-166">Create backend servers</span></span>

<span data-ttu-id="35cee-167">In this section, you create a virtual network, create two virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test port forwarding using the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-167">In this section, you create a virtual network, create two virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test port forwarding using the load balancer.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="35cee-168">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="35cee-168">Create a virtual network</span></span>
1. <span data-ttu-id="35cee-169">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="35cee-169">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span></span>
    - <span data-ttu-id="35cee-170">*myVnet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="35cee-170">*myVnet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="35cee-171">*myResourceGroupSLB* - for the name of the existing resource group</span><span class="sxs-lookup"><span data-stu-id="35cee-171">*myResourceGroupSLB* - for the name of the existing resource group</span></span>
    - <span data-ttu-id="35cee-172">*myBackendSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="35cee-172">*myBackendSubnet* - for the subnet name.</span></span>
2. <span data-ttu-id="35cee-173">Click **Create** to create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="35cee-173">Click **Create** to create the virtual network.</span></span>

    ![Create a virtual network](./media/load-balancer-standard-public-portal/2-load-balancer-virtual-network.png)

### <a name="create-virtual-machines"></a><span data-ttu-id="35cee-175">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="35cee-175">Create virtual machines</span></span>

1. <span data-ttu-id="35cee-176">On the top left-hand side of the screen, click **New** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="35cee-176">On the top left-hand side of the screen, click **New** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    - <span data-ttu-id="35cee-177">*myVM1* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="35cee-177">*myVM1* - for the name of the virtual machine.</span></span>        
    - <span data-ttu-id="35cee-178">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="35cee-178">*azureuser* - for the administrator user name.</span></span>    
    - <span data-ttu-id="35cee-179">*myResourceGroupSLB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="35cee-179">*myResourceGroupSLB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span></span>
2. <span data-ttu-id="35cee-180">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-180">Click **OK**.</span></span>
3. <span data-ttu-id="35cee-181">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="35cee-181">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="35cee-182">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="35cee-182">Enter these values for the VM settings:</span></span>
    -  <span data-ttu-id="35cee-183">*myVNet* - ensure it is selected as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="35cee-183">*myVNet* - ensure it is selected as the virtual network.</span></span>
    - <span data-ttu-id="35cee-184">*myBackendSubnet* - ensure it is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="35cee-184">*myBackendSubnet* - ensure it is selected as the subnet.</span></span>
    - <span data-ttu-id="35cee-185">*myNetworkSecurityGroup* - for the name of the new network security group (firewall) that you must create.</span><span class="sxs-lookup"><span data-stu-id="35cee-185">*myNetworkSecurityGroup* - for the name of the new network security group (firewall) that you must create.</span></span>
5. <span data-ttu-id="35cee-186">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="35cee-186">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="35cee-187">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="35cee-187">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>
7. <span data-ttu-id="35cee-188">Create another VM, named, *VM2* with *myVnet* as its virtual network, *myBackendSubnet* and its subnet, and \**myNetworkSecurityGroup* as its network security group using steps 1-6.</span><span class="sxs-lookup"><span data-stu-id="35cee-188">Create another VM, named, *VM2* with *myVnet* as its virtual network, *myBackendSubnet* and its subnet, and \**myNetworkSecurityGroup* as its network security group using steps 1-6.</span></span> 

### <a name="create-nsg-rules"></a><span data-ttu-id="35cee-189">Create NSG rules</span><span class="sxs-lookup"><span data-stu-id="35cee-189">Create NSG rules</span></span>

<span data-ttu-id="35cee-190">In this section, you create NSG rules to allow inbound connections using HTTP and RDP.</span><span class="sxs-lookup"><span data-stu-id="35cee-190">In this section, you create NSG rules to allow inbound connections using HTTP and RDP.</span></span>

1. <span data-ttu-id="35cee-191">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span><span class="sxs-lookup"><span data-stu-id="35cee-191">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span></span>
2. <span data-ttu-id="35cee-192">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="35cee-192">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span></span>
3. <span data-ttu-id="35cee-193">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span><span class="sxs-lookup"><span data-stu-id="35cee-193">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span></span>
    - <span data-ttu-id="35cee-194">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="35cee-194">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="35cee-195">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="35cee-195">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="35cee-196">*80* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="35cee-196">*80* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="35cee-197">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="35cee-197">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="35cee-198">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="35cee-198">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="35cee-199">*100* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="35cee-199">*100* for **Priority**</span></span>
    - <span data-ttu-id="35cee-200">*myHTTPRule* for name</span><span class="sxs-lookup"><span data-stu-id="35cee-200">*myHTTPRule* for name</span></span>
    - <span data-ttu-id="35cee-201">*Allow HTTP* - for description</span><span class="sxs-lookup"><span data-stu-id="35cee-201">*Allow HTTP* - for description</span></span>
4. <span data-ttu-id="35cee-202">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-202">Click **OK**.</span></span>
 
 ![Create a virtual network](./media/load-balancer-standard-public-portal/8-load-balancer-nsg-rules.png)
5. <span data-ttu-id="35cee-204">Repeat steps 2 to 4 to create another rule named *myRDPRule* to allow for an inbound RDP connection using port 3389 with the following values:</span><span class="sxs-lookup"><span data-stu-id="35cee-204">Repeat steps 2 to 4 to create another rule named *myRDPRule* to allow for an inbound RDP connection using port 3389 with the following values:</span></span>
    - <span data-ttu-id="35cee-205">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="35cee-205">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="35cee-206">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="35cee-206">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="35cee-207">*3389* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="35cee-207">*3389* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="35cee-208">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="35cee-208">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="35cee-209">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="35cee-209">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="35cee-210">*200* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="35cee-210">*200* for **Priority**</span></span>
    - <span data-ttu-id="35cee-211">*myRDPRule* for name</span><span class="sxs-lookup"><span data-stu-id="35cee-211">*myRDPRule* for name</span></span>
    - <span data-ttu-id="35cee-212">*Allow RDP* - for description</span><span class="sxs-lookup"><span data-stu-id="35cee-212">*Allow RDP* - for description</span></span>

### <a name="install-iis-on-vms"></a><span data-ttu-id="35cee-213">Install IIS on VMs</span><span class="sxs-lookup"><span data-stu-id="35cee-213">Install IIS on VMs</span></span>

1. <span data-ttu-id="35cee-214">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupSLB* resource group.</span><span class="sxs-lookup"><span data-stu-id="35cee-214">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupSLB* resource group.</span></span>
2. <span data-ttu-id="35cee-215">On the **Overview** page, click **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="35cee-215">On the **Overview** page, click **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="35cee-216">Log into the VM with username *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="35cee-216">Log into the VM with username *azureuser*.</span></span>
4. <span data-ttu-id="35cee-217">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="35cee-217">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span></span>
5. <span data-ttu-id="35cee-218">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span><span class="sxs-lookup"><span data-stu-id="35cee-218">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span></span>

   ```azurepowershell-interactive
    
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add a new htm file that displays server name
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from" + $env:computername)
   ```
6. <span data-ttu-id="35cee-219">Close the RDP session with *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="35cee-219">Close the RDP session with *myVM1*.</span></span>
7. <span data-ttu-id="35cee-220">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="35cee-220">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2*.</span></span>

## <a name="add-vms-to-the-backend-address-pool"></a><span data-ttu-id="35cee-221">Add VMs to the backend address pool</span><span class="sxs-lookup"><span data-stu-id="35cee-221">Add VMs to the backend address pool</span></span>

<span data-ttu-id="35cee-222">To distribute traffic to the VMs, add virtual machines *VM1* and *VM2* to the previously created backend address pool *myBackendPool*.</span><span class="sxs-lookup"><span data-stu-id="35cee-222">To distribute traffic to the VMs, add virtual machines *VM1* and *VM2* to the previously created backend address pool *myBackendPool*.</span></span> <span data-ttu-id="35cee-223">The backend pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-223">The backend pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

1. <span data-ttu-id="35cee-224">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="35cee-224">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="35cee-225">Under **Settings**, click **Backend pools**, then within the backend pool's list, click **myBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="35cee-225">Under **Settings**, click **Backend pools**, then within the backend pool's list, click **myBackendPool**.</span></span>
3. <span data-ttu-id="35cee-226">On the **myBackendPool** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="35cee-226">On the **myBackendPool** page, do the following:</span></span>
    - <span data-ttu-id="35cee-227">Click **Add a target network IP configuration** to add each virtual machine (*myVM1* and *myVM2*) that you created to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="35cee-227">Click **Add a target network IP configuration** to add each virtual machine (*myVM1* and *myVM2*) that you created to the backend pool.</span></span>
    - <span data-ttu-id="35cee-228">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-228">Click **OK**.</span></span>
4. <span data-ttu-id="35cee-229">Check to make sure your load balancer backend pool setting displays all the VMs **VM1** and **VM2**.</span><span class="sxs-lookup"><span data-stu-id="35cee-229">Check to make sure your load balancer backend pool setting displays all the VMs **VM1** and **VM2**.</span></span>

## <a name="create-inbound-nat-rules"></a><span data-ttu-id="35cee-230">Create inbound NAT rules</span><span class="sxs-lookup"><span data-stu-id="35cee-230">Create inbound NAT rules</span></span>
<span data-ttu-id="35cee-231">With Load Balancer, you can create an inbound NAT rule to port forward traffic from a specific port of a frontend IP address to a specific port of a backend instance inside the virtual network.</span><span class="sxs-lookup"><span data-stu-id="35cee-231">With Load Balancer, you can create an inbound NAT rule to port forward traffic from a specific port of a frontend IP address to a specific port of a backend instance inside the virtual network.</span></span>

<span data-ttu-id="35cee-232">Create inbound NAT rule to port forward traffic from load balancer's frontend ports to port 3389 for the backend VMs.</span><span class="sxs-lookup"><span data-stu-id="35cee-232">Create inbound NAT rule to port forward traffic from load balancer's frontend ports to port 3389 for the backend VMs.</span></span>

1. <span data-ttu-id="35cee-233">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="35cee-233">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="35cee-234">Under **Settings**, click **Inbound NAT rules**, then within the backend pool's list, click **myBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="35cee-234">Under **Settings**, click **Inbound NAT rules**, then within the backend pool's list, click **myBackendPool**.</span></span>
3. <span data-ttu-id="35cee-235">In the **Add inbound NAT rule** page, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="35cee-235">In the **Add inbound NAT rule** page, enter the following values:</span></span>
    - <span data-ttu-id="35cee-236">For the name of the NAT rule, type *myNATRuleRDPVM1*,</span><span class="sxs-lookup"><span data-stu-id="35cee-236">For the name of the NAT rule, type *myNATRuleRDPVM1*,</span></span>
    - <span data-ttu-id="35cee-237">For port, type *4221*.</span><span class="sxs-lookup"><span data-stu-id="35cee-237">For port, type *4221*.</span></span>
    - <span data-ttu-id="35cee-238">For **Target virtual machine**, from the drop-down, select *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="35cee-238">For **Target virtual machine**, from the drop-down, select *myVM1*.</span></span>
    - <span data-ttu-id="35cee-239">For **Port mapping**, click custom, anf then for **Target port**, type **3389**.</span><span class="sxs-lookup"><span data-stu-id="35cee-239">For **Port mapping**, click custom, anf then for **Target port**, type **3389**.</span></span>
    - <span data-ttu-id="35cee-240">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-240">Click **OK**.</span></span>
4. <span data-ttu-id="35cee-241">Repeat step 2 & 3 to create inbound NAT rules named *myNATRuleRDPVM2* for virutal machines *myVM2* using frontend port *4222*.</span><span class="sxs-lookup"><span data-stu-id="35cee-241">Repeat step 2 & 3 to create inbound NAT rules named *myNATRuleRDPVM2* for virutal machines *myVM2* using frontend port *4222*.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="35cee-242">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="35cee-242">Test the load balancer</span></span>
1. <span data-ttu-id="35cee-243">Find the public IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="35cee-243">Find the public IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="35cee-244">Click **All resources** and then click **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="35cee-244">Click **All resources** and then click **myPublicIP**.</span></span>

2. <span data-ttu-id="35cee-245">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="35cee-245">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="35cee-246">The default page of IIS Web server is displayed on the browser.</span><span class="sxs-lookup"><span data-stu-id="35cee-246">The default page of IIS Web server is displayed on the browser.</span></span>

      ![IIS Web server](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

<span data-ttu-id="35cee-248">To see the load balancer distribute traffic across the three VMs running your app, you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="35cee-248">To see the load balancer distribute traffic across the three VMs running your app, you can force-refresh your web browser.</span></span>

## <a name="test-port-forwarding"></a><span data-ttu-id="35cee-249">Test port forwarding</span><span class="sxs-lookup"><span data-stu-id="35cee-249">Test port forwarding</span></span>
<span data-ttu-id="35cee-250">With port forwarding, you can create a remote desktop connection to the VMs in the backend address pool using the IP address of the load balancer and the frontend port value that were defined in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="35cee-250">With port forwarding, you can create a remote desktop connection to the VMs in the backend address pool using the IP address of the load balancer and the frontend port value that were defined in the preceding step.</span></span>

1. <span data-ttu-id="35cee-251">Find the public IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="35cee-251">Find the public IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="35cee-252">Click **All resources** and then click **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="35cee-252">Click **All resources** and then click **myPublicIP**.</span></span>
2. <span data-ttu-id="35cee-253">Use the following command to create a remote desktop session with the *myVM2* VM from your local computer.</span><span class="sxs-lookup"><span data-stu-id="35cee-253">Use the following command to create a remote desktop session with the *myVM2* VM from your local computer.</span></span> <span data-ttu-id="35cee-254">Replace `<publicIpAddress>` with the IP address returned from the previous step.</span><span class="sxs-lookup"><span data-stu-id="35cee-254">Replace `<publicIpAddress>` with the IP address returned from the previous step.</span></span>

    ```
    mstsc /v:<publicIpAddress>:4222
    ```
  
3. <span data-ttu-id="35cee-255">Open the downloaded RDP file.</span><span class="sxs-lookup"><span data-stu-id="35cee-255">Open the downloaded RDP file.</span></span> <span data-ttu-id="35cee-256">If prompted, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="35cee-256">If prompted, select **Connect**.</span></span>

4. <span data-ttu-id="35cee-257">Enter the user name and password you specified when creating the VM (you may need to select **More choices**, then **Use a different account**, to specify the credentials you entered when you created the VM), then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="35cee-257">Enter the user name and password you specified when creating the VM (you may need to select **More choices**, then **Use a different account**, to specify the credentials you entered when you created the VM), then select **OK**.</span></span> <span data-ttu-id="35cee-258">You may receive a certificate warning during the sign-in process.</span><span class="sxs-lookup"><span data-stu-id="35cee-258">You may receive a certificate warning during the sign-in process.</span></span> <span data-ttu-id="35cee-259">Select **Yes** to proceed with the connection.</span><span class="sxs-lookup"><span data-stu-id="35cee-259">Select **Yes** to proceed with the connection.</span></span>
 
   <span data-ttu-id="35cee-260">The RDP connection succeeds, as per the inbound NAT rule *myNATRuleRDPVM2*, traffic from the load balancer's Frontend port **4222** is configured to redirect to port 3389 of the virtual machine *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="35cee-260">The RDP connection succeeds, as per the inbound NAT rule *myNATRuleRDPVM2*, traffic from the load balancer's Frontend port **4222** is configured to redirect to port 3389 of the virtual machine *myVM2*.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="35cee-261">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="35cee-261">Clean up resources</span></span>

<span data-ttu-id="35cee-262">When no longer needed, delete the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="35cee-262">When no longer needed, delete the resource group, load balancer, and all related resources.</span></span> <span data-ttu-id="35cee-263">To do so, select the resource group that contains the load balancer and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="35cee-263">To do so, select the resource group that contains the load balancer and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="35cee-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="35cee-264">Next steps</span></span>

<span data-ttu-id="35cee-265">In this tutorial, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-265">In this tutorial, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="35cee-266">You also, removed a VM from the load-balanced set, and added the VM back to the backend address pool.</span><span class="sxs-lookup"><span data-stu-id="35cee-266">You also, removed a VM from the load-balanced set, and added the VM back to the backend address pool.</span></span> <span data-ttu-id="35cee-267">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="35cee-267">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="35cee-268">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="35cee-268">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-standard-public-zone-redundant-portal.md)
