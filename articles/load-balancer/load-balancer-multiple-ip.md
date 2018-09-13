---
title: Load balancing on multiple IP configurations in Azure| Microsoft Docs
description: Load balancing across primary and secondary IP configurations.
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: na
ms.assetid: 244907cd-b275-4494-aaf7-dcfc4d93edfe
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: kumud
ms.openlocfilehash: fe700c12d3d03b61e004438e7140df615dd0f38a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564512"
---
# <a name="load-balancing-on-multiple-ip-configurations-using-the-azure-portal"></a><span data-ttu-id="28d86-103">Load balancing on multiple IP configurations using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="28d86-103">Load balancing on multiple IP configurations using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Portal](load-balancer-multiple-ip.md)
> * [PowerShell](load-balancer-multiple-ip-powershell.md)
> * [CLI](load-balancer-multiple-ip-cli.md)

<span data-ttu-id="28d86-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span><span class="sxs-lookup"><span data-stu-id="28d86-107">This article describes how to use Azure Load Balancer with multiple IP addresses on a secondary network interface (NIC).For this scenario, we have two VMs running Windows, each with a primary and a secondary NIC.</span></span> <span data-ttu-id="28d86-108">Each of the secondary NICs have two IP configurations.</span><span class="sxs-lookup"><span data-stu-id="28d86-108">Each of the secondary NICs have two IP configurations.</span></span> <span data-ttu-id="28d86-109">Each VM hosts both websites contoso.com and fabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="28d86-109">Each VM hosts both websites contoso.com and fabrikam.com.</span></span> <span data-ttu-id="28d86-110">Each website is bound to one of the IP configurations on the secondary NIC.</span><span class="sxs-lookup"><span data-stu-id="28d86-110">Each website is bound to one of the IP configurations on the secondary NIC.</span></span> <span data-ttu-id="28d86-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span><span class="sxs-lookup"><span data-stu-id="28d86-111">We use Azure Load Balancer to expose two frontend IP addresses, one for each website, to distribute traffic to the respective IP configuration for the website.</span></span> <span data-ttu-id="28d86-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span><span class="sxs-lookup"><span data-stu-id="28d86-112">This scenario uses the same port number across both frontends, as well as both backend pool IP addresses.</span></span>

![LB scenario image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-multiple-ip/lb-multi-ip.PNG)

