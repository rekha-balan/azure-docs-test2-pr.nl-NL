---
title: Azure Active Directory hybrid identity design considerations - determine multi-factor authentication requirements
description: With Conditional access control, Azure Active Directory checks the specific conditions you pick when authenticating the user and before allowing access to the application. Once those conditions are met, the user is authenticated and allowed access to the application.
documentationcenter: ''
services: active-directory
author: femila
manager: billmath
editor: ''
ms.assetid: 9c59fda9-47d0-4c7e-b3e7-3575c29beabe
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.openlocfilehash: f5006b6ce1b409fae5e540d8414e8e56651f9349
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540787"
---
# <a name="determine-multi-factor-authentication-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="be31a-104">Determine multi-factor authentication requirements for your hybrid identity solution</span><span class="sxs-lookup"><span data-stu-id="be31a-104">Determine multi-factor authentication requirements for your hybrid identity solution</span></span>
<span data-ttu-id="be31a-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span><span class="sxs-lookup"><span data-stu-id="be31a-105">In this world of mobility, with users accessing data and applications in the cloud and from any device, securing this information has become paramount.</span></span>  <span data-ttu-id="be31a-106">Every day there is a new headline about a security breach.</span><span class="sxs-lookup"><span data-stu-id="be31a-106">Every day there is a new headline about a security breach.</span></span>  <span data-ttu-id="be31a-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span><span class="sxs-lookup"><span data-stu-id="be31a-107">Although, there is no guarantee against such breaches, multi-factor authentication, provides an additional layer of security to help prevent these breaches.</span></span>
<span data-ttu-id="be31a-108">Start by evaluating the organizations requirements for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="be31a-108">Start by evaluating the organizations requirements for multi-factor authentication.</span></span> <span data-ttu-id="be31a-109">That is, what is the organization trying to secure.</span><span class="sxs-lookup"><span data-stu-id="be31a-109">That is, what is the organization trying to secure.</span></span>  <span data-ttu-id="be31a-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="be31a-110">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="be31a-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span><span class="sxs-lookup"><span data-stu-id="be31a-111">If you are not familiar with MFA and what it does, it is strongly recommended that you read the article [What is Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md) prior to continue reading this section.</span></span>
> 
> 

<span data-ttu-id="be31a-112">Make sure to answer the following:</span><span class="sxs-lookup"><span data-stu-id="be31a-112">Make sure to answer the following:</span></span>

* <span data-ttu-id="be31a-113">Is your company trying to secure Microsoft apps?</span><span class="sxs-lookup"><span data-stu-id="be31a-113">Is your company trying to secure Microsoft apps?</span></span> 
* <span data-ttu-id="be31a-114">How these apps are published?</span><span class="sxs-lookup"><span data-stu-id="be31a-114">How these apps are published?</span></span>
* <span data-ttu-id="be31a-115">Does your company provide remote access to allow employees to access on-premises apps?</span><span class="sxs-lookup"><span data-stu-id="be31a-115">Does your company provide remote access to allow employees to access on-premises apps?</span></span>

<span data-ttu-id="be31a-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span><span class="sxs-lookup"><span data-stu-id="be31a-116">If yes, what type of remote access?You also need to evaluate where the users who are accessing these applications will be located.</span></span> <span data-ttu-id="be31a-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span><span class="sxs-lookup"><span data-stu-id="be31a-117">This evaluation is another important step to define the proper multi-factor authentication strategy.</span></span> <span data-ttu-id="be31a-118">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="be31a-118">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="be31a-119">Where are the users going to be located?</span><span class="sxs-lookup"><span data-stu-id="be31a-119">Where are the users going to be located?</span></span>
* <span data-ttu-id="be31a-120">Can they be located anywhere?</span><span class="sxs-lookup"><span data-stu-id="be31a-120">Can they be located anywhere?</span></span>
* <span data-ttu-id="be31a-121">Does your company want to establish restrictions according to the user’s location?</span><span class="sxs-lookup"><span data-stu-id="be31a-121">Does your company want to establish restrictions according to the user’s location?</span></span>

<span data-ttu-id="be31a-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="be31a-122">Once you understand these requirements, it is important to also evaluate the user’s requirements for multi-factor authentication.</span></span> <span data-ttu-id="be31a-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="be31a-123">This evaluation is important because it will define the requirements for rolling out multi-factor authentication.</span></span> <span data-ttu-id="be31a-124">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="be31a-124">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="be31a-125">Are the users familiar with multi-factor authentication?</span><span class="sxs-lookup"><span data-stu-id="be31a-125">Are the users familiar with multi-factor authentication?</span></span>
* <span data-ttu-id="be31a-126">Will some uses be required to provide additional authentication?</span><span class="sxs-lookup"><span data-stu-id="be31a-126">Will some uses be required to provide additional authentication?</span></span>  
  * <span data-ttu-id="be31a-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span><span class="sxs-lookup"><span data-stu-id="be31a-127">If yes, all the time, when coming from external networks, or accessing specific applications, or under other conditions?</span></span>
* <span data-ttu-id="be31a-128">Will the users require training on how to setup and implement multi-factor authentication?</span><span class="sxs-lookup"><span data-stu-id="be31a-128">Will the users require training on how to setup and implement multi-factor authentication?</span></span>
* <span data-ttu-id="be31a-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span><span class="sxs-lookup"><span data-stu-id="be31a-129">What are the key scenarios that your company wants to enable multi-factor authentication for their users?</span></span>

<span data-ttu-id="be31a-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span><span class="sxs-lookup"><span data-stu-id="be31a-130">After answering the previous questions, you will be able to understand if there are multi-factor authentication already implemented on-premises.</span></span> <span data-ttu-id="be31a-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span><span class="sxs-lookup"><span data-stu-id="be31a-131">This evaluation is important to define the technical requirements for setting up and enabling the organizations users for multi-factor authentication.</span></span> <span data-ttu-id="be31a-132">Make sure to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="be31a-132">Make sure to answer the following questions:</span></span>

* <span data-ttu-id="be31a-133">Does your company need to protect privileged accounts with MFA?</span><span class="sxs-lookup"><span data-stu-id="be31a-133">Does your company need to protect privileged accounts with MFA?</span></span>
* <span data-ttu-id="be31a-134">Does your company need to enable MFA for certain application for compliance reasons?</span><span class="sxs-lookup"><span data-stu-id="be31a-134">Does your company need to enable MFA for certain application for compliance reasons?</span></span>
* <span data-ttu-id="be31a-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span><span class="sxs-lookup"><span data-stu-id="be31a-135">Does your company need to enable MFA for all eligible users of these application or only administrators?</span></span>
* <span data-ttu-id="be31a-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span><span class="sxs-lookup"><span data-stu-id="be31a-136">Do you need have MFA always enabled or only when the users are logged outside of your corporate network?</span></span>

## <a name="next-steps"></a><span data-ttu-id="be31a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="be31a-137">Next steps</span></span>
[<span data-ttu-id="be31a-138">Define a hybrid identity adoption strategy</span><span class="sxs-lookup"><span data-stu-id="be31a-138">Define a hybrid identity adoption strategy</span></span>](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md)

## <a name="see-also"></a><span data-ttu-id="be31a-139">See also</span><span class="sxs-lookup"><span data-stu-id="be31a-139">See also</span></span>
[<span data-ttu-id="be31a-140">Design considerations overview</span><span class="sxs-lookup"><span data-stu-id="be31a-140">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

