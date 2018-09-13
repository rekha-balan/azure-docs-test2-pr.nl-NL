---
title: 'Azure AD Connect: Hybrid Azure AD join post configuration tasks | Microsoft Docs'
description: This document details post configuration tasks needed to complete the Hybrid Azure AD join
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: billmath
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: 05cb6d10a7e4269cbe5f9c97ef70cd9eb5a4d68e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865841"
---
# <a name="post-configuration-tasks-for-hybrid-azure-ad-join"></a><span data-ttu-id="62fcb-103">Post configuration tasks for Hybrid Azure AD join</span><span class="sxs-lookup"><span data-stu-id="62fcb-103">Post configuration tasks for Hybrid Azure AD join</span></span>

<span data-ttu-id="62fcb-104">After you have run Azure AD Connect to configure your organization for Hybrid Azure AD join, there are a few additional steps that you must complete to finalize that setup.</span><span class="sxs-lookup"><span data-stu-id="62fcb-104">After you have run Azure AD Connect to configure your organization for Hybrid Azure AD join, there are a few additional steps that you must complete to finalize that setup.</span></span>  <span data-ttu-id="62fcb-105">Carry out only the steps that apply for your devices.</span><span class="sxs-lookup"><span data-stu-id="62fcb-105">Carry out only the steps that apply for your devices.</span></span>

## <a name="1-configure-controlled-rollout-optional"></a><span data-ttu-id="62fcb-106">1. Configure controlled rollout (Optional)</span><span class="sxs-lookup"><span data-stu-id="62fcb-106">1. Configure controlled rollout (Optional)</span></span>
<span data-ttu-id="62fcb-107">All domain-joined devices running Windows 10 and Windows Server 2016 automatically register with Azure AD once all configuration steps are complete.</span><span class="sxs-lookup"><span data-stu-id="62fcb-107">All domain-joined devices running Windows 10 and Windows Server 2016 automatically register with Azure AD once all configuration steps are complete.</span></span> <span data-ttu-id="62fcb-108">If you prefer a controlled rollout rather than this auto-registration, you can use group policy to selectively enable or disable automatic rollout.</span><span class="sxs-lookup"><span data-stu-id="62fcb-108">If you prefer a controlled rollout rather than this auto-registration, you can use group policy to selectively enable or disable automatic rollout.</span></span>  <span data-ttu-id="62fcb-109">This group policy should be set before starting the other configuration steps:Azure AD</span><span class="sxs-lookup"><span data-stu-id="62fcb-109">This group policy should be set before starting the other configuration steps:Azure AD</span></span>
* <span data-ttu-id="62fcb-110">Create a group policy object in your Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62fcb-110">Create a group policy object in your Active Directory.</span></span>
* <span data-ttu-id="62fcb-111">Name it (ex- Hybrid Azure AD join).</span><span class="sxs-lookup"><span data-stu-id="62fcb-111">Name it (ex- Hybrid Azure AD join).</span></span>
* <span data-ttu-id="62fcb-112">Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration.</span><span class="sxs-lookup"><span data-stu-id="62fcb-112">Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration.</span></span>

>[!NOTE]
><span data-ttu-id="62fcb-113">For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**</span><span class="sxs-lookup"><span data-stu-id="62fcb-113">For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**</span></span>

* <span data-ttu-id="62fcb-114">Disable this setting:  Register domain-joined computers as devices.</span><span class="sxs-lookup"><span data-stu-id="62fcb-114">Disable this setting:  Register domain-joined computers as devices.</span></span>
* <span data-ttu-id="62fcb-115">Apply and click OK.</span><span class="sxs-lookup"><span data-stu-id="62fcb-115">Apply and click OK.</span></span>
* <span data-ttu-id="62fcb-116">Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).</span><span class="sxs-lookup"><span data-stu-id="62fcb-116">Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).</span></span>

## <a name="2-configure-network-with-device-registration-endpoints"></a><span data-ttu-id="62fcb-117">2. Configure network with device registration endpoints</span><span class="sxs-lookup"><span data-stu-id="62fcb-117">2. Configure network with device registration endpoints</span></span>
<span data-ttu-id="62fcb-118">Make sure that the following URLs are accessible from computers inside your organizational network for registration to Azure AD:</span><span class="sxs-lookup"><span data-stu-id="62fcb-118">Make sure that the following URLs are accessible from computers inside your organizational network for registration to Azure AD:</span></span>

* https://enterpriseregistration.windows.net
* https://login.microsoftonline.com
* https://device.login.microsoftonline.com 

