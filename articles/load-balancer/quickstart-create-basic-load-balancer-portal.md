---
title: 'Quickstart: Create a public Basic load balancer by using the Azure portal | Microsoft Docs'
description: This quickstart shows how to create a public Basic load balancer by using the Azure portal.
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: I want to create a Basic Load balancer so that I can load balance internet traffic to VMs.
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 7451d6ade7f8b042a68f456e604e2919cacab0a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869334"
---
# <a name="quickstart-create-a-public-basic-load-balancer-by-using-the-azure-portal"></a><span data-ttu-id="1efde-103">Quickstart: Create a public Basic load balancer by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1efde-103">Quickstart: Create a public Basic load balancer by using the Azure portal</span></span>

<span data-ttu-id="1efde-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="1efde-104">Load balancing provides a higher level of availability and scale by spreading incoming requests across multiple virtual machines (VMs).</span></span> <span data-ttu-id="1efde-105">You can use the Azure portal to create a load balancer that will load balance virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1efde-105">You can use the Azure portal to create a load balancer that will load balance virtual machines.</span></span> <span data-ttu-id="1efde-106">This quickstart shows you how to create network resources, back-end servers, and a load balancer at the Basic pricing tier.</span><span class="sxs-lookup"><span data-stu-id="1efde-106">This quickstart shows you how to create network resources, back-end servers, and a load balancer at the Basic pricing tier.</span></span>

<span data-ttu-id="1efde-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1efde-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="sign-in-to-the-azure-portal"></a><span data-ttu-id="1efde-108">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1efde-108">Sign in to the Azure portal</span></span>

<span data-ttu-id="1efde-109">For all the tasks in this quickstart, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1efde-109">For all the tasks in this quickstart, sign in to the [Azure portal](http://portal.azure.com).</span></span>

## <a name="create-a-basic-load-balancer"></a><span data-ttu-id="1efde-110">Create a Basic load balancer</span><span class="sxs-lookup"><span data-stu-id="1efde-110">Create a Basic load balancer</span></span>

<span data-ttu-id="1efde-111">In this section, you create a public Basic load balancer by using the  portal.</span><span class="sxs-lookup"><span data-stu-id="1efde-111">In this section, you create a public Basic load balancer by using the  portal.</span></span> <span data-ttu-id="1efde-112">The public IP address is automatically configured as the load balancer's front end when you create the public IP and the load balancer resource by using the portal.</span><span class="sxs-lookup"><span data-stu-id="1efde-112">The public IP address is automatically configured as the load balancer's front end when you create the public IP and the load balancer resource by using the portal.</span></span> <span data-ttu-id="1efde-113">The name of the front end is **myLoadBalancer**.</span><span class="sxs-lookup"><span data-stu-id="1efde-113">The name of the front end is **myLoadBalancer**.</span></span>

1. <span data-ttu-id="1efde-114">On the upper-left side of the portal, select **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="1efde-114">On the upper-left side of the portal, select **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="1efde-115">In the **Create load balancer** pane, enter these values:</span><span class="sxs-lookup"><span data-stu-id="1efde-115">In the **Create load balancer** pane, enter these values:</span></span>
   - <span data-ttu-id="1efde-116">**myLoadBalancer** for the name of the load balancer</span><span class="sxs-lookup"><span data-stu-id="1efde-116">**myLoadBalancer** for the name of the load balancer</span></span>
   - <span data-ttu-id="1efde-117">**Public** for the type of the load balancer</span><span class="sxs-lookup"><span data-stu-id="1efde-117">**Public** for the type of the load balancer</span></span> 
   - <span data-ttu-id="1efde-118">**myPublicIP** for the public IP that you must create, with **SKU** set as **Basic** and **Assignment** set as **Dynamic**</span><span class="sxs-lookup"><span data-stu-id="1efde-118">**myPublicIP** for the public IP that you must create, with **SKU** set as **Basic** and **Assignment** set as **Dynamic**</span></span>
   - <span data-ttu-id="1efde-119">**myResourceGroupLB** for the name of the new resource group</span><span class="sxs-lookup"><span data-stu-id="1efde-119">**myResourceGroupLB** for the name of the new resource group</span></span>
3. <span data-ttu-id="1efde-120">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1efde-120">Select **Create**.</span></span>
   
