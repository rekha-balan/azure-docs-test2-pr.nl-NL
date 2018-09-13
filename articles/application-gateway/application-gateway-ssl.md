---
title: Configure SSL offload - Azure Application Gateway - PowerShell classic | Microsoft Docs
description: This article provides instructions to create an application gateway with SSL offload by using the Azure classic deployment model
documentationcenter: na
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.assetid: 63f28d96-9c47-410e-97dd-f5ca1ad1b8a4
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: victorh
ms.openlocfilehash: e620730b86d648c1ac9db7a9e6faa7a2d206b46e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44781279"
---
# <a name="configure-an-application-gateway-for-ssl-offload-by-using-the-classic-deployment-model"></a><span data-ttu-id="8a255-103">Configure an application gateway for SSL offload by using the classic deployment model</span><span class="sxs-lookup"><span data-stu-id="8a255-103">Configure an application gateway for SSL offload by using the classic deployment model</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](application-gateway-ssl-portal.md)
> * [Azure Resource Manager PowerShell](application-gateway-ssl-arm.md)
> * [Azure classic PowerShell](application-gateway-ssl.md)
> * [Azure CLI 2.0](application-gateway-ssl-cli.md)

<span data-ttu-id="8a255-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span><span class="sxs-lookup"><span data-stu-id="8a255-108">Azure Application Gateway can be configured to terminate the Secure Sockets Layer (SSL) session at the gateway to avoid costly SSL decryption tasks to happen at the web farm.</span></span> <span data-ttu-id="8a255-109">SSL offload also simplifies the front-end server setup and management of the web application.</span><span class="sxs-lookup"><span data-stu-id="8a255-109">SSL offload also simplifies the front-end server setup and management of the web application.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8a255-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="8a255-110">Before you begin</span></span>

1. <span data-ttu-id="8a255-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="8a255-111">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="8a255-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8a255-112">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="8a255-113">Verify that you have a working virtual network with a valid subnet.</span><span class="sxs-lookup"><span data-stu-id="8a255-113">Verify that you have a working virtual network with a valid subnet.</span></span> <span data-ttu-id="8a255-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span><span class="sxs-lookup"><span data-stu-id="8a255-114">Make sure that no virtual machines or cloud deployments are using the subnet.</span></span> <span data-ttu-id="8a255-115">The application gateway must be by itself in a virtual network subnet.</span><span class="sxs-lookup"><span data-stu-id="8a255-115">The application gateway must be by itself in a virtual network subnet.</span></span>
3. <span data-ttu-id="8a255-116">The servers that you configure to use the application gateway must exist or have their endpoints that are created either in the virtual network or with a public IP address or virtual IP address (VIP) assigned.</span><span class="sxs-lookup"><span data-stu-id="8a255-116">The servers that you configure to use the application gateway must exist or have their endpoints that are created either in the virtual network or with a public IP address or virtual IP address (VIP) assigned.</span></span>

<span data-ttu-id="8a255-117">To configure SSL offload on an application gateway, complete the following steps in the order listed:</span><span class="sxs-lookup"><span data-stu-id="8a255-117">To configure SSL offload on an application gateway, complete the following steps in the order listed:</span></span>

