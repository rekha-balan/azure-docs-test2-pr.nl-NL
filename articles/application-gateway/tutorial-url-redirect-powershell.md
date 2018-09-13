---
title: Create an application gateway with URL path-based redirection - Azure PowerShell
description: Learn how to create an application gateway with URL path-based redirected traffic using Azure PowerShell.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 120ce3f6de112460f558fc10aede04df4074f165
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857669"
---
# <a name="create-an-application-gateway-with-url-path-based-redirection-using-azure-powershell"></a><span data-ttu-id="700f5-103">Create an application gateway with URL path-based redirection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="700f5-103">Create an application gateway with URL path-based redirection using Azure PowerShell</span></span>

<span data-ttu-id="700f5-104">You can use Azure PowerShell to configure [URL-based routing rules](application-gateway-url-route-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="700f5-104">You can use Azure PowerShell to configure [URL-based routing rules](application-gateway-url-route-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="700f5-105">In this tutorial, you create backend pools using  [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="700f5-105">In this tutorial, you create backend pools using  [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span> <span data-ttu-id="700f5-106">You then create URL routing rules that make sure web traffic is redirected to the appropriate backend pool.</span><span class="sxs-lookup"><span data-stu-id="700f5-106">You then create URL routing rules that make sure web traffic is redirected to the appropriate backend pool.</span></span>

<span data-ttu-id="700f5-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="700f5-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="700f5-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="700f5-108">Set up the network</span></span>
> * <span data-ttu-id="700f5-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-109">Create an application gateway</span></span>
> * <span data-ttu-id="700f5-110">Add listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="700f5-110">Add listeners and routing rules</span></span>
> * <span data-ttu-id="700f5-111">Create virtual machine scale sets for backend pools</span><span class="sxs-lookup"><span data-stu-id="700f5-111">Create virtual machine scale sets for backend pools</span></span>

<span data-ttu-id="700f5-112">The following example shows site traffic coming from both ports 8080 and 8081 and being directed to the same backend pools:</span><span class="sxs-lookup"><span data-stu-id="700f5-112">The following example shows site traffic coming from both ports 8080 and 8081 and being directed to the same backend pools:</span></span>

![URL routing example](./media/tutorial-url-redirect-powershell/scenario.png)

<span data-ttu-id="700f5-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="700f5-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="700f5-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="700f5-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="700f5-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="700f5-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="700f5-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="700f5-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="700f5-118">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="700f5-118">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="700f5-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="700f5-119">Create a resource group</span></span>

<span data-ttu-id="700f5-120">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="700f5-120">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="700f5-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="700f5-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="700f5-122">Create network resources</span><span class="sxs-lookup"><span data-stu-id="700f5-122">Create network resources</span></span>

<span data-ttu-id="700f5-123">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="700f5-123">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="700f5-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="700f5-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="700f5-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="700f5-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="700f5-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="700f5-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

```azurepowershell-interactive
$backendSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
  -AddressPrefix 10.0.1.0/24

$agSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myAGSubnet `
  -AddressPrefix 10.0.2.0/24

New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $backendSubnetConfig, $agSubnetConfig

New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myAGPublicIPAddress `
  -AllocationMethod Dynamic
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="700f5-127">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-127">Create an application gateway</span></span>

<span data-ttu-id="700f5-128">In this section, you create resources that support the application gateway, and then finally create it.</span><span class="sxs-lookup"><span data-stu-id="700f5-128">In this section, you create resources that support the application gateway, and then finally create it.</span></span> <span data-ttu-id="700f5-129">The resources that you create include:</span><span class="sxs-lookup"><span data-stu-id="700f5-129">The resources that you create include:</span></span>

- <span data-ttu-id="700f5-130">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span><span class="sxs-lookup"><span data-stu-id="700f5-130">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span></span>
- <span data-ttu-id="700f5-131">*Default pool* - All application gateways must have at least one backend pool of servers.</span><span class="sxs-lookup"><span data-stu-id="700f5-131">*Default pool* - All application gateways must have at least one backend pool of servers.</span></span>
- <span data-ttu-id="700f5-132">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span><span class="sxs-lookup"><span data-stu-id="700f5-132">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="700f5-133">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="700f5-133">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="700f5-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="700f5-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="700f5-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="700f5-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span> <span data-ttu-id="700f5-136">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="700f5-136">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span></span>

```azurepowershell-interactive
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet

$subnet=$vnet.Subnets[0]

$pip = Get-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupAG `
  -Name myAGPublicIPAddress

$gipconfig = New-AzureRmApplicationGatewayIPConfiguration `
  -Name myAGIPConfig `
  -Subnet $subnet

$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig `
  -Name myAGFrontendIPConfig `
  -PublicIPAddress $pip

$frontendport = New-AzureRmApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -Port 80
```

### <a name="create-the-default-pool-and-settings"></a><span data-ttu-id="700f5-137">Create the default pool and settings</span><span class="sxs-lookup"><span data-stu-id="700f5-137">Create the default pool and settings</span></span>

<span data-ttu-id="700f5-138">Create the default backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="700f5-138">Create the default backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="700f5-139">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="700f5-139">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```azurepowershell-interactive
$defaultPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name appGatewayBackendPool

$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="700f5-140">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="700f5-140">Create the default listener and rule</span></span>

<span data-ttu-id="700f5-141">A listener is required to enable the application gateway to route traffic appropriately to a backend pool.</span><span class="sxs-lookup"><span data-stu-id="700f5-141">A listener is required to enable the application gateway to route traffic appropriately to a backend pool.</span></span> <span data-ttu-id="700f5-142">In this tutorial, you create multiple listeners.</span><span class="sxs-lookup"><span data-stu-id="700f5-142">In this tutorial, you create multiple listeners.</span></span> <span data-ttu-id="700f5-143">The first basic listener expects traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="700f5-143">The first basic listener expects traffic at the root URL.</span></span> <span data-ttu-id="700f5-144">The other listeners expect traffic at specific URLs, such as *http://52.168.55.24:8080/images/* or *http://52.168.55.24:8081/video/*.</span><span class="sxs-lookup"><span data-stu-id="700f5-144">The other listeners expect traffic at specific URLs, such as *http://52.168.55.24:8080/images/* or *http://52.168.55.24:8081/video/*.</span></span>

<span data-ttu-id="700f5-145">Create a listener named *defaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="700f5-145">Create a listener named *defaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="700f5-146">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="700f5-146">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="700f5-147">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="700f5-147">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$defaultlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name defaultListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport

$frontendRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name rule1 `
  -RuleType Basic `
  -HttpListener $defaultlistener `
  -BackendAddressPool $defaultPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="700f5-148">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-148">Create the application gateway</span></span>

<span data-ttu-id="700f5-149">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="700f5-149">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

```azurepowershell-interactive
$sku = New-AzureRmApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2

New-AzureRmApplicationGateway `
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
  -Sku $sku
```

### <a name="add-backend-pools-and-ports"></a><span data-ttu-id="700f5-150">Add backend pools and ports</span><span class="sxs-lookup"><span data-stu-id="700f5-150">Add backend pools and ports</span></span>

<span data-ttu-id="700f5-151">You can add backend pools to your application gateway by using [Add-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/add-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="700f5-151">You can add backend pools to your application gateway by using [Add-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/add-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="700f5-152">In this example, *imagesBackendPool* and *videoBackendPool* are created.</span><span class="sxs-lookup"><span data-stu-id="700f5-152">In this example, *imagesBackendPool* and *videoBackendPool* are created.</span></span> <span data-ttu-id="700f5-153">You add the frontend port for the pools using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="700f5-153">You add the frontend port for the pools using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span></span> <span data-ttu-id="700f5-154">You then submit the changes to the application gateway using [Set-AzureRmApplicationGateway](/powershell/module/azurerm.network/set-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="700f5-154">You then submit the changes to the application gateway using [Set-AzureRmApplicationGateway](/powershell/module/azurerm.network/set-azurermapplicationgateway).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

Add-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name imagesBackendPool

Add-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name videoBackendPool

Add-AzureRmApplicationGatewayFrontendPort `
  -ApplicationGateway $appgw `
  -Name bport `
  -Port 8080

Add-AzureRmApplicationGatewayFrontendPort `
  -ApplicationGateway $appgw `
  -Name rport `
  -Port 8081

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

## <a name="add-listeners-and-rules"></a><span data-ttu-id="700f5-155">Add listeners and rules</span><span class="sxs-lookup"><span data-stu-id="700f5-155">Add listeners and rules</span></span>

### <a name="add-listeners"></a><span data-ttu-id="700f5-156">Add listeners</span><span class="sxs-lookup"><span data-stu-id="700f5-156">Add listeners</span></span>

<span data-ttu-id="700f5-157">Add the listeners named *backendListener* and *redirectedListener* that are needed to route traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span><span class="sxs-lookup"><span data-stu-id="700f5-157">Add the listeners named *backendListener* and *redirectedListener* that are needed to route traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$backendPort = Get-AzureRmApplicationGatewayFrontendPort `
  -ApplicationGateway $appgw `
  -Name bport

$redirectPort = Get-AzureRmApplicationGatewayFrontendPort `
  -ApplicationGateway $appgw `
  -Name rport

$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig `
  -ApplicationGateway $appgw

Add-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name backendListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $backendPort

Add-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name redirectedListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $redirectPort

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-the-default-url-path-map"></a><span data-ttu-id="700f5-158">Add the default URL path map</span><span class="sxs-lookup"><span data-stu-id="700f5-158">Add the default URL path map</span></span>

<span data-ttu-id="700f5-159">URL path maps make sure that specific URLs are routed to specific backend pools.</span><span class="sxs-lookup"><span data-stu-id="700f5-159">URL path maps make sure that specific URLs are routed to specific backend pools.</span></span> <span data-ttu-id="700f5-160">You can create the URL path maps named *imagePathRule* and *videoPathRule* using [New-AzureRmApplicationGatewayPathRuleConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewaypathruleconfig) and [Add-AzureRmApplicationGatewayUrlPathMapConfig](/powershell/module/azurerm.network/add-azurermapplicationgatewayurlpathmapconfig).</span><span class="sxs-lookup"><span data-stu-id="700f5-160">You can create the URL path maps named *imagePathRule* and *videoPathRule* using [New-AzureRmApplicationGatewayPathRuleConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewaypathruleconfig) and [Add-AzureRmApplicationGatewayUrlPathMapConfig](/powershell/module/azurerm.network/add-azurermapplicationgatewayurlpathmapconfig).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$poolSettings = Get-AzureRmApplicationGatewayBackendHttpSettings `
  -ApplicationGateway $appgw `
  -Name myPoolSettings

$imagePool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name imagesBackendPool

$videoPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name videoBackendPool

$defaultPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name appGatewayBackendPool

$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig `
  -Name imagePathRule `
  -Paths "/images/*" `
  -BackendAddressPool $imagePool `
  -BackendHttpSettings $poolSettings

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig `
  -Name videoPathRule `
  -Paths "/video/*" `
  -BackendAddressPool $videoPool `
  -BackendHttpSettings $poolSettings

Add-AzureRmApplicationGatewayUrlPathMapConfig `
  -ApplicationGateway $appgw `
  -Name urlpathmap `
  -PathRules $imagePathRule, $videoPathRule `
  -DefaultBackendAddressPool $defaultPool `
  -DefaultBackendHttpSettings $poolSettings

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-redirection-configuration"></a><span data-ttu-id="700f5-161">Add redirection configuration</span><span class="sxs-lookup"><span data-stu-id="700f5-161">Add redirection configuration</span></span>

<span data-ttu-id="700f5-162">You can configure redirection for the listener using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span><span class="sxs-lookup"><span data-stu-id="700f5-162">You can configure redirection for the listener using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$backendListener = Get-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name backendListener

$redirectConfig = Add-AzureRmApplicationGatewayRedirectConfiguration `
  -ApplicationGateway $appgw `
  -Name redirectConfig `
  -RedirectType Found `
  -TargetListener $backendListener `
  -IncludePath $true `
  -IncludeQueryString $true

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-the-redirection-url-path-map"></a><span data-ttu-id="700f5-163">Add the redirection URL path map</span><span class="sxs-lookup"><span data-stu-id="700f5-163">Add the redirection URL path map</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$poolSettings = Get-AzureRmApplicationGatewayBackendHttpSettings `
  -ApplicationGateway $appgw `
  -Name myPoolSettings

$defaultPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -ApplicationGateway $appgw `
  -Name appGatewayBackendPool

$redirectConfig = Get-AzureRmApplicationGatewayRedirectConfiguration `
  -ApplicationGateway $appgw `
  -Name redirectConfig

$redirectPathRule = New-AzureRmApplicationGatewayPathRuleConfig `
  -Name redirectPathRule `
  -Paths "/images/*" `
  -RedirectConfiguration $redirectConfig

Add-AzureRmApplicationGatewayUrlPathMapConfig `
  -ApplicationGateway $appgw `
  -Name redirectpathmap `
  -PathRules $redirectPathRule `
  -DefaultBackendAddressPool $defaultPool `
  -DefaultBackendHttpSettings $poolSettings

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-routing-rules"></a><span data-ttu-id="700f5-164">Add routing rules</span><span class="sxs-lookup"><span data-stu-id="700f5-164">Add routing rules</span></span>

<span data-ttu-id="700f5-165">The routing rules associate the URL maps with the listeners that you created.</span><span class="sxs-lookup"><span data-stu-id="700f5-165">The routing rules associate the URL maps with the listeners that you created.</span></span> <span data-ttu-id="700f5-166">You can add the rules named *defaultRule* and *redirectedRule* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="700f5-166">You can add the rules named *defaultRule* and *redirectedRule* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span></span>


```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$backendlistener = Get-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name backendListener

$redirectlistener = Get-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name redirectedListener

$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig `
  -ApplicationGateway $appgw `
  -Name urlpathmap

$redirectPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig `
  -ApplicationGateway $appgw `
  -Name redirectpathmap

Add-AzureRmApplicationGatewayRequestRoutingRule `
  -ApplicationGateway $appgw `
  -Name defaultRule `
  -RuleType PathBasedRouting `
  -HttpListener $backendlistener `
  -UrlPathMap $urlPathMap

Add-AzureRmApplicationGatewayRequestRoutingRule `
  -ApplicationGateway $appgw `
  -Name redirectedRule `
  -RuleType PathBasedRouting `
  -HttpListener $redirectlistener `
  -UrlPathMap $redirectPathMap

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="700f5-167">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="700f5-167">Create virtual machine scale sets</span></span>

<span data-ttu-id="700f5-168">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span><span class="sxs-lookup"><span data-stu-id="700f5-168">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span></span> <span data-ttu-id="700f5-169">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="700f5-169">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="700f5-170">Each scale set contains two virtual machine instances on which you install IIS.</span><span class="sxs-lookup"><span data-stu-id="700f5-170">Each scale set contains two virtual machine instances on which you install IIS.</span></span> <span data-ttu-id="700f5-171">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="700f5-171">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

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

$imagesPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name imagesBackendPool `
  -ApplicationGateway $appgw

$videoPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name videoBackendPool `
  -ApplicationGateway $appgw

for ($i=1; $i -le 3; $i++)
{
  if ($i -eq 1)
  {
     $poolId = $backendPool.Id
  }
  if ($i -eq 2) 
  {
    $poolId = $imagesPool.Id
  }
  if ($i -eq 3)
  {
    $poolId = $videoPool.Id
  }

  $ipConfig = New-AzureRmVmssIpConfig `
    -Name myVmssIPConfig$i `
    -SubnetId $vnet.Subnets[1].Id `
    -ApplicationGatewayBackendAddressPoolsId $poolId

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
    -ComputerNamePrefix myvmss$i

  Add-AzureRmVmssNetworkInterfaceConfiguration `
    -VirtualMachineScaleSet $vmssConfig `
    -Name myVmssNetConfig$i `
    -Primary $true `
    -IPConfiguration $ipConfig

  New-AzureRmVmss `
    -ResourceGroupName myResourceGroupAG `
    -Name myvmss$i `
    -VirtualMachineScaleSet $vmssConfig
}
```

### <a name="install-iis"></a><span data-ttu-id="700f5-172">Install IIS</span><span class="sxs-lookup"><span data-stu-id="700f5-172">Install IIS</span></span>

```azurepowershell-interactive
$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1"); 
  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }

for ($i=1; $i -le 3; $i++)
{
  $vmss = Get-AzureRmVmss -ResourceGroupName myResourceGroupAG -VMScaleSetName myvmss$i

  Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings

  Update-AzureRmVmss `
    -ResourceGroupName myResourceGroupAG `
    -Name myvmss$i `
    -VirtualMachineScaleSet $vmss
}
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="700f5-173">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-173">Test the application gateway</span></span>

<span data-ttu-id="700f5-174">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="700f5-174">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="700f5-175">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="700f5-175">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="700f5-176">Such as, *http://52.168.55.24*, *http://52.168.55.24:8080/images/test.htm*, *http://52.168.55.24:8080/video/test.htm*, or *http://52.168.55.24:8081/images/test.htm*.</span><span class="sxs-lookup"><span data-stu-id="700f5-176">Such as, *http://52.168.55.24*, *http://52.168.55.24:8080/images/test.htm*, *http://52.168.55.24:8080/video/test.htm*, or *http://52.168.55.24:8081/images/test.htm*.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Test base URL in application gateway](./media/tutorial-url-redirect-powershell/application-gateway-iistest.png)

<span data-ttu-id="700f5-178">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="700f5-178">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test images URL in application gateway](./media/tutorial-url-redirect-powershell/application-gateway-iistest-images.png)

<span data-ttu-id="700f5-180">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="700f5-180">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test video URL in application gateway](./media/tutorial-url-redirect-powershell/application-gateway-iistest-video.png)

<span data-ttu-id="700f5-182">Now, change the URL to http://&lt;ip-address&gt;:8081/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see traffic redirected back to the images backend pool at http://&lt;ip-address&gt;:8080/images.</span><span class="sxs-lookup"><span data-stu-id="700f5-182">Now, change the URL to http://&lt;ip-address&gt;:8081/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see traffic redirected back to the images backend pool at http://&lt;ip-address&gt;:8080/images.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="700f5-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="700f5-183">Clean up resources</span></span>

<span data-ttu-id="700f5-184">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="700f5-184">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```
## <a name="next-steps"></a><span data-ttu-id="700f5-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="700f5-185">Next steps</span></span>

<span data-ttu-id="700f5-186">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="700f5-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="700f5-187">Set up the network</span><span class="sxs-lookup"><span data-stu-id="700f5-187">Set up the network</span></span>
> * <span data-ttu-id="700f5-188">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-188">Create an application gateway</span></span>
> * <span data-ttu-id="700f5-189">Add listeners and routing rules</span><span class="sxs-lookup"><span data-stu-id="700f5-189">Add listeners and routing rules</span></span>
> * <span data-ttu-id="700f5-190">Create virtual machine scale sets for backend pools</span><span class="sxs-lookup"><span data-stu-id="700f5-190">Create virtual machine scale sets for backend pools</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="700f5-191">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="700f5-191">Learn more about what you can do with application gateway</span></span>](application-gateway-introduction.md)
