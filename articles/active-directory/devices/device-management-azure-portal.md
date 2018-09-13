---
title: How to manage devices using the Azure portal | Microsoft Docs
description: Learn how to use the Azure portal to manage devices.
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
ms.date: 08/25/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: ff1d51021038909c132bef4cb680589b9951f218
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869349"
---
# <a name="how-to-manage-devices-using-the-azure-portal"></a><span data-ttu-id="5e7e4-103">How to manage devices using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5e7e4-103">How to manage devices using the Azure portal</span></span>


<span data-ttu-id="5e7e4-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-104">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="5e7e4-105">This article:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-105">This article:</span></span>

- <span data-ttu-id="5e7e4-106">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](overview.md)</span><span class="sxs-lookup"><span data-stu-id="5e7e4-106">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](overview.md)</span></span>

- <span data-ttu-id="5e7e4-107">Provides you with information about managing your devices using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="5e7e4-107">Provides you with information about managing your devices using the Azure portal</span></span>

## <a name="manage-devices"></a><span data-ttu-id="5e7e4-108">Manage devices</span><span class="sxs-lookup"><span data-stu-id="5e7e4-108">Manage devices</span></span> 

<span data-ttu-id="5e7e4-109">The Azure portal provides you with a central place to manage your devices.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-109">The Azure portal provides you with a central place to manage your devices.</span></span> <span data-ttu-id="5e7e4-110">You can get to this place by either using a [direct link](https://portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/Devices) or by following these manual steps:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-110">You can get to this place by either using a [direct link](https://portal.azure.com/#blade/Microsoft_AAD_IAM/DevicesMenuBlade/Devices) or by following these manual steps:</span></span>

1. <span data-ttu-id="5e7e4-111">Sign in to the [Azure portal](https://portal.azure.com) as administrator.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-111">Sign in to the [Azure portal](https://portal.azure.com) as administrator.</span></span>

2. <span data-ttu-id="5e7e4-112">On the left navbar, click **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-112">On the left navbar, click **Active Directory**.</span></span>

    ![Configure device settings](./media/device-management-azure-portal/01.png)

3. <span data-ttu-id="5e7e4-114">In the **Manage** section, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-114">In the **Manage** section, click **Devices**.</span></span>

    ![Configure device settings](./media/device-management-azure-portal/74.png)
 
<span data-ttu-id="5e7e4-116">The **Devices** page enables you to:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-116">The **Devices** page enables you to:</span></span>

- <span data-ttu-id="5e7e4-117">Configure your device management settings</span><span class="sxs-lookup"><span data-stu-id="5e7e4-117">Configure your device management settings</span></span>

- <span data-ttu-id="5e7e4-118">Locate devices</span><span class="sxs-lookup"><span data-stu-id="5e7e4-118">Locate devices</span></span>

- <span data-ttu-id="5e7e4-119">Perform device management tasks</span><span class="sxs-lookup"><span data-stu-id="5e7e4-119">Perform device management tasks</span></span>

- <span data-ttu-id="5e7e4-120">Review the device management related audit logs</span><span class="sxs-lookup"><span data-stu-id="5e7e4-120">Review the device management related audit logs</span></span>  
  

## <a name="configure-device-settings"></a><span data-ttu-id="5e7e4-121">Configure device settings</span><span class="sxs-lookup"><span data-stu-id="5e7e4-121">Configure device settings</span></span>

<span data-ttu-id="5e7e4-122">To manage your devices using the Azure portal, your devices need to be either [registered or joined](overview.md#getting-devices-under-the-control-of-azure-ad) to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-122">To manage your devices using the Azure portal, your devices need to be either [registered or joined](overview.md#getting-devices-under-the-control-of-azure-ad) to Azure AD.</span></span> <span data-ttu-id="5e7e4-123">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-123">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span> 

![Configure device settings](./media/device-management-azure-portal/22.png)

<span data-ttu-id="5e7e4-125">The device settings page enables you to configure:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-125">The device settings page enables you to configure:</span></span>

![Manage an Intune device](./media/device-management-azure-portal/21.png)


- <span data-ttu-id="5e7e4-127">**Users may join devices to Azure AD** - This setting enables you to select the users who can [join devices](overview.md#azure-ad-joined-devices) to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-127">**Users may join devices to Azure AD** - This setting enables you to select the users who can [join devices](overview.md#azure-ad-joined-devices) to Azure AD.</span></span> <span data-ttu-id="5e7e4-128">The default is **All**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-128">The default is **All**.</span></span> <span data-ttu-id="5e7e4-129">This setting is only applicable to Azure AD Join on Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-129">This setting is only applicable to Azure AD Join on Windows 10.</span></span>

- <span data-ttu-id="5e7e4-130">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-130">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="5e7e4-131">Users added here are added to the *Device Administrators* role in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-131">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="5e7e4-132">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-132">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="5e7e4-133">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="5e7e4-133">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="5e7e4-134">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be [registered](overview.md#azure-ad-registered-devices) with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-134">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be [registered](overview.md#azure-ad-registered-devices) with Azure AD.</span></span> <span data-ttu-id="5e7e4-135">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-135">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="5e7e4-136">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-136">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="5e7e4-137">If you have configured either of these services, **ALL** is selected and **NONE** is not available.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-137">If you have configured either of these services, **ALL** is selected and **NONE** is not available.</span></span>

- <span data-ttu-id="5e7e4-138">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to [join](overview.md#azure-ad-joined-devices) their device to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-138">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to [join](overview.md#azure-ad-joined-devices) their device to Azure AD.</span></span> <span data-ttu-id="5e7e4-139">The default is **No**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-139">The default is **No**.</span></span> <span data-ttu-id="5e7e4-140">We recommend requiring multi-factor authentication when registering a device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-140">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="5e7e4-141">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-141">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="5e7e4-142">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../authentication/concept-mfa-whichversion.md).</span><span class="sxs-lookup"><span data-stu-id="5e7e4-142">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../authentication/concept-mfa-whichversion.md).</span></span> <span data-ttu-id="5e7e4-143">This setting does not impact hybrid join for Windows 10 or Windows 7.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-143">This setting does not impact hybrid join for Windows 10 or Windows 7.</span></span> <span data-ttu-id="5e7e4-144">This is only applicable to Azure AD Join on Windows 10 and BYO device registration for Windows 10, iOS and Android.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-144">This is only applicable to Azure AD Join on Windows 10 and BYO device registration for Windows 10, iOS and Android.</span></span> 

- <span data-ttu-id="5e7e4-145">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-145">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="5e7e4-146">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-146">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="5e7e4-147">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-147">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="5e7e4-148">The default value is **20**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-148">The default value is **20**.</span></span>

- <span data-ttu-id="5e7e4-149">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-149">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="5e7e4-150">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-150">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="5e7e4-151">Learn more on how sync works in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-151">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="5e7e4-152">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="5e7e4-152">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 




## <a name="locate-devices"></a><span data-ttu-id="5e7e4-153">Locate devices</span><span class="sxs-lookup"><span data-stu-id="5e7e4-153">Locate devices</span></span>

<span data-ttu-id="5e7e4-154">You have two options to locate registered and joined devices:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-154">You have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="5e7e4-155">**All devices** in the **Manage** section of the **Devices** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-155">**All devices** in the **Manage** section of the **Devices** page</span></span>  

    ![All devices](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="5e7e4-157">**Devices** in the **Manage** section of a **User** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-157">**Devices** in the **Manage** section of a **User** page</span></span>
 
    ![All devices](./media/device-management-azure-portal/43.png)



<span data-ttu-id="5e7e4-159">With both options, you can get to a view that:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-159">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="5e7e4-160">Enables you to search for devices using the display name as filter.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-160">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="5e7e4-161">Provides you with detailed overview of registered and joined devices</span><span class="sxs-lookup"><span data-stu-id="5e7e4-161">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="5e7e4-162">Enables you to perform common device management tasks</span><span class="sxs-lookup"><span data-stu-id="5e7e4-162">Enables you to perform common device management tasks</span></span>
   

![All devices](./media/device-management-azure-portal/51.png)

<span data-ttu-id="5e7e4-164">For some iOS devices, the device names containing apostrophes can potentially use different characters that look like apostrophes.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-164">For some iOS devices, the device names containing apostrophes can potentially use different characters that look like apostrophes.</span></span> <span data-ttu-id="5e7e4-165">So searching for such devices is a little tricky - if you are not seeing search results correctly, please ensure that the search string contains matching apostrophe character.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-165">So searching for such devices is a little tricky - if you are not seeing search results correctly, please ensure that the search string contains matching apostrophe character.</span></span>

## <a name="device-management-tasks"></a><span data-ttu-id="5e7e4-166">Device management tasks</span><span class="sxs-lookup"><span data-stu-id="5e7e4-166">Device management tasks</span></span>

<span data-ttu-id="5e7e4-167">As an administrator, you can manage the registered or joined devices.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-167">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="5e7e4-168">This section provides you with information about common device management tasks.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-168">This section provides you with information about common device management tasks.</span></span>


### <a name="manage-an-intune-device"></a><span data-ttu-id="5e7e4-169">Manage an Intune device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-169">Manage an Intune device</span></span>

<span data-ttu-id="5e7e4-170">If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-170">If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="5e7e4-171">An administrator can see additional device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-171">An administrator can see additional device</span></span> 

![Manage an Intune device](./media/device-management-azure-portal/31.png)


### <a name="enable--disable-an-azure-ad-device"></a><span data-ttu-id="5e7e4-173">Enable / disable an Azure AD device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-173">Enable / disable an Azure AD device</span></span>

<span data-ttu-id="5e7e4-174">To enable / disable a device, you have two options:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-174">To enable / disable a device, you have two options:</span></span>

- <span data-ttu-id="5e7e4-175">The tasks menu ("...") on the **All devices** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-175">The tasks menu ("...") on the **All devices** page</span></span>

    ![Manage an Intune device](./media/device-management-azure-portal/71.png)

- <span data-ttu-id="5e7e4-177">The toolbar on the **Devices** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-177">The toolbar on the **Devices** page</span></span>

    ![Manage an Intune device](./media/device-management-azure-portal/32.png)


<span data-ttu-id="5e7e4-179">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="5e7e4-179">**Remarks:**</span></span>

- <span data-ttu-id="5e7e4-180">You need to be a global administrator in Azure  AD to enable / disable a device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-180">You need to be a global administrator in Azure  AD to enable / disable a device.</span></span> 
- <span data-ttu-id="5e7e4-181">Disabling a device prevents a device from accessing your Azure AD resources.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-181">Disabling a device prevents a device from accessing your Azure AD resources.</span></span> 



### <a name="delete-an-azure-ad-device"></a><span data-ttu-id="5e7e4-182">Delete an Azure AD device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-182">Delete an Azure AD device</span></span>

<span data-ttu-id="5e7e4-183">To delete a device, you have two options:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-183">To delete a device, you have two options:</span></span>

- <span data-ttu-id="5e7e4-184">The tasks menu ("...") on the **All devices** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-184">The tasks menu ("...") on the **All devices** page</span></span>

    ![Manage an Intune device](./media/device-management-azure-portal/72.png)

- <span data-ttu-id="5e7e4-186">The toolbar on the **Devices** page</span><span class="sxs-lookup"><span data-stu-id="5e7e4-186">The toolbar on the **Devices** page</span></span>

    ![Delete a device](./media/device-management-azure-portal/34.png)


<span data-ttu-id="5e7e4-188">**Remarks:**</span><span class="sxs-lookup"><span data-stu-id="5e7e4-188">**Remarks:**</span></span>

- <span data-ttu-id="5e7e4-189">You need to be a global administrator or an Intune administrator in Azure AD to delete a device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-189">You need to be a global administrator or an Intune administrator in Azure AD to delete a device.</span></span>

- <span data-ttu-id="5e7e4-190">Deleting a device:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-190">Deleting a device:</span></span>
 
    - <span data-ttu-id="5e7e4-191">Prevents a device from accessing your Azure AD resources.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-191">Prevents a device from accessing your Azure AD resources.</span></span> 

    - <span data-ttu-id="5e7e4-192">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-192">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices.</span></span>  

    - <span data-ttu-id="5e7e4-193">Represents a non-recoverable activity and is not recommended unless it is required.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-193">Represents a non-recoverable activity and is not recommended unless it is required.</span></span>

<span data-ttu-id="5e7e4-194">If a device is managed by another management authority (for example, Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-194">If a device is managed by another management authority (for example, Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

 


### <a name="view-or-copy-device-id"></a><span data-ttu-id="5e7e4-195">View or copy device ID</span><span class="sxs-lookup"><span data-stu-id="5e7e4-195">View or copy device ID</span></span>

<span data-ttu-id="5e7e4-196">You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-196">You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="5e7e4-197">To access the copy option, click the device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-197">To access the copy option, click the device.</span></span>

![View a device ID](./media/device-management-azure-portal/35.png)
  

### <a name="view-or-copy-bitlocker-keys"></a><span data-ttu-id="5e7e4-199">View or copy BitLocker keys</span><span class="sxs-lookup"><span data-stu-id="5e7e4-199">View or copy BitLocker keys</span></span>

<span data-ttu-id="5e7e4-200">You can view and copy the BitLocker keys to help users to recover their encrypted drive.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-200">You can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="5e7e4-201">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-201">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="5e7e4-202">You can copy these keys when accessing details of the device.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-202">You can copy these keys when accessing details of the device.</span></span>
 
![View BitLocker keys](./media/device-management-azure-portal/36.png)

<span data-ttu-id="5e7e4-204">to view or copy the BitLocker keys, you need to be either the owner of the device, or a user that has at least one of the following roles assigned:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-204">to view or copy the BitLocker keys, you need to be either the owner of the device, or a user that has at least one of the following roles assigned:</span></span>

- <span data-ttu-id="5e7e4-205">Global admins</span><span class="sxs-lookup"><span data-stu-id="5e7e4-205">Global admins</span></span>
- <span data-ttu-id="5e7e4-206">Helpdesk Admins</span><span class="sxs-lookup"><span data-stu-id="5e7e4-206">Helpdesk Admins</span></span>
- <span data-ttu-id="5e7e4-207">Security Administrators</span><span class="sxs-lookup"><span data-stu-id="5e7e4-207">Security Administrators</span></span>
- <span data-ttu-id="5e7e4-208">Security Readers</span><span class="sxs-lookup"><span data-stu-id="5e7e4-208">Security Readers</span></span>
- <span data-ttu-id="5e7e4-209">Intune Service Administrators</span><span class="sxs-lookup"><span data-stu-id="5e7e4-209">Intune Service Administrators</span></span>

> [!NOTE]
> <span data-ttu-id="5e7e4-210">Hybrid Azure AD Joined Windows 10 devices do not have an owner.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-210">Hybrid Azure AD Joined Windows 10 devices do not have an owner.</span></span> <span data-ttu-id="5e7e4-211">So, if you are looking for a device by owner and didn't find it, search by the device ID.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-211">So, if you are looking for a device by owner and didn't find it, search by the device ID.</span></span>


## <a name="audit-logs"></a><span data-ttu-id="5e7e4-212">Audit logs</span><span class="sxs-lookup"><span data-stu-id="5e7e4-212">Audit logs</span></span>


<span data-ttu-id="5e7e4-213">Device activities are available through the activity logs.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-213">Device activities are available through the activity logs.</span></span> <span data-ttu-id="5e7e4-214">This includes activities triggered by the device registration service and by users:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-214">This includes activities triggered by the device registration service and by users:</span></span>

- <span data-ttu-id="5e7e4-215">Device creation and adding owners / users on the device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-215">Device creation and adding owners / users on the device</span></span>

- <span data-ttu-id="5e7e4-216">Changes to device settings</span><span class="sxs-lookup"><span data-stu-id="5e7e4-216">Changes to device settings</span></span>

- <span data-ttu-id="5e7e4-217">Device operations such as deleting or updating a device</span><span class="sxs-lookup"><span data-stu-id="5e7e4-217">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="5e7e4-218">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices** page.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-218">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices** page.</span></span>

![Audit logs](./media/device-management-azure-portal/61.png)


<span data-ttu-id="5e7e4-220">An audit log has a default list view that shows:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-220">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="5e7e4-221">The date and time of the occurrence</span><span class="sxs-lookup"><span data-stu-id="5e7e4-221">The date and time of the occurrence</span></span>

- <span data-ttu-id="5e7e4-222">The targets</span><span class="sxs-lookup"><span data-stu-id="5e7e4-222">The targets</span></span>

- <span data-ttu-id="5e7e4-223">The initiator / actor (who) of an activity</span><span class="sxs-lookup"><span data-stu-id="5e7e4-223">The initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="5e7e4-224">The activity (what)</span><span class="sxs-lookup"><span data-stu-id="5e7e4-224">The activity (what)</span></span>

![Audit logs](./media/device-management-azure-portal/63.png)

<span data-ttu-id="5e7e4-226">You can customize the list view by clicking **Columns** in the toolbar.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-226">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Audit logs](./media/device-management-azure-portal/64.png)


<span data-ttu-id="5e7e4-228">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span><span class="sxs-lookup"><span data-stu-id="5e7e4-228">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="5e7e4-229">Category</span><span class="sxs-lookup"><span data-stu-id="5e7e4-229">Category</span></span>
- <span data-ttu-id="5e7e4-230">Activity resource type</span><span class="sxs-lookup"><span data-stu-id="5e7e4-230">Activity resource type</span></span>
- <span data-ttu-id="5e7e4-231">Activity</span><span class="sxs-lookup"><span data-stu-id="5e7e4-231">Activity</span></span>
- <span data-ttu-id="5e7e4-232">Date range</span><span class="sxs-lookup"><span data-stu-id="5e7e4-232">Date range</span></span>
- <span data-ttu-id="5e7e4-233">Target</span><span class="sxs-lookup"><span data-stu-id="5e7e4-233">Target</span></span>
- <span data-ttu-id="5e7e4-234">Initiated By (Actor)</span><span class="sxs-lookup"><span data-stu-id="5e7e4-234">Initiated By (Actor)</span></span>

<span data-ttu-id="5e7e4-235">In addition to the filters, you can search for specific entries.</span><span class="sxs-lookup"><span data-stu-id="5e7e4-235">In addition to the filters, you can search for specific entries.</span></span>

![Audit logs](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="5e7e4-237">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e7e4-237">Next steps</span></span>

* [<span data-ttu-id="5e7e4-238">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e7e4-238">Introduction to device management in Azure Active Directory</span></span>](overview.md)



