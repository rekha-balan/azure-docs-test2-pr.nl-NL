---
title: Configure SSL offload - Azure Application Gateway - PowerShell classic | Microsoft Docs
description: This article provides instructions to create an application gateway with SSL offload by using the Azure classic deployment model.
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 9c56914091ecac3eb97977dd5afc2dc4588a052c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662217"
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="be27e-103">Configure an application gateway for SSL offload by using the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="be27e-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure Classic PowerShell](application-gateway-ssl.md)

<span data-ttu-id="be27e-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span><span class="sxs-lookup"><span data-stu-id="be27e-107">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="be27e-108">SSL offload also simplifies the front-end server setup and management of the web application.</span><span class="sxs-lookup"><span data-stu-id="be27e-108">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="be27e-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="be27e-109">Before you begin</span></span>

1. <span data-ttu-id="be27e-110">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="be27e-110">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="be27e-111">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="be27e-111">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="be27e-112">Verify that you have a working virtual network with a valid subnet.</span><span class="sxs-lookup"><span data-stu-id="be27e-112">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="be27e-113">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="be27e-113">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="be27e-114">The application gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="be27e-114">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="be27e-115">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span><span class="sxs-lookup"><span data-stu-id="be27e-115">The servers that you configure to use the application gateway must exist or have their endpoints created either in the virtual network or with a public IP/VIP assigned.</span></span>

<span data-ttu-id="be27e-116">To configure SSL offload on an application gateway, do the following steps in the order listed:</span><span class="sxs-lookup"><span data-stu-id="be27e-116">To configure SSL offload on an application gateway, do the following steps in the order listed:</span></span>

