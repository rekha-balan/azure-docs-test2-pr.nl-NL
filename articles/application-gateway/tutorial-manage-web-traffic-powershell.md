---
title: Manage web traffic - Azure PowerShell
description: Learn how to create an application gateway with a virtual machine scale set to manage web traffic using Azure PowerShell.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 6/5/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 0ece839777747ac7f3683f6f475f3af9d050190e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869320"
---
# <a name="manage-web-traffic-with-an-application-gateway-using-azure-powershell"></a><span data-ttu-id="61651-103">Manage web traffic with an application gateway using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="61651-103">Manage web traffic with an application gateway using Azure PowerShell</span></span>

<span data-ttu-id="61651-104">Application gateway is used to manage and secure web traffic to servers that you maintain.</span><span class="sxs-lookup"><span data-stu-id="61651-104">Application gateway is used to manage and secure web traffic to servers that you maintain.</span></span> <span data-ttu-id="61651-105">You can use Azure PowerShell to create an [application gateway](overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers to manage web traffic.</span><span class="sxs-lookup"><span data-stu-id="61651-105">You can use Azure PowerShell to create an [application gateway](overview.md) that uses a [virtual machine scale set](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) for backend servers to manage web traffic.</span></span> <span data-ttu-id="61651-106">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="61651-106">In this example, the scale set contains two virtual machine instances that are added to the default backend pool of the application gateway.</span></span>

<span data-ttu-id="61651-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="61651-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61651-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="61651-108">Set up the network</span></span>
> * <span data-ttu-id="61651-109">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="61651-109">Create an application gateway</span></span>
> * <span data-ttu-id="61651-110">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="61651-110">Create a virtual machine scale set with the default backend pool</span></span>

<span data-ttu-id="61651-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="61651-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="61651-112">If you choose to install and use PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="61651-112">If you choose to install and use PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="61651-113">To find the version, run `Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="61651-113">To find the version, run `Get-Module -ListAvailable AzureRM`.</span></span> <span data-ttu-id="61651-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="61651-114">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="61651-115">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="61651-115">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="61651-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="61651-116">Create a resource group</span></span>

<span data-ttu-id="61651-117">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="61651-117">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="61651-118">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="61651-118">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="61651-119">Create network resources</span><span class="sxs-lookup"><span data-stu-id="61651-119">Create network resources</span></span> 

<span data-ttu-id="61651-120">Configure the subnets named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="61651-120">Configure the subnets named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="61651-121">Create the virtual network *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="61651-121">Create the virtual network *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="61651-122">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="61651-122">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="61651-123">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="61651-123">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="61651-124">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="61651-124">Create an application gateway</span></span>

<span data-ttu-id="61651-125">In this section you create resources that support the application gateway, and then finally create it.</span><span class="sxs-lookup"><span data-stu-id="61651-125">In this section you create resources that support the application gateway, and then finally create it.</span></span> <span data-ttu-id="61651-126">The resources that you create include:</span><span class="sxs-lookup"><span data-stu-id="61651-126">The resources that you create include:</span></span>

- <span data-ttu-id="61651-127">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span><span class="sxs-lookup"><span data-stu-id="61651-127">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span></span>
- <span data-ttu-id="61651-128">*Default pool* - All application gateways must have at least one backend pool of servers.</span><span class="sxs-lookup"><span data-stu-id="61651-128">*Default pool* - All application gateways must have at least one backend pool of servers.</span></span>
- <span data-ttu-id="61651-129">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span><span class="sxs-lookup"><span data-stu-id="61651-129">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="61651-130">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="61651-130">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="61651-131">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="61651-131">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="61651-132">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="61651-132">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span>

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

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="61651-133">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="61651-133">Create the backend pool and settings</span></span>

<span data-ttu-id="61651-134">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="61651-134">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="61651-135">Configure the settings for the backend address pools using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="61651-135">Configure the settings for the backend address pools using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

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

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="61651-136">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="61651-136">Create the default listener and rule</span></span>

<span data-ttu-id="61651-137">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="61651-137">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="61651-138">In this example, you create a basic listener that listens for traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="61651-138">In this example, you create a basic listener that listens for traffic at the root URL.</span></span> 

<span data-ttu-id="61651-139">Create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="61651-139">Create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="61651-140">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="61651-140">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="61651-141">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="61651-141">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$defaultlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name mydefaultListener `
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

### <a name="create-the-application-gateway"></a><span data-ttu-id="61651-142">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="61651-142">Create the application gateway</span></span>

<span data-ttu-id="61651-143">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="61651-143">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

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

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="61651-144">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="61651-144">Create a virtual machine scale set</span></span>

<span data-ttu-id="61651-145">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="61651-145">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="61651-146">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="61651-146">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

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
  -ImageReferenceVersion latest `
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

### <a name="install-iis"></a><span data-ttu-id="61651-147">Install IIS</span><span class="sxs-lookup"><span data-stu-id="61651-147">Install IIS</span></span>

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

## <a name="test-the-application-gateway"></a><span data-ttu-id="61651-148">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="61651-148">Test the application gateway</span></span>

<span data-ttu-id="61651-149">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="61651-149">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="61651-150">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="61651-150">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Test base URL in application gateway](./media/tutorial-manage-web-traffic-powershell/tutorial-iistest.png)

## <a name="clean-up-resources"></a><span data-ttu-id="61651-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="61651-152">Clean up resources</span></span>

<span data-ttu-id="61651-153">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="61651-153">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="61651-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="61651-154">Next steps</span></span>

<span data-ttu-id="61651-155">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="61651-155">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="61651-156">Set up the network</span><span class="sxs-lookup"><span data-stu-id="61651-156">Set up the network</span></span>
> * <span data-ttu-id="61651-157">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="61651-157">Create an application gateway</span></span>
> * <span data-ttu-id="61651-158">Create a virtual machine scale set with the default backend pool</span><span class="sxs-lookup"><span data-stu-id="61651-158">Create a virtual machine scale set with the default backend pool</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61651-159">Restrict web traffic with a web application firewall</span><span class="sxs-lookup"><span data-stu-id="61651-159">Restrict web traffic with a web application firewall</span></span>](./tutorial-restrict-web-traffic-powershell.md)
