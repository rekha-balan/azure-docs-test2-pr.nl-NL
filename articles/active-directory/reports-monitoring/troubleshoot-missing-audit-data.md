---
title: Troubleshoot Missing data in the Azure Active Directory activity logs  | Microsoft Docs
description: Provides you with a resolution to missing data in Azure Active Directory activity logs.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.component: report-monitor
ms.date: 01/15/2018
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 871dd3fda0ee5dc350a468f16e8f389ac3c71d34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869101"
---
# <a name="troubleshoot-missing-data-in-the-azure-active-directory-activity-logs"></a><span data-ttu-id="45041-103">Troubleshoot: Missing data in the Azure Active Directory activity logs</span><span class="sxs-lookup"><span data-stu-id="45041-103">Troubleshoot: Missing data in the Azure Active Directory activity logs</span></span> 

## <a name="i-cant-find-audit-logs-for-recent-actions-in-the-azure-portal"></a><span data-ttu-id="45041-104">I can't find audit logs for recent actions in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="45041-104">I can't find audit logs for recent actions in the Azure portal</span></span>

### <a name="symptoms"></a><span data-ttu-id="45041-105">Symptoms</span><span class="sxs-lookup"><span data-stu-id="45041-105">Symptoms</span></span>

<span data-ttu-id="45041-106">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span><span class="sxs-lookup"><span data-stu-id="45041-106">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Reporting](./media/troubleshoot-missing-audit-data/01.png)
 
### <a name="cause"></a><span data-ttu-id="45041-108">Cause</span><span class="sxs-lookup"><span data-stu-id="45041-108">Cause</span></span>

<span data-ttu-id="45041-109">Actions don’t appear immediately in the activity logs.</span><span class="sxs-lookup"><span data-stu-id="45041-109">Actions don’t appear immediately in the activity logs.</span></span> <span data-ttu-id="45041-110">The table below enumerates our latency numbers for activity logs.</span><span class="sxs-lookup"><span data-stu-id="45041-110">The table below enumerates our latency numbers for activity logs.</span></span> 

| <span data-ttu-id="45041-111">Report</span><span class="sxs-lookup"><span data-stu-id="45041-111">Report</span></span> | &nbsp; | <span data-ttu-id="45041-112">Latency (P95)</span><span class="sxs-lookup"><span data-stu-id="45041-112">Latency (P95)</span></span> | <span data-ttu-id="45041-113">Latency (P99)</span><span class="sxs-lookup"><span data-stu-id="45041-113">Latency (P99)</span></span> |
|--------|--------|---------------|---------------|
| <span data-ttu-id="45041-114">Directory audit</span><span class="sxs-lookup"><span data-stu-id="45041-114">Directory audit</span></span> | &nbsp; | <span data-ttu-id="45041-115">2 mins</span><span class="sxs-lookup"><span data-stu-id="45041-115">2 mins</span></span> | <span data-ttu-id="45041-116">5 mins</span><span class="sxs-lookup"><span data-stu-id="45041-116">5 mins</span></span> |
| <span data-ttu-id="45041-117">Sign-in activity</span><span class="sxs-lookup"><span data-stu-id="45041-117">Sign-in activity</span></span> | &nbsp; | <span data-ttu-id="45041-118">2 mins</span><span class="sxs-lookup"><span data-stu-id="45041-118">2 mins</span></span> | <span data-ttu-id="45041-119">5 mins</span><span class="sxs-lookup"><span data-stu-id="45041-119">5 mins</span></span> | 

### <a name="resolution"></a><span data-ttu-id="45041-120">Resolution</span><span class="sxs-lookup"><span data-stu-id="45041-120">Resolution</span></span>

<span data-ttu-id="45041-121">Wait for 15 minutes to two hours and see if the actions appear in the log.</span><span class="sxs-lookup"><span data-stu-id="45041-121">Wait for 15 minutes to two hours and see if the actions appear in the log.</span></span> <span data-ttu-id="45041-122">If you don’t see the logs even after two hours, please [file a support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) and we will look into it.</span><span class="sxs-lookup"><span data-stu-id="45041-122">If you don’t see the logs even after two hours, please [file a support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) and we will look into it.</span></span>

## <a name="i-cant-find-recent-user-sign-ins-in-the-azure-active-directory-sign-ins-activity-log"></a><span data-ttu-id="45041-123">I can’t find recent user sign-ins in the Azure Active Directory sign-ins activity log</span><span class="sxs-lookup"><span data-stu-id="45041-123">I can’t find recent user sign-ins in the Azure Active Directory sign-ins activity log</span></span>

