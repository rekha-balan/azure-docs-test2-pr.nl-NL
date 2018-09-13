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
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a>How to change the token lifetime defaults for a custom-developed application

Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients. Token lifetime policies are set on a tenant-wide basis or the resources being accessed.

 * To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).

 * Run the **Connect-AzureAD -Confirm** command.

 * Here’s an example policy that sets the max age single factor refresh token. Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.

## <a name="next-steps"></a>Next steps
[Configuring Token Lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Azure AD Token Reference](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

