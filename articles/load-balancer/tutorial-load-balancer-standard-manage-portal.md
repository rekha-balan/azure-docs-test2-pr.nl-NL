---
title: Tutorial:Create and manage a Standard Load Balancer - Azure portal | Microsoft Docs
description: This tutorial shows how to create and manage a Standard Load Balancer by using the Azure portal.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I want to create and Standard Load balancer so that I can load balance internet traffic to VMs and add and remove VMs from the load-balanced set.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/20/18
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 7c3e5c0cc8297ba60925d36d667e0b72a5072553
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856564"
---
# <a name="tutorial-create-and-manage-standard-load-balancer-using-the-azure-portal"></a><span data-ttu-id="25161-103">Tutorial: Create and manage Standard Load Balancer using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="25161-103">Tutorial: Create and manage Standard Load Balancer using the Azure portal</span></span>

<span data-ttu-id="25161-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span><span class="sxs-lookup"><span data-stu-id="25161-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="25161-105">In this tutorial, you learn about the different components of the Azure Standard Load Balancer that distribute traffic and provide high availability.</span><span class="sxs-lookup"><span data-stu-id="25161-105">In this tutorial, you learn about the different components of the Azure Standard Load Balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="25161-106">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="25161-106">You learn how to:</span></span>


> [!div class="checklist"]
> * <span data-ttu-id="25161-107">Create an Azure load balancer</span><span class="sxs-lookup"><span data-stu-id="25161-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="25161-108">Create virtual machines and install IIS server</span><span class="sxs-lookup"><span data-stu-id="25161-108">Create virtual machines and install IIS server</span></span>
> * <span data-ttu-id="25161-109">Create load balancer resources</span><span class="sxs-lookup"><span data-stu-id="25161-109">Create load balancer resources</span></span>
> * <span data-ttu-id="25161-110">View a load balancer in action</span><span class="sxs-lookup"><span data-stu-id="25161-110">View a load balancer in action</span></span>
> * <span data-ttu-id="25161-111">Add and remove VMs from a load balancer</span><span class="sxs-lookup"><span data-stu-id="25161-111">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="25161-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="25161-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="25161-113">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="25161-113">Sign in to the Azure portal</span></span>

<span data-ttu-id="25161-114">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25161-114">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

## <a name="create-a-standard-load-balancer"></a><span data-ttu-id="25161-115">Create a Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="25161-115">Create a Standard Load Balancer</span></span>

<span data-ttu-id="25161-116">In this section, you create a public load balancer that helps load balance virtual machines.</span><span class="sxs-lookup"><span data-stu-id="25161-116">In this section, you create a public load balancer that helps load balance virtual machines.</span></span> <span data-ttu-id="25161-117">Standard Load Balancer only supports a Standard Public IP address.</span><span class="sxs-lookup"><span data-stu-id="25161-117">Standard Load Balancer only supports a Standard Public IP address.</span></span> <span data-ttu-id="25161-118">When you create a Standard Load Balancer, you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-118">When you create a Standard Load Balancer, you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span></span> 

