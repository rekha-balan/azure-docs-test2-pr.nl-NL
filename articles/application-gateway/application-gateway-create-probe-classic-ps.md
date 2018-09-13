---
title: Create a custom probe - Azure Application Gateway - PowerShell classic | Microsoft Docs
description: Learn how to create a custom probe for Application Gateway by using PowerShell in the classic deployment model
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 4787a382b837b71a28c45211a26aa512e8fb177e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660849"
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="ae579-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae579-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)


[!INCLUDE [azure-probe-intro-include](../../includes/application-gateway-create-probe-intro-include.md)]

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="ae579-111">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="ae579-111">Create an application gateway</span></span>

<span data-ttu-id="ae579-112">To create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="ae579-112">To create an application gateway:</span></span>

1. <span data-ttu-id="ae579-113">Create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="ae579-113">Create an application gateway resource.</span></span>
2. <span data-ttu-id="ae579-114">Create a configuration XML file or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="ae579-114">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="ae579-115">Commit the configuration to the newly created application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="ae579-115">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource"></a><span data-ttu-id="ae579-116">Create an application gateway resource</span><span class="sxs-lookup"><span data-stu-id="ae579-116">Create an application gateway resource</span></span>

<span data-ttu-id="ae579-117">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="ae579-117">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="ae579-118">Billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="ae579-118">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="ae579-119">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="ae579-119">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="ae579-120">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="ae579-120">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="ae579-121">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ae579-121">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> The default value for *InstanceCount* is 2, with a maximum value of 10. The default value for *GatewaySize* is Medium. You can choose between Small, Medium, and Large.
> 
> 

<span data-ttu-id="ae579-125">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="ae579-125">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="ae579-126">These values are created once the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="ae579-126">These values are created once the gateway is in the running state.</span></span>

## <a name="configure-an-application-gateway"></a><span data-ttu-id="ae579-127">Configure an application gateway</span><span class="sxs-lookup"><span data-stu-id="ae579-127">Configure an application gateway</span></span>

<span data-ttu-id="ae579-128">You can configure the application gateway by using XML or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="ae579-128">You can configure the application gateway by using XML or a configuration object.</span></span>

## <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="ae579-129">Configure an application gateway by using XML</span><span class="sxs-lookup"><span data-stu-id="ae579-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="ae579-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="ae579-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

### <a name="step-1"></a><span data-ttu-id="ae579-131">Step 1</span><span class="sxs-lookup"><span data-stu-id="ae579-131">Step 1</span></span>

<span data-ttu-id="ae579-132">Copy the following text to Notepad.</span><span class="sxs-lookup"><span data-stu-id="ae579-132">Copy the following text to Notepad.</span></span>

