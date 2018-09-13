---
title: Create an application gateway using URL routing rules | Microsoft Docs
description: This page provides instructions to create, configure an Azure application gateway using URL routing rules
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 393fba150326fa7e10192e922a04ed26b2f5d089
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549267"
---
# <a name="create-an-application-gateway-using-path-based-routing"></a><span data-ttu-id="17c41-103">Create an application gateway using Path-based routing</span><span class="sxs-lookup"><span data-stu-id="17c41-103">Create an application gateway using Path-based routing</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-url-route-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-url-route-arm-ps.md)

<span data-ttu-id="17c41-106">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span><span class="sxs-lookup"><span data-stu-id="17c41-106">URL Path-based routing enables you to associate routes based on the URL path of an Http request.</span></span> <span data-ttu-id="17c41-107">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-107">It checks if there is a route to a back-end pool configured for the URL presented in the Application Gateway and sends the network traffic to the defined back-end pool.</span></span> <span data-ttu-id="17c41-108">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span><span class="sxs-lookup"><span data-stu-id="17c41-108">A common use for URL-based routing is to load balance requests for different content types to different back-end server pools.</span></span>

<span data-ttu-id="17c41-109">URL-based routing introduces a new rule type to application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-109">URL-based routing introduces a new rule type to application gateway.</span></span> <span data-ttu-id="17c41-110">Application gateway has two rule types: basic and PathBasedRouting.</span><span class="sxs-lookup"><span data-stu-id="17c41-110">Application gateway has two rule types: basic and PathBasedRouting.</span></span> <span data-ttu-id="17c41-111">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-111">Basic rule type provides round-robin service for the back-end pools while PathBasedRouting in addition to round robin distribution, also takes path pattern of the request URL into account while choosing the backend pool.</span></span>

## <a name="scenario"></a><span data-ttu-id="17c41-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="17c41-112">Scenario</span></span>

<span data-ttu-id="17c41-113">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-113">In the following example, Application Gateway is serving traffic for contoso.com with two back-end server pools: video server pool and image server pool.</span></span>

<span data-ttu-id="17c41-114">Requests for http://contoso.com/image\* are routed to image server pool (pool1), and http://contoso.com/video\* are routed to video server pool (pool2).</span><span class="sxs-lookup"><span data-stu-id="17c41-114">Requests for http://contoso.com/image\* are routed to image server pool (pool1), and http://contoso.com/video\* are routed to video server pool (pool2).</span></span> <span data-ttu-id="17c41-115">if none of the path patterns match , a default server pool (pool1) is selected.</span><span class="sxs-lookup"><span data-stu-id="17c41-115">if none of the path patterns match , a default server pool (pool1) is selected.</span></span>

