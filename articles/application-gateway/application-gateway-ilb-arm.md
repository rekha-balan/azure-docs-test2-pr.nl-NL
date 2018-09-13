---
title: Using Azure Application Gateway with Internal Load Balancer - PowerShell | Microsoft Docs
description: This page provides instructions to create, configure, start, and delete an Azure application gateway with internal load balancer (ILB) for Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 75cfd5a2-e378-4365-99ee-a2b2abda2e0d
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: db097fd947112dc4747523693f89c80d984bd26d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552295"
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb-by-using-azure-resource-manager"></a><span data-ttu-id="e6a94-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6a94-103">Create an application gateway with an internal load balancer (ILB) by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

<span data-ttu-id="e6a94-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span><span class="sxs-lookup"><span data-stu-id="e6a94-106">Azure Application Gateway can be configured with an Internet-facing VIP or with an internal endpoint that is not exposed to the Internet, also known as an internal load balancer (ILB) endpoint.</span></span> <span data-ttu-id="e6a94-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-107">Configuring the gateway with an ILB is useful for internal line-of-business applications that are not exposed to the Internet.</span></span> <span data-ttu-id="e6a94-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span><span class="sxs-lookup"><span data-stu-id="e6a94-108">It's also useful for services and tiers within a multi-tier application that sit in a security boundary that is not exposed to the Internet but still require round-robin load distribution, session stickiness, or Secure Sockets Layer (SSL) termination.</span></span>

<span data-ttu-id="e6a94-109">This article walks you through the steps to configure an application gateway with an ILB.</span><span class="sxs-lookup"><span data-stu-id="e6a94-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e6a94-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e6a94-110">Before you begin</span></span>

1. <span data-ttu-id="e6a94-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="e6a94-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="e6a94-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e6a94-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="e6a94-113">You create a virtual network and a subnet for Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-113">You create a virtual network and a subnet for Application Gateway.</span></span> <span data-ttu-id="e6a94-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="e6a94-115">Application Gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-115">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="e6a94-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="e6a94-116">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="e6a94-117">What is required to create an application gateway?</span><span class="sxs-lookup"><span data-stu-id="e6a94-117">What is required to create an application gateway?</span></span>

* <span data-ttu-id="e6a94-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="e6a94-118">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="e6a94-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="e6a94-119">The IP addresses listed should either belong to the virtual network but in a different subnet for the application gateway or should be a public IP/VIP.</span></span>
* <span data-ttu-id="e6a94-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="e6a94-120">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="e6a94-121">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="e6a94-121">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="e6a94-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-122">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="e6a94-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="e6a94-123">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="e6a94-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="e6a94-124">**Listener:** The listener has a front-end port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="e6a94-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="e6a94-125">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="e6a94-126">Currently, only the *basic* rule is supported.</span><span class="sxs-lookup"><span data-stu-id="e6a94-126">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="e6a94-127">The *basic* rule is round-robin load distribution.</span><span class="sxs-lookup"><span data-stu-id="e6a94-127">The *basic* rule is round-robin load distribution.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="e6a94-128">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="e6a94-128">Create an application gateway</span></span>

<span data-ttu-id="e6a94-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span><span class="sxs-lookup"><span data-stu-id="e6a94-129">The difference between using Azure Classic and Azure Resource Manager is the order in which you create the application gateway and the items that need to be configured.</span></span>
<span data-ttu-id="e6a94-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="e6a94-130">With Resource Manager, all items that make an application gateway is configured individually and then put together to create the application gateway resource.</span></span>

<span data-ttu-id="e6a94-131">Here are the steps that are needed to create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="e6a94-131">Here are the steps that are needed to create an application gateway:</span></span>

1. <span data-ttu-id="e6a94-132">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6a94-132">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="e6a94-133">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="e6a94-133">Create a virtual network and a subnet for the application gateway</span></span>
3. <span data-ttu-id="e6a94-134">Create an application gateway configuration object</span><span class="sxs-lookup"><span data-stu-id="e6a94-134">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="e6a94-135">Create an application gateway resource</span><span class="sxs-lookup"><span data-stu-id="e6a94-135">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="e6a94-136">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e6a94-136">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="e6a94-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e6a94-137">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="e6a94-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e6a94-138">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="e6a94-139">Step 1</span><span class="sxs-lookup"><span data-stu-id="e6a94-139">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="e6a94-140">Step 2</span><span class="sxs-lookup"><span data-stu-id="e6a94-140">Step 2</span></span>