1. <span data-ttu-id="25161-119">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="25161-119">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="25161-120">In the **Create load balancer** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Create**:</span><span class="sxs-lookup"><span data-stu-id="25161-120">In the **Create load balancer** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Create**:</span></span>
    
    | <span data-ttu-id="25161-121">Setting</span><span class="sxs-lookup"><span data-stu-id="25161-121">Setting</span></span>                 | <span data-ttu-id="25161-122">Value</span><span class="sxs-lookup"><span data-stu-id="25161-122">Value</span></span>                                              |
    | ---                     | ---                                                |
    | <span data-ttu-id="25161-123">Name</span><span class="sxs-lookup"><span data-stu-id="25161-123">Name</span></span>                   | <span data-ttu-id="25161-124">*myLoadBalancer*</span><span class="sxs-lookup"><span data-stu-id="25161-124">*myLoadBalancer*</span></span>                                   |
    | <span data-ttu-id="25161-125">Type</span><span class="sxs-lookup"><span data-stu-id="25161-125">Type</span></span>          | <span data-ttu-id="25161-126">Public</span><span class="sxs-lookup"><span data-stu-id="25161-126">Public</span></span>                                        |
    | <span data-ttu-id="25161-127">SKU</span><span class="sxs-lookup"><span data-stu-id="25161-127">SKU</span></span>           | <span data-ttu-id="25161-128">Standard</span><span class="sxs-lookup"><span data-stu-id="25161-128">Standard</span></span>                          |
    | <span data-ttu-id="25161-129">Public IP address</span><span class="sxs-lookup"><span data-stu-id="25161-129">Public IP address</span></span> | <span data-ttu-id="25161-130">Select **Create new** and type *myPublicIP* in the text box.</span><span class="sxs-lookup"><span data-stu-id="25161-130">Select **Create new** and type *myPublicIP* in the text box.</span></span> <span data-ttu-id="25161-131">The Standard SKU for the Public IP address is selected by default.</span><span class="sxs-lookup"><span data-stu-id="25161-131">The Standard SKU for the Public IP address is selected by default.</span></span> <span data-ttu-id="25161-132">For **Availability zone**, select **Zone-redundant**.</span><span class="sxs-lookup"><span data-stu-id="25161-132">For **Availability zone**, select **Zone-redundant**.</span></span> |
    | <span data-ttu-id="25161-133">Subscription</span><span class="sxs-lookup"><span data-stu-id="25161-133">Subscription</span></span>               | <span data-ttu-id="25161-134">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="25161-134">Select your subscription.</span></span>    |
    |<span data-ttu-id="25161-135">Resource group</span><span class="sxs-lookup"><span data-stu-id="25161-135">Resource group</span></span> | <span data-ttu-id="25161-136">Select **Create new**, and then type *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="25161-136">Select **Create new**, and then type *myResourceGroupSLB*.</span></span>    |
    | <span data-ttu-id="25161-137">Location</span><span class="sxs-lookup"><span data-stu-id="25161-137">Location</span></span>           | <span data-ttu-id="25161-138">Select **West Europe**.</span><span class="sxs-lookup"><span data-stu-id="25161-138">Select **West Europe**.</span></span>                          |
    

![Create a load balancer](./media/load-balancer-standard-public-portal/create-load-balancer.png)
   
## <a name="create-backend-servers"></a><span data-ttu-id="25161-140">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="25161-140">Create backend servers</span></span>

<span data-ttu-id="25161-141">In this section, you create a virtual network, create three virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test the load balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-141">In this section, you create a virtual network, create three virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test the load balancer.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="25161-142">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="25161-142">Create a virtual network</span></span>
1. <span data-ttu-id="25161-143">On the top left-hand side of the Azure portal, select **Create a resource** > **Networking** > **Virtual network** and then enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="25161-143">On the top left-hand side of the Azure portal, select **Create a resource** > **Networking** > **Virtual network** and then enter these values for the virtual network:</span></span>
    |<span data-ttu-id="25161-144">Setting</span><span class="sxs-lookup"><span data-stu-id="25161-144">Setting</span></span>|<span data-ttu-id="25161-145">Value</span><span class="sxs-lookup"><span data-stu-id="25161-145">Value</span></span>|
    |---|---|
    |<span data-ttu-id="25161-146">Name</span><span class="sxs-lookup"><span data-stu-id="25161-146">Name</span></span>|<span data-ttu-id="25161-147">Enter *myVNet*.</span><span class="sxs-lookup"><span data-stu-id="25161-147">Enter *myVNet*.</span></span>|
    |<span data-ttu-id="25161-148">Subscription</span><span class="sxs-lookup"><span data-stu-id="25161-148">Subscription</span></span>| <span data-ttu-id="25161-149">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="25161-149">Select your subscription.</span></span>|
    |<span data-ttu-id="25161-150">Resource group</span><span class="sxs-lookup"><span data-stu-id="25161-150">Resource group</span></span>| <span data-ttu-id="25161-151">Select **Use existing** and then select *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="25161-151">Select **Use existing** and then select *myResourceGroupSLB*.</span></span>|
    |<span data-ttu-id="25161-152">Subnet name</span><span class="sxs-lookup"><span data-stu-id="25161-152">Subnet name</span></span>| <span data-ttu-id="25161-153">Enter *myBackendSubnet*.</span><span class="sxs-lookup"><span data-stu-id="25161-153">Enter *myBackendSubnet*.</span></span>|
    
