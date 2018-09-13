---
title: Azure Active Directory Terms of use| Microsoft Docs
description: Azure AD Terms of use will allow you and your company the ability to provide Terms of use to users of Azure AD services.
services: active-directory
author: rolyon
manager: mtillman
editor: ''
ms.assetid: d55872ef-7e45-4de5-a9a0-3298e3de3565
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.component: compliance
ms.date: 09/04/2018
ms.author: rolyon
ms.openlocfilehash: fbed0f5fb213a18f4450ee3aa96c3b8485b16e8b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967342"
---
# <a name="azure-active-directory-terms-of-use-feature"></a><span data-ttu-id="f90fe-103">Azure Active Directory Terms of use feature</span><span class="sxs-lookup"><span data-stu-id="f90fe-103">Azure Active Directory Terms of use feature</span></span>
<span data-ttu-id="f90fe-104">Azure AD Terms of use provides a simple method that organizations can use to present information to end users.</span><span class="sxs-lookup"><span data-stu-id="f90fe-104">Azure AD Terms of use provides a simple method that organizations can use to present information to end users.</span></span> <span data-ttu-id="f90fe-105">This presentation ensures users see relevant disclaimers for legal or compliance requirements.</span><span class="sxs-lookup"><span data-stu-id="f90fe-105">This presentation ensures users see relevant disclaimers for legal or compliance requirements.</span></span> <span data-ttu-id="f90fe-106">This article describes how to get started with Azure AD Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-106">This article describes how to get started with Azure AD Terms of use.</span></span>

[!INCLUDE [GDPR-related guidance](../../includes/gdpr-intro-sentence.md)]

## <a name="what-can-i-do-with-terms-of-use"></a><span data-ttu-id="f90fe-107">What can I do with Terms of use?</span><span class="sxs-lookup"><span data-stu-id="f90fe-107">What can I do with Terms of use?</span></span>
<span data-ttu-id="f90fe-108">Azure AD Terms of use enables you to do the following:</span><span class="sxs-lookup"><span data-stu-id="f90fe-108">Azure AD Terms of use enables you to do the following:</span></span>
- <span data-ttu-id="f90fe-109">Require employees or guests to agree to your Terms of use before getting access.</span><span class="sxs-lookup"><span data-stu-id="f90fe-109">Require employees or guests to agree to your Terms of use before getting access.</span></span>
- <span data-ttu-id="f90fe-110">Present general Terms of use for all users in your organization.</span><span class="sxs-lookup"><span data-stu-id="f90fe-110">Present general Terms of use for all users in your organization.</span></span>
- <span data-ttu-id="f90fe-111">Present specific Terms of use based on a user attributes (ex.</span><span class="sxs-lookup"><span data-stu-id="f90fe-111">Present specific Terms of use based on a user attributes (ex.</span></span> <span data-ttu-id="f90fe-112">doctors vs nurses or domestic vs international employees, by using [dynamic groups](users-groups-roles/groups-dynamic-membership.md)).</span><span class="sxs-lookup"><span data-stu-id="f90fe-112">doctors vs nurses or domestic vs international employees, by using [dynamic groups](users-groups-roles/groups-dynamic-membership.md)).</span></span>
- <span data-ttu-id="f90fe-113">Present specific Terms of use when accessing high business impact applications, like Salesforce.</span><span class="sxs-lookup"><span data-stu-id="f90fe-113">Present specific Terms of use when accessing high business impact applications, like Salesforce.</span></span>
- <span data-ttu-id="f90fe-114">Present Terms of use in different languages.</span><span class="sxs-lookup"><span data-stu-id="f90fe-114">Present Terms of use in different languages.</span></span>
- <span data-ttu-id="f90fe-115">List who has or hasn't agreed to your Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-115">List who has or hasn't agreed to your Terms of use.</span></span>
- <span data-ttu-id="f90fe-116">Display an audit log of Terms of use activity.</span><span class="sxs-lookup"><span data-stu-id="f90fe-116">Display an audit log of Terms of use activity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f90fe-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f90fe-117">Prerequisites</span></span>
<span data-ttu-id="f90fe-118">To use and configure Azure AD Terms of use, you must have:</span><span class="sxs-lookup"><span data-stu-id="f90fe-118">To use and configure Azure AD Terms of use, you must have:</span></span>

