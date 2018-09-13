---
title: Configure SSL offload - Azure Application Gateway - PowerShell | Microsoft Docs
description: This page provides instructions to create an application gateway with SSL offload by using Azure Resource Manager
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 3c3681e0-f928-4682-9d97-567f8e278e13
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 2982cf9154780166f1363ae6380702299c717236
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550796"
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-azure-resource-manager"></a><span data-ttu-id="268b8-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="268b8-103">Configure an application gateway for SSL offload by using Azure Resource Manager</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)

<span data-ttu-id="268b8-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span><span class="sxs-lookup"><span data-stu-id="268b8-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="268b8-108">SSL offload also simplifies the front-end server setup and management of the web application.</span><span class="sxs-lookup"><span data-stu-id="268b8-108">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="268b8-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="268b8-109">Before you begin</span></span>

1. <span data-ttu-id="268b8-110">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="268b8-110">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="268b8-111">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="268b8-111">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="268b8-112">You create a virtual network and a subnet for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-112">You create a virtual network and a subnet for the application gateway.</span></span> <span data-ttu-id="268b8-113">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="268b8-113">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="268b8-114">Application Gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="268b8-114">Application Gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="268b8-115">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="268b8-115">The servers you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="268b8-116">What is required to create an application gateway?</span><span class="sxs-lookup"><span data-stu-id="268b8-116">What is required to create an application gateway?</span></span>

* <span data-ttu-id="268b8-117">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="268b8-117">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="268b8-118">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="268b8-118">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="268b8-119">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="268b8-119">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="268b8-120">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="268b8-120">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="268b8-121">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-121">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="268b8-122">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="268b8-122">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="268b8-123">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="268b8-123">**Listener:** The listener has a front-end port, a protocol (Http or Https, these settings are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="268b8-124">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="268b8-124">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="268b8-125">Currently, only the *basic* rule is supported.</span><span class="sxs-lookup"><span data-stu-id="268b8-125">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="268b8-126">The *basic* rule is round-robin load distribution.</span><span class="sxs-lookup"><span data-stu-id="268b8-126">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="268b8-127">**Additional configuration notes**</span><span class="sxs-lookup"><span data-stu-id="268b8-127">**Additional configuration notes**</span></span>

<span data-ttu-id="268b8-128">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span><span class="sxs-lookup"><span data-stu-id="268b8-128">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="268b8-129">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="268b8-129">The **SslCertificate** element is added to **HttpListener** with the variable value configured for the SSL certificate.</span></span> <span data-ttu-id="268b8-130">The front-end port should be updated to 443.</span><span class="sxs-lookup"><span data-stu-id="268b8-130">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="268b8-131">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span><span class="sxs-lookup"><span data-stu-id="268b8-131">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="268b8-132">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span><span class="sxs-lookup"><span data-stu-id="268b8-132">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="268b8-133">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span><span class="sxs-lookup"><span data-stu-id="268b8-133">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="268b8-134">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="268b8-134">Create an application gateway</span></span>

<span data-ttu-id="268b8-135">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span><span class="sxs-lookup"><span data-stu-id="268b8-135">The difference between using the Azure Classic deployment model and Azure Resource Manager is the order that you create an application gateway and the items that need to be configured.</span></span>

<span data-ttu-id="268b8-136">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="268b8-136">With Resource Manager, all components of an application gateway are configured individually and then put together to create an application gateway resource.</span></span>

<span data-ttu-id="268b8-137">Here are the steps needed to create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="268b8-137">Here are the steps needed to create an application gateway:</span></span>

1. <span data-ttu-id="268b8-138">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="268b8-138">Create a resource group for Resource Manager</span></span>
2. <span data-ttu-id="268b8-139">Create virtual network, subnet, and public IP for the application gateway</span><span class="sxs-lookup"><span data-stu-id="268b8-139">Create virtual network, subnet, and public IP for the application gateway</span></span>
3. <span data-ttu-id="268b8-140">Create an application gateway configuration object</span><span class="sxs-lookup"><span data-stu-id="268b8-140">Create an application gateway configuration object</span></span>
4. <span data-ttu-id="268b8-141">Create an application gateway resource</span><span class="sxs-lookup"><span data-stu-id="268b8-141">Create an application gateway resource</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="268b8-142">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="268b8-142">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="268b8-143">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="268b8-143">Make sure that you switch PowerShell mode to use the Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="268b8-144">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="268b8-144">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="268b8-145">Step 1</span><span class="sxs-lookup"><span data-stu-id="268b8-145">Step 1</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="268b8-146">Step 2</span><span class="sxs-lookup"><span data-stu-id="268b8-146">Step 2</span></span>

