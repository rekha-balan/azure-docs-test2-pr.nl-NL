---
title: How to configure automatic registration of Windows domain-joined devices with Azure Active Directory | Microsoft Docs
description: Set up your domain-joined Windows devices to register automatically and silently with Azure Active Directory.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/09/2017
ms.author: markvi
ms.openlocfilehash: 9934902811354ffa4047d70d995a6dd44be0229b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554256"
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="4aafe-103">Get started with Azure Active Directory device registration</span><span class="sxs-lookup"><span data-stu-id="4aafe-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="4aafe-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span><span class="sxs-lookup"><span data-stu-id="4aafe-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="4aafe-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span><span class="sxs-lookup"><span data-stu-id="4aafe-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="4aafe-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span><span class="sxs-lookup"><span data-stu-id="4aafe-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="4aafe-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span><span class="sxs-lookup"><span data-stu-id="4aafe-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="4aafe-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span><span class="sxs-lookup"><span data-stu-id="4aafe-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="4aafe-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span><span class="sxs-lookup"><span data-stu-id="4aafe-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="4aafe-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="4aafe-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span><span class="sxs-lookup"><span data-stu-id="4aafe-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="4aafe-112">These scenarios are as follows:</span><span class="sxs-lookup"><span data-stu-id="4aafe-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="4aafe-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span><span class="sxs-lookup"><span data-stu-id="4aafe-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="4aafe-114">For more information, see Conditional Access Device Policies for Office 365 services.</span><span class="sxs-lookup"><span data-stu-id="4aafe-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="4aafe-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="4aafe-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="4aafe-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4aafe-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="4aafe-117">Setting up Azure Active Directory Device Registration</span><span class="sxs-lookup"><span data-stu-id="4aafe-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="4aafe-118">To setup device registration, you have multiple options:</span><span class="sxs-lookup"><span data-stu-id="4aafe-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="4aafe-119">Devices can register when joined to Azure AD domain.</span><span class="sxs-lookup"><span data-stu-id="4aafe-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="4aafe-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span><span class="sxs-lookup"><span data-stu-id="4aafe-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="4aafe-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span><span class="sxs-lookup"><span data-stu-id="4aafe-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="4aafe-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4aafe-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="4aafe-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span><span class="sxs-lookup"><span data-stu-id="4aafe-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="4aafe-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span><span class="sxs-lookup"><span data-stu-id="4aafe-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="4aafe-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4aafe-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="4aafe-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4aafe-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="4aafe-127">Enable the Azure Active Directory device registration service</span><span class="sxs-lookup"><span data-stu-id="4aafe-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="4aafe-128">**To enable the Azure Active Directory device registration service:**</span><span class="sxs-lookup"><span data-stu-id="4aafe-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="4aafe-129">Sign in to the Microsoft Azure portal as administrator.</span><span class="sxs-lookup"><span data-stu-id="4aafe-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="4aafe-130">On the left pane, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="4aafe-131">On the Directory tab, select your directory.</span><span class="sxs-lookup"><span data-stu-id="4aafe-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="4aafe-132">Click **Configure**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="4aafe-133">Scroll to **Devices**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="4aafe-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span><span class="sxs-lookup"><span data-stu-id="4aafe-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="4aafe-135">Select the maximum number of devices you want to authorize per user.</span><span class="sxs-lookup"><span data-stu-id="4aafe-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="4aafe-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span><span class="sxs-lookup"><span data-stu-id="4aafe-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="4aafe-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span><span class="sxs-lookup"><span data-stu-id="4aafe-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="4aafe-138">Please ensure that they are configured correctly and have the appropriate licensing.</span><span class="sxs-lookup"><span data-stu-id="4aafe-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="4aafe-139">By default, two-factor authentication is not enabled for the service.</span><span class="sxs-lookup"><span data-stu-id="4aafe-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="4aafe-140">However, two-factor authentication is recommended when registering a device.</span><span class="sxs-lookup"><span data-stu-id="4aafe-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="4aafe-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4aafe-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="4aafe-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="4aafe-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="4aafe-143">View and manage device objects in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4aafe-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="4aafe-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="4aafe-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="4aafe-146">**To view and manage device objects in Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="4aafe-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="4aafe-147">Log on to the Microsoft Azure portal as administrator.</span><span class="sxs-lookup"><span data-stu-id="4aafe-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="4aafe-148">On the left pane, select **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="4aafe-149">Select your directory.</span><span class="sxs-lookup"><span data-stu-id="4aafe-149">Select your directory.</span></span>

4.  <span data-ttu-id="4aafe-150">Select **Users**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="4aafe-151">Click the user for which you want to see the devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="4aafe-152">Select **Devices**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="4aafe-153">Select **Registered Devices**.</span><span class="sxs-lookup"><span data-stu-id="4aafe-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="4aafe-154">Now, you can review, block, or unblock the user's registered devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="4aafe-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab. Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span><span class="sxs-lookup"><span data-stu-id="4aafe-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab. Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="4aafe-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="4aafe-156">Next steps</span></span>

<span data-ttu-id="4aafe-157">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="4aafe-157">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


