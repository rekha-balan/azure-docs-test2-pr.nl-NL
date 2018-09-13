---
title: Create and manage an Azure Application Gateway - PowerShell | Microsoft Docs
description: This page provides instructions to create, configure, start, and delete an Azure application gateway by using Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 866e9b5f-0222-4b6a-a95f-77bc3d31d17b
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: gwallace
ms.openlocfilehash: 11ecfc993f17c89d4ac4431e9a835000d30afe76
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551511"
---
# <a name="create-start-or-delete-an-application-gateway-by-using-azure-resource-manager"></a><span data-ttu-id="11667-103">Create, start, or delete an application gateway by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11667-103">Create, start, or delete an application gateway by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

<span data-ttu-id="11667-109">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="11667-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="11667-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="11667-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span>
<span data-ttu-id="11667-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="11667-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span>

<span data-ttu-id="11667-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="11667-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="11667-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

> [!IMPORTANT]
> Before you work with Azure resources, it is important to understand that Azure currently has two deployment models: Resource Manager and classic. Make sure that you understand [deployment models and tools](../azure-classic-rm.md) before working with any Azure resource. You can view the documentation for different tools by clicking the tabs at the top of this article. This document covers creating an application gateway by using Azure Resource Manager. To use the classic version, go to [Create an application gateway classic deployment by using PowerShell](application-gateway-create-gateway.md).

## <a name="before-you-begin"></a><span data-ttu-id="11667-119">Before you begin</span><span class="sxs-lookup"><span data-stu-id="11667-119">Before you begin</span></span>

1. <span data-ttu-id="11667-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="11667-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="11667-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="11667-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
1. <span data-ttu-id="11667-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-122">If you have an existing virtual network, either select an existing empty subnet or create a subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="11667-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-123">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway.</span></span>
1. <span data-ttu-id="11667-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="11667-124">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="11667-125">What is required to create an application gateway?</span><span class="sxs-lookup"><span data-stu-id="11667-125">What is required to create an application gateway?</span></span>

* <span data-ttu-id="11667-126">**Back-end server pool:** The list of IP addresses, FQDNs, or NICs of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="11667-126">**Back-end server pool:** The list of IP addresses, FQDNs, or NICs of the back-end servers.</span></span> <span data-ttu-id="11667-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="11667-127">If IP addresses are used, they should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="11667-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="11667-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="11667-129">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="11667-129">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="11667-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-130">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="11667-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="11667-131">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="11667-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="11667-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="11667-133">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="11667-133">**Rule:** The rule binds the listener, the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="11667-134">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="11667-134">Create an application gateway</span></span>

<span data-ttu-id="11667-135">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span><span class="sxs-lookup"><span data-stu-id="11667-135">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="11667-136">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="11667-136">With Resource Manager, all items that make an application gateway are configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="11667-137">The following are the steps that are needed to create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-137">The following are the steps that are needed to create an application gateway.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="11667-138">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="11667-138">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="11667-139">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11667-139">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="11667-140">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="11667-140">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="11667-141">Step 1</span><span class="sxs-lookup"><span data-stu-id="11667-141">Step 1</span></span>

<span data-ttu-id="11667-142">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="11667-142">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="11667-143">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="11667-143">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="11667-144">Step 2</span><span class="sxs-lookup"><span data-stu-id="11667-144">Step 2</span></span>

<span data-ttu-id="11667-145">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="11667-145">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="11667-146">Step 3</span><span class="sxs-lookup"><span data-stu-id="11667-146">Step 3</span></span>

<span data-ttu-id="11667-147">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="11667-147">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="11667-148">Step 4</span><span class="sxs-lookup"><span data-stu-id="11667-148">Step 4</span></span>

<span data-ttu-id="11667-149">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="11667-149">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="11667-150">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="11667-150">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="11667-151">This location is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="11667-151">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="11667-152">Make sure that all commands to create an application gateway uses the same resource group.</span><span class="sxs-lookup"><span data-stu-id="11667-152">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="11667-153">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span><span class="sxs-lookup"><span data-stu-id="11667-153">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

