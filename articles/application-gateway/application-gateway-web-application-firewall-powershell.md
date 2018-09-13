---
title: Configure web application firewall - Azure Application Gateway | Microsoft Docs
description: This article provides guidance on how to start using web application firewall on an existing or new application gateway.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 670b9732-874b-43e6-843b-d2585c160982
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/22/2017
ms.author: gwallace
ms.openlocfilehash: c222cefdd3e33d26ccba5cfcad9cad21b8a7cebc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550810"
---
# <a name="configure-web-application-firewall-on-a-new-or-existing-application-gateway"></a><span data-ttu-id="a974c-103">Configure web application firewall on a new or existing Application Gateway</span><span class="sxs-lookup"><span data-stu-id="a974c-103">Configure web application firewall on a new or existing Application Gateway</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-web-application-firewall-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-web-application-firewall-powershell.md)

<span data-ttu-id="a974c-106">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span><span class="sxs-lookup"><span data-stu-id="a974c-106">The web application firewall (WAF) in Azure Application Gateway protects web applications from common web-based attacks like SQL injection, cross-site scripting attacks, and session hijacks.</span></span>

<span data-ttu-id="a974c-107">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="a974c-107">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="a974c-108">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="a974c-108">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="a974c-109">Application provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="a974c-109">Application provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="a974c-110">To find a complete list of supported features, visit Application Gateway Overview</span><span class="sxs-lookup"><span data-stu-id="a974c-110">To find a complete list of supported features, visit Application Gateway Overview</span></span>

