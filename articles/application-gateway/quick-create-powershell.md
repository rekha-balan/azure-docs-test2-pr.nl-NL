---
title: Quickstart - Direct web traffic with Azure Application Gateway - Azure PowerShell | Microsoft Docs
description: Learn how use Azure PowerShell to create an Azure Application Gateway that directs web traffic to virtual machines in a backend pool.
services: application-gateway
author: vhorne
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: azurepowershell
ms.topic: quickstart
ms.workload: infrastructure-services
ms.date: 01/25/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: 95b806eaabaf0ba93b1e8b6823340e82842b0f1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869056"
---
# <a name="quickstart-direct-web-traffic-with-azure-application-gateway---azure-powershell"></a><span data-ttu-id="1b418-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b418-103">Quickstart: Direct web traffic with Azure Application Gateway - Azure PowerShell</span></span>

<span data-ttu-id="1b418-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span><span class="sxs-lookup"><span data-stu-id="1b418-104">With Azure Application Gateway, you can direct your application web traffic to specific resources by assigning listeners to ports, creating rules, and adding resources to a backend pool.</span></span>

<span data-ttu-id="1b418-105">This quickstart shows you how to use the Azure portal to quickly create the application gateway with two virtual machines in its backend pool.</span><span class="sxs-lookup"><span data-stu-id="1b418-105">This quickstart shows you how to use the Azure portal to quickly create the application gateway with two virtual machines in its backend pool.</span></span> <span data-ttu-id="1b418-106">You then test it to make sure it's working correctly.</span><span class="sxs-lookup"><span data-stu-id="1b418-106">You then test it to make sure it's working correctly.</span></span>

<span data-ttu-id="1b418-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="1b418-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="1b418-108">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="1b418-108">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="1b418-109">To find the version, run `Get-Module -ListAvailable AzureRM` .</span><span class="sxs-lookup"><span data-stu-id="1b418-109">To find the version, run `Get-Module -ListAvailable AzureRM` .</span></span> <span data-ttu-id="1b418-110">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="1b418-110">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="1b418-111">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="1b418-111">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="1b418-112">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="1b418-112">Create a resource group</span></span>

<span data-ttu-id="1b418-113">You need to always create resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="1b418-113">You need to always create resources in a resource group.</span></span> <span data-ttu-id="1b418-114">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="1b418-114">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> 

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="1b418-115">Create network resources</span><span class="sxs-lookup"><span data-stu-id="1b418-115">Create network resources</span></span> 

<span data-ttu-id="1b418-116">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span><span class="sxs-lookup"><span data-stu-id="1b418-116">You need to create a virtual network for the application gateway to be able to communicate with other resources.</span></span> <span data-ttu-id="1b418-117">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span><span class="sxs-lookup"><span data-stu-id="1b418-117">Two subnets are created in this example: one for the application gateway, and the other for the backend servers.</span></span> 

<span data-ttu-id="1b418-118">Create the subnet configurations using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="1b418-118">Create the subnet configurations using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="1b418-119">Create the virtual network using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="1b418-119">Create the virtual network using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="1b418-120">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="1b418-120">And finally, create the public IP address using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span>

```azurepowershell-interactive
$backendSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myAGSubnet `
  -AddressPrefix 10.0.1.0/24
$agSubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name myBackendSubnet `
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
## <a name="create-backend-servers"></a><span data-ttu-id="1b418-121">Create backend servers</span><span class="sxs-lookup"><span data-stu-id="1b418-121">Create backend servers</span></span>

<span data-ttu-id="1b418-122">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-122">In this example, you create two virtual machines to be used as backend servers for the application gateway.</span></span> 

<span data-ttu-id="1b418-123">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="1b418-123">You also install IIS on the virtual machines to verify that the application gateway was successfully created.</span></span>

### <a name="create-two-virtual-machines"></a><span data-ttu-id="1b418-124">Create two virtual machines</span><span class="sxs-lookup"><span data-stu-id="1b418-124">Create two virtual machines</span></span>

<span data-ttu-id="1b418-125">Create a network interface with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="1b418-125">Create a network interface with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="1b418-126">Create a virtual machine configuration with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="1b418-126">Create a virtual machine configuration with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="1b418-127">When you run the following commands, you are prompted for credentials.</span><span class="sxs-lookup"><span data-stu-id="1b418-127">When you run the following commands, you are prompted for credentials.</span></span> <span data-ttu-id="1b418-128">Enter *azureuser* for the user name and *Azure123456!*</span><span class="sxs-lookup"><span data-stu-id="1b418-128">Enter *azureuser* for the user name and *Azure123456!*</span></span> <span data-ttu-id="1b418-129">for the password.</span><span class="sxs-lookup"><span data-stu-id="1b418-129">for the password.</span></span> <span data-ttu-id="1b418-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="1b418-130">Create the virtual machine with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span>

```azurepowershell-interactive
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName myResourceGroupAG -Name myVNet
$cred = Get-Credential
for ($i=1; $i -le 2; $i++)
{
  $nic = New-AzureRmNetworkInterface `
    -Name myNic$i `
    -ResourceGroupName myResourceGroupAG `
    -Location EastUS `
    -SubnetId $vnet.Subnets[1].Id
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_DS2
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Add-AzureRmVMNetworkInterface `
    -VM $vm `
    -Id $nic.Id
  $vm = Set-AzureRmVMBootDiagnostics `
    -VM $vm `
    -Disable
  New-AzureRmVM -ResourceGroupName myResourceGroupAG -Location EastUS -VM $vm
  Set-AzureRmVMExtension `
    -ResourceGroupName myResourceGroupAG `
    -ExtensionName IIS `
    -VMName myVM$i `
    -Publisher Microsoft.Compute `
    -ExtensionType CustomScriptExtension `
    -TypeHandlerVersion 1.4 `
    -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
    -Location EastUS
}
```

## <a name="create-an-application-gateway"></a><span data-ttu-id="1b418-131">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="1b418-131">Create an application gateway</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="1b418-132">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="1b418-132">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="1b418-133">Use [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration) to create the configuration that associates the subnet that you previously created with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-133">Use [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration) to create the configuration that associates the subnet that you previously created with the application gateway.</span></span> <span data-ttu-id="1b418-134">Use [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig) to create the configuration that assigns the public IP address that you also previously created to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-134">Use [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig) to create the configuration that assigns the public IP address that you also previously created to the application gateway.</span></span> <span data-ttu-id="1b418-135">Use [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport) to assign port 80 to be used to access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-135">Use [New-AzureRmApplicationGatewayFrontendPort](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport) to assign port 80 to be used to access the application gateway.</span></span>

```azurepowershell-interactive
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName myResourceGroupAG -Name myVNet
$pip = Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress 
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

### <a name="create-the-backend-pool"></a><span data-ttu-id="1b418-136">Create the backend pool</span><span class="sxs-lookup"><span data-stu-id="1b418-136">Create the backend pool</span></span>

<span data-ttu-id="1b418-137">Use [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool) to create the backend pool for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-137">Use [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool) to create the backend pool for the application gateway.</span></span> <span data-ttu-id="1b418-138">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="1b418-138">Configure the settings for the backend pool using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

```azurepowershell-interactive
$address1 = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroupAG -Name myNic1
$address2 = Get-AzureRmNetworkInterface -ResourceGroupName myResourceGroupAG -Name myNic2
$backendPool = New-AzureRmApplicationGatewayBackendAddressPool `
  -Name myAGBackendPool `
  -BackendIPAddresses $address1.ipconfigurations[0].privateipaddress, $address2.ipconfigurations[0].privateipaddress
$poolSettings = New-AzureRmApplicationGatewayBackendHttpSettings `
  -Name myPoolSettings `
  -Port 80 `
  -Protocol Http `
  -CookieBasedAffinity Enabled `
  -RequestTimeout 120
```

### <a name="create-the-listener-and-add-a-rule"></a><span data-ttu-id="1b418-139">Create the listener and add a rule</span><span class="sxs-lookup"><span data-stu-id="1b418-139">Create the listener and add a rule</span></span>

<span data-ttu-id="1b418-140">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span><span class="sxs-lookup"><span data-stu-id="1b418-140">A listener is required to enable the application gateway to route traffic appropriately to the backend pool.</span></span> <span data-ttu-id="1b418-141">Create a listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="1b418-141">Create a listener using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="1b418-142">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="1b418-142">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="1b418-143">Use [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) to create a rule named *rule1*.</span><span class="sxs-lookup"><span data-stu-id="1b418-143">Use [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) to create a rule named *rule1*.</span></span>

```azurepowershell-interactive
$defaultlistener = New-AzureRmApplicationGatewayHttpListener `
  -Name myAGListener `
  -Protocol Http `
  -FrontendIPConfiguration $fipconfig `
  -FrontendPort $frontendport
$frontendRule = New-AzureRmApplicationGatewayRequestRoutingRule `
  -Name rule1 `
  -RuleType Basic `
  -HttpListener $defaultlistener `
  -BackendAddressPool $backendPool `
  -BackendHttpSettings $poolSettings
```

### <a name="create-the-application-gateway"></a><span data-ttu-id="1b418-144">Create the application gateway</span><span class="sxs-lookup"><span data-stu-id="1b418-144">Create the application gateway</span></span>

<span data-ttu-id="1b418-145">Now that you created the necessary supporting resources, use [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku) to specify parameters for the application gateway, and then use [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) to create it.</span><span class="sxs-lookup"><span data-stu-id="1b418-145">Now that you created the necessary supporting resources, use [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku) to specify parameters for the application gateway, and then use [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway) to create it.</span></span>

```azurepowershell-interactive
$sku = New-AzureRmApplicationGatewaySku `
  -Name Standard_Medium `
  -Tier Standard `
  -Capacity 2
New-AzureRmApplicationGateway `
  -Name myAppGateway `
  -ResourceGroupName myResourceGroupAG `
  -Location eastus `
  -BackendAddressPools $backendPool `
  -BackendHttpSettingsCollection $poolSettings `
  -FrontendIpConfigurations $fipconfig `
  -GatewayIpConfigurations $gipconfig `
  -FrontendPorts $frontendport `
  -HttpListeners $defaultlistener `
  -RequestRoutingRules $frontendRule `
  -Sku $sku
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="1b418-146">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="1b418-146">Test the application gateway</span></span>

<span data-ttu-id="1b418-147">Installing IIS is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span><span class="sxs-lookup"><span data-stu-id="1b418-147">Installing IIS is not required to create the application gateway, but you installed it in this quickstart to verify whether the application gateway was successfully created.</span></span> <span data-ttu-id="1b418-148">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="1b418-148">Use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="1b418-149">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="1b418-149">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Test application gateway](./media/quick-create-powershell/application-gateway-iistest.png)

<span data-ttu-id="1b418-151">When you refresh the browser, you should see the name of the other VM appear.</span><span class="sxs-lookup"><span data-stu-id="1b418-151">When you refresh the browser, you should see the name of the other VM appear.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1b418-152">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="1b418-152">Clean up resources</span></span>

<span data-ttu-id="1b418-153">First explore the resources that were created with the application gateway, and then when no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="1b418-153">First explore the resources that were created with the application gateway, and then when no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, application gateway, and all related resources.</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="1b418-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b418-154">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b418-155">Manage web traffic with an application gateway using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b418-155">Manage web traffic with an application gateway using Azure PowerShell</span></span>](./tutorial-manage-web-traffic-powershell.md)

