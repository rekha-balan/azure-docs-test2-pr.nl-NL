---
title: What is device management in Azure Active Directory? | Microsoft Docs
description: Learn how device management can help you to get control over the devices that are accessing resources in your environment.
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
ms.topic: overview
ms.date: 08/25/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3e96d709c71eb3a04956e933c94840f712abecd2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969182"
---
# <a name="what-is-device-management-in-azure-active-directory"></a><span data-ttu-id="a6988-104">What is device management in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6988-104">What is device management in Azure Active Directory?</span></span>

<span data-ttu-id="a6988-105">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span><span class="sxs-lookup"><span data-stu-id="a6988-105">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="a6988-106">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span><span class="sxs-lookup"><span data-stu-id="a6988-106">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="a6988-107">Empower the end users to be productive wherever and whenever</span><span class="sxs-lookup"><span data-stu-id="a6988-107">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="a6988-108">Protect the corporate assets at any time</span><span class="sxs-lookup"><span data-stu-id="a6988-108">Protect the corporate assets at any time</span></span>

<span data-ttu-id="a6988-109">Through devices, your users are getting access to your corporate assets.</span><span class="sxs-lookup"><span data-stu-id="a6988-109">Through devices, your users are getting access to your corporate assets.</span></span> <span data-ttu-id="a6988-110">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-110">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span></span> <span data-ttu-id="a6988-111">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="a6988-111">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="a6988-112">Device management is also the foundation for [device-based conditional access](../conditional-access/require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a6988-112">Device management is also the foundation for [device-based conditional access](../conditional-access/require-managed-devices.md).</span></span> <span data-ttu-id="a6988-113">With device-based conditional access, you can ensure that access to resources in your environment is only possible with managed devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-113">With device-based conditional access, you can ensure that access to resources in your environment is only possible with managed devices.</span></span>   

<span data-ttu-id="a6988-114">This article explains how device management in Azure Active Directory works.</span><span class="sxs-lookup"><span data-stu-id="a6988-114">This article explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-the-control-of-azure-ad"></a><span data-ttu-id="a6988-115">Getting devices under the control of Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6988-115">Getting devices under the control of Azure AD</span></span>

<span data-ttu-id="a6988-116">To get a device under the control of Azure AD, you have two options:</span><span class="sxs-lookup"><span data-stu-id="a6988-116">To get a device under the control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="a6988-117">Registering</span><span class="sxs-lookup"><span data-stu-id="a6988-117">Registering</span></span> 
- <span data-ttu-id="a6988-118">Joining</span><span class="sxs-lookup"><span data-stu-id="a6988-118">Joining</span></span>

<span data-ttu-id="a6988-119">**Registering** a device to Azure AD enables you to manage a device’s identity.</span><span class="sxs-lookup"><span data-stu-id="a6988-119">**Registering** a device to Azure AD enables you to manage a device’s identity.</span></span> <span data-ttu-id="a6988-120">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6988-120">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span></span> <span data-ttu-id="a6988-121">You can use the identity to enable or disable a device.</span><span class="sxs-lookup"><span data-stu-id="a6988-121">You can use the identity to enable or disable a device.</span></span>

<span data-ttu-id="a6988-122">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span><span class="sxs-lookup"><span data-stu-id="a6988-122">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span></span> <span data-ttu-id="a6988-123">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="a6988-123">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="a6988-124">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span><span class="sxs-lookup"><span data-stu-id="a6988-124">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="a6988-125">**Joining** a device is an extension to registering a device.</span><span class="sxs-lookup"><span data-stu-id="a6988-125">**Joining** a device is an extension to registering a device.</span></span> <span data-ttu-id="a6988-126">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span><span class="sxs-lookup"><span data-stu-id="a6988-126">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span></span> <span data-ttu-id="a6988-127">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span><span class="sxs-lookup"><span data-stu-id="a6988-127">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="a6988-128">Azure AD registered devices</span><span class="sxs-lookup"><span data-stu-id="a6988-128">Azure AD registered devices</span></span>   

<span data-ttu-id="a6988-129">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span><span class="sxs-lookup"><span data-stu-id="a6988-129">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="a6988-130">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span><span class="sxs-lookup"><span data-stu-id="a6988-130">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Azure AD registered devices](./media/overview/03.png)

