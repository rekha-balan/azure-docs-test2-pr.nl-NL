---
title: Risky sign-ins report in the Azure Active Directory portal | Microsoft Docs
description: Learn about the risky sign-ins report in the Azure Active Directory portal
services: active-directory
author: priyamohanram
manager: mtillman
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 11/14/2017
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 4546734cd1b5bf2f4aaddc6477310128c9e62d51
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867017"
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="df80c-103">Risky sign-ins report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="df80c-103">Risky sign-ins report in the Azure Active Directory portal</span></span>

<span data-ttu-id="df80c-104">With the security reports in Azure Active Directory (Azure AD) you can gain insights into the probability of compromised user accounts in your environment.</span><span class="sxs-lookup"><span data-stu-id="df80c-104">With the security reports in Azure Active Directory (Azure AD) you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="df80c-105">Azure AD detects suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="df80c-105">Azure AD detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="df80c-106">For each detected action, a record called *risk event* is created.</span><span class="sxs-lookup"><span data-stu-id="df80c-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="df80c-107">For more details, see [Azure Active Directory risk events](concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="df80c-107">For more details, see [Azure Active Directory risk events](concept-risk-events.md).</span></span> 

<span data-ttu-id="df80c-108">The detected risk events are used to calculate:</span><span class="sxs-lookup"><span data-stu-id="df80c-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="df80c-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="df80c-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="df80c-110">For more details, see [Risky sign-ins](../identity-protection/overview.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="df80c-110">For more details, see [Risky sign-ins](../identity-protection/overview.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="df80c-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="df80c-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="df80c-112">For more details, see [Users flagged for risk](../identity-protection/overview.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="df80c-112">For more details, see [Users flagged for risk](../identity-protection/overview.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="df80c-113">In [the Azure portal](https://portal.azure.com), you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="df80c-113">In [the Azure portal](https://portal.azure.com), you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span> 