### <a name="symptoms"></a><span data-ttu-id="45041-124">Symptoms</span><span class="sxs-lookup"><span data-stu-id="45041-124">Symptoms</span></span>

<span data-ttu-id="45041-125">I recently signed into the Azure portal and expected to see the sign-in logs for those actions in the `Activity logs > Sign-ins` blade, but I can’t find them.</span><span class="sxs-lookup"><span data-stu-id="45041-125">I recently signed into the Azure portal and expected to see the sign-in logs for those actions in the `Activity logs > Sign-ins` blade, but I can’t find them.</span></span>

 ![Reporting](./media/troubleshoot-missing-audit-data/02.png)
 
### <a name="cause"></a><span data-ttu-id="45041-127">Cause</span><span class="sxs-lookup"><span data-stu-id="45041-127">Cause</span></span>

<span data-ttu-id="45041-128">Actions don’t appear immediately in the activity logs.</span><span class="sxs-lookup"><span data-stu-id="45041-128">Actions don’t appear immediately in the activity logs.</span></span> <span data-ttu-id="45041-129">The table below enumerates our latency numbers for activity logs.</span><span class="sxs-lookup"><span data-stu-id="45041-129">The table below enumerates our latency numbers for activity logs.</span></span> 

| <span data-ttu-id="45041-130">Report</span><span class="sxs-lookup"><span data-stu-id="45041-130">Report</span></span> | &nbsp; | <span data-ttu-id="45041-131">Latency (P95)</span><span class="sxs-lookup"><span data-stu-id="45041-131">Latency (P95)</span></span> | <span data-ttu-id="45041-132">Latency (P99)</span><span class="sxs-lookup"><span data-stu-id="45041-132">Latency (P99)</span></span> |
|--------|--------|---------------|---------------|
| <span data-ttu-id="45041-133">Directory audit</span><span class="sxs-lookup"><span data-stu-id="45041-133">Directory audit</span></span> | &nbsp; | <span data-ttu-id="45041-134">2 mins</span><span class="sxs-lookup"><span data-stu-id="45041-134">2 mins</span></span> | <span data-ttu-id="45041-135">5 mins</span><span class="sxs-lookup"><span data-stu-id="45041-135">5 mins</span></span> |
| <span data-ttu-id="45041-136">Sign-in activity</span><span class="sxs-lookup"><span data-stu-id="45041-136">Sign-in activity</span></span> | &nbsp; | <span data-ttu-id="45041-137">2 mins</span><span class="sxs-lookup"><span data-stu-id="45041-137">2 mins</span></span> | <span data-ttu-id="45041-138">5 mins</span><span class="sxs-lookup"><span data-stu-id="45041-138">5 mins</span></span> | 

### <a name="resolution"></a><span data-ttu-id="45041-139">Resolution</span><span class="sxs-lookup"><span data-stu-id="45041-139">Resolution</span></span>

<span data-ttu-id="45041-140">Wait for 15 minutes to two hours and see if the actions appear in the log.</span><span class="sxs-lookup"><span data-stu-id="45041-140">Wait for 15 minutes to two hours and see if the actions appear in the log.</span></span> <span data-ttu-id="45041-141">If you don’t see the logs even after two hours, please [file a support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) and we will look into it.</span><span class="sxs-lookup"><span data-stu-id="45041-141">If you don’t see the logs even after two hours, please [file a support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) and we will look into it.</span></span>

## <a name="i-cant-view-more-than-30-days-of-report-data-in-the-azure-portal"></a><span data-ttu-id="45041-142">I can't view more than 30 days of report data in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="45041-142">I can't view more than 30 days of report data in the Azure portal</span></span>

### <a name="symptoms"></a><span data-ttu-id="45041-143">Symptoms</span><span class="sxs-lookup"><span data-stu-id="45041-143">Symptoms</span></span>

<span data-ttu-id="45041-144">I can't view more than 30 days of sign-in and audit data from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="45041-144">I can't view more than 30 days of sign-in and audit data from the Azure portal.</span></span> <span data-ttu-id="45041-145">Why?</span><span class="sxs-lookup"><span data-stu-id="45041-145">Why?</span></span> 

 ![Reporting](./media/troubleshoot-missing-audit-data/03.png)

### <a name="cause"></a><span data-ttu-id="45041-147">Cause</span><span class="sxs-lookup"><span data-stu-id="45041-147">Cause</span></span>

