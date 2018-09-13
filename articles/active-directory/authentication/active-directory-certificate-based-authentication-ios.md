---
title: Azure Active Directory certificate-based authentication on iOS
description: Learn about the supported scenarios and the requirements for configuring certificate-based authentication in solutions with iOS devices
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: article
ms.date: 01/15/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: annaba
ms.openlocfilehash: 655fa6b4bf0f04f2d88e9a3f11cb9d3917ea3dd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866408"
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="fbc39-103">Azure Active Directory certificate-based authentication on iOS</span><span class="sxs-lookup"><span data-stu-id="fbc39-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="fbc39-104">iOS devices can use certificate-based authentication (CBA) to authenticate to Azure Active Directory using a client certificate on their device when connecting to:</span><span class="sxs-lookup"><span data-stu-id="fbc39-104">iOS devices can use certificate-based authentication (CBA) to authenticate to Azure Active Directory using a client certificate on their device when connecting to:</span></span>

* <span data-ttu-id="fbc39-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="fbc39-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>
* <span data-ttu-id="fbc39-106">Exchange ActiveSync (EAS) clients</span><span class="sxs-lookup"><span data-stu-id="fbc39-106">Exchange ActiveSync (EAS) clients</span></span>

<span data-ttu-id="fbc39-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="fbc39-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span>

<span data-ttu-id="fbc39-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span><span class="sxs-lookup"><span data-stu-id="fbc39-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="fbc39-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span><span class="sxs-lookup"><span data-stu-id="fbc39-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>

## <a name="microsoft-mobile-applications-support"></a><span data-ttu-id="fbc39-110">Microsoft mobile applications support</span><span class="sxs-lookup"><span data-stu-id="fbc39-110">Microsoft mobile applications support</span></span>

| <span data-ttu-id="fbc39-111">Apps</span><span class="sxs-lookup"><span data-stu-id="fbc39-111">Apps</span></span> | <span data-ttu-id="fbc39-112">Support</span><span class="sxs-lookup"><span data-stu-id="fbc39-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="fbc39-113">Azure Information Protection app</span><span class="sxs-lookup"><span data-stu-id="fbc39-113">Azure Information Protection app</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-115">Intune Company Portal</span><span class="sxs-lookup"><span data-stu-id="fbc39-115">Intune Company Portal</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-117">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fbc39-117">Microsoft Teams</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-119">OneNote</span><span class="sxs-lookup"><span data-stu-id="fbc39-119">OneNote</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-121">OneDrive</span><span class="sxs-lookup"><span data-stu-id="fbc39-121">OneDrive</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-123">Outlook</span><span class="sxs-lookup"><span data-stu-id="fbc39-123">Outlook</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-125">Power BI</span><span class="sxs-lookup"><span data-stu-id="fbc39-125">Power BI</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-127">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="fbc39-127">Skype for Business</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-129">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="fbc39-129">Word / Excel / PowerPoint</span></span> |![Check][1] |
| <span data-ttu-id="fbc39-131">Yammer</span><span class="sxs-lookup"><span data-stu-id="fbc39-131">Yammer</span></span> |![Check][1] |

## <a name="requirements"></a><span data-ttu-id="fbc39-133">Requirements</span><span class="sxs-lookup"><span data-stu-id="fbc39-133">Requirements</span></span>

<span data-ttu-id="fbc39-134">The device OS version must be iOS 9 and above</span><span class="sxs-lookup"><span data-stu-id="fbc39-134">The device OS version must be iOS 9 and above</span></span>

<span data-ttu-id="fbc39-135">A federation server must be configured.</span><span class="sxs-lookup"><span data-stu-id="fbc39-135">A federation server must be configured.</span></span>

<span data-ttu-id="fbc39-136">Microsoft Authenticator is required for Office applications on iOS.</span><span class="sxs-lookup"><span data-stu-id="fbc39-136">Microsoft Authenticator is required for Office applications on iOS.</span></span>

<span data-ttu-id="fbc39-137">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span><span class="sxs-lookup"><span data-stu-id="fbc39-137">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>

* <span data-ttu-id="fbc39-138">`http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` (The serial number of the client certificate)</span><span class="sxs-lookup"><span data-stu-id="fbc39-138">`http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>` (The serial number of the client certificate)</span></span>
* <span data-ttu-id="fbc39-139">`http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` (The string for the issuer of the client certificate)</span><span class="sxs-lookup"><span data-stu-id="fbc39-139">`http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>` (The string for the issuer of the client certificate)</span></span>

<span data-ttu-id="fbc39-140">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span><span class="sxs-lookup"><span data-stu-id="fbc39-140">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="fbc39-141">When the refresh token needs to be validated, this information is used to check the revocation.</span><span class="sxs-lookup"><span data-stu-id="fbc39-141">When the refresh token needs to be validated, this information is used to check the revocation.</span></span>

<span data-ttu-id="fbc39-142">As a best practice, you should update your organization's ADFS error pages with the following information:</span><span class="sxs-lookup"><span data-stu-id="fbc39-142">As a best practice, you should update your organization's ADFS error pages with the following information:</span></span>

* <span data-ttu-id="fbc39-143">The requirement for installing the Microsoft Authenticator on iOS</span><span class="sxs-lookup"><span data-stu-id="fbc39-143">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="fbc39-144">Instructions on how to get a user certificate.</span><span class="sxs-lookup"><span data-stu-id="fbc39-144">Instructions on how to get a user certificate.</span></span>

<span data-ttu-id="fbc39-145">For more information, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc39-145">For more information, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="fbc39-146">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span><span class="sxs-lookup"><span data-stu-id="fbc39-146">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="fbc39-147">By default, Azure AD translates ‘*prompt=login*’ in the request to ADFS as ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P Auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span><span class="sxs-lookup"><span data-stu-id="fbc39-147">By default, Azure AD translates ‘*prompt=login*’ in the request to ADFS as ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P Auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="fbc39-148">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span><span class="sxs-lookup"><span data-stu-id="fbc39-148">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="fbc39-149">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span><span class="sxs-lookup"><span data-stu-id="fbc39-149">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span>
<span data-ttu-id="fbc39-150">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span><span class="sxs-lookup"><span data-stu-id="fbc39-150">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="fbc39-151">Exchange ActiveSync clients support</span><span class="sxs-lookup"><span data-stu-id="fbc39-151">Exchange ActiveSync clients support</span></span>

<span data-ttu-id="fbc39-152">On iOS 9 or later, the native iOS mail client is supported.</span><span class="sxs-lookup"><span data-stu-id="fbc39-152">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="fbc39-153">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span><span class="sxs-lookup"><span data-stu-id="fbc39-153">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbc39-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbc39-154">Next steps</span></span>

<span data-ttu-id="fbc39-155">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](../authentication/active-directory-certificate-based-authentication-get-started.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="fbc39-155">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](../authentication/active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
