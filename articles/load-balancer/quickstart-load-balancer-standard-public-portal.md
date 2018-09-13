---
title: Quickstart:Create a Standard Load Balancer - Azure portal | Microsoft Docs
description: This quickstart shows how to create a Standard load balancer by using the Azure portal.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I want to create a Standard Load balancer so that I can load balance internet traffic to VMs.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/21/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 2197ab230341fb2945e7b1acd9a010ef3d3f8c22
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968337"
---
# <a name="quickstart-create-a-standard-load-balancer-to-load-balance-vms-using-the-azure-portal"></a><span data-ttu-id="ea964-103">Quickstart: Create a Standard Load Balancer to load balance VMs using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ea964-103">Quickstart: Create a Standard Load Balancer to load balance VMs using the Azure portal</span></span>

<span data-ttu-id="ea964-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ea964-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="ea964-105">You can use the Azure portal to create a load balancer to load balance virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="ea964-105">You can use the Azure portal to create a load balancer to load balance virtual machines (VMs).</span></span> <span data-ttu-id="ea964-106">This quickstart shows you how to load balance VMs using a Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-106">This quickstart shows you how to load balance VMs using a Standard Load Balancer.</span></span>

<span data-ttu-id="ea964-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="ea964-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="ea964-108">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="ea964-108">Sign in to Azure</span></span>

<span data-ttu-id="ea964-109">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ea964-109">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

## <a name="create-a-public-load-balancer"></a><span data-ttu-id="ea964-110">Create a public load balancer</span><span class="sxs-lookup"><span data-stu-id="ea964-110">Create a public load balancer</span></span>

<span data-ttu-id="ea964-111">In this section, you create a public load balancer that helps load balance virtual machines.</span><span class="sxs-lookup"><span data-stu-id="ea964-111">In this section, you create a public load balancer that helps load balance virtual machines.</span></span> <span data-ttu-id="ea964-112">Standard Load Balancer only supports a Standard Public IP address.</span><span class="sxs-lookup"><span data-stu-id="ea964-112">Standard Load Balancer only supports a Standard Public IP address.</span></span> <span data-ttu-id="ea964-113">When you create a Standard Load Balancer, and you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-113">When you create a Standard Load Balancer, and you must also create a new Standard Public IP address that is configured as the frontend (named as *LoadBalancerFrontend* by default) for the Standard Load Balancer.</span></span> 

1. <span data-ttu-id="ea964-114">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="ea964-114">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="ea964-115">In the **Create load balancer** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Create**:</span><span class="sxs-lookup"><span data-stu-id="ea964-115">In the **Create load balancer** page, enter or select the following information, accept the defaults for the remaining settings, and then select **Create**:</span></span>

    | <span data-ttu-id="ea964-116">Setting</span><span class="sxs-lookup"><span data-stu-id="ea964-116">Setting</span></span>                 | <span data-ttu-id="ea964-117">Value</span><span class="sxs-lookup"><span data-stu-id="ea964-117">Value</span></span>                                              |
    | ---                     | ---                                                |
    | <span data-ttu-id="ea964-118">Name</span><span class="sxs-lookup"><span data-stu-id="ea964-118">Name</span></span>                   | <span data-ttu-id="ea964-119">*myLoadBalancer*</span><span class="sxs-lookup"><span data-stu-id="ea964-119">*myLoadBalancer*</span></span>                                   |
    | <span data-ttu-id="ea964-120">Type</span><span class="sxs-lookup"><span data-stu-id="ea964-120">Type</span></span>          | <span data-ttu-id="ea964-121">Public</span><span class="sxs-lookup"><span data-stu-id="ea964-121">Public</span></span>                                        |
    | <span data-ttu-id="ea964-122">SKU</span><span class="sxs-lookup"><span data-stu-id="ea964-122">SKU</span></span>           | <span data-ttu-id="ea964-123">Standard</span><span class="sxs-lookup"><span data-stu-id="ea964-123">Standard</span></span>                          |
    | <span data-ttu-id="ea964-124">Public IP address</span><span class="sxs-lookup"><span data-stu-id="ea964-124">Public IP address</span></span> | <span data-ttu-id="ea964-125">Select **Create new** and type *myPublicIP* in the text box.</span><span class="sxs-lookup"><span data-stu-id="ea964-125">Select **Create new** and type *myPublicIP* in the text box.</span></span> <span data-ttu-id="ea964-126">The Standard SKU for the Public IP address is selected by default.</span><span class="sxs-lookup"><span data-stu-id="ea964-126">The Standard SKU for the Public IP address is selected by default.</span></span> <span data-ttu-id="ea964-127">For **Availability zone**, select **Zone-redundant**.</span><span class="sxs-lookup"><span data-stu-id="ea964-127">For **Availability zone**, select **Zone-redundant**.</span></span> |
    | <span data-ttu-id="ea964-128">Subscription</span><span class="sxs-lookup"><span data-stu-id="ea964-128">Subscription</span></span>               | <span data-ttu-id="ea964-129">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="ea964-129">Select your subscription.</span></span>    |
    |<span data-ttu-id="ea964-130">Resource group</span><span class="sxs-lookup"><span data-stu-id="ea964-130">Resource group</span></span> | <span data-ttu-id="ea964-131">Select **Create new**, and then type *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="ea964-131">Select **Create new**, and then type *myResourceGroupSLB*.</span></span>    |
    | <span data-ttu-id="ea964-132">Location</span><span class="sxs-lookup"><span data-stu-id="ea964-132">Location</span></span>           | <span data-ttu-id="ea964-133">Select **West Europe**.</span><span class="sxs-lookup"><span data-stu-id="ea964-133">Select **West Europe**.</span></span>                          |
    

