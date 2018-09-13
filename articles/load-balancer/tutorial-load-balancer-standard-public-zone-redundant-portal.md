---
title: Tutorial:Load Balancer VMs across availability zones - Azure portal | Microsoft Docs
description: This tutorial demonstrates how to create a Standard Load Balancer with zone-redundant frontend to load balance VMs across availability zones using Azure portal
services: load-balancer
documentationcenter: na
author: KumudD
manager: jeconnoc
editor: ''
tags: azure-resource-manager
Customer intent: As an IT administrator, I want to create a load balancer that load balances incoming internet traffic to virtual machines across availability zones in a region, so that the customers can still access the web service if a datacenter is unavailable.
ms.assetid: ''
ms.service: load-balancer
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/17/2018
ms.author: kumud
ms.custom: mvc
ms.openlocfilehash: 5ec1cc42a0c932e47c08493fa632495426abc4c7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867557"
---
# <a name="tutorial-load-balance-vms-across-availability-zones-with-a-standard-load-balancer-using-the-azure-portal"></a><span data-ttu-id="3f62d-103">Tutorial: Load balance VMs across availability zones with a Standard Load Balancer using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="3f62d-103">Tutorial: Load balance VMs across availability zones with a Standard Load Balancer using the Azure portal</span></span>

<span data-ttu-id="3f62d-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span><span class="sxs-lookup"><span data-stu-id="3f62d-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="3f62d-105">This tutorial steps through creating a public Load Balancer Standard that load balances VMs across availability zones.</span><span class="sxs-lookup"><span data-stu-id="3f62d-105">This tutorial steps through creating a public Load Balancer Standard that load balances VMs across availability zones.</span></span> <span data-ttu-id="3f62d-106">This helps to protect your apps and data from an unlikely failure or loss of an entire datacenter.</span><span class="sxs-lookup"><span data-stu-id="3f62d-106">This helps to protect your apps and data from an unlikely failure or loss of an entire datacenter.</span></span> <span data-ttu-id="3f62d-107">With zone-redundancy, one or more availability zones can fail and the data path survives as long as one zone in the region remains healthy.</span><span class="sxs-lookup"><span data-stu-id="3f62d-107">With zone-redundancy, one or more availability zones can fail and the data path survives as long as one zone in the region remains healthy.</span></span> <span data-ttu-id="3f62d-108">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="3f62d-108">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3f62d-109">Create a Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="3f62d-109">Create a Standard Load Balancer</span></span>
> * <span data-ttu-id="3f62d-110">Create network security groups to define incoming traffic rules</span><span class="sxs-lookup"><span data-stu-id="3f62d-110">Create network security groups to define incoming traffic rules</span></span>
> * <span data-ttu-id="3f62d-111">Create zone-redundant VMs across multiple zones and attach to a load balancer</span><span class="sxs-lookup"><span data-stu-id="3f62d-111">Create zone-redundant VMs across multiple zones and attach to a load balancer</span></span>
> * <span data-ttu-id="3f62d-112">Create load balancer health probe</span><span class="sxs-lookup"><span data-stu-id="3f62d-112">Create load balancer health probe</span></span>
> * <span data-ttu-id="3f62d-113">Create load balancer traffic rules</span><span class="sxs-lookup"><span data-stu-id="3f62d-113">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="3f62d-114">Create a basic IIS site</span><span class="sxs-lookup"><span data-stu-id="3f62d-114">Create a basic IIS site</span></span>
> * <span data-ttu-id="3f62d-115">View a load balancer in action</span><span class="sxs-lookup"><span data-stu-id="3f62d-115">View a load balancer in action</span></span>

<span data-ttu-id="3f62d-116">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span><span class="sxs-lookup"><span data-stu-id="3f62d-116">For more information about using Availability zones with Standard Load Balancer, see [Standard Load Balancer and Availability Zones](load-balancer-standard-availability-zones.md).</span></span>

