---
title: Problems signing in to a gallery application configured for federated single sign-on | Microsoft Docs
description: Guidance for the specific errors when signing into an application you have configured for SAML-based federated single sign-on with Azure AD
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/11/2017
ms.author: barbkess
ms.reviewer: asteen
ms.openlocfilehash: 8d910ffcf966e98def33a42a6452baea9f4b3998
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858080"
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="afaa5-103">Problems signing in to a gallery application configured for federated single sign-on</span><span class="sxs-lookup"><span data-stu-id="afaa5-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="afaa5-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span><span class="sxs-lookup"><span data-stu-id="afaa5-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="afaa5-105">You have followed all the configuration steps for the Azure AD gallery application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="afaa5-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span><span class="sxs-lookup"><span data-stu-id="afaa5-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="afaa5-107">You have assigned users to the application</span><span class="sxs-lookup"><span data-stu-id="afaa5-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="afaa5-108">Application not found in directory</span><span class="sxs-lookup"><span data-stu-id="afaa5-108">Application not found in directory</span></span>

<span data-ttu-id="afaa5-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span><span class="sxs-lookup"><span data-stu-id="afaa5-109">*Error AADSTS70001: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="afaa5-110">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-110">**Possible cause**</span></span>

<span data-ttu-id="afaa5-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afaa5-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="afaa5-112">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="afaa5-112">**Resolution**</span></span>

<span data-ttu-id="afaa5-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="afaa5-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="afaa5-114">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-114">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afaa5-115">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-115">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-117">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-117">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-118">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afaa5-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-120">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="afaa5-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afaa5-121">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-121">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="afaa5-122">Go to **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="afaa5-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="afaa5-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span><span class="sxs-lookup"><span data-stu-id="afaa5-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="afaa5-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="the-reply-address-does-not-match-the-reply-addresses-configured-for-the-application"></a><span data-ttu-id="afaa5-125">The reply address does not match the reply addresses configured for the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-125">The reply address does not match the reply addresses configured for the application.</span></span>

<span data-ttu-id="afaa5-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span><span class="sxs-lookup"><span data-stu-id="afaa5-126">*Error AADSTS50011: The reply address ‘https://contoso.com’ does not match the reply addresses configured for the application*</span></span>

<span data-ttu-id="afaa5-127">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-127">**Possible cause**</span></span>

<span data-ttu-id="afaa5-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afaa5-128">The AssertionConsumerServiceURL value in the SAML request doesn't match the Reply URL value or pattern configured in Azure AD.</span></span> <span data-ttu-id="afaa5-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span><span class="sxs-lookup"><span data-stu-id="afaa5-129">The AssertionConsumerServiceURL value in the SAML request is the URL you see in the error.</span></span>

<span data-ttu-id="afaa5-130">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="afaa5-130">**Resolution**</span></span>

<span data-ttu-id="afaa5-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afaa5-131">Ensure that the AssertionConsumerServiceURL value in the SAML request it's matching the Reply URL value configured in Azure AD.</span></span>

1.  <span data-ttu-id="afaa5-132">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-132">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afaa5-133">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-133">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-134">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-135">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-135">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-136">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-136">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afaa5-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-137">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-138">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="afaa5-138">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afaa5-139">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-139">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="afaa5-140">Go to **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="afaa5-140">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="afaa5-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span><span class="sxs-lookup"><span data-stu-id="afaa5-141">Verify or update the value in the Reply URL textbox to match the AssertionConsumerServiceURL value in the SAML request.</span></span>  
    * <span data-ttu-id="afaa5-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span><span class="sxs-lookup"><span data-stu-id="afaa5-142">If you don't see the Reply URL textbox, select the **Show advanced URL settings** checkbox.</span></span>

<span data-ttu-id="afaa5-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-143">After you have updated the Reply URL value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="afaa5-144">User not assigned a role</span><span class="sxs-lookup"><span data-stu-id="afaa5-144">User not assigned a role</span></span>

<span data-ttu-id="afaa5-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span><span class="sxs-lookup"><span data-stu-id="afaa5-145">*Error AADSTS50105: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="afaa5-146">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-146">**Possible cause**</span></span>

<span data-ttu-id="afaa5-147">The user has not been granted access to the application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="afaa5-147">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="afaa5-148">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="afaa5-148">**Resolution**</span></span>