> [!NOTE]
> If you need to configure a custom probe for your application gateway, visit: [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md). Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="11667-156">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="11667-156">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="11667-157">The following example shows how to create a virtual network by using Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="11667-157">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="11667-158">This example creates a VNET for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-158">This example creates a VNET for the Application Gateway.</span></span> <span data-ttu-id="11667-159">Application Gateway requires it's own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span><span class="sxs-lookup"><span data-stu-id="11667-159">Application Gateway requires it's own subnet, for this reason the subnet created for the Application Gateway is smaller than the VNET address space.</span></span> <span data-ttu-id="11667-160">By using a smaller subnet it allows for other resources, including but not limited to web servers to be configured in the same VNET.</span><span class="sxs-lookup"><span data-stu-id="11667-160">By using a smaller subnet it allows for other resources, including but not limited to web servers to be configured in the same VNET.</span></span>

### <a name="step-1"></a><span data-ttu-id="11667-161">Step 1</span><span class="sxs-lookup"><span data-stu-id="11667-161">Step 1</span></span>

<span data-ttu-id="11667-162">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="11667-162">Assign the address range 10.0.0.0/24 to the subnet variable to be used to create a virtual network.</span></span> <span data-ttu-id="11667-163">This step creates the subnet configuration object for the Application Gateway, which is used in the next example.</span><span class="sxs-lookup"><span data-stu-id="11667-163">This step creates the subnet configuration object for the Application Gateway, which is used in the next example.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="11667-164">Step 2</span><span class="sxs-lookup"><span data-stu-id="11667-164">Step 2</span></span>

<span data-ttu-id="11667-165">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="11667-165">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span> <span data-ttu-id="11667-166">This step completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span><span class="sxs-lookup"><span data-stu-id="11667-166">This step completes the configuration of the VNET with a single subnet for the Application Gateway to reside.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="11667-167">Step 3</span><span class="sxs-lookup"><span data-stu-id="11667-167">Step 3</span></span>

<span data-ttu-id="11667-168">Assign the subnet variable for the next steps, this variable is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span><span class="sxs-lookup"><span data-stu-id="11667-168">Assign the subnet variable for the next steps, this variable is passed to the `New-AzureRMApplicationGateway` cmdlet in a future step.</span></span>

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="11667-169">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="11667-169">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="11667-170">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="11667-170">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span> <span data-ttu-id="11667-171">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span><span class="sxs-lookup"><span data-stu-id="11667-171">Application Gateway can use a public IP address, internal IP address or both to receive requests for load balancing.</span></span>  <span data-ttu-id="11667-172">This example only uses a public IP address.</span><span class="sxs-lookup"><span data-stu-id="11667-172">This example only uses a public IP address.</span></span> <span data-ttu-id="11667-173">In the following example, no DNS name is configured for creating the Public IP address.</span><span class="sxs-lookup"><span data-stu-id="11667-173">In the following example, no DNS name is configured for creating the Public IP address.</span></span>  <span data-ttu-id="11667-174">Application Gateway does not support custom DNS names on public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="11667-174">Application Gateway does not support custom DNS names on public IP addresses.</span></span>  <span data-ttu-id="11667-175">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span><span class="sxs-lookup"><span data-stu-id="11667-175">If a custom name is required for the public endpoint, a CNAME record should be created to point to the automatically generated DNS name for the public IP address.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

> [!NOTE]
> An IP address is assigned to the application gateway when the service starts.

## <a name="create-the-application-gateway-configuration-objects"></a><span data-ttu-id="11667-177">Create the application gateway configuration objects</span><span class="sxs-lookup"><span data-stu-id="11667-177">Create the application gateway configuration objects</span></span>

<span data-ttu-id="11667-178">All configuration items must be set up before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-178">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="11667-179">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="11667-179">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="11667-180">Step 1</span><span class="sxs-lookup"><span data-stu-id="11667-180">Step 1</span></span>

<span data-ttu-id="11667-181">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="11667-181">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="11667-182">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="11667-182">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="11667-183">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="11667-183">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="11667-184">Step 2</span><span class="sxs-lookup"><span data-stu-id="11667-184">Step 2</span></span>

