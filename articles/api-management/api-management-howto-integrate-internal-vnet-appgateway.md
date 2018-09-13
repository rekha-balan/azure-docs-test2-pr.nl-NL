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
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="d7685-103">Integrate API Management in an internal VNET with Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d7685-103">Integrate API Management in an internal VNET with Application Gateway</span></span> 

##<span data-ttu-id="d7685-104"><a name="overview"> </a> Overview</span><span class="sxs-lookup"><span data-stu-id="d7685-104"><a name="overview"> </a> Overview</span></span>
 
<span data-ttu-id="d7685-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="d7685-105">The API Management service can be configured in a Virtual Network in internal mode which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="d7685-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="d7685-106">Azure Application Gateway is a PAAS Service which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="d7685-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="d7685-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="d7685-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d7685-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="d7685-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span><span class="sxs-lookup"><span data-stu-id="d7685-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="d7685-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span><span class="sxs-lookup"><span data-stu-id="d7685-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="d7685-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span><span class="sxs-lookup"><span data-stu-id="d7685-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span> 

##<span data-ttu-id="d7685-112"><a name="scenario"> </a> Scenario</span><span class="sxs-lookup"><span data-stu-id="d7685-112"><a name="scenario"> </a> Scenario</span></span>
<span data-ttu-id="d7685-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span><span class="sxs-lookup"><span data-stu-id="d7685-113">This article will cover how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="d7685-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-114">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using the PathBasedRouting functionality available in Application Gateway.</span></span>

<span data-ttu-id="d7685-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="d7685-115">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="d7685-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span><span class="sxs-lookup"><span data-stu-id="d7685-116">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="d7685-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span><span class="sxs-lookup"><span data-stu-id="d7685-117">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![url route](https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="d7685-119"><a name="before-you-begin"> </a> Before you begin</span><span class="sxs-lookup"><span data-stu-id="d7685-119"><a name="before-you-begin"> </a> Before you begin</span></span>

1. <span data-ttu-id="d7685-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="d7685-120">Install the latest version of the Azure PowerShell cmdlets by using the Web Platform Installer.</span></span> <span data-ttu-id="d7685-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d7685-121">You can download and install the latest version from the **Windows PowerShell** section of the [Downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="d7685-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-122">Create a Virtual Network and create separate subnets for API Management and Application Gateway.</span></span> 
3. <span data-ttu-id="d7685-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span><span class="sxs-lookup"><span data-stu-id="d7685-123">If you intend to create a custom DNS server for the Virtual Network, do so before starting the deployment.</span></span> <span data-ttu-id="d7685-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span><span class="sxs-lookup"><span data-stu-id="d7685-124">Double check it works by ensuring a virtual machine created in a new subnet in the Virtual Network can resolve and access all Azure service endpoints.</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="d7685-125">What is required to create an integration between API Management and Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="d7685-125">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="d7685-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span><span class="sxs-lookup"><span data-stu-id="d7685-126">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="d7685-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="d7685-127">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="d7685-128">These settings are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="d7685-128">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="d7685-129">**Front-end port:** This is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-129">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="d7685-130">Traffic hitting it gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="d7685-130">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="d7685-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="d7685-131">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="d7685-132">**Rule:** The rule binds a listener to a back-end server pool.</span><span class="sxs-lookup"><span data-stu-id="d7685-132">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="d7685-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span><span class="sxs-lookup"><span data-stu-id="d7685-133">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="d7685-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span><span class="sxs-lookup"><span data-stu-id="d7685-134">The API Management service only responds to requests which have the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="d7685-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span><span class="sxs-lookup"><span data-stu-id="d7685-135">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="d7685-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span><span class="sxs-lookup"><span data-stu-id="d7685-136">**Custom domain certificate:** To access API Management from the internet you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="d7685-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span><span class="sxs-lookup"><span data-stu-id="d7685-137">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span>

## <span data-ttu-id="d7685-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d7685-138"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span> 

1. <span data-ttu-id="d7685-139">Create a resource group for Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7685-139">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="d7685-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-140">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="d7685-141">Create another subnet for API Management.</span><span class="sxs-lookup"><span data-stu-id="d7685-141">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="d7685-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span><span class="sxs-lookup"><span data-stu-id="d7685-142">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="d7685-143">Setup the custom domain name in the API Management service.</span><span class="sxs-lookup"><span data-stu-id="d7685-143">Setup the custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="d7685-144">Create an Application Gateway configuration object.</span><span class="sxs-lookup"><span data-stu-id="d7685-144">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="d7685-145">Create an Application Gateway resource.</span><span class="sxs-lookup"><span data-stu-id="d7685-145">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="d7685-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span><span class="sxs-lookup"><span data-stu-id="d7685-146">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="d7685-147">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7685-147">Create a resource group for Resource Manager</span></span>

