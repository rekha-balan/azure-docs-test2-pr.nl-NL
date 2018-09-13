---
title: Securing Privileged Access in Azure AD | Microsoft Docs
description: A topic that explains the approaches for securing privileged access across Azure, Azure Active Directory and Microsoft Online Services.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: mwahl
ms.assetid: 235a0ce9-1daf-4433-8f65-9c6afcd64d08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: kgremban
ms.openlocfilehash: 39286f2d39e8226634557cae59fdf284323dd5f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550704"
---
# <a name="securing-privileged-access-in-azure-ad"></a><span data-ttu-id="cb4e9-103">Securing privileged access in Azure AD</span><span class="sxs-lookup"><span data-stu-id="cb4e9-103">Securing privileged access in Azure AD</span></span>
<span data-ttu-id="cb4e9-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-104">Securing privileged access is a critical first step to help protect business assets in a modern organization.</span></span> <span data-ttu-id="cb4e9-105">Privileged accounts are those that administer and manage IT systems.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-105">Privileged accounts are those that administer and manage IT systems.</span></span> <span data-ttu-id="cb4e9-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-106">Cyber-attackers target these accounts to gain access to an organization’s data and systems.</span></span> <span data-ttu-id="cb4e9-107">In order to secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-107">In order to secure privileged access, you should isolate the accounts and systems from the risk of being exposed to a malicious user.</span></span>

<span data-ttu-id="cb4e9-108">More users are starting to get privileged access through cloud services.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-108">More users are starting to get privileged access through cloud services.</span></span> <span data-ttu-id="cb4e9-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-109">This can include global administrators of Office365, Azure subscription administrators, and users who have administrative access in VMs or on SaaS apps.</span></span>