2. <span data-ttu-id="25161-154">Click **Create** to create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="25161-154">Click **Create** to create the virtual network.</span></span>

### <a name="create-virtual-machines"></a><span data-ttu-id="25161-155">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="25161-155">Create virtual machines</span></span>

1. <span data-ttu-id="25161-156">On the top left-hand side of the Azure portal, select **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="25161-156">On the top left-hand side of the Azure portal, select **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    1. <span data-ttu-id="25161-157">For the name of the virtual machine, enter *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="25161-157">For the name of the virtual machine, enter *myVM1*.</span></span>        
    2. <span data-ttu-id="25161-158">For **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="25161-158">For **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span></span>
2. <span data-ttu-id="25161-159">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-159">Click **OK**.</span></span>
3. <span data-ttu-id="25161-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="25161-160">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="25161-161">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="25161-161">Enter these values for the VM settings:</span></span>
    1. <span data-ttu-id="25161-162">Ensure that  *myVNet* is selected as the virtual network, and *myBackendSubnet* is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="25161-162">Ensure that  *myVNet* is selected as the virtual network, and *myBackendSubnet* is selected as the subnet.</span></span>
    2. <span data-ttu-id="25161-163">For **Public IP address**, in the **Create Public IP address** pane, select **Standard**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-163">For **Public IP address**, in the **Create Public IP address** pane, select **Standard**, and then select **OK**.</span></span>
    3. <span data-ttu-id="25161-164">For **Network Security Group**, select **Advanced**, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="25161-164">For **Network Security Group**, select **Advanced**, and then do the following:</span></span>
        1. <span data-ttu-id="25161-165">Select \*Network security group (firewall), and the **Choose network security group** page, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="25161-165">Select \*Network security group (firewall), and the **Choose network security group** page, select **Create new**.</span></span> 
        2. <span data-ttu-id="25161-166">In the **Choose network security group** page, for **Name**, enter *myNetworkSecurityGroup* as the name of the new network security group, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-166">In the **Choose network security group** page, for **Name**, enter *myNetworkSecurityGroup* as the name of the new network security group, and then select **OK**.</span></span>
5. <span data-ttu-id="25161-167">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="25161-167">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="25161-168">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="25161-168">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>
7. <span data-ttu-id="25161-169">Create two more VMs, named, *VM2* and *VM3* with *myVnet* as its virtual network, *myBackendSubnet* as its subnet, and *myNetworkSecurityGroup* as its network security group using steps 1-6.</span><span class="sxs-lookup"><span data-stu-id="25161-169">Create two more VMs, named, *VM2* and *VM3* with *myVnet* as its virtual network, *myBackendSubnet* as its subnet, and *myNetworkSecurityGroup* as its network security group using steps 1-6.</span></span> 

### <a name="create-network-security-group-rule"></a><span data-ttu-id="25161-170">Create network security group rule</span><span class="sxs-lookup"><span data-stu-id="25161-170">Create network security group rule</span></span>

<span data-ttu-id="25161-171">In this section, you create a NSG rule to allow inbound connections using HTTP.</span><span class="sxs-lookup"><span data-stu-id="25161-171">In this section, you create a NSG rule to allow inbound connections using HTTP.</span></span>

1. <span data-ttu-id="25161-172">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span><span class="sxs-lookup"><span data-stu-id="25161-172">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span></span>
2. <span data-ttu-id="25161-173">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-173">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span></span>
3. <span data-ttu-id="25161-174">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span><span class="sxs-lookup"><span data-stu-id="25161-174">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span></span>
    - <span data-ttu-id="25161-175">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="25161-175">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="25161-176">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="25161-176">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="25161-177">*80* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="25161-177">*80* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="25161-178">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="25161-178">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="25161-179">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="25161-179">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="25161-180">*100* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="25161-180">*100* for **Priority**</span></span>
    - <span data-ttu-id="25161-181">*myHTTPRule* for name</span><span class="sxs-lookup"><span data-stu-id="25161-181">*myHTTPRule* for name</span></span>
    - <span data-ttu-id="25161-182">*Allow HTTP* - for description</span><span class="sxs-lookup"><span data-stu-id="25161-182">*Allow HTTP* - for description</span></span>
