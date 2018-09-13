---
title: Azure Active Directory PoC Playbook Ingredients | Microsoft Docs
description: Explore and quickly implement Identity and Access Management scenarios
services: active-directory
keywords: azure active directory, playbook, Proof of Concept, PoC
documentationcenter: ''
author: dstefanMSFT
manager: asuthar
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555564"
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="14aab-104">Azure Active Directory Proof of Concept Playbook Ingredients</span><span class="sxs-lookup"><span data-stu-id="14aab-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="14aab-105">Theme</span><span class="sxs-lookup"><span data-stu-id="14aab-105">Theme</span></span>
<span data-ttu-id="14aab-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span><span class="sxs-lookup"><span data-stu-id="14aab-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="14aab-107">We classify the scenarios in the following areas:</span><span class="sxs-lookup"><span data-stu-id="14aab-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="14aab-108">Lots of apps, one identity</span><span class="sxs-lookup"><span data-stu-id="14aab-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="14aab-109">Increase your security</span><span class="sxs-lookup"><span data-stu-id="14aab-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="14aab-110">Scale with Self Service</span><span class="sxs-lookup"><span data-stu-id="14aab-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="14aab-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span><span class="sxs-lookup"><span data-stu-id="14aab-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="14aab-112">Environment</span><span class="sxs-lookup"><span data-stu-id="14aab-112">Environment</span></span>

<span data-ttu-id="14aab-113">It is important to determine the details of the environment where you will deliver the PoC.</span><span class="sxs-lookup"><span data-stu-id="14aab-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="14aab-114">Ideally you can build upon it after the PoC is completed.</span><span class="sxs-lookup"><span data-stu-id="14aab-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="14aab-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span><span class="sxs-lookup"><span data-stu-id="14aab-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="14aab-116">The typical environments for PoCs are:</span><span class="sxs-lookup"><span data-stu-id="14aab-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="14aab-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span><span class="sxs-lookup"><span data-stu-id="14aab-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="14aab-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span><span class="sxs-lookup"><span data-stu-id="14aab-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="14aab-119">Typically, the test environment is shared across multiple projects in the enterprise.</span><span class="sxs-lookup"><span data-stu-id="14aab-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="14aab-120">Most scenarios in this guide are additive in nature.</span><span class="sxs-lookup"><span data-stu-id="14aab-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="14aab-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span><span class="sxs-lookup"><span data-stu-id="14aab-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="14aab-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span><span class="sxs-lookup"><span data-stu-id="14aab-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="14aab-123">In those cases, you might want to consider a non-production environment.</span><span class="sxs-lookup"><span data-stu-id="14aab-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="14aab-124">Target Users</span><span class="sxs-lookup"><span data-stu-id="14aab-124">Target Users</span></span>

<span data-ttu-id="14aab-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span><span class="sxs-lookup"><span data-stu-id="14aab-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="14aab-126">The categories of target users for PoC are:</span><span class="sxs-lookup"><span data-stu-id="14aab-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="14aab-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span><span class="sxs-lookup"><span data-stu-id="14aab-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="14aab-128">**Test Users:** Test accounts created in the environment</span><span class="sxs-lookup"><span data-stu-id="14aab-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="14aab-129">Most scenarios in this guide can be exercised by pilot users.</span><span class="sxs-lookup"><span data-stu-id="14aab-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="14aab-130">Throughout this document, we will be calling out target user considerations if needed.</span><span class="sxs-lookup"><span data-stu-id="14aab-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]