<span data-ttu-id="11667-185">Configure the back-end IP address pool named **pool01** with IP addresses for **pool1**.</span><span class="sxs-lookup"><span data-stu-id="11667-185">Configure the back-end IP address pool named **pool01** with IP addresses for **pool1**.</span></span> <span data-ttu-id="11667-186">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-186">These IP addresses are the IP addresses of the resources that are hosting the web application to be protected by the application gateway.</span></span> <span data-ttu-id="11667-187">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span><span class="sxs-lookup"><span data-stu-id="11667-187">These backend pool members are all validated to be healthy by probes whether they are basic probes or custom probes.</span></span>  <span data-ttu-id="11667-188">Traffic is then routed to them when requests come into the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-188">Traffic is then routed to them when requests come into the application gateway.</span></span> <span data-ttu-id="11667-189">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span><span class="sxs-lookup"><span data-stu-id="11667-189">Backend pools can be used by multiple rules within the application gateway, which means one backend pool could be used for multiple web applications that reside on the same host.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50
```

<span data-ttu-id="11667-190">In this example, there are two back-end pools to route network traffic based on the URL path.</span><span class="sxs-lookup"><span data-stu-id="11667-190">In this example, there are two back-end pools to route network traffic based on the URL path.</span></span> <span data-ttu-id="11667-191">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span><span class="sxs-lookup"><span data-stu-id="11667-191">One pool receives traffic from URL path "/video" and other pool receive traffic from path "/image".</span></span> <span data-ttu-id="11667-192">Replace the preceding IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="11667-192">Replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="11667-193">Step 3</span><span class="sxs-lookup"><span data-stu-id="11667-193">Step 3</span></span>

<span data-ttu-id="11667-194">Configure application gateway setting **poolsetting01** for the load-balanced network traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="11667-194">Configure application gateway setting **poolsetting01** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="11667-195">Each back-end pool can have its own back-end pool setting.</span><span class="sxs-lookup"><span data-stu-id="11667-195">Each back-end pool can have its own back-end pool setting.</span></span>  <span data-ttu-id="11667-196">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span><span class="sxs-lookup"><span data-stu-id="11667-196">Backend HTTP settings are used by rules to route traffic to the correct backend pool members.</span></span> <span data-ttu-id="11667-197">Backend HTTP settings determine the protocol and port that is used when sending traffic to the backend pool members.</span><span class="sxs-lookup"><span data-stu-id="11667-197">Backend HTTP settings determine the protocol and port that is used when sending traffic to the backend pool members.</span></span> <span data-ttu-id="11667-198">Cookie-based sessions are also determined by the backend HTTP settings.</span><span class="sxs-lookup"><span data-stu-id="11667-198">Cookie-based sessions are also determined by the backend HTTP settings.</span></span>  <span data-ttu-id="11667-199">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span><span class="sxs-lookup"><span data-stu-id="11667-199">If enabled, cookie-based session affinity sends traffic to the same backend as previous requests for each packet.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
```

### <a name="step-4"></a><span data-ttu-id="11667-200">Step 4</span><span class="sxs-lookup"><span data-stu-id="11667-200">Step 4</span></span>

<span data-ttu-id="11667-201">Configure the front-end port for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-201">Configure the front-end port for an application gateway.</span></span> <span data-ttu-id="11667-202">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span><span class="sxs-lookup"><span data-stu-id="11667-202">The front-end port configuration object is used by a listener to define what port the Application Gateway listens for traffic on the listener.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

### <a name="step-5"></a><span data-ttu-id="11667-203">Step 5</span><span class="sxs-lookup"><span data-stu-id="11667-203">Step 5</span></span>

<span data-ttu-id="11667-204">Configure the front-end IP with public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="11667-204">Configure the front-end IP with public IP endpoint.</span></span> <span data-ttu-id="11667-205">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span><span class="sxs-lookup"><span data-stu-id="11667-205">The front-end IP configuration object is used by a listener to relate the outward facing IP address with the listener.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

### <a name="step-6"></a><span data-ttu-id="11667-206">Step 6</span><span class="sxs-lookup"><span data-stu-id="11667-206">Step 6</span></span>

<span data-ttu-id="11667-207">Configure the listener.</span><span class="sxs-lookup"><span data-stu-id="11667-207">Configure the listener.</span></span> <span data-ttu-id="11667-208">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span><span class="sxs-lookup"><span data-stu-id="11667-208">This step configures the listener for the public IP address and port used to receive incoming network traffic.</span></span> <span data-ttu-id="11667-209">The following example takes the previously configured front-end IP configuration, front-end port configuration, and a protocol (http or https) and configures the listener.</span><span class="sxs-lookup"><span data-stu-id="11667-209">The following example takes the previously configured front-end IP configuration, front-end port configuration, and a protocol (http or https) and configures the listener.</span></span> <span data-ttu-id="11667-210">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span><span class="sxs-lookup"><span data-stu-id="11667-210">In this example, the listener listens to HTTP traffic on port 80 on the public IP address that was created earlier.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

