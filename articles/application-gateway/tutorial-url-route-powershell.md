---
title: Route web traffic based on the URL - Azure PowerShell
description: Learn how to route web traffic based on the URL to specific scalable pools of servers using Azure PowerShell.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 66f79b68c003aa3605653b0decc091d22fbf3860
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868742"
---
# <a name="route-web-traffic-based-on-the-url-using-azure-powershell"></a><span data-ttu-id="81af6-103">Route web traffic based on the URL using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="81af6-103">Route web traffic based on the URL using Azure PowerShell</span></span>

<span data-ttu-id="81af6-104">You can use Azure PowerShell to configure web traffic routing to specific scalable server pools based on the URL that is used to access your application.</span><span class="sxs-lookup"><span data-stu-id="81af6-104">You can use Azure PowerShell to configure web traffic routing to specific scalable server pools based on the URL that is used to access your application.</span></span> <span data-ttu-id="81af6-105">In this tutorial, you create an [Azure Application Gateway](application-gateway-introduction.md) with three backend pools using [Virtual Machine Scale Sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="81af6-105">In this tutorial, you create an [Azure Application Gateway](application-gateway-introduction.md) with three backend pools using [Virtual Machine Scale Sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span> <span data-ttu-id="81af6-106">Each of the backend pools serves a specific purpose such as, common data, images, and video.</span><span class="sxs-lookup"><span data-stu-id="81af6-106">Each of the backend pools serves a specific purpose such as, common data, images, and video.</span></span>  <span data-ttu-id="81af6-107">Routing traffic to separate pools ensures that your customers get the information that they need when they need it.</span><span class="sxs-lookup"><span data-stu-id="81af6-107">Routing traffic to separate pools ensures that your customers get the information that they need when they need it.</span></span>

<span data-ttu-id="81af6-108">To enable traffic routing, you create [routing rules](application-gateway-url-route-overview.md) assigned to listeners that listen on specific ports to ensure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="81af6-108">To enable traffic routing, you create [routing rules](application-gateway-url-route-overview.md) assigned to listeners that listen on specific ports to ensure web traffic arrives at the appropriate servers in the pools.</span></span>

<span data-ttu-id="81af6-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="81af6-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81af6-110">Set up the network</span><span class="sxs-lookup"><span data-stu-id="81af6-110">Set up the network</span></span>
> * <span data-ttu-id="81af6-111">Create listeners, URL path map, and rules</span><span class="sxs-lookup"><span data-stu-id="81af6-111">Create listeners, URL path map, and rules</span></span>
> * <span data-ttu-id="81af6-112">Create scalable backend pools</span><span class="sxs-lookup"><span data-stu-id="81af6-112">Create scalable backend pools</span></span>

![URL routing example](./media/tutorial-url-route-powershell/scenario.png)

<span data-ttu-id="81af6-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="81af6-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="81af6-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="81af6-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="81af6-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="81af6-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="81af6-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="81af6-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="81af6-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="81af6-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

<span data-ttu-id="81af6-119">Because of the time needed to create resources, it can take up to 90 minutes to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="81af6-119">Because of the time needed to create resources, it can take up to 90 minutes to complete this tutorial.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="81af6-120">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="81af6-120">Create a resource group</span></span>

<span data-ttu-id="81af6-121">You need to create a resource group that contains all of the resources for your application.</span><span class="sxs-lookup"><span data-stu-id="81af6-121">You need to create a resource group that contains all of the resources for your application.</span></span> 

<span data-ttu-id="81af6-122">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="81af6-122">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="81af6-123">Create network resources</span><span class="sxs-lookup"><span data-stu-id="81af6-123">Create network resources</span></span>

<span data-ttu-id="81af6-124">Whether you have an existing virtual network or create a new one, you need to make sure that it contains a subnet that is only used for application gateways.</span><span class="sxs-lookup"><span data-stu-id="81af6-124">Whether you have an existing virtual network or create a new one, you need to make sure that it contains a subnet that is only used for application gateways.</span></span> <span data-ttu-id="81af6-125">In this tutorial, you create a subnet for the application gateway and a subnet for the scale sets.</span><span class="sxs-lookup"><span data-stu-id="81af6-125">In this tutorial, you create a subnet for the application gateway and a subnet for the scale sets.</span></span> <span data-ttu-id="81af6-126">You create a public IP address to enable access to the resources in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="81af6-126">You create a public IP address to enable access to the resources in the application gateway.</span></span>

<span data-ttu-id="81af6-127">Create the subnet configurations *myAGSubnet* and *myBackendSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="81af6-127">Create the subnet configurations *myAGSubnet* and *myBackendSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="81af6-128">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="81af6-128">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="81af6-129">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="81af6-129">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="81af6-130">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="81af6-130">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

```azurepowershell-interactive
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

## <a name="create-an-application-gateway"></a><span data-ttu-id="81af6-131">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="81af6-131">Create an application gateway</span></span>

<span data-ttu-id="81af6-132">In this section you create resources that support the application gateway, and then finally create it.</span><span class="sxs-lookup"><span data-stu-id="81af6-132">In this section you create resources that support the application gateway, and then finally create it.</span></span> <span data-ttu-id="81af6-133">The resources that you create include:</span><span class="sxs-lookup"><span data-stu-id="81af6-133">The resources that you create include:</span></span>

- <span data-ttu-id="81af6-134">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span><span class="sxs-lookup"><span data-stu-id="81af6-134">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span></span>
- <span data-ttu-id="81af6-135">*Default pool* - All application gateways must have at least one backend pool of servers.</span><span class="sxs-lookup"><span data-stu-id="81af6-135">*Default pool* - All application gateways must have at least one backend pool of servers.</span></span>
- <span data-ttu-id="81af6-136">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span><span class="sxs-lookup"><span data-stu-id="81af6-136">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="81af6-137">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="81af6-137">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="81af6-138">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="81af6-138">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="81af6-139">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="81af6-139">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span>

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

### <a name="create-the-default-pool-and-settings"></a><span data-ttu-id="81af6-140">Create the default pool and settings</span><span class="sxs-lookup"><span data-stu-id="81af6-140">Create the default pool and settings</span></span>

<span data-ttu-id="81af6-141">Create the default backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="81af6-141">Create the default backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="81af6-142">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="81af6-142">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

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

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="81af6-143">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="81af6-143">Create the default listener and rule</span></span>

<span data-ttu-id="81af6-144">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="81af6-144">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="81af6-145">In this tutorial, you create two listeners.</span><span class="sxs-lookup"><span data-stu-id="81af6-145">In this tutorial, you create two listeners.</span></span> <span data-ttu-id="81af6-146">The first basic listener that you create listens for traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="81af6-146">The first basic listener that you create listens for traffic at the root URL.</span></span> <span data-ttu-id="81af6-147">The second listener that you create listens for traffic at specific URLs.</span><span class="sxs-lookup"><span data-stu-id="81af6-147">The second listener that you create listens for traffic at specific URLs.</span></span>

<span data-ttu-id="81af6-148">Create the default listener named *myDefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="81af6-148">Create the default listener named *myDefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> 

<span data-ttu-id="81af6-149">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="81af6-149">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="81af6-150">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="81af6-150">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$defaultlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name myDefaultListener `
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

### <a name="create-the-application-gateway"></a><span data-ttu-id="81af6-151">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="81af6-151">Create the application gateway</span></span>

<span data-ttu-id="81af6-152">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="81af6-152">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

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
  -Sku $sku
```

<span data-ttu-id="81af6-153">It may take up to 30 minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span><span class="sxs-lookup"><span data-stu-id="81af6-153">It may take up to 30 minutes for the application gateway to be created, wait until the deployment finishes successfully before moving on to the next section.</span></span> <span data-ttu-id="81af6-154">At this point in the tutorial, you have an application gateway that is listening for traffic on port 80 and sends that traffic to a default pool of servers.</span><span class="sxs-lookup"><span data-stu-id="81af6-154">At this point in the tutorial, you have an application gateway that is listening for traffic on port 80 and sends that traffic to a default pool of servers.</span></span>

### <a name="add-image-and-video-backend-pools-and-port"></a><span data-ttu-id="81af6-155">Add image and video backend pools and port</span><span class="sxs-lookup"><span data-stu-id="81af6-155">Add image and video backend pools and port</span></span>

<span data-ttu-id="81af6-156">Add backend pools named *imagesBackendPool* and *videoBackendPool* to your application gateway[Add-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/add-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="81af6-156">Add backend pools named *imagesBackendPool* and *videoBackendPool* to your application gateway[Add-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/add-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="81af6-157">Add the frontend port for the pools using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="81af6-157">Add the frontend port for the pools using [Add-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/add-azurermapplicationgatewayfrontendport).</span></span> <span data-ttu-id="81af6-158">Submit the changes to the application gateway using [Set-AzureRmApplicationGateway](/powershell/module/azurerm.network/set-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="81af6-158">Submit the changes to the application gateway using [Set-AzureRmApplicationGateway](/powershell/module/azurerm.network/set-azurermapplicationgateway).</span></span>

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

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

<span data-ttu-id="81af6-159">Updating the application gateway can also take up to 20 minutes to finish.</span><span class="sxs-lookup"><span data-stu-id="81af6-159">Updating the application gateway can also take up to 20 minutes to finish.</span></span>

### <a name="add-backend-listener"></a><span data-ttu-id="81af6-160">Add backend listener</span><span class="sxs-lookup"><span data-stu-id="81af6-160">Add backend listener</span></span>

<span data-ttu-id="81af6-161">Add the backend listener named *backendListener* that's needed to route traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span><span class="sxs-lookup"><span data-stu-id="81af6-161">Add the backend listener named *backendListener* that's needed to route traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$backendPort = Get-AzureRmApplicationGatewayFrontendPort `
  -ApplicationGateway $appgw `
  -Name bport

$fipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig `
  -ApplicationGateway $appgw

Add-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name backendListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $backendPort

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-url-path-map"></a><span data-ttu-id="81af6-162">Add URL path map</span><span class="sxs-lookup"><span data-stu-id="81af6-162">Add URL path map</span></span>

<span data-ttu-id="81af6-163">URL path maps make sure that the URLs sent to your application are routed to specific backend pools.</span><span class="sxs-lookup"><span data-stu-id="81af6-163">URL path maps make sure that the URLs sent to your application are routed to specific backend pools.</span></span> <span data-ttu-id="81af6-164">Create URL path maps named *imagePathRule* and *videoPathRule* using [New-AzureRmApplicationGatewayPathRuleConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewaypathruleconfig) and [Add-AzureRmApplicationGatewayUrlPathMapConfig](/powershell/module/azurerm.network/add-azurermapplicationgatewayurlpathmapconfig).</span><span class="sxs-lookup"><span data-stu-id="81af6-164">Create URL path maps named *imagePathRule* and *videoPathRule* using [New-AzureRmApplicationGatewayPathRuleConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewaypathruleconfig) and [Add-AzureRmApplicationGatewayUrlPathMapConfig](/powershell/module/azurerm.network/add-azurermapplicationgatewayurlpathmapconfig).</span></span>

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

### <a name="add-routing-rule"></a><span data-ttu-id="81af6-165">Add routing rule</span><span class="sxs-lookup"><span data-stu-id="81af6-165">Add routing rule</span></span>

<span data-ttu-id="81af6-166">The routing rule associates the URL map with the listener that you created.</span><span class="sxs-lookup"><span data-stu-id="81af6-166">The routing rule associates the URL map with the listener that you created.</span></span> <span data-ttu-id="81af6-167">Add the rule named *rule2* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="81af6-167">Add the rule named *rule2* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$backendlistener = Get-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name backendListener

$urlPathMap = Get-AzureRmApplicationGatewayUrlPathMapConfig `
  -ApplicationGateway $appgw `
  -Name urlpathmap

Add-AzureRmApplicationGatewayRequestRoutingRule `
  -ApplicationGateway $appgw `
  -Name rule2 `
  -RuleType PathBasedRouting `
  -HttpListener $backendlistener `
  -UrlPathMap $urlPathMap

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="81af6-168">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="81af6-168">Create virtual machine scale sets</span></span>

<span data-ttu-id="81af6-169">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span><span class="sxs-lookup"><span data-stu-id="81af6-169">In this example, you create three virtual machine scale sets that support the three backend pools that you created.</span></span> <span data-ttu-id="81af6-170">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span><span class="sxs-lookup"><span data-stu-id="81af6-170">The scale sets that you create are named *myvmss1*, *myvmss2*, and *myvmss3*.</span></span> <span data-ttu-id="81af6-171">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="81af6-171">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

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

### <a name="install-iis"></a><span data-ttu-id="81af6-172">Install IIS</span><span class="sxs-lookup"><span data-stu-id="81af6-172">Install IIS</span></span>

<span data-ttu-id="81af6-173">Each scale set contains two virtual machine instances on which you install IIS, which runs a sample page to test whether the application gateway is working.</span><span class="sxs-lookup"><span data-stu-id="81af6-173">Each scale set contains two virtual machine instances on which you install IIS, which runs a sample page to test whether the application gateway is working.</span></span>

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

## <a name="test-the-application-gateway"></a><span data-ttu-id="81af6-174">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="81af6-174">Test the application gateway</span></span>

<span data-ttu-id="81af6-175">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="81af6-175">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="81af6-176">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="81af6-176">Copy the public IP address, and then paste it into the address bar of your browser.</span></span> <span data-ttu-id="81af6-177">Such as, *http://52.168.55.24*, *http://52.168.55.24:8080/images/test.htm*, or *http://52.168.55.24:8080/video/test.htm*.</span><span class="sxs-lookup"><span data-stu-id="81af6-177">Such as, *http://52.168.55.24*, *http://52.168.55.24:8080/images/test.htm*, or *http://52.168.55.24:8080/video/test.htm*.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Test base URL in application gateway](./media/tutorial-url-route-powershell/application-gateway-iistest.png)

<span data-ttu-id="81af6-179">Change the URL to http://&lt;ip-address&gt;:8080/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="81af6-179">Change the URL to http://&lt;ip-address&gt;:8080/images/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test images URL in application gateway](./media/tutorial-url-route-powershell/application-gateway-iistest-images.png)

<span data-ttu-id="81af6-181">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="81af6-181">Change the URL to http://&lt;ip-address&gt;:8080/video/test.htm, substituting your IP address for &lt;ip-address&gt;, and you should see something like the following example:</span></span>

![Test video URL in application gateway](./media/tutorial-url-route-powershell/application-gateway-iistest-video.png)

## <a name="clean-up-resources"></a><span data-ttu-id="81af6-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="81af6-183">Clean up resources</span></span>

<span data-ttu-id="81af6-184">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="81af6-184">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="81af6-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="81af6-185">Next steps</span></span>

<span data-ttu-id="81af6-186">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="81af6-186">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="81af6-187">Set up the network</span><span class="sxs-lookup"><span data-stu-id="81af6-187">Set up the network</span></span>
> * <span data-ttu-id="81af6-188">Create listeners, URL path map, and rules</span><span class="sxs-lookup"><span data-stu-id="81af6-188">Create listeners, URL path map, and rules</span></span>
> * <span data-ttu-id="81af6-189">Create scalable backend pools</span><span class="sxs-lookup"><span data-stu-id="81af6-189">Create scalable backend pools</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="81af6-190">Redirect web traffic based on the URL</span><span class="sxs-lookup"><span data-stu-id="81af6-190">Redirect web traffic based on the URL</span></span>](./tutorial-url-redirect-powershell.md)
