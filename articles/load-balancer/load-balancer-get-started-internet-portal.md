---
title: Create an Internet-facing load balancer - Azure portal | Microsoft Docs
description: Learn how to create an Internet-facing load balancer in Resource Manager using the Azure portal
services: load-balancer
documentationcenter: na
author: anavinahar
manager: narayan
editor: ''
tags: azure-resource-manager
ms.assetid: aa9d26ca-3d8a-4a99-83b7-c410dd20b9d0
ms.service: load-balancer
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: annahar
ms.openlocfilehash: cbcb5ad6a78572ce884e3d4fc962c00789f0e008
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552420"
---
# <a name="creating-an-internet-facing-load-balancer-using-the-azure-portal"></a><span data-ttu-id="d30ee-103">Creating an Internet-facing load balancer using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="d30ee-103">Creating an Internet-facing load balancer using the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [Azure CLI](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Template](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="d30ee-108">This article covers the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="d30ee-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="d30ee-109">You can also [Learn how to create an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="d30ee-109">You can also [Learn how to create an Internet-facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

<span data-ttu-id="d30ee-110">This covers the sequence of individual tasks that have to be done to create a load balancer and explain in detail what is being done to accomplish the goal.</span><span class="sxs-lookup"><span data-stu-id="d30ee-110">This covers the sequence of individual tasks that have to be done to create a load balancer and explain in detail what is being done to accomplish the goal.</span></span>

## <a name="what-is-required-to-create-an-internet-facing-load-balancer"></a><span data-ttu-id="d30ee-111">What is required to create an Internet-facing load balancer?</span><span class="sxs-lookup"><span data-stu-id="d30ee-111">What is required to create an Internet-facing load balancer?</span></span>

<span data-ttu-id="d30ee-112">You need to create and configure the following objects to deploy a load balancer.</span><span class="sxs-lookup"><span data-stu-id="d30ee-112">You need to create and configure the following objects to deploy a load balancer.</span></span>

* <span data-ttu-id="d30ee-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span><span class="sxs-lookup"><span data-stu-id="d30ee-113">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="d30ee-114">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span><span class="sxs-lookup"><span data-stu-id="d30ee-114">Back-end address pool - contains network interfaces (NICs) for the virtual machines to receive network traffic from the load balancer.</span></span>
* <span data-ttu-id="d30ee-115">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="d30ee-115">Load balancing rules - contains rules mapping a public port on the load balancer to port in the back-end address pool.</span></span>
* <span data-ttu-id="d30ee-116">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="d30ee-116">Inbound NAT rules - contains rules mapping a public port on the load balancer to a port for a specific virtual machine in the back-end address pool.</span></span>
* <span data-ttu-id="d30ee-117">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="d30ee-117">Probes - contains health probes used to check availability of virtual machines instances in the back-end address pool.</span></span>

<span data-ttu-id="d30ee-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="d30ee-118">You can get more information about load balancer components with Azure Resource Manager at [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-a-load-balancer-in-azure-portal"></a><span data-ttu-id="d30ee-119">Set up a load balancer in Azure portal</span><span class="sxs-lookup"><span data-stu-id="d30ee-119">Set up a load balancer in Azure portal</span></span>

