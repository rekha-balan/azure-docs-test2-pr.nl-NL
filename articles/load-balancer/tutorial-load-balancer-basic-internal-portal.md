---
title: Tutorial - Create a public Basic Load Balancer - Azure portal | Microsoft Docs
description: This tutorial shows you how to create an internal Basic Load Balancer by using the Azure portal.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: As an IT administrator, I want to create a load balancer that load balances incoming internet traffic to virtual machines within a specific zone in a region.
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 7c1e56b7c94c51a00fabdac56dd2d8c3eb621ae0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870153"
---
# <a name="tutorial-load-balance-internal-traffic-with-basic-load-balancer-to-vms-using-the-azure-portal"></a><span data-ttu-id="d884b-103">Tutorial: Load balance internal traffic with Basic Load Balancer to VMs using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d884b-103">Tutorial: Load balance internal traffic with Basic Load Balancer to VMs using the Azure portal</span></span>

<span data-ttu-id="d884b-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span><span class="sxs-lookup"><span data-stu-id="d884b-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="d884b-105">You can use the Azure portal to load balance internal traffic to virtual machines with a Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-105">You can use the Azure portal to load balance internal traffic to virtual machines with a Basic Load Balancer.</span></span> <span data-ttu-id="d884b-106">This tutorial shows you how to create network resources, backend servers, and an internal Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-106">This tutorial shows you how to create network resources, backend servers, and an internal Basic Load Balancer.</span></span>

