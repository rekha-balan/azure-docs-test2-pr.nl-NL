---
title: Create an application gateway with SSL termination - Azure PowerShell
description: Learn how to create an application gateway and add a certificate for SSL termination using Azure PowerShell.
services: application-gateway
author: vhorne
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: a11aa119e46a01b964776ca9352da41d1ce2991a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871436"
---
# <a name="create-an-application-gateway-with-ssl-termination-using-azure-powershell"></a><span data-ttu-id="a4fd4-103">Create an application gateway with SSL termination using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a4fd4-103">Create an application gateway with SSL termination using Azure PowerShell</span></span>

<span data-ttu-id="a4fd4-104">You can use Azure PowerShell to create an [application gateway](overview.md) with a certificate for [SSL termination](ssl-overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-104">You can use Azure PowerShell to create an [application gateway](overview.md) with a certificate for [SSL termination](ssl-overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers.</span></span> <span data-ttu-id="a4fd4-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-105">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span></span> 

<span data-ttu-id="a4fd4-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a4fd4-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4fd4-107">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-107">Create a self-signed certificate</span></span>
> * <span data-ttu-id="a4fd4-108">Set up a network</span><span class="sxs-lookup"><span data-stu-id="a4fd4-108">Set up a network</span></span>
> * <span data-ttu-id="a4fd4-109">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-109">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="a4fd4-110">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="a4fd4-110">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="a4fd4-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="a4fd4-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-112">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a4fd4-113">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-113">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="a4fd4-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="a4fd4-115">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-115">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-self-signed-certificate"></a><span data-ttu-id="a4fd4-116">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-116">Create a self-signed certificate</span></span>

<span data-ttu-id="a4fd4-117">For production use, you should import a valid certificate signed by trusted provider.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-117">For production use, you should import a valid certificate signed by trusted provider.</span></span> <span data-ttu-id="a4fd4-118">For this tutorial, you create a self-signed certificate using [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-118">For this tutorial, you create a self-signed certificate using [New-SelfSignedCertificate](https://docs.microsoft.com/powershell/module/pkiclient/new-selfsignedcertificate).</span></span> <span data-ttu-id="a4fd4-119">You can use [Export-PfxCertificate](https://docs.microsoft.com/powershell/module/pkiclient/export-pfxcertificate) with the Thumbprint that was returned to export a pfx file from the certificate.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-119">You can use [Export-PfxCertificate](https://docs.microsoft.com/powershell/module/pkiclient/export-pfxcertificate) with the Thumbprint that was returned to export a pfx file from the certificate.</span></span>

```powershell
New-SelfSignedCertificate `
  -certstorelocation cert:\localmachine\my `
  -dnsname www.contoso.com
```

<span data-ttu-id="a4fd4-120">You should see something like this result:</span><span class="sxs-lookup"><span data-stu-id="a4fd4-120">You should see something like this result:</span></span>

```
PSParentPath: Microsoft.PowerShell.Security\Certificate::LocalMachine\my

Thumbprint                                Subject
----------                                -------
E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630  CN=www.contoso.com
```

<span data-ttu-id="a4fd4-121">Use the thumbprint to create the pfx file:</span><span class="sxs-lookup"><span data-stu-id="a4fd4-121">Use the thumbprint to create the pfx file:</span></span>

```powershell
$pwd = ConvertTo-SecureString -String "Azure123456!" -Force -AsPlainText

Export-PfxCertificate `
  -cert cert:\localMachine\my\E1E81C23B3AD33F9B4D1717B20AB65DBB91AC630 `
  -FilePath c:\appgwcert.pfx `
  -Password $pwd
```

## <a name="create-a-resource-group"></a><span data-ttu-id="a4fd4-122">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="a4fd4-122">Create a resource group</span></span>

<span data-ttu-id="a4fd4-123">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-123">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="a4fd4-124">Create an Azure resource group named *myResourceGroupAG* with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-124">Create an Azure resource group named *myResourceGroupAG* with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="a4fd4-125">Create network resources</span><span class="sxs-lookup"><span data-stu-id="a4fd4-125">Create network resources</span></span>

<span data-ttu-id="a4fd4-126">Configure the subnets named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-126">Configure the subnets named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="a4fd4-127">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-127">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="a4fd4-128">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-128">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="a4fd4-129">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-129">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="a4fd4-130">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="a4fd4-130">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="a4fd4-131">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="a4fd4-131">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="a4fd4-132">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-132">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="a4fd4-133">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-133">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span>

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

$frontendport = New-AzureRmApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -Port 443
```

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="a4fd4-134">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="a4fd4-134">Create the backend pool and settings</span></span>

<span data-ttu-id="a4fd4-135">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-135">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="a4fd4-136">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-136">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

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

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="a4fd4-137">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="a4fd4-137">Create the default listener and rule</span></span>

<span data-ttu-id="a4fd4-138">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-138">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="a4fd4-139">In this example, you create a basic listener that listens for HTTPS traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-139">In this example, you create a basic listener that listens for HTTPS traffic at the root URL.</span></span> 

<span data-ttu-id="a4fd4-140">Create a certificate object using [New-AzureRmApplicationGatewaySslCertificate](/powershell/module/azurerm.network/new-azurermapplicationgatewaysslcertificate) and then create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration, frontend port, and certificate that you previously created.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-140">Create a certificate object using [New-AzureRmApplicationGatewaySslCertificate](/powershell/module/azurerm.network/new-azurermapplicationgatewaysslcertificate) and then create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration, frontend port, and certificate that you previously created.</span></span> <span data-ttu-id="a4fd4-141">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-141">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="a4fd4-142">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-142">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```powershell
$pwd = ConvertTo-SecureString `
  -String "Azure123456!" `
  -Force `
  -AsPlainText

$cert = New-AzureRmApplicationGatewaySslCertificate `
  -Name "appgwcert" `
  -CertificateFile "c:\appgwcert.pfx" `
  -Password $pwd

$defaultlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name mydefaultListener `
  -Protocol Https `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport `
  -SslCertificate $cert

$frontendRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name rule1 `
  -RuleType Basic `
  -HttpListener $defaultlistener `
  -BackendAddressPool $defaultPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway-with-the-certificate"></a><span data-ttu-id="a4fd4-143">Create the application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-143">Create the application gateway with the certificate</span></span>

<span data-ttu-id="a4fd4-144">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) with the certificate.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-144">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) with the certificate.</span></span>

### <a name="create-the-application-gateway"></a><span data-ttu-id="a4fd4-145">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="a4fd4-145">Create the application gateway</span></span>

```azurepowershell-interactive
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
  -FrontendPorts $frontendport `
  -HttpListeners $defaultlistener `
  -RequestRoutingRules $frontendRule `
  -Sku $sku `
  -SslCertificates $cert
```

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="a4fd4-146">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="a4fd4-146">Create a virtual machine scale set</span></span>

<span data-ttu-id="a4fd4-147">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-147">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="a4fd4-148">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-148">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

```azurepowershell-interactive
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
  -OsDiskCreateOption FromImage

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

### <a name="install-iis"></a><span data-ttu-id="a4fd4-149">Install IIS</span><span class="sxs-lookup"><span data-stu-id="a4fd4-149">Install IIS</span></span>

```azurepowershell-interactive
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

## <a name="test-the-application-gateway"></a><span data-ttu-id="a4fd4-150">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="a4fd4-150">Test the application gateway</span></span>

<span data-ttu-id="a4fd4-151">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-151">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="a4fd4-152">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-152">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Secure warning](./media/tutorial-ssl-powershell/application-gateway-secure.png)