## <a name="3-implement-wpad-for-windows-10-devices"></a><span data-ttu-id="62fcb-119">3. Implement WPAD for Windows 10 devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-119">3. Implement WPAD for Windows 10 devices</span></span>
<span data-ttu-id="62fcb-120">If your organization accesses the Internet via an outbound proxy, implement Web Proxy Auto-Discovery (WPAD)to enable Windows 10 computers to register to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62fcb-120">If your organization accesses the Internet via an outbound proxy, implement Web Proxy Auto-Discovery (WPAD)to enable Windows 10 computers to register to Azure AD.</span></span>

## <a name="4-configure-the-scp-in-any-forests-that-were-not-configured-by-azure-ad-connect"></a><span data-ttu-id="62fcb-121">4. Configure the SCP in any forests that were not configured by Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="62fcb-121">4. Configure the SCP in any forests that were not configured by Azure AD Connect</span></span> 

<span data-ttu-id="62fcb-122">The service connection point (SCP) contains your Azure AD tenant information that will be used by your devices for auto-registration.</span><span class="sxs-lookup"><span data-stu-id="62fcb-122">The service connection point (SCP) contains your Azure AD tenant information that will be used by your devices for auto-registration.</span></span>  <span data-ttu-id="62fcb-123">Run the PowerShell script, ConfigureSCP.ps1, that you downloaded from Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="62fcb-123">Run the PowerShell script, ConfigureSCP.ps1, that you downloaded from Azure AD Connect.</span></span>

## <a name="5-configure-any-federation-service-that-was-not-configured-by-azure-ad-connect"></a><span data-ttu-id="62fcb-124">5. Configure any federation service that was not configured by Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="62fcb-124">5. Configure any federation service that was not configured by Azure AD Connect</span></span>