![Create a load balancer](./media/load-balancer-get-started-internet-portal/1-load-balancer.png)


## <a name="create-back-end-servers"></a><span data-ttu-id="1efde-122">Create back-end servers</span><span class="sxs-lookup"><span data-stu-id="1efde-122">Create back-end servers</span></span>

<span data-ttu-id="1efde-123">In this section, you create a virtual network, and you create two virtual machines for the back-end pool of your Basic load balancer.</span><span class="sxs-lookup"><span data-stu-id="1efde-123">In this section, you create a virtual network, and you create two virtual machines for the back-end pool of your Basic load balancer.</span></span> <span data-ttu-id="1efde-124">Then you install Internet Information Services (IIS) on the virtual machines to help test the load balancer.</span><span class="sxs-lookup"><span data-stu-id="1efde-124">Then you install Internet Information Services (IIS) on the virtual machines to help test the load balancer.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="1efde-125">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="1efde-125">Create a virtual network</span></span>
1. <span data-ttu-id="1efde-126">On the upper-left side of the portal, select **New** > **Networking** > **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="1efde-126">On the upper-left side of the portal, select **New** > **Networking** > **Virtual network**.</span></span>
2. <span data-ttu-id="1efde-127">In the **Create virtual network** pane, enter these values, and then select **Create**:</span><span class="sxs-lookup"><span data-stu-id="1efde-127">In the **Create virtual network** pane, enter these values, and then select **Create**:</span></span>
   - <span data-ttu-id="1efde-128">**myVnet** for the name of the virtual network</span><span class="sxs-lookup"><span data-stu-id="1efde-128">**myVnet** for the name of the virtual network</span></span>
   - <span data-ttu-id="1efde-129">**myResourceGroupLB** for the name of the existing resource group</span><span class="sxs-lookup"><span data-stu-id="1efde-129">**myResourceGroupLB** for the name of the existing resource group</span></span>
   - <span data-ttu-id="1efde-130">**myBackendSubnet** for the subnet name</span><span class="sxs-lookup"><span data-stu-id="1efde-130">**myBackendSubnet** for the subnet name</span></span>

   ![Create a virtual network](./media/load-balancer-get-started-internet-portal/2-load-balancer-virtual-network.png)

### <a name="create-virtual-machines"></a><span data-ttu-id="1efde-132">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="1efde-132">Create virtual machines</span></span>

1. <span data-ttu-id="1efde-133">On the upper-left side of the portal, select **New** > **Compute** > **Windows Server 2016 Datacenter**.</span><span class="sxs-lookup"><span data-stu-id="1efde-133">On the upper-left side of the portal, select **New** > **Compute** > **Windows Server 2016 Datacenter**.</span></span> 
2. <span data-ttu-id="1efde-134">Enter these values for the virtual machine, and then select **OK**:</span><span class="sxs-lookup"><span data-stu-id="1efde-134">Enter these values for the virtual machine, and then select **OK**:</span></span>
   - <span data-ttu-id="1efde-135">**myVM1** for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="1efde-135">**myVM1** for the name of the virtual machine.</span></span>        
   - <span data-ttu-id="1efde-136">**azureuser** for the administrator username.</span><span class="sxs-lookup"><span data-stu-id="1efde-136">**azureuser** for the administrator username.</span></span>    
   - <span data-ttu-id="1efde-137">**myResourceGroupLB** for the resource group.</span><span class="sxs-lookup"><span data-stu-id="1efde-137">**myResourceGroupLB** for the resource group.</span></span> <span data-ttu-id="1efde-138">(Under **Resource group**, select **Use existing**, and then select **myResourceGroupLB**.)</span><span class="sxs-lookup"><span data-stu-id="1efde-138">(Under **Resource group**, select **Use existing**, and then select **myResourceGroupLB**.)</span></span>   
