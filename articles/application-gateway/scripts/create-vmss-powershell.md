---
title: Azure PowerShell Script Sample - Manage web traffic | Microsoft Docs
description: Azure PowerShell Script Sample - Manage web traffic with an application gateway and a virtual machine scale set.
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
ms.openlocfilehash: ef6a4171c582e3eb82fbcc73171797e1c806de05
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965920"
---
# <a name="manage-web-traffic-with-azure-powershell"></a><span data-ttu-id="debdb-103">Manage web traffic with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="debdb-103">Manage web traffic with Azure PowerShell</span></span>

<span data-ttu-id="debdb-104">This script creates an application gateway that uses a virtual machine scale set for backend servers.</span><span class="sxs-lookup"><span data-stu-id="debdb-104">This script creates an application gateway that uses a virtual machine scale set for backend servers.</span></span> <span data-ttu-id="debdb-105">The application gateway can then be configured to manage web traffic.</span><span class="sxs-lookup"><span data-stu-id="debdb-105">The application gateway can then be configured to manage web traffic.</span></span> <span data-ttu-id="debdb-106">After running the script, you can test the application gateway using its public IP address.</span><span class="sxs-lookup"><span data-stu-id="debdb-106">After running the script, you can test the application gateway using its public IP address.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="debdb-107">Sample script</span><span class="sxs-lookup"><span data-stu-id="debdb-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/application-gateway/create-vmss/create-vmss.ps1 "Create application gateway")]

## <a name="clean-up-deployment"></a><span data-ttu-id="debdb-108">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="debdb-108">Clean up deployment</span></span> 