<span data-ttu-id="afaa5-149">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="afaa5-149">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="afaa5-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="afaa5-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-154">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afaa5-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-156">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="afaa5-156">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="afaa5-157">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-157">Once the application loads, click **Users and Groups** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="afaa5-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="afaa5-158">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** pane.</span></span>

9.  <span data-ttu-id="afaa5-159">click the **Users and groups** selector from the **Add Assignment** pane.</span><span class="sxs-lookup"><span data-stu-id="afaa5-159">click the **Users and groups** selector from the **Add Assignment** pane.</span></span>

10. <span data-ttu-id="afaa5-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="afaa5-160">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="afaa5-161">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="afaa5-161">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="afaa5-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="afaa5-162">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="afaa5-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="afaa5-163">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="afaa5-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-164">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="afaa5-165">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="afaa5-165">**Optional:** click the **Select Role** selector in the **Add Assignment** pane to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="afaa5-166">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="afaa5-166">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="afaa5-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="afaa5-167">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="afaa5-168">Not a valid SAML Request</span><span class="sxs-lookup"><span data-stu-id="afaa5-168">Not a valid SAML Request</span></span>

<span data-ttu-id="afaa5-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span><span class="sxs-lookup"><span data-stu-id="afaa5-169">*Error AADSTS75005: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="afaa5-170">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-170">**Possible cause**</span></span>

<span data-ttu-id="afaa5-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="afaa5-171">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="afaa5-172">Some common issues are:</span><span class="sxs-lookup"><span data-stu-id="afaa5-172">Some common issues are:</span></span>

-   <span data-ttu-id="afaa5-173">Missing required fields in the SAML request</span><span class="sxs-lookup"><span data-stu-id="afaa5-173">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="afaa5-174">SAML request encoded method</span><span class="sxs-lookup"><span data-stu-id="afaa5-174">SAML request encoded method</span></span>

<span data-ttu-id="afaa5-175">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="afaa5-175">**Resolution**</span></span>

