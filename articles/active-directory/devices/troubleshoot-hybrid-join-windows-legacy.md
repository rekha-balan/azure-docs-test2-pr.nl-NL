---
title: Troubleshooting hybrid Azure Active Directory joined down-level devices | Microsoft Docs
description: Troubleshooting hybrid Azure Active Directory joined down-level devices.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.component: devices
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/23/2018
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 2c50ba1abfe3681a39b39bf52f127efd9d518aef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865397"
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="960fc-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span><span class="sxs-lookup"><span data-stu-id="960fc-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="960fc-104">This article is applicable only to the following devices:</span><span class="sxs-lookup"><span data-stu-id="960fc-104">This article is applicable only to the following devices:</span></span> 

- <span data-ttu-id="960fc-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="960fc-105">Windows 7</span></span> 
- <span data-ttu-id="960fc-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="960fc-106">Windows 8.1</span></span> 
- <span data-ttu-id="960fc-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="960fc-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="960fc-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="960fc-108">Windows Server 2012</span></span> 
- <span data-ttu-id="960fc-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="960fc-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="960fc-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="960fc-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="960fc-111">This article assumes that you have [configured hybrid Azure Active Directory joined devices](hybrid-azuread-join-plan.md) to support the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="960fc-111">This article assumes that you have [configured hybrid Azure Active Directory joined devices](hybrid-azuread-join-plan.md) to support the following scenarios:</span></span>

- <span data-ttu-id="960fc-112">Device-based conditional access</span><span class="sxs-lookup"><span data-stu-id="960fc-112">Device-based conditional access</span></span>

- [<span data-ttu-id="960fc-113">Enterprise roaming of settings</span><span class="sxs-lookup"><span data-stu-id="960fc-113">Enterprise roaming of settings</span></span>](../active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="960fc-114">Windows Hello for Business</span><span class="sxs-lookup"><span data-stu-id="960fc-114">Windows Hello for Business</span></span>](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification) 





<span data-ttu-id="960fc-115">This article provides you with troubleshooting guidance on how to resolve potential issues.</span><span class="sxs-lookup"><span data-stu-id="960fc-115">This article provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  

<span data-ttu-id="960fc-116">**What you should know:**</span><span class="sxs-lookup"><span data-stu-id="960fc-116">**What you should know:**</span></span> 

- <span data-ttu-id="960fc-117">The maximum number of devices per user is device-centric.</span><span class="sxs-lookup"><span data-stu-id="960fc-117">The maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="960fc-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span><span class="sxs-lookup"><span data-stu-id="960fc-118">For example, if *jdoe* and *jharnett* sign-in to a device, a separate registration (DeviceID) is created for each of them in the **USER** info tab.</span></span>  

- <span data-ttu-id="960fc-119">The initial registration / join of devices is configured to perform an attempt at either sign-in or lock / unlock.</span><span class="sxs-lookup"><span data-stu-id="960fc-119">The initial registration / join of devices is configured to perform an attempt at either sign-in or lock / unlock.</span></span> <span data-ttu-id="960fc-120">There could be 5-minute delay triggered by a task scheduler task.</span><span class="sxs-lookup"><span data-stu-id="960fc-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="960fc-121">You can get multiple entries for a device on the user info tab because of a reinstallation of the operating system or a manual re-registration.</span><span class="sxs-lookup"><span data-stu-id="960fc-121">You can get multiple entries for a device on the user info tab because of a reinstallation of the operating system or a manual re-registration.</span></span> 