<span data-ttu-id="3f62d-117">If you prefer, you can complete this tutorial using the [Azure CLI](load-balancer-standard-public-zone-redundant-cli.md).</span><span class="sxs-lookup"><span data-stu-id="3f62d-117">If you prefer, you can complete this tutorial using the [Azure CLI](load-balancer-standard-public-zone-redundant-cli.md).</span></span>

<span data-ttu-id="3f62d-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3f62d-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="3f62d-119">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="3f62d-119">Sign in to Azure</span></span>

<span data-ttu-id="3f62d-120">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3f62d-120">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

## <a name="create-a-standard-load-balancer"></a><span data-ttu-id="3f62d-121">Create a Standard Load Balancer</span><span class="sxs-lookup"><span data-stu-id="3f62d-121">Create a Standard Load Balancer</span></span>

<span data-ttu-id="3f62d-122">Standard Load Balancer only supports a Standard Public IP address.</span><span class="sxs-lookup"><span data-stu-id="3f62d-122">Standard Load Balancer only supports a Standard Public IP address.</span></span> <span data-ttu-id="3f62d-123">When you create a new public IP while creating the load balancer, it is automatically configured as a Standard SKU version, and is also automatically zone-redundant.</span><span class="sxs-lookup"><span data-stu-id="3f62d-123">When you create a new public IP while creating the load balancer, it is automatically configured as a Standard SKU version, and is also automatically zone-redundant.</span></span>

1. <span data-ttu-id="3f62d-124">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-124">On the top left-hand side of the screen, click **Create a resource** > **Networking** > **Load Balancer**.</span></span>
2. <span data-ttu-id="3f62d-125">In the **Create a load balancer** page enter these values for the load balancer:</span><span class="sxs-lookup"><span data-stu-id="3f62d-125">In the **Create a load balancer** page enter these values for the load balancer:</span></span>
    - <span data-ttu-id="3f62d-126">*myLoadBalancer* - for the name of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-126">*myLoadBalancer* - for the name of the load balancer.</span></span>
    - <span data-ttu-id="3f62d-127">**Public** - for the type of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-127">**Public** - for the type of the load balancer.</span></span>
     - <span data-ttu-id="3f62d-128">*myPublicIP* - for the new Public IP address that you create.</span><span class="sxs-lookup"><span data-stu-id="3f62d-128">*myPublicIP* - for the new Public IP address that you create.</span></span> <span data-ttu-id="3f62d-129">To do so, click **Choose a public IP address**, and then click **Create new**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-129">To do so, click **Choose a public IP address**, and then click **Create new**.</span></span> <span data-ttu-id="3f62d-130">For name type *myPublicIP*, SKU is Standard by default, and select **Zone-redundant** for **Availability zone**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-130">For name type *myPublicIP*, SKU is Standard by default, and select **Zone-redundant** for **Availability zone**.</span></span>
    - <span data-ttu-id="3f62d-131">*myResourceGroupLBAZ* -  for the name of the new resource group that you create.</span><span class="sxs-lookup"><span data-stu-id="3f62d-131">*myResourceGroupLBAZ* -  for the name of the new resource group that you create.</span></span>
    - <span data-ttu-id="3f62d-132">**westeurope** - for the location.</span><span class="sxs-lookup"><span data-stu-id="3f62d-132">**westeurope** - for the location.</span></span>
3. <span data-ttu-id="3f62d-133">Click **Create** to create the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-133">Click **Create** to create the load balancer.</span></span>
   
    ![Create a load balancer](./media/load-balancer-standard-public-availability-zones-portal/1a-load-balancer.png)


## <a name="create-backend-servers"></a><span data-ttu-id="3f62d-135">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="3f62d-135">Create backend servers</span></span>

<span data-ttu-id="3f62d-136">In this section, you create a virtual network, virtual machines in different zones for the region, and then install IIS on the virtual machines to help test the zone-redundant load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-136">In this section, you create a virtual network, virtual machines in different zones for the region, and then install IIS on the virtual machines to help test the zone-redundant load balancer.</span></span> <span data-ttu-id="3f62d-137">Hence, if a zone fails, the health probe for VM in the same zone fails, and traffic continues to be served by VMs in the other zones.</span><span class="sxs-lookup"><span data-stu-id="3f62d-137">Hence, if a zone fails, the health probe for VM in the same zone fails, and traffic continues to be served by VMs in the other zones.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="3f62d-138">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="3f62d-138">Create a virtual network</span></span>
<span data-ttu-id="3f62d-139">Create a virtual network for deploying your backend servers.</span><span class="sxs-lookup"><span data-stu-id="3f62d-139">Create a virtual network for deploying your backend servers.</span></span>

