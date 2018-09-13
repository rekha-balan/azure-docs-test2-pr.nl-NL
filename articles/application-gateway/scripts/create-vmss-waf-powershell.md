---
title: Azure PowerShell Script Sample - Restrict web traffic | Microsoft Docs
description: Azure PowerShell Script Sample - Create an application gateway with a web application firewall and a virtual machine scale set that uses OWASP rules to restrict traffic.
services: application-gateway
documentationcenter: networking
author: vhorne
manager: jpconnock
editor: tysonn
tags: azure-resource-manager
ms.service: application-gateway
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 01/29/2018
ms.author: victorh
ms.custom: mvc
ms.openlocfilehash: d6f8083e0070435e6ad8bb0dc0ff520b58c7eead
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864620"
---
# <a name="restrict-web-traffic-using-azure-powershell"></a><span data-ttu-id="a2344-103">Restrict web traffic using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2344-103">Restrict web traffic using Azure PowerShell</span></span>

<span data-ttu-id="a2344-104">This script creates an application gateway with a web application firewall that uses a virtual machine scale set for backend servers.</span><span class="sxs-lookup"><span data-stu-id="a2344-104">This script creates an application gateway with a web application firewall that uses a virtual machine scale set for backend servers.</span></span> <span data-ttu-id="a2344-105">The web application firewall restricts web traffic based on OWASP rules.</span><span class="sxs-lookup"><span data-stu-id="a2344-105">The web application firewall restricts web traffic based on OWASP rules.</span></span> <span data-ttu-id="a2344-106">After running the script, you can test the application gateway using its public IP address.</span><span class="sxs-lookup"><span data-stu-id="a2344-106">After running the script, you can test the application gateway using its public IP address.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a2344-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="a2344-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/application-gateway/create-vmss/create-vmss-waf.ps1 "Create application gateway with WAF")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a2344-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="a2344-108">Clean up deployment</span></span> 

<span data-ttu-id="a2344-109">Run the following command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="a2344-109">Run the following command to remove the resource group, application gateway, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="script-explanation"></a><span data-ttu-id="a2344-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="a2344-110">Script explanation</span></span>

