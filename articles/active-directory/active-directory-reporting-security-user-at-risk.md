---
title: Users at risk security report in the Azure Active Directory portal - preview | Microsoft Docs
description: Learn about the users at risk security report in the Azure Active Directory portal - preview
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/21/2017
ms.author: markvi
ms.openlocfilehash: 0bc83fd2bbdd05a1f257f7c59860aec9cca99cc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563415"
---
# <a name="users-at-risk-security-report-in-the-azure-active-directory-portal---preview"></a><span data-ttu-id="197c7-103">Users at risk security report in the Azure Active Directory portal - preview</span><span class="sxs-lookup"><span data-stu-id="197c7-103">Users at risk security report in the Azure Active Directory portal - preview</span></span>

<span data-ttu-id="197c7-104">With the security reports in the Azure Active Directory [preview](active-directory-preview-explainer.md), you can gain insights into the probability of compromised user accounts in your environment.</span><span class="sxs-lookup"><span data-stu-id="197c7-104">With the security reports in the Azure Active Directory [preview](active-directory-preview-explainer.md), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="197c7-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="197c7-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="197c7-106">For each detected action, a record called *risk event* is created.</span><span class="sxs-lookup"><span data-stu-id="197c7-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="197c7-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="197c7-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="197c7-108">The detected risk events are used to calculate:</span><span class="sxs-lookup"><span data-stu-id="197c7-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="197c7-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="197c7-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="197c7-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="197c7-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="197c7-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="197c7-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="197c7-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="197c7-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="197c7-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="197c7-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/10.png)

## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="197c7-115">Azure Active Directory free and basic edition</span><span class="sxs-lookup"><span data-stu-id="197c7-115">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="197c7-116">The users at risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span><span class="sxs-lookup"><span data-stu-id="197c7-116">The users at risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="197c7-118">Selecting a user opens the related user data blade.</span><span class="sxs-lookup"><span data-stu-id="197c7-118">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="197c7-119">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span><span class="sxs-lookup"><span data-stu-id="197c7-119">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/46.png)

## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="197c7-121">Azure Active Directory premium editions</span><span class="sxs-lookup"><span data-stu-id="197c7-121">Azure Active Directory premium editions</span></span>

<span data-ttu-id="197c7-122">The users at risk report in the Azure Active Directory premium editions provides you with:</span><span class="sxs-lookup"><span data-stu-id="197c7-122">The users at risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="197c7-123">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span><span class="sxs-lookup"><span data-stu-id="197c7-123">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="197c7-124">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span><span class="sxs-lookup"><span data-stu-id="197c7-124">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="197c7-125">An option to download the report</span><span class="sxs-lookup"><span data-stu-id="197c7-125">An option to download the report</span></span>

- <span data-ttu-id="197c7-126">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="197c7-126">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="197c7-128">When you select a user, you get a detailed report view for this user that enables you to:</span><span class="sxs-lookup"><span data-stu-id="197c7-128">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="197c7-129">Open the All sign-ins view</span><span class="sxs-lookup"><span data-stu-id="197c7-129">Open the All sign-ins view</span></span>

- <span data-ttu-id="197c7-130">Reset the user's password</span><span class="sxs-lookup"><span data-stu-id="197c7-130">Reset the user's password</span></span>

- <span data-ttu-id="197c7-131">Dismiss all events</span><span class="sxs-lookup"><span data-stu-id="197c7-131">Dismiss all events</span></span>

- <span data-ttu-id="197c7-132">Investigate reported risk events for the user.</span><span class="sxs-lookup"><span data-stu-id="197c7-132">Investigate reported risk events for the user.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="197c7-134">To investigate a risk event, select one from the list.</span><span class="sxs-lookup"><span data-stu-id="197c7-134">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="197c7-135">This opens the **Details** blade for this risk event.</span><span class="sxs-lookup"><span data-stu-id="197c7-135">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="197c7-136">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="197c7-136">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="197c7-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="197c7-138">Next steps</span></span>

- <span data-ttu-id="197c7-139">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="197c7-139">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>







