---
title: Risky sign-ins report in the Azure Active Directory portal - preview | Microsoft Docs
description: Learn about the risky sign-ins report in the Azure Active Directory portal - preview
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/21/2017
ms.author: markvi
ms.openlocfilehash: b8de6b9e8bb8480fa29ae5e32bef6213f25b4cea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549616"
---
# <a name="risky-sign-ins-report-in-the-azure-active-directory-portal---preview"></a><span data-ttu-id="f1565-103">Risky sign-ins report in the Azure Active Directory portal - preview</span><span class="sxs-lookup"><span data-stu-id="f1565-103">Risky sign-ins report in the Azure Active Directory portal - preview</span></span>

<span data-ttu-id="f1565-104">With the security reports in the Azure Active Directory [preview](active-directory-preview-explainer.md), you can gain insights into the probability of compromised user accounts in your environment.</span><span class="sxs-lookup"><span data-stu-id="f1565-104">With the security reports in the Azure Active Directory [preview](active-directory-preview-explainer.md), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="f1565-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span><span class="sxs-lookup"><span data-stu-id="f1565-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="f1565-106">For each detected action, a record called *risk event* is created.</span><span class="sxs-lookup"><span data-stu-id="f1565-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="f1565-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f1565-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="f1565-108">The detected risk events are used to calculate:</span><span class="sxs-lookup"><span data-stu-id="f1565-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="f1565-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="f1565-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="f1565-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="f1565-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="f1565-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="f1565-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="f1565-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="f1565-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="f1565-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span><span class="sxs-lookup"><span data-stu-id="f1565-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span> 

![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="f1565-115">Azure Active Directory free and basic edition</span><span class="sxs-lookup"><span data-stu-id="f1565-115">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="f1565-116">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span><span class="sxs-lookup"><span data-stu-id="f1565-116">The Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="f1565-117">The risk events report provides you with:</span><span class="sxs-lookup"><span data-stu-id="f1565-117">The risk events report provides you with:</span></span>

- <span data-ttu-id="f1565-118">**User** - The name of the user that was used during the sign-in operation</span><span class="sxs-lookup"><span data-stu-id="f1565-118">**User** - The name of the user that was used during the sign-in operation</span></span>
- <span data-ttu-id="f1565-119">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1565-119">**IP** - The IP address of the device that was used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="f1565-120">**Location** - The location used to connect to Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f1565-120">**Location** - The location used to connect to Azure Active Directory</span></span>
- <span data-ttu-id="f1565-121">**Sign-in time** - The time when the sign-in was performed</span><span class="sxs-lookup"><span data-stu-id="f1565-121">**Sign-in time** - The time when the sign-in was performed</span></span>
- <span data-ttu-id="f1565-122">**Status** - The status of the sign-in</span><span class="sxs-lookup"><span data-stu-id="f1565-122">**Status** - The status of the sign-in</span></span>

<span data-ttu-id="f1565-123">This report provides you with an option to download the report data.</span><span class="sxs-lookup"><span data-stu-id="f1565-123">This report provides you with an option to download the report data.</span></span>

![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="f1565-125">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span><span class="sxs-lookup"><span data-stu-id="f1565-125">Based on your investigation of the risky sign-in, you can provide feedback to Azure Active Directory in form of the following actions:</span></span>

- <span data-ttu-id="f1565-126">Resolve</span><span class="sxs-lookup"><span data-stu-id="f1565-126">Resolve</span></span>
- <span data-ttu-id="f1565-127">Mark as false positive</span><span class="sxs-lookup"><span data-stu-id="f1565-127">Mark as false positive</span></span>
- <span data-ttu-id="f1565-128">Ignore</span><span class="sxs-lookup"><span data-stu-id="f1565-128">Ignore</span></span>
- <span data-ttu-id="f1565-129">Reactivate</span><span class="sxs-lookup"><span data-stu-id="f1565-129">Reactivate</span></span>

![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="f1565-131">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="f1565-131">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="f1565-132">Azure Active Directory premium editions</span><span class="sxs-lookup"><span data-stu-id="f1565-132">Azure Active Directory premium editions</span></span>

<span data-ttu-id="f1565-133">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span><span class="sxs-lookup"><span data-stu-id="f1565-133">The risky sign-ins report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="f1565-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span><span class="sxs-lookup"><span data-stu-id="f1565-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="f1565-135">An option to download the report</span><span class="sxs-lookup"><span data-stu-id="f1565-135">An option to download the report</span></span>


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="f1565-137">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span><span class="sxs-lookup"><span data-stu-id="f1565-137">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="f1565-138">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="f1565-138">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="f1565-139">Review the detection timeline for the risk event</span><span class="sxs-lookup"><span data-stu-id="f1565-139">Review the detection timeline for the risk event</span></span>  

- <span data-ttu-id="f1565-140">Review a list of users for which this risk event has been detected</span><span class="sxs-lookup"><span data-stu-id="f1565-140">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="f1565-141">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="f1565-141">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="f1565-143">When you select a user, you get a detailed report view for this user that enables you to:</span><span class="sxs-lookup"><span data-stu-id="f1565-143">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="f1565-144">Open the All sign-ins view</span><span class="sxs-lookup"><span data-stu-id="f1565-144">Open the All sign-ins view</span></span>

- <span data-ttu-id="f1565-145">Reset the user's password</span><span class="sxs-lookup"><span data-stu-id="f1565-145">Reset the user's password</span></span>

- <span data-ttu-id="f1565-146">Dismiss all events</span><span class="sxs-lookup"><span data-stu-id="f1565-146">Dismiss all events</span></span>

- <span data-ttu-id="f1565-147">Investigate reported risk events for the user.</span><span class="sxs-lookup"><span data-stu-id="f1565-147">Investigate reported risk events for the user.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="f1565-149">To investigate a risk event, select one from the list.</span><span class="sxs-lookup"><span data-stu-id="f1565-149">To investigate a risk event, select one from the list.</span></span>  
<span data-ttu-id="f1565-150">This opens the **Details** blade for this risk event.</span><span class="sxs-lookup"><span data-stu-id="f1565-150">This opens the **Details** blade for this risk event.</span></span> <span data-ttu-id="f1565-151">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span><span class="sxs-lookup"><span data-stu-id="f1565-151">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Risky Sign-ins](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="f1565-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="f1565-153">Next steps</span></span>

- <span data-ttu-id="f1565-154">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="f1565-154">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>








