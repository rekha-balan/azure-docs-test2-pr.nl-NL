---
title: Using Azure Application Gateway with Internal Load Balancer | Microsoft Docs
description: This page provides instructions to configure an Azure Application Gateway with an Internal Load Balanced endpoint
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: d6f3af61934c8c645be1f2c6b4c056fc7ee2e3aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554785"
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a><span data-ttu-id="c96b7-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span><span class="sxs-lookup"><span data-stu-id="c96b7-103">Create an Application Gateway with an Internal Load Balancer (ILB)</span></span>

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Azure Resource Manager PowerShell](application-gateway-ilb-arm.md)

<span data-ttu-id="c96b7-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span><span class="sxs-lookup"><span data-stu-id="c96b7-106">Application Gateway can be configured with an internet facing virtual IP or with an internal end-point not exposed to the internet, also known as Internal Load Balancer (ILB) endpoint.</span></span> <span data-ttu-id="c96b7-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span><span class="sxs-lookup"><span data-stu-id="c96b7-107">Configuring the gateway with an ILB is useful for internal line-of-business applications not exposed to internet.</span></span> <span data-ttu-id="c96b7-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span><span class="sxs-lookup"><span data-stu-id="c96b7-108">It's also useful for services/tiers within a multi-tier application, which sits in a security boundary not exposed to internet, but still require round robin load distribution, session stickiness, or SSL termination.</span></span> <span data-ttu-id="c96b7-109">This article walks you through the steps to configure an application gateway with an ILB.</span><span class="sxs-lookup"><span data-stu-id="c96b7-109">This article walks you through the steps to configure an application gateway with an ILB.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c96b7-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="c96b7-110">Before you begin</span></span>

1. <span data-ttu-id="c96b7-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="c96b7-111">Install latest version of the Azure PowerShell cmdlets using the Web Platform Installer.</span></span> <span data-ttu-id="c96b7-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c96b7-112">You can download and install the latest version from the **Windows PowerShell** section of the [Download page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="c96b7-113">Verify that you have a working virtual network with valid subnet.</span><span class="sxs-lookup"><span data-stu-id="c96b7-113">Verify that you have a working virtual network with valid subnet.</span></span>
3. <span data-ttu-id="c96b7-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="c96b7-114">Verify that you have backend servers either in the virtual network, or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="c96b7-115">To create an application gateway, perform the following steps in the order listed.</span><span class="sxs-lookup"><span data-stu-id="c96b7-115">To create an application gateway, perform the following steps in the order listed.</span></span> 