<span data-ttu-id="a6988-132">The access is based on a work or school account that has been entered on the device.</span><span class="sxs-lookup"><span data-stu-id="a6988-132">The access is based on a work or school account that has been entered on the device.</span></span>  
<span data-ttu-id="a6988-133">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span><span class="sxs-lookup"><span data-stu-id="a6988-133">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="a6988-134">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span><span class="sxs-lookup"><span data-stu-id="a6988-134">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="a6988-135">Your organization’s users can add a work or school account to a personal device conveniently:</span><span class="sxs-lookup"><span data-stu-id="a6988-135">Your organization’s users can add a work or school account to a personal device conveniently:</span></span>

- <span data-ttu-id="a6988-136">When accessing a work application for the first time</span><span class="sxs-lookup"><span data-stu-id="a6988-136">When accessing a work application for the first time</span></span>
- <span data-ttu-id="a6988-137">Manually via the **Settings** menu in the case of Windows 10</span><span class="sxs-lookup"><span data-stu-id="a6988-137">Manually via the **Settings** menu in the case of Windows 10</span></span> 

<span data-ttu-id="a6988-138">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span><span class="sxs-lookup"><span data-stu-id="a6988-138">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="a6988-139">Azure AD joined devices</span><span class="sxs-lookup"><span data-stu-id="a6988-139">Azure AD joined devices</span></span>

<span data-ttu-id="a6988-140">The goal of Azure AD joined devices is to simplify:</span><span class="sxs-lookup"><span data-stu-id="a6988-140">The goal of Azure AD joined devices is to simplify:</span></span>

- <span data-ttu-id="a6988-141">Windows deployments of work-owned devices</span><span class="sxs-lookup"><span data-stu-id="a6988-141">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="a6988-142">Access to organizational apps and resources from any Windows device</span><span class="sxs-lookup"><span data-stu-id="a6988-142">Access to organizational apps and resources from any Windows device</span></span>
- <span data-ttu-id="a6988-143">Cloud-based management of work-owned devices</span><span class="sxs-lookup"><span data-stu-id="a6988-143">Cloud-based management of work-owned devices</span></span>

![Azure AD registered devices](./media/overview/02.png)

<span data-ttu-id="a6988-145">Azure AD Join can be deployed by using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="a6988-145">Azure AD Join can be deployed by using any of the following methods:</span></span> 
 - [<span data-ttu-id="a6988-146">Windows Autopilot</span><span class="sxs-lookup"><span data-stu-id="a6988-146">Windows Autopilot</span></span>](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot)
 - [<span data-ttu-id="a6988-147">Bulk deployment</span><span class="sxs-lookup"><span data-stu-id="a6988-147">Bulk deployment</span></span>](https://docs.microsoft.com/intune/windows-bulk-enroll)
 - [<span data-ttu-id="a6988-148">Self-service experience</span><span class="sxs-lookup"><span data-stu-id="a6988-148">Self-service experience</span></span>](azuread-joined-devices-frx.md) 

<span data-ttu-id="a6988-149">**Azure AD Join** is intended for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure).</span><span class="sxs-lookup"><span data-stu-id="a6988-149">**Azure AD Join** is intended for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure).</span></span> <span data-ttu-id="a6988-150">There are no restrictions on the size or type of organizations that can deploy Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="a6988-150">There are no restrictions on the size or type of organizations that can deploy Azure AD Join.</span></span> <span data-ttu-id="a6988-151">Azure AD Join works well even in a hybrid environment, enabling access to both cloud and on-premises apps and resources.</span><span class="sxs-lookup"><span data-stu-id="a6988-151">Azure AD Join works well even in a hybrid environment, enabling access to both cloud and on-premises apps and resources.</span></span>

<span data-ttu-id="a6988-152">Implementing Azure AD joined devices provides you with the following benefits:</span><span class="sxs-lookup"><span data-stu-id="a6988-152">Implementing Azure AD joined devices provides you with the following benefits:</span></span>

- <span data-ttu-id="a6988-153">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span><span class="sxs-lookup"><span data-stu-id="a6988-153">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span></span> <span data-ttu-id="a6988-154">Your users don’t see additional authentication prompts when accessing work resources.</span><span class="sxs-lookup"><span data-stu-id="a6988-154">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="a6988-155">The SSO functionality is even when they are not connected to the domain network available.</span><span class="sxs-lookup"><span data-stu-id="a6988-155">The SSO functionality is even when they are not connected to the domain network available.</span></span>

- <span data-ttu-id="a6988-156">**Enterprise compliant roaming** of user settings across joined devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-156">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="a6988-157">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-157">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span></span>

