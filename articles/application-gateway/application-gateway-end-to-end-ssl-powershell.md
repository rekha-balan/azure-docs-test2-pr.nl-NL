---
title: Configure SSL Policy and end to end SSL with Application Gateway | Microsoft Docs
description: This article describes how to configure end to end SSL with Application Gateway using Azure Resource Manager PowerShell
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/14/2016
ms.author: gwallace
ms.openlocfilehash: f4cf7617ec6eaa8d0864f048bdf478406ecbfcac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551440"
---
# <a name="configure-ssl-policy-and-end-to-end-ssl-with-application-gateway-using-powershell"></a><span data-ttu-id="cce63-103">Configure SSL Policy and end to end SSL with Application Gateway using PowerShell</span><span class="sxs-lookup"><span data-stu-id="cce63-103">Configure SSL Policy and end to end SSL with Application Gateway using PowerShell</span></span>

## <a name="overview"></a><span data-ttu-id="cce63-104">Overview</span><span class="sxs-lookup"><span data-stu-id="cce63-104">Overview</span></span>

<span data-ttu-id="cce63-105">Application Gateway supports end to end encryption of traffic.</span><span class="sxs-lookup"><span data-stu-id="cce63-105">Application Gateway supports end to end encryption of traffic.</span></span> <span data-ttu-id="cce63-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-106">Application Gateway does this by terminating the SSL connection at the application gateway.</span></span> <span data-ttu-id="cce63-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span><span class="sxs-lookup"><span data-stu-id="cce63-107">The gateway then applies the routing rules to the traffic, re-encrypts the packet, and forwards the packet to the appropriate backend based on the routing rules defined.</span></span> <span data-ttu-id="cce63-108">Any response from the web server goes through the same process back to the end user.</span><span class="sxs-lookup"><span data-stu-id="cce63-108">Any response from the web server goes through the same process back to the end user.</span></span>

<span data-ttu-id="cce63-109">Another feature that application gateway supports is disabling certain SSL protocol versions.</span><span class="sxs-lookup"><span data-stu-id="cce63-109">Another feature that application gateway supports is disabling certain SSL protocol versions.</span></span> <span data-ttu-id="cce63-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2**.</span><span class="sxs-lookup"><span data-stu-id="cce63-110">Application Gateway supports disabling the following protocol version; **TLSv1.0**, **TLSv1.1**, and **TLSv1.2**.</span></span>

> [!NOTE]
> <span data-ttu-id="cce63-111">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span><span class="sxs-lookup"><span data-stu-id="cce63-111">SSL 2.0 and SSL 3.0 are disabled by default and cannot be enabled.</span></span> <span data-ttu-id="cce63-112">They are considered unsecure and are not able to be used with Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-112">They are considered unsecure and are not able to be used with Application Gateway.</span></span>

![scenario image][scenario]

## <a name="scenario"></a><span data-ttu-id="cce63-114">Scenario</span><span class="sxs-lookup"><span data-stu-id="cce63-114">Scenario</span></span>

<span data-ttu-id="cce63-115">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cce63-115">In this scenario, you learn how to create an application gateway using end to end SSL using PowerShell.</span></span>

<span data-ttu-id="cce63-116">This scenario will:</span><span class="sxs-lookup"><span data-stu-id="cce63-116">This scenario will:</span></span>

* <span data-ttu-id="cce63-117">Create a resource group named **appgw-rg**</span><span class="sxs-lookup"><span data-stu-id="cce63-117">Create a resource group named **appgw-rg**</span></span>
* <span data-ttu-id="cce63-118">Create a virtual network named **appgwvnet** with a reserved CIDR block of 10.0.0.0/16.</span><span class="sxs-lookup"><span data-stu-id="cce63-118">Create a virtual network named **appgwvnet** with a reserved CIDR block of 10.0.0.0/16.</span></span>
* <span data-ttu-id="cce63-119">Create two subnets called **appgwsubnet** and **appsubnet**.</span><span class="sxs-lookup"><span data-stu-id="cce63-119">Create two subnets called **appgwsubnet** and **appsubnet**.</span></span>
* <span data-ttu-id="cce63-120">Create a small application gateway supporting end to end SSL encryption that disables certain SSL protocols.</span><span class="sxs-lookup"><span data-stu-id="cce63-120">Create a small application gateway supporting end to end SSL encryption that disables certain SSL protocols.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cce63-121">Before you begin</span><span class="sxs-lookup"><span data-stu-id="cce63-121">Before you begin</span></span>

