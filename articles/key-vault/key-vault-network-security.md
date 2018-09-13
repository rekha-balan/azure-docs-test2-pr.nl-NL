---
ms.assetid: ''
title: Configure Azure Key Vault Firewalls and Virtual Networks
description: Step-by-step instructions to configure Key Vault firewalls and virtual networks
services: key-vault
author: amitbapat
manager: mbaldwin
ms.service: key-vault
ms.topic: conceptual
ms.workload: identity
ms.date: 08/31/2018
ms.author: ambapat
ms.openlocfilehash: 6315434c1e8acc82e02f5c9e5ae8ab2d1cacc887
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867488"
---
# <a name="configure-azure-key-vault-firewalls-and-virtual-networks"></a><span data-ttu-id="b5b57-103">Configure Azure Key Vault Firewalls and Virtual Networks</span><span class="sxs-lookup"><span data-stu-id="b5b57-103">Configure Azure Key Vault Firewalls and Virtual Networks</span></span>

<span data-ttu-id="b5b57-104">This guide describes step-by-step instructions to configure Key Vault firewalls and virtual networks to restrict access to your key vault.</span><span class="sxs-lookup"><span data-stu-id="b5b57-104">This guide describes step-by-step instructions to configure Key Vault firewalls and virtual networks to restrict access to your key vault.</span></span> <span data-ttu-id="b5b57-105">The [Virtual Network Service Endpoints for Key Vault](key-vault-overview-vnet-service-endpoints.md) allow you to restrict access to key vault to specified Virtual Network and/or a set of IPv4 (Internet Protocol version 4) address ranges.</span><span class="sxs-lookup"><span data-stu-id="b5b57-105">The [Virtual Network Service Endpoints for Key Vault](key-vault-overview-vnet-service-endpoints.md) allow you to restrict access to key vault to specified Virtual Network and/or a set of IPv4 (Internet Protocol version 4) address ranges.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b5b57-106">Once firewall and virtual network rules are in effect, all Key Vault [data plane](../key-vault/key-vault-secure-your-key-vault.md#data-plane-access-control) operations can ONLY be performed when caller  requests originate from allowed virtual network(s) or IPV4 address ranges.</span><span class="sxs-lookup"><span data-stu-id="b5b57-106">Once firewall and virtual network rules are in effect, all Key Vault [data plane](../key-vault/key-vault-secure-your-key-vault.md#data-plane-access-control) operations can ONLY be performed when caller  requests originate from allowed virtual network(s) or IPV4 address ranges.</span></span> <span data-ttu-id="b5b57-107">This also applies to accessing key vault from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b5b57-107">This also applies to accessing key vault from Azure portal.</span></span> <span data-ttu-id="b5b57-108">While a user can browser to a key vault from Azure portal, they may not be able to list keys/secrets/certificates if their client machine is not in the allowed list.</span><span class="sxs-lookup"><span data-stu-id="b5b57-108">While a user can browser to a key vault from Azure portal, they may not be able to list keys/secrets/certificates if their client machine is not in the allowed list.</span></span> <span data-ttu-id="b5b57-109">This also affects the 'Key Vault Picker' by other Azure services.</span><span class="sxs-lookup"><span data-stu-id="b5b57-109">This also affects the 'Key Vault Picker' by other Azure services.</span></span> <span data-ttu-id="b5b57-110">Users may be able to see list of key vaults but not list keys, if firewall rules prevent their client machine.</span><span class="sxs-lookup"><span data-stu-id="b5b57-110">Users may be able to see list of key vaults but not list keys, if firewall rules prevent their client machine.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="b5b57-111">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b5b57-111">Azure portal</span></span>

