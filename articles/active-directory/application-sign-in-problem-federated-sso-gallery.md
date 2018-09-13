---
title: Problems signing in to a gallery application configured for federated single sign-on | Microsoft Docs
description: Guidance for the specific errors when signing into an application you have configured for SAML-based federated single sign-on with Azure AD
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
ms.openlocfilehash: 64f5480dd533d2b7581e1e7ab1e09dffee07e838
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553751"
---
# <a name="problems-signing-in-to-a-gallery-application-configured-for-federated-single-sign-on"></a><span data-ttu-id="9d201-103">Problems signing in to a gallery application configured for federated single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d201-103">Problems signing in to a gallery application configured for federated single sign-on</span></span>

<span data-ttu-id="9d201-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span><span class="sxs-lookup"><span data-stu-id="9d201-104">To troubleshoot your problem, you need to verify the application configuration in Azure AD as follow:</span></span>

-   <span data-ttu-id="9d201-105">You have followed all the configuration steps for the Azure AD gallery application.</span><span class="sxs-lookup"><span data-stu-id="9d201-105">You have followed all the configuration steps for the Azure AD gallery application.</span></span>

-   <span data-ttu-id="9d201-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span><span class="sxs-lookup"><span data-stu-id="9d201-106">The Identifier and Reply URL configured in AAD match they expected values in the application</span></span>

-   <span data-ttu-id="9d201-107">You have assigned users to the application</span><span class="sxs-lookup"><span data-stu-id="9d201-107">You have assigned users to the application</span></span>

## <a name="application-not-found-in-directory"></a><span data-ttu-id="9d201-108">Application not found in directory</span><span class="sxs-lookup"><span data-stu-id="9d201-108">Application not found in directory</span></span>

<span data-ttu-id="9d201-109">*Error: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span><span class="sxs-lookup"><span data-stu-id="9d201-109">*Error: Application with Identifier ‘https://contoso.com’ was not found in the directory*.</span></span>

<span data-ttu-id="9d201-110">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="9d201-110">**Possible cause**</span></span>

<span data-ttu-id="9d201-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d201-111">The Issuer attribute sends from the application to Azure AD in the SAML request doesn’t match the Identifier value configured in the application Azure AD.</span></span>

<span data-ttu-id="9d201-112">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="9d201-112">**Resolution**</span></span>

<span data-ttu-id="9d201-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span><span class="sxs-lookup"><span data-stu-id="9d201-113">Ensure that the Issuer attribute in the SAML request it’s matching the Identifier value configured in Azure AD:</span></span>

1.  <span data-ttu-id="9d201-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9d201-114">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9d201-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-115">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d201-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9d201-116">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d201-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-117">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9d201-118">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9d201-118">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9d201-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9d201-119">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9d201-120">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d201-120">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="9d201-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-121">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9d201-122">Go to **Domain and URLs** section.</span><span class="sxs-lookup"><span data-stu-id="9d201-122">Go to **Domain and URLs** section.</span></span> <span data-ttu-id="9d201-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span><span class="sxs-lookup"><span data-stu-id="9d201-123">Verify that the value in the Identifier textbox is matching the value for the identifier value displayed in the error.</span></span>

<span data-ttu-id="9d201-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="9d201-124">After you have updated the Identifier value in Azure AD and it’s matching the value sends by the application in the SAML request, you should be able to sign in to the application.</span></span>

## <a name="user-not-assigned-a-role"></a><span data-ttu-id="9d201-125">User not assigned a role</span><span class="sxs-lookup"><span data-stu-id="9d201-125">User not assigned a role</span></span>

<span data-ttu-id="9d201-126">*Error: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span><span class="sxs-lookup"><span data-stu-id="9d201-126">*Error: The signed in user 'brian@contoso.com' is not assigned to a role for the application*.</span></span>

<span data-ttu-id="9d201-127">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="9d201-127">**Possible cause**</span></span>

<span data-ttu-id="9d201-128">The user has not been granted access to the application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d201-128">The user has not been granted access to the application in Azure AD.</span></span>

<span data-ttu-id="9d201-129">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="9d201-129">**Resolution**</span></span>

