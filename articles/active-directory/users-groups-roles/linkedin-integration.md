---
title: Enable LinkedIn connections integration in Azure Active Directory | Microsoft Docs
description: Explains how to enable or disable LinkedIn account connections for Microsoft apps in Azure Active Directory
services: active-directory
author: curtand
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.component: users-groups-roles
ms.topic: article
ms.date: 09/11/2018
ms.author: curtand
ms.reviewer: beengen
ms.custom: it-pro
ms.openlocfilehash: 0eaa2656313ecd9b64503051265dc16285f0a1f3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867639"
---
# <a name="linkedin-account-connections"></a>LinkedIn account connections

In this article, you can learn how to enable or disable LinkedIn account connections for your tenant in the Azure Active Directory (Azure AD) admin center.

> [!IMPORTANT]
> The LinkedIn account connections setting is currently being rolled out to Azure AD tenants. When it is rolled out to your tenant, it is enabled by default. 
> 
> Exceptions:
> * The setting is not available for customers using Microsoft Cloud for US Government, Microsoft Cloud Germany, or Azure and Office 365 operated by 21Vianet in China.
> * The setting is off by default for tenants provisioned in Germany. Note that the setting is not available for customers using Microsoft Cloud Germany.
> * The setting is off by default for tenants provisioned in France.

> The integration works only if you have it enabled *and* if you allow users to consent to apps accessing company data on their behalf. For information about the consent setting, see [How to remove a user’s access to an application](https://docs.microsoft.com/azure/active-directory/application-access-assignment-how-to-remove-assignment).

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-in-the-azure-portal"></a>Enable or disable LinkedIn account connections for your tenant in the Azure portal

You can enable or disable LinkedIn account connections for your entire tenant or for only selected users in your tenant.

1. Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com/) with an account that's a global admin for the Azure AD tenant.
2. Select **Users**.
3. On the **Users** blade, select **User settings**.
4. Under **LinkedIn account connections**:
  * Select **Yes** to enable LinkedIn account connections for all users in your tenant
  * Select **Selected** to enable LinkedIn account connections for only selected tenant users
  * Select **No** to disable LinkedIn account connections for all users ![Enabling LinkedIn account connections](./media/linkedin-integration/linkedin-integration.png)
5. Save your settings when you're done by selecting **Save**.

## <a name="enable-or-disable-linkedin-account-connections-for-your-tenant-using-group-policy"></a>Enable or disable LinkedIn account connections for your tenant using Group Policy

1. Download the [Office 2016 Administrative Template files (ADMX/ADML)](https://www.microsoft.com/download/details.aspx?id=49030)
2. Extract the **ADMX** files and copy them to your central store.
3. Open Group Policy Management.
4. Create a Group Policy Object with the following setting: **User Configuration** > **Administrative Templates** > **Microsoft Office 2016** > **Miscellaneous** > **Show LinkedIn features in Office applications**.
5. Select **Enabled** or **Disabled**.
  
 State | Effect
------ | ------
**Enabled** | The **Show LinkedIn features in Office applications** setting in Office 2016 Options is enabled. Users in your organization can use LinkedIn features in their Office applications.
 **Disabled** | The **Show LinkedIn features in Office applications** setting in Office 2016 Options is disabled and end users can't change this setting. Users in your organization can't use LinkedIn features in their Office 2016 applications.

This group policy affects only Office 2016 apps for a local computer. Users can see LinkedIn features in profile cards throughout Office 365 even if they disable LinkedIn in their Office 2016 apps.

## <a name="learn-more"></a>Learn more

* [Integrate LinkedIn in your organization](linkedin-user-consent.md)

* [LinkedIn information and features in your Microsoft apps](https://go.microsoft.com/fwlink/?linkid=850740)

* [LinkedIn help center](https://www.linkedin.com/help/linkedin)

## <a name="next-steps"></a>Next steps
Use the following link to see your current LinkedIn account connections setting in the Azure portal:

[Configure LinkedIn account connections](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/UserSettings) 