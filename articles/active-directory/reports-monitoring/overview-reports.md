---
title: Azure Active Directory reporting | Microsoft Docs
description: Provides a general overview of Azure Active Directory reporting.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 01/15/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 96faeaefc6c58f03328a85b626528267396121a5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857046"
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="84a1b-103">Azure Active Directory reporting</span><span class="sxs-lookup"><span data-stu-id="84a1b-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="84a1b-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span><span class="sxs-lookup"><span data-stu-id="84a1b-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="84a1b-105">The provided data enables you to:</span><span class="sxs-lookup"><span data-stu-id="84a1b-105">The provided data enables you to:</span></span>

- <span data-ttu-id="84a1b-106">Determine how your apps and services are utilized by your users</span><span class="sxs-lookup"><span data-stu-id="84a1b-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="84a1b-107">Detect potential risks affecting the health of your environment</span><span class="sxs-lookup"><span data-stu-id="84a1b-107">Detect potential risks affecting the health of your environment</span></span>
- <span data-ttu-id="84a1b-108">Troubleshoot issues preventing your users from getting their work done</span><span class="sxs-lookup"><span data-stu-id="84a1b-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="84a1b-109">The reporting architecture relies on two main pillars:</span><span class="sxs-lookup"><span data-stu-id="84a1b-109">The reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="84a1b-110">Security reports</span><span class="sxs-lookup"><span data-stu-id="84a1b-110">Security reports</span></span>
- <span data-ttu-id="84a1b-111">Activity reports</span><span class="sxs-lookup"><span data-stu-id="84a1b-111">Activity reports</span></span>

![Reporting](./media/overview-reports/01.png)


## <a name="security-reports"></a><span data-ttu-id="84a1b-113">Security reports</span><span class="sxs-lookup"><span data-stu-id="84a1b-113">Security reports</span></span>

<span data-ttu-id="84a1b-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span><span class="sxs-lookup"><span data-stu-id="84a1b-114">The security reports in Azure Active Directory help you to protect your organization's identities.</span></span>  
<span data-ttu-id="84a1b-115">There are two types of security reports in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="84a1b-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="84a1b-116">**Users flagged for risk** - From the [users flagged for risk security report](concept-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span><span class="sxs-lookup"><span data-stu-id="84a1b-116">**Users flagged for risk** - From the [users flagged for risk security report](concept-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="84a1b-117">**Risky sign-ins** - With the [risky sign-in security report](concept-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span><span class="sxs-lookup"><span data-stu-id="84a1b-117">**Risky sign-ins** - With the [risky sign-in security report](concept-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 

<span data-ttu-id="84a1b-118">**What Azure AD license do you need to access a security report?**</span><span class="sxs-lookup"><span data-stu-id="84a1b-118">**What Azure AD license do you need to access a security report?**</span></span>  
<span data-ttu-id="84a1b-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span><span class="sxs-lookup"><span data-stu-id="84a1b-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="84a1b-120">However, the level of report granularity varies between the editions:</span><span class="sxs-lookup"><span data-stu-id="84a1b-120">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="84a1b-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span><span class="sxs-lookup"><span data-stu-id="84a1b-121">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="84a1b-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span><span class="sxs-lookup"><span data-stu-id="84a1b-122">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="84a1b-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span><span class="sxs-lookup"><span data-stu-id="84a1b-123">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about the underlying risk events and it also enables you to configure security policies that automatically respond to configured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="84a1b-124">Activity reports</span><span class="sxs-lookup"><span data-stu-id="84a1b-124">Activity reports</span></span>

<span data-ttu-id="84a1b-125">There are two types of activity reports in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="84a1b-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="84a1b-126">**Audit logs** - The [audit logs activity report](concept-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span><span class="sxs-lookup"><span data-stu-id="84a1b-126">**Audit logs** - The [audit logs activity report](concept-audit-logs.md) provides you with access to the history of every task performed in your tenant.</span></span>

