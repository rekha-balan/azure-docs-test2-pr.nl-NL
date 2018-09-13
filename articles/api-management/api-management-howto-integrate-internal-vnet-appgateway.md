---
title: How to use Azure API Management in Virtual Network with Application Gateway | Microsoft Docs
description: Learn how to setup and configure Azure API Management in Internal Virtual Network with Application Gateway (WAF) as FrontEnd
services: api-management
documentationcenter: ''
author: solankisamir
manager: kjoshi
editor: vlvinogr
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2018
ms.author: sasolank
ms.openlocfilehash: ce4fd27c89f529b9c12999689152c3025648d2ce
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808475"
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a><span data-ttu-id="41008-103">Integrate API Management in an internal VNET with Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41008-103">Integrate API Management in an internal VNET with Application Gateway</span></span>

##<span data-ttu-id="41008-104"><a name="overview"> </a> Overview</span><span class="sxs-lookup"><span data-stu-id="41008-104"><a name="overview"> </a> Overview</span></span>

<span data-ttu-id="41008-105">The API Management service can be configured in a Virtual Network in internal mode, which makes it accessible only from within the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41008-105">The API Management service can be configured in a Virtual Network in internal mode, which makes it accessible only from within the Virtual Network.</span></span> <span data-ttu-id="41008-106">Azure Application Gateway is a PAAS Service, which provides a Layer-7 load balancer.</span><span class="sxs-lookup"><span data-stu-id="41008-106">Azure Application Gateway is a PAAS Service, which provides a Layer-7 load balancer.</span></span> <span data-ttu-id="41008-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span><span class="sxs-lookup"><span data-stu-id="41008-107">It acts as a reverse-proxy service and provides among its offering a Web Application Firewall (WAF).</span></span>

<span data-ttu-id="41008-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="41008-108">Combining API Management provisioned in an internal VNET with the Application Gateway frontend enables the following scenarios:</span></span>

* <span data-ttu-id="41008-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span><span class="sxs-lookup"><span data-stu-id="41008-109">Use the same API Management resource for consumption by both internal consumers and external consumers.</span></span>
* <span data-ttu-id="41008-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span><span class="sxs-lookup"><span data-stu-id="41008-110">Use a single API Management resource and have a subset of APIs defined in API Management available for external consumers.</span></span>
* <span data-ttu-id="41008-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span><span class="sxs-lookup"><span data-stu-id="41008-111">Provide a turn-key way to switch access to API Management from the public Internet on and off.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41008-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="41008-112">Prerequisites</span></span>

<span data-ttu-id="41008-113">To follow the steps described in this article, you must have:</span><span class="sxs-lookup"><span data-stu-id="41008-113">To follow the steps described in this article, you must have:</span></span>

