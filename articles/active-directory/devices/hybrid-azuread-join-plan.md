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
ms.openlocfilehash: 12d3b358be8bb90b63e5e7310123f8ae7093994c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868020"
---
# <a name="how-to-plan-your-hybrid-azure-active-directory-join-implementation"></a><span data-ttu-id="d2fab-103">How to plan your hybrid Azure Active Directory join implementation</span><span class="sxs-lookup"><span data-stu-id="d2fab-103">How to plan your hybrid Azure Active Directory join implementation</span></span>

<span data-ttu-id="d2fab-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span><span class="sxs-lookup"><span data-stu-id="d2fab-104">In a similar way to a user, a device is becoming another identity you want to protect and also use to protect your resources at any time and location.</span></span> <span data-ttu-id="d2fab-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="d2fab-105">You can accomplish this goal by bringing your devices' identities to Azure AD using one of the following methods:</span></span>

- <span data-ttu-id="d2fab-106">Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d2fab-106">Azure AD join</span></span>
- <span data-ttu-id="d2fab-107">Hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="d2fab-107">Hybrid Azure AD join</span></span>
- <span data-ttu-id="d2fab-108">Azure AD registration</span><span class="sxs-lookup"><span data-stu-id="d2fab-108">Azure AD registration</span></span>

<span data-ttu-id="d2fab-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span><span class="sxs-lookup"><span data-stu-id="d2fab-109">By bringing your devices to Azure AD, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources.</span></span> <span data-ttu-id="d2fab-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2fab-110">At the same time, you can secure access to your cloud and on-premises resources with [conditional access](../active-directory-conditional-access-azure-portal.md).</span></span>

<span data-ttu-id="d2fab-111">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span><span class="sxs-lookup"><span data-stu-id="d2fab-111">If you have an on-premises Active Directory environment and you want to join your domain-joined devices to Azure AD, you can accomplish this by configuring hybrid Azure AD joined devices.</span></span> <span data-ttu-id="d2fab-112">This article provides you with the related steps to implement a hybrid Azure AD join in your environment.</span><span class="sxs-lookup"><span data-stu-id="d2fab-112">This article provides you with the related steps to implement a hybrid Azure AD join in your environment.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="d2fab-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d2fab-113">Prerequisites</span></span>

