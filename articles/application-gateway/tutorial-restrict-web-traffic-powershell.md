---
title: Restrict web traffic with a web application firewall - Azure PowerShell
description: Learn how to restrict web traffic with a web application firewall on an application gateway using Azure PowerShell.
services: application-gateway
author: vhorne
manager: jpconnock
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: tutorial
ms.workload: infrastructure-services
ms.date: 7/13/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: d7610d1f73db022ef2af41f51b67176857525a20
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856784"
---
# <a name="enable-web-application-firewall-using-azure-powershell"></a><span data-ttu-id="e2c17-103">Enable web application firewall using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2c17-103">Enable web application firewall using Azure PowerShell</span></span>

<span data-ttu-id="e2c17-104">You can restrict traffic on an [application gateway](overview.md) with a [web application firewall](waf-overview.md) (WAF).</span><span class="sxs-lookup"><span data-stu-id="e2c17-104">You can restrict traffic on an [application gateway](overview.md) with a [web application firewall](waf-overview.md) (WAF).</span></span> <span data-ttu-id="e2c17-105">The WAF uses [OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) rules to protect your application.</span><span class="sxs-lookup"><span data-stu-id="e2c17-105">The WAF uses [OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) rules to protect your application.</span></span> <span data-ttu-id="e2c17-106">These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.</span><span class="sxs-lookup"><span data-stu-id="e2c17-106">These rules include protection against attacks such as SQL injection, cross-site scripting attacks, and session hijacks.</span></span> 

<span data-ttu-id="e2c17-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e2c17-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2c17-108">Set up the network</span><span class="sxs-lookup"><span data-stu-id="e2c17-108">Set up the network</span></span>
> * <span data-ttu-id="e2c17-109">Create an application gateway with WAF enabled</span><span class="sxs-lookup"><span data-stu-id="e2c17-109">Create an application gateway with WAF enabled</span></span>
> * <span data-ttu-id="e2c17-110">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="e2c17-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e2c17-111">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e2c17-111">Create a storage account and configure diagnostics</span></span>

![Web application firewall example](./media/tutorial-restrict-web-traffic-powershell/scenario-waf.png)