<span data-ttu-id="cce63-122">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span><span class="sxs-lookup"><span data-stu-id="cce63-122">To configure end to end SSL with an application gateway, a certificate is required for the gateway and certificates are required for the backend servers.</span></span> <span data-ttu-id="cce63-123">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span><span class="sxs-lookup"><span data-stu-id="cce63-123">The gateway certificate is used to encrypt and decrypt the traffic sent to it using SSL.</span></span> <span data-ttu-id="cce63-124">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span><span class="sxs-lookup"><span data-stu-id="cce63-124">The gateway certificate needs to be in Personal Information Exchange (pfx) format.</span></span> <span data-ttu-id="cce63-125">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span><span class="sxs-lookup"><span data-stu-id="cce63-125">This file format allows for the private key to be exported which is required by the application gateway to perform the encryption and decryption of traffic.</span></span>

<span data-ttu-id="cce63-126">For end to end ssl encryption the backend must be whitelisted with application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-126">For end to end ssl encryption the backend must be whitelisted with application gateway.</span></span> <span data-ttu-id="cce63-127">This is done by uploading the public certificate of the backends to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-127">This is done by uploading the public certificate of the backends to the application gateway.</span></span> <span data-ttu-id="cce63-128">This ensures that the application gateway only communicates with known backend instances.</span><span class="sxs-lookup"><span data-stu-id="cce63-128">This ensures that the application gateway only communicates with known backend instances.</span></span> <span data-ttu-id="cce63-129">This further secures the end to end communication.</span><span class="sxs-lookup"><span data-stu-id="cce63-129">This further secures the end to end communication.</span></span>

<span data-ttu-id="cce63-130">This process is described in the following steps:</span><span class="sxs-lookup"><span data-stu-id="cce63-130">This process is described in the following steps:</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="cce63-131">Create the Resource Group</span><span class="sxs-lookup"><span data-stu-id="cce63-131">Create the Resource Group</span></span>

<span data-ttu-id="cce63-132">This section walks you through creating a resource group, that contains the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-132">This section walks you through creating a resource group, that contains the application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="cce63-133">Step 1</span><span class="sxs-lookup"><span data-stu-id="cce63-133">Step 1</span></span>

<span data-ttu-id="cce63-134">Log in to your Azure Account.</span><span class="sxs-lookup"><span data-stu-id="cce63-134">Log in to your Azure Account.</span></span>

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a><span data-ttu-id="cce63-135">Step 2</span><span class="sxs-lookup"><span data-stu-id="cce63-135">Step 2</span></span>

<span data-ttu-id="cce63-136">Select the subscription to use for this scenario.</span><span class="sxs-lookup"><span data-stu-id="cce63-136">Select the subscription to use for this scenario.</span></span>

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a><span data-ttu-id="cce63-137">Step 3</span><span class="sxs-lookup"><span data-stu-id="cce63-137">Step 3</span></span>

<span data-ttu-id="cce63-138">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="cce63-138">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="cce63-139">Create a virtual network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="cce63-139">Create a virtual network and a subnet for the application gateway</span></span>

<span data-ttu-id="cce63-140">The following example creates a virtual network and two subnets.</span><span class="sxs-lookup"><span data-stu-id="cce63-140">The following example creates a virtual network and two subnets.</span></span> <span data-ttu-id="cce63-141">One subnet is used to hold the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-141">One subnet is used to hold the application gateway.</span></span> <span data-ttu-id="cce63-142">The other subnet is used for the backends hosting the web application.</span><span class="sxs-lookup"><span data-stu-id="cce63-142">The other subnet is used for the backends hosting the web application.</span></span>

