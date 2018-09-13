---
title: Azure Active Directory hybrid identity design considerations - determine access control requirements| Microsoft Docs
description: Covers the pillars of identity, and identifying access requirements for resources for users in a hybrid environment.
documentationcenter: ''
services: active-directory
author: billmath
manager: femila
editor: ''
ms.assetid: e3b3b984-0d15-4654-93be-a396324b9f5e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: f0121aa9e78291f2d533f85331fbb0e06e1cc1bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660579"
---
# <a name="determine-access-control-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="28eed-103">Determine access control requirements for your hybrid identity solution</span><span class="sxs-lookup"><span data-stu-id="28eed-103">Determine access control requirements for your hybrid identity solution</span></span>
<span data-ttu-id="28eed-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span><span class="sxs-lookup"><span data-stu-id="28eed-104">When an organization is designing their hybrid identity solution they can also use this opportunity to review access requirements for the resources that they are planning to make it available for users.</span></span> <span data-ttu-id="28eed-105">The data access cross all four pillars of identity, which are:</span><span class="sxs-lookup"><span data-stu-id="28eed-105">The data access cross all four pillars of identity, which are:</span></span>

* <span data-ttu-id="28eed-106">Administration</span><span class="sxs-lookup"><span data-stu-id="28eed-106">Administration</span></span>
* <span data-ttu-id="28eed-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="28eed-107">Authentication</span></span>
* <span data-ttu-id="28eed-108">Authorization</span><span class="sxs-lookup"><span data-stu-id="28eed-108">Authorization</span></span>
* <span data-ttu-id="28eed-109">Auditing</span><span class="sxs-lookup"><span data-stu-id="28eed-109">Auditing</span></span>

<span data-ttu-id="28eed-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span><span class="sxs-lookup"><span data-stu-id="28eed-110">The sections that follows will cover authentication and authorization in more details, administration and auditing are part of the hybrid identity lifecycle.</span></span> <span data-ttu-id="28eed-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span><span class="sxs-lookup"><span data-stu-id="28eed-111">Read [Determine hybrid identity management tasks](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) for more information about these capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="28eed-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span><span class="sxs-lookup"><span data-stu-id="28eed-112">Read [The Four Pillars of Identity - Identity Management in the Age of Hybrid IT](http://social.technet.microsoft.com/wiki/contents/articles/15530.the-four-pillars-of-identity-identity-management-in-the-age-of-hybrid-it.aspx) for more information about each one of those pillars.</span></span>
> 
> 

## <a name="authentication-and-authorization"></a><span data-ttu-id="28eed-113">Authentication and authorization</span><span class="sxs-lookup"><span data-stu-id="28eed-113">Authentication and authorization</span></span>
<span data-ttu-id="28eed-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span><span class="sxs-lookup"><span data-stu-id="28eed-114">There are different scenarios for authentication and authorization, these scenarios will have specific requirements that must be fulfilled by the hybrid identity solution that the company is going to adopt.</span></span> <span data-ttu-id="28eed-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span><span class="sxs-lookup"><span data-stu-id="28eed-115">Scenarios involving Business to Business (B2B) communication can add an extra challenge for IT Admins since they will need to ensure that the authentication and authorization method used by the organization can communicate with their business partners.</span></span> <span data-ttu-id="28eed-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span><span class="sxs-lookup"><span data-stu-id="28eed-116">During the designing process for authentication and authorization requirements, ensure that the following questions are answered:</span></span>

* <span data-ttu-id="28eed-117">Will your organization authenticate and authorize only users located at their identity management system?</span><span class="sxs-lookup"><span data-stu-id="28eed-117">Will your organization authenticate and authorize only users located at their identity management system?</span></span>
  * <span data-ttu-id="28eed-118">Are there any plans for B2B scenarios?</span><span class="sxs-lookup"><span data-stu-id="28eed-118">Are there any plans for B2B scenarios?</span></span>
  * <span data-ttu-id="28eed-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span><span class="sxs-lookup"><span data-stu-id="28eed-119">If yes, do you already know which protocols (SAML, OAuth, Kerberos, Tokens or Certificates) will be used to connect both businesses?</span></span>
* <span data-ttu-id="28eed-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span><span class="sxs-lookup"><span data-stu-id="28eed-120">Does the hybrid identity solution that you are going to adopt support those protocols?</span></span>

<span data-ttu-id="28eed-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span><span class="sxs-lookup"><span data-stu-id="28eed-121">Another important point to consider is where the authentication repository that will be used by users and partners will be located and the administrative model to be used.</span></span> <span data-ttu-id="28eed-122">Consider the following two core options:</span><span class="sxs-lookup"><span data-stu-id="28eed-122">Consider the following two core options:</span></span>

* <span data-ttu-id="28eed-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span><span class="sxs-lookup"><span data-stu-id="28eed-123">Centralized: in this model the user’s credentials, policies and administration can be centralized on-premises or in the cloud.</span></span>
* <span data-ttu-id="28eed-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span><span class="sxs-lookup"><span data-stu-id="28eed-124">Hybrid: in this model the user’s credentials, policies and administration will be centralized on-premises and a replicated in the cloud.</span></span>