<span data-ttu-id="e6a94-141">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="e6a94-141">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e6a94-142">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="e6a94-142">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="e6a94-143">Step 3</span><span class="sxs-lookup"><span data-stu-id="e6a94-143">Step 3</span></span>

<span data-ttu-id="e6a94-144">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="e6a94-144">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="e6a94-145">Step 4</span><span class="sxs-lookup"><span data-stu-id="e6a94-145">Step 4</span></span>

<span data-ttu-id="e6a94-146">Create a new resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="e6a94-146">Create a new resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -location "West US"
```

<span data-ttu-id="e6a94-147">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="e6a94-147">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="e6a94-148">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="e6a94-148">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="e6a94-149">Make sure that all commands to create an application gateway uses the same resource group.</span><span class="sxs-lookup"><span data-stu-id="e6a94-149">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="e6a94-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span><span class="sxs-lookup"><span data-stu-id="e6a94-150">In the preceding example, we created a resource group called "appgw-rg" and location "West US".</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="e6a94-151">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="e6a94-151">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="e6a94-152">The following example shows how to create a virtual network by using Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="e6a94-152">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="e6a94-153">Step 1</span><span class="sxs-lookup"><span data-stu-id="e6a94-153">Step 1</span></span>

```powershell
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="e6a94-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="e6a94-154">This step assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="e6a94-155">Step 2</span><span class="sxs-lookup"><span data-stu-id="e6a94-155">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnetconfig
```

<span data-ttu-id="e6a94-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="e6a94-156">This step creates a virtual network named "appgwvnet" in resource group "appgw-rg" for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="e6a94-157">Step 3</span><span class="sxs-lookup"><span data-stu-id="e6a94-157">Step 3</span></span>

```powershell
$subnet = $vnet.subnets[0]
```

<span data-ttu-id="e6a94-158">This step assigns the subnet object to variable $subnet for the next steps.</span><span class="sxs-lookup"><span data-stu-id="e6a94-158">This step assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="e6a94-159">Create an application gateway configuration object</span><span class="sxs-lookup"><span data-stu-id="e6a94-159">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="e6a94-160">Step 1</span><span class="sxs-lookup"><span data-stu-id="e6a94-160">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="e6a94-161">This step creates an application gateway IP configuration named "gatewayIP01".</span><span class="sxs-lookup"><span data-stu-id="e6a94-161">This step creates an application gateway IP configuration named "gatewayIP01".</span></span> <span data-ttu-id="e6a94-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="e6a94-162">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="e6a94-163">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="e6a94-163">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="e6a94-164">Step 2</span><span class="sxs-lookup"><span data-stu-id="e6a94-164">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="e6a94-165">This step configures the back-end IP address pool named "pool01" with IP addresses "134.170.185.46, 134.170.188.221,134.170.185.50".</span><span class="sxs-lookup"><span data-stu-id="e6a94-165">This step configures the back-end IP address pool named "pool01" with IP addresses "134.170.185.46, 134.170.188.221,134.170.185.50".</span></span> <span data-ttu-id="e6a94-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="e6a94-166">Those are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="e6a94-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="e6a94-167">You replace the preceding IP addresses to add your own application IP address endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="e6a94-168">Step 3</span><span class="sxs-lookup"><span data-stu-id="e6a94-168">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

<span data-ttu-id="e6a94-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="e6a94-169">This step configures application gateway setting "poolsetting01" for the load balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="e6a94-170">Step 4</span><span class="sxs-lookup"><span data-stu-id="e6a94-170">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 80
```

<span data-ttu-id="e6a94-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span><span class="sxs-lookup"><span data-stu-id="e6a94-171">This step configures the front-end IP port named "frontendport01" for the ILB.</span></span>