### <a name="step-1"></a><span data-ttu-id="cce63-143">Step 1</span><span class="sxs-lookup"><span data-stu-id="cce63-143">Step 1</span></span>

<span data-ttu-id="cce63-144">Assign an address range for the subnet be used for the Application Gateway itself.</span><span class="sxs-lookup"><span data-stu-id="cce63-144">Assign an address range for the subnet be used for the Application Gateway itself.</span></span>

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> <span data-ttu-id="cce63-145">Subnets configured for application gateway should be properly sized.</span><span class="sxs-lookup"><span data-stu-id="cce63-145">Subnets configured for application gateway should be properly sized.</span></span> <span data-ttu-id="cce63-146">An application gateway can be configured for up to 10 instances.</span><span class="sxs-lookup"><span data-stu-id="cce63-146">An application gateway can be configured for up to 10 instances.</span></span> <span data-ttu-id="cce63-147">Each instance takes 1 IP address from the subnet.</span><span class="sxs-lookup"><span data-stu-id="cce63-147">Each instance takes 1 IP address from the subnet.</span></span> <span data-ttu-id="cce63-148">Too small of a subnet can adversely affect scaling out an application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-148">Too small of a subnet can adversely affect scaling out an application gateway.</span></span>
> 
> 

### <a name="step-2"></a><span data-ttu-id="cce63-149">Step 2</span><span class="sxs-lookup"><span data-stu-id="cce63-149">Step 2</span></span>

<span data-ttu-id="cce63-150">Assign an address range to be used for the Backend address pool.</span><span class="sxs-lookup"><span data-stu-id="cce63-150">Assign an address range to be used for the Backend address pool.</span></span>

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a><span data-ttu-id="cce63-151">Step 3</span><span class="sxs-lookup"><span data-stu-id="cce63-151">Step 3</span></span>

<span data-ttu-id="cce63-152">Create a virtual network with the subnets defined in the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="cce63-152">Create a virtual network with the subnets defined in the preceding steps.</span></span>

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a><span data-ttu-id="cce63-153">Step 4</span><span class="sxs-lookup"><span data-stu-id="cce63-153">Step 4</span></span>

<span data-ttu-id="cce63-154">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span><span class="sxs-lookup"><span data-stu-id="cce63-154">Retrieve the virtual network resource and subnet resources to be used in the following steps:</span></span>

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="cce63-155">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="cce63-155">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="cce63-156">Create a public IP resource to be used for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-156">Create a public IP resource to be used for the application gateway.</span></span> <span data-ttu-id="cce63-157">This public IP address is used a following step.</span><span class="sxs-lookup"><span data-stu-id="cce63-157">This public IP address is used a following step.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> <span data-ttu-id="cce63-158">Application Gateway does not support the use of a public IP address created with a domain label defined.</span><span class="sxs-lookup"><span data-stu-id="cce63-158">Application Gateway does not support the use of a public IP address created with a domain label defined.</span></span> <span data-ttu-id="cce63-159">Only a public IP address with a dynamically created domain label is supported.</span><span class="sxs-lookup"><span data-stu-id="cce63-159">Only a public IP address with a dynamically created domain label is supported.</span></span> <span data-ttu-id="cce63-160">If you require a friendly dns name for the application gateway, it is recommended to use a cname record as an alias.</span><span class="sxs-lookup"><span data-stu-id="cce63-160">If you require a friendly dns name for the application gateway, it is recommended to use a cname record as an alias.</span></span>

## <a name="create-an-application-gateway-configuration-object"></a><span data-ttu-id="cce63-161">Create an application gateway configuration object</span><span class="sxs-lookup"><span data-stu-id="cce63-161">Create an application gateway configuration object</span></span>