<span data-ttu-id="9d201-130">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9d201-130">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="9d201-131">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="9d201-131">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="9d201-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-132">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d201-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9d201-133">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d201-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-134">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9d201-135">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9d201-135">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9d201-136">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9d201-136">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9d201-137">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="9d201-137">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="9d201-138">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-138">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9d201-139">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9d201-139">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="9d201-140">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="9d201-140">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="9d201-141">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="9d201-141">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="9d201-142">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="9d201-142">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="9d201-143">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9d201-143">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="9d201-144">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="9d201-144">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="9d201-145">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="9d201-145">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="9d201-146">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="9d201-146">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="9d201-147">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="9d201-147">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="9d201-148">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span><span class="sxs-lookup"><span data-stu-id="9d201-148">After a short period of time, the users you have selected be able to launch these applications using the methods described in the solution description section.</span></span>

## <a name="not-a-valid-saml-request"></a><span data-ttu-id="9d201-149">Not a valid SAML Request</span><span class="sxs-lookup"><span data-stu-id="9d201-149">Not a valid SAML Request</span></span>

<span data-ttu-id="9d201-150">*Error: The request is not a valid Saml2 protocol message.*</span><span class="sxs-lookup"><span data-stu-id="9d201-150">*Error: The request is not a valid Saml2 protocol message.*</span></span>

<span data-ttu-id="9d201-151">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="9d201-151">**Possible cause**</span></span>

<span data-ttu-id="9d201-152">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d201-152">Azure AD doesn’t support the SAML Request sent by the application for Single Sign-on.</span></span> <span data-ttu-id="9d201-153">Some common issues are:</span><span class="sxs-lookup"><span data-stu-id="9d201-153">Some common issues are:</span></span>

-   <span data-ttu-id="9d201-154">Missing required fields in the SAML request</span><span class="sxs-lookup"><span data-stu-id="9d201-154">Missing required fields in the SAML request</span></span>

-   <span data-ttu-id="9d201-155">SAML request encoded method</span><span class="sxs-lookup"><span data-stu-id="9d201-155">SAML request encoded method</span></span>

<span data-ttu-id="9d201-156">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="9d201-156">**Resolution**</span></span>

1.  <span data-ttu-id="9d201-157">Capture SAML request.</span><span class="sxs-lookup"><span data-stu-id="9d201-157">Capture SAML request.</span></span> <span data-ttu-id="9d201-158">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span><span class="sxs-lookup"><span data-stu-id="9d201-158">follow the tutorial [How to debug SAML-based single sign-on to applications in Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging) to learn how to capture the SAML request.</span></span>

2.  <span data-ttu-id="9d201-159">Contact the application vendor and share:</span><span class="sxs-lookup"><span data-stu-id="9d201-159">Contact the application vendor and share:</span></span>

   -   <span data-ttu-id="9d201-160">SAML request</span><span class="sxs-lookup"><span data-stu-id="9d201-160">SAML request</span></span>

   -   [<span data-ttu-id="9d201-161">Azure AD Single Sign-on SAML protocol requirements</span><span class="sxs-lookup"><span data-stu-id="9d201-161">Azure AD Single Sign-on SAML protocol requirements</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference)

<span data-ttu-id="9d201-162">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span><span class="sxs-lookup"><span data-stu-id="9d201-162">They should validate they support the Azure AD SAML implementation for Single Sign-on.</span></span>

## <a name="no-resource-in-requiredresourceaccess-list"></a><span data-ttu-id="9d201-163">No resource in requiredResourceAccess list</span><span class="sxs-lookup"><span data-stu-id="9d201-163">No resource in requiredResourceAccess list</span></span>

<span data-ttu-id="9d201-164">*Error: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span><span class="sxs-lookup"><span data-stu-id="9d201-164">*Error: The client application has requested access to resource '00000002-0000-0000-c000-000000000000'. This request has failed because the client has not specified this resource in its requiredResourceAccess list*.</span></span>

<span data-ttu-id="9d201-165">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="9d201-165">**Possible cause**</span></span>

<span data-ttu-id="9d201-166">The application object is corrupted.</span><span class="sxs-lookup"><span data-stu-id="9d201-166">The application object is corrupted.</span></span>

<span data-ttu-id="9d201-167">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="9d201-167">**Resolution**</span></span>