<span data-ttu-id="a4fd4-154">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span><span class="sxs-lookup"><span data-stu-id="a4fd4-154">To accept the security warning if you used a self-signed certificate, select **Details** and then **Go on to the webpage**.</span></span> <span data-ttu-id="a4fd4-155">Your secured IIS website is then displayed as in the following example:</span><span class="sxs-lookup"><span data-stu-id="a4fd4-155">Your secured IIS website is then displayed as in the following example:</span></span>

![Test base URL in application gateway](./media/tutorial-ssl-powershell/application-gateway-iistest.png)

## <a name="clean-up-resources"></a><span data-ttu-id="a4fd4-157">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="a4fd4-157">Clean up resources</span></span>

<span data-ttu-id="a4fd4-158">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a4fd4-158">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="a4fd4-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="a4fd4-159">Next steps</span></span>

<span data-ttu-id="a4fd4-160">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="a4fd4-160">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4fd4-161">Create a self-signed certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-161">Create a self-signed certificate</span></span>
> * <span data-ttu-id="a4fd4-162">Set up a network</span><span class="sxs-lookup"><span data-stu-id="a4fd4-162">Set up a network</span></span>
> * <span data-ttu-id="a4fd4-163">Create an application gateway with the certificate</span><span class="sxs-lookup"><span data-stu-id="a4fd4-163">Create an application gateway with the certificate</span></span>
> * <span data-ttu-id="a4fd4-164">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="a4fd4-164">Create a virtual machine scale set with the default backend pool</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4fd4-165">Create an application gateway that hosts multiple web sites</span><span class="sxs-lookup"><span data-stu-id="a4fd4-165">Create an application gateway that hosts multiple web sites</span></span>](./tutorial-multiple-sites-powershell.md)