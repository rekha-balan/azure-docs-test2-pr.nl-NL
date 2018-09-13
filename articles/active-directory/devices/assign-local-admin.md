---
title: How to manage the local administrators group on Azure AD joined devices | Microsoft Docs
description: Learn how to assign Azure roles to the local administrators group of a Windows device.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2018
ms.author: markvi
ms.reviewer: ravenn
ms.openlocfilehash: cde364cb5231c1cc0b1947da35994862cf45b571
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967482"
---
# <a name="how-to-manage-the-local-administrators-group-on-azure-ad-joined-devices"></a>How to manage the local administrators group on Azure AD joined devices

To manage a Windows device, you need to be a member of the local administrators group. As part of the Azure Active Directory (Azure AD) join process, Azure AD updates the membership of this group on a device. You can customize the membership update to satisfy your business requirements. A membership update is, for example, helpful if you want to enable your helpdesk staff to do tasks requiring administrator rights on a device.

This article explains how the membership update works and how you can customize it during an Azure AD Join. The content of this article doesn't apply to a **hybrid** Azure AD join.


## <a name="how-it-works"></a>How it works

When you connect a Windows device with Azure AD using an Azure AD join, Azure AD adds the following security principles to the local administrators group on the device:

- The Azure AD global administrator role
- The Azure AD device administrator role 
- The user performing the Azure AD join   

By adding Azure AD roles to the local administrators group, you can update the users that can manage a device anytime in Azure AD without modifying anything on the device. Currently, you cannot assign groups to an administrator role.
Azure AD also adds the Azure AD device administrator role to the local administrators group to support the principle of least privilege (PoLP). In addition to the global administrators, you can also enable users that have been *only* assigned the device administrator role to manage a device. 


## <a name="manage-the-global-administrators-role"></a>Manage the global administrators role

To view and update the membership of the global administrator role, see:

- [View all members of an administrator role in Azure Active Directory](../users-groups-roles/directory-manage-roles-portal.md)

- [Assign a user to administrator roles in Azure Active Directory](../fundamentals/active-directory-users-assign-role-azure-portal.md)


## <a name="manage-the-device-administrator-role"></a>Manage the device administrator role 

In the Azure portal, you can manage the device administrator role on the **Devices** page. To open the **Devices** page:

1. Sign in to your [Azure portal](https://portal.azure.com) as a global administrator or device administrator.
2. On the left navbar, click **Azure Active Directory**. 
3. In the **Manage** section, click **Devices**.
4. On the **Devices** page, click **Device settings**.

To modify the device administrator role, configure **Additional local administrators on Azure AD joined devices**.  

![Additional local administrators](./media/assign-local-admin/10.png)

 
Device administrators are assigned to all Azure AD joined devices. You cannot scope device administrators to a specific set of devices. Updating the device administrator role doesn't necessarily have an immediate impact on the affected users. For the devices, a user is already signed into, the privilege update takes place:
     

- When a user signs off.
- After 4 hours, when a new Primary Refresh Token is issued. 




## <a name="manage-regular-users"></a>Manage regular users

By default, Azure AD adds the user performing the Azure AD join to the administrator group on the device. If you want to prevent regular users from becoming local administrators, you have the following options:

- [Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot) - Windows Autopilot provides you with an option to prevent primary user performing the join from becoming a local administrator. You can accomplish this by [creating an Autopilot profile](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile).
 
- [Bulk enrollment](https://docs.microsoft.com/intune/windows-bulk-enroll) - An Azure AD join that is performed in the context of a bulk enrollment happens in the context of an auto-created user. Users signing in after a device has been joined are not added to the administrators group.   



## <a name="manually-elevate-a-user-on-a-device"></a>Manually elevate a user on a device 

In addition to using the Azure AD join process, you can also manually elevate a regular user to become a local administrator on one specific device. This step requires you to already be a member of the local administrators group. 

Starting with the **Windows 10 1709** release, you can do perform this task from **Settings -> Accounts -> Other users** by selecting **Add a work or school user**.
 
Additionally, you can also add users using the command prompt:

- If your tenant users are synchronized from on-premises Active Directory, use `net localgroup administrators /add “Contoso\username”`.

- If your tenant users are created in Azure AD, use `net localgroup administrators /add “AzureAD\UserUpn”`


## <a name="considerations"></a>Considerations 

You cannot assign groups to the device administrator role, only individual users are allowed.

Device administrators are assigned to all Azure AD Joined devices. They can't be scoped to a specific set of devices.

When you remove users from the device administrator role, they still have the local administrator privilege on a device as long as they are signed in to it. The privilege is revoked during the next sing-in, or after 4 hours when a new primary refresh token is issued.



## <a name="next-steps"></a>Next steps

- To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)

- To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](../conditional-access/require-managed-devices.md).

