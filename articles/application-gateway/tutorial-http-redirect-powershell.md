---
title: Create an application gateway with HTTP to HTTPS redirection - Azure PowerShell | Microsoft Docs
description: Learn how to create an application gateway with redirected traffic from HTTP to HTTPS using Azure PowerShell.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 01/23/2018
ms.author: victorh
ms.openlocfilehash: 29de5badb83319cd03dd29f2dcfd0be9997a1202
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864810"
---
# <a name="create-an-application-gateway-with-http-to-https-redirection-using-azure-powershell"></a><span data-ttu-id="f8cfa-103">Create an application gateway with HTTP to HTTPS redirection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f8cfa-103">Create an application gateway with HTTP to HTTPS redirection using Azure PowerShell</span></span>

<span data-ttu-id="f8cfa-104">You can use the Azure PowerShell to create an [application gateway](application-gateway-introduction.md) with a certificate for SSL termination.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-104">You can use the Azure PowerShell to create an [application gateway](application-gateway-introduction.md) with a certificate for SSL termination.</span></span> <span data-ttu-id="f8cfa-105">A routing rule is used to redirect HTTP traffic to the HTTPS port in your application gateway.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-105">A routing rule is used to redirect HTTP traffic to the HTTPS port in your application gateway.</span></span> <span data-ttu-id="f8cfa-106">In this example, you also create a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for the backend pool of the application gateway that contains two virtual machine instances.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-106">In this example, you also create a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for the backend pool of the application gateway that contains two virtual machine instances.</span></span> 

<span data-ttu-id="f8cfa-107">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="f8cfa-107">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8cfa-108">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f8cfa-108">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f8cfa-109">Set up a network</span><span class="sxs-lookup"><span data-stu-id="f8cfa-109">Set up a network</span></span>
> * <span data-ttu-id="f8cfa-110">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f8cfa-110">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f8cfa-111">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="f8cfa-111">Add a listener and redirection rule</span></span>
> * <span data-ttu-id="f8cfa-112">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="f8cfa-112">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="f8cfa-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-113">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="f8cfa-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-114">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f8cfa-115">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-115">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="f8cfa-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-116">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="f8cfa-117">To run the commands in this tutorial, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-117">To run the commands in this tutorial, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="f8cfa-118">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f8cfa-118">Create a self-signed certificate</span></span>

