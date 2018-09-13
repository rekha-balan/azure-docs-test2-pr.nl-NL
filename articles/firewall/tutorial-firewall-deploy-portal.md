---
title: Deploy and configure Azure Firewall using the Azure portal
description: In this tutorial, you learn how to deploy and configure Azure Firewall using the Azure portal.
services: firewall
author: vhorne
manager: jpconnock
ms.service: firewall
ms.topic: tutorial
ms.date: 7/11/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 84696b4135570168f8093b15f9a2deb4790eeebe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867400"
---
# <a name="tutorial-deploy-and-configure-azure-firewall-using-the-azure-portal"></a><span data-ttu-id="8bccd-103">Tutorial: Deploy and configure Azure Firewall using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8bccd-103">Tutorial: Deploy and configure Azure Firewall using the Azure portal</span></span>

<span data-ttu-id="8bccd-104">Azure Firewall has two rule types to control outbound access:</span><span class="sxs-lookup"><span data-stu-id="8bccd-104">Azure Firewall has two rule types to control outbound access:</span></span>

- <span data-ttu-id="8bccd-105">**Application rules**</span><span class="sxs-lookup"><span data-stu-id="8bccd-105">**Application rules**</span></span>

   <span data-ttu-id="8bccd-106">Allows you to configure fully qualified domain names (FQDNs) that can be accessed from a subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-106">Allows you to configure fully qualified domain names (FQDNs) that can be accessed from a subnet.</span></span> <span data-ttu-id="8bccd-107">For example, you could allow access to *github.com* from your subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-107">For example, you could allow access to *github.com* from your subnet.</span></span>
- <span data-ttu-id="8bccd-108">**Network rules**</span><span class="sxs-lookup"><span data-stu-id="8bccd-108">**Network rules**</span></span>

   <span data-ttu-id="8bccd-109">Allows you to configure rules containing source address, protocol, destination port, and destination address.</span><span class="sxs-lookup"><span data-stu-id="8bccd-109">Allows you to configure rules containing source address, protocol, destination port, and destination address.</span></span> <span data-ttu-id="8bccd-110">For example, you could create a rule to allow traffic to port 53 (DNS) to the IP address of your DNS server from your subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-110">For example, you could create a rule to allow traffic to port 53 (DNS) to the IP address of your DNS server from your subnet.</span></span>

<span data-ttu-id="8bccd-111">Network traffic is subjected to the configured firewall rules when you route your network traffic to the firewall as the subnet default gateway.</span><span class="sxs-lookup"><span data-stu-id="8bccd-111">Network traffic is subjected to the configured firewall rules when you route your network traffic to the firewall as the subnet default gateway.</span></span>

<span data-ttu-id="8bccd-112">Application and network rules are stored in *rule collections*.</span><span class="sxs-lookup"><span data-stu-id="8bccd-112">Application and network rules are stored in *rule collections*.</span></span> <span data-ttu-id="8bccd-113">A rule collection is a list of rules that share the same action and priority.</span><span class="sxs-lookup"><span data-stu-id="8bccd-113">A rule collection is a list of rules that share the same action and priority.</span></span>  <span data-ttu-id="8bccd-114">A network rule collection is a list of network rules and an application rule collection is a list of application rules.</span><span class="sxs-lookup"><span data-stu-id="8bccd-114">A network rule collection is a list of network rules and an application rule collection is a list of application rules.</span></span>

<span data-ttu-id="8bccd-115">Network rule collections are always processed before application rule collections.</span><span class="sxs-lookup"><span data-stu-id="8bccd-115">Network rule collections are always processed before application rule collections.</span></span> <span data-ttu-id="8bccd-116">All rules are terminating, so if a match is found in a network rule collection, the following application rule collections for the session are not be processed.</span><span class="sxs-lookup"><span data-stu-id="8bccd-116">All rules are terminating, so if a match is found in a network rule collection, the following application rule collections for the session are not be processed.</span></span>

<span data-ttu-id="8bccd-117">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="8bccd-117">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8bccd-118">Set up a test network environment</span><span class="sxs-lookup"><span data-stu-id="8bccd-118">Set up a test network environment</span></span>
> * <span data-ttu-id="8bccd-119">Deploy a firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-119">Deploy a firewall</span></span>
> * <span data-ttu-id="8bccd-120">Create a default route</span><span class="sxs-lookup"><span data-stu-id="8bccd-120">Create a default route</span></span>
> * <span data-ttu-id="8bccd-121">Configure application rules</span><span class="sxs-lookup"><span data-stu-id="8bccd-121">Configure application rules</span></span>
> * <span data-ttu-id="8bccd-122">Configure network rules</span><span class="sxs-lookup"><span data-stu-id="8bccd-122">Configure network rules</span></span>
> * <span data-ttu-id="8bccd-123">Test the firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-123">Test the firewall</span></span>



<span data-ttu-id="8bccd-124">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="8bccd-124">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [firewall-preview-notice](../../includes/firewall-preview-notice.md)]

