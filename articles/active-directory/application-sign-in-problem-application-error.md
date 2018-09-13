---
title: Error on an application's page after signing in | Microsoft Docs
description: How to resolve issues with Azure AD sign in when the application itself emits an error
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
ms.openlocfilehash: b92c86a82205d9840168a606abc66420f0208a1e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669383"
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="7ae39-103">Error on an application's page after signing in</span><span class="sxs-lookup"><span data-stu-id="7ae39-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="7ae39-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span><span class="sxs-lookup"><span data-stu-id="7ae39-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign in flow.</span></span> <span data-ttu-id="7ae39-105">In this scenario, the application is not accepting the response issue by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ae39-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="7ae39-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7ae39-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="7ae39-107">If the error in the application is not clear enough to know what is missing in the response, then:</span><span class="sxs-lookup"><span data-stu-id="7ae39-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="7ae39-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="7ae39-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="7ae39-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span><span class="sxs-lookup"><span data-stu-id="7ae39-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="7ae39-110">Share the SAML response with the application vendor to know what is missing.</span><span class="sxs-lookup"><span data-stu-id="7ae39-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="7ae39-111">Missing attributes in the SAML response</span><span class="sxs-lookup"><span data-stu-id="7ae39-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="7ae39-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="7ae39-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow the steps below:</span></span>

1.  <span data-ttu-id="7ae39-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-113">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7ae39-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-114">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ae39-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7ae39-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ae39-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-116">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ae39-117">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="7ae39-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7ae39-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ae39-119">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ae39-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7ae39-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-120">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ae39-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span><span class="sxs-lookup"><span data-stu-id="7ae39-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when user sign in.</span></span>

   <span data-ttu-id="7ae39-122">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="7ae39-122">To add an attribute:</span></span>

   * <span data-ttu-id="7ae39-123">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="7ae39-123">click **Add attribute**.</span></span> <span data-ttu-id="7ae39-124">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="7ae39-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="7ae39-125">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-125">Click **Save.**</span></span> <span data-ttu-id="7ae39-126">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="7ae39-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="7ae39-127">Save the configuration.</span><span class="sxs-lookup"><span data-stu-id="7ae39-127">Save the configuration.</span></span>

<span data-ttu-id="7ae39-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span><span class="sxs-lookup"><span data-stu-id="7ae39-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="7ae39-129">The application expects a different User Identifier value or format</span><span class="sxs-lookup"><span data-stu-id="7ae39-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="7ae39-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span><span class="sxs-lookup"><span data-stu-id="7ae39-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="7ae39-131">Add an attribute in the Azure AD application configuration:</span><span class="sxs-lookup"><span data-stu-id="7ae39-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="7ae39-132">To change the User Identifier value, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="7ae39-132">To change the User Identifier value, follow the steps below:</span></span>

1.  <span data-ttu-id="7ae39-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-133">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7ae39-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-134">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ae39-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7ae39-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ae39-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-136">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ae39-137">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="7ae39-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7ae39-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ae39-139">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ae39-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7ae39-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-140">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ae39-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="7ae39-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="7ae39-142">Change EntityID (User Identifier) format</span><span class="sxs-lookup"><span data-stu-id="7ae39-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="7ae39-143">If the application expects another format for the EntityID attribute.</span><span class="sxs-lookup"><span data-stu-id="7ae39-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="7ae39-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span><span class="sxs-lookup"><span data-stu-id="7ae39-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="7ae39-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="7ae39-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="7ae39-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="7ae39-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="7ae39-147">The application expects a different signature method for the SAML response</span><span class="sxs-lookup"><span data-stu-id="7ae39-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="7ae39-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7ae39-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="7ae39-149">Follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="7ae39-149">Follow the steps below:</span></span>

1.  <span data-ttu-id="7ae39-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-150">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7ae39-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-151">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ae39-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7ae39-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ae39-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-153">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ae39-154">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="7ae39-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7ae39-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ae39-156">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ae39-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7ae39-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-157">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ae39-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="7ae39-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="7ae39-159">Select the appropriate **Signing Option** expected by the application:</span><span class="sxs-lookup"><span data-stu-id="7ae39-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="7ae39-160">Sign SAML response</span><span class="sxs-lookup"><span data-stu-id="7ae39-160">Sign SAML response</span></span>

  * <span data-ttu-id="7ae39-161">Sign SAML response and assertion</span><span class="sxs-lookup"><span data-stu-id="7ae39-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="7ae39-162">Sign SAML assertion</span><span class="sxs-lookup"><span data-stu-id="7ae39-162">Sign SAML assertion</span></span>

<span data-ttu-id="7ae39-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span><span class="sxs-lookup"><span data-stu-id="7ae39-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="7ae39-164">The application expects the signing algorithm to be SHA-1</span><span class="sxs-lookup"><span data-stu-id="7ae39-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="7ae39-165">By default, Azure AD signs the SAML token using the most security algorithm.</span><span class="sxs-lookup"><span data-stu-id="7ae39-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="7ae39-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span><span class="sxs-lookup"><span data-stu-id="7ae39-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="7ae39-167">To change the signing algorithm, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="7ae39-167">To change the signing algorithm, follow the steps below:</span></span>

1.  <span data-ttu-id="7ae39-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-168">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="7ae39-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-169">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7ae39-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="7ae39-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7ae39-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-171">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7ae39-172">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="7ae39-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="7ae39-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="7ae39-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7ae39-174">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="7ae39-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="7ae39-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="7ae39-175">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7ae39-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="7ae39-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="7ae39-177">Select SHA-1, in the **Signing Algorithm**.</span><span class="sxs-lookup"><span data-stu-id="7ae39-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="7ae39-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span><span class="sxs-lookup"><span data-stu-id="7ae39-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ae39-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ae39-179">Next steps</span></span>
[<span data-ttu-id="7ae39-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7ae39-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
