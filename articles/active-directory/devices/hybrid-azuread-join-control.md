---
title: How to configure hybrid Azure Active Directory joined devices | Microsoft Docs
description: Learn how to configure hybrid Azure Active Directory joined devices.
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
ms.date: 07/31/2018
ms.author: markvi
ms.reviewer: sandeo
ms.openlocfilehash: d49b5404f1a2b4ac7fa4cc170ccc010a28bf98a2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867207"
---
# <a name="how-to-control-the-hybrid-azure-ad-join-of-your-devices"></a><span data-ttu-id="c5e2e-103">How to control the hybrid Azure AD join of your devices</span><span class="sxs-lookup"><span data-stu-id="c5e2e-103">How to control the hybrid Azure AD join of your devices</span></span>

<span data-ttu-id="c5e2e-104">Hybrid Azure AD join is a process to automatically register your on-premises domain-joined devices with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-104">Hybrid Azure AD join is a process to automatically register your on-premises domain-joined devices with Azure AD.</span></span> <span data-ttu-id="c5e2e-105">There are cases where you don't want all your devices to register automatically.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-105">There are cases where you don't want all your devices to register automatically.</span></span> <span data-ttu-id="c5e2e-106">This is for example true, during the initial rollout to verify that everything works as expected.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-106">This is for example true, during the initial rollout to verify that everything works as expected.</span></span>

<span data-ttu-id="c5e2e-107">This article provides you with guidance on how you can control hybrid Azure AD join of your devices.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-107">This article provides you with guidance on how you can control hybrid Azure AD join of your devices.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="c5e2e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c5e2e-108">Prerequisites</span></span>

<span data-ttu-id="c5e2e-109">This article assumes that you are familiar with:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-109">This article assumes that you are familiar with:</span></span>