<span data-ttu-id="268b8-147">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="268b8-147">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="268b8-148">You are prompted to authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="268b8-148">You are prompted to authenticate with your credentials.</span></span>

### <a name="step-3"></a><span data-ttu-id="268b8-149">Step 3</span><span class="sxs-lookup"><span data-stu-id="268b8-149">Step 3</span></span>

<span data-ttu-id="268b8-150">Choose which of your Azure subscriptions to use.</span><span class="sxs-lookup"><span data-stu-id="268b8-150">Choose which of your Azure subscriptions to use.</span></span>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a><span data-ttu-id="268b8-151">Step 4</span><span class="sxs-lookup"><span data-stu-id="268b8-151">Step 4</span></span>

<span data-ttu-id="268b8-152">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="268b8-152">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

<span data-ttu-id="268b8-153">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="268b8-153">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="268b8-154">This setting is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="268b8-154">This setting is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="268b8-155">Make sure that all commands to create an application gateway uses the same resource group.</span><span class="sxs-lookup"><span data-stu-id="268b8-155">Make sure that all commands to create an application gateway uses the same resource group.</span></span>

<span data-ttu-id="268b8-156">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span><span class="sxs-lookup"><span data-stu-id="268b8-156">In the example above, we created a resource group called **appgw-RG** and location **West US**.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="268b8-157">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="268b8-157">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="268b8-158">The following example shows how to create a virtual network by using Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="268b8-158">The following example shows how to create a virtual network by using Resource Manager:</span></span>

### <a name="step-1"></a><span data-ttu-id="268b8-159">Step 1</span><span class="sxs-lookup"><span data-stu-id="268b8-159">Step 1</span></span>

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

<span data-ttu-id="268b8-160">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span><span class="sxs-lookup"><span data-stu-id="268b8-160">This sample assigns the address range 10.0.0.0/24 to a subnet variable to be used to create a virtual network.</span></span>

### <a name="step-2"></a><span data-ttu-id="268b8-161">Step 2</span><span class="sxs-lookup"><span data-stu-id="268b8-161">Step 2</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

<span data-ttu-id="268b8-162">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span><span class="sxs-lookup"><span data-stu-id="268b8-162">This sample creates a virtual network named **appgwvnet** in resource group **appgw-rg** for the West US region using the prefix 10.0.0.0/16 with subnet 10.0.0.0/24.</span></span>

### <a name="step-3"></a><span data-ttu-id="268b8-163">Step 3</span><span class="sxs-lookup"><span data-stu-id="268b8-163">Step 3</span></span>

```powershell
$subnet = $vnet.Subnets[0]
```

<span data-ttu-id="268b8-164">This sample assigns the subnet object to variable $subnet for the next steps.</span><span class="sxs-lookup"><span data-stu-id="268b8-164">This sample assigns the subnet object to variable $subnet for the next steps.</span></span>

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="268b8-165">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="268b8-165">Create a public IP address for the front-end configuration</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="268b8-166">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="268b8-166">This sample creates a public IP resource **publicIP01** in resource group **appgw-rg** for the West US region.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="268b8-167">Create an application gateway configuration object</span><span class="sxs-lookup"><span data-stu-id="268b8-167">Create an application gateway configuration object</span></span>

### <a name="step-1"></a><span data-ttu-id="268b8-168">Step 1</span><span class="sxs-lookup"><span data-stu-id="268b8-168">Step 1</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

<span data-ttu-id="268b8-169">This sample creates an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="268b8-169">This sample creates an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="268b8-170">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="268b8-170">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="268b8-171">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="268b8-171">Keep in mind that each instance takes one IP address.</span></span>

### <a name="step-2"></a><span data-ttu-id="268b8-172">Step 2</span><span class="sxs-lookup"><span data-stu-id="268b8-172">Step 2</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50
```

<span data-ttu-id="268b8-173">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span><span class="sxs-lookup"><span data-stu-id="268b8-173">This sample configures the back-end IP address pool named **pool01** with IP addresses **134.170.185.46**, **134.170.188.221**, **134.170.185.50**.</span></span> <span data-ttu-id="268b8-174">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="268b8-174">Those values are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="268b8-175">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span><span class="sxs-lookup"><span data-stu-id="268b8-175">Replace the IP addresses from the preceding example with the IP addresses of your web application endpoints.</span></span>

### <a name="step-3"></a><span data-ttu-id="268b8-176">Step 3</span><span class="sxs-lookup"><span data-stu-id="268b8-176">Step 3</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled
```