1. <span data-ttu-id="3f62d-140">On the top left-hand side of the screen click **Create a resource** > **Networking** > **Virtual network** and enter these values for the virtual network:</span><span class="sxs-lookup"><span data-stu-id="3f62d-140">On the top left-hand side of the screen click **Create a resource** > **Networking** > **Virtual network** and enter these values for the virtual network:</span></span>
    - <span data-ttu-id="3f62d-141">*myVnet* - for the name of the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3f62d-141">*myVnet* - for the name of the virtual network.</span></span>
    - <span data-ttu-id="3f62d-142">*myResourceGroupLBAZ* - for the name of the existing resource group</span><span class="sxs-lookup"><span data-stu-id="3f62d-142">*myResourceGroupLBAZ* - for the name of the existing resource group</span></span>
    - <span data-ttu-id="3f62d-143">*myBackendSubnet* - for the subnet name.</span><span class="sxs-lookup"><span data-stu-id="3f62d-143">*myBackendSubnet* - for the subnet name.</span></span>
2. <span data-ttu-id="3f62d-144">Click **Create** to create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3f62d-144">Click **Create** to create the virtual network.</span></span>

    ![Create a virtual network](./media/load-balancer-standard-public-availability-zones-portal/2-load-balancer-virtual-network.png)

## <a name="create-a-network-security-group"></a><span data-ttu-id="3f62d-146">Create a network security group</span><span class="sxs-lookup"><span data-stu-id="3f62d-146">Create a network security group</span></span>

<span data-ttu-id="3f62d-147">Create network security group to define inbound connections to your virtual network.</span><span class="sxs-lookup"><span data-stu-id="3f62d-147">Create network security group to define inbound connections to your virtual network.</span></span>

1. <span data-ttu-id="3f62d-148">On the top left-hand side of the screen, click **Create a resource**, in the search box type *Network Security Group*, and in the network security group page, click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-148">On the top left-hand side of the screen, click **Create a resource**, in the search box type *Network Security Group*, and in the network security group page, click **Create**.</span></span>
2. <span data-ttu-id="3f62d-149">In the Create network security group page, enter these values:</span><span class="sxs-lookup"><span data-stu-id="3f62d-149">In the Create network security group page, enter these values:</span></span>
    - <span data-ttu-id="3f62d-150">*myNetworkSecurityGroup*  - for the name of the network security group.</span><span class="sxs-lookup"><span data-stu-id="3f62d-150">*myNetworkSecurityGroup*  - for the name of the network security group.</span></span>
    - <span data-ttu-id="3f62d-151">*myResourceGroupLBAZ* - for the name of the existing resource group.</span><span class="sxs-lookup"><span data-stu-id="3f62d-151">*myResourceGroupLBAZ* - for the name of the existing resource group.</span></span>
   
![Create a virtual network](./media/load-balancer-standard-public-availability-zones-portal/create-nsg.png)

### <a name="create-network-security-group-rules"></a><span data-ttu-id="3f62d-153">Create network security group rules</span><span class="sxs-lookup"><span data-stu-id="3f62d-153">Create network security group rules</span></span>

<span data-ttu-id="3f62d-154">In this section, you create network security group rules to allow inbound connections using HTTP and RDP using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3f62d-154">In this section, you create network security group rules to allow inbound connections using HTTP and RDP using the Azure portal.</span></span>

