---
title: Users flagged for risk security report in the Azure Active Directory portal | Microsoft Docs
description: Learn about the users flagged for risk security report in the Azure Active Directory portal
services: active-directory
author: priyamohanram
manager: mtillman
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/14/2017
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 030774716e1af4a7d6817d64ae66ded2bcaf4081
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857635"
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="53cae-103">Users flagged for risk security report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="53cae-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="53cae-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span><span class="sxs-lookup"><span data-stu-id="53cae-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="53cae-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="53cae-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="53cae-106">For each detected action, a record called *risk event* is created.</span><span class="sxs-lookup"><span data-stu-id="53cae-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="53cae-107">For more information, see [Azure Active Directory risk events](concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="53cae-107">For more information, see [Azure Active Directory risk events](concept-risk-events.md).</span></span> 

<span data-ttu-id="53cae-108">The detected risk events are used to calculate:</span><span class="sxs-lookup"><span data-stu-id="53cae-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="53cae-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="53cae-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="53cae-110">For more information, see [Risky sign-ins](../identity-protection/overview.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="53cae-110">For more information, see [Risky sign-ins](../identity-protection/overview.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="53cae-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="53cae-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="53cae-112">For more information, see [Users flagged for risk](../identity-protection/overview.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="53cae-112">For more information, see [Users flagged for risk](../identity-protection/overview.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="53cae-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="53cae-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![Risky Sign-ins](./media/concept-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="53cae-115">What Azure AD license do you need to access a security report?</span><span class="sxs-lookup"><span data-stu-id="53cae-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="53cae-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span><span class="sxs-lookup"><span data-stu-id="53cae-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="53cae-117">However, the level of report granularity varies between the editions:</span><span class="sxs-lookup"><span data-stu-id="53cae-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="53cae-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span><span class="sxs-lookup"><span data-stu-id="53cae-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="53cae-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span><span class="sxs-lookup"><span data-stu-id="53cae-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="53cae-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span><span class="sxs-lookup"><span data-stu-id="53cae-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="53cae-121">Azure Active Directory free and basic edition</span><span class="sxs-lookup"><span data-stu-id="53cae-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="53cae-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span><span class="sxs-lookup"><span data-stu-id="53cae-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Risky Sign-ins](./media/concept-user-at-risk/03.png)

<span data-ttu-id="53cae-124">Selecting a user opens the related user data blade.</span><span class="sxs-lookup"><span data-stu-id="53cae-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="53cae-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span><span class="sxs-lookup"><span data-stu-id="53cae-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Risky Sign-ins](./media/concept-user-at-risk/46.png)


<span data-ttu-id="53cae-127">This dialog provides you with an option to:</span><span class="sxs-lookup"><span data-stu-id="53cae-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="53cae-128">Download the report</span><span class="sxs-lookup"><span data-stu-id="53cae-128">Download the report</span></span>

- <span data-ttu-id="53cae-129">Search users</span><span class="sxs-lookup"><span data-stu-id="53cae-129">Search users</span></span>

![Risky Sign-ins](./media/concept-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="53cae-131">Azure Active Directory premium editions</span><span class="sxs-lookup"><span data-stu-id="53cae-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="53cae-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span><span class="sxs-lookup"><span data-stu-id="53cae-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="53cae-133">A [list of user accounts](../identity-protection/overview.md#users-flagged-for-risk) that may have been compromised</span><span class="sxs-lookup"><span data-stu-id="53cae-133">A [list of user accounts](../identity-protection/overview.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="53cae-134">Aggregated information about the [risk event types](concept-risk-events.md) that have been detected</span><span class="sxs-lookup"><span data-stu-id="53cae-134">Aggregated information about the [risk event types](concept-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="53cae-135">An option to download the report</span><span class="sxs-lookup"><span data-stu-id="53cae-135">An option to download the report</span></span>

- <span data-ttu-id="53cae-136">An option to configure a [user risk remediation policy](../identity-protection/overview.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="53cae-136">An option to configure a [user risk remediation policy](../identity-protection/overview.md#user-risk-security-policy)</span></span>  


![Risky Sign-ins](./media/concept-user-at-risk/71.png)

<span data-ttu-id="53cae-138">When you select a user, you get a detailed report view for this user that enables you to:</span><span class="sxs-lookup"><span data-stu-id="53cae-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="53cae-139">Open the All sign-ins view</span><span class="sxs-lookup"><span data-stu-id="53cae-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="53cae-140">Reset the user's password</span><span class="sxs-lookup"><span data-stu-id="53cae-140">Reset the user's password</span></span>

- <span data-ttu-id="53cae-141">Dismiss all events</span><span class="sxs-lookup"><span data-stu-id="53cae-141">Dismiss all events</span></span>

- <span data-ttu-id="53cae-142">Investigate reported risk events for the user.</span><span class="sxs-lookup"><span data-stu-id="53cae-142">Investigate reported risk events for the user.</span></span> 


![Risky Sign-ins](./media/concept-user-at-risk/324.png)


<span data-ttu-id="53cae-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span><span class="sxs-lookup"><span data-stu-id="53cae-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="53cae-145">On the **Details** blade, you have the option to either [manually close a risk event](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="53cae-145">On the **Details** blade, you have the option to either [manually close a risk event](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](./media/concept-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="53cae-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="53cae-147">Next steps</span></span>

- <span data-ttu-id="53cae-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="53cae-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>

