---
title: Create an application gateway for hosting multiple sites | Microsoft Docs
description: This page provides instructions to create, configure an Azure application gateway for hosting multiple web applications on the same gateway.
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: 21ed9a2e86e4effbc396de675d3e8f6ca491777a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552376"
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a><span data-ttu-id="cd14d-103">Create an application gateway for hosting multiple web applications</span><span class="sxs-lookup"><span data-stu-id="cd14d-103">Create an application gateway for hosting multiple web applications</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-multisite-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-multisite-azureresourcemanager-powershell.md)

<span data-ttu-id="cd14d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-106">Multiple site hosting allows you to deploy more than one web application on the same application gateway.</span></span> <span data-ttu-id="cd14d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span><span class="sxs-lookup"><span data-stu-id="cd14d-107">It relies on presence of host header in the incoming HTTP request, to determine which listener would receive traffic.</span></span> <span data-ttu-id="cd14d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-108">The listener then directs traffic to appropriate backend pool as configured in the rules definition of the gateway.</span></span> <span data-ttu-id="cd14d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span><span class="sxs-lookup"><span data-stu-id="cd14d-109">In SSL enabled web applications, application gateway relies on the Server Name Indication (SNI) extension to choose the correct listener for the web traffic.</span></span> <span data-ttu-id="cd14d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span><span class="sxs-lookup"><span data-stu-id="cd14d-110">A common use for multiple site hosting is to load balance requests for different web domains to different back-end server pools.</span></span> <span data-ttu-id="cd14d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-111">Similarly multiple subdomains of the same root domain could also be hosted on the same application gateway.</span></span>

## <a name="scenario"></a><span data-ttu-id="cd14d-112">Scenario</span><span class="sxs-lookup"><span data-stu-id="cd14d-112">Scenario</span></span>

<span data-ttu-id="cd14d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span><span class="sxs-lookup"><span data-stu-id="cd14d-113">In the following example, application gateway is serving traffic for contoso.com and fabrikam.com with two back-end server pools: contoso server pool and fabrikam server pool.</span></span> <span data-ttu-id="cd14d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="cd14d-114">Similar setup could be used to host subdomains like app.contoso.com and blog.contoso.com.</span></span>

