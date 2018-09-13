---
title: Error on an application's page after signing in | Microsoft Docs
description: How to resolve issues with Azure AD sign in when the application itself emits an error
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
ms.openlocfilehash: 4cce49509a452153815c845d9ab72a1b4a8a5b7f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867195"
---
# <a name="error-on-an-applications-page-after-signing-in"></a><span data-ttu-id="f0c77-103">Error on an application's page after signing in</span><span class="sxs-lookup"><span data-stu-id="f0c77-103">Error on an application's page after signing in</span></span>

<span data-ttu-id="f0c77-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign-in flow.</span><span class="sxs-lookup"><span data-stu-id="f0c77-104">In this scenario, Azure AD has signed the user in, but the application is displaying an error not allowing the user to successfully finish the sign-in flow.</span></span> <span data-ttu-id="f0c77-105">In this scenario, the application is not accepting the response issue by Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c77-105">In this scenario, the application is not accepting the response issue by Azure AD.</span></span>

<span data-ttu-id="f0c77-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0c77-106">There are some possible reasons why the application didn’t accept the response from Azure AD.</span></span> <span data-ttu-id="f0c77-107">If the error in the application is not clear enough to know what is missing in the response, then:</span><span class="sxs-lookup"><span data-stu-id="f0c77-107">If the error in the application is not clear enough to know what is missing in the response, then:</span></span>

-   <span data-ttu-id="f0c77-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span><span class="sxs-lookup"><span data-stu-id="f0c77-108">If the application is the Azure AD Gallery, verify you have followed all the steps in the article [How to debug SAML-based single sign-on to applications in Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging).</span></span>

-   <span data-ttu-id="f0c77-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span><span class="sxs-lookup"><span data-stu-id="f0c77-109">Use a tool like [Fiddler](http://www.telerik.com/fiddler) to capture SAML request, SAML response and SAML token.</span></span>

-   <span data-ttu-id="f0c77-110">Share the SAML response with the application vendor to know what is missing.</span><span class="sxs-lookup"><span data-stu-id="f0c77-110">Share the SAML response with the application vendor to know what is missing.</span></span>

## <a name="missing-attributes-in-the-saml-response"></a><span data-ttu-id="f0c77-111">Missing attributes in the SAML response</span><span class="sxs-lookup"><span data-stu-id="f0c77-111">Missing attributes in the SAML response</span></span>

<span data-ttu-id="f0c77-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f0c77-112">To add an attribute in the Azure AD configuration to be sent in the Azure AD response, follow these steps:</span></span>

1.  <span data-ttu-id="f0c77-113">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-113">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f0c77-114">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-114">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="f0c77-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f0c77-115">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f0c77-116">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-116">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="f0c77-117">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="f0c77-117">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="f0c77-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-118">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f0c77-119">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c77-119">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f0c77-120">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-120">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="f0c77-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when users sign in.</span><span class="sxs-lookup"><span data-stu-id="f0c77-121">click **View and edit all other user attributes under** the **User Attributes** section to edit the attributes to be sent to the application in the SAML token when users sign in.</span></span>

   <span data-ttu-id="f0c77-122">To add an attribute:</span><span class="sxs-lookup"><span data-stu-id="f0c77-122">To add an attribute:</span></span>

   * <span data-ttu-id="f0c77-123">click **Add attribute**.</span><span class="sxs-lookup"><span data-stu-id="f0c77-123">click **Add attribute**.</span></span> <span data-ttu-id="f0c77-124">Enter the **Name** and the select the **Value** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="f0c77-124">Enter the **Name** and the select the **Value** from the dropdown.</span></span>

   * <span data-ttu-id="f0c77-125">Click **Save.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-125">Click **Save.**</span></span> <span data-ttu-id="f0c77-126">You see the new attribute in the table.</span><span class="sxs-lookup"><span data-stu-id="f0c77-126">You see the new attribute in the table.</span></span>

9.  <span data-ttu-id="f0c77-127">Save the configuration.</span><span class="sxs-lookup"><span data-stu-id="f0c77-127">Save the configuration.</span></span>

<span data-ttu-id="f0c77-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span><span class="sxs-lookup"><span data-stu-id="f0c77-128">Next time the user signs in to the application, Azure AD send the new attribute in the SAML response.</span></span>

## <a name="the-application-expects-a-different-user-identifier-value-or-format"></a><span data-ttu-id="f0c77-129">The application expects a different User Identifier value or format</span><span class="sxs-lookup"><span data-stu-id="f0c77-129">The application expects a different User Identifier value or format</span></span>

<span data-ttu-id="f0c77-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span><span class="sxs-lookup"><span data-stu-id="f0c77-130">The sign-in to the application is failing because the SAML response is missing attributes such as roles or because the application is expecting a different format for the EntityID attribute.</span></span>

## <a name="add-an-attribute-in-the-azure-ad-application-configuration"></a><span data-ttu-id="f0c77-131">Add an attribute in the Azure AD application configuration:</span><span class="sxs-lookup"><span data-stu-id="f0c77-131">Add an attribute in the Azure AD application configuration:</span></span>

<span data-ttu-id="f0c77-132">To change the User Identifier value, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f0c77-132">To change the User Identifier value, follow these steps:</span></span>

1.  <span data-ttu-id="f0c77-133">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-133">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f0c77-134">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-134">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="f0c77-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f0c77-135">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f0c77-136">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-136">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="f0c77-137">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="f0c77-137">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="f0c77-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-138">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f0c77-139">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c77-139">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f0c77-140">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-140">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="f0c77-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span><span class="sxs-lookup"><span data-stu-id="f0c77-141">Under the **User attributes**, select the unique identifier for your users in the **User Identifier** dropdown.</span></span>