- <span data-ttu-id="a6988-158">**Access to Windows Store for Business** using an Azure AD account.</span><span class="sxs-lookup"><span data-stu-id="a6988-158">**Access to Windows Store for Business** using an Azure AD account.</span></span> <span data-ttu-id="a6988-159">Your users can choose from an inventory of applications pre-selected by the organization.</span><span class="sxs-lookup"><span data-stu-id="a6988-159">Your users can choose from an inventory of applications pre-selected by the organization.</span></span>

- <span data-ttu-id="a6988-160">**Windows Hello** support for secure and convenient access to work resources.</span><span class="sxs-lookup"><span data-stu-id="a6988-160">**Windows Hello** support for secure and convenient access to work resources.</span></span>

- <span data-ttu-id="a6988-161">**Restriction of access** to apps from only devices that meet compliance policy.</span><span class="sxs-lookup"><span data-stu-id="a6988-161">**Restriction of access** to apps from only devices that meet compliance policy.</span></span>

- <span data-ttu-id="a6988-162">**Seamless access to on-premises resources** when the device has line of sight to the on-premises domain controller.</span><span class="sxs-lookup"><span data-stu-id="a6988-162">**Seamless access to on-premises resources** when the device has line of sight to the on-premises domain controller.</span></span> 


<span data-ttu-id="a6988-163">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly use it in scenarios where:</span><span class="sxs-lookup"><span data-stu-id="a6988-163">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly use it in scenarios where:</span></span>

- <span data-ttu-id="a6988-164">You want to transition to cloud-based infrastructure using Azure AD and MDM like Intune.</span><span class="sxs-lookup"><span data-stu-id="a6988-164">You want to transition to cloud-based infrastructure using Azure AD and MDM like Intune.</span></span>

- <span data-ttu-id="a6988-165">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span><span class="sxs-lookup"><span data-stu-id="a6988-165">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="a6988-166">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a6988-166">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="a6988-167">You want to manage a group of users in Azure AD instead of in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6988-167">You want to manage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="a6988-168">This can apply, for example, to seasonal workers, contractors, or students.</span><span class="sxs-lookup"><span data-stu-id="a6988-168">This can apply, for example, to seasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="a6988-169">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="a6988-169">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="a6988-170">You can configure Azure AD joined devices for Windows 10 devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-170">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="a6988-171">Hybrid Azure AD joined devices</span><span class="sxs-lookup"><span data-stu-id="a6988-171">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="a6988-172">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span><span class="sxs-lookup"><span data-stu-id="a6988-172">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span></span>

- <span data-ttu-id="a6988-173">IT departments to manage work-owned devices from a central location.</span><span class="sxs-lookup"><span data-stu-id="a6988-173">IT departments to manage work-owned devices from a central location.</span></span>

- <span data-ttu-id="a6988-174">Users to sign in to their devices with their Active Directory work or school accounts.</span><span class="sxs-lookup"><span data-stu-id="a6988-174">Users to sign in to their devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="a6988-175">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span><span class="sxs-lookup"><span data-stu-id="a6988-175">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span></span>

<span data-ttu-id="a6988-176">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-176">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="a6988-177">These are devices that are joined to your on-premises Active Directory and registered with your Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6988-177">These are devices that are joined to your on-premises Active Directory and registered with your Azure Active Directory.</span></span>

![Azure AD registered devices](./media/overview/01.png)


<span data-ttu-id="a6988-179">You should use Azure AD hybrid joined devices if:</span><span class="sxs-lookup"><span data-stu-id="a6988-179">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="a6988-180">You have Win32 apps deployed to these devices that rely on Active Directory machine authentication.</span><span class="sxs-lookup"><span data-stu-id="a6988-180">You have Win32 apps deployed to these devices that rely on Active Directory machine authentication.</span></span>

- <span data-ttu-id="a6988-181">You require GP to manage devices.</span><span class="sxs-lookup"><span data-stu-id="a6988-181">You require GP to manage devices.</span></span>

- <span data-ttu-id="a6988-182">You want to continue to use imaging solutions to configure devices for your employees.</span><span class="sxs-lookup"><span data-stu-id="a6988-182">You want to continue to use imaging solutions to configure devices for your employees.</span></span>

<span data-ttu-id="a6988-183">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span><span class="sxs-lookup"><span data-stu-id="a6988-183">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="a6988-184">Summary</span><span class="sxs-lookup"><span data-stu-id="a6988-184">Summary</span></span>

<span data-ttu-id="a6988-185">With device management in Azure AD, you can:</span><span class="sxs-lookup"><span data-stu-id="a6988-185">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="a6988-186">Simplify the process of bringing devices under the control of Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6988-186">Simplify the process of bringing devices under the control of Azure AD</span></span>