<span data-ttu-id="268b8-177">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span><span class="sxs-lookup"><span data-stu-id="268b8-177">This sample configures application gateway setting **poolsetting01** to load-balanced network traffic in the back-end pool.</span></span>

### <a name="step-4"></a><span data-ttu-id="268b8-178">Step 4</span><span class="sxs-lookup"><span data-stu-id="268b8-178">Step 4</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443
```

<span data-ttu-id="268b8-179">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="268b8-179">This sample configures the front-end IP port named **frontendport01** for the public IP endpoint.</span></span>

### <a name="step-5"></a><span data-ttu-id="268b8-180">Step 5</span><span class="sxs-lookup"><span data-stu-id="268b8-180">Step 5</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path for certificate file> -Password "<password>"
```

<span data-ttu-id="268b8-181">This sample configures the certificate used for SSL connection.</span><span class="sxs-lookup"><span data-stu-id="268b8-181">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="268b8-182">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span><span class="sxs-lookup"><span data-stu-id="268b8-182">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="268b8-183">Step 6</span><span class="sxs-lookup"><span data-stu-id="268b8-183">Step 6</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip
```

<span data-ttu-id="268b8-184">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="268b8-184">This sample creates the front-end IP configuration named **fipconfig01** and associates the public IP address with the front-end IP configuration.</span></span>

### <a name="step-7"></a><span data-ttu-id="268b8-185">Step 7</span><span class="sxs-lookup"><span data-stu-id="268b8-185">Step 7</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

<span data-ttu-id="268b8-186">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span><span class="sxs-lookup"><span data-stu-id="268b8-186">This sample creates the listener name **listener01** and associates the front-end port to the front-end IP configuration and certificate.</span></span>

### <a name="step-8"></a><span data-ttu-id="268b8-187">Step 8</span><span class="sxs-lookup"><span data-stu-id="268b8-187">Step 8</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

<span data-ttu-id="268b8-188">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="268b8-188">This sample creates the load balancer routing rule named **rule01** that configures the load balancer behavior.</span></span>

### <a name="step-9"></a><span data-ttu-id="268b8-189">Step 9</span><span class="sxs-lookup"><span data-stu-id="268b8-189">Step 9</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

<span data-ttu-id="268b8-190">This sample configures the instance size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-190">This sample configures the instance size of the application gateway.</span></span>

> [!NOTE]
> The default value for *InstanceCount* is 2, with a maximum value of 10. The default value for *GatewaySize* is Medium. You can choose between Standard_Small, Standard_Medium, and Standard_Large.

## <a name="create-an-application-gateway-by-using-new-azureapplicationgateway"></a><span data-ttu-id="268b8-194">Create an application gateway by using New-AzureApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="268b8-194">Create an application gateway by using New-AzureApplicationGateway</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-rg -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert
```

<span data-ttu-id="268b8-195">This sample creates an application gateway with all configuration items from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="268b8-195">This sample creates an application gateway with all configuration items from the preceding steps.</span></span> <span data-ttu-id="268b8-196">In the example, the application gateway is called **appgwtest**.</span><span class="sxs-lookup"><span data-stu-id="268b8-196">In the example, the application gateway is called **appgwtest**.</span></span>

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="268b8-197">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="268b8-197">Get application gateway DNS name</span></span>

<span data-ttu-id="268b8-198">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="268b8-198">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="268b8-199">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="268b8-199">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="268b8-200">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-200">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="268b8-201">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="268b8-201">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="268b8-202">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-202">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="268b8-203">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="268b8-203">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="268b8-204">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="268b8-204">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>


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

## <a name="next-steps"></a><span data-ttu-id="268b8-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="268b8-205">Next steps</span></span>

<span data-ttu-id="268b8-206">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="268b8-206">If you want to configure an application gateway to use with an internal load balancer (ILB), see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="268b8-207">If you want more information about load balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="268b8-207">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="268b8-208">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="268b8-208">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="268b8-209">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="268b8-209">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

