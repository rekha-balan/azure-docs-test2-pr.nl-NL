---
title: 'Connect an Azure virtual network to another VNet: PowerShell | Microsoft Docs'
description: This article walks you through connecting virtual networks together by using Azure Resource Manager and PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: cherylmc
ms.openlocfilehash: e58a125d335f3e79c63750d821fdc3ed751f5ee6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563748"
---
# <a name="configure-a-vnet-to-vnet-connection-using-powershell"></a><span data-ttu-id="905f0-103">Configure a VNet-to-VNet connection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="905f0-103">Configure a VNet-to-VNet connection using PowerShell</span></span>

<span data-ttu-id="905f0-104">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span><span class="sxs-lookup"><span data-stu-id="905f0-104">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="905f0-105">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="905f0-105">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="905f0-106">You can even combine VNet-to-VNet communication with multi-site connection configurations.</span><span class="sxs-lookup"><span data-stu-id="905f0-106">You can even combine VNet-to-VNet communication with multi-site connection configurations.</span></span> <span data-ttu-id="905f0-107">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span><span class="sxs-lookup"><span data-stu-id="905f0-107">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>


![v2v diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

<span data-ttu-id="905f0-109">This article walks you through the steps to create a connection between VNets in the Resource Manager deployment model by using VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="905f0-109">This article walks you through the steps to create a connection between VNets in the Resource Manager deployment model by using VPN Gateway.</span></span> <span data-ttu-id="905f0-110">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="905f0-110">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> 

<span data-ttu-id="905f0-111">[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)] If you want to create a VNet-to-VNet connection using a different deployment model, between different deployment models, or using a different deployment tool, you can select an option from following article dropdown list:</span><span class="sxs-lookup"><span data-stu-id="905f0-111">[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)] If you want to create a VNet-to-VNet connection using a different deployment model, between different deployment models, or using a different deployment tool, you can select an option from following article dropdown list:</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Classic - Azure portal](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Connect different deployment models - Azure portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Connect different deployment models - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

[!INCLUDE [vpn-gateway-vnetpeeringlink](../../includes/vpn-gateway-vnetpeeringlink-include.md)]


## <a name="about-vnet-to-vnet-connections"></a><span data-ttu-id="905f0-117">About VNet-to-VNet connections</span><span class="sxs-lookup"><span data-stu-id="905f0-117">About VNet-to-VNet connections</span></span>
<span data-ttu-id="905f0-118">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span><span class="sxs-lookup"><span data-stu-id="905f0-118">Connecting a virtual network to another virtual network (VNet-to-VNet) is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="905f0-119">Both connectivity types use an Azure VPN gateway to provide a secure tunnel using IPsec/IKE.</span><span class="sxs-lookup"><span data-stu-id="905f0-119">Both connectivity types use an Azure VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="905f0-120">The VNets you connect can be in different regions.</span><span class="sxs-lookup"><span data-stu-id="905f0-120">The VNets you connect can be in different regions.</span></span> <span data-ttu-id="905f0-121">Or in different subscriptions.</span><span class="sxs-lookup"><span data-stu-id="905f0-121">Or in different subscriptions.</span></span> <span data-ttu-id="905f0-122">You can even combine VNet-to-VNet communication with multi-site configurations.</span><span class="sxs-lookup"><span data-stu-id="905f0-122">You can even combine VNet-to-VNet communication with multi-site configurations.</span></span> <span data-ttu-id="905f0-123">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="905f0-123">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity, as shown in the following diagram:</span></span>

![About connections](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a><span data-ttu-id="905f0-125">Why connect virtual networks?</span><span class="sxs-lookup"><span data-stu-id="905f0-125">Why connect virtual networks?</span></span>
<span data-ttu-id="905f0-126">You may want to connect virtual networks for the following reasons:</span><span class="sxs-lookup"><span data-stu-id="905f0-126">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="905f0-127">**Cross region geo-redundancy and geo-presence**</span><span class="sxs-lookup"><span data-stu-id="905f0-127">**Cross region geo-redundancy and geo-presence**</span></span>
  
  * <span data-ttu-id="905f0-128">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span><span class="sxs-lookup"><span data-stu-id="905f0-128">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="905f0-129">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span><span class="sxs-lookup"><span data-stu-id="905f0-129">With Azure Traffic Manager and Load Balancer, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="905f0-130">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span><span class="sxs-lookup"><span data-stu-id="905f0-130">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="905f0-131">**Regional multi-tier applications with isolation or administrative boundary**</span><span class="sxs-lookup"><span data-stu-id="905f0-131">**Regional multi-tier applications with isolation or administrative boundary**</span></span>
  
  * <span data-ttu-id="905f0-132">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span><span class="sxs-lookup"><span data-stu-id="905f0-132">Within the same region, you can set up multi-tier applications with multiple virtual networks connected together due to isolation or administrative requirements.</span></span>

<span data-ttu-id="905f0-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at the end of this article.</span><span class="sxs-lookup"><span data-stu-id="905f0-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at the end of this article.</span></span>

## <a name="which-set-of-steps-should-i-use"></a><span data-ttu-id="905f0-134">Which set of steps should I use?</span><span class="sxs-lookup"><span data-stu-id="905f0-134">Which set of steps should I use?</span></span>
<span data-ttu-id="905f0-135">In this article, you see two different sets of steps.</span><span class="sxs-lookup"><span data-stu-id="905f0-135">In this article, you see two different sets of steps.</span></span> <span data-ttu-id="905f0-136">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span><span class="sxs-lookup"><span data-stu-id="905f0-136">One set of steps for [VNets that reside in the same subscription](#samesub), and another for [VNets that reside in different subscriptions](#difsub).</span></span> <span data-ttu-id="905f0-137">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="905f0-137">The key difference between the sets is whether you can create and configure all virtual network and gateway resources within the same PowerShell session.</span></span>

<span data-ttu-id="905f0-138">The steps in this article use variables that are declared at the beginning of each section.</span><span class="sxs-lookup"><span data-stu-id="905f0-138">The steps in this article use variables that are declared at the beginning of each section.</span></span> <span data-ttu-id="905f0-139">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span><span class="sxs-lookup"><span data-stu-id="905f0-139">If you already are working with existing VNets, modify the variables to reflect the settings in your own environment.</span></span> 

## <a name="samesub"></a><span data-ttu-id="905f0-140">How to connect VNets that are in the same subscription</span><span class="sxs-lookup"><span data-stu-id="905f0-140">How to connect VNets that are in the same subscription</span></span>
![v2v diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a><span data-ttu-id="905f0-142">Before you begin</span><span class="sxs-lookup"><span data-stu-id="905f0-142">Before you begin</span></span>
<span data-ttu-id="905f0-143">Before beginning, you need to install the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="905f0-143">Before beginning, you need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="905f0-144">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="905f0-144">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="Step1"></a><span data-ttu-id="905f0-145">Step 1 - Plan your IP address ranges</span><span class="sxs-lookup"><span data-stu-id="905f0-145">Step 1 - Plan your IP address ranges</span></span>
<span data-ttu-id="905f0-146">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span><span class="sxs-lookup"><span data-stu-id="905f0-146">In the following steps, we create two virtual networks along with their respective gateway subnets and configurations.</span></span> <span data-ttu-id="905f0-147">We then create a VPN connection between the two VNets.</span><span class="sxs-lookup"><span data-stu-id="905f0-147">We then create a VPN connection between the two VNets.</span></span> <span data-ttu-id="905f0-148">It’s important to plan the IP address ranges for your network configuration.</span><span class="sxs-lookup"><span data-stu-id="905f0-148">It’s important to plan the IP address ranges for your network configuration.</span></span> <span data-ttu-id="905f0-149">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span><span class="sxs-lookup"><span data-stu-id="905f0-149">Keep in mind that you must make sure that none of your VNet ranges or local network ranges overlap in any way.</span></span>

<span data-ttu-id="905f0-150">We use the following values in the examples:</span><span class="sxs-lookup"><span data-stu-id="905f0-150">We use the following values in the examples:</span></span>

<span data-ttu-id="905f0-151">**Values for TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="905f0-151">**Values for TestVNet1:**</span></span>

* <span data-ttu-id="905f0-152">VNet Name: TestVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-152">VNet Name: TestVNet1</span></span>
* <span data-ttu-id="905f0-153">Resource Group: TestRG1</span><span class="sxs-lookup"><span data-stu-id="905f0-153">Resource Group: TestRG1</span></span>
* <span data-ttu-id="905f0-154">Location: East US</span><span class="sxs-lookup"><span data-stu-id="905f0-154">Location: East US</span></span>
* <span data-ttu-id="905f0-155">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="905f0-155">TestVNet1: 10.11.0.0/16 & 10.12.0.0/16</span></span>
* <span data-ttu-id="905f0-156">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-156">FrontEnd: 10.11.0.0/24</span></span>
* <span data-ttu-id="905f0-157">BackEnd: 10.12.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-157">BackEnd: 10.12.0.0/24</span></span>
* <span data-ttu-id="905f0-158">GatewaySubnet: 10.12.255.0/27</span><span class="sxs-lookup"><span data-stu-id="905f0-158">GatewaySubnet: 10.12.255.0/27</span></span>
* <span data-ttu-id="905f0-159">DNS Server: 8.8.8.8</span><span class="sxs-lookup"><span data-stu-id="905f0-159">DNS Server: 8.8.8.8</span></span>
* <span data-ttu-id="905f0-160">GatewayName: VNet1GW</span><span class="sxs-lookup"><span data-stu-id="905f0-160">GatewayName: VNet1GW</span></span>
* <span data-ttu-id="905f0-161">Public IP: VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="905f0-161">Public IP: VNet1GWIP</span></span>
* <span data-ttu-id="905f0-162">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="905f0-162">VPNType: RouteBased</span></span>
* <span data-ttu-id="905f0-163">Connection(1to4): VNet1toVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-163">Connection(1to4): VNet1toVNet4</span></span>
* <span data-ttu-id="905f0-164">Connection(1to5): VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="905f0-164">Connection(1to5): VNet1toVNet5</span></span>
* <span data-ttu-id="905f0-165">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="905f0-165">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="905f0-166">**Values for TestVNet4:**</span><span class="sxs-lookup"><span data-stu-id="905f0-166">**Values for TestVNet4:**</span></span>

* <span data-ttu-id="905f0-167">VNet Name: TestVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-167">VNet Name: TestVNet4</span></span>
* <span data-ttu-id="905f0-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span><span class="sxs-lookup"><span data-stu-id="905f0-168">TestVNet2: 10.41.0.0/16 & 10.42.0.0/16</span></span>
* <span data-ttu-id="905f0-169">FrontEnd: 10.41.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-169">FrontEnd: 10.41.0.0/24</span></span>
* <span data-ttu-id="905f0-170">BackEnd: 10.42.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-170">BackEnd: 10.42.0.0/24</span></span>
* <span data-ttu-id="905f0-171">GatewaySubnet: 10.42.255.0/27</span><span class="sxs-lookup"><span data-stu-id="905f0-171">GatewaySubnet: 10.42.255.0/27</span></span>
* <span data-ttu-id="905f0-172">Resource Group: TestRG4</span><span class="sxs-lookup"><span data-stu-id="905f0-172">Resource Group: TestRG4</span></span>
* <span data-ttu-id="905f0-173">Location: West US</span><span class="sxs-lookup"><span data-stu-id="905f0-173">Location: West US</span></span>
* <span data-ttu-id="905f0-174">DNS Server: 8.8.8.8</span><span class="sxs-lookup"><span data-stu-id="905f0-174">DNS Server: 8.8.8.8</span></span>
* <span data-ttu-id="905f0-175">GatewayName: VNet4GW</span><span class="sxs-lookup"><span data-stu-id="905f0-175">GatewayName: VNet4GW</span></span>
* <span data-ttu-id="905f0-176">Public IP: VNet4GWIP</span><span class="sxs-lookup"><span data-stu-id="905f0-176">Public IP: VNet4GWIP</span></span>
* <span data-ttu-id="905f0-177">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="905f0-177">VPNType: RouteBased</span></span>
* <span data-ttu-id="905f0-178">Connection: VNet4toVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-178">Connection: VNet4toVNet1</span></span>
* <span data-ttu-id="905f0-179">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="905f0-179">ConnectionType: VNet2VNet</span></span>

### <a name="Step2"></a><span data-ttu-id="905f0-180">Step 2 - Create and configure TestVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-180">Step 2 - Create and configure TestVNet1</span></span>
1. <span data-ttu-id="905f0-181">Declare your variables</span><span class="sxs-lookup"><span data-stu-id="905f0-181">Declare your variables</span></span>
   
    <span data-ttu-id="905f0-182">Start by declaring variables.</span><span class="sxs-lookup"><span data-stu-id="905f0-182">Start by declaring variables.</span></span> <span data-ttu-id="905f0-183">This example declares the variables using the values for this exercise.</span><span class="sxs-lookup"><span data-stu-id="905f0-183">This example declares the variables using the values for this exercise.</span></span> <span data-ttu-id="905f0-184">In most cases, you should replace the values with your own.</span><span class="sxs-lookup"><span data-stu-id="905f0-184">In most cases, you should replace the values with your own.</span></span> <span data-ttu-id="905f0-185">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span><span class="sxs-lookup"><span data-stu-id="905f0-185">However, you can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="905f0-186">Modify the variables if needed, then copy and paste them into your PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="905f0-186">Modify the variables if needed, then copy and paste them into your PowerShell console.</span></span>

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $DNS1 = "8.8.8.8"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```
2. <span data-ttu-id="905f0-187">Connect to your subscription</span><span class="sxs-lookup"><span data-stu-id="905f0-187">Connect to your subscription</span></span>
   
    <span data-ttu-id="905f0-188">Switch to PowerShell mode to use the Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="905f0-188">Switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="905f0-189">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="905f0-189">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="905f0-190">Use the following example to help you connect:</span><span class="sxs-lookup"><span data-stu-id="905f0-190">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
   
    <span data-ttu-id="905f0-191">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="905f0-191">Check the subscriptions for the account.</span></span>
 
  ```powershell
  Get-AzureRmSubscription
  ``` 
   
    <span data-ttu-id="905f0-192">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="905f0-192">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```

3. <span data-ttu-id="905f0-193">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="905f0-193">Create a new resource group</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. <span data-ttu-id="905f0-194">Create the subnet configurations for TestVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-194">Create the subnet configurations for TestVNet1</span></span>
   
    <span data-ttu-id="905f0-195">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span><span class="sxs-lookup"><span data-stu-id="905f0-195">This example creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="905f0-196">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="905f0-196">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="905f0-197">If you name it something else, your gateway creation will fail.</span><span class="sxs-lookup"><span data-stu-id="905f0-197">If you name it something else, your gateway creation will fail.</span></span> 
   
    <span data-ttu-id="905f0-198">The following example uses the variables that you set earlier.</span><span class="sxs-lookup"><span data-stu-id="905f0-198">The following example uses the variables that you set earlier.</span></span> <span data-ttu-id="905f0-199">In this example, the gateway subnet is using a /27.</span><span class="sxs-lookup"><span data-stu-id="905f0-199">In this example, the gateway subnet is using a /27.</span></span> <span data-ttu-id="905f0-200">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span><span class="sxs-lookup"><span data-stu-id="905f0-200">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="905f0-201">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span><span class="sxs-lookup"><span data-stu-id="905f0-201">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. <span data-ttu-id="905f0-202">Create TestVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-202">Create TestVNet1</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. <span data-ttu-id="905f0-203">Request a public IP address</span><span class="sxs-lookup"><span data-stu-id="905f0-203">Request a public IP address</span></span>
   
  <span data-ttu-id="905f0-204">Request a public IP address to be allocated to the gateway you will create for your VNet.</span><span class="sxs-lookup"><span data-stu-id="905f0-204">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="905f0-205">Notice that the AllocationMethod is Dynamic.</span><span class="sxs-lookup"><span data-stu-id="905f0-205">Notice that the AllocationMethod is Dynamic.</span></span> <span data-ttu-id="905f0-206">You cannot specify the IP address that you want to use.</span><span class="sxs-lookup"><span data-stu-id="905f0-206">You cannot specify the IP address that you want to use.</span></span> <span data-ttu-id="905f0-207">It's dynamically allocated to your gateway.</span><span class="sxs-lookup"><span data-stu-id="905f0-207">It's dynamically allocated to your gateway.</span></span> 
   
  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="905f0-208">Create the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="905f0-208">Create the gateway configuration</span></span>
   
    <span data-ttu-id="905f0-209">The gateway configuration defines the subnet and the public IP address to use.</span><span class="sxs-lookup"><span data-stu-id="905f0-209">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="905f0-210">Use the example to create your gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="905f0-210">Use the example to create your gateway configuration.</span></span>

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. <span data-ttu-id="905f0-211">Create the gateway for TestVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-211">Create the gateway for TestVNet1</span></span>
   
    <span data-ttu-id="905f0-212">In this step, you create the virtual network gateway for your TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="905f0-212">In this step, you create the virtual network gateway for your TestVNet1.</span></span> <span data-ttu-id="905f0-213">VNet-to-VNet configurations require a RouteBased VpnType.</span><span class="sxs-lookup"><span data-stu-id="905f0-213">VNet-to-VNet configurations require a RouteBased VpnType.</span></span> <span data-ttu-id="905f0-214">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="905f0-214">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku Standard
  ```

### <a name="step-3---create-and-configure-testvnet4"></a><span data-ttu-id="905f0-215">Step 3 - Create and configure TestVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-215">Step 3 - Create and configure TestVNet4</span></span>
<span data-ttu-id="905f0-216">Once you've configured TestVNet1, create TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="905f0-216">Once you've configured TestVNet1, create TestVNet4.</span></span> <span data-ttu-id="905f0-217">Follow the steps below, replacing the values with your own when needed.</span><span class="sxs-lookup"><span data-stu-id="905f0-217">Follow the steps below, replacing the values with your own when needed.</span></span> <span data-ttu-id="905f0-218">This step can be done within the same PowerShell session because it is in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-218">This step can be done within the same PowerShell session because it is in the same subscription.</span></span>

1. <span data-ttu-id="905f0-219">Declare your variables</span><span class="sxs-lookup"><span data-stu-id="905f0-219">Declare your variables</span></span>
   
    <span data-ttu-id="905f0-220">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="905f0-220">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $DNS4 = "8.8.8.8"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
   
    <span data-ttu-id="905f0-221">Before you continue, make sure you are still connected to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="905f0-221">Before you continue, make sure you are still connected to Subscription 1.</span></span>
2. <span data-ttu-id="905f0-222">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="905f0-222">Create a new resource group</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. <span data-ttu-id="905f0-223">Create the subnet configurations for TestVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-223">Create the subnet configurations for TestVNet4</span></span>

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. <span data-ttu-id="905f0-224">Create TestVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-224">Create TestVNet4</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. <span data-ttu-id="905f0-225">Request a public IP address</span><span class="sxs-lookup"><span data-stu-id="905f0-225">Request a public IP address</span></span>

  ```powershell  
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. <span data-ttu-id="905f0-226">Create the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="905f0-226">Create the gateway configuration</span></span>

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. <span data-ttu-id="905f0-227">Create the TestVNet4 gateway.</span><span class="sxs-lookup"><span data-stu-id="905f0-227">Create the TestVNet4 gateway.</span></span> <span data-ttu-id="905f0-228">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span><span class="sxs-lookup"><span data-stu-id="905f0-228">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku Standard
  ```

### <a name="step-4---connect-the-gateways"></a><span data-ttu-id="905f0-229">Step 4 - Connect the gateways</span><span class="sxs-lookup"><span data-stu-id="905f0-229">Step 4 - Connect the gateways</span></span>
1. <span data-ttu-id="905f0-230">Get both virtual network gateways</span><span class="sxs-lookup"><span data-stu-id="905f0-230">Get both virtual network gateways</span></span>
   
    <span data-ttu-id="905f0-231">In this example, because both gateways are in the same subscription, this step can be completed in the same PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="905f0-231">In this example, because both gateways are in the same subscription, this step can be completed in the same PowerShell session.</span></span>
   
  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. <span data-ttu-id="905f0-232">Create the TestVNet1 to TestVNet4 connection</span><span class="sxs-lookup"><span data-stu-id="905f0-232">Create the TestVNet1 to TestVNet4 connection</span></span>
   
    <span data-ttu-id="905f0-233">In this step, you create the connection from TestVNet1 to TestVNet4.</span><span class="sxs-lookup"><span data-stu-id="905f0-233">In this step, you create the connection from TestVNet1 to TestVNet4.</span></span> <span data-ttu-id="905f0-234">You'll see a shared key referenced in the examples.</span><span class="sxs-lookup"><span data-stu-id="905f0-234">You'll see a shared key referenced in the examples.</span></span> <span data-ttu-id="905f0-235">You can use your own values for the shared key.</span><span class="sxs-lookup"><span data-stu-id="905f0-235">You can use your own values for the shared key.</span></span> <span data-ttu-id="905f0-236">The important thing is that the shared key must match for both connections.</span><span class="sxs-lookup"><span data-stu-id="905f0-236">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="905f0-237">Creating a connection can take a short while to complete.</span><span class="sxs-lookup"><span data-stu-id="905f0-237">Creating a connection can take a short while to complete.</span></span>
   
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. <span data-ttu-id="905f0-238">Create the TestVNet4 to TestVNet1 connection</span><span class="sxs-lookup"><span data-stu-id="905f0-238">Create the TestVNet4 to TestVNet1 connection</span></span>
   
    <span data-ttu-id="905f0-239">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="905f0-239">This step is similar to the one above, except you are creating the connection from TestVNet4 to TestVNet1.</span></span> <span data-ttu-id="905f0-240">Make sure the shared keys match.</span><span class="sxs-lookup"><span data-stu-id="905f0-240">Make sure the shared keys match.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
   
    <span data-ttu-id="905f0-241">The connection should be established after a few minutes.</span><span class="sxs-lookup"><span data-stu-id="905f0-241">The connection should be established after a few minutes.</span></span>
4. <span data-ttu-id="905f0-242">Verify your connection.</span><span class="sxs-lookup"><span data-stu-id="905f0-242">Verify your connection.</span></span> <span data-ttu-id="905f0-243">See the section [How to verify your connection](#verify).</span><span class="sxs-lookup"><span data-stu-id="905f0-243">See the section [How to verify your connection](#verify).</span></span>

## <a name="difsub"></a><span data-ttu-id="905f0-244">How to connect VNets that are in different subscriptions</span><span class="sxs-lookup"><span data-stu-id="905f0-244">How to connect VNets that are in different subscriptions</span></span>
![v2v diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

<span data-ttu-id="905f0-246">In this scenario, we connect TestVNet1 and TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="905f0-246">In this scenario, we connect TestVNet1 and TestVNet5.</span></span> <span data-ttu-id="905f0-247">TestVNet1 and TestVNet5 reside in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-247">TestVNet1 and TestVNet5 reside in a different subscription.</span></span> <span data-ttu-id="905f0-248">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="905f0-248">The steps for this configuration add an additional VNet-to-VNet connection in order to connect TestVNet1 to TestVNet5.</span></span> 

<span data-ttu-id="905f0-249">The difference here is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-249">The difference here is that some of the configuration steps need to be performed in a separate PowerShell session in the context of the second subscription.</span></span> <span data-ttu-id="905f0-250">Especially when the two subscriptions belong to different organizations.</span><span class="sxs-lookup"><span data-stu-id="905f0-250">Especially when the two subscriptions belong to different organizations.</span></span> 

<span data-ttu-id="905f0-251">The instructions continue from the previous steps listed above.</span><span class="sxs-lookup"><span data-stu-id="905f0-251">The instructions continue from the previous steps listed above.</span></span> <span data-ttu-id="905f0-252">You must complete [Step 1](#Step1) and [Step 2](#Step2) to create and configure TestVNet1, and the VPN Gateway for TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="905f0-252">You must complete [Step 1](#Step1) and [Step 2](#Step2) to create and configure TestVNet1, and the VPN Gateway for TestVNet1.</span></span> <span data-ttu-id="905f0-253">Once you complete Step 1 and Step 2, continue with Step 5 to create TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="905f0-253">Once you complete Step 1 and Step 2, continue with Step 5 to create TestVNet5.</span></span>

### <a name="step-5---verify-the-additional-ip-address-ranges"></a><span data-ttu-id="905f0-254">Step 5 - Verify the additional IP address ranges</span><span class="sxs-lookup"><span data-stu-id="905f0-254">Step 5 - Verify the additional IP address ranges</span></span>
<span data-ttu-id="905f0-255">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span><span class="sxs-lookup"><span data-stu-id="905f0-255">It is important to make sure that the IP address space of the new virtual network, TestVNet5, does not overlap with any of your VNet ranges or local network gateway ranges.</span></span> 

<span data-ttu-id="905f0-256">In this example, the virtual networks may belong to different organizations.</span><span class="sxs-lookup"><span data-stu-id="905f0-256">In this example, the virtual networks may belong to different organizations.</span></span> <span data-ttu-id="905f0-257">For this exercise, you can use the following values for the TestVNet5:</span><span class="sxs-lookup"><span data-stu-id="905f0-257">For this exercise, you can use the following values for the TestVNet5:</span></span>

<span data-ttu-id="905f0-258">**Values for TestVNet5:**</span><span class="sxs-lookup"><span data-stu-id="905f0-258">**Values for TestVNet5:**</span></span>

* <span data-ttu-id="905f0-259">VNet Name: TestVNet5</span><span class="sxs-lookup"><span data-stu-id="905f0-259">VNet Name: TestVNet5</span></span>
* <span data-ttu-id="905f0-260">Resource Group: TestRG5</span><span class="sxs-lookup"><span data-stu-id="905f0-260">Resource Group: TestRG5</span></span>
* <span data-ttu-id="905f0-261">Location: Japan East</span><span class="sxs-lookup"><span data-stu-id="905f0-261">Location: Japan East</span></span>
* <span data-ttu-id="905f0-262">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="905f0-262">TestVNet5: 10.51.0.0/16 & 10.52.0.0/16</span></span>
* <span data-ttu-id="905f0-263">FrontEnd: 10.51.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-263">FrontEnd: 10.51.0.0/24</span></span>
* <span data-ttu-id="905f0-264">BackEnd: 10.52.0.0/24</span><span class="sxs-lookup"><span data-stu-id="905f0-264">BackEnd: 10.52.0.0/24</span></span>
* <span data-ttu-id="905f0-265">GatewaySubnet: 10.52.255.0.0/27</span><span class="sxs-lookup"><span data-stu-id="905f0-265">GatewaySubnet: 10.52.255.0.0/27</span></span>
* <span data-ttu-id="905f0-266">DNS Server: 8.8.8.8</span><span class="sxs-lookup"><span data-stu-id="905f0-266">DNS Server: 8.8.8.8</span></span>
* <span data-ttu-id="905f0-267">GatewayName: VNet5GW</span><span class="sxs-lookup"><span data-stu-id="905f0-267">GatewayName: VNet5GW</span></span>
* <span data-ttu-id="905f0-268">Public IP: VNet5GWIP</span><span class="sxs-lookup"><span data-stu-id="905f0-268">Public IP: VNet5GWIP</span></span>
* <span data-ttu-id="905f0-269">VPNType: RouteBased</span><span class="sxs-lookup"><span data-stu-id="905f0-269">VPNType: RouteBased</span></span>
* <span data-ttu-id="905f0-270">Connection: VNet5toVNet1</span><span class="sxs-lookup"><span data-stu-id="905f0-270">Connection: VNet5toVNet1</span></span>
* <span data-ttu-id="905f0-271">ConnectionType: VNet2VNet</span><span class="sxs-lookup"><span data-stu-id="905f0-271">ConnectionType: VNet2VNet</span></span>

<span data-ttu-id="905f0-272">**Additional Values for TestVNet1:**</span><span class="sxs-lookup"><span data-stu-id="905f0-272">**Additional Values for TestVNet1:**</span></span>

* <span data-ttu-id="905f0-273">Connection: VNet1toVNet5</span><span class="sxs-lookup"><span data-stu-id="905f0-273">Connection: VNet1toVNet5</span></span>

### <a name="step-6---create-and-configure-testvnet5"></a><span data-ttu-id="905f0-274">Step 6 - Create and configure TestVNet5</span><span class="sxs-lookup"><span data-stu-id="905f0-274">Step 6 - Create and configure TestVNet5</span></span>
<span data-ttu-id="905f0-275">This step must be done in the context of the new subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-275">This step must be done in the context of the new subscription.</span></span> <span data-ttu-id="905f0-276">This part may be performed by the administrator in a different organization that owns the subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-276">This part may be performed by the administrator in a different organization that owns the subscription.</span></span>

1. <span data-ttu-id="905f0-277">Declare your variables</span><span class="sxs-lookup"><span data-stu-id="905f0-277">Declare your variables</span></span>
   
    <span data-ttu-id="905f0-278">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="905f0-278">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $DNS5 = "8.8.8.8"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. <span data-ttu-id="905f0-279">Connect to subscription 5</span><span class="sxs-lookup"><span data-stu-id="905f0-279">Connect to subscription 5</span></span>
   
    <span data-ttu-id="905f0-280">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="905f0-280">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="905f0-281">Use the following sample to help you connect:</span><span class="sxs-lookup"><span data-stu-id="905f0-281">Use the following sample to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```
   
    <span data-ttu-id="905f0-282">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="905f0-282">Check the subscriptions for the account.</span></span>
   
  ```powershell
  Get-AzureRmSubscription
  ```
   
    <span data-ttu-id="905f0-283">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="905f0-283">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. <span data-ttu-id="905f0-284">Create a new resource group</span><span class="sxs-lookup"><span data-stu-id="905f0-284">Create a new resource group</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. <span data-ttu-id="905f0-285">Create the subnet configurations for TestVNet4</span><span class="sxs-lookup"><span data-stu-id="905f0-285">Create the subnet configurations for TestVNet4</span></span>

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. <span data-ttu-id="905f0-286">Create TestVNet5</span><span class="sxs-lookup"><span data-stu-id="905f0-286">Create TestVNet5</span></span>

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. <span data-ttu-id="905f0-287">Request a public IP address</span><span class="sxs-lookup"><span data-stu-id="905f0-287">Request a public IP address</span></span>

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. <span data-ttu-id="905f0-288">Create the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="905f0-288">Create the gateway configuration</span></span>

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. <span data-ttu-id="905f0-289">Create the TestVNet5 gateway</span><span class="sxs-lookup"><span data-stu-id="905f0-289">Create the TestVNet5 gateway</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard
  ```

### <a name="step-7---connecting-the-gateways"></a><span data-ttu-id="905f0-290">Step 7 - Connecting the gateways</span><span class="sxs-lookup"><span data-stu-id="905f0-290">Step 7 - Connecting the gateways</span></span>
<span data-ttu-id="905f0-291">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span><span class="sxs-lookup"><span data-stu-id="905f0-291">In this example, because the gateways are in the different subscriptions, we've split this step into two PowerShell sessions marked as [Subscription 1] and [Subscription 5].</span></span>

1. <span data-ttu-id="905f0-292">**[Subscription 1]** Get the virtual network gateway for Subscription 1</span><span class="sxs-lookup"><span data-stu-id="905f0-292">**[Subscription 1]** Get the virtual network gateway for Subscription 1</span></span>
   
    <span data-ttu-id="905f0-293">Make sure you log in and connect to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="905f0-293">Make sure you log in and connect to Subscription 1.</span></span>

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```
   
    <span data-ttu-id="905f0-294">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span><span class="sxs-lookup"><span data-stu-id="905f0-294">Copy the output of the following elements and send these to the administrator of Subscription 5 via email or another method.</span></span>

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```
   
    <span data-ttu-id="905f0-295">These two elements will have values similar to the following example output:</span><span class="sxs-lookup"><span data-stu-id="905f0-295">These two elements will have values similar to the following example output:</span></span>

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. <span data-ttu-id="905f0-296">**[Subscription 5]** Get the virtual network gateway for Subscription 5</span><span class="sxs-lookup"><span data-stu-id="905f0-296">**[Subscription 5]** Get the virtual network gateway for Subscription 5</span></span>
   
    <span data-ttu-id="905f0-297">Make sure you log in and connect to Subscription 5.</span><span class="sxs-lookup"><span data-stu-id="905f0-297">Make sure you log in and connect to Subscription 5.</span></span>

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```
   
    <span data-ttu-id="905f0-298">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span><span class="sxs-lookup"><span data-stu-id="905f0-298">Copy the output of the following elements and send these to the administrator of Subscription 1 via email or another method.</span></span>

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```
   
    <span data-ttu-id="905f0-299">These two elements will have values similar to the following example output:</span><span class="sxs-lookup"><span data-stu-id="905f0-299">These two elements will have values similar to the following example output:</span></span>

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. <span data-ttu-id="905f0-300">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection</span><span class="sxs-lookup"><span data-stu-id="905f0-300">**[Subscription 1]** Create the TestVNet1 to TestVNet5 connection</span></span>
   
    <span data-ttu-id="905f0-301">In this step, you create the connection from TestVNet1 to TestVNet5.</span><span class="sxs-lookup"><span data-stu-id="905f0-301">In this step, you create the connection from TestVNet1 to TestVNet5.</span></span> <span data-ttu-id="905f0-302">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span><span class="sxs-lookup"><span data-stu-id="905f0-302">The difference here is that $vnet5gw cannot be obtained directly because it is in a different subscription.</span></span> <span data-ttu-id="905f0-303">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span><span class="sxs-lookup"><span data-stu-id="905f0-303">You will need to create a new PowerShell object with the values communicated from Subscription 1 in the steps above.</span></span> <span data-ttu-id="905f0-304">Use the example below.</span><span class="sxs-lookup"><span data-stu-id="905f0-304">Use the example below.</span></span> <span data-ttu-id="905f0-305">Replace the Name, Id, and shared key with your own values.</span><span class="sxs-lookup"><span data-stu-id="905f0-305">Replace the Name, Id, and shared key with your own values.</span></span> <span data-ttu-id="905f0-306">The important thing is that the shared key must match for both connections.</span><span class="sxs-lookup"><span data-stu-id="905f0-306">The important thing is that the shared key must match for both connections.</span></span> <span data-ttu-id="905f0-307">Creating a connection can take a short while to complete.</span><span class="sxs-lookup"><span data-stu-id="905f0-307">Creating a connection can take a short while to complete.</span></span>
   
    <span data-ttu-id="905f0-308">Make sure you connect to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="905f0-308">Make sure you connect to Subscription 1.</span></span>

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. <span data-ttu-id="905f0-309">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection</span><span class="sxs-lookup"><span data-stu-id="905f0-309">**[Subscription 5]** Create the TestVNet5 to TestVNet1 connection</span></span>
   
    <span data-ttu-id="905f0-310">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="905f0-310">This step is similar to the one above, except you are creating the connection from TestVNet5 to TestVNet1.</span></span> <span data-ttu-id="905f0-311">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span><span class="sxs-lookup"><span data-stu-id="905f0-311">The same process of creating a PowerShell object based on the values obtained from Subscription 1 applies here as well.</span></span> <span data-ttu-id="905f0-312">In this step, be sure that the shared keys match.</span><span class="sxs-lookup"><span data-stu-id="905f0-312">In this step, be sure that the shared keys match.</span></span>
   
    <span data-ttu-id="905f0-313">Make sure you connect to Subscription 5.</span><span class="sxs-lookup"><span data-stu-id="905f0-313">Make sure you connect to Subscription 5.</span></span>

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a><span data-ttu-id="905f0-314">How to verify a connection</span><span class="sxs-lookup"><span data-stu-id="905f0-314">How to verify a connection</span></span>
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

### <a name="faq"></a><span data-ttu-id="905f0-315">VNet-to-VNet considerations</span><span class="sxs-lookup"><span data-stu-id="905f0-315">VNet-to-VNet considerations</span></span>
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a><span data-ttu-id="905f0-316">Next steps</span><span class="sxs-lookup"><span data-stu-id="905f0-316">Next steps</span></span>

* <span data-ttu-id="905f0-317">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="905f0-317">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="905f0-318">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span><span class="sxs-lookup"><span data-stu-id="905f0-318">See the [Virtual Machines documentation](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) for more information.</span></span>
* <span data-ttu-id="905f0-319">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="905f0-319">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span> 





