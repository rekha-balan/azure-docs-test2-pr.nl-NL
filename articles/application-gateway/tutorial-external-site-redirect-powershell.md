---
title: Create an application gateway with external redirection - Azure PowerShell | Microsoft Docs
description: Learn how to create an application gateway that redirects web traffic to an external site using Azure Powershell.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.topic: article
ms.workload: infrastructure-services
ms.date: 01/24/2018
ms.author: victorh
ms.openlocfilehash: 6e2f0dadcb1158863282090bf6f81b0ae368416f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967715"
---
# <a name="create-an-application-gateway-with-external-redirection-using-azure-powershell"></a><span data-ttu-id="227b0-103">Create an application gateway with external redirection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="227b0-103">Create an application gateway with external redirection using Azure PowerShell</span></span>

<span data-ttu-id="227b0-104">You can use Azure Powershell to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="227b0-104">You can use Azure Powershell to configure [web traffic redirection](application-gateway-multi-site-overview.md) when you create an [application gateway](application-gateway-introduction.md).</span></span> <span data-ttu-id="227b0-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span><span class="sxs-lookup"><span data-stu-id="227b0-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span></span>

<span data-ttu-id="227b0-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="227b0-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="227b0-107">Set up the network</span><span class="sxs-lookup"><span data-stu-id="227b0-107">Set up the network</span></span>
> * <span data-ttu-id="227b0-108">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="227b0-108">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="227b0-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-109">Create an application gateway</span></span>

<span data-ttu-id="227b0-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="227b0-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="227b0-111">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="227b0-111">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="227b0-112">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="227b0-112">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="227b0-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="227b0-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="227b0-114">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="227b0-114">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="227b0-115">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="227b0-115">Create a resource group</span></span>

<span data-ttu-id="227b0-116">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="227b0-116">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="227b0-117">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="227b0-117">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="227b0-118">Create network resources</span><span class="sxs-lookup"><span data-stu-id="227b0-118">Create network resources</span></span>

<span data-ttu-id="227b0-119">Create the subnet configuration *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="227b0-119">Create the subnet configuration *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="227b0-120">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="227b0-120">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configuration.</span></span> <span data-ttu-id="227b0-121">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="227b0-121">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="227b0-122">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="227b0-122">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

```azurepowershell-interactive
$agSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myAGSubnet `
  -AddressPrefix 10.0.1.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myVNet `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $agSubnetConfig
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -Name myAGPublicIPAddress `
  -AllocationMethod Dynamic
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="227b0-123">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-123">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="227b0-124">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="227b0-124">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="227b0-125">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="227b0-125">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="227b0-126">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="227b0-126">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span> <span data-ttu-id="227b0-127">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="227b0-127">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span></span>

```azurepowershell-interactive
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
  -Port 80
```

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="227b0-128">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="227b0-128">Create the backend pool and settings</span></span>

<span data-ttu-id="227b0-129">Create the backend pool named *defaultPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="227b0-129">Create the backend pool named *defaultPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="227b0-130">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="227b0-130">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```azurepowershell-interactive
$defaultPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name defaultPool 
$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-listener-and-rule"></a><span data-ttu-id="227b0-131">Create the listener and rule</span><span class="sxs-lookup"><span data-stu-id="227b0-131">Create the listener and rule</span></span>

<span data-ttu-id="227b0-132">A listener is required to enable the application gateway to appropriately route traffic.</span><span class="sxs-lookup"><span data-stu-id="227b0-132">A listener is required to enable the application gateway to appropriately route traffic.</span></span> <span data-ttu-id="227b0-133">Create the listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="227b0-133">Create the listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="227b0-134">You redirect traffic by creating a redirection configuration that can be added to the routing rule that you create.</span><span class="sxs-lookup"><span data-stu-id="227b0-134">You redirect traffic by creating a redirection configuration that can be added to the routing rule that you create.</span></span>

<span data-ttu-id="227b0-135">A routing rule is required for the listener to know where to send incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="227b0-135">A routing rule is required for the listener to know where to send incoming traffic.</span></span> <span data-ttu-id="227b0-136">Create a basic rule named *redirectRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) with the redirection configuration.</span><span class="sxs-lookup"><span data-stu-id="227b0-136">Create a basic rule named *redirectRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) with the redirection configuration.</span></span>

```azurepowershell-interactive
$defaultListener = New-AzureRmApplicationGatewayHttpListener `
  -Name defaultListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport
$redirectConfig = New-AzureRmApplicationGatewayRedirectConfiguration `
  -Name myredirect `
  -RedirectType Temporary `
  -TargetUrl "http://bing.com"
$redirectRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name redirectRule `
  -RuleType Basic `
  -HttpListener $defaultListener `
  -RedirectConfiguration $redirectConfig
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="227b0-137">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-137">Create the application gateway</span></span>

<span data-ttu-id="227b0-138">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="227b0-138">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

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
  -HttpListeners $defaultListener `
  -RequestRoutingRules $redirectRule `
  -RedirectConfigurations $redirectConfig `
  -Sku $sku
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="227b0-139">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-139">Test the application gateway</span></span>

<span data-ttu-id="227b0-140">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="227b0-140">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="227b0-141">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="227b0-141">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

<span data-ttu-id="227b0-142">You should see *bing.com* appear in your browser.</span><span class="sxs-lookup"><span data-stu-id="227b0-142">You should see *bing.com* appear in your browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="227b0-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="227b0-143">Next steps</span></span>

<span data-ttu-id="227b0-144">In this article, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="227b0-144">In this article, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="227b0-145">Set up the network</span><span class="sxs-lookup"><span data-stu-id="227b0-145">Set up the network</span></span>
> * <span data-ttu-id="227b0-146">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="227b0-146">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="227b0-147">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-147">Create an application gateway</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="227b0-148">Learn more about what you can do with application gateway</span><span class="sxs-lookup"><span data-stu-id="227b0-148">Learn more about what you can do with application gateway</span></span>](./application-gateway-introduction.md)