![url route](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a><span data-ttu-id="17c41-117">Before you begin</span><span class="sxs-lookup"><span data-stu-id="17c41-117">Before you begin</span></span>

1. <span data-ttu-id="17c41-118">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="17c41-118">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="17c41-119">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="17c41-119">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="17c41-120">You create a virtual network and subnet for Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-120">You create a virtual network and subnet for Application Gateway.</span></span> <span data-ttu-id="17c41-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="17c41-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="17c41-122">The application gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="17c41-122">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="17c41-123">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="17c41-123">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="17c41-124">What is required to create an application gateway?</span><span class="sxs-lookup"><span data-stu-id="17c41-124">What is required to create an application gateway?</span></span>

* <span data-ttu-id="17c41-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="17c41-125">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="17c41-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="17c41-126">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="17c41-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="17c41-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="17c41-128">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-128">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="17c41-129">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-129">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="17c41-130">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="17c41-130">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="17c41-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="17c41-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="17c41-132">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="17c41-132">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="17c41-133">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="17c41-133">Create an application gateway</span></span>

<span data-ttu-id="17c41-134">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span><span class="sxs-lookup"><span data-stu-id="17c41-134">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="17c41-135">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="17c41-135">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="17c41-136">Here are the steps that are needed to create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="17c41-136">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="17c41-137">Create a resource group for Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="17c41-137">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="17c41-138">Create a virtual network, subnet, and public IP for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-138">Create a virtual network, subnet, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="17c41-139">Create an application gateway configuration object.</span><span class="sxs-lookup"><span data-stu-id="17c41-139">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="17c41-140">Create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="17c41-140">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="17c41-141">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="17c41-141">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="17c41-142">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="17c41-142">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="17c41-143">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="17c41-143">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="17c41-144">Step 1</span><span class="sxs-lookup"><span data-stu-id="17c41-144">Step 1</span></span>

<span data-ttu-id="17c41-145">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="17c41-145">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="17c41-146">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="17c41-146">You are prompted to authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="17c41-147">Step 2</span><span class="sxs-lookup"><span data-stu-id="17c41-147">Step 2</span></span>

<span data-ttu-id="17c41-148">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="17c41-148">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="17c41-149">Step 3</span><span class="sxs-lookup"><span data-stu-id="17c41-149">Step 3</span></span>

<span data-ttu-id="17c41-150">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="17c41-150">Choose which of your Azure subscriptions to use.</span></span> <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="17c41-151">Step 4</span><span class="sxs-lookup"><span data-stu-id="17c41-151">Step 4</span></span>

<span data-ttu-id="17c41-152">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="17c41-152">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

<span data-ttu-id="17c41-153">Alternatively you can also create tags for a resource group for application gateway:</span><span class="sxs-lookup"><span data-stu-id="17c41-153">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

<span data-ttu-id="17c41-154">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="17c41-154">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="17c41-155">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="17c41-155">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="17c41-156">Make sure that all commands to create an application gateway use the same resource group.</span><span class="sxs-lookup"><span data-stu-id="17c41-156">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="17c41-157">In the example above, we created a resource group called "appgw-RG" and location "West US".</span><span class="sxs-lookup"><span data-stu-id="17c41-157">In the example above, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md). Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="17c41-160">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="17c41-160">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="17c41-161">The following example shows how to create a virtual network by using Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="17c41-161">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="17c41-162">This example creates a VNET for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-162">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="17c41-163">Application Gateway requires it's own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span><span class="sxs-lookup"><span data-stu-id="17c41-163">Application Gateway requires it's own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="17c41-164">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span><span class="sxs-lookup"><span data-stu-id="17c41-164">This allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="17c41-165">Step 1</span><span class="sxs-lookup"><span data-stu-id="17c41-165">Step 1</span></span>

<span data-ttu-id="17c41-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="17c41-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span>  <span data-ttu-id="17c41-167">This creates the subnet configuration object for the Application Gateway which is used in the next example.</span><span class="sxs-lookup"><span data-stu-id="17c41-167">This creates the subnet configuration object for the Application Gateway which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="17c41-168">Step 2</span><span class="sxs-lookup"><span data-stu-id="17c41-168">Step 2</span></span>

<span data-ttu-id="17c41-169">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="17c41-169">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="17c41-170">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span><span class="sxs-lookup"><span data-stu-id="17c41-170">This completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="17c41-171">Step 3</span><span class="sxs-lookup"><span data-stu-id="17c41-171">Step 3</span></span>

<span data-ttu-id="17c41-172">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span><span class="sxs-lookup"><span data-stu-id="17c41-172">Assign the subnet variable for the next steps, this is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="17c41-173">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="17c41-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="17c41-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="17c41-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="17c41-175">Application Gateway can use a public IP address, internal IP address or both to receieve requests for load balancing.</span><span class="sxs-lookup"><span data-stu-id="17c41-175">Application Gateway can use a public IP address, internal IP address or both to receieve requests for load balancing.</span></span>  <span data-ttu-id="17c41-176">This example only uses a public IP address.</span><span class="sxs-lookup"><span data-stu-id="17c41-176">This example only uses a public IP address.</span></span> <span data-ttu-id="17c41-177">In the following example no DNS name is configured for creating the Public IP address.</span><span class="sxs-lookup"><span data-stu-id="17c41-177">In the following example no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="17c41-178">Application Gateway does not support custom DNS names on public IP addreses.</span><span class="sxs-lookup"><span data-stu-id="17c41-178">Application Gateway does not support custom DNS names on public IP addreses.</span></span>  <span data-ttu-id="17c41-179">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span><span class="sxs-lookup"><span data-stu-id="17c41-179">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="17c41-180">An IP address is assigned to the application gateway when the service starts.</span><span class="sxs-lookup"><span data-stu-id="17c41-180">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="17c41-181">Create application gateway configuration</span><span class="sxs-lookup"><span data-stu-id="17c41-181">Create application gateway configuration</span></span>

<span data-ttu-id="17c41-182">All configuration items must be set up before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-182">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="17c41-183">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="17c41-183">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="17c41-184">Step 1</span><span class="sxs-lookup"><span data-stu-id="17c41-184">Step 1</span></span>

<span data-ttu-id="17c41-185">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="17c41-185">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="17c41-186">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-186">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="17c41-187">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="17c41-187">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="17c41-188">Step 2</span><span class="sxs-lookup"><span data-stu-id="17c41-188">Step 2</span></span>

