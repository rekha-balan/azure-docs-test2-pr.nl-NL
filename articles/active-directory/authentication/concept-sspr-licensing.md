---
title: License Azure Active Directory self-service password
description: Azure AD self-service password reset licensing requirements
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: conceptual
ms.date: 07/17/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: sahenry
ms.openlocfilehash: 83054c505689768c14d168841764a4557c3e1f8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868667"
---
# <a name="licensing-requirements-for-azure-ad-self-service-password-reset"></a><span data-ttu-id="abeb9-103">Licensing requirements for Azure AD self-service password reset</span><span class="sxs-lookup"><span data-stu-id="abeb9-103">Licensing requirements for Azure AD self-service password reset</span></span>

<span data-ttu-id="abeb9-104">Azure Active Directory (Azure AD) comes in four editions: Free, Basic, Premium P1, and Premium P2.</span><span class="sxs-lookup"><span data-stu-id="abeb9-104">Azure Active Directory (Azure AD) comes in four editions: Free, Basic, Premium P1, and Premium P2.</span></span> <span data-ttu-id="abeb9-105">There are several different features that make up self-service password reset, including change, reset, unlock, and writeback, that are available in the different editions of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abeb9-105">There are several different features that make up self-service password reset, including change, reset, unlock, and writeback, that are available in the different editions of Azure AD.</span></span> <span data-ttu-id="abeb9-106">This article tries to explain the differences.</span><span class="sxs-lookup"><span data-stu-id="abeb9-106">This article tries to explain the differences.</span></span> <span data-ttu-id="abeb9-107">More details of the features included in each Azure AD edition can be found on the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="abeb9-107">More details of the features included in each Azure AD edition can be found on the [Azure Active Directory pricing page](https://azure.microsoft.com/pricing/details/active-directory/).</span></span>

## <a name="compare-editions-and-features"></a><span data-ttu-id="abeb9-108">Compare editions and features</span><span class="sxs-lookup"><span data-stu-id="abeb9-108">Compare editions and features</span></span>

<span data-ttu-id="abeb9-109">Azure AD self-service password reset is licensed per user, to maintain compliance organizations are required to assign the appropriate license to their users.</span><span class="sxs-lookup"><span data-stu-id="abeb9-109">Azure AD self-service password reset is licensed per user, to maintain compliance organizations are required to assign the appropriate license to their users.</span></span>

* <span data-ttu-id="abeb9-110">Self-Service Password Change for cloud users</span><span class="sxs-lookup"><span data-stu-id="abeb9-110">Self-Service Password Change for cloud users</span></span>
   * <span data-ttu-id="abeb9-111">I am a **cloud-only user** and know my password.</span><span class="sxs-lookup"><span data-stu-id="abeb9-111">I am a **cloud-only user** and know my password.</span></span>
      * <span data-ttu-id="abeb9-112">I would like to **change** my password to something new.</span><span class="sxs-lookup"><span data-stu-id="abeb9-112">I would like to **change** my password to something new.</span></span>
   * <span data-ttu-id="abeb9-113">This functionality is included in all editions of Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abeb9-113">This functionality is included in all editions of Azure AD.</span></span>

* <span data-ttu-id="abeb9-114">Self-Service Password Reset for cloud users</span><span class="sxs-lookup"><span data-stu-id="abeb9-114">Self-Service Password Reset for cloud users</span></span>
   * <span data-ttu-id="abeb9-115">I am a **cloud-only user** and have forgotten my password.</span><span class="sxs-lookup"><span data-stu-id="abeb9-115">I am a **cloud-only user** and have forgotten my password.</span></span>
      * <span data-ttu-id="abeb9-116">I would like to **reset** my password to something I know.</span><span class="sxs-lookup"><span data-stu-id="abeb9-116">I would like to **reset** my password to something I know.</span></span>
   * <span data-ttu-id="abeb9-117">This functionality is included in Azure AD Basic, Premium P1, or Premium P2 editions.</span><span class="sxs-lookup"><span data-stu-id="abeb9-117">This functionality is included in Azure AD Basic, Premium P1, or Premium P2 editions.</span></span>