1. <span data-ttu-id="3f62d-155">In the Azure portal, click **All resources** in the left-hand menu, and then search and click **myNetworkSecurityGroup** that is located in the **myResourceGroupLBAZ** resource group.</span><span class="sxs-lookup"><span data-stu-id="3f62d-155">In the Azure portal, click **All resources** in the left-hand menu, and then search and click **myNetworkSecurityGroup** that is located in the **myResourceGroupLBAZ** resource group.</span></span>
2. <span data-ttu-id="3f62d-156">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-156">Under **Settings**, click **Inbound security rules**, and then click **Add**.</span></span>
3. <span data-ttu-id="3f62d-157">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span><span class="sxs-lookup"><span data-stu-id="3f62d-157">Enter these values for the inbound security rule named *myHTTPRule* to allow for an inbound HTTP connections using port 80:</span></span>
    - <span data-ttu-id="3f62d-158">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-158">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="3f62d-159">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="3f62d-159">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="3f62d-160">*80* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="3f62d-160">*80* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="3f62d-161">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="3f62d-161">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="3f62d-162">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="3f62d-162">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="3f62d-163">*100* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="3f62d-163">*100* for **Priority**</span></span>
    - <span data-ttu-id="3f62d-164">*myHTTPRule* - for name of the load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="3f62d-164">*myHTTPRule* - for name of the load balancer rule.</span></span>
    - <span data-ttu-id="3f62d-165">*Allow HTTP* - for description of the load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="3f62d-165">*Allow HTTP* - for description of the load balancer rule.</span></span>
4. <span data-ttu-id="3f62d-166">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-166">Click **OK**.</span></span>
 
 ![Create a virtual network](./media/load-balancer-standard-public-availability-zones-portal/8-load-balancer-nsg-rules.png)
5. <span data-ttu-id="3f62d-168">Repeat steps 2 to 4 to create another rule named *myRDPRule* to allow for an inbound RDP connection using port 3389 with the following values:</span><span class="sxs-lookup"><span data-stu-id="3f62d-168">Repeat steps 2 to 4 to create another rule named *myRDPRule* to allow for an inbound RDP connection using port 3389 with the following values:</span></span>
    - <span data-ttu-id="3f62d-169">*Service Tag* - for **Source**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-169">*Service Tag* - for **Source**.</span></span>
    - <span data-ttu-id="3f62d-170">*Internet* - for **Source service tag**</span><span class="sxs-lookup"><span data-stu-id="3f62d-170">*Internet* - for **Source service tag**</span></span>
    - <span data-ttu-id="3f62d-171">*3389* - for **Destination port ranges**</span><span class="sxs-lookup"><span data-stu-id="3f62d-171">*3389* - for **Destination port ranges**</span></span>
    - <span data-ttu-id="3f62d-172">*TCP* - for **Protocol**</span><span class="sxs-lookup"><span data-stu-id="3f62d-172">*TCP* - for **Protocol**</span></span>
    - <span data-ttu-id="3f62d-173">*Allow* - for **Action**</span><span class="sxs-lookup"><span data-stu-id="3f62d-173">*Allow* - for **Action**</span></span>
    - <span data-ttu-id="3f62d-174">*200* for **Priority**</span><span class="sxs-lookup"><span data-stu-id="3f62d-174">*200* for **Priority**</span></span>
    - <span data-ttu-id="3f62d-175">*myRDPRule* for name</span><span class="sxs-lookup"><span data-stu-id="3f62d-175">*myRDPRule* for name</span></span>
    - <span data-ttu-id="3f62d-176">*Allow RDP* - for description</span><span class="sxs-lookup"><span data-stu-id="3f62d-176">*Allow RDP* - for description</span></span>

### <a name="create-virtual-machines"></a><span data-ttu-id="3f62d-177">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="3f62d-177">Create virtual machines</span></span>

<span data-ttu-id="3f62d-178">Create virtual machines in different zones (zone 1, zone 2, and zone 3) for the region that can act as backend servers to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-178">Create virtual machines in different zones (zone 1, zone 2, and zone 3) for the region that can act as backend servers to the load balancer.</span></span>

