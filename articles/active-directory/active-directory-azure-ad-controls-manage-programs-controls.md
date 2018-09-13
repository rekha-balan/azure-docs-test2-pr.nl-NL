---
title: Manage programs and controls for Azure AD access reviews| Microsoft Docs
description: You can create additional programs for each governance, risk management, and compliance initiative in your organization to collect and organize Azure Active Directory access reviews as controls.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: compliance
ms.date: 06/21/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: a1a08ac29605e66dc14ac5e32d21e00dad8cb655
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866204"
---
# <a name="manage-programs-and-their-controls"></a>Manage programs and their controls 

Azure Active Directory (Azure AD) includes access reviews of group members and application access. These examples of controls ensure oversight for who has access to your organization's group memberships and applications. Organizations can use these controls to efficiently address their governance, risk management, and compliance requirements.

## <a name="create-and-manage-programs-and-their-controls"></a>Create and manage programs and their controls
You can simplify how to track and collect access reviews for different purposes by organizing them into programs. Each access review can be linked to a program. Then when you prepare reports for an auditor, you can focus on the access reviews in scope for a particular initiative.  Programs and access review results are visible to users in the Global Administrator, User Account Administrator, Security Administrator, or Security Reader role.

To see a list of programs, go to the [access reviews page](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/) and select **Programs**.

**Default Program** is always present. If you're in a global administrator or user account administrator role, you can create additional programs. For example, you can choose to have one program for each compliance initiative or business goal.

If you no longer need a program and it doesn't have any controls linked to it, you can delete it.

## <a name="next-steps"></a>Next steps

- [Create an access review for members of a group or access to an application](active-directory-azure-ad-controls-create-access-review.md)
- [Retrieve the results of an access review](active-directory-azure-ad-controls-retrieve-access-review.md)
