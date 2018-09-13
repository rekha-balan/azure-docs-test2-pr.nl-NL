---
title: Enable subscription management in your tenant - Azure | Microsoft Docs
description: Learn how to enable enable subscription management in your tenant when using Azure AD Privileged Identity Management (PIM).
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
ms.date: 03/27/2018
ms.author: rolyon
ms.custom: pim
ms.openlocfilehash: 89bb6fd48c58b7672b7a2251a172cc169093d368
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857901"
---
# <a name="enable-subscription-management-in-your-tenant"></a>Enable subscription management in your tenant

As a global administrator of your directory, you might not have default access to all subscription resources in your tenant. This article outlines the steps to give yourself access to all subscriptions in your tenant. It also provides a recommended approach to remaining compliant with any security controls your organization requires after you receive access.

## <a name="who-can-enable-management-of-subscriptions-in-my-directory"></a>Who can enable management of subscriptions in my directory?

Each user assigned to the global administrator role must follow the steps below to enable subscription management. After you have enabled subscription management for yourself, you can add other global administrators who might need resource access as well. There is no directory setting that enables access for all members of the global administrator role.

## <a name="sign-in-to-the-azure-portal"></a>Sign in to the Azure portal

Sign in to the Azure portal with an account that is an eligible or active member of the global administrator role. If the account is an eligible global administrator, you must first activate the role before moving on to the next step.

## <a name="access-the-azure-active-directory-admin-center"></a>Access the Azure Active Directory admin center

Now that you are signed in to the Azure portal as a global administrator, you can edit settings that provide access to Azure subscriptions. Browse to the Azure Active Directory (Azure AD) admin center, and select **Properties**.

![Screenshot of Azure AD admin center, with Properties highlighted](media/azure-pim-resource-rbac/aad_properties.png)

In the list of properties, under **Global admin can manage Azure subscriptions**, select **Yes**.

![Screenshot of Properties page, with toggle set to Yes](media/azure-pim-resource-rbac/aad_properties_save.png)

Now your account is automatically added to the user access administrator role for every subscription resource in the tenant.

## <a name="browse-to-azure-ad-pim"></a>Browse to Azure AD PIM

 From here, go to Azure AD Privileged Identity Management (PIM). Under **Manage**, select **Azure resources**.

![Screenshot of PIM, with Azure resources highlighted](media/azure-pim-resource-rbac/aadpim_manage_azure_resources.png)

## <a name="manage-and-discover-resources"></a>Manage and discover resources

If your organization is already using Azure AD PIM to protect administrators in Azure AD, you can see a list of subscriptions when the blade loads.

![Screenshot of PIM, with list of subscriptions shown in blade](media/azure-pim-resource-rbac/aadpim_manage_azure_resource_some_there.png)

> [!NOTE]
> If you do not see any resources, confirm that:
>- Your global administrator role is not expired. 
>- Your organization has an Azure subscription.

![Screenshot of PIM, with empty resource list](media/azure-pim-resource-rbac/aadpim_rbac_empty_resource_list.png)

## <a name="configure-assignments"></a>Configure assignments

Select a subscription from the list, and assign yourself (or a group you are a member of) as an eligible owner of the resource. 
[Read more about assigning roles](pim-resource-roles-assign-roles.md).

Repeat this process for each resource before proceeding to the next step.

## <a name="clean-up-standing-access"></a>Clean up standing access

Now that you have eligible assignments for the important subscriptions in your organization, you can clean up standing access by disabling the option in directory properties.

![Screenshot of Properties page, with toggle set to No](media/azure-pim-resource-rbac/aad_properties_no.png)

## <a name="next-steps"></a>Next steps

- [Discover Azure resources to manage in PIM](pim-resource-roles-discover-resources.md)
- [Configure Azure resource role settings in PIM](pim-resource-roles-configure-role-settings.md)