1. <span data-ttu-id="b5b57-112">Navigate to the key vault you want to secure.</span><span class="sxs-lookup"><span data-stu-id="b5b57-112">Navigate to the key vault you want to secure.</span></span>
2. <span data-ttu-id="b5b57-113">Click on **Firewalls and virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="b5b57-113">Click on **Firewalls and virtual networks**.</span></span>
3. <span data-ttu-id="b5b57-114">Click on **Selected networks** under **Allow access from**.</span><span class="sxs-lookup"><span data-stu-id="b5b57-114">Click on **Selected networks** under **Allow access from**.</span></span>
4. <span data-ttu-id="b5b57-115">To add existing virtual networks to firewalls and virtual network rules, click **+ Add existing virtual networks**.</span><span class="sxs-lookup"><span data-stu-id="b5b57-115">To add existing virtual networks to firewalls and virtual network rules, click **+ Add existing virtual networks**.</span></span>
5. <span data-ttu-id="b5b57-116">In the new blade that pops up, select the subscription, virtual network(s), and subnet(s) that you want to allow access to this key vault.</span><span class="sxs-lookup"><span data-stu-id="b5b57-116">In the new blade that pops up, select the subscription, virtual network(s), and subnet(s) that you want to allow access to this key vault.</span></span> <span data-ttu-id="b5b57-117">If the virtual network(s) and subnet(s) you select, do not have service endpoints enabled you'll see a message saying, "The following networks don't have service endpoints enavled...".</span><span class="sxs-lookup"><span data-stu-id="b5b57-117">If the virtual network(s) and subnet(s) you select, do not have service endpoints enabled you'll see a message saying, "The following networks don't have service endpoints enavled...".</span></span> <span data-ttu-id="b5b57-118">Click **Enable** after confirming that you want to enable service endpoints for the listed the virtual network(s) and subnet(s).</span><span class="sxs-lookup"><span data-stu-id="b5b57-118">Click **Enable** after confirming that you want to enable service endpoints for the listed the virtual network(s) and subnet(s).</span></span> <span data-ttu-id="b5b57-119">It may take up to 15 minutes to take effect.</span><span class="sxs-lookup"><span data-stu-id="b5b57-119">It may take up to 15 minutes to take effect.</span></span>
6. <span data-ttu-id="b5b57-120">You can also add new virtual network(s) and subnet(s) and then enable service endpoints for the newly created virtual network(s) and subnet(s), by clicking **+ Add new virtual network** and following prompts.</span><span class="sxs-lookup"><span data-stu-id="b5b57-120">You can also add new virtual network(s) and subnet(s) and then enable service endpoints for the newly created virtual network(s) and subnet(s), by clicking **+ Add new virtual network** and following prompts.</span></span>
7. <span data-ttu-id="b5b57-121">Under **IP Networks**, you can add IPv4 address ranges by typing IPv4 address ranges in [CIDR (Classless Inter-domain Routing) notation](https://tools.ietf.org/html/rfc4632) or individual IP addresses.</span><span class="sxs-lookup"><span data-stu-id="b5b57-121">Under **IP Networks**, you can add IPv4 address ranges by typing IPv4 address ranges in [CIDR (Classless Inter-domain Routing) notation](https://tools.ietf.org/html/rfc4632) or individual IP addresses.</span></span>
8. <span data-ttu-id="b5b57-122">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="b5b57-122">Click **Save**.</span></span>

## <a name="azure-cli-20"></a><span data-ttu-id="b5b57-123">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b5b57-123">Azure CLI 2.0</span></span>

1. <span data-ttu-id="b5b57-124">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b5b57-124">[Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>

2. <span data-ttu-id="b5b57-125">List available virtual network rules, if you have not set any rules for this key vault, the list will be empty.</span><span class="sxs-lookup"><span data-stu-id="b5b57-125">List available virtual network rules, if you have not set any rules for this key vault, the list will be empty.</span></span>
```azurecli
az keyvault network-rule list --resource-group myresourcegroup --name mykeyvault
```

3. <span data-ttu-id="b5b57-126">Enable Service Endpoint for Key Vault on an existing Virtual Network and subnet</span><span class="sxs-lookup"><span data-stu-id="b5b57-126">Enable Service Endpoint for Key Vault on an existing Virtual Network and subnet</span></span>
```azurecli
az network vnet subnet update --resource-group "myresourcegroup" --vnet-name "myvnet" --name "mysubnet" --service-endpoints "Microsoft.KeyVault"
```

4. <span data-ttu-id="b5b57-127">Add a network rule for a virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="b5b57-127">Add a network rule for a virtual network and subnet</span></span>
```azurecli
subnetid=$(az network vnet subnet show --resource-group "myresourcegroup" --vnet-name "myvnet" --name "mysubnet" --query id --output tsv)
az keyvault network-rule add --resource-group "demo9311" --name "demo9311premium" --subnet $subnetid
```

5. <span data-ttu-id="b5b57-128">Add IP address range to allow traffic from</span><span class="sxs-lookup"><span data-stu-id="b5b57-128">Add IP address range to allow traffic from</span></span>
```azurecli
az keyvault network-rule add --resource-group "myresourcegroup" --name "mykeyvault" --ip-address "191.10.18.0/24"
```

6. <span data-ttu-id="b5b57-129">If this key vault needs to be accessible by any trusted services, set 'bypass' to AzureServices</span><span class="sxs-lookup"><span data-stu-id="b5b57-129">If this key vault needs to be accessible by any trusted services, set 'bypass' to AzureServices</span></span>
```azurecli
az keyvault update --resource-group "myresourcegroup" --name "mykeyvault" --bypass AzureServices
```

7. <span data-ttu-id="b5b57-130">Now the final and important step, turn the network rules ON by setting the default action to 'Deny'</span><span class="sxs-lookup"><span data-stu-id="b5b57-130">Now the final and important step, turn the network rules ON by setting the default action to 'Deny'</span></span>
```azurecli
az keyvault update --resource-group "myresourcegroup" --name "mekeyvault" --default-action Deny
```

## <a name="azure-powershell"></a><span data-ttu-id="b5b57-131">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5b57-131">Azure PowerShell</span></span>

1. <span data-ttu-id="b5b57-132">Install the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) and [Login](https://docs.microsoft.com/powershell/azure/authenticate-azureps).</span><span class="sxs-lookup"><span data-stu-id="b5b57-132">Install the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) and [Login](https://docs.microsoft.com/powershell/azure/authenticate-azureps).</span></span>

2. <span data-ttu-id="b5b57-133">List available virtual network rules, if you have not set any rules for this key vault, the list will be empty.</span><span class="sxs-lookup"><span data-stu-id="b5b57-133">List available virtual network rules, if you have not set any rules for this key vault, the list will be empty.</span></span>
```PowerShell
(Get-AzureRmKeyVault -VaultName "mykeyvault").NetworkAcls
```

3. <span data-ttu-id="b5b57-134">Enable Service Endpoint for Key Vault on an existing Virtual Network and subnet</span><span class="sxs-lookup"><span data-stu-id="b5b57-134">Enable Service Endpoint for Key Vault on an existing Virtual Network and subnet</span></span>
```PowerShell
Get-AzureRmVirtualNetwork -ResourceGroupName "myresourcegroup" -Name "myvnet" | Set-AzureRmVirtualNetworkSubnetConfig -Name "mysubnet" -AddressPrefix "10.1.1.0/24" -ServiceEndpoint "Microsoft.KeyVault" | Set-AzureRmVirtualNetwork
```

4. <span data-ttu-id="b5b57-135">Add a network rule for a virtual network and subnet</span><span class="sxs-lookup"><span data-stu-id="b5b57-135">Add a network rule for a virtual network and subnet</span></span>
```PowerShell
$subnet = Get-AzureRmVirtualNetwork -ResourceGroupName "myresourcegroup" -Name "myvnet" | Get-AzureRmVirtualNetworkSubnetConfig -Name "mysubnet"
Add-AzureRmKeyVaultNetworkRule -VaultName "mykeyvault" -VirtualNetworkResourceId $subnet.Id
```

5. <span data-ttu-id="b5b57-136">Add IP address range to allow traffic from</span><span class="sxs-lookup"><span data-stu-id="b5b57-136">Add IP address range to allow traffic from</span></span>
```PowerShell
Add-AzureRmKeyVaultNetworkRule -VaultName "mykeyvault" -IpAddressRange "16.17.18.0/24"
```

6. <span data-ttu-id="b5b57-137">If this key vault needs to be accessible by any trusted services, set 'bypass' to AzureServices</span><span class="sxs-lookup"><span data-stu-id="b5b57-137">If this key vault needs to be accessible by any trusted services, set 'bypass' to AzureServices</span></span>
```PowerShell
Update-AzureRmKeyVaultNetworkRuleSet -VaultName "mykeyvault" -Bypass AzureServices
```

7. <span data-ttu-id="b5b57-138">Now the final and important step, turn the network rules ON by setting the default action to 'Deny'</span><span class="sxs-lookup"><span data-stu-id="b5b57-138">Now the final and important step, turn the network rules ON by setting the default action to 'Deny'</span></span>
```PowerShell
Update-AzureRmKeyVaultNetworkRuleSet -VaultName "mykeyvault" -DefaultAction Deny
```

## <a name="references"></a><span data-ttu-id="b5b57-139">References</span><span class="sxs-lookup"><span data-stu-id="b5b57-139">References</span></span>

* <span data-ttu-id="b5b57-140">Azure CLI 2.0 commands - [az keyvault network-rule](https://docs.microsoft.com/cli/azure/keyvault/network-rule?view=azure-cli-latest)</span><span class="sxs-lookup"><span data-stu-id="b5b57-140">Azure CLI 2.0 commands - [az keyvault network-rule](https://docs.microsoft.com/cli/azure/keyvault/network-rule?view=azure-cli-latest)</span></span>
* <span data-ttu-id="b5b57-141">Azure PowerShell cmdlets - [Get-AzureRmKeyVault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/get-azurermkeyvault), [Add-AzureRmKeyVaultNetworkRule](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Add-AzureRmKeyVaultNetworkRule), [Remove-AzureRmKeyVaultNetworkRule](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Remove-AzureRmKeyVaultNetworkRule), [Update-AzureRmKeyVaultNetworkRuleSet](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Update-AzureRmKeyVaultNetworkRuleSet)</span><span class="sxs-lookup"><span data-stu-id="b5b57-141">Azure PowerShell cmdlets - [Get-AzureRmKeyVault](https://docs.microsoft.com/powershell/module/azurerm.keyvault/get-azurermkeyvault), [Add-AzureRmKeyVaultNetworkRule](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Add-AzureRmKeyVaultNetworkRule), [Remove-AzureRmKeyVaultNetworkRule](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Remove-AzureRmKeyVaultNetworkRule), [Update-AzureRmKeyVaultNetworkRuleSet](https://docs.microsoft.com/powershell/module/AzureRM.KeyVault/Update-AzureRmKeyVaultNetworkRuleSet)</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5b57-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5b57-142">Next steps</span></span>

* [<span data-ttu-id="b5b57-143">Virtual Network Service Endpoints for Key Vault</span><span class="sxs-lookup"><span data-stu-id="b5b57-143">Virtual Network Service Endpoints for Key Vault</span></span>](key-vault-overview-vnet-service-endpoints.md)
* [<span data-ttu-id="b5b57-144">Secure your key vault</span><span class="sxs-lookup"><span data-stu-id="b5b57-144">Secure your key vault</span></span>](key-vault-secure-your-key-vault.md)