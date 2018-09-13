---
title: Azure PowerShell script sample - Create Azure Firewall test environment
description: Azure PowerShell script sample - Create Azure Firewall test enviroment.
services: virtual-network
author: vhorne
ms.service: firewall
ms.devlang: powershell
ms.topic: sample
ms.date: 8/13/2018
ms.author: victorh
ms.openlocfilehash: b65a5dec63bdc625dda64e101620f56cd6dd7308
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866265"
---
# <a name="create-an-azure-firewall-test-environment"></a><span data-ttu-id="8b5cb-103">Create an Azure Firewall test environment</span><span class="sxs-lookup"><span data-stu-id="8b5cb-103">Create an Azure Firewall test environment</span></span>

[!INCLUDE [firewall-preview-notice](../../../includes/firewall-preview-notice.md)]

<span data-ttu-id="8b5cb-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-104">The examples in the Azure Firewall articles assume that you have already enabled the Azure Firewall public preview.</span></span> <span data-ttu-id="8b5cb-105">For more information, see [Enable the Azure Firewall public preview](../public-preview.md).</span><span class="sxs-lookup"><span data-stu-id="8b5cb-105">For more information, see [Enable the Azure Firewall public preview](../public-preview.md).</span></span>

<span data-ttu-id="8b5cb-106">This script sample creates a firewall and a test network environment.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-106">This script sample creates a firewall and a test network environment.</span></span> <span data-ttu-id="8b5cb-107">The network has one VNet, with three subnets: an *AzureFirewallSubnet*, and *ServersSubnet*, and a *JumpboxSubnet*.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-107">The network has one VNet, with three subnets: an *AzureFirewallSubnet*, and *ServersSubnet*, and a *JumpboxSubnet*.</span></span> <span data-ttu-id="8b5cb-108">The ServersSubnet and JumpboxSubnet each have one 2-core Windows Server in them.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-108">The ServersSubnet and JumpboxSubnet each have one 2-core Windows Server in them.</span></span>

<span data-ttu-id="8b5cb-109">The firewall is in the AzureFirewallSubnet and is configured with an Application Rule Collection with a single rule that allows access to www.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-109">The firewall is in the AzureFirewallSubnet and is configured with an Application Rule Collection with a single rule that allows access to www.microsoft.com.</span></span>

<span data-ttu-id="8b5cb-110">A user defined route is created that points the network traffic from the ServersSubnet through the firewall, where the firewall rules are applied.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-110">A user defined route is created that points the network traffic from the ServersSubnet through the firewall, where the firewall rules are applied.</span></span>