3. <span data-ttu-id="1efde-139">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="1efde-139">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="1efde-140">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="1efde-140">Enter these values for the VM settings:</span></span>
   - <span data-ttu-id="1efde-141">**myAvailabilitySet** for the name of the new availability set that you create.</span><span class="sxs-lookup"><span data-stu-id="1efde-141">**myAvailabilitySet** for the name of the new availability set that you create.</span></span>
   - <span data-ttu-id="1efde-142">**myVNet** for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1efde-142">**myVNet** for the name of the virtual network.</span></span> <span data-ttu-id="1efde-143">(Ensure that it's selected.)</span><span class="sxs-lookup"><span data-stu-id="1efde-143">(Ensure that it's selected.)</span></span>
   - <span data-ttu-id="1efde-144">**myBackendSubnet** for the name of the subnet.</span><span class="sxs-lookup"><span data-stu-id="1efde-144">**myBackendSubnet** for the name of the subnet.</span></span> <span data-ttu-id="1efde-145">(Ensure that it's selected.)</span><span class="sxs-lookup"><span data-stu-id="1efde-145">(Ensure that it's selected.)</span></span>
   - <span data-ttu-id="1efde-146">**myVM1-ip** for the public IP address.</span><span class="sxs-lookup"><span data-stu-id="1efde-146">**myVM1-ip** for the public IP address.</span></span>
   - <span data-ttu-id="1efde-147">**myNetworkSecurityGroup** for the name of the new network security group (NSG, a type of firewall) that you must create.</span><span class="sxs-lookup"><span data-stu-id="1efde-147">**myNetworkSecurityGroup** for the name of the new network security group (NSG, a type of firewall) that you must create.</span></span>
5. <span data-ttu-id="1efde-148">Select **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="1efde-148">Select **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="1efde-149">Select **OK**, review the settings on the summary page, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="1efde-149">Select **OK**, review the settings on the summary page, and then select **Create**.</span></span>
7. <span data-ttu-id="1efde-150">By using steps 1 to 6, create a second VM named **VM2**, with:</span><span class="sxs-lookup"><span data-stu-id="1efde-150">By using steps 1 to 6, create a second VM named **VM2**, with:</span></span>
   - <span data-ttu-id="1efde-151">**myAvailabilityset** as the availability set.</span><span class="sxs-lookup"><span data-stu-id="1efde-151">**myAvailabilityset** as the availability set.</span></span>
   - <span data-ttu-id="1efde-152">**myVnet** as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="1efde-152">**myVnet** as the virtual network.</span></span>
   - <span data-ttu-id="1efde-153">**myBackendSubnet** as the subnet.</span><span class="sxs-lookup"><span data-stu-id="1efde-153">**myBackendSubnet** as the subnet.</span></span>
   - <span data-ttu-id="1efde-154">**myNetworkSecurityGroup** as the network security group.</span><span class="sxs-lookup"><span data-stu-id="1efde-154">**myNetworkSecurityGroup** as the network security group.</span></span> 

### <a name="create-nsg-rules"></a><span data-ttu-id="1efde-155">Create NSG rules</span><span class="sxs-lookup"><span data-stu-id="1efde-155">Create NSG rules</span></span>

<span data-ttu-id="1efde-156">In this section, you create NSG rules to allow inbound connections that use HTTP and RDP.</span><span class="sxs-lookup"><span data-stu-id="1efde-156">In this section, you create NSG rules to allow inbound connections that use HTTP and RDP.</span></span>

