---
title: Problem using self-service application access | Microsoft Docs
description: Troubleshoot problems related to self-service application access
services: active-directory
documentationcenter: ''
author: ajamess
manager: femila
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: asteen
ms.openlocfilehash: 4d8c241344485e50a1afde3cd67adf3d0a7c041f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672339"
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="3493f-103">Problem using self-service application access</span><span class="sxs-lookup"><span data-stu-id="3493f-103">Problem using self-service application access</span></span>

<span data-ttu-id="3493f-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span><span class="sxs-lookup"><span data-stu-id="3493f-104">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="3493f-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span><span class="sxs-lookup"><span data-stu-id="3493f-105">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="3493f-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span><span class="sxs-lookup"><span data-stu-id="3493f-106">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="3493f-107">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="3493f-107">General issues to check first</span></span>

-   <span data-ttu-id="3493f-108">Make sure self-service application access is configured correctly.</span><span class="sxs-lookup"><span data-stu-id="3493f-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="3493f-109">See “How to configure self-service application access”.</span><span class="sxs-lookup"><span data-stu-id="3493f-109">See “How to configure self-service application access”.</span></span>

-   <span data-ttu-id="3493f-110">Make sure the user or group has been enabled to request self-service application access.</span><span class="sxs-lookup"><span data-stu-id="3493f-110">Make sure the user or group has been enabled to request self-service application access.</span></span>

-   <span data-ttu-id="3493f-111">Make sure the user is visiting the correct place for self-service application access.</span><span class="sxs-lookup"><span data-stu-id="3493f-111">Make sure the user is visiting the correct place for self-service application access.</span></span> <span data-ttu-id="3493f-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span><span class="sxs-lookup"><span data-stu-id="3493f-112">users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled self-service access.</span></span>

-   <span data-ttu-id="3493f-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span><span class="sxs-lookup"><span data-stu-id="3493f-113">If self-service application access was just recently configured, try to sign in and out again into the user’s Access Panel after a few minutes to see if the self-service access changes have appeared.</span></span>

## <a name="how-to-configure-self-service-application-access"></a><span data-ttu-id="3493f-114">How to configure self-service application access</span><span class="sxs-lookup"><span data-stu-id="3493f-114">How to configure self-service application access</span></span>

<span data-ttu-id="3493f-115">To enable self-service application access to an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="3493f-115">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="3493f-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="3493f-116">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3493f-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3493f-117">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3493f-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="3493f-118">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3493f-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3493f-119">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3493f-120">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="3493f-120">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="3493f-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="3493f-121">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="3493f-122">Select the application you want to enable Self-service access to from the list.</span><span class="sxs-lookup"><span data-stu-id="3493f-122">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="3493f-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="3493f-123">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3493f-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span><span class="sxs-lookup"><span data-stu-id="3493f-124">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="3493f-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span><span class="sxs-lookup"><span data-stu-id="3493f-125">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="3493f-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3493f-126">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="3493f-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="3493f-127">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="3493f-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span><span class="sxs-lookup"><span data-stu-id="3493f-128">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="3493f-129">Groups are not supported.</span><span class="sxs-lookup"><span data-stu-id="3493f-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="3493f-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span><span class="sxs-lookup"><span data-stu-id="3493f-130">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="3493f-131">Click the **Save** button at the top of the blade to finish.</span><span class="sxs-lookup"><span data-stu-id="3493f-131">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="3493f-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span><span class="sxs-lookup"><span data-stu-id="3493f-132">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="3493f-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3493f-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="3493f-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span><span class="sxs-lookup"><span data-stu-id="3493f-134">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="3493f-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span><span class="sxs-lookup"><span data-stu-id="3493f-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access to the application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-the-issue"></a><span data-ttu-id="3493f-136">If these troubleshooting steps do not resolve the issue</span><span class="sxs-lookup"><span data-stu-id="3493f-136">If these troubleshooting steps do not resolve the issue</span></span> 

<span data-ttu-id="3493f-137">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="3493f-137">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="3493f-138">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="3493f-138">Correlation error ID</span></span>

-   <span data-ttu-id="3493f-139">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="3493f-139">UPN (user email address)</span></span>

-   <span data-ttu-id="3493f-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="3493f-140">TenantID</span></span>

-   <span data-ttu-id="3493f-141">Browser type</span><span class="sxs-lookup"><span data-stu-id="3493f-141">Browser type</span></span>

-   <span data-ttu-id="3493f-142">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="3493f-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="3493f-143">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="3493f-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="3493f-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="3493f-144">Next steps</span></span>
[<span data-ttu-id="3493f-145">Setting up Azure Active Directory for self-service group management</span><span class="sxs-lookup"><span data-stu-id="3493f-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
