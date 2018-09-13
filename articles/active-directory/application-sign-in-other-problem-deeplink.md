---
title: Problems signing in to an application using a deeplink | Microsoft Docs
description: How to troubleshoot issues accessing an application from a deeplink URL using Azure AD
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
ms.openlocfilehash: 346c53ae9b4ebe8a17d351142f13201689677ef3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672107"
---
# <a name="problems-signing-in-to-an-application-using-a-deeplink"></a><span data-ttu-id="a595b-103">Problems signing in to an application using a deeplink</span><span class="sxs-lookup"><span data-stu-id="a595b-103">Problems signing in to an application using a deeplink</span></span>

<span data-ttu-id="a595b-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span><span class="sxs-lookup"><span data-stu-id="a595b-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> 

<span data-ttu-id="a595b-105">These applications are configured on behalf of the user in the Azure AD portal.</span><span class="sxs-lookup"><span data-stu-id="a595b-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="a595b-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a595b-106">The application must be configured properly and assigned to the user or a group the user is a member of to see the application in the Access Panel.</span></span>

<span data-ttu-id="a595b-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span><span class="sxs-lookup"><span data-stu-id="a595b-107">Deep links or User access URLs are links your users may use to access their password-SSO applications directly from their browsers URL bars.</span></span> <span data-ttu-id="a595b-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span><span class="sxs-lookup"><span data-stu-id="a595b-108">By navigating to this link, users be automatically signed into the application without having to go to the Access Panel first.</span></span> <span data-ttu-id="a595b-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span><span class="sxs-lookup"><span data-stu-id="a595b-109">This is the same link that users use to access these applications from the Office 365 application launcher.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="a595b-110">General issues to check first</span><span class="sxs-lookup"><span data-stu-id="a595b-110">General issues to check first</span></span>

-   <span data-ttu-id="a595b-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a595b-111">Make sure your using a **browser** that meets the minimum requirements for the Access Panel.</span></span>

-   <span data-ttu-id="a595b-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span><span class="sxs-lookup"><span data-stu-id="a595b-112">Make sure the user’s browser has added the URL of the application to its **trusted sites**.</span></span>

-   <span data-ttu-id="a595b-113">Make sure to check the application is **configured** correctly.</span><span class="sxs-lookup"><span data-stu-id="a595b-113">Make sure to check the application is **configured** correctly.</span></span>

-   <span data-ttu-id="a595b-114">Make sure the user’s account is **enabled** for sign ins.</span><span class="sxs-lookup"><span data-stu-id="a595b-114">Make sure the user’s account is **enabled** for sign ins.</span></span>

-   <span data-ttu-id="a595b-115">Make sure the user’s account is **not locked out.**</span><span class="sxs-lookup"><span data-stu-id="a595b-115">Make sure the user’s account is **not locked out.**</span></span>

-   <span data-ttu-id="a595b-116">Make sure the user’s **password is not expired or forgotten.**</span><span class="sxs-lookup"><span data-stu-id="a595b-116">Make sure the user’s **password is not expired or forgotten.**</span></span>

-   <span data-ttu-id="a595b-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="a595b-117">Make sure **Multi-Factor Authentication** is not blocking user access.</span></span>

-   <span data-ttu-id="a595b-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span><span class="sxs-lookup"><span data-stu-id="a595b-118">Make sure a **Conditional Access policy** or **Identity Protection** policy is not blocking user access.</span></span>

-   <span data-ttu-id="a595b-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span><span class="sxs-lookup"><span data-stu-id="a595b-119">Make sure that a user’s **authentication contact info** is up to date to allow Multi-Factor Authentication or Conditional Access policies to be enforced.</span></span>

-   <span data-ttu-id="a595b-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span><span class="sxs-lookup"><span data-stu-id="a595b-120">Make sure to also try clearing your browser’s cookies and trying to sign in again.</span></span>

## <a name="checking-the-deeplink"></a><span data-ttu-id="a595b-121">Checking the deeplink</span><span class="sxs-lookup"><span data-stu-id="a595b-121">Checking the deeplink</span></span>

<span data-ttu-id="a595b-122">To check if you have the correct deeplink, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-122">To check if you have the correct deeplink, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a595b-123">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a595b-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-124">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-125">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-126">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-127">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a595b-127">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a595b-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a595b-128">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a595b-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a595b-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

7.  <span data-ttu-id="a595b-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

8.  <span data-ttu-id="a595b-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

9.  <span data-ttu-id="a595b-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-132">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

10. <span data-ttu-id="a595b-133">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a595b-133">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="a595b-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a595b-134">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

11. <span data-ttu-id="a595b-135">Select the application you want the check the deeplink for.</span><span class="sxs-lookup"><span data-stu-id="a595b-135">Select the application you want the check the deeplink for.</span></span>

