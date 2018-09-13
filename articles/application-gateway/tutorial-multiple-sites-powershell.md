---
title: Create an application gateway that hosts multiple web sites - Azure PowerShell
description: Learn how to create an application gateway that hosts multiple web sites using Azure Powershell.
services: application-gateway
author: vhorne
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 7d376ab958a1fb56753e033129ece84bc1c439c2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864913"
---
# <a name="create-an-application-gateway-that-hosts-multiple-web-sites-using-azure-powershell"></a><span data-ttu-id="3c3ce-103">Create an application gateway that hosts multiple web sites using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c3ce-103">Create an application gateway that hosts multiple web sites using Azure PowerShell</span></span>

<span data-ttu-id="3c3ce-104">You can use Azure Powershell to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-104">You can use Azure Powershell to [configure the hosting of multiple web sites](multiple-site-overview.md) when you create an [application gateway](overview.md).</span></span> <span data-ttu-id="3c3ce-105">In this tutorial, you define backend address pools using virtual machines scale sets.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-105">In this tutorial, you define backend address pools using virtual machines scale sets.</span></span> <span data-ttu-id="3c3ce-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-106">You then configure listeners and rules based on domains that you own to make sure web traffic arrives at the appropriate servers in the pools.</span></span> <span data-ttu-id="3c3ce-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-107">This tutorial assumes that you own multiple domains and uses examples of *www.contoso.com* and *www.fabrikam.com*.</span></span>

<span data-ttu-id="3c3ce-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="3c3ce-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c3ce-109">Set up the network</span><span class="sxs-lookup"><span data-stu-id="3c3ce-109">Set up the network</span></span>
> * <span data-ttu-id="3c3ce-110">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3c3ce-110">Create an application gateway</span></span>
> * <span data-ttu-id="3c3ce-111">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="3c3ce-111">Create backend listeners</span></span>
> * <span data-ttu-id="3c3ce-112">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="3c3ce-112">Create routing rules</span></span>
> * <span data-ttu-id="3c3ce-113">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="3c3ce-113">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="3c3ce-114">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="3c3ce-114">Create a CNAME record in your domain</span></span>

![Multi-site routing example](./media/tutorial-multiple-sites-powershell/scenario.png)

<span data-ttu-id="3c3ce-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-116">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="3c3ce-117">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-117">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="3c3ce-118">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="3c3ce-118">To find the version, run ` Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="3c3ce-119">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-119">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="3c3ce-120">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-120">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="3c3ce-121">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="3c3ce-121">Create a resource group</span></span>

<span data-ttu-id="3c3ce-122">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-122">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="3c3ce-123">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-123">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="3c3ce-124">Create network resources</span><span class="sxs-lookup"><span data-stu-id="3c3ce-124">Create network resources</span></span>

<span data-ttu-id="3c3ce-125">Create the subnet configurations using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-125">Create the subnet configurations using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="3c3ce-126">Create the virtual network using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-126">Create the virtual network using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="3c3ce-127">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-127">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="3c3ce-128">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-128">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="3c3ce-129">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3c3ce-129">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="3c3ce-130">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="3c3ce-130">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="3c3ce-131">Associate the subnet that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-131">Associate the subnet that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="3c3ce-132">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-132">Assign the public IP address to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span>

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

### <a name="create-the-backend-pools-and-settings"></a><span data-ttu-id="3c3ce-133">Create the backend pools and settings</span><span class="sxs-lookup"><span data-stu-id="3c3ce-133">Create the backend pools and settings</span></span>

<span data-ttu-id="3c3ce-134">Create the first backend address pool for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-134">Create the first backend address pool for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="3c3ce-135">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-135">Configure the settings for the pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```azurepowershell-interactive
$contosoPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name contosoPool

$fabrikamPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name fabrikamPool

$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-listeners-and-rules"></a><span data-ttu-id="3c3ce-136">Create the listeners and rules</span><span class="sxs-lookup"><span data-stu-id="3c3ce-136">Create the listeners and rules</span></span>

<span data-ttu-id="3c3ce-137">Listeners are required to enable the application gateway to route traffic appropriately to the backend address pools.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-137">Listeners are required to enable the application gateway to route traffic appropriately to the backend address pools.</span></span> <span data-ttu-id="3c3ce-138">In this tutorial, you create two listeners for your two domains.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-138">In this tutorial, you create two listeners for your two domains.</span></span> <span data-ttu-id="3c3ce-139">In this example, listeners are created for the domains of *www.contoso.com* and *www.fabrikam.com*.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-139">In this example, listeners are created for the domains of *www.contoso.com* and *www.fabrikam.com*.</span></span>

<span data-ttu-id="3c3ce-140">Create the first listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-140">Create the first listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="3c3ce-141">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-141">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="3c3ce-142">Create a basic rule named *contosoRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-142">Create a basic rule named *contosoRule* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

```azurepowershell-interactive
$contosolistener = New-AzureRmApplicationGatewayHttpListener `
  -Name contosoListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport `
  -HostName "www.contoso.com"

$fabrikamlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name fabrikamListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport `
  -HostName "www.fabrikam.com"

$contosoRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name contosoRule `
  -RuleType Basic `
  -HttpListener $contosoListener `
  -BackendAddressPool $contosoPool `
  -BackendHttpSettings $poolSettings

$fabrikamRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name fabrikamRule `
  -RuleType Basic `
  -HttpListener $fabrikamListener `
  -BackendAddressPool $fabrikamPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="3c3ce-143">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="3c3ce-143">Create the application gateway</span></span>

<span data-ttu-id="3c3ce-144">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-144">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku), and then create it using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