<span data-ttu-id="d2fab-114">This article assumes that you are familiar with the [Introduction to device management in Azure Active Directory](../device-management-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2fab-114">This article assumes that you are familiar with the [Introduction to device management in Azure Active Directory](../device-management-introduction.md).</span></span>


## <a name="plan-your-implementation"></a><span data-ttu-id="d2fab-115">Plan your implementation</span><span class="sxs-lookup"><span data-stu-id="d2fab-115">Plan your implementation</span></span>

<span data-ttu-id="d2fab-116">To plan your hybrid Azure AD implementation, you should familiarize yourself with:</span><span class="sxs-lookup"><span data-stu-id="d2fab-116">To plan your hybrid Azure AD implementation, you should familiarize yourself with:</span></span>

|   |   |
|---|---|
|![Check][1]|<span data-ttu-id="d2fab-118">Review supported devices</span><span class="sxs-lookup"><span data-stu-id="d2fab-118">Review supported devices</span></span>|
|![Check][1]|<span data-ttu-id="d2fab-120">Review things you should know</span><span class="sxs-lookup"><span data-stu-id="d2fab-120">Review things you should know</span></span>|
|![Check][1]|<span data-ttu-id="d2fab-122">Select your scenario</span><span class="sxs-lookup"><span data-stu-id="d2fab-122">Select your scenario</span></span>|


 


## <a name="review-supported-devices"></a><span data-ttu-id="d2fab-123">Review supported devices</span><span class="sxs-lookup"><span data-stu-id="d2fab-123">Review supported devices</span></span> 

<span data-ttu-id="d2fab-124">Hybrid Azure AD join supports a broad range of Windows devices.</span><span class="sxs-lookup"><span data-stu-id="d2fab-124">Hybrid Azure AD join supports a broad range of Windows devices.</span></span> <span data-ttu-id="d2fab-125">Because the configuration for devices running older versions of Windows requires additional or different steps, the supported devices are grouped into two categories:</span><span class="sxs-lookup"><span data-stu-id="d2fab-125">Because the configuration for devices running older versions of Windows requires additional or different steps, the supported devices are grouped into two categories:</span></span>

<span data-ttu-id="d2fab-126">**Windows current devices**</span><span class="sxs-lookup"><span data-stu-id="d2fab-126">**Windows current devices**</span></span>

- <span data-ttu-id="d2fab-127">Windows 10</span><span class="sxs-lookup"><span data-stu-id="d2fab-127">Windows 10</span></span>
    
- <span data-ttu-id="d2fab-128">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d2fab-128">Windows Server 2016</span></span>


<span data-ttu-id="d2fab-129">For devices running the Windows desktop operating system, the supported version is the Windows 10 Anniversary Update (version 1607) or later.</span><span class="sxs-lookup"><span data-stu-id="d2fab-129">For devices running the Windows desktop operating system, the supported version is the Windows 10 Anniversary Update (version 1607) or later.</span></span> <span data-ttu-id="d2fab-130">As a best practice, upgrade to the latest version of Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d2fab-130">As a best practice, upgrade to the latest version of Windows 10.</span></span>



 <span data-ttu-id="d2fab-131">**Windows down-level devices**</span><span class="sxs-lookup"><span data-stu-id="d2fab-131">**Windows down-level devices**</span></span>

- <span data-ttu-id="d2fab-132">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="d2fab-132">Windows 8.1</span></span>
 
- <span data-ttu-id="d2fab-133">Windows 7</span><span class="sxs-lookup"><span data-stu-id="d2fab-133">Windows 7</span></span>

- <span data-ttu-id="d2fab-134">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="d2fab-134">Windows Server 2012 R2</span></span>
 
- <span data-ttu-id="d2fab-135">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="d2fab-135">Windows Server 2012</span></span> 
 
- <span data-ttu-id="d2fab-136">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="d2fab-136">Windows Server 2008 R2</span></span> 


<span data-ttu-id="d2fab-137">As a first planning step, you should review your environment and determine whether you need to support Windows down-level devices.</span><span class="sxs-lookup"><span data-stu-id="d2fab-137">As a first planning step, you should review your environment and determine whether you need to support Windows down-level devices.</span></span>



## <a name="review-things-you-should-know"></a><span data-ttu-id="d2fab-138">Review things you should know</span><span class="sxs-lookup"><span data-stu-id="d2fab-138">Review things you should know</span></span>

<span data-ttu-id="d2fab-139">You can't use a hybrid Azure AD join if your environment consists of a single forest that synchronized identity data to more than one Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="d2fab-139">You can't use a hybrid Azure AD join if your environment consists of a single forest that synchronized identity data to more than one Azure AD tenant.</span></span>

<span data-ttu-id="d2fab-140">If you are relying on the System Preparation Tool (Sysprep), make sure you create images from an installation of Windows that has not been configured for hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="d2fab-140">If you are relying on the System Preparation Tool (Sysprep), make sure you create images from an installation of Windows that has not been configured for hybrid Azure AD join.</span></span>

<span data-ttu-id="d2fab-141">If you are relying on a Virtual Machine (VM) snapshot to create additional VMs, make sure you use a VM snapshot that has not been configured for hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="d2fab-141">If you are relying on a Virtual Machine (VM) snapshot to create additional VMs, make sure you use a VM snapshot that has not been configured for hybrid Azure AD join.</span></span>

<span data-ttu-id="d2fab-142">The registration of Windows down-level devices is not supported for devices configured for user profile roaming or credential roaming.</span><span class="sxs-lookup"><span data-stu-id="d2fab-142">The registration of Windows down-level devices is not supported for devices configured for user profile roaming or credential roaming.</span></span> <span data-ttu-id="d2fab-143">If you are relying on roaming of profiles or settings, use Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d2fab-143">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>

- <span data-ttu-id="d2fab-144">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso-quick-start).</span><span class="sxs-lookup"><span data-stu-id="d2fab-144">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso-quick-start).</span></span> 
 
- <span data-ttu-id="d2fab-145">The registration of Windows down-level devices **is not** supported when using Azure AD Pass-through Authentication without Seamless Single Sign On.</span><span class="sxs-lookup"><span data-stu-id="d2fab-145">The registration of Windows down-level devices **is not** supported when using Azure AD Pass-through Authentication without Seamless Single Sign On.</span></span>

- <span data-ttu-id="d2fab-146">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span><span class="sxs-lookup"><span data-stu-id="d2fab-146">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="d2fab-147">If you are relying on roaming of profiles or settings, use Windows 10.</span><span class="sxs-lookup"><span data-stu-id="d2fab-147">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>


<span data-ttu-id="d2fab-148">The registration of Windows Server running the Domain Controller (DC) role is not supported.</span><span class="sxs-lookup"><span data-stu-id="d2fab-148">The registration of Windows Server running the Domain Controller (DC) role is not supported.</span></span>