![Create a load balancer](./media/load-balancer-standard-public-portal/create-load-balancer.png)


## <a name="create-backend-servers"></a><span data-ttu-id="ea964-135">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="ea964-135">Create backend servers</span></span>

<span data-ttu-id="ea964-136">In this section, you create a virtual network, create two virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test the load balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-136">In this section, you create a virtual network, create two virtual machines for the backend pool of your load balancer, and then install IIS on the virtual machines to help test the load balancer.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="ea964-137">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="ea964-137">Create a virtual network</span></span>
1. <span data-ttu-id="ea964-138">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="ea964-138">On the top left-hand side of the screen click **New** > **Networking** > **Virtual network** and enter these values for the virtual network:</span></span>
    - <span data-ttu-id="ea964-139">*myVnet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="ea964-139">*myVnet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="ea964-140">*myResourceGroupSLB* - for the name of the existing resource group</span><span class="sxs-lookup"><span data-stu-id="ea964-140">*myResourceGroupSLB* - for the name of the existing resource group</span></span>
    - <span data-ttu-id="ea964-141">*myBackendSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="ea964-141">*myBackendSubnet* - for the subnet name.</span></span>
2. <span data-ttu-id="ea964-142">Click **Create** to create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="ea964-142">Click **Create** to create the virtual network.</span></span>

    ![Create a virtual network](./media/load-balancer-standard-public-portal/2-load-balancer-virtual-network.png)

### <a name="create-virtual-machines"></a><span data-ttu-id="ea964-144">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="ea964-144">Create virtual machines</span></span>

1. <span data-ttu-id="ea964-145">On the top left-hand side of the screen, click **New** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="ea964-145">On the top left-hand side of the screen, click **New** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    - <span data-ttu-id="ea964-146">*myVM1* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ea964-146">*myVM1* - for the name of the virtual machine.</span></span>        
    - <span data-ttu-id="ea964-147">*myResourceGroupSLB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span><span class="sxs-lookup"><span data-stu-id="ea964-147">*myResourceGroupSLB* - for **Resource group**, select **Use existing**, and then select *myResourceGroupSLB*.</span></span>
2. <span data-ttu-id="ea964-148">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-148">Click **OK**.</span></span>
3. <span data-ttu-id="ea964-149">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="ea964-149">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="ea964-150">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="ea964-150">Enter these values for the VM settings:</span></span>
    1. <span data-ttu-id="ea964-151">Ensure that  *myVNet* is selected as the virtual network, and *myBackendSubnet* is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="ea964-151">Ensure that  *myVNet* is selected as the virtual network, and *myBackendSubnet* is selected as the subnet.</span></span>
    2. <span data-ttu-id="ea964-152">For **Public IP address**, in the **Create Public IP address** pane, select **Standard**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-152">For **Public IP address**, in the **Create Public IP address** pane, select **Standard**, and then select **OK**.</span></span>
    3. <span data-ttu-id="ea964-153">For **Network Security Group**, select **Advanced**, and then do the following:</span><span class="sxs-lookup"><span data-stu-id="ea964-153">For **Network Security Group**, select **Advanced**, and then do the following:</span></span>
        1. <span data-ttu-id="ea964-154">Select \*Network security group (firewall), and the **Choose network security group** page, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="ea964-154">Select \*Network security group (firewall), and the **Choose network security group** page, select **Create new**.</span></span> 
        2. <span data-ttu-id="ea964-155">In the **Create network security group** page, for **Name**, enter *myNetworkSecurityGroup*, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-155">In the **Create network security group** page, for **Name**, enter *myNetworkSecurityGroup*, and then select **OK**.</span></span>
