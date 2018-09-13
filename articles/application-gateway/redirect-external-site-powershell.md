---
title: Create an application gateway with external redirection - Azure PowerShell | Microsoft Docs
description: Learn how to create an application gateway that redirects web traffic to an external site using Azure Powershell.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/24/2018
ms.author: victorh
ms.openlocfilehash: ae3fcc65d3a377d3317e632f28a43263e1d1fce2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867562"
---
# <a name="create-an-application-gateway-with-external-redirection-using-azure-powershell"></a><span data-ttu-id="57e3f-103">Create an application gateway with external redirection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="57e3f-103">Create an application gateway with external redirection using Azure PowerShell</span></span>

<span data-ttu-id="57e3f-104">You can use Azure Powershell to configure [web traffic redirection](multiple-site-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="57e3f-104">You can use Azure Powershell to configure [web traffic redirection](multiple-site-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="57e3f-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span><span class="sxs-lookup"><span data-stu-id="57e3f-105">In this tutorial, you configure a listener and rule that redirects web traffic that arrives at the application gateway to an external site.</span></span>

<span data-ttu-id="57e3f-106">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="57e3f-106">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57e3f-107">Set up the network</span><span class="sxs-lookup"><span data-stu-id="57e3f-107">Set up the network</span></span>
> * <span data-ttu-id="57e3f-108">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="57e3f-108">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="57e3f-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="57e3f-109">Create an application gateway</span></span>

<span data-ttu-id="57e3f-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="57e3f-110">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="57e3f-111">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="57e3f-111">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="57e3f-112">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="57e3f-112">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="57e3f-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="57e3f-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="57e3f-114">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="57e3f-114">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="57e3f-115">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="57e3f-115">Create a resource group</span></span>

<span data-ttu-id="57e3f-116">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="57e3f-116">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="57e3f-117">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="57e3f-117">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="57e3f-118">Create network resources</span><span class="sxs-lookup"><span data-stu-id="57e3f-118">Create network resources</span></span>

<span data-ttu-id="57e3f-119">Create the subnet configuration *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="57e3f-119">Create the subnet configuration *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="57e3f-120">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="57e3f-120">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configuration.</span></span> <span data-ttu-id="57e3f-121">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="57e3f-121">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="57e3f-122">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="57e3f-122">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="57e3f-123">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="57e3f-123">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="57e3f-124">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="57e3f-124">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="57e3f-125">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="57e3f-125">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="57e3f-126">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="57e3f-126">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span> <span data-ttu-id="57e3f-127">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="57e3f-127">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span></span>

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

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="57e3f-128">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="57e3f-128">Create the backend pool and settings</span></span>

<span data-ttu-id="57e3f-129">Create the backend pool named *defaultPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="57e3f-129">Create the backend pool named *defaultPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="57e3f-130">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="57e3f-130">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

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

### <a name="create-the-listener-and-rule"></a><span data-ttu-id="57e3f-131">Create the listener and rule</span><span class="sxs-lookup"><span data-stu-id="57e3f-131">Create the listener and rule</span></span>

<span data-ttu-id="57e3f-132">A listener is required to enable the application gateway to appropriately route traffic.</span><span class="sxs-lookup"><span data-stu-id="57e3f-132">A listener is required to enable the application gateway to appropriately route traffic.</span></span> <span data-ttu-id="57e3f-133">Create the listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="57e3f-133">Create the listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="57e3f-134">A rule is required for the listener to know where to send incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="57e3f-134">A rule is required for the listener to know where to send incoming traffic.</span></span> <span data-ttu-id="57e3f-135">Create a basic rule named *redirectRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="57e3f-135">Create a basic rule named *redirectRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

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

### <a name="create-the-application-gateway"></a><span data-ttu-id="57e3f-136">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="57e3f-136">Create the application gateway</span></span>

<span data-ttu-id="57e3f-137">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="57e3f-137">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

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

## <a name="test-the-application-gateway"></a><span data-ttu-id="57e3f-138">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="57e3f-138">Test the application gateway</span></span>

<span data-ttu-id="57e3f-139">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="57e3f-139">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="57e3f-140">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="57e3f-140">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

<span data-ttu-id="57e3f-141">You should see *bing.com* appear in your browser.</span><span class="sxs-lookup"><span data-stu-id="57e3f-141">You should see *bing.com* appear in your browser.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57e3f-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="57e3f-142">Next steps</span></span>

<span data-ttu-id="57e3f-143">In this article, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="57e3f-143">In this article, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57e3f-144">Set up the network</span><span class="sxs-lookup"><span data-stu-id="57e3f-144">Set up the network</span></span>
> * <span data-ttu-id="57e3f-145">Create a listener and redirection rule</span><span class="sxs-lookup"><span data-stu-id="57e3f-145">Create a listener and redirection rule</span></span>
> * <span data-ttu-id="57e3f-146">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="57e3f-146">Create an application gateway</span></span>