* <span data-ttu-id="abeb9-118">Self-Service Password Reset/Change/Unlock **with on-premises writeback**</span><span class="sxs-lookup"><span data-stu-id="abeb9-118">Self-Service Password Reset/Change/Unlock **with on-premises writeback**</span></span>
   * <span data-ttu-id="abeb9-119">I am a **hybrid user** my on-premises Active Directory user account is synchronized with my Azure AD account using Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="abeb9-119">I am a **hybrid user** my on-premises Active Directory user account is synchronized with my Azure AD account using Azure AD Connect.</span></span> <span data-ttu-id="abeb9-120">I would like to change my password, have forgotten my password, or been locked out.</span><span class="sxs-lookup"><span data-stu-id="abeb9-120">I would like to change my password, have forgotten my password, or been locked out.</span></span>
      * <span data-ttu-id="abeb9-121">I would like to change my password or reset it to something I know, or unlock my account, **and** have that change synchronized back to on-premises Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abeb9-121">I would like to change my password or reset it to something I know, or unlock my account, **and** have that change synchronized back to on-premises Active Directory.</span></span>
   * <span data-ttu-id="abeb9-122">This functionality is included in Azure AD Premium P1, or Premium P2 editions.</span><span class="sxs-lookup"><span data-stu-id="abeb9-122">This functionality is included in Azure AD Premium P1, or Premium P2 editions.</span></span>

> [!WARNING]
> <span data-ttu-id="abeb9-123">Standalone Office 365 licensing plans **don't support password writeback** and require Azure AD Premium P1, or Premium P2 editions for this functionality to work.</span><span class="sxs-lookup"><span data-stu-id="abeb9-123">Standalone Office 365 licensing plans **don't support password writeback** and require Azure AD Premium P1, or Premium P2 editions for this functionality to work.</span></span>
>

<span data-ttu-id="abeb9-124">Additional licensing information, including costs, can be found on the following pages:</span><span class="sxs-lookup"><span data-stu-id="abeb9-124">Additional licensing information, including costs, can be found on the following pages:</span></span>

* [<span data-ttu-id="abeb9-125">Azure Active Directory pricing site</span><span class="sxs-lookup"><span data-stu-id="abeb9-125">Azure Active Directory pricing site</span></span>](https://azure.microsoft.com/pricing/details/active-directory/)
* [<span data-ttu-id="abeb9-126">Azure Active Directory features and capabilities</span><span class="sxs-lookup"><span data-stu-id="abeb9-126">Azure Active Directory features and capabilities</span></span>](https://www.microsoft.com/cloud-platform/azure-active-directory-features)
* [<span data-ttu-id="abeb9-127">Enterprise Mobility + Security</span><span class="sxs-lookup"><span data-stu-id="abeb9-127">Enterprise Mobility + Security</span></span>](https://www.microsoft.com/cloud-platform/enterprise-mobility-security)
* [<span data-ttu-id="abeb9-128">Microsoft 365 Enterprise</span><span class="sxs-lookup"><span data-stu-id="abeb9-128">Microsoft 365 Enterprise</span></span>](https://www.microsoft.com/microsoft-365/enterprise)

## <a name="enable-group-or-user-based-licensing"></a><span data-ttu-id="abeb9-129">Enable group or user-based licensing</span><span class="sxs-lookup"><span data-stu-id="abeb9-129">Enable group or user-based licensing</span></span>

<span data-ttu-id="abeb9-130">Azure AD now supports group-based licensing.</span><span class="sxs-lookup"><span data-stu-id="abeb9-130">Azure AD now supports group-based licensing.</span></span> <span data-ttu-id="abeb9-131">Administrators can assign licenses in bulk to a group of users, rather than assigning them one at a time.</span><span class="sxs-lookup"><span data-stu-id="abeb9-131">Administrators can assign licenses in bulk to a group of users, rather than assigning them one at a time.</span></span> <span data-ttu-id="abeb9-132">For more information, see [Assign, verify, and resolve problems with licenses](../users-groups-roles/licensing-groups-assign.md#step-1-assign-the-required-licenses).</span><span class="sxs-lookup"><span data-stu-id="abeb9-132">For more information, see [Assign, verify, and resolve problems with licenses](../users-groups-roles/licensing-groups-assign.md#step-1-assign-the-required-licenses).</span></span>

<span data-ttu-id="abeb9-133">Some Microsoft services are not available in all locations.</span><span class="sxs-lookup"><span data-stu-id="abeb9-133">Some Microsoft services are not available in all locations.</span></span> <span data-ttu-id="abeb9-134">Before a license can be assigned to a user, the administrator must specify the **Usage location** property on the user.</span><span class="sxs-lookup"><span data-stu-id="abeb9-134">Before a license can be assigned to a user, the administrator must specify the **Usage location** property on the user.</span></span> <span data-ttu-id="abeb9-135">Assignment of licenses can be done under the **User** > **Profile** > **Settings** section in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="abeb9-135">Assignment of licenses can be done under the **User** > **Profile** > **Settings** section in the Azure portal.</span></span> <span data-ttu-id="abeb9-136">*When you use group license assignment, any users without a usage location specified inherit the location of the directory.*</span><span class="sxs-lookup"><span data-stu-id="abeb9-136">*When you use group license assignment, any users without a usage location specified inherit the location of the directory.*</span></span>

## <a name="next-steps"></a><span data-ttu-id="abeb9-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="abeb9-137">Next steps</span></span>

* [<span data-ttu-id="abeb9-138">How do I complete a successful rollout of SSPR?</span><span class="sxs-lookup"><span data-stu-id="abeb9-138">How do I complete a successful rollout of SSPR?</span></span>](howto-sspr-deployment.md)
* [<span data-ttu-id="abeb9-139">Reset or change your password</span><span class="sxs-lookup"><span data-stu-id="abeb9-139">Reset or change your password</span></span>](../user-help/active-directory-passwords-update-your-own-password.md)
* [<span data-ttu-id="abeb9-140">Register for self-service password reset</span><span class="sxs-lookup"><span data-stu-id="abeb9-140">Register for self-service password reset</span></span>](../user-help/active-directory-passwords-reset-register.md)
* [<span data-ttu-id="abeb9-141">What data is used by SSPR and what data should you populate for your users?</span><span class="sxs-lookup"><span data-stu-id="abeb9-141">What data is used by SSPR and what data should you populate for your users?</span></span>](howto-sspr-authenticationdata.md)
* [<span data-ttu-id="abeb9-142">What authentication methods are available to users?</span><span class="sxs-lookup"><span data-stu-id="abeb9-142">What authentication methods are available to users?</span></span>](concept-sspr-howitworks.md#authentication-methods)
* [<span data-ttu-id="abeb9-143">What are the policy options with SSPR?</span><span class="sxs-lookup"><span data-stu-id="abeb9-143">What are the policy options with SSPR?</span></span>](concept-sspr-policy.md)
* [<span data-ttu-id="abeb9-144">What is password writeback and why do I care about it?</span><span class="sxs-lookup"><span data-stu-id="abeb9-144">What is password writeback and why do I care about it?</span></span>](howto-sspr-writeback.md)
* [<span data-ttu-id="abeb9-145">How do I report on activity in SSPR?</span><span class="sxs-lookup"><span data-stu-id="abeb9-145">How do I report on activity in SSPR?</span></span>](howto-sspr-reporting.md)
* [<span data-ttu-id="abeb9-146">What are all of the options in SSPR and what do they mean?</span><span class="sxs-lookup"><span data-stu-id="abeb9-146">What are all of the options in SSPR and what do they mean?</span></span>](concept-sspr-howitworks.md)
* [<span data-ttu-id="abeb9-147">I think something is broken. How do I troubleshoot SSPR?</span><span class="sxs-lookup"><span data-stu-id="abeb9-147">I think something is broken. How do I troubleshoot SSPR?</span></span>](active-directory-passwords-troubleshoot.md)
* [<span data-ttu-id="abeb9-148">I have a question that was not covered somewhere else</span><span class="sxs-lookup"><span data-stu-id="abeb9-148">I have a question that was not covered somewhere else</span></span>](active-directory-passwords-faq.md)
