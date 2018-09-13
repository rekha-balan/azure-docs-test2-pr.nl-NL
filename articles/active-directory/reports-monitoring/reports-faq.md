---
title: Azure Active Directory Reporting FAQ | Microsoft Docs
description: Azure Active Directory reporting FAQ.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: report-monitor
ms.date: 05/10/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: f1683321e23eff82e73dc9bb44941fc390633b8c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968516"
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="6dd1a-103">Azure Active Directory reporting FAQ</span><span class="sxs-lookup"><span data-stu-id="6dd1a-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="6dd1a-104">This article includes answers to frequently asked questions about Azure Active Directory (Azure AD) reporting.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-104">This article includes answers to frequently asked questions about Azure Active Directory (Azure AD) reporting.</span></span> <span data-ttu-id="6dd1a-105">For more information, see [Azure Active Directory reporting](overview-reports.md).</span><span class="sxs-lookup"><span data-stu-id="6dd1a-105">For more information, see [Azure Active Directory reporting](overview-reports.md).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="6dd1a-106">Getting started</span><span class="sxs-lookup"><span data-stu-id="6dd1a-106">Getting started</span></span> 

<span data-ttu-id="6dd1a-107">**Q: I am using the https://graph.windows.net/&lt;tenant-name&gt;/reports/ endpoint APIs to pull Azure AD audit and integrated application usage reports into our reporting systems programmatically. What should I switch to?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-107">**Q: I am using the https://graph.windows.net/&lt;tenant-name&gt;/reports/ endpoint APIs to pull Azure AD audit and integrated application usage reports into our reporting systems programmatically. What should I switch to?**</span></span>