* <span data-ttu-id="41008-114">An active Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="41008-114">An active Azure subscription.</span></span>

    [!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

* <span data-ttu-id="41008-115">Certificates - pfx and cer for the API hostname and pfx for the developer portal's hostname.</span><span class="sxs-lookup"><span data-stu-id="41008-115">Certificates - pfx and cer for the API hostname and pfx for the developer portal's hostname.</span></span>

##<span data-ttu-id="41008-116"><a name="scenario"> </a> Scenario</span><span class="sxs-lookup"><span data-stu-id="41008-116"><a name="scenario"> </a> Scenario</span></span>

<span data-ttu-id="41008-117">This article covers how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span><span class="sxs-lookup"><span data-stu-id="41008-117">This article covers how to use a single API Management service for both internal and external consumers and make it act as a single frontend for both on-prem and cloud APIs.</span></span> <span data-ttu-id="41008-118">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using routing functionality available in Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-118">You will also see how to expose only a subset of your APIs (in the example they are highlighted in green) for External Consumption using routing functionality available in Application Gateway.</span></span>

<span data-ttu-id="41008-119">In the first setup example all your APIs are managed only from within your Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41008-119">In the first setup example all your APIs are managed only from within your Virtual Network.</span></span> <span data-ttu-id="41008-120">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span><span class="sxs-lookup"><span data-stu-id="41008-120">Internal consumers (highlighted in orange) can access all your internal and external APIs.</span></span> <span data-ttu-id="41008-121">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span><span class="sxs-lookup"><span data-stu-id="41008-121">Traffic never goes out to Internet a high performance is delivered via Express Route circuits.</span></span>

![url route](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <span data-ttu-id="41008-123"><a name="before-you-begin"> </a> Before you begin</span><span class="sxs-lookup"><span data-stu-id="41008-123"><a name="before-you-begin"> </a> Before you begin</span></span>

* <span data-ttu-id="41008-124">Make sure that you are using the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="41008-124">Make sure that you are using the latest version of Azure PowerShell.</span></span> <span data-ttu-id="41008-125">More info is available at [Using Windows PowerShell with Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/powershell-azure-resource-manager).</span><span class="sxs-lookup"><span data-stu-id="41008-125">More info is available at [Using Windows PowerShell with Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/powershell-azure-resource-manager).</span></span>

## <a name="what-is-required-to-create-an-integration-between-api-management-and-application-gateway"></a><span data-ttu-id="41008-126">What is required to create an integration between API Management and Application Gateway?</span><span class="sxs-lookup"><span data-stu-id="41008-126">What is required to create an integration between API Management and Application Gateway?</span></span>

* <span data-ttu-id="41008-127">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span><span class="sxs-lookup"><span data-stu-id="41008-127">**Back-end server pool:** This is the internal virtual IP address of the API Management service.</span></span>
* <span data-ttu-id="41008-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span><span class="sxs-lookup"><span data-stu-id="41008-128">**Back-end server pool settings:** Every pool has settings like port, protocol, and cookie-based affinity.</span></span> <span data-ttu-id="41008-129">These settings are applied to all servers within the pool.</span><span class="sxs-lookup"><span data-stu-id="41008-129">These settings are applied to all servers within the pool.</span></span>
* <span data-ttu-id="41008-130">**Front-end port:** This is the public port that is opened on the application gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-130">**Front-end port:** This is the public port that is opened on the application gateway.</span></span> <span data-ttu-id="41008-131">Traffic hitting it gets redirected to one of the back-end servers.</span><span class="sxs-lookup"><span data-stu-id="41008-131">Traffic hitting it gets redirected to one of the back-end servers.</span></span>
* <span data-ttu-id="41008-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span><span class="sxs-lookup"><span data-stu-id="41008-132">**Listener:** The listener has a front-end port, a protocol (Http or Https, these values are case-sensitive), and the SSL certificate name (if configuring SSL offload).</span></span>
* <span data-ttu-id="41008-133">**Rule:** The rule binds a listener to a back-end server pool.</span><span class="sxs-lookup"><span data-stu-id="41008-133">**Rule:** The rule binds a listener to a back-end server pool.</span></span>
* <span data-ttu-id="41008-134">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span><span class="sxs-lookup"><span data-stu-id="41008-134">**Custom Health Probe:** Application Gateway, by default, uses IP address based probes to figure out which servers in the BackendAddressPool are active.</span></span> <span data-ttu-id="41008-135">The API Management service only responds to requests with the correct host header, hence the default probes fail.</span><span class="sxs-lookup"><span data-stu-id="41008-135">The API Management service only responds to requests with the correct host header, hence the default probes fail.</span></span> <span data-ttu-id="41008-136">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span><span class="sxs-lookup"><span data-stu-id="41008-136">A custom health probe needs to be defined to help application gateway determine that the service is alive and it should forward requests.</span></span>
* <span data-ttu-id="41008-137">**Custom domain certificates:** To access API Management from the internet, you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span><span class="sxs-lookup"><span data-stu-id="41008-137">**Custom domain certificates:** To access API Management from the internet, you need to create a CNAME mapping of its hostname to the Application Gateway front-end DNS name.</span></span> <span data-ttu-id="41008-138">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span><span class="sxs-lookup"><span data-stu-id="41008-138">This ensures that the hostname header and certificate sent to Application Gateway that is forwarded to API Management is one APIM can recognize as valid.</span></span> <span data-ttu-id="41008-139">In this example, we will use two certificates - for the backend and for the developer portal.</span><span class="sxs-lookup"><span data-stu-id="41008-139">In this example, we will use two certificates - for the backend and for the developer portal.</span></span>  

## <span data-ttu-id="41008-140"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41008-140"><a name="overview-steps"> </a> Steps required for integrating API Management and Application Gateway</span></span>

1. <span data-ttu-id="41008-141">Create a resource group for Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="41008-141">Create a resource group for Resource Manager.</span></span>
2. <span data-ttu-id="41008-142">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-142">Create a Virtual Network, subnet, and public IP for the Application Gateway.</span></span> <span data-ttu-id="41008-143">Create another subnet for API Management.</span><span class="sxs-lookup"><span data-stu-id="41008-143">Create another subnet for API Management.</span></span>
3. <span data-ttu-id="41008-144">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span><span class="sxs-lookup"><span data-stu-id="41008-144">Create an API Management service inside the VNET subnet created above and ensure you use the Internal mode.</span></span>
4. <span data-ttu-id="41008-145">Set up a custom domain name in the API Management service.</span><span class="sxs-lookup"><span data-stu-id="41008-145">Set up a custom domain name in the API Management service.</span></span>
5. <span data-ttu-id="41008-146">Create an Application Gateway configuration object.</span><span class="sxs-lookup"><span data-stu-id="41008-146">Create an Application Gateway configuration object.</span></span>
6. <span data-ttu-id="41008-147">Create an Application Gateway resource.</span><span class="sxs-lookup"><span data-stu-id="41008-147">Create an Application Gateway resource.</span></span>
7. <span data-ttu-id="41008-148">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span><span class="sxs-lookup"><span data-stu-id="41008-148">Create a CNAME from the public DNS name of the Application Gateway to the API Management proxy hostname.</span></span>

## <a name="exposing-the-developer-portal-externally-through-application-gateway"></a><span data-ttu-id="41008-149">Exposing the developer portal externally through Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41008-149">Exposing the developer portal externally through Application Gateway</span></span>

<span data-ttu-id="41008-150">In this guide we will also expose the **developer portal** to external audiences through the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-150">In this guide we will also expose the **developer portal** to external audiences through the Application Gateway.</span></span> <span data-ttu-id="41008-151">It requires additional steps to create developer portal's listener, probe, settings and rules.</span><span class="sxs-lookup"><span data-stu-id="41008-151">It requires additional steps to create developer portal's listener, probe, settings and rules.</span></span> <span data-ttu-id="41008-152">All details are provided in respective steps.</span><span class="sxs-lookup"><span data-stu-id="41008-152">All details are provided in respective steps.</span></span>

> [!WARNING]
> <span data-ttu-id="41008-153">In the described setup of the developer portal being accessed through Application Gateway, you may experience problems with the AAD and third party authentication.</span><span class="sxs-lookup"><span data-stu-id="41008-153">In the described setup of the developer portal being accessed through Application Gateway, you may experience problems with the AAD and third party authentication.</span></span>

## <a name="create-a-resource-group-for-resource-manager"></a><span data-ttu-id="41008-154">Create a resource group for Resource Manager</span><span class="sxs-lookup"><span data-stu-id="41008-154">Create a resource group for Resource Manager</span></span>

### <a name="step-1"></a><span data-ttu-id="41008-155">Step 1</span><span class="sxs-lookup"><span data-stu-id="41008-155">Step 1</span></span>

<span data-ttu-id="41008-156">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="41008-156">Log in to Azure</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="41008-157">Authenticate with your credentials.</span><span class="sxs-lookup"><span data-stu-id="41008-157">Authenticate with your credentials.</span></span>

### <a name="step-2"></a><span data-ttu-id="41008-158">Step 2</span><span class="sxs-lookup"><span data-stu-id="41008-158">Step 2</span></span>

<span data-ttu-id="41008-159">Select the desired subscription.</span><span class="sxs-lookup"><span data-stu-id="41008-159">Select the desired subscription.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000" # GUID of your Azure subscription
Get-AzureRmSubscription -Subscriptionid $subscriptionId | Select-AzureRmSubscription
```

### <a name="step-3"></a><span data-ttu-id="41008-160">Step 3</span><span class="sxs-lookup"><span data-stu-id="41008-160">Step 3</span></span>

<span data-ttu-id="41008-161">Create a resource group (skip this step if you're using an existing resource group).</span><span class="sxs-lookup"><span data-stu-id="41008-161">Create a resource group (skip this step if you're using an existing resource group).</span></span>

```powershell
$resGroupName = "apim-appGw-RG" # resource group name
$location = "West US"           # Azure region
New-AzureRmResourceGroup -Name $resGroupName -Location $location
```

<span data-ttu-id="41008-162">Azure Resource Manager requires that all resource groups specify a location.</span><span class="sxs-lookup"><span data-stu-id="41008-162">Azure Resource Manager requires that all resource groups specify a location.</span></span> <span data-ttu-id="41008-163">This is used as the default location for resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="41008-163">This is used as the default location for resources in that resource group.</span></span> <span data-ttu-id="41008-164">Make sure that all commands to create an application gateway use the same resource group.</span><span class="sxs-lookup"><span data-stu-id="41008-164">Make sure that all commands to create an application gateway use the same resource group.</span></span>

## <a name="create-a-virtual-network-and-a-subnet-for-the-application-gateway"></a><span data-ttu-id="41008-165">Create a Virtual Network and a subnet for the application gateway</span><span class="sxs-lookup"><span data-stu-id="41008-165">Create a Virtual Network and a subnet for the application gateway</span></span>

<span data-ttu-id="41008-166">The following example shows how to create a Virtual Network using the resource manager.</span><span class="sxs-lookup"><span data-stu-id="41008-166">The following example shows how to create a Virtual Network using the resource manager.</span></span>

### <a name="step-1"></a><span data-ttu-id="41008-167">Step 1</span><span class="sxs-lookup"><span data-stu-id="41008-167">Step 1</span></span>

<span data-ttu-id="41008-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41008-168">Assign the address range 10.0.0.0/24 to the subnet variable to be used for Application Gateway while creating a Virtual Network.</span></span>

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a><span data-ttu-id="41008-169">Step 2</span><span class="sxs-lookup"><span data-stu-id="41008-169">Step 2</span></span>

<span data-ttu-id="41008-170">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41008-170">Assign the address range 10.0.1.0/24 to the subnet variable to be used for API Management while creating a Virtual Network.</span></span>

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a><span data-ttu-id="41008-171">Step 3</span><span class="sxs-lookup"><span data-stu-id="41008-171">Step 3</span></span>

<span data-ttu-id="41008-172">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region.</span><span class="sxs-lookup"><span data-stu-id="41008-172">Create a Virtual Network named **appgwvnet** in resource group **apim-appGw-RG** for the West US region.</span></span> <span data-ttu-id="41008-173">Use the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span><span class="sxs-lookup"><span data-stu-id="41008-173">Use the prefix 10.0.0.0/16 with subnets 10.0.0.0/24 and 10.0.1.0/24.</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName $resGroupName -Location $location -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a><span data-ttu-id="41008-174">Step 4</span><span class="sxs-lookup"><span data-stu-id="41008-174">Step 4</span></span>

<span data-ttu-id="41008-175">Assign a subnet variable for the next steps</span><span class="sxs-lookup"><span data-stu-id="41008-175">Assign a subnet variable for the next steps</span></span>

```powershell
$appgatewaysubnetdata = $vnet.Subnets[0]
$apimsubnetdata = $vnet.Subnets[1]
```

## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a><span data-ttu-id="41008-176">Create an API Management service inside a VNET configured in internal mode</span><span class="sxs-lookup"><span data-stu-id="41008-176">Create an API Management service inside a VNET configured in internal mode</span></span>

<span data-ttu-id="41008-177">The following example shows how to create an API Management service in a VNET configured for internal access only.</span><span class="sxs-lookup"><span data-stu-id="41008-177">The following example shows how to create an API Management service in a VNET configured for internal access only.</span></span>

### <a name="step-1"></a><span data-ttu-id="41008-178">Step 1</span><span class="sxs-lookup"><span data-stu-id="41008-178">Step 1</span></span>

<span data-ttu-id="41008-179">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span><span class="sxs-lookup"><span data-stu-id="41008-179">Create an API Management Virtual Network object using the subnet $apimsubnetdata created above.</span></span>

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location $location -SubnetResourceId $apimsubnetdata.Id
```

### <a name="step-2"></a><span data-ttu-id="41008-180">Step 2</span><span class="sxs-lookup"><span data-stu-id="41008-180">Step 2</span></span>

<span data-ttu-id="41008-181">Create an API Management service inside the Virtual Network.</span><span class="sxs-lookup"><span data-stu-id="41008-181">Create an API Management service inside the Virtual Network.</span></span>

```powershell
$apimServiceName = "ContosoApi"       # API Management service instance name
$apimOrganization = "Contoso"         # organization name
$apimAdminEmail = "admin@contoso.com" # administrator's email address
$apimService = New-AzureRmApiManagement -ResourceGroupName $resGroupName -Location $location -Name $apimServiceName -Organization $apimOrganization -AdminEmail $apimAdminEmail -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```

<span data-ttu-id="41008-182">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span><span class="sxs-lookup"><span data-stu-id="41008-182">After the above command succeeds refer to [DNS Configuration required to access internal VNET API Management service](api-management-using-with-internal-vnet.md#apim-dns-configuration) to access it.</span></span> <span data-ttu-id="41008-183">This step may take more than half an hour.</span><span class="sxs-lookup"><span data-stu-id="41008-183">This step may take more than half an hour.</span></span>

## <a name="set-up-a-custom-domain-name-in-api-management"></a><span data-ttu-id="41008-184">Set-up a custom domain name in API Management</span><span class="sxs-lookup"><span data-stu-id="41008-184">Set-up a custom domain name in API Management</span></span>

### <a name="step-1"></a><span data-ttu-id="41008-185">Step 1</span><span class="sxs-lookup"><span data-stu-id="41008-185">Step 1</span></span>

<span data-ttu-id="41008-186">Upload the certificates with private keys for the domains.</span><span class="sxs-lookup"><span data-stu-id="41008-186">Upload the certificates with private keys for the domains.</span></span> <span data-ttu-id="41008-187">In this example, we will use `api.contoso.net` and `portal.contoso.net`.</span><span class="sxs-lookup"><span data-stu-id="41008-187">In this example, we will use `api.contoso.net` and `portal.contoso.net`.</span></span>  

```powershell
$gatewayHostname = "api.contoso.net"                 # API gateway host
$portalHostname = "portal.contoso.net"               # API developer portal host
$gatewayCertCerPath = "C:\Users\Contoso\gateway.cer" # full path to api.contoso.net .cer file
$gatewayCertPfxPath = "C:\Users\Contoso\gateway.pfx" # full path to api.contoso.net .pfx file
$portalCertPfxPath = "C:\Users\Contoso\portal.pfx"   # full path to portal.contoso.net .pfx file
$gatewayCertPfxPassword = "certificatePassword123"   # password for api.contoso.net pfx certificate
$portalCertPfxPassword = "certificatePassword123"    # password for portal.contoso.net pfx certificate

$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName $resGroupName -Name $apimServiceName -HostnameType "Proxy" -PfxPath $gatewayCertPfxPath -PfxPassword $gatewayCertPfxPassword -PassThru
$certPortalUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName $resGroupName -Name $apimServiceName -HostnameType "Proxy" -PfxPath $portalCertPfxPath -PfxPassword $portalCertPfxPassword -PassThru
```

### <a name="step-2"></a><span data-ttu-id="41008-188">Step 2</span><span class="sxs-lookup"><span data-stu-id="41008-188">Step 2</span></span>

<span data-ttu-id="41008-189">Once the certificates are uploaded, create hostname configuration objects for the proxy and for the portal.</span><span class="sxs-lookup"><span data-stu-id="41008-189">Once the certificates are uploaded, create hostname configuration objects for the proxy and for the portal.</span></span>  

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname $gatewayHostname
$portalHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certPortalUploadResult.Thumbprint -Hostname $portalHostname
$result = Set-AzureRmApiManagementHostnames -Name $apimServiceName -ResourceGroupName $resGroupName –PortalHostnameConfiguration $portalHostnameConfig -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-the-front-end-configuration"></a><span data-ttu-id="41008-190">Create a public IP address for the front-end configuration</span><span class="sxs-lookup"><span data-stu-id="41008-190">Create a public IP address for the front-end configuration</span></span>

<span data-ttu-id="41008-191">Create a public IP resource **publicIP01** in the resource group.</span><span class="sxs-lookup"><span data-stu-id="41008-191">Create a public IP resource **publicIP01** in the resource group.</span></span>

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName $resGroupName -name "publicIP01" -location $location -AllocationMethod Dynamic
```

<span data-ttu-id="41008-192">An IP address is assigned to the application gateway when the service starts.</span><span class="sxs-lookup"><span data-stu-id="41008-192">An IP address is assigned to the application gateway when the service starts.</span></span>

## <a name="create-application-gateway-configuration"></a><span data-ttu-id="41008-193">Create application gateway configuration</span><span class="sxs-lookup"><span data-stu-id="41008-193">Create application gateway configuration</span></span>

<span data-ttu-id="41008-194">All configuration items must be set up before creating the application gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-194">All configuration items must be set up before creating the application gateway.</span></span> <span data-ttu-id="41008-195">The following steps create the configuration items that are needed for an application gateway resource.</span><span class="sxs-lookup"><span data-stu-id="41008-195">The following steps create the configuration items that are needed for an application gateway resource.</span></span>

### <a name="step-1"></a><span data-ttu-id="41008-196">Step 1</span><span class="sxs-lookup"><span data-stu-id="41008-196">Step 1</span></span>

<span data-ttu-id="41008-197">Create an application gateway IP configuration named **gatewayIP01**.</span><span class="sxs-lookup"><span data-stu-id="41008-197">Create an application gateway IP configuration named **gatewayIP01**.</span></span> <span data-ttu-id="41008-198">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span><span class="sxs-lookup"><span data-stu-id="41008-198">When Application Gateway starts, it picks up an IP address from the subnet configured and route network traffic to the IP addresses in the back-end IP pool.</span></span> <span data-ttu-id="41008-199">Keep in mind that each instance takes one IP address.</span><span class="sxs-lookup"><span data-stu-id="41008-199">Keep in mind that each instance takes one IP address.</span></span>

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a><span data-ttu-id="41008-200">Step 2</span><span class="sxs-lookup"><span data-stu-id="41008-200">Step 2</span></span>

<span data-ttu-id="41008-201">Configure the front-end IP port for the public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="41008-201">Configure the front-end IP port for the public IP endpoint.</span></span> <span data-ttu-id="41008-202">This port is the port that end users connect to.</span><span class="sxs-lookup"><span data-stu-id="41008-202">This port is the port that end users connect to.</span></span>

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```

### <a name="step-3"></a><span data-ttu-id="41008-203">Step 3</span><span class="sxs-lookup"><span data-stu-id="41008-203">Step 3</span></span>

<span data-ttu-id="41008-204">Configure the front-end IP with public IP endpoint.</span><span class="sxs-lookup"><span data-stu-id="41008-204">Configure the front-end IP with public IP endpoint.</span></span>

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a><span data-ttu-id="41008-205">Step 4</span><span class="sxs-lookup"><span data-stu-id="41008-205">Step 4</span></span>

<span data-ttu-id="41008-206">Configure the certificates for the Application Gateway, which will be used to decrypt and re-encrypt the traffic passing through.</span><span class="sxs-lookup"><span data-stu-id="41008-206">Configure the certificates for the Application Gateway, which will be used to decrypt and re-encrypt the traffic passing through.</span></span>

```powershell
$certPwd = ConvertTo-SecureString $gatewayCertPfxPassword -AsPlainText -Force
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile $gatewayCertPfxPath -Password $certPwd
$certPortalPwd = ConvertTo-SecureString $portalCertPfxPassword -AsPlainText -Force
$certPortal = New-AzureRmApplicationGatewaySslCertificate -Name "cert02" -CertificateFile $portalCertPfxPath -Password $certPortalPwd
```

### <a name="step-5"></a><span data-ttu-id="41008-207">Step 5</span><span class="sxs-lookup"><span data-stu-id="41008-207">Step 5</span></span>

<span data-ttu-id="41008-208">Create the HTTP listeners for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-208">Create the HTTP listeners for the Application Gateway.</span></span> <span data-ttu-id="41008-209">Assign the front-end IP configuration, port, and ssl certificates to them.</span><span class="sxs-lookup"><span data-stu-id="41008-209">Assign the front-end IP configuration, port, and ssl certificates to them.</span></span>

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert -HostName $gatewayHostname -RequireServerNameIndication true
$portalListener = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $certPortal -HostName $portalHostname -RequireServerNameIndication true
```

### <a name="step-6"></a><span data-ttu-id="41008-210">Step 6</span><span class="sxs-lookup"><span data-stu-id="41008-210">Step 6</span></span>

<span data-ttu-id="41008-211">Create custom probes to the API Management service `ContosoApi` proxy domain endpoint.</span><span class="sxs-lookup"><span data-stu-id="41008-211">Create custom probes to the API Management service `ContosoApi` proxy domain endpoint.</span></span> <span data-ttu-id="41008-212">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span><span class="sxs-lookup"><span data-stu-id="41008-212">The path `/status-0123456789abcdef` is a default health endpoint hosted on all the API Management services.</span></span> <span data-ttu-id="41008-213">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span><span class="sxs-lookup"><span data-stu-id="41008-213">Set `api.contoso.net` as a custom probe hostname to secure it with SSL certificate.</span></span>

> [!NOTE]
> <span data-ttu-id="41008-214">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span><span class="sxs-lookup"><span data-stu-id="41008-214">The hostname `contosoapi.azure-api.net` is the default proxy hostname configured when a service named `contosoapi` is created in public Azure.</span></span>
>

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName $gatewayHostname -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
$apimPortalProbe = New-AzureRmApplicationGatewayProbeConfig -Name "apimportalprobe" -Protocol "Https" -HostName $portalHostname -Path "/signin" -Interval 60 -Timeout 300 -UnhealthyThreshold 8
```

### <a name="step-7"></a><span data-ttu-id="41008-215">Step 7</span><span class="sxs-lookup"><span data-stu-id="41008-215">Step 7</span></span>

<span data-ttu-id="41008-216">Upload the certificate to be used on the SSL-enabled backend pool resources.</span><span class="sxs-lookup"><span data-stu-id="41008-216">Upload the certificate to be used on the SSL-enabled backend pool resources.</span></span> <span data-ttu-id="41008-217">This is the same certificate which you provided in Step 4 above.</span><span class="sxs-lookup"><span data-stu-id="41008-217">This is the same certificate which you provided in Step 4 above.</span></span>

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile $gatewayCertCerPath
```

### <a name="step-8"></a><span data-ttu-id="41008-218">Step 8</span><span class="sxs-lookup"><span data-stu-id="41008-218">Step 8</span></span>

<span data-ttu-id="41008-219">Configure HTTP backend settings for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-219">Configure HTTP backend settings for the Application Gateway.</span></span> <span data-ttu-id="41008-220">This includes setting a time-out limit for backend request, after which they're canceled.</span><span class="sxs-lookup"><span data-stu-id="41008-220">This includes setting a time-out limit for backend request, after which they're canceled.</span></span> <span data-ttu-id="41008-221">This value is different from the probe time-out.</span><span class="sxs-lookup"><span data-stu-id="41008-221">This value is different from the probe time-out.</span></span>

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
$apimPoolPortalSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolPortalSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimPortalProbe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a><span data-ttu-id="41008-222">Step 9</span><span class="sxs-lookup"><span data-stu-id="41008-222">Step 9</span></span>

<span data-ttu-id="41008-223">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span><span class="sxs-lookup"><span data-stu-id="41008-223">Configure a back-end IP address pool named **apimbackend**  with the internal virtual IP address of the API Management service created above.</span></span>

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.PrivateIPAddresses[0]
```

### <a name="step-10"></a><span data-ttu-id="41008-224">Step 10</span><span class="sxs-lookup"><span data-stu-id="41008-224">Step 10</span></span>

<span data-ttu-id="41008-225">Create rules for the Application Gateway to use basic routing.</span><span class="sxs-lookup"><span data-stu-id="41008-225">Create rules for the Application Gateway to use basic routing.</span></span>

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType Basic -HttpListener $listener -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule2" -RuleType Basic -HttpListener $portalListener -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolPortalSetting
```

> [!TIP]
> <span data-ttu-id="41008-226">Change the -RuleType and routing, to restrict access to certain pages of the developer portal.</span><span class="sxs-lookup"><span data-stu-id="41008-226">Change the -RuleType and routing, to restrict access to certain pages of the developer portal.</span></span>

### <a name="step-11"></a><span data-ttu-id="41008-227">Step 11</span><span class="sxs-lookup"><span data-stu-id="41008-227">Step 11</span></span>

<span data-ttu-id="41008-228">Configure the number of instances and size for the Application Gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-228">Configure the number of instances and size for the Application Gateway.</span></span> <span data-ttu-id="41008-229">In this example, we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span><span class="sxs-lookup"><span data-stu-id="41008-229">In this example, we are using the [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) for increased security of the API Management resource.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-12"></a><span data-ttu-id="41008-230">Step 12</span><span class="sxs-lookup"><span data-stu-id="41008-230">Step 12</span></span>

<span data-ttu-id="41008-231">Configure WAF to be in "Prevention" mode.</span><span class="sxs-lookup"><span data-stu-id="41008-231">Configure WAF to be in "Prevention" mode.</span></span>

```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a><span data-ttu-id="41008-232">Create Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41008-232">Create Application Gateway</span></span>

<span data-ttu-id="41008-233">Create an Application Gateway with all the configuration objects from the preceding steps.</span><span class="sxs-lookup"><span data-stu-id="41008-233">Create an Application Gateway with all the configuration objects from the preceding steps.</span></span>

```powershell
$appgwName = "apim-app-gw"
$appgw = New-AzureRmApplicationGateway -Name $appgwName -ResourceGroupName $resGroupName -Location $location -BackendAddressPools $apimProxyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $apimPoolPortalSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener, $portalListener -RequestRoutingRules $rule01, $rule02 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert, $certPortal -AuthenticationCertificates $authcert -Probes $apimprobe, $apimPortalProbe
```

## <a name="cname-the-api-management-proxy-hostname-to-the-public-dns-name-of-the-application-gateway-resource"></a><span data-ttu-id="41008-234">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span><span class="sxs-lookup"><span data-stu-id="41008-234">CNAME the API Management proxy hostname to the public DNS name of the Application Gateway resource</span></span>

<span data-ttu-id="41008-235">Once the gateway is created, the next step is to configure the front end for communication.</span><span class="sxs-lookup"><span data-stu-id="41008-235">Once the gateway is created, the next step is to configure the front end for communication.</span></span> <span data-ttu-id="41008-236">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span><span class="sxs-lookup"><span data-stu-id="41008-236">When using a public IP, Application Gateway requires a dynamically assigned DNS name, which may not be easy to use.</span></span>

<span data-ttu-id="41008-237">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span><span class="sxs-lookup"><span data-stu-id="41008-237">The Application Gateway's DNS name should be used to create a CNAME record which points the APIM proxy host name (e.g. `api.contoso.net` in the examples above) to this DNS name.</span></span> <span data-ttu-id="41008-238">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span><span class="sxs-lookup"><span data-stu-id="41008-238">To configure the frontend IP CNAME record, retrieve the details of the Application Gateway and its associated IP/DNS name using the PublicIPAddress element.</span></span> <span data-ttu-id="41008-239">The use of A-records is not recommended since the VIP may change on restart of gateway.</span><span class="sxs-lookup"><span data-stu-id="41008-239">The use of A-records is not recommended since the VIP may change on restart of gateway.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName $resGroupName -Name "publicIP01"
```

##<span data-ttu-id="41008-240"><a name="summary"> </a> Summary</span><span class="sxs-lookup"><span data-stu-id="41008-240"><a name="summary"> </a> Summary</span></span>
<span data-ttu-id="41008-241">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="41008-241">Azure API Management configured in a VNET provides a single gateway interface for all configured APIs, whether they are hosted on-prem or in the cloud.</span></span> <span data-ttu-id="41008-242">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span><span class="sxs-lookup"><span data-stu-id="41008-242">Integrating Application Gateway with API Management provides the flexibility of selectively enabling particular APIs to be accessible on the Internet, as well as providing a Web Application Firewall as a frontend to your API Management instance.</span></span>

##<span data-ttu-id="41008-243"><a name="next-steps"> </a> Next steps</span><span class="sxs-lookup"><span data-stu-id="41008-243"><a name="next-steps"> </a> Next steps</span></span>
* <span data-ttu-id="41008-244">Learn more about Azure Application Gateway</span><span class="sxs-lookup"><span data-stu-id="41008-244">Learn more about Azure Application Gateway</span></span>
  * [<span data-ttu-id="41008-245">Application Gateway Overview</span><span class="sxs-lookup"><span data-stu-id="41008-245">Application Gateway Overview</span></span>](../application-gateway/application-gateway-introduction.md)
  * [<span data-ttu-id="41008-246">Application Gateway Web Application Firewall</span><span class="sxs-lookup"><span data-stu-id="41008-246">Application Gateway Web Application Firewall</span></span>](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [<span data-ttu-id="41008-247">Application Gateway using Path-based Routing</span><span class="sxs-lookup"><span data-stu-id="41008-247">Application Gateway using Path-based Routing</span></span>](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* <span data-ttu-id="41008-248">Learn more about API Management and VNETs</span><span class="sxs-lookup"><span data-stu-id="41008-248">Learn more about API Management and VNETs</span></span>
  * [<span data-ttu-id="41008-249">Using API Management available only within the VNET</span><span class="sxs-lookup"><span data-stu-id="41008-249">Using API Management available only within the VNET</span></span>](api-management-using-with-internal-vnet.md)
  * [<span data-ttu-id="41008-250">Using API Management in VNET</span><span class="sxs-lookup"><span data-stu-id="41008-250">Using API Management in VNET</span></span>](api-management-using-with-vnet.md)