<span data-ttu-id="8b5cb-111">You can run the script from the Azure [Cloud Shell](https://shell.azure.com/powershell), or from a local PowerShell installation.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-111">You can run the script from the Azure [Cloud Shell](https://shell.azure.com/powershell), or from a local PowerShell installation.</span></span> 

<span data-ttu-id="8b5cb-112">If you run PowerShell locally, this script requires the AzureRM PowerShell module version 6.4.0 or later.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-112">If you run PowerShell locally, this script requires the AzureRM PowerShell module version 6.4.0 or later.</span></span> <span data-ttu-id="8b5cb-113">To find the installed version, run `Get-Module -ListAvailable AzureRM`.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-113">To find the installed version, run `Get-Module -ListAvailable AzureRM`.</span></span> 

<span data-ttu-id="8b5cb-114">You can use `PowerShellGet` if you need to upgrade, which is built into Windows 10 and Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-114">You can use `PowerShellGet` if you need to upgrade, which is built into Windows 10 and Windows Server 2016.</span></span>

> [!NOTE]
><span data-ttu-id="8b5cb-115">Other Windows version require you to install `PowerShellGet` before you can use it.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-115">Other Windows version require you to install `PowerShellGet` before you can use it.</span></span> <span data-ttu-id="8b5cb-116">You can run `Get-Module -Name PowerShellGet -ListAvailable | Select-Object -Property Name,Version,Path` to determine if it is installed on your system.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-116">You can run `Get-Module -Name PowerShellGet -ListAvailable | Select-Object -Property Name,Version,Path` to determine if it is installed on your system.</span></span> <span data-ttu-id="8b5cb-117">If the output is blank, you need to install the latest [Windows Management framework](https://www.microsoft.com/download/details.aspx?id=54616).</span><span class="sxs-lookup"><span data-stu-id="8b5cb-117">If the output is blank, you need to install the latest [Windows Management framework](https://www.microsoft.com/download/details.aspx?id=54616).</span></span>

<span data-ttu-id="8b5cb-118">For more information, see [Install Azure PowerShell on Windows with PowerShellGet](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-6.4.0)</span><span class="sxs-lookup"><span data-stu-id="8b5cb-118">For more information, see [Install Azure PowerShell on Windows with PowerShellGet](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps?view=azurermps-6.4.0)</span></span>

<span data-ttu-id="8b5cb-119">Any existing Azure PowerShell installation done with the Web Platform installer will conflict with the PowerShellGet installation and needs to be removed.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-119">Any existing Azure PowerShell installation done with the Web Platform installer will conflict with the PowerShellGet installation and needs to be removed.</span></span>

<span data-ttu-id="8b5cb-120">Additionally, you must install the preview version of AzureRM.Network (version 6.4.0).</span><span class="sxs-lookup"><span data-stu-id="8b5cb-120">Additionally, you must install the preview version of AzureRM.Network (version 6.4.0).</span></span> <span data-ttu-id="8b5cb-121">If have an older module, run `Uninstall-Module AzureRM.Network -Force` to remove it.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-121">If have an older module, run `Uninstall-Module AzureRM.Network -Force` to remove it.</span></span> <span data-ttu-id="8b5cb-122">Then run:</span><span class="sxs-lookup"><span data-stu-id="8b5cb-122">Then run:</span></span>

 `Install-Module -Name AzureRM.Network -Repository PSGallery -RequiredVersion 6.4.0-preview -AllowPrerelease -Force`

<span data-ttu-id="8b5cb-123">to install verion 6.4.0.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-123">to install verion 6.4.0.</span></span>

<span data-ttu-id="8b5cb-124">Remember that if you run PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-124">Remember that if you run PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8b5cb-125">Sample script</span><span class="sxs-lookup"><span data-stu-id="8b5cb-125">Sample script</span></span>


[!code-azurepowershell-interactive[main](../../../powershell_scripts/firewall/create-fw-test.ps1  "Create a firewall test environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8b5cb-126">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="8b5cb-126">Clean up deployment</span></span> 

<span data-ttu-id="8b5cb-127">Run the following command to remove the resource group, VM, and all related resources:</span><span class="sxs-lookup"><span data-stu-id="8b5cb-127">Run the following command to remove the resource group, VM, and all related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name AzfwSampleScriptEastUS -Force
```

## <a name="script-explanation"></a><span data-ttu-id="8b5cb-128">Script explanation</span><span class="sxs-lookup"><span data-stu-id="8b5cb-128">Script explanation</span></span>

<span data-ttu-id="8b5cb-129">This script uses the following commands to create a resource group, virtual network, and network security groups.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-129">This script uses the following commands to create a resource group, virtual network, and network security groups.</span></span> <span data-ttu-id="8b5cb-130">Each command in the following table links to command-specific documentation:</span><span class="sxs-lookup"><span data-stu-id="8b5cb-130">Each command in the following table links to command-specific documentation:</span></span>

| <span data-ttu-id="8b5cb-131">Command</span><span class="sxs-lookup"><span data-stu-id="8b5cb-131">Command</span></span> | <span data-ttu-id="8b5cb-132">Notes</span><span class="sxs-lookup"><span data-stu-id="8b5cb-132">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8b5cb-133">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8b5cb-133">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8b5cb-134">Creates a resource group in which all resources are stored.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-134">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8b5cb-135">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8b5cb-135">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8b5cb-136">Creates a subnet configuration object</span><span class="sxs-lookup"><span data-stu-id="8b5cb-136">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="8b5cb-137">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8b5cb-137">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8b5cb-138">Creates an Azure virtual network and front-end subnet.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-138">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="8b5cb-139">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8b5cb-139">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8b5cb-140">Creates security rules to be assigned to a network security group.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-140">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="8b5cb-141">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8b5cb-141">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="8b5cb-142">Creates NSG rules that allow or block specific ports to specific subnets.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-142">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="8b5cb-143">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8b5cb-143">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8b5cb-144">Associates NSGs to subnets.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-144">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="8b5cb-145">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8b5cb-145">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8b5cb-146">Creates a public IP address to access the VM from the internet.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-146">Creates a public IP address to access the VM from the internet.</span></span> |
| [<span data-ttu-id="8b5cb-147">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8b5cb-147">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8b5cb-148">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-148">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="8b5cb-149">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="8b5cb-149">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="8b5cb-150">Creates a VM configuration.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-150">Creates a VM configuration.</span></span> <span data-ttu-id="8b5cb-151">This configuration includes information such as VM name, operating system, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-151">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="8b5cb-152">The configuration is used during VM creation.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-152">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="8b5cb-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8b5cb-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8b5cb-154">Create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-154">Create a virtual machine.</span></span> |
|[<span data-ttu-id="8b5cb-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8b5cb-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8b5cb-156">Removes a resource group and all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-156">Removes a resource group and all resources contained within.</span></span> |
|[<span data-ttu-id="8b5cb-157">New-AzureRmFirewall</span><span class="sxs-lookup"><span data-stu-id="8b5cb-157">New-AzureRmFirewall</span></span>](https://github.com/Azure/azure-powershell/blob/Networking-AzureFirewall/src/ResourceManager/Network/Commands.Network/help/New-AzureRmFirewall.md)| <span data-ttu-id="8b5cb-158">Creates a new Azure Firewall.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-158">Creates a new Azure Firewall.</span></span>|
|[<span data-ttu-id="8b5cb-159">Get-AzureRmFirewall</span><span class="sxs-lookup"><span data-stu-id="8b5cb-159">Get-AzureRmFirewall</span></span>](https://github.com/Azure/azure-powershell/blob/Networking-AzureFirewall/src/ResourceManager/Network/Commands.Network/help/Get-AzureRmFirewall.md)|<span data-ttu-id="8b5cb-160">Gets an Azure Firewall object.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-160">Gets an Azure Firewall object.</span></span>|
|[<span data-ttu-id="8b5cb-161">New-AzureRmFirewallApplicationRule</span><span class="sxs-lookup"><span data-stu-id="8b5cb-161">New-AzureRmFirewallApplicationRule</span></span>](https://github.com/Azure/azure-powershell/blob/Networking-AzureFirewall/src/ResourceManager/Network/Commands.Network/help/New-AzureRmFirewallApplicationRule.md)|<span data-ttu-id="8b5cb-162">Creates a new Azure Firewall application rule.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-162">Creates a new Azure Firewall application rule.</span></span>|
|[<span data-ttu-id="8b5cb-163">Set-AzureRmFirewall</span><span class="sxs-lookup"><span data-stu-id="8b5cb-163">Set-AzureRmFirewall</span></span>](https://github.com/Azure/azure-powershell/blob/Networking-AzureFirewall/src/ResourceManager/Network/Commands.Network/help/Set-AzureRmFirewall.md)|<span data-ttu-id="8b5cb-164">Commits changes to the Azure Firewall object.</span><span class="sxs-lookup"><span data-stu-id="8b5cb-164">Commits changes to the Azure Firewall object.</span></span>|


## <a name="next-steps"></a><span data-ttu-id="8b5cb-165">Next steps</span><span class="sxs-lookup"><span data-stu-id="8b5cb-165">Next steps</span></span>

<span data-ttu-id="8b5cb-166">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="8b5cb-166">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