<span data-ttu-id="a974c-111">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span><span class="sxs-lookup"><span data-stu-id="a974c-111">The following article shows how to [add web application firewall to an existing application gateway](#add-web-application-firewall-to-an-existing-application-gateway) and [create an application gateway that uses web application firewall](#create-an-application-gateway-with-web-application-firewall).</span></span>

![scenario image][scenario]

## <a name="waf-configuration-differences"></a><span data-ttu-id="a974c-113">WAF configuration differences</span><span class="sxs-lookup"><span data-stu-id="a974c-113">WAF configuration differences</span></span>

<span data-ttu-id="a974c-114">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-114">If you have read [Create an Application Gateway with PowerShell](application-gateway-create-gateway-arm.md), you understand the SKU settings to configure when creating an application gateway.</span></span> <span data-ttu-id="a974c-115">WAF provides additional settings to define when configuring the SKU on an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-115">WAF provides additional settings to define when configuring the SKU on an application gateway.</span></span> <span data-ttu-id="a974c-116">There are no additional changes that you make on the application gateway itself.</span><span class="sxs-lookup"><span data-stu-id="a974c-116">There are no additional changes that you make on the application gateway itself.</span></span>

<span data-ttu-id="a974c-117">**SKU** - A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span><span class="sxs-lookup"><span data-stu-id="a974c-117">**SKU** - A normal application gateway without WAF supports **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large** sizes.</span></span> <span data-ttu-id="a974c-118">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span><span class="sxs-lookup"><span data-stu-id="a974c-118">With the introduction of WAF, there are two additional SKUs, **WAF\_Medium** and **WAF\_Large**.</span></span> <span data-ttu-id="a974c-119">WAF is not supported on small application gateways.</span><span class="sxs-lookup"><span data-stu-id="a974c-119">WAF is not supported on small application gateways.</span></span>

<span data-ttu-id="a974c-120">**Tier** - The available values are **Standard** or **WAF**.</span><span class="sxs-lookup"><span data-stu-id="a974c-120">**Tier** - The available values are **Standard** or **WAF**.</span></span> <span data-ttu-id="a974c-121">When using web application firewall, **WAF** must be chosen.</span><span class="sxs-lookup"><span data-stu-id="a974c-121">When using web application firewall, **WAF** must be chosen.</span></span>

<span data-ttu-id="a974c-122">**Mode** - This setting is the mode of WAF.</span><span class="sxs-lookup"><span data-stu-id="a974c-122">**Mode** - This setting is the mode of WAF.</span></span> <span data-ttu-id="a974c-123">allowed values are **Detection** and **Prevention**.</span><span class="sxs-lookup"><span data-stu-id="a974c-123">allowed values are **Detection** and **Prevention**.</span></span> <span data-ttu-id="a974c-124">When WAF is set up in detection mode, all threats are stored in a log file.</span><span class="sxs-lookup"><span data-stu-id="a974c-124">When WAF is set up in detection mode, all threats are stored in a log file.</span></span> <span data-ttu-id="a974c-125">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-125">In prevention mode, events are still logged but the attacker receives a 403 unauthorized response from the application gateway.</span></span>

## <a name="add-web-application-firewall-to-an-existing-application-gateway"></a><span data-ttu-id="a974c-126">Add web application firewall to an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="a974c-126">Add web application firewall to an existing application gateway</span></span>

<span data-ttu-id="a974c-127">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a974c-127">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a974c-128">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a974c-128">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a974c-129">Step 1</span><span class="sxs-lookup"><span data-stu-id="a974c-129">Step 1</span></span>

<span data-ttu-id="a974c-130">Log in to your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="a974c-130">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="a974c-131">Step 2</span><span class="sxs-lookup"><span data-stu-id="a974c-131">Step 2</span></span>

<span data-ttu-id="a974c-132">Select the subscription to use for this scenario.</span><span class="sxs-lookup"><span data-stu-id="a974c-132">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="a974c-133">Step 3</span><span class="sxs-lookup"><span data-stu-id="a974c-133">Step 3</span></span>

<span data-ttu-id="a974c-134">Retrieve the gateway that you are adding web application firewall to.</span><span class="sxs-lookup"><span data-stu-id="a974c-134">Retrieve the gateway that you are adding web application firewall to.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name "AdatumGateway" -ResourceGroupName "MyResourceGroup"
```

### <a name="step-4"></a><span data-ttu-id="a974c-135">Step 4</span><span class="sxs-lookup"><span data-stu-id="a974c-135">Step 4</span></span>

<span data-ttu-id="a974c-136">Configure the web application firewall sku.</span><span class="sxs-lookup"><span data-stu-id="a974c-136">Configure the web application firewall sku.</span></span> <span data-ttu-id="a974c-137">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span><span class="sxs-lookup"><span data-stu-id="a974c-137">The available sizes are **WAF\_Large** and **WAF\_Medium**.</span></span> <span data-ttu-id="a974c-138">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span><span class="sxs-lookup"><span data-stu-id="a974c-138">When web application firewall is used the tier must be **WAF**, the capacity must be confirmed when setting the sku.</span></span>

```powershell
$gw | Set-AzureRmApplicationGatewaySku -Name WAF_Large -Tier WAF -Capacity 2
```

### <a name="step-5"></a><span data-ttu-id="a974c-139">Step 5</span><span class="sxs-lookup"><span data-stu-id="a974c-139">Step 5</span></span>

<span data-ttu-id="a974c-140">Configure the WAF settings as defined in the following example:</span><span class="sxs-lookup"><span data-stu-id="a974c-140">Configure the WAF settings as defined in the following example:</span></span>

<span data-ttu-id="a974c-141">For the **WafMode** setting, the available values are Prevention and Detection.</span><span class="sxs-lookup"><span data-stu-id="a974c-141">For the **WafMode** setting, the available values are Prevention and Detection.</span></span>

```powershell
$gw | Set-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode Prevention
```

### <a name="step-6"></a><span data-ttu-id="a974c-142">Step 6</span><span class="sxs-lookup"><span data-stu-id="a974c-142">Step 6</span></span>

<span data-ttu-id="a974c-143">Update the application gateway with the settings defined in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="a974c-143">Update the application gateway with the settings defined in the preceding step.</span></span>

```powershell
Set-AzureRmApplicationGateway -ApplicationGateway $gw
```

<span data-ttu-id="a974c-144">This command updates the application gateway with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="a974c-144">This command updates the application gateway with web application firewall.</span></span> <span data-ttu-id="a974c-145">It is recommended to view [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-145">It is recommended to view [Application Gateway Diagnostics](application-gateway-diagnostics.md) to understand how to view logs for your application gateway.</span></span> <span data-ttu-id="a974c-146">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span><span class="sxs-lookup"><span data-stu-id="a974c-146">Due to the security nature of WAF, logs need to be reviewed regularly to understand the security posture of your web applications.</span></span>

## <a name="create-an-application-gateway-with-web-application-firewall"></a><span data-ttu-id="a974c-147">Create an Application Gateway with web application firewall</span><span class="sxs-lookup"><span data-stu-id="a974c-147">Create an Application Gateway with web application firewall</span></span>

<span data-ttu-id="a974c-148">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span><span class="sxs-lookup"><span data-stu-id="a974c-148">The following steps take you through the entire process from beginning to end for creating an Application Gateway with web application firewall.</span></span>

<span data-ttu-id="a974c-149">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a974c-149">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="a974c-150">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a974c-150">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="a974c-151">Step 1</span><span class="sxs-lookup"><span data-stu-id="a974c-151">Step 1</span></span>

<span data-ttu-id="a974c-152">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="a974c-152">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="a974c-153">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="a974c-153">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="a974c-154">Step 2</span><span class="sxs-lookup"><span data-stu-id="a974c-154">Step 2</span></span>

<span data-ttu-id="a974c-155">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="a974c-155">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="a974c-156">Step 3</span><span class="sxs-lookup"><span data-stu-id="a974c-156">Step 3</span></span>

<span data-ttu-id="a974c-157">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="a974c-157">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-4"></a><span data-ttu-id="a974c-158">Step 4</span><span class="sxs-lookup"><span data-stu-id="a974c-158">Step 4</span></span>

<span data-ttu-id="a974c-159">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="a974c-159">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="a974c-160">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="a974c-160">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="a974c-161">This location is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="a974c-161">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="a974c-162">Make sure that all commands to create an application gateway uses the same resource group.</span><span class="sxs-lookup"><span data-stu-id="a974c-162">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="a974c-163">In the preceding example, we created a resource group called "appgw-RG" and location "West US".</span><span class="sxs-lookup"><span data-stu-id="a974c-163">In the preceding example, we created a resource group called "appgw-RG" and location "West US".</span></span>

> [!NOTE]
> If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md). Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.

### <a name="step-5"></a><span data-ttu-id="a974c-166">Step 5</span><span class="sxs-lookup"><span data-stu-id="a974c-166">Step 5</span></span>

<span data-ttu-id="a974c-167">Assign an address range for the subnet be used for the Application Gateway itself.</span><span class="sxs-lookup"><span data-stu-id="a974c-167">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> A subnet for an application should have a minimum of 28 mask bits. This value leaves 10 available addresses in the subnet for Application Gateway instances. With a smaller subnet, you may not be able to add more instance of your application gateway in the future.


### <a name="step-6"></a><span data-ttu-id="a974c-171">Step 6</span><span class="sxs-lookup"><span data-stu-id="a974c-171">Step 6</span></span>

<span data-ttu-id="a974c-172">Assign an address range to be used for the Backend address pool.</span><span class="sxs-lookup"><span data-stu-id="a974c-172">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-7"></a><span data-ttu-id="a974c-173">Step 7</span><span class="sxs-lookup"><span data-stu-id="a974c-173">Step 7</span></span>

<span data-ttu-id="a974c-174">Create a virtual network with the preceding subnets in the resource group created in step: [Create the Resource Group](#create-the-resource-group)</span><span class="sxs-lookup"><span data-stu-id="a974c-174">Create a virtual network with the preceding subnets in the resource group created in step: [Create the Resource Group](#create-the-resource-group)</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-8"></a><span data-ttu-id="a974c-175">Step 8</span><span class="sxs-lookup"><span data-stu-id="a974c-175">Step 8</span></span>

<span data-ttu-id="a974c-176">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span><span class="sxs-lookup"><span data-stu-id="a974c-176">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

### <a name="step-9"></a><span data-ttu-id="a974c-177">Step 9</span><span class="sxs-lookup"><span data-stu-id="a974c-177">Step 9</span></span>

<span data-ttu-id="a974c-178">Create a public IP resource to be used for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-178">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="a974c-179">This public IP address is used in one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="a974c-179">This public IP address is used in one of the following steps:</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name 'appgwpip' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Application Gateway does not support the use of a public IP address created with a domain label defined. Only a public IP address with a dynamically created domain label is supported. If you require a friendly dns name for the application gateway, it is recommended to use a cname record as an alias.


### <a name="step-10"></a><span data-ttu-id="a974c-183">Step 10</span><span class="sxs-lookup"><span data-stu-id="a974c-183">Step 10</span></span>

<span data-ttu-id="a974c-184">You must set up all configuration items before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-184">You must set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="a974c-185">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="a974c-185">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

<span data-ttu-id="a974c-186">Create an application gateway IP configuration, this configures what subnet the Application Gateway uses.</span><span class="sxs-lookup"><span data-stu-id="a974c-186">Create an application gateway IP configuration, this configures what subnet the Application Gateway uses.</span></span> <span data-ttu-id="a974c-187">When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="a974c-187">When Application Gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="a974c-188">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="a974c-188">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-11"></a><span data-ttu-id="a974c-189">Step 11</span><span class="sxs-lookup"><span data-stu-id="a974c-189">Step 11</span></span>

<span data-ttu-id="a974c-190">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span><span class="sxs-lookup"><span data-stu-id="a974c-190">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="a974c-191">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="a974c-191">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="a974c-192">You replace the following IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="a974c-192">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

### <a name="step-12"></a><span data-ttu-id="a974c-193">Step 12</span><span class="sxs-lookup"><span data-stu-id="a974c-193">Step 12</span></span>

<span data-ttu-id="a974c-194">Upload the certificate to be used on the ssl enabled backend pool resources.</span><span class="sxs-lookup"><span data-stu-id="a974c-194">Upload the certificate to be used on the ssl enabled backend pool resources.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile <full path to .cer file>
```

### <a name="step-13"></a><span data-ttu-id="a974c-195">Step 13</span><span class="sxs-lookup"><span data-stu-id="a974c-195">Step 13</span></span>

<span data-ttu-id="a974c-196">Configure the application gateway back-end http settings.</span><span class="sxs-lookup"><span data-stu-id="a974c-196">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="a974c-197">Assign the certificate uploaded in the preceding step to the http settings.</span><span class="sxs-lookup"><span data-stu-id="a974c-197">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-14"></a><span data-ttu-id="a974c-198">Step 14</span><span class="sxs-lookup"><span data-stu-id="a974c-198">Step 14</span></span>

<span data-ttu-id="a974c-199">Configure the front-end IP port for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="a974c-199">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="a974c-200">This port is the port that end users connect to.</span><span class="sxs-lookup"><span data-stu-id="a974c-200">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-15"></a><span data-ttu-id="a974c-201">Step 15</span><span class="sxs-lookup"><span data-stu-id="a974c-201">Step 15</span></span>

<span data-ttu-id="a974c-202">Create a front-end IP configuration, this setting maps a private or public ip address to the front-end of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-202">Create a front-end IP configuration, this setting maps a private or public ip address to the front-end of the application gateway.</span></span> <span data-ttu-id="a974c-203">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="a974c-203">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-16"></a><span data-ttu-id="a974c-204">Step 16</span><span class="sxs-lookup"><span data-stu-id="a974c-204">Step 16</span></span>

<span data-ttu-id="a974c-205">Configure the certificate for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-205">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="a974c-206">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-206">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-17"></a><span data-ttu-id="a974c-207">Step 17</span><span class="sxs-lookup"><span data-stu-id="a974c-207">Step 17</span></span>

<span data-ttu-id="a974c-208">Create the HTTP listener for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-208">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="a974c-209">Assign the front-end ip configuration, port, and ssl certificate to use.</span><span class="sxs-lookup"><span data-stu-id="a974c-209">Assign the front-end ip configuration, port, and ssl certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

### <a name="step-18"></a><span data-ttu-id="a974c-210">Step 18</span><span class="sxs-lookup"><span data-stu-id="a974c-210">Step 18</span></span>

<span data-ttu-id="a974c-211">Create a load balancer routing rule that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="a974c-211">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="a974c-212">In this example, a basic round robin rule is created.</span><span class="sxs-lookup"><span data-stu-id="a974c-212">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-19"></a><span data-ttu-id="a974c-213">Step 19</span><span class="sxs-lookup"><span data-stu-id="a974c-213">Step 19</span></span>

<span data-ttu-id="a974c-214">Configure the instance size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-214">Configure the instance size of the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name WAF_Medium -Tier WAF -Capacity 2
```

> [!NOTE]
> You can choose between **WAF\_Medium** and **WAF\_Large**, the tier when using WAF is always **WAF**. Capacity is any number between 1 and 10.

### <a name="step-20"></a><span data-ttu-id="a974c-217">Step 20</span><span class="sxs-lookup"><span data-stu-id="a974c-217">Step 20</span></span>

<span data-ttu-id="a974c-218">Configure the mode for WAF, acceptable values are **Prevention** and **Detection**.</span><span class="sxs-lookup"><span data-stu-id="a974c-218">Configure the mode for WAF, acceptable values are **Prevention** and **Detection**.</span></span>

```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

### <a name="step-21"></a><span data-ttu-id="a974c-219">Step 21</span><span class="sxs-lookup"><span data-stu-id="a974c-219">Step 21</span></span>

<span data-ttu-id="a974c-220">Create an application gateway with all configuration items from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="a974c-220">Create an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="a974c-221">In this example, the application gateway is called "appgwtest".</span><span class="sxs-lookup"><span data-stu-id="a974c-221">In this example, the application gateway is called "appgwtest".</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert
```

> [!NOTE]
> Application gateways created with the basic web application firewall configuration are configured with CRS 3.0 for protections.

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="a974c-223">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="a974c-223">Get application gateway DNS name</span></span>

<span data-ttu-id="a974c-224">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="a974c-224">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="a974c-225">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="a974c-225">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="a974c-226">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-226">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="a974c-227">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a974c-227">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="a974c-228">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-228">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="a974c-229">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="a974c-229">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="a974c-230">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="a974c-230">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a974c-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="a974c-231">Next steps</span></span>

<span data-ttu-id="a974c-232">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="a974c-232">Learn how to configure diagnostic logging, to log the events that are detected or prevented with web application firewall by visiting [Application Gateway Diagnostics](application-gateway-diagnostics.md)</span></span>

[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-web-application-firewall-powershell/scenario.png