<span data-ttu-id="d7685-148">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d7685-148">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="d7685-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="d7685-149">More info is available at [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

### <a name="step-1"></a><span data-ttu-id="d7685-150">Step 1</span><span class="sxs-lookup"><span data-stu-id="d7685-150">Step 1</span></span>

<span data-ttu-id="d7685-151">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="d7685-151">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="d7685-152">Authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="d7685-152">Authenticate with your credentials.</span></span><BR>

### <a name="step-2"></a><span data-ttu-id="d7685-153">Step 2</span><span class="sxs-lookup"><span data-stu-id="d7685-153">Step 2</span></span>

<span data-ttu-id="d7685-154">Check the subscriptions for the account and select it.</span><span class="sxs-lookup"><span data-stu-id="d7685-154">Check the subscriptions for the account and select it.</span></span>

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="d7685-155">Step 3</span><span class="sxs-lookup"><span data-stu-id="d7685-155">Step 3</span></span>

<span data-ttu-id="d7685-156">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="d7685-156">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
<span data-ttu-id="d7685-157">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="d7685-157">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="d7685-158">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="d7685-158">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="d7685-159">Make sure that all commands to create an application gateway use the same resource group.</span><span class="sxs-lookup"><span data-stu-id="d7685-159">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="d7685-160">Create a Virtual Network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="d7685-160">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="d7685-161">The following example shows how to create a Virtual Network using the resource manager.</span><span class="sxs-lookup"><span data-stu-id="d7685-161">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7685-162">Step 1</span><span class="sxs-lookup"><span data-stu-id="d7685-162">Step 1</span></span>

<span data-ttu-id="d7685-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="d7685-163">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="d7685-164">Step 2</span><span class="sxs-lookup"><span data-stu-id="d7685-164">Step 2</span></span>

<span data-ttu-id="d7685-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="d7685-165">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="d7685-166">Step 3</span><span class="sxs-lookup"><span data-stu-id="d7685-166">Step 3</span></span>

<span data-ttu-id="d7685-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="d7685-167">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region using the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="d7685-168">Step 4</span><span class="sxs-lookup"><span data-stu-id="d7685-168">Step 4</span></span>

<span data-ttu-id="d7685-169">Assign a subnet variable for the next steps</span><span class="sxs-lookup"><span data-stu-id="d7685-169">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="d7685-170">Create an API Management service inside a VNET configured in internal mode</span><span class="sxs-lookup"><span data-stu-id="d7685-170">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="d7685-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span><span class="sxs-lookup"><span data-stu-id="d7685-171">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7685-172">Step 1</span><span class="sxs-lookup"><span data-stu-id="d7685-172">Step 1</span></span>
<span data-ttu-id="d7685-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span><span class="sxs-lookup"><span data-stu-id="d7685-173">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a><span data-ttu-id="d7685-174">Step 2</span><span class="sxs-lookup"><span data-stu-id="d7685-174">Step 2</span></span>
<span data-ttu-id="d7685-175">Create an API Management service inside the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="d7685-175">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Premium"
```
<span data-ttu-id="d7685-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span><span class="sxs-lookup"><span data-stu-id="d7685-176">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="d7685-177">Set-up a custom domain name in API Management</span><span class="sxs-lookup"><span data-stu-id="d7685-177">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="d7685-178">Step 1</span><span class="sxs-lookup"><span data-stu-id="d7685-178">Step 1</span></span>
<span data-ttu-id="d7685-179">Upload the certificate with private key for the domain.</span><span class="sxs-lookup"><span data-stu-id="d7685-179">Upload the certificate with private key for the domain.</span></span> <span data-ttu-id="d7685-180">For this example it will be `*.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="d7685-180">For this example it will be `*.contoso.net`.</span></span> 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path to .pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a><span data-ttu-id="d7685-181">Step 2</span><span class="sxs-lookup"><span data-stu-id="d7685-181">Step 2</span></span>
<span data-ttu-id="d7685-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span><span class="sxs-lookup"><span data-stu-id="d7685-182">Once the certificate is uploaded, create a hostname configuration object for the proxy with a hostname of `api.contoso.net`, as the example certificate provides authority for the  `*.contoso.net` domain.</span></span> 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="d7685-183">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="d7685-183">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="d7685-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="d7685-184">Create a public IP resource **publicIP01** in resource group **apim-appGw-RG** for the West US region.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

<span data-ttu-id="d7685-185">An IP address is assigned to the application gateway when the service starts.</span><span class="sxs-lookup"><span data-stu-id="d7685-185">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="d7685-186">Create application gateway configuration</span><span class="sxs-lookup"><span data-stu-id="d7685-186">Create application gateway configuration</span></span>

<span data-ttu-id="d7685-187">All configuration items must be set up before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-187">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="d7685-188">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="d7685-188">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="d7685-189">Step 1</span><span class="sxs-lookup"><span data-stu-id="d7685-189">Step 1</span></span>

<span data-ttu-id="d7685-190">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="d7685-190">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="d7685-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="d7685-191">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="d7685-192">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="d7685-192">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="d7685-193">Step 2</span><span class="sxs-lookup"><span data-stu-id="d7685-193">Step 2</span></span>

<span data-ttu-id="d7685-194">Configure the front-end IP port for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="d7685-194">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="d7685-195">This port is the port that end users connect to.</span><span class="sxs-lookup"><span data-stu-id="d7685-195">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a><span data-ttu-id="d7685-196">Step 3</span><span class="sxs-lookup"><span data-stu-id="d7685-196">Step 3</span></span>

<span data-ttu-id="d7685-197">Configure the front-end IP with public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="d7685-197">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="d7685-198">Step 4</span><span class="sxs-lookup"><span data-stu-id="d7685-198">Step 4</span></span>

<span data-ttu-id="d7685-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span><span class="sxs-lookup"><span data-stu-id="d7685-199">Configure the certificate for the Application Gateway, used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path to .pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a><span data-ttu-id="d7685-200">Step 5</span><span class="sxs-lookup"><span data-stu-id="d7685-200">Step 5</span></span>

<span data-ttu-id="d7685-201">Create the HTTP listener for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-201">Create the HTTP listener for the Application Gateway.</span></span> <span data-ttu-id="d7685-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span><span class="sxs-lookup"><span data-stu-id="d7685-202">Assign the front-end IP configuration, port, and ssl certificate to it.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a><span data-ttu-id="d7685-203">Step 6</span><span class="sxs-lookup"><span data-stu-id="d7685-203">Step 6</span></span>

<span data-ttu-id="d7685-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span><span class="sxs-lookup"><span data-stu-id="d7685-204">Create a custom probe to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="d7685-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span><span class="sxs-lookup"><span data-stu-id="d7685-205">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="d7685-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="d7685-206">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="d7685-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span><span class="sxs-lookup"><span data-stu-id="d7685-207">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span> 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="d7685-208">Step 7</span><span class="sxs-lookup"><span data-stu-id="d7685-208">Step 7</span></span>

<span data-ttu-id="d7685-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span><span class="sxs-lookup"><span data-stu-id="d7685-209">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path to .cer file>
```

### <a name="step-8"></a><span data-ttu-id="d7685-210">Step 8</span><span class="sxs-lookup"><span data-stu-id="d7685-210">Step 8</span></span>

<span data-ttu-id="d7685-211">Configure HTTP backend settings for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-211">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="d7685-212">This includes setting a time-out limit for backend request after which they are cancelled.</span><span class="sxs-lookup"><span data-stu-id="d7685-212">This includes setting a time-out limit for backend request after which they are cancelled.</span></span> <span data-ttu-id="d7685-213">This value is different from the probe time-out.</span><span class="sxs-lookup"><span data-stu-id="d7685-213">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="d7685-214">Step 9</span><span class="sxs-lookup"><span data-stu-id="d7685-214">Step 9</span></span>

<span data-ttu-id="d7685-215">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span><span class="sxs-lookup"><span data-stu-id="d7685-215">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a><span data-ttu-id="d7685-216">Step 10</span><span class="sxs-lookup"><span data-stu-id="d7685-216">Step 10</span></span>
<span data-ttu-id="d7685-217">Configure URL rule paths for the back-end pools.</span><span class="sxs-lookup"><span data-stu-id="d7685-217">Configure URL rule paths for the back-end pools.</span></span> <span data-ttu-id="d7685-218">This enables selecting only some of the APIs from API Management for being exposed to the public.</span><span class="sxs-lookup"><span data-stu-id="d7685-218">This enables selecting only some of the APIs from API Management for being exposed to the public.</span></span> <span data-ttu-id="d7685-219">(e.g. if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span><span class="sxs-lookup"><span data-stu-id="d7685-219">(e.g. if there are `Echo API` (/echo/), `Calculator API` (/calc/) etc. make only `Echo API` accessible from Internet).</span></span> 

<span data-ttu-id="d7685-220">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span><span class="sxs-lookup"><span data-stu-id="d7685-220">The following example creates a simple rule for the "/echo/" path routing traffic to the back-end "apimProxyBackendPool".</span></span>

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting

$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule -DefaultBackendAddressPool $apimProxyBackendPool -DefaultBackendHttpSettings $apimPoolSetting
```

<span data-ttu-id="d7685-221">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-221">The above step ensures that only requests for the path "/echo" are allowed through the Application Gateway.</span></span> <span data-ttu-id="d7685-222">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span><span class="sxs-lookup"><span data-stu-id="d7685-222">Requests to other APIs configured in API Management will throw 404 errors from Application Gateway when accessed from the Internet.</span></span> 

### <a name="step-11"></a><span data-ttu-id="d7685-223">Step 11</span><span class="sxs-lookup"><span data-stu-id="d7685-223">Step 11</span></span>

<span data-ttu-id="d7685-224">Create a rule setting for the Application Gateway to use URL path-based routing.</span><span class="sxs-lookup"><span data-stu-id="d7685-224">Create a rule setting for the Application Gateway to use URL path-based routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-12"></a><span data-ttu-id="d7685-225">Step 12</span><span class="sxs-lookup"><span data-stu-id="d7685-225">Step 12</span></span>

<span data-ttu-id="d7685-226">Configure the number of instances and size for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-226">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="d7685-227">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span><span class="sxs-lookup"><span data-stu-id="d7685-227">Here we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-13"></a><span data-ttu-id="d7685-228">Step 13</span><span class="sxs-lookup"><span data-stu-id="d7685-228">Step 13</span></span>

<span data-ttu-id="d7685-229">Configure WAF to be in "Prevention" mode.</span><span class="sxs-lookup"><span data-stu-id="d7685-229">Configure WAF to be in "Prevention" mode.</span></span>
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="d7685-230">Create Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d7685-230">Create Application Gateway</span></span>

<span data-ttu-id="d7685-231">Create an Application Gateway with all the configuration objects from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="d7685-231">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgw = New-AzureRmApplicationGateway -Name "appgwtest" -ResourceGroupName "apim-appGw-RG" -Location "West US" -BackendAddressPools $apimProxyBackendPool -BackendHttpSettingsCollection $apimPoolSetting -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="d7685-232">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span><span class="sxs-lookup"><span data-stu-id="d7685-232">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="d7685-233">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="d7685-233">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="d7685-234">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span><span class="sxs-lookup"><span data-stu-id="d7685-234">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span> 

<span data-ttu-id="d7685-235">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="d7685-235">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="d7685-236">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span><span class="sxs-lookup"><span data-stu-id="d7685-236">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="d7685-237">The use of A-records is not recommended since the VIP may change on restart of gateway.</span><span class="sxs-lookup"><span data-stu-id="d7685-237">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<span data-ttu-id="d7685-238"><a name="summary"> </a> Summary</span><span class="sxs-lookup"><span data-stu-id="d7685-238"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="d7685-239">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="d7685-239">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="d7685-240">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="d7685-240">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="d7685-241"><a name="next-steps"> </a> Next steps</span><span class="sxs-lookup"><span data-stu-id="d7685-241"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="d7685-242">Learn more about Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="d7685-242">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="d7685-243">Application Gateway Overview</span><span class="sxs-lookup"><span data-stu-id="d7685-243">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="d7685-244">Application Gateway Web Application Firewall</span><span class="sxs-lookup"><span data-stu-id="d7685-244">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
* <span data-ttu-id="d7685-245">Learn more about API Management and VNETs</span><span class="sxs-lookup"><span data-stu-id="d7685-245">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="d7685-246">Using API Management in VNET</span><span class="sxs-lookup"><span data-stu-id="d7685-246">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)