<span data-ttu-id="28eed-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span><span class="sxs-lookup"><span data-stu-id="28eed-125">Which model your organization will adopt will vary according to their business requirements, you want to answer the following questions to identify where the identity management system will reside and the administrative mode to use:</span></span>

* <span data-ttu-id="28eed-126">Does your organization currently have an identity management on-premises?</span><span class="sxs-lookup"><span data-stu-id="28eed-126">Does your organization currently have an identity management on-premises?</span></span>
  * <span data-ttu-id="28eed-127">If yes, do they plan to keep it?</span><span class="sxs-lookup"><span data-stu-id="28eed-127">If yes, do they plan to keep it?</span></span>
  * <span data-ttu-id="28eed-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span><span class="sxs-lookup"><span data-stu-id="28eed-128">Are there any regulation or compliance requirements that your organization must follow that dictates where the identity management system should reside?</span></span>
* <span data-ttu-id="28eed-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span><span class="sxs-lookup"><span data-stu-id="28eed-129">Does your organization use single sign-on for apps located on-premises or in the cloud?</span></span>
  * <span data-ttu-id="28eed-130">If yes, does the adoption of a hybrid identity model affect this process?</span><span class="sxs-lookup"><span data-stu-id="28eed-130">If yes, does the adoption of a hybrid identity model affect this process?</span></span>

## <a name="access-control"></a><span data-ttu-id="28eed-131">Access Control</span><span class="sxs-lookup"><span data-stu-id="28eed-131">Access Control</span></span>
<span data-ttu-id="28eed-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span><span class="sxs-lookup"><span data-stu-id="28eed-132">While authentication and authorization are core elements to enable access to corporate data through user’s validation, it is also important to control the level of access that these users will have and the level of access administrators will have over the resources that they are managing.</span></span> <span data-ttu-id="28eed-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span><span class="sxs-lookup"><span data-stu-id="28eed-133">Your hybrid identity solution must be able to provide granular access to resources, delegation and role base access control.</span></span> <span data-ttu-id="28eed-134">Ensure that the following question are answered regarding access control:</span><span class="sxs-lookup"><span data-stu-id="28eed-134">Ensure that the following question are answered regarding access control:</span></span>

* <span data-ttu-id="28eed-135">Does your company have more than one user with elevated privilege to manage your identity system?</span><span class="sxs-lookup"><span data-stu-id="28eed-135">Does your company have more than one user with elevated privilege to manage your identity system?</span></span>
  * <span data-ttu-id="28eed-136">If yes, does each user need the same access level?</span><span class="sxs-lookup"><span data-stu-id="28eed-136">If yes, does each user need the same access level?</span></span>
* <span data-ttu-id="28eed-137">Would your company need to delegate access to users to manage specific resources?</span><span class="sxs-lookup"><span data-stu-id="28eed-137">Would your company need to delegate access to users to manage specific resources?</span></span>
  * <span data-ttu-id="28eed-138">If yes, how frequently this happens?</span><span class="sxs-lookup"><span data-stu-id="28eed-138">If yes, how frequently this happens?</span></span>
* <span data-ttu-id="28eed-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span><span class="sxs-lookup"><span data-stu-id="28eed-139">Would your company need to integrate access control capabilities between on-premises and cloud resources?</span></span>
* <span data-ttu-id="28eed-140">Would your company need to limit access to resources according to some conditions?</span><span class="sxs-lookup"><span data-stu-id="28eed-140">Would your company need to limit access to resources according to some conditions?</span></span>
* <span data-ttu-id="28eed-141">Would your company have any application that needs custom control access to some resources?</span><span class="sxs-lookup"><span data-stu-id="28eed-141">Would your company have any application that needs custom control access to some resources?</span></span>
  * <span data-ttu-id="28eed-142">If yes, where are those apps located (on-premises or in the cloud)?</span><span class="sxs-lookup"><span data-stu-id="28eed-142">If yes, where are those apps located (on-premises or in the cloud)?</span></span>
  * <span data-ttu-id="28eed-143">If yes, where are those target resources located (on-premises or in the cloud)?</span><span class="sxs-lookup"><span data-stu-id="28eed-143">If yes, where are those target resources located (on-premises or in the cloud)?</span></span>

> [!NOTE]
> <span data-ttu-id="28eed-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span><span class="sxs-lookup"><span data-stu-id="28eed-144">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="28eed-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span><span class="sxs-lookup"><span data-stu-id="28eed-145">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="28eed-146">By answering those questions you will select which option best suits your business needs.</span><span class="sxs-lookup"><span data-stu-id="28eed-146">By answering those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="28eed-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="28eed-147">Next steps</span></span>
[<span data-ttu-id="28eed-148">Determine incident response requirements</span><span class="sxs-lookup"><span data-stu-id="28eed-148">Determine incident response requirements</span></span>](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md)

## <a name="see-also"></a><span data-ttu-id="28eed-149">See Also</span><span class="sxs-lookup"><span data-stu-id="28eed-149">See Also</span></span>
[<span data-ttu-id="28eed-150">Design considerations overview</span><span class="sxs-lookup"><span data-stu-id="28eed-150">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