```azurepowershell-interactive
$sku = New-AzureRmApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2

$appgw = New-AzureRmApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -BackendAddressPools $contosoPool, $fabrikamPool `
  -BackendHttpSettingsCollection $poolSettings `
  -FrontendIpConfigurations $fipconfig `
  -GatewayIpConfigurations $gipconfig `
  -FrontendPorts $frontendport `
  -HttpListeners $contosoListener, $fabrikamListener `
  -RequestRoutingRules $contosoRule, $fabrikamRule `
  -Sku $sku
```

## <a name="create-virtual-machine-scale-sets"></a><span data-ttu-id="3c3ce-145">Create virtual machine scale sets</span><span class="sxs-lookup"><span data-stu-id="3c3ce-145">Create virtual machine scale sets</span></span>

<span data-ttu-id="3c3ce-146">In this example, you create two virtual machine scale sets that support the two backend pools that you created.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-146">In this example, you create two virtual machine scale sets that support the two backend pools that you created.</span></span> <span data-ttu-id="3c3ce-147">The scale sets that you create are named *myvmss1* and *myvmss2*.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-147">The scale sets that you create are named *myvmss1* and *myvmss2*.</span></span> <span data-ttu-id="3c3ce-148">Each scale set contains two virtual machine instances on which you install IIS.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-148">Each scale set contains two virtual machine instances on which you install IIS.</span></span> <span data-ttu-id="3c3ce-149">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-149">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

```azurepowershell-interactive
$vnet = Get-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupAG `
  -Name myVNet

$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$contosoPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name contosoPool `
  -ApplicationGateway $appgw

$fabrikamPool = Get-AzureRmApplicationGatewayBackendAddressPool `
  -Name fabrikamPool `
  -ApplicationGateway $appgw

for ($i=1; $i -le 2; $i++)
{
  if ($i -eq 1) 
  {
    $poolId = $contosoPool.Id
  }
  if ($i -eq 2)
  {
    $poolId = $fabrikamPool.Id
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

### <a name="install-iis"></a><span data-ttu-id="3c3ce-150">Install IIS</span><span class="sxs-lookup"><span data-stu-id="3c3ce-150">Install IIS</span></span>

```azurepowershell-interactive
$publicSettings = @{ "fileUris" = (,"https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/application-gateway/iis/appgatewayurl.ps1"); 
  "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File appgatewayurl.ps1" }

for ($i=1; $i -le 2; $i++)
{
  $vmss = Get-AzureRmVmss `
    -ResourceGroupName myResourceGroupAG `
    -VMScaleSetName myvmss$i

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

## <a name="create-cname-record-in-your-domain"></a><span data-ttu-id="3c3ce-151">Create CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="3c3ce-151">Create CNAME record in your domain</span></span>

<span data-ttu-id="3c3ce-152">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-152">After the application gateway is created with its public IP address, you can get the DNS address and use it to create a CNAME record in your domain.</span></span> <span data-ttu-id="3c3ce-153">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the DNS address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-153">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the DNS address of the application gateway.</span></span> <span data-ttu-id="3c3ce-154">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-154">Copy the *fqdn* value of the DNSSettings and use it as the value of the CNAME record that you create.</span></span> <span data-ttu-id="3c3ce-155">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-155">The use of A-records is not recommended because the VIP may change when the application gateway is restarted.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="3c3ce-156">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="3c3ce-156">Test the application gateway</span></span>

<span data-ttu-id="3c3ce-157">Enter your domain name into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-157">Enter your domain name into the address bar of your browser.</span></span> <span data-ttu-id="3c3ce-158">Such as, http://www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3c3ce-158">Such as, http://www.contoso.com.</span></span>

![Test contoso site in application gateway](./media/tutorial-multiple-sites-powershell/application-gateway-iistest.png)

<span data-ttu-id="3c3ce-160">Change the address to your other domain and you should see something like the following example:</span><span class="sxs-lookup"><span data-stu-id="3c3ce-160">Change the address to your other domain and you should see something like the following example:</span></span>

![Test fabrikam site in application gateway](./media/tutorial-multiple-sites-powershell/application-gateway-iistest2.png)

## <a name="clean-up-resources"></a><span data-ttu-id="3c3ce-162">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="3c3ce-162">Clean up resources</span></span>

<span data-ttu-id="3c3ce-163">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="3c3ce-163">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="3c3ce-164">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c3ce-164">Next steps</span></span>

<span data-ttu-id="3c3ce-165">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="3c3ce-165">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3c3ce-166">Set up the network</span><span class="sxs-lookup"><span data-stu-id="3c3ce-166">Set up the network</span></span>
> * <span data-ttu-id="3c3ce-167">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="3c3ce-167">Create an application gateway</span></span>
> * <span data-ttu-id="3c3ce-168">Create backend listeners</span><span class="sxs-lookup"><span data-stu-id="3c3ce-168">Create backend listeners</span></span>
> * <span data-ttu-id="3c3ce-169">Create routing rules</span><span class="sxs-lookup"><span data-stu-id="3c3ce-169">Create routing rules</span></span>
> * <span data-ttu-id="3c3ce-170">Create virtual machine scale sets with the backend pools</span><span class="sxs-lookup"><span data-stu-id="3c3ce-170">Create virtual machine scale sets with the backend pools</span></span>
> * <span data-ttu-id="3c3ce-171">Create a CNAME record in your domain</span><span class="sxs-lookup"><span data-stu-id="3c3ce-171">Create a CNAME record in your domain</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3c3ce-172">Create an application gateway with URL path-based routing rules</span><span class="sxs-lookup"><span data-stu-id="3c3ce-172">Create an application gateway with URL path-based routing rules</span></span>](./tutorial-url-route-powershell.md)