<span data-ttu-id="9d201-168">To solve the problem, remove the application from the directory.</span><span class="sxs-lookup"><span data-stu-id="9d201-168">To solve the problem, remove the application from the directory.</span></span> <span data-ttu-id="9d201-169">Then, add and reconfigure the application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9d201-169">Then, add and reconfigure the application, follow the steps below:</span></span>

1.  <span data-ttu-id="9d201-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9d201-170">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9d201-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-171">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d201-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9d201-172">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d201-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-173">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9d201-174">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9d201-174">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="9d201-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9d201-175">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9d201-176">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d201-176">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="9d201-177">Click **Delete** at the top-left of the application **Overview** blade.</span><span class="sxs-lookup"><span data-stu-id="9d201-177">Click **Delete** at the top-left of the application **Overview** blade.</span></span>

8.  <span data-ttu-id="9d201-178">Refresh Azure AD and Add the application from the Azure AD gallery.</span><span class="sxs-lookup"><span data-stu-id="9d201-178">Refresh Azure AD and Add the application from the Azure AD gallery.</span></span> <span data-ttu-id="9d201-179">Then, Configure the application</span><span class="sxs-lookup"><span data-stu-id="9d201-179">Then, Configure the application</span></span>

<span data-ttu-id="9d201-180"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span><span class="sxs-lookup"><span data-stu-id="9d201-180"><span id="_Hlk477190176" class="anchor"></span>After reconfiguring the application, you should be able to sign in to the application.</span></span>

## <a name="certificate-or-key-not-configured"></a><span data-ttu-id="9d201-181">Certificate or key not configured</span><span class="sxs-lookup"><span data-stu-id="9d201-181">Certificate or key not configured</span></span>

<span data-ttu-id="9d201-182">*Error: No signing key configured.*</span><span class="sxs-lookup"><span data-stu-id="9d201-182">*Error: No signing key configured.*</span></span>

<span data-ttu-id="9d201-183">**Possible cause**</span><span class="sxs-lookup"><span data-stu-id="9d201-183">**Possible cause**</span></span>

<span data-ttu-id="9d201-184">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span><span class="sxs-lookup"><span data-stu-id="9d201-184">The application object is corrupted and Azure AD doesn’t recognize the certificate configured for the application.</span></span>

<span data-ttu-id="9d201-185">**Resolution**</span><span class="sxs-lookup"><span data-stu-id="9d201-185">**Resolution**</span></span>

<span data-ttu-id="9d201-186">To delete and create a new certificate, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="9d201-186">To delete and create a new certificate, follow the steps below:</span></span>

1.  <span data-ttu-id="9d201-187">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="9d201-187">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="9d201-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="9d201-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="9d201-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="9d201-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="9d201-191">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="9d201-191">click **All Applications** to view a list of all your applications.</span></span>

 * <span data-ttu-id="9d201-192">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="9d201-192">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="9d201-193">Select the application you want to configure single sign-on</span><span class="sxs-lookup"><span data-stu-id="9d201-193">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="9d201-194">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="9d201-194">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="9d201-195">click **Create new certificate** under the **SAML signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="9d201-195">click **Create new certificate** under the **SAML signing Certificate** section.</span></span>

9.  <span data-ttu-id="9d201-196">Select Expiration date.</span><span class="sxs-lookup"><span data-stu-id="9d201-196">Select Expiration date.</span></span> <span data-ttu-id="9d201-197">Then, click **Save.**</span><span class="sxs-lookup"><span data-stu-id="9d201-197">Then, click **Save.**</span></span>

10. <span data-ttu-id="9d201-198">Check **Make new certificate active** to override the active certificate.</span><span class="sxs-lookup"><span data-stu-id="9d201-198">Check **Make new certificate active** to override the active certificate.</span></span> <span data-ttu-id="9d201-199">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span><span class="sxs-lookup"><span data-stu-id="9d201-199">Then, click **Save** at the top of the blade and accept to activate the rollover certificate.</span></span>

11. <span data-ttu-id="9d201-200">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span><span class="sxs-lookup"><span data-stu-id="9d201-200">Under the **SAML Signing Certificate** section, click **remove** to remove the **Unused** certificate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d201-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d201-201">Next steps</span></span>
[<span data-ttu-id="9d201-202">How to debug SAML-based single sign-on to applications in Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d201-202">How to debug SAML-based single sign-on to applications in Azure AD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-debugging)