1. <span data-ttu-id="3f62d-179">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="3f62d-179">On the top left-hand side of the screen, click **Create a resource** > **Compute** > **Windows Server 2016 Datacenter** and enter these values for the virtual machine:</span></span>
    - <span data-ttu-id="3f62d-180">*myVM1* - for the name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="3f62d-180">*myVM1* - for the name of the virtual machine.</span></span>        
    - <span data-ttu-id="3f62d-181">*azureuser* - for the administrator user name.</span><span class="sxs-lookup"><span data-stu-id="3f62d-181">*azureuser* - for the administrator user name.</span></span>    
    - <span data-ttu-id="3f62d-182">*myResourceGroupLBAZ* - for **Resource group**, select **Use existing**, and then select *myResourceGroupLBAZ*.</span><span class="sxs-lookup"><span data-stu-id="3f62d-182">*myResourceGroupLBAZ* - for **Resource group**, select **Use existing**, and then select *myResourceGroupLBAZ*.</span></span>
2. <span data-ttu-id="3f62d-183">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-183">Click **OK**.</span></span>
3. <span data-ttu-id="3f62d-184">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-184">Select **DS1_V2** for the size of the virtual machine, and click **Select**.</span></span>
4. <span data-ttu-id="3f62d-185">Enter these values for the VM settings:</span><span class="sxs-lookup"><span data-stu-id="3f62d-185">Enter these values for the VM settings:</span></span>
    - <span data-ttu-id="3f62d-186">*zone 1* - for the zone where you place the VM.</span><span class="sxs-lookup"><span data-stu-id="3f62d-186">*zone 1* - for the zone where you place the VM.</span></span>
    -  <span data-ttu-id="3f62d-187">*myVNet* - ensure it is selected as the virtual network.</span><span class="sxs-lookup"><span data-stu-id="3f62d-187">*myVNet* - ensure it is selected as the virtual network.</span></span>
    - <span data-ttu-id="3f62d-188">*myBackendSubnet* - ensure it is selected as the subnet.</span><span class="sxs-lookup"><span data-stu-id="3f62d-188">*myBackendSubnet* - ensure it is selected as the subnet.</span></span>
    - <span data-ttu-id="3f62d-189">*myNetworkSecurityGroup* - for the name of network security group (firewall).</span><span class="sxs-lookup"><span data-stu-id="3f62d-189">*myNetworkSecurityGroup* - for the name of network security group (firewall).</span></span>
5. <span data-ttu-id="3f62d-190">Click **Disabled** to disable boot diagnostics.</span><span class="sxs-lookup"><span data-stu-id="3f62d-190">Click **Disabled** to disable boot diagnostics.</span></span>
6. <span data-ttu-id="3f62d-191">Click **OK**, review the settings on the summary page, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-191">Click **OK**, review the settings on the summary page, and then click **Create**.</span></span>
  
 ![Create a virtual machine](./media/load-balancer-standard-public-availability-zones-portal/create-vm-standard-ip.png)

7. <span data-ttu-id="3f62d-193">Create a second VM, named, *VM2* in Zone 2, and third VM in Zone 3, and with *myVnet* as the virtual network, *myBackendSubnet* as the subnet, and \**myNetworkSecurityGroup* as the network security group using steps 1-6.</span><span class="sxs-lookup"><span data-stu-id="3f62d-193">Create a second VM, named, *VM2* in Zone 2, and third VM in Zone 3, and with *myVnet* as the virtual network, *myBackendSubnet* as the subnet, and \**myNetworkSecurityGroup* as the network security group using steps 1-6.</span></span>

### <a name="install-iis-on-vms"></a><span data-ttu-id="3f62d-194">Install IIS on VMs</span><span class="sxs-lookup"><span data-stu-id="3f62d-194">Install IIS on VMs</span></span>