12. <span data-ttu-id="a595b-136">Find the label **User Access URL**.</span><span class="sxs-lookup"><span data-stu-id="a595b-136">Find the label **User Access URL**.</span></span> <span data-ttu-id="a595b-137">You deeplink should match this URL.</span><span class="sxs-lookup"><span data-stu-id="a595b-137">You deeplink should match this URL.</span></span>

## <a name="how-to-install-the-access-panel-browser-extension"></a><span data-ttu-id="a595b-138">How to install the Access Panel Browser extension</span><span class="sxs-lookup"><span data-stu-id="a595b-138">How to install the Access Panel Browser extension</span></span>

<span data-ttu-id="a595b-139">To install the Access Panel Browser extension, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-139">To install the Access Panel Browser extension, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a595b-140">Open the [Access Panel](https://myapps.microsoft.com) in one of the supported browsers and sign in as a **user** in your Azure AD.</span></span>

2.  <span data-ttu-id="a595b-141">click a **password-SSO application** in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a595b-141">click a **password-SSO application** in the Access Panel.</span></span>

3.  <span data-ttu-id="a595b-142">In the prompt asking to install the software, select **Install Now**.</span><span class="sxs-lookup"><span data-stu-id="a595b-142">In the prompt asking to install the software, select **Install Now**.</span></span>

4.  <span data-ttu-id="a595b-143">Based on your browser you be directed to the download link.</span><span class="sxs-lookup"><span data-stu-id="a595b-143">Based on your browser you be directed to the download link.</span></span> <span data-ttu-id="a595b-144">**Add** the extension to your browser.</span><span class="sxs-lookup"><span data-stu-id="a595b-144">**Add** the extension to your browser.</span></span>

5.  <span data-ttu-id="a595b-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span><span class="sxs-lookup"><span data-stu-id="a595b-145">If your browser asks, select to either **Enable** or **Allow** the extension.</span></span>

6.  <span data-ttu-id="a595b-146">Once installed, **restart** your browser session.</span><span class="sxs-lookup"><span data-stu-id="a595b-146">Once installed, **restart** your browser session.</span></span>

7.  <span data-ttu-id="a595b-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span><span class="sxs-lookup"><span data-stu-id="a595b-147">Sign in into the Access Panel and see if you can **launch** your password-SSO applications</span></span>

<span data-ttu-id="a595b-148">You may also download the extension for Chrome and Firefox from the direct links below:</span><span class="sxs-lookup"><span data-stu-id="a595b-148">You may also download the extension for Chrome and Firefox from the direct links below:</span></span>

-   [<span data-ttu-id="a595b-149">Chrome Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="a595b-149">Chrome Access Panel Extension</span></span>](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [<span data-ttu-id="a595b-150">Firefox Access Panel Extension</span><span class="sxs-lookup"><span data-stu-id="a595b-150">Firefox Access Panel Extension</span></span>](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-to-configure-password-single-sign-on-for-an-azure-ad-gallery-application"></a><span data-ttu-id="a595b-151">How to configure password single sign-on for an Azure AD gallery application</span><span class="sxs-lookup"><span data-stu-id="a595b-151">How to configure password single sign-on for an Azure AD gallery application</span></span>

<span data-ttu-id="a595b-152">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="a595b-152">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a595b-153">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="a595b-153">Add an application from the Azure AD gallery</span></span>](#add-an-application-from-the-Azure-AD-gallery)

-   [<span data-ttu-id="a595b-154">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a595b-154">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-the-azure-ad-gallery"></a><span data-ttu-id="a595b-155">Add an application from the Azure AD gallery</span><span class="sxs-lookup"><span data-stu-id="a595b-155">Add an application from the Azure AD gallery</span></span>

<span data-ttu-id="a595b-156">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-156">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="a595b-157">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="a595b-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-158">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-159">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-160">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-161">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a595b-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span><span class="sxs-lookup"><span data-stu-id="a595b-162">In the **Enter a name** textbox from the **Add from the gallery** section, type the name of the application.</span></span>

7.  <span data-ttu-id="a595b-163">Select the application you want to configure for single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a595b-163">Select the application you want to configure for single sign-on.</span></span>

8.  <span data-ttu-id="a595b-164">Before adding the application, you can change its name from the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="a595b-164">Before adding the application, you can change its name from the **Name** textbox.</span></span>

9.  <span data-ttu-id="a595b-165">Click **Add** button, to add the application.</span><span class="sxs-lookup"><span data-stu-id="a595b-165">Click **Add** button, to add the application.</span></span>

<span data-ttu-id="a595b-166">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-166">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="a595b-167">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a595b-167">Configure the application for password single sign-on</span></span>

<span data-ttu-id="a595b-168">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-168">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a595b-169">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a595b-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-170">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-171">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-172">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-173">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a595b-173">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a595b-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a595b-174">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a595b-175">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a595b-175">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a595b-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-176">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a595b-177">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="a595b-177">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a595b-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span><span class="sxs-lookup"><span data-stu-id="a595b-178">[Assign users to the application](#how-to-assign-a-user-to-an-application-directly).</span></span>

10. <span data-ttu-id="a595b-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="a595b-179">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="a595b-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="a595b-180">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-configure-password-single-sign-on-for-a-non-gallery-application"></a><span data-ttu-id="a595b-181">How to configure password single sign-on for a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="a595b-181">How to configure password single sign-on for a non-gallery application</span></span>

<span data-ttu-id="a595b-182">To configure an application from the Azure AD gallery you need to:</span><span class="sxs-lookup"><span data-stu-id="a595b-182">To configure an application from the Azure AD gallery you need to:</span></span>

-   [<span data-ttu-id="a595b-183">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="a595b-183">Add a non-gallery application</span></span>](#add-a-non-gallery-application)

-   [<span data-ttu-id="a595b-184">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a595b-184">Configure the application for password single sign-on</span></span>](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a><span data-ttu-id="a595b-185">Add a non-gallery application</span><span class="sxs-lookup"><span data-stu-id="a595b-185">Add a non-gallery application</span></span>

<span data-ttu-id="a595b-186">To add an application from the Azure AD Gallery, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-186">To add an application from the Azure AD Gallery, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span><span class="sxs-lookup"><span data-stu-id="a595b-187">Open the [Azure Portal](https://portal.azure.com) and sign in as a **Global Administrator** or **Co-admin**.</span></span>

2.  <span data-ttu-id="a595b-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-188">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-189">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-190">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-191">click the **Add** button at the top-right corner on the **Enterprise Applications** blade.</span></span>

6.  <span data-ttu-id="a595b-192">click **Non-gallery application.**</span><span class="sxs-lookup"><span data-stu-id="a595b-192">click **Non-gallery application.**</span></span>

7.  <span data-ttu-id="a595b-193">Enter the name of your application in the **Name** textbox.</span><span class="sxs-lookup"><span data-stu-id="a595b-193">Enter the name of your application in the **Name** textbox.</span></span> <span data-ttu-id="a595b-194">Select **Add.**</span><span class="sxs-lookup"><span data-stu-id="a595b-194">Select **Add.**</span></span>

<span data-ttu-id="a595b-195">After a short period, you be able to see the application’s configuration blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-195">After a short period, you be able to see the application’s configuration blade.</span></span>

### <a name="configure-the-application-for-password-single-sign-on"></a><span data-ttu-id="a595b-196">Configure the application for password single sign-on</span><span class="sxs-lookup"><span data-stu-id="a595b-196">Configure the application for password single sign-on</span></span>

<span data-ttu-id="a595b-197">To configure single sign-on for an application, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-197">To configure single sign-on for an application, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span><span class="sxs-lookup"><span data-stu-id="a595b-198">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="a595b-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-199">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-200">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-201">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-202">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a595b-202">click **All Applications** to view a list of all your applications.</span></span>

    1.  <span data-ttu-id="a595b-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a595b-203">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a595b-204">Select the application you want to configure single sign-on.</span><span class="sxs-lookup"><span data-stu-id="a595b-204">Select the application you want to configure single sign-on.</span></span>

7.  <span data-ttu-id="a595b-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-205">Once the application loads, click the **Single sign-on** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a595b-206">Select the mode **Password-based Sign-on.**</span><span class="sxs-lookup"><span data-stu-id="a595b-206">Select the mode **Password-based Sign-on.**</span></span>

9.  <span data-ttu-id="a595b-207">Enter the **Sign-on URL**.</span><span class="sxs-lookup"><span data-stu-id="a595b-207">Enter the **Sign-on URL**.</span></span> <span data-ttu-id="a595b-208">This is the URL where users enter their username and password to sign in to.</span><span class="sxs-lookup"><span data-stu-id="a595b-208">This is the URL where users enter their username and password to sign in to.</span></span> <span data-ttu-id="a595b-209">Ensure the sign in fields are visible at the URL.</span><span class="sxs-lookup"><span data-stu-id="a595b-209">Ensure the sign in fields are visible at the URL.</span></span>

10. <span data-ttu-id="a595b-210">Assign users to the application.</span><span class="sxs-lookup"><span data-stu-id="a595b-210">Assign users to the application.</span></span>

11. <span data-ttu-id="a595b-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span><span class="sxs-lookup"><span data-stu-id="a595b-211">Additionally, you can also provide credentials on behalf of the user by selecting the rows of the users and clicking on **Update Credentials** and entering the username and password on behalf of the users.</span></span> <span data-ttu-id="a595b-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span><span class="sxs-lookup"><span data-stu-id="a595b-212">Otherwise, users be prompted to enter the credentials themselves upon launch.</span></span>

## <a name="how-to-assign-a-user-to-an-application-directly"></a><span data-ttu-id="a595b-213">How to assign a user to an application directly</span><span class="sxs-lookup"><span data-stu-id="a595b-213">How to assign a user to an application directly</span></span>

<span data-ttu-id="a595b-214">To assign one or more users to an application directly, follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="a595b-214">To assign one or more users to an application directly, follow the steps below:</span></span>

1.  <span data-ttu-id="a595b-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span><span class="sxs-lookup"><span data-stu-id="a595b-215">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a595b-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-216">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a595b-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span><span class="sxs-lookup"><span data-stu-id="a595b-217">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a595b-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-218">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a595b-219">click **All Applications** to view a list of all your applications.</span><span class="sxs-lookup"><span data-stu-id="a595b-219">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="a595b-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span><span class="sxs-lookup"><span data-stu-id="a595b-220">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="a595b-221">Select the application you want to assign a user to from the list.</span><span class="sxs-lookup"><span data-stu-id="a595b-221">Select the application you want to assign a user to from the list.</span></span>

7.  <span data-ttu-id="a595b-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a595b-222">Once the application loads, click **Users and Groups** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a595b-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-223">Click the **Add** button on top of the **Users and Groups** list to open the **Add Assignment** blade.</span></span>

9.  <span data-ttu-id="a595b-224">click the **Users and groups** selector from the **Add Assignment** blade.</span><span class="sxs-lookup"><span data-stu-id="a595b-224">click the **Users and groups** selector from the **Add Assignment** blade.</span></span>

10. <span data-ttu-id="a595b-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span><span class="sxs-lookup"><span data-stu-id="a595b-225">Type in the **full name** or **email address** of the user you are interested in assigning into the **Search by name or email address** search box.</span></span>

11. <span data-ttu-id="a595b-226">Hover over the **user** in the list to reveal a **checkbox**.</span><span class="sxs-lookup"><span data-stu-id="a595b-226">Hover over the **user** in the list to reveal a **checkbox**.</span></span> <span data-ttu-id="a595b-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="a595b-227">Click the checkbox next to the user’s profile photo or logo to add your user to the **Selected** list.</span></span>

12. <span data-ttu-id="a595b-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span><span class="sxs-lookup"><span data-stu-id="a595b-228">**Optional:** If you would like to **add more than one user**, type in another **full name** or **email address** into the **Search by name or email address** search box, and click the checkbox to add this user to the **Selected** list.</span></span>

13. <span data-ttu-id="a595b-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span><span class="sxs-lookup"><span data-stu-id="a595b-229">When you are finished selecting users, click the **Select** button to add them to the list of users and groups to be assigned to the application.</span></span>

14. <span data-ttu-id="a595b-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span><span class="sxs-lookup"><span data-stu-id="a595b-230">**Optional:** click the **Select Role** selector in the **Add Assignment** blade to select a role to assign to the users you have selected.</span></span>

15. <span data-ttu-id="a595b-231">Click the **Assign** button to assign the application to the selected users.</span><span class="sxs-lookup"><span data-stu-id="a595b-231">Click the **Assign** button to assign the application to the selected users.</span></span>

<span data-ttu-id="a595b-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span><span class="sxs-lookup"><span data-stu-id="a595b-232">After a short period, the users you have selected be able to launch these applications in the Access Panel.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="a595b-233">If these troubleshooting steps do not the resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="a595b-233">If these troubleshooting steps do not the resolve the issue.</span></span> 

<span data-ttu-id="a595b-234">open a support ticket with the following information if available:</span><span class="sxs-lookup"><span data-stu-id="a595b-234">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="a595b-235">Correlation error ID</span><span class="sxs-lookup"><span data-stu-id="a595b-235">Correlation error ID</span></span>

-   <span data-ttu-id="a595b-236">UPN (user email address)</span><span class="sxs-lookup"><span data-stu-id="a595b-236">UPN (user email address)</span></span>

-   <span data-ttu-id="a595b-237">TenantID</span><span class="sxs-lookup"><span data-stu-id="a595b-237">TenantID</span></span>

-   <span data-ttu-id="a595b-238">Browser type</span><span class="sxs-lookup"><span data-stu-id="a595b-238">Browser type</span></span>

-   <span data-ttu-id="a595b-239">Time zone and time/timeframe during error occurs</span><span class="sxs-lookup"><span data-stu-id="a595b-239">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a595b-240">Fiddler traces</span><span class="sxs-lookup"><span data-stu-id="a595b-240">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a595b-241">Next steps</span><span class="sxs-lookup"><span data-stu-id="a595b-241">Next steps</span></span>
[<span data-ttu-id="a595b-242">Provide single sign-on to your apps with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="a595b-242">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
