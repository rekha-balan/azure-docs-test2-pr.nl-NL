---
title: Create, start, or delete an application gateway | Microsoft Docs
description: This page provides instructions to create, configure, start, and delete an Azure application gateway
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: victorh
ms.openlocfilehash: a1cfd42f5b1c31b911005b2539047630c6d320dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825500"
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a><span data-ttu-id="f850c-103">Create, start, or delete an application gateway with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f850c-103">Create, start, or delete an application gateway with PowerShell</span></span> 

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-gateway-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Azure Resource Manager template](application-gateway-create-gateway-arm-template.md)
> * [Azure CLI](application-gateway-create-gateway-cli.md)

<span data-ttu-id="f850c-109">Azure Application Gateway is a layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="f850c-109">Azure Application Gateway is a layer-7 load balancer.</span></span> <span data-ttu-id="f850c-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span><span class="sxs-lookup"><span data-stu-id="f850c-110">It provides failover, performance-routing HTTP requests between different servers, whether they are on the cloud or on-premises.</span></span> <span data-ttu-id="f850c-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span><span class="sxs-lookup"><span data-stu-id="f850c-111">Application Gateway provides many Application Delivery Controller (ADC) features including HTTP load balancing, cookie-based session affinity, Secure Sockets Layer (SSL) offload, custom health probes, support for multi-site, and many others.</span></span> <span data-ttu-id="f850c-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="f850c-112">To find a complete list of supported features, visit [Application Gateway Overview](application-gateway-introduction.md)</span></span>

<span data-ttu-id="f850c-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-113">This article walks you through the steps to create, configure, start, and delete an application gateway.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f850c-114">Before you begin</span><span class="sxs-lookup"><span data-stu-id="f850c-114">Before you begin</span></span>

1. <span data-ttu-id="f850c-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="f850c-115">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="f850c-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f850c-116">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f850c-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-117">If you have an existing virtual network, either select an existing empty subnet or create a new subnet in your existing virtual network solely for use by the application gateway.</span></span> <span data-ttu-id="f850c-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span><span class="sxs-lookup"><span data-stu-id="f850c-118">You cannot deploy the application gateway to a different virtual network than the resources you intend to deploy behind the application gateway unless vnet peering is used.</span></span> <span data-ttu-id="f850c-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f850c-119">To learn more visit [Vnet Peering](../virtual-network/virtual-network-peering-overview.md)</span></span>
3. <span data-ttu-id="f850c-120">Verify that you have a working virtual network with a valid subnet.</span><span class="sxs-lookup"><span data-stu-id="f850c-120">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="f850c-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="f850c-121">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="f850c-122">The application gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="f850c-122">The application gateway must be by itself in a virtual network subnet.</span></span>
4. <span data-ttu-id="f850c-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="f850c-123">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

## <a name="what-is-required-to-create-an-application-gateway"></a><span data-ttu-id="f850c-124">What is required to create an application gateway?</span><span class="sxs-lookup"><span data-stu-id="f850c-124">What is required to create an application gateway?</span></span>

<span data-ttu-id="f850c-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="f850c-125">When you use the `New-AzureApplicationGateway` command to create the application gateway, no configuration is set at this point and the newly created resource are configured either by using XML or a configuration object.</span></span>

<span data-ttu-id="f850c-126">The values are:</span><span class="sxs-lookup"><span data-stu-id="f850c-126">The values are:</span></span>

* <span data-ttu-id="f850c-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="f850c-127">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="f850c-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="f850c-128">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="f850c-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="f850c-129">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="f850c-130">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="f850c-130">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="f850c-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-131">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="f850c-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="f850c-132">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="f850c-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="f850c-133">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="f850c-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="f850c-134">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span>

## <a name="create-an-application-gateway"></a><span data-ttu-id="f850c-135">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="f850c-135">Create an application gateway</span></span>

<span data-ttu-id="f850c-136">To create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="f850c-136">To create an application gateway:</span></span>

1. <span data-ttu-id="f850c-137">Create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="f850c-137">Create an application gateway resource.</span></span>
2. <span data-ttu-id="f850c-138">Create a configuration XML file or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="f850c-138">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="f850c-139">Commit the configuration to the newly created application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="f850c-139">Commit the configuration to the newly created application gateway resource.</span></span>

> [!NOTE]
> If you need to configure a custom probe for your application gateway, see [Create an application gateway with custom probes by using PowerShell](application-gateway-create-probe-classic-ps.md). Check out [custom probes and health monitoring](application-gateway-probe-overview.md) for more information.

![Scenario example][scenario]

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="f850c-143">Create an application gateway resource</span><span class="sxs-lookup"><span data-stu-id="f850c-143">Create an application gateway resource</span></span>

