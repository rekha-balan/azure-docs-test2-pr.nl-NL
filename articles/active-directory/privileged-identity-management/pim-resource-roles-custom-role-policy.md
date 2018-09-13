---
title: Use custom roles for Azure resources in PIM | Microsoft Docs
description: Learn how to use custom roles for Azure resources in Azure AD Privileged Identity Management (PIM).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: pim
ms.date: 03/30/2018
ms.author: rolyon
ms.openlocfilehash: b01e785ac85c71b2982561e8b5e118775750fc69
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855773"
---
# <a name="use-custom-roles-for-azure-resources-in-pim"></a>Use custom roles for Azure resources in PIM

You might need to apply strict Privileged Identity Management (PIM) settings to some members of a role, while providing greater autonomy for others. Consider a scenario in which your organization hires several contract associates to assist in the development of an application that will run in an Azure subscription.

As a resource administrator, you want employees to be eligible for access without requiring approval. However, all contract associates must be approved when they request access to the organization's resources.

Follow the steps outlined in the next section to set up targeted PIM settings for Azure resource roles.

## <a name="create-the-custom-role"></a>Create the custom role

To create a custom role for a resource, follow the steps described in [Create custom roles for Azure Role-Based Access Control](../role-based-access-control-custom-roles.md).

When you create custom role, include a descriptive name so you can easily remember which built-in role you intended to duplicate.

> [!NOTE]
> Ensure that the custom role is a duplicate of the built-in role you want to duplicate, and that its scope matches the built-in role.

## <a name="apply-pim-settings"></a>Apply PIM settings

After the role is created in your tenant, in the Azure portal, go to the **Privileged Identity Management - Azure resources** pane. Select the resource that the role applies to.

![The "Privileged Identity Management - Azure resources" pane](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

[Configure PIM role settings](pim-resource-roles-configure-role-settings.md) that should apply to these members of the role.

Finally, [assign roles](pim-resource-roles-assign-roles.md) to the distinct group of members that you want to target with these settings.

## <a name="next-steps"></a>Next steps

- [Configure Azure resource role settings in PIM](pim-resource-roles-configure-role-settings.md)
- [Custom roles in Azure](../../role-based-access-control/custom-roles.md)
