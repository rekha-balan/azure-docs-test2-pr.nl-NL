---
title: Find Azure Active Directory user activity reports in Azure portal | Microsoft Docs
description: Learn where the Azure Active Directory user activity reports are in the Azure portal.
services: active-directory
documentationcenter: ''
author: priyamohanram
manager: mtillman
editor: ''
ms.service: active-directory
ms.topic: conceptual
ms.workload: identity
ms.component: report-monitor
ms.date: 12/06/2017
ms.author: priyamo
ms.reviewer: dhanyahk
ms.openlocfilehash: 182537d6f07b624f2395f591681ed4596579bde0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864580"
---
# <a name="find-activity-reports-in-the-azure-portal"></a><span data-ttu-id="abfb6-103">Find activity reports in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="abfb6-103">Find activity reports in the Azure portal</span></span>

<span data-ttu-id="abfb6-104">In this article, we describe how to find Azure Active Directory user activity reports in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="abfb6-104">In this article, we describe how to find Azure Active Directory user activity reports in the Azure portal.</span></span>

## <a name="activity-and-integrated-app-reports"></a><span data-ttu-id="abfb6-105">Activity and integrated app reports</span><span class="sxs-lookup"><span data-stu-id="abfb6-105">Activity and integrated app reports</span></span>

<span data-ttu-id="abfb6-106">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span><span class="sxs-lookup"><span data-stu-id="abfb6-106">For context-based reporting in the Azure portal, existing reports are merged into a single view.</span></span> <span data-ttu-id="abfb6-107">A single, underlying API provides the data to the view.</span><span class="sxs-lookup"><span data-stu-id="abfb6-107">A single, underlying API provides the data to the view.</span></span>

<span data-ttu-id="abfb6-108">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="abfb6-108">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Audit logs**.</span></span>

<span data-ttu-id="abfb6-109">![Audit logs](./media/howto-find-activity-reports/482.png "Audit logs")</span><span class="sxs-lookup"><span data-stu-id="abfb6-109">![Audit logs](./media/howto-find-activity-reports/482.png "Audit logs")</span></span>

<span data-ttu-id="abfb6-110">The following reports are consolidated in this view:</span><span class="sxs-lookup"><span data-stu-id="abfb6-110">The following reports are consolidated in this view:</span></span>

* <span data-ttu-id="abfb6-111">Audit report</span><span class="sxs-lookup"><span data-stu-id="abfb6-111">Audit report</span></span>
* <span data-ttu-id="abfb6-112">Password reset activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-112">Password reset activity</span></span>
* <span data-ttu-id="abfb6-113">Password reset registration activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-113">Password reset registration activity</span></span>
* <span data-ttu-id="abfb6-114">Self-service groups activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-114">Self-service groups activity</span></span>
* <span data-ttu-id="abfb6-115">Office365 Group Name Changes</span><span class="sxs-lookup"><span data-stu-id="abfb6-115">Office365 Group Name Changes</span></span>
* <span data-ttu-id="abfb6-116">Account provisioning activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-116">Account provisioning activity</span></span>
* <span data-ttu-id="abfb6-117">Password rollover status</span><span class="sxs-lookup"><span data-stu-id="abfb6-117">Password rollover status</span></span>
* <span data-ttu-id="abfb6-118">Account provisioning errors</span><span class="sxs-lookup"><span data-stu-id="abfb6-118">Account provisioning errors</span></span>


<span data-ttu-id="abfb6-119">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span><span class="sxs-lookup"><span data-stu-id="abfb6-119">The Application Usage report has been enhanced and is included in the **Sign-ins** view.</span></span> <span data-ttu-id="abfb6-120">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span><span class="sxs-lookup"><span data-stu-id="abfb6-120">To see this view, on the **Azure Active Directory** blade, under **ACTIVITY**, select **Sign-ins**.</span></span>

