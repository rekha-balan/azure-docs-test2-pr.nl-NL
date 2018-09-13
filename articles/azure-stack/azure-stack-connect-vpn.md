---
title: Connect Azure Stack to Azure using VPN
description: How to connect virtual networks in Azure Stack to virtual networks in Azure using VPN.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2018
ms.author: brenduns
ms.reviewer: scottnap
ms.openlocfilehash: 0b9ed21ca969d86c9b30db42bafef86b061c3d6c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868752"
---
# <a name="connect-azure-stack-to-azure-using-vpn"></a><span data-ttu-id="674f4-103">Connect Azure Stack to Azure using VPN</span><span class="sxs-lookup"><span data-stu-id="674f4-103">Connect Azure Stack to Azure using VPN</span></span>

<span data-ttu-id="674f4-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="674f4-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="674f4-105">This article shows you how to create a site-to-site VPN to connect a virtual network in Azure Stack to a virtual network in Azure.</span><span class="sxs-lookup"><span data-stu-id="674f4-105">This article shows you how to create a site-to-site VPN to connect a virtual network in Azure Stack to a virtual network in Azure.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="674f4-106">Before you begin</span><span class="sxs-lookup"><span data-stu-id="674f4-106">Before you begin</span></span>

<span data-ttu-id="674f4-107">To complete the connection configuration, make sure you have the following items before you begin:</span><span class="sxs-lookup"><span data-stu-id="674f4-107">To complete the connection configuration, make sure you have the following items before you begin:</span></span>

