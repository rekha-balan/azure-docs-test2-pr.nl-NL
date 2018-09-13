---
title: Create an application gateway with internal redirection - Azure PowerShell | Microsoft Docs
description: Learn how to create an application gateway that redirects internal web traffic to the appropriate backend pool of servers using Azure Powershell.
services: application-gateway
author: vhorne
manager: jpconnock
editor: tysonn
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.openlocfilehash: 47780b9c1d6a83dfedb9607dee3ac4c89b443f93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870152"
---
# <a name="create-an-application-gateway-with-internal-redirection-using-azure-powershell"></a><span data-ttu-id="1ae15-103">Create an application gateway with internal redirection using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ae15-103">Create an application gateway with internal redirection using Azure PowerShell</span></span>

<span data-ttu-id="1ae15-104">You can use Azure Powershell to configure [web traffic redirection](multiple-site-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="1ae15-104">You can use Azure Powershell to configure [web traffic redirection](multiple-site-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="1ae15-105">In this tutorial, you define a backend pool using a virtual machines scale set.</span><span class="sxs-lookup"><span data-stu-id="1ae15-105">In this tutorial, you define a backend pool using a virtual machines scale set.</span></span> <span data-ttu-id="1ae15-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate pool.</span><span class="sxs-lookup"><span data-stu-id="1ae15-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate pool.</span></span> <span data-ttu-id="1ae15-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.contoso.org*.</span><span class="sxs-lookup"><span data-stu-id="1ae15-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.contoso.org*.</span></span>

<span data-ttu-id="1ae15-108">In this article, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1ae15-108">In this article, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ae15-109">Set up the network</span><span class="sxs-lookup"><span data-stu-id="1ae15-109">Set up the network</span></span>
> * <span data-ttu-id="1ae15-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1ae15-110">Create an application gateway</span></span>
> * <span data-ttu-id="1ae15-111">Add listeners and redirection rule</span><span class="sxs-lookup"><span data-stu-id="1ae15-111">Add listeners and redirection rule</span></span>
> * <span data-ttu-id="1ae15-112">Create a virtual machine scale set with the backend pool</span><span class="sxs-lookup"><span data-stu-id="1ae15-112">Create a virtual machine scale set with the backend pool</span></span>
> * <span data-ttu-id="1ae15-113">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1ae15-113">Create a CNAME record in your domain</span></span>

<span data-ttu-id="1ae15-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1ae15-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="1ae15-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="1ae15-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1ae15-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="1ae15-116">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="1ae15-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1ae15-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="1ae15-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="1ae15-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="1ae15-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="1ae15-119">Create a resource group</span></span>

<span data-ttu-id="1ae15-120">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="1ae15-120">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="1ae15-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1ae15-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="1ae15-122">Create network resources</span><span class="sxs-lookup"><span data-stu-id="1ae15-122">Create network resources</span></span>

<span data-ttu-id="1ae15-123">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="1ae15-123">Create the subnet configurations for *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="1ae15-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="1ae15-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="1ae15-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="1ae15-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="1ae15-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="1ae15-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="1ae15-127">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1ae15-127">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="1ae15-128">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="1ae15-128">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="1ae15-129">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="1ae15-129">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="1ae15-130">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="1ae15-130">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span> <span data-ttu-id="1ae15-131">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span><span class="sxs-lookup"><span data-stu-id="1ae15-131">And then you can create the HTTP port using [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport).</span></span>

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
$frontendPort = New-AzureRmApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -Port 80
```

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="1ae15-132">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="1ae15-132">Create the backend pool and settings</span></span>

<span data-ttu-id="1ae15-133">Create a backend pool named *contosoPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="1ae15-133">Create a backend pool named *contosoPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="1ae15-134">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="1ae15-134">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```azurepowershell-interactive
$contosoPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name contosoPool 
$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-first-listener-and-rule"></a><span data-ttu-id="1ae15-135">Create the first listener and rule</span><span class="sxs-lookup"><span data-stu-id="1ae15-135">Create the first listener and rule</span></span>

<span data-ttu-id="1ae15-136">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="1ae15-136">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="1ae15-137">In this tutorial, you create two listeners for your two domains.</span><span class="sxs-lookup"><span data-stu-id="1ae15-137">In this tutorial, you create two listeners for your two domains.</span></span> <span data-ttu-id="1ae15-138">In this example, listeners are created for the domains of *www.contoso.com* and *www.contoso.org*.</span><span class="sxs-lookup"><span data-stu-id="1ae15-138">In this example, listeners are created for the domains of *www.contoso.com* and *www.contoso.org*.</span></span>

<span data-ttu-id="1ae15-139">Create the first listener named *contosoComListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="1ae15-139">Create the first listener named *contosoComListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="1ae15-140">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="1ae15-140">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="1ae15-141">Create a basic rule named *contosoComRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="1ae15-141">Create a basic rule named *contosoComRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$contosoComlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name contosoComListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendPort `
  -HostName "www.contoso.com"
$frontendRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name contosoComRule `
  -RuleType Basic `
  -HttpListener $contosoComListener `
  -BackendAddressPool $contosoPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="1ae15-142">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="1ae15-142">Create the application gateway</span></span>

<span data-ttu-id="1ae15-143">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="1ae15-143">Now that you created the necessary supporting resources, specify parameters for the application gateway named *myAppGateway* using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

```azurepowershell-interactive
$sku = New-AzureRmApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2
$appgw = New-AzureRmApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -BackendAddressPools $contosoPool `
  -BackendHttpSettingsCollection $poolSettings `
  -FrontendIpConfigurations $fipconfig `
  -GatewayIpConfigurations $gipconfig `
  -FrontendPorts $frontendPort `
  -HttpListeners $contosoComListener `
  -RequestRoutingRules $frontendRule `
  -Sku $sku
```

### <a name="add-the-second-listener"></a><span data-ttu-id="1ae15-144">Add the second listener</span><span class="sxs-lookup"><span data-stu-id="1ae15-144">Add the second listener</span></span>

<span data-ttu-id="1ae15-145">Add the listener named *contosoOrgListener* that's needed to redirect traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span><span class="sxs-lookup"><span data-stu-id="1ae15-145">Add the listener named *contosoOrgListener* that's needed to redirect traffic using [Add-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/add-azurermapplicationgatewayhttplistener).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway
$frontendPort = Get-AzureRmApplicationGatewayFrontendPort `
  -Name myFrontendPort `
  -ApplicationGateway $appgw
$ipconfig = Get-AzureRmApplicationGatewayFrontendIPConfig `
  -Name myAGFrontendIPConfig `
  -ApplicationGateway $appgw
Add-AzureRmApplicationGatewayHttpListener `
  -ApplicationGateway $appgw `
  -Name contosoOrgListener `
  -Protocol Http `
  -FrontendIPConfiguration $ipconfig `
  -FrontendPort $frontendPort `
  -HostName "www.contoso.org"
Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-the-redirection-configuration"></a><span data-ttu-id="1ae15-146">Add the redirection configuration</span><span class="sxs-lookup"><span data-stu-id="1ae15-146">Add the redirection configuration</span></span>

<span data-ttu-id="1ae15-147">You can cconfigure redirection for the listener using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span><span class="sxs-lookup"><span data-stu-id="1ae15-147">You can cconfigure redirection for the listener using [Add-AzureRmApplicationGatewayRedirectConfiguration](/powershell/module/azurerm.network/add-azurermapplicationgatewayredirectconfiguration).</span></span> 

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway
$contosoComlistener = Get-AzureRmApplicationGatewayHttpListener `
  -Name contosoComListener `
  -ApplicationGateway $appgw
$contosoOrglistener = Get-AzureRmApplicationGatewayHttpListener `
  -Name contosoOrgListener `
  -ApplicationGateway $appgw
Add-AzureRmApplicationGatewayRedirectConfiguration `
  -ApplicationGateway $appgw `
  -Name redirectOrgtoCom `
  -RedirectType Found `
  -TargetListener $contosoComListener `
  -IncludePath $true `
  -IncludeQueryString $true
Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

### <a name="add-the-second-routing-rule"></a><span data-ttu-id="1ae15-148">Add the second routing rule</span><span class="sxs-lookup"><span data-stu-id="1ae15-148">Add the second routing rule</span></span>

<span data-ttu-id="1ae15-149">You can then associate the redirection configuration to a new rule named *contosoOrgRule* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="1ae15-149">You can then associate the redirection configuration to a new rule named *contosoOrgRule* using [Add-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/add-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway
$contosoOrglistener = Get-AzureRmApplicationGatewayHttpListener `
  -Name contosoOrgListener `
  -ApplicationGateway $appgw
$redirectConfig = Get-AzureRmApplicationGatewayRedirectConfiguration `
  -Name redirectOrgtoCom `
  -ApplicationGateway $appgw   
Add-AzureRmApplicationGatewayRequestRoutingRule `
  -ApplicationGateway $appgw `
  -Name contosoOrgRule `
  -RuleType Basic `
  -HttpListener $contosoOrgListener `
  -RedirectConfiguration $redirectConfig
Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="1ae15-150">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="1ae15-150">Create a virtual machine scale set</span></span>

<span data-ttu-id="1ae15-151">In this example, you create a virtual machine scale set that supports the backend pool that you created.</span><span class="sxs-lookup"><span data-stu-id="1ae15-151">In this example, you create a virtual machine scale set that supports the backend pool that you created.</span></span> <span data-ttu-id="1ae15-152">The scale set that you create is named *myvmss* and contains two virtual machine instances on which you install IIS.</span><span class="sxs-lookup"><span data-stu-id="1ae15-152">The scale set that you create is named *myvmss* and contains two virtual machine instances on which you install IIS.</span></span> <span data-ttu-id="1ae15-153">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="1ae15-153">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

```azurepowershell-interactive
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway
$backendPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name contosoPool `
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

### <a name="install-iis"></a><span data-ttu-id="1ae15-154">Install IIS</span><span class="sxs-lookup"><span data-stu-id="1ae15-154">Install IIS</span></span>

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

## <a name="create-cname-record-in-your-domain"></a><span data-ttu-id="1ae15-155">Create CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1ae15-155">Create CNAME record in your domain</span></span>

<span data-ttu-id="1ae15-156">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="1ae15-156">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="1ae15-157">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the DNS address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1ae15-157">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the DNS address of the application gateway.</span></span> <span data-ttu-id="1ae15-158">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span><span class="sxs-lookup"><span data-stu-id="1ae15-158">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span></span> <span data-ttu-id="1ae15-159">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="1ae15-159">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="1ae15-160">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="1ae15-160">Test the application gateway</span></span>

<span data-ttu-id="1ae15-161">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="1ae15-161">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="1ae15-162">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1ae15-162">Such as, http://www.contoso.com.</span></span>

![Test contoso site in application gateway](./media/redirect-internal-site-powershell/application-gateway-iistest.png)

<span data-ttu-id="1ae15-164">Change the address to your other domain, for example http://www.contoso.org and you should see that the traffic has been redirected back to the listener for www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="1ae15-164">Change the address to your other domain, for example http://www.contoso.org and you should see that the traffic has been redirected back to the listener for www.contoso.com.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ae15-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ae15-165">Next steps</span></span>

<span data-ttu-id="1ae15-166">In this article, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="1ae15-166">In this article, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1ae15-167">Set up the network</span><span class="sxs-lookup"><span data-stu-id="1ae15-167">Set up the network</span></span>
> * <span data-ttu-id="1ae15-168">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1ae15-168">Create an application gateway</span></span>
> * <span data-ttu-id="1ae15-169">Add listeners and redirection rule</span><span class="sxs-lookup"><span data-stu-id="1ae15-169">Add listeners and redirection rule</span></span>
> * <span data-ttu-id="1ae15-170">Create a virtual machine scale set with the backend pools</span><span class="sxs-lookup"><span data-stu-id="1ae15-170">Create a virtual machine scale set with the backend pools</span></span>
> * <span data-ttu-id="1ae15-171">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="1ae15-171">Create a CNAME record in your domain</span></span>