<span data-ttu-id="abfb6-121">![Sign-ins view](./media/howto-find-activity-reports/483.png "Sign-ins view")</span><span class="sxs-lookup"><span data-stu-id="abfb6-121">![Sign-ins view](./media/howto-find-activity-reports/483.png "Sign-ins view")</span></span>

<span data-ttu-id="abfb6-122">The **Sign-ins** view includes all user sign-ins. You can use this information to get application usage information.</span><span class="sxs-lookup"><span data-stu-id="abfb6-122">The **Sign-ins** view includes all user sign-ins. You can use this information to get application usage information.</span></span> <span data-ttu-id="abfb6-123">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span><span class="sxs-lookup"><span data-stu-id="abfb6-123">You also can view application usage information in the **Enterprise applications** overview, in the **MANAGE** section.</span></span>

<span data-ttu-id="abfb6-124">![Enterprise applications](./media/howto-find-activity-reports/484.png "Enterprise applications")</span><span class="sxs-lookup"><span data-stu-id="abfb6-124">![Enterprise applications](./media/howto-find-activity-reports/484.png "Enterprise applications")</span></span>

## <a name="access-a-specific-report"></a><span data-ttu-id="abfb6-125">Access a specific report</span><span class="sxs-lookup"><span data-stu-id="abfb6-125">Access a specific report</span></span>

<span data-ttu-id="abfb6-126">Although the Azure portal offers a single view, you also can look at specific reports.</span><span class="sxs-lookup"><span data-stu-id="abfb6-126">Although the Azure portal offers a single view, you also can look at specific reports.</span></span>

### <a name="audit-logs"></a><span data-ttu-id="abfb6-127">Audit logs</span><span class="sxs-lookup"><span data-stu-id="abfb6-127">Audit logs</span></span>

<span data-ttu-id="abfb6-128">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span><span class="sxs-lookup"><span data-stu-id="abfb6-128">In response to customer feedback, in the Azure portal, you can use advanced filtering to access the data you want.</span></span> <span data-ttu-id="abfb6-129">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abfb6-129">One filter you can use is an *activity category*, which lists the different types of activity logs in Azure AD.</span></span> <span data-ttu-id="abfb6-130">To narrow results to what you are looking for, you can select a category.</span><span class="sxs-lookup"><span data-stu-id="abfb6-130">To narrow results to what you are looking for, you can select a category.</span></span>

<span data-ttu-id="abfb6-131">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span><span class="sxs-lookup"><span data-stu-id="abfb6-131">For example, if you are interested only in activities related to self-service password resets, you can choose the **Self-service Password Management** category.</span></span> <span data-ttu-id="abfb6-132">The categories you see are based on the resource you are working in.</span><span class="sxs-lookup"><span data-stu-id="abfb6-132">The categories you see are based on the resource you are working in.</span></span>  

<span data-ttu-id="abfb6-133">![Category options on the Filter Audit Logs page](./media/howto-find-activity-reports/06.png "Category options on the Filter Audit Logs page")</span><span class="sxs-lookup"><span data-stu-id="abfb6-133">![Category options on the Filter Audit Logs page](./media/howto-find-activity-reports/06.png "Category options on the Filter Audit Logs page")</span></span>

<span data-ttu-id="abfb6-134">Activity categories include:</span><span class="sxs-lookup"><span data-stu-id="abfb6-134">Activity categories include:</span></span>

- <span data-ttu-id="abfb6-135">Core Directory</span><span class="sxs-lookup"><span data-stu-id="abfb6-135">Core Directory</span></span>
- <span data-ttu-id="abfb6-136">Self-service Password Management</span><span class="sxs-lookup"><span data-stu-id="abfb6-136">Self-service Password Management</span></span>
- <span data-ttu-id="abfb6-137">Self-service Group Management</span><span class="sxs-lookup"><span data-stu-id="abfb6-137">Self-service Group Management</span></span>
- <span data-ttu-id="abfb6-138">Account Provisioning</span><span class="sxs-lookup"><span data-stu-id="abfb6-138">Account Provisioning</span></span>