- <span data-ttu-id="a6988-187">Provide your users with an easy to use access to your organization’s cloud-based resources</span><span class="sxs-lookup"><span data-stu-id="a6988-187">Provide your users with an easy to use access to your organization’s cloud-based resources</span></span>

<span data-ttu-id="a6988-188">As a rule of a thumb, you should use:</span><span class="sxs-lookup"><span data-stu-id="a6988-188">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="a6988-189">Azure AD registered devices:</span><span class="sxs-lookup"><span data-stu-id="a6988-189">Azure AD registered devices:</span></span>

    - <span data-ttu-id="a6988-190">For personal devices</span><span class="sxs-lookup"><span data-stu-id="a6988-190">For personal devices</span></span> 

    - <span data-ttu-id="a6988-191">To manually register devices with Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6988-191">To manually register devices with Azure AD</span></span>

- <span data-ttu-id="a6988-192">Azure AD joined devices:</span><span class="sxs-lookup"><span data-stu-id="a6988-192">Azure AD joined devices:</span></span> 

    - <span data-ttu-id="a6988-193">For devices that are owned by your organization</span><span class="sxs-lookup"><span data-stu-id="a6988-193">For devices that are owned by your organization</span></span>

    - <span data-ttu-id="a6988-194">For devices that are **not** joined to an on-premises AD</span><span class="sxs-lookup"><span data-stu-id="a6988-194">For devices that are **not** joined to an on-premises AD</span></span>

    - <span data-ttu-id="a6988-195">To manually register devices with Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6988-195">To manually register devices with Azure AD</span></span>

    - <span data-ttu-id="a6988-196">To change the local state of a device</span><span class="sxs-lookup"><span data-stu-id="a6988-196">To change the local state of a device</span></span>

- <span data-ttu-id="a6988-197">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span><span class="sxs-lookup"><span data-stu-id="a6988-197">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span></span>     

    - <span data-ttu-id="a6988-198">For devices that are owned by your organization</span><span class="sxs-lookup"><span data-stu-id="a6988-198">For devices that are owned by your organization</span></span>

    - <span data-ttu-id="a6988-199">For devices that are joined to an on-premises AD</span><span class="sxs-lookup"><span data-stu-id="a6988-199">For devices that are joined to an on-premises AD</span></span>

    - <span data-ttu-id="a6988-200">To automatically register devices with Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6988-200">To automatically register devices with Azure AD</span></span>

    - <span data-ttu-id="a6988-201">To change the local state of a device</span><span class="sxs-lookup"><span data-stu-id="a6988-201">To change the local state of a device</span></span>



## <a name="next-steps"></a><span data-ttu-id="a6988-202">Next steps</span><span class="sxs-lookup"><span data-stu-id="a6988-202">Next steps</span></span>

- <span data-ttu-id="a6988-203">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a6988-203">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="a6988-204">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](../conditional-access/require-managed-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a6988-204">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](../conditional-access/require-managed-devices.md).</span></span>

- <span data-ttu-id="a6988-205">To setup:</span><span class="sxs-lookup"><span data-stu-id="a6988-205">To setup:</span></span>
    - <span data-ttu-id="a6988-206">Azure Active Directory registered Windows 10 devices, see [how to configure Azure Active Directory registered Windows 10 devices](../user-help/device-management-azuread-registered-devices-windows10-setup.md)</span><span class="sxs-lookup"><span data-stu-id="a6988-206">Azure Active Directory registered Windows 10 devices, see [how to configure Azure Active Directory registered Windows 10 devices](../user-help/device-management-azuread-registered-devices-windows10-setup.md)</span></span>
    - <span data-ttu-id="a6988-207">Azure Active Directory joined devices, see [how to configure Azure Active Directory joined devices](../user-help/device-management-azuread-joined-devices-setup.md)</span><span class="sxs-lookup"><span data-stu-id="a6988-207">Azure Active Directory joined devices, see [how to configure Azure Active Directory joined devices](../user-help/device-management-azuread-joined-devices-setup.md)</span></span>
    - <span data-ttu-id="a6988-208">Hybrid Azure AD joined devices, see [How to plan your hybrid Azure Active Directory join implementation](hybrid-azuread-join-plan.md).</span><span class="sxs-lookup"><span data-stu-id="a6988-208">Hybrid Azure AD joined devices, see [How to plan your hybrid Azure Active Directory join implementation](hybrid-azuread-join-plan.md).</span></span>