```xml
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
<FrontendIPConfigurations>
    <FrontendIPConfiguration>
        <Name>fip1</Name>
        <Type>Private</Type>
    </FrontendIPConfiguration>
</FrontendIPConfigurations>
<FrontendPorts>
    <FrontendPort>
        <Name>port1</Name>
        <Port>80</Port>
    </FrontendPort>
</FrontendPorts>
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
    </Probes>
    <BackendAddressPools>
    <BackendAddressPool>
        <Name>pool1</Name>
        <IPAddresses>
            <IPAddress>1.1.1.1</IPAddress>
            <IPAddress>2.2.2.2</IPAddress>
        </IPAddresses>
    </BackendAddressPool>
</BackendAddressPools>
<BackendHttpSettingsList>
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
</BackendHttpSettingsList>
<HttpListeners>
    <HttpListener>
        <Name>listener1</Name>
        <FrontendIP>fip1</FrontendIP>
    <FrontendPort>port1</FrontendPort>
        <Protocol>Http</Protocol>
    </HttpListener>
</HttpListeners>
<HttpLoadBalancingRules>
    <HttpLoadBalancingRule>
        <Name>lbrule1</Name>
        <Type>basic</Type>
        <BackendHttpSettings>setting1</BackendHttpSettings>
        <Listener>listener1</Listener>
        <BackendAddressPool>pool1</BackendAddressPool>
    </HttpLoadBalancingRule>
</HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

<span data-ttu-id="ae579-133">Edit the values between the parentheses for the configuration items.</span><span class="sxs-lookup"><span data-stu-id="ae579-133">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="ae579-134">Save the file with extension .xml.</span><span class="sxs-lookup"><span data-stu-id="ae579-134">Save the file with extension .xml.</span></span>

<span data-ttu-id="ae579-135">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span><span class="sxs-lookup"><span data-stu-id="ae579-135">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> The protocol item Http or Https is case-sensitive.

<span data-ttu-id="ae579-137">A new configuration item \<Probe\> is added to configure custom probes.</span><span class="sxs-lookup"><span data-stu-id="ae579-137">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="ae579-138">The configuration parameters are:</span><span class="sxs-lookup"><span data-stu-id="ae579-138">The configuration parameters are:</span></span>

* <span data-ttu-id="ae579-139">**Name** - Reference name for custom probe.</span><span class="sxs-lookup"><span data-stu-id="ae579-139">**Name** - Reference name for custom probe.</span></span>
* <span data-ttu-id="ae579-140">**Protocol** - Protocol used (possible values are HTTP or HTTPS).</span><span class="sxs-lookup"><span data-stu-id="ae579-140">**Protocol** - Protocol used (possible values are HTTP or HTTPS).</span></span>
* <span data-ttu-id="ae579-141">**Host** and **Path** - Complete URL path that is invoked by the application gateway to determine the health of the instance.</span><span class="sxs-lookup"><span data-stu-id="ae579-141">**Host** and **Path** - Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="ae579-142">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span><span class="sxs-lookup"><span data-stu-id="ae579-142">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>
* <span data-ttu-id="ae579-143">**Interval** - Configures the probe interval checks in seconds.</span><span class="sxs-lookup"><span data-stu-id="ae579-143">**Interval** - Configures the probe interval checks in seconds.</span></span>
* <span data-ttu-id="ae579-144">**Timeout** - Defines the probe time-out for an HTTP response check.</span><span class="sxs-lookup"><span data-stu-id="ae579-144">**Timeout** - Defines the probe time-out for an HTTP response check.</span></span>
* <span data-ttu-id="ae579-145">**UnhealthyThreshold** - The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span><span class="sxs-lookup"><span data-stu-id="ae579-145">**UnhealthyThreshold** - The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>

<span data-ttu-id="ae579-146">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span><span class="sxs-lookup"><span data-stu-id="ae579-146">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-configuration-to-an-existing-application-gateway"></a><span data-ttu-id="ae579-147">Add a custom probe configuration to an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="ae579-147">Add a custom probe configuration to an existing application gateway</span></span>

<span data-ttu-id="ae579-148">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span><span class="sxs-lookup"><span data-stu-id="ae579-148">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

### <a name="step-1"></a><span data-ttu-id="ae579-149">Step 1</span><span class="sxs-lookup"><span data-stu-id="ae579-149">Step 1</span></span>

<span data-ttu-id="ae579-150">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="ae579-150">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="ae579-151">This cmdlet exports the configuration XML to be modified to add a probe setting.</span><span class="sxs-lookup"><span data-stu-id="ae579-151">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

```powershell
Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
```

### <a name="step-2"></a><span data-ttu-id="ae579-152">Step 2</span><span class="sxs-lookup"><span data-stu-id="ae579-152">Step 2</span></span>

<span data-ttu-id="ae579-153">Open the XML file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="ae579-153">Open the XML file in a text editor.</span></span> <span data-ttu-id="ae579-154">Add a `<probe>` section after `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="ae579-154">Add a `<probe>` section after `<frontendport>`.</span></span>

```xml
<Probes>
    <Probe>
        <Name>Probe01</Name>
        <Protocol>Http</Protocol>
        <Host>contoso.com</Host>
        <Path>/path/custompath.htm</Path>
        <Interval>15</Interval>
        <Timeout>15</Timeout>
        <UnhealthyThreshold>5</UnhealthyThreshold>
    </Probe>
</Probes>
```

<span data-ttu-id="ae579-155">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="ae579-155">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

```xml
    <BackendHttpSettings>
        <Name>setting1</Name>
        <Port>80</Port>
        <Protocol>Http</Protocol>
        <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        <RequestTimeout>120</RequestTimeout>
        <Probe>Probe01</Probe>
    </BackendHttpSettings>
```

<span data-ttu-id="ae579-156">Save the XML file.</span><span class="sxs-lookup"><span data-stu-id="ae579-156">Save the XML file.</span></span>

### <a name="step-3"></a><span data-ttu-id="ae579-157">Step 3</span><span class="sxs-lookup"><span data-stu-id="ae579-157">Step 3</span></span>

<span data-ttu-id="ae579-158">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="ae579-158">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="ae579-159">This cmdlet updates your application gateway with the new configuration.</span><span class="sxs-lookup"><span data-stu-id="ae579-159">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="ae579-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="ae579-160">Next steps</span></span>

<span data-ttu-id="ae579-161">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="ae579-161">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="ae579-162">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="ae579-162">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