### <a name="step-5"></a><span data-ttu-id="e6a94-172">Step 5</span><span class="sxs-lookup"><span data-stu-id="e6a94-172">Step 5</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -Subnet $subnet
```

<span data-ttu-id="e6a94-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-173">This step creates the front-end IP configuration called "fipconfig01" and associates it with a private IP from the current virtual network subnet.</span></span>

### <a name="step-6"></a><span data-ttu-id="e6a94-174">Step 6</span><span class="sxs-lookup"><span data-stu-id="e6a94-174">Step 6</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

<span data-ttu-id="e6a94-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="e6a94-175">This step creates the listener called "listener01" and associates the front-end port to the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="e6a94-176">Step 7</span><span class="sxs-lookup"><span data-stu-id="e6a94-176">Step 7</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="e6a94-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="e6a94-177">This step creates the load balancer routing rule called "rule01" that configures the load balancer behavior.</span></span>

### <a name="step-8"></a><span data-ttu-id="e6a94-178">Step 8</span><span class="sxs-lookup"><span data-stu-id="e6a94-178">Step 8</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="e6a94-179">This step configures the instance size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-179">This step configures the instance size of the application gateway.</span></span>

> [!NOTE]
> The default value for *InstanceCount* is 2, with a maximum value of 10. The default value for *GatewaySize* is Medium. You can choose between Standard_Small, Standard_Medium, and Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="e6a94-183">Create an application gateway by using New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="e6a94-183">Create an application gateway by using New-AzureApplicationGateway</span></span>

<span data-ttu-id="e6a94-184">Creates an application gateway with all configuration items from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="e6a94-184">Creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="e6a94-185">In this example, the application gateway is called "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="e6a94-185">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

<span data-ttu-id="e6a94-186">This step creates an application gateway with all configuration items from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="e6a94-186">This step creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="e6a94-187">In the example, the application gateway is called "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="e6a94-187">In the example, the application gateway is called "appgwtest".</span></span>

## <a name="delete-an-application-gateway"></a><span data-ttu-id="e6a94-188">Delete an application gateway</span><span class="sxs-lookup"><span data-stu-id="e6a94-188">Delete an application gateway</span></span>

<span data-ttu-id="e6a94-189">To delete an application gateway, you need to do the following steps in order:</span><span class="sxs-lookup"><span data-stu-id="e6a94-189">To delete an application gateway, you need to do the following steps in order:</span></span>

1. <span data-ttu-id="e6a94-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-190">Use the `Stop-AzureRmApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="e6a94-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-191">Use the `Remove-AzureRmApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="e6a94-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-192">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

### <a name="step-1"></a><span data-ttu-id="e6a94-193">Step 1</span><span class="sxs-lookup"><span data-stu-id="e6a94-193">Step 1</span></span>

<span data-ttu-id="e6a94-194">Get the application gateway object and associate it to a variable "$getgw".</span><span class="sxs-lookup"><span data-stu-id="e6a94-194">Get the application gateway object and associate it to a variable "$getgw".</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="e6a94-195">Step 2</span><span class="sxs-lookup"><span data-stu-id="e6a94-195">Step 2</span></span>

<span data-ttu-id="e6a94-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e6a94-196">Use `Stop-AzureRmApplicationGateway` to stop the application gateway.</span></span> <span data-ttu-id="e6a94-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span><span class="sxs-lookup"><span data-stu-id="e6a94-197">This sample shows the `Stop-AzureRmApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureRmApplicationGateway -ApplicationGateway $getgw  
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="e6a94-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span><span class="sxs-lookup"><span data-stu-id="e6a94-198">Once the application gateway is in a stopped state, use the `Remove-AzureRmApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Force
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

> [!NOTE]
> The **-force** switch can be used to suppress the remove confirmation message.

<span data-ttu-id="e6a94-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e6a94-200">To verify that the service has been removed, you can use the `Get-AzureRmApplicationGateway` cmdlet.</span></span> <span data-ttu-id="e6a94-201">This step is not required.</span><span class="sxs-lookup"><span data-stu-id="e6a94-201">This step is not required.</span></span>

```powershell
Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
```

## <a name="next-steps"></a><span data-ttu-id="e6a94-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6a94-202">Next steps</span></span>

<span data-ttu-id="e6a94-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="e6a94-203">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="e6a94-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="e6a94-204">If you want to configure an application gateway to use with an ILB, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="e6a94-205">If you want more information about load balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="e6a94-205">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="e6a94-206">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="e6a94-206">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="e6a94-207">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="e6a94-207">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

