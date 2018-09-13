---
title: Permissions in Azure Security Center | Microsoft Docs
description: This article explains how Azure Security Center uses role-based access control to assign permissions to users and identifies the allowed actions for each role.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: ''
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: terrylan
ms.openlocfilehash: d1c8a39bbcda7d22fdce08d122098e994ca87451
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554071"
---
# <a name="permissions-in-azure-security-center"></a>Permissions in Azure Security Center

Azure Security Center uses [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md), which provides [built-in roles](../active-directory/role-based-access-built-in-roles.md) that can be assigned to users, groups, and services in Azure.

Security Center assesses the configuration of your resources to identify security issues and vulnerabilities. In Security Center, you only see information related to a resource when you are assigned the role of Owner, Contributor, or Reader for the subscription or resource group that a resource belongs to.

## <a name="roles-and-allowed-actions"></a>Roles and allowed actions

The following table displays roles and allowed actions in Security Center. An X indicates that the action is allowed for that role.

| Role | Edit security policy | Apply security recommendations for a resource | Remediate or Dismiss alerts | View alerts across a subscription | View alerts for a specific resource |
|:--- |:---:|:---:|:---:|:---:|:---:|
| Subscription Owner | X | X | X | X | X |
| Subscription Contributor | X | X | X | X | X |
| Resource Group Owner | -- | X | -- | -- | X |
| Resource Group Contributor | -- | X | -- | -- | X |
| Reader | -- | -- | -- | X | X |

> [!NOTE]
> We recommend that you assign the least permissive role needed for users to complete their tasks. For example, assign the Reader role to users who only need to view information about the security health of a resource but not take action, such as applying recommendations or editing policies.
>
>

## <a name="next-steps"></a>Next steps
This article explained how Security Center uses RBAC to assign permissions to users and identified the allowed actions for each role. Now that you're familiar with the role assignments needed to monitor the security state of your subscription, edit security policies, and apply recommendations, learn how to:

- [Set security policies in Security Center](security-center-policies.md)
- [Manage security recommendations in Security Center](security-center-recommendations.md)
- [Monitor the security health of your Azure resources](security-center-monitoring.md)
- [Manage and respond to security alerts in Security Center](security-center-managing-and-responding-alerts.md)
- [Monitor partner security solutions](security-center-partner-solutions.md)