5. <span data-ttu-id="ea964-156">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="ea964-156">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="ea964-157">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ea964-157">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>
7. <span data-ttu-id="ea964-158">Using steps 1-6, create a second VM, named, *VM2* with *myAvailibilityset* as the Availability set, *myVnet* as its virtual network, *myBackendSubnet* and its subnet, and \**myNetworkSecurityGroup* as its network security group.</span><span class="sxs-lookup"><span data-stu-id="ea964-158">Using steps 1-6, create a second VM, named, *VM2* with *myAvailibilityset* as the Availability set, *myVnet* as its virtual network, *myBackendSubnet* and its subnet, and \**myNetworkSecurityGroup* as its network security group.</span></span> 

### <a name="create-nsg-rule"></a><span data-ttu-id="ea964-159">Create NSG rule</span><span class="sxs-lookup"><span data-stu-id="ea964-159">Create NSG rule</span></span>

<span data-ttu-id="ea964-160">In this section, you create a NSG rule to allow inbound connections using HTTP.</span><span class="sxs-lookup"><span data-stu-id="ea964-160">In this section, you create a NSG rule to allow inbound connections using HTTP.</span></span>

1. <span data-ttu-id="ea964-161">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span><span class="sxs-lookup"><span data-stu-id="ea964-161">Click **All resources** in the left-hand menu, and then from the resources list click **myNetworkSecurityGroup** that is located in the **myResourceGroupSLB** resource group.</span></span>
2. <span data-ttu-id="ea964-162">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ea964-162">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span></span>
3. <span data-ttu-id="ea964-163">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span><span class="sxs-lookup"><span data-stu-id="ea964-163">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span></span>
    - <span data-ttu-id="ea964-164">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="ea964-164">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="ea964-165">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="ea964-165">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="ea964-166">*80* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="ea964-166">*80* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="ea964-167">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="ea964-167">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="ea964-168">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="ea964-168">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="ea964-169">*100* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="ea964-169">*100* for **Priority**</span></span>
    - <span data-ttu-id="ea964-170">*myHTTPRule* for name</span><span class="sxs-lookup"><span data-stu-id="ea964-170">*myHTTPRule* for name</span></span>
    - <span data-ttu-id="ea964-171">*Allow HTTP* - for description</span><span class="sxs-lookup"><span data-stu-id="ea964-171">*Allow HTTP* - for description</span></span>
4. <span data-ttu-id="ea964-172">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-172">Click **OK**.</span></span>
 
### <a name="install-iis"></a><span data-ttu-id="ea964-173">Install IIS</span><span class="sxs-lookup"><span data-stu-id="ea964-173">Install IIS</span></span>

