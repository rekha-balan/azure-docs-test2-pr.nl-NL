---
title: Set device-based conditional access policy for Azure Active Directory-connected applications | Microsoft Docs
description: Set device-based conditional access policies for Azure AD-connected applications.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
editor: ''
ms.assetid: a27862a6-d513-43ba-97c1-1c0d400bf243
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: markvi
ms.openlocfilehash: 35b467b62231ab79a27330581da992494fa82cfc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555934"
---
# <a name="set-device-based-conditional-access-policy-for-azure-active-directory-connected-applications"></a><span data-ttu-id="4c40b-103">Set device-based conditional access policy for Azure Active Directory-connected applications</span><span class="sxs-lookup"><span data-stu-id="4c40b-103">Set device-based conditional access policy for Azure Active Directory-connected applications</span></span>
<span data-ttu-id="4c40b-104">Azure Active Directory (Azure AD) device-based conditional access can help you protect organization resources from:</span><span class="sxs-lookup"><span data-stu-id="4c40b-104">Azure Active Directory (Azure AD) device-based conditional access can help you protect organization resources from:</span></span>

* <span data-ttu-id="4c40b-105">Access attempts from unknown or unmanaged devices.</span><span class="sxs-lookup"><span data-stu-id="4c40b-105">Access attempts from unknown or unmanaged devices.</span></span>
* <span data-ttu-id="4c40b-106">Devices that don’t meet the security policies of your organization.</span><span class="sxs-lookup"><span data-stu-id="4c40b-106">Devices that don’t meet the security policies of your organization.</span></span>

<span data-ttu-id="4c40b-107">For an overview of conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="4c40b-107">For an overview of conditional access, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span></span>

<span data-ttu-id="4c40b-108">You can set device-based conditional access policies to protect these applications:</span><span class="sxs-lookup"><span data-stu-id="4c40b-108">You can set device-based conditional access policies to protect these applications:</span></span>

* <span data-ttu-id="4c40b-109">Office 365 SharePoint Online, to protect your organization's sites and documents</span><span class="sxs-lookup"><span data-stu-id="4c40b-109">Office 365 SharePoint Online, to protect your organization's sites and documents</span></span>
* <span data-ttu-id="4c40b-110">Office 365 Exchange Online, to protect your organization's email</span><span class="sxs-lookup"><span data-stu-id="4c40b-110">Office 365 Exchange Online, to protect your organization's email</span></span>
* <span data-ttu-id="4c40b-111">Software as a service (SaaS) applications that are connected to Azure AD for authentication</span><span class="sxs-lookup"><span data-stu-id="4c40b-111">Software as a service (SaaS) applications that are connected to Azure AD for authentication</span></span>
* <span data-ttu-id="4c40b-112">On-premises applications that are published by using Azure AD Application Proxy services</span><span class="sxs-lookup"><span data-stu-id="4c40b-112">On-premises applications that are published by using Azure AD Application Proxy services</span></span>

