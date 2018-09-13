---
title: Vulnerabilities detected by Azure Active Directory Identity Protection | Microsoft Docs
description: Overview of the vulnerabilities detected by Azure Active Directory Identity Protection.
services: active-directory
keywords: azure active directory identity protection, cloud discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2018
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 680e52fefd8256b3ac270e8d721f27645ced49eb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866447"
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="6343b-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6343b-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="6343b-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span><span class="sxs-lookup"><span data-stu-id="6343b-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="6343b-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span><span class="sxs-lookup"><span data-stu-id="6343b-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="6343b-107">![vulnerabilities](./media/vulnerabilities/101.png "vulnerabilities")</span><span class="sxs-lookup"><span data-stu-id="6343b-107">![vulnerabilities](./media/vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="6343b-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="6343b-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="6343b-109">Multi-factor authentication registration not configured</span><span class="sxs-lookup"><span data-stu-id="6343b-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="6343b-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span><span class="sxs-lookup"><span data-stu-id="6343b-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="6343b-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span><span class="sxs-lookup"><span data-stu-id="6343b-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="6343b-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span><span class="sxs-lookup"><span data-stu-id="6343b-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="6343b-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span><span class="sxs-lookup"><span data-stu-id="6343b-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and third party OATH tokens.</span></span>

<span data-ttu-id="6343b-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="6343b-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="6343b-115">For more information, see [What is Azure Multi-Factor Authentication?](../authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6343b-115">For more information, see [What is Azure Multi-Factor Authentication?](../authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="6343b-116">Unmanaged cloud apps</span><span class="sxs-lookup"><span data-stu-id="6343b-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="6343b-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span><span class="sxs-lookup"><span data-stu-id="6343b-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="6343b-118">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span><span class="sxs-lookup"><span data-stu-id="6343b-118">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="6343b-119">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage, and other security risks.</span><span class="sxs-lookup"><span data-stu-id="6343b-119">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage, and other security risks.</span></span> 

<span data-ttu-id="6343b-120">We recommend to deploy Cloud Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6343b-120">We recommend to deploy Cloud Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="6343b-121">For more information, see [Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).</span><span class="sxs-lookup"><span data-stu-id="6343b-121">For more information, see [Cloud Discovery](/cloud-app-security/set-up-cloud-discovery).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="6343b-122">Security Alerts from Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="6343b-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="6343b-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span><span class="sxs-lookup"><span data-stu-id="6343b-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="6343b-124">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="6343b-124">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="6343b-125">Each of these privileged users increases the attack surface of your organization.</span><span class="sxs-lookup"><span data-stu-id="6343b-125">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="6343b-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span><span class="sxs-lookup"><span data-stu-id="6343b-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="6343b-127">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="6343b-127">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="6343b-128">For more information, see [Azure AD Privileged Identity Management](../privileged-identity-management/pim-configure.md).</span><span class="sxs-lookup"><span data-stu-id="6343b-128">For more information, see [Azure AD Privileged Identity Management](../privileged-identity-management/pim-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="6343b-129">See also</span><span class="sxs-lookup"><span data-stu-id="6343b-129">See also</span></span>

[<span data-ttu-id="6343b-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="6343b-130">Azure Active Directory Identity Protection</span></span>](../active-directory-identityprotection.md)

