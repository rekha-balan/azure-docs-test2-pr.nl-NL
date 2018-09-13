---
title: How to change the token lifetime defaults for a custom-developed application | Microsoft Docs
description: How to update Token Lifetime policies for your application that you are developing on Azure AD
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 54c30123bb582f515dfb0324cdfd897a6c4af5c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555146"
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="5e757-103">How to change the token lifetime defaults for a custom-developed application</span><span class="sxs-lookup"><span data-stu-id="5e757-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="5e757-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span><span class="sxs-lookup"><span data-stu-id="5e757-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="5e757-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span><span class="sxs-lookup"><span data-stu-id="5e757-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="5e757-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="5e757-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="5e757-107">Run the **Connect-AzureAD -Confirm** command.</span><span class="sxs-lookup"><span data-stu-id="5e757-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="5e757-108">Here’s an example policy that sets the max age single factor refresh token.</span><span class="sxs-lookup"><span data-stu-id="5e757-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="5e757-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="5e757-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="5e757-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span><span class="sxs-lookup"><span data-stu-id="5e757-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e757-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e757-111">Next steps</span></span>
[<span data-ttu-id="5e757-112">Configuring Token Lifetime</span><span class="sxs-lookup"><span data-stu-id="5e757-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="5e757-113">Azure AD Token Reference</span><span class="sxs-lookup"><span data-stu-id="5e757-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