## <a name="change-entityid-user-identifier-format"></a><span data-ttu-id="f0c77-142">Change EntityID (User Identifier) format</span><span class="sxs-lookup"><span data-stu-id="f0c77-142">Change EntityID (User Identifier) format</span></span>

<span data-ttu-id="f0c77-143">If the application expects another format for the EntityID attribute.</span><span class="sxs-lookup"><span data-stu-id="f0c77-143">If the application expects another format for the EntityID attribute.</span></span> <span data-ttu-id="f0c77-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span><span class="sxs-lookup"><span data-stu-id="f0c77-144">Then, you won’t be able to select the EntityID (User Identifier) format that Azure AD sends to the application in the response after user authentication.</span></span>

<span data-ttu-id="f0c77-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span><span class="sxs-lookup"><span data-stu-id="f0c77-145">Azure AD select the format for the NameID attribute (User Identifier) based on the value selected or the format requested by the application in the SAML AuthRequest.</span></span> <span data-ttu-id="f0c77-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span><span class="sxs-lookup"><span data-stu-id="f0c77-146">For more information visit the article [Single Sign-On SAML protocol](https://docs.microsoft.com/azure/active-directory/develop/active-directory-single-sign-on-protocol-reference#authnrequest) under the section NameIDPolicy.</span></span>

## <a name="the-application-expects-a-different-signature-method-for-the-saml-response"></a><span data-ttu-id="f0c77-147">The application expects a different signature method for the SAML response</span><span class="sxs-lookup"><span data-stu-id="f0c77-147">The application expects a different signature method for the SAML response</span></span>

<span data-ttu-id="f0c77-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0c77-148">To change what parts of the SAML token are digitally signed by Azure Active Directory.</span></span> <span data-ttu-id="f0c77-149">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f0c77-149">Follow these steps:</span></span>

1.  <span data-ttu-id="f0c77-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-150">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f0c77-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-151">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="f0c77-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f0c77-152">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f0c77-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-153">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="f0c77-154">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="f0c77-154">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="f0c77-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-155">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f0c77-156">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c77-156">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f0c77-157">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-157">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="f0c77-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="f0c77-158">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="f0c77-159">Select the appropriate **Signing Option** expected by the application:</span><span class="sxs-lookup"><span data-stu-id="f0c77-159">Select the appropriate **Signing Option** expected by the application:</span></span>

  * <span data-ttu-id="f0c77-160">Sign SAML response</span><span class="sxs-lookup"><span data-stu-id="f0c77-160">Sign SAML response</span></span>

  * <span data-ttu-id="f0c77-161">Sign SAML response and assertion</span><span class="sxs-lookup"><span data-stu-id="f0c77-161">Sign SAML response and assertion</span></span>

  * <span data-ttu-id="f0c77-162">Sign SAML assertion</span><span class="sxs-lookup"><span data-stu-id="f0c77-162">Sign SAML assertion</span></span>

<span data-ttu-id="f0c77-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span><span class="sxs-lookup"><span data-stu-id="f0c77-163">Next time the user signs in to the application, Azure AD sign the part of the SAML response selected.</span></span>

## <a name="the-application-expects-the-signing-algorithm-to-be-sha-1"></a><span data-ttu-id="f0c77-164">The application expects the signing algorithm to be SHA-1</span><span class="sxs-lookup"><span data-stu-id="f0c77-164">The application expects the signing algorithm to be SHA-1</span></span>

<span data-ttu-id="f0c77-165">By default, Azure AD signs the SAML token using the most security algorithm.</span><span class="sxs-lookup"><span data-stu-id="f0c77-165">By default, Azure AD signs the SAML token using the most security algorithm.</span></span> <span data-ttu-id="f0c77-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span><span class="sxs-lookup"><span data-stu-id="f0c77-166">Changing the sign algorithm to SHA-1 is not recommended unless required by the application.</span></span>

<span data-ttu-id="f0c77-167">To change the signing algorithm, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f0c77-167">To change the signing algorithm, follow these steps:</span></span>

1.  <span data-ttu-id="f0c77-168">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-168">Open the [**Azure portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="f0c77-169">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-169">Open the **Azure Active Directory Extension** by clicking **All services** at the top of the main left-hand navigation menu.</span></span>

3.  <span data-ttu-id="f0c77-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="f0c77-170">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="f0c77-171">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-171">click **Enterprise Applications** from the Azure Active Directory left-hand navigation menu.</span></span>

5.  <span data-ttu-id="f0c77-172">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="f0c77-172">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="f0c77-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="f0c77-173">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="f0c77-174">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="f0c77-174">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="f0c77-175">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f0c77-175">Once the application loads, click the **Single sign-on** from the application’s left-hand navigation menu.</span></span>

8.  <span data-ttu-id="f0c77-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span><span class="sxs-lookup"><span data-stu-id="f0c77-176">click **Show advanced certificate signing settings** under the **SAML Signing Certificate** section.</span></span>

9.  <span data-ttu-id="f0c77-177">Select SHA-1, in the **Signing Algorithm**.</span><span class="sxs-lookup"><span data-stu-id="f0c77-177">Select SHA-1, in the **Signing Algorithm**.</span></span>

<span data-ttu-id="f0c77-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span><span class="sxs-lookup"><span data-stu-id="f0c77-178">Next time the user signs in to the application, Azure AD sign the SAML token using SHA-1 algorithm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c77-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0c77-179">Next steps</span></span>
[<span data-ttu-id="f0c77-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0c77-180">How to debug SAML-based single sign-on to applications in Azure Active Directory</span></span>](https://azure.microsoft.com/documentation/articles/active-directory-saml-debugging)
