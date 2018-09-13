---
title: Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments | Microsoft Docs
description: Step-by-step procedure that a cloud administrator uses to create a site-to-site VPN connection between two single-node Azure Stack Development Kit environments.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: 3f1b4e02-dbab-46a3-8e11-a777722120ec
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 7/10/2017
ms.author: brenduns
ms.reviewer: scottnap
ROBOTS: NOINDEX
ms.openlocfilehash: 6225a12b50ebb7bf0a0cb9244153800ba734d93a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867701"
---
# <a name="create-a-site-to-site-vpn-connection-between-two-virtual-networks-in-different-azure-stack-development-kit-environments"></a><span data-ttu-id="b2b4b-103">Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments</span><span class="sxs-lookup"><span data-stu-id="b2b4b-103">Create a site-to-site VPN connection between two virtual networks in different Azure Stack Development Kit environments</span></span>
## <a name="overview"></a><span data-ttu-id="b2b4b-104">Overview</span><span class="sxs-lookup"><span data-stu-id="b2b4b-104">Overview</span></span>
<span data-ttu-id="b2b4b-105">This article shows you how to create a site-to-site VPN connection between two virtual networks in two separate Azure Stack Development Kit environments.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-105">This article shows you how to create a site-to-site VPN connection between two virtual networks in two separate Azure Stack Development Kit environments.</span></span> <span data-ttu-id="b2b4b-106">While you configure the connections, you learn how VPN gateways in Azure Stack work.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-106">While you configure the connections, you learn how VPN gateways in Azure Stack work.</span></span>

### <a name="connection-diagram"></a><span data-ttu-id="b2b4b-107">Connection diagram</span><span class="sxs-lookup"><span data-stu-id="b2b4b-107">Connection diagram</span></span>
<span data-ttu-id="b2b4b-108">The following diagram shows what the connection configuration should look like when you’re done.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-108">The following diagram shows what the connection configuration should look like when you’re done.</span></span>

![Site-to-site VPN connection configuration](media/azure-stack-create-vpn-connection-one-node-tp2/OneNodeS2SVPN.png)

### <a name="before-you-begin"></a><span data-ttu-id="b2b4b-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="b2b4b-110">Before you begin</span></span>
<span data-ttu-id="b2b4b-111">To complete the connection configuration, ensure that you have the following items before you begin:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-111">To complete the connection configuration, ensure that you have the following items before you begin:</span></span>