<span data-ttu-id="f850c-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="f850c-144">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="f850c-145">Billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="f850c-145">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="f850c-146">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="f850c-146">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="f850c-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span><span class="sxs-lookup"><span data-stu-id="f850c-147">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1":</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="f850c-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span><span class="sxs-lookup"><span data-stu-id="f850c-148">*Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span>

<span data-ttu-id="f850c-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f850c-149">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> The default value for *InstanceCount* is 2, with a maximum value of 10. The default value for *GatewaySize* is Medium. You can choose between Small, Medium and Large.

<span data-ttu-id="f850c-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="f850c-153">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="f850c-154">These are created once the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="f850c-154">These are created once the gateway is in the running state.</span></span>

## <a name="configure-the-application-gateway"></a><span data-ttu-id="f850c-155">Configure the application gateway</span><span class="sxs-lookup"><span data-stu-id="f850c-155">Configure the application gateway</span></span>

<span data-ttu-id="f850c-156">You can configure the application gateway by using XML or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="f850c-156">You can configure the application gateway by using XML or a configuration object.</span></span>

### <a name="configure-the-application-gateway-by-using-xml"></a><span data-ttu-id="f850c-157">Configure the application gateway by using XML</span><span class="sxs-lookup"><span data-stu-id="f850c-157">Configure the application gateway by using XML</span></span>

<span data-ttu-id="f850c-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="f850c-158">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

#### <a name="step-1"></a><span data-ttu-id="f850c-159">Step 1</span><span class="sxs-lookup"><span data-stu-id="f850c-159">Step 1</span></span>

<span data-ttu-id="f850c-160">Copy the following text to Notepad.</span><span class="sxs-lookup"><span data-stu-id="f850c-160">Copy the following text to Notepad.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="f850c-161">Edit the values between the parentheses for the configuration items.</span><span class="sxs-lookup"><span data-stu-id="f850c-161">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="f850c-162">Save the file with extension .xml.</span><span class="sxs-lookup"><span data-stu-id="f850c-162">Save the file with extension .xml.</span></span>

> [!IMPORTANT]
> The protocol item Http or Https is case-sensitive.

<span data-ttu-id="f850c-164">The following example shows how to use a configuration file to set up the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-164">The following example shows how to use a configuration file to set up the application gateway.</span></span> <span data-ttu-id="f850c-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span><span class="sxs-lookup"><span data-stu-id="f850c-165">The example load balances HTTP traffic on public port 80 and sends network traffic to back-end port 80 between two IP addresses.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a><span data-ttu-id="f850c-166">Step 2</span><span class="sxs-lookup"><span data-stu-id="f850c-166">Step 2</span></span>

<span data-ttu-id="f850c-167">Next, set the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-167">Next, set the application gateway.</span></span> <span data-ttu-id="f850c-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="f850c-168">Use the `Set-AzureApplicationGatewayConfig` cmdlet with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-the-application-gateway-by-using-a-configuration-object"></a><span data-ttu-id="f850c-169">Configure the application gateway by using a configuration object</span><span class="sxs-lookup"><span data-stu-id="f850c-169">Configure the application gateway by using a configuration object</span></span>

<span data-ttu-id="f850c-170">The following example shows how to configure the application gateway by using configuration objects.</span><span class="sxs-lookup"><span data-stu-id="f850c-170">The following example shows how to configure the application gateway by using configuration objects.</span></span> <span data-ttu-id="f850c-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span><span class="sxs-lookup"><span data-stu-id="f850c-171">All configuration items must be configured individually and then added to an application gateway configuration object.</span></span> <span data-ttu-id="f850c-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="f850c-172">After creating the configuration object, you use the `Set-AzureApplicationGateway` command to commit the configuration to the previously created application gateway resource.</span></span>

> [!NOTE]
> Before assigning a value to each configuration object, you need to declare what kind of object PowerShell uses for storage. The first line to create the individual items defines what `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` are used.

#### <a name="step-1"></a><span data-ttu-id="f850c-175">Step 1</span><span class="sxs-lookup"><span data-stu-id="f850c-175">Step 1</span></span>

<span data-ttu-id="f850c-176">Create all individual configuration items.</span><span class="sxs-lookup"><span data-stu-id="f850c-176">Create all individual configuration items.</span></span>

<span data-ttu-id="f850c-177">Create the front-end IP as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="f850c-177">Create the front-end IP as shown in the following example.</span></span>

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

<span data-ttu-id="f850c-178">Create the front-end port as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="f850c-178">Create the front-end port as shown in the following example.</span></span>

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

<span data-ttu-id="f850c-179">Create the back-end server pool.</span><span class="sxs-lookup"><span data-stu-id="f850c-179">Create the back-end server pool.</span></span>

<span data-ttu-id="f850c-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span><span class="sxs-lookup"><span data-stu-id="f850c-180">Define the IP addresses that are added to the back-end server pool as shown in the next example.</span></span>

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