### <a name="application-usage"></a><span data-ttu-id="abfb6-139">Application usage</span><span class="sxs-lookup"><span data-stu-id="abfb6-139">Application usage</span></span>

<span data-ttu-id="abfb6-140">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. To narrow the results, you can filter on user name or application name.</span><span class="sxs-lookup"><span data-stu-id="abfb6-140">To view details about application usage for all apps or for a single app, under **ACTIVITY**, select **Sign-ins**. To narrow the results, you can filter on user name or application name.</span></span>

<span data-ttu-id="abfb6-141">![Filter Sign-In Events page](./media/howto-find-activity-reports/07.png "Filter Sign-In Events page")</span><span class="sxs-lookup"><span data-stu-id="abfb6-141">![Filter Sign-In Events page](./media/howto-find-activity-reports/07.png "Filter Sign-In Events page")</span></span>

### <a name="security-reports"></a><span data-ttu-id="abfb6-142">Security reports</span><span class="sxs-lookup"><span data-stu-id="abfb6-142">Security reports</span></span>

#### <a name="azure-ad-anomalous-activity-reports"></a><span data-ttu-id="abfb6-143">Azure AD anomalous activity reports</span><span class="sxs-lookup"><span data-stu-id="abfb6-143">Azure AD anomalous activity reports</span></span>

<span data-ttu-id="abfb6-144">Azure AD anomalous activity security reports are consolidated to provide you with one central view.</span><span class="sxs-lookup"><span data-stu-id="abfb6-144">Azure AD anomalous activity security reports are consolidated to provide you with one central view.</span></span> <span data-ttu-id="abfb6-145">This view shows all security-related risk events that Azure AD can detect and report on.</span><span class="sxs-lookup"><span data-stu-id="abfb6-145">This view shows all security-related risk events that Azure AD can detect and report on.</span></span>

<span data-ttu-id="abfb6-146">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="abfb6-146">The following table lists the Azure AD anomalous activity security reports, and corresponding risk event types in the Azure portal.</span></span>

| <span data-ttu-id="abfb6-147">Azure AD anomalous activity report</span><span class="sxs-lookup"><span data-stu-id="abfb6-147">Azure AD anomalous activity report</span></span> |  <span data-ttu-id="abfb6-148">Identity protection risk event type</span><span class="sxs-lookup"><span data-stu-id="abfb6-148">Identity protection risk event type</span></span>|
| :--- | :--- |
| <span data-ttu-id="abfb6-149">Users with leaked credentials</span><span class="sxs-lookup"><span data-stu-id="abfb6-149">Users with leaked credentials</span></span> | <span data-ttu-id="abfb6-150">Leaked credentials</span><span class="sxs-lookup"><span data-stu-id="abfb6-150">Leaked credentials</span></span> |
| <span data-ttu-id="abfb6-151">Irregular sign-in activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-151">Irregular sign-in activity</span></span> | <span data-ttu-id="abfb6-152">Impossible travel to atypical locations</span><span class="sxs-lookup"><span data-stu-id="abfb6-152">Impossible travel to atypical locations</span></span> |
| <span data-ttu-id="abfb6-153">Sign-ins from possibly infected devices</span><span class="sxs-lookup"><span data-stu-id="abfb6-153">Sign-ins from possibly infected devices</span></span> | <span data-ttu-id="abfb6-154">Sign-ins from infected devices</span><span class="sxs-lookup"><span data-stu-id="abfb6-154">Sign-ins from infected devices</span></span>|
| <span data-ttu-id="abfb6-155">Sign-ins from unknown sources</span><span class="sxs-lookup"><span data-stu-id="abfb6-155">Sign-ins from unknown sources</span></span> | <span data-ttu-id="abfb6-156">Sign-ins from anonymous IP addresses</span><span class="sxs-lookup"><span data-stu-id="abfb6-156">Sign-ins from anonymous IP addresses</span></span> |
| <span data-ttu-id="abfb6-157">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-157">Sign-ins from IP addresses with suspicious activity</span></span> | <span data-ttu-id="abfb6-158">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="abfb6-158">Sign-ins from IP addresses with suspicious activity</span></span> |
| - | <span data-ttu-id="abfb6-159">Sign-ins from unfamiliar locations</span><span class="sxs-lookup"><span data-stu-id="abfb6-159">Sign-ins from unfamiliar locations</span></span> |