1. <span data-ttu-id="3f62d-195">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupLBAZ* resource group.</span><span class="sxs-lookup"><span data-stu-id="3f62d-195">Click **All resources** in the left-hand menu, and then from the resources list click **myVM1** that is located in the *myResourceGroupLBAZ* resource group.</span></span>
2. <span data-ttu-id="3f62d-196">On the **Overview** page, click **Connect** to RDP into the VM.</span><span class="sxs-lookup"><span data-stu-id="3f62d-196">On the **Overview** page, click **Connect** to RDP into the VM.</span></span>
3. <span data-ttu-id="3f62d-197">Log into the VM with username *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="3f62d-197">Log into the VM with username *azureuser*.</span></span>
4. <span data-ttu-id="3f62d-198">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-198">On the server desktop, navigate to **Windows Administrative Tools**>**Windows PowerShell**.</span></span>
5. <span data-ttu-id="3f62d-199">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span><span class="sxs-lookup"><span data-stu-id="3f62d-199">In the PowerShell Window, run the following commands to install the IIS server, remove the  default iisstart.htm file, and then add a new iisstart.htm file that displays the name of the VM:</span></span>
   ```azurepowershell-interactive
    
    # install IIS server role
    Install-WindowsFeature -name Web-Server -IncludeManagementTools
    
    # remove default htm file
     remove-item  C:\inetpub\wwwroot\iisstart.htm
    
    # Add a new htm file that displays server name
     Add-Content -Path "C:\inetpub\wwwroot\iisstart.htm" -Value $("Hello World from" + $env:computername)
   ```
6. <span data-ttu-id="3f62d-200">Close the RDP session with *myVM1*.</span><span class="sxs-lookup"><span data-stu-id="3f62d-200">Close the RDP session with *myVM1*.</span></span>
7. <span data-ttu-id="3f62d-201">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2* and *myVM3*.</span><span class="sxs-lookup"><span data-stu-id="3f62d-201">Repeat steps 1 to 6 to install IIS and the updated iisstart.htm file on *myVM2* and *myVM3*.</span></span>

## <a name="create-load-balancer-resources"></a><span data-ttu-id="3f62d-202">Create load balancer resources</span><span class="sxs-lookup"><span data-stu-id="3f62d-202">Create load balancer resources</span></span>

<span data-ttu-id="3f62d-203">In this section, you configure load balancer settings for a backend address pool and a health probe, and specify load balancer and NAT rules.</span><span class="sxs-lookup"><span data-stu-id="3f62d-203">In this section, you configure load balancer settings for a backend address pool and a health probe, and specify load balancer and NAT rules.</span></span>


### <a name="create-a-backend-address-pool"></a><span data-ttu-id="3f62d-204">Create a backend address pool</span><span class="sxs-lookup"><span data-stu-id="3f62d-204">Create a backend address pool</span></span>

<span data-ttu-id="3f62d-205">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-205">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span> <span data-ttu-id="3f62d-206">Create the backend address pool *myBackendPool* to include *VM1*, *VM2*, and *VM3*.</span><span class="sxs-lookup"><span data-stu-id="3f62d-206">Create the backend address pool *myBackendPool* to include *VM1*, *VM2*, and *VM3*.</span></span>

1. <span data-ttu-id="3f62d-207">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="3f62d-207">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="3f62d-208">Under **Settings**, click **Backend pools**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-208">Under **Settings**, click **Backend pools**, then click **Add**.</span></span>
3. <span data-ttu-id="3f62d-209">On the **Add a backend pool** page, do the following:</span><span class="sxs-lookup"><span data-stu-id="3f62d-209">On the **Add a backend pool** page, do the following:</span></span>
    - <span data-ttu-id="3f62d-210">For name, type *myBackEndPool*, as the name for your backend pool.</span><span class="sxs-lookup"><span data-stu-id="3f62d-210">For name, type *myBackEndPool*, as the name for your backend pool.</span></span>
    - <span data-ttu-id="3f62d-211">For **Virtual network**, in the drop-down menu, click **myVNet**</span><span class="sxs-lookup"><span data-stu-id="3f62d-211">For **Virtual network**, in the drop-down menu, click **myVNet**</span></span>
    - <span data-ttu-id="3f62d-212">For **Virtual machine**, in the drop-down menu, click, **myVM1**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-212">For **Virtual machine**, in the drop-down menu, click, **myVM1**.</span></span>
    - <span data-ttu-id="3f62d-213">For **IP address**, in the drop-down menu, click the IP address of myVM1.</span><span class="sxs-lookup"><span data-stu-id="3f62d-213">For **IP address**, in the drop-down menu, click the IP address of myVM1.</span></span>
