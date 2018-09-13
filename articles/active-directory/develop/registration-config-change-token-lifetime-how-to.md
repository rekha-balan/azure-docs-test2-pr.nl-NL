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
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a>How to change the token lifetime defaults for a custom-developed application

Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients. Token lifetime policies are set on a tenant-wide basis or the resources being accessed.

 * To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).

 * Run the **Connect-AzureAD -Confirm** command.

 * Here’s an example policy that sets the max age single factor refresh token. Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Checkout the [Configuring token lifetime](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.

## <a name="next-steps"></a>Next steps
[Configuring Token Lifetime](https://docs.microsoft.com/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD Token Reference](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims)

