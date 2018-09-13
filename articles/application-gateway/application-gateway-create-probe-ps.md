---
title: Create a custom probe - Azure Application Gateway - PowerShell | Microsoft Docs
description: Learn how to create a custom probe for Application Gateway by using PowerShell in Resource Manager
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 68feb660-7fa4-4f69-a7e4-bdd7bdc474db
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 794797d9c42ec7f2fc351bab109147e45ce06070
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551654"
---
# <a name="create-a-custom-probe-for-azure-application-gateway-by-using-powershell-for-azure-resource-manager"></a><span data-ttu-id="4577a-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4577a-103">Create a custom probe for Azure Application Gateway by using PowerShell for Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

[!INCLUDE [azure-probe-intro-include](../../includes/application-gateway-create-probe-intro-include.md)]

> [!NOTE]
> Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).  This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](application-gateway-create-probe-classic-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

### <a name="step-1"></a><span data-ttu-id="4577a-109">Step 1</span><span class="sxs-lookup"><span data-stu-id="4577a-109">Step 1</span></span>

<span data-ttu-id="4577a-110">Use `Login-AzureRmAccount` to authenticate.</span><span class="sxs-lookup"><span data-stu-id="4577a-110">Use `Login-AzureRmAccount` to authenticate.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="4577a-111">Step 2</span><span class="sxs-lookup"><span data-stu-id="4577a-111">Step 2</span></span>

<span data-ttu-id="4577a-112">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="4577a-112">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="4577a-113">Step 3</span><span class="sxs-lookup"><span data-stu-id="4577a-113">Step 3</span></span>

<span data-ttu-id="4577a-114">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="4577a-114">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="4577a-115">Step 4</span><span class="sxs-lookup"><span data-stu-id="4577a-115">Step 4</span></span>

<span data-ttu-id="4577a-116">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="4577a-116">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="4577a-117">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="4577a-117">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="4577a-118">This location is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="4577a-118">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="4577a-119">Make sure that all commands to create an application gateway use the same resource group.</span><span class="sxs-lookup"><span data-stu-id="4577a-119">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="4577a-120">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span><span class="sxs-lookup"><span data-stu-id="4577a-120">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="4577a-121">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="4577a-121">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="4577a-122">The following steps create a virtual network and a subnet for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-122">The following steps create a virtual network and a subnet for the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="4577a-123">Step 1</span><span class="sxs-lookup"><span data-stu-id="4577a-123">Step 1</span></span>

<span data-ttu-id="4577a-124">Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="4577a-124">Assign the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a><span data-ttu-id="4577a-125">Step 2</span><span class="sxs-lookup"><span data-stu-id="4577a-125">Step 2</span></span>

<span data-ttu-id="4577a-126">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="4577a-126">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a><span data-ttu-id="4577a-127">Step 3</span><span class="sxs-lookup"><span data-stu-id="4577a-127">Step 3</span></span>

<span data-ttu-id="4577a-128">Assign a subnet variable for the next steps, which create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-128">Assign a subnet variable for the next steps, which create an application gateway.</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="4577a-129">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="4577a-129">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="4577a-130">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="4577a-130">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name publicIP01 -Location "West US" -AllocationMethod Dynamic
```

## <a name="create-an-application-gateway-configuration-object-with-a-custom-probe"></a><span data-ttu-id="4577a-131">Create an application gateway configuration object with a custom probe</span><span class="sxs-lookup"><span data-stu-id="4577a-131">Create an application gateway configuration object with a custom probe</span></span>

<span data-ttu-id="4577a-132">You set up all configuration items before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-132">You set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="4577a-133">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="4577a-133">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="4577a-134">Step 1</span><span class="sxs-lookup"><span data-stu-id="4577a-134">Step 1</span></span>

<span data-ttu-id="4577a-135">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="4577a-135">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="4577a-136">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="4577a-136">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="4577a-137">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="4577a-137">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a><span data-ttu-id="4577a-138">Step 2</span><span class="sxs-lookup"><span data-stu-id="4577a-138">Step 2</span></span>

<span data-ttu-id="4577a-139">Configure the back-end IP address pool named **pool01** with IP addresses **134.170.185.46, 134.170.188.221, 134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="4577a-139">Configure the back-end IP address pool named **pool01** with IP addresses **134.170.185.46, 134.170.188.221, 134.170.185.50**.</span></span> <span data-ttu-id="4577a-140">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="4577a-140">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="4577a-141">You replace the IP addresses above to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="4577a-141">You replace the IP addresses above to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50
```

### <a name="step-3"></a><span data-ttu-id="4577a-142">Step 3</span><span class="sxs-lookup"><span data-stu-id="4577a-142">Step 3</span></span>

<span data-ttu-id="4577a-143">The custom probe is configured in this step.</span><span class="sxs-lookup"><span data-stu-id="4577a-143">The custom probe is configured in this step.</span></span>

<span data-ttu-id="4577a-144">The parameters used are:</span><span class="sxs-lookup"><span data-stu-id="4577a-144">The parameters used are:</span></span>

* <span data-ttu-id="4577a-145">**Interval** - Configures the probe interval checks in seconds.</span><span class="sxs-lookup"><span data-stu-id="4577a-145">**Interval** - Configures the probe interval checks in seconds.</span></span>
* <span data-ttu-id="4577a-146">**Timeout** - Defines the probe time-out for an HTTP response check.</span><span class="sxs-lookup"><span data-stu-id="4577a-146">**Timeout** - Defines the probe time-out for an HTTP response check.</span></span>
* <span data-ttu-id="4577a-147">**Hostname and path** - Complete URL path that is invoked by Application Gateway to determine the health of the instance.</span><span class="sxs-lookup"><span data-stu-id="4577a-147">**Hostname and path** - Complete URL path that is invoked by Application Gateway to determine the health of the instance.</span></span> <span data-ttu-id="4577a-148">For example, if you have a website **http://contoso.com/**, then the custom probe can be configured for **http://contoso.com/path/custompath.htm** for probe checks to have a successful HTTP response.</span><span class="sxs-lookup"><span data-stu-id="4577a-148">For example, if you have a website **http://contoso.com/**, then the custom probe can be configured for **http://contoso.com/path/custompath.htm** for probe checks to have a successful HTTP response.</span></span>
* <span data-ttu-id="4577a-149">**UnhealthyThreshold** - The number of failed HTTP responses needed to flag the back-end instance as **unhealthy**.</span><span class="sxs-lookup"><span data-stu-id="4577a-149">**UnhealthyThreshold** - The number of failed HTTP responses needed to flag the back-end instance as **unhealthy**.</span></span>

```powershell
$probe = New-AzureRmApplicationGatewayProbeConfig -Name probe01 -Protocol Http -HostName "contoso.com" -Path "/path/path.htm" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-4"></a><span data-ttu-id="4577a-150">Step 4</span><span class="sxs-lookup"><span data-stu-id="4577a-150">Step 4</span></span>

<span data-ttu-id="4577a-151">Configure application gateway setting **poolsetting01** for the traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="4577a-151">Configure application gateway setting **poolsetting01** for the traffic in the back-end pool.</span></span> <span data-ttu-id="4577a-152">This step also has a time-out configuration that is for the back-end pool response to an application gateway request.</span><span class="sxs-lookup"><span data-stu-id="4577a-152">This step also has a time-out configuration that is for the back-end pool response to an application gateway request.</span></span> <span data-ttu-id="4577a-153">When a back-end response hits a time-out limit, Application Gateway cancels the request.</span><span class="sxs-lookup"><span data-stu-id="4577a-153">When a back-end response hits a time-out limit, Application Gateway cancels the request.</span></span> <span data-ttu-id="4577a-154">This value is different from a probe time-out that is only for the back-end response to probe checks.</span><span class="sxs-lookup"><span data-stu-id="4577a-154">This value is different from a probe time-out that is only for the back-end response to probe checks.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 80
```

### <a name="step-5"></a><span data-ttu-id="4577a-155">Step 5</span><span class="sxs-lookup"><span data-stu-id="4577a-155">Step 5</span></span>

<span data-ttu-id="4577a-156">Configure the front-end IP port named **frontendport01** for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="4577a-156">Configure the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01 -Port 80
```

### <a name="step-6"></a><span data-ttu-id="4577a-157">Step 6</span><span class="sxs-lookup"><span data-stu-id="4577a-157">Step 6</span></span>

<span data-ttu-id="4577a-158">Create the front-end IP configuration named **fipconfig01** and associate the public IP address with the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="4577a-158">Create the front-end IP configuration named **fipconfig01** and associate the public IP address with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

### <a name="step-7"></a><span data-ttu-id="4577a-159">Step 7</span><span class="sxs-lookup"><span data-stu-id="4577a-159">Step 7</span></span>

<span data-ttu-id="4577a-160">Create the listener name **listener01** and associate the front-end port to the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="4577a-160">Create the listener name **listener01** and associate the front-end port to the front-end IP configuration.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Http -FrontendIPConfiguration $fipconfig -FrontendPort $fp
```

### <a name="step-8"></a><span data-ttu-id="4577a-161">Step 8</span><span class="sxs-lookup"><span data-stu-id="4577a-161">Step 8</span></span>

<span data-ttu-id="4577a-162">Create the load balancer routing rule named **rule01** that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="4577a-162">Create the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-9"></a><span data-ttu-id="4577a-163">Step 9</span><span class="sxs-lookup"><span data-stu-id="4577a-163">Step 9</span></span>

<span data-ttu-id="4577a-164">Configure the instance size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-164">Configure the instance size of the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> The default value for **InstanceCount** is 2, with a maximum value of 10. The default value for **GatewaySize** is Medium. You can choose between **Standard_Small**, **Standard_Medium**, and **Standard_Large**. 

## <a name="create-an-application-gateway-by-using-new-azurermapplicationgateway"></a><span data-ttu-id="4577a-168">Create an application gateway by using New-AzureRmApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="4577a-168">Create an application gateway by using New-AzureRmApplicationGateway</span></span>

<span data-ttu-id="4577a-169">Create an application gateway with all configuration items from the steps above.</span><span class="sxs-lookup"><span data-stu-id="4577a-169">Create an application gateway with all configuration items from the steps above.</span></span> <span data-ttu-id="4577a-170">In this example, the application gateway is called **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="4577a-170">In this example, the application gateway is called **appgwtest**.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -Probes $probe -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku
```

## <a name="add-a-probe-to-an-existing-application-gateway"></a><span data-ttu-id="4577a-171">Add a probe to an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="4577a-171">Add a probe to an existing application gateway</span></span>

<span data-ttu-id="4577a-172">You have four steps to add a custom probe to an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-172">You have four steps to add a custom probe to an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="4577a-173">Step 1</span><span class="sxs-lookup"><span data-stu-id="4577a-173">Step 1</span></span>

<span data-ttu-id="4577a-174">Load the application gateway resource into a PowerShell variable by using `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4577a-174">Load the application gateway resource into a PowerShell variable by using `Get-AzureRmApplicationGateway`.</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="4577a-175">Step 2</span><span class="sxs-lookup"><span data-stu-id="4577a-175">Step 2</span></span>

<span data-ttu-id="4577a-176">Add a probe to the existing gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="4577a-176">Add a probe to the existing gateway configuration.</span></span>

```powershell
$getgw = Add-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name probe01 -Protocol Http -HostName "contoso.com" -Path "/path/custompath.htm" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

<span data-ttu-id="4577a-177">In the example, the custom probe is configured to check for URL path contoso.com/path/custompath.htm every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="4577a-177">In the example, the custom probe is configured to check for URL path contoso.com/path/custompath.htm every 30 seconds.</span></span> <span data-ttu-id="4577a-178">A time-out threshold of 120 seconds is configured with a maximum number of 8 failed probe requests.</span><span class="sxs-lookup"><span data-stu-id="4577a-178">A time-out threshold of 120 seconds is configured with a maximum number of 8 failed probe requests.</span></span>

### <a name="step-3"></a><span data-ttu-id="4577a-179">Step 3</span><span class="sxs-lookup"><span data-stu-id="4577a-179">Step 3</span></span>

<span data-ttu-id="4577a-180">Add the probe to the back-end pool setting configuration and time-out by using `Set-AzureRmApplicationGatewayBackendHttpSettings`.</span><span class="sxs-lookup"><span data-stu-id="4577a-180">Add the probe to the back-end pool setting configuration and time-out by using `Set-AzureRmApplicationGatewayBackendHttpSettings`.</span></span>

```powershell
    $getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol Http -CookieBasedAffinity Disabled -Probe $probe -RequestTimeout 120
```

### <a name="step-4"></a><span data-ttu-id="4577a-181">Step 4</span><span class="sxs-lookup"><span data-stu-id="4577a-181">Step 4</span></span>

<span data-ttu-id="4577a-182">Save the configuration to the application gateway by using `Set-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4577a-182">Save the configuration to the application gateway by using `Set-AzureRmApplicationGateway`.</span></span>

```powershell
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="remove-a-probe-from-an-existing-application-gateway"></a><span data-ttu-id="4577a-183">Remove a probe from an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="4577a-183">Remove a probe from an existing application gateway</span></span>

<span data-ttu-id="4577a-184">Here are the steps to remove a custom probe from an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-184">Here are the steps to remove a custom probe from an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="4577a-185">Step 1</span><span class="sxs-lookup"><span data-stu-id="4577a-185">Step 1</span></span>

<span data-ttu-id="4577a-186">Load the application gateway resource into a PowerShell variable by using `Get-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4577a-186">Load the application gateway resource into a PowerShell variable by using `Get-AzureRmApplicationGateway`.</span></span>

```powershell
$getgw =  Get-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg
```

### <a name="step-2"></a><span data-ttu-id="4577a-187">Step 2</span><span class="sxs-lookup"><span data-stu-id="4577a-187">Step 2</span></span>

<span data-ttu-id="4577a-188">Remove the probe configuration from the application gateway by using `Remove-AzureRmApplicationGatewayProbeConfig`.</span><span class="sxs-lookup"><span data-stu-id="4577a-188">Remove the probe configuration from the application gateway by using `Remove-AzureRmApplicationGatewayProbeConfig`.</span></span>

```powershell
$getgw = Remove-AzureRmApplicationGatewayProbeConfig -ApplicationGateway $getgw -Name $getgw.Probes.name
```

### <a name="step-3"></a><span data-ttu-id="4577a-189">Step 3</span><span class="sxs-lookup"><span data-stu-id="4577a-189">Step 3</span></span>

<span data-ttu-id="4577a-190">Update the back-end pool setting to remove the probe and time-out setting by using `Set-AzureRmApplicationGatewayBackendHttpSettings`.</span><span class="sxs-lookup"><span data-stu-id="4577a-190">Update the back-end pool setting to remove the probe and time-out setting by using `Set-AzureRmApplicationGatewayBackendHttpSettings`.</span></span>

```powershell
    $getgw = Set-AzureRmApplicationGatewayBackendHttpSettings -ApplicationGateway $getgw -Name $getgw.BackendHttpSettingsCollection.name -Port 80 -Protocol http -CookieBasedAffinity Disabled
```

### <a name="step-4"></a><span data-ttu-id="4577a-191">Step 4</span><span class="sxs-lookup"><span data-stu-id="4577a-191">Step 4</span></span>

<span data-ttu-id="4577a-192">Save the configuration to the application gateway by using `Set-AzureRmApplicationGateway`.</span><span class="sxs-lookup"><span data-stu-id="4577a-192">Save the configuration to the application gateway by using `Set-AzureRmApplicationGateway`.</span></span> 

```powershell
Set-AzureRmApplicationGateway -ApplicationGateway $getgw
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="4577a-193">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="4577a-193">Get application gateway DNS name</span></span>

<span data-ttu-id="4577a-194">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="4577a-194">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="4577a-195">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="4577a-195">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="4577a-196">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-196">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="4577a-197">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4577a-197">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="4577a-198">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-198">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="4577a-199">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="4577a-199">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="4577a-200">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="4577a-200">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4577a-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="4577a-201">Next steps</span></span>

<span data-ttu-id="4577a-202">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span><span class="sxs-lookup"><span data-stu-id="4577a-202">Learn to configure SSL offloading by visiting: [Configure SSL Offload](application-gateway-ssl-arm.md)</span></span>