* <span data-ttu-id="b2b4b-112">Two servers and other prerequisites that meet the Azure Stack Development Kit hardware requirements, as described in [Quickstart: Evaluate the Azure Stack Development Kit](azure-stack-deploy-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b2b4b-112">Two servers and other prerequisites that meet the Azure Stack Development Kit hardware requirements, as described in [Quickstart: Evaluate the Azure Stack Development Kit](azure-stack-deploy-overview.md).</span></span> 
* <span data-ttu-id="b2b4b-113">The [Azure Stack Development Kit](https://azure.microsoft.com/overview/azure-stack/try/) deployment package.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-113">The [Azure Stack Development Kit](https://azure.microsoft.com/overview/azure-stack/try/) deployment package.</span></span>

## <a name="deploy-the-azure-stack-development-kit-environments"></a><span data-ttu-id="b2b4b-114">Deploy the Azure Stack Development Kit environments</span><span class="sxs-lookup"><span data-stu-id="b2b4b-114">Deploy the Azure Stack Development Kit environments</span></span>
<span data-ttu-id="b2b4b-115">To complete the connection configuration, you must deploy two Azure Stack Development Kit environments.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-115">To complete the connection configuration, you must deploy two Azure Stack Development Kit environments.</span></span>
> [!NOTE] 
> <span data-ttu-id="b2b4b-116">For each Azure Stack Development Kit that you deploy, follow the [deployment instructions](azure-stack-run-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="b2b4b-116">For each Azure Stack Development Kit that you deploy, follow the [deployment instructions](azure-stack-run-powershell-script.md).</span></span> <span data-ttu-id="b2b4b-117">In this article, the Azure Stack Development Kit environments are called *POC1* and *POC2*.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-117">In this article, the Azure Stack Development Kit environments are called *POC1* and *POC2*.</span></span>


## <a name="prepare-an-offer-on-poc1-and-poc2"></a><span data-ttu-id="b2b4b-118">Prepare an offer on POC1 and POC2</span><span class="sxs-lookup"><span data-stu-id="b2b4b-118">Prepare an offer on POC1 and POC2</span></span>
<span data-ttu-id="b2b4b-119">On both POC1 and POC2, prepare an offer so that a user can subscribe to the offer and deploy the virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-119">On both POC1 and POC2, prepare an offer so that a user can subscribe to the offer and deploy the virtual machines.</span></span> <span data-ttu-id="b2b4b-120">For information on how to create an offer, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span><span class="sxs-lookup"><span data-stu-id="b2b4b-120">For information on how to create an offer, see [Make virtual machines available to your Azure Stack users](azure-stack-tutorial-tenant-vm.md).</span></span>

## <a name="review-and-complete-the-network-configuration-table"></a><span data-ttu-id="b2b4b-121">Review and complete the network configuration table</span><span class="sxs-lookup"><span data-stu-id="b2b4b-121">Review and complete the network configuration table</span></span>
<span data-ttu-id="b2b4b-122">The following table summarizes the network configuration for both Azure Stack Development Kit environments.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-122">The following table summarizes the network configuration for both Azure Stack Development Kit environments.</span></span> <span data-ttu-id="b2b4b-123">Use the procedure that appears after the table to add the External BGPNAT address that is specific for your network.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-123">Use the procedure that appears after the table to add the External BGPNAT address that is specific for your network.</span></span>

<span data-ttu-id="b2b4b-124">**Network configuration table**</span><span class="sxs-lookup"><span data-stu-id="b2b4b-124">**Network configuration table**</span></span>
|   |<span data-ttu-id="b2b4b-125">POC1</span><span class="sxs-lookup"><span data-stu-id="b2b4b-125">POC1</span></span>|<span data-ttu-id="b2b4b-126">POC2</span><span class="sxs-lookup"><span data-stu-id="b2b4b-126">POC2</span></span>|
|---------|---------|---------|
|<span data-ttu-id="b2b4b-127">Virtual network name</span><span class="sxs-lookup"><span data-stu-id="b2b4b-127">Virtual network name</span></span>     |<span data-ttu-id="b2b4b-128">VNET-01</span><span class="sxs-lookup"><span data-stu-id="b2b4b-128">VNET-01</span></span>|<span data-ttu-id="b2b4b-129">VNET-02</span><span class="sxs-lookup"><span data-stu-id="b2b4b-129">VNET-02</span></span> |
|<span data-ttu-id="b2b4b-130">Virtual network address space</span><span class="sxs-lookup"><span data-stu-id="b2b4b-130">Virtual network address space</span></span> |<span data-ttu-id="b2b4b-131">10.0.10.0/23</span><span class="sxs-lookup"><span data-stu-id="b2b4b-131">10.0.10.0/23</span></span>|<span data-ttu-id="b2b4b-132">10.0.20.0/23</span><span class="sxs-lookup"><span data-stu-id="b2b4b-132">10.0.20.0/23</span></span>|
|<span data-ttu-id="b2b4b-133">Subnet name</span><span class="sxs-lookup"><span data-stu-id="b2b4b-133">Subnet name</span></span>     |<span data-ttu-id="b2b4b-134">Subnet-01</span><span class="sxs-lookup"><span data-stu-id="b2b4b-134">Subnet-01</span></span>|<span data-ttu-id="b2b4b-135">Subnet-02</span><span class="sxs-lookup"><span data-stu-id="b2b4b-135">Subnet-02</span></span>|
|<span data-ttu-id="b2b4b-136">Subnet address range</span><span class="sxs-lookup"><span data-stu-id="b2b4b-136">Subnet address range</span></span>|<span data-ttu-id="b2b4b-137">10.0.10.0/24</span><span class="sxs-lookup"><span data-stu-id="b2b4b-137">10.0.10.0/24</span></span> |<span data-ttu-id="b2b4b-138">10.0.20.0/24</span><span class="sxs-lookup"><span data-stu-id="b2b4b-138">10.0.20.0/24</span></span> |
|<span data-ttu-id="b2b4b-139">Gateway subnet</span><span class="sxs-lookup"><span data-stu-id="b2b4b-139">Gateway subnet</span></span>     |<span data-ttu-id="b2b4b-140">10.0.11.0/24</span><span class="sxs-lookup"><span data-stu-id="b2b4b-140">10.0.11.0/24</span></span>|<span data-ttu-id="b2b4b-141">10.0.21.0/24</span><span class="sxs-lookup"><span data-stu-id="b2b4b-141">10.0.21.0/24</span></span>|
|<span data-ttu-id="b2b4b-142">External BGPNAT address</span><span class="sxs-lookup"><span data-stu-id="b2b4b-142">External BGPNAT address</span></span>     |         |         |

> [!NOTE]
> <span data-ttu-id="b2b4b-143">The external BGPNAT IP addresses in the example environment are 10.16.167.195 for POC1, and 10.16.169.131 for POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-143">The external BGPNAT IP addresses in the example environment are 10.16.167.195 for POC1, and 10.16.169.131 for POC2.</span></span> <span data-ttu-id="b2b4b-144">Use the following procedure to determine the external BGPNAT IP addresses for your Azure Stack Development Kit hosts, and then add them to the previous network configuration table.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-144">Use the following procedure to determine the external BGPNAT IP addresses for your Azure Stack Development Kit hosts, and then add them to the previous network configuration table.</span></span>


### <a name="get-the-ip-address-of-the-external-adapter-of-the-nat-vm"></a><span data-ttu-id="b2b4b-145">Get the IP address of the external adapter of the NAT VM</span><span class="sxs-lookup"><span data-stu-id="b2b4b-145">Get the IP address of the external adapter of the NAT VM</span></span>
1. <span data-ttu-id="b2b4b-146">Sign in to the Azure Stack physical machine for POC1.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-146">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="b2b4b-147">Edit the following Powershell code to replace your administrator password, and then run the code on the POC host:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-147">Edit the following Powershell code to replace your administrator password, and then run the code on the POC host:</span></span>

   ```powershell
   cd \AzureStack-Tools-master\connect
   Import-Module .\AzureStack.Connect.psm1
   $Password = ConvertTo-SecureString "<your administrator password>" `
    -AsPlainText `
    -Force
   Get-AzureStackNatServerAddress `
    -HostComputer "AzS-bgpnat01" `
    -Password $Password
   ```
3. <span data-ttu-id="b2b4b-148">Add the IP address to the network configuration table that appears in the previous section.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-148">Add the IP address to the network configuration table that appears in the previous section.</span></span>

4. <span data-ttu-id="b2b4b-149">Repeat this procedure on POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-149">Repeat this procedure on POC2.</span></span>

## <a name="create-the-network-resources-in-poc1"></a><span data-ttu-id="b2b4b-150">Create the network resources in POC1</span><span class="sxs-lookup"><span data-stu-id="b2b4b-150">Create the network resources in POC1</span></span>
<span data-ttu-id="b2b4b-151">Now you create the POC1 network resources that you need to set up your gateways.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-151">Now you create the POC1 network resources that you need to set up your gateways.</span></span> <span data-ttu-id="b2b4b-152">The following instructions show you how to create the resources by using the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-152">The following instructions show you how to create the resources by using the user portal.</span></span> <span data-ttu-id="b2b4b-153">You can also use PowerShell code to create the resources.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-153">You can also use PowerShell code to create the resources.</span></span>

![Workflow that is used to create resources](media/azure-stack-create-vpn-connection-one-node-tp2/image2.png)

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="b2b4b-155">Sign in as a tenant</span><span class="sxs-lookup"><span data-stu-id="b2b4b-155">Sign in as a tenant</span></span>
<span data-ttu-id="b2b4b-156">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-156">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="b2b4b-157">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-157">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="b2b4b-158">Create the virtual network and VM subnet</span><span class="sxs-lookup"><span data-stu-id="b2b4b-158">Create the virtual network and VM subnet</span></span>
1. <span data-ttu-id="b2b4b-159">Use a tenant account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-159">Use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="b2b4b-160">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-160">In the user portal, select **New**.</span></span>

    ![Create new virtual network](media/azure-stack-create-vpn-connection-one-node-tp2/image3.png)

3. <span data-ttu-id="b2b4b-162">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-162">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b2b4b-163">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-163">Select **Virtual network**.</span></span>
5. <span data-ttu-id="b2b4b-164">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values that appear earlier in the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-164">For **Name**, **Address space**, **Subnet name**, and **Subnet address range**, use the values that appear earlier in the network configuration table.</span></span>
6. <span data-ttu-id="b2b4b-165">In **Subscription**, the subscription that you created earlier appears.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-165">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="b2b4b-166">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-166">For **Resource Group**, you can either create a resource group or if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="b2b4b-167">Verify the default location.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-167">Verify the default location.</span></span>
9. <span data-ttu-id="b2b4b-168">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-168">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="b2b4b-169">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-169">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="b2b4b-170">Create the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="b2b4b-170">Create the gateway subnet</span></span>
1. <span data-ttu-id="b2b4b-171">On the dashboard, open the VNET-01 virtual network resource that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-171">On the dashboard, open the VNET-01 virtual network resource that you created earlier.</span></span>
2. <span data-ttu-id="b2b4b-172">On the **Settings** blade, select **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-172">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="b2b4b-173">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-173">To add a gateway subnet to the virtual network, select **Gateway Subnet**.</span></span>
   
    ![Add gateway subnet](media/azure-stack-create-vpn-connection-one-node-tp2/image4.png)

4. <span data-ttu-id="b2b4b-175">By default, the subnet name is set to **GatewaySubnet**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-175">By default, the subnet name is set to **GatewaySubnet**.</span></span>
   <span data-ttu-id="b2b4b-176">Gateway subnets are special.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-176">Gateway subnets are special.</span></span> <span data-ttu-id="b2b4b-177">To function properly, they must use the *GatewaySubnet* name.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-177">To function properly, they must use the *GatewaySubnet* name.</span></span>
5. <span data-ttu-id="b2b4b-178">In **Address range**, verify that the address is **10.0.11.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-178">In **Address range**, verify that the address is **10.0.11.0/24**.</span></span>
6. <span data-ttu-id="b2b4b-179">Select **OK** to create the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-179">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="b2b4b-180">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="b2b4b-180">Create the virtual network gateway</span></span>
1. <span data-ttu-id="b2b4b-181">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-181">In the Azure portal, select **New**.</span></span> 
2. <span data-ttu-id="b2b4b-182">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-182">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b2b4b-183">From the list of network resources, select **Virtual network gateway**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-183">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="b2b4b-184">In **Name**, enter **GW1**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-184">In **Name**, enter **GW1**.</span></span>
5. <span data-ttu-id="b2b4b-185">Select the **Virtual network** item to choose a virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-185">Select the **Virtual network** item to choose a virtual network.</span></span>
   <span data-ttu-id="b2b4b-186">Select **VNET-01** from the list.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-186">Select **VNET-01** from the list.</span></span>
6. <span data-ttu-id="b2b4b-187">Select the **Public IP address** menu item.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-187">Select the **Public IP address** menu item.</span></span> <span data-ttu-id="b2b4b-188">When the **Choose public IP address** blade opens, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-188">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="b2b4b-189">In **Name**, enter **GW1-PiP**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-189">In **Name**, enter **GW1-PiP**, and then select **OK**.</span></span>
8.  <span data-ttu-id="b2b4b-190">By default, for **VPN type**, **Route-based** is selected.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-190">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="b2b4b-191">Keep the **Route-based** VPN type.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-191">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="b2b4b-192">Verify that **Subscription** and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-192">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="b2b4b-193">You can pin the resource to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-193">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="b2b4b-194">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-194">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway"></a><span data-ttu-id="b2b4b-195">Create the local network gateway</span><span class="sxs-lookup"><span data-stu-id="b2b4b-195">Create the local network gateway</span></span>
<span data-ttu-id="b2b4b-196">The implementation of a *local network gateway* in this Azure Stack evaluation deployment is a bit different than in an actual Azure deployment.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-196">The implementation of a *local network gateway* in this Azure Stack evaluation deployment is a bit different than in an actual Azure deployment.</span></span>

<span data-ttu-id="b2b4b-197">In an Azure deployment, a local network gateway represents an on-premises (at the tenant) physical device, that you use to connect to a virtual network gateway in Azure.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-197">In an Azure deployment, a local network gateway represents an on-premises (at the tenant) physical device, that you use to connect to a virtual network gateway in Azure.</span></span> <span data-ttu-id="b2b4b-198">In this Azure Stack evaluation deployment, both ends of the connection are virtual network gateways!</span><span class="sxs-lookup"><span data-stu-id="b2b4b-198">In this Azure Stack evaluation deployment, both ends of the connection are virtual network gateways!</span></span>

<span data-ttu-id="b2b4b-199">A way to think about this more generically is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-199">A way to think about this more generically is that the local network gateway resource always indicates the remote gateway at the other end of the connection.</span></span> <span data-ttu-id="b2b4b-200">Because of the way the Azure Stack Development Kit was designed, you need to provide the IP address of the external network adapter on the network address translation (NAT) VM of the other Azure Stack Development Kit as the Public IP Address of the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-200">Because of the way the Azure Stack Development Kit was designed, you need to provide the IP address of the external network adapter on the network address translation (NAT) VM of the other Azure Stack Development Kit as the Public IP Address of the local network gateway.</span></span> <span data-ttu-id="b2b4b-201">You then create NAT mappings on the NAT VM to make sure that both ends are connected properly.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-201">You then create NAT mappings on the NAT VM to make sure that both ends are connected properly.</span></span>


### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="b2b4b-202">Create the local network gateway resource</span><span class="sxs-lookup"><span data-stu-id="b2b4b-202">Create the local network gateway resource</span></span>
1. <span data-ttu-id="b2b4b-203">Sign in to the Azure Stack physical machine for POC1.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-203">Sign in to the Azure Stack physical machine for POC1.</span></span>
2. <span data-ttu-id="b2b4b-204">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-204">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="b2b4b-205">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-205">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b2b4b-206">From the list of resources, select **local network gateway**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-206">From the list of resources, select **local network gateway**.</span></span>
5. <span data-ttu-id="b2b4b-207">In **Name**, enter **POC2-GW**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-207">In **Name**, enter **POC2-GW**.</span></span>
6. <span data-ttu-id="b2b4b-208">In **IP address**, enter the External BGPNAT address for POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-208">In **IP address**, enter the External BGPNAT address for POC2.</span></span> <span data-ttu-id="b2b4b-209">This address appears earlier in the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-209">This address appears earlier in the network configuration table.</span></span>
7. <span data-ttu-id="b2b4b-210">In **Address Space**, for the address space of the POC2 VNET that you create later, enter **10.0.20.0/23**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-210">In **Address Space**, for the address space of the POC2 VNET that you create later, enter **10.0.20.0/23**.</span></span>
8. <span data-ttu-id="b2b4b-211">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-211">Verify that your **Subscription**, **Resource Group**, and **location** are correct, and then select **Create**.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="b2b4b-212">Create the connection</span><span class="sxs-lookup"><span data-stu-id="b2b4b-212">Create the connection</span></span>
1. <span data-ttu-id="b2b4b-213">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-213">In the user portal, select **New**.</span></span>
2. <span data-ttu-id="b2b4b-214">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-214">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b2b4b-215">From the list of resources, select **Connection**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-215">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="b2b4b-216">On the **Basics** settings blade, for the **Connection type**, select **Site-to-site (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-216">On the **Basics** settings blade, for the **Connection type**, select **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="b2b4b-217">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-217">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="b2b4b-218">On the **Settings** blade,  select **Virtual network gateway**, and then select **GW1**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-218">On the **Settings** blade,  select **Virtual network gateway**, and then select **GW1**.</span></span>
7. <span data-ttu-id="b2b4b-219">Select **Local network gateway**, and then select **POC2-GW**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-219">Select **Local network gateway**, and then select **POC2-GW**.</span></span>
8. <span data-ttu-id="b2b4b-220">In **Connection Name**, enter **POC1-POC2**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-220">In **Connection Name**, enter **POC1-POC2**.</span></span>
9. <span data-ttu-id="b2b4b-221">In **Shared key (PSK)**, enter **12345**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-221">In **Shared key (PSK)**, enter **12345**, and then select **OK**.</span></span>
10. <span data-ttu-id="b2b4b-222">On the **Summary** blade, select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-222">On the **Summary** blade, select **OK**.</span></span>

### <a name="create-a-vm"></a><span data-ttu-id="b2b4b-223">Create a VM</span><span class="sxs-lookup"><span data-stu-id="b2b4b-223">Create a VM</span></span>
<span data-ttu-id="b2b4b-224">To validate the data that travels through the VPN connection, you need the virtual machines to send and receive data in each Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-224">To validate the data that travels through the VPN connection, you need the virtual machines to send and receive data in each Azure Stack Development Kit.</span></span> <span data-ttu-id="b2b4b-225">Create a virtual machine in POC1 now, and then in your virtual network, put it on your VM subnet.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-225">Create a virtual machine in POC1 now, and then in your virtual network, put it on your VM subnet.</span></span>

1. <span data-ttu-id="b2b4b-226">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-226">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="b2b4b-227">Go to **Marketplace**, and then select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-227">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="b2b4b-228">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-228">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="b2b4b-229">On the **Basics** blade, in **Name**, enter **VM01**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-229">On the **Basics** blade, in **Name**, enter **VM01**.</span></span>
5. <span data-ttu-id="b2b4b-230">Enter a valid username and password.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-230">Enter a valid username and password.</span></span> <span data-ttu-id="b2b4b-231">You use this account to sign in to the VM after it's created.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-231">You use this account to sign in to the VM after it's created.</span></span>
6. <span data-ttu-id="b2b4b-232">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-232">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="b2b4b-233">On the **Size** blade, for this instance, select a virtual machine size, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-233">On the **Size** blade, for this instance, select a virtual machine size, and then select **Select**.</span></span>
8. <span data-ttu-id="b2b4b-234">On the **Settings** blade, accept the defaults.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-234">On the **Settings** blade, accept the defaults.</span></span> <span data-ttu-id="b2b4b-235">Ensure that the **VNET-01** virtual network is selected.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-235">Ensure that the **VNET-01** virtual network is selected.</span></span> <span data-ttu-id="b2b4b-236">Verify that the subnet is set to **10.0.10.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-236">Verify that the subnet is set to **10.0.10.0/24**.</span></span> <span data-ttu-id="b2b4b-237">Then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-237">Then select **OK**.</span></span>
9. <span data-ttu-id="b2b4b-238">On the **Summary** blade, review the settings, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-238">On the **Summary** blade, review the settings, and then select **OK**.</span></span>



## <a name="create-the-network-resources-in-poc2"></a><span data-ttu-id="b2b4b-239">Create the network resources in POC2</span><span class="sxs-lookup"><span data-stu-id="b2b4b-239">Create the network resources in POC2</span></span>

<span data-ttu-id="b2b4b-240">The next step is to create the network resources for POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-240">The next step is to create the network resources for POC2.</span></span> <span data-ttu-id="b2b4b-241">The following instructions show how to create the resources by using the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-241">The following instructions show how to create the resources by using the user portal.</span></span>

### <a name="sign-in-as-a-tenant"></a><span data-ttu-id="b2b4b-242">Sign in as a tenant</span><span class="sxs-lookup"><span data-stu-id="b2b4b-242">Sign in as a tenant</span></span>
<span data-ttu-id="b2b4b-243">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-243">A service administrator can sign in as a tenant to test the plans, offers, and subscriptions that their tenants might use.</span></span> <span data-ttu-id="b2b4b-244">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-244">If you don’t already have one, [create a tenant account](azure-stack-add-new-user-aad.md) before you sign in.</span></span>

### <a name="create-the-virtual-network-and-vm-subnet"></a><span data-ttu-id="b2b4b-245">Create the virtual network and VM subnet</span><span class="sxs-lookup"><span data-stu-id="b2b4b-245">Create the virtual network and VM subnet</span></span>

1. <span data-ttu-id="b2b4b-246">Sign in by using a tenant account.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-246">Sign in by using a tenant account.</span></span>
2. <span data-ttu-id="b2b4b-247">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-247">In the user portal, select **New**.</span></span>
3. <span data-ttu-id="b2b4b-248">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-248">Go to **Marketplace**, and then select **Networking**.</span></span>
4. <span data-ttu-id="b2b4b-249">Select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-249">Select **Virtual network**.</span></span>
5. <span data-ttu-id="b2b4b-250">Use the information appearing earlier in the network configuration table to identify the values for the POC2 **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-250">Use the information appearing earlier in the network configuration table to identify the values for the POC2 **Name**, **Address space**, **Subnet name**, and **Subnet address range**.</span></span>
6. <span data-ttu-id="b2b4b-251">In **Subscription**, the subscription that you created earlier appears.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-251">In **Subscription**, the subscription that you created earlier appears.</span></span>
7. <span data-ttu-id="b2b4b-252">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-252">For **Resource Group**, create a new resource group or, if you already have one, select **Use existing**.</span></span>
8. <span data-ttu-id="b2b4b-253">Verify the default **Location**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-253">Verify the default **Location**.</span></span>
9. <span data-ttu-id="b2b4b-254">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-254">Select **Pin to dashboard**.</span></span>
10. <span data-ttu-id="b2b4b-255">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-255">Select **Create**.</span></span>

### <a name="create-the-gateway-subnet"></a><span data-ttu-id="b2b4b-256">Create the Gateway Subnet</span><span class="sxs-lookup"><span data-stu-id="b2b4b-256">Create the Gateway Subnet</span></span>
1. <span data-ttu-id="b2b4b-257">Open the Virtual network resource you created (**VNET-02**) from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-257">Open the Virtual network resource you created (**VNET-02**) from the dashboard.</span></span>
2. <span data-ttu-id="b2b4b-258">On the **Settings** blade, select **Subnets**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-258">On the **Settings** blade, select **Subnets**.</span></span>
3. <span data-ttu-id="b2b4b-259">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-259">Select  **Gateway subnet** to add a gateway subnet to the virtual network.</span></span>
4. <span data-ttu-id="b2b4b-260">The name of the subnet is set to **GatewaySubnet** by default.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-260">The name of the subnet is set to **GatewaySubnet** by default.</span></span>
   <span data-ttu-id="b2b4b-261">Gateway subnets are special and must have this specific name to function properly.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-261">Gateway subnets are special and must have this specific name to function properly.</span></span>
5. <span data-ttu-id="b2b4b-262">In the **Address range** field, verify the address is **10.0.21.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-262">In the **Address range** field, verify the address is **10.0.21.0/24**.</span></span>
6. <span data-ttu-id="b2b4b-263">Select **OK** to create the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-263">Select **OK** to create the gateway subnet.</span></span>

### <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="b2b4b-264">Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="b2b4b-264">Create the virtual network gateway</span></span>
1. <span data-ttu-id="b2b4b-265">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-265">In the Azure portal, select **New**.</span></span>  
2. <span data-ttu-id="b2b4b-266">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-266">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b2b4b-267">From the list of network resources, select **Virtual network gateway**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-267">From the list of network resources, select **Virtual network gateway**.</span></span>
4. <span data-ttu-id="b2b4b-268">In **Name**, enter **GW2**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-268">In **Name**, enter **GW2**.</span></span>
5. <span data-ttu-id="b2b4b-269">To choose a virtual network, select **Virtual network**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-269">To choose a virtual network, select **Virtual network**.</span></span> <span data-ttu-id="b2b4b-270">Then select **VNET-02** from the list.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-270">Then select **VNET-02** from the list.</span></span>
6. <span data-ttu-id="b2b4b-271">Select **Public IP address**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-271">Select **Public IP address**.</span></span> <span data-ttu-id="b2b4b-272">When the **Choose public IP address** blade opens, select **Create new**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-272">When the **Choose public IP address** blade opens, select **Create new**.</span></span>
7. <span data-ttu-id="b2b4b-273">In **Name**, enter **GW2-PiP**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-273">In **Name**, enter **GW2-PiP**, and then select **OK**.</span></span>
8. <span data-ttu-id="b2b4b-274">By default, for **VPN type**, **Route-based** is selected.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-274">By default, for **VPN type**, **Route-based** is selected.</span></span>
    <span data-ttu-id="b2b4b-275">Keep the **Route-based** VPN type.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-275">Keep the **Route-based** VPN type.</span></span>
9. <span data-ttu-id="b2b4b-276">Verify that **Subscription** and **Location** are correct.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-276">Verify that **Subscription** and **Location** are correct.</span></span> <span data-ttu-id="b2b4b-277">You can pin the resource to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-277">You can pin the resource to the dashboard.</span></span> <span data-ttu-id="b2b4b-278">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-278">Select **Create**.</span></span>

### <a name="create-the-local-network-gateway-resource"></a><span data-ttu-id="b2b4b-279">Create the local network gateway resource</span><span class="sxs-lookup"><span data-stu-id="b2b4b-279">Create the local network gateway resource</span></span>

1. <span data-ttu-id="b2b4b-280">In the POC2 user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-280">In the POC2 user portal, select **New**.</span></span> 
4. <span data-ttu-id="b2b4b-281">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-281">Go to **Marketplace**, and then select **Networking**.</span></span>
5. <span data-ttu-id="b2b4b-282">From the list of resources, select **Local network gateway**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-282">From the list of resources, select **Local network gateway**.</span></span>
6. <span data-ttu-id="b2b4b-283">In **Name**, enter **POC1-GW**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-283">In **Name**, enter **POC1-GW**.</span></span>
7. <span data-ttu-id="b2b4b-284">In **IP address**, enter the External BGPNAT address for POC1 that is listed earlier in the network configuration table.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-284">In **IP address**, enter the External BGPNAT address for POC1 that is listed earlier in the network configuration table.</span></span>
8. <span data-ttu-id="b2b4b-285">In **Address Space**, from POC1, enter the **10.0.10.0/23** address space of **VNET-01**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-285">In **Address Space**, from POC1, enter the **10.0.10.0/23** address space of **VNET-01**.</span></span>
9. <span data-ttu-id="b2b4b-286">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-286">Verify that your **Subscription**, **Resource Group**, and **Location** are correct, and then select **Create**.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="b2b4b-287">Create the connection</span><span class="sxs-lookup"><span data-stu-id="b2b4b-287">Create the connection</span></span>
1. <span data-ttu-id="b2b4b-288">In the user portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-288">In the user portal, select **New**.</span></span> 
2. <span data-ttu-id="b2b4b-289">Go to **Marketplace**, and then select **Networking**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-289">Go to **Marketplace**, and then select **Networking**.</span></span>
3. <span data-ttu-id="b2b4b-290">From the list of resources, select **Connection**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-290">From the list of resources, select **Connection**.</span></span>
4. <span data-ttu-id="b2b4b-291">On the **Basic** settings blade, for the **Connection type**, choose **Site-to-site (IPSec)**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-291">On the **Basic** settings blade, for the **Connection type**, choose **Site-to-site (IPSec)**.</span></span>
5. <span data-ttu-id="b2b4b-292">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-292">Select the **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
6. <span data-ttu-id="b2b4b-293">On the **Settings** blade, select **Virtual network gateway**, and then select **GW2**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-293">On the **Settings** blade, select **Virtual network gateway**, and then select **GW2**.</span></span>
7. <span data-ttu-id="b2b4b-294">Select **Local network gateway**, and then select **POC1-GW**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-294">Select **Local network gateway**, and then select **POC1-GW**.</span></span>
8. <span data-ttu-id="b2b4b-295">In **Connection name**, enter **POC2-POC1**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-295">In **Connection name**, enter **POC2-POC1**.</span></span>
9. <span data-ttu-id="b2b4b-296">In **Shared key (PSK)**, enter **12345**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-296">In **Shared key (PSK)**, enter **12345**.</span></span> <span data-ttu-id="b2b4b-297">If you choose a different value, remember that it *must* match the value for the shared key that you created on POC1.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-297">If you choose a different value, remember that it *must* match the value for the shared key that you created on POC1.</span></span> <span data-ttu-id="b2b4b-298">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-298">Select **OK**.</span></span>
10. <span data-ttu-id="b2b4b-299">Review the **Summary** blade, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-299">Review the **Summary** blade, and then select **OK**.</span></span>

## <a name="create-a-virtual-machine"></a><span data-ttu-id="b2b4b-300">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="b2b4b-300">Create a virtual machine</span></span>
<span data-ttu-id="b2b4b-301">Create a virtual machine in POC2 now, and put it on your VM subnet in your virtual network.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-301">Create a virtual machine in POC2 now, and put it on your VM subnet in your virtual network.</span></span>

1. <span data-ttu-id="b2b4b-302">In the Azure portal, select **New**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-302">In the Azure portal, select **New**.</span></span>
2. <span data-ttu-id="b2b4b-303">Go to **Marketplace**, and then select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-303">Go to **Marketplace**, and then select **Compute**.</span></span>
3. <span data-ttu-id="b2b4b-304">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-304">In the list of virtual machine images, select the **Windows Server 2016 Datacenter Eval** image.</span></span>
4. <span data-ttu-id="b2b4b-305">On the **Basics** blade, for **Name**, enter **VM02**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-305">On the **Basics** blade, for **Name**, enter **VM02**.</span></span>
5. <span data-ttu-id="b2b4b-306">Enter a valid username and password.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-306">Enter a valid username and password.</span></span> <span data-ttu-id="b2b4b-307">You use this account to sign in to the virtual machine after it's created.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-307">You use this account to sign in to the virtual machine after it's created.</span></span>
6. <span data-ttu-id="b2b4b-308">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-308">Provide a **Subscription**, **Resource Group**, and **Location**, and then select **OK**.</span></span>
7. <span data-ttu-id="b2b4b-309">On the **Size** blade, select a virtual machine size for this instance, and then select **Select**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-309">On the **Size** blade, select a virtual machine size for this instance, and then select **Select**.</span></span>
8. <span data-ttu-id="b2b4b-310">On the **Settings** blade, you can accept the defaults.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-310">On the **Settings** blade, you can accept the defaults.</span></span> <span data-ttu-id="b2b4b-311">Ensure that the **VNET-02** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-311">Ensure that the **VNET-02** virtual network is selected, and verify that the subnet is set to **10.0.20.0/24**.</span></span> <span data-ttu-id="b2b4b-312">Select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-312">Select **OK**.</span></span>
9. <span data-ttu-id="b2b4b-313">Review the settings on the **Summary** blade, and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-313">Review the settings on the **Summary** blade, and then select **OK**.</span></span>

## <a name="configure-the-nat-virtual-machine-on-each-azure-stack-development-kit-for-gateway-traversal"></a><span data-ttu-id="b2b4b-314">Configure the NAT virtual machine on each Azure Stack Development Kit for gateway traversal</span><span class="sxs-lookup"><span data-stu-id="b2b4b-314">Configure the NAT virtual machine on each Azure Stack Development Kit for gateway traversal</span></span>
<span data-ttu-id="b2b4b-315">Because the Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed, the *external* VIP network that the gateways are connected to is not actually external.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-315">Because the Azure Stack Development Kit is self-contained and isolated from the network on which the physical host is deployed, the *external* VIP network that the gateways are connected to is not actually external.</span></span> <span data-ttu-id="b2b4b-316">Instead, the VIP network is hidden behind a router that performs network address translation.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-316">Instead, the VIP network is hidden behind a router that performs network address translation.</span></span> 

<span data-ttu-id="b2b4b-317">The router is a Windows Server virtual machine, called *AzS-bgpnat01*, that runs the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-317">The router is a Windows Server virtual machine, called *AzS-bgpnat01*, that runs the Routing and Remote Access Services (RRAS) role in the Azure Stack Development Kit infrastructure.</span></span> <span data-ttu-id="b2b4b-318">You must configure NAT on the AzS-bgpnat01 virtual machine to allow the site-to-site VPN connection to connect on both ends.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-318">You must configure NAT on the AzS-bgpnat01 virtual machine to allow the site-to-site VPN connection to connect on both ends.</span></span> 

<span data-ttu-id="b2b4b-319">To configure the VPN connection, you must create a static NAT map route that maps the external interface on the BGPNAT virtual machine to the VIP of the Edge Gateway Pool.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-319">To configure the VPN connection, you must create a static NAT map route that maps the external interface on the BGPNAT virtual machine to the VIP of the Edge Gateway Pool.</span></span> <span data-ttu-id="b2b4b-320">A static NAT map route is required for each port in a VPN connection.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-320">A static NAT map route is required for each port in a VPN connection.</span></span>

> [!NOTE]
> <span data-ttu-id="b2b4b-321">This configuration is required for Azure Stack Development Kit environments only.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-321">This configuration is required for Azure Stack Development Kit environments only.</span></span>
> 
> 

### <a name="configure-the-nat"></a><span data-ttu-id="b2b4b-322">Configure the NAT</span><span class="sxs-lookup"><span data-stu-id="b2b4b-322">Configure the NAT</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b2b4b-323">You must complete this procedure for *both* Azure Stack Development Kit environments.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-323">You must complete this procedure for *both* Azure Stack Development Kit environments.</span></span>

1. <span data-ttu-id="b2b4b-324">Determine the **Internal IP address** to use in the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-324">Determine the **Internal IP address** to use in the following PowerShell script.</span></span> <span data-ttu-id="b2b4b-325">Open the virtual network gateway (GW1 and GW2), and then on the **Overview** blade, save the value for the **Public IP address** for later use.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-325">Open the virtual network gateway (GW1 and GW2), and then on the **Overview** blade, save the value for the **Public IP address** for later use.</span></span>
<span data-ttu-id="b2b4b-326">![Internal IP address](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span><span class="sxs-lookup"><span data-stu-id="b2b4b-326">![Internal IP address](media/azure-stack-create-vpn-connection-one-node-tp2/InternalIP.PNG)</span></span>
2. <span data-ttu-id="b2b4b-327">Sign in to the Azure Stack physical machine for POC1.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-327">Sign in to the Azure Stack physical machine for POC1.</span></span>
3. <span data-ttu-id="b2b4b-328">Copy and edit the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-328">Copy and edit the following PowerShell script.</span></span> <span data-ttu-id="b2b4b-329">To configure the NAT on each Azure Stack Development Kit, run the script in an elevated Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-329">To configure the NAT on each Azure Stack Development Kit, run the script in an elevated Windows PowerShell ISE.</span></span> <span data-ttu-id="b2b4b-330">In the script, add values to the *External BGPNAT address* and *Internal IP address* placeholders:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-330">In the script, add values to the *External BGPNAT address* and *Internal IP address* placeholders:</span></span>

   ```powershell
   # Designate the external NAT address for the ports that use the IKE authentication.
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 499 `
      -PortEnd 501}
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatExternalAddress `
      -NatName BGPNAT `
      -IPAddress <External BGPNAT address> `
      -PortStart 4499 `
      -PortEnd 4501}
   # create a static NAT mapping to map the external address to the Gateway
   # Public IP Address to map the ISAKMP port 500 for PHASE 1 of the IPSEC tunnel
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 500 `
      -InternalPort 500}
   # Finally, configure NAT traversal which uses port 4500 to
   # successfully establish the complete IPSEC tunnel over NAT devices
   Invoke-Command `
    -ComputerName AzS-bgpnat01 `
     {Add-NetNatStaticMapping `
      -NatName BGPNAT `
      -Protocol UDP `
      -ExternalIPAddress <External BGPNAT address> `
      -InternalIPAddress <Internal IP address> `
      -ExternalPort 4500 `
      -InternalPort 4500}
   ```

4. <span data-ttu-id="b2b4b-331">Repeat this procedure on POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-331">Repeat this procedure on POC2.</span></span>

## <a name="test-the-connection"></a><span data-ttu-id="b2b4b-332">Test the connection</span><span class="sxs-lookup"><span data-stu-id="b2b4b-332">Test the connection</span></span>
<span data-ttu-id="b2b4b-333">Now that the site-to-site connection is established, you should validate that you can get traffic flowing through it.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-333">Now that the site-to-site connection is established, you should validate that you can get traffic flowing through it.</span></span> <span data-ttu-id="b2b4b-334">To validate, sign in to one of the virtual machines that you created in either Azure Stack Development Kit environment.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-334">To validate, sign in to one of the virtual machines that you created in either Azure Stack Development Kit environment.</span></span> <span data-ttu-id="b2b4b-335">Then, ping the virtual machine that you created in the other environment.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-335">Then, ping the virtual machine that you created in the other environment.</span></span> 

<span data-ttu-id="b2b4b-336">To ensure that you send the traffic through the site-to-site connection, ensure that you ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-336">To ensure that you send the traffic through the site-to-site connection, ensure that you ping the Direct IP (DIP) address of the virtual machine on the remote subnet, not the VIP.</span></span> <span data-ttu-id="b2b4b-337">To do this, find the DIP address on the other end of the connection.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-337">To do this, find the DIP address on the other end of the connection.</span></span> <span data-ttu-id="b2b4b-338">Save the address for later use.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-338">Save the address for later use.</span></span>

### <a name="sign-in-to-the-tenant-vm-in-poc1"></a><span data-ttu-id="b2b4b-339">Sign in to the tenant VM in POC1</span><span class="sxs-lookup"><span data-stu-id="b2b4b-339">Sign in to the tenant VM in POC1</span></span>
1. <span data-ttu-id="b2b4b-340">Sign in to the Azure Stack physical machine for POC1, and then use a tenant account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-340">Sign in to the Azure Stack physical machine for POC1, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="b2b4b-341">In the left navigation bar, select **Compute**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-341">In the left navigation bar, select **Compute**.</span></span>
3. <span data-ttu-id="b2b4b-342">In the list of VMs, find **VM01** that you created previously, and then select it.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-342">In the list of VMs, find **VM01** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="b2b4b-343">On the blade for the virtual machine, click **Connect**, and then open the VM01.rdp file.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-343">On the blade for the virtual machine, click **Connect**, and then open the VM01.rdp file.</span></span>
   
     ![Connect button](media/azure-stack-create-vpn-connection-one-node-tp2/image17.png)
5. <span data-ttu-id="b2b4b-345">Sign in with the account that you configured when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-345">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="b2b4b-346">Open an elevated **Windows PowerShell** window.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-346">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="b2b4b-347">Enter **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-347">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="b2b4b-348">In the output, find the **IPv4 Address**, and then save the address for later use.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-348">In the output, find the **IPv4 Address**, and then save the address for later use.</span></span> <span data-ttu-id="b2b4b-349">This is the address that you will ping from POC2.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-349">This is the address that you will ping from POC2.</span></span> <span data-ttu-id="b2b4b-350">In the example environment, the address is **10.0.10.4**, but in your environment it might be different.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-350">In the example environment, the address is **10.0.10.4**, but in your environment it might be different.</span></span> <span data-ttu-id="b2b4b-351">It should fall within the **10.0.10.0/24** subnet that you created previously.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-351">It should fall within the **10.0.10.0/24** subnet that you created previously.</span></span>
9. <span data-ttu-id="b2b4b-352">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-352">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

### <a name="sign-in-to-the-tenant-vm-in-poc2"></a><span data-ttu-id="b2b4b-353">Sign in to the tenant VM in POC2</span><span class="sxs-lookup"><span data-stu-id="b2b4b-353">Sign in to the tenant VM in POC2</span></span>
1. <span data-ttu-id="b2b4b-354">Sign in to the Azure Stack physical machine for POC2, and then use a tenant account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-354">Sign in to the Azure Stack physical machine for POC2, and then use a tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="b2b4b-355">In the left navigation bar, click **Compute**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-355">In the left navigation bar, click **Compute**.</span></span>
3. <span data-ttu-id="b2b4b-356">From the list of virtual machines, find **VM02** that you created previously, and then select it.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-356">From the list of virtual machines, find **VM02** that you created previously, and then select it.</span></span>
4. <span data-ttu-id="b2b4b-357">On the blade for the virtual machine, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-357">On the blade for the virtual machine, click **Connect**.</span></span>
5. <span data-ttu-id="b2b4b-358">Sign in with the account that you configured when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-358">Sign in with the account that you configured when you created the virtual machine.</span></span>
6. <span data-ttu-id="b2b4b-359">Open an elevated **Windows PowerShell** window.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-359">Open an elevated **Windows PowerShell** window.</span></span>
7. <span data-ttu-id="b2b4b-360">Enter **ipconfig /all**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-360">Enter **ipconfig /all**.</span></span>
8. <span data-ttu-id="b2b4b-361">You should see an IPv4 address that falls within **10.0.20.0/24**.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-361">You should see an IPv4 address that falls within **10.0.20.0/24**.</span></span> <span data-ttu-id="b2b4b-362">In the example environment, the address is **10.0.20.4**, but your address might be different.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-362">In the example environment, the address is **10.0.20.4**, but your address might be different.</span></span>
9. <span data-ttu-id="b2b4b-363">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-363">To create a firewall rule that allows the virtual machine to respond to pings, run the following PowerShell command:</span></span>

   ```powershell
   New-NetFirewallRule `
    –DisplayName “Allow ICMPv4-In” `
    –Protocol ICMPv4
   ```

10. <span data-ttu-id="b2b4b-364">From the virtual machine on POC2, ping the virtual machine on POC1, through the tunnel.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-364">From the virtual machine on POC2, ping the virtual machine on POC1, through the tunnel.</span></span> <span data-ttu-id="b2b4b-365">To do this, you ping the DIP that you recorded from VM01.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-365">To do this, you ping the DIP that you recorded from VM01.</span></span>
   <span data-ttu-id="b2b4b-366">In the example environment, this is **10.0.10.4**, but be sure to ping the address you noted in your lab.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-366">In the example environment, this is **10.0.10.4**, but be sure to ping the address you noted in your lab.</span></span> <span data-ttu-id="b2b4b-367">You should see a result that looks like the following:</span><span class="sxs-lookup"><span data-stu-id="b2b4b-367">You should see a result that looks like the following:</span></span>
   
    ![Successful ping](media/azure-stack-create-vpn-connection-one-node-tp2/image19b.png)
11. <span data-ttu-id="b2b4b-369">A reply from the remote virtual machine indicates a successful test!</span><span class="sxs-lookup"><span data-stu-id="b2b4b-369">A reply from the remote virtual machine indicates a successful test!</span></span> <span data-ttu-id="b2b4b-370">You can close the virtual machine window.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-370">You can close the virtual machine window.</span></span> <span data-ttu-id="b2b4b-371">To test your connection, you can try other kinds of data transfers like a file copy.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-371">To test your connection, you can try other kinds of data transfers like a file copy.</span></span>

### <a name="viewing-data-transfer-statistics-through-the-gateway-connection"></a><span data-ttu-id="b2b4b-372">Viewing data transfer statistics through the gateway connection</span><span class="sxs-lookup"><span data-stu-id="b2b4b-372">Viewing data transfer statistics through the gateway connection</span></span>
<span data-ttu-id="b2b4b-373">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** blade.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-373">If you want to know how much data passes through your site-to-site connection, this information is available on the **Connection** blade.</span></span> <span data-ttu-id="b2b4b-374">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-374">This test is also another way to verify that the ping you just sent actually went through the VPN connection.</span></span>

1. <span data-ttu-id="b2b4b-375">While you're signed in to the tenant virtual machine in POC2, use your tenant account to sign in to the user portal.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-375">While you're signed in to the tenant virtual machine in POC2, use your tenant account to sign in to the user portal.</span></span>
2. <span data-ttu-id="b2b4b-376">Go to **All resources**, and then select the **POC2-POC1** connection.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-376">Go to **All resources**, and then select the **POC2-POC1** connection.</span></span> <span data-ttu-id="b2b4b-377">**Connections** appears.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-377">**Connections** appears.</span></span>
4. <span data-ttu-id="b2b4b-378">On the **Connection** blade, the statistics for **Data in** and **Data out** appear.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-378">On the **Connection** blade, the statistics for **Data in** and **Data out** appear.</span></span> <span data-ttu-id="b2b4b-379">In the following screenshot, the large numbers are attributed to additional file transfer.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-379">In the following screenshot, the large numbers are attributed to additional file transfer.</span></span> <span data-ttu-id="b2b4b-380">You should see some nonzero values there.</span><span class="sxs-lookup"><span data-stu-id="b2b4b-380">You should see some nonzero values there.</span></span>
   
    ![Data in and out](media/azure-stack-create-vpn-connection-one-node-tp2/image20.png)
