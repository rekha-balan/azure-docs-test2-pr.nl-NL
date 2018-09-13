---
title: Create a custom probe - Azure Application Gateway - PowerShell classic | Microsoft Docs
description: Learn how to create a custom probe for Application Gateway by using PowerShell in the classic deployment model
services: application-gateway
documentationcenter: na
author: vhorne
manager: jpconnock
editor: ''
tags: azure-service-management
ms.assetid: 338a7be1-835c-48e9-a072-95662dc30f5e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: victorh
ms.openlocfilehash: 97d1376dc7908b72d8e8ec15145229cf3cf4acae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805498"
---
# <a name="create-a-custom-probe-for-azure-application-gateway-classic-by-using-powershell"></a><span data-ttu-id="19565-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span><span class="sxs-lookup"><span data-stu-id="19565-103">Create a custom probe for Azure Application Gateway (classic) by using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-create-probe-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

<span data-ttu-id="19565-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19565-107">In this article, you add a custom probe to an existing application gateway with PowerShell.</span></span> <span data-ttu-id="19565-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span><span class="sxs-lookup"><span data-stu-id="19565-108">Custom probes are useful for applications that have a specific health check page or for applications that do not provide a successful response on the default web application.</span></span>

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. Learn how to [perform these steps using the Resource Manager model](application-gateway-create-probe-ps.md).

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-application-gateway"></a><span data-ttu-id="19565-113">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="19565-113">Create an application gateway</span></span>

<span data-ttu-id="19565-114">To create an application gateway:</span><span class="sxs-lookup"><span data-stu-id="19565-114">To create an application gateway:</span></span>

1. <span data-ttu-id="19565-115">Create an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="19565-115">Create an application gateway resource.</span></span>
2. <span data-ttu-id="19565-116">Create a configuration XML file or a configuration object.</span><span class="sxs-lookup"><span data-stu-id="19565-116">Create a configuration XML file or a configuration object.</span></span>
3. <span data-ttu-id="19565-117">Commit the configuration to the newly created application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="19565-117">Commit the configuration to the newly created application gateway resource.</span></span>

### <a name="create-an-application-gateway-resource-with-a-custom-probe"></a><span data-ttu-id="19565-118">Create an application gateway resource with a custom probe</span><span class="sxs-lookup"><span data-stu-id="19565-118">Create an application gateway resource with a custom probe</span></span>

<span data-ttu-id="19565-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="19565-119">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="19565-120">Billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="19565-120">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="19565-121">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="19565-121">Billing begins in a later step, when the gateway is successfully started.</span></span>

<span data-ttu-id="19565-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span><span class="sxs-lookup"><span data-stu-id="19565-122">The following example creates an application gateway by using a virtual network called "testvnet1" and a subnet called "subnet-1".</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="19565-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="19565-123">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

> [!NOTE]
> The default value for *InstanceCount* is 2, with a maximum value of 10. The default value for *GatewaySize* is Medium. You can choose between Small, Medium, and Large.
> 
> 

<span data-ttu-id="19565-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="19565-127">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="19565-128">These values are created once the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="19565-128">These values are created once the gateway is in the running state.</span></span>

### <a name="configure-an-application-gateway-by-using-xml"></a><span data-ttu-id="19565-129">Configure an application gateway by using XML</span><span class="sxs-lookup"><span data-stu-id="19565-129">Configure an application gateway by using XML</span></span>

<span data-ttu-id="19565-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="19565-130">In the following example, you use an XML file to configure all application gateway settings and commit them to the application gateway resource.</span></span>  

<span data-ttu-id="19565-131">Copy the following text to Notepad.</span><span class="sxs-lookup"><span data-stu-id="19565-131">Copy the following text to Notepad.</span></span>

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

<span data-ttu-id="19565-132">Edit the values between the parentheses for the configuration items.</span><span class="sxs-lookup"><span data-stu-id="19565-132">Edit the values between the parentheses for the configuration items.</span></span> <span data-ttu-id="19565-133">Save the file with extension .xml.</span><span class="sxs-lookup"><span data-stu-id="19565-133">Save the file with extension .xml.</span></span>

<span data-ttu-id="19565-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span><span class="sxs-lookup"><span data-stu-id="19565-134">The following example shows how to use a configuration file to set up the application gateway to load balance HTTP traffic on public port 80 and send network traffic to back-end port 80 between two IP addresses by using a custom probe.</span></span>

> [!IMPORTANT]
> The protocol item Http or Https is case-sensitive.

<span data-ttu-id="19565-136">A new configuration item \<Probe\> is added to configure custom probes.</span><span class="sxs-lookup"><span data-stu-id="19565-136">A new configuration item \<Probe\> is added to configure custom probes.</span></span>

<span data-ttu-id="19565-137">The configuration parameters are:</span><span class="sxs-lookup"><span data-stu-id="19565-137">The configuration parameters are:</span></span>