<span data-ttu-id="debdb-109">Run the following command to remove the resource group, application gateway, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="debdb-109">Run the following command to remove the resource group, application gateway, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroupAG
```

## <a name="script-explanation"></a><span data-ttu-id="debdb-110">Script explanation</span><span class="sxs-lookup"><span data-stu-id="debdb-110">Script explanation</span></span>

<span data-ttu-id="debdb-111">This script uses the following commands to create the deployment.</span><span class="sxs-lookup"><span data-stu-id="debdb-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="debdb-112">Each item in the table links to command specific documentation.</span><span class="sxs-lookup"><span data-stu-id="debdb-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="debdb-113">Command</span><span class="sxs-lookup"><span data-stu-id="debdb-113">Command</span></span> | <span data-ttu-id="debdb-114">Notes</span><span class="sxs-lookup"><span data-stu-id="debdb-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="debdb-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="debdb-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="debdb-116">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="debdb-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="debdb-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="debdb-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="debdb-118">Creates the subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="debdb-118">Creates the subnet configuration.</span></span> |
| [<span data-ttu-id="debdb-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="debdb-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="debdb-120">Creates the virtual network using with the subnet configurations.</span><span class="sxs-lookup"><span data-stu-id="debdb-120">Creates the virtual network using with the subnet configurations.</span></span> |
| [<span data-ttu-id="debdb-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="debdb-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="debdb-122">Creates the public IP address for the application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-122">Creates the public IP address for the application gateway.</span></span> |
| [<span data-ttu-id="debdb-123">New-AzureRmApplicationGatewayIPConfiguration</span><span class="sxs-lookup"><span data-stu-id="debdb-123">New-AzureRmApplicationGatewayIPConfiguration</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayipconfiguration) | <span data-ttu-id="debdb-124">Creates the configuration that associates a subnet with the application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-124">Creates the configuration that associates a subnet with the application gateway.</span></span> |
| [<span data-ttu-id="debdb-125">New-AzureRmApplicationGatewayFrontendIPConfig</span><span class="sxs-lookup"><span data-stu-id="debdb-125">New-AzureRmApplicationGatewayFrontendIPConfig</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendipconfig) | <span data-ttu-id="debdb-126">Creates the configuration that assigns a public IP address to the application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-126">Creates the configuration that assigns a public IP address to the application gateway.</span></span> |
| [<span data-ttu-id="debdb-127">New-AzureRmApplicationGatewayFrontendPort</span><span class="sxs-lookup"><span data-stu-id="debdb-127">New-AzureRmApplicationGatewayFrontendPort</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayfrontendport) | <span data-ttu-id="debdb-128">Assigns a port to be used to access the application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-128">Assigns a port to be used to access the application gateway.</span></span> |
| [<span data-ttu-id="debdb-129">New-AzureRmApplicationGatewayBackendAddressPool</span><span class="sxs-lookup"><span data-stu-id="debdb-129">New-AzureRmApplicationGatewayBackendAddressPool</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendaddresspool) | <span data-ttu-id="debdb-130">Creates a backend pool for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-130">Creates a backend pool for an application gateway.</span></span> |
| [<span data-ttu-id="debdb-131">New-AzureRmApplicationGatewayBackendHttpSettings</span><span class="sxs-lookup"><span data-stu-id="debdb-131">New-AzureRmApplicationGatewayBackendHttpSettings</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaybackendhttpsettings) | <span data-ttu-id="debdb-132">Configures settings for a backend pool.</span><span class="sxs-lookup"><span data-stu-id="debdb-132">Configures settings for a backend pool.</span></span> |
| [<span data-ttu-id="debdb-133">New-AzureRmApplicationGatewayHttpListener</span><span class="sxs-lookup"><span data-stu-id="debdb-133">New-AzureRmApplicationGatewayHttpListener</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayhttplistener) | <span data-ttu-id="debdb-134">Creates a listener.</span><span class="sxs-lookup"><span data-stu-id="debdb-134">Creates a listener.</span></span> |
| [<span data-ttu-id="debdb-135">New-AzureRmApplicationGatewayRequestRoutingRule</span><span class="sxs-lookup"><span data-stu-id="debdb-135">New-AzureRmApplicationGatewayRequestRoutingRule</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewayrequestroutingrule) | <span data-ttu-id="debdb-136">Creates a routing rule.</span><span class="sxs-lookup"><span data-stu-id="debdb-136">Creates a routing rule.</span></span> |
| [<span data-ttu-id="debdb-137">New-AzureRmApplicationGatewaySku</span><span class="sxs-lookup"><span data-stu-id="debdb-137">New-AzureRmApplicationGatewaySku</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgatewaysku) | <span data-ttu-id="debdb-138">Specify the tier and capacity for an application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-138">Specify the tier and capacity for an application gateway.</span></span> |
| [<span data-ttu-id="debdb-139">New-AzureRmApplicationGateway</span><span class="sxs-lookup"><span data-stu-id="debdb-139">New-AzureRmApplicationGateway</span></span>](/powershell/module/azurerm.network/new-azurermapplicationgateway) | <span data-ttu-id="debdb-140">Create an application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-140">Create an application gateway.</span></span> |
| [<span data-ttu-id="debdb-141">Set-AzureRmVmssStorageProfile</span><span class="sxs-lookup"><span data-stu-id="debdb-141">Set-AzureRmVmssStorageProfile</span></span>](/powershell/module/azurerm.compute/set-azurermvmssstorageprofile) | <span data-ttu-id="debdb-142">Create a storage profile for the scale set.</span><span class="sxs-lookup"><span data-stu-id="debdb-142">Create a storage profile for the scale set.</span></span> |
| [<span data-ttu-id="debdb-143">Set-AzureRmVmssOsProfile</span><span class="sxs-lookup"><span data-stu-id="debdb-143">Set-AzureRmVmssOsProfile</span></span>](/powershell/module/azurerm.compute/set-azurermvmssosprofile) | <span data-ttu-id="debdb-144">Define the operating system for the scale set.</span><span class="sxs-lookup"><span data-stu-id="debdb-144">Define the operating system for the scale set.</span></span> |
| [<span data-ttu-id="debdb-145">Add-AzureRmVmssNetworkInterfaceConfiguration</span><span class="sxs-lookup"><span data-stu-id="debdb-145">Add-AzureRmVmssNetworkInterfaceConfiguration</span></span>](/powershell/module/azurerm.compute/add-azurermvmssnetworkinterfaceconfiguration) | <span data-ttu-id="debdb-146">Define the network interface for the scale set.</span><span class="sxs-lookup"><span data-stu-id="debdb-146">Define the network interface for the scale set.</span></span> |
| [<span data-ttu-id="debdb-147">New-AzureRmVmss</span><span class="sxs-lookup"><span data-stu-id="debdb-147">New-AzureRmVmss</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="debdb-148">Create a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="debdb-148">Create a virtual machine scale set.</span></span> |
| [<span data-ttu-id="debdb-149">Get-AzureRmPublicIPAddress</span><span class="sxs-lookup"><span data-stu-id="debdb-149">Get-AzureRmPublicIPAddress</span></span>](/powershell/module/azurerm.network/get-azurermpublicipaddress) | <span data-ttu-id="debdb-150">Gets the public IP address of an application gateway.</span><span class="sxs-lookup"><span data-stu-id="debdb-150">Gets the public IP address of an application gateway.</span></span> |
|[<span data-ttu-id="debdb-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="debdb-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="debdb-152">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="debdb-152">Removes a resource group and all resources contained within.</span></span> | 

## <a name="next-steps"></a><span data-ttu-id="debdb-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="debdb-153">Next steps</span></span>

<span data-ttu-id="debdb-154">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="debdb-154">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="debdb-155">Additional application gateway PowerShell script samples can be found in the [Azure Application Gateway documentation](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="debdb-155">Additional application gateway PowerShell script samples can be found in the [Azure Application Gateway documentation](../powershell-samples.md).</span></span>