![imageURLroute](https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a><span data-ttu-id="cd14d-116">Before you begin</span><span class="sxs-lookup"><span data-stu-id="cd14d-116">Before you begin</span></span>

1. <span data-ttu-id="cd14d-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="cd14d-117">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="cd14d-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cd14d-118">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="cd14d-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="cd14d-119">The servers added to the back-end pool to use the application gateway must exist or have their endpoints created either in the virtual network in a separate subnet or with a public IP/VIP assigned.</span></span>

## <a name="requirements"></a><span data-ttu-id="cd14d-120">Requirements</span><span class="sxs-lookup"><span data-stu-id="cd14d-120">Requirements</span></span>

* <span data-ttu-id="cd14d-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="cd14d-121">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="cd14d-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="cd14d-122">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span> <span data-ttu-id="cd14d-123">FQDN can also be used.</span><span class="sxs-lookup"><span data-stu-id="cd14d-123">FQDN can also be used.</span></span>
* <span data-ttu-id="cd14d-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="cd14d-124">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="cd14d-125">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="cd14d-125">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="cd14d-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-126">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="cd14d-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="cd14d-127">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="cd14d-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="cd14d-128">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> <span data-ttu-id="cd14d-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span><span class="sxs-lookup"><span data-stu-id="cd14d-129">For multi-site enabled application gateways, host name and SNI indicators are also added.</span></span>
* <span data-ttu-id="cd14d-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="cd14d-130">**Rule:** The rule binds the listener, the back-end server pool, and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="cd14d-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span><span class="sxs-lookup"><span data-stu-id="cd14d-131">Rules are processed in the order they are listed, and traffic will be directed via the first rule that matches regardless of specificity.</span></span> <span data-ttu-id="cd14d-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span><span class="sxs-lookup"><span data-stu-id="cd14d-132">For example, if you have a rule using a basic listener and a rule using a multi-site listener both on the same port, the rule with the multi-site listener must be listed before the rule with the basic listener in order for the multi-site rule to function as expected.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="cd14d-133">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="cd14d-133">Create an application gateway</span></span>

<span data-ttu-id="cd14d-134">The following are the steps needed to create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="cd14d-134">The following are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="cd14d-135">Create a resource group for Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd14d-135">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="cd14d-136">Create a virtual network, subnets, and public IP for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-136">Create a virtual network, subnets, and public IP for the application gateway.</span></span>
3. <span data-ttu-id="cd14d-137">Create an application gateway configuration object.</span><span class="sxs-lookup"><span data-stu-id="cd14d-137">Create an application gateway configuration object.</span></span>
4. <span data-ttu-id="cd14d-138">Create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="cd14d-138">Create an application gateway resource.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="cd14d-139">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cd14d-139">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="cd14d-140">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cd14d-140">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="cd14d-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="cd14d-141">More information is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="cd14d-142">Step 1</span><span class="sxs-lookup"><span data-stu-id="cd14d-142">Step 1</span></span>

<span data-ttu-id="cd14d-143">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="cd14d-143">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="cd14d-144">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="cd14d-144">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="cd14d-145">Step 2</span><span class="sxs-lookup"><span data-stu-id="cd14d-145">Step 2</span></span>

<span data-ttu-id="cd14d-146">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="cd14d-146">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="cd14d-147">Step 3</span><span class="sxs-lookup"><span data-stu-id="cd14d-147">Step 3</span></span>

<span data-ttu-id="cd14d-148">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="cd14d-148">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="cd14d-149">Step 4</span><span class="sxs-lookup"><span data-stu-id="cd14d-149">Step 4</span></span>

<span data-ttu-id="cd14d-150">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="cd14d-150">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

<span data-ttu-id="cd14d-151">Alternatively you can also create tags for a resource group for application gateway:</span><span class="sxs-lookup"><span data-stu-id="cd14d-151">Alternatively you can also create tags for a resource group for application gateway:</span></span>

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

<span data-ttu-id="cd14d-152">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="cd14d-152">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="cd14d-153">This location is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="cd14d-153">This location is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="cd14d-154">Make sure that all commands to create an application gateway use the same resource group.</span><span class="sxs-lookup"><span data-stu-id="cd14d-154">Make sure that all commands to create an application gateway use the same resource group.</span></span>

<span data-ttu-id="cd14d-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span><span class="sxs-lookup"><span data-stu-id="cd14d-155">In the example above, we created a resource group called **appgw-RG** with a location of **West US**.</span></span>

> [!NOTE]
> If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-ps.md). Visit [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.

## <a name="create-a-virtual-network-and-subnets"></a><span data-ttu-id="cd14d-158">Create a virtual network and subnets</span><span class="sxs-lookup"><span data-stu-id="cd14d-158">Create a virtual network and subnets</span></span>

<span data-ttu-id="cd14d-159">The following example shows how to create a virtual network by using Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cd14d-159">The following example shows how to create a virtual network by using Resource Manager.</span></span> <span data-ttu-id="cd14d-160">Two subnets are created in this step.</span><span class="sxs-lookup"><span data-stu-id="cd14d-160">Two subnets are created in this step.</span></span> <span data-ttu-id="cd14d-161">The first subnet is for the application gateway itself.</span><span class="sxs-lookup"><span data-stu-id="cd14d-161">The first subnet is for the application gateway itself.</span></span> <span data-ttu-id="cd14d-162">Application gateway requires its own subnet to hold its instances.</span><span class="sxs-lookup"><span data-stu-id="cd14d-162">Application gateway requires its own subnet to hold its instances.</span></span> <span data-ttu-id="cd14d-163">Only other application gateways can be deployed in that subnet.</span><span class="sxs-lookup"><span data-stu-id="cd14d-163">Only other application gateways can be deployed in that subnet.</span></span> <span data-ttu-id="cd14d-164">The second subnet is used to hold the application backend servers.</span><span class="sxs-lookup"><span data-stu-id="cd14d-164">The second subnet is used to hold the application backend servers.</span></span>

### <a name="step-1"></a><span data-ttu-id="cd14d-165">Step 1</span><span class="sxs-lookup"><span data-stu-id="cd14d-165">Step 1</span></span>

<span data-ttu-id="cd14d-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-166">Assign the address range 10.0.0.0/24 to the subnet variable to be used to hold the application gateway.</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a><span data-ttu-id="cd14d-167">Step 2</span><span class="sxs-lookup"><span data-stu-id="cd14d-167">Step 2</span></span>

<span data-ttu-id="cd14d-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span><span class="sxs-lookup"><span data-stu-id="cd14d-168">Assign the address range 10.0.1.0/24 to the subnet2 variable to be used for the backend pools.</span></span>

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a><span data-ttu-id="cd14d-169">Step 3</span><span class="sxs-lookup"><span data-stu-id="cd14d-169">Step 3</span></span>

<span data-ttu-id="cd14d-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="cd14d-170">Create a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24, and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a><span data-ttu-id="cd14d-171">Step 4</span><span class="sxs-lookup"><span data-stu-id="cd14d-171">Step 4</span></span>

<span data-ttu-id="cd14d-172">Assign a subnet variable for the next steps, which creates an application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-172">Assign a subnet variable for the next steps, which creates an application gateway.</span></span>

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="cd14d-173">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="cd14d-173">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="cd14d-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="cd14d-174">Create a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="cd14d-175">An IP address is assigned to the application gateway when the service starts.</span><span class="sxs-lookup"><span data-stu-id="cd14d-175">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="cd14d-176">Create application gateway configuration</span><span class="sxs-lookup"><span data-stu-id="cd14d-176">Create application gateway configuration</span></span>

<span data-ttu-id="cd14d-177">You have to set up all configuration items before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-177">You have to set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="cd14d-178">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="cd14d-178">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="cd14d-179">Step 1</span><span class="sxs-lookup"><span data-stu-id="cd14d-179">Step 1</span></span>

<span data-ttu-id="cd14d-180">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="cd14d-180">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="cd14d-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="cd14d-181">When application gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="cd14d-182">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="cd14d-182">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a><span data-ttu-id="cd14d-183">Step 2</span><span class="sxs-lookup"><span data-stu-id="cd14d-183">Step 2</span></span>

<span data-ttu-id="cd14d-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span><span class="sxs-lookup"><span data-stu-id="cd14d-184">Configure the back-end IP address pool named **pool01** and **pool2** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50** for **pool1** and **134.170.186.46**, **134.170.189.221**, **134.170.186.50** for **pool2**.</span></span>

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

<span data-ttu-id="cd14d-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span><span class="sxs-lookup"><span data-stu-id="cd14d-185">In this example, there are two back-end pools to route network traffic based on the requested site.</span></span> <span data-ttu-id="cd14d-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span><span class="sxs-lookup"><span data-stu-id="cd14d-186">One pool receives traffic from site "contoso.com" and other pool receives traffic from site "fabrikam.com".</span></span> <span data-ttu-id="cd14d-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="cd14d-187">You have to replace the preceding IP addresses to add your own application IP address endpoints.</span></span> <span data-ttu-id="cd14d-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span><span class="sxs-lookup"><span data-stu-id="cd14d-188">In place of internal IP addresses, you could also use public IP addresses, FQDN, or a VM's NIC for backend instances.</span></span> <span data-ttu-id="cd14d-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span><span class="sxs-lookup"><span data-stu-id="cd14d-189">To specify FQDNs instead of IPs in PowerShell use "-BackendFQDNs" parameter.</span></span>

### <a name="step-3"></a><span data-ttu-id="cd14d-190">Step 3</span><span class="sxs-lookup"><span data-stu-id="cd14d-190">Step 3</span></span>

<span data-ttu-id="cd14d-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="cd14d-191">Configure application gateway setting **poolsetting01** and **poolsetting02** for the load-balanced network traffic in the back-end pool.</span></span> <span data-ttu-id="cd14d-192">In this example, you configure different back-end pool settings for the back-end pools.</span><span class="sxs-lookup"><span data-stu-id="cd14d-192">In this example, you configure different back-end pool settings for the back-end pools.</span></span> <span data-ttu-id="cd14d-193">Each back-end pool can have its own back-end pool setting.</span><span class="sxs-lookup"><span data-stu-id="cd14d-193">Each back-end pool can have its own back-end pool setting.</span></span>

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a><span data-ttu-id="cd14d-194">Step 4</span><span class="sxs-lookup"><span data-stu-id="cd14d-194">Step 4</span></span>

<span data-ttu-id="cd14d-195">Configure the front-end IP with public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="cd14d-195">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a><span data-ttu-id="cd14d-196">Step 5</span><span class="sxs-lookup"><span data-stu-id="cd14d-196">Step 5</span></span>

<span data-ttu-id="cd14d-197">Configure the front-end port for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-197">Configure the front-end port for an application gateway.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a><span data-ttu-id="cd14d-198">Step 6</span><span class="sxs-lookup"><span data-stu-id="cd14d-198">Step 6</span></span>

<span data-ttu-id="cd14d-199">Configure two SSL certificates for the two websites we are going to support in this example.</span><span class="sxs-lookup"><span data-stu-id="cd14d-199">Configure two SSL certificates for the two websites we are going to support in this example.</span></span> <span data-ttu-id="cd14d-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span><span class="sxs-lookup"><span data-stu-id="cd14d-200">One certificate is for contoso.com traffic and the other is for fabrikam.com traffic.</span></span> <span data-ttu-id="cd14d-201">These certificates should be a Certificate Authority issued certificates for your websites.</span><span class="sxs-lookup"><span data-stu-id="cd14d-201">These certificates should be a Certificate Authority issued certificates for your websites.</span></span> <span data-ttu-id="cd14d-202">Self-signed certificates are supported but not recommended for production traffic.</span><span class="sxs-lookup"><span data-stu-id="cd14d-202">Self-signed certificates are supported but not recommended for production traffic.</span></span>

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a><span data-ttu-id="cd14d-203">Step 7</span><span class="sxs-lookup"><span data-stu-id="cd14d-203">Step 7</span></span>

<span data-ttu-id="cd14d-204">Configure two listeners for the two web sites in this example.</span><span class="sxs-lookup"><span data-stu-id="cd14d-204">Configure two listeners for the two web sites in this example.</span></span> <span data-ttu-id="cd14d-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="cd14d-205">This step configures the listeners for public IP address, port, and host used to receive incoming traffic.</span></span> <span data-ttu-id="cd14d-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span><span class="sxs-lookup"><span data-stu-id="cd14d-206">HostName parameter is required for multiple site support and should be set to the appropriate website for which the traffic is received.</span></span> <span data-ttu-id="cd14d-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span><span class="sxs-lookup"><span data-stu-id="cd14d-207">RequireServerNameIndication parameter should be set to true for websites that need support for SSL in a multiple host scenario.</span></span> <span data-ttu-id="cd14d-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span><span class="sxs-lookup"><span data-stu-id="cd14d-208">If SSL support is required, you also need to specify the SSL certificate that is used to secure traffic for that web application.</span></span> <span data-ttu-id="cd14d-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span><span class="sxs-lookup"><span data-stu-id="cd14d-209">The combination of FrontendIPConfiguration, FrontendPort, and HostName must be unique to a listener.</span></span> <span data-ttu-id="cd14d-210">Each listener can support one certificate.</span><span class="sxs-lookup"><span data-stu-id="cd14d-210">Each listener can support one certificate.</span></span>

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a><span data-ttu-id="cd14d-211">Step 8</span><span class="sxs-lookup"><span data-stu-id="cd14d-211">Step 8</span></span>

<span data-ttu-id="cd14d-212">Create two rule setting for the two web applications in this example.</span><span class="sxs-lookup"><span data-stu-id="cd14d-212">Create two rule setting for the two web applications in this example.</span></span> <span data-ttu-id="cd14d-213">A rule ties together listeners, backend pools and http settings.</span><span class="sxs-lookup"><span data-stu-id="cd14d-213">A rule ties together listeners, backend pools and http settings.</span></span> <span data-ttu-id="cd14d-214">This step configures the application gateway to use Basic routing rule, one for each website.</span><span class="sxs-lookup"><span data-stu-id="cd14d-214">This step configures the application gateway to use Basic routing rule, one for each website.</span></span> <span data-ttu-id="cd14d-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span><span class="sxs-lookup"><span data-stu-id="cd14d-215">Traffic to each website is received by its configured listener, and is then directed to its configured backend pool, using the properties specified in the BackendHttpSettings.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a><span data-ttu-id="cd14d-216">Step 9</span><span class="sxs-lookup"><span data-stu-id="cd14d-216">Step 9</span></span>

<span data-ttu-id="cd14d-217">Configure the number of instances and size for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-217">Configure the number of instances and size for the application gateway.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a><span data-ttu-id="cd14d-218">Create application gateway</span><span class="sxs-lookup"><span data-stu-id="cd14d-218">Create application gateway</span></span>

<span data-ttu-id="cd14d-219">Create an application gateway with all configuration objects from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="cd14d-219">Create an application gateway with all configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Application Gateway provisioning is a long running operation and may take some time to complete.
> 
> 

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cd14d-221">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="cd14d-221">Get application gateway DNS name</span></span>

<span data-ttu-id="cd14d-222">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="cd14d-222">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="cd14d-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="cd14d-223">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cd14d-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-224">To ensure end users can hit the application gateway, a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="cd14d-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cd14d-225">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="cd14d-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-226">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="cd14d-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="cd14d-227">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="cd14d-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="cd14d-228">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cd14d-229">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd14d-229">Next steps</span></span>

<span data-ttu-id="cd14d-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cd14d-230">Learn how to protect your websites with [Application Gateway - Web Application Firewall](application-gateway-webapplicationfirewall-overview.md)</span></span>