4. <span data-ttu-id="25161-183">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-183">Select **Add**.</span></span>

### <a name="install-iis-on-vms"></a><span data-ttu-id="25161-184">Install IIS on VMs</span><span class="sxs-lookup"><span data-stu-id="25161-184">Install IIS on VMs</span></span>

1. <span data-ttu-id="25161-185">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupSLB* resource group.</span><span class="sxs-lookup"><span data-stu-id="25161-185">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupSLB* resource group.</span></span>
2. <span data-ttu-id="25161-186">On the **Overview** page, click **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="25161-186">On the **Overview** page, click **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="25161-187">In the **Connect to virtual machine** pop-up window, select **Download RDP File**, and then Open the downloaded RDP file.</span><span class="sxs-lookup"><span data-stu-id="25161-187">In the **Connect to virtual machine** pop-up window, select **Download RDP File**, and then Open the downloaded RDP file.</span></span>
4. <span data-ttu-id="25161-188">In the **Remote Desktop Connection** window, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="25161-188">In the **Remote Desktop Connection** window, click **Connect**.</span></span>
5. <span data-ttu-id="25161-189">Log into the VM with the credentials that you provided during the creation of this VM.</span><span class="sxs-lookup"><span data-stu-id="25161-189">Log into the VM with the credentials that you provided during the creation of this VM.</span></span> <span data-ttu-id="25161-190">This launches a remote desktop session with virtual machine - *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="25161-190">This launches a remote desktop session with virtual machine - *myVM1*.</span></span>
6. <span data-ttu-id="25161-191">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="25161-191">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span></span>
7. <span data-ttu-id="25161-192">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span><span class="sxs-lookup"><span data-stu-id="25161-192">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span></span>

   ```azurepowershell-interactive
    
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add a new htm file that displays server name
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from " + $env:computername)
   ```
6. <span data-ttu-id="25161-193">Close the RDP session with *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="25161-193">Close the RDP session with *myVM1*.</span></span>
7. <span data-ttu-id="25161-194">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2* and *myVM3*.</span><span class="sxs-lookup"><span data-stu-id="25161-194">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2* and *myVM3*.</span></span>

## <a name="create-load-balancer-resources"></a><span data-ttu-id="25161-195">Create load balancer resources</span><span class="sxs-lookup"><span data-stu-id="25161-195">Create load balancer resources</span></span>

<span data-ttu-id="25161-196">In this section, you configure load balancer settings for a backend address pool, a health probe, and specify a balancer rule.</span><span class="sxs-lookup"><span data-stu-id="25161-196">In this section, you configure load balancer settings for a backend address pool, a health probe, and specify a balancer rule.</span></span>

### <a name="create-a-backend-address-pool"></a><span data-ttu-id="25161-197">Create a backend address pool</span><span class="sxs-lookup"><span data-stu-id="25161-197">Create a backend address pool</span></span>

<span data-ttu-id="25161-198">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-198">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span> <span data-ttu-id="25161-199">Create the backend address pool *myBackendPool* to include *VM1* and *VM2*.</span><span class="sxs-lookup"><span data-stu-id="25161-199">Create the backend address pool *myBackendPool* to include *VM1* and *VM2*.</span></span>

