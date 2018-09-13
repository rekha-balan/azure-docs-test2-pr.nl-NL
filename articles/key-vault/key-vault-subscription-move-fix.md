---
title: Change the key vault tenant ID after a subscription move | Microsoft Docs
description: Learn how to switch the tenant ID for a key vault after a subscription is moved to a different tenant
services: key-vault
documentationcenter: ''
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 8fc002e1e27de76fd53faa443de2639282eabe56
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660974"
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="580d3-103">Change a key vault tenant ID after a subscription move</span><span class="sxs-lookup"><span data-stu-id="580d3-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="580d3-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span><span class="sxs-lookup"><span data-stu-id="580d3-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="580d3-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span><span class="sxs-lookup"><span data-stu-id="580d3-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="580d3-106">All access policy entries are also tied to this tenant ID.</span><span class="sxs-lookup"><span data-stu-id="580d3-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="580d3-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span><span class="sxs-lookup"><span data-stu-id="580d3-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="580d3-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span><span class="sxs-lookup"><span data-stu-id="580d3-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="580d3-109">Remove all existing access policy entries.</span><span class="sxs-lookup"><span data-stu-id="580d3-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="580d3-110">Add new access policy entries that are associated with tenant B.</span><span class="sxs-lookup"><span data-stu-id="580d3-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="580d3-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span><span class="sxs-lookup"><span data-stu-id="580d3-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="580d3-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span><span class="sxs-lookup"><span data-stu-id="580d3-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="580d3-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="580d3-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="580d3-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="580d3-114">Next steps</span></span>
<span data-ttu-id="580d3-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="580d3-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

