---
title: How to change the token lifetime defaults for a custom-developed application | Microsoft Docs
description: How to update Token Lifetime policies for your application that you are developing on Azure AD
services: active-directory
documentationcenter: ''
author: CelesteDG
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 09/11/2018
ms.author: celested
ms.openlocfilehash: 059920c710b202e22a22f8431c536c5dfa19f2b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967414"
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="de2b7-103">How to change the token lifetime defaults for a custom-developed application</span><span class="sxs-lookup"><span data-stu-id="de2b7-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="de2b7-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span><span class="sxs-lookup"><span data-stu-id="de2b7-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="de2b7-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span><span class="sxs-lookup"><span data-stu-id="de2b7-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="de2b7-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="de2b7-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="de2b7-107">Run the **Connect-AzureAD -Confirm** command.</span><span class="sxs-lookup"><span data-stu-id="de2b7-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="de2b7-108">Here’s an example policy that sets the max age single factor refresh token.</span><span class="sxs-lookup"><span data-stu-id="de2b7-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="de2b7-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="de2b7-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="de2b7-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span><span class="sxs-lookup"><span data-stu-id="de2b7-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de2b7-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="de2b7-111">Next steps</span></span>
[<span data-ttu-id="de2b7-112">Configuring Token Lifetime</span><span class="sxs-lookup"><span data-stu-id="de2b7-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="de2b7-113">Azure AD Token Reference</span><span class="sxs-lookup"><span data-stu-id="de2b7-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims)