<span data-ttu-id="d884b-107">If you prefer, you can complete this tutorial using the [Azure CLI](load-balancer-get-started-ilb-arm-cli.md) or [Azure PowerShell](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="d884b-107">If you prefer, you can complete this tutorial using the [Azure CLI](load-balancer-get-started-ilb-arm-cli.md) or [Azure PowerShell](load-balancer-get-started-ilb-arm-ps.md).</span></span>

<span data-ttu-id="d884b-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="d884b-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="d884b-109">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d884b-109">Sign in to the Azure portal</span></span>

<span data-ttu-id="d884b-110">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d884b-110">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="d884b-111">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="d884b-111">Create a virtual network</span></span>
1. <span data-ttu-id="d884b-112">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="d884b-112">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span></span>
    - <span data-ttu-id="d884b-113">*myVnet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d884b-113">*myVnet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="d884b-114">*myResourceGroupILB* - for the name of the existing resource group</span><span class="sxs-lookup"><span data-stu-id="d884b-114">*myResourceGroupILB* - for the name of the existing resource group</span></span>
    - <span data-ttu-id="d884b-115">*myBackendSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="d884b-115">*myBackendSubnet* - for the subnet name.</span></span>
2. <span data-ttu-id="d884b-116">Click **Create** to create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d884b-116">Click **Create** to create the virtual network.</span></span>

![Create a load balancer](./media/tutorial-load-balancer-basic-internal-portal/1-load-balancer.png)

## <a name="create-a-basic-load-balancer"></a><span data-ttu-id="d884b-118">Create a Basic Load Balancer</span><span class="sxs-lookup"><span data-stu-id="d884b-118">Create a Basic Load Balancer</span></span>
<span data-ttu-id="d884b-119">Create an internal Basic Load Balancer using the portal.</span><span class="sxs-lookup"><span data-stu-id="d884b-119">Create an internal Basic Load Balancer using the portal.</span></span>

1. <span data-ttu-id="d884b-120">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="d884b-120">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="d884b-121">In the **Create a load balancer** page enter these values for the load balancer:</span><span class="sxs-lookup"><span data-stu-id="d884b-121">In the **Create a load balancer** page enter these values for the load balancer:</span></span>
    - <span data-ttu-id="d884b-122">*myLoadBalancer* - for the name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-122">*myLoadBalancer* - for the name of the load balancer.</span></span>
    - <span data-ttu-id="d884b-123">**Internal** - for the type of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-123">**Internal** - for the type of the load balancer.</span></span>
    - <span data-ttu-id="d884b-124">**Basic** - for SKU version.</span><span class="sxs-lookup"><span data-stu-id="d884b-124">**Basic** - for SKU version.</span></span>
    - <span data-ttu-id="d884b-125">**10.1.0.7** - for the static private IP address.</span><span class="sxs-lookup"><span data-stu-id="d884b-125">**10.1.0.7** - for the static private IP address.</span></span>
    - <span data-ttu-id="d884b-126">*myVNet* - for virtual network that you choose from the list of existing networks.</span><span class="sxs-lookup"><span data-stu-id="d884b-126">*myVNet* - for virtual network that you choose from the list of existing networks.</span></span>
    - <span data-ttu-id="d884b-127">*mySubnet* - for subnet that you choose from the list of existing subnets.</span><span class="sxs-lookup"><span data-stu-id="d884b-127">*mySubnet* - for subnet that you choose from the list of existing subnets.</span></span>
    - <span data-ttu-id="d884b-128">*myResourceGroupILB* - for the name of the new resource group that you create.</span><span class="sxs-lookup"><span data-stu-id="d884b-128">*myResourceGroupILB* - for the name of the new resource group that you create.</span></span>
3. <span data-ttu-id="d884b-129">Click **Create** to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-129">Click **Create** to create the load balancer.</span></span>
   
    ## <a name="create-backend-servers"></a><span data-ttu-id="d884b-130">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="d884b-130">Create backend servers</span></span>

<span data-ttu-id="d884b-131">In this section, you create two virtual machines for the backend pool of your Basic Load Balancer, and then install IIS on the virtual machines to help test the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-131">In this section, you create two virtual machines for the backend pool of your Basic Load Balancer, and then install IIS on the virtual machines to help test the load balancer.</span></span>

### <a name="create-virtual-machines"></a><span data-ttu-id="d884b-132">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="d884b-132">Create virtual machines</span></span>

1. <span data-ttu-id="d884b-133">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="d884b-133">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    - <span data-ttu-id="d884b-134">*myVM1* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d884b-134">*myVM1* - for the name of the virtual machine.</span></span>        
    - <span data-ttu-id="d884b-135">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="d884b-135">*azureuser* - for the administrator user name.</span></span>   
    - <span data-ttu-id="d884b-136">*myResourceGroupILB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupILB*.</span><span class="sxs-lookup"><span data-stu-id="d884b-136">*myResourceGroupILB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupILB*.</span></span>
2. <span data-ttu-id="d884b-137">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d884b-137">Click **OK**.</span></span>
3. <span data-ttu-id="d884b-138">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="d884b-138">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="d884b-139">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="d884b-139">Enter these values for the VM settings:</span></span>
    - <span data-ttu-id="d884b-140">*myAvailabilitySet* - for the name of the new Availability set that you create.</span><span class="sxs-lookup"><span data-stu-id="d884b-140">*myAvailabilitySet* - for the name of the new Availability set that you create.</span></span>
    -  <span data-ttu-id="d884b-141">*myVNet* - ensure it is selected as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d884b-141">*myVNet* - ensure it is selected as the virtual network.</span></span>
    - <span data-ttu-id="d884b-142">*myBackendSubnet* - ensure it is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="d884b-142">*myBackendSubnet* - ensure it is selected as the subnet.</span></span>
5. <span data-ttu-id="d884b-143">Under **Network Security Group**, select **Advanced**.</span><span class="sxs-lookup"><span data-stu-id="d884b-143">Under **Network Security Group**, select **Advanced**.</span></span> <span data-ttu-id="d884b-144">Next, for **Network security group (firewall)**, select **None**.</span><span class="sxs-lookup"><span data-stu-id="d884b-144">Next, for **Network security group (firewall)**, select **None**.</span></span>
5. <span data-ttu-id="d884b-145">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d884b-145">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="d884b-146">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d884b-146">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>
7. <span data-ttu-id="d884b-147">Using steps 1-6, create a second VM, named, *VM2* with *myAvailabilityset* as the Availability set, *myVnet* as the virtual network, *myBackendSubnet* as subnet, and select **None** for the **Network security group (firewall)**.</span><span class="sxs-lookup"><span data-stu-id="d884b-147">Using steps 1-6, create a second VM, named, *VM2* with *myAvailabilityset* as the Availability set, *myVnet* as the virtual network, *myBackendSubnet* as subnet, and select **None** for the **Network security group (firewall)**.</span></span> 

### <a name="install-iis-and-customize-the-default-web-page"></a><span data-ttu-id="d884b-148">Install IIS and customize the default web page</span><span class="sxs-lookup"><span data-stu-id="d884b-148">Install IIS and customize the default web page</span></span>

1. <span data-ttu-id="d884b-149">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupILB* resource group.</span><span class="sxs-lookup"><span data-stu-id="d884b-149">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupILB* resource group.</span></span>
2. <span data-ttu-id="d884b-150">On the **Overview** page, click **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="d884b-150">On the **Overview** page, click **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="d884b-151">Log into the VM.</span><span class="sxs-lookup"><span data-stu-id="d884b-151">Log into the VM.</span></span>
4. <span data-ttu-id="d884b-152">On the server desktop, navigate to **Windows Administrative Tools**>**Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="d884b-152">On the server desktop, navigate to **Windows Administrative Tools**>**Server Manager**.</span></span>
5. <span data-ttu-id="d884b-153">Launch Windows PowerShell on VM1 and using the following commands to install IIS server and update the default htm file.</span><span class="sxs-lookup"><span data-stu-id="d884b-153">Launch Windows PowerShell on VM1 and using the following commands to install IIS server and update the default htm file.</span></span>
    ```powershell-interactive
    # Install IIS
      Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # Remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    #Add custom htm file
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
    ```
5. <span data-ttu-id="d884b-154">Close the RDP connection with *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="d884b-154">Close the RDP connection with *myVM1*.</span></span>
6. <span data-ttu-id="d884b-155">Repeat steps 1-5 with *myVM2* to install IIS and customize the default web page.</span><span class="sxs-lookup"><span data-stu-id="d884b-155">Repeat steps 1-5 with *myVM2* to install IIS and customize the default web page.</span></span>

## <a name="create-basic-load-balancer-resources"></a><span data-ttu-id="d884b-156">Create Basic Load Balancer resources</span><span class="sxs-lookup"><span data-stu-id="d884b-156">Create Basic Load Balancer resources</span></span>

<span data-ttu-id="d884b-157">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify load balancer and NAT rules.</span><span class="sxs-lookup"><span data-stu-id="d884b-157">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify load balancer and NAT rules.</span></span>


### <a name="create-a-backend-address-pool"></a><span data-ttu-id="d884b-158">Create a backend address pool</span><span class="sxs-lookup"><span data-stu-id="d884b-158">Create a backend address pool</span></span>

<span data-ttu-id="d884b-159">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d884b-159">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span> <span data-ttu-id="d884b-160">Create the backend address pool *myBackendPool* to include *VM1* and *VM2*.</span><span class="sxs-lookup"><span data-stu-id="d884b-160">Create the backend address pool *myBackendPool* to include *VM1* and *VM2*.</span></span>

1. <span data-ttu-id="d884b-161">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="d884b-161">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="d884b-162">Under **Settings**, click **Backend pools**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d884b-162">Under **Settings**, click **Backend pools**, then click **Add**.</span></span>
3. <span data-ttu-id="d884b-163">On the **Add a backend pool** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="d884b-163">On the **Add a backend pool** page, do the following:</span></span>
    - <span data-ttu-id="d884b-164">For name, type *myBackEndPool*, as the name for your backend pool.</span><span class="sxs-lookup"><span data-stu-id="d884b-164">For name, type *myBackEndPool*, as the name for your backend pool.</span></span>
    - <span data-ttu-id="d884b-165">For **Associated to**, from the drop-down menu, click **Availability set**</span><span class="sxs-lookup"><span data-stu-id="d884b-165">For **Associated to**, from the drop-down menu, click **Availability set**</span></span>
    - <span data-ttu-id="d884b-166">For **Availability set**, click, **myAvailabilitySet**.</span><span class="sxs-lookup"><span data-stu-id="d884b-166">For **Availability set**, click, **myAvailabilitySet**.</span></span>
    - <span data-ttu-id="d884b-167">Click **Add a target network IP configuration** to add each virtual machine (*myVM1* & *myVM2*) that you created to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="d884b-167">Click **Add a target network IP configuration** to add each virtual machine (*myVM1* & *myVM2*) that you created to the backend pool.</span></span>
    - <span data-ttu-id="d884b-168">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d884b-168">Click **OK**.</span></span>

        ![<span data-ttu-id="d884b-169">Adding to the backend address pool -</span><span class="sxs-lookup"><span data-stu-id="d884b-169">Adding to the backend address pool -</span></span> ](./media/tutorial-load-balancer-basic-internal-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="d884b-170">Check to make sure your load balancer backend pool setting displays both the VMs **VM1** and **VM2**.</span><span class="sxs-lookup"><span data-stu-id="d884b-170">Check to make sure your load balancer backend pool setting displays both the VMs **VM1** and **VM2**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="d884b-171">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="d884b-171">Create a health probe</span></span>

<span data-ttu-id="d884b-172">To allow the Basic Load Balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="d884b-172">To allow the Basic Load Balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="d884b-173">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="d884b-173">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="d884b-174">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="d884b-174">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="d884b-175">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="d884b-175">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="d884b-176">Under **Settings**, click **Health probes**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d884b-176">Under **Settings**, click **Health probes**, then click **Add**.</span></span>
3. <span data-ttu-id="d884b-177">Use these values to create the health probe:</span><span class="sxs-lookup"><span data-stu-id="d884b-177">Use these values to create the health probe:</span></span>
    - <span data-ttu-id="d884b-178">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="d884b-178">*myHealthProbe* - for the name of the health probe.</span></span>
    - <span data-ttu-id="d884b-179">**HTTP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="d884b-179">**HTTP** - for the protocol type.</span></span>
    - <span data-ttu-id="d884b-180">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="d884b-180">*80* - for the port number.</span></span>
    - <span data-ttu-id="d884b-181">*15* - for number of **Interval** in seconds between probe attempts.</span><span class="sxs-lookup"><span data-stu-id="d884b-181">*15* - for number of **Interval** in seconds between probe attempts.</span></span>
    - <span data-ttu-id="d884b-182">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="d884b-182">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span></span>
4. <span data-ttu-id="d884b-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d884b-183">Click **OK**.</span></span>

   ![Adding a probe](./media/tutorial-load-balancer-basic-internal-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="d884b-185">Create a Load Balancer rule</span><span class="sxs-lookup"><span data-stu-id="d884b-185">Create a Load Balancer rule</span></span>

<span data-ttu-id="d884b-186">A Load Balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="d884b-186">A Load Balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="d884b-187">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="d884b-187">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="d884b-188">Create a Load Balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *LoadBalancerFrontEnd* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="d884b-188">Create a Load Balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *LoadBalancerFrontEnd* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

1. <span data-ttu-id="d884b-189">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="d884b-189">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="d884b-190">Under **Settings**, click **Load balancing rules**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d884b-190">Under **Settings**, click **Load balancing rules**, then click **Add**.</span></span>
3. <span data-ttu-id="d884b-191">Use these values to configure the load balancing rule:</span><span class="sxs-lookup"><span data-stu-id="d884b-191">Use these values to configure the load balancing rule:</span></span>
    - <span data-ttu-id="d884b-192">*myHTTPRule* - for the name of the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="d884b-192">*myHTTPRule* - for the name of the load balancing rule.</span></span>
    - <span data-ttu-id="d884b-193">**TCP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="d884b-193">**TCP** - for the protocol type.</span></span>
    - <span data-ttu-id="d884b-194">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="d884b-194">*80* - for the port number.</span></span>
    - <span data-ttu-id="d884b-195">*80* - for the backend port.</span><span class="sxs-lookup"><span data-stu-id="d884b-195">*80* - for the backend port.</span></span>
    - <span data-ttu-id="d884b-196">*myBackendPool* - for the name of the backend pool.</span><span class="sxs-lookup"><span data-stu-id="d884b-196">*myBackendPool* - for the name of the backend pool.</span></span>
    - <span data-ttu-id="d884b-197">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="d884b-197">*myHealthProbe* - for the name of the health probe.</span></span>
4. <span data-ttu-id="d884b-198">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d884b-198">Click **OK**.</span></span>
    
    ![Adding a load balancing rule](./media/tutorial-load-balancer-basic-internal-portal/5-load-balancing-rules.png)

## <a name="create-a-virtual-machine-to-test-the-load-balancer"></a><span data-ttu-id="d884b-200">Create a virtual machine to test the load balancer</span><span class="sxs-lookup"><span data-stu-id="d884b-200">Create a virtual machine to test the load balancer</span></span>
<span data-ttu-id="d884b-201">In order to test the internal load balancer, you must create a virtual machine that is located in the same virtual network as the backend server VMs.</span><span class="sxs-lookup"><span data-stu-id="d884b-201">In order to test the internal load balancer, you must create a virtual machine that is located in the same virtual network as the backend server VMs.</span></span>
1. <span data-ttu-id="d884b-202">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="d884b-202">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    - <span data-ttu-id="d884b-203">*myVMTest* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="d884b-203">*myVMTest* - for the name of the virtual machine.</span></span>        
    - <span data-ttu-id="d884b-204">*myResourceGroupILB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupILB*.</span><span class="sxs-lookup"><span data-stu-id="d884b-204">*myResourceGroupILB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupILB*.</span></span>
2. <span data-ttu-id="d884b-205">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d884b-205">Click **OK**.</span></span>
3. <span data-ttu-id="d884b-206">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="d884b-206">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="d884b-207">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="d884b-207">Enter these values for the VM settings:</span></span>
    -  <span data-ttu-id="d884b-208">*myVNet* - ensure it is selected as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d884b-208">*myVNet* - ensure it is selected as the virtual network.</span></span>
    - <span data-ttu-id="d884b-209">*myBackendSubnet* - ensure it is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="d884b-209">*myBackendSubnet* - ensure it is selected as the subnet.</span></span>
5. <span data-ttu-id="d884b-210">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="d884b-210">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="d884b-211">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="d884b-211">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="d884b-212">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="d884b-212">Test the load balancer</span></span>
1. <span data-ttu-id="d884b-213">In the Azure portal, get the Private IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="d884b-213">In the Azure portal, get the Private IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="d884b-214">To do so: a.</span><span class="sxs-lookup"><span data-stu-id="d884b-214">To do so: a.</span></span> <span data-ttu-id="d884b-215">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="d884b-215">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
    <span data-ttu-id="d884b-216">b.</span><span class="sxs-lookup"><span data-stu-id="d884b-216">b.</span></span> <span data-ttu-id="d884b-217">In the **Overview** details page, copy the Private IP address (in this example, it is 10.1.0.7).</span><span class="sxs-lookup"><span data-stu-id="d884b-217">In the **Overview** details page, copy the Private IP address (in this example, it is 10.1.0.7).</span></span>

2. <span data-ttu-id="d884b-218">Create a remote connection to *myVMTest* as follows: a.</span><span class="sxs-lookup"><span data-stu-id="d884b-218">Create a remote connection to *myVMTest* as follows: a.</span></span> <span data-ttu-id="d884b-219">Click **All resources** in the left-hand menu, and then from the resources list click **myVMTest** that is located in the *myResourceGroupILB* resource group.</span><span class="sxs-lookup"><span data-stu-id="d884b-219">Click **All resources** in the left-hand menu, and then from the resources list click **myVMTest** that is located in the *myResourceGroupILB* resource group.</span></span>
2. <span data-ttu-id="d884b-220">On the **Overview** page, click **Connect** to start a remote session with the VM.</span><span class="sxs-lookup"><span data-stu-id="d884b-220">On the **Overview** page, click **Connect** to start a remote session with the VM.</span></span>
3. <span data-ttu-id="d884b-221">Log into the *myVMTest*.</span><span class="sxs-lookup"><span data-stu-id="d884b-221">Log into the *myVMTest*.</span></span>
3. <span data-ttu-id="d884b-222">Paste the Private IP address into the address bar of the browser in *myVMTest*.</span><span class="sxs-lookup"><span data-stu-id="d884b-222">Paste the Private IP address into the address bar of the browser in *myVMTest*.</span></span> <span data-ttu-id="d884b-223">The default page of IIS Web server is displayed on the browser.</span><span class="sxs-lookup"><span data-stu-id="d884b-223">The default page of IIS Web server is displayed on the browser.</span></span>

      ![IIS Web server](./media/tutorial-load-balancer-basic-internal-portal/9-load-balancer-test.png)

<span data-ttu-id="d884b-225">To see the load balancer distribute traffic across both VMs running your app, you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="d884b-225">To see the load balancer distribute traffic across both VMs running your app, you can force-refresh your web browser.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d884b-226">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d884b-226">Clean up resources</span></span>

<span data-ttu-id="d884b-227">When no longer needed, delete the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="d884b-227">When no longer needed, delete the resource group, load balancer, and all related resources.</span></span> <span data-ttu-id="d884b-228">To do so, select the resource group that contains the load balancer and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="d884b-228">To do so, select the resource group that contains the load balancer and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d884b-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="d884b-229">Next steps</span></span>

<span data-ttu-id="d884b-230">In this tutorial, you created a resource group, network resources, and backend servers.</span><span class="sxs-lookup"><span data-stu-id="d884b-230">In this tutorial, you created a resource group, network resources, and backend servers.</span></span> <span data-ttu-id="d884b-231">You then used those resources to create an internal load balancer to load balance internal traffic to VMs.</span><span class="sxs-lookup"><span data-stu-id="d884b-231">You then used those resources to create an internal load balancer to load balance internal traffic to VMs.</span></span> <span data-ttu-id="d884b-232">Next, learn how to [load balance VMs across availability zones](tutorial-load-balancer-standard-public-zone-redundant-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d884b-232">Next, learn how to [load balance VMs across availability zones](tutorial-load-balancer-standard-public-zone-redundant-portal.md)</span></span>