1. [<span data-ttu-id="8a255-118">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-118">Create an application gateway</span></span>](#create-an-application-gateway)
2. [<span data-ttu-id="8a255-119">Upload SSL certificates</span><span class="sxs-lookup"><span data-stu-id="8a255-119">Upload SSL certificates</span></span>](#upload-ssl-certificates)
3. [<span data-ttu-id="8a255-120">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-120">Configure the gateway</span></span>](#configure-the-gateway)
4. [<span data-ttu-id="8a255-121">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="8a255-121">Set the gateway configuration</span></span>](#set-the-gateway-configuration)
5. [<span data-ttu-id="8a255-122">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-122">Start the gateway</span></span>](#start-the-gateway)
6. [<span data-ttu-id="8a255-123">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="8a255-123">Verify the gateway status</span></span>](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a><span data-ttu-id="8a255-124">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-124">Create an application gateway</span></span>

<span data-ttu-id="8a255-125">To create the gateway, enter the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span><span class="sxs-lookup"><span data-stu-id="8a255-125">To create the gateway, enter the `New-AzureApplicationGateway` cmdlet, replacing the values with your own.</span></span> <span data-ttu-id="8a255-126">Billing for the gateway does not start at this point.</span><span class="sxs-lookup"><span data-stu-id="8a255-126">Billing for the gateway does not start at this point.</span></span> <span data-ttu-id="8a255-127">Billing begins in a later step, when the gateway is successfully started.</span><span class="sxs-lookup"><span data-stu-id="8a255-127">Billing begins in a later step, when the gateway is successfully started.</span></span>

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

<span data-ttu-id="8a255-128">To validate that the gateway was created, you can enter the `Get-AzureApplicationGateway` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a255-128">To validate that the gateway was created, you can enter the `Get-AzureApplicationGateway` cmdlet.</span></span>

<span data-ttu-id="8a255-129">In the sample, **Description**, **InstanceCount**, and **GatewaySize** are optional parameters.</span><span class="sxs-lookup"><span data-stu-id="8a255-129">In the sample, **Description**, **InstanceCount**, and **GatewaySize** are optional parameters.</span></span> <span data-ttu-id="8a255-130">The default value for **InstanceCount** is **2**, with a maximum value of **10**.</span><span class="sxs-lookup"><span data-stu-id="8a255-130">The default value for **InstanceCount** is **2**, with a maximum value of **10**.</span></span> <span data-ttu-id="8a255-131">The default value for **GatewaySize** is **Medium**.</span><span class="sxs-lookup"><span data-stu-id="8a255-131">The default value for **GatewaySize** is **Medium**.</span></span> <span data-ttu-id="8a255-132">Small and Large are other available values.</span><span class="sxs-lookup"><span data-stu-id="8a255-132">Small and Large are other available values.</span></span> <span data-ttu-id="8a255-133">**VirtualIPs** and **DnsName** are shown as blank, because the gateway has not started yet.</span><span class="sxs-lookup"><span data-stu-id="8a255-133">**VirtualIPs** and **DnsName** are shown as blank, because the gateway has not started yet.</span></span> <span data-ttu-id="8a255-134">These values are created after the gateway is in the running state.</span><span class="sxs-lookup"><span data-stu-id="8a255-134">These values are created after the gateway is in the running state.</span></span>

```powershell
Get-AzureApplicationGateway AppGwTest
```

## <a name="upload-ssl-certificates"></a><span data-ttu-id="8a255-135">Upload SSL certificates</span><span class="sxs-lookup"><span data-stu-id="8a255-135">Upload SSL certificates</span></span>

<span data-ttu-id="8a255-136">Enter `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in PFX format to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-136">Enter `Add-AzureApplicationGatewaySslCertificate` to upload the server certificate in PFX format to the application gateway.</span></span> <span data-ttu-id="8a255-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-137">The certificate name is a user-chosen name and must be unique within the application gateway.</span></span> <span data-ttu-id="8a255-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-138">This certificate is referred to by this name in all certificate management operations on the application gateway.</span></span>

<span data-ttu-id="8a255-139">The following sample shows the cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a255-139">The following sample shows the cmdlet.</span></span> <span data-ttu-id="8a255-140">Replace the values in the sample with your own.</span><span class="sxs-lookup"><span data-stu-id="8a255-140">Replace the values in the sample with your own.</span></span>

```powershell
Add-AzureApplicationGatewaySslCertificate  -Name AppGwTest -CertificateName GWCert -Password <password> -CertificateFile <full path to pfx file>
```

<span data-ttu-id="8a255-141">Next, validate the certificate upload.</span><span class="sxs-lookup"><span data-stu-id="8a255-141">Next, validate the certificate upload.</span></span> <span data-ttu-id="8a255-142">Enter the `Get-AzureApplicationGatewayCertificate` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8a255-142">Enter the `Get-AzureApplicationGatewayCertificate` cmdlet.</span></span>

<span data-ttu-id="8a255-143">The following sample shows the cmdlet on the first line, followed by the output:</span><span class="sxs-lookup"><span data-stu-id="8a255-143">The following sample shows the cmdlet on the first line, followed by the output:</span></span>

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
> The certificate password must be between 4 to 12 characters made up of letters or numbers. Special characters are not accepted.

## <a name="configure-the-gateway"></a><span data-ttu-id="8a255-146">Configure the gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-146">Configure the gateway</span></span>

<span data-ttu-id="8a255-147">An application gateway configuration consists of multiple values.</span><span class="sxs-lookup"><span data-stu-id="8a255-147">An application gateway configuration consists of multiple values.</span></span> <span data-ttu-id="8a255-148">The values can be tied together to construct the configuration.</span><span class="sxs-lookup"><span data-stu-id="8a255-148">The values can be tied together to construct the configuration.</span></span>

<span data-ttu-id="8a255-149">The values are:</span><span class="sxs-lookup"><span data-stu-id="8a255-149">The values are:</span></span>

* <span data-ttu-id="8a255-150">**Back-end server pool**: The list of IP addresses of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="8a255-150">**Back-end server pool**: The list of IP addresses of the back-end servers.</span></span> <span data-ttu-id="8a255-151">The IP addresses listed should belong to the virtual network subnet or should be a public IP or VIP address.</span><span class="sxs-lookup"><span data-stu-id="8a255-151">The IP addresses listed should belong to the virtual network subnet or should be a public IP or VIP address.</span></span>
* <span data-ttu-id="8a255-152">**Back-end server pool settings**: Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="8a255-152">**Back-end server pool settings**: Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="8a255-153">These settings are tied to a pool and are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="8a255-153">These settings are tied to a pool and are applied to all servers within the pool.</span></span>
* <span data-ttu-id="8a255-154">**Front-end port**: This port is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-154">**Front-end port**: This port is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="8a255-155">Traffic hits this port, and then gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="8a255-155">Traffic hits this port, and then gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="8a255-156">**Listener**: The listener has a front-end port, a protocol (Http or Https; these values are case-sensitive), and the SSL certificate name (if configuring an SSL offload).</span><span class="sxs-lookup"><span data-stu-id="8a255-156">**Listener**: The listener has a front-end port, a protocol (Http or Https; these values are case-sensitive), and the SSL certificate name (if configuring an SSL offload).</span></span>
* <span data-ttu-id="8a255-157">**Rule**: The rule binds the listener and the back-end server pool and defines which back-end server pool to direct the traffic to when it hits a particular listener.</span><span class="sxs-lookup"><span data-stu-id="8a255-157">**Rule**: The rule binds the listener and the back-end server pool and defines which back-end server pool to direct the traffic to when it hits a particular listener.</span></span> <span data-ttu-id="8a255-158">Currently, only the *basic* rule is supported.</span><span class="sxs-lookup"><span data-stu-id="8a255-158">Currently, only the *basic* rule is supported.</span></span> <span data-ttu-id="8a255-159">The *basic* rule is round-robin load distribution.</span><span class="sxs-lookup"><span data-stu-id="8a255-159">The *basic* rule is round-robin load distribution.</span></span>

<span data-ttu-id="8a255-160">**Additional configuration notes**</span><span class="sxs-lookup"><span data-stu-id="8a255-160">**Additional configuration notes**</span></span>

<span data-ttu-id="8a255-161">For SSL certificates configuration, the protocol in **HttpListener** should change to **Https** (case sensitive).</span><span class="sxs-lookup"><span data-stu-id="8a255-161">For SSL certificates configuration, the protocol in **HttpListener** should change to **Https** (case sensitive).</span></span> <span data-ttu-id="8a255-162">Add the **SslCert** element to **HttpListener** with the value set to the same name used in the [Upload SSL certificates](#upload-ssl-certificates) section.</span><span class="sxs-lookup"><span data-stu-id="8a255-162">Add the **SslCert** element to **HttpListener** with the value set to the same name used in the [Upload SSL certificates](#upload-ssl-certificates) section.</span></span> <span data-ttu-id="8a255-163">The front-end port should be updated to **443**.</span><span class="sxs-lookup"><span data-stu-id="8a255-163">The front-end port should be updated to **443**.</span></span>

<span data-ttu-id="8a255-164">**To enable cookie-based affinity**: You can configure an application gateway to ensure that a request from a client session is always directed to the same VM in the web farm.</span><span class="sxs-lookup"><span data-stu-id="8a255-164">**To enable cookie-based affinity**: You can configure an application gateway to ensure that a request from a client session is always directed to the same VM in the web farm.</span></span> <span data-ttu-id="8a255-165">To accomplish this, insert a session cookie that allows the gateway to direct traffic appropriately.</span><span class="sxs-lookup"><span data-stu-id="8a255-165">To accomplish this, insert a session cookie that allows the gateway to direct traffic appropriately.</span></span> <span data-ttu-id="8a255-166">To enable cookie-based affinity, set **CookieBasedAffinity** to **Enabled** in the **BackendHttpSettings** element.</span><span class="sxs-lookup"><span data-stu-id="8a255-166">To enable cookie-based affinity, set **CookieBasedAffinity** to **Enabled** in the **BackendHttpSettings** element.</span></span>

<span data-ttu-id="8a255-167">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="8a255-167">You can construct your configuration either by creating a configuration object or by using a configuration XML file.</span></span>
<span data-ttu-id="8a255-168">To construct your configuration by using a configuration XML file, enter the following sample:</span><span class="sxs-lookup"><span data-stu-id="8a255-168">To construct your configuration by using a configuration XML file, enter the following sample:</span></span>


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

## <a name="set-the-gateway-configuration"></a><span data-ttu-id="8a255-169">Set the gateway configuration</span><span class="sxs-lookup"><span data-stu-id="8a255-169">Set the gateway configuration</span></span>

<span data-ttu-id="8a255-170">Next, set the application gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-170">Next, set the application gateway.</span></span> <span data-ttu-id="8a255-171">You can enter the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or a configuration XML file.</span><span class="sxs-lookup"><span data-stu-id="8a255-171">You can enter the `Set-AzureApplicationGatewayConfig` cmdlet with either a configuration object or a configuration XML file.</span></span>

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

## <a name="start-the-gateway"></a><span data-ttu-id="8a255-172">Start the gateway</span><span class="sxs-lookup"><span data-stu-id="8a255-172">Start the gateway</span></span>

<span data-ttu-id="8a255-173">After the gateway has been configured, enter the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-173">After the gateway has been configured, enter the `Start-AzureApplicationGateway` cmdlet to start the gateway.</span></span> <span data-ttu-id="8a255-174">Billing for an application gateway begins after the gateway has been successfully started.</span><span class="sxs-lookup"><span data-stu-id="8a255-174">Billing for an application gateway begins after the gateway has been successfully started.</span></span>

> [!NOTE]
> The `Start-AzureApplicationGateway` cmdlet can take 15-20 minutes to finish.
>
>

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-the-gateway-status"></a><span data-ttu-id="8a255-176">Verify the gateway status</span><span class="sxs-lookup"><span data-stu-id="8a255-176">Verify the gateway status</span></span>

<span data-ttu-id="8a255-177">Enter the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span><span class="sxs-lookup"><span data-stu-id="8a255-177">Enter the `Get-AzureApplicationGateway` cmdlet to check the status of the gateway.</span></span> <span data-ttu-id="8a255-178">If `Start-AzureApplicationGateway` succeeded in the previous step, the **State** should be **Running**, and the **VirtualIPs** and **DnsName** should have valid entries.</span><span class="sxs-lookup"><span data-stu-id="8a255-178">If `Start-AzureApplicationGateway` succeeded in the previous step, the **State** should be **Running**, and the **VirtualIPs** and **DnsName** should have valid entries.</span></span>

<span data-ttu-id="8a255-179">This sample shows an application gateway that is up, running, and ready to take traffic:</span><span class="sxs-lookup"><span data-stu-id="8a255-179">This sample shows an application gateway that is up, running, and ready to take traffic:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8a255-180">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a255-180">Next steps</span></span>

<span data-ttu-id="8a255-181">For more information about load-balancing options in general, see:</span><span class="sxs-lookup"><span data-stu-id="8a255-181">For more information about load-balancing options in general, see:</span></span>

* [<span data-ttu-id="8a255-182">Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="8a255-182">Azure Load Balancer</span></span>](https://azure.microsoft.com/documentation/services/load-balancer/)
* [<span data-ttu-id="8a255-183">Azure Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="8a255-183">Azure Traffic Manager</span></span>](https://azure.microsoft.com/documentation/services/traffic-manager/)