4. <span data-ttu-id="3f62d-214">Click **Add new backend resource** to add each virtual machine (*myVM2* and *myVM3*) to add to the backend pool of the load balancer.</span><span class="sxs-lookup"><span data-stu-id="3f62d-214">Click **Add new backend resource** to add each virtual machine (*myVM2* and *myVM3*) to add to the backend pool of the load balancer.</span></span>
5. <span data-ttu-id="3f62d-215">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-215">Click **Add**.</span></span>

    ![<span data-ttu-id="3f62d-216">Adding to the backend address pool -</span><span class="sxs-lookup"><span data-stu-id="3f62d-216">Adding to the backend address pool -</span></span> ](./media/load-balancer-standard-public-availability-zones-portal/add-backend-pool.png)

3. <span data-ttu-id="3f62d-217">Check to make sure your load balancer backend pool setting displays all the three VMs - **myVM1**, **myVM2** and **myVM3**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-217">Check to make sure your load balancer backend pool setting displays all the three VMs - **myVM1**, **myVM2** and **myVM3**.</span></span>

### <a name="create-a-health-probe"></a><span data-ttu-id="3f62d-218">Create a health probe</span><span class="sxs-lookup"><span data-stu-id="3f62d-218">Create a health probe</span></span>

<span data-ttu-id="3f62d-219">To allow the load balancer to monitor the status of your app, you use a health probe.</span><span class="sxs-lookup"><span data-stu-id="3f62d-219">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="3f62d-220">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span><span class="sxs-lookup"><span data-stu-id="3f62d-220">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="3f62d-221">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span><span class="sxs-lookup"><span data-stu-id="3f62d-221">Create a health probe *myHealthProbe* to monitor the health of the VMs.</span></span>

1. <span data-ttu-id="3f62d-222">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="3f62d-222">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="3f62d-223">Under **Settings**, click **Health probes**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-223">Under **Settings**, click **Health probes**, then click **Add**.</span></span>
3. <span data-ttu-id="3f62d-224">Use these values to create the health probe:</span><span class="sxs-lookup"><span data-stu-id="3f62d-224">Use these values to create the health probe:</span></span>
    - <span data-ttu-id="3f62d-225">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="3f62d-225">*myHealthProbe* - for the name of the health probe.</span></span>
    - <span data-ttu-id="3f62d-226">**HTTP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="3f62d-226">**HTTP** - for the protocol type.</span></span>
    - <span data-ttu-id="3f62d-227">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="3f62d-227">*80* - for the port number.</span></span>
    - <span data-ttu-id="3f62d-228">*15* - for number of **Interval** in seconds between probe attempts.</span><span class="sxs-lookup"><span data-stu-id="3f62d-228">*15* - for number of **Interval** in seconds between probe attempts.</span></span>
    - <span data-ttu-id="3f62d-229">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span><span class="sxs-lookup"><span data-stu-id="3f62d-229">*2* - for number of **Unhealthy threshold** or consecutive probe failures that must occur before a VM is considered unhealthy.</span></span>
4. <span data-ttu-id="3f62d-230">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-230">Click **OK**.</span></span>

   ![Adding a probe](./media/load-balancer-standard-public-availability-zones-portal/4-load-balancer-probes.png)

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="3f62d-232">Create a load balancer rule</span><span class="sxs-lookup"><span data-stu-id="3f62d-232">Create a load balancer rule</span></span>

<span data-ttu-id="3f62d-233">A load balancer rule is used to define how traffic is distributed to the VMs.</span><span class="sxs-lookup"><span data-stu-id="3f62d-233">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="3f62d-234">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span><span class="sxs-lookup"><span data-stu-id="3f62d-234">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="3f62d-235">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span><span class="sxs-lookup"><span data-stu-id="3f62d-235">Create a load balancer rule *myLoadBalancerRuleWeb* for listening to port 80 in the frontend *FrontendLoadBalancer* and sending load-balanced network traffic to the backend address pool *myBackEndPool* also using port 80.</span></span> 

