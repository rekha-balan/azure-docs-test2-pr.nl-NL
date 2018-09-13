---
title: Vulnerabilities detected by Azure Active Directory Identity Protection | Microsoft Docs
description: Overview of the vulnerabilities detected by Azure Active Directory Identity Protection.
services: active-directory
keywords: azure active directory identity protection, cloud app discovery, managing applications, security, risk, risk level, vulnerability, security policy
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: markvi
ms.openlocfilehash: 8a5bcb076a9ea8e7b25cec421191e215d3b591fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550152"
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a><span data-ttu-id="af702-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="af702-104">Vulnerabilities detected by Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="af702-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span><span class="sxs-lookup"><span data-stu-id="af702-105">Vulnerabilities are weaknesses in your environment that can be exploited by an attacker.</span></span> <span data-ttu-id="af702-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span><span class="sxs-lookup"><span data-stu-id="af702-106">We recommend that you address these vulnerabilities to improve the security posture of your organization, and prevent attackers from exploiting them.</span></span>


<span data-ttu-id="af702-107">![vulnerabilities](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span><span class="sxs-lookup"><span data-stu-id="af702-107">![vulnerabilities](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilities")</span></span>



<span data-ttu-id="af702-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="af702-108">The following sections provide you with an overview of the vulnerabilities reported by Identity Protection.</span></span>

## <a name="multi-factor-authentication-registration-not-configured"></a><span data-ttu-id="af702-109">Multi-factor authentication registration not configured</span><span class="sxs-lookup"><span data-stu-id="af702-109">Multi-factor authentication registration not configured</span></span>
<span data-ttu-id="af702-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span><span class="sxs-lookup"><span data-stu-id="af702-110">This vulnerability helps you control the deployment of Azure Multi-Factor Authentication in your organization.</span></span> 

<span data-ttu-id="af702-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span><span class="sxs-lookup"><span data-stu-id="af702-111">Azure multi-factor authentication provides a second layer of security to user authentication.</span></span> <span data-ttu-id="af702-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span><span class="sxs-lookup"><span data-stu-id="af702-112">It helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="af702-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span><span class="sxs-lookup"><span data-stu-id="af702-113">It delivers strong authentication via a range of easy verification options—phone call, text message, or mobile app notification or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="af702-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="af702-114">We recommend that you require Azure Multi-Factor Authentication for user sign-ins. Multi-factor authentication plays a key role in risk-based conditional access policies available through Identity Protection.</span></span>

<span data-ttu-id="af702-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="af702-115">For more details, see [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>

## <a name="unmanaged-cloud-apps"></a><span data-ttu-id="af702-116">Unmanaged cloud apps</span><span class="sxs-lookup"><span data-stu-id="af702-116">Unmanaged cloud apps</span></span>
<span data-ttu-id="af702-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span><span class="sxs-lookup"><span data-stu-id="af702-117">This vulnerability helps you identify unmanaged cloud apps in your organization.</span></span>

<span data-ttu-id="af702-118">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span><span class="sxs-lookup"><span data-stu-id="af702-118">In modern enterprises, IT departments are often unaware of all the cloud applications that users in their organization are using to do their work.</span></span> <span data-ttu-id="af702-119">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span><span class="sxs-lookup"><span data-stu-id="af702-119">It is easy to see why administrators would have concerns about unauthorized access to corporate data, possible data leakage and other security risks.</span></span> 

<span data-ttu-id="af702-120">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="af702-120">We recommend that your organization deploy Cloud App Discovery to discover unmanaged cloud applications, and to manage these applications using Azure Active Directory.</span></span>

<span data-ttu-id="af702-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="af702-121">For more details, see [Finding unmanaged cloud applications with Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>

## <a name="security-alerts-from-privileged-identity-management"></a><span data-ttu-id="af702-122">Security Alerts from Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="af702-122">Security Alerts from Privileged Identity Management</span></span>
<span data-ttu-id="af702-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span><span class="sxs-lookup"><span data-stu-id="af702-123">This vulnerability helps you discover and resolve alerts about privileged identities in your organization.</span></span>  

<span data-ttu-id="af702-124">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="af702-124">To enable users to carry out privileged operations, organizations need to grant users temporary or permanent privileged access in Azure AD, Azure or Office 365 resources, or other SaaS apps.</span></span> <span data-ttu-id="af702-125">Each of these privileged users increases the attack surface of your organization.</span><span class="sxs-lookup"><span data-stu-id="af702-125">Each of these privileged users increases the attack surface of your organization.</span></span> <span data-ttu-id="af702-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span><span class="sxs-lookup"><span data-stu-id="af702-126">This vulnerability helps you identify users with unnecessary privileged access, and take appropriate action to reduce or eliminate the risk they pose.</span></span> 

<span data-ttu-id="af702-127">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="af702-127">We recommend that your organization uses Azure AD Privileged Identity Management to manage, control, and monitor privileged identities and their access to resources in Azure AD as well as other Microsoft online services like Office 365 or Microsoft Intune.</span></span>

<span data-ttu-id="af702-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="af702-128">For more details, see [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="see-also"></a><span data-ttu-id="af702-129">See also</span><span class="sxs-lookup"><span data-stu-id="af702-129">See also</span></span>
* [<span data-ttu-id="af702-130">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="af702-130">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)


