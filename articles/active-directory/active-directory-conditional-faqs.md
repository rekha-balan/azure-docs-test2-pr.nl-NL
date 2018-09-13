---
title: Azure Active Directory Conditional Access FAQ | Microsoft Docs
description: 'Frequently asked questions about conditional access '
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/11/2017
ms.author: markvi
ms.openlocfilehash: dee29df176389f39907d302cedc6143c0d3e3322
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563603"
---
# <a name="azure-active-directory-conditional-access-faq"></a><span data-ttu-id="694fc-103">Azure Active Directory Conditional Access FAQ</span><span class="sxs-lookup"><span data-stu-id="694fc-103">Azure Active Directory Conditional Access FAQ</span></span>

## <a name="which-applications-work-with-conditional-access-policies"></a><span data-ttu-id="694fc-104">Which applications work with conditional access policies?</span><span class="sxs-lookup"><span data-stu-id="694fc-104">Which applications work with conditional access policies?</span></span>

<span data-ttu-id="694fc-105">**A:** Please see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span><span class="sxs-lookup"><span data-stu-id="694fc-105">**A:** Please see [Applications and browsers that use conditional access rules in Azure Active Directory](active-directory-conditional-access-supported-apps.md).</span></span>

---

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a><span data-ttu-id="694fc-106">Are conditional access policies enforced for B2B collaboration and guest users?</span><span class="sxs-lookup"><span data-stu-id="694fc-106">Are conditional access policies enforced for B2B collaboration and guest users?</span></span>
<span data-ttu-id="694fc-107">**A:** Policies are enforced for B2B collaboration users.</span><span class="sxs-lookup"><span data-stu-id="694fc-107">**A:** Policies are enforced for B2B collaboration users.</span></span> <span data-ttu-id="694fc-108">However, in some cases, a user might not be able to satisfy the policy requirement if, for example, an organization does not support multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="694fc-108">However, in some cases, a user might not be able to satisfy the policy requirement if, for example, an organization does not support multi-factor authentication.</span></span> <span data-ttu-id="694fc-109">The policy is currently not enforced for SharePoint guest users.</span><span class="sxs-lookup"><span data-stu-id="694fc-109">The policy is currently not enforced for SharePoint guest users.</span></span> <span data-ttu-id="694fc-110">The guest relationship is maintained within SharePoint.</span><span class="sxs-lookup"><span data-stu-id="694fc-110">The guest relationship is maintained within SharePoint.</span></span> <span data-ttu-id="694fc-111">Guest users accounts are not subject to access polices at the authentication server.</span><span class="sxs-lookup"><span data-stu-id="694fc-111">Guest users accounts are not subject to access polices at the authentication server.</span></span> <span data-ttu-id="694fc-112">Guest access can be managed at SharePoint.</span><span class="sxs-lookup"><span data-stu-id="694fc-112">Guest access can be managed at SharePoint.</span></span>

---

## <a name="does-a-sharepoint-online-policy-also-apply-to-onedrive-for-business"></a><span data-ttu-id="694fc-113">Does a SharePoint Online policy also apply to OneDrive for Business?</span><span class="sxs-lookup"><span data-stu-id="694fc-113">Does a SharePoint Online policy also apply to OneDrive for Business?</span></span>
<span data-ttu-id="694fc-114">**A:** Yes.</span><span class="sxs-lookup"><span data-stu-id="694fc-114">**A:** Yes.</span></span>

---

## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a><span data-ttu-id="694fc-115">Why can’t I set a policy on client apps, like Word or Outlook?</span><span class="sxs-lookup"><span data-stu-id="694fc-115">Why can’t I set a policy on client apps, like Word or Outlook?</span></span>
<span data-ttu-id="694fc-116">**A:** A conditional access policy sets requirements for accessing a service and is enforced when authentication happens to that service.</span><span class="sxs-lookup"><span data-stu-id="694fc-116">**A:** A conditional access policy sets requirements for accessing a service and is enforced when authentication happens to that service.</span></span> <span data-ttu-id="694fc-117">The policy is not set directly on a client application; instead, it is applied when it calls into a service.</span><span class="sxs-lookup"><span data-stu-id="694fc-117">The policy is not set directly on a client application; instead, it is applied when it calls into a service.</span></span> <span data-ttu-id="694fc-118">For example, a policy set on SharePoint applies to clients calling SharePoint and a policy set on Exchange applies to Outlook.</span><span class="sxs-lookup"><span data-stu-id="694fc-118">For example, a policy set on SharePoint applies to clients calling SharePoint and a policy set on Exchange applies to Outlook.</span></span>

--- 

## <a name="does-a-conditional-access-policy-apply-to-service-accounts"></a><span data-ttu-id="694fc-119">Does a conditional access policy apply to service accounts?</span><span class="sxs-lookup"><span data-stu-id="694fc-119">Does a conditional access policy apply to service accounts?</span></span>
<span data-ttu-id="694fc-120">**A:** Conditional access policies apply to all user accounts.</span><span class="sxs-lookup"><span data-stu-id="694fc-120">**A:** Conditional access policies apply to all user accounts.</span></span> <span data-ttu-id="694fc-121">This includes user accounts used as service accounts.</span><span class="sxs-lookup"><span data-stu-id="694fc-121">This includes user accounts used as service accounts.</span></span> <span data-ttu-id="694fc-122">In many cases, a service account that runs unattended is not able to satisfy a policy.</span><span class="sxs-lookup"><span data-stu-id="694fc-122">In many cases, a service account that runs unattended is not able to satisfy a policy.</span></span> <span data-ttu-id="694fc-123">This is, for example the case, when MFA is required.</span><span class="sxs-lookup"><span data-stu-id="694fc-123">This is, for example the case, when MFA is required.</span></span> <span data-ttu-id="694fc-124">In these cases, services accounts can be excluded from a policy, using conditional access policy management settings.</span><span class="sxs-lookup"><span data-stu-id="694fc-124">In these cases, services accounts can be excluded from a policy, using conditional access policy management settings.</span></span> <span data-ttu-id="694fc-125">Learn more about applying a policy to users here.</span><span class="sxs-lookup"><span data-stu-id="694fc-125">Learn more about applying a policy to users here.</span></span>

---

## <a name="are-graph-apis-available-to-configure-configure-conditional-access-policies"></a><span data-ttu-id="694fc-126">Are Graph APIs available to configure configure conditional access policies?</span><span class="sxs-lookup"><span data-stu-id="694fc-126">Are Graph APIs available to configure configure conditional access policies?</span></span>
<span data-ttu-id="694fc-127">**A:** not yet.</span><span class="sxs-lookup"><span data-stu-id="694fc-127">**A:** not yet.</span></span> 

---