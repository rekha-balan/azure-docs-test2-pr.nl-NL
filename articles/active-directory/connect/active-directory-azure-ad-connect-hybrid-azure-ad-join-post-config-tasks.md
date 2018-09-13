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
# <a name="post-configuration-tasks-for-hybrid-azure-ad-join"></a>Post configuration tasks for Hybrid Azure AD join

After you have run Azure AD Connect to configure your organization for Hybrid Azure AD join, there are a few additional steps that you must complete to finalize that setup.  Carry out only the steps that apply for your devices.

## <a name="1-configure-controlled-rollout-optional"></a>1. Configure controlled rollout (Optional)
All domain-joined devices running Windows 10 and Windows Server 2016 automatically register with Azure AD once all configuration steps are complete. If you prefer a controlled rollout rather than this auto-registration, you can use group policy to selectively enable or disable automatic rollout.  This group policy should be set before starting the other configuration steps:Azure AD
* Create a group policy object in your Active Directory.
* Name it (ex- Hybrid Azure AD join).
* Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration.

>[!NOTE]
>For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**

* Disable this setting:  Register domain-joined computers as devices.
* Apply and click OK.
* Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).

## <a name="2-configure-network-with-device-registration-endpoints"></a>2. Configure network with device registration endpoints
Make sure that the following URLs are accessible from computers inside your organizational network for registration to Azure AD:

* https://enterpriseregistration.windows.net
* https://login.microsoftonline.com
* https://device.login.microsoftonline.com 

## <a name="3-implement-wpad-for-windows-10-devices"></a>3. Implement WPAD for Windows 10 devices
If your organization accesses the Internet via an outbound proxy, implement Web Proxy Auto-Discovery (WPAD)to enable Windows 10 computers to register to Azure AD.

## <a name="4-configure-the-scp-in-any-forests-that-were-not-configured-by-azure-ad-connect"></a>4. Configure the SCP in any forests that were not configured by Azure AD Connect 

The service connection point (SCP) contains your Azure AD tenant information that will be used by your devices for auto-registration.  Run the PowerShell script, ConfigureSCP.ps1, that you downloaded from Azure AD Connect.

## <a name="5-configure-any-federation-service-that-was-not-configured-by-azure-ad-connect"></a>5. Configure any federation service that was not configured by Azure AD Connect

If your organization uses a federation service to sign in to Azure AD, the claim rules in your Azure AD relying party trust must allow device authentication. If you are using federation with AD FS, go to [AD FS Help](https://aka.ms/aadrptclaimrules) to generate the claim rules. If you are using a non-Microsoft federation solution, contact that provider for guidance.  

>[!NOTE]
>If you have Windows down-level devices, the service must support issuing the authenticationmethod and wiaormultiauthn claims when receiving requests to the Azure AD trust. In AD FS, you should add an issuance transform rule that passes-through the authentication method.

## <a name="6-enable-azure-ad-seamless-sso-for-windows-down-level-devices"></a>6. Enable Azure AD Seamless SSO for Windows down-level devices

If your organization uses Password Hash Synchronization or Pass-through Authentication to sign in to Azure AD, enable Azure AD Seamless SSO with that sign-in method to authenticate Windows down-level devices:  https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-sso. 

## <a name="7-set-azure-ad-policy-for-windows-down-level-devices"></a>7. Set Azure AD policy for Windows down-level devices

To register Windows down-level devices, you need to make sure that the Azure AD policy allows users to register devices. 

* Log-in to your account in the Azure portal.
* Go to:  Azure Active Directory > Devices > Device settings
* Set "Users may register their devices with Azure AD" to ALL.
* Click Save

## <a name="8-add-azure-ad-endpoint-to-windows-down-level-devices"></a>8. Add Azure AD endpoint to Windows down-level devices

Add the Azure AD device authentication endpoint to the local Intranet zones on your Windows down-level devices to avoid certificate prompts when authenticating the devices: https://device.login.microsoftonline.com 

If you are using [Seamless SSO](https://aka.ms/hybrid/sso), also enable “Allow status bar updates via script” on that zone and add the following endpoint: https://autologon.microsoftazuread-sso.com 

## <a name="9-install-microsoft-workplace-join-on-windows-down-level-devices"></a>9. Install Microsoft Workplace Join on Windows down-level devices

This installer creates a scheduled task on the device system that runs in the user’s context. The task is triggered when the user signs in to Windows. The task silently joins the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication. The download center is at https://www.microsoft.com/download/details.aspx?id=53554. 

## <a name="10-configure-group-policy-to-allow-device-registration"></a>10. Configure group policy to allow device registration

* Create a group policy object in your Active Directory--if not already created.
* Name it (ex- Hybrid Azure AD join).
* Edit & go to:  Computer Configuration > Policies > Administrative Templates > Windows Components > Device Registration
* Enable:  Register domain-joined computers as devices
* Apply and click OK.
* Link the GPO to the location of your choice (organizational unit, security group, or to the domain for all devices).

>[!NOTE]
>For 2012R2 the policy settings are at **Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers**

## <a name="next-steps"></a>Next steps
[Configure device writeback](./active-directory-aadconnect-feature-device-writeback.md)