<span data-ttu-id="45041-148">Depending on your license, Azure Active Directory Actions stores activity reports for the following durations:</span><span class="sxs-lookup"><span data-stu-id="45041-148">Depending on your license, Azure Active Directory Actions stores activity reports for the following durations:</span></span>

| <span data-ttu-id="45041-149">Report</span><span class="sxs-lookup"><span data-stu-id="45041-149">Report</span></span>           | &nbsp; |  <span data-ttu-id="45041-150">Azure AD Free</span><span class="sxs-lookup"><span data-stu-id="45041-150">Azure AD Free</span></span> | <span data-ttu-id="45041-151">Azure AD Premium P1</span><span class="sxs-lookup"><span data-stu-id="45041-151">Azure AD Premium P1</span></span> | <span data-ttu-id="45041-152">Azure AD Premium P2</span><span class="sxs-lookup"><span data-stu-id="45041-152">Azure AD Premium P2</span></span> |
| ---              | ----   |  ---           | ---                 | ---                 |
| <span data-ttu-id="45041-153">Directory Audit</span><span class="sxs-lookup"><span data-stu-id="45041-153">Directory Audit</span></span>  | &nbsp; |   <span data-ttu-id="45041-154">7 days</span><span class="sxs-lookup"><span data-stu-id="45041-154">7 days</span></span>     | <span data-ttu-id="45041-155">30 days</span><span class="sxs-lookup"><span data-stu-id="45041-155">30 days</span></span>             | <span data-ttu-id="45041-156">30 days</span><span class="sxs-lookup"><span data-stu-id="45041-156">30 days</span></span>             |
| <span data-ttu-id="45041-157">Sign-in Activity</span><span class="sxs-lookup"><span data-stu-id="45041-157">Sign-in Activity</span></span> | &nbsp; | <span data-ttu-id="45041-158">Not available.</span><span class="sxs-lookup"><span data-stu-id="45041-158">Not available.</span></span> <span data-ttu-id="45041-159">You can access your own sign-ins for 7 days from the individual user profile blade</span><span class="sxs-lookup"><span data-stu-id="45041-159">You can access your own sign-ins for 7 days from the individual user profile blade</span></span> | <span data-ttu-id="45041-160">30 days</span><span class="sxs-lookup"><span data-stu-id="45041-160">30 days</span></span> | <span data-ttu-id="45041-161">30 days</span><span class="sxs-lookup"><span data-stu-id="45041-161">30 days</span></span>             |

<span data-ttu-id="45041-162">For more information, see [Azure Active Directory report retention policies](reference-reports-data-retention.md).</span><span class="sxs-lookup"><span data-stu-id="45041-162">For more information, see [Azure Active Directory report retention policies](reference-reports-data-retention.md).</span></span>  

### <a name="resolution"></a><span data-ttu-id="45041-163">Resolution</span><span class="sxs-lookup"><span data-stu-id="45041-163">Resolution</span></span>

<span data-ttu-id="45041-164">You have two options to retain the data for longer than 30 days.</span><span class="sxs-lookup"><span data-stu-id="45041-164">You have two options to retain the data for longer than 30 days.</span></span> <span data-ttu-id="45041-165">You can use the [Azure AD Reporting APIs](concept-reporting-api.md) to retrieve the data programmatically and store it in a database.</span><span class="sxs-lookup"><span data-stu-id="45041-165">You can use the [Azure AD Reporting APIs](concept-reporting-api.md) to retrieve the data programmatically and store it in a database.</span></span> <span data-ttu-id="45041-166">Alternatively, you can integrate audit logs into a third party SIEM system like Splunk or SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="45041-166">Alternatively, you can integrate audit logs into a third party SIEM system like Splunk or SumoLogic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45041-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="45041-167">Next steps</span></span>

* <span data-ttu-id="45041-168">[Azure AD reporting retention](reference-reports-data-retention.md).</span><span class="sxs-lookup"><span data-stu-id="45041-168">[Azure AD reporting retention](reference-reports-data-retention.md).</span></span>
* <span data-ttu-id="45041-169">[Azure Active Directory reporting latencies](reference-reports-latencies.md).</span><span class="sxs-lookup"><span data-stu-id="45041-169">[Azure Active Directory reporting latencies](reference-reports-latencies.md).</span></span>
* <span data-ttu-id="45041-170">[Azure Active Directory reporting FAQ](reports-faq.md).</span><span class="sxs-lookup"><span data-stu-id="45041-170">[Azure Active Directory reporting FAQ](reports-faq.md).</span></span>