|<span data-ttu-id="19565-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="19565-138">Parameter</span></span>|<span data-ttu-id="19565-139">Description</span><span class="sxs-lookup"><span data-stu-id="19565-139">Description</span></span>|
|---|---|
|<span data-ttu-id="19565-140">**Name**</span><span class="sxs-lookup"><span data-stu-id="19565-140">**Name**</span></span> |<span data-ttu-id="19565-141">Reference name for custom probe.</span><span class="sxs-lookup"><span data-stu-id="19565-141">Reference name for custom probe.</span></span> |
<span data-ttu-id="19565-142">\* **Protocol**</span><span class="sxs-lookup"><span data-stu-id="19565-142">\* **Protocol**</span></span> | <span data-ttu-id="19565-143">Protocol used (possible values are HTTP or HTTPS).</span><span class="sxs-lookup"><span data-stu-id="19565-143">Protocol used (possible values are HTTP or HTTPS).</span></span>|
| <span data-ttu-id="19565-144">**Host** and **Path**</span><span class="sxs-lookup"><span data-stu-id="19565-144">**Host** and **Path**</span></span> | <span data-ttu-id="19565-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span><span class="sxs-lookup"><span data-stu-id="19565-145">Complete URL path that is invoked by the application gateway to determine the health of the instance.</span></span> <span data-ttu-id="19565-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span><span class="sxs-lookup"><span data-stu-id="19565-146">For example, if you have a website http://contoso.com/, then the custom probe can be configured for "http://contoso.com/path/custompath.htm" for probe checks to have a successful HTTP response.</span></span>|
| <span data-ttu-id="19565-147">**Interval**</span><span class="sxs-lookup"><span data-stu-id="19565-147">**Interval**</span></span> | <span data-ttu-id="19565-148">Configures the probe interval checks in seconds.</span><span class="sxs-lookup"><span data-stu-id="19565-148">Configures the probe interval checks in seconds.</span></span>|
| <span data-ttu-id="19565-149">**Timeout**</span><span class="sxs-lookup"><span data-stu-id="19565-149">**Timeout**</span></span> | <span data-ttu-id="19565-150">Defines the probe time-out for an HTTP response check.</span><span class="sxs-lookup"><span data-stu-id="19565-150">Defines the probe time-out for an HTTP response check.</span></span>|
| <span data-ttu-id="19565-151">**UnhealthyThreshold**</span><span class="sxs-lookup"><span data-stu-id="19565-151">**UnhealthyThreshold**</span></span> | <span data-ttu-id="19565-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span><span class="sxs-lookup"><span data-stu-id="19565-152">The number of failed HTTP responses needed to flag the back-end instance as *unhealthy*.</span></span>|

<span data-ttu-id="19565-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span><span class="sxs-lookup"><span data-stu-id="19565-153">The probe name is referenced in the \<BackendHttpSettings\> configuration to assign which back-end pool uses custom probe settings.</span></span>

## <a name="add-a-custom-probe-to-an-existing-application-gateway"></a><span data-ttu-id="19565-154">Add a custom probe to an existing application gateway</span><span class="sxs-lookup"><span data-stu-id="19565-154">Add a custom probe to an existing application gateway</span></span>

<span data-ttu-id="19565-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span><span class="sxs-lookup"><span data-stu-id="19565-155">Changing the current configuration of an application gateway requires three steps: Get the current XML configuration file, modify to have a custom probe, and configure the application gateway with the new XML settings.</span></span>

1. <span data-ttu-id="19565-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="19565-156">Get the XML file by using `Get-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="19565-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span><span class="sxs-lookup"><span data-stu-id="19565-157">This cmdlet exports the configuration XML to be modified to add a probe setting.</span></span>

  ```powershell
  Get-AzureApplicationGatewayConfig -Name "<application gateway name>" -Exporttofile "<path to file>"
  ```

1. <span data-ttu-id="19565-158">Open the XML file in a text editor.</span><span class="sxs-lookup"><span data-stu-id="19565-158">Open the XML file in a text editor.</span></span> <span data-ttu-id="19565-159">Add a `<probe>` section after `<frontendport>`.</span><span class="sxs-lookup"><span data-stu-id="19565-159">Add a `<probe>` section after `<frontendport>`.</span></span>

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

  <span data-ttu-id="19565-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="19565-160">In the backendHttpSettings section of the XML, add the probe name as shown in the following example:</span></span>

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

  <span data-ttu-id="19565-161">Save the XML file.</span><span class="sxs-lookup"><span data-stu-id="19565-161">Save the XML file.</span></span>

1. <span data-ttu-id="19565-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span><span class="sxs-lookup"><span data-stu-id="19565-162">Update the application gateway configuration with the new XML file by using `Set-AzureApplicationGatewayConfig`.</span></span> <span data-ttu-id="19565-163">This cmdlet updates your application gateway with the new configuration.</span><span class="sxs-lookup"><span data-stu-id="19565-163">This cmdlet updates your application gateway with the new configuration.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name "<application gateway name>" -Configfile "<path to file>"
```

## <a name="next-steps"></a><span data-ttu-id="19565-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="19565-164">Next steps</span></span>

<span data-ttu-id="19565-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="19565-165">If you want to configure Secure Sockets Layer (SSL) offload, see [Configure an application gateway for SSL offload](application-gateway-ssl.md).</span></span>

<span data-ttu-id="19565-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span><span class="sxs-lookup"><span data-stu-id="19565-166">If you want to configure an application gateway to use with an internal load balancer, see [Create an application gateway with an internal load balancer (ILB)](application-gateway-ilb.md).</span></span>