- <span data-ttu-id="960fc-122">Make sure [KB4284842](https://support.microsoft.com/help/4284842) is installed, in case of Windows 7 SP1 or Windows Server 2008 R2 SP1.</span><span class="sxs-lookup"><span data-stu-id="960fc-122">Make sure [KB4284842](https://support.microsoft.com/help/4284842) is installed, in case of Windows 7 SP1 or Windows Server 2008 R2 SP1.</span></span> <span data-ttu-id="960fc-123">This update prevents future authentication failures due to customer's access loss to protected keys after changing password.</span><span class="sxs-lookup"><span data-stu-id="960fc-123">This update prevents future authentication failures due to customer's access loss to protected keys after changing password.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="960fc-124">Step 1: Retrieve the registration status</span><span class="sxs-lookup"><span data-stu-id="960fc-124">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="960fc-125">**To verify the registration status:**</span><span class="sxs-lookup"><span data-stu-id="960fc-125">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="960fc-126">Sign on with the user account that has performed a hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="960fc-126">Sign on with the user account that has performed a hybrid Azure AD join.</span></span>

2. <span data-ttu-id="960fc-127">Open the command prompt as an administrator</span><span class="sxs-lookup"><span data-stu-id="960fc-127">Open the command prompt as an administrator</span></span> 

3. <span data-ttu-id="960fc-128">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe" /i`</span><span class="sxs-lookup"><span data-stu-id="960fc-128">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe" /i`</span></span>

<span data-ttu-id="960fc-129">This command displays a dialog box that provides you with more details about the join status.</span><span class="sxs-lookup"><span data-stu-id="960fc-129">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join for Windows](./media/troubleshoot-hybrid-join-windows-legacy/01.png)


## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a><span data-ttu-id="960fc-131">Step 2: Evaluate the hybrid Azure AD join status</span><span class="sxs-lookup"><span data-stu-id="960fc-131">Step 2: Evaluate the hybrid Azure AD join status</span></span> 

<span data-ttu-id="960fc-132">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span><span class="sxs-lookup"><span data-stu-id="960fc-132">If the hybrid Azure AD join was not successful, the dialog box provides you with details about the issue that has occurred.</span></span>

<span data-ttu-id="960fc-133">**The most common issues are:**</span><span class="sxs-lookup"><span data-stu-id="960fc-133">**The most common issues are:**</span></span>

- <span data-ttu-id="960fc-134">A misconfigured AD FS or Azure AD</span><span class="sxs-lookup"><span data-stu-id="960fc-134">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/troubleshoot-hybrid-join-windows-legacy/02.png)

- <span data-ttu-id="960fc-136">You are not signed on as a domain user</span><span class="sxs-lookup"><span data-stu-id="960fc-136">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/troubleshoot-hybrid-join-windows-legacy/03.png)
    
    <span data-ttu-id="960fc-138">There are a few different reasons why this can occur:</span><span class="sxs-lookup"><span data-stu-id="960fc-138">There are a few different reasons why this can occur:</span></span>
    
    - <span data-ttu-id="960fc-139">The signed in user is not a domain user (for example, a local user).</span><span class="sxs-lookup"><span data-stu-id="960fc-139">The signed in user is not a domain user (for example, a local user).</span></span> <span data-ttu-id="960fc-140">Hybrid Azure AD join on down-level devices is supported only for domain users.</span><span class="sxs-lookup"><span data-stu-id="960fc-140">Hybrid Azure AD join on down-level devices is supported only for domain users.</span></span>
    
    - <span data-ttu-id="960fc-141">Autoworkplace.exe is unable to silently authenticate with Azure AD or AD FS.</span><span class="sxs-lookup"><span data-stu-id="960fc-141">Autoworkplace.exe is unable to silently authenticate with Azure AD or AD FS.</span></span> <span data-ttu-id="960fc-142">This could be caused by an out-bound network connectivity issues to the Azure AD URLs.</span><span class="sxs-lookup"><span data-stu-id="960fc-142">This could be caused by an out-bound network connectivity issues to the Azure AD URLs.</span></span> <span data-ttu-id="960fc-143">It could also be that multi-factor authentication (MFA) is enabled/configured for the user and WIAORMUTLIAUTHN is not configured at the federation server.</span><span class="sxs-lookup"><span data-stu-id="960fc-143">It could also be that multi-factor authentication (MFA) is enabled/configured for the user and WIAORMUTLIAUTHN is not configured at the federation server.</span></span> <span data-ttu-id="960fc-144">Another possibility is that home realm discovery (HRD) page is waiting for user interaction, which prevents **autoworkplace.exe** from silently requesting a token.</span><span class="sxs-lookup"><span data-stu-id="960fc-144">Another possibility is that home realm discovery (HRD) page is waiting for user interaction, which prevents **autoworkplace.exe** from silently requesting a token.</span></span>
    
    - <span data-ttu-id="960fc-145">Your organization uses Azure AD Seamless Single Sign-On, `https://autologon.microsoftazuread-sso.com` or `https://aadg.windows.net.nsatc.net` are not present on the device's IE intranet settings, and **Allow updates to status bar via script** is not enabled for the Intranet zone.</span><span class="sxs-lookup"><span data-stu-id="960fc-145">Your organization uses Azure AD Seamless Single Sign-On, `https://autologon.microsoftazuread-sso.com` or `https://aadg.windows.net.nsatc.net` are not present on the device's IE intranet settings, and **Allow updates to status bar via script** is not enabled for the Intranet zone.</span></span>

- <span data-ttu-id="960fc-146">A quota has been reached</span><span class="sxs-lookup"><span data-stu-id="960fc-146">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/troubleshoot-hybrid-join-windows-legacy/04.png)

- <span data-ttu-id="960fc-148">The service is not responding</span><span class="sxs-lookup"><span data-stu-id="960fc-148">The service is not responding</span></span> 

    ![Workplace Join for Windows](./media/troubleshoot-hybrid-join-windows-legacy/05.png)

<span data-ttu-id="960fc-150">You can also find the status information in the event log under: **Applications and Services Log\Microsoft-Workplace Join**</span><span class="sxs-lookup"><span data-stu-id="960fc-150">You can also find the status information in the event log under: **Applications and Services Log\Microsoft-Workplace Join**</span></span>
  
<span data-ttu-id="960fc-151">**The most common causes for a failed hybrid Azure AD join are:**</span><span class="sxs-lookup"><span data-stu-id="960fc-151">**The most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="960fc-152">Your computer is not connected to your organization’s internal network or to a VPN with a connection to your on-premises AD domain controller.</span><span class="sxs-lookup"><span data-stu-id="960fc-152">Your computer is not connected to your organization’s internal network or to a VPN with a connection to your on-premises AD domain controller.</span></span>

- <span data-ttu-id="960fc-153">You are logged on to your computer with a local computer account.</span><span class="sxs-lookup"><span data-stu-id="960fc-153">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="960fc-154">Service configuration issues:</span><span class="sxs-lookup"><span data-stu-id="960fc-154">Service configuration issues:</span></span> 

  - <span data-ttu-id="960fc-155">The federation server has been configured to support **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="960fc-155">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="960fc-156">Your computer's forest has no Service Connection Point object that points to your verified domain name in Azure AD</span><span class="sxs-lookup"><span data-stu-id="960fc-156">Your computer's forest has no Service Connection Point object that points to your verified domain name in Azure AD</span></span> 

  - <span data-ttu-id="960fc-157">A user has reached the limit of devices.</span><span class="sxs-lookup"><span data-stu-id="960fc-157">A user has reached the limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="960fc-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="960fc-158">Next steps</span></span>

<span data-ttu-id="960fc-159">For questions, see the [device management FAQ](faq.md)</span><span class="sxs-lookup"><span data-stu-id="960fc-159">For questions, see the [device management FAQ](faq.md)</span></span>  
