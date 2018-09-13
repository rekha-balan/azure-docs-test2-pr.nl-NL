---
title: Add an app to your Azure Active Directory tenant | Microsoft Docs
description: This quickstart uses the Azure portal to add a gallery application to your Azure Active Directory (Azure AD) tenant.
services: active-directory
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.topic: quickstart
ms.workload: identity
ms.date: 07/24/2018
ms.author: barbkess
ms.openlocfilehash: 16910e51380a9d3f5ddf46b0deabc79830bb10c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857911"
---
# <a name="quickstart-add-an-application-to-your-azure-active-directory-tenant"></a><span data-ttu-id="073fa-103">Quickstart: Add an application to your Azure Active Directory tenant</span><span class="sxs-lookup"><span data-stu-id="073fa-103">Quickstart: Add an application to your Azure Active Directory tenant</span></span>

<span data-ttu-id="073fa-104">Azure Active Directory (Azure AD) has a gallery that contains thousands of pre-integrated applications.</span><span class="sxs-lookup"><span data-stu-id="073fa-104">Azure Active Directory (Azure AD) has a gallery that contains thousands of pre-integrated applications.</span></span> <span data-ttu-id="073fa-105">Some of the applications your organization uses are probably in the gallery.</span><span class="sxs-lookup"><span data-stu-id="073fa-105">Some of the applications your organization uses are probably in the gallery.</span></span> <span data-ttu-id="073fa-106">This quickstart uses the Azure portal to add a gallery application to your Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="073fa-106">This quickstart uses the Azure portal to add a gallery application to your Azure Active Directory (Azure AD) tenant.</span></span> 
 
<span data-ttu-id="073fa-107">After an application is added to your Azure AD tenant, you can:</span><span class="sxs-lookup"><span data-stu-id="073fa-107">After an application is added to your Azure AD tenant, you can:</span></span>

- <span data-ttu-id="073fa-108">Manage user access to the application with a conditional access policy.</span><span class="sxs-lookup"><span data-stu-id="073fa-108">Manage user access to the application with a conditional access policy.</span></span>
- <span data-ttu-id="073fa-109">Configure users to single sign-on to the application with their Azure AD accounts.</span><span class="sxs-lookup"><span data-stu-id="073fa-109">Configure users to single sign-on to the application with their Azure AD accounts.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="073fa-110">Before you begin</span><span class="sxs-lookup"><span data-stu-id="073fa-110">Before you begin</span></span>

<span data-ttu-id="073fa-111">To add an application to your tenant, you need:</span><span class="sxs-lookup"><span data-stu-id="073fa-111">To add an application to your tenant, you need:</span></span>

- <span data-ttu-id="073fa-112">An Azure AD subscription</span><span class="sxs-lookup"><span data-stu-id="073fa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="073fa-113">A single sign-on enabled subscription for your application</span><span class="sxs-lookup"><span data-stu-id="073fa-113">A single sign-on enabled subscription for your application</span></span>

