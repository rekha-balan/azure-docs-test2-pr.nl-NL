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
# <a name="how-to-manage-the-local-administrators-group-on-azure-ad-joined-devices"></a><span data-ttu-id="6300b-103">How to manage the local administrators group on Azure AD joined devices</span><span class="sxs-lookup"><span data-stu-id="6300b-103">How to manage the local administrators group on Azure AD joined devices</span></span>

<span data-ttu-id="6300b-104">To manage a Windows device, you need to be a member of the local administrators group.</span><span class="sxs-lookup"><span data-stu-id="6300b-104">To manage a Windows device, you need to be a member of the local administrators group.</span></span> <span data-ttu-id="6300b-105">As part of the Azure Active Directory (Azure AD) join process, Azure AD updates the membership of this group on a device.</span><span class="sxs-lookup"><span data-stu-id="6300b-105">As part of the Azure Active Directory (Azure AD) join process, Azure AD updates the membership of this group on a device.</span></span> <span data-ttu-id="6300b-106">You can customize the membership update to satisfy your business requirements.</span><span class="sxs-lookup"><span data-stu-id="6300b-106">You can customize the membership update to satisfy your business requirements.</span></span> <span data-ttu-id="6300b-107">A membership update is, for example, helpful if you want to enable your helpdesk staff to do tasks requiring administrator rights on a device.</span><span class="sxs-lookup"><span data-stu-id="6300b-107">A membership update is, for example, helpful if you want to enable your helpdesk staff to do tasks requiring administrator rights on a device.</span></span>

<span data-ttu-id="6300b-108">This article explains how the membership update works and how you can customize it during an Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="6300b-108">This article explains how the membership update works and how you can customize it during an Azure AD Join.</span></span> <span data-ttu-id="6300b-109">The content of this article doesn't apply to a **hybrid** Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="6300b-109">The content of this article doesn't apply to a **hybrid** Azure AD join.</span></span>


## <a name="how-it-works"></a><span data-ttu-id="6300b-110">How it works</span><span class="sxs-lookup"><span data-stu-id="6300b-110">How it works</span></span>

<span data-ttu-id="6300b-111">When you connect a Windows device with Azure AD using an Azure AD join, Azure AD adds the following security principles to the local administrators group on the device:</span><span class="sxs-lookup"><span data-stu-id="6300b-111">When you connect a Windows device with Azure AD using an Azure AD join, Azure AD adds the following security principles to the local administrators group on the device:</span></span>

- <span data-ttu-id="6300b-112">The Azure AD global administrator role</span><span class="sxs-lookup"><span data-stu-id="6300b-112">The Azure AD global administrator role</span></span>
- <span data-ttu-id="6300b-113">The Azure AD device administrator role</span><span class="sxs-lookup"><span data-stu-id="6300b-113">The Azure AD device administrator role</span></span> 
- <span data-ttu-id="6300b-114">The user performing the Azure AD join</span><span class="sxs-lookup"><span data-stu-id="6300b-114">The user performing the Azure AD join</span></span>   

<span data-ttu-id="6300b-115">By adding Azure AD roles to the local administrators group, you can update the users that can manage a device anytime in Azure AD without modifying anything on the device.</span><span class="sxs-lookup"><span data-stu-id="6300b-115">By adding Azure AD roles to the local administrators group, you can update the users that can manage a device anytime in Azure AD without modifying anything on the device.</span></span> <span data-ttu-id="6300b-116">Currently, you cannot assign groups to an administrator role.</span><span class="sxs-lookup"><span data-stu-id="6300b-116">Currently, you cannot assign groups to an administrator role.</span></span>
<span data-ttu-id="6300b-117">Azure AD also adds the Azure AD device administrator role to the local administrators group to support the principle of least privilege (PoLP).</span><span class="sxs-lookup"><span data-stu-id="6300b-117">Azure AD also adds the Azure AD device administrator role to the local administrators group to support the principle of least privilege (PoLP).</span></span> <span data-ttu-id="6300b-118">In addition to the global administrators, you can also enable users that have been *only* assigned the device administrator role to manage a device.</span><span class="sxs-lookup"><span data-stu-id="6300b-118">In addition to the global administrators, you can also enable users that have been *only* assigned the device administrator role to manage a device.</span></span> 


## <a name="manage-the-global-administrators-role"></a><span data-ttu-id="6300b-119">Manage the global administrators role</span><span class="sxs-lookup"><span data-stu-id="6300b-119">Manage the global administrators role</span></span>

<span data-ttu-id="6300b-120">To view and update the membership of the global administrator role, see:</span><span class="sxs-lookup"><span data-stu-id="6300b-120">To view and update the membership of the global administrator role, see:</span></span>