### <a name="step-7"></a><span data-ttu-id="11667-211">Step 7</span><span class="sxs-lookup"><span data-stu-id="11667-211">Step 7</span></span>

<span data-ttu-id="11667-212">Create the load balancer routing rule named **rule01** that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="11667-212">Create the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span> <span data-ttu-id="11667-213">The back-end pool settings, listener, and back-end pool created in the previous steps make up the rule.</span><span class="sxs-lookup"><span data-stu-id="11667-213">The back-end pool settings, listener, and back-end pool created in the previous steps make up the rule.</span></span> <span data-ttu-id="11667-214">Based on the criteria defined traffic is routed to the appropriate backend.</span><span class="sxs-lookup"><span data-stu-id="11667-214">Based on the criteria defined traffic is routed to the appropriate backend.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting01 -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-8"></a><span data-ttu-id="11667-215">Step 8</span><span class="sxs-lookup"><span data-stu-id="11667-215">Step 8</span></span>

<span data-ttu-id="11667-216">Configure the number of instances and size for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-216">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> The default value for **InstanceCount** is 2, with a maximum value of 10. The default value for **GatewaySize** is Medium. You can choose between **Standard_Small**, **Standard_Medium**, and **Standard_Large**.

## <a name="create-an-application-gateway-by-using-new-azurermapplicationgateway"></a><span data-ttu-id="11667-220">Create an application gateway by using New-AzureRmApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="11667-220">Create an application gateway by using New-AzureRmApplicationGateway</span></span>

<span data-ttu-id="11667-221">Create an application gateway with all configuration items from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="11667-221">Create an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="11667-222">In this example, the application gateway is called **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="11667-222">In this example, the application gateway is called **appgwtest**.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="11667-223">Retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-223">Retrieve DNS and VIP details of the application gateway from the public IP resource attached to the application gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name publicIP01 -ResourceGroupName appgw-rg  
```

## <a name="delete-an-application-gateway"></a><span data-ttu-id="11667-224">Delete an application gateway</span><span class="sxs-lookup"><span data-stu-id="11667-224">Delete an application gateway</span></span>

<span data-ttu-id="11667-225">To delete an application gateway, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="11667-225">To delete an application gateway, follow these steps:</span></span>

### <a name="step-1"></a><span data-ttu-id="11667-226">Step 1</span><span class="sxs-lookup"><span data-stu-id="11667-226">Step 1</span></span>

<span data-ttu-id="11667-227">Get the application gateway object and associate it to a variable `$getgw`.</span><span class="sxs-lookup"><span data-stu-id="11667-227">Get the application gateway object and associate it to a variable `$getgw`.</span></span>

```powershell
$getgw = Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="11667-228">Step 2</span><span class="sxs-lookup"><span data-stu-id="11667-228">Step 2</span></span>

<span data-ttu-id="11667-229">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-229">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw
```

<span data-ttu-id="11667-230">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span><span class="sxs-lookup"><span data-stu-id="11667-230">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name $appgwtest -ResourceGroupName appgw-rg -Force
```

> [!NOTE]
> The **-force** switch can be used to suppress the remove confirmation message.

<span data-ttu-id="11667-232">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11667-232">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="11667-233">This step is not required.</span><span class="sxs-lookup"><span data-stu-id="11667-233">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="11667-234">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="11667-234">Get application gateway DNS name</span></span>

<span data-ttu-id="11667-235">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="11667-235">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="11667-236">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="11667-236">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="11667-237">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-237">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="11667-238">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="11667-238">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="11667-239">To To find the dynamically created DNS name, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-239">To To find the dynamically created DNS name, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="11667-240">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="11667-240">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="11667-241">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="11667-241">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="11667-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="11667-242">Next steps</span></span>

<span data-ttu-id="11667-243">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="11667-243">If you want to configure SSL offload, visit: [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="11667-244">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="11667-244">If you want to configure an application gateway to use with an internal load balancer, visit: [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="11667-245">If you want more information about load balancing options in general, visit:</span><span class="sxs-lookup"><span data-stu-id="11667-245">If you want more information about load balancing options in general, visit:</span></span>

* [<span data-ttu-id="11667-246">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="11667-246">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="11667-247">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="11667-247">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