<span data-ttu-id="e2c17-113">If you prefer, you can complete this tutorial using [Azure CLI](tutorial-restrict-web-traffic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e2c17-113">If you prefer, you can complete this tutorial using [Azure CLI](tutorial-restrict-web-traffic-cli.md).</span></span>

<span data-ttu-id="e2c17-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="e2c17-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="e2c17-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span><span class="sxs-lookup"><span data-stu-id="e2c17-115">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="e2c17-116">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="e2c17-116">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="e2c17-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="e2c17-117">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="e2c17-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="e2c17-118">If you are running PowerShell locally, you also need to run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="e2c17-119">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="e2c17-119">Create a resource group</span></span>

<span data-ttu-id="e2c17-120">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="e2c17-120">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e2c17-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e2c17-121">Create an Azure resource group using [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span>  

```azurepowershell-interactive
New-AzureRmResourceGroup -Name myResourceGroupAG -Location eastus
```

## <a name="create-network-resources"></a><span data-ttu-id="e2c17-122">Create network resources</span><span class="sxs-lookup"><span data-stu-id="e2c17-122">Create network resources</span></span> 

<span data-ttu-id="e2c17-123">Create the subnet configurations named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="e2c17-123">Create the subnet configurations named *myBackendSubnet* and *myAGSubnet* using [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="e2c17-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="e2c17-124">Create the virtual network named *myVNet* using [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) with the subnet configurations.</span></span> <span data-ttu-id="e2c17-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="e2c17-125">And finally, create the public IP address named *myAGPublicIPAddress* using [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="e2c17-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span><span class="sxs-lookup"><span data-stu-id="e2c17-126">These resources are used to provide network connectivity to the application gateway and its associated resources.</span></span>

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

## <a name="create-an-application-gateway"></a><span data-ttu-id="e2c17-127">Create an application gateway</span><span class="sxs-lookup"><span data-stu-id="e2c17-127">Create an application gateway</span></span>

<span data-ttu-id="e2c17-128">In this section you create resources that support the application gateway, and then finally create it and a WAF.</span><span class="sxs-lookup"><span data-stu-id="e2c17-128">In this section you create resources that support the application gateway, and then finally create it and a WAF.</span></span> <span data-ttu-id="e2c17-129">The resources that you create include:</span><span class="sxs-lookup"><span data-stu-id="e2c17-129">The resources that you create include:</span></span>

- <span data-ttu-id="e2c17-130">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span><span class="sxs-lookup"><span data-stu-id="e2c17-130">*IP configurations and frontend port* - Associates the subnet that you previously created to the application gateway and assigns a port to use to access it.</span></span>
- <span data-ttu-id="e2c17-131">*Default pool* - All application gateways must have at least one backend pool of servers.</span><span class="sxs-lookup"><span data-stu-id="e2c17-131">*Default pool* - All application gateways must have at least one backend pool of servers.</span></span>
- <span data-ttu-id="e2c17-132">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span><span class="sxs-lookup"><span data-stu-id="e2c17-132">*Default listener and rule* - The default listener listens for traffic on the port that was assigned and the default rule sends traffic to the default pool.</span></span>

### <a name="create-the-ip-configurations-and-frontend-port"></a><span data-ttu-id="e2c17-133">Create the IP configurations and frontend port</span><span class="sxs-lookup"><span data-stu-id="e2c17-133">Create the IP configurations and frontend port</span></span>

<span data-ttu-id="e2c17-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span><span class="sxs-lookup"><span data-stu-id="e2c17-134">Associate *myAGSubnet* that you previously created to the application gateway using [New-AzureRmApplicationGatewayIPConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration).</span></span> <span data-ttu-id="e2c17-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="e2c17-135">Assign *myAGPublicIPAddress* to the application gateway using [New-AzureRmApplicationGatewayFrontendIPConfig](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig).</span></span>

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

### <a name="create-the-backend-pool-and-settings"></a><span data-ttu-id="e2c17-136">Create the backend pool and settings</span><span class="sxs-lookup"><span data-stu-id="e2c17-136">Create the backend pool and settings</span></span>

<span data-ttu-id="e2c17-137">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span><span class="sxs-lookup"><span data-stu-id="e2c17-137">Create the backend pool named *appGatewayBackendPool* for the application gateway using [New-AzureRmApplicationGatewayBackendAddressPool](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool).</span></span> <span data-ttu-id="e2c17-138">Configure the settings for the backend address pools using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span><span class="sxs-lookup"><span data-stu-id="e2c17-138">Configure the settings for the backend address pools using [New-AzureRmApplicationGatewayBackendHttpSettings](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings).</span></span>

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

### <a name="create-the-default-listener-and-rule"></a><span data-ttu-id="e2c17-139">Create the default listener and rule</span><span class="sxs-lookup"><span data-stu-id="e2c17-139">Create the default listener and rule</span></span>

<span data-ttu-id="e2c17-140">A listener is required to enable the application gateway to route traffic appropriately to the backend address pools.</span><span class="sxs-lookup"><span data-stu-id="e2c17-140">A listener is required to enable the application gateway to route traffic appropriately to the backend address pools.</span></span> <span data-ttu-id="e2c17-141">In this example, you create a basic listener that listens for traffic at the root URL.</span><span class="sxs-lookup"><span data-stu-id="e2c17-141">In this example, you create a basic listener that listens for traffic at the root URL.</span></span> 

<span data-ttu-id="e2c17-142">Create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span><span class="sxs-lookup"><span data-stu-id="e2c17-142">Create a listener named *mydefaultListener* using [New-AzureRmApplicationGatewayHttpListener](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) with the frontend configuration and frontend port that you previously created.</span></span> <span data-ttu-id="e2c17-143">A rule is required for the listener to know which backend pool to use for incoming traffic.</span><span class="sxs-lookup"><span data-stu-id="e2c17-143">A rule is required for the listener to know which backend pool to use for incoming traffic.</span></span> <span data-ttu-id="e2c17-144">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span><span class="sxs-lookup"><span data-stu-id="e2c17-144">Create a basic rule named *rule1* using [New-AzureRmApplicationGatewayRequestRoutingRule](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule).</span></span>

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

### <a name="create-the-application-gateway-with-the-waf"></a><span data-ttu-id="e2c17-145">Create the application gateway with the WAF</span><span class="sxs-lookup"><span data-stu-id="e2c17-145">Create the application gateway with the WAF</span></span>

<span data-ttu-id="e2c17-146">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku).</span><span class="sxs-lookup"><span data-stu-id="e2c17-146">Now that you created the necessary supporting resources, specify parameters for the application gateway using [New-AzureRmApplicationGatewaySku](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku).</span></span> <span data-ttu-id="e2c17-147">Specify the WAF configuration using [New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewaywebapplicationfirewallconfiguration).</span><span class="sxs-lookup"><span data-stu-id="e2c17-147">Specify the WAF configuration using [New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration](/powershell/module/azurerm.network/new-azurermapplicationgatewaywebapplicationfirewallconfiguration).</span></span> <span data-ttu-id="e2c17-148">And then create the application gateway named *myAppGateway* using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span><span class="sxs-lookup"><span data-stu-id="e2c17-148">And then create the application gateway named *myAppGateway* using [New-AzureRmApplicationGateway](/powershell/module/azurerm.network/new-azurermapplicationgateway).</span></span>

```azurepowershell-interactive
$sku = New-AzureRmApplicationGatewaySku `
  -Name WAF_Medium `
  -Tier WAF `
  -Capacity 2

$wafConfig = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration `
  -Enabled $true `
  -FirewallMode "Detection"

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
  -WebApplicationFirewallConfig $wafConfig
```

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="e2c17-149">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="e2c17-149">Create a virtual machine scale set</span></span>

<span data-ttu-id="e2c17-150">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e2c17-150">In this example, you create a virtual machine scale set to provide servers for the backend pool in the application gateway.</span></span> <span data-ttu-id="e2c17-151">You assign the scale set to the backend pool when you configure the IP settings.</span><span class="sxs-lookup"><span data-stu-id="e2c17-151">You assign the scale set to the backend pool when you configure the IP settings.</span></span>

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

### <a name="install-iis"></a><span data-ttu-id="e2c17-152">Install IIS</span><span class="sxs-lookup"><span data-stu-id="e2c17-152">Install IIS</span></span>

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

## <a name="create-a-storage-account-and-configure-diagnostics"></a><span data-ttu-id="e2c17-153">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e2c17-153">Create a storage account and configure diagnostics</span></span>

<span data-ttu-id="e2c17-154">In this tutorial, the application gateway uses a storage account to store data for detection and prevention purposes.</span><span class="sxs-lookup"><span data-stu-id="e2c17-154">In this tutorial, the application gateway uses a storage account to store data for detection and prevention purposes.</span></span> <span data-ttu-id="e2c17-155">You could also use Log Analytics or Event Hub to record data.</span><span class="sxs-lookup"><span data-stu-id="e2c17-155">You could also use Log Analytics or Event Hub to record data.</span></span>

### <a name="create-the-storage-account"></a><span data-ttu-id="e2c17-156">Create the storage account</span><span class="sxs-lookup"><span data-stu-id="e2c17-156">Create the storage account</span></span>

<span data-ttu-id="e2c17-157">Create a storage account named *myagstore1* using [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span><span class="sxs-lookup"><span data-stu-id="e2c17-157">Create a storage account named *myagstore1* using [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount).</span></span>

```azurepowershell-interactive
$storageAccount = New-AzureRmStorageAccount `
  -ResourceGroupName myResourceGroupAG `
  -Name myagstore1 `
  -Location eastus `
  -SkuName "Standard_LRS"
```

### <a name="configure-diagnostics"></a><span data-ttu-id="e2c17-158">Configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e2c17-158">Configure diagnostics</span></span>

<span data-ttu-id="e2c17-159">Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs using [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting).</span><span class="sxs-lookup"><span data-stu-id="e2c17-159">Configure diagnostics to record data into the ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, and ApplicationGatewayFirewallLog logs using [Set-AzureRmDiagnosticSetting](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting).</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName myResourceGroupAG `
  -Name myAppGateway

$store = Get-AzureRmStorageAccount `
  -ResourceGroupName myResourceGroupAG `
  -Name myagstore1

Set-AzureRmDiagnosticSetting `
  -ResourceId $appgw.Id `
  -StorageAccountId $store.Id `
  -Categories ApplicationGatewayAccessLog, ApplicationGatewayPerformanceLog, ApplicationGatewayFirewallLog `
  -Enabled $true `
  -RetentionEnabled $true `
  -RetentionInDays 30
```

## <a name="test-the-application-gateway"></a><span data-ttu-id="e2c17-160">Test the application gateway</span><span class="sxs-lookup"><span data-stu-id="e2c17-160">Test the application gateway</span></span>

<span data-ttu-id="e2c17-161">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span><span class="sxs-lookup"><span data-stu-id="e2c17-161">You can use [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) to get the public IP address of the application gateway.</span></span> <span data-ttu-id="e2c17-162">Copy the public IP address, and then paste it into the address bar of your browser.</span><span class="sxs-lookup"><span data-stu-id="e2c17-162">Copy the public IP address, and then paste it into the address bar of your browser.</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupAG -Name myAGPublicIPAddress
```

![Test base URL in application gateway](./media/tutorial-restrict-web-traffic-powershell/application-gateway-iistest.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e2c17-164">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e2c17-164">Clean up resources</span></span>

<span data-ttu-id="e2c17-165">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="e2c17-165">When no longer needed, remove the resource group, application gateway, and all related resources using [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup).</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="next-steps"></a><span data-ttu-id="e2c17-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2c17-166">Next steps</span></span>

<span data-ttu-id="e2c17-167">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="e2c17-167">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e2c17-168">Set up the network</span><span class="sxs-lookup"><span data-stu-id="e2c17-168">Set up the network</span></span>
> * <span data-ttu-id="e2c17-169">Create an application gateway with WAF enabled</span><span class="sxs-lookup"><span data-stu-id="e2c17-169">Create an application gateway with WAF enabled</span></span>
> * <span data-ttu-id="e2c17-170">Create a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="e2c17-170">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e2c17-171">Create a storage account and configure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e2c17-171">Create a storage account and configure diagnostics</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e2c17-172">Create an application gateway with SSL termination</span><span class="sxs-lookup"><span data-stu-id="e2c17-172">Create an application gateway with SSL termination</span></span>](./tutorial-ssl-powershell.md)