- [<span data-ttu-id="6300b-121">View all members of an administrator role in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6300b-121">View all members of an administrator role in Azure Active Directory</span></span>](../users-groups-roles/directory-manage-roles-portal.md)

- [<span data-ttu-id="6300b-122">Assign a user to administrator roles in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6300b-122">Assign a user to administrator roles in Azure Active Directory</span></span>](../fundamentals/active-directory-users-assign-role-azure-portal.md)


## <a name="manage-the-device-administrator-role"></a><span data-ttu-id="6300b-123">Manage the device administrator role</span><span class="sxs-lookup"><span data-stu-id="6300b-123">Manage the device administrator role</span></span> 

<span data-ttu-id="6300b-124">In the Azure portal, you can manage the device administrator role on the **Devices** page.</span><span class="sxs-lookup"><span data-stu-id="6300b-124">In the Azure portal, you can manage the device administrator role on the **Devices** page.</span></span> <span data-ttu-id="6300b-125">To open the **Devices** page:</span><span class="sxs-lookup"><span data-stu-id="6300b-125">To open the **Devices** page:</span></span>

1. <span data-ttu-id="6300b-126">Sign in to your [Azure portal](https://portal.azure.com) as a global administrator or device administrator.</span><span class="sxs-lookup"><span data-stu-id="6300b-126">Sign in to your [Azure portal](https://portal.azure.com) as a global administrator or device administrator.</span></span>
2. <span data-ttu-id="6300b-127">On the left navbar, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6300b-127">On the left navbar, click **Azure Active Directory**.</span></span> 
3. <span data-ttu-id="6300b-128">In the **Manage** section, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="6300b-128">In the **Manage** section, click **Devices**.</span></span>
4. <span data-ttu-id="6300b-129">On the **Devices** page, click **Device settings**.</span><span class="sxs-lookup"><span data-stu-id="6300b-129">On the **Devices** page, click **Device settings**.</span></span>

<span data-ttu-id="6300b-130">To modify the device administrator role, configure **Additional local administrators on Azure AD joined devices**.</span><span class="sxs-lookup"><span data-stu-id="6300b-130">To modify the device administrator role, configure **Additional local administrators on Azure AD joined devices**.</span></span>  

![Additional local administrators](./media/assign-local-admin/10.png)

 
<span data-ttu-id="6300b-132">Device administrators are assigned to all Azure AD joined devices.</span><span class="sxs-lookup"><span data-stu-id="6300b-132">Device administrators are assigned to all Azure AD joined devices.</span></span> <span data-ttu-id="6300b-133">You cannot scope device administrators to a specific set of devices.</span><span class="sxs-lookup"><span data-stu-id="6300b-133">You cannot scope device administrators to a specific set of devices.</span></span> <span data-ttu-id="6300b-134">Updating the device administrator role doesn't necessarily have an immediate impact on the affected users.</span><span class="sxs-lookup"><span data-stu-id="6300b-134">Updating the device administrator role doesn't necessarily have an immediate impact on the affected users.</span></span> <span data-ttu-id="6300b-135">For the devices, a user is already signed into, the privilege update takes place:</span><span class="sxs-lookup"><span data-stu-id="6300b-135">For the devices, a user is already signed into, the privilege update takes place:</span></span>
     

- <span data-ttu-id="6300b-136">When a user signs off.</span><span class="sxs-lookup"><span data-stu-id="6300b-136">When a user signs off.</span></span>
- <span data-ttu-id="6300b-137">After 4 hours, when a new Primary Refresh Token is issued.</span><span class="sxs-lookup"><span data-stu-id="6300b-137">After 4 hours, when a new Primary Refresh Token is issued.</span></span> 




## <a name="manage-regular-users"></a><span data-ttu-id="6300b-138">Manage regular users</span><span class="sxs-lookup"><span data-stu-id="6300b-138">Manage regular users</span></span>

<span data-ttu-id="6300b-139">By default, Azure AD adds the user performing the Azure AD join to the administrator group on the device.</span><span class="sxs-lookup"><span data-stu-id="6300b-139">By default, Azure AD adds the user performing the Azure AD join to the administrator group on the device.</span></span> <span data-ttu-id="6300b-140">If you want to prevent regular users from becoming local administrators, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="6300b-140">If you want to prevent regular users from becoming local administrators, you have the following options:</span></span>

- <span data-ttu-id="6300b-141">[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot) - Windows Autopilot provides you with an option to prevent primary user performing the join from becoming a local administrator.</span><span class="sxs-lookup"><span data-stu-id="6300b-141">[Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot) - Windows Autopilot provides you with an option to prevent primary user performing the join from becoming a local administrator.</span></span> <span data-ttu-id="6300b-142">You can accomplish this by [creating an Autopilot profile](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile).</span><span class="sxs-lookup"><span data-stu-id="6300b-142">You can accomplish this by [creating an Autopilot profile](https://docs.microsoft.com/intune/enrollment-autopilot#create-an-autopilot-deployment-profile).</span></span>
 
- <span data-ttu-id="6300b-143">[Bulk enrollment](https://docs.microsoft.com/intune/windows-bulk-enroll) - An Azure AD join that is performed in the context of a bulk enrollment happens in the context of an auto-created user.</span><span class="sxs-lookup"><span data-stu-id="6300b-143">[Bulk enrollment](https://docs.microsoft.com/intune/windows-bulk-enroll) - An Azure AD join that is performed in the context of a bulk enrollment happens in the context of an auto-created user.</span></span> <span data-ttu-id="6300b-144">Users signing in after a device has been joined are not added to the administrators group.</span><span class="sxs-lookup"><span data-stu-id="6300b-144">Users signing in after a device has been joined are not added to the administrators group.</span></span>   



## <a name="manually-elevate-a-user-on-a-device"></a><span data-ttu-id="6300b-145">Manually elevate a user on a device</span><span class="sxs-lookup"><span data-stu-id="6300b-145">Manually elevate a user on a device</span></span> 

<span data-ttu-id="6300b-146">In addition to using the Azure AD join process, you can also manually elevate a regular user to become a local administrator on one specific device.</span><span class="sxs-lookup"><span data-stu-id="6300b-146">In addition to using the Azure AD join process, you can also manually elevate a regular user to become a local administrator on one specific device.</span></span> <span data-ttu-id="6300b-147">This step requires you to already be a member of the local administrators group.</span><span class="sxs-lookup"><span data-stu-id="6300b-147">This step requires you to already be a member of the local administrators group.</span></span> 

<span data-ttu-id="6300b-148">Starting with the **Windows 10 1709** release, you can do perform this task from **Settings -> Accounts -> Other users** by selecting **Add a work or school user**.</span><span class="sxs-lookup"><span data-stu-id="6300b-148">Starting with the **Windows 10 1709** release, you can do perform this task from **Settings -> Accounts -> Other users** by selecting **Add a work or school user**.</span></span>
 
<span data-ttu-id="6300b-149">Additionally, you can also add users using the command prompt:</span><span class="sxs-lookup"><span data-stu-id="6300b-149">Additionally, you can also add users using the command prompt:</span></span>

- <span data-ttu-id="6300b-150">If your tenant users are synchronized from on-premises Active Directory, use `net localgroup administrators /add “Contoso\username”`.</span><span class="sxs-lookup"><span data-stu-id="6300b-150">If your tenant users are synchronized from on-premises Active Directory, use `net localgroup administrators /add “Contoso\username”`.</span></span>

- <span data-ttu-id="6300b-151">If your tenant users are created in Azure AD, use `net localgroup administrators /add “AzureAD\UserUpn”`</span><span class="sxs-lookup"><span data-stu-id="6300b-151">If your tenant users are created in Azure AD, use `net localgroup administrators /add “AzureAD\UserUpn”`</span></span>


## <a name="considerations"></a><span data-ttu-id="6300b-152">Considerations</span><span class="sxs-lookup"><span data-stu-id="6300b-152">Considerations</span></span> 

<span data-ttu-id="6300b-153">You cannot assign groups to the device administrator role, only individual users are allowed.</span><span class="sxs-lookup"><span data-stu-id="6300b-153">You cannot assign groups to the device administrator role, only individual users are allowed.</span></span>

<span data-ttu-id="6300b-154">Device administrators are assigned to all Azure AD Joined devices.</span><span class="sxs-lookup"><span data-stu-id="6300b-154">Device administrators are assigned to all Azure AD Joined devices.</span></span> <span data-ttu-id="6300b-155">They can't be scoped to a specific set of devices.</span><span class="sxs-lookup"><span data-stu-id="6300b-155">They can't be scoped to a specific set of devices.</span></span>

<span data-ttu-id="6300b-156">When you remove users from the device administrator role, they still have the local administrator privilege on a device as long as they are signed in to it.</span><span class="sxs-lookup"><span data-stu-id="6300b-156">When you remove users from the device administrator role, they still have the local administrator privilege on a device as long as they are signed in to it.</span></span> <span data-ttu-id="6300b-157">The privilege is revoked during the next sing-in, or after 4 hours when a new primary refresh token is issued.</span><span class="sxs-lookup"><span data-stu-id="6300b-157">The privilege is revoked during the next sing-in, or after 4 hours when a new primary refresh token is issued.</span></span>



## <a name="next-steps"></a><span data-ttu-id="6300b-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="6300b-158">Next steps</span></span>

- <span data-ttu-id="6300b-159">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6300b-159">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="6300b-160">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](../conditional-access/require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="6300b-160">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](../conditional-access/require-managed-devices.md).</span></span>