<span data-ttu-id="6dd1a-108">**A:** Look up the [API reference documentation](https://developer.microsoft.com/graph/) to see how you can use the new APIs to access [activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="6dd1a-108">**A:** Look up the [API reference documentation](https://developer.microsoft.com/graph/) to see how you can use the new APIs to access [activity reports](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started-azure-portal).</span></span> <span data-ttu-id="6dd1a-109">This endpoint has two reports (Audit and Sign-ins) which provide all the data you got in the old API endpoint.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-109">This endpoint has two reports (Audit and Sign-ins) which provide all the data you got in the old API endpoint.</span></span> <span data-ttu-id="6dd1a-110">This new endpoint also has a sign-ins report with the Azure AD Premium license that you can use to get app usage, device usage, and user sign-in information.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-110">This new endpoint also has a sign-ins report with the Azure AD Premium license that you can use to get app usage, device usage, and user sign-in information.</span></span>

--- 

<span data-ttu-id="6dd1a-111">**Q: I am using the https://graph.windows.net/&lt;tenant-name&gt;/reports/ endpoint APIs to pull Azure AD security reports (specific types of detections, such as leaked credentials or sign-ins from anonymous IP addresses) into our reporting systems programmatically. What should I switch to?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-111">**Q: I am using the https://graph.windows.net/&lt;tenant-name&gt;/reports/ endpoint APIs to pull Azure AD security reports (specific types of detections, such as leaked credentials or sign-ins from anonymous IP addresses) into our reporting systems programmatically. What should I switch to?**</span></span>

<span data-ttu-id="6dd1a-112">**A:** You can use the [Identity Protection risk events API](../identity-protection/graph-get-started.md) to access security detections through Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-112">**A:** You can use the [Identity Protection risk events API](../identity-protection/graph-get-started.md) to access security detections through Microsoft Graph.</span></span> <span data-ttu-id="6dd1a-113">This new format gives greater flexibility in how you can query data, with advanced filtering, field selection, and more, and standardizes risk events into one type for easier integration into SIEMs and other data collection tools.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-113">This new format gives greater flexibility in how you can query data, with advanced filtering, field selection, and more, and standardizes risk events into one type for easier integration into SIEMs and other data collection tools.</span></span> <span data-ttu-id="6dd1a-114">Because the data is in a different format, you can't substitute a new query for your old queries.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-114">Because the data is in a different format, you can't substitute a new query for your old queries.</span></span> <span data-ttu-id="6dd1a-115">However, [the new API uses Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/identityriskevent), which is the Microsoft standard for such APIs as O365 or Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-115">However, [the new API uses Microsoft Graph](https://developer.microsoft.com/graph/docs/api-reference/beta/resources/identityriskevent), which is the Microsoft standard for such APIs as O365 or Azure AD.</span></span> <span data-ttu-id="6dd1a-116">So the work required can either extend your current MS Graph investments or help you begin your transition to this new standard platform.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-116">So the work required can either extend your current MS Graph investments or help you begin your transition to this new standard platform.</span></span>

--- 

<span data-ttu-id="6dd1a-117">**Q: How do I get a premium license?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-117">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="6dd1a-118">**A:** See [Getting started with Azure Active Directory Premium](../fundamentals/active-directory-get-started-premium.md) for an answer to this question.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-118">**A:** See [Getting started with Azure Active Directory Premium](../fundamentals/active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="6dd1a-119">**Q: How soon should I see activities data after getting a premium license?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-119">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="6dd1a-120">**A:** If you already have activities data as a free license, then you can see the same data.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-120">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="6dd1a-121">If you don’t have any data, then it will take one or two days.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-121">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="6dd1a-122">**Q: Do I see last month's data after getting an Azure AD premium license?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-122">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="6dd1a-123">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-123">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="6dd1a-124">When data accumulates, you will see up to 30 days.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-124">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="6dd1a-125">**Q: Do I need to be a global admin to see the activity sign-ins to the Azure portal or to get data through the API?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-125">**Q: Do I need to be a global admin to see the activity sign-ins to the Azure portal or to get data through the API?**</span></span>

<span data-ttu-id="6dd1a-126">**A:** No.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-126">**A:** No.</span></span> <span data-ttu-id="6dd1a-127">You must be a **Security Reader**, a **Security Admin**, or a **Global Admin** to get reporting data in the Azure portal or through the API.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-127">You must be a **Security Reader**, a **Security Admin**, or a **Global Admin** to get reporting data in the Azure portal or through the API.</span></span>

---


## <a name="activity-logs"></a><span data-ttu-id="6dd1a-128">Activity logs</span><span class="sxs-lookup"><span data-stu-id="6dd1a-128">Activity logs</span></span>


<span data-ttu-id="6dd1a-129">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-129">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="6dd1a-130">**A:** See [for how long is the collected data stored?](reference-reports-data-retention.md#q-for-how-long-is-the-collected-data-stored) for an answer to this question.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-130">**A:** See [for how long is the collected data stored?](reference-reports-data-retention.md#q-for-how-long-is-the-collected-data-stored) for an answer to this question.</span></span>

--- 

<span data-ttu-id="6dd1a-131">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-131">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="6dd1a-132">**A:** Audit activity logs have a latency ranging from 15 minutes to an hour.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-132">**A:** Audit activity logs have a latency ranging from 15 minutes to an hour.</span></span> <span data-ttu-id="6dd1a-133">Sign-in activity logs can take from 15 minutes to up to 2 hours for some records.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-133">Sign-in activity logs can take from 15 minutes to up to 2 hours for some records.</span></span>

---


<span data-ttu-id="6dd1a-134">**Q: Can I get Office 365 activity log information through the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-134">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="6dd1a-135">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-135">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="6dd1a-136">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-136">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="6dd1a-137">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="6dd1a-137">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="6dd1a-138">**Q: How many records I can download from Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-138">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="6dd1a-139">**A:** You can download up to 5000 records from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-139">**A:** You can download up to 5000 records from the Azure portal.</span></span> <span data-ttu-id="6dd1a-140">The records are sorted by *most recent* and by default, you get the most recent 5000 records.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-140">The records are sorted by *most recent* and by default, you get the most recent 5000 records.</span></span>

---

## <a name="risky-sign-ins"></a><span data-ttu-id="6dd1a-141">Risky sign-ins</span><span class="sxs-lookup"><span data-stu-id="6dd1a-141">Risky sign-ins</span></span>

<span data-ttu-id="6dd1a-142">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-142">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="6dd1a-143">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether interactive or non-interactive.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-143">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether interactive or non-interactive.</span></span> <span data-ttu-id="6dd1a-144">However, all sign-ins only report shows only the interactive sign-ins.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-144">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="6dd1a-145">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-145">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="6dd1a-146">**A:** The option to download *Users flagged for risk* report will be added soon.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-146">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="6dd1a-147">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-147">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="6dd1a-148">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-148">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="6dd1a-149">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-149">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="6dd1a-150">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-150">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report?**</span></span>

<span data-ttu-id="6dd1a-151">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-151">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="6dd1a-152">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-152">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="6dd1a-153">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-153">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---

<span data-ttu-id="6dd1a-154">**Q: What does the risk event "Sign-in with additional risk detected" signify?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-154">**Q: What does the risk event "Sign-in with additional risk detected" signify?**</span></span>

<span data-ttu-id="6dd1a-155">**A:** To give you an insight into all the risky sign-ins in your environment, "Sign-in with additional risk detected" functions as placeholder for sign-ins for detections that are exclusive to Azure AD Identity Protection subscribers.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-155">**A:** To give you an insight into all the risky sign-ins in your environment, "Sign-in with additional risk detected" functions as placeholder for sign-ins for detections that are exclusive to Azure AD Identity Protection subscribers.</span></span>

---

<span data-ttu-id="6dd1a-156">**Q: What does the risk event "Sign-in with additional risk detected" signify?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-156">**Q: What does the risk event "Sign-in with additional risk detected" signify?**</span></span>

<span data-ttu-id="6dd1a-157">**A:** To give you an insight into all the risky sign-ins in your environment, "Sign-in with additional risk detected" functions as placeholder for sign-ins for detections that are exclusive to Azure AD Identity Protection subscribers.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-157">**A:** To give you an insight into all the risky sign-ins in your environment, "Sign-in with additional risk detected" functions as placeholder for sign-ins for detections that are exclusive to Azure AD Identity Protection subscribers.</span></span>

---

## <a name="conditional-access"></a><span data-ttu-id="6dd1a-158">Conditional access</span><span class="sxs-lookup"><span data-stu-id="6dd1a-158">Conditional access</span></span>

<span data-ttu-id="6dd1a-159">**Q: What's new with this feature?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-159">**Q: What's new with this feature?**</span></span>

<span data-ttu-id="6dd1a-160">**A:** Customers can now troubleshoot conditional access policies through all sign-ins report.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-160">**A:** Customers can now troubleshoot conditional access policies through all sign-ins report.</span></span> <span data-ttu-id="6dd1a-161">Customers can review the conditional access status and dive into the details of the policies that applied to the sign-in and the result for each policy.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-161">Customers can review the conditional access status and dive into the details of the policies that applied to the sign-in and the result for each policy.</span></span>

<span data-ttu-id="6dd1a-162">**Q: How do I get started?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-162">**Q: How do I get started?**</span></span>

<span data-ttu-id="6dd1a-163">**A:** To get started:</span><span class="sxs-lookup"><span data-stu-id="6dd1a-163">**A:** To get started:</span></span>
    * <span data-ttu-id="6dd1a-164">Navigate to the sign-ins report in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="6dd1a-164">Navigate to the sign-ins report in the [Azure portal](https://portal.azure.com).</span></span> 
    * <span data-ttu-id="6dd1a-165">Click on the sign-in that you want to troubleshoot.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-165">Click on the sign-in that you want to troubleshoot.</span></span>
    * <span data-ttu-id="6dd1a-166">Navigate to the **Conditional access** tab. Here, you can view all the policies that impacted the sign-in and the result for each policy.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-166">Navigate to the **Conditional access** tab. Here, you can view all the policies that impacted the sign-in and the result for each policy.</span></span> 
    
<span data-ttu-id="6dd1a-167">**Q: What are all possible values for the conditional access status?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-167">**Q: What are all possible values for the conditional access status?**</span></span>

<span data-ttu-id="6dd1a-168">**A:** Conditional access status can have the following values:</span><span class="sxs-lookup"><span data-stu-id="6dd1a-168">**A:** Conditional access status can have the following values:</span></span>
    * <span data-ttu-id="6dd1a-169">**Not Applied**: This means that there was no CA policy with the user and app in scope.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-169">**Not Applied**: This means that there was no CA policy with the user and app in scope.</span></span> 
    * <span data-ttu-id="6dd1a-170">**Success**: This means that there was a CA policy with the user and app in scope and CA policies were successfully satisfied.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-170">**Success**: This means that there was a CA policy with the user and app in scope and CA policies were successfully satisfied.</span></span> 
    * <span data-ttu-id="6dd1a-171">**Failure**: This means that there was a CA policy with the user and app in scope and CA policies were not satisfied.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-171">**Failure**: This means that there was a CA policy with the user and app in scope and CA policies were not satisfied.</span></span> 
    
<span data-ttu-id="6dd1a-172">**Q: What are all possible values for the conditional access policy result?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-172">**Q: What are all possible values for the conditional access policy result?**</span></span>

<span data-ttu-id="6dd1a-173">**A:** A conditional access policy can have the following results:</span><span class="sxs-lookup"><span data-stu-id="6dd1a-173">**A:** A conditional access policy can have the following results:</span></span>
    * <span data-ttu-id="6dd1a-174">**Success**: The policy was successfully satisfied.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-174">**Success**: The policy was successfully satisfied.</span></span>
    * <span data-ttu-id="6dd1a-175">**Failure**: The policy was not satisfied.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-175">**Failure**: The policy was not satisfied.</span></span>
    * <span data-ttu-id="6dd1a-176">**Not applied**: This might be because the policy conditions did not meet.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-176">**Not applied**: This might be because the policy conditions did not meet.</span></span>
    * <span data-ttu-id="6dd1a-177">**Not enabled**: This is due to the policy in disabled state.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-177">**Not enabled**: This is due to the policy in disabled state.</span></span> 
    
<span data-ttu-id="6dd1a-178">**Q: The policy name in the all sign-in report does not match the policy name in CA. Why?**</span><span class="sxs-lookup"><span data-stu-id="6dd1a-178">**Q: The policy name in the all sign-in report does not match the policy name in CA. Why?**</span></span>

<span data-ttu-id="6dd1a-179">**A:** The policy name in the all sign-in report is based on the CA policy name at the time of the sign-in.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-179">**A:** The policy name in the all sign-in report is based on the CA policy name at the time of the sign-in.</span></span> <span data-ttu-id="6dd1a-180">This can be inconsistent with the policy name in CA if you updated the policy name later, that is, after the sign-in.</span><span class="sxs-lookup"><span data-stu-id="6dd1a-180">This can be inconsistent with the policy name in CA if you updated the policy name later, that is, after the sign-in.</span></span>