1.  <span data-ttu-id="afaa5-176">Capture SAML request.</span><span class="sxs-lookup"><span data-stu-id="afaa5-176">Capture SAML request.</span></span> <span data-ttu-id="afaa5-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span><span class="sxs-lookup"><span data-stu-id="afaa5-177">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="afaa5-178">Contact the application vendor and share:</span><span class="sxs-lookup"><span data-stu-id="afaa5-178">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="afaa5-179">SAML request</span><span class="sxs-lookup"><span data-stu-id="afaa5-179">SAML request</span></span>

   -   [<span data-ttu-id="afaa5-180">Azure AD Single Sign-on SAML protocol requirements</span><span class="sxs-lookup"><span data-stu-id="afaa5-180">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="afaa5-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="afaa5-181">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="afaa5-182">No resource in requiredResourceAccess list</span><span class="sxs-lookup"><span data-stu-id="afaa5-182">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="afaa5-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span><span class="sxs-lookup"><span data-stu-id="afaa5-183">*Error AADSTS65005:The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="afaa5-184">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-184">**Possible cause**</span></span>

<span data-ttu-id="afaa5-185">The application object is corrupted.</span><span class="sxs-lookup"><span data-stu-id="afaa5-185">The application object is corrupted.</span></span>

<span data-ttu-id="afaa5-186">**Resolution: option 1**</span><span class="sxs-lookup"><span data-stu-id="afaa5-186">**Resolution: option 1**</span></span>

<span data-ttu-id="afaa5-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span><span class="sxs-lookup"><span data-stu-id="afaa5-187">To solve the problem, add the unique Identifier value in the Azure AD configuration.</span></span> <span data-ttu-id="afaa5-188">To add a Identifier value, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="afaa5-188">To add a Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="afaa5-189">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-189">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afaa5-190">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-190">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-191">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-192">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-192">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-193">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-193">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afaa5-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-194">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-195">Select the application you have configured single sign-on.</span><span class="sxs-lookup"><span data-stu-id="afaa5-195">Select the application you have configured single sign-on.</span></span>

7.  <span data-ttu-id="afaa5-196">Once the application loads, click on the **Single sign-on** from the application’s left-hand navigation menu</span><span class="sxs-lookup"><span data-stu-id="afaa5-196">Once the application loads, click on the **Single sign-on** from the application’s left-hand navigation menu</span></span>

8.  <span data-ttu-id="afaa5-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span><span class="sxs-lookup"><span data-stu-id="afaa5-197">Under the **Domain and URL** section, check on the **Show advanced URL settings**.</span></span>

9.  <span data-ttu-id="afaa5-198">in the **Identifier** textbox type a unique identifier for the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-198">in the **Identifier** textbox type a unique identifier for the application.</span></span>

10. <span data-ttu-id="afaa5-199">**Save** the configuration.</span><span class="sxs-lookup"><span data-stu-id="afaa5-199">**Save** the configuration.</span></span>


<span data-ttu-id="afaa5-200">**Resolution option 2**</span><span class="sxs-lookup"><span data-stu-id="afaa5-200">**Resolution option 2**</span></span>

<span data-ttu-id="afaa5-201">If option 1 above did not work for you, try removing the application from the directory.</span><span class="sxs-lookup"><span data-stu-id="afaa5-201">If option 1 above did not work for you, try removing the application from the directory.</span></span> <span data-ttu-id="afaa5-202">Then, add and reconfigure the application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="afaa5-202">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="afaa5-203">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-203">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afaa5-204">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-204">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-205">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-206">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-206">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-207">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-207">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="afaa5-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-208">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-209">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="afaa5-209">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afaa5-210">Click **Delete** at the top-left of the application **Overview** pane.</span><span class="sxs-lookup"><span data-stu-id="afaa5-210">Click **Delete** at the top-left of the application **Overview** pane.</span></span>

8.  <span data-ttu-id="afaa5-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span><span class="sxs-lookup"><span data-stu-id="afaa5-211">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="afaa5-212">Then, Configure the application</span><span class="sxs-lookup"><span data-stu-id="afaa5-212">Then, Configure the application</span></span>

<span data-ttu-id="afaa5-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-213"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="afaa5-214">Certificate or key not configured</span><span class="sxs-lookup"><span data-stu-id="afaa5-214">Certificate or key not configured</span></span>

<span data-ttu-id="afaa5-215">*Error AADSTS50003: No signing key configured.*</span><span class="sxs-lookup"><span data-stu-id="afaa5-215">*Error AADSTS50003: No signing key configured.*</span></span>

<span data-ttu-id="afaa5-216">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="afaa5-216">**Possible cause**</span></span>

<span data-ttu-id="afaa5-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span><span class="sxs-lookup"><span data-stu-id="afaa5-217">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="afaa5-218">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="afaa5-218">**Resolution**</span></span>

<span data-ttu-id="afaa5-219">To delete and create a new certificate, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="afaa5-219">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="afaa5-220">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-220">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="afaa5-221">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-221">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="afaa5-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="afaa5-222">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="afaa5-223">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-223">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="afaa5-224">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="afaa5-224">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="afaa5-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-225">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="afaa5-226">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="afaa5-226">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="afaa5-227">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="afaa5-227">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="afaa5-228">click **Create new certificate** under the **SAML signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="afaa5-228">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="afaa5-229">Select Expiration date.</span><span class="sxs-lookup"><span data-stu-id="afaa5-229">Select Expiration date.</span></span> <span data-ttu-id="afaa5-230">Then, click **Save.**</span><span class="sxs-lookup"><span data-stu-id="afaa5-230">Then, click **Save.**</span></span>

10. <span data-ttu-id="afaa5-231">Check **Make new certificate active** to override the active certificate.</span><span class="sxs-lookup"><span data-stu-id="afaa5-231">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="afaa5-232">Then, click **Save** at the top of the pane and accept to activate the rollover certificate.</span><span class="sxs-lookup"><span data-stu-id="afaa5-232">Then, click **Save** at the top of the pane and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="afaa5-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span><span class="sxs-lookup"><span data-stu-id="afaa5-233">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="problem-when-customizing-the-saml-claims-sent-to-an-application"></a><span data-ttu-id="afaa5-234">Problem when customizing the SAML claims sent to an application</span><span class="sxs-lookup"><span data-stu-id="afaa5-234">Problem when customizing the SAML claims sent to an application</span></span>

<span data-ttu-id="afaa5-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span><span class="sxs-lookup"><span data-stu-id="afaa5-235">To learn how to customize the SAML attribute claims sent to your application, see [Claims mapping in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-claims-mapping) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afaa5-236">Next steps</span><span class="sxs-lookup"><span data-stu-id="afaa5-236">Next steps</span></span>
[<span data-ttu-id="afaa5-237">How to debug SAML-based single sign-on to applications in Azure AD</span><span class="sxs-lookup"><span data-stu-id="afaa5-237">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