<span data-ttu-id="f850c-181">Use the $server object to add the values to the back-end pool object ($pool).</span><span class="sxs-lookup"><span data-stu-id="f850c-181">Use the $server object to add the values to the back-end pool object ($pool).</span></span>

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

<span data-ttu-id="f850c-182">Create the back-end server pool setting.</span><span class="sxs-lookup"><span data-stu-id="f850c-182">Create the back-end server pool setting.</span></span>

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

<span data-ttu-id="f850c-183">Create the listener.</span><span class="sxs-lookup"><span data-stu-id="f850c-183">Create the listener.</span></span>

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

<span data-ttu-id="f850c-184">Create the rule.</span><span class="sxs-lookup"><span data-stu-id="f850c-184">Create the rule.</span></span>

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a><span data-ttu-id="f850c-185">Step 2</span><span class="sxs-lookup"><span data-stu-id="f850c-185">Step 2</span></span>

<span data-ttu-id="f850c-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span><span class="sxs-lookup"><span data-stu-id="f850c-186">Assign all individual configuration items to an application gateway configuration object ($appgwconfig).</span></span>

<span data-ttu-id="f850c-187">Add the front-end IP to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-187">Add the front-end IP to the configuration.</span></span>

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

<span data-ttu-id="f850c-188">Add the front-end port to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-188">Add the front-end port to the configuration.</span></span>

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
<span data-ttu-id="f850c-189">Add the back-end server pool to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-189">Add the back-end server pool to the configuration.</span></span>

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

<span data-ttu-id="f850c-190">Add the back-end pool setting to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-190">Add the back-end pool setting to the configuration.</span></span>

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

<span data-ttu-id="f850c-191">Add the listener to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-191">Add the listener to the configuration.</span></span>

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

<span data-ttu-id="f850c-192">Add the rule to the configuration.</span><span class="sxs-lookup"><span data-stu-id="f850c-192">Add the rule to the configuration.</span></span>

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a><span data-ttu-id="f850c-193">Step 3</span><span class="sxs-lookup"><span data-stu-id="f850c-193">Step 3</span></span>
<span data-ttu-id="f850c-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="f850c-194">Commit the configuration object to the application gateway resource by using `Set-AzureApplicationGatewayConfig`.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-the-gateway"></a><span data-ttu-id="f850c-195">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="f850c-195">Start the gateway</span></span>

<span data-ttu-id="f850c-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-196">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="f850c-197">Billing for an application gateway begins after the gateway has been successfully started.</span><span class="sxs-lookup"><span data-stu-id="f850c-197">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="f850c-199">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="f850c-199">Verify the gateway status</span></span>

<span data-ttu-id="f850c-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-200">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="f850c-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span><span class="sxs-lookup"><span data-stu-id="f850c-201">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *Vip* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="f850c-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="f850c-202">The following example shows an application gateway that is up, running, and ready to take traffic destined for `http://<generated-dns-name>.cloudapp.net`.</span></span>

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-the-application-gateway"></a><span data-ttu-id="f850c-203">Delete the application gateway</span><span class="sxs-lookup"><span data-stu-id="f850c-203">Delete the application gateway</span></span>

<span data-ttu-id="f850c-204">To delete the application gateway:</span><span class="sxs-lookup"><span data-stu-id="f850c-204">To delete the application gateway:</span></span>

1. <span data-ttu-id="f850c-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-205">Use the `Stop-AzureApplicationGateway` cmdlet to stop the gateway.</span></span>
2. <span data-ttu-id="f850c-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span><span class="sxs-lookup"><span data-stu-id="f850c-206">Use the `Remove-AzureApplicationGateway` cmdlet to remove the gateway.</span></span>
3. <span data-ttu-id="f850c-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f850c-207">Verify that the gateway has been removed by using the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="f850c-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span><span class="sxs-lookup"><span data-stu-id="f850c-208">The following example shows the `Stop-AzureApplicationGateway` cmdlet on the first line, followed by the output.</span></span>

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

<span data-ttu-id="f850c-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span><span class="sxs-lookup"><span data-stu-id="f850c-209">Once the application gateway is in a stopped state, use the `Remove-AzureApplicationGateway` cmdlet to remove the service.</span></span>

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

<span data-ttu-id="f850c-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f850c-210">To verify that the service has been removed, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span> <span data-ttu-id="f850c-211">This step is not required.</span><span class="sxs-lookup"><span data-stu-id="f850c-211">This step is not required.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: The gateway does not exist.
.....
```

## <a name="next-steps"></a><span data-ttu-id="f850c-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="f850c-212">Next steps</span></span>

<span data-ttu-id="f850c-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f850c-213">If you want to configure SSL offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="f850c-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="f850c-214">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

<span data-ttu-id="f850c-215">If you want more information about load balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="f850c-215">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="f850c-216">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="f850c-216">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="f850c-217">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="f850c-217">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
