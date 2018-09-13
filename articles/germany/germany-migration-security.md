---
title: Migration of security resources from Azure Germany to global Azure
description: This article provides help for migrating security resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: ef4582d3e542714b95c8ffd34edeac4051045268
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870041"
---
# <a name="migration-of-security-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="b14ee-103">Migration of security resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="b14ee-103">Migration of security resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="b14ee-104">This article will provide you some help for the migration of Azure Security resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="b14ee-104">This article will provide you some help for the migration of Azure Security resources from Azure Germany to global Azure.</span></span>

## <a name="azure-active-directory"></a><span data-ttu-id="b14ee-105">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b14ee-105">Azure Active Directory</span></span>

<span data-ttu-id="b14ee-106">This service is covered under [Migration of Identities](./germany-migration-identity.md#azure-active-directory).</span><span class="sxs-lookup"><span data-stu-id="b14ee-106">This service is covered under [Migration of Identities](./germany-migration-identity.md#azure-active-directory).</span></span>





## <a name="key-vault"></a><span data-ttu-id="b14ee-107">Key Vault</span><span class="sxs-lookup"><span data-stu-id="b14ee-107">Key Vault</span></span>

### <a name="encryption-keys"></a><span data-ttu-id="b14ee-108">Encryption Keys</span><span class="sxs-lookup"><span data-stu-id="b14ee-108">Encryption Keys</span></span>

<span data-ttu-id="b14ee-109">Encryption keys can't be migrated.</span><span class="sxs-lookup"><span data-stu-id="b14ee-109">Encryption keys can't be migrated.</span></span> <span data-ttu-id="b14ee-110">Create new keys in the target region and use them to protect the target resource (Storage, SQL DB, etc.).</span><span class="sxs-lookup"><span data-stu-id="b14ee-110">Create new keys in the target region and use them to protect the target resource (Storage, SQL DB, etc.).</span></span> <span data-ttu-id="b14ee-111">Then securely migrate the data from the old region to the new region.</span><span class="sxs-lookup"><span data-stu-id="b14ee-111">Then securely migrate the data from the old region to the new region.</span></span>

### <a name="application-secrets"></a><span data-ttu-id="b14ee-112">Application secrets</span><span class="sxs-lookup"><span data-stu-id="b14ee-112">Application secrets</span></span>

<span data-ttu-id="b14ee-113">Application secrets are certificates, storage account keys and other application-related secrets.</span><span class="sxs-lookup"><span data-stu-id="b14ee-113">Application secrets are certificates, storage account keys and other application-related secrets.</span></span>

- <span data-ttu-id="b14ee-114">Create a new KeyVault in global Azure</span><span class="sxs-lookup"><span data-stu-id="b14ee-114">Create a new KeyVault in global Azure</span></span>
- <span data-ttu-id="b14ee-115">create new application secrets, **or**</span><span class="sxs-lookup"><span data-stu-id="b14ee-115">create new application secrets, **or**</span></span>
- <span data-ttu-id="b14ee-116">read the current secrets in Azure Germany and enter the value into the new vault.</span><span class="sxs-lookup"><span data-stu-id="b14ee-116">read the current secrets in Azure Germany and enter the value into the new vault.</span></span>

```powershell
Get-AzureKeyVaultSecret -vaultname mysecrets -name Deploydefaultpw
```

### <a name="next-steps"></a><span data-ttu-id="b14ee-117">Next steps</span><span class="sxs-lookup"><span data-stu-id="b14ee-117">Next steps</span></span>

<span data-ttu-id="b14ee-118">Refresh your knowledge about Key Vault by following these [Step-by-step tutorials](https://docs.microsoft.com/azure/key-vault/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="b14ee-118">Refresh your knowledge about Key Vault by following these [Step-by-step tutorials](https://docs.microsoft.com/azure/key-vault/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="b14ee-119">References</span><span class="sxs-lookup"><span data-stu-id="b14ee-119">References</span></span>

- [<span data-ttu-id="b14ee-120">KeyVault overview</span><span class="sxs-lookup"><span data-stu-id="b14ee-120">KeyVault overview</span></span>](../key-vault/key-vault-overview.md)
- [<span data-ttu-id="b14ee-121">KeyVault PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b14ee-121">KeyVault PowerShell cmdlets</span></span>](/powershell/module/azurerm.keyvault/?view=azurermps-6.5.0)















## <a name="vpn-gateway"></a><span data-ttu-id="b14ee-122">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b14ee-122">VPN Gateway</span></span>

<span data-ttu-id="b14ee-123">Migration of Virtual Private Network (VPN) Gateways between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="b14ee-123">Migration of Virtual Private Network (VPN) Gateways between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="b14ee-124">The recommended approach is to create and configure a new VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="b14ee-124">The recommended approach is to create and configure a new VPN Gateway.</span></span>

<span data-ttu-id="b14ee-125">Collect information about your current VPN gateway configuration by using the portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b14ee-125">Collect information about your current VPN gateway configuration by using the portal or by using PowerShell.</span></span> <span data-ttu-id="b14ee-126">There's a set of cmdlets starting with `Get-AzureRmVirtualNetworkGateway*`.</span><span class="sxs-lookup"><span data-stu-id="b14ee-126">There's a set of cmdlets starting with `Get-AzureRmVirtualNetworkGateway*`.</span></span>

<span data-ttu-id="b14ee-127">Don't forget to update your on-premise configuration and delete any existing rules for the old IP ranges once you updated your Azure network environment.</span><span class="sxs-lookup"><span data-stu-id="b14ee-127">Don't forget to update your on-premise configuration and delete any existing rules for the old IP ranges once you updated your Azure network environment.</span></span>

### <a name="next-steps"></a><span data-ttu-id="b14ee-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="b14ee-128">Next steps</span></span>

- <span data-ttu-id="b14ee-129">Refresh your knowledge about VPN Gateways by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/vpn-gateway/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="b14ee-129">Refresh your knowledge about VPN Gateways by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/vpn-gateway/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="b14ee-130">References</span><span class="sxs-lookup"><span data-stu-id="b14ee-130">References</span></span>

- <span data-ttu-id="b14ee-131">[Create Site-to-Site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) with VPN gateway</span><span class="sxs-lookup"><span data-stu-id="b14ee-131">[Create Site-to-Site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) with VPN gateway</span></span>
- <span data-ttu-id="b14ee-132">[Get-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/get-azurermvirtualnetworkgateway?view=azurermps-6.5.0) PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b14ee-132">[Get-AzureRmVirtualNetworkGateway](/powershell/module/azurerm.network/get-azurermvirtualnetworkgateway?view=azurermps-6.5.0) PowerShell cmdlets</span></span>
- <span data-ttu-id="b14ee-133">Blog: [Create Site-to-Site connection](https://blogs.technet.microsoft.com/ralfwi/2017/02/02/connecting-clouds/) between Azure Germany and global Azure</span><span class="sxs-lookup"><span data-stu-id="b14ee-133">Blog: [Create Site-to-Site connection](https://blogs.technet.microsoft.com/ralfwi/2017/02/02/connecting-clouds/) between Azure Germany and global Azure</span></span>
 






## <a name="application-gateway"></a><span data-ttu-id="b14ee-134">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b14ee-134">Application Gateway</span></span>

<span data-ttu-id="b14ee-135">Migration of Application Gateways between Azure Germany and global Azure isn't supported at this time.</span><span class="sxs-lookup"><span data-stu-id="b14ee-135">Migration of Application Gateways between Azure Germany and global Azure isn't supported at this time.</span></span> <span data-ttu-id="b14ee-136">The recommended approach is to create and configure a new Gateway.</span><span class="sxs-lookup"><span data-stu-id="b14ee-136">The recommended approach is to create and configure a new Gateway.</span></span>

<span data-ttu-id="b14ee-137">Collect information about your current gateway configuration by using the portal or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b14ee-137">Collect information about your current gateway configuration by using the portal or by using PowerShell.</span></span> <span data-ttu-id="b14ee-138">There's a set of cmdlets starting with `Get-AzureRmApplicationGateway*`.</span><span class="sxs-lookup"><span data-stu-id="b14ee-138">There's a set of cmdlets starting with `Get-AzureRmApplicationGateway*`.</span></span>

### <a name="next-steps"></a><span data-ttu-id="b14ee-139">Next steps</span><span class="sxs-lookup"><span data-stu-id="b14ee-139">Next steps</span></span>

- <span data-ttu-id="b14ee-140">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/application-gateway/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="b14ee-140">Refresh your knowledge about Application Gateway by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/application-gateway/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="b14ee-141">References</span><span class="sxs-lookup"><span data-stu-id="b14ee-141">References</span></span>

- [<span data-ttu-id="b14ee-142">Create Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b14ee-142">Create Application Gateway</span></span>](../application-gateway/quick-create-portal.md)
- <span data-ttu-id="b14ee-143">[Get-AzureRmApplicationGateway](/powershell/module/azurerm.network/get-azurermapplicationgateway?view=azurermps-6.5.0) PowerShell cmdlets</span><span class="sxs-lookup"><span data-stu-id="b14ee-143">[Get-AzureRmApplicationGateway](/powershell/module/azurerm.network/get-azurermapplicationgateway?view=azurermps-6.5.0) PowerShell cmdlets</span></span>