1. [<span data-ttu-id="be27e-117">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-117">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="be27e-118">Upload SSL certificates</span><span class="sxs-lookup"><span data-stu-id="be27e-118">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="be27e-119">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-119">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="be27e-120">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="be27e-120">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="be27e-121">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-121">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="be27e-122">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="be27e-122">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="be27e-123">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-123">Create an application gateway</span></span>

<span data-ttu-id="be27e-124">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="be27e-124">To create the gateway, use the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="be27e-125">Billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="be27e-125">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="be27e-126">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="be27e-126">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="be27e-127">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be27e-127">To validate that the gateway was created, you can use the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="be27e-128">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span><span class="sxs-lookup"><span data-stu-id="be27e-128">In the sample, *Description*, *InstanceCount*, and *GatewaySize* are optional parameters.</span></span> <span data-ttu-id="be27e-129">The default value for *InstanceCount* is 2, with a maximum value of 10.</span><span class="sxs-lookup"><span data-stu-id="be27e-129">The default value for *InstanceCount* is 2, with a maximum value of 10.</span></span> <span data-ttu-id="be27e-130">The default value for *GatewaySize* is Medium.</span><span class="sxs-lookup"><span data-stu-id="be27e-130">The default value for *GatewaySize* is Medium.</span></span> <span data-ttu-id="be27e-131">Small and Large are other available values.</span><span class="sxs-lookup"><span data-stu-id="be27e-131">Small and Large are other available values.</span></span> <span data-ttu-id="be27e-132">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="be27e-132">*VirtualIPs* and *DnsName* are shown as blank because the gateway has not started yet.</span></span> <span data-ttu-id="be27e-133">These values are created once the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="be27e-133">These values are created once the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="be27e-134">Upload SSL certificates</span><span class="sxs-lookup"><span data-stu-id="be27e-134">Upload SSL certificates</span></span>

<span data-ttu-id="be27e-135">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-135">Use `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in *pfx* format to the application gateway.</span></span> <span data-ttu-id="be27e-136">The certificate name is a user-chosen name and must be unique within the application gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-136">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="be27e-137">This certificate is referred to by this name in all certificate management operations on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-137">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="be27e-138">This following sample shows the cmdlet, replace the values in the sample with your own.</span><span class="sxs-lookup"><span data-stu-id="be27e-138">This following sample shows the cmdlet, replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="be27e-139">Next, validate the certificate upload.</span><span class="sxs-lookup"><span data-stu-id="be27e-139">Next, validate the certificate upload.</span></span> <span data-ttu-id="be27e-140">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="be27e-140">Use the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="be27e-141">This sample shows the cmdlet on the first line, followed by the output.</span><span class="sxs-lookup"><span data-stu-id="be27e-141">This sample shows the cmdlet on the first line, followed by the output.</span></span>

```powershell
Get-AzureApplicationGatewaySslCertificate AppGwTest
```

```
VERBOSE: 5:07:54 PM - Begin Operation: Get-AzureApplicationGatewaySslCertificate
VERBOSE: 5:07:55 PM - Completed Operation: Get-AzureApplicationGatewaySslCertificate
Name           : SslCert
SubjectName    : CN=gwcert.app.test.contoso.com
Thumbprint     : AF5ADD77E160A01A6......EE48D1A
ThumbprintAlgo : sha1RSA
State..........: Provisioned
```

> [!NOTE]
> The certificate password has to be between 4 to 12 characters, letters, or numbers. Special characters are not accepted.

## <a name="configure-the-gateway"></a><span data-ttu-id="be27e-144">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-144">Configure the gateway</span></span>

<span data-ttu-id="be27e-145">An application gateway configuration consists of multiple values.</span><span class="sxs-lookup"><span data-stu-id="be27e-145">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="be27e-146">The values can be tied together to construct the configuration.</span><span class="sxs-lookup"><span data-stu-id="be27e-146">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="be27e-147">The values are:</span><span class="sxs-lookup"><span data-stu-id="be27e-147">The values are:</span></span>

* <span data-ttu-id="be27e-148">**Back-end server pool:** The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="be27e-148">**Back-end server pool:** The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="be27e-149">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span><span class="sxs-lookup"><span data-stu-id="be27e-149">The IP addresses listed should either belong to the virtual network subnet or should be a public IP/VIP.</span></span>
* <span data-ttu-id="be27e-150">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="be27e-150">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="be27e-151">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="be27e-151">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="be27e-152">**Front-end port:** This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-152">**Front-end port:** This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="be27e-153">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="be27e-153">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="be27e-154">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="be27e-154">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="be27e-155">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="be27e-155">**Rule:** The rule binds the listener and the back-end server pool and defines which back-end server pool the traffic should be directed to when it hits a particular listener.</span></span> <span data-ttu-id="be27e-156">Currently, only the *basic* rule is supported.</span><span class="sxs-lookup"><span data-stu-id="be27e-156">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="be27e-157">The *basic* rule is round-robin load distribution.</span><span class="sxs-lookup"><span data-stu-id="be27e-157">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="be27e-158">**Additional configuration notes**</span><span class="sxs-lookup"><span data-stu-id="be27e-158">**Additional configuration notes**</span></span>

<span data-ttu-id="be27e-159">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span><span class="sxs-lookup"><span data-stu-id="be27e-159">For SSL certificates configuration, the protocol in **HttpListener** should change to *Https* (case sensitive).</span></span> <span data-ttu-id="be27e-160">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span><span class="sxs-lookup"><span data-stu-id="be27e-160">The **SslCert** element is added to **HttpListener** with the value set to the same name as used in the upload of preceding SSL certificates section.</span></span> <span data-ttu-id="be27e-161">The front-end port should be updated to 443.</span><span class="sxs-lookup"><span data-stu-id="be27e-161">The front-end port should be updated to 443.</span></span>

<span data-ttu-id="be27e-162">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span><span class="sxs-lookup"><span data-stu-id="be27e-162">**To enable cookie-based affinity**: An application gateway can be configured to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="be27e-163">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span><span class="sxs-lookup"><span data-stu-id="be27e-163">This scenario is done by injection of a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="be27e-164">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span><span class="sxs-lookup"><span data-stu-id="be27e-164">To enable cookie-based affinity, set **CookieBasedAffinity** to *Enabled* in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="be27e-165">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="be27e-165">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="be27e-166">To construct your configuration by using a configuration XML file, use the following sample:</span><span class="sxs-lookup"><span data-stu-id="be27e-166">To construct your configuration by using a configuration XML file, use the following sample:</span></span>

<span data-ttu-id="be27e-167">**Configuration XML sample**</span><span class="sxs-lookup"><span data-stu-id="be27e-167">**Configuration XML sample**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations />
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>443</Port>
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
            <Protocol>Https</Protocol>
            <SslCert>GWCert</SslCert>
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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="be27e-168">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="be27e-168">Set the gateway configuration</span></span>

<span data-ttu-id="be27e-169">Next, you set the application gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-169">Next, you set the application gateway.</span></span> <span data-ttu-id="be27e-170">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="be27e-170">You can use the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or with a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="be27e-171">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="be27e-171">Start the gateway</span></span>

<span data-ttu-id="be27e-172">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-172">Once the gateway has been configured, use the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="be27e-173">Billing for an application gateway begins after the gateway has been successfully started.</span><span class="sxs-lookup"><span data-stu-id="be27e-173">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> The `Start-AzureApplicationGateway` cmdlet might take up to 15-20 minutes to finish.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="be27e-175">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="be27e-175">Verify the gateway status</span></span>

<span data-ttu-id="be27e-176">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span><span class="sxs-lookup"><span data-stu-id="be27e-176">Use the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="be27e-177">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span><span class="sxs-lookup"><span data-stu-id="be27e-177">If `Start-AzureApplicationGateway` succeeded in the previous step, *State* should be Running, and *VirtualIPs* and *DnsName* should have valid entries.</span></span>

<span data-ttu-id="be27e-178">This sample shows an application gateway that is up, running, and is ready to take traffic.</span><span class="sxs-lookup"><span data-stu-id="be27e-178">This sample shows an application gateway that is up, running, and is ready to take traffic.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest2
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {23.96.22.241}
DnsName       : appgw-4c960426-d1e6-4aae-8670-81fd7a519a43.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="be27e-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="be27e-179">Next steps</span></span>

<span data-ttu-id="be27e-180">If you want more information about load balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="be27e-180">If you want more information about load balancing options in general, see:</span></span>

* [<span data-ttu-id="be27e-181">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="be27e-181">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="be27e-182">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="be27e-182">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)