1. <span data-ttu-id="1efde-157">Select **All resources** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="1efde-157">Select **All resources** on the left menu.</span></span> <span data-ttu-id="1efde-158">From the resource list, select **myNetworkSecurityGroup** in the **myResourceGroupLB** resource group.</span><span class="sxs-lookup"><span data-stu-id="1efde-158">From the resource list, select **myNetworkSecurityGroup** in the **myResourceGroupLB** resource group.</span></span>
2. <span data-ttu-id="1efde-159">Under **Settings**, select **Inbound security rules**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1efde-159">Under **Settings**, select **Inbound security rules**, and then select **Add**.</span></span>
3. <span data-ttu-id="1efde-160">Enter the following values for the inbound security rule named **myHTTPRule** to allow for inbound HTTP connections that use port 80.</span><span class="sxs-lookup"><span data-stu-id="1efde-160">Enter the following values for the inbound security rule named **myHTTPRule** to allow for inbound HTTP connections that use port 80.</span></span> <span data-ttu-id="1efde-161">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="1efde-161">Then select **OK**.</span></span>
   - <span data-ttu-id="1efde-162">**Service Tag** for **Source**</span><span class="sxs-lookup"><span data-stu-id="1efde-162">**Service Tag** for **Source**</span></span>
   - <span data-ttu-id="1efde-163">**Internet** for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="1efde-163">**Internet** for **Source service tag**</span></span>
   - <span data-ttu-id="1efde-164">**80** for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="1efde-164">**80** for **Destination port ranges**</span></span>
   - <span data-ttu-id="1efde-165">**TCP** for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="1efde-165">**TCP** for **Protocol**</span></span>
   - <span data-ttu-id="1efde-166">**Allow** for **Action**</span><span class="sxs-lookup"><span data-stu-id="1efde-166">**Allow** for **Action**</span></span>
   - <span data-ttu-id="1efde-167">**100** for **Priority**</span><span class="sxs-lookup"><span data-stu-id="1efde-167">**100** for **Priority**</span></span>
   - <span data-ttu-id="1efde-168">**myHTTPRule** for **Name**</span><span class="sxs-lookup"><span data-stu-id="1efde-168">**myHTTPRule** for **Name**</span></span>
   - <span data-ttu-id="1efde-169">**Allow HTTP** for **Description**</span><span class="sxs-lookup"><span data-stu-id="1efde-169">**Allow HTTP** for **Description**</span></span>
 
   ![Create an NSG rule](./media/load-balancer-get-started-internet-portal/8-load-balancer-nsg-rules.png)
4. <span data-ttu-id="1efde-171">Repeat steps 2 and 3 to create another rule named **myRDPRule** to allow for an inbound RDP connection through port 3389.</span><span class="sxs-lookup"><span data-stu-id="1efde-171">Repeat steps 2 and 3 to create another rule named **myRDPRule** to allow for an inbound RDP connection through port 3389.</span></span> <span data-ttu-id="1efde-172">Use the following values:</span><span class="sxs-lookup"><span data-stu-id="1efde-172">Use the following values:</span></span>
   - <span data-ttu-id="1efde-173">**Service Tag** for **Source**</span><span class="sxs-lookup"><span data-stu-id="1efde-173">**Service Tag** for **Source**</span></span>
   - <span data-ttu-id="1efde-174">**Internet** for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="1efde-174">**Internet** for **Source service tag**</span></span>
   - <span data-ttu-id="1efde-175">**3389** for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="1efde-175">**3389** for **Destination port ranges**</span></span>
   - <span data-ttu-id="1efde-176">**TCP** for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="1efde-176">**TCP** for **Protocol**</span></span>
   - <span data-ttu-id="1efde-177">**Allow** for **Action**</span><span class="sxs-lookup"><span data-stu-id="1efde-177">**Allow** for **Action**</span></span>
   - <span data-ttu-id="1efde-178">**200** for **Priority**</span><span class="sxs-lookup"><span data-stu-id="1efde-178">**200** for **Priority**</span></span>
   - <span data-ttu-id="1efde-179">**myRDPRule** for **Name**</span><span class="sxs-lookup"><span data-stu-id="1efde-179">**myRDPRule** for **Name**</span></span>
   - <span data-ttu-id="1efde-180">**Allow RDP** for **Description**</span><span class="sxs-lookup"><span data-stu-id="1efde-180">**Allow RDP** for **Description**</span></span>

   

### <a name="install-iis"></a><span data-ttu-id="1efde-181">Install IIS</span><span class="sxs-lookup"><span data-stu-id="1efde-181">Install IIS</span></span>