- <span data-ttu-id="f90fe-119">Azure AD Premium P1, P2, EMS E3, or EMS E5 subscription.</span><span class="sxs-lookup"><span data-stu-id="f90fe-119">Azure AD Premium P1, P2, EMS E3, or EMS E5 subscription.</span></span>
    - <span data-ttu-id="f90fe-120">If you don't have one of theses subscriptions, you can [get Azure AD Premium](fundamentals/active-directory-get-started-premium.md) or [enable Azure AD Premium trial](https://azure.microsoft.com/trial/get-started-active-directory/).</span><span class="sxs-lookup"><span data-stu-id="f90fe-120">If you don't have one of theses subscriptions, you can [get Azure AD Premium](fundamentals/active-directory-get-started-premium.md) or [enable Azure AD Premium trial](https://azure.microsoft.com/trial/get-started-active-directory/).</span></span>
- <span data-ttu-id="f90fe-121">One of the following administrator accounts for the directory you want to configure:</span><span class="sxs-lookup"><span data-stu-id="f90fe-121">One of the following administrator accounts for the directory you want to configure:</span></span>
    - <span data-ttu-id="f90fe-122">Global administrator</span><span class="sxs-lookup"><span data-stu-id="f90fe-122">Global administrator</span></span>
    - <span data-ttu-id="f90fe-123">Security administrator</span><span class="sxs-lookup"><span data-stu-id="f90fe-123">Security administrator</span></span>
    - <span data-ttu-id="f90fe-124">Conditional access administrator</span><span class="sxs-lookup"><span data-stu-id="f90fe-124">Conditional access administrator</span></span>

## <a name="terms-of-use-document"></a><span data-ttu-id="f90fe-125">Terms of use document</span><span class="sxs-lookup"><span data-stu-id="f90fe-125">Terms of use document</span></span>

<span data-ttu-id="f90fe-126">Azure AD Terms of use uses the PDF format to present content.</span><span class="sxs-lookup"><span data-stu-id="f90fe-126">Azure AD Terms of use uses the PDF format to present content.</span></span> <span data-ttu-id="f90fe-127">The PDF file can be any content, such as existing contract documents, allowing you to collect end-user agreements during user sign in.</span><span class="sxs-lookup"><span data-stu-id="f90fe-127">The PDF file can be any content, such as existing contract documents, allowing you to collect end-user agreements during user sign in.</span></span> <span data-ttu-id="f90fe-128">The recommended font size in the PDF is 24.</span><span class="sxs-lookup"><span data-stu-id="f90fe-128">The recommended font size in the PDF is 24.</span></span>

## <a name="add-terms-of-use"></a><span data-ttu-id="f90fe-129">Add Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-129">Add Terms of use</span></span>
<span data-ttu-id="f90fe-130">Once you have finalized your Terms of use document, use the following procedure to add it.</span><span class="sxs-lookup"><span data-stu-id="f90fe-130">Once you have finalized your Terms of use document, use the following procedure to add it.</span></span>

1. <span data-ttu-id="f90fe-131">Sign in to Azure as a Global administrator, Security administrator, or Conditional access administrator.</span><span class="sxs-lookup"><span data-stu-id="f90fe-131">Sign in to Azure as a Global administrator, Security administrator, or Conditional access administrator.</span></span>

1. <span data-ttu-id="f90fe-132">Navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-132">Navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

    ![Terms of use blade](media/active-directory-tou/tou-blade.png)

1. <span data-ttu-id="f90fe-134">Click **New terms**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-134">Click **New terms**.</span></span>

    ![Add TOU](media/active-directory-tou/new-tou.png)

1. <span data-ttu-id="f90fe-136">Enter the **Name** for the Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-136">Enter the **Name** for the Terms of use</span></span>

2. <span data-ttu-id="f90fe-137">Enter **Display name**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-137">Enter **Display name**.</span></span>  <span data-ttu-id="f90fe-138">This is the header that users see when they sign in.</span><span class="sxs-lookup"><span data-stu-id="f90fe-138">This is the header that users see when they sign in.</span></span>

3. <span data-ttu-id="f90fe-139">**Browse** to your finalized Terms of use PDF and select it.</span><span class="sxs-lookup"><span data-stu-id="f90fe-139">**Browse** to your finalized Terms of use PDF and select it.</span></span>

4. <span data-ttu-id="f90fe-140">**Select** a language for the Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-140">**Select** a language for the Terms of use.</span></span>  <span data-ttu-id="f90fe-141">The language option allows you to upload multiple Terms of use, each with a different language.</span><span class="sxs-lookup"><span data-stu-id="f90fe-141">The language option allows you to upload multiple Terms of use, each with a different language.</span></span>  <span data-ttu-id="f90fe-142">The version of the Terms of use that an end user will see will be based on their browser preferences.</span><span class="sxs-lookup"><span data-stu-id="f90fe-142">The version of the Terms of use that an end user will see will be based on their browser preferences.</span></span>

5. <span data-ttu-id="f90fe-143">For **Require users to expand the Terms of use**, select On or Off.</span><span class="sxs-lookup"><span data-stu-id="f90fe-143">For **Require users to expand the Terms of use**, select On or Off.</span></span>  <span data-ttu-id="f90fe-144">If this setting is set to On, end users will be required to view the Terms of use prior to accepting them.</span><span class="sxs-lookup"><span data-stu-id="f90fe-144">If this setting is set to On, end users will be required to view the Terms of use prior to accepting them.</span></span>

6. <span data-ttu-id="f90fe-145">Under **Conditional Access**, you can **Enforce** the uploaded Terms of use by selecting a template from the drop-down list or a custom conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="f90fe-145">Under **Conditional Access**, you can **Enforce** the uploaded Terms of use by selecting a template from the drop-down list or a custom conditional access policy.</span></span>  <span data-ttu-id="f90fe-146">Custom conditional access policies enable granular Terms of use, down to a specific cloud application or group of users.</span><span class="sxs-lookup"><span data-stu-id="f90fe-146">Custom conditional access policies enable granular Terms of use, down to a specific cloud application or group of users.</span></span>  <span data-ttu-id="f90fe-147">For more information, see [configuring conditional access policies](conditional-access/best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="f90fe-147">For more information, see [configuring conditional access policies](conditional-access/best-practices.md).</span></span>

    >[!IMPORTANT]
    ><span data-ttu-id="f90fe-148">Conditional access policy controls (including Terms of use) do not support enforcement on service accounts.</span><span class="sxs-lookup"><span data-stu-id="f90fe-148">Conditional access policy controls (including Terms of use) do not support enforcement on service accounts.</span></span>  <span data-ttu-id="f90fe-149">We recommend excluding all service accounts from the conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="f90fe-149">We recommend excluding all service accounts from the conditional access policy.</span></span>

7. <span data-ttu-id="f90fe-150">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-150">Click **Create**.</span></span>

8. <span data-ttu-id="f90fe-151">If you selected a custom conditional access template, then a new screen appears which allows you to customize the conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="f90fe-151">If you selected a custom conditional access template, then a new screen appears which allows you to customize the conditional access policy.</span></span>

    <span data-ttu-id="f90fe-152">You should now see your new Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-152">You should now see your new Terms of use.</span></span>

    ![Add TOU](media/active-directory-tou/create-tou.png)

## <a name="view-report-of-who-has-accepted-and-declined"></a><span data-ttu-id="f90fe-154">View report of who has accepted and declined</span><span class="sxs-lookup"><span data-stu-id="f90fe-154">View report of who has accepted and declined</span></span>
<span data-ttu-id="f90fe-155">The Terms of use blade shows a count of the users who have accepted and declined.</span><span class="sxs-lookup"><span data-stu-id="f90fe-155">The Terms of use blade shows a count of the users who have accepted and declined.</span></span> <span data-ttu-id="f90fe-156">These counts and who accepted/declined are stored for the life of the Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-156">These counts and who accepted/declined are stored for the life of the Terms of use.</span></span>

1. <span data-ttu-id="f90fe-157">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-157">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

    ![Audit Event](media/active-directory-tou/view-tou.png)

1. <span data-ttu-id="f90fe-159">Click the numbers under **Accepted** or **Declined** to view the current state for users.</span><span class="sxs-lookup"><span data-stu-id="f90fe-159">Click the numbers under **Accepted** or **Declined** to view the current state for users.</span></span>

    ![Audit Event](media/active-directory-tou/accepted-tou.png)

## <a name="view-azure-ad-audit-logs"></a><span data-ttu-id="f90fe-161">View Azure AD audit logs</span><span class="sxs-lookup"><span data-stu-id="f90fe-161">View Azure AD audit logs</span></span>
<span data-ttu-id="f90fe-162">If you want to view additional activity, Azure AD Terms of use includes audit logs.</span><span class="sxs-lookup"><span data-stu-id="f90fe-162">If you want to view additional activity, Azure AD Terms of use includes audit logs.</span></span> <span data-ttu-id="f90fe-163">Each user consent triggers an event in the audit logs that is stored for 30 days.</span><span class="sxs-lookup"><span data-stu-id="f90fe-163">Each user consent triggers an event in the audit logs that is stored for 30 days.</span></span> <span data-ttu-id="f90fe-164">You can view these logs in the portal or download as a .csv file.</span><span class="sxs-lookup"><span data-stu-id="f90fe-164">You can view these logs in the portal or download as a .csv file.</span></span>

<span data-ttu-id="f90fe-165">To get started with Azure AD audit logs, use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="f90fe-165">To get started with Azure AD audit logs, use the following procedure:</span></span>

1. <span data-ttu-id="f90fe-166">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-166">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

1. <span data-ttu-id="f90fe-167">Click **View audit logs**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-167">Click **View audit logs**.</span></span>

    ![Audit Event](media/active-directory-tou/audit-tou.png)

1. <span data-ttu-id="f90fe-169">On the Azure AD audit logs screen, you can filter the information using the provided drop-down lists to target specific audit log information.</span><span class="sxs-lookup"><span data-stu-id="f90fe-169">On the Azure AD audit logs screen, you can filter the information using the provided drop-down lists to target specific audit log information.</span></span>

    ![Audit Event](media/active-directory-tou/audit-logs-tou.png)

1. <span data-ttu-id="f90fe-171">You can also click **Download** to download the information in a .csv file for use locally.</span><span class="sxs-lookup"><span data-stu-id="f90fe-171">You can also click **Download** to download the information in a .csv file for use locally.</span></span>

## <a name="what-terms-of-use-looks-like-for-users"></a><span data-ttu-id="f90fe-172">What Terms of use looks like for users</span><span class="sxs-lookup"><span data-stu-id="f90fe-172">What Terms of use looks like for users</span></span>
<span data-ttu-id="f90fe-173">Once a Terms of use is created and enforced, users, who are in scope, will see the following screen during sign in.</span><span class="sxs-lookup"><span data-stu-id="f90fe-173">Once a Terms of use is created and enforced, users, who are in scope, will see the following screen during sign in.</span></span>

![Audit Event](media/active-directory-tou/user-tou.png)

<span data-ttu-id="f90fe-175">The following screen shows how Terms of use looks on mobile devices.</span><span class="sxs-lookup"><span data-stu-id="f90fe-175">The following screen shows how Terms of use looks on mobile devices.</span></span>

![Audit Event](media/active-directory-tou/mobile-tou.png)

<span data-ttu-id="f90fe-177">Users are only required to accept the Terms of use once and they will not see the Terms of use again on subsequent sign ins.</span><span class="sxs-lookup"><span data-stu-id="f90fe-177">Users are only required to accept the Terms of use once and they will not see the Terms of use again on subsequent sign ins.</span></span>

### <a name="how-users-can-review-their-terms-of-use"></a><span data-ttu-id="f90fe-178">How users can review their Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-178">How users can review their Terms of use</span></span>
<span data-ttu-id="f90fe-179">Users can review and see the Terms of use that they have accepted by using the following procedure.</span><span class="sxs-lookup"><span data-stu-id="f90fe-179">Users can review and see the Terms of use that they have accepted by using the following procedure.</span></span>

1. <span data-ttu-id="f90fe-180">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f90fe-180">Sign in to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>

1. <span data-ttu-id="f90fe-181">In the upper right corner, click your name and select **Profile** from the drop-down.</span><span class="sxs-lookup"><span data-stu-id="f90fe-181">In the upper right corner, click your name and select **Profile** from the drop-down.</span></span>

    ![Profile](media/active-directory-tou/tou14.png)

1. <span data-ttu-id="f90fe-183">On your Profile page, click **Review terms of use**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-183">On your Profile page, click **Review terms of use**.</span></span>

    ![Audit Event](media/active-directory-tou/tou13a.png)

1. <span data-ttu-id="f90fe-185">From there, you can review the Terms of use you have accepted.</span><span class="sxs-lookup"><span data-stu-id="f90fe-185">From there, you can review the Terms of use you have accepted.</span></span> 

## <a name="edit-terms-of-use-details"></a><span data-ttu-id="f90fe-186">Edit Terms of use details</span><span class="sxs-lookup"><span data-stu-id="f90fe-186">Edit Terms of use details</span></span>
<span data-ttu-id="f90fe-187">You can edit some details of Terms of use, but you can't modify an existing document.</span><span class="sxs-lookup"><span data-stu-id="f90fe-187">You can edit some details of Terms of use, but you can't modify an existing document.</span></span> <span data-ttu-id="f90fe-188">The following procedure describes how to edit the details.</span><span class="sxs-lookup"><span data-stu-id="f90fe-188">The following procedure describes how to edit the details.</span></span>

1. <span data-ttu-id="f90fe-189">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-189">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

1. <span data-ttu-id="f90fe-190">Select the Terms of use you want to edit.</span><span class="sxs-lookup"><span data-stu-id="f90fe-190">Select the Terms of use you want to edit.</span></span>

1. <span data-ttu-id="f90fe-191">Click **Edit terms**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-191">Click **Edit terms**.</span></span>

1. <span data-ttu-id="f90fe-192">In the Edit terms of use pane, change the name, display name, or require users to expand values.</span><span class="sxs-lookup"><span data-stu-id="f90fe-192">In the Edit terms of use pane, change the name, display name, or require users to expand values.</span></span>

    ![Add TOU](media/active-directory-tou/edit-tou.png)

1. <span data-ttu-id="f90fe-194">Click **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="f90fe-194">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="f90fe-195">Once you save your changes, users will have to reaccept the new terms.</span><span class="sxs-lookup"><span data-stu-id="f90fe-195">Once you save your changes, users will have to reaccept the new terms.</span></span>

## <a name="add-a-terms-of-use-language"></a><span data-ttu-id="f90fe-196">Add a Terms of use language</span><span class="sxs-lookup"><span data-stu-id="f90fe-196">Add a Terms of use language</span></span>
<span data-ttu-id="f90fe-197">The following procedure describes how to add a Terms of use language.</span><span class="sxs-lookup"><span data-stu-id="f90fe-197">The following procedure describes how to add a Terms of use language.</span></span>

1. <span data-ttu-id="f90fe-198">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-198">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

1. <span data-ttu-id="f90fe-199">Select the Terms of use you want to edit.</span><span class="sxs-lookup"><span data-stu-id="f90fe-199">Select the Terms of use you want to edit.</span></span>

1. <span data-ttu-id="f90fe-200">In the details pane, click the **Languages** tab.</span><span class="sxs-lookup"><span data-stu-id="f90fe-200">In the details pane, click the **Languages** tab.</span></span>

    ![Add TOU](media/active-directory-tou/languages-tou.png)

1. <span data-ttu-id="f90fe-202">Click **Add language**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-202">Click **Add language**.</span></span>

1. <span data-ttu-id="f90fe-203">In the Add terms of use language pane, upload your localized PDF and select the language.</span><span class="sxs-lookup"><span data-stu-id="f90fe-203">In the Add terms of use language pane, upload your localized PDF and select the language.</span></span>

    ![Add TOU](media/active-directory-tou/language-add-tou.png)

1. <span data-ttu-id="f90fe-205">Click **Add** to add the language.</span><span class="sxs-lookup"><span data-stu-id="f90fe-205">Click **Add** to add the language.</span></span>

## <a name="delete-terms-of-use"></a><span data-ttu-id="f90fe-206">Delete Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-206">Delete Terms of use</span></span>
<span data-ttu-id="f90fe-207">You can delete old Terms of use using the following procedure.</span><span class="sxs-lookup"><span data-stu-id="f90fe-207">You can delete old Terms of use using the following procedure.</span></span>

1. <span data-ttu-id="f90fe-208">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span><span class="sxs-lookup"><span data-stu-id="f90fe-208">Sign in to Azure and navigate to **Terms of use** at [https://aka.ms/catou](https://aka.ms/catou).</span></span>

1. <span data-ttu-id="f90fe-209">Select the Terms of use you want to remove.</span><span class="sxs-lookup"><span data-stu-id="f90fe-209">Select the Terms of use you want to remove.</span></span>

1. <span data-ttu-id="f90fe-210">Click **Delete terms**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-210">Click **Delete terms**.</span></span>

1. <span data-ttu-id="f90fe-211">In the message that appears asking if you want to continue, click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-211">In the message that appears asking if you want to continue, click **Yes**.</span></span>

    ![Add TOU](media/active-directory-tou/delete-tou.png)

    <span data-ttu-id="f90fe-213">You should no longer see your Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-213">You should no longer see your Terms of use.</span></span>

## <a name="deleted-users-and-active-terms-of-use"></a><span data-ttu-id="f90fe-214">Deleted users and active Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-214">Deleted users and active Terms of use</span></span>
<span data-ttu-id="f90fe-215">By default, a deleted user is in a deleted state in Azure AD for 30 days, during which time they can be restored by an administrator if necessary.</span><span class="sxs-lookup"><span data-stu-id="f90fe-215">By default, a deleted user is in a deleted state in Azure AD for 30 days, during which time they can be restored by an administrator if necessary.</span></span>  <span data-ttu-id="f90fe-216">After 30 days, that user is permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="f90fe-216">After 30 days, that user is permanently deleted.</span></span>  <span data-ttu-id="f90fe-217">In addition, using the Azure Active Directory portal, a Global administrator can explicitly [permanently delete a recently deleted user](fundamentals/active-directory-users-restore.md) before that time period is reached.</span><span class="sxs-lookup"><span data-stu-id="f90fe-217">In addition, using the Azure Active Directory portal, a Global administrator can explicitly [permanently delete a recently deleted user](fundamentals/active-directory-users-restore.md) before that time period is reached.</span></span>  <span data-ttu-id="f90fe-218">One a user has been permanently deleted, subsequent data about that user will be removed from the active Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-218">One a user has been permanently deleted, subsequent data about that user will be removed from the active Terms of use.</span></span>  <span data-ttu-id="f90fe-219">Audit information about deleted users remains in the audit log.</span><span class="sxs-lookup"><span data-stu-id="f90fe-219">Audit information about deleted users remains in the audit log.</span></span>

## <a name="policy-changes"></a><span data-ttu-id="f90fe-220">Policy changes</span><span class="sxs-lookup"><span data-stu-id="f90fe-220">Policy changes</span></span>
<span data-ttu-id="f90fe-221">Conditional access policies take effect immediately.</span><span class="sxs-lookup"><span data-stu-id="f90fe-221">Conditional access policies take effect immediately.</span></span> <span data-ttu-id="f90fe-222">When this happens, the administrator will start to see “sad clouds” or "Azure AD token issues".</span><span class="sxs-lookup"><span data-stu-id="f90fe-222">When this happens, the administrator will start to see “sad clouds” or "Azure AD token issues".</span></span> <span data-ttu-id="f90fe-223">The administrator must sign out and sign in again in order to satisfy the new policy.</span><span class="sxs-lookup"><span data-stu-id="f90fe-223">The administrator must sign out and sign in again in order to satisfy the new policy.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f90fe-224">Users in scope will need to sign-out and sign-in in order to satisfy a new policy if:</span><span class="sxs-lookup"><span data-stu-id="f90fe-224">Users in scope will need to sign-out and sign-in in order to satisfy a new policy if:</span></span>
> - <span data-ttu-id="f90fe-225">a conditional access policy is enabled on a Terms of use</span><span class="sxs-lookup"><span data-stu-id="f90fe-225">a conditional access policy is enabled on a Terms of use</span></span>
> - <span data-ttu-id="f90fe-226">or a second Terms of use is created</span><span class="sxs-lookup"><span data-stu-id="f90fe-226">or a second Terms of use is created</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="f90fe-227">Frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="f90fe-227">Frequently asked questions</span></span>

<span data-ttu-id="f90fe-228">**Q: How do I see when/if a user has accepted a Terms of use?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-228">**Q: How do I see when/if a user has accepted a Terms of use?**</span></span></br>
<span data-ttu-id="f90fe-229">A: On the Terms of use blade, click the number under **Accepted**.</span><span class="sxs-lookup"><span data-stu-id="f90fe-229">A: On the Terms of use blade, click the number under **Accepted**.</span></span> <span data-ttu-id="f90fe-230">You can also view or search the accept activity in the Azure AD audit logs.</span><span class="sxs-lookup"><span data-stu-id="f90fe-230">You can also view or search the accept activity in the Azure AD audit logs.</span></span> <span data-ttu-id="f90fe-231">For more information, see [View report of who has accepted and declined](#view-who-has-accepted-and-declined) and [View Azure AD audit logs](#view-azure-ad-audit-logs).</span><span class="sxs-lookup"><span data-stu-id="f90fe-231">For more information, see [View report of who has accepted and declined](#view-who-has-accepted-and-declined) and [View Azure AD audit logs](#view-azure-ad-audit-logs).</span></span>
 
<span data-ttu-id="f90fe-232">**Q: How long is information stored?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-232">**Q: How long is information stored?**</span></span></br>
<span data-ttu-id="f90fe-233">A: The user counts in the Terms of use report and who accepted/declined are stored for the life of the Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-233">A: The user counts in the Terms of use report and who accepted/declined are stored for the life of the Terms of use.</span></span> <span data-ttu-id="f90fe-234">The Azure AD audit logs are stored for 30 days.</span><span class="sxs-lookup"><span data-stu-id="f90fe-234">The Azure AD audit logs are stored for 30 days.</span></span>

<span data-ttu-id="f90fe-235">**Q: Why do I see a different number of consents in the Terms of use report vs. the Azure AD audit logs?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-235">**Q: Why do I see a different number of consents in the Terms of use report vs. the Azure AD audit logs?**</span></span></br>
<span data-ttu-id="f90fe-236">A: The Terms of use report is stored for the lifetime of that Terms of use, while the Azure AD audit logs are stored for 30 days.</span><span class="sxs-lookup"><span data-stu-id="f90fe-236">A: The Terms of use report is stored for the lifetime of that Terms of use, while the Azure AD audit logs are stored for 30 days.</span></span> <span data-ttu-id="f90fe-237">Also, the Terms of use report only displays the users current consent state.</span><span class="sxs-lookup"><span data-stu-id="f90fe-237">Also, the Terms of use report only displays the users current consent state.</span></span> <span data-ttu-id="f90fe-238">For example, if a user declines and then accepts, the Terms of use report will only show that user's accept.</span><span class="sxs-lookup"><span data-stu-id="f90fe-238">For example, if a user declines and then accepts, the Terms of use report will only show that user's accept.</span></span> <span data-ttu-id="f90fe-239">If you need to see the history, you can use the Azure AD audit logs.</span><span class="sxs-lookup"><span data-stu-id="f90fe-239">If you need to see the history, you can use the Azure AD audit logs.</span></span>

<span data-ttu-id="f90fe-240">**Q: If I edit the details for a Terms of use, does it require users to accept again?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-240">**Q: If I edit the details for a Terms of use, does it require users to accept again?**</span></span></br>
<span data-ttu-id="f90fe-241">A: Yes, if an administrator edits the details for a Terms of use, it requires users to reaccept the new terms.</span><span class="sxs-lookup"><span data-stu-id="f90fe-241">A: Yes, if an administrator edits the details for a Terms of use, it requires users to reaccept the new terms.</span></span>

<span data-ttu-id="f90fe-242">**Q: Can I update an existing Terms of use document?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-242">**Q: Can I update an existing Terms of use document?**</span></span></br>
<span data-ttu-id="f90fe-243">A: Currently, you can't update an existing Terms of use document.</span><span class="sxs-lookup"><span data-stu-id="f90fe-243">A: Currently, you can't update an existing Terms of use document.</span></span> <span data-ttu-id="f90fe-244">To change a Terms of use document, you will have to create a new Terms of use instance.</span><span class="sxs-lookup"><span data-stu-id="f90fe-244">To change a Terms of use document, you will have to create a new Terms of use instance.</span></span>

<span data-ttu-id="f90fe-245">**Q: If hyperlinks are in the Terms of use PDF document, will end users be able to click them?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-245">**Q: If hyperlinks are in the Terms of use PDF document, will end users be able to click them?**</span></span></br>
<span data-ttu-id="f90fe-246">A: The PDF is rendered by default as a JPEG, so hyperlinks are not clickable.</span><span class="sxs-lookup"><span data-stu-id="f90fe-246">A: The PDF is rendered by default as a JPEG, so hyperlinks are not clickable.</span></span> <span data-ttu-id="f90fe-247">Users have the option to select **Having trouble viewing? Click here**, which renders the PDF natively where hyperlinks are supported.</span><span class="sxs-lookup"><span data-stu-id="f90fe-247">Users have the option to select **Having trouble viewing? Click here**, which renders the PDF natively where hyperlinks are supported.</span></span>

<span data-ttu-id="f90fe-248">**Q: Can a Terms of use support multiple languages?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-248">**Q: Can a Terms of use support multiple languages?**</span></span></br>
<span data-ttu-id="f90fe-249">A: Yes.</span><span class="sxs-lookup"><span data-stu-id="f90fe-249">A: Yes.</span></span> <span data-ttu-id="f90fe-250">Currently there are 108 different languages an administrator can configure for a single Terms of use.</span><span class="sxs-lookup"><span data-stu-id="f90fe-250">Currently there are 108 different languages an administrator can configure for a single Terms of use.</span></span>

<span data-ttu-id="f90fe-251">**Q: When is the Terms of use triggered?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-251">**Q: When is the Terms of use triggered?**</span></span></br>
<span data-ttu-id="f90fe-252">A: The Terms of use is triggered during the sign-in experience.</span><span class="sxs-lookup"><span data-stu-id="f90fe-252">A: The Terms of use is triggered during the sign-in experience.</span></span>

<span data-ttu-id="f90fe-253">**Q: What applications can I target a Terms of use to?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-253">**Q: What applications can I target a Terms of use to?**</span></span></br>
<span data-ttu-id="f90fe-254">A: You can create a conditional access policy on the enterprise applications using modern authentication.</span><span class="sxs-lookup"><span data-stu-id="f90fe-254">A: You can create a conditional access policy on the enterprise applications using modern authentication.</span></span>  <span data-ttu-id="f90fe-255">For more information, see [enterprise applications](./manage-apps/view-applications-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f90fe-255">For more information, see [enterprise applications](./manage-apps/view-applications-portal.md).</span></span>

<span data-ttu-id="f90fe-256">**Q: Can I add multiple Terms of use to a given user or app?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-256">**Q: Can I add multiple Terms of use to a given user or app?**</span></span></br>
<span data-ttu-id="f90fe-257">A: Yes, by creating multiple conditional access policies targeting those groups or applications.</span><span class="sxs-lookup"><span data-stu-id="f90fe-257">A: Yes, by creating multiple conditional access policies targeting those groups or applications.</span></span> <span data-ttu-id="f90fe-258">If a user falls in scope of multiple Terms of use, they agree to one Terms of use at a time.</span><span class="sxs-lookup"><span data-stu-id="f90fe-258">If a user falls in scope of multiple Terms of use, they agree to one Terms of use at a time.</span></span>
 
<span data-ttu-id="f90fe-259">**Q: What happens if a user declines the Terms of use?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-259">**Q: What happens if a user declines the Terms of use?**</span></span></br>
<span data-ttu-id="f90fe-260">A: The user is blocked from getting access to the application.</span><span class="sxs-lookup"><span data-stu-id="f90fe-260">A: The user is blocked from getting access to the application.</span></span> <span data-ttu-id="f90fe-261">The user would have to sign in again and agree to the terms in order to get access.</span><span class="sxs-lookup"><span data-stu-id="f90fe-261">The user would have to sign in again and agree to the terms in order to get access.</span></span>
 
<span data-ttu-id="f90fe-262">**Q: Is it possible to unaccept Terms of use that were previously accepted?**</span><span class="sxs-lookup"><span data-stu-id="f90fe-262">**Q: Is it possible to unaccept Terms of use that were previously accepted?**</span></span></br>
<span data-ttu-id="f90fe-263">A: You can [review previously accepted Terms of use](#how-users-can-review-their-terms-of-use), but currently there isn't a way to unaccept.</span><span class="sxs-lookup"><span data-stu-id="f90fe-263">A: You can [review previously accepted Terms of use](#how-users-can-review-their-terms-of-use), but currently there isn't a way to unaccept.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f90fe-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="f90fe-264">Next steps</span></span>

- [<span data-ttu-id="f90fe-265">Best practices for conditional access in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f90fe-265">Best practices for conditional access in Azure Active Directory</span></span>](conditional-access/best-practices.md)