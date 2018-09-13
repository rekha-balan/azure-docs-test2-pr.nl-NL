---
title: Azure Active Directory conditional access FAQs | Microsoft Docs
description: Get answers to frequently asked questions about conditional access in Azure Active Directory.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: mtillman
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.component: conditional-access
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2018
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: e9ce5e1d86f6c1756f8871dc45d60d36cea74515
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866868"
---
# <a name="azure-active-directory-conditional-access-faqs"></a><span data-ttu-id="70190-103">Azure Active Directory conditional access FAQs</span><span class="sxs-lookup"><span data-stu-id="70190-103">Azure Active Directory conditional access FAQs</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="70190-104">Which applications work with conditional access policies?</span><span class="sxs-lookup"><span data-stu-id="70190-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="70190-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](technical-reference.md).</span><span class="sxs-lookup"><span data-stu-id="70190-105">For information about applications that work with conditional access policies, see [Applications and browsers that use conditional access rules in Azure Active Directory](technical-reference.md).</span></span>

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="70190-106">Are conditional access policies enforced for B2B collaboration and guest users?</span><span class="sxs-lookup"><span data-stu-id="70190-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>

<span data-ttu-id="70190-107">Policies are enforced for business-to-business (B2B) collaboration users.</span><span class="sxs-lookup"><span data-stu-id="70190-107">Policies are enforced for business-to-business (B2B) collaboration users.</span></span> <span data-ttu-id="70190-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span><span class="sxs-lookup"><span data-stu-id="70190-108">However, in some cases, a user might not be able to satisfy the policy requirements.</span></span> <span data-ttu-id="70190-109">For example, a guest user's organization might not support multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="70190-109">For example, a guest user's organization might not support multi-factor authentication.</span></span> 



## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="70190-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span><span class="sxs-lookup"><span data-stu-id="70190-110">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>

<span data-ttu-id="70190-111">Yes.</span><span class="sxs-lookup"><span data-stu-id="70190-111">Yes.</span></span> <span data-ttu-id="70190-112">A SharePoint Online policy also applies to OneDrive for Business.</span><span class="sxs-lookup"><span data-stu-id="70190-112">A SharePoint Online policy also applies to OneDrive for Business.</span></span>


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="70190-113">Why can’t I set a policy on client apps, like Word or Outlook?</span><span class="sxs-lookup"><span data-stu-id="70190-113">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>

<span data-ttu-id="70190-114">A conditional access policy sets requirements for accessing a service.</span><span class="sxs-lookup"><span data-stu-id="70190-114">A conditional access policy sets requirements for accessing a service.</span></span> <span data-ttu-id="70190-115">It's enforced when authentication to that service occurs.</span><span class="sxs-lookup"><span data-stu-id="70190-115">It's enforced when authentication to that service occurs.</span></span> <span data-ttu-id="70190-116">The policy is not set directly on a client application.</span><span class="sxs-lookup"><span data-stu-id="70190-116">The policy is not set directly on a client application.</span></span> <span data-ttu-id="70190-117">Instead, it is applied when a client calls a service.</span><span class="sxs-lookup"><span data-stu-id="70190-117">Instead, it is applied when a client calls a service.</span></span> <span data-ttu-id="70190-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span><span class="sxs-lookup"><span data-stu-id="70190-118">For example, a policy set on SharePoint applies to clients calling SharePoint.</span></span> <span data-ttu-id="70190-119">A policy set on Exchange applies to Outlook.</span><span class="sxs-lookup"><span data-stu-id="70190-119">A policy set on Exchange applies to Outlook.</span></span>

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="70190-120">Does a conditional access policy apply to service accounts?</span><span class="sxs-lookup"><span data-stu-id="70190-120">Does a conditional access policy apply to service accounts?</span></span>

<span data-ttu-id="70190-121">Conditional access policies apply to all user accounts.</span><span class="sxs-lookup"><span data-stu-id="70190-121">Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="70190-122">This includes user accounts that are used as service accounts.</span><span class="sxs-lookup"><span data-stu-id="70190-122">This includes user accounts that are used as service accounts.</span></span> <span data-ttu-id="70190-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="70190-123">Often, a service account that runs unattended can't satisfy the requirements of a conditional access policy.</span></span> <span data-ttu-id="70190-124">For example, multi-factor authentication might be required.</span><span class="sxs-lookup"><span data-stu-id="70190-124">For example, multi-factor authentication might be required.</span></span> <span data-ttu-id="70190-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span><span class="sxs-lookup"><span data-stu-id="70190-125">Service accounts can be excluded from a policy by using conditional access policy management settings.</span></span> 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a><span data-ttu-id="70190-126">Are Graph APIs available for configuring conditional access policies?</span><span class="sxs-lookup"><span data-stu-id="70190-126">Are Graph APIs available for configuring conditional access policies?</span></span>

<span data-ttu-id="70190-127">Currently, no.</span><span class="sxs-lookup"><span data-stu-id="70190-127">Currently, no.</span></span> 

## <a name="what-is-the-default-exclusion-policy-for-unsupported-device-platforms"></a><span data-ttu-id="70190-128">What is the default exclusion policy for unsupported device platforms?</span><span class="sxs-lookup"><span data-stu-id="70190-128">What is the default exclusion policy for unsupported device platforms?</span></span>

<span data-ttu-id="70190-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span><span class="sxs-lookup"><span data-stu-id="70190-129">Currently, conditional access policies are selectively enforced on users of iOS and Android devices.</span></span> <span data-ttu-id="70190-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span><span class="sxs-lookup"><span data-stu-id="70190-130">Applications on other device platforms are, by default, not affected by the conditional access policy for iOS and Android devices.</span></span> <span data-ttu-id="70190-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span><span class="sxs-lookup"><span data-stu-id="70190-131">A tenant admin can choose to override the global policy to disallow access to users on platforms that are not supported.</span></span>


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a><span data-ttu-id="70190-132">How do conditional access policies work for Microsoft Teams?</span><span class="sxs-lookup"><span data-stu-id="70190-132">How do conditional access policies work for Microsoft Teams?</span></span>

<span data-ttu-id="70190-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span><span class="sxs-lookup"><span data-stu-id="70190-133">Microsoft Teams relies heavily on Exchange Online and SharePoint Online for core productivity scenarios, like meetings, calendars, and file sharing.</span></span> <span data-ttu-id="70190-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs directly into Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="70190-134">Conditional access policies that are set for these cloud apps apply to Microsoft Teams when a user signs directly into Microsoft Teams.</span></span>

<span data-ttu-id="70190-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span><span class="sxs-lookup"><span data-stu-id="70190-135">Microsoft Teams also is supported separately as a cloud app in Azure Active Directory conditional access policies.</span></span> <span data-ttu-id="70190-136">Conditional access policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span><span class="sxs-lookup"><span data-stu-id="70190-136">Conditional access policies that are set for a cloud app apply to Microsoft Teams when a user signs in.</span></span> <span data-ttu-id="70190-137">However, without the correct policies on other apps like Exchange Online and SharePoint Online users may still be able to access those resources directly.</span><span class="sxs-lookup"><span data-stu-id="70190-137">However, without the correct policies on other apps like Exchange Online and SharePoint Online users may still be able to access those resources directly.</span></span>

<span data-ttu-id="70190-138">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span><span class="sxs-lookup"><span data-stu-id="70190-138">Microsoft Teams desktop clients for Windows and Mac support modern authentication.</span></span> <span data-ttu-id="70190-139">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span><span class="sxs-lookup"><span data-stu-id="70190-139">Modern authentication brings sign-in based on the Azure Active Directory Authentication Library (ADAL) to Microsoft Office client applications across platforms.</span></span>