<span data-ttu-id="8bccd-125">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span><span class="sxs-lookup"><span data-stu-id="8bccd-125">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span></span> <span data-ttu-id="8bccd-126">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span><span class="sxs-lookup"><span data-stu-id="8bccd-126">For more information, see [Enable the Azure Firewall public preview](public-preview.md).</span></span>

<span data-ttu-id="8bccd-127">For this tutorial, you create a single VNet with three subnets:</span><span class="sxs-lookup"><span data-stu-id="8bccd-127">For this tutorial, you create a single VNet with three subnets:</span></span>
- <span data-ttu-id="8bccd-128">**FW-SN** - the firewall is in this subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-128">**FW-SN** - the firewall is in this subnet.</span></span>
- <span data-ttu-id="8bccd-129">**Workload-SN** - the workload server is in this subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-129">**Workload-SN** - the workload server is in this subnet.</span></span> <span data-ttu-id="8bccd-130">This subnet's network traffic goes through the firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-130">This subnet's network traffic goes through the firewall.</span></span>
- <span data-ttu-id="8bccd-131">**Jump-SN** - The "jump" server is in this subnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-131">**Jump-SN** - The "jump" server is in this subnet.</span></span> <span data-ttu-id="8bccd-132">The jump server has a public IP address that you can connect to using Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="8bccd-132">The jump server has a public IP address that you can connect to using Remote Desktop.</span></span> <span data-ttu-id="8bccd-133">From there, you can then connect to (using another Remote Desktop) the workload server.</span><span class="sxs-lookup"><span data-stu-id="8bccd-133">From there, you can then connect to (using another Remote Desktop) the workload server.</span></span>

![Tutorial network infrastructure](media/tutorial-firewall-rules-portal/Tutorial_network.png)