##<a name="prerequisites"></a><span data-ttu-id="28d86-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="28d86-114">Prerequisites</span></span>
<span data-ttu-id="28d86-115">This example assumes that you have a Resource Group named *contosofabrikam* with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="28d86-115">This example assumes that you have a Resource Group named *contosofabrikam* with the following configuration:</span></span>
 -  <span data-ttu-id="28d86-116">includes a virtual network named *myVNet*, two VMs called *VM1* and *VM2* respectively within the same availability set named *myAvailset*.</span><span class="sxs-lookup"><span data-stu-id="28d86-116">includes a virtual network named *myVNet*, two VMs called *VM1* and *VM2* respectively within the same availability set named *myAvailset*.</span></span> 
 - <span data-ttu-id="28d86-117">each VM has a primary NIC and a secondary NIC.</span><span class="sxs-lookup"><span data-stu-id="28d86-117">each VM has a primary NIC and a secondary NIC.</span></span> <span data-ttu-id="28d86-118">The primary NICs are named *VM1NIC1* and *VM2NIC1* and the secondary NICs are named *VM1NIC2* and *VM2NIC2*.</span><span class="sxs-lookup"><span data-stu-id="28d86-118">The primary NICs are named *VM1NIC1* and *VM2NIC1* and the secondary NICs are named *VM1NIC2* and *VM2NIC2*.</span></span> <span data-ttu-id="28d86-119">For more information about creating VMs with multiple NICs, see [Create a VM with multiple NICs using PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="28d86-119">For more information about creating VMs with multiple NICs, see [Create a VM with multiple NICs using PowerShell](../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="steps-to-load-balance-on-multiple-ip-configurations"></a><span data-ttu-id="28d86-120">Steps to load balance on multiple IP configurations</span><span class="sxs-lookup"><span data-stu-id="28d86-120">Steps to load balance on multiple IP configurations</span></span>

<span data-ttu-id="28d86-121">Follow these steps below to achieve the scenario outlined in this article:</span><span class="sxs-lookup"><span data-stu-id="28d86-121">Follow these steps below to achieve the scenario outlined in this article:</span></span>

### <a name="step-1-configure-the-secondary-nics-for-each-vm"></a><span data-ttu-id="28d86-122">STEP 1: Configure the secondary NICs for each VM</span><span class="sxs-lookup"><span data-stu-id="28d86-122">STEP 1: Configure the secondary NICs for each VM</span></span>

<span data-ttu-id="28d86-123">For each VM in your virtual network, add set IP configuration for the secondary NIC as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-123">For each VM in your virtual network, add set IP configuration for the secondary NIC as follows:</span></span>  

1. <span data-ttu-id="28d86-124">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="28d86-124">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="28d86-125">On the top left-hand side of the screen, click the Resource Group icon, and then click the resource group the VMs are located in (for example, *contosofabrikam*).</span><span class="sxs-lookup"><span data-stu-id="28d86-125">On the top left-hand side of the screen, click the Resource Group icon, and then click the resource group the VMs are located in (for example, *contosofabrikam*).</span></span> <span data-ttu-id="28d86-126">The **Resource groups** blade that lists all the resources along with the network interfaces for the VMs is now displayed.</span><span class="sxs-lookup"><span data-stu-id="28d86-126">The **Resource groups** blade that lists all the resources along with the network interfaces for the VMs is now displayed.</span></span>
3. <span data-ttu-id="28d86-127">To the secondary NIC of each VM, add an IP configuration as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-127">To the secondary NIC of each VM, add an IP configuration as follows:</span></span>
    1. <span data-ttu-id="28d86-128">Select the network interface you want to add the IP configuration to.</span><span class="sxs-lookup"><span data-stu-id="28d86-128">Select the network interface you want to add the IP configuration to.</span></span>
    2. <span data-ttu-id="28d86-129">In the blade that appears for the NIC that you selected, click **IP configurations**.</span><span class="sxs-lookup"><span data-stu-id="28d86-129">In the blade that appears for the NIC that you selected, click **IP configurations**.</span></span> <span data-ttu-id="28d86-130">Then click **Add** towards the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-130">Then click **Add** towards the top of the blade that shows up.</span></span>
    3. <span data-ttu-id="28d86-131">In the **Add IP configurations** blade, add a second IP configuration to the NIC as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-131">In the **Add IP configurations** blade, add a second IP configuration to the NIC as follows:</span></span> 
        1. <span data-ttu-id="28d86-132">Type a name for your secondary IP configuration (for example, for VM1 and VM2 name the IP configurations as *VM1NIC2-ipconfig2* and *VM2NIC2-ipconfig2* respectively).</span><span class="sxs-lookup"><span data-stu-id="28d86-132">Type a name for your secondary IP configuration (for example, for VM1 and VM2 name the IP configurations as *VM1NIC2-ipconfig2* and *VM2NIC2-ipconfig2* respectively).</span></span>
        2. <span data-ttu-id="28d86-133">For **Private IP address**, for **Allocation**, select **Static**.</span><span class="sxs-lookup"><span data-stu-id="28d86-133">For **Private IP address**, for **Allocation**, select **Static**.</span></span>
        3. <span data-ttu-id="28d86-134">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-134">Click **OK**.</span></span>
        4. <span data-ttu-id="28d86-135">When the second IP configuration for the secondary NIC is complete, it is displayed in the **IP configurations** settings blade for the given NIC.</span><span class="sxs-lookup"><span data-stu-id="28d86-135">When the second IP configuration for the secondary NIC is complete, it is displayed in the **IP configurations** settings blade for the given NIC.</span></span>

### <a name="step-2-create-a-load-balancer"></a><span data-ttu-id="28d86-136">STEP 2: Create a load balancer</span><span class="sxs-lookup"><span data-stu-id="28d86-136">STEP 2: Create a load balancer</span></span>

<span data-ttu-id="28d86-137">Create a load balancer as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-137">Create a load balancer as follows:</span></span>

1. <span data-ttu-id="28d86-138">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="28d86-138">From a browser navigate to the Azure portal: http://portal.azure.com and login with your Azure account.</span></span>
2. <span data-ttu-id="28d86-139">On the top left-hand side of the screen, click **New** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="28d86-139">On the top left-hand side of the screen, click **New** > **Networking** > **Load Balancer**.</span></span> <span data-ttu-id="28d86-140">Next, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="28d86-140">Next, click **Create**.</span></span>
3. <span data-ttu-id="28d86-141">In the **Create load balancer** blade, type a name for your load balancer.</span><span class="sxs-lookup"><span data-stu-id="28d86-141">In the **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="28d86-142">Here it is called *mylb*.</span><span class="sxs-lookup"><span data-stu-id="28d86-142">Here it is called *mylb*.</span></span>
4. <span data-ttu-id="28d86-143">Under Public IP address, create a new public IP called **PublicIP1**.</span><span class="sxs-lookup"><span data-stu-id="28d86-143">Under Public IP address, create a new public IP called **PublicIP1**.</span></span>
5. <span data-ttu-id="28d86-144">Under Resource Group, select the existing Resource group of your VMs (for example, *contosofabrikam*).</span><span class="sxs-lookup"><span data-stu-id="28d86-144">Under Resource Group, select the existing Resource group of your VMs (for example, *contosofabrikam*).</span></span> <span data-ttu-id="28d86-145">Then, select an appropriate location, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-145">Then, select an appropriate location, and then click **OK**.</span></span> <span data-ttu-id="28d86-146">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span><span class="sxs-lookup"><span data-stu-id="28d86-146">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span></span>
6. <span data-ttu-id="28d86-147">Once deployed, the load balancer is displayed as a resource in your Resource Group.</span><span class="sxs-lookup"><span data-stu-id="28d86-147">Once deployed, the load balancer is displayed as a resource in your Resource Group.</span></span>

### <a name="step-3-configure-the-frontend-ip-pool"></a><span data-ttu-id="28d86-148">STEP 3: Configure the frontend IP pool</span><span class="sxs-lookup"><span data-stu-id="28d86-148">STEP 3: Configure the frontend IP pool</span></span>

<span data-ttu-id="28d86-149">Configure your frontend IP pool for each website (Contoso and Fabrikam) as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-149">Configure your frontend IP pool for each website (Contoso and Fabrikam) as follows:</span></span>

1. <span data-ttu-id="28d86-150">In the portal, click **More services** > type **Public IP address** in the filter box, and then click **Public IP addresses**.</span><span class="sxs-lookup"><span data-stu-id="28d86-150">In the portal, click **More services** > type **Public IP address** in the filter box, and then click **Public IP addresses**.</span></span> <span data-ttu-id="28d86-151">Click **Add** towards the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-151">Click **Add** towards the top of the blade that shows up.</span></span>
2. <span data-ttu-id="28d86-152">Configure two Public IP addresses (*PublicIP1* and *PublicIP2*) for both websites (contoso and fabrikam) as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-152">Configure two Public IP addresses (*PublicIP1* and *PublicIP2*) for both websites (contoso and fabrikam) as follows:</span></span>
    1. <span data-ttu-id="28d86-153">Type a name for your frontend IP address.</span><span class="sxs-lookup"><span data-stu-id="28d86-153">Type a name for your frontend IP address.</span></span>
    2. <span data-ttu-id="28d86-154">For **Resource Group**, select the existing Resource Group of the VMs (for example, *contosofabrikam*).</span><span class="sxs-lookup"><span data-stu-id="28d86-154">For **Resource Group**, select the existing Resource Group of the VMs (for example, *contosofabrikam*).</span></span>
    3. <span data-ttu-id="28d86-155">For **Location**, select the same location as the VMs.</span><span class="sxs-lookup"><span data-stu-id="28d86-155">For **Location**, select the same location as the VMs.</span></span>
    4. <span data-ttu-id="28d86-156">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-156">Click **OK**.</span></span>
    5. <span data-ttu-id="28d86-157">Once the two Public IP addresses are created, they are both displayed in the **Public IP** addresses blade.</span><span class="sxs-lookup"><span data-stu-id="28d86-157">Once the two Public IP addresses are created, they are both displayed in the **Public IP** addresses blade.</span></span>
3. <span data-ttu-id="28d86-158">In the portal, click **More services** > type **load balancer** in the filter box, and then click **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="28d86-158">In the portal, click **More services** > type **load balancer** in the filter box, and then click **Load Balancer**.</span></span>  
4. <span data-ttu-id="28d86-159">Select the load balancer (*mylb*) that you want to add the frontend IP pool to.</span><span class="sxs-lookup"><span data-stu-id="28d86-159">Select the load balancer (*mylb*) that you want to add the frontend IP pool to.</span></span>
5. <span data-ttu-id="28d86-160">Under **Settings**, select **Frontend Pools**.</span><span class="sxs-lookup"><span data-stu-id="28d86-160">Under **Settings**, select **Frontend Pools**.</span></span> <span data-ttu-id="28d86-161">Then click **Add** towards the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-161">Then click **Add** towards the top of the blade that shows up.</span></span>
6. <span data-ttu-id="28d86-162">Type a name for your frontend IP address (*farbikamfe* or \**contosofe*).</span><span class="sxs-lookup"><span data-stu-id="28d86-162">Type a name for your frontend IP address (*farbikamfe* or \**contosofe*).</span></span>
7. <span data-ttu-id="28d86-163">Click **IP address** and on the **Choose Public IP address** blade, select the IP addresses for your frontend (*PublicIP1* or *PublicIP2*).</span><span class="sxs-lookup"><span data-stu-id="28d86-163">Click **IP address** and on the **Choose Public IP address** blade, select the IP addresses for your frontend (*PublicIP1* or *PublicIP2*).</span></span>
8. <span data-ttu-id="28d86-164">Repeat steps 3 to 7 within this section to create the second frontend IP address.</span><span class="sxs-lookup"><span data-stu-id="28d86-164">Repeat steps 3 to 7 within this section to create the second frontend IP address.</span></span>
9. <span data-ttu-id="28d86-165">When the frontend IP pool configuration is complete, both frontend IP addresses are displayed in the **Frontend IP Pool** blade of your load balancer.</span><span class="sxs-lookup"><span data-stu-id="28d86-165">When the frontend IP pool configuration is complete, both frontend IP addresses are displayed in the **Frontend IP Pool** blade of your load balancer.</span></span> 
    
### <a name="step-4-configure-the-backend-pool"></a><span data-ttu-id="28d86-166">STEP 4: Configure the backend pool</span><span class="sxs-lookup"><span data-stu-id="28d86-166">STEP 4: Configure the backend pool</span></span>   
<span data-ttu-id="28d86-167">Configure the backend address pools on your load balancer for each website (Contoso and Fabrikam) as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-167">Configure the backend address pools on your load balancer for each website (Contoso and Fabrikam) as follows:</span></span>
        
1. <span data-ttu-id="28d86-168">In the portal, click **More services** > type load balancer in the filter box, and then click **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="28d86-168">In the portal, click **More services** > type load balancer in the filter box, and then click **Load Balancer**.</span></span>  
2. <span data-ttu-id="28d86-169">Select the load balancer (*mylb*) that you want to add the backend pools to.</span><span class="sxs-lookup"><span data-stu-id="28d86-169">Select the load balancer (*mylb*) that you want to add the backend pools to.</span></span>
3. <span data-ttu-id="28d86-170">Under **Settings**, select **Backend Pools**.</span><span class="sxs-lookup"><span data-stu-id="28d86-170">Under **Settings**, select **Backend Pools**.</span></span> <span data-ttu-id="28d86-171">Type a name for your backend pool (for example, *contosopool* or *fabrikampool*).</span><span class="sxs-lookup"><span data-stu-id="28d86-171">Type a name for your backend pool (for example, *contosopool* or *fabrikampool*).</span></span> <span data-ttu-id="28d86-172">Then click the **Add** button toward the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-172">Then click the **Add** button toward the top of the blade that shows up.</span></span> 
4. <span data-ttu-id="28d86-173">For **Associated to**, select **Availability set**.</span><span class="sxs-lookup"><span data-stu-id="28d86-173">For **Associated to**, select **Availability set**.</span></span>
5. <span data-ttu-id="28d86-174">For **Availability set**, select **myAvailset**.</span><span class="sxs-lookup"><span data-stu-id="28d86-174">For **Availability set**, select **myAvailset**.</span></span>
6. <span data-ttu-id="28d86-175">Add Target network IP configurations, for both VMs as follows (see Figure 2):</span><span class="sxs-lookup"><span data-stu-id="28d86-175">Add Target network IP configurations, for both VMs as follows (see Figure 2):</span></span>  
    1. <span data-ttu-id="28d86-176">For **Target Virtual machine**, select the VM that you want to add to the backend pool (for example, VM1 or VM2).</span><span class="sxs-lookup"><span data-stu-id="28d86-176">For **Target Virtual machine**, select the VM that you want to add to the backend pool (for example, VM1 or VM2).</span></span>
    2. <span data-ttu-id="28d86-177">For **Network IP configuration**, select the secondary NICs IP configuration for that VM (for example, VM1NIC2-ipconfig2 or VM2NIC2-ipconfig2).</span><span class="sxs-lookup"><span data-stu-id="28d86-177">For **Network IP configuration**, select the secondary NICs IP configuration for that VM (for example, VM1NIC2-ipconfig2 or VM2NIC2-ipconfig2).</span></span>
    <span data-ttu-id="28d86-178">![LB scenario image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-multiple-ip/lb-backendpool.png)</span><span class="sxs-lookup"><span data-stu-id="28d86-178">![LB scenario image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-multiple-ip/lb-backendpool.png)</span></span>
            
        <span data-ttu-id="28d86-179">**Figure 2**: Configuring the load balancer with backend pools</span><span class="sxs-lookup"><span data-stu-id="28d86-179">**Figure 2**: Configuring the load balancer with backend pools</span></span>  
7. <span data-ttu-id="28d86-180">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-180">Click **OK**.</span></span>
8. <span data-ttu-id="28d86-181">When the backend pool configuration is complete, both backend address pools are displayed in the **Backend pool blade** of your load balancer.</span><span class="sxs-lookup"><span data-stu-id="28d86-181">When the backend pool configuration is complete, both backend address pools are displayed in the **Backend pool blade** of your load balancer.</span></span>

### <a name="step-5-configure-a-health-probe-for-your-load-balancer"></a><span data-ttu-id="28d86-182">STEP 5: Configure a health probe for your load balancer</span><span class="sxs-lookup"><span data-stu-id="28d86-182">STEP 5: Configure a health probe for your load balancer</span></span>
<span data-ttu-id="28d86-183">Configure a health probe for your load balancer as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-183">Configure a health probe for your load balancer as follows:</span></span>
    1. <span data-ttu-id="28d86-184">In the portal, click More services > type load balancer in the filter box, and then click **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="28d86-184">In the portal, click More services > type load balancer in the filter box, and then click **Load Balancer**.</span></span>  
    2. <span data-ttu-id="28d86-185">Select the load balancer that you want to add the backend pools to.</span><span class="sxs-lookup"><span data-stu-id="28d86-185">Select the load balancer that you want to add the backend pools to.</span></span>
    3. <span data-ttu-id="28d86-186">Under **Settings**, select **Health probe**.</span><span class="sxs-lookup"><span data-stu-id="28d86-186">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="28d86-187">Then click **Add** towards the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-187">Then click **Add** towards the top of the blade that shows up.</span></span>
    4. <span data-ttu-id="28d86-188">Type a name for the health probe (for example, HTTP), and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-188">Type a name for the health probe (for example, HTTP), and click **OK**.</span></span>

### <a name="step-6-configure-load-balancing-rules"></a><span data-ttu-id="28d86-189">STEP 6: Configure load balancing rules</span><span class="sxs-lookup"><span data-stu-id="28d86-189">STEP 6: Configure load balancing rules</span></span>
<span data-ttu-id="28d86-190">Configure load balancing rules (*HTTPc* and *HTTPf*) for each website as follows:</span><span class="sxs-lookup"><span data-stu-id="28d86-190">Configure load balancing rules (*HTTPc* and *HTTPf*) for each website as follows:</span></span>
    
1. <span data-ttu-id="28d86-191">Under **Settings**, select **Health probe**.</span><span class="sxs-lookup"><span data-stu-id="28d86-191">Under **Settings**, select **Health probe**.</span></span> <span data-ttu-id="28d86-192">Then click **Add** towards the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="28d86-192">Then click **Add** towards the top of the blade that shows up.</span></span>
2. <span data-ttu-id="28d86-193">For **Name**, type a name for the load balancing rule (for example, *HTTPc* for Contoso, or *HTTPf* for Fabrikam)</span><span class="sxs-lookup"><span data-stu-id="28d86-193">For **Name**, type a name for the load balancing rule (for example, *HTTPc* for Contoso, or *HTTPf* for Fabrikam)</span></span>
3. <span data-ttu-id="28d86-194">For Frontend IP address, select the the frontend IP address (for example *Contosofe* or *Fabrikamfe*)</span><span class="sxs-lookup"><span data-stu-id="28d86-194">For Frontend IP address, select the the frontend IP address (for example *Contosofe* or *Fabrikamfe*)</span></span>
4. <span data-ttu-id="28d86-195">For **Port** and **Backend port**, keep the default value **80**.</span><span class="sxs-lookup"><span data-stu-id="28d86-195">For **Port** and **Backend port**, keep the default value **80**.</span></span>
5. <span data-ttu-id="28d86-196">For **Floating IP (direct server return)**, click **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="28d86-196">For **Floating IP (direct server return)**, click **Enabled**.</span></span>
6. <span data-ttu-id="28d86-197">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="28d86-197">Click **OK**.</span></span>
7. <span data-ttu-id="28d86-198">Repeat steps 1 to 6 within this section to create the second Load Balancer rule.</span><span class="sxs-lookup"><span data-stu-id="28d86-198">Repeat steps 1 to 6 within this section to create the second Load Balancer rule.</span></span>
8. <span data-ttu-id="28d86-199">When the load balancing rules configuration is complete, both rules ((*HTTPc* and *HTTPf*) are displayed in the **Load balancing rules** blade of your load balancer.</span><span class="sxs-lookup"><span data-stu-id="28d86-199">When the load balancing rules configuration is complete, both rules ((*HTTPc* and *HTTPf*) are displayed in the **Load balancing rules** blade of your load balancer.</span></span>

### <a name="step-7-configure-dns-records"></a><span data-ttu-id="28d86-200">STEP 7: Configure DNS records</span><span class="sxs-lookup"><span data-stu-id="28d86-200">STEP 7: Configure DNS records</span></span>
<span data-ttu-id="28d86-201">Finally, you must configure DNS resource records to point to the respective frontend IP address of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="28d86-201">Finally, you must configure DNS resource records to point to the respective frontend IP address of the load balancer.</span></span> <span data-ttu-id="28d86-202">You may host your domains in Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="28d86-202">You may host your domains in Azure DNS.</span></span> <span data-ttu-id="28d86-203">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span><span class="sxs-lookup"><span data-stu-id="28d86-203">For more information about using Azure DNS with Load Balancer, see [Using Azure DNS with other Azure services](../dns/dns-for-azure-services.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="28d86-204">Next steps</span><span class="sxs-lookup"><span data-stu-id="28d86-204">Next steps</span></span>
- <span data-ttu-id="28d86-205">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span><span class="sxs-lookup"><span data-stu-id="28d86-205">Learn more about how to combine load balancing services in Azure in [Using load-balancing services in Azure](../traffic-manager/traffic-manager-load-balancing-azure.md).</span></span>
- <span data-ttu-id="28d86-206">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span><span class="sxs-lookup"><span data-stu-id="28d86-206">Learn how you can use different types of logs in Azure to manage and troubleshoot load balancer in [Log analytics for Azure Load Balancer](../load-balancer/load-balancer-monitor-log.md).</span></span>