<span data-ttu-id="abfb6-160">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="abfb6-160">The following Azure AD anomalous activity security reports are not included as risk events in the Azure portal:</span></span>

* <span data-ttu-id="abfb6-161">Sign-ins after multiple failures</span><span class="sxs-lookup"><span data-stu-id="abfb6-161">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="abfb6-162">Sign-ins from multiple geographies</span><span class="sxs-lookup"><span data-stu-id="abfb6-162">Sign-ins from multiple geographies</span></span>

<span data-ttu-id="abfb6-163">For more information, see [Azure Active Directory risk events](concept-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="abfb6-163">For more information, see [Azure Active Directory risk events](concept-risk-events.md).</span></span>  


#### <a name="detected-risk-events"></a><span data-ttu-id="abfb6-164">Detected risk events</span><span class="sxs-lookup"><span data-stu-id="abfb6-164">Detected risk events</span></span>

<span data-ttu-id="abfb6-165">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span><span class="sxs-lookup"><span data-stu-id="abfb6-165">In the Azure portal, you can access reports about detected risk events on the **Azure Active Directory** blade, under **SECURITY**.</span></span> <span data-ttu-id="abfb6-166">Detected risk events are tracked in the following reports:</span><span class="sxs-lookup"><span data-stu-id="abfb6-166">Detected risk events are tracked in the following reports:</span></span>   

- <span data-ttu-id="abfb6-167">Users at Risk</span><span class="sxs-lookup"><span data-stu-id="abfb6-167">Users at Risk</span></span>
- <span data-ttu-id="abfb6-168">Risky Sign-ins</span><span class="sxs-lookup"><span data-stu-id="abfb6-168">Risky Sign-ins</span></span>

<span data-ttu-id="abfb6-169">![Security reports](./media/howto-find-activity-reports/04.png "Security reports")</span><span class="sxs-lookup"><span data-stu-id="abfb6-169">![Security reports](./media/howto-find-activity-reports/04.png "Security reports")</span></span>

<span data-ttu-id="abfb6-170">For more information about security reports, see:</span><span class="sxs-lookup"><span data-stu-id="abfb6-170">For more information about security reports, see:</span></span>

- [<span data-ttu-id="abfb6-171">Users at Risk security report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="abfb6-171">Users at Risk security report in the Azure Active Directory portal</span></span>](concept-user-at-risk.md)
- [<span data-ttu-id="abfb6-172">Risky Sign-ins report in the Azure Active Directory portal</span><span class="sxs-lookup"><span data-stu-id="abfb6-172">Risky Sign-ins report in the Azure Active Directory portal</span></span>](concept-risky-sign-ins.md)


<span data-ttu-id="abfb6-173">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span><span class="sxs-lookup"><span data-stu-id="abfb6-173">To view the **Application Usage** report, on the **Azure Active Directory** blade, under **MANAGE**, select **Enterprise Applications**, and then select **Sign-ins**.</span></span>


![Enterprise Applications Sign-Ins report](./media/howto-find-activity-reports/199.png)

## <a name="next-steps"></a><span data-ttu-id="abfb6-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="abfb6-175">Next steps</span></span>

<span data-ttu-id="abfb6-176">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span><span class="sxs-lookup"><span data-stu-id="abfb6-176">For an overview of reporting, see the [Azure Active Directory reporting](overview-reports.md).</span></span>