<span data-ttu-id="8bccd-135">This tutorial uses a simplified network configuration for easy deployment.</span><span class="sxs-lookup"><span data-stu-id="8bccd-135">This tutorial uses a simplified network configuration for easy deployment.</span></span> <span data-ttu-id="8bccd-136">For production deployments, a [hub and spoke model](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) is recommended, where the firewall is in its own VNet, and workload servers are in peered VNets in the same region with one or more subnets.</span><span class="sxs-lookup"><span data-stu-id="8bccd-136">For production deployments, a [hub and spoke model](https://docs.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) is recommended, where the firewall is in its own VNet, and workload servers are in peered VNets in the same region with one or more subnets.</span></span>



## <a name="set-up-the-network-environment"></a><span data-ttu-id="8bccd-137">Set up the network environment</span><span class="sxs-lookup"><span data-stu-id="8bccd-137">Set up the network environment</span></span>
<span data-ttu-id="8bccd-138">First, create a resource group to contain the resources needed to deploy the firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-138">First, create a resource group to contain the resources needed to deploy the firewall.</span></span> <span data-ttu-id="8bccd-139">Then create a VNet, subnets, and test servers.</span><span class="sxs-lookup"><span data-stu-id="8bccd-139">Then create a VNet, subnets, and test servers.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="8bccd-140">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="8bccd-140">Create a resource group</span></span>
1. <span data-ttu-id="8bccd-141">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8bccd-141">Sign in to the Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>
1. <span data-ttu-id="8bccd-142">On the Azure portal home page, click **Resource groups**, then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-142">On the Azure portal home page, click **Resource groups**, then click **Add**.</span></span>
2. <span data-ttu-id="8bccd-143">For **Resource group name**, type **Test-FW-RG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-143">For **Resource group name**, type **Test-FW-RG**.</span></span>
3. <span data-ttu-id="8bccd-144">For **Subscription**, select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8bccd-144">For **Subscription**, select your subscription.</span></span>
4. <span data-ttu-id="8bccd-145">For **Resource group location**, select a location.</span><span class="sxs-lookup"><span data-stu-id="8bccd-145">For **Resource group location**, select a location.</span></span> <span data-ttu-id="8bccd-146">All subsequent resources that you create must be in the same location.</span><span class="sxs-lookup"><span data-stu-id="8bccd-146">All subsequent resources that you create must be in the same location.</span></span>
5. <span data-ttu-id="8bccd-147">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-147">Click **Create**.</span></span>


### <a name="create-a-vnet"></a><span data-ttu-id="8bccd-148">Create a VNet</span><span class="sxs-lookup"><span data-stu-id="8bccd-148">Create a VNet</span></span>
1. <span data-ttu-id="8bccd-149">From the Azure portal home page, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-149">From the Azure portal home page, click **All services**.</span></span>
2. <span data-ttu-id="8bccd-150">Under **Networking**, click **Virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-150">Under **Networking**, click **Virtual networks**.</span></span>
3. <span data-ttu-id="8bccd-151">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-151">Click **Add**.</span></span>
4. <span data-ttu-id="8bccd-152">For **Name**, type **Test-FW-VN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-152">For **Name**, type **Test-FW-VN**.</span></span>
5. <span data-ttu-id="8bccd-153">For **Address space**, type **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-153">For **Address space**, type **10.0.0.0/16**.</span></span>
7. <span data-ttu-id="8bccd-154">For **Subscription**, select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8bccd-154">For **Subscription**, select your subscription.</span></span>
8. <span data-ttu-id="8bccd-155">For **Resource group**, select **Use existing**, and then select **Test-FW-RG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-155">For **Resource group**, select **Use existing**, and then select **Test-FW-RG**.</span></span>
9. <span data-ttu-id="8bccd-156">For **Location**, select the same location that you used previously.</span><span class="sxs-lookup"><span data-stu-id="8bccd-156">For **Location**, select the same location that you used previously.</span></span>
10. <span data-ttu-id="8bccd-157">Under **Subnet**, for **Name** type **AzureFirewallSubnet**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-157">Under **Subnet**, for **Name** type **AzureFirewallSubnet**.</span></span>

    <span data-ttu-id="8bccd-158">The firewall will be in this subnet, and the subnet name **must** be AzureFirewallSubnet.</span><span class="sxs-lookup"><span data-stu-id="8bccd-158">The firewall will be in this subnet, and the subnet name **must** be AzureFirewallSubnet.</span></span>
11. <span data-ttu-id="8bccd-159">For **Address range**, type **10.0.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-159">For **Address range**, type **10.0.1.0/24**.</span></span>
12. <span data-ttu-id="8bccd-160">Use the other default settings, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-160">Use the other default settings, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="8bccd-161">The minimum size of the AzureFirewallSubnet subnet is /25.</span><span class="sxs-lookup"><span data-stu-id="8bccd-161">The minimum size of the AzureFirewallSubnet subnet is /25.</span></span>

### <a name="create-additional-subnets"></a><span data-ttu-id="8bccd-162">Create additional subnets</span><span class="sxs-lookup"><span data-stu-id="8bccd-162">Create additional subnets</span></span>

<span data-ttu-id="8bccd-163">Next, create subnets for the jump server, and a subnet for the workload servers.</span><span class="sxs-lookup"><span data-stu-id="8bccd-163">Next, create subnets for the jump server, and a subnet for the workload servers.</span></span>

1. <span data-ttu-id="8bccd-164">On the Azure portal home page, click **Resource groups**, then click **Test-FW-RG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-164">On the Azure portal home page, click **Resource groups**, then click **Test-FW-RG**.</span></span>
2. <span data-ttu-id="8bccd-165">Click the **Test-FW-VN** virtual network.</span><span class="sxs-lookup"><span data-stu-id="8bccd-165">Click the **Test-FW-VN** virtual network.</span></span>
3. <span data-ttu-id="8bccd-166">Click **Subnets**, and then click **+Subnet**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-166">Click **Subnets**, and then click **+Subnet**.</span></span>
4. <span data-ttu-id="8bccd-167">For **Name**, type **Workload-SN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-167">For **Name**, type **Workload-SN**.</span></span>
5. <span data-ttu-id="8bccd-168">For **Address range**, type **10.0.2.0/24**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-168">For **Address range**, type **10.0.2.0/24**.</span></span>
6. <span data-ttu-id="8bccd-169">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-169">Click **OK**.</span></span>

<span data-ttu-id="8bccd-170">Create another subnet named **Jump-SN**, address range **10.0.3.0/24**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-170">Create another subnet named **Jump-SN**, address range **10.0.3.0/24**.</span></span>

### <a name="create-virtual-machines"></a><span data-ttu-id="8bccd-171">Create virtual machines</span><span class="sxs-lookup"><span data-stu-id="8bccd-171">Create virtual machines</span></span>

<span data-ttu-id="8bccd-172">Now create the jump and workload virtual machines, and place them in the appropriate subnets.</span><span class="sxs-lookup"><span data-stu-id="8bccd-172">Now create the jump and workload virtual machines, and place them in the appropriate subnets.</span></span>

1. <span data-ttu-id="8bccd-173">From the Azure portal home page, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-173">From the Azure portal home page, click **All services**.</span></span>
2. <span data-ttu-id="8bccd-174">Under **Compute**, click **Virtual machines**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-174">Under **Compute**, click **Virtual machines**.</span></span>
3. <span data-ttu-id="8bccd-175">Click **Add**, and click **Windows Server**,  click **Windows Server 2016 Datacenter**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-175">Click **Add**, and click **Windows Server**,  click **Windows Server 2016 Datacenter**, and then click **Create**.</span></span>

<span data-ttu-id="8bccd-176">**Basics**</span><span class="sxs-lookup"><span data-stu-id="8bccd-176">**Basics**</span></span>

1. <span data-ttu-id="8bccd-177">For **Name**, type **Srv-Jump**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-177">For **Name**, type **Srv-Jump**.</span></span>
5. <span data-ttu-id="8bccd-178">Type a username and password.</span><span class="sxs-lookup"><span data-stu-id="8bccd-178">Type a username and password.</span></span>
6. <span data-ttu-id="8bccd-179">For **Subscription**, select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8bccd-179">For **Subscription**, select your subscription.</span></span>
7. <span data-ttu-id="8bccd-180">For **Resource group**, click **Use existing**, and then select **Test-FW-RG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-180">For **Resource group**, click **Use existing**, and then select **Test-FW-RG**.</span></span>
8. <span data-ttu-id="8bccd-181">For **Location**, select the same location that you used previously.</span><span class="sxs-lookup"><span data-stu-id="8bccd-181">For **Location**, select the same location that you used previously.</span></span>
9. <span data-ttu-id="8bccd-182">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-182">Click **OK**.</span></span>

<span data-ttu-id="8bccd-183">**Size**</span><span class="sxs-lookup"><span data-stu-id="8bccd-183">**Size**</span></span>

1. <span data-ttu-id="8bccd-184">Choose an appropriate size for a test virtual machine running Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8bccd-184">Choose an appropriate size for a test virtual machine running Windows Server.</span></span> <span data-ttu-id="8bccd-185">For example, **B2ms** (8 GB RAM, 16 GB storage).</span><span class="sxs-lookup"><span data-stu-id="8bccd-185">For example, **B2ms** (8 GB RAM, 16 GB storage).</span></span>
2. <span data-ttu-id="8bccd-186">Click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-186">Click **Select**.</span></span>

<span data-ttu-id="8bccd-187">**Settings**</span><span class="sxs-lookup"><span data-stu-id="8bccd-187">**Settings**</span></span>

1. <span data-ttu-id="8bccd-188">Under **Network**, for **Virtual network**, select **Test-FW-VN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-188">Under **Network**, for **Virtual network**, select **Test-FW-VN**.</span></span>
2. <span data-ttu-id="8bccd-189">For **Subnet**, select **Jump-SN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-189">For **Subnet**, select **Jump-SN**.</span></span>
3. <span data-ttu-id="8bccd-190">For **Select public inbound ports**, select **RDP (3389)**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-190">For **Select public inbound ports**, select **RDP (3389)**.</span></span> 

    <span data-ttu-id="8bccd-191">You'll want to limit the access to your public IP address, but you need to open port 3389 so you can connect a remote desktop to the jump server.</span><span class="sxs-lookup"><span data-stu-id="8bccd-191">You'll want to limit the access to your public IP address, but you need to open port 3389 so you can connect a remote desktop to the jump server.</span></span> 
2. <span data-ttu-id="8bccd-192">Leave the other default settings and click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-192">Leave the other default settings and click **OK**.</span></span>

<span data-ttu-id="8bccd-193">**Summary**</span><span class="sxs-lookup"><span data-stu-id="8bccd-193">**Summary**</span></span>

<span data-ttu-id="8bccd-194">Review the summary, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-194">Review the summary, and then click **Create**.</span></span> <span data-ttu-id="8bccd-195">This will take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="8bccd-195">This will take a few minutes to complete.</span></span>

<span data-ttu-id="8bccd-196">Repeat this process to create another virtual machine named **Srv-Work**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-196">Repeat this process to create another virtual machine named **Srv-Work**.</span></span>

<span data-ttu-id="8bccd-197">Use the information in the following table to configure the **Settings** for the Srv-Work virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bccd-197">Use the information in the following table to configure the **Settings** for the Srv-Work virtual machine.</span></span> <span data-ttu-id="8bccd-198">The rest of the configuration is the same as the Srv-Jump virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bccd-198">The rest of the configuration is the same as the Srv-Jump virtual machine.</span></span>


|<span data-ttu-id="8bccd-199">Setting</span><span class="sxs-lookup"><span data-stu-id="8bccd-199">Setting</span></span>  |<span data-ttu-id="8bccd-200">Value</span><span class="sxs-lookup"><span data-stu-id="8bccd-200">Value</span></span>  |
|---------|---------|
|<span data-ttu-id="8bccd-201">Subnet</span><span class="sxs-lookup"><span data-stu-id="8bccd-201">Subnet</span></span>|<span data-ttu-id="8bccd-202">Workload-SN</span><span class="sxs-lookup"><span data-stu-id="8bccd-202">Workload-SN</span></span>|
|<span data-ttu-id="8bccd-203">Public IP address</span><span class="sxs-lookup"><span data-stu-id="8bccd-203">Public IP address</span></span>|<span data-ttu-id="8bccd-204">None</span><span class="sxs-lookup"><span data-stu-id="8bccd-204">None</span></span>|
|<span data-ttu-id="8bccd-205">Select public inbound ports</span><span class="sxs-lookup"><span data-stu-id="8bccd-205">Select public inbound ports</span></span>|<span data-ttu-id="8bccd-206">No public inbound ports</span><span class="sxs-lookup"><span data-stu-id="8bccd-206">No public inbound ports</span></span>|


## <a name="deploy-the-firewall"></a><span data-ttu-id="8bccd-207">Deploy the firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-207">Deploy the firewall</span></span>

1. <span data-ttu-id="8bccd-208">From the portal home page, click **Create a resource**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-208">From the portal home page, click **Create a resource**.</span></span>
2. <span data-ttu-id="8bccd-209">Click **Networking**, and after **Featured**, click **See all**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-209">Click **Networking**, and after **Featured**, click **See all**.</span></span>
3. <span data-ttu-id="8bccd-210">Click **Firewall**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-210">Click **Firewall**, and then click **Create**.</span></span> 
4. <span data-ttu-id="8bccd-211">On the **Create a Firewall** page, use the following table to configure the firewall:</span><span class="sxs-lookup"><span data-stu-id="8bccd-211">On the **Create a Firewall** page, use the following table to configure the firewall:</span></span>
   
   |<span data-ttu-id="8bccd-212">Setting</span><span class="sxs-lookup"><span data-stu-id="8bccd-212">Setting</span></span>  |<span data-ttu-id="8bccd-213">Value</span><span class="sxs-lookup"><span data-stu-id="8bccd-213">Value</span></span>  |
   |---------|---------|
   |<span data-ttu-id="8bccd-214">Name</span><span class="sxs-lookup"><span data-stu-id="8bccd-214">Name</span></span>     |<span data-ttu-id="8bccd-215">Test-FW01</span><span class="sxs-lookup"><span data-stu-id="8bccd-215">Test-FW01</span></span>|
   |<span data-ttu-id="8bccd-216">Subscription</span><span class="sxs-lookup"><span data-stu-id="8bccd-216">Subscription</span></span>     |<span data-ttu-id="8bccd-217">\<your subscription\></span><span class="sxs-lookup"><span data-stu-id="8bccd-217">\<your subscription\></span></span>|
   |<span data-ttu-id="8bccd-218">Resource group</span><span class="sxs-lookup"><span data-stu-id="8bccd-218">Resource group</span></span>     |<span data-ttu-id="8bccd-219">**Use existing**: Test-FW-RG</span><span class="sxs-lookup"><span data-stu-id="8bccd-219">**Use existing**: Test-FW-RG</span></span> |
   |<span data-ttu-id="8bccd-220">Location</span><span class="sxs-lookup"><span data-stu-id="8bccd-220">Location</span></span>     |<span data-ttu-id="8bccd-221">Select the same location that you used previously</span><span class="sxs-lookup"><span data-stu-id="8bccd-221">Select the same location that you used previously</span></span>|
   |<span data-ttu-id="8bccd-222">Choose a virtual network</span><span class="sxs-lookup"><span data-stu-id="8bccd-222">Choose a virtual network</span></span>     |<span data-ttu-id="8bccd-223">**Use existing**: Test-FW-VN</span><span class="sxs-lookup"><span data-stu-id="8bccd-223">**Use existing**: Test-FW-VN</span></span>|
   |<span data-ttu-id="8bccd-224">Public IP address</span><span class="sxs-lookup"><span data-stu-id="8bccd-224">Public IP address</span></span>     |<span data-ttu-id="8bccd-225">**Create new**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-225">**Create new**.</span></span> <span data-ttu-id="8bccd-226">The Public IP address must be the Standard SKU type.</span><span class="sxs-lookup"><span data-stu-id="8bccd-226">The Public IP address must be the Standard SKU type.</span></span>|

2. <span data-ttu-id="8bccd-227">Click **Review + create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-227">Click **Review + create**.</span></span>
3. <span data-ttu-id="8bccd-228">Review the summary, and then click **Create** to create the firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-228">Review the summary, and then click **Create** to create the firewall.</span></span>

   <span data-ttu-id="8bccd-229">This will take a few minutes to deploy.</span><span class="sxs-lookup"><span data-stu-id="8bccd-229">This will take a few minutes to deploy.</span></span>
4. <span data-ttu-id="8bccd-230">After deployment completes, go to the **Test-FW-RG** resource group, and click the **Test-FW01** firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-230">After deployment completes, go to the **Test-FW-RG** resource group, and click the **Test-FW01** firewall.</span></span>
6. <span data-ttu-id="8bccd-231">Note the private IP address.</span><span class="sxs-lookup"><span data-stu-id="8bccd-231">Note the private IP address.</span></span> <span data-ttu-id="8bccd-232">You'll use it later when you create the default route.</span><span class="sxs-lookup"><span data-stu-id="8bccd-232">You'll use it later when you create the default route.</span></span>


## <a name="create-a-default-route"></a><span data-ttu-id="8bccd-233">Create a default route</span><span class="sxs-lookup"><span data-stu-id="8bccd-233">Create a default route</span></span>

<span data-ttu-id="8bccd-234">For the **Workload-SN** subnet, you configure the outbound default route to go through the firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-234">For the **Workload-SN** subnet, you configure the outbound default route to go through the firewall.</span></span>

1. <span data-ttu-id="8bccd-235">From the Azure portal home page, click **All services**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-235">From the Azure portal home page, click **All services**.</span></span>
2. <span data-ttu-id="8bccd-236">Under **Networking**, click **Route tables**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-236">Under **Networking**, click **Route tables**.</span></span>
3. <span data-ttu-id="8bccd-237">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-237">Click **Add**.</span></span>
4. <span data-ttu-id="8bccd-238">For **Name**, type **Firewall-route**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-238">For **Name**, type **Firewall-route**.</span></span>
5. <span data-ttu-id="8bccd-239">For **Subscription**, select your subscription.</span><span class="sxs-lookup"><span data-stu-id="8bccd-239">For **Subscription**, select your subscription.</span></span>
6. <span data-ttu-id="8bccd-240">For **Resource group**, select **Use existing**, and select **Test-FW-RG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-240">For **Resource group**, select **Use existing**, and select **Test-FW-RG**.</span></span>
7. <span data-ttu-id="8bccd-241">For **Location**, select the same location that you used previously.</span><span class="sxs-lookup"><span data-stu-id="8bccd-241">For **Location**, select the same location that you used previously.</span></span>
8. <span data-ttu-id="8bccd-242">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-242">Click **Create**.</span></span>
9. <span data-ttu-id="8bccd-243">Click **Refresh**, and then click the **Firewall-route** route table.</span><span class="sxs-lookup"><span data-stu-id="8bccd-243">Click **Refresh**, and then click the **Firewall-route** route table.</span></span>
10. <span data-ttu-id="8bccd-244">Click **Subnets**, and then click **Associate**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-244">Click **Subnets**, and then click **Associate**.</span></span>
11. <span data-ttu-id="8bccd-245">Click **Virtual network**, and then select **Test-FW-VN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-245">Click **Virtual network**, and then select **Test-FW-VN**.</span></span>
12. <span data-ttu-id="8bccd-246">For **Subnet**, click **Workload-SN**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-246">For **Subnet**, click **Workload-SN**.</span></span>
13. <span data-ttu-id="8bccd-247">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-247">Click **OK**.</span></span>
14. <span data-ttu-id="8bccd-248">Click **Routes**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-248">Click **Routes**, and then click **Add**.</span></span>
15. <span data-ttu-id="8bccd-249">For **Route name**, type **FW-DG**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-249">For **Route name**, type **FW-DG**.</span></span>
16. <span data-ttu-id="8bccd-250">For **Address prefix**, type **0.0.0.0/0**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-250">For **Address prefix**, type **0.0.0.0/0**.</span></span>
17. <span data-ttu-id="8bccd-251">For **Next hop type**, select **Virtual appliance**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-251">For **Next hop type**, select **Virtual appliance**.</span></span>

    <span data-ttu-id="8bccd-252">Azure Firewall is actually a managed service, but virtual appliance works in this situation.</span><span class="sxs-lookup"><span data-stu-id="8bccd-252">Azure Firewall is actually a managed service, but virtual appliance works in this situation.</span></span>
1. <span data-ttu-id="8bccd-253">For **Next hop address**, type the private IP address for the firewall that you noted previously.</span><span class="sxs-lookup"><span data-stu-id="8bccd-253">For **Next hop address**, type the private IP address for the firewall that you noted previously.</span></span>
2. <span data-ttu-id="8bccd-254">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-254">Click **OK**.</span></span>


## <a name="configure-application-rules"></a><span data-ttu-id="8bccd-255">Configure application rules</span><span class="sxs-lookup"><span data-stu-id="8bccd-255">Configure application rules</span></span>


1. <span data-ttu-id="8bccd-256">Open the **Test-FW-RG**, and click the **Test-FW01** firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-256">Open the **Test-FW-RG**, and click the **Test-FW01** firewall.</span></span>
1. <span data-ttu-id="8bccd-257">On the **Test-FW01** page, under **Settings**, click **Rules**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-257">On the **Test-FW01** page, under **Settings**, click **Rules**.</span></span>
2. <span data-ttu-id="8bccd-258">Click **Add application rule collection**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-258">Click **Add application rule collection**.</span></span>
3. <span data-ttu-id="8bccd-259">For **Name**, type **App-Coll01**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-259">For **Name**, type **App-Coll01**.</span></span>
1. <span data-ttu-id="8bccd-260">For **Priority**, type **200**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-260">For **Priority**, type **200**.</span></span>
2. <span data-ttu-id="8bccd-261">For **Action**, select **Allow**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-261">For **Action**, select **Allow**.</span></span>

6. <span data-ttu-id="8bccd-262">Under **Rules**, for **Name**, type **AllowGH**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-262">Under **Rules**, for **Name**, type **AllowGH**.</span></span>
7. <span data-ttu-id="8bccd-263">For **Source Addresses**, type **10.0.2.0/24**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-263">For **Source Addresses**, type **10.0.2.0/24**.</span></span>
8. <span data-ttu-id="8bccd-264">For **Protocol:port**, type **http, https**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-264">For **Protocol:port**, type **http, https**.</span></span> 
9. <span data-ttu-id="8bccd-265">For **Target FQDNS**, type **github.com**</span><span class="sxs-lookup"><span data-stu-id="8bccd-265">For **Target FQDNS**, type **github.com**</span></span>
10. <span data-ttu-id="8bccd-266">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-266">Click **Add**.</span></span>

> [!NOTE]
> <span data-ttu-id="8bccd-267">Azure Firewall includes a built-in rule collection for infrastructure FQDNs that are allowed by default.</span><span class="sxs-lookup"><span data-stu-id="8bccd-267">Azure Firewall includes a built-in rule collection for infrastructure FQDNs that are allowed by default.</span></span> <span data-ttu-id="8bccd-268">These FQDNs are specific for the platform and can't be used for other purposes.</span><span class="sxs-lookup"><span data-stu-id="8bccd-268">These FQDNs are specific for the platform and can't be used for other purposes.</span></span> <span data-ttu-id="8bccd-269">The allowed infrastructure FQDNs include:</span><span class="sxs-lookup"><span data-stu-id="8bccd-269">The allowed infrastructure FQDNs include:</span></span>
>- <span data-ttu-id="8bccd-270">Compute access to storage Platform Image Repository (PIR).</span><span class="sxs-lookup"><span data-stu-id="8bccd-270">Compute access to storage Platform Image Repository (PIR).</span></span>
>- <span data-ttu-id="8bccd-271">Managed disks status storage access.</span><span class="sxs-lookup"><span data-stu-id="8bccd-271">Managed disks status storage access.</span></span>
>- <span data-ttu-id="8bccd-272">Windows Diagnostics</span><span class="sxs-lookup"><span data-stu-id="8bccd-272">Windows Diagnostics</span></span>
>
> <span data-ttu-id="8bccd-273">You can override this build-in infrastructure rule collection by creating a *deny all* application rule collection which is processed last.</span><span class="sxs-lookup"><span data-stu-id="8bccd-273">You can override this build-in infrastructure rule collection by creating a *deny all* application rule collection which is processed last.</span></span> <span data-ttu-id="8bccd-274">It will always be processed before the infrastructure rule collection.</span><span class="sxs-lookup"><span data-stu-id="8bccd-274">It will always be processed before the infrastructure rule collection.</span></span> <span data-ttu-id="8bccd-275">Anything not in the infrastructure rule collection is denied by default.</span><span class="sxs-lookup"><span data-stu-id="8bccd-275">Anything not in the infrastructure rule collection is denied by default.</span></span>

## <a name="configure-network-rules"></a><span data-ttu-id="8bccd-276">Configure network rules</span><span class="sxs-lookup"><span data-stu-id="8bccd-276">Configure network rules</span></span>

1. <span data-ttu-id="8bccd-277">Click **Add network rule collection**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-277">Click **Add network rule collection**.</span></span>
2. <span data-ttu-id="8bccd-278">For **Name**, type **Net-Coll01**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-278">For **Name**, type **Net-Coll01**.</span></span>
3. <span data-ttu-id="8bccd-279">For **Priority**, type **200**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-279">For **Priority**, type **200**.</span></span>
4. <span data-ttu-id="8bccd-280">For **Action**, select **Allow**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-280">For **Action**, select **Allow**.</span></span>

6. <span data-ttu-id="8bccd-281">Under **Rules**, for **Name**, type **AllowDNS**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-281">Under **Rules**, for **Name**, type **AllowDNS**.</span></span>
8. <span data-ttu-id="8bccd-282">For **Protocol**, select **UDP**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-282">For **Protocol**, select **UDP**.</span></span>
9. <span data-ttu-id="8bccd-283">For **Source Addresses**, type **10.0.2.0/24**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-283">For **Source Addresses**, type **10.0.2.0/24**.</span></span>
10. <span data-ttu-id="8bccd-284">For Destination address, type **209.244.0.3,209.244.0.4**</span><span class="sxs-lookup"><span data-stu-id="8bccd-284">For Destination address, type **209.244.0.3,209.244.0.4**</span></span>
11. <span data-ttu-id="8bccd-285">For **Destination Ports**, type **53**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-285">For **Destination Ports**, type **53**.</span></span>
12. <span data-ttu-id="8bccd-286">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-286">Click **Add**.</span></span>

### <a name="change-the-primary-and-secondary-dns-address-for-the-srv-work-network-interface"></a><span data-ttu-id="8bccd-287">Change the primary and secondary DNS address for the **Srv-Work** network interface</span><span class="sxs-lookup"><span data-stu-id="8bccd-287">Change the primary and secondary DNS address for the **Srv-Work** network interface</span></span>

<span data-ttu-id="8bccd-288">For testing purposes in this tutorial, you configure the primary and secondary DNS addresses.</span><span class="sxs-lookup"><span data-stu-id="8bccd-288">For testing purposes in this tutorial, you configure the primary and secondary DNS addresses.</span></span> <span data-ttu-id="8bccd-289">This is not a general Azure Firewall requirement.</span><span class="sxs-lookup"><span data-stu-id="8bccd-289">This is not a general Azure Firewall requirement.</span></span> 

1. <span data-ttu-id="8bccd-290">From the Azure portal, open the **Test-FW-RG** resource group.</span><span class="sxs-lookup"><span data-stu-id="8bccd-290">From the Azure portal, open the **Test-FW-RG** resource group.</span></span>
2. <span data-ttu-id="8bccd-291">Click the network interface for the **Srv-Work** virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bccd-291">Click the network interface for the **Srv-Work** virtual machine.</span></span>
3. <span data-ttu-id="8bccd-292">Under **Settings**, click **DNS servers**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-292">Under **Settings**, click **DNS servers**.</span></span>
4. <span data-ttu-id="8bccd-293">Under **DNS servers**, click **Custom**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-293">Under **DNS servers**, click **Custom**.</span></span>
5. <span data-ttu-id="8bccd-294">Type **209.244.0.3** in the **Add DNS server** text box, and **209.244.0.4** in the next text box.</span><span class="sxs-lookup"><span data-stu-id="8bccd-294">Type **209.244.0.3** in the **Add DNS server** text box, and **209.244.0.4** in the next text box.</span></span>
6. <span data-ttu-id="8bccd-295">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8bccd-295">Click **Save**.</span></span> 
7. <span data-ttu-id="8bccd-296">Restart the **Srv-Work** virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8bccd-296">Restart the **Srv-Work** virtual machine.</span></span>


## <a name="test-the-firewall"></a><span data-ttu-id="8bccd-297">Test the firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-297">Test the firewall</span></span>

1. <span data-ttu-id="8bccd-298">From the Azure portal, review the network settings for the **Srv-Work** virtual machine and note the private IP address.</span><span class="sxs-lookup"><span data-stu-id="8bccd-298">From the Azure portal, review the network settings for the **Srv-Work** virtual machine and note the private IP address.</span></span>
2. <span data-ttu-id="8bccd-299">Connect a remote desktop to **Srv-Jump** virtual machine, and from there open a remote desktop connection to the **Srv-Work** private IP address.</span><span class="sxs-lookup"><span data-stu-id="8bccd-299">Connect a remote desktop to **Srv-Jump** virtual machine, and from there open a remote desktop connection to the **Srv-Work** private IP address.</span></span>

5. <span data-ttu-id="8bccd-300">Open Internet Explorer and browse to http://github.com.</span><span class="sxs-lookup"><span data-stu-id="8bccd-300">Open Internet Explorer and browse to http://github.com.</span></span>
6. <span data-ttu-id="8bccd-301">Click **OK**, and **Close** on the security alerts.</span><span class="sxs-lookup"><span data-stu-id="8bccd-301">Click **OK**, and **Close** on the security alerts.</span></span>

   <span data-ttu-id="8bccd-302">You should see the GitHub home page.</span><span class="sxs-lookup"><span data-stu-id="8bccd-302">You should see the GitHub home page.</span></span>

7. <span data-ttu-id="8bccd-303">Browse to http://www.msn.com.</span><span class="sxs-lookup"><span data-stu-id="8bccd-303">Browse to http://www.msn.com.</span></span>

   <span data-ttu-id="8bccd-304">You should be blocked by the firewall.</span><span class="sxs-lookup"><span data-stu-id="8bccd-304">You should be blocked by the firewall.</span></span>

<span data-ttu-id="8bccd-305">So now you have verified that the firewall rules are working:</span><span class="sxs-lookup"><span data-stu-id="8bccd-305">So now you have verified that the firewall rules are working:</span></span>

- <span data-ttu-id="8bccd-306">You can browse to the one allowed FQDN, but not to any others.</span><span class="sxs-lookup"><span data-stu-id="8bccd-306">You can browse to the one allowed FQDN, but not to any others.</span></span>
- <span data-ttu-id="8bccd-307">You can resolve DNS names using the configured external DNS server.</span><span class="sxs-lookup"><span data-stu-id="8bccd-307">You can resolve DNS names using the configured external DNS server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="8bccd-308">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="8bccd-308">Clean up resources</span></span>

<span data-ttu-id="8bccd-309">You can keep your firewall resources for the next tutorial, or if no longer needed, delete the **Test-FW-RG** resource group to delete all firewall-related resources.</span><span class="sxs-lookup"><span data-stu-id="8bccd-309">You can keep your firewall resources for the next tutorial, or if no longer needed, delete the **Test-FW-RG** resource group to delete all firewall-related resources.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8bccd-310">Next steps</span><span class="sxs-lookup"><span data-stu-id="8bccd-310">Next steps</span></span>

<span data-ttu-id="8bccd-311">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="8bccd-311">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8bccd-312">Set up the network</span><span class="sxs-lookup"><span data-stu-id="8bccd-312">Set up the network</span></span>
> * <span data-ttu-id="8bccd-313">Create a firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-313">Create a firewall</span></span>
> * <span data-ttu-id="8bccd-314">Create a default route</span><span class="sxs-lookup"><span data-stu-id="8bccd-314">Create a default route</span></span>
> * <span data-ttu-id="8bccd-315">Configure application and network firewall rules</span><span class="sxs-lookup"><span data-stu-id="8bccd-315">Configure application and network firewall rules</span></span>
> * <span data-ttu-id="8bccd-316">Test the firewall</span><span class="sxs-lookup"><span data-stu-id="8bccd-316">Test the firewall</span></span>

<span data-ttu-id="8bccd-317">Next, you can monitor the Azure Firewall logs.</span><span class="sxs-lookup"><span data-stu-id="8bccd-317">Next, you can monitor the Azure Firewall logs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8bccd-318">Tutorial: Monitor Azure Firewall logs</span><span class="sxs-lookup"><span data-stu-id="8bccd-318">Tutorial: Monitor Azure Firewall logs</span></span>](./tutorial-diagnostics.md)