<span data-ttu-id="cb4e9-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb4e9-110">Microsoft recommends you follow this roadmap on [Securing Privileged Access](https://technet.microsoft.com/library/mt631194.aspx).</span></span>

<span data-ttu-id="cb4e9-111">For customers using Azure Active Directory to manage access to Azure, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-111">For customers using Azure Active Directory to manage access to Azure, Office 365, or other Microsoft services and applications, these principles apply whether user accounts are managed and authenticated by Active Directory or in Azure Active Directory.</span></span> <span data-ttu-id="cb4e9-112">The following sections provide more information on Azure AD features to support securing privileged access.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-112">The following sections provide more information on Azure AD features to support securing privileged access.</span></span>

## <a name="multi-factor-authentication"></a><span data-ttu-id="cb4e9-113">Multi-factor authentication</span><span class="sxs-lookup"><span data-stu-id="cb4e9-113">Multi-factor authentication</span></span>
<span data-ttu-id="cb4e9-114">To increase the security of administrator authentication, you should require multi-factor authentication (MFA) before granting privileges.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-114">To increase the security of administrator authentication, you should require multi-factor authentication (MFA) before granting privileges.</span></span> <span data-ttu-id="cb4e9-115">MFA is a method of verifying who you are that requires the use of more than just a username and password.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-115">MFA is a method of verifying who you are that requires the use of more than just a username and password.</span></span> <span data-ttu-id="cb4e9-116">It provides a second layer of security to user sign-ins and transactions.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-116">It provides a second layer of security to user sign-ins and transactions.</span></span>

<span data-ttu-id="cb4e9-117">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-117">Azure Multi-Factor Authentication helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="cb4e9-118">It delivers strong authentication via a range of easy verification options including phone calls, text messages, mobile app notifications, or verification code and 3rd party OATH tokens.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-118">It delivers strong authentication via a range of easy verification options including phone calls, text messages, mobile app notifications, or verification code and 3rd party OATH tokens.</span></span>

<span data-ttu-id="cb4e9-119">For an overview of how Azure Multi-Factor Authentication works see the following video.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-119">For an overview of how Azure Multi-Factor Authentication works see the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]
> 
> 

<span data-ttu-id="cb4e9-120">For more details, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span><span class="sxs-lookup"><span data-stu-id="cb4e9-120">For more details, see [MFA for Office 365 and MFA for Azure](https://blogs.technet.microsoft.com/ad/2014/02/11/mfa-for-office-365-and-mfa-for-azure/).</span></span>

## <a name="time-bound-privileges"></a><span data-ttu-id="cb4e9-121">Time-bound privileges</span><span class="sxs-lookup"><span data-stu-id="cb4e9-121">Time-bound privileges</span></span>
<span data-ttu-id="cb4e9-122">Some organizations may find that they have too many users in highly privileged roles.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-122">Some organizations may find that they have too many users in highly privileged roles.</span></span> <span data-ttu-id="cb4e9-123">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-123">A user might have been added to the role for a particular activity, like to sign up for a service, but didn't use those privileges frequently afterward.</span></span>

<span data-ttu-id="cb4e9-124">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges Just in Time (JIT), when they need to perform a task.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-124">To lower the exposure time of privileges and increase your visibility into their use, limit users to only taking on their privileges Just in Time (JIT), when they need to perform a task.</span></span> <span data-ttu-id="cb4e9-125">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span><span class="sxs-lookup"><span data-stu-id="cb4e9-125">For Azure Active Directory and Microsoft Online Services, you can use [Azure AD Privileged Identity Management (PIM)](http://aka.ms/AzurePIM).</span></span>

![PIM dashboard][2]

## <a name="attack-detection"></a><span data-ttu-id="cb4e9-127">Attack detection</span><span class="sxs-lookup"><span data-stu-id="cb4e9-127">Attack detection</span></span>
<span data-ttu-id="cb4e9-128">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-128">[Azure Active Directory Identity Protection](../active-directory-identityprotection.md) provides a consolidated view into risk events and potential vulnerabilities affecting your organization’s identities.</span></span> <span data-ttu-id="cb4e9-129">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-129">Based on risk events, Identity Protection calculates a user risk level for each user, enabling you to configure risk-based policies to automatically protect the identities of your organization.</span></span> <span data-ttu-id="cb4e9-130">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-130">These policies, along with other conditional access controls provided by Azure Active Directory and EMS, can automatically block the user or offer suggestions that include password resets and multi-factor authentication enforcement.</span></span>

![Azure AD Identity Protection][3]

## <a name="conditional-access"></a><span data-ttu-id="cb4e9-132">Conditional access</span><span class="sxs-lookup"><span data-stu-id="cb4e9-132">Conditional access</span></span>
<span data-ttu-id="cb4e9-133">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-133">With conditional access control, Azure Active Directory checks the specific conditions you choose when authenticating a user, before allowing access to an application.</span></span> <span data-ttu-id="cb4e9-134">Once those conditions are met, the user is authenticated and allowed access to the application.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-134">Once those conditions are met, the user is authenticated and allowed access to the application.</span></span>

![Setting conditional access rules with MFA][4]

## <a name="related-articles"></a><span data-ttu-id="cb4e9-136">Related articles</span><span class="sxs-lookup"><span data-stu-id="cb4e9-136">Related articles</span></span>
* <span data-ttu-id="cb4e9-137">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span><span class="sxs-lookup"><span data-stu-id="cb4e9-137">Enable [Azure Multi-Factor Authentication](../../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)</span></span>
* <span data-ttu-id="cb4e9-138">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span><span class="sxs-lookup"><span data-stu-id="cb4e9-138">Enable [Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-configure.md)</span></span>
* <span data-ttu-id="cb4e9-139">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span><span class="sxs-lookup"><span data-stu-id="cb4e9-139">Enable [Azure AD Identity Protection](../active-directory-identityprotection.md)</span></span>
* <span data-ttu-id="cb4e9-140">Enable [conditional access controls](../active-directory-conditional-access.md)</span><span class="sxs-lookup"><span data-stu-id="cb4e9-140">Enable [conditional access controls](../active-directory-conditional-access.md)</span></span>

<span data-ttu-id="cb4e9-141">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span><span class="sxs-lookup"><span data-stu-id="cb4e9-141">For more information on building a complete security roadmap, see the “Customer responsibilities and roadmap” section of the [Microsoft Cloud Security for Enterprise Architects](http://aka.ms/securecustomer) document.</span></span> <span data-ttu-id="cb4e9-142">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/microsoftservices/campaigns/cybersecurity-protection.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb4e9-142">For more information on engaging Microsoft services to assist with any of these topics, contact your Microsoft representative or visit our [Cybersecurity solutions page](https://www.microsoft.com/microsoftservices/campaigns/cybersecurity-protection.aspx).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/Search_PIM.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-privileged-identity-management-configure/PIM_Dash.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-identityprotection/29.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-conditional-access/conditionalaccess-saas-apps.png




