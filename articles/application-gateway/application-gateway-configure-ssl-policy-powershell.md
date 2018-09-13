---
title: Configure SSL policy on Azure Application Gateway - PowerShell
description: This page provides instructions to configure SSL Policy on Azure Application Gateway
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 3/27/2018
ms.author: victorh
ms.openlocfilehash: 4c9ca5cee14603fb39115defc574aa7e956886ba
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865323"
---
# <a name="configure-ssl-policy-versions-and-cipher-suites-on-application-gateway"></a><span data-ttu-id="3bf53-103">Configure SSL policy versions and cipher suites on Application Gateway</span><span class="sxs-lookup"><span data-stu-id="3bf53-103">Configure SSL policy versions and cipher suites on Application Gateway</span></span>

<span data-ttu-id="3bf53-104">Learn how to configure SSL policy versions and cipher suites on Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-104">Learn how to configure SSL policy versions and cipher suites on Application Gateway.</span></span> <span data-ttu-id="3bf53-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span><span class="sxs-lookup"><span data-stu-id="3bf53-105">You can select from a [list of predefined policies](#predefined-ssl-policies) that contain different configurations of SSL policy versions and enabled cipher suites.</span></span> <span data-ttu-id="3bf53-106">You also have the ability to define a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="3bf53-106">You also have the ability to define a [custom SSL policy](#configure-a-custom-ssl-policy) based on your requirements.</span></span>

## <a name="get-available-ssl-options"></a><span data-ttu-id="3bf53-107">Get available SSL options</span><span class="sxs-lookup"><span data-stu-id="3bf53-107">Get available SSL options</span></span>

<span data-ttu-id="3bf53-108">The `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span><span class="sxs-lookup"><span data-stu-id="3bf53-108">The `Get-AzureRMApplicationGatewayAvailableSslOptions` cmdlet provides a listing of available pre-defined policies, available cipher suites, and protocol versions that can be configured.</span></span> <span data-ttu-id="3bf53-109">The following example shows an example output from running the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3bf53-109">The following example shows an example output from running the cmdlet.</span></span>

```
DefaultPolicy: AppGwSslPolicy20150501
PredefinedPolicies:
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20150501
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401
    /subscriptions/147a22e9-2356-4e56-b3de-1f5842ae4a3b/resourceGroups//providers/Microsoft.Network/ApplicationGatewayAvailableSslOptions/default/Applic
ationGatewaySslPredefinedPolicy/AppGwSslPolicy20170401S

AvailableCipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
    TLS_RSA_WITH_AES_128_GCM_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA256
    TLS_RSA_WITH_AES_128_CBC_SHA256
    TLS_RSA_WITH_AES_256_CBC_SHA
    TLS_RSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
    TLS_DHE_DSS_WITH_AES_256_CBC_SHA
    TLS_DHE_DSS_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_3DES_EDE_CBC_SHA
    TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

AvailableProtocols:
    TLSv1_0
    TLSv1_1
    TLSv1_2
```

## <a name="list-pre-defined-ssl-policies"></a><span data-ttu-id="3bf53-110">List pre-defined SSL Policies</span><span class="sxs-lookup"><span data-stu-id="3bf53-110">List pre-defined SSL Policies</span></span>

<span data-ttu-id="3bf53-111">Application gateway comes with three pre-defined policies that can be used.</span><span class="sxs-lookup"><span data-stu-id="3bf53-111">Application gateway comes with three pre-defined policies that can be used.</span></span> <span data-ttu-id="3bf53-112">The `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span><span class="sxs-lookup"><span data-stu-id="3bf53-112">The `Get-AzureRmApplicationGatewaySslPredefinedPolicy` cmdlet retrieves these policies.</span></span> <span data-ttu-id="3bf53-113">Each policy has different protocol versions and cipher suites enabled.</span><span class="sxs-lookup"><span data-stu-id="3bf53-113">Each policy has different protocol versions and cipher suites enabled.</span></span> <span data-ttu-id="3bf53-114">These pre-defined policies can be used to quickly configure an SSL policy on your application gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-114">These pre-defined policies can be used to quickly configure an SSL policy on your application gateway.</span></span> <span data-ttu-id="3bf53-115">By default **AppGwSslPolicy20150501** is selected if no specific SSL policy is defined.</span><span class="sxs-lookup"><span data-stu-id="3bf53-115">By default **AppGwSslPolicy20150501** is selected if no specific SSL policy is defined.</span></span>

<span data-ttu-id="3bf53-116">The following output is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span><span class="sxs-lookup"><span data-stu-id="3bf53-116">The following output is an example of running `Get-AzureRmApplicationGatewaySslPredefinedPolicy`.</span></span>

```
Name: AppGwSslPolicy20150501
MinProtocolVersion: TLSv1_0
CipherSuites:
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
    TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
    TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
    TLS_DHE_RSA_WITH_AES_256_CBC_SHA
    TLS_DHE_RSA_WITH_AES_128_CBC_SHA
    TLS_RSA_WITH_AES_256_GCM_SHA384
 ...
Name: AppGwSslPolicy20170401
MinProtocolVersion: TLSv1_1
CipherSuites:
    TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
    TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
    TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
    TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384
...
```

## <a name="configure-a-custom-ssl-policy"></a><span data-ttu-id="3bf53-117">Configure a custom SSL policy</span><span class="sxs-lookup"><span data-stu-id="3bf53-117">Configure a custom SSL policy</span></span>

<span data-ttu-id="3bf53-118">When configuring a custom SSL policy, you pass the following parameters: PolicyType, MinProtocolVersion, CipherSuite, and ApplicationGateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-118">When configuring a custom SSL policy, you pass the following parameters: PolicyType, MinProtocolVersion, CipherSuite, and ApplicationGateway.</span></span> <span data-ttu-id="3bf53-119">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-119">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span></span> 

<span data-ttu-id="3bf53-120">The following example sets a custom SSL policy on an application gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-120">The following example sets a custom SSL policy on an application gateway.</span></span> <span data-ttu-id="3bf53-121">It sets the minimum protocol version to `TLSv1_1` and enables the following cipher suites:</span><span class="sxs-lookup"><span data-stu-id="3bf53-121">It sets the minimum protocol version to `TLSv1_1` and enables the following cipher suites:</span></span>

* <span data-ttu-id="3bf53-122">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span><span class="sxs-lookup"><span data-stu-id="3bf53-122">TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384</span></span>
* <span data-ttu-id="3bf53-123">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-123">TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3bf53-124">At least one cipher suite from the following list must be selected when configuring a custom SSL policy.</span><span class="sxs-lookup"><span data-stu-id="3bf53-124">At least one cipher suite from the following list must be selected when configuring a custom SSL policy.</span></span> <span data-ttu-id="3bf53-125">Application gateway uses RSA SHA256 cipher suites for backend management.</span><span class="sxs-lookup"><span data-stu-id="3bf53-125">Application gateway uses RSA SHA256 cipher suites for backend management.</span></span>
> * <span data-ttu-id="3bf53-126">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-126">TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256</span></span> 
> * <span data-ttu-id="3bf53-127">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-127">TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256</span></span>
> * <span data-ttu-id="3bf53-128">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-128">TLS_DHE_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="3bf53-129">TLS_RSA_WITH_AES_128_GCM_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-129">TLS_RSA_WITH_AES_128_GCM_SHA256</span></span>
> * <span data-ttu-id="3bf53-130">TLS_RSA_WITH_AES_256_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-130">TLS_RSA_WITH_AES_256_CBC_SHA256</span></span>
> * <span data-ttu-id="3bf53-131">TLS_RSA_WITH_AES_128_CBC_SHA256</span><span class="sxs-lookup"><span data-stu-id="3bf53-131">TLS_RSA_WITH_AES_128_CBC_SHA256</span></span>

```powershell
# get an application gateway resource
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroup AdatumAppGatewayRG

# set the SSL policy on the application gateway
Set-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw -PolicyType Custom -MinProtocolVersion TLSv1_1 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"

# validate the SSL policy locally
Get-AzureRmApplicationGatewaySslPolicy -ApplicationGateway $gw

# update the gateway with validated SSL policy
Set-AzureRmApplicationGateway -ApplicationGateway $gw
```

## <a name="create-an-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="3bf53-132">Create an application gateway with a pre-defined SSL policy</span><span class="sxs-lookup"><span data-stu-id="3bf53-132">Create an application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="3bf53-133">When configuring a Predefined SSL policy, you pass the following parameters: PolicyType, PolicyName, and ApplicationGateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-133">When configuring a Predefined SSL policy, you pass the following parameters: PolicyType, PolicyName, and ApplicationGateway.</span></span> <span data-ttu-id="3bf53-134">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-134">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span></span>

<span data-ttu-id="3bf53-135">The following example creates a new application gateway with a pre-defined SSL policy.</span><span class="sxs-lookup"><span data-stu-id="3bf53-135">The following example creates a new application gateway with a pre-defined SSL policy.</span></span>

```powershell
# Create a resource group
$rg = New-AzureRmResourceGroup -Name ContosoRG -Location "East US"

# Create a subnet for the application gateway
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24

# Create a virtual network with a 10.0.0.0/16 address space
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName $rg.ResourceGroupName -Location "East US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet

# Retrieve the subnet object for later use
$subnet = $vnet.Subnets[0]

# Create a public IP address
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $rg.ResourceGroupName -name publicIP01 -location "East US" -AllocationMethod Dynamic

# Create a ip configuration object
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet

# Create a backend pool for backend web servers
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221,134.170.185.50

# Define the backend http settings to be used.
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name poolsetting01 -Port 80 -Protocol Http -CookieBasedAffinity Enabled

# Create a new port for SSL
$fp = New-AzureRmApplicationGatewayFrontendPort -Name frontendport01  -Port 443

# Upload an existing pfx certificate for SSL offload
$password = ConvertTo-SecureString -String "P@ssw0rd" -AsPlainText -Force
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile C:\folder\contoso.pfx -Password $password

# Create a frontend IP configuration for the public IP address
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name fipconfig01 -PublicIPAddress $publicip

# Create a new listener with the certificate, port, and frontend ip.
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01  -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert

# Create a new rule for backend traffic routing
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name rule01 -RuleType Basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool

# Define the size of the application gateway
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2

# Configure the SSL policy to use a different pre-defined policy
$policy = New-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName AppGwSslPolicy20170401S

# Create the application gateway.
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName $rg.ResourceGroupName -Location "East US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig  -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslCertificates $cert -SslPolicy $policy
```

## <a name="update-an-existing-application-gateway-with-a-pre-defined-ssl-policy"></a><span data-ttu-id="3bf53-136">Update an existing application gateway with a pre-defined SSL policy</span><span class="sxs-lookup"><span data-stu-id="3bf53-136">Update an existing application gateway with a pre-defined SSL policy</span></span>

<span data-ttu-id="3bf53-137">To set a custom SSL policy, pass the following parameters: **PolicyType**, **MinProtocolVersion**, **CipherSuite**, and **ApplicationGateway**.</span><span class="sxs-lookup"><span data-stu-id="3bf53-137">To set a custom SSL policy, pass the following parameters: **PolicyType**, **MinProtocolVersion**, **CipherSuite**, and **ApplicationGateway**.</span></span> <span data-ttu-id="3bf53-138">To set a Predefined SSL policy, pass the following parameters: **PolicyType**, **PolicyName**, and **ApplicationGateway**.</span><span class="sxs-lookup"><span data-stu-id="3bf53-138">To set a Predefined SSL policy, pass the following parameters: **PolicyType**, **PolicyName**, and **ApplicationGateway**.</span></span> <span data-ttu-id="3bf53-139">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="3bf53-139">If you attempt to pass other parameters, you get an error when creating or updating the Application Gateway.</span></span>

<span data-ttu-id="3bf53-140">In the following example, there are code samples for both Custom Policy and Predefined Policy.</span><span class="sxs-lookup"><span data-stu-id="3bf53-140">In the following example, there are code samples for both Custom Policy and Predefined Policy.</span></span> <span data-ttu-id="3bf53-141">Uncomment the policy you want to use.</span><span class="sxs-lookup"><span data-stu-id="3bf53-141">Uncomment the policy you want to use.</span></span>

```powershell
# You have to change these parameters to match your environment.
$AppGWname = "YourAppGwName"
$RG = "YourResourceGroupName"

$AppGw = get-azurermapplicationgateway -Name $AppGWname -ResourceGroupName $RG

# Choose either custom policy or prefedined policy and uncomment the one you want to use.

# SSL Custom Policy
# Set-AzureRmApplicationGatewaySslPolicy -PolicyType Custom -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_RSA_WITH_AES_128_CBC_SHA256" -ApplicationGateway $AppGw

# SSL Predefined Policy
# Set-AzureRmApplicationGatewaySslPolicy -PolicyType Predefined -PolicyName "AppGwSslPolicy20170401S" -ApplicationGateway $AppGW

# Update AppGW
# The SSL policy options are not validated or updated on the Application Gateway until this cmdlet is executed.
$SetGW = Set-AzureRmApplicationGateway -ApplicationGateway $AppGW
```

## <a name="next-steps"></a><span data-ttu-id="3bf53-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="3bf53-142">Next steps</span></span>

<span data-ttu-id="3bf53-143">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn how to redirect HTTP traffic to an HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="3bf53-143">Visit [Application Gateway redirect overview](application-gateway-redirect-overview.md) to learn how to redirect HTTP traffic to an HTTPS endpoint.</span></span>