<span data-ttu-id="073fa-114">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span><span class="sxs-lookup"><span data-stu-id="073fa-114">Sign in to the [Azure portal](https://portal.azure.com) as a global admin for your Azure AD tenant, a cloud application admin, or an application admin.</span></span>

<span data-ttu-id="073fa-115">To test the steps in this tutorial, we recommend using a non-production environment.</span><span class="sxs-lookup"><span data-stu-id="073fa-115">To test the steps in this tutorial, we recommend using a non-production environment.</span></span> <span data-ttu-id="073fa-116">If you don't have an Azure AD non-production environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="073fa-116">If you don't have an Azure AD non-production environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-an-application-to-your-azure-ad-tenant"></a><span data-ttu-id="073fa-117">Add an application to your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="073fa-117">Add an application to your Azure AD tenant</span></span>

<span data-ttu-id="073fa-118">To add a gallery application to your Azure AD tenant:</span><span class="sxs-lookup"><span data-stu-id="073fa-118">To add a gallery application to your Azure AD tenant:</span></span>

1. <span data-ttu-id="073fa-119">In the [Azure portal](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="073fa-119">In the [Azure portal](https://portal.azure.com), on the left navigation panel, click **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="073fa-120">In the **Azure Active Directory** blade, click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="073fa-120">In the **Azure Active Directory** blade, click **Enterprise applications**.</span></span> 

    ![Open enterprise applications](media/add-application-portal/open-enterprise-apps.png)

3. <span data-ttu-id="073fa-122">The **All applications** blade opens to show a random sample of the applications in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="073fa-122">The **All applications** blade opens to show a random sample of the applications in your Azure AD tenant.</span></span> 

    ![All applications blade](media/add-application-portal/applications-blade.png)


4. <span data-ttu-id="073fa-124">Click **New application** at the top of the **All applications** blade.</span><span class="sxs-lookup"><span data-stu-id="073fa-124">Click **New application** at the top of the **All applications** blade.</span></span>

    ![New application](media/add-application-portal/new-application.png)

5. <span data-ttu-id="073fa-126">To see a list of applications in the gallery, it's easiest to use the **Categories** since the icons under **Featured applications** are a random sample of gallery applications.</span><span class="sxs-lookup"><span data-stu-id="073fa-126">To see a list of applications in the gallery, it's easiest to use the **Categories** since the icons under **Featured applications** are a random sample of gallery applications.</span></span> 

    ![Search by name or category](media/add-application-portal/categories.png)

    <span data-ttu-id="073fa-128">To see more applications, you could click **Show more**.</span><span class="sxs-lookup"><span data-stu-id="073fa-128">To see more applications, you could click **Show more**.</span></span> <span data-ttu-id="073fa-129">We don't recommend searching this way since there are thousands of applications in the gallery.</span><span class="sxs-lookup"><span data-stu-id="073fa-129">We don't recommend searching this way since there are thousands of applications in the gallery.</span></span>

6. <span data-ttu-id="073fa-130">To search for an application, under **Add from the gallery** enter the name of the application you want to add.</span><span class="sxs-lookup"><span data-stu-id="073fa-130">To search for an application, under **Add from the gallery** enter the name of the application you want to add.</span></span> <span data-ttu-id="073fa-131">Select the application from the results, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="073fa-131">Select the application from the results, and click **Add**.</span></span> <span data-ttu-id="073fa-132">The following example shows the **Add app** form that appears after searching for GitHub.com.</span><span class="sxs-lookup"><span data-stu-id="073fa-132">The following example shows the **Add app** form that appears after searching for GitHub.com.</span></span>

    ![Add an application](media/add-application-portal/add-an-application.png)

6. <span data-ttu-id="073fa-134">In the application-specific form, you can change property information.</span><span class="sxs-lookup"><span data-stu-id="073fa-134">In the application-specific form, you can change property information.</span></span> <span data-ttu-id="073fa-135">For example, you can edit the name of the application to match the needs of your organization.</span><span class="sxs-lookup"><span data-stu-id="073fa-135">For example, you can edit the name of the application to match the needs of your organization.</span></span> <span data-ttu-id="073fa-136">This example uses the name **GitHub-test**.</span><span class="sxs-lookup"><span data-stu-id="073fa-136">This example uses the name **GitHub-test**.</span></span>

8. <span data-ttu-id="073fa-137">When you are finished making changes to the properties, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="073fa-137">When you are finished making changes to the properties, click **Add**.</span></span>

9. <span data-ttu-id="073fa-138">A getting started page appears with the options for configuring the application for your organization.</span><span class="sxs-lookup"><span data-stu-id="073fa-138">A getting started page appears with the options for configuring the application for your organization.</span></span> 

    ![Get started menu](media/add-application-portal/get-started.png)

<span data-ttu-id="073fa-140">You have finished adding your application.</span><span class="sxs-lookup"><span data-stu-id="073fa-140">You have finished adding your application.</span></span> <span data-ttu-id="073fa-141">Feel free to take a break.</span><span class="sxs-lookup"><span data-stu-id="073fa-141">Feel free to take a break.</span></span>  <span data-ttu-id="073fa-142">The next sections show you how to change the logo and edit other properties for your application.</span><span class="sxs-lookup"><span data-stu-id="073fa-142">The next sections show you how to change the logo and edit other properties for your application.</span></span>

## <a name="find-your-azure-ad-tenant-application"></a><span data-ttu-id="073fa-143">Find your Azure AD tenant application</span><span class="sxs-lookup"><span data-stu-id="073fa-143">Find your Azure AD tenant application</span></span>

<span data-ttu-id="073fa-144">Let's assume you had to leave and now you're returning to continue configuring your application.</span><span class="sxs-lookup"><span data-stu-id="073fa-144">Let's assume you had to leave and now you're returning to continue configuring your application.</span></span> <span data-ttu-id="073fa-145">The first thing you need to do is find your application.</span><span class="sxs-lookup"><span data-stu-id="073fa-145">The first thing you need to do is find your application.</span></span>

1. <span data-ttu-id="073fa-146">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="073fa-146">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="073fa-147">In the Azure Active Directory blade, click **Enterprise applications**.</span><span class="sxs-lookup"><span data-stu-id="073fa-147">In the Azure Active Directory blade, click **Enterprise applications**.</span></span> 

3. <span data-ttu-id="073fa-148">From the **Application Type** drop-down menu, select **All Applications**, and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="073fa-148">From the **Application Type** drop-down menu, select **All Applications**, and click **Apply**.</span></span> <span data-ttu-id="073fa-149">To learn more about the viewing options, see [View tenant applications](view-applications-portal.md).</span><span class="sxs-lookup"><span data-stu-id="073fa-149">To learn more about the viewing options, see [View tenant applications](view-applications-portal.md).</span></span>

4. <span data-ttu-id="073fa-150">You can now see a list of all the applications in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="073fa-150">You can now see a list of all the applications in your Azure AD tenant.</span></span>  <span data-ttu-id="073fa-151">The list is a random sample.</span><span class="sxs-lookup"><span data-stu-id="073fa-151">The list is a random sample.</span></span> <span data-ttu-id="073fa-152">To see more applications, click **Show more** one or more times.</span><span class="sxs-lookup"><span data-stu-id="073fa-152">To see more applications, click **Show more** one or more times.</span></span> 

5. <span data-ttu-id="073fa-153">To quickly find an application in your tenant, enter the application name in the search box and click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="073fa-153">To quickly find an application in your tenant, enter the application name in the search box and click **Apply**.</span></span> <span data-ttu-id="073fa-154">This example finds the GitHub-test application that we added previously.</span><span class="sxs-lookup"><span data-stu-id="073fa-154">This example finds the GitHub-test application that we added previously.</span></span>

    ![Search for an application](media/add-application-portal/find-application.png)


## <a name="configure-user-sign-in-properties"></a><span data-ttu-id="073fa-156">Configure user sign-in properties</span><span class="sxs-lookup"><span data-stu-id="073fa-156">Configure user sign-in properties</span></span>

<span data-ttu-id="073fa-157">Now that you have found the application, you can open it and configure application properties.</span><span class="sxs-lookup"><span data-stu-id="073fa-157">Now that you have found the application, you can open it and configure application properties.</span></span>

<span data-ttu-id="073fa-158">To edit the application properties</span><span class="sxs-lookup"><span data-stu-id="073fa-158">To edit the application properties</span></span>

1. <span data-ttu-id="073fa-159">Click the application to open it.</span><span class="sxs-lookup"><span data-stu-id="073fa-159">Click the application to open it.</span></span>
2. <span data-ttu-id="073fa-160">Click **Properties** to open the properties blade for editing.</span><span class="sxs-lookup"><span data-stu-id="073fa-160">Click **Properties** to open the properties blade for editing.</span></span>

    ![Edit properties blade](media/add-application-portal/edit-properties.png)

3. <span data-ttu-id="073fa-162">Take a moment to understand the sign-in options.</span><span class="sxs-lookup"><span data-stu-id="073fa-162">Take a moment to understand the sign-in options.</span></span> <span data-ttu-id="073fa-163">The **Enabled for users to sign-in**, **User assignment required**, and **Visible to user** combine to determine whether users who are assigned or unassigned to the application can sign in.</span><span class="sxs-lookup"><span data-stu-id="073fa-163">The **Enabled for users to sign-in**, **User assignment required**, and **Visible to user** combine to determine whether users who are assigned or unassigned to the application can sign in.</span></span>  <span data-ttu-id="073fa-164">They also determine if the user can see the application in the access panel.</span><span class="sxs-lookup"><span data-stu-id="073fa-164">They also determine if the user can see the application in the access panel.</span></span> 

    - <span data-ttu-id="073fa-165">**Enabled for users to sign-in** determines whether users assigned to the application can sign in.</span><span class="sxs-lookup"><span data-stu-id="073fa-165">**Enabled for users to sign-in** determines whether users assigned to the application can sign in.</span></span>
    - <span data-ttu-id="073fa-166">**User assignment required** determines whether users who are not assigned to the application can sign in.</span><span class="sxs-lookup"><span data-stu-id="073fa-166">**User assignment required** determines whether users who are not assigned to the application can sign in.</span></span>
    - <span data-ttu-id="073fa-167">**Visible to user** determines whether users assigned to an app can see it in the access panel and O365 launcher.</span><span class="sxs-lookup"><span data-stu-id="073fa-167">**Visible to user** determines whether users assigned to an app can see it in the access panel and O365 launcher.</span></span> 

4. <span data-ttu-id="073fa-168">Use the following tables to help you choose the options that are best for your needs.</span><span class="sxs-lookup"><span data-stu-id="073fa-168">Use the following tables to help you choose the options that are best for your needs.</span></span> 

     - <span data-ttu-id="073fa-169">Behavior for **assigned** users:</span><span class="sxs-lookup"><span data-stu-id="073fa-169">Behavior for **assigned** users:</span></span>

       | <span data-ttu-id="073fa-170">Application property settings</span><span class="sxs-lookup"><span data-stu-id="073fa-170">Application property settings</span></span> | | | <span data-ttu-id="073fa-171">Assigned-user experience</span><span class="sxs-lookup"><span data-stu-id="073fa-171">Assigned-user experience</span></span> | |
       |---|---|---|---|---|
       | <span data-ttu-id="073fa-172">Enabled for users to sign-in?</span><span class="sxs-lookup"><span data-stu-id="073fa-172">Enabled for users to sign-in?</span></span> | <span data-ttu-id="073fa-173">User assignment required?</span><span class="sxs-lookup"><span data-stu-id="073fa-173">User assignment required?</span></span> | <span data-ttu-id="073fa-174">Visible to users?</span><span class="sxs-lookup"><span data-stu-id="073fa-174">Visible to users?</span></span> | <span data-ttu-id="073fa-175">Can assigned users sign in?</span><span class="sxs-lookup"><span data-stu-id="073fa-175">Can assigned users sign in?</span></span> | <span data-ttu-id="073fa-176">Can assigned users see the application?\*</span><span class="sxs-lookup"><span data-stu-id="073fa-176">Can assigned users see the application?\*</span></span> |
       | <span data-ttu-id="073fa-177">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-177">yes</span></span> | <span data-ttu-id="073fa-178">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-178">yes</span></span> | <span data-ttu-id="073fa-179">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-179">yes</span></span> | <span data-ttu-id="073fa-180">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-180">yes</span></span> | <span data-ttu-id="073fa-181">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-181">yes</span></span>  |
       | <span data-ttu-id="073fa-182">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-182">yes</span></span> | <span data-ttu-id="073fa-183">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-183">yes</span></span> | <span data-ttu-id="073fa-184">no</span><span class="sxs-lookup"><span data-stu-id="073fa-184">no</span></span>  | <span data-ttu-id="073fa-185">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-185">yes</span></span> | <span data-ttu-id="073fa-186">no</span><span class="sxs-lookup"><span data-stu-id="073fa-186">no</span></span>   |
       | <span data-ttu-id="073fa-187">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-187">yes</span></span> | <span data-ttu-id="073fa-188">no</span><span class="sxs-lookup"><span data-stu-id="073fa-188">no</span></span>  | <span data-ttu-id="073fa-189">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-189">yes</span></span> | <span data-ttu-id="073fa-190">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-190">yes</span></span> | <span data-ttu-id="073fa-191">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-191">yes</span></span>  |
       | <span data-ttu-id="073fa-192">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-192">yes</span></span> | <span data-ttu-id="073fa-193">no</span><span class="sxs-lookup"><span data-stu-id="073fa-193">no</span></span>  | <span data-ttu-id="073fa-194">no</span><span class="sxs-lookup"><span data-stu-id="073fa-194">no</span></span>  | <span data-ttu-id="073fa-195">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-195">yes</span></span> | <span data-ttu-id="073fa-196">no</span><span class="sxs-lookup"><span data-stu-id="073fa-196">no</span></span>   |
       | <span data-ttu-id="073fa-197">no</span><span class="sxs-lookup"><span data-stu-id="073fa-197">no</span></span>  | <span data-ttu-id="073fa-198">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-198">yes</span></span> | <span data-ttu-id="073fa-199">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-199">yes</span></span> | <span data-ttu-id="073fa-200">no</span><span class="sxs-lookup"><span data-stu-id="073fa-200">no</span></span>  | <span data-ttu-id="073fa-201">no</span><span class="sxs-lookup"><span data-stu-id="073fa-201">no</span></span>   |
       | <span data-ttu-id="073fa-202">no</span><span class="sxs-lookup"><span data-stu-id="073fa-202">no</span></span>  | <span data-ttu-id="073fa-203">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-203">yes</span></span> | <span data-ttu-id="073fa-204">no</span><span class="sxs-lookup"><span data-stu-id="073fa-204">no</span></span>  | <span data-ttu-id="073fa-205">no</span><span class="sxs-lookup"><span data-stu-id="073fa-205">no</span></span>  | <span data-ttu-id="073fa-206">no</span><span class="sxs-lookup"><span data-stu-id="073fa-206">no</span></span>   |
       | <span data-ttu-id="073fa-207">no</span><span class="sxs-lookup"><span data-stu-id="073fa-207">no</span></span>  | <span data-ttu-id="073fa-208">no</span><span class="sxs-lookup"><span data-stu-id="073fa-208">no</span></span>  | <span data-ttu-id="073fa-209">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-209">yes</span></span> | <span data-ttu-id="073fa-210">no</span><span class="sxs-lookup"><span data-stu-id="073fa-210">no</span></span>  | <span data-ttu-id="073fa-211">no</span><span class="sxs-lookup"><span data-stu-id="073fa-211">no</span></span>   |
       | <span data-ttu-id="073fa-212">no</span><span class="sxs-lookup"><span data-stu-id="073fa-212">no</span></span>  | <span data-ttu-id="073fa-213">no</span><span class="sxs-lookup"><span data-stu-id="073fa-213">no</span></span>  | <span data-ttu-id="073fa-214">no</span><span class="sxs-lookup"><span data-stu-id="073fa-214">no</span></span>  | <span data-ttu-id="073fa-215">no</span><span class="sxs-lookup"><span data-stu-id="073fa-215">no</span></span>  | <span data-ttu-id="073fa-216">no</span><span class="sxs-lookup"><span data-stu-id="073fa-216">no</span></span>   |

     - <span data-ttu-id="073fa-217">Behavior for **unassigned** users:</span><span class="sxs-lookup"><span data-stu-id="073fa-217">Behavior for **unassigned** users:</span></span>
  
       | <span data-ttu-id="073fa-218">Application property settings</span><span class="sxs-lookup"><span data-stu-id="073fa-218">Application property settings</span></span> | | | <span data-ttu-id="073fa-219">Unassigned-user experience</span><span class="sxs-lookup"><span data-stu-id="073fa-219">Unassigned-user experience</span></span> | |
       |---|---|---|---|---|
       | <span data-ttu-id="073fa-220">Enabled for users to sign-in?</span><span class="sxs-lookup"><span data-stu-id="073fa-220">Enabled for users to sign-in?</span></span> | <span data-ttu-id="073fa-221">User assignment required?</span><span class="sxs-lookup"><span data-stu-id="073fa-221">User assignment required?</span></span> | <span data-ttu-id="073fa-222">Visible to users?</span><span class="sxs-lookup"><span data-stu-id="073fa-222">Visible to users?</span></span> | <span data-ttu-id="073fa-223">Can unassigned users sign in?</span><span class="sxs-lookup"><span data-stu-id="073fa-223">Can unassigned users sign in?</span></span> | <span data-ttu-id="073fa-224">Can unassigned users see the application?\*</span><span class="sxs-lookup"><span data-stu-id="073fa-224">Can unassigned users see the application?\*</span></span> |
       | <span data-ttu-id="073fa-225">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-225">yes</span></span> | <span data-ttu-id="073fa-226">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-226">yes</span></span> | <span data-ttu-id="073fa-227">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-227">yes</span></span> | <span data-ttu-id="073fa-228">no</span><span class="sxs-lookup"><span data-stu-id="073fa-228">no</span></span>  | <span data-ttu-id="073fa-229">no</span><span class="sxs-lookup"><span data-stu-id="073fa-229">no</span></span>   |
       | <span data-ttu-id="073fa-230">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-230">yes</span></span> | <span data-ttu-id="073fa-231">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-231">yes</span></span> | <span data-ttu-id="073fa-232">no</span><span class="sxs-lookup"><span data-stu-id="073fa-232">no</span></span>  | <span data-ttu-id="073fa-233">no</span><span class="sxs-lookup"><span data-stu-id="073fa-233">no</span></span>  | <span data-ttu-id="073fa-234">no</span><span class="sxs-lookup"><span data-stu-id="073fa-234">no</span></span>   |
       | <span data-ttu-id="073fa-235">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-235">yes</span></span> | <span data-ttu-id="073fa-236">no</span><span class="sxs-lookup"><span data-stu-id="073fa-236">no</span></span>  | <span data-ttu-id="073fa-237">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-237">yes</span></span> | <span data-ttu-id="073fa-238">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-238">yes</span></span> | <span data-ttu-id="073fa-239">no</span><span class="sxs-lookup"><span data-stu-id="073fa-239">no</span></span>   |
       | <span data-ttu-id="073fa-240">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-240">yes</span></span> | <span data-ttu-id="073fa-241">no</span><span class="sxs-lookup"><span data-stu-id="073fa-241">no</span></span>  | <span data-ttu-id="073fa-242">no</span><span class="sxs-lookup"><span data-stu-id="073fa-242">no</span></span>  | <span data-ttu-id="073fa-243">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-243">yes</span></span> | <span data-ttu-id="073fa-244">no</span><span class="sxs-lookup"><span data-stu-id="073fa-244">no</span></span>   |
       | <span data-ttu-id="073fa-245">no</span><span class="sxs-lookup"><span data-stu-id="073fa-245">no</span></span>  | <span data-ttu-id="073fa-246">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-246">yes</span></span> | <span data-ttu-id="073fa-247">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-247">yes</span></span> | <span data-ttu-id="073fa-248">no</span><span class="sxs-lookup"><span data-stu-id="073fa-248">no</span></span>  | <span data-ttu-id="073fa-249">no</span><span class="sxs-lookup"><span data-stu-id="073fa-249">no</span></span>   |
       | <span data-ttu-id="073fa-250">no</span><span class="sxs-lookup"><span data-stu-id="073fa-250">no</span></span>  | <span data-ttu-id="073fa-251">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-251">yes</span></span> | <span data-ttu-id="073fa-252">no</span><span class="sxs-lookup"><span data-stu-id="073fa-252">no</span></span>  | <span data-ttu-id="073fa-253">no</span><span class="sxs-lookup"><span data-stu-id="073fa-253">no</span></span>  | <span data-ttu-id="073fa-254">no</span><span class="sxs-lookup"><span data-stu-id="073fa-254">no</span></span>   |
       | <span data-ttu-id="073fa-255">no</span><span class="sxs-lookup"><span data-stu-id="073fa-255">no</span></span>  | <span data-ttu-id="073fa-256">no</span><span class="sxs-lookup"><span data-stu-id="073fa-256">no</span></span>  | <span data-ttu-id="073fa-257">yes</span><span class="sxs-lookup"><span data-stu-id="073fa-257">yes</span></span> | <span data-ttu-id="073fa-258">no</span><span class="sxs-lookup"><span data-stu-id="073fa-258">no</span></span>  | <span data-ttu-id="073fa-259">no</span><span class="sxs-lookup"><span data-stu-id="073fa-259">no</span></span>   |
       | <span data-ttu-id="073fa-260">no</span><span class="sxs-lookup"><span data-stu-id="073fa-260">no</span></span>  | <span data-ttu-id="073fa-261">no</span><span class="sxs-lookup"><span data-stu-id="073fa-261">no</span></span>  | <span data-ttu-id="073fa-262">no</span><span class="sxs-lookup"><span data-stu-id="073fa-262">no</span></span>  | <span data-ttu-id="073fa-263">no</span><span class="sxs-lookup"><span data-stu-id="073fa-263">no</span></span>  | <span data-ttu-id="073fa-264">no</span><span class="sxs-lookup"><span data-stu-id="073fa-264">no</span></span>   |

    <span data-ttu-id="073fa-265">\*Can the user see the application in the access panel and the Office 365 app launcher?</span><span class="sxs-lookup"><span data-stu-id="073fa-265">\*Can the user see the application in the access panel and the Office 365 app launcher?</span></span>

## <a name="use-a-custom-logo"></a><span data-ttu-id="073fa-266">Use a custom logo</span><span class="sxs-lookup"><span data-stu-id="073fa-266">Use a custom logo</span></span>

<span data-ttu-id="073fa-267">To use a custom logo:</span><span class="sxs-lookup"><span data-stu-id="073fa-267">To use a custom logo:</span></span>

1. <span data-ttu-id="073fa-268">Create a logo that is 215 by 215 pixels, and save it in PNG format.</span><span class="sxs-lookup"><span data-stu-id="073fa-268">Create a logo that is 215 by 215 pixels, and save it in PNG format.</span></span>
2. <span data-ttu-id="073fa-269">Since you have already found your application, click on the application.</span><span class="sxs-lookup"><span data-stu-id="073fa-269">Since you have already found your application, click on the application.</span></span>
2. <span data-ttu-id="073fa-270">In the left blade, click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="073fa-270">In the left blade, click **Properties**.</span></span>
4. <span data-ttu-id="073fa-271">Upload the logo.</span><span class="sxs-lookup"><span data-stu-id="073fa-271">Upload the logo.</span></span>
5. <span data-ttu-id="073fa-272">When you're finished, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="073fa-272">When you're finished, click **Save**.</span></span>

    ![Change the logo](media/add-application-portal/change-logo.png)


## <a name="next-steps"></a><span data-ttu-id="073fa-274">Next steps</span><span class="sxs-lookup"><span data-stu-id="073fa-274">Next steps</span></span>

<span data-ttu-id="073fa-275">In this quickstart, you've learned how to add a gallery application to your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="073fa-275">In this quickstart, you've learned how to add a gallery application to your Azure AD tenant.</span></span> <span data-ttu-id="073fa-276">You also learned how to edit the properties for an application.</span><span class="sxs-lookup"><span data-stu-id="073fa-276">You also learned how to edit the properties for an application.</span></span> 

<span data-ttu-id="073fa-277">Now, you're ready to configure the application for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="073fa-277">Now, you're ready to configure the application for single sign-on.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="073fa-278">Configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="073fa-278">Configure single sign-on</span></span>](configure-single-sign-on-portal.md)