1. <span data-ttu-id="3f62d-236">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span><span class="sxs-lookup"><span data-stu-id="3f62d-236">Click **All resources** in the left-hand menu, and then click **myLoadBalancer** from the resources list.</span></span>
2. <span data-ttu-id="3f62d-237">Under **Settings**, click **Load balancing rules**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-237">Under **Settings**, click **Load balancing rules**, then click **Add**.</span></span>
3. <span data-ttu-id="3f62d-238">Use these values to configure the load balancing rule:</span><span class="sxs-lookup"><span data-stu-id="3f62d-238">Use these values to configure the load balancing rule:</span></span>
    - <span data-ttu-id="3f62d-239">*myHTTPRule* - for the name of the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="3f62d-239">*myHTTPRule* - for the name of the load balancing rule.</span></span>
    - <span data-ttu-id="3f62d-240">**TCP** - for the protocol type.</span><span class="sxs-lookup"><span data-stu-id="3f62d-240">**TCP** - for the protocol type.</span></span>
    - <span data-ttu-id="3f62d-241">*80* - for the port number.</span><span class="sxs-lookup"><span data-stu-id="3f62d-241">*80* - for the port number.</span></span>
    - <span data-ttu-id="3f62d-242">*80* - for the backend port.</span><span class="sxs-lookup"><span data-stu-id="3f62d-242">*80* - for the backend port.</span></span>
    - <span data-ttu-id="3f62d-243">*myBackendPool* - for the name of the backend pool.</span><span class="sxs-lookup"><span data-stu-id="3f62d-243">*myBackendPool* - for the name of the backend pool.</span></span>
    - <span data-ttu-id="3f62d-244">*myHealthProbe* - for the name of the health probe.</span><span class="sxs-lookup"><span data-stu-id="3f62d-244">*myHealthProbe* - for the name of the health probe.</span></span>
4. <span data-ttu-id="3f62d-245">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-245">Click **OK**.</span></span>
    
    ![Adding a load balancing rule](./media/load-balancer-standard-public-availability-zones-portal/load-balancing-rule.png)

## <a name="test-the-load-balancer"></a><span data-ttu-id="3f62d-247">Test the load balancer</span><span class="sxs-lookup"><span data-stu-id="3f62d-247">Test the load balancer</span></span>
1. <span data-ttu-id="3f62d-248">Find the public IP address for the Load Balancer on the **Overview** screen.</span><span class="sxs-lookup"><span data-stu-id="3f62d-248">Find the public IP address for the Load Balancer on the **Overview** screen.</span></span> <span data-ttu-id="3f62d-249">Click **All resources** and then click **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-249">Click **All resources** and then click **myPublicIP**.</span></span>

2. <span data-ttu-id="3f62d-250">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="3f62d-250">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="3f62d-251">The default page of IIS Web server is displayed on the browser.</span><span class="sxs-lookup"><span data-stu-id="3f62d-251">The default page of IIS Web server is displayed on the browser.</span></span>

      ![IIS Web server](./media/tutorial-load-balancer-standard-zonal-portal/load-balancer-test.png)

<span data-ttu-id="3f62d-253">To see the load balancer distribute traffic across the VMs distributed across the zone you can force-refresh your web browser.</span><span class="sxs-lookup"><span data-stu-id="3f62d-253">To see the load balancer distribute traffic across the VMs distributed across the zone you can force-refresh your web browser.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3f62d-254">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3f62d-254">Clean up resources</span></span>

<span data-ttu-id="3f62d-255">When no longer needed, delete the resource group, load balancer, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="3f62d-255">When no longer needed, delete the resource group, load balancer, and all related resources.</span></span> <span data-ttu-id="3f62d-256">To do so, select the resource group that contains the load balancer and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="3f62d-256">To do so, select the resource group that contains the load balancer and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f62d-257">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f62d-257">Next steps</span></span>

<span data-ttu-id="3f62d-258">Learn more about [Standard Load Balancer](load-balancer-standard-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f62d-258">Learn more about [Standard Load Balancer](load-balancer-standard-overview.md).</span></span>