<span data-ttu-id="17c41-189">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span><span class="sxs-lookup"><span data-stu-id="17c41-189">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses for **pool1** and **pool2**.</span></span> <span data-ttu-id="17c41-190">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-190">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="17c41-191">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span><span class="sxs-lookup"><span data-stu-id="17c41-191">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="17c41-192">Traffic is then routed to them when requests come into the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-192">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="17c41-193">Backend pools can be used by multiple rules within the application gateway which means one backend pool could be used for multiple web applications that reside on the same host.</span><span class="sxs-lookup"><span data-stu-id="17c41-193">Backend pools can be used by multiple rules within the application gateway which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

<span data-ttu-id="17c41-194">In this example, there are two back-end pools to route network traffic based on the URL path.</span><span class="sxs-lookup"><span data-stu-id="17c41-194">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="17c41-195">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span><span class="sxs-lookup"><span data-stu-id="17c41-195">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="17c41-196">Replace the preceding IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="17c41-196">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span> 

### <a name="step-3"></a><span data-ttu-id="17c41-197">Step 3</span><span class="sxs-lookup"><span data-stu-id="17c41-197">Step 3</span></span>

<span data-ttu-id="17c41-198">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-198">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="17c41-199">In this example, you configure different back-end pool settings for the back-end pools.</span><span class="sxs-lookup"><span data-stu-id="17c41-199">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="17c41-200">Each back-end pool can have its own back-end pool setting.</span><span class="sxs-lookup"><span data-stu-id="17c41-200">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="17c41-201">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span><span class="sxs-lookup"><span data-stu-id="17c41-201">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="17c41-202">This determines the protocol and port that is used when sending traffic to the backend pool members.</span><span class="sxs-lookup"><span data-stu-id="17c41-202">This determines the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="17c41-203">Cookie-based sessions are also determined by the backend HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="17c41-203">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="17c41-204">If enabled, cookie-based session affinity will send traffic to the same backend as previous requests for each packet.</span><span class="sxs-lookup"><span data-stu-id="17c41-204">If enabled, cookie-based session affinity will send traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="17c41-205">Step 4</span><span class="sxs-lookup"><span data-stu-id="17c41-205">Step 4</span></span>

<span data-ttu-id="17c41-206">Configure the front-end IP with public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="17c41-206">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="17c41-207">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span><span class="sxs-lookup"><span data-stu-id="17c41-207">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="17c41-208">Step 5</span><span class="sxs-lookup"><span data-stu-id="17c41-208">Step 5</span></span>

<span data-ttu-id="17c41-209">Configure the front-end port for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-209">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="17c41-210">The front-end port configuration object is used by a listener to define what port the Application Gateway will listen for traffic on the listener.</span><span class="sxs-lookup"><span data-stu-id="17c41-210">The front-end port configuration object is used by a listener to define what port the Application Gateway will listen for traffic on the listener.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a><span data-ttu-id="17c41-211">Step 6</span><span class="sxs-lookup"><span data-stu-id="17c41-211">Step 6</span></span>

<span data-ttu-id="17c41-212">Configure the listener.</span><span class="sxs-lookup"><span data-stu-id="17c41-212">Configure the listener.</span></span> <span data-ttu-id="17c41-213">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span><span class="sxs-lookup"><span data-stu-id="17c41-213">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="17c41-214">The following example takes the previously configured front-end IP configuration,  front-end port configuration and a protocol (http or https) and configures the listener.</span><span class="sxs-lookup"><span data-stu-id="17c41-214">The following example takes the previously configured front-end IP configuration,  front-end port configuration and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="17c41-215">In this example the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span><span class="sxs-lookup"><span data-stu-id="17c41-215">In this example the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a><span data-ttu-id="17c41-216">Step 7</span><span class="sxs-lookup"><span data-stu-id="17c41-216">Step 7</span></span>

<span data-ttu-id="17c41-217">Configure URL rule paths for the back-end pools.</span><span class="sxs-lookup"><span data-stu-id="17c41-217">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="17c41-218">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="17c41-218">This step configures the relative path used by application gateway to define the mapping between URL path and which back-end pool is assigned to handle the incoming traffic.</span></span>

