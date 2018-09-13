---
title: Troubleshooting dynamic membership for groups | Microsoft Docs
description: Troubleshooting tips for dynamic membership for groups in Azure AD.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 08/01/2018
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: 82a5c57ce874e77a7912945a6fca07acee339197
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864930"
---
# <a name="troubleshooting-dynamic-memberships-for-groups"></a>Troubleshooting dynamic memberships for groups

**I configured a rule on a group but no memberships get updated in the group**<br/>Verify the values for user attributes on the rule: are there users that satisfy the rule? If everything looks good, please allow some time for the group to populate. Depending on the size of your tenant, the group may take up to 24 hours for populating for the first time or after a rule change.

**I configured a rule, but now the existing members of the rule are removed**<br/>This is expected behavior. Existing members of the group are removed when a rule is enabled or changed. The users returned from evaluation of the rule are added as members to the group.

**I don’t see membership changes instantly when I add or change a rule, why not?**<br/>Dedicated membership evaluation is done periodically in an asynchronous background process. How long the process takes is determined by the number of users in your directory and the size of the group created as a result of the rule. Typically, directories with small numbers of users will see the group membership changes in less than a few minutes. Directories with a large number of users can take 30 minutes or longer to populate.

**I encountered a rule processing error**<br/>The following table lists common dynamic membership rule errors and how to correct them.

| Rule parser error | Error usage | Corrected usage |
| --- | --- | --- |
| Error: Attribute not supported. |(user.invalidProperty -eq "Value") |(user.department -eq "value")<br/><br/>Make sure the attribute is on the [supported properties list](groups-dynamic-membership.md#supported-properties). |
| Error: Operator is not supported on attribute. |(user.accountEnabled -contains true) |(user.accountEnabled -eq true)<br/><br/>The operator used is not supported for the property type (in this example, -contains cannot be used on type boolean). Use the correct operators for the property type. |
| Error: Query compilation error. | 1. (user.department -eq "Sales") (user.department -eq "Marketing")<br>2.  (user.userPrincipalName -match "*@domain.ext") | 1. Missing operator. Use -and or -or two join predicates<br>(user.department -eq "Sales") -or (user.department -eq "Marketing")<br>2. Error in regular expression used with -match<br>(user.userPrincipalName -match ".*@domain.ext")<br>or alternatively: (user.userPrincipalName -match "@domain.ext$") |

## <a name="next-steps"></a>Next steps

These articles provide additional information on Azure Active Directory.

* [Managing access to resources with Azure Active Directory groups](../fundamentals/active-directory-manage-groups.md)
* [Article Index for Application Management in Azure Active Directory](../active-directory-apps-index.md)
* [What is Azure Active Directory?](../fundamentals/active-directory-whatis.md)
* [Integrating your on-premises identities with Azure Active Directory](../connect/active-directory-aadconnect.md)