- <span data-ttu-id="84a1b-127">**Sign-ins** -  With the [sign-ins activity report](concept-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span><span class="sxs-lookup"><span data-stu-id="84a1b-127">**Sign-ins** -  With the [sign-ins activity report](concept-sign-ins.md), you can determine, who has performed the tasks reported by the audit logs report.</span></span>



<span data-ttu-id="84a1b-128">The **audit logs report** provides you with records of system activities for compliance.</span><span class="sxs-lookup"><span data-stu-id="84a1b-128">The **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="84a1b-129">Amongst others, the provided data enables you to address common scenarios such as:</span><span class="sxs-lookup"><span data-stu-id="84a1b-129">Amongst others, the provided data enables you to address common scenarios such as:</span></span>

- <span data-ttu-id="84a1b-130">Someone in my tenant got access to an admin group.</span><span class="sxs-lookup"><span data-stu-id="84a1b-130">Someone in my tenant got access to an admin group.</span></span> <span data-ttu-id="84a1b-131">Who gave them access?</span><span class="sxs-lookup"><span data-stu-id="84a1b-131">Who gave them access?</span></span> 

- <span data-ttu-id="84a1b-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span><span class="sxs-lookup"><span data-stu-id="84a1b-132">I want to know the list of users signing into a specific app since I recently onboarded the app and want to know if it’s doing well</span></span>

- <span data-ttu-id="84a1b-133">I want to know how many password resets are happening in my tenant</span><span class="sxs-lookup"><span data-stu-id="84a1b-133">I want to know how many password resets are happening in my tenant</span></span>


<span data-ttu-id="84a1b-134">**What Azure AD license do you need to access the audit logs report?**</span><span class="sxs-lookup"><span data-stu-id="84a1b-134">**What Azure AD license do you need to access the audit logs report?**</span></span>  
<span data-ttu-id="84a1b-135">The audit logs report is available for features for which you have licenses.</span><span class="sxs-lookup"><span data-stu-id="84a1b-135">The audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="84a1b-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span><span class="sxs-lookup"><span data-stu-id="84a1b-136">If you have a license for a specific feature, you also have access to the audit log information for it.</span></span>

<span data-ttu-id="84a1b-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="84a1b-137">For more details, see **Comparing generally available features of the Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="84a1b-138">The **sign-ins activity report** enables you to find answers to questions such as:</span><span class="sxs-lookup"><span data-stu-id="84a1b-138">The **sign-ins activity report** enables you to find answers to questions such as:</span></span>

- <span data-ttu-id="84a1b-139">What is the sign-in pattern of a user?</span><span class="sxs-lookup"><span data-stu-id="84a1b-139">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="84a1b-140">How many users have users signed in over a week?</span><span class="sxs-lookup"><span data-stu-id="84a1b-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="84a1b-141">What’s the status of these sign-ins?</span><span class="sxs-lookup"><span data-stu-id="84a1b-141">What’s the status of these sign-ins?</span></span>


<span data-ttu-id="84a1b-142">**What Azure AD license do you need to access the sign-ins activity report?**</span><span class="sxs-lookup"><span data-stu-id="84a1b-142">**What Azure AD license do you need to access the sign-ins activity report?**</span></span>  
<span data-ttu-id="84a1b-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span><span class="sxs-lookup"><span data-stu-id="84a1b-143">To access the sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="84a1b-144">Programmatic access</span><span class="sxs-lookup"><span data-stu-id="84a1b-144">Programmatic access</span></span>

<span data-ttu-id="84a1b-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](concept-reporting-api.md) to the reporting data.</span><span class="sxs-lookup"><span data-stu-id="84a1b-145">In addition to the user interface, Azure Active Directory reporting also provides you with [programmatic access](concept-reporting-api.md) to the reporting data.</span></span> <span data-ttu-id="84a1b-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span><span class="sxs-lookup"><span data-stu-id="84a1b-146">The data of these reports can be very useful to your applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="84a1b-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span><span class="sxs-lookup"><span data-stu-id="84a1b-147">The Azure AD reporting APIs provide programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="84a1b-148">You can call these APIs from a variety of programming languages and tools.</span><span class="sxs-lookup"><span data-stu-id="84a1b-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="84a1b-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="84a1b-149">Next steps</span></span>

<span data-ttu-id="84a1b-150">If you want to know more about the various report types in Azure Active Directory, see:</span><span class="sxs-lookup"><span data-stu-id="84a1b-150">If you want to know more about the various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="84a1b-151">Users flagged for risk report</span><span class="sxs-lookup"><span data-stu-id="84a1b-151">Users flagged for risk report</span></span>](concept-user-at-risk.md)
- [<span data-ttu-id="84a1b-152">Risky sign-ins report</span><span class="sxs-lookup"><span data-stu-id="84a1b-152">Risky sign-ins report</span></span>](concept-risky-sign-ins.md)
- [<span data-ttu-id="84a1b-153">Audit logs report</span><span class="sxs-lookup"><span data-stu-id="84a1b-153">Audit logs report</span></span>](concept-audit-logs.md)
- [<span data-ttu-id="84a1b-154">Sign-ins logs report</span><span class="sxs-lookup"><span data-stu-id="84a1b-154">Sign-ins logs report</span></span>](concept-sign-ins.md)

<span data-ttu-id="84a1b-155">If you want to know more about accessing the reporting data using the reporting API, see:</span><span class="sxs-lookup"><span data-stu-id="84a1b-155">If you want to know more about accessing the reporting data using the reporting API, see:</span></span> 

- [<span data-ttu-id="84a1b-156">Getting started with the Azure Active Directory reporting API</span><span class="sxs-lookup"><span data-stu-id="84a1b-156">Getting started with the Azure Active Directory reporting API</span></span>](concept-reporting-api.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png