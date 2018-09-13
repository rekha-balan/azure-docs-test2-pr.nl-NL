---
title: Azure Active Directory hybrid identity design considerations - determine incident rResponse requirements | Microsoft Docs
description: Determine monitoring and reporting capabilities for the hybrid identity solution that can be leveraged by IT to take actions to identify and mitigate a potential threats
documentationcenter: ''
services: active-directory
author: billmath
manager: femila
editor: ''
ms.assetid: a3d2a459-599b-4b67-8e51-7369ee25082d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: b40151d084230d453e72604db7e8dbf37e849824
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563120"
---
# <a name="determine-incident-response-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="e077f-103">Determine incident response requirements for your hybrid identity solution</span><span class="sxs-lookup"><span data-stu-id="e077f-103">Determine incident response requirements for your hybrid identity solution</span></span>
<span data-ttu-id="e077f-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place to help IT take actions accordingly to the level of incident.</span><span class="sxs-lookup"><span data-stu-id="e077f-104">Large or medium organizations most likely will have a [security incident response](https://technet.microsoft.com/library/cc700825.aspx) in place to help IT take actions accordingly to the level of incident.</span></span> <span data-ttu-id="e077f-105">The identity management system is an important component in the incident response process because it can be used to help identifying who performed a specific action against the target.</span><span class="sxs-lookup"><span data-stu-id="e077f-105">The identity management system is an important component in the incident response process because it can be used to help identifying who performed a specific action against the target.</span></span> <span data-ttu-id="e077f-106">The hybrid identity solution must be able to provide monitoring and reporting capabilities that can be leveraged by IT to take actions to identify and mitigate a potential threat.</span><span class="sxs-lookup"><span data-stu-id="e077f-106">The hybrid identity solution must be able to provide monitoring and reporting capabilities that can be leveraged by IT to take actions to identify and mitigate a potential threat.</span></span> <span data-ttu-id="e077f-107">In a typical incident response plan you will have the following phases as part of the plan:</span><span class="sxs-lookup"><span data-stu-id="e077f-107">In a typical incident response plan you will have the following phases as part of the plan:</span></span>

1. <span data-ttu-id="e077f-108">Initial assessment.</span><span class="sxs-lookup"><span data-stu-id="e077f-108">Initial assessment.</span></span>
2. <span data-ttu-id="e077f-109">Incident communication.</span><span class="sxs-lookup"><span data-stu-id="e077f-109">Incident communication.</span></span>
3. <span data-ttu-id="e077f-110">Damage control and risk reduction.</span><span class="sxs-lookup"><span data-stu-id="e077f-110">Damage control and risk reduction.</span></span>
4. <span data-ttu-id="e077f-111">Identification of what it was compromise and severity.</span><span class="sxs-lookup"><span data-stu-id="e077f-111">Identification of what it was compromise and severity.</span></span>
5. <span data-ttu-id="e077f-112">Evidence preservation.</span><span class="sxs-lookup"><span data-stu-id="e077f-112">Evidence preservation.</span></span>
6. <span data-ttu-id="e077f-113">Notification to appropriate parties.</span><span class="sxs-lookup"><span data-stu-id="e077f-113">Notification to appropriate parties.</span></span>
7. <span data-ttu-id="e077f-114">System recovery.</span><span class="sxs-lookup"><span data-stu-id="e077f-114">System recovery.</span></span>
8. <span data-ttu-id="e077f-115">Documentation.</span><span class="sxs-lookup"><span data-stu-id="e077f-115">Documentation.</span></span>
9. <span data-ttu-id="e077f-116">Damage and cost assessment.</span><span class="sxs-lookup"><span data-stu-id="e077f-116">Damage and cost assessment.</span></span>
10. <span data-ttu-id="e077f-117">Process and plan revision.</span><span class="sxs-lookup"><span data-stu-id="e077f-117">Process and plan revision.</span></span>

<span data-ttu-id="e077f-118">During the identification of what it was compromise and severity- phase, it will be necessary to identify the systems that have been compromised, files that have been accessed and determine the sensitivity of those files.</span><span class="sxs-lookup"><span data-stu-id="e077f-118">During the identification of what it was compromise and severity- phase, it will be necessary to identify the systems that have been compromised, files that have been accessed and determine the sensitivity of those files.</span></span> <span data-ttu-id="e077f-119">Your hybrid identity system should be able to fulfill these requirements to assist you identifying the user that made those changes.</span><span class="sxs-lookup"><span data-stu-id="e077f-119">Your hybrid identity system should be able to fulfill these requirements to assist you identifying the user that made those changes.</span></span> 

## <a name="monitoring-and-reporting"></a><span data-ttu-id="e077f-120">Monitoring and reporting</span><span class="sxs-lookup"><span data-stu-id="e077f-120">Monitoring and reporting</span></span>
<span data-ttu-id="e077f-121">Many times the identity system can also help in initial assessment phase mainly if the system has built in auditing and reporting capabilities.</span><span class="sxs-lookup"><span data-stu-id="e077f-121">Many times the identity system can also help in initial assessment phase mainly if the system has built in auditing and reporting capabilities.</span></span> <span data-ttu-id="e077f-122">During the initial assessment, IT Admin must be able to identify a suspicious activity, or the system should be able to trigger it automatically based on a pre-configured task.</span><span class="sxs-lookup"><span data-stu-id="e077f-122">During the initial assessment, IT Admin must be able to identify a suspicious activity, or the system should be able to trigger it automatically based on a pre-configured task.</span></span> <span data-ttu-id="e077f-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead to a number of false positives in an intrusion detection system.</span><span class="sxs-lookup"><span data-stu-id="e077f-123">Many activities could indicate a possible attack, however in other cases, a badly configured system might lead to a number of false positives in an intrusion detection system.</span></span> 

