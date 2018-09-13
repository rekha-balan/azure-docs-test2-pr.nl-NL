---
title: Azure Active Directory certificate-based authentication on iOS | Microsoft Docs
description: Learn about the supported scenarios and the requirements for configuring certificate-based authentication in solutions with iOS devices
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/30/2017
ms.author: markvi
ms.openlocfilehash: 2ef770120ce9026a36b0abbd4fc831d5ff34957e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554501"
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="d7ee0-103">Azure Active Directory certificate-based authentication on iOS</span><span class="sxs-lookup"><span data-stu-id="d7ee0-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="d7ee0-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span><span class="sxs-lookup"><span data-stu-id="d7ee0-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="d7ee0-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="d7ee0-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="d7ee0-106">Exchange ActiveSync (EAS) clients</span><span class="sxs-lookup"><span data-stu-id="d7ee0-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="d7ee0-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="d7ee0-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS device for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS device for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> 

<span data-ttu-id="d7ee0-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="d7ee0-110">Office mobile applications support</span><span class="sxs-lookup"><span data-stu-id="d7ee0-110">Office mobile applications support</span></span>

| <span data-ttu-id="d7ee0-111">Apps</span><span class="sxs-lookup"><span data-stu-id="d7ee0-111">Apps</span></span> | <span data-ttu-id="d7ee0-112">Support</span><span class="sxs-lookup"><span data-stu-id="d7ee0-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="d7ee0-113">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="d7ee0-113">Word / Excel / PowerPoint</span></span> |![Check][1] |
| <span data-ttu-id="d7ee0-115">OneNote</span><span class="sxs-lookup"><span data-stu-id="d7ee0-115">OneNote</span></span> |![Check][1] |
| <span data-ttu-id="d7ee0-117">OneDrive</span><span class="sxs-lookup"><span data-stu-id="d7ee0-117">OneDrive</span></span> |![Check][1] |
| <span data-ttu-id="d7ee0-119">Outlook</span><span class="sxs-lookup"><span data-stu-id="d7ee0-119">Outlook</span></span> |![Check][1] |
| <span data-ttu-id="d7ee0-121">Yammer</span><span class="sxs-lookup"><span data-stu-id="d7ee0-121">Yammer</span></span> |![Check][1] |
| <span data-ttu-id="d7ee0-123">Skype for Business</span><span class="sxs-lookup"><span data-stu-id="d7ee0-123">Skype for Business</span></span> |![Check][1] |

## <a name="requirements"></a><span data-ttu-id="d7ee0-125">Requirements</span><span class="sxs-lookup"><span data-stu-id="d7ee0-125">Requirements</span></span> 

<span data-ttu-id="d7ee0-126">The device OS version must be iOS 9 and above</span><span class="sxs-lookup"><span data-stu-id="d7ee0-126">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="d7ee0-127">A federation server must be configured.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-127">A federation server must be configured.</span></span>  

<span data-ttu-id="d7ee0-128">Microsoft Authenticator is required for Office applications on iOS.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-128">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="d7ee0-129">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span><span class="sxs-lookup"><span data-stu-id="d7ee0-129">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="d7ee0-130">(The serial number of the client certificate)</span><span class="sxs-lookup"><span data-stu-id="d7ee0-130">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="d7ee0-131">(The string for the issuer of the client certificate)</span><span class="sxs-lookup"><span data-stu-id="d7ee0-131">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="d7ee0-132">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span><span class="sxs-lookup"><span data-stu-id="d7ee0-132">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="d7ee0-133">When the refresh token needs to be validated, this information is used to check the revocation.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-133">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="d7ee0-134">As a best practice, you should update the ADFS error pages with the following:</span><span class="sxs-lookup"><span data-stu-id="d7ee0-134">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="d7ee0-135">The requirement for installing the Microsoft Authenticator on iOS</span><span class="sxs-lookup"><span data-stu-id="d7ee0-135">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="d7ee0-136">Instructions on how to get a user certificate.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-136">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="d7ee0-137">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="d7ee0-137">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="d7ee0-138">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-138">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="d7ee0-139">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span><span class="sxs-lookup"><span data-stu-id="d7ee0-139">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="d7ee0-140">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-140">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="d7ee0-141">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-141">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="d7ee0-142">You can use the [MSOLDomainFederationSettings](https://docs.microsoft.com/en-us/powershell/msonline/v1/set-msoldomainfederationsettings) cmdlet to perform this task:</span><span class="sxs-lookup"><span data-stu-id="d7ee0-142">You can use the [MSOLDomainFederationSettings](https://docs.microsoft.com/en-us/powershell/msonline/v1/set-msoldomainfederationsettings) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="d7ee0-143">Exchange ActiveSync clients support</span><span class="sxs-lookup"><span data-stu-id="d7ee0-143">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="d7ee0-144">On iOS 9 or later, the native iOS mail client is supported.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-144">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="d7ee0-145">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-145">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="d7ee0-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="d7ee0-146">Next steps</span></span>

<span data-ttu-id="d7ee0-147">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="d7ee0-147">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-certificate-based-authentication-ios/ic195031.png