<span data-ttu-id="a2344-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="a2344-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="a2344-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="a2344-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a2344-113">Command</span><span class="sxs-lookup"><span data-stu-id="a2344-113">Command</span></span> | <span data-ttu-id="a2344-114">Notes</span><span class="sxs-lookup"><span data-stu-id="a2344-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2344-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2344-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="a2344-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="a2344-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2344-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="a2344-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="a2344-118">Creates the subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="a2344-118">Creates the subnet configuration.</span></span> |
| [<span data-ttu-id="a2344-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="a2344-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="a2344-120">Creates the virtual network using with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="a2344-120">Creates the virtual network using with the subnet configurations.</span></span> |
| [<span data-ttu-id="a2344-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="a2344-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="a2344-122">Creates the public IP address for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-122">Creates the public IP address for the application gateway.</span></span> |
| [<span data-ttu-id="a2344-123">New-AzureRmApplicationGatewayIPConfiguration</span><span class="sxs-lookup"><span data-stu-id="a2344-123">New-AzureRmApplicationGatewayIPConfiguration</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration) | <span data-ttu-id="a2344-124">Creates the configuration that associates a subnet with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-124">Creates the configuration that associates a subnet with the application gateway.</span></span> |
| [<span data-ttu-id="a2344-125">New-AzureRmApplicationGatewayFrontendIPConfig</span><span class="sxs-lookup"><span data-stu-id="a2344-125">New-AzureRmApplicationGatewayFrontendIPConfig</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig) | <span data-ttu-id="a2344-126">Creates the configuration that assigns a public IP address to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-126">Creates the configuration that assigns a public IP address to the application gateway.</span></span> |
| [<span data-ttu-id="a2344-127">New-AzureRmApplicationGatewayFrontendPort</span><span class="sxs-lookup"><span data-stu-id="a2344-127">New-AzureRmApplicationGatewayFrontendPort</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport) | <span data-ttu-id="a2344-128">Assigns a port to be used to access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-128">Assigns a port to be used to access the application gateway.</span></span> |
| [<span data-ttu-id="a2344-129">New-AzureRmApplicationGatewayBackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="a2344-129">New-AzureRmApplicationGatewayBackendAddressPool</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool) | <span data-ttu-id="a2344-130">Creates a backend pool for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-130">Creates a backend pool for an application gateway.</span></span> |
| [<span data-ttu-id="a2344-131">New-AzureRmApplicationGatewayBackendHttpSettings</span><span class="sxs-lookup"><span data-stu-id="a2344-131">New-AzureRmApplicationGatewayBackendHttpSettings</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings) | <span data-ttu-id="a2344-132">Configures settings for a backend pool.</span><span class="sxs-lookup"><span data-stu-id="a2344-132">Configures settings for a backend pool.</span></span> |
| [<span data-ttu-id="a2344-133">New-AzureRmApplicationGatewayHttpListener</span><span class="sxs-lookup"><span data-stu-id="a2344-133">New-AzureRmApplicationGatewayHttpListener</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) | <span data-ttu-id="a2344-134">Creates a listener.</span><span class="sxs-lookup"><span data-stu-id="a2344-134">Creates a listener.</span></span> |
| [<span data-ttu-id="a2344-135">New-AzureRmApplicationGatewayRequestRoutingRule</span><span class="sxs-lookup"><span data-stu-id="a2344-135">New-AzureRmApplicationGatewayRequestRoutingRule</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) | <span data-ttu-id="a2344-136">Creates a routing rule.</span><span class="sxs-lookup"><span data-stu-id="a2344-136">Creates a routing rule.</span></span> |
| [<span data-ttu-id="a2344-137">New-AzureRmApplicationGatewaySku</span><span class="sxs-lookup"><span data-stu-id="a2344-137">New-AzureRmApplicationGatewaySku</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku) | <span data-ttu-id="a2344-138">Specify the tier and capacity for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-138">Specify the tier and capacity for an application gateway.</span></span> |
| [<span data-ttu-id="a2344-139">New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration</span><span class="sxs-lookup"><span data-stu-id="a2344-139">New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaywebapplicationfirewallconfiguration) | <span data-ttu-id="a2344-140">Creates the web application firewall configuration.</span><span class="sxs-lookup"><span data-stu-id="a2344-140">Creates the web application firewall configuration.</span></span> |
| [<span data-ttu-id="a2344-141">New-AzureRmApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="a2344-141">New-AzureRmApplicationGateway</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgateway) | <span data-ttu-id="a2344-142">Create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-142">Create an application gateway.</span></span> |
| [<span data-ttu-id="a2344-143">Set-AzureRmVmssStorageProfile</span><span class="sxs-lookup"><span data-stu-id="a2344-143">Set-AzureRmVmssStorageProfile</span></span>](/powershell/module/azurerm.compute/set-azurermvmssstorageprofile) | <span data-ttu-id="a2344-144">Create a storage profile for the scale set.</span><span class="sxs-lookup"><span data-stu-id="a2344-144">Create a storage profile for the scale set.</span></span> |
| [<span data-ttu-id="a2344-145">Set-AzureRmVmssOsProfile</span><span class="sxs-lookup"><span data-stu-id="a2344-145">Set-AzureRmVmssOsProfile</span></span>](/powershell/module/azurerm.compute/set-azurermvmssosprofile) | <span data-ttu-id="a2344-146">Define the operating system for the scale set.</span><span class="sxs-lookup"><span data-stu-id="a2344-146">Define the operating system for the scale set.</span></span> |
| [<span data-ttu-id="a2344-147">Add-AzureRmVmssNetworkInterfaceConfiguration</span><span class="sxs-lookup"><span data-stu-id="a2344-147">Add-AzureRmVmssNetworkInterfaceConfiguration</span></span>](/powershell/module/azurerm.compute/add-azurermvmssnetworkinterfaceconfiguration) | <span data-ttu-id="a2344-148">Define the network interface for the scale set.</span><span class="sxs-lookup"><span data-stu-id="a2344-148">Define the network interface for the scale set.</span></span> |
| [<span data-ttu-id="a2344-149">New-AzureRmVmss</span><span class="sxs-lookup"><span data-stu-id="a2344-149">New-AzureRmVmss</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="a2344-150">Create a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="a2344-150">Create a virtual machine scale set.</span></span> |
| [<span data-ttu-id="a2344-151">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="a2344-151">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="a2344-152">Creates a storage account.</span><span class="sxs-lookup"><span data-stu-id="a2344-152">Creates a storage account.</span></span> |
| [<span data-ttu-id="a2344-153">Set-AzureRmDiagnosticSetting</span><span class="sxs-lookup"><span data-stu-id="a2344-153">Set-AzureRmDiagnosticSetting</span></span>](/powershell/module/azurerm.insights/set-azurermdiagnosticsetting) | <span data-ttu-id="a2344-154">Configures diagnostics to record data.</span><span class="sxs-lookup"><span data-stu-id="a2344-154">Configures diagnostics to record data.</span></span> |
| [<span data-ttu-id="a2344-155">Get-AzureRmPublicIPAddress</span><span class="sxs-lookup"><span data-stu-id="a2344-155">Get-AzureRmPublicIPAddress</span></span>](/powershell/module/azurerm.network/get-azurermpublicipaddress) | <span data-ttu-id="a2344-156">Gets the public IP address of an application gateway.</span><span class="sxs-lookup"><span data-stu-id="a2344-156">Gets the public IP address of an application gateway.</span></span> |
|[<span data-ttu-id="a2344-157">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a2344-157">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="a2344-158">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="a2344-158">Removes a resource group and all resources contained within.</span></span> | 
## <a name="next-steps"></a><span data-ttu-id="a2344-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="a2344-159">Next steps</span></span>

<span data-ttu-id="a2344-160">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2344-160">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="a2344-161">Additional application gateway PowerShell script samples can be found in the [Azure Application Gateway documentation](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2344-161">Additional application gateway PowerShell script samples can be found in the [Azure Application Gateway documentation](../powershell-samples.md).</span></span>