<span data-ttu-id="e077f-124">The identity management system should assist IT admins to identify and report those suspicious activities.</span><span class="sxs-lookup"><span data-stu-id="e077f-124">The identity management system should assist IT admins to identify and report those suspicious activities.</span></span> <span data-ttu-id="e077f-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span><span class="sxs-lookup"><span data-stu-id="e077f-125">Usually these technical requirements can be fulfilled by monitoring all systems and having a reporting capability that can highlight potential threats.</span></span> <span data-ttu-id="e077f-126">Use the questions below to help you design your hybrid identity solution while taking into consideration incident response requirements:</span><span class="sxs-lookup"><span data-stu-id="e077f-126">Use the questions below to help you design your hybrid identity solution while taking into consideration incident response requirements:</span></span>

* <span data-ttu-id="e077f-127">Does your company has a security incident response in place?</span><span class="sxs-lookup"><span data-stu-id="e077f-127">Does your company has a security incident response in place?</span></span>
  * <span data-ttu-id="e077f-128">If yes, is the current identity management system used as part of the process?</span><span class="sxs-lookup"><span data-stu-id="e077f-128">If yes, is the current identity management system used as part of the process?</span></span>
* <span data-ttu-id="e077f-129">Does your company need to identify suspicious sign-on attempts from users across different devices?</span><span class="sxs-lookup"><span data-stu-id="e077f-129">Does your company need to identify suspicious sign-on attempts from users across different devices?</span></span>
* <span data-ttu-id="e077f-130">Does your company need to detect potential compromised user’s credentials?</span><span class="sxs-lookup"><span data-stu-id="e077f-130">Does your company need to detect potential compromised user’s credentials?</span></span>
* <span data-ttu-id="e077f-131">Does your company need to audit user’s access and action?</span><span class="sxs-lookup"><span data-stu-id="e077f-131">Does your company need to audit user’s access and action?</span></span>
* <span data-ttu-id="e077f-132">Does your company need to know when a user reset his password?</span><span class="sxs-lookup"><span data-stu-id="e077f-132">Does your company need to know when a user reset his password?</span></span>

## <a name="policy-enforcement"></a><span data-ttu-id="e077f-133">Policy enforcement</span><span class="sxs-lookup"><span data-stu-id="e077f-133">Policy enforcement</span></span>
<span data-ttu-id="e077f-134">During damage control and risk reduction-phase, it is important to quickly reduce the actual and potential effects of an attack.</span><span class="sxs-lookup"><span data-stu-id="e077f-134">During damage control and risk reduction-phase, it is important to quickly reduce the actual and potential effects of an attack.</span></span> <span data-ttu-id="e077f-135">That action that you will take at this point can make the difference between a minor and a major one.</span><span class="sxs-lookup"><span data-stu-id="e077f-135">That action that you will take at this point can make the difference between a minor and a major one.</span></span> <span data-ttu-id="e077f-136">The exact response will depend on your organization and the nature of the attack that you face.</span><span class="sxs-lookup"><span data-stu-id="e077f-136">The exact response will depend on your organization and the nature of the attack that you face.</span></span> <span data-ttu-id="e077f-137">If the initial assessment concluded that an account was compromised, you will need to enforce policy to block this account.</span><span class="sxs-lookup"><span data-stu-id="e077f-137">If the initial assessment concluded that an account was compromised, you will need to enforce policy to block this account.</span></span> <span data-ttu-id="e077f-138">That’s just one example where the identity management system will be leveraged.</span><span class="sxs-lookup"><span data-stu-id="e077f-138">That’s just one example where the identity management system will be leveraged.</span></span> <span data-ttu-id="e077f-139">Use the questions below to help you design your hybrid identity solution while taking into consideration how policies will be enforced to react to an ongoing incident:</span><span class="sxs-lookup"><span data-stu-id="e077f-139">Use the questions below to help you design your hybrid identity solution while taking into consideration how policies will be enforced to react to an ongoing incident:</span></span>

* <span data-ttu-id="e077f-140">Does your company have policies in place to block users from access the network if necessary?</span><span class="sxs-lookup"><span data-stu-id="e077f-140">Does your company have policies in place to block users from access the network if necessary?</span></span>
  * <span data-ttu-id="e077f-141">If yes, does the current solution integrate with the hybrid identity management system that you are going to adopt?</span><span class="sxs-lookup"><span data-stu-id="e077f-141">If yes, does the current solution integrate with the hybrid identity management system that you are going to adopt?</span></span>
* <span data-ttu-id="e077f-142">Does your company need to enforce conditional access for users that are in quarantine?</span><span class="sxs-lookup"><span data-stu-id="e077f-142">Does your company need to enforce conditional access for users that are in quarantine?</span></span> 

> [!NOTE]
> <span data-ttu-id="e077f-143">Make sure to take notes of each answer and understand the rationale behind the answer.</span><span class="sxs-lookup"><span data-stu-id="e077f-143">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="e077f-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span><span class="sxs-lookup"><span data-stu-id="e077f-144">[Define data protection strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="e077f-145">By having answered those questions you will select which option best suits your business needs.</span><span class="sxs-lookup"><span data-stu-id="e077f-145">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e077f-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="e077f-146">Next steps</span></span>
[<span data-ttu-id="e077f-147">Define data protection strategy</span><span class="sxs-lookup"><span data-stu-id="e077f-147">Define data protection strategy</span></span>](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md)

## <a name="see-also"></a><span data-ttu-id="e077f-148">See Also</span><span class="sxs-lookup"><span data-stu-id="e077f-148">See Also</span></span>
[<span data-ttu-id="e077f-149">Design considerations overview</span><span class="sxs-lookup"><span data-stu-id="e077f-149">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)