1. <span data-ttu-id="25161-200">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="25161-200">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="25161-201">Under **Settings**, click **Backend pools**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-201">Under **Settings**, click **Backend pools**, then click **Add**.</span></span>
3. <span data-ttu-id="25161-202">On the **Add a backend pool** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="25161-202">On the **Add a backend pool** page, do the following:</span></span>
   - <span data-ttu-id="25161-203">For name, type *myBackendPool*, as the name for your backend pool.</span><span class="sxs-lookup"><span data-stu-id="25161-203">For name, type *myBackendPool*, as the name for your backend pool.</span></span>
   - <span data-ttu-id="25161-204">For **Virtual network**, select *myVNet*.</span><span class="sxs-lookup"><span data-stu-id="25161-204">For **Virtual network**, select *myVNet*.</span></span>
   - <span data-ttu-id="25161-205">Add *myVM1*, *myVM2*, and *my VM3* under **Virtual Machine** along with their corresponding IP addresses, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-205">Add *myVM1*, *myVM2*, and *my VM3* under **Virtual Machine** along with their corresponding IP addresses, and then select **Add**.</span></span>
4. <span data-ttu-id="25161-206">Check to make sure your load balancer backend pool setting displays all the VMs *myVM1*, *myVM2*, and *myVM3*, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-206">Check to make sure your load balancer backend pool setting displays all the VMs *myVM1*, *myVM2*, and *myVM3*, and then click **OK**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="25161-207">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="25161-207">Create a health probe</span></span>

<span data-ttu-id="25161-208">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="25161-208">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="25161-209">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="25161-209">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="25161-210">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="25161-210">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="25161-211">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="25161-211">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="25161-212">Under **Settings**, click **Health probes**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-212">Under **Settings**, click **Health probes**, then click **Add**.</span></span>
3. <span data-ttu-id="25161-213">Use these values to create the health probe:</span><span class="sxs-lookup"><span data-stu-id="25161-213">Use these values to create the health probe:</span></span>
    - <span data-ttu-id="25161-214">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="25161-214">*myHealthProbe* - for the name of the health probe.</span></span>
    - <span data-ttu-id="25161-215">**HTTP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="25161-215">**HTTP** - for the protocol type.</span></span>
    - <span data-ttu-id="25161-216">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="25161-216">*80* - for the port number.</span></span>
    - <span data-ttu-id="25161-217">*15* - for number of **Interval** in seconds between probe attempts.</span><span class="sxs-lookup"><span data-stu-id="25161-217">*15* - for number of **Interval** in seconds between probe attempts.</span></span>
    - <span data-ttu-id="25161-218">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="25161-218">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span></span>