1. [<span data-ttu-id="c96b7-116">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-116">Create an application gateway</span></span>](#create-a-new-application-gateway)
2. [<span data-ttu-id="c96b7-117">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-117">Configure the gateway</span></span>](#configure-the-gateway)
3. [<span data-ttu-id="c96b7-118">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="c96b7-118">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
4. [<span data-ttu-id="c96b7-119">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-119">Start the gateway</span></span>](#start-the-gateway)
5. [<span data-ttu-id="c96b7-120">Verify the gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-120">Verify the gateway</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="c96b7-121">Create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="c96b7-121">Create an application gateway:</span></span>

<span data-ttu-id="c96b7-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="c96b7-122">**To create the gateway**, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="c96b7-123">Note that billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="c96b7-123">Note that billing for the gateway does not start at this point.</span></span> <span data-ttu-id="c96b7-124">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="c96b7-124">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

<span data-ttu-id="c96b7-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c96b7-125">**To validate** that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> 

<span data-ttu-id="c96b7-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span><span class="sxs-lookup"><span data-stu-id="c96b7-126">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="c96b7-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span><span class="sxs-lookup"><span data-stu-id="c96b7-127">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="c96b7-128">The default value for *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="c96b7-128">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="c96b7-129">Small and Large are other available values.</span><span class="sxs-lookup"><span data-stu-id="c96b7-129">Small and Large are other available values.</span></span> <span data-ttu-id="c96b7-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="c96b7-130">*Vip* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="c96b7-131">These are created once the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="c96b7-131">These are created once the gateway is in the running state.</span></span> 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-the-gateway"></a><span data-ttu-id="c96b7-132">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-132">Configure the gateway</span></span>
<span data-ttu-id="c96b7-133">An application gateway configuration consists of multiple values.</span><span class="sxs-lookup"><span data-stu-id="c96b7-133">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="c96b7-134">The values can be tied together to construct the configuration.</span><span class="sxs-lookup"><span data-stu-id="c96b7-134">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="c96b7-135">The values are:</span><span class="sxs-lookup"><span data-stu-id="c96b7-135">The values are:</span></span>

* <span data-ttu-id="c96b7-136">**Backend server pool:** The list of IP addresses of the backend servers.</span><span class="sxs-lookup"><span data-stu-id="c96b7-136">**Backend server pool:** The list of IP addresses of the backend servers.</span></span> <span data-ttu-id="c96b7-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="c96b7-137">The IP addresses listed should either belong to the VNet subnet, or should be a public IP/VIP.</span></span> 
* <span data-ttu-id="c96b7-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="c96b7-138">**Backend server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="c96b7-139">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="c96b7-139">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="c96b7-140">**Frontend Port:** This port is the public port opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="c96b7-140">**Frontend Port:** This port is the public port opened on the application gateway.</span></span> <span data-ttu-id="c96b7-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span><span class="sxs-lookup"><span data-stu-id="c96b7-141">Traffic hits this port, and then gets redirected to one of the backend servers.</span></span>
* <span data-ttu-id="c96b7-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="c96b7-142">**Listener:** The listener has a frontend port, a protocol (Http or Https, these are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span> 
* <span data-ttu-id="c96b7-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="c96b7-143">**Rule:** The rule binds the listener and the backend server pool and defines which backend server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="c96b7-144">Currently, only the *basic* rule is supported.</span><span class="sxs-lookup"><span data-stu-id="c96b7-144">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="c96b7-145">The *basic* rule is round-robin load distribution.</span><span class="sxs-lookup"><span data-stu-id="c96b7-145">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="c96b7-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="c96b7-146">You can construct your configuration either by creating a configuration object, or by using a configuration XML file.</span></span> <span data-ttu-id="c96b7-147">To construct your configuration by using a configuration XML file, use the sample below.</span><span class="sxs-lookup"><span data-stu-id="c96b7-147">To construct your configuration by using a configuration XML file, use the sample below.</span></span>

<span data-ttu-id="c96b7-148">Note the following:</span><span class="sxs-lookup"><span data-stu-id="c96b7-148">Note the following:</span></span>

* <span data-ttu-id="c96b7-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span><span class="sxs-lookup"><span data-stu-id="c96b7-149">The *FrontendIPConfigurations* element describes the ILB details relevant for configuring Application Gateway with an ILB.</span></span> 
* <span data-ttu-id="c96b7-150">The Frontend IP *Type* should be set to 'Private'</span><span class="sxs-lookup"><span data-stu-id="c96b7-150">The Frontend IP *Type* should be set to 'Private'</span></span>
* <span data-ttu-id="c96b7-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span><span class="sxs-lookup"><span data-stu-id="c96b7-151">The *StaticIPAddress* should be set to the desired internal IP on which the gateway receives traffic.</span></span> <span data-ttu-id="c96b7-152">Note that the *StaticIPAddress* element is optional.</span><span class="sxs-lookup"><span data-stu-id="c96b7-152">Note that the *StaticIPAddress* element is optional.</span></span> <span data-ttu-id="c96b7-153">If not set, an available internal IP from the deployed subnet is chosen.</span><span class="sxs-lookup"><span data-stu-id="c96b7-153">If not set, an available internal IP from the deployed subnet is chosen.</span></span> 
* <span data-ttu-id="c96b7-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span><span class="sxs-lookup"><span data-stu-id="c96b7-154">The value of the *Name* element specified in *FrontendIPConfiguration* should be used in the HTTPListener's *FrontendIP* element to refer to the FrontendIPConfiguration.</span></span>
  
  <span data-ttu-id="c96b7-155">**Configuration XML sample**</span><span class="sxs-lookup"><span data-stu-id="c96b7-155">**Configuration XML sample**</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-the-gateway-configuration"></a><span data-ttu-id="c96b7-156">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="c96b7-156">Set the gateway configuration</span></span>
<span data-ttu-id="c96b7-157">Next, you'll set the application gateway.</span><span class="sxs-lookup"><span data-stu-id="c96b7-157">Next, you'll set the application gateway.</span></span> <span data-ttu-id="c96b7-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="c96b7-158">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration object, or with a configuration XML file.</span></span> 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-the-gateway"></a><span data-ttu-id="c96b7-159">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="c96b7-159">Start the gateway</span></span>

<span data-ttu-id="c96b7-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span><span class="sxs-lookup"><span data-stu-id="c96b7-160">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="c96b7-161">Billing for an application gateway begins after the gateway has been successfully started.</span><span class="sxs-lookup"><span data-stu-id="c96b7-161">Billing for an application gateway begins after the gateway has been successfully started.</span></span> 

> [!NOTE]
> The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to complete. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="c96b7-163">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="c96b7-163">Verify the gateway status</span></span>

<span data-ttu-id="c96b7-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span><span class="sxs-lookup"><span data-stu-id="c96b7-164">Use the `Get-AzureApplicationGateway` cmdlet to check the status of gateway.</span></span> <span data-ttu-id="c96b7-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span><span class="sxs-lookup"><span data-stu-id="c96b7-165">If `Start-AzureApplicationGateway` succeeded in the previous step, the State should be *Running*, and the Vip and DnsName should have valid entries.</span></span> <span data-ttu-id="c96b7-166">This sample shows the cmdlet on the first line, followed by the output.</span><span class="sxs-lookup"><span data-stu-id="c96b7-166">This sample shows the cmdlet on the first line, followed by the output.</span></span> <span data-ttu-id="c96b7-167">In this sample, the gateway is running, and is ready to take traffic.</span><span class="sxs-lookup"><span data-stu-id="c96b7-167">In this sample, the gateway is running, and is ready to take traffic.</span></span> 

> [!NOTE]
> The application gateway is configured to accept traffic at the configured ILB endpoint of 10.0.0.10 in this example.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="c96b7-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="c96b7-169">Next steps</span></span>
<span data-ttu-id="c96b7-170">If you want more information about load balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="c96b7-170">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="c96b7-171">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="c96b7-171">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="c96b7-172">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="c96b7-172">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