1. <span data-ttu-id="ea964-174">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupLB* resource group.</span><span class="sxs-lookup"><span data-stu-id="ea964-174">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupLB* resource group.</span></span>
2. <span data-ttu-id="ea964-175">On the **Overview** page, click **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="ea964-175">On the **Overview** page, click **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="ea964-176">Log into the VM with username *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="ea964-176">Log into the VM with username *azureuser*.</span></span>
4. <span data-ttu-id="ea964-177">On the server desktop, navigate to **Windows Administrative Tools**>**Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="ea964-177">On the server desktop, navigate to **Windows Administrative Tools**>**Server Manager**.</span></span>
5. <span data-ttu-id="ea964-178">In Server Manager, click **Add Roles and features**.</span><span class="sxs-lookup"><span data-stu-id="ea964-178">In Server Manager, click **Add Roles and features**.</span></span>
6. <span data-ttu-id="ea964-179">In the **Add Roles and Features Wizard**, use the following values:</span><span class="sxs-lookup"><span data-stu-id="ea964-179">In the **Add Roles and Features Wizard**, use the following values:</span></span>
    - <span data-ttu-id="ea964-180">In the **Select installation type** page, click **Role-based or feature-based installation**.</span><span class="sxs-lookup"><span data-stu-id="ea964-180">In the **Select installation type** page, click **Role-based or feature-based installation**.</span></span>
    - <span data-ttu-id="ea964-181">In the **Select destination server** page, click **myVM1**</span><span class="sxs-lookup"><span data-stu-id="ea964-181">In the **Select destination server** page, click **myVM1**</span></span>
    - <span data-ttu-id="ea964-182">In the **Select server role** page, click **Web Server (IIS)**</span><span class="sxs-lookup"><span data-stu-id="ea964-182">In the **Select server role** page, click **Web Server (IIS)**</span></span>
    - <span data-ttu-id="ea964-183">Follow instructions to complete the rest of the wizard</span><span class="sxs-lookup"><span data-stu-id="ea964-183">Follow instructions to complete the rest of the wizard</span></span> 
7. <span data-ttu-id="ea964-184">Repeat steps 1 to 6 for the virtual machine *myVM2*.</span><span class="sxs-lookup"><span data-stu-id="ea964-184">Repeat steps 1 to 6 for the virtual machine *myVM2*.</span></span>

## <a name="create-load-balancer-resources"></a><span data-ttu-id="ea964-185">Create load balancer resources</span><span class="sxs-lookup"><span data-stu-id="ea964-185">Create load balancer resources</span></span>

<span data-ttu-id="ea964-186">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="ea964-186">In this section, you  configure load balancer settings for a backend address pool and a health probe, and specify a load balancer rule.</span></span>


### <a name="create-a-backend-address-pool"></a><span data-ttu-id="ea964-187">Create a backend address pool</span><span class="sxs-lookup"><span data-stu-id="ea964-187">Create a backend address pool</span></span>

<span data-ttu-id="ea964-188">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-188">To distribute traffic to the VMs, a backend address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span> <span data-ttu-id="ea964-189">Create the backend address pool *myBackendPool* to inlcude *VM1* and *VM2*.</span><span class="sxs-lookup"><span data-stu-id="ea964-189">Create the backend address pool *myBackendPool* to inlcude *VM1* and *VM2*.</span></span>

1. <span data-ttu-id="ea964-190">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="ea964-190">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="ea964-191">Under **Settings**, click **Backend pools**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ea964-191">Under **Settings**, click **Backend pools**, then click **Add**.</span></span>
3. <span data-ttu-id="ea964-192">On the **Add a backend pool** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="ea964-192">On the **Add a backend pool** page, do the following:</span></span>
   - <span data-ttu-id="ea964-193">For name, type *myBackendPool*, as the name for your backend pool.</span><span class="sxs-lookup"><span data-stu-id="ea964-193">For name, type *myBackendPool*, as the name for your backend pool.</span></span>
   - <span data-ttu-id="ea964-194">For **Virtual network**, select *myVNet*.</span><span class="sxs-lookup"><span data-stu-id="ea964-194">For **Virtual network**, select *myVNet*.</span></span>
   - <span data-ttu-id="ea964-195">Add *myVM1* and *my VM2* under **Virtual Machine** along with their corresponding IP addresses, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="ea964-195">Add *myVM1* and *my VM2* under **Virtual Machine** along with their corresponding IP addresses, and then select **Add**.</span></span>
    - <span data-ttu-id="ea964-196">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-196">Click **OK**.</span></span>

3. <span data-ttu-id="ea964-197">Check to make sure your load balancer backend pool setting displays both the VMs **VM1** and **VM2**.</span><span class="sxs-lookup"><span data-stu-id="ea964-197">Check to make sure your load balancer backend pool setting displays both the VMs **VM1** and **VM2**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="ea964-198">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="ea964-198">Create a health probe</span></span>