<span data-ttu-id="f8cfa-119">For production use, you should import a valid certificate signed by a trusted provider.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-119">For production use, you should import a valid certificate signed by a trusted provider.</span></span> <span data-ttu-id="f8cfa-120">For this tutorial, you create a self-signed certificate using [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-120">For this tutorial, you create a self-signed certificate using [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate).</span></span> <span data-ttu-id="f8cfa-121">You can use [Export-PfxCertificate](https://docs.microsoft.com/powershell/module/pkiclient/export-pfxcertificate) with the Thumbprint that was returned to export a pfx file from the certificate.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-121">You can use [Export-PfxCertificate](https://docs.microsoft.com/powershell/module/pkiclient/export-pfxcertificate) with the Thumbprint that was returned to export a pfx file from the certificate.</span></span>

```powershell
New-SelfSignedCertificate `
  -certstorelocation cert:\localmachine\my `
  -dnsname www.contoso.com
```

<span data-ttu-id="f8cfa-122">You should see something like this result:</span><span class="sxs-lookup"><span data-stu-id="f8cfa-122">You should see something like this result:</span></span>

```
PSParentPath: Microsoft.PowerShell.Security\Certificate::LocalMachine\my

Thumbprint                                Subject
----------                                -------
E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630  CN=www.contoso.com
```

<span data-ttu-id="f8cfa-123">Use the thumbprint to create the pfx file:</span><span class="sxs-lookup"><span data-stu-id="f8cfa-123">Use the thumbprint to create the pfx file:</span></span>

```powershell
$pwd = ConvertTo-SecureString -String "Azure123456!" -Force -AsPlainText
Export-PfxCertificate `
  -cert cert:\localMachine\my\E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630 `
  -FilePath c:\appgwcert.pfx `
  -Password $pwd
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f8cfa-124">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f8cfa-124">Create a resource group</span></span>

<span data-ttu-id="f8cfa-125">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-125">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f8cfa-126">Create an Azure resource group named *myResourceGroupAG* using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-126">Create an Azure resource group named *myResourceGroupAG* using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="f8cfa-127">Create network resources</span><span class="sxs-lookup"><span data-stu-id="f8cfa-127">Create network resources</span></span>

<span data-ttu-id="f8cfa-128">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-128">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="f8cfa-129">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-129">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="f8cfa-130">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-130">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="f8cfa-131">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-131">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

```powershell
$backendSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -AddressPrefix 10.0.1.0/24
$agSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myAGSubnet `
  -AddressPrefix 10.0.2.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $backendSubnetConfig, $agSubnetConfig
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myAGPublicIPAddress `
  -AllocationMethod Dynamic
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="f8cfa-132">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="f8cfa-132">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="f8cfa-133">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="f8cfa-133">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="f8cfa-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="f8cfa-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span> <span data-ttu-id="f8cfa-136">And then you can create the HTTPS port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-136">And then you can create the HTTPS port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet
$subnet=$vnet.Subnets[0]
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration `
  -Name myAGIPConfig `
  -Subnet $subnet
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig `
  -Name myAGFrontendIPConfig `
  -PublicIPAddress $pip
$frontendPort = New-AzureRmApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -Port 443
```

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="f8cfa-137">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="f8cfa-137">Create the backend pool and settings</span></span>

<span data-ttu-id="f8cfa-138">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-138">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="f8cfa-139">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-139">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```powershell
$defaultPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name appGatewayBackendPool 
$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="f8cfa-140">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="f8cfa-140">Create the default listener and rule</span></span>

<span data-ttu-id="f8cfa-141">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-141">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="f8cfa-142">In this example, you create a basic listener that listens for HTTPS traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-142">In this example, you create a basic listener that listens for HTTPS traffic at the root URL.</span></span> 

<span data-ttu-id="f8cfa-143">Create a certificate object using [New-AzureRmApplicationGatewaySslCertificate](/powershell/module/azurerm.network/new-azurermapplicationgatewaysslcertificate) and then create a listener named *appGatewayHttpListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration, frontend port, and certificate that you previously created.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-143">Create a certificate object using [New-AzureRmApplicationGatewaySslCertificate](/powershell/module/azurerm.network/new-azurermapplicationgatewaysslcertificate) and then create a listener named *appGatewayHttpListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration, frontend port, and certificate that you previously created.</span></span> <span data-ttu-id="f8cfa-144">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-144">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="f8cfa-145">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-145">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```powershell
$pwd = ConvertTo-SecureString `
  -String "Azure123456!" `
  -Force `
  -AsPlainText
$cert = New-AzureRmApplicationGatewaySslCertificate `
  -Name "appgwcert" `
  -CertificateFile "c:\appgwcert.pfx" `
  -Password $pwd
$defaultListener = New-AzureRmApplicationGatewayHttpListener `
  -Name appGatewayHttpListener `
  -Protocol Https `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendPort `
  -SslCertificate $cert
$frontendRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name rule1 `
  -RuleType Basic `
  -HttpListener $defaultListener `
  -BackendAddressPool $defaultPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="f8cfa-146">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="f8cfa-146">Create the application gateway</span></span>

<span data-ttu-id="f8cfa-147">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) with the certificate.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-147">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) with the certificate.</span></span>

```powershell
$sku = New-AzureRmApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2
$appgw = New-AzureRmApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -BackendAddressPools $defaultPool `
  -BackendHttpSettingsCollection $poolSettings `
  -FrontendIpConfigurations $fipconfig `
  -GatewayIpConfigurations $gipconfig `
  -FrontendPorts $frontendPort `
  -HttpListeners $defaultListener `
  -RequestRoutingRules $frontendRule `
  -Sku $sku `
  -SslCertificates $cert
```

## <a name="add-a-listener-and-redirection-rule"></a><span data-ttu-id="f8cfa-148">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="f8cfa-148">Add a listener and redirection rule</span></span>

### <a name="add-the-http-port"></a><span data-ttu-id="f8cfa-149">Add the HTTP port</span><span class="sxs-lookup"><span data-stu-id="f8cfa-149">Add the HTTP port</span></span>

<span data-ttu-id="f8cfa-150">Add the HTTP port to the application gateway using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-150">Add the HTTP port to the application gateway using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span></span>

```powershell
$appgw = Get-AzureRmApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG
Add-AzureRmApplicationGatewayFrontendPort `
  -Name httpPort  `
  -Port 80 `
  -ApplicationGateway $appgw
```

### <a name="add-the-http-listener"></a><span data-ttu-id="f8cfa-151">Add the HTTP listener</span><span class="sxs-lookup"><span data-stu-id="f8cfa-151">Add the HTTP listener</span></span>

<span data-ttu-id="f8cfa-152">Add the HTTP listener named *myListener* to the application gateway using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-152">Add the HTTP listener named *myListener* to the application gateway using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span></span>

```powershell
$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig `
  -Name myAGFrontendIPConfig `
  -ApplicationGateway $appgw
$fp = Get-AzureRmApplicationGatewayFrontendPort `
  -Name httpPort `
  -ApplicationGateway $appgw
Add-AzureRmApplicationGatewayHttpListener `
  -Name myListener `
  -Protocol Http `
  -FrontendPort $fp `
  -FrontendIPConfiguration $fipconfig `
  -ApplicationGateway $appgw
```

### <a name="add-the-redirection-configuration"></a><span data-ttu-id="f8cfa-153">Add the redirection configuration</span><span class="sxs-lookup"><span data-stu-id="f8cfa-153">Add the redirection configuration</span></span>

<span data-ttu-id="f8cfa-154">Add the HTTP to HTTPS redirection configuration to the application gateway using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-154">Add the HTTP to HTTPS redirection configuration to the application gateway using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span></span>

```powershell
$defaultListener = Get-AzureRmApplicationGatewayHttpListener `
  -Name appGatewayHttpListener `
  -ApplicationGateway $appgw
Add-AzureRmApplicationGatewayRedirectConfiguration -Name httpToHttps `
  -RedirectType Permanent `
  -TargetListener $defaultListener `
  -IncludePath $true `
  -IncludeQueryString $true `
  -ApplicationGateway $appgw
```

### <a name="add-the-routing-rule"></a><span data-ttu-id="f8cfa-155">Add the routing rule</span><span class="sxs-lookup"><span data-stu-id="f8cfa-155">Add the routing rule</span></span>

<span data-ttu-id="f8cfa-156">Add the routing rule with the redirection configuration to the application gateway using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="f8cfa-156">Add the routing rule with the redirection configuration to the application gateway using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span></span>

```powershell
$myListener = Get-AzureRmApplicationGatewayHttpListener `
  -Name myListener `
  -ApplicationGateway $appgw
$redirectConfig = Get-AzureRmApplicationGatewayRedirectConfiguration `
  -Name httpToHttps `
  -ApplicationGateway $appgw
Add-AzureRmApplicationGatewayRequestRoutingRule `
  -Name rule2 `
  -RuleType Basic `
  -HttpListener $myListener `
  -RedirectConfiguration $redirectConfig `
  -ApplicationGateway $appgw
Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="f8cfa-157">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f8cfa-157">Create a virtual machine scale set</span></span>

<span data-ttu-id="f8cfa-158">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-158">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="f8cfa-159">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-159">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway
$backendPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name appGatewayBackendPool `
  -ApplicationGateway $appgw
$ipConfig = New-AzureRmVmssIpConfig `
  -Name myVmssIPConfig `
  -SubnetId $vnet.Subnets[1].Id `
  -ApplicationGatewayBackendAddressPoolsId $backendPool.Id
$vmssConfig = New-AzureRmVmssConfig `
  -Location eastus `
  -SkuCapacity 2 `
  -SkuName Standard_DS2 `
  -UpgradePolicyMode Automatic
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword "Azure123456!" `
  -ComputerNamePrefix myvmss
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name myVmssNetConfig `
  -Primary $true `
  -IPConfiguration $ipConfig
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupAG `
  -Name myvmss `
  -VirtualMachineScaleSet $vmssConfig
```

### <a name="install-iis"></a><span data-ttu-id="f8cfa-160">Install IIS</span><span class="sxs-lookup"><span data-stu-id="f8cfa-160">Install IIS</span></span>

```powershell
$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1"); 
  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }
$vmss = Get-AzureRmVmss -ResourceGroupName myResourceGroupAG -VMScaleSetName myvmss
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss `
  -Name "customScript" `
  -Publisher "Microsoft.Compute" `
  -Type "CustomScriptExtension" `
  -TypeHandlerVersion 1.8 `
  -Setting $publicSettings
Update-AzureRmVmss `
  -ResourceGroupName myResourceGroupAG `
  -Name myvmss `
  -VirtualMachineScaleSet $vmss
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="f8cfa-161">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="f8cfa-161">Test the application gateway</span></span>

<span data-ttu-id="f8cfa-162">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-162">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="f8cfa-163">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-163">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="f8cfa-164">For example, http://52.170.203.149</span><span class="sxs-lookup"><span data-stu-id="f8cfa-164">For example, http://52.170.203.149</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Secure warning](./media/tutorial-http-redirect-powershell/application-gateway-secure.png)

<span data-ttu-id="f8cfa-166">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span><span class="sxs-lookup"><span data-stu-id="f8cfa-166">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span></span> <span data-ttu-id="f8cfa-167">Your secured IIS website is then displayed as in the following example:</span><span class="sxs-lookup"><span data-stu-id="f8cfa-167">Your secured IIS website is then displayed as in the following example:</span></span>

![Test base URL in application gateway](./media/tutorial-http-redirect-powershell/application-gateway-iistest.png)

## <a name="next-steps"></a><span data-ttu-id="f8cfa-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="f8cfa-169">Next steps</span></span>

<span data-ttu-id="f8cfa-170">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="f8cfa-170">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f8cfa-171">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="f8cfa-171">Create a self-signed certificate</span></span>
> * <span data-ttu-id="f8cfa-172">Set up a network</span><span class="sxs-lookup"><span data-stu-id="f8cfa-172">Set up a network</span></span>
> * <span data-ttu-id="f8cfa-173">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="f8cfa-173">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="f8cfa-174">Add a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="f8cfa-174">Add a listener and redirection rule</span></span>
> * <span data-ttu-id="f8cfa-175">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="f8cfa-175">Create a virtual machine scale set with the default backend pool</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8cfa-176">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="f8cfa-176">Learn more about what you can do with application gateway</span></span>](application-gateway-introduction.md)