1. <span data-ttu-id="1efde-182">Select **All resources** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="1efde-182">Select **All resources** on the left menu.</span></span> <span data-ttu-id="1efde-183">From the resource list, select **myVM1** in the **myResourceGroupLB** resource group.</span><span class="sxs-lookup"><span data-stu-id="1efde-183">From the resource list, select **myVM1** in the **myResourceGroupLB** resource group.</span></span>
2. <span data-ttu-id="1efde-184">On the **Overview** page, select **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="1efde-184">On the **Overview** page, select **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="1efde-185">Sign in to the VM with username **azureuser** and password **Azure123456!**.</span><span class="sxs-lookup"><span data-stu-id="1efde-185">Sign in to the VM with username **azureuser** and password **Azure123456!**.</span></span>
4. <span data-ttu-id="1efde-186">On the server desktop, browse to **Windows Administrative Tools** > **Server Manager**.</span><span class="sxs-lookup"><span data-stu-id="1efde-186">On the server desktop, browse to **Windows Administrative Tools** > **Server Manager**.</span></span>
5. <span data-ttu-id="1efde-187">In Server Manager, select **Manage**, and then select **Add Roles and features**.</span><span class="sxs-lookup"><span data-stu-id="1efde-187">In Server Manager, select **Manage**, and then select **Add Roles and features**.</span></span>
   <span data-ttu-id="1efde-188">![Adding server manager role](./media/load-balancer-get-started-internet-portal/servermanager.png)</span><span class="sxs-lookup"><span data-stu-id="1efde-188">![Adding server manager role](./media/load-balancer-get-started-internet-portal/servermanager.png)</span></span>
6. <span data-ttu-id="1efde-189">In the Add Roles and Features Wizard, use the following values:</span><span class="sxs-lookup"><span data-stu-id="1efde-189">In the Add Roles and Features Wizard, use the following values:</span></span>
   - <span data-ttu-id="1efde-190">On the **Select installation type** page, select **Role-based or feature-based installation**.</span><span class="sxs-lookup"><span data-stu-id="1efde-190">On the **Select installation type** page, select **Role-based or feature-based installation**.</span></span>
   - <span data-ttu-id="1efde-191">On the **Select destination server** page, select **myVM1**.</span><span class="sxs-lookup"><span data-stu-id="1efde-191">On the **Select destination server** page, select **myVM1**.</span></span>
   - <span data-ttu-id="1efde-192">On the **Select server role** page, select **Web Server (IIS)**.</span><span class="sxs-lookup"><span data-stu-id="1efde-192">On the **Select server role** page, select **Web Server (IIS)**.</span></span>
   - <span data-ttu-id="1efde-193">Follow the instructions to complete the rest of the wizard.</span><span class="sxs-lookup"><span data-stu-id="1efde-193">Follow the instructions to complete the rest of the wizard.</span></span> 
7. <span data-ttu-id="1efde-194">Repeat steps 1 to 6 for the virtual machine **myVM2**.</span><span class="sxs-lookup"><span data-stu-id="1efde-194">Repeat steps 1 to 6 for the virtual machine **myVM2**.</span></span>

## <a name="create-resources-for-the-basic-load-balancer"></a><span data-ttu-id="1efde-195">Create resources for the Basic load balancer</span><span class="sxs-lookup"><span data-stu-id="1efde-195">Create resources for the Basic load balancer</span></span>

<span data-ttu-id="1efde-196">In this section, you configure load balancer settings for a back-end address pool and a health probe.</span><span class="sxs-lookup"><span data-stu-id="1efde-196">In this section, you configure load balancer settings for a back-end address pool and a health probe.</span></span> <span data-ttu-id="1efde-197">You also specify load balancer and NAT rules.</span><span class="sxs-lookup"><span data-stu-id="1efde-197">You also specify load balancer and NAT rules.</span></span>


### <a name="create-a-back-end-address-pool"></a><span data-ttu-id="1efde-198">Create a back-end address pool</span><span class="sxs-lookup"><span data-stu-id="1efde-198">Create a back-end address pool</span></span>

<span data-ttu-id="1efde-199">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual NICs that are connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="1efde-199">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual NICs that are connected to the load balancer.</span></span> <span data-ttu-id="1efde-200">Create the back-end address pool **myBackendPool** to include **VM1** and **VM2**.</span><span class="sxs-lookup"><span data-stu-id="1efde-200">Create the back-end address pool **myBackendPool** to include **VM1** and **VM2**.</span></span>

