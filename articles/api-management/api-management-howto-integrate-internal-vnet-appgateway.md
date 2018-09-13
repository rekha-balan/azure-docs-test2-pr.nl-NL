---
title: How to use Azure API Management in Virtual Network with Application Gateway | Microsoft Docs
description: Learn how to setup and configure Azure API Management in Internal Virtual Network with Application Gateway (WAF) as FrontEnd
services: api-management
documentationcenter: ''
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 3fc30ae699dcf99e49fd7a4b948d5c3f4aa08a5b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554547"
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Integrate API Management in an internal VNET with Application Gateway 

##<a name="overview"> </a> Overview
 
The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network. Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer. It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).

Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:

* Use the same API Management resource for consumption by both internal consumers and external consumers.
* Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.
* Provide a turn-key way to switch access to API Management from the public Internet on and off. 

##<a name="scenario"> </a> Scenario
This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs. You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.

In the first setup example all your APIs are managed only from within your Virtual Network. Internal consumers (highlighted in orange) can access all your internal and external APIs. Traffic never goes out to Internet a high performance is delivered via Express Route circuits.

![url route](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"> </a> Before you begin

1. Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer. You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).
2. Create a Virtual Network and create separate subnets for API Management and Application Gateway. 
3. If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment. Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a>What is required to create an integration between API Management and Application Gateway?

* **Back-end server pool:** This is the internal virtual IP address of the API Management service.
* **Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity. These settings are applied to all servers within the pool.
* **Front-end port:** This is the public port that is opened on the application gateway. Traffic hitting it gets redirected to one of the back-end servers.
* **Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).
* **Rule:** The rule binds a listener to a back-end server pool.
* **Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active. The API Management service only responds to requests which have the correct host header, hence the default probes fail. A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.
* **Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name. This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.

## <a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway 

1. Create a resource group for Resource Manager.
2. Create a Virtual Network, subnet, and public IP for the Application Gateway. Create another subnet for API Management.
3. Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.
4. Setup the custom domain name in the API Management service.
5. Create an Application Gateway configuration object.
6. Create an Application Gateway resource.
7. Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.

## <a name="create-a-resource-group-for-resource-manager"></a>Create a resource group for Resource Manager

Make sure that you are using the latest version of Azure PowerShell. More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Step 1

Log in to Azure

```powershell
Login-AzureRmAccount
```

Authenticate with your credentials.<BR>

### <a name="step-2"></a>Step 2

Check the subscriptions for the account and select it.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Step 3

Create a resource group (skip this step if you're using an existing resource group).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager requires that all resource groups specify a location. This is used as the default location for resources in that resource group. Make sure that all commands to create an application gateway use the same resource group.

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a>Create a Virtual Network and a subnet for the application gateway

The following example shows how to create a Virtual Network using the resource manager.

### <a name="step-1"></a>Step 1

Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Step 2

Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Step 3

Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Step 4

Assign a subnet variable for the next steps

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Create an API Management service inside a VNET configured in internal mode

The following example shows how to create an API Management service in a VNET configured for internal access only.

### <a name="step-1"></a>Step 1
Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Step 2
Create an API Management service inside the Virtual Network.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Premium"
```
After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Set-up a custom domain name in API Management

### <a name="step-1"></a>Step 1
Upload the certificate with private key for the domain. For this example it will be `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Step 2
Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a>Create a public IP address for the front-end configuration

Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

An IP address is assigned to the application gateway when the service starts.

## <a name="create-application-gateway-configuration"></a>Create application gateway configuration

All configuration items must be set up before creating the application gateway. The following steps create the configuration items that are needed for an application gateway resource.

### <a name="step-1"></a>Step 1

Create an application gateway IP configuration named **gatewayIP01**. When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool. Keep in mind that each instance takes one IP address.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Step 2

Configure the front-end IP port for the public IP endpoint. This port is the port that end users connect to.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Step 3

Configure the front-end IP with public IP endpoint.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Step 4

Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Step 5

Create the HTTP listener for the Application Gateway. Assign the front-end IP configuration, port, and ssl certificate to it.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Step 6

Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint. The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services. Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.

> [!NOTE]
> The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Step 7

Upload the certificate to be used on the SSL-enabled backend pool resources.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a>Step 8

Configure HTTP backend settings for the Application Gateway. This includes setting a time-out limit for backend request after which they are cancelled. This value is different from the probe time-out.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Step 9

Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Step 10
Configure URL rule paths for the back-end pools. This enables selecting only some of the APIs from API Management for being exposed to the public. (e.g. if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet). 

The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting

$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule -DefaultBackendAddressPool $apimProxyBackendPool -DefaultBackendHttpSettings $apimPoolSetting
```

The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway. Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet. 

### <a name="step-11"></a>Step 11

Create a rule setting for the Application Gateway to use URL path-based routing.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-12"></a>Step 12

Configure the number of instances and size for the Application Gateway. Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-13"></a>Step 13

Configure WAF to be in "Prevention" mode.
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Create Application Gateway

Create an Application Gateway with all the configuration objects from the preceding steps.

```powershell
$appgw = New-AzureRmApplicationGateway -Name "appgwtest" -ResourceGroupName "apim-appGw-RG" -Location "West US" -BackendAddressPools $apimProxyBackendPool -BackendHttpSettingsCollection $apimPoolSetting -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a>CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource

Once the gateway is created, the next step is to configure the front end for communication. When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use. 

The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name. To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element. The use of A-records is not recommended since the VIP may change on restart of gateway.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"> </a> Summary
Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud. Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.

##<a name="next-steps"> </a> Next steps
* Learn more about Azure Application Gateway
  * [Application Gateway Overview](../application-gateway/application-gateway-introduction.md)
  * [Application Gateway Web Application Firewall](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
* Learn more about API Management and VNETs
  * [Using API Management in VNET](api-management-using-with-vnet.md)