4. <span data-ttu-id="25161-219">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-219">Click **OK**.</span></span>

   ![Adding a probe](./media/load-balancer-standard-public-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="25161-221">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="25161-221">Create a load balancer rule</span></span>

<span data-ttu-id="25161-222">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="25161-222">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="25161-223">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="25161-223">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="25161-224">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="25161-224">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

1. <span data-ttu-id="25161-225">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="25161-225">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="25161-226">Under **Settings**, click **Load balancing rules**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="25161-226">Under **Settings**, click **Load balancing rules**, then click **Add**.</span></span>
3. <span data-ttu-id="25161-227">Use these values to configure the load balancing rule:</span><span class="sxs-lookup"><span data-stu-id="25161-227">Use these values to configure the load balancing rule:</span></span>
    - <span data-ttu-id="25161-228">*myHTTPRule* - for the name of the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="25161-228">*myHTTPRule* - for the name of the load balancing rule.</span></span>
    - <span data-ttu-id="25161-229">**TCP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="25161-229">**TCP** - for the protocol type.</span></span>
    - <span data-ttu-id="25161-230">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="25161-230">*80* - for the port number.</span></span>
    - <span data-ttu-id="25161-231">*80* - for the backend port.</span><span class="sxs-lookup"><span data-stu-id="25161-231">*80* - for the backend port.</span></span>
    - <span data-ttu-id="25161-232">*myBackendPool* - for the name of the backend pool.</span><span class="sxs-lookup"><span data-stu-id="25161-232">*myBackendPool* - for the name of the backend pool.</span></span>
    - <span data-ttu-id="25161-233">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="25161-233">*myHealthProbe* - for the name of the health probe.</span></span>
4. <span data-ttu-id="25161-234">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="25161-234">Click **OK**.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="25161-235">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="25161-235">Test the load balancer</span></span>
1. <span data-ttu-id="25161-236">Find the public IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="25161-236">Find the public IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="25161-237">Click **All resources** and then click **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="25161-237">Click **All resources** and then click **myPublicIP**.</span></span>

2. <span data-ttu-id="25161-238">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="25161-238">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="25161-239">The default page of IIS Web server is displayed on the browser.</span><span class="sxs-lookup"><span data-stu-id="25161-239">The default page of IIS Web server is displayed on the browser.</span></span>

      ![IIS Web server](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

<span data-ttu-id="25161-241">To see the load balancer distribute traffic across the three VMs running your app, you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="25161-241">To see the load balancer distribute traffic across the three VMs running your app, you can force-refresh your web browser.</span></span>

## <a name="remove-or-add-vms-from-the-backend-pool"></a><span data-ttu-id="25161-242">Remove or add VMs from the backend pool</span><span class="sxs-lookup"><span data-stu-id="25161-242">Remove or add VMs from the backend pool</span></span>
<span data-ttu-id="25161-243">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span><span class="sxs-lookup"><span data-stu-id="25161-243">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="25161-244">To deal with increased traffic to your app, you may need to add additional VMs.</span><span class="sxs-lookup"><span data-stu-id="25161-244">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="25161-245">This section shows you how to remove or add a VM from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-245">This section shows you how to remove or add a VM from the load balancer.</span></span>

1. <span data-ttu-id="25161-246">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="25161-246">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="25161-247">Under **Settings**, click **Backend pools**, then within the backend pool's list, click **myBackendPool**.</span><span class="sxs-lookup"><span data-stu-id="25161-247">Under **Settings**, click **Backend pools**, then within the backend pool's list, click **myBackendPool**.</span></span>
3. <span data-ttu-id="25161-248">On the **myBackendPool** page, under **Target network IP configurations**, to remove *VM1* from the backend click the delete icon next to **Virtual machine:myVM1**</span><span class="sxs-lookup"><span data-stu-id="25161-248">On the **myBackendPool** page, under **Target network IP configurations**, to remove *VM1* from the backend click the delete icon next to **Virtual machine:myVM1**</span></span>

<span data-ttu-id="25161-249">With *myVM1* no longer in the backend address pool, you can perform any maintenance tasks on *myVM1*, such as installing software updates.</span><span class="sxs-lookup"><span data-stu-id="25161-249">With *myVM1* no longer in the backend address pool, you can perform any maintenance tasks on *myVM1*, such as installing software updates.</span></span> <span data-ttu-id="25161-250">In the absence of \*VM1\*\*, the load is now balanced across *myVM2* and *myVM3*.</span><span class="sxs-lookup"><span data-stu-id="25161-250">In the absence of \*VM1\*\*, the load is now balanced across *myVM2* and *myVM3*.</span></span> 

<span data-ttu-id="25161-251">To add *myVM1* back to the backend pool, follow the procedure in the *Add VMs to the backend pool* section of this article.</span><span class="sxs-lookup"><span data-stu-id="25161-251">To add *myVM1* back to the backend pool, follow the procedure in the *Add VMs to the backend pool* section of this article.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="25161-252">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="25161-252">Clean up resources</span></span>

<span data-ttu-id="25161-253">When they are no longer needed, delete the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="25161-253">When they are no longer needed, delete the resource group, load balancer, and all related resources.</span></span> <span data-ttu-id="25161-254">To do so, select the resource group that contains the load balancer and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="25161-254">To do so, select the resource group that contains the load balancer and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25161-255">Next steps</span><span class="sxs-lookup"><span data-stu-id="25161-255">Next steps</span></span>

<span data-ttu-id="25161-256">In this tutorial, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-256">In this tutorial, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="25161-257">You also removed a VM from the load-balanced set, and added the VM back to the backend address pool.</span><span class="sxs-lookup"><span data-stu-id="25161-257">You also removed a VM from the load-balanced set, and added the VM back to the backend address pool.</span></span> <span data-ttu-id="25161-258">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="25161-258">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="25161-259">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="25161-259">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-standard-public-zone-redundant-portal.md)