1. <span data-ttu-id="1efde-201">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span><span class="sxs-lookup"><span data-stu-id="1efde-201">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span></span>
2. <span data-ttu-id="1efde-202">Under **Settings**, select **Backend pools**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1efde-202">Under **Settings**, select **Backend pools**, and then select **Add**.</span></span>
3. <span data-ttu-id="1efde-203">On the **Add a backend pool** page, do the following, and then select **OK**:</span><span class="sxs-lookup"><span data-stu-id="1efde-203">On the **Add a backend pool** page, do the following, and then select **OK**:</span></span>
   - <span data-ttu-id="1efde-204">For **Name**, enter **myBackEndPool**.</span><span class="sxs-lookup"><span data-stu-id="1efde-204">For **Name**, enter **myBackEndPool**.</span></span>
   - <span data-ttu-id="1efde-205">For **Associated to**, from the drop-down menu, select **Availability set**.</span><span class="sxs-lookup"><span data-stu-id="1efde-205">For **Associated to**, from the drop-down menu, select **Availability set**.</span></span>
   - <span data-ttu-id="1efde-206">For **Availability set**, select **myAvailabilitySet**.</span><span class="sxs-lookup"><span data-stu-id="1efde-206">For **Availability set**, select **myAvailabilitySet**.</span></span>
   - <span data-ttu-id="1efde-207">Select **Add a target network IP configuration** to add each virtual machine (**myVM1** and **myVM2**) that you created to the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="1efde-207">Select **Add a target network IP configuration** to add each virtual machine (**myVM1** and **myVM2**) that you created to the back-end pool.</span></span>

   ![Adding to the back-end address pool](./media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="1efde-209">Make sure that your load balancer's back-end pool setting displays both the VMs **VM1** and **VM2**.</span><span class="sxs-lookup"><span data-stu-id="1efde-209">Make sure that your load balancer's back-end pool setting displays both the VMs **VM1** and **VM2**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="1efde-210">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="1efde-210">Create a health probe</span></span>

<span data-ttu-id="1efde-211">To allow the Basic load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="1efde-211">To allow the Basic load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="1efde-212">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="1efde-212">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="1efde-213">Create a health probe named **myHealthProbe** to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="1efde-213">Create a health probe named **myHealthProbe** to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="1efde-214">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span><span class="sxs-lookup"><span data-stu-id="1efde-214">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span></span>
2. <span data-ttu-id="1efde-215">Under **Settings**, select **Health probes**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1efde-215">Under **Settings**, select **Health probes**, and then select **Add**.</span></span>
3. <span data-ttu-id="1efde-216">Use these values, and then select **OK**:</span><span class="sxs-lookup"><span data-stu-id="1efde-216">Use these values, and then select **OK**:</span></span>
   - <span data-ttu-id="1efde-217">**myHealthProbe** for the name of the health probe</span><span class="sxs-lookup"><span data-stu-id="1efde-217">**myHealthProbe** for the name of the health probe</span></span>
   - <span data-ttu-id="1efde-218">**HTTP** for the protocol type</span><span class="sxs-lookup"><span data-stu-id="1efde-218">**HTTP** for the protocol type</span></span>
   - <span data-ttu-id="1efde-219">**80** for the port number</span><span class="sxs-lookup"><span data-stu-id="1efde-219">**80** for the port number</span></span>
   - <span data-ttu-id="1efde-220">**15** for **Interval**, the number of seconds between probe attempts</span><span class="sxs-lookup"><span data-stu-id="1efde-220">**15** for **Interval**, the number of seconds between probe attempts</span></span>
   - <span data-ttu-id="1efde-221">**2** for **Unhealthy threshold**, the number of consecutive probe failures that must occur before a VM is considered unhealthy</span><span class="sxs-lookup"><span data-stu-id="1efde-221">**2** for **Unhealthy threshold**, the number of consecutive probe failures that must occur before a VM is considered unhealthy</span></span>

   ![Adding a probe](./media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="1efde-223">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="1efde-223">Create a load balancer rule</span></span>

<span data-ttu-id="1efde-224">You use a load balancer rule to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="1efde-224">You use a load balancer rule to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="1efde-225">You define the frontend IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="1efde-225">You define the frontend IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> 

<span data-ttu-id="1efde-226">Create a load balancer rule named **myLoadBalancerRuleWeb** for listening to port 80 in the front end **LoadBalancerFrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="1efde-226">Create a load balancer rule named **myLoadBalancerRuleWeb** for listening to port 80 in the front end **LoadBalancerFrontEnd**.</span></span> <span data-ttu-id="1efde-227">The rule is also for sending load-balanced network traffic to the back-end address pool **myBackEndPool**, also by using port 80.</span><span class="sxs-lookup"><span data-stu-id="1efde-227">The rule is also for sending load-balanced network traffic to the back-end address pool **myBackEndPool**, also by using port 80.</span></span> 

1. <span data-ttu-id="1efde-228">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span><span class="sxs-lookup"><span data-stu-id="1efde-228">Select **All resources** on the left menu, and then select **myLoadBalancer** from the resource list.</span></span>
2. <span data-ttu-id="1efde-229">Under **Settings**, select **Load balancing rules**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="1efde-229">Under **Settings**, select **Load balancing rules**, and then select **Add**.</span></span>
3. <span data-ttu-id="1efde-230">Use these values, and then select **OK**:</span><span class="sxs-lookup"><span data-stu-id="1efde-230">Use these values, and then select **OK**:</span></span>
   - <span data-ttu-id="1efde-231">**myHTTPRule** for the name of the load balancer rule</span><span class="sxs-lookup"><span data-stu-id="1efde-231">**myHTTPRule** for the name of the load balancer rule</span></span>
   - <span data-ttu-id="1efde-232">**TCP** for the protocol type</span><span class="sxs-lookup"><span data-stu-id="1efde-232">**TCP** for the protocol type</span></span>
   - <span data-ttu-id="1efde-233">**80** for the port number</span><span class="sxs-lookup"><span data-stu-id="1efde-233">**80** for the port number</span></span>
   - <span data-ttu-id="1efde-234">**80** for the back-end port</span><span class="sxs-lookup"><span data-stu-id="1efde-234">**80** for the back-end port</span></span>
   - <span data-ttu-id="1efde-235">**myBackendPool** for the name of the back-end pool</span><span class="sxs-lookup"><span data-stu-id="1efde-235">**myBackendPool** for the name of the back-end pool</span></span>
   - <span data-ttu-id="1efde-236">**myHealthProbe** for the name of the health probe</span><span class="sxs-lookup"><span data-stu-id="1efde-236">**myHealthProbe** for the name of the health probe</span></span>
    
   ![Adding a load balancer rule](./media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

## <a name="test-the-load-balancer"></a><span data-ttu-id="1efde-238">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="1efde-238">Test the load balancer</span></span>
1. <span data-ttu-id="1efde-239">Find the public IP address for the load balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="1efde-239">Find the public IP address for the load balancer on the **Overview** screen.</span></span> <span data-ttu-id="1efde-240">Select **All resources**, and then select **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="1efde-240">Select **All resources**, and then select **myPublicIP**.</span></span>

2. <span data-ttu-id="1efde-241">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="1efde-241">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="1efde-242">The default page of IIS web server is displayed in the browser.</span><span class="sxs-lookup"><span data-stu-id="1efde-242">The default page of IIS web server is displayed in the browser.</span></span>

   ![IIS web server](./media/load-balancer-get-started-internet-portal/9-load-balancer-test.png)

## <a name="clean-up-resources"></a><span data-ttu-id="1efde-244">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1efde-244">Clean up resources</span></span>

<span data-ttu-id="1efde-245">You can delete the resource group, load balancer, and all related resources when you no longer need them.</span><span class="sxs-lookup"><span data-stu-id="1efde-245">You can delete the resource group, load balancer, and all related resources when you no longer need them.</span></span> <span data-ttu-id="1efde-246">Select the resource group that contains the load balancer, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="1efde-246">Select the resource group that contains the load balancer, and select **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1efde-247">Next steps</span><span class="sxs-lookup"><span data-stu-id="1efde-247">Next steps</span></span>

<span data-ttu-id="1efde-248">In this quickstart, you created a resource group, network resources, and back-end servers.</span><span class="sxs-lookup"><span data-stu-id="1efde-248">In this quickstart, you created a resource group, network resources, and back-end servers.</span></span> <span data-ttu-id="1efde-249">You then used those resources to create a Basic Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1efde-249">You then used those resources to create a Basic Load Balancer.</span></span> <span data-ttu-id="1efde-250">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="1efde-250">To learn more about Azure Load Balancer, continue to the tutorials for Azure Load Balancer.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1efde-251">Azure Load Balancer tutorials</span><span class="sxs-lookup"><span data-stu-id="1efde-251">Azure Load Balancer tutorials</span></span>](tutorial-load-balancer-basic-internal-portal.md)