<span data-ttu-id="ea964-199">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="ea964-199">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="ea964-200">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="ea964-200">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="ea964-201">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="ea964-201">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="ea964-202">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="ea964-202">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="ea964-203">Under **Settings**, click **Health probes**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ea964-203">Under **Settings**, click **Health probes**, then click **Add**.</span></span>
3. <span data-ttu-id="ea964-204">Use these values to create the health probe:</span><span class="sxs-lookup"><span data-stu-id="ea964-204">Use these values to create the health probe:</span></span>
    - <span data-ttu-id="ea964-205">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="ea964-205">*myHealthProbe* - for the name of the health probe.</span></span>
    - <span data-ttu-id="ea964-206">**HTTP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="ea964-206">**HTTP** - for the protocol type.</span></span>
    - <span data-ttu-id="ea964-207">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="ea964-207">*80* - for the port number.</span></span>
    - <span data-ttu-id="ea964-208">*15* - for number of **Interval** in seconds between probe attempts.</span><span class="sxs-lookup"><span data-stu-id="ea964-208">*15* - for number of **Interval** in seconds between probe attempts.</span></span>
    - <span data-ttu-id="ea964-209">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="ea964-209">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span></span>
4. <span data-ttu-id="ea964-210">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-210">Click **OK**.</span></span>

   ![Adding a probe](./media/load-balancer-standard-public-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="ea964-212">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="ea964-212">Create a load balancer rule</span></span>

<span data-ttu-id="ea964-213">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="ea964-213">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="ea964-214">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="ea964-214">You define the frontend IP configuration for the incoming traffic and the backend IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="ea964-215">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="ea964-215">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

1. <span data-ttu-id="ea964-216">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="ea964-216">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="ea964-217">Under **Settings**, click **Load balancing rules**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="ea964-217">Under **Settings**, click **Load balancing rules**, then click **Add**.</span></span>
3. <span data-ttu-id="ea964-218">Use these values to configure the load balancing rule:</span><span class="sxs-lookup"><span data-stu-id="ea964-218">Use these values to configure the load balancing rule:</span></span>
    - <span data-ttu-id="ea964-219">*myHTTPRule* - for the name of the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="ea964-219">*myHTTPRule* - for the name of the load balancing rule.</span></span>
    - <span data-ttu-id="ea964-220">**TCP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="ea964-220">**TCP** - for the protocol type.</span></span>
    - <span data-ttu-id="ea964-221">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="ea964-221">*80* - for the port number.</span></span>
    - <span data-ttu-id="ea964-222">*80* - for the backend port.</span><span class="sxs-lookup"><span data-stu-id="ea964-222">*80* - for the backend port.</span></span>
    - <span data-ttu-id="ea964-223">*myBackendPool* - for the name of the backend pool.</span><span class="sxs-lookup"><span data-stu-id="ea964-223">*myBackendPool* - for the name of the backend pool.</span></span>
    - <span data-ttu-id="ea964-224">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="ea964-224">*myHealthProbe* - for the name of the health probe.</span></span>
4. <span data-ttu-id="ea964-225">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ea964-225">Click **OK**.</span></span>
    
    ![Adding a load balancing rule](./media/load-balancer-standard-public-portal/5-load-balancing-rules.png)

## <a name="test-the-load-balancer"></a><span data-ttu-id="ea964-227">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="ea964-227">Test the load balancer</span></span>
1. <span data-ttu-id="ea964-228">Find the public IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="ea964-228">Find the public IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="ea964-229">Click **All resources** and then click **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="ea964-229">Click **All resources** and then click **myPublicIP**.</span></span>

2. <span data-ttu-id="ea964-230">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="ea964-230">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="ea964-231">The default page of IIS Web server is displayed on the browser.</span><span class="sxs-lookup"><span data-stu-id="ea964-231">The default page of IIS Web server is displayed on the browser.</span></span>

      ![IIS Web server](./media/load-balancer-standard-public-portal/9-load-balancer-test.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ea964-233">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ea964-233">Clean up resources</span></span>

<span data-ttu-id="ea964-234">When no longer needed, delete the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="ea964-234">When no longer needed, delete the resource group, load balancer, and all related resources.</span></span> <span data-ttu-id="ea964-235">To do so, select the resource group that contains the load balancer and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ea964-235">To do so, select the resource group that contains the load balancer and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea964-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea964-236">Next steps</span></span>

<span data-ttu-id="ea964-237">In this quickstart, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-237">In this quickstart, you created a Standard Load Balancer, attached VMs to it, configured the load balancer traffic rule, health probe, and then tested the load balancer.</span></span> <span data-ttu-id="ea964-238">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="ea964-238">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ea964-239">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="ea964-239">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-standard-public-zone-redundant-portal.md)
