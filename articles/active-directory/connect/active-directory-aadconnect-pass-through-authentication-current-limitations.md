---
title: 'Azure AD Connect: Pass-through Authentication - Current limitations | Microsoft Docs'
description: This article describes the current limitations of Azure Active Directory (Azure AD) Pass-through Authentication
services: active-directory
keywords: Azure AD Connect Pass-through Authentication, install Active Directory, required components for Azure AD, SSO, Single Sign-on
documentationcenter: ''
author: billmath
manager: mtillman
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/04/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: ff023812acd5e30bfec34254379431b3e620dac9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864488"
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a><span data-ttu-id="dc15a-104">Azure Active Directory Pass-through Authentication: Current limitations</span><span class="sxs-lookup"><span data-stu-id="dc15a-104">Azure Active Directory Pass-through Authentication: Current limitations</span></span>

>[!IMPORTANT]
><span data-ttu-id="dc15a-105">Azure Active Directory (Azure AD) Pass-through Authentication is a free feature, and you don't need any paid editions of Azure AD to use it.</span><span class="sxs-lookup"><span data-stu-id="dc15a-105">Azure Active Directory (Azure AD) Pass-through Authentication is a free feature, and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="dc15a-106">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on the [Microsoft Azure Germany cloud](http://www.microsoft.de/cloud-deutschland) or the [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/).</span><span class="sxs-lookup"><span data-stu-id="dc15a-106">Pass-through Authentication is only available in the world-wide instance of Azure AD, and not on the [Microsoft Azure Germany cloud](http://www.microsoft.de/cloud-deutschland) or the [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="dc15a-107">Supported scenarios</span><span class="sxs-lookup"><span data-stu-id="dc15a-107">Supported scenarios</span></span>

<span data-ttu-id="dc15a-108">The following scenarios are supported:</span><span class="sxs-lookup"><span data-stu-id="dc15a-108">The following scenarios are supported:</span></span>