<span data-ttu-id="4c40b-113">To set a device-based conditional access policy, in the Azure portal, go to the specific application in the directory.</span><span class="sxs-lookup"><span data-stu-id="4c40b-113">To set a device-based conditional access policy, in the Azure portal, go to the specific application in the directory.</span></span>

  <span data-ttu-id="4c40b-114">![List of applications in the Azure portal directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/01.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-114">![List of applications in the Azure portal directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/01.png "Applications")</span></span>

<span data-ttu-id="4c40b-115">Select the application, and then click the **Configure** tab to set the conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="4c40b-115">Select the application, and then click the **Configure** tab to set the conditional access policy.</span></span>  

  <span data-ttu-id="4c40b-116">![Configure the application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/02.png "Device based access rules")</span><span class="sxs-lookup"><span data-stu-id="4c40b-116">![Configure the application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/02.png "Device based access rules")</span></span>

<span data-ttu-id="4c40b-117">To set a device-based conditional access policy, in the **Device based access rules** section, in **Enable Access Rules**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-117">To set a device-based conditional access policy, in the **Device based access rules** section, in **Enable Access Rules**, select **On**.</span></span>

<span data-ttu-id="4c40b-118">A device-based conditional access policy has three components:</span><span class="sxs-lookup"><span data-stu-id="4c40b-118">A device-based conditional access policy has three components:</span></span>

* <span data-ttu-id="4c40b-119">**Apply To**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-119">**Apply To**.</span></span> <span data-ttu-id="4c40b-120">The scope of users the policy applies to.</span><span class="sxs-lookup"><span data-stu-id="4c40b-120">The scope of users the policy applies to.</span></span>
* <span data-ttu-id="4c40b-121">**Device Rules**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-121">**Device Rules**.</span></span> <span data-ttu-id="4c40b-122">The conditions a device must meet before it can access the application.</span><span class="sxs-lookup"><span data-stu-id="4c40b-122">The conditions a device must meet before it can access the application.</span></span>
* <span data-ttu-id="4c40b-123">**Application Enforcement**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-123">**Application Enforcement**.</span></span> <span data-ttu-id="4c40b-124">The client applications (native versus browser) the policy applies to.</span><span class="sxs-lookup"><span data-stu-id="4c40b-124">The client applications (native versus browser) the policy applies to.</span></span>
  
  <span data-ttu-id="4c40b-125">![The three components of a device-based access policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/03.png "Device based access rules")</span><span class="sxs-lookup"><span data-stu-id="4c40b-125">![The three components of a device-based access policy](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/03.png "Device based access rules")</span></span>

## <a name="select-the-users-the-policy-applies-to"></a><span data-ttu-id="4c40b-126">Select the users the policy applies to</span><span class="sxs-lookup"><span data-stu-id="4c40b-126">Select the users the policy applies to</span></span>
<span data-ttu-id="4c40b-127">In the **Apply To** section, you can select the scope of users this policy applies to.</span><span class="sxs-lookup"><span data-stu-id="4c40b-127">In the **Apply To** section, you can select the scope of users this policy applies to.</span></span>

<span data-ttu-id="4c40b-128">You have two options when you create an access policy scope for users:</span><span class="sxs-lookup"><span data-stu-id="4c40b-128">You have two options when you create an access policy scope for users:</span></span>

* <span data-ttu-id="4c40b-129">**All Users**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-129">**All Users**.</span></span> <span data-ttu-id="4c40b-130">Apply the policy to all users who access the application.</span><span class="sxs-lookup"><span data-stu-id="4c40b-130">Apply the policy to all users who access the application.</span></span>
* <span data-ttu-id="4c40b-131">**Groups**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-131">**Groups**.</span></span> <span data-ttu-id="4c40b-132">Limit the policy to users who are a member of a specific group.</span><span class="sxs-lookup"><span data-stu-id="4c40b-132">Limit the policy to users who are a member of a specific group.</span></span>

<span data-ttu-id="4c40b-133">![Apply policy to all users or to a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/11.png "Apply to")</span><span class="sxs-lookup"><span data-stu-id="4c40b-133">![Apply policy to all users or to a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/11.png "Apply to")</span></span>

 <span data-ttu-id="4c40b-134">To exclude a user from a policy, select the **Except** check box.</span><span class="sxs-lookup"><span data-stu-id="4c40b-134">To exclude a user from a policy, select the **Except** check box.</span></span> <span data-ttu-id="4c40b-135">This is helpful when you need to give permissions to a specific user to temporarily access the application.</span><span class="sxs-lookup"><span data-stu-id="4c40b-135">This is helpful when you need to give permissions to a specific user to temporarily access the application.</span></span> <span data-ttu-id="4c40b-136">Select this option, for example, if some of your users have devices that are not ready for conditional access.</span><span class="sxs-lookup"><span data-stu-id="4c40b-136">Select this option, for example, if some of your users have devices that are not ready for conditional access.</span></span> <span data-ttu-id="4c40b-137">The devices might not be registered yet, or they are about to be out of compliance.</span><span class="sxs-lookup"><span data-stu-id="4c40b-137">The devices might not be registered yet, or they are about to be out of compliance.</span></span>

## <a name="select-the-conditions-that-devices-must-meet"></a><span data-ttu-id="4c40b-138">Select the conditions that devices must meet</span><span class="sxs-lookup"><span data-stu-id="4c40b-138">Select the conditions that devices must meet</span></span>
<span data-ttu-id="4c40b-139">Use **Device Rules** to set the conditions a device must meet to access the application.</span><span class="sxs-lookup"><span data-stu-id="4c40b-139">Use **Device Rules** to set the conditions a device must meet to access the application.</span></span>

<span data-ttu-id="4c40b-140">You can set device-based conditional access for these device types:</span><span class="sxs-lookup"><span data-stu-id="4c40b-140">You can set device-based conditional access for these device types:</span></span>

* <span data-ttu-id="4c40b-141">Windows 10 Anniversary Update, Windows 8.1, and Windows 7</span><span class="sxs-lookup"><span data-stu-id="4c40b-141">Windows 10 Anniversary Update, Windows 8.1, and Windows 7</span></span>
* <span data-ttu-id="4c40b-142">Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4c40b-142">Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2</span></span>
* <span data-ttu-id="4c40b-143">iOS devices (iPad, iPhone)</span><span class="sxs-lookup"><span data-stu-id="4c40b-143">iOS devices (iPad, iPhone)</span></span>
* <span data-ttu-id="4c40b-144">Android devices</span><span class="sxs-lookup"><span data-stu-id="4c40b-144">Android devices</span></span>

<span data-ttu-id="4c40b-145">Support for Mac is coming soon.</span><span class="sxs-lookup"><span data-stu-id="4c40b-145">Support for Mac is coming soon.</span></span>

  <span data-ttu-id="4c40b-146">![Apply policy to devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/04.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-146">![Apply policy to devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/04.png "Applications")</span></span>

> [!NOTE]
> <span data-ttu-id="4c40b-147">For information about the differences between domain-joined and Azure AD-joined devices, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="4c40b-147">For information about the differences between domain-joined and Azure AD-joined devices, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>
> 
> 

<span data-ttu-id="4c40b-148">You have two options for device rules:</span><span class="sxs-lookup"><span data-stu-id="4c40b-148">You have two options for device rules:</span></span>

* <span data-ttu-id="4c40b-149">**All devices must be compliant**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-149">**All devices must be compliant**.</span></span> <span data-ttu-id="4c40b-150">All device platforms that access the application must be compliant.</span><span class="sxs-lookup"><span data-stu-id="4c40b-150">All device platforms that access the application must be compliant.</span></span> <span data-ttu-id="4c40b-151">Devices that run on platforms that don't support device-based conditional access are denied access.</span><span class="sxs-lookup"><span data-stu-id="4c40b-151">Devices that run on platforms that don't support device-based conditional access are denied access.</span></span>
* <span data-ttu-id="4c40b-152">**Only selected devices must be compliant**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-152">**Only selected devices must be compliant**.</span></span> <span data-ttu-id="4c40b-153">Only specific device platforms must be compliant.</span><span class="sxs-lookup"><span data-stu-id="4c40b-153">Only specific device platforms must be compliant.</span></span> <span data-ttu-id="4c40b-154">Other platforms, or other platforms that can access the application, have access.</span><span class="sxs-lookup"><span data-stu-id="4c40b-154">Other platforms, or other platforms that can access the application, have access.</span></span>
  
  <span data-ttu-id="4c40b-155">![Set the scope for device rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/05.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-155">![Set the scope for device rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/05.png "Applications")</span></span>

<span data-ttu-id="4c40b-156">Azure AD-joined devices are compliant if they are marked as **compliant** in the directory by Intune or by a third-party mobile device management system that integrates with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c40b-156">Azure AD-joined devices are compliant if they are marked as **compliant** in the directory by Intune or by a third-party mobile device management system that integrates with Azure AD.</span></span>

<span data-ttu-id="4c40b-157">A domain-joined device is compliant if:</span><span class="sxs-lookup"><span data-stu-id="4c40b-157">A domain-joined device is compliant if:</span></span>

* <span data-ttu-id="4c40b-158">It is registered with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c40b-158">It is registered with Azure AD.</span></span> <span data-ttu-id="4c40b-159">Many organizations treat domain-joined devices as trusted devices.</span><span class="sxs-lookup"><span data-stu-id="4c40b-159">Many organizations treat domain-joined devices as trusted devices.</span></span>
* <span data-ttu-id="4c40b-160">It is marked as **compliant** in Azure AD by System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="4c40b-160">It is marked as **compliant** in Azure AD by System Center Configuration Manager.</span></span>
  
  <span data-ttu-id="4c40b-161">![Domain-joined devices that are compliant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/06.png "Device Rules")</span><span class="sxs-lookup"><span data-stu-id="4c40b-161">![Domain-joined devices that are compliant](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/06.png "Device Rules")</span></span>

<span data-ttu-id="4c40b-162">Windows personal devices are compliant if they are marked as **compliant** in the directory by Intune or by a third-party mobile device management system that integrates with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c40b-162">Windows personal devices are compliant if they are marked as **compliant** in the directory by Intune or by a third-party mobile device management system that integrates with Azure AD.</span></span>

<span data-ttu-id="4c40b-163">Non-Windows devices are compliant if they are marked as **compliant** in the directory by Intune.</span><span class="sxs-lookup"><span data-stu-id="4c40b-163">Non-Windows devices are compliant if they are marked as **compliant** in the directory by Intune.</span></span>

> [!NOTE]
> <span data-ttu-id="4c40b-164">For more information about how to set up Azure AD for device compliance in different management systems, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="4c40b-164">For more information about how to set up Azure AD for device compliance in different management systems, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span></span>
> 
> 

<span data-ttu-id="4c40b-165">You can select one or multiple device platforms for a device-based access policy.</span><span class="sxs-lookup"><span data-stu-id="4c40b-165">You can select one or multiple device platforms for a device-based access policy.</span></span> <span data-ttu-id="4c40b-166">This includes Android, iOS, Windows Mobile (Windows 8.1 phones and tablets), and Windows (all other Windows devices, including all Windows 10 devices).</span><span class="sxs-lookup"><span data-stu-id="4c40b-166">This includes Android, iOS, Windows Mobile (Windows 8.1 phones and tablets), and Windows (all other Windows devices, including all Windows 10 devices).</span></span>
<span data-ttu-id="4c40b-167">Policy evaluation occurs only on the selected platforms.</span><span class="sxs-lookup"><span data-stu-id="4c40b-167">Policy evaluation occurs only on the selected platforms.</span></span> <span data-ttu-id="4c40b-168">If a device that attempts access is not running one of the selected platforms, the device can access the application if the user has access.</span><span class="sxs-lookup"><span data-stu-id="4c40b-168">If a device that attempts access is not running one of the selected platforms, the device can access the application if the user has access.</span></span> <span data-ttu-id="4c40b-169">No device policy is evaluated.</span><span class="sxs-lookup"><span data-stu-id="4c40b-169">No device policy is evaluated.</span></span>

<span data-ttu-id="4c40b-170">![Select platforms for device rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/07.png "Device Rules")</span><span class="sxs-lookup"><span data-stu-id="4c40b-170">![Select platforms for device rules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/07.png "Device Rules")</span></span>

## <a name="set-policy-evaluation-for-a-type-of-application"></a><span data-ttu-id="4c40b-171">Set policy evaluation for a type of application</span><span class="sxs-lookup"><span data-stu-id="4c40b-171">Set policy evaluation for a type of application</span></span>
<span data-ttu-id="4c40b-172">In the **Application Enforcement** section, set the type of applications the policy will evaluate for user or device access.</span><span class="sxs-lookup"><span data-stu-id="4c40b-172">In the **Application Enforcement** section, set the type of applications the policy will evaluate for user or device access.</span></span>

<span data-ttu-id="4c40b-173">You have two options for the type of application to include:</span><span class="sxs-lookup"><span data-stu-id="4c40b-173">You have two options for the type of application to include:</span></span>

* <span data-ttu-id="4c40b-174">Browser and native applications</span><span class="sxs-lookup"><span data-stu-id="4c40b-174">Browser and native applications</span></span>
* <span data-ttu-id="4c40b-175">Native applications only</span><span class="sxs-lookup"><span data-stu-id="4c40b-175">Native applications only</span></span>

<span data-ttu-id="4c40b-176">![Choose browser or native applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/08.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-176">![Choose browser or native applications](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/08.png "Applications")</span></span>

<span data-ttu-id="4c40b-177">To enforce access policy for applications, select **For browser and native applications**.</span><span class="sxs-lookup"><span data-stu-id="4c40b-177">To enforce access policy for applications, select **For browser and native applications**.</span></span> <span data-ttu-id="4c40b-178">Then, you can include:</span><span class="sxs-lookup"><span data-stu-id="4c40b-178">Then, you can include:</span></span>

* <span data-ttu-id="4c40b-179">Browsers (for example, Microsoft Edge in Windows 10 or Safari in iOS).</span><span class="sxs-lookup"><span data-stu-id="4c40b-179">Browsers (for example, Microsoft Edge in Windows 10 or Safari in iOS).</span></span>
* <span data-ttu-id="4c40b-180">Applications that use the Active Directory Authentication Library (ADAL) on any platform, or that use the WebAccountManager (WAM) API in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="4c40b-180">Applications that use the Active Directory Authentication Library (ADAL) on any platform, or that use the WebAccountManager (WAM) API in Windows 10.</span></span>

> [!NOTE]
> <span data-ttu-id="4c40b-181">For more information about browser support and other considerations for a user who is accessing a device-based, certificate authority-protected application, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span><span class="sxs-lookup"><span data-stu-id="4c40b-181">For more information about browser support and other considerations for a user who is accessing a device-based, certificate authority-protected application, see [Azure Active Directory conditional access](active-directory-conditional-access.md).</span></span>
> 
> 

## <a name="help-protect-email-access-from-exchange-activesync-based-applications"></a><span data-ttu-id="4c40b-182">Help protect email access from Exchange ActiveSync-based applications</span><span class="sxs-lookup"><span data-stu-id="4c40b-182">Help protect email access from Exchange ActiveSync-based applications</span></span>
<span data-ttu-id="4c40b-183">In Office 365 Exchange Online applications, you can use Exchange ActiveSync to block email access to Exchange ActiveSync-based mail applications.</span><span class="sxs-lookup"><span data-stu-id="4c40b-183">In Office 365 Exchange Online applications, you can use Exchange ActiveSync to block email access to Exchange ActiveSync-based mail applications.</span></span>

<span data-ttu-id="4c40b-184">![Exchange ActiveSync compliance options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/09.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-184">![Exchange ActiveSync compliance options](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/09.png "Applications")</span></span>

<span data-ttu-id="4c40b-185">![Require a compliant device to access email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/10.png "Applications")</span><span class="sxs-lookup"><span data-stu-id="4c40b-185">![Require a compliant device to access email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access-policy-connected-applications/10.png "Applications")</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c40b-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="4c40b-186">Next steps</span></span>
* [<span data-ttu-id="4c40b-187">Azure Active Directory conditional access</span><span class="sxs-lookup"><span data-stu-id="4c40b-187">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)