![Risky Sign-ins](./media/concept-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="df80c-115">What Azure AD license do you need to access a security report?</span><span class="sxs-lookup"><span data-stu-id="df80c-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="df80c-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span><span class="sxs-lookup"><span data-stu-id="df80c-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="df80c-117">However, the level of report granularity varies between the editions:</span><span class="sxs-lookup"><span data-stu-id="df80c-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="df80c-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span><span class="sxs-lookup"><span data-stu-id="df80c-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="df80c-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span><span class="sxs-lookup"><span data-stu-id="df80c-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="df80c-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span><span class="sxs-lookup"><span data-stu-id="df80c-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="df80c-121">Azure Active Directory free and basic edition</span><span class="sxs-lookup"><span data-stu-id="df80c-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="df80c-122">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span><span class="sxs-lookup"><span data-stu-id="df80c-122">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="df80c-123">This report lists:</span><span class="sxs-lookup"><span data-stu-id="df80c-123">This report lists:</span></span>

- <span data-ttu-id="df80c-124">**User** - The name of the user that was used during the sign-in operation</span><span class="sxs-lookup"><span data-stu-id="df80c-124">**User** - The name of the user that was used during the sign-in operation</span></span>
- <span data-ttu-id="df80c-125">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df80c-125">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="df80c-126">**Location** - The location used to connect to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="df80c-126">**Location** - The location used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="df80c-127">**Sign-in time** - The time when the sign-in was performed</span><span class="sxs-lookup"><span data-stu-id="df80c-127">**Sign-in time** - The time when the sign-in was performed</span></span>
- <span data-ttu-id="df80c-128">**Status** - The status of the sign-in</span><span class="sxs-lookup"><span data-stu-id="df80c-128">**Status** - The status of the sign-in</span></span>


![Risky Sign-ins](./media/concept-risky-sign-ins/01.png)

<span data-ttu-id="df80c-130">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span><span class="sxs-lookup"><span data-stu-id="df80c-130">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span></span>

- <span data-ttu-id="df80c-131">Resolve</span><span class="sxs-lookup"><span data-stu-id="df80c-131">Resolve</span></span>
- <span data-ttu-id="df80c-132">Mark as false positive</span><span class="sxs-lookup"><span data-stu-id="df80c-132">Mark as false positive</span></span>
- <span data-ttu-id="df80c-133">Ignore</span><span class="sxs-lookup"><span data-stu-id="df80c-133">Ignore</span></span>
- <span data-ttu-id="df80c-134">Reactivate</span><span class="sxs-lookup"><span data-stu-id="df80c-134">Reactivate</span></span>

![Risky Sign-ins](./media/concept-risky-sign-ins/21.png)

<span data-ttu-id="df80c-136">For more details, see [Closing risk events manually](../identity-protection/overview.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="df80c-136">For more details, see [Closing risk events manually](../identity-protection/overview.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="df80c-137">This report provides you with an option to:</span><span class="sxs-lookup"><span data-stu-id="df80c-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="df80c-138">Search resources</span><span class="sxs-lookup"><span data-stu-id="df80c-138">Search resources</span></span>
- <span data-ttu-id="df80c-139">Download the report data</span><span class="sxs-lookup"><span data-stu-id="df80c-139">Download the report data</span></span>


![Risky Sign-ins](./media/concept-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="df80c-141">Azure Active Directory premium editions</span><span class="sxs-lookup"><span data-stu-id="df80c-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="df80c-142">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span><span class="sxs-lookup"><span data-stu-id="df80c-142">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="df80c-143">Aggregated information about the [risk event types](concept-risk-events.md) that have been detected</span><span class="sxs-lookup"><span data-stu-id="df80c-143">Aggregated information about the [risk event types](concept-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="df80c-144">An option to download the report</span><span class="sxs-lookup"><span data-stu-id="df80c-144">An option to download the report</span></span>


![Risky Sign-ins](./media/concept-risky-sign-ins/456.png)


<span data-ttu-id="df80c-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span><span class="sxs-lookup"><span data-stu-id="df80c-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="df80c-147">An option to configure a [user risk remediation policy](../identity-protection/overview.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="df80c-147">An option to configure a [user risk remediation policy](../identity-protection/overview.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="df80c-148">Review the detection timeline for the risk event</span><span class="sxs-lookup"><span data-stu-id="df80c-148">Review the detection timeline for the risk event</span></span>  

- <span data-ttu-id="df80c-149">Review a list of users for which this risk event has been detected</span><span class="sxs-lookup"><span data-stu-id="df80c-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="df80c-150">[Manually close risk events](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="df80c-150">[Manually close risk events](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](./media/concept-risky-sign-ins/457.png)

<span data-ttu-id="df80c-152">When you select a user, you get a detailed report view for this user that enables you to:</span><span class="sxs-lookup"><span data-stu-id="df80c-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="df80c-153">Open the All sign-ins view</span><span class="sxs-lookup"><span data-stu-id="df80c-153">Open the All sign-ins view</span></span>

- <span data-ttu-id="df80c-154">Reset the user's password</span><span class="sxs-lookup"><span data-stu-id="df80c-154">Reset the user's password</span></span>

- <span data-ttu-id="df80c-155">Dismiss all events</span><span class="sxs-lookup"><span data-stu-id="df80c-155">Dismiss all events</span></span>

- <span data-ttu-id="df80c-156">Investigate reported risk events for the user.</span><span class="sxs-lookup"><span data-stu-id="df80c-156">Investigate reported risk events for the user.</span></span> 


![Risky Sign-ins](./media/concept-risky-sign-ins/324.png)


<span data-ttu-id="df80c-158">To investigate a risk event, select one from the list.</span><span class="sxs-lookup"><span data-stu-id="df80c-158">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="df80c-159">This opens the **Details** blade for this risk event.</span><span class="sxs-lookup"><span data-stu-id="df80c-159">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="df80c-160">On the **Details** blade, you have the option to either [manually close a risk event](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="df80c-160">On the **Details** blade, you have the option to either [manually close a risk event](../identity-protection/overview.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](./media/concept-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="df80c-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="df80c-162">Next steps</span></span>

- <span data-ttu-id="df80c-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="df80c-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](../active-directory-identityprotection.md).</span></span>