<span data-ttu-id="d2fab-149">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span><span class="sxs-lookup"><span data-stu-id="d2fab-149">If your organization requires access to the Internet via an authenticated outbound proxy, you must make sure that your Windows 10 computers can successfully authenticate to the outbound proxy.</span></span> <span data-ttu-id="d2fab-150">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span><span class="sxs-lookup"><span data-stu-id="d2fab-150">Because Windows 10 computers run device registration using machine context, it is necessary to configure outbound proxy authentication using machine context.</span></span>


<span data-ttu-id="d2fab-151">Hybrid Azure AD join is a process to automatically register your on-premises domain-joined devices with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2fab-151">Hybrid Azure AD join is a process to automatically register your on-premises domain-joined devices with Azure AD.</span></span> <span data-ttu-id="d2fab-152">There are cases where you don't want all your devices to register automatically.</span><span class="sxs-lookup"><span data-stu-id="d2fab-152">There are cases where you don't want all your devices to register automatically.</span></span> <span data-ttu-id="d2fab-153">If this is true for you, see [How to control the hybrid Azure AD join of your devices](hybrid-azuread-join-control.md).</span><span class="sxs-lookup"><span data-stu-id="d2fab-153">If this is true for you, see [How to control the hybrid Azure AD join of your devices](hybrid-azuread-join-control.md).</span></span>



## <a name="select-your-scenario"></a><span data-ttu-id="d2fab-154">Select your scenario</span><span class="sxs-lookup"><span data-stu-id="d2fab-154">Select your scenario</span></span>

<span data-ttu-id="d2fab-155">You can configure hybrid Azure AD join for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="d2fab-155">You can configure hybrid Azure AD join for the following scenarios:</span></span>

- <span data-ttu-id="d2fab-156">Managed domains</span><span class="sxs-lookup"><span data-stu-id="d2fab-156">Managed domains</span></span>
- <span data-ttu-id="d2fab-157">Federated domains</span><span class="sxs-lookup"><span data-stu-id="d2fab-157">Federated domains</span></span>  



<span data-ttu-id="d2fab-158">If your environment has managed domains, hybrid Azure AD join supports:</span><span class="sxs-lookup"><span data-stu-id="d2fab-158">If your environment has managed domains, hybrid Azure AD join supports:</span></span>

- <span data-ttu-id="d2fab-159">Pass Through Authentication (PTA) with Seamless Single Sign On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d2fab-159">Pass Through Authentication (PTA) with Seamless Single Sign On (SSO)</span></span> 

- <span data-ttu-id="d2fab-160">Password Hash Sync (PHS) with Seamless Single Sign On (SSO)</span><span class="sxs-lookup"><span data-stu-id="d2fab-160">Password Hash Sync (PHS) with Seamless Single Sign On (SSO)</span></span> 

<span data-ttu-id="d2fab-161">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="d2fab-161">Beginning with version 1.1.819.0, Azure AD Connect provides you with a wizard to configure hybrid Azure AD join.</span></span> <span data-ttu-id="d2fab-162">The wizard enables you to significantly simplify the configuration process.</span><span class="sxs-lookup"><span data-stu-id="d2fab-162">The wizard enables you to significantly simplify the configuration process.</span></span> <span data-ttu-id="d2fab-163">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="d2fab-163">For more information, see:</span></span>

- [<span data-ttu-id="d2fab-164">Configure hybrid Azure Active Directory join for federated domains</span><span class="sxs-lookup"><span data-stu-id="d2fab-164">Configure hybrid Azure Active Directory join for federated domains</span></span>](hybrid-azuread-join-federated-domains.md)


- [<span data-ttu-id="d2fab-165">Configure hybrid Azure Active Directory join for managed domains</span><span class="sxs-lookup"><span data-stu-id="d2fab-165">Configure hybrid Azure Active Directory join for managed domains</span></span>](hybrid-azuread-join-managed-domains.md)


 <span data-ttu-id="d2fab-166">If installing the required version of Azure AD Connect is not an option for you, see [how to manually configure device registration](../device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d2fab-166">If installing the required version of Azure AD Connect is not an option for you, see [how to manually configure device registration](../device-management-hybrid-azuread-joined-devices-setup.md).</span></span> 






## <a name="next-steps"></a><span data-ttu-id="d2fab-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="d2fab-167">Next steps</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="d2fab-168">[Configure hybrid Azure Active Directory join for federated domains](hybrid-azuread-join-federated-domains.md)
> [Configure hybrid Azure Active Directory join for managed domains](hybrid-azuread-join-managed-domains.md)</span><span class="sxs-lookup"><span data-stu-id="d2fab-168">[Configure hybrid Azure Active Directory join for federated domains](hybrid-azuread-join-federated-domains.md)
[Configure hybrid Azure Active Directory join for managed domains](hybrid-azuread-join-managed-domains.md)</span></span>




<!--Image references-->
[1]: ./media/hybrid-azuread-join-plan/12.png