> [!IMPORTANT]
> This example assumes you have a virtual network called **myVNet**. Refer to [create virtual network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) to do this. It also assumes there is a subnet within **myVNet** called **LB-Subnet-BE** and two VMs called **web1** and **web2** respectively within the same availability set called **myAvailSet** in **myVNet**. Refer to [this link](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to create VMs.

1. <span data-ttu-id="d30ee-124">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="d30ee-124">From a browser navigate to the Azure portal: [http://portal.azure.com](http://portal.azure.com) and login with your Azure account.</span></span>
2. <span data-ttu-id="d30ee-125">On the top left-hand side of the screen select **New** > **Networking** > **Load Balancer.**</span><span class="sxs-lookup"><span data-stu-id="d30ee-125">On the top left-hand side of the screen select **New** > **Networking** > **Load Balancer.**</span></span>
3. <span data-ttu-id="d30ee-126">In the **Create load balancer** blade, type a name for your load balancer.</span><span class="sxs-lookup"><span data-stu-id="d30ee-126">In the **Create load balancer** blade, type a name for your load balancer.</span></span> <span data-ttu-id="d30ee-127">Here it is called **myLoadBalancer**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-127">Here it is called **myLoadBalancer**.</span></span>
4. <span data-ttu-id="d30ee-128">Under **Type**, select **Public**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-128">Under **Type**, select **Public**.</span></span>
5. <span data-ttu-id="d30ee-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-129">Under **Public IP address**, create a new public IP called **myPublicIP**.</span></span>
6. <span data-ttu-id="d30ee-130">Under Resource Group, select **myRG**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-130">Under Resource Group, select **myRG**.</span></span> <span data-ttu-id="d30ee-131">Then select an appropriate **Location**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-131">Then select an appropriate **Location**, and then click **OK**.</span></span> <span data-ttu-id="d30ee-132">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span><span class="sxs-lookup"><span data-stu-id="d30ee-132">The load balancer will then start to deploy and will take a few minutes to successfully complete deployment.</span></span>

    ![Updating resource group of load balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-get-started-internet-portal/1-load-balancer.png)

## <a name="create-a-back-end-address-pool"></a><span data-ttu-id="d30ee-134">Create a back-end address pool</span><span class="sxs-lookup"><span data-stu-id="d30ee-134">Create a back-end address pool</span></span>

1. <span data-ttu-id="d30ee-135">Once your load balancer has successfully deployed, select it from within your resources.</span><span class="sxs-lookup"><span data-stu-id="d30ee-135">Once your load balancer has successfully deployed, select it from within your resources.</span></span> <span data-ttu-id="d30ee-136">Under settings, select Backend Pools.</span><span class="sxs-lookup"><span data-stu-id="d30ee-136">Under settings, select Backend Pools.</span></span> <span data-ttu-id="d30ee-137">Type a name for your backend pool.</span><span class="sxs-lookup"><span data-stu-id="d30ee-137">Type a name for your backend pool.</span></span> <span data-ttu-id="d30ee-138">Then click on the **Add** button toward the top of the blade that shows up.</span><span class="sxs-lookup"><span data-stu-id="d30ee-138">Then click on the **Add** button toward the top of the blade that shows up.</span></span>
2. <span data-ttu-id="d30ee-139">Click on **Add a virtual machine** in the **Add backend pool** blade.</span><span class="sxs-lookup"><span data-stu-id="d30ee-139">Click on **Add a virtual machine** in the **Add backend pool** blade.</span></span>  <span data-ttu-id="d30ee-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-140">Select **Choose an availability set** under **Availability set** and select **myAvailSet**.</span></span> <span data-ttu-id="d30ee-141">Next, select **Choose the virtual machines** under the Virtual Machines section in the blade and click on **web1** and **web2**, the two VMs created for load balancing.</span><span class="sxs-lookup"><span data-stu-id="d30ee-141">Next, select **Choose the virtual machines** under the Virtual Machines section in the blade and click on **web1** and **web2**, the two VMs created for load balancing.</span></span> <span data-ttu-id="d30ee-142">Ensure that both have blue check marks to the left as shown in the image below.</span><span class="sxs-lookup"><span data-stu-id="d30ee-142">Ensure that both have blue check marks to the left as shown in the image below.</span></span> <span data-ttu-id="d30ee-143">Then, click **Select** in that blade followed by OK in the **Choose Virtual machines** blade and then **OK** in the **Add backend pool** blade.</span><span class="sxs-lookup"><span data-stu-id="d30ee-143">Then, click **Select** in that blade followed by OK in the **Choose Virtual machines** blade and then **OK** in the **Add backend pool** blade.</span></span>

    ![<span data-ttu-id="d30ee-144">Adding to the backend address pool -</span><span class="sxs-lookup"><span data-stu-id="d30ee-144">Adding to the backend address pool -</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-get-started-internet-portal/3-load-balancer-backend-02.png)

3. <span data-ttu-id="d30ee-145">Check to make sure your notifications drop down list has an update regarding saving the load balancer backend pool in addition to updating the network interface for both the VMs **web1** and **web2**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-145">Check to make sure your notifications drop down list has an update regarding saving the load balancer backend pool in addition to updating the network interface for both the VMs **web1** and **web2**.</span></span>

## <a name="create-a-probe-lb-rule-and-nat-rules"></a><span data-ttu-id="d30ee-146">Create a probe, LB rule, and NAT rules</span><span class="sxs-lookup"><span data-stu-id="d30ee-146">Create a probe, LB rule, and NAT rules</span></span>

1. <span data-ttu-id="d30ee-147">Create a health probe.</span><span class="sxs-lookup"><span data-stu-id="d30ee-147">Create a health probe.</span></span>

    <span data-ttu-id="d30ee-148">Under Settings of your load balancer, select Probes.</span><span class="sxs-lookup"><span data-stu-id="d30ee-148">Under Settings of your load balancer, select Probes.</span></span> <span data-ttu-id="d30ee-149">Then click **Add** located at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="d30ee-149">Then click **Add** located at the top of the blade.</span></span>

    <span data-ttu-id="d30ee-150">There are two ways to configure a probe: HTTP or TCP.</span><span class="sxs-lookup"><span data-stu-id="d30ee-150">There are two ways to configure a probe: HTTP or TCP.</span></span> <span data-ttu-id="d30ee-151">This example shows HTTP, but TCP can be configured in a similar manner.</span><span class="sxs-lookup"><span data-stu-id="d30ee-151">This example shows HTTP, but TCP can be configured in a similar manner.</span></span>
    <span data-ttu-id="d30ee-152">Update the necessary information.</span><span class="sxs-lookup"><span data-stu-id="d30ee-152">Update the necessary information.</span></span> <span data-ttu-id="d30ee-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span><span class="sxs-lookup"><span data-stu-id="d30ee-153">As mentioned, **myLoadBalancer** will load balance traffic on Port 80.</span></span> <span data-ttu-id="d30ee-154">The path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span><span class="sxs-lookup"><span data-stu-id="d30ee-154">The path selected is HealthProbe.aspx, Interval is 15 seconds, and Unhealthy threshold is 2.</span></span> <span data-ttu-id="d30ee-155">Once finished, click **OK** to create the probe.</span><span class="sxs-lookup"><span data-stu-id="d30ee-155">Once finished, click **OK** to create the probe.</span></span>

    <span data-ttu-id="d30ee-156">Hover your pointer over the 'i' icon to learn more about these individual configurations and how they can be changed to cater to your requirements.</span><span class="sxs-lookup"><span data-stu-id="d30ee-156">Hover your pointer over the 'i' icon to learn more about these individual configurations and how they can be changed to cater to your requirements.</span></span>

    ![Adding a probe](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-get-started-internet-portal/4-load-balancer-probes.png)

2. <span data-ttu-id="d30ee-158">Create a load balancer rule.</span><span class="sxs-lookup"><span data-stu-id="d30ee-158">Create a load balancer rule.</span></span>

    <span data-ttu-id="d30ee-159">Click on Load balancing rules in the Settings section of your load balancer.</span><span class="sxs-lookup"><span data-stu-id="d30ee-159">Click on Load balancing rules in the Settings section of your load balancer.</span></span> <span data-ttu-id="d30ee-160">In the new blade, click on **Add**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-160">In the new blade, click on **Add**.</span></span> <span data-ttu-id="d30ee-161">Name your rule.</span><span class="sxs-lookup"><span data-stu-id="d30ee-161">Name your rule.</span></span> <span data-ttu-id="d30ee-162">Here, it is HTTP.</span><span class="sxs-lookup"><span data-stu-id="d30ee-162">Here, it is HTTP.</span></span> <span data-ttu-id="d30ee-163">Choose the frontend port and Backend port.</span><span class="sxs-lookup"><span data-stu-id="d30ee-163">Choose the frontend port and Backend port.</span></span> <span data-ttu-id="d30ee-164">Here, 80 is chosen for both.</span><span class="sxs-lookup"><span data-stu-id="d30ee-164">Here, 80 is chosen for both.</span></span> <span data-ttu-id="d30ee-165">Choose **LB-backend** as your Backend pool and the previously created **HealthProbe** as the Probe.</span><span class="sxs-lookup"><span data-stu-id="d30ee-165">Choose **LB-backend** as your Backend pool and the previously created **HealthProbe** as the Probe.</span></span> <span data-ttu-id="d30ee-166">Other configurations can be set according to your requirements.</span><span class="sxs-lookup"><span data-stu-id="d30ee-166">Other configurations can be set according to your requirements.</span></span> <span data-ttu-id="d30ee-167">Then click OK to save the load balancing rule.</span><span class="sxs-lookup"><span data-stu-id="d30ee-167">Then click OK to save the load balancing rule.</span></span>

    ![Adding a load balancing rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-get-started-internet-portal/5-load-balancing-rules.png)

3. <span data-ttu-id="d30ee-169">Create inbound NAT rules</span><span class="sxs-lookup"><span data-stu-id="d30ee-169">Create inbound NAT rules</span></span>

    <span data-ttu-id="d30ee-170">Click on Inbound NAT rules under the settings section of your load balancer.</span><span class="sxs-lookup"><span data-stu-id="d30ee-170">Click on Inbound NAT rules under the settings section of your load balancer.</span></span> <span data-ttu-id="d30ee-171">In the new blade that, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-171">In the new blade that, click **Add**.</span></span> <span data-ttu-id="d30ee-172">Then name your inbound NAT rule.</span><span class="sxs-lookup"><span data-stu-id="d30ee-172">Then name your inbound NAT rule.</span></span> <span data-ttu-id="d30ee-173">Here it is called **inboundNATrule1**.</span><span class="sxs-lookup"><span data-stu-id="d30ee-173">Here it is called **inboundNATrule1**.</span></span> <span data-ttu-id="d30ee-174">The destination should be the Public IP previously created.</span><span class="sxs-lookup"><span data-stu-id="d30ee-174">The destination should be the Public IP previously created.</span></span> <span data-ttu-id="d30ee-175">Select Custom under Service and select the protocol you would like to use.</span><span class="sxs-lookup"><span data-stu-id="d30ee-175">Select Custom under Service and select the protocol you would like to use.</span></span> <span data-ttu-id="d30ee-176">Here TCP is selected.</span><span class="sxs-lookup"><span data-stu-id="d30ee-176">Here TCP is selected.</span></span> <span data-ttu-id="d30ee-177">Enter the port, 3441, and the Target port, in this case, 3389.</span><span class="sxs-lookup"><span data-stu-id="d30ee-177">Enter the port, 3441, and the Target port, in this case, 3389.</span></span> <span data-ttu-id="d30ee-178">then click OK to save this rule.</span><span class="sxs-lookup"><span data-stu-id="d30ee-178">then click OK to save this rule.</span></span>

    <span data-ttu-id="d30ee-179">Once the first rule is created, repeat this step for the second inbound NAT rule called inboundNATrule2 from port 3442 to Target port 3389.</span><span class="sxs-lookup"><span data-stu-id="d30ee-179">Once the first rule is created, repeat this step for the second inbound NAT rule called inboundNATrule2 from port 3442 to Target port 3389.</span></span>

    ![Adding an inbound NAT rule](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-get-started-internet-portal/6-load-balancer-inbound-nat-rules.png)

## <a name="remove-a-load-balancer"></a><span data-ttu-id="d30ee-181">Remove a Load Balancer</span><span class="sxs-lookup"><span data-stu-id="d30ee-181">Remove a Load Balancer</span></span>

<span data-ttu-id="d30ee-182">To delete a load balancer, select the load balancer you want to remove.</span><span class="sxs-lookup"><span data-stu-id="d30ee-182">To delete a load balancer, select the load balancer you want to remove.</span></span> <span data-ttu-id="d30ee-183">In the *Load Balancer* blade, click on **Delete** located at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="d30ee-183">In the *Load Balancer* blade, click on **Delete** located at the top of the blade.</span></span> <span data-ttu-id="d30ee-184">Then select **Yes** when prompted.</span><span class="sxs-lookup"><span data-stu-id="d30ee-184">Then select **Yes** when prompted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d30ee-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="d30ee-185">Next steps</span></span>

[<span data-ttu-id="d30ee-186">Get started configuring an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="d30ee-186">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="d30ee-187">Configure a load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="d30ee-187">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="d30ee-188">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="d30ee-188">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)