-  [<span data-ttu-id="c5e2e-110">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5e2e-110">Introduction to device management in Azure Active Directory</span></span>](../device-management-introduction.md)
 
-  [<span data-ttu-id="c5e2e-111">How to plan your hybrid Azure Active Directory join implementation</span><span class="sxs-lookup"><span data-stu-id="c5e2e-111">How to plan your hybrid Azure Active Directory join implementation</span></span>](hybrid-azuread-join-plan.md)

-  <span data-ttu-id="c5e2e-112">Configure hybrid Azure Active Directory join for [managed domains](hybrid-azuread-join-managed-domains.md) or [federated domains](hybrid-azuread-join-federated-domains.md)</span><span class="sxs-lookup"><span data-stu-id="c5e2e-112">Configure hybrid Azure Active Directory join for [managed domains](hybrid-azuread-join-managed-domains.md) or [federated domains](hybrid-azuread-join-federated-domains.md)</span></span>



## <a name="control-windows-current-devices"></a><span data-ttu-id="c5e2e-113">Control Windows current devices</span><span class="sxs-lookup"><span data-stu-id="c5e2e-113">Control Windows current devices</span></span>

<span data-ttu-id="c5e2e-114">For devices running the Windows desktop operating system, the supported version is the Windows 10 Anniversary Update (version 1607) or later.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-114">For devices running the Windows desktop operating system, the supported version is the Windows 10 Anniversary Update (version 1607) or later.</span></span> <span data-ttu-id="c5e2e-115">As a best practice, upgrade to the latest version of Windows 10.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-115">As a best practice, upgrade to the latest version of Windows 10.</span></span>

<span data-ttu-id="c5e2e-116">All windows current devices automatically register with Azure AD at device start or user sign-in.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-116">All windows current devices automatically register with Azure AD at device start or user sign-in.</span></span> <span data-ttu-id="c5e2e-117">You can control this behavior either with a group policy object (GPO) or System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-117">You can control this behavior either with a group policy object (GPO) or System Center Configuration Manager.</span></span>

<span data-ttu-id="c5e2e-118">To control Windows current devices, you need to:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-118">To control Windows current devices, you need to:</span></span> 

1.  <span data-ttu-id="c5e2e-119">**To all devices**: Disable automatic device registration.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-119">**To all devices**: Disable automatic device registration.</span></span>
2.  <span data-ttu-id="c5e2e-120">**To selected devices**: Enable automatic device registration.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-120">**To selected devices**: Enable automatic device registration.</span></span>

<span data-ttu-id="c5e2e-121">If you have verified that everything works as expected, you are ready to enable automatic device registration for all devices again.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-121">If you have verified that everything works as expected, you are ready to enable automatic device registration for all devices again.</span></span>



## <a name="group-policy-object"></a><span data-ttu-id="c5e2e-122">Group Policy Object</span><span class="sxs-lookup"><span data-stu-id="c5e2e-122">Group Policy Object</span></span> 

<span data-ttu-id="c5e2e-123">You can control the device registration behavior of your devices by deploying the following GPO: **Register domain-joined computers as devices**</span><span class="sxs-lookup"><span data-stu-id="c5e2e-123">You can control the device registration behavior of your devices by deploying the following GPO: **Register domain-joined computers as devices**</span></span>

<span data-ttu-id="c5e2e-124">**To set the GPO**:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-124">**To set the GPO**:</span></span>

1.  <span data-ttu-id="c5e2e-125">Open **Server Manager**, and then go to **Tools \> Group Policy Management**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-125">Open **Server Manager**, and then go to **Tools \> Group Policy Management**.</span></span>

2.  <span data-ttu-id="c5e2e-126">Go to the domain node that corresponds to the domain where you want to disable/enable the auto-registration.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-126">Go to the domain node that corresponds to the domain where you want to disable/enable the auto-registration.</span></span>

3.  <span data-ttu-id="c5e2e-127">Right-click **Group Policy Objects**, and then select **New**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-127">Right-click **Group Policy Objects**, and then select **New**.</span></span>

4.  <span data-ttu-id="c5e2e-128">Type a name (for example, *Hybrid Azure AD join*) for your Group Policy object.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-128">Type a name (for example, *Hybrid Azure AD join*) for your Group Policy object.</span></span> 

5.  <span data-ttu-id="c5e2e-129">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-129">Click **OK**.</span></span>

6.  <span data-ttu-id="c5e2e-130">Right-click your new GPO, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-130">Right-click your new GPO, and then select **Edit**.</span></span>

7.  <span data-ttu-id="c5e2e-131">Go to **Computer Configuration \> Policies \> Administrative Templates \> Windows Components \> Device Registration**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-131">Go to **Computer Configuration \> Policies \> Administrative Templates \> Windows Components \> Device Registration**.</span></span> 

8.  <span data-ttu-id="c5e2e-132">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-132">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c5e2e-133">This group policy template has been renamed from earlier versions of the Group Policy Management console.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-133">This group policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="c5e2e-134">If you are using an earlier version of the console, go to **Computer Configuration \> Policies \> Administrative Templates \> Windows Components \> Workplace Join \> Automatically workplace join client computers**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-134">If you are using an earlier version of the console, go to **Computer Configuration \> Policies \> Administrative Templates \> Windows Components \> Workplace Join \> Automatically workplace join client computers**.</span></span> 

9.  <span data-ttu-id="c5e2e-135">Select one of the following settings, and then click **Apply**:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-135">Select one of the following settings, and then click **Apply**:</span></span>

    - <span data-ttu-id="c5e2e-136">**Disabled** - To prevent the automatic device registration</span><span class="sxs-lookup"><span data-stu-id="c5e2e-136">**Disabled** - To prevent the automatic device registration</span></span>
    - <span data-ttu-id="c5e2e-137">**Enabled** - To enable the automatic device registration</span><span class="sxs-lookup"><span data-stu-id="c5e2e-137">**Enabled** - To enable the automatic device registration</span></span>

10. <span data-ttu-id="c5e2e-138">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-138">Click **OK**.</span></span>

<span data-ttu-id="c5e2e-139">You need to link the GPO to a location of your choice.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-139">You need to link the GPO to a location of your choice.</span></span> <span data-ttu-id="c5e2e-140">For example, to set this policy for all domain-joined current devices in your organization, link the GPO to the domain.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-140">For example, to set this policy for all domain-joined current devices in your organization, link the GPO to the domain.</span></span> <span data-ttu-id="c5e2e-141">To do a controlled deployment, set this policy to domain-joined Windows current devices that belong to an organizational unit or a security group.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-141">To do a controlled deployment, set this policy to domain-joined Windows current devices that belong to an organizational unit or a security group.</span></span>

### <a name="configuration-manager-controlled-deployment"></a><span data-ttu-id="c5e2e-142">Configuration Manager controlled deployment</span><span class="sxs-lookup"><span data-stu-id="c5e2e-142">Configuration Manager controlled deployment</span></span> 

<span data-ttu-id="c5e2e-143">You can control the device registration behavior of your current devices by configuring the following client setting: \*\*Automatically register new Windows 10 domain joined devices with azure Active Directory \*\*</span><span class="sxs-lookup"><span data-stu-id="c5e2e-143">You can control the device registration behavior of your current devices by configuring the following client setting: \*\*Automatically register new Windows 10 domain joined devices with azure Active Directory \*\*</span></span>


<span data-ttu-id="c5e2e-144">**To set the client setting**:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-144">**To set the client setting**:</span></span>

1.  <span data-ttu-id="c5e2e-145">Open **Configuration Manager**, and then go to **Cloud Services**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-145">Open **Configuration Manager**, and then go to **Cloud Services**.</span></span>

2.  <span data-ttu-id="c5e2e-146">Under **Device Settings**, select one of the following settings for **Automatically register new Windows 10 domain joined devices with azure Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="c5e2e-146">Under **Device Settings**, select one of the following settings for **Automatically register new Windows 10 domain joined devices with azure Active Directory**:</span></span>

    - <span data-ttu-id="c5e2e-147">**No** - To prevent the automatic device registration</span><span class="sxs-lookup"><span data-stu-id="c5e2e-147">**No** - To prevent the automatic device registration</span></span>
    - <span data-ttu-id="c5e2e-148">**Yes** - To enable the automatic device registration</span><span class="sxs-lookup"><span data-stu-id="c5e2e-148">**Yes** - To enable the automatic device registration</span></span>


3.  <span data-ttu-id="c5e2e-149">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-149">Click **OK**.</span></span>
    

<span data-ttu-id="c5e2e-150">You need to link this client setting to a location of your choice.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-150">You need to link this client setting to a location of your choice.</span></span> <span data-ttu-id="c5e2e-151">For example, to configure this client setting for all Windows current devices in your organization, link the client setting to the domain.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-151">For example, to configure this client setting for all Windows current devices in your organization, link the client setting to the domain.</span></span> <span data-ttu-id="c5e2e-152">To do a controlled deployment, you can configure the client setting to domain-joined Windows current devices that belong to an organizational unit or a security group.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-152">To do a controlled deployment, you can configure the client setting to domain-joined Windows current devices that belong to an organizational unit or a security group.</span></span>

> [!Important]
> <span data-ttu-id="c5e2e-153">While the above configuration takes care of existing domain joined Windows 10 devices, there is a potential for newly domain joining devices to still attempt to complete hybrid Azure AD join due to the potential delay in the actual application of group policy or Configuration Manager settings on the newly domain joined Windows 10 device.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-153">While the above configuration takes care of existing domain joined Windows 10 devices, there is a potential for newly domain joining devices to still attempt to complete hybrid Azure AD join due to the potential delay in the actual application of group policy or Configuration Manager settings on the newly domain joined Windows 10 device.</span></span> <span data-ttu-id="c5e2e-154">To avoid this, it is recommended that you create a new sysprep image (used as an example for a provisioning method) from a device that was never previously hybrid Azure AD joined and that already has the above group policy setting applied or Configuration Manager client setting applied.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-154">To avoid this, it is recommended that you create a new sysprep image (used as an example for a provisioning method) from a device that was never previously hybrid Azure AD joined and that already has the above group policy setting applied or Configuration Manager client setting applied.</span></span> <span data-ttu-id="c5e2e-155">You must also use the new image for provisioning new computers that join your organization's domain.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-155">You must also use the new image for provisioning new computers that join your organization's domain.</span></span> 

## <a name="control-windows-down-level-devices"></a><span data-ttu-id="c5e2e-156">Control Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="c5e2e-156">Control Windows down-level devices</span></span>

<span data-ttu-id="c5e2e-157">To register Windows down-level devices, you need to download and install Windows Installer package (.msi) from Download Center on the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/download/details.aspx?id=53554) page.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-157">To register Windows down-level devices, you need to download and install Windows Installer package (.msi) from Download Center on the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="c5e2e-158">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-158">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="c5e2e-159">The package supports the standard silent install options with the quiet parameter.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-159">The package supports the standard silent install options with the quiet parameter.</span></span> <span data-ttu-id="c5e2e-160">[System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-160">[System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager) Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span>

<span data-ttu-id="c5e2e-161">The installer creates a scheduled task on the system that runs in the user’s context.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-161">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="c5e2e-162">The task is triggered when the user signs in to Windows.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-162">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="c5e2e-163">The task silently joins the device with Azure AD with the user credentials after authenticating with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-163">The task silently joins the device with Azure AD with the user credentials after authenticating with Azure AD.</span></span>


<span data-ttu-id="c5e2e-164">To control the device registration, you should deploy the Windows Installer package only to a selected group of Windows down-level devices.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-164">To control the device registration, you should deploy the Windows Installer package only to a selected group of Windows down-level devices.</span></span> <span data-ttu-id="c5e2e-165">If you have verified that everything works as expected, you are ready to rollout the package to all down-level devices.</span><span class="sxs-lookup"><span data-stu-id="c5e2e-165">If you have verified that everything works as expected, you are ready to rollout the package to all down-level devices.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c5e2e-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="c5e2e-166">Next steps</span></span>

* [<span data-ttu-id="c5e2e-167">Introduction to device management in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c5e2e-167">Introduction to device management in Azure Active Directory</span></span>](../device-management-introduction.md)