> [!IMPORTANT]
> Each path must start with / and the only place a "\*" is allowed, is at the end. Valid examples are /xyz, /xyz* or /xyz/*. The string fed to the path matcher does not include any text after the first "?" or "#", and those characters are not allowed. 

<span data-ttu-id="17c41-222">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2".</span><span class="sxs-lookup"><span data-stu-id="17c41-222">The following example creates two rules: one for "/image/" path routing traffic to back-end "pool1" and another one for "/video/" path routing traffic to back-end "pool2".</span></span> <span data-ttu-id="17c41-223">These rules ensure that traffic for each set of urls is routed to the backend.</span><span class="sxs-lookup"><span data-stu-id="17c41-223">These rules ensure that traffic for each set of urls is routed to the backend.</span></span> <span data-ttu-id="17c41-224">For example, http://contoso.com/image/figure1.jpg will go to pool1 and http://contoso.com/video/example.mp4 will go to pool2.</span><span class="sxs-lookup"><span data-stu-id="17c41-224">For example, http://contoso.com/image/figure1.jpg will go to pool1 and http://contoso.com/video/example.mp4 will go to pool2.</span></span>

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

<span data-ttu-id="17c41-225">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span><span class="sxs-lookup"><span data-stu-id="17c41-225">If the path doesn't match any of the pre-defined path rules, the rule path map configuration also configures a default back-end address pool.</span></span> <span data-ttu-id="17c41-226">For example, http://contoso.com/shoppingcart/test.html will go to pool1 as it is defined as the default pool for un-matched traffic.</span><span class="sxs-lookup"><span data-stu-id="17c41-226">For example, http://contoso.com/shoppingcart/test.html will go to pool1 as it is defined as the default pool for un-matched traffic.</span></span>

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a><span data-ttu-id="17c41-227">Step 8</span><span class="sxs-lookup"><span data-stu-id="17c41-227">Step 8</span></span>

<span data-ttu-id="17c41-228">Create a rule setting.</span><span class="sxs-lookup"><span data-stu-id="17c41-228">Create a rule setting.</span></span> <span data-ttu-id="17c41-229">This step configures the application gateway to use URL path-based routing.</span><span class="sxs-lookup"><span data-stu-id="17c41-229">This step configures the application gateway to use URL path-based routing.</span></span> <span data-ttu-id="17c41-230">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span><span class="sxs-lookup"><span data-stu-id="17c41-230">The `$urlPathMap` variable defined in the earlier step is now used to create the path-based rule.</span></span> <span data-ttu-id="17c41-231">In this step we associate the rule with a listener and the url path mapping created earlier.</span><span class="sxs-lookup"><span data-stu-id="17c41-231">In this step we associate the rule with a listener and the url path mapping created earlier.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a><span data-ttu-id="17c41-232">Step 9</span><span class="sxs-lookup"><span data-stu-id="17c41-232">Step 9</span></span>

<span data-ttu-id="17c41-233">Configure the number of instances and size for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-233">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="17c41-234">Create Application Gateway</span><span class="sxs-lookup"><span data-stu-id="17c41-234">Create Application Gateway</span></span>

<span data-ttu-id="17c41-235">Create an application gateway with all configuration objects from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="17c41-235">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="17c41-236">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="17c41-236">Get application gateway DNS name</span></span>

<span data-ttu-id="17c41-237">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="17c41-237">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="17c41-238">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="17c41-238">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="17c41-239">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-239">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="17c41-240">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="17c41-240">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="17c41-241">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-241">To configure the frontend IP CNAME record, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="17c41-242">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="17c41-242">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="17c41-243">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="17c41-243">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -Name publicIP01
```

```
Name                     : publicIP01
ResourceGroupName        : appgw-RG
Location                 : westus
Id                       : /subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/publicIPAddresses/publicIP01
Etag                     : W/"00000d5b-54ed-4907-bae8-99bd5766d0e5"
ResourceGuid             : 00000000-0000-0000-0000-000000000000
ProvisioningState        : Succeeded
Tags                     : 
PublicIpAllocationMethod : Dynamic
IpAddress                : xx.xx.xxx.xx
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : {
                                "Id": "/subscriptions/<subscription_id>/resourceGroups/appgw-RG/providers/Microsoft.Network/applicationGateways/appgwtest/frontendIP
                            Configurations/frontend1"
                            }
DnsSettings              : {
                                "Fqdn": "00000000-0000-xxxx-xxxx-xxxxxxxxxxxx.cloudapp.net"
                            }
```

## <a name="next-steps"></a><span data-ttu-id="17c41-244">Next steps</span><span class="sxs-lookup"><span data-stu-id="17c41-244">Next steps</span></span>

<span data-ttu-id="17c41-245">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span><span class="sxs-lookup"><span data-stu-id="17c41-245">If you want to learn Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl-arm.md).</span></span>