* <span data-ttu-id="674f4-108">An Azure Stack integrated systems (multi-node) deployment that is directly connected to the Internet.</span><span class="sxs-lookup"><span data-stu-id="674f4-108">An Azure Stack integrated systems (multi-node) deployment that is directly connected to the Internet.</span></span> <span data-ttu-id="674f4-109">Your external public IP address range must be directly reachable from the public Internet.</span><span class="sxs-lookup"><span data-stu-id="674f4-109">Your external public IP address range must be directly reachable from the public Internet.</span></span>
* <span data-ttu-id="674f4-110">A valid Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="674f4-110">A valid Azure subscription.</span></span> <span data-ttu-id="674f4-111">If you don’t have an Azure subscription, you can create a [free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span><span class="sxs-lookup"><span data-stu-id="674f4-111">If you don’t have an Azure subscription, you can create a [free Azure account here](https://azure.microsoft.com/free/?b=17.06).</span></span>

### <a name="vpn-connection-diagram"></a><span data-ttu-id="674f4-112">VPN connection diagram</span><span class="sxs-lookup"><span data-stu-id="674f4-112">VPN connection diagram</span></span>

<span data-ttu-id="674f4-113">The following diagram shows what the connection configuration should look like when you’re done:</span><span class="sxs-lookup"><span data-stu-id="674f4-113">The following diagram shows what the connection configuration should look like when you’re done:</span></span>

![Site-to-site VPN connection configuration](media/azure-stack-connect-vpn/image2.png)

### <a name="network-configuration-example-values"></a><span data-ttu-id="674f4-115">Network configuration example values</span><span class="sxs-lookup"><span data-stu-id="674f4-115">Network configuration example values</span></span>

<span data-ttu-id="674f4-116">The network configuration examples table shows the values that are used for examples in this article.</span><span class="sxs-lookup"><span data-stu-id="674f4-116">The network configuration examples table shows the values that are used for examples in this article.</span></span> <span data-ttu-id="674f4-117">You can use these values or you can refer to them to better understand the examples in this article.</span><span class="sxs-lookup"><span data-stu-id="674f4-117">You can use these values or you can refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="674f4-118">**Network configuration examples**</span><span class="sxs-lookup"><span data-stu-id="674f4-118">**Network configuration examples**</span></span>

|   |<span data-ttu-id="674f4-119">Azure Stack</span><span class="sxs-lookup"><span data-stu-id="674f4-119">Azure Stack</span></span>|<span data-ttu-id="674f4-120">Azure</span><span class="sxs-lookup"><span data-stu-id="674f4-120">Azure</span></span>|
|---------|---------|---------|
|<span data-ttu-id="674f4-121">Virtual network name</span><span class="sxs-lookup"><span data-stu-id="674f4-121">Virtual network name</span></span>     |<span data-ttu-id="674f4-122">Azs-VNet</span><span class="sxs-lookup"><span data-stu-id="674f4-122">Azs-VNet</span></span>|<span data-ttu-id="674f4-123">AzureVNet</span><span class="sxs-lookup"><span data-stu-id="674f4-123">AzureVNet</span></span> |
|<span data-ttu-id="674f4-124">Virtual network address space</span><span class="sxs-lookup"><span data-stu-id="674f4-124">Virtual network address space</span></span> |<span data-ttu-id="674f4-125">10.1.0.0/16</span><span class="sxs-lookup"><span data-stu-id="674f4-125">10.1.0.0/16</span></span>|<span data-ttu-id="674f4-126">10.100.0.0/16</span><span class="sxs-lookup"><span data-stu-id="674f4-126">10.100.0.0/16</span></span>|
|<span data-ttu-id="674f4-127">Subnet name</span><span class="sxs-lookup"><span data-stu-id="674f4-127">Subnet name</span></span>     |<span data-ttu-id="674f4-128">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="674f4-128">FrontEnd</span></span>|<span data-ttu-id="674f4-129">FrontEnd</span><span class="sxs-lookup"><span data-stu-id="674f4-129">FrontEnd</span></span>|
|<span data-ttu-id="674f4-130">Subnet address range</span><span class="sxs-lookup"><span data-stu-id="674f4-130">Subnet address range</span></span>|<span data-ttu-id="674f4-131">10.1.0.0/24</span><span class="sxs-lookup"><span data-stu-id="674f4-131">10.1.0.0/24</span></span> |<span data-ttu-id="674f4-132">10.100.0.0/24</span><span class="sxs-lookup"><span data-stu-id="674f4-132">10.100.0.0/24</span></span> |
|<span data-ttu-id="674f4-133">Gateway subnet</span><span class="sxs-lookup"><span data-stu-id="674f4-133">Gateway subnet</span></span>     |<span data-ttu-id="674f4-134">10.1.1.0/24</span><span class="sxs-lookup"><span data-stu-id="674f4-134">10.1.1.0/24</span></span>|<span data-ttu-id="674f4-135">10.100.1.0/24</span><span class="sxs-lookup"><span data-stu-id="674f4-135">10.100.1.0/24</span></span>|

## <a name="create-the-network-resources-in-azure"></a><span data-ttu-id="674f4-136">Create the network resources in Azure</span><span class="sxs-lookup"><span data-stu-id="674f4-136">Create the network resources in Azure</span></span>

<span data-ttu-id="674f4-137">First you create the network resources for Azure.</span><span class="sxs-lookup"><span data-stu-id="674f4-137">First you create the network resources for Azure.</span></span> <span data-ttu-id="674f4-138">The following instructions show how to create the resources by using the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="674f4-138">The following instructions show how to create the resources by using the [Azure portal](http://portal.azure.com/).</span></span>

### <a name="create-the-virtual-network-and-virtual-machine-vm-subnet"></a><span data-ttu-id="674f4-139">Create the virtual network and virtual machine (VM) subnet</span><span class="sxs-lookup"><span data-stu-id="674f4-139">Create the virtual network and virtual machine (VM) subnet</span></span>

1. <span data-ttu-id="674f4-140">Sign in to the [Azure portal](http://portal.azure.com/) using your Azure account.</span><span class="sxs-lookup"><span data-stu-id="674f4-140">Sign in to the [Azure portal](http://portal.azure.com/) using your Azure account.</span></span>
2. <span data-ttu-id="674f4-141">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-141">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="674f4-142">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-142">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="674f4-143">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="674f4-143">Select **Virtual network**.</span></span>
5. <span data-ttu-id="674f4-144">Use the information from the network configuration table to identify the values for Azure **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span><span class="sxs-lookup"><span data-stu-id="674f4-144">Use the information from the network configuration table to identify the values for Azure **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="674f4-145">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="674f4-145">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
7. <span data-ttu-id="674f4-146">Select the **Location** of your VNet.</span><span class="sxs-lookup"><span data-stu-id="674f4-146">Select the **Location** of your VNet.</span></span>  <span data-ttu-id="674f4-147">If you're using the example values, select **East US** or use another location if you prefer.</span><span class="sxs-lookup"><span data-stu-id="674f4-147">If you're using the example values, select **East US** or use another location if you prefer.</span></span>
8. <span data-ttu-id="674f4-148">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="674f4-148">Select **Pin to dashboard**.</span></span>
9. <span data-ttu-id="674f4-149">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-149">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="674f4-150">Create the Gateway Subnet</span><span class="sxs-lookup"><span data-stu-id="674f4-150">Create the Gateway Subnet</span></span>

1. <span data-ttu-id="674f4-151">Open the Virtual network resource you created (**AzureVNet**) from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="674f4-151">Open the Virtual network resource you created (**AzureVNet**) from the dashboard.</span></span>
2. <span data-ttu-id="674f4-152">On the **Settings** section, select **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="674f4-152">On the **Settings** section, select **Subnets**.</span></span>
3. <span data-ttu-id="674f4-153">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="674f4-153">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
4. <span data-ttu-id="674f4-154">The name of the subnet is set to **GatewaySubnet** by default.</span><span class="sxs-lookup"><span data-stu-id="674f4-154">The name of the subnet is set to **GatewaySubnet** by default.</span></span>

   >[!IMPORTANT]
   ><span data-ttu-id="674f4-155">Gateway subnets are special and **must** have this specific name to function properly.</span><span class="sxs-lookup"><span data-stu-id="674f4-155">Gateway subnets are special and **must** have this specific name to function properly.</span></span>

5. <span data-ttu-id="674f4-156">In the **Address range** field, verify the address is **10.100.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-156">In the **Address range** field, verify the address is **10.100.1.0/24**.</span></span>
6. <span data-ttu-id="674f4-157">Select **OK** to create the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="674f4-157">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="674f4-158">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="674f4-158">Create the virtual network gateway</span></span>

1. <span data-ttu-id="674f4-159">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-159">In the Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="674f4-160">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-160">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="674f4-161">From the list of network resources, select **Virtual network gateway**.</span><span class="sxs-lookup"><span data-stu-id="674f4-161">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="674f4-162">In **Name**, type **Azure-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-162">In **Name**, type **Azure-GW**.</span></span>
5. <span data-ttu-id="674f4-163">To choose a virtual network, select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="674f4-163">To choose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="674f4-164">Then select **AzureVnet** from the list.</span><span class="sxs-lookup"><span data-stu-id="674f4-164">Then select **AzureVnet** from the list.</span></span>
6. <span data-ttu-id="674f4-165">Select **Public IP address**.</span><span class="sxs-lookup"><span data-stu-id="674f4-165">Select **Public IP address**.</span></span> <span data-ttu-id="674f4-166">When the **Choose public IP address** section opens, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="674f4-166">When the **Choose public IP address** section opens, select **Create new**.</span></span>
7. <span data-ttu-id="674f4-167">In **Name**, type **Azure-GW-PiP**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-167">In **Name**, type **Azure-GW-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="674f4-168">By default, for **VPN type**, **Route-based** is selected.</span><span class="sxs-lookup"><span data-stu-id="674f4-168">By default, for **VPN type**, **Route-based** is selected.</span></span> <span data-ttu-id="674f4-169">Keep the **Route-based** VPN type.</span><span class="sxs-lookup"><span data-stu-id="674f4-169">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="674f4-170">Verify that **Subscription** and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="674f4-170">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="674f4-171">You can pin the resource to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="674f4-171">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="674f4-172">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-172">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="674f4-173">Create the local network gateway resource</span><span class="sxs-lookup"><span data-stu-id="674f4-173">Create the local network gateway resource</span></span>

1. <span data-ttu-id="674f4-174">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-174">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-175">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-175">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="674f4-176">From the list of resources, select **Local network gateway**.</span><span class="sxs-lookup"><span data-stu-id="674f4-176">From the list of resources, select **Local network gateway**.</span></span>
4. <span data-ttu-id="674f4-177">In **Name**, type **Azs-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-177">In **Name**, type **Azs-GW**.</span></span>
5. <span data-ttu-id="674f4-178">In **IP address**, type the public IP address for your Azure Stack Virtual Network Gateway that is listed earlier in the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="674f4-178">In **IP address**, type the public IP address for your Azure Stack Virtual Network Gateway that is listed earlier in the network configuration table.</span></span>
6. <span data-ttu-id="674f4-179">In **Address Space**, from Azure Stack, type the **10.1.0.0/24** and **10.1.1.0/24** address space for **AzureVNet**.</span><span class="sxs-lookup"><span data-stu-id="674f4-179">In **Address Space**, from Azure Stack, type the **10.1.0.0/24** and **10.1.1.0/24** address space for **AzureVNet**.</span></span>
7. <span data-ttu-id="674f4-180">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-180">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="674f4-181">Create the connection</span><span class="sxs-lookup"><span data-stu-id="674f4-181">Create the connection</span></span>

1. <span data-ttu-id="674f4-182">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-182">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-183">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-183">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="674f4-184">From the list of resources, select **Connection**.</span><span class="sxs-lookup"><span data-stu-id="674f4-184">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="674f4-185">On the **Basic** settings section, for the **Connection type**, choose **Site-to-site (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="674f4-185">On the **Basic** settings section, for the **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="674f4-186">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-186">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="674f4-187">On the **Settings** section, select **Virtual network gateway**, and then select **Azure-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-187">On the **Settings** section, select **Virtual network gateway**, and then select **Azure-GW**.</span></span>
7. <span data-ttu-id="674f4-188">Select **Local network gateway**, and then select **Azs-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-188">Select **Local network gateway**, and then select **Azs-GW**.</span></span>
8. <span data-ttu-id="674f4-189">In **Connection name**, type **Azure-Azs**.</span><span class="sxs-lookup"><span data-stu-id="674f4-189">In **Connection name**, type **Azure-Azs**.</span></span>
9. <span data-ttu-id="674f4-190">In **Shared key (PSK)**, type **12345**.</span><span class="sxs-lookup"><span data-stu-id="674f4-190">In **Shared key (PSK)**, type **12345**.</span></span> <span data-ttu-id="674f4-191">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-191">Select **OK**.</span></span>

   >[!NOTE]
   ><span data-ttu-id="674f4-192">If you use a different value for the shared key, remember that it *must* match the value for the shared key that you create on the other end of the connection.</span><span class="sxs-lookup"><span data-stu-id="674f4-192">If you use a different value for the shared key, remember that it *must* match the value for the shared key that you create on the other end of the connection.</span></span>

10. <span data-ttu-id="674f4-193">Review the **Summary** section, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-193">Review the **Summary** section, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="674f4-194">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="674f4-194">Create a virtual machine</span></span>

<span data-ttu-id="674f4-195">Create a virtual machine in Azure now, and put it on your VM subnet in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="674f4-195">Create a virtual machine in Azure now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="674f4-196">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-196">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-197">Go to **Marketplace**, and then select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="674f4-197">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="674f4-198">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Oval** image.</span><span class="sxs-lookup"><span data-stu-id="674f4-198">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Oval** image.</span></span>
4. <span data-ttu-id="674f4-199">On the **Basics** section, for **Name**, type **AzureVM**.</span><span class="sxs-lookup"><span data-stu-id="674f4-199">On the **Basics** section, for **Name**, type **AzureVM**.</span></span>
5. <span data-ttu-id="674f4-200">Type a valid username and password.</span><span class="sxs-lookup"><span data-stu-id="674f4-200">Type a valid username and password.</span></span> <span data-ttu-id="674f4-201">You use this account to sign in to the virtual machine after it's created.</span><span class="sxs-lookup"><span data-stu-id="674f4-201">You use this account to sign in to the virtual machine after it's created.</span></span>
6. <span data-ttu-id="674f4-202">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-202">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="674f4-203">On the **Size** section, select a virtual machine size for this instance, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="674f4-203">On the **Size** section, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="674f4-204">On the **Settings** section, you can use the default settings.</span><span class="sxs-lookup"><span data-stu-id="674f4-204">On the **Settings** section, you can use the default settings.</span></span> <span data-ttu-id="674f4-205">Before you select OK, confirm that:</span><span class="sxs-lookup"><span data-stu-id="674f4-205">Before you select OK, confirm that:</span></span>

   * <span data-ttu-id="674f4-206">The **AzureVnet** virtual network is selected.</span><span class="sxs-lookup"><span data-stu-id="674f4-206">The **AzureVnet** virtual network is selected.</span></span>
   * <span data-ttu-id="674f4-207">The subnet is set to **10.100.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-207">The subnet is set to **10.100.0.0/24**.</span></span>

   <span data-ttu-id="674f4-208">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-208">Select **OK**.</span></span>

9. <span data-ttu-id="674f4-209">Review the settings on the **Summary** section, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-209">Review the settings on the **Summary** section, and then select **OK**.</span></span>

## <a name="create-the-network-resources-in-azure-stack"></a><span data-ttu-id="674f4-210">Create the network resources in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="674f4-210">Create the network resources in Azure Stack</span></span>

<span data-ttu-id="674f4-211">Next you create the network resources in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="674f4-211">Next you create the network resources in Azure Stack.</span></span>

### <a name="sign-in-as-a-user"></a><span data-ttu-id="674f4-212">Sign in as a user</span><span class="sxs-lookup"><span data-stu-id="674f4-212">Sign in as a user</span></span>

<span data-ttu-id="674f4-213">A service administrator can sign in as a user to test the plans, offers, and subscriptions that their users might use.</span><span class="sxs-lookup"><span data-stu-id="674f4-213">A service administrator can sign in as a user to test the plans, offers, and subscriptions that their users might use.</span></span> <span data-ttu-id="674f4-214">If you don’t already have one, [create a user account](azure-stack-add-new-user-aad.md) before you sign in.</span><span class="sxs-lookup"><span data-stu-id="674f4-214">If you don’t already have one, [create a user account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-a-vm-subnet"></a><span data-ttu-id="674f4-215">Create the virtual network and a VM subnet</span><span class="sxs-lookup"><span data-stu-id="674f4-215">Create the virtual network and a VM subnet</span></span>

1. <span data-ttu-id="674f4-216">Use a user account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="674f4-216">Use a user account to sign in to the user portal.</span></span>
2. <span data-ttu-id="674f4-217">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-217">In the user portal, select **New**.</span></span>

    ![Create new virtual network](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="674f4-219">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-219">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="674f4-220">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="674f4-220">Select **Virtual network**.</span></span>
5. <span data-ttu-id="674f4-221">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values from the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="674f4-221">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values from the network configuration table.</span></span>
6. <span data-ttu-id="674f4-222">In **Subscription**, the subscription that you created earlier appears.</span><span class="sxs-lookup"><span data-stu-id="674f4-222">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="674f4-223">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="674f4-223">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="674f4-224">Verify the default location.</span><span class="sxs-lookup"><span data-stu-id="674f4-224">Verify the default location.</span></span>
9. <span data-ttu-id="674f4-225">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="674f4-225">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="674f4-226">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-226">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="674f4-227">Create the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="674f4-227">Create the gateway subnet</span></span>

1. <span data-ttu-id="674f4-228">On the dashboard, open the Azs-VNet virtual network resource you created.</span><span class="sxs-lookup"><span data-stu-id="674f4-228">On the dashboard, open the Azs-VNet virtual network resource you created.</span></span>
2. <span data-ttu-id="674f4-229">On the **Settings** section, select **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="674f4-229">On the **Settings** section, select **Subnets**.</span></span>
3. <span data-ttu-id="674f4-230">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span><span class="sxs-lookup"><span data-stu-id="674f4-230">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span></span>

    ![Add gateway subnet](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="674f4-232">By default, the subnet name is set to **GatewaySubnet**.</span><span class="sxs-lookup"><span data-stu-id="674f4-232">By default, the subnet name is set to **GatewaySubnet**.</span></span> <span data-ttu-id="674f4-233">Gateway subnets are special.</span><span class="sxs-lookup"><span data-stu-id="674f4-233">Gateway subnets are special.</span></span> <span data-ttu-id="674f4-234">To function properly, they must use the *GatewaySubnet* name.</span><span class="sxs-lookup"><span data-stu-id="674f4-234">To function properly, they must use the *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="674f4-235">In **Address range**, verify that the address is **10.1.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-235">In **Address range**, verify that the address is **10.1.1.0/24**.</span></span>
6. <span data-ttu-id="674f4-236">Select **OK** to create the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="674f4-236">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="674f4-237">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="674f4-237">Create the virtual network gateway</span></span>

1. <span data-ttu-id="674f4-238">In the Azure Stack portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-238">In the Azure Stack portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-239">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-239">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="674f4-240">From the list of network resources, select **Virtual network gateway**.</span><span class="sxs-lookup"><span data-stu-id="674f4-240">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="674f4-241">In **Name**, type **Azs-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-241">In **Name**, type **Azs-GW**.</span></span>
5. <span data-ttu-id="674f4-242">Select the **Virtual network** item to choose a virtual network.</span><span class="sxs-lookup"><span data-stu-id="674f4-242">Select the **Virtual network** item to choose a virtual network.</span></span> <span data-ttu-id="674f4-243">Select **Azs-VNet** from the list.</span><span class="sxs-lookup"><span data-stu-id="674f4-243">Select **Azs-VNet** from the list.</span></span>
6. <span data-ttu-id="674f4-244">Select the **Public IP address** menu item.</span><span class="sxs-lookup"><span data-stu-id="674f4-244">Select the **Public IP address** menu item.</span></span> <span data-ttu-id="674f4-245">When the **Choose public IP address** section opens, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="674f4-245">When the **Choose public IP address** section opens, select **Create new**.</span></span>
7. <span data-ttu-id="674f4-246">In **Name**, type **Azs-GW-PiP**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-246">In **Name**, type **Azs-GW-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="674f4-247">By default, **Route-based** is selected for **VPN type**.</span><span class="sxs-lookup"><span data-stu-id="674f4-247">By default, **Route-based** is selected for **VPN type**.</span></span> <span data-ttu-id="674f4-248">Keep the **Route-based** VPN type.</span><span class="sxs-lookup"><span data-stu-id="674f4-248">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="674f4-249">Verify that **Subscription** and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="674f4-249">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="674f4-250">You can pin the resource to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="674f4-250">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="674f4-251">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-251">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway"></a><span data-ttu-id="674f4-252">Create the local network gateway</span><span class="sxs-lookup"><span data-stu-id="674f4-252">Create the local network gateway</span></span>

<span data-ttu-id="674f4-253">The concept of a *local network gateway* in Azure Stack is a bit different than in an Azure deployment.</span><span class="sxs-lookup"><span data-stu-id="674f4-253">The concept of a *local network gateway* in Azure Stack is a bit different than in an Azure deployment.</span></span>

<span data-ttu-id="674f4-254">In an Azure deployment, a local network gateway represents an on-premises (at the user location) physical device that you connect to a virtual network gateway in Azure.</span><span class="sxs-lookup"><span data-stu-id="674f4-254">In an Azure deployment, a local network gateway represents an on-premises (at the user location) physical device that you connect to a virtual network gateway in Azure.</span></span> <span data-ttu-id="674f4-255">But in Azure Stack, both ends of the connection are virtual network gateways!</span><span class="sxs-lookup"><span data-stu-id="674f4-255">But in Azure Stack, both ends of the connection are virtual network gateways!</span></span>

<span data-ttu-id="674f4-256">A more generic way to think about this is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span><span class="sxs-lookup"><span data-stu-id="674f4-256">A more generic way to think about this is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="674f4-257">Create the local network gateway resource</span><span class="sxs-lookup"><span data-stu-id="674f4-257">Create the local network gateway resource</span></span>

1. <span data-ttu-id="674f4-258">Sign in to the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="674f4-258">Sign in to the Azure Stack portal.</span></span>
2. <span data-ttu-id="674f4-259">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-259">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="674f4-260">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-260">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="674f4-261">From the list of resources, select **local network gateway**.</span><span class="sxs-lookup"><span data-stu-id="674f4-261">From the list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="674f4-262">In **Name**, type **Azure-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-262">In **Name**, type **Azure-GW**.</span></span>
6. <span data-ttu-id="674f4-263">In **IP address**, type the Public IP Address for the virtual network gateway in Azure **Azure-GW-PiP**.</span><span class="sxs-lookup"><span data-stu-id="674f4-263">In **IP address**, type the Public IP Address for the virtual network gateway in Azure **Azure-GW-PiP**.</span></span> <span data-ttu-id="674f4-264">This address appears earlier in the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="674f4-264">This address appears earlier in the network configuration table.</span></span>
7. <span data-ttu-id="674f4-265">In **Address Space**, for the address space of the Azure VNET that you created, type **10.100.0.0/24** and **10.100.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-265">In **Address Space**, for the address space of the Azure VNET that you created, type **10.100.0.0/24** and **10.100.1.0/24**.</span></span>
8. <span data-ttu-id="674f4-266">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="674f4-266">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="674f4-267">Create the connection</span><span class="sxs-lookup"><span data-stu-id="674f4-267">Create the connection</span></span>

1. <span data-ttu-id="674f4-268">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-268">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-269">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="674f4-269">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="674f4-270">From the list of resources, select **Connection**.</span><span class="sxs-lookup"><span data-stu-id="674f4-270">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="674f4-271">On the **Basics** settings section, for the **Connection type**, select **Site-to-site (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="674f4-271">On the **Basics** settings section, for the **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="674f4-272">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-272">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="674f4-273">On the **Settings** section,  select **Virtual network gateway**, and then select **Azs-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-273">On the **Settings** section,  select **Virtual network gateway**, and then select **Azs-GW**.</span></span>
7. <span data-ttu-id="674f4-274">Select **Local network gateway**, and then select **Azure-GW**.</span><span class="sxs-lookup"><span data-stu-id="674f4-274">Select **Local network gateway**, and then select **Azure-GW**.</span></span>
8. <span data-ttu-id="674f4-275">In **Connection Name**, type **Azs-Azure**.</span><span class="sxs-lookup"><span data-stu-id="674f4-275">In **Connection Name**, type **Azs-Azure**.</span></span>
9. <span data-ttu-id="674f4-276">In **Shared key (PSK)**, type **12345**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-276">In **Shared key (PSK)**, type **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="674f4-277">On the **Summary** section, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-277">On the **Summary** section, select **OK**.</span></span>

### <a name="create-a-virtual-machine-vm"></a><span data-ttu-id="674f4-278">Create a virtual machine (VM)</span><span class="sxs-lookup"><span data-stu-id="674f4-278">Create a virtual machine (VM)</span></span>

<span data-ttu-id="674f4-279">To check the VPN connection, you need to create two VMs, one in Azure, and one in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="674f4-279">To check the VPN connection, you need to create two VMs, one in Azure, and one in Azure Stack.</span></span> <span data-ttu-id="674f4-280">After you create these VMs, you can use them to send and receive data through the VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="674f4-280">After you create these VMs, you can use them to send and receive data through the VPN tunnel.</span></span>

1. <span data-ttu-id="674f4-281">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="674f4-281">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="674f4-282">Go to **Marketplace**, and then select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="674f4-282">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="674f4-283">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Oval** image.</span><span class="sxs-lookup"><span data-stu-id="674f4-283">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Oval** image.</span></span>
4. <span data-ttu-id="674f4-284">On the **Basics** section, in **Name**, type **Azs-VM**.</span><span class="sxs-lookup"><span data-stu-id="674f4-284">On the **Basics** section, in **Name**, type **Azs-VM**.</span></span>
5. <span data-ttu-id="674f4-285">Type a valid username and password.</span><span class="sxs-lookup"><span data-stu-id="674f4-285">Type a valid username and password.</span></span> <span data-ttu-id="674f4-286">You use this account to sign in to the VM after it's created.</span><span class="sxs-lookup"><span data-stu-id="674f4-286">You use this account to sign in to the VM after it's created.</span></span>
6. <span data-ttu-id="674f4-287">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-287">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="674f4-288">On the **Size** section, for this instance, select a virtual machine size, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="674f4-288">On the **Size** section, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="674f4-289">On the **Settings** section, accept the defaults.</span><span class="sxs-lookup"><span data-stu-id="674f4-289">On the **Settings** section, accept the defaults.</span></span> <span data-ttu-id="674f4-290">Make sure that the **Azs-VNet** virtual network is selected.</span><span class="sxs-lookup"><span data-stu-id="674f4-290">Make sure that the **Azs-VNet** virtual network is selected.</span></span> <span data-ttu-id="674f4-291">Verify that the subnet is set to **10.1.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-291">Verify that the subnet is set to **10.1.0.0/24**.</span></span> <span data-ttu-id="674f4-292">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-292">Then select **OK**.</span></span>
9. <span data-ttu-id="674f4-293">On the **Summary** section, review the settings, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="674f4-293">On the **Summary** section, review the settings, and then select **OK**.</span></span>

## <a name="test-the-connection"></a><span data-ttu-id="674f4-294">Test the connection</span><span class="sxs-lookup"><span data-stu-id="674f4-294">Test the connection</span></span>

<span data-ttu-id="674f4-295">After the site-to-site connection is established, you should verify that you can get data flowing in both directions.</span><span class="sxs-lookup"><span data-stu-id="674f4-295">After the site-to-site connection is established, you should verify that you can get data flowing in both directions.</span></span> <span data-ttu-id="674f4-296">The easiest way to test the connection is by doing a ping test:</span><span class="sxs-lookup"><span data-stu-id="674f4-296">The easiest way to test the connection is by doing a ping test:</span></span>

* <span data-ttu-id="674f4-297">Sign in to the virtual machine you created in Azure Stack and ping the virtual machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="674f4-297">Sign in to the virtual machine you created in Azure Stack and ping the virtual machine in Azure.</span></span>
* <span data-ttu-id="674f4-298">Sign in to the virtual machine you created in Azure and ping the virtual machine in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="674f4-298">Sign in to the virtual machine you created in Azure and ping the virtual machine in Azure Stack.</span></span>

>[!NOTE]
><span data-ttu-id="674f4-299">To make sure that you're sending traffic through the site-to-site connection, ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span><span class="sxs-lookup"><span data-stu-id="674f4-299">To make sure that you're sending traffic through the site-to-site connection, ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span></span>

### <a name="sign-in-to-the-user-vm-in-azure-stack"></a><span data-ttu-id="674f4-300">Sign in to the user VM in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="674f4-300">Sign in to the user VM in Azure Stack</span></span>

1. <span data-ttu-id="674f4-301">Sign in to the Azure Stack portal.</span><span class="sxs-lookup"><span data-stu-id="674f4-301">Sign in to the Azure Stack portal.</span></span>
2. <span data-ttu-id="674f4-302">In the left navigation bar, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="674f4-302">In the left navigation bar, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="674f4-303">In the list of VMs, find **Azs-VM** that you created previously, and then select it.</span><span class="sxs-lookup"><span data-stu-id="674f4-303">In the list of VMs, find **Azs-VM** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="674f4-304">On the section for the virtual machine, select **Connect**, and then open the Azs-VM.rdp file.</span><span class="sxs-lookup"><span data-stu-id="674f4-304">On the section for the virtual machine, select **Connect**, and then open the Azs-VM.rdp file.</span></span>

     ![Connect button](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)

5. <span data-ttu-id="674f4-306">Sign in with the account that you configured when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="674f4-306">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="674f4-307">Open an elevated **Windows PowerShell** window.</span><span class="sxs-lookup"><span data-stu-id="674f4-307">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="674f4-308">Type **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="674f4-308">Type **ipconfig /all**.</span></span>
8. <span data-ttu-id="674f4-309">In the output, find the **IPv4 Address**, and then save the address for later use.</span><span class="sxs-lookup"><span data-stu-id="674f4-309">In the output, find the **IPv4 Address**, and then save the address for later use.</span></span> <span data-ttu-id="674f4-310">This is the address that you will ping from Azure.</span><span class="sxs-lookup"><span data-stu-id="674f4-310">This is the address that you will ping from Azure.</span></span> <span data-ttu-id="674f4-311">In the example environment, the address is **10.1.0.4**, but in your environment it might be different.</span><span class="sxs-lookup"><span data-stu-id="674f4-311">In the example environment, the address is **10.1.0.4**, but in your environment it might be different.</span></span> <span data-ttu-id="674f4-312">It should fall within the **10.1.0.0/24** subnet that you created previously.</span><span class="sxs-lookup"><span data-stu-id="674f4-312">It should fall within the **10.1.0.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="674f4-313">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="674f4-313">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-azure"></a><span data-ttu-id="674f4-314">Sign in to the tenant VM in Azure</span><span class="sxs-lookup"><span data-stu-id="674f4-314">Sign in to the tenant VM in Azure</span></span>

1. <span data-ttu-id="674f4-315">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="674f4-315">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="674f4-316">In the left navigation bar, select **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="674f4-316">In the left navigation bar, select **Virtual Machines**.</span></span>
3. <span data-ttu-id="674f4-317">From the list of virtual machines, find **Azure-VM** that you created previously, and then select it.</span><span class="sxs-lookup"><span data-stu-id="674f4-317">From the list of virtual machines, find **Azure-VM** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="674f4-318">On the section for the virtual machine, select **Connect**.</span><span class="sxs-lookup"><span data-stu-id="674f4-318">On the section for the virtual machine, select **Connect**.</span></span>
5. <span data-ttu-id="674f4-319">Sign in with the account that you configured when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="674f4-319">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="674f4-320">Open an elevated **Windows PowerShell** window.</span><span class="sxs-lookup"><span data-stu-id="674f4-320">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="674f4-321">Type **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="674f4-321">Type **ipconfig /all**.</span></span>
8. <span data-ttu-id="674f4-322">You should see an IPv4 address that falls within **10.100.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="674f4-322">You should see an IPv4 address that falls within **10.100.0.0/24**.</span></span> <span data-ttu-id="674f4-323">In the example environment, the address is **10.100.0.4**, but your address might be different.</span><span class="sxs-lookup"><span data-stu-id="674f4-323">In the example environment, the address is **10.100.0.4**, but your address might be different.</span></span>
9. <span data-ttu-id="674f4-324">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="674f4-324">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="674f4-325">From the virtual machine in Azure, ping the virtual machine in Azure Stack, through the tunnel.</span><span class="sxs-lookup"><span data-stu-id="674f4-325">From the virtual machine in Azure, ping the virtual machine in Azure Stack, through the tunnel.</span></span> <span data-ttu-id="674f4-326">To do this, you ping the DIP that you recorded from Azs-VM.</span><span class="sxs-lookup"><span data-stu-id="674f4-326">To do this, you ping the DIP that you recorded from Azs-VM.</span></span> <span data-ttu-id="674f4-327">In the example environment, this is **10.1.0.4**, but be sure to ping the address you noted in your lab.</span><span class="sxs-lookup"><span data-stu-id="674f4-327">In the example environment, this is **10.1.0.4**, but be sure to ping the address you noted in your lab.</span></span> <span data-ttu-id="674f4-328">You should see a result that looks like the following screen capture:</span><span class="sxs-lookup"><span data-stu-id="674f4-328">You should see a result that looks like the following screen capture:</span></span>

    ![Successful ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)

11. <span data-ttu-id="674f4-330">A reply from the remote virtual machine indicates a successful test!</span><span class="sxs-lookup"><span data-stu-id="674f4-330">A reply from the remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="674f4-331">You can close the virtual machine window.</span><span class="sxs-lookup"><span data-stu-id="674f4-331">You can close the virtual machine window.</span></span>

<span data-ttu-id="674f4-332">You should also do more rigorous data transfer testing.</span><span class="sxs-lookup"><span data-stu-id="674f4-332">You should also do more rigorous data transfer testing.</span></span> <span data-ttu-id="674f4-333">For example, copying different sized files in both directions.</span><span class="sxs-lookup"><span data-stu-id="674f4-333">For example, copying different sized files in both directions.</span></span>

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a><span data-ttu-id="674f4-334">Viewing data transfer statistics through the gateway connection</span><span class="sxs-lookup"><span data-stu-id="674f4-334">Viewing data transfer statistics through the gateway connection</span></span>

<span data-ttu-id="674f4-335">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** section.</span><span class="sxs-lookup"><span data-stu-id="674f4-335">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** section.</span></span> <span data-ttu-id="674f4-336">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span><span class="sxs-lookup"><span data-stu-id="674f4-336">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span></span>

1. <span data-ttu-id="674f4-337">While you're signed in to the user virtual machine in Azure Stack, use your user account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="674f4-337">While you're signed in to the user virtual machine in Azure Stack, use your user account to sign in to the user portal.</span></span>
2. <span data-ttu-id="674f4-338">Go to **All resources**, and then select the **Azs-Azure** connection.</span><span class="sxs-lookup"><span data-stu-id="674f4-338">Go to **All resources**, and then select the **Azs-Azure** connection.</span></span> <span data-ttu-id="674f4-339">**Connections** appears.</span><span class="sxs-lookup"><span data-stu-id="674f4-339">**Connections** appears.</span></span>
3. <span data-ttu-id="674f4-340">On the **Connection** section, the statistics for **Data in** and **Data out** appear.</span><span class="sxs-lookup"><span data-stu-id="674f4-340">On the **Connection** section, the statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="674f4-341">In the following screen capture, the large numbers are attributed to additional file transfer.</span><span class="sxs-lookup"><span data-stu-id="674f4-341">In the following screen capture, the large numbers are attributed to additional file transfer.</span></span> <span data-ttu-id="674f4-342">You should see some nonzero values there.</span><span class="sxs-lookup"><span data-stu-id="674f4-342">You should see some nonzero values there.</span></span>

    ![Data in and out](media/azure-stack-connect-vpn/Connection.png)

## <a name="next-steps"></a><span data-ttu-id="674f4-344">Next steps</span><span class="sxs-lookup"><span data-stu-id="674f4-344">Next steps</span></span>

[<span data-ttu-id="674f4-345">Deploy apps to Azure and Azure Stack</span><span class="sxs-lookup"><span data-stu-id="674f4-345">Deploy apps to Azure and Azure Stack</span></span>](azure-stack-solution-pipeline.md)