- <span data-ttu-id="dc15a-109">User sign-ins to web browser-based applications.</span><span class="sxs-lookup"><span data-stu-id="dc15a-109">User sign-ins to web browser-based applications.</span></span>
- <span data-ttu-id="dc15a-110">User sign-ins to Outlook clients using legacy protocols such as Exchange ActiveSync, EAS, SMTP, POP and IMAP.</span><span class="sxs-lookup"><span data-stu-id="dc15a-110">User sign-ins to Outlook clients using legacy protocols such as Exchange ActiveSync, EAS, SMTP, POP and IMAP.</span></span>
- <span data-ttu-id="dc15a-111">User sign-ins to legacy Office client applications and Office applications that support [modern authentication](https://aka.ms/modernauthga): Office 2010, 2013 and 2016 versions.</span><span class="sxs-lookup"><span data-stu-id="dc15a-111">User sign-ins to legacy Office client applications and Office applications that support [modern authentication](https://aka.ms/modernauthga): Office 2010, 2013 and 2016 versions.</span></span>
- <span data-ttu-id="dc15a-112">User sign-ins to legacy protocol applications such as PowerShell version 1.0 and others.</span><span class="sxs-lookup"><span data-stu-id="dc15a-112">User sign-ins to legacy protocol applications such as PowerShell version 1.0 and others.</span></span>
- <span data-ttu-id="dc15a-113">Azure AD joins for Windows 10 devices.</span><span class="sxs-lookup"><span data-stu-id="dc15a-113">Azure AD joins for Windows 10 devices.</span></span>
- <span data-ttu-id="dc15a-114">App passwords for Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="dc15a-114">App passwords for Multi-Factor Authentication.</span></span>

## <a name="unsupported-scenarios"></a><span data-ttu-id="dc15a-115">Unsupported scenarios</span><span class="sxs-lookup"><span data-stu-id="dc15a-115">Unsupported scenarios</span></span>

<span data-ttu-id="dc15a-116">The following scenarios are _not_ supported:</span><span class="sxs-lookup"><span data-stu-id="dc15a-116">The following scenarios are _not_ supported:</span></span>

- <span data-ttu-id="dc15a-117">Detection of users with [leaked credentials](../reports-monitoring/concept-risk-events.md#leaked-credentials).</span><span class="sxs-lookup"><span data-stu-id="dc15a-117">Detection of users with [leaked credentials](../reports-monitoring/concept-risk-events.md#leaked-credentials).</span></span>
- <span data-ttu-id="dc15a-118">Azure AD Domain Services needs Password Hash Synchronization to be enabled on the tenant.</span><span class="sxs-lookup"><span data-stu-id="dc15a-118">Azure AD Domain Services needs Password Hash Synchronization to be enabled on the tenant.</span></span> <span data-ttu-id="dc15a-119">Therefore tenants that use Pass-through Authentication _only_ don't work for scenarios that need Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="dc15a-119">Therefore tenants that use Pass-through Authentication _only_ don't work for scenarios that need Azure AD Domain Services.</span></span>
- <span data-ttu-id="dc15a-120">Pass-through Authentication is not integrated with [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md).</span><span class="sxs-lookup"><span data-stu-id="dc15a-120">Pass-through Authentication is not integrated with [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="dc15a-121">As a workaround for unsupported scenarios _only_ (except Azure AD Connect Health integration), enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span><span class="sxs-lookup"><span data-stu-id="dc15a-121">As a workaround for unsupported scenarios _only_ (except Azure AD Connect Health integration), enable Password Hash Synchronization on the [Optional features](active-directory-aadconnect-get-started-custom.md#optional-features) page in the Azure AD Connect wizard.</span></span>

>[!NOTE]
<span data-ttu-id="dc15a-122">Enabling Password Hash Synchronization gives you the option to failover authentication if your on-premises infrastructure is disrupted.</span><span class="sxs-lookup"><span data-stu-id="dc15a-122">Enabling Password Hash Synchronization gives you the option to failover authentication if your on-premises infrastructure is disrupted.</span></span> <span data-ttu-id="dc15a-123">This failover from Pass-through Authentication to Password Hash Synchronization is not automatic.</span><span class="sxs-lookup"><span data-stu-id="dc15a-123">This failover from Pass-through Authentication to Password Hash Synchronization is not automatic.</span></span> <span data-ttu-id="dc15a-124">You'll need to switch the sign-in method manually using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="dc15a-124">You'll need to switch the sign-in method manually using Azure AD Connect.</span></span> <span data-ttu-id="dc15a-125">If the server running Azure AD Connect goes down, you'll require help from Microsoft Support to turn off Pass-through Authentication.</span><span class="sxs-lookup"><span data-stu-id="dc15a-125">If the server running Azure AD Connect goes down, you'll require help from Microsoft Support to turn off Pass-through Authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc15a-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc15a-126">Next steps</span></span>
- <span data-ttu-id="dc15a-127">[Quick start](active-directory-aadconnect-pass-through-authentication-quick-start.md): Get up and running with Azure AD Pass-through Authentication.</span><span class="sxs-lookup"><span data-stu-id="dc15a-127">[Quick start](active-directory-aadconnect-pass-through-authentication-quick-start.md): Get up and running with Azure AD Pass-through Authentication.</span></span>
- <span data-ttu-id="dc15a-128">[Migrate from AD FS to Pass-through Authentication](https://github.com/Identity-Deployment-Guides/Identity-Deployment-Guides/blob/master/Authentication/Migrating%20from%20Federated%20Authentication%20to%20Pass-through%20Authentication.docx) - A detailed guide to migrate from AD FS (or other federation technologies) to Pass-through Authentication.</span><span class="sxs-lookup"><span data-stu-id="dc15a-128">[Migrate from AD FS to Pass-through Authentication](https://github.com/Identity-Deployment-Guides/Identity-Deployment-Guides/blob/master/Authentication/Migrating%20from%20Federated%20Authentication%20to%20Pass-through%20Authentication.docx) - A detailed guide to migrate from AD FS (or other federation technologies) to Pass-through Authentication.</span></span>
- <span data-ttu-id="dc15a-129">[Smart Lockout](../authentication/howto-password-smart-lockout.md): Learn how to configure the Smart Lockout capability on your tenant to protect user accounts.</span><span class="sxs-lookup"><span data-stu-id="dc15a-129">[Smart Lockout](../authentication/howto-password-smart-lockout.md): Learn how to configure the Smart Lockout capability on your tenant to protect user accounts.</span></span>
- <span data-ttu-id="dc15a-130">[Technical deep dive](active-directory-aadconnect-pass-through-authentication-how-it-works.md): Understand how the Pass-through Authentication feature works.</span><span class="sxs-lookup"><span data-stu-id="dc15a-130">[Technical deep dive](active-directory-aadconnect-pass-through-authentication-how-it-works.md): Understand how the Pass-through Authentication feature works.</span></span>
- <span data-ttu-id="dc15a-131">[Frequently asked questions](active-directory-aadconnect-pass-through-authentication-faq.md): Find answers to frequently asked questions about the Pass-through Authentication feature.</span><span class="sxs-lookup"><span data-stu-id="dc15a-131">[Frequently asked questions](active-directory-aadconnect-pass-through-authentication-faq.md): Find answers to frequently asked questions about the Pass-through Authentication feature.</span></span>
- <span data-ttu-id="dc15a-132">[Troubleshoot](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): Learn how to resolve common problems with the Pass-through Authentication feature.</span><span class="sxs-lookup"><span data-stu-id="dc15a-132">[Troubleshoot](active-directory-aadconnect-troubleshoot-pass-through-authentication.md): Learn how to resolve common problems with the Pass-through Authentication feature.</span></span>
- <span data-ttu-id="dc15a-133">[Security deep dive](active-directory-aadconnect-pass-through-authentication-security-deep-dive.md): Get deep technical information on the Pass-through Authentication feature.</span><span class="sxs-lookup"><span data-stu-id="dc15a-133">[Security deep dive](active-directory-aadconnect-pass-through-authentication-security-deep-dive.md): Get deep technical information on the Pass-through Authentication feature.</span></span>
- <span data-ttu-id="dc15a-134">[Azure AD Seamless SSO](active-directory-aadconnect-sso.md): Learn more about this complementary feature.</span><span class="sxs-lookup"><span data-stu-id="dc15a-134">[Azure AD Seamless SSO](active-directory-aadconnect-sso.md): Learn more about this complementary feature.</span></span>
- <span data-ttu-id="dc15a-135">[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): Use the Azure Active Directory Forum to file new feature requests.</span><span class="sxs-lookup"><span data-stu-id="dc15a-135">[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): Use the Azure Active Directory Forum to file new feature requests.</span></span>