<span data-ttu-id="62fcb-125">If your organization uses a federation service to sign in to Azure AD, the claim rules in your Azure AD relying party trust must allow device authentication.</span><span class="sxs-lookup"><span data-stu-id="62fcb-125">If your organization uses a federation service to sign in to Azure AD, the claim rules in your Azure AD relying party trust must allow device authentication.</span></span> <span data-ttu-id="62fcb-126">If you are using federation with AD FS, go to [AD FS Help](https://aka.ms/aadrptclaimrules) to generate the claim rules.</span><span class="sxs-lookup"><span data-stu-id="62fcb-126">If you are using federation with AD FS, go to [AD FS Help](https://aka.ms/aadrptclaimrules) to generate the claim rules.</span></span> <span data-ttu-id="62fcb-127">If you are using a non-Microsoft federation solution, contact that provider for guidance.</span><span class="sxs-lookup"><span data-stu-id="62fcb-127">If you are using a non-Microsoft federation solution, contact that provider for guidance.</span></span>  

>[!NOTE]
><span data-ttu-id="62fcb-128">If you have Windows down-level devices, the service must support issuing the authenticationmethod and wiaormultiauthn claims when receiving requests to the Azure AD trust.</span><span class="sxs-lookup"><span data-stu-id="62fcb-128">If you have Windows down-level devices, the service must support issuing the authenticationmethod and wiaormultiauthn claims when receiving requests to the Azure AD trust.</span></span> <span data-ttu-id="62fcb-129">In AD FS, you should add an issuance transform rule that passes-through the authentication method.</span><span class="sxs-lookup"><span data-stu-id="62fcb-129">In AD FS, you should add an issuance transform rule that passes-through the authentication method.</span></span>

## <a name="6-enable-azure-ad-seamless-sso-for-windows-down-level-devices"></a><span data-ttu-id="62fcb-130">6. Enable Azure AD Seamless SSO for Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-130">6. Enable Azure AD Seamless SSO for Windows down-level devices</span></span>

<span data-ttu-id="62fcb-131">If your organization uses Password Hash Synchronization or Pass-through Authentication to sign in to Azure AD, enable Azure AD Seamless SSO with that sign-in method to authenticate Windows down-level devices:  https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso.</span><span class="sxs-lookup"><span data-stu-id="62fcb-131">If your organization uses Password Hash Synchronization or Pass-through Authentication to sign in to Azure AD, enable Azure AD Seamless SSO with that sign-in method to authenticate Windows down-level devices:  https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso.</span></span> 

## <a name="7-set-azure-ad-policy-for-windows-down-level-devices"></a><span data-ttu-id="62fcb-132">7. Set Azure AD policy for Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-132">7. Set Azure AD policy for Windows down-level devices</span></span>

<span data-ttu-id="62fcb-133">To register Windows down-level devices, you need to make sure that the Azure AD policy allows users to register devices.</span><span class="sxs-lookup"><span data-stu-id="62fcb-133">To register Windows down-level devices, you need to make sure that the Azure AD policy allows users to register devices.</span></span> 

* <span data-ttu-id="62fcb-134">Log-in to your account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="62fcb-134">Log-in to your account in the Azure portal.</span></span>
* <span data-ttu-id="62fcb-135">Go to:  Azure Active Directory > Devices > Device settings</span><span class="sxs-lookup"><span data-stu-id="62fcb-135">Go to:  Azure Active Directory > Devices > Device settings</span></span>
* <span data-ttu-id="62fcb-136">Set "Users may register their devices with Azure AD" to ALL.</span><span class="sxs-lookup"><span data-stu-id="62fcb-136">Set "Users may register their devices with Azure AD" to ALL.</span></span>
* <span data-ttu-id="62fcb-137">Click Save</span><span class="sxs-lookup"><span data-stu-id="62fcb-137">Click Save</span></span>

## <a name="8-add-azure-ad-endpoint-to-windows-down-level-devices"></a><span data-ttu-id="62fcb-138">8. Add Azure AD endpoint to Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-138">8. Add Azure AD endpoint to Windows down-level devices</span></span>

<span data-ttu-id="62fcb-139">Add the Azure AD device authentication endpoint to the local Intranet zones on your Windows down-level devices to avoid certificate prompts when authenticating the devices: https://device.login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="62fcb-139">Add the Azure AD device authentication endpoint to the local Intranet zones on your Windows down-level devices to avoid certificate prompts when authenticating the devices: https://device.login.microsoftonline.com</span></span> 

<span data-ttu-id="62fcb-140">If you are using [Seamless SSO](https://aka.ms/hybrid/sso), also enable “Allow status bar updates via script” on that zone and add the following endpoint: https://autologon.microsoftazuread-sso.com</span><span class="sxs-lookup"><span data-stu-id="62fcb-140">If you are using [Seamless SSO](https://aka.ms/hybrid/sso), also enable “Allow status bar updates via script” on that zone and add the following endpoint: https://autologon.microsoftazuread-sso.com</span></span> 

## <a name="9-install-microsoft-workplace-join-on-windows-down-level-devices"></a><span data-ttu-id="62fcb-141">9. Install Microsoft Workplace Join on Windows down-level devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-141">9. Install Microsoft Workplace Join on Windows down-level devices</span></span>

<span data-ttu-id="62fcb-142">This installer creates a scheduled task on the device system that runs in the user’s context.</span><span class="sxs-lookup"><span data-stu-id="62fcb-142">This installer creates a scheduled task on the device system that runs in the user’s context.</span></span> <span data-ttu-id="62fcb-143">The task is triggered when the user signs in to Windows.</span><span class="sxs-lookup"><span data-stu-id="62fcb-143">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="62fcb-144">The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span><span class="sxs-lookup"><span data-stu-id="62fcb-144">The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="62fcb-145">The download center is at https://www.microsoft.com/download/details.aspx?id=53554.</span><span class="sxs-lookup"><span data-stu-id="62fcb-145">The download center is at https://www.microsoft.com/download/details.aspx?id=53554.</span></span> 

## <a name="10-configure-group-policy-to-allow-device-registration"></a><span data-ttu-id="62fcb-146">10. Configure group policy to allow device registration</span><span class="sxs-lookup"><span data-stu-id="62fcb-146">10. Configure group policy to allow device registration</span></span>

* <span data-ttu-id="62fcb-147">Create a group policy object in your Active Directory--if not already created.</span><span class="sxs-lookup"><span data-stu-id="62fcb-147">Create a group policy object in your Active Directory--if not already created.</span></span>
* <span data-ttu-id="62fcb-148">Name it (ex- Hybrid Azure AD join).</span><span class="sxs-lookup"><span data-stu-id="62fcb-148">Name it (ex- Hybrid Azure AD join).</span></span>
* <span data-ttu-id="62fcb-149">Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration</span><span class="sxs-lookup"><span data-stu-id="62fcb-149">Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration</span></span>
* <span data-ttu-id="62fcb-150">Enable:  Register domain-joined computers as devices</span><span class="sxs-lookup"><span data-stu-id="62fcb-150">Enable:  Register domain-joined computers as devices</span></span>
* <span data-ttu-id="62fcb-151">Apply and click OK.</span><span class="sxs-lookup"><span data-stu-id="62fcb-151">Apply and click OK.</span></span>
* <span data-ttu-id="62fcb-152">Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).</span><span class="sxs-lookup"><span data-stu-id="62fcb-152">Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).</span></span>

>[!NOTE]
><span data-ttu-id="62fcb-153">For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**</span><span class="sxs-lookup"><span data-stu-id="62fcb-153">For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**</span></span>

## <a name="next-steps"></a><span data-ttu-id="62fcb-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="62fcb-154">Next steps</span></span>
[<span data-ttu-id="62fcb-155">Configure device writeback</span><span class="sxs-lookup"><span data-stu-id="62fcb-155">Configure device writeback</span></span>](./active-directory-aadconnect-feature-device-writeback.md)