<span data-ttu-id="cce63-162">You must set up all configuration items before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-162">You must set up all configuration items before creating the application gateway.</span></span> <span data-ttu-id="cce63-163">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="cce63-163">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="cce63-164">Step 1</span><span class="sxs-lookup"><span data-stu-id="cce63-164">Step 1</span></span>

<span data-ttu-id="cce63-165">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span><span class="sxs-lookup"><span data-stu-id="cce63-165">Create an application gateway IP configuration, this setting configures what subnet the application gateway uses.</span></span> <span data-ttu-id="cce63-166">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="cce63-166">When application gateway starts, it picks up an IP address from the subnet configured and routes network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="cce63-167">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="cce63-167">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a><span data-ttu-id="cce63-168">Step 2</span><span class="sxs-lookup"><span data-stu-id="cce63-168">Step 2</span></span>

<span data-ttu-id="cce63-169">Create a front-end IP configuration, this setting maps a private or public ip address to the front-end of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-169">Create a front-end IP configuration, this setting maps a private or public ip address to the front-end of the application gateway.</span></span> <span data-ttu-id="cce63-170">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span><span class="sxs-lookup"><span data-stu-id="cce63-170">The following step associates the public IP address in the preceding step with the front-end IP configuration.</span></span>

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a><span data-ttu-id="cce63-171">Step 3</span><span class="sxs-lookup"><span data-stu-id="cce63-171">Step 3</span></span>

<span data-ttu-id="cce63-172">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span><span class="sxs-lookup"><span data-stu-id="cce63-172">Configure the back-end IP address pool with the IP addresses of the backend web servers.</span></span> <span data-ttu-id="cce63-173">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="cce63-173">These IP addresses are the IP addresses that receive the network traffic that comes from the front-end IP endpoint.</span></span> <span data-ttu-id="cce63-174">You replace the following IP addresses to add your own application IP address endpoints.</span><span class="sxs-lookup"><span data-stu-id="cce63-174">You replace the following IP addresses to add your own application IP address endpoints.</span></span>

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> <span data-ttu-id="cce63-175">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span><span class="sxs-lookup"><span data-stu-id="cce63-175">A fully qualified domain name (FQDN) is also a valid value in place of an ip address for the backend servers by using the -BackendFqdns switch.</span></span> 

### <a name="step-4"></a><span data-ttu-id="cce63-176">Step 4</span><span class="sxs-lookup"><span data-stu-id="cce63-176">Step 4</span></span>

<span data-ttu-id="cce63-177">Configure the front-end IP port for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="cce63-177">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="cce63-178">This port is the port that end users connect to.</span><span class="sxs-lookup"><span data-stu-id="cce63-178">This port is the port that end users connect to.</span></span>

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a><span data-ttu-id="cce63-179">Step 5</span><span class="sxs-lookup"><span data-stu-id="cce63-179">Step 5</span></span>

<span data-ttu-id="cce63-180">Configure the certificate for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-180">Configure the certificate for the application gateway.</span></span> <span data-ttu-id="cce63-181">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-181">This certificate is used to decrypt and re-encrypt the traffic on the application gateway.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name cert01 -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

> [!NOTE]
> <span data-ttu-id="cce63-182">This sample configures the certificate used for SSL connection.</span><span class="sxs-lookup"><span data-stu-id="cce63-182">This sample configures the certificate used for SSL connection.</span></span> <span data-ttu-id="cce63-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span><span class="sxs-lookup"><span data-stu-id="cce63-183">The certificate needs to be in .pfx format, and the password must be between 4 to 12 characters.</span></span>

### <a name="step-6"></a><span data-ttu-id="cce63-184">Step 6</span><span class="sxs-lookup"><span data-stu-id="cce63-184">Step 6</span></span>

<span data-ttu-id="cce63-185">Create the HTTP listener for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-185">Create the HTTP listener for the application gateway.</span></span> <span data-ttu-id="cce63-186">Assign the front-end ip configuration, port, and ssl certificate to use.</span><span class="sxs-lookup"><span data-stu-id="cce63-186">Assign the front-end ip configuration, port, and ssl certificate to use.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SslCertificate $cert
```

### <a name="step-7"></a><span data-ttu-id="cce63-187">Step 7</span><span class="sxs-lookup"><span data-stu-id="cce63-187">Step 7</span></span>

<span data-ttu-id="cce63-188">Upload the certificate to be used on the ssl enabled backend pool resources.</span><span class="sxs-lookup"><span data-stu-id="cce63-188">Upload the certificate to be used on the ssl enabled backend pool resources.</span></span>

> [!NOTE]
> <span data-ttu-id="cce63-189">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span><span class="sxs-lookup"><span data-stu-id="cce63-189">The default probe gets the public key from the **default** SSL binding on the back-end's IP address and compares the public key value it receives to the public key value you provide here.</span></span> <span data-ttu-id="cce63-190">The retrieved public key may not necessarily be the intended site to which traffic will flow **if** you are using host headers and SNI on the back-end.</span><span class="sxs-lookup"><span data-stu-id="cce63-190">The retrieved public key may not necessarily be the intended site to which traffic will flow **if** you are using host headers and SNI on the back-end.</span></span> <span data-ttu-id="cce63-191">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span><span class="sxs-lookup"><span data-stu-id="cce63-191">If in doubt, visit https://127.0.0.1/ on the back-ends to confirm which certificate is used for the **default** SSL binding.</span></span> <span data-ttu-id="cce63-192">Use the public key from that request in this section.</span><span class="sxs-lookup"><span data-stu-id="cce63-192">Use the public key from that request in this section.</span></span> <span data-ttu-id="cce63-193">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span><span class="sxs-lookup"><span data-stu-id="cce63-193">If you are using host-headers and SNI on HTTPS bindings and you do not receive a response and certificate from a manual browser request to https://127.0.0.1/ on the back-ends, you must set up a default SSL binding on the back-ends.</span></span> <span data-ttu-id="cce63-194">If you do not do so, probes will fail and the back-end will be not be whitelisted.</span><span class="sxs-lookup"><span data-stu-id="cce63-194">If you do not do so, probes will fail and the back-end will be not be whitelisted.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> <span data-ttu-id="cce63-195">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span><span class="sxs-lookup"><span data-stu-id="cce63-195">The certificate provided in this step should be the public key of the pfx cert present on the backend.</span></span> <span data-ttu-id="cce63-196">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span><span class="sxs-lookup"><span data-stu-id="cce63-196">Export the certificate (not the root certificate) installed on the backend server in .CER format and use it in this step.</span></span> <span data-ttu-id="cce63-197">This step whitelists the backend with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-197">This step whitelists the backend with the application gateway.</span></span>

### <a name="step-8"></a><span data-ttu-id="cce63-198">Step 8</span><span class="sxs-lookup"><span data-stu-id="cce63-198">Step 8</span></span>

<span data-ttu-id="cce63-199">Configure the application gateway back-end http settings.</span><span class="sxs-lookup"><span data-stu-id="cce63-199">Configure the application gateway back-end http settings.</span></span> <span data-ttu-id="cce63-200">Assign the certificate uploaded in the preceding step to the http settings.</span><span class="sxs-lookup"><span data-stu-id="cce63-200">Assign the certificate uploaded in the preceding step to the http settings.</span></span>

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a><span data-ttu-id="cce63-201">Step 9</span><span class="sxs-lookup"><span data-stu-id="cce63-201">Step 9</span></span>

<span data-ttu-id="cce63-202">Create a load balancer routing rule that configures the load balancer behavior.</span><span class="sxs-lookup"><span data-stu-id="cce63-202">Create a load balancer routing rule that configures the load balancer behavior.</span></span> <span data-ttu-id="cce63-203">In this example, a basic round robin rule is created.</span><span class="sxs-lookup"><span data-stu-id="cce63-203">In this example, a basic round robin rule is created.</span></span>

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a><span data-ttu-id="cce63-204">Step 10</span><span class="sxs-lookup"><span data-stu-id="cce63-204">Step 10</span></span>

<span data-ttu-id="cce63-205">Configure the instance size of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-205">Configure the instance size of the application gateway.</span></span>  <span data-ttu-id="cce63-206">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span><span class="sxs-lookup"><span data-stu-id="cce63-206">The available sizes are **Standard\_Small**, **Standard\_Medium**, and **Standard\_Large**.</span></span>  <span data-ttu-id="cce63-207">For capacity, the available values are 1 through 10.</span><span class="sxs-lookup"><span data-stu-id="cce63-207">For capacity, the available values are 1 through 10.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> <span data-ttu-id="cce63-208">An instance count of 1 can be chosen for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="cce63-208">An instance count of 1 can be chosen for testing purposes.</span></span> <span data-ttu-id="cce63-209">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span><span class="sxs-lookup"><span data-stu-id="cce63-209">It is important to know that any instance count under two instances is not covered by the SLA and are therefore not recommended.</span></span> <span data-ttu-id="cce63-210">Small gateways are to be used for dev test and not for production purposes.</span><span class="sxs-lookup"><span data-stu-id="cce63-210">Small gateways are to be used for dev test and not for production purposes.</span></span>

### <a name="step-11"></a><span data-ttu-id="cce63-211">Step 11</span><span class="sxs-lookup"><span data-stu-id="cce63-211">Step 11</span></span>

<span data-ttu-id="cce63-212">Configure the SSL policy to be used on the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-212">Configure the SSL policy to be used on the Application Gateway.</span></span> <span data-ttu-id="cce63-213">Application Gateway supports the ability to disable certain SSL protocol versions.</span><span class="sxs-lookup"><span data-stu-id="cce63-213">Application Gateway supports the ability to disable certain SSL protocol versions.</span></span>

<span data-ttu-id="cce63-214">The following values are a list of protocol versions that can be disabled.</span><span class="sxs-lookup"><span data-stu-id="cce63-214">The following values are a list of protocol versions that can be disabled.</span></span>

* <span data-ttu-id="cce63-215">**TLSv1_0**</span><span class="sxs-lookup"><span data-stu-id="cce63-215">**TLSv1_0**</span></span>
* <span data-ttu-id="cce63-216">**TLSv1_1**</span><span class="sxs-lookup"><span data-stu-id="cce63-216">**TLSv1_1**</span></span>
* <span data-ttu-id="cce63-217">**TLSv1_2**</span><span class="sxs-lookup"><span data-stu-id="cce63-217">**TLSv1_2**</span></span>

<span data-ttu-id="cce63-218">The following example disables **TLSv1\_0**.</span><span class="sxs-lookup"><span data-stu-id="cce63-218">The following example disables **TLSv1\_0**.</span></span>

```powershell
$sslPolicy = New-AzureRmApplicationGatewaySslPolicy -DisabledSslProtocols TLSv1_0
```

## <a name="create-the-application-gateway"></a><span data-ttu-id="cce63-219">Create the Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cce63-219">Create the Application Gateway</span></span>

<span data-ttu-id="cce63-220">Using all the preceding steps, create the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-220">Using all the preceding steps, create the Application Gateway.</span></span> <span data-ttu-id="cce63-221">The creation of the gateway is a long running process.</span><span class="sxs-lookup"><span data-stu-id="cce63-221">The creation of the gateway is a long running process.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SslCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SslPolicy $sslPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="disable-ssl-protocol-versions-on-an-existing-application-gateway"></a><span data-ttu-id="cce63-222">Disable SSL protocol versions on an existing Application Gateway</span><span class="sxs-lookup"><span data-stu-id="cce63-222">Disable SSL protocol versions on an existing Application Gateway</span></span>

<span data-ttu-id="cce63-223">The preceding steps take you through creating an application with end to end ssl and disabling certain SSL protocol versions.</span><span class="sxs-lookup"><span data-stu-id="cce63-223">The preceding steps take you through creating an application with end to end ssl and disabling certain SSL protocol versions.</span></span> <span data-ttu-id="cce63-224">The following example disables certain SSL policies on an existing application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-224">The following example disables certain SSL policies on an existing application gateway.</span></span>

### <a name="step-1"></a><span data-ttu-id="cce63-225">Step 1</span><span class="sxs-lookup"><span data-stu-id="cce63-225">Step 1</span></span>

<span data-ttu-id="cce63-226">Retrieve the application gateway to update.</span><span class="sxs-lookup"><span data-stu-id="cce63-226">Retrieve the application gateway to update.</span></span>

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a><span data-ttu-id="cce63-227">Step 2</span><span class="sxs-lookup"><span data-stu-id="cce63-227">Step 2</span></span>

<span data-ttu-id="cce63-228">Define an SSL policy.</span><span class="sxs-lookup"><span data-stu-id="cce63-228">Define an SSL policy.</span></span> <span data-ttu-id="cce63-229">In the following example, TLSv1.0 and TLSv1.1 are disabled.</span><span class="sxs-lookup"><span data-stu-id="cce63-229">In the following example, TLSv1.0 and TLSv1.1 are disabled.</span></span>

```powershell
Set-AzureRmApplicationGatewaySslPolicy -DisabledSslProtocols TLSv1_0, TLSv1_1 -ApplicationGateway $gw
```

### <a name="step-3"></a><span data-ttu-id="cce63-230">Step 3</span><span class="sxs-lookup"><span data-stu-id="cce63-230">Step 3</span></span>

<span data-ttu-id="cce63-231">Finally, update the gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-231">Finally, update the gateway.</span></span> <span data-ttu-id="cce63-232">It is important to note that this last step is a long running task.</span><span class="sxs-lookup"><span data-stu-id="cce63-232">It is important to note that this last step is a long running task.</span></span> <span data-ttu-id="cce63-233">When it is done, end to end ssl is configured on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-233">When it is done, end to end ssl is configured on the application gateway.</span></span>

```powershell
$gw | Set-AzureRmApplicationGateway
```

## <a name="get-application-gateway-dns-name"></a><span data-ttu-id="cce63-234">Get application gateway DNS name</span><span class="sxs-lookup"><span data-stu-id="cce63-234">Get application gateway DNS name</span></span>

<span data-ttu-id="cce63-235">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="cce63-235">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="cce63-236">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span><span class="sxs-lookup"><span data-stu-id="cce63-236">When using a public IP, application gateway requires a dynamically assigned DNS name, which is not friendly.</span></span> <span data-ttu-id="cce63-237">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-237">To ensure end users can hit the application gateway a CNAME record can be used to point to the public endpoint of the application gateway.</span></span> <span data-ttu-id="cce63-238">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cce63-238">[Configuring a custom domain name for in Azure](../cloud-services/cloud-services-custom-domain-name-portal.md).</span></span> <span data-ttu-id="cce63-239">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-239">To do this, retrieve details of the application gateway and its associated IP/DNS name using the PublicIPAddress element attached to the application gateway.</span></span> <span data-ttu-id="cce63-240">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="cce63-240">The application gateway's DNS name should be used to create a CNAME record, which points the two web applications to this DNS name.</span></span> <span data-ttu-id="cce63-241">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span><span class="sxs-lookup"><span data-stu-id="cce63-241">The use of A-records is not recommended since the VIP may change on restart of application gateway.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="cce63-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="cce63-242">Next steps</span></span>

<span data-ttu-id="cce63-243">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span><span class="sxs-lookup"><span data-stu-id="cce63-243">Learn about hardening the security of your web applications with Web Application Firewall through Application Gateway by visiting [Web Application Firewall Overview](application-gateway-webapplicationfirewall-overview.md)</span></span>

[scenario]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/application-gateway/media/application-gateway-end-to-end-ssl-powershell